---
title: "didacticiel aaaQuickstart langage R pour l’apprentissage | Documents Microsoft"
description: "Utiliser ce didacticiel tooget démarré rapidement à l’aide d’un langage de hello R avec Azure Machine Learning Studio toocreate une solution de prévision de programmation de R."
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
ms.openlocfilehash: 9995f8728f4d7bf9a5c15412015e4cf769cdac96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-tutorial-for-hello-r-programming-language-for-azure-machine-learning"></a><span data-ttu-id="4ad27-104">Didacticiel de démarrage rapide pour le langage de programmation hello R pour Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="4ad27-104">Quickstart tutorial for hello R programming language for Azure Machine Learning</span></span>

<!-- Stephen F Elston, Ph.D. -->

## <a name="introduction"></a><span data-ttu-id="4ad27-105">Introduction</span><span class="sxs-lookup"><span data-stu-id="4ad27-105">Introduction</span></span>
<span data-ttu-id="4ad27-106">Ce didacticiel de démarrage rapide vous permet de commencer rapidement l’extension Azure Machine Learning à l’aide du langage de programmation hello R.</span><span class="sxs-lookup"><span data-stu-id="4ad27-106">This quickstart tutorial helps you quickly start extending Azure Machine Learning by using hello R programming language.</span></span> <span data-ttu-id="4ad27-107">Suivez ce didacticiel toocreate de programmation de R, tester et exécuter le code R dans Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="4ad27-107">Follow this R programming tutorial toocreate, test and execute R code within Azure Machine Learning.</span></span> <span data-ttu-id="4ad27-108">Lorsque vous travaillez dans le didacticiel, vous allez créer une solution complète de prévision à l’aide du langage de hello R dans Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="4ad27-108">As you work through tutorial, you will create a complete forecasting solution by using hello R language in Azure Machine Learning.</span></span>  

<span data-ttu-id="4ad27-109">Si Microsoft Azure Machine Learning intègre divers modules d’apprentissage automatique et de manipulation de données très efficaces,</span><span class="sxs-lookup"><span data-stu-id="4ad27-109">Microsoft Azure Machine Learning contains many powerful machine learning and data manipulation modules.</span></span> <span data-ttu-id="4ad27-110">puissant langage R de Hello a été décrite comme hello langue véhiculaire d’analytique.</span><span class="sxs-lookup"><span data-stu-id="4ad27-110">hello powerful R language has been described as hello lingua franca of analytics.</span></span> <span data-ttu-id="4ad27-111">Heureusement, la manipulation des données et d’analytique dans Azure Machine Learning peut être étendue à l’aide de R. Cette combinaison offre l’évolutivité de hello et faciliter le déploiement d’Azure Machine Learning avec une grande souplesse hello et analytique approfondie de R.</span><span class="sxs-lookup"><span data-stu-id="4ad27-111">Happily, analytics and data manipulation in Azure Machine Learning can be extended by using R. This combination provides hello scalability and ease of deployment of Azure Machine Learning with hello flexibility and deep analytics of R.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

### <a name="forecasting-and-hello-dataset"></a><span data-ttu-id="4ad27-112">Jeu de données de prévision et hello</span><span class="sxs-lookup"><span data-stu-id="4ad27-112">Forecasting and hello dataset</span></span>
<span data-ttu-id="4ad27-113">La prévision est une méthode analytique largement répandue et très utile.</span><span class="sxs-lookup"><span data-stu-id="4ad27-113">Forecasting is a widely employed and quite useful analytical method.</span></span> <span data-ttu-id="4ad27-114">Plage de prédire les ventes saisonnières d’éléments de, déterminer les niveaux de stock optimaux, les variables macroéconomiques toopredicting d’utilisations courantes.</span><span class="sxs-lookup"><span data-stu-id="4ad27-114">Common uses range from predicting sales of seasonal items, determining optimal inventory levels, toopredicting macroeconomic variables.</span></span> <span data-ttu-id="4ad27-115">La prévision s'appuie généralement sur des modèles chronologiques.</span><span class="sxs-lookup"><span data-stu-id="4ad27-115">Forecasting is typically done with time series models.</span></span>

<span data-ttu-id="4ad27-116">Données de série chronologique sont données dans laquelle les valeurs hello ont un index de temps.</span><span class="sxs-lookup"><span data-stu-id="4ad27-116">Time series data is data in which hello values have a time index.</span></span> <span data-ttu-id="4ad27-117">index de temps Hello peut être normal, par exemple, tous les mois ou chaque minute, ou irréguliers.</span><span class="sxs-lookup"><span data-stu-id="4ad27-117">hello time index can be regular, e.g. every month or every minute, or irregular.</span></span> <span data-ttu-id="4ad27-118">Un modèle chronologique repose sur des données chronologiques.</span><span class="sxs-lookup"><span data-stu-id="4ad27-118">A time series model is based on time series data.</span></span> <span data-ttu-id="4ad27-119">langage de programmation Hello R contient un cadre souple et l’analytique très bien pour les données de série chronologique.</span><span class="sxs-lookup"><span data-stu-id="4ad27-119">hello R programming language contains a flexible framework and extensive analytics for time series data.</span></span>

<span data-ttu-id="4ad27-120">Dans ce guide de démarrage rapide, nous allons utiliser les données de production et de tarification des produits laitiers en Californie.</span><span class="sxs-lookup"><span data-stu-id="4ad27-120">In this quickstart guide we will be working with California dairy production and pricing data.</span></span> <span data-ttu-id="4ad27-121">Ces données incluent tous les mois d’informations sur la production hello de plusieurs produits laitiers et prix hello des matières grasses, un produit d’évaluation.</span><span class="sxs-lookup"><span data-stu-id="4ad27-121">This data includes monthly information on hello production of several dairy products and hello price of milk fat, a benchmark commodity.</span></span>

<span data-ttu-id="4ad27-122">Hello les données utilisées dans cet article, ainsi que des scripts R, peuvent être [téléchargé ici][download].</span><span class="sxs-lookup"><span data-stu-id="4ad27-122">hello data used in this article, along with R scripts, can be [downloaded here][download].</span></span> <span data-ttu-id="4ad27-123">Ces données a été initialement synthétisées à partir des informations disponibles à partir de hello Université de Wisconsin à http://future.aae.wisc.edu/tab/production.html.</span><span class="sxs-lookup"><span data-stu-id="4ad27-123">This data was originally synthesized from information available from hello University of Wisconsin at http://future.aae.wisc.edu/tab/production.html.</span></span>

### <a name="organization"></a><span data-ttu-id="4ad27-124">Organisation</span><span class="sxs-lookup"><span data-stu-id="4ad27-124">Organization</span></span>
<span data-ttu-id="4ad27-125">Nous traiterons à travers plusieurs étapes comme vous apprendre comment toocreate, tester et exécuter du code de manipulation R analytique et les données dans un environnement d’Azure Machine Learning hello.</span><span class="sxs-lookup"><span data-stu-id="4ad27-125">We will progress through several steps as you learn how toocreate, test and execute analytics and data manipulation R code in hello Azure Machine Learning environment.</span></span>  

* <span data-ttu-id="4ad27-126">Tout d’abord, nous allons examiner les bases de hello de l’utilisation de la langue de hello R dans l’environnement d’Azure Machine Learning Studio hello.</span><span class="sxs-lookup"><span data-stu-id="4ad27-126">First we will explore hello basics of using hello R language in hello Azure Machine Learning Studio environment.</span></span>
* <span data-ttu-id="4ad27-127">Puis nous avançons toodiscussing divers aspects d’e/s de données, de code R et de graphiques dans l’environnement d’Azure Machine Learning hello.</span><span class="sxs-lookup"><span data-stu-id="4ad27-127">Then we progress toodiscussing various aspects of I/O for data, R code and graphics in hello Azure Machine Learning environment.</span></span>
* <span data-ttu-id="4ad27-128">Nous allons ensuite construire hello première partie de notre solution prévision en créant le code de nettoyage des données et la transformation.</span><span class="sxs-lookup"><span data-stu-id="4ad27-128">We will then construct hello first part of our forecasting solution by creating code for data cleaning and transformation.</span></span>
* <span data-ttu-id="4ad27-129">Avec nos données préparées, nous allons effectuer une analyse de corrélations hello entre plusieurs variables hello dans notre jeu de données.</span><span class="sxs-lookup"><span data-stu-id="4ad27-129">With our data prepared we will perform an analysis of hello correlations between several of hello variables in our dataset.</span></span>
* <span data-ttu-id="4ad27-130">Enfin, nous créerons un modèle de prévision chronologique saisonnier pour la production de lait.</span><span class="sxs-lookup"><span data-stu-id="4ad27-130">Finally, we will create a seasonal time series forecasting model for milk production.</span></span>

## <span data-ttu-id="4ad27-131"><a id="mlstudio"></a>Interaction avec le langage R dans Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="4ad27-131"><a id="mlstudio"></a>Interact with R language in Machine Learning Studio</span></span>
<span data-ttu-id="4ad27-132">Cette section présente les notions de base de l’interaction avec le langage de programmation hello R dans un environnement de Machine Learning Studio hello.</span><span class="sxs-lookup"><span data-stu-id="4ad27-132">This section takes you through some basics of interacting with hello R programming language in hello Machine Learning Studio environment.</span></span> <span data-ttu-id="4ad27-133">langue de Hello R fournit un outil puissant toocreate personnalisé analytique et les données manipulation modules au sein de l’environnement d’Azure Machine Learning hello.</span><span class="sxs-lookup"><span data-stu-id="4ad27-133">hello R language provides a powerful tool toocreate customized analytics and data manipulation modules within hello Azure Machine Learning environment.</span></span>

<span data-ttu-id="4ad27-134">Je vais utiliser RStudio toodevelop, tester et déboguer du code R à petite échelle.</span><span class="sxs-lookup"><span data-stu-id="4ad27-134">I will use RStudio toodevelop, test and debug R code on a small scale.</span></span> <span data-ttu-id="4ad27-135">Ce code est puis couper et coller dans un [Execute R Script] [ execute-r-script] module toorun prêt de Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="4ad27-135">This code is then cut and paste into an [Execute R Script][execute-r-script] module in Machine Learning Studio ready toorun.</span></span>  

### <a name="hello-execute-r-script-module"></a><span data-ttu-id="4ad27-136">module Execute R Script de Hello</span><span class="sxs-lookup"><span data-stu-id="4ad27-136">hello Execute R Script module</span></span>
<span data-ttu-id="4ad27-137">Au sein de la Machine Learning Studio, les scripts R sont exécutés au sein de hello [Execute R Script] [ execute-r-script] module.</span><span class="sxs-lookup"><span data-stu-id="4ad27-137">Within Machine Learning Studio, R scripts are run within hello [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="4ad27-138">Un exemple de hello [Execute R Script] [ execute-r-script] module dans Machine Learning Studio est indiqué dans la Figure 1.</span><span class="sxs-lookup"><span data-stu-id="4ad27-138">An example of hello [Execute R Script][execute-r-script] module in Machine Learning Studio is shown in Figure 1.</span></span>

 ![Langage de programmation de R : module Execute R Script hello dans Machine Learning Studio][1]

<span data-ttu-id="4ad27-140">*Figure 1. environnement de Machine Learning Studio Hello montrant le module Execute R Script de hello sélectionné.*</span><span class="sxs-lookup"><span data-stu-id="4ad27-140">*Figure 1. hello Machine Learning Studio environment showing hello Execute R Script module selected.*</span></span>

<span data-ttu-id="4ad27-141">Référence tooFigure 1, examinons certains des éléments clés de hello d’environnement de Machine Learning Studio hello pour travailler avec hello [Execute R Script] [ execute-r-script] module.</span><span class="sxs-lookup"><span data-stu-id="4ad27-141">Referring tooFigure 1, let's look at some of hello key parts of hello Machine Learning Studio environment for working with hello [Execute R Script][execute-r-script] module.</span></span>

* <span data-ttu-id="4ad27-142">modules Hello dans expérience de hello sont affichés dans le volet central de hello.</span><span class="sxs-lookup"><span data-stu-id="4ad27-142">hello modules in hello experiment are shown in hello center pane.</span></span>
* <span data-ttu-id="4ad27-143">Hello partie supérieure droite hello contient une fenêtre tooview et modifier vos scripts R.</span><span class="sxs-lookup"><span data-stu-id="4ad27-143">hello upper part of hello right pane contains a window tooview and edit your R scripts.</span></span>  
* <span data-ttu-id="4ad27-144">partie inférieure de Hello du volet de droite montre certaines propriétés de hello [Execute R Script][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="4ad27-144">hello lower part of right pane shows some properties of hello [Execute R Script][execute-r-script].</span></span> <span data-ttu-id="4ad27-145">Vous pouvez afficher les journaux d’erreur et de sortie de hello en cliquant sur l’endroit approprié de hello de ce volet.</span><span class="sxs-lookup"><span data-stu-id="4ad27-145">You can view hello error and output logs by clicking on hello appropriate spots of this pane.</span></span>

<span data-ttu-id="4ad27-146">Nous, bien entendu, aborderons hello [Execute R Script] [ execute-r-script] plus en détail dans le reste de hello de ce document.</span><span class="sxs-lookup"><span data-stu-id="4ad27-146">We will, of course, be discussing hello [Execute R Script][execute-r-script] in greater detail in hello rest of this document.</span></span>

<span data-ttu-id="4ad27-147">Lorsqu'il s'agit d'utiliser des fonctions R complexes, je vous recommande de modifier, tester et déboguer dans RStudio.</span><span class="sxs-lookup"><span data-stu-id="4ad27-147">When working with complex R functions, I recommend that you edit, test and debug in RStudio.</span></span> <span data-ttu-id="4ad27-148">Comme pour tout projet de développement logiciel, développez votre code graduellement et testez-le dans un petit cas de test simple.</span><span class="sxs-lookup"><span data-stu-id="4ad27-148">As with any software development, extend your code incrementally and test it on small simple test cases.</span></span> <span data-ttu-id="4ad27-149">Coupez et collez vos fonctions dans la fenêtre de script hello R Hello [Execute R Script] [ execute-r-script] module.</span><span class="sxs-lookup"><span data-stu-id="4ad27-149">Then cut and paste your functions into hello R script window of hello [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="4ad27-150">Cette approche permet de vous tooharness hello RStudio, environnement de développement intégré (IDE) et hello puissance d’Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="4ad27-150">This approach allows you tooharness both hello RStudio integrated development environment (IDE) and hello power of Azure Machine Learning.</span></span>  

#### <a name="execute-r-code"></a><span data-ttu-id="4ad27-151">Exécution du code R</span><span class="sxs-lookup"><span data-stu-id="4ad27-151">Execute R code</span></span>
<span data-ttu-id="4ad27-152">Tout code hello R [Execute R Script] [ execute-r-script] module s’exécute lorsque vous exécutez hello expérience en cliquant sur hello **exécuter** bouton.</span><span class="sxs-lookup"><span data-stu-id="4ad27-152">Any R code in hello [Execute R Script][execute-r-script] module will execute when you run hello experiment by clicking on hello **Run** button.</span></span> <span data-ttu-id="4ad27-153">Une fois l’exécution terminée, une coche s’affiche sur hello [Execute R Script] [ execute-r-script] icône.</span><span class="sxs-lookup"><span data-stu-id="4ad27-153">When execution has completed, a check mark will appear on hello [Execute R Script][execute-r-script] icon.</span></span>

#### <a name="defensive-r-coding-for-azure-machine-learning"></a><span data-ttu-id="4ad27-154">Codage R défensif pour Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="4ad27-154">Defensive R coding for Azure Machine Learning</span></span>
<span data-ttu-id="4ad27-155">Si vous développez du code R pour, par exemple, un service Web à l’aide d’Azure Machine Learning, vous devez absolument prévoir la façon dont votre code traitera une entrée de données inattendue et les exceptions.</span><span class="sxs-lookup"><span data-stu-id="4ad27-155">If you are developing R code for, say, a web service by using Azure Machine Learning, you should definitely plan how your code will deal with an unexpected data input and exceptions.</span></span> <span data-ttu-id="4ad27-156">toomaintain plus de clarté, je n'ai pas inclus une grande partie de façon hello de la vérification ou la gestion des exceptions dans la plupart des exemples de code hello indiqués.</span><span class="sxs-lookup"><span data-stu-id="4ad27-156">toomaintain clarity, I have not included much in hello way of checking or exception handling in most of hello code examples shown.</span></span> <span data-ttu-id="4ad27-157">Cependant, je vous montrerai par la suite plusieurs exemples de fonctions qui font appel à la fonctionnalité de gestion des exceptions du langage R.</span><span class="sxs-lookup"><span data-stu-id="4ad27-157">However, as we proceed I will give you several examples of functions by using R's exception handling capability.</span></span>  

<span data-ttu-id="4ad27-158">Si vous avez besoin d’un traitement plus complète de gestion des exceptions de R, je vous conseillons de lire sections appropriées hello livre hello Wickham répertorié dans [annexe B : obtenir des informations supplémentaires](#appendixb).</span><span class="sxs-lookup"><span data-stu-id="4ad27-158">If you need a more complete treatment of R exception handling, I recommend you read hello applicable sections of hello book by Wickham listed in [Appendix B - Further Reading](#appendixb).</span></span>

#### <a name="debug-and-test-r-in-machine-learning-studio"></a><span data-ttu-id="4ad27-159">Débogage et test du langage R dans Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="4ad27-159">Debug and test R in Machine Learning Studio</span></span>
<span data-ttu-id="4ad27-160">tooreiterate, je vous recommande de tester et de déboguer votre code R à petite échelle dans RStudio.</span><span class="sxs-lookup"><span data-stu-id="4ad27-160">tooreiterate, I recommend you test and debug your R code on a small scale in RStudio.</span></span> <span data-ttu-id="4ad27-161">Toutefois, il existe des cas où vous devez tootrack les problèmes de code R Bonjour [Execute R Script] [ execute-r-script] lui-même.</span><span class="sxs-lookup"><span data-stu-id="4ad27-161">However, there are cases where you will need tootrack down R code problems in hello [Execute R Script][execute-r-script] itself.</span></span> <span data-ttu-id="4ad27-162">En outre, il est conseillé toocheck vos résultats dans Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="4ad27-162">In addition, it is good practice toocheck your results in Machine Learning Studio.</span></span>

<span data-ttu-id="4ad27-163">Sortie de l’exécution de hello de votre code R et sur la plateforme Azure Machine Learning de hello se trouve principalement dans le fichier sortie.log.</span><span class="sxs-lookup"><span data-stu-id="4ad27-163">Output from hello execution of your R code and on hello Azure Machine Learning platform is found primarily in output.log.</span></span> <span data-ttu-id="4ad27-164">Vous pourrez trouver des informations complémentaires dans le fichier error.log.</span><span class="sxs-lookup"><span data-stu-id="4ad27-164">Some additional information will be seen in error.log.</span></span>  

<span data-ttu-id="4ad27-165">Si une erreur se produit dans Machine Learning Studio lors de l’exécution de votre code R, votre premier plan d’action doit être toolook à error.log.</span><span class="sxs-lookup"><span data-stu-id="4ad27-165">If an error occurs in Machine Learning Studio while running your R code, your first course of action should be toolook at error.log.</span></span> <span data-ttu-id="4ad27-166">Ce fichier peut contenir toohelp de messages d’erreur utiles comprendre et de corriger votre erreur.</span><span class="sxs-lookup"><span data-stu-id="4ad27-166">This file can contain useful error messages toohelp you understand and correct your error.</span></span> <span data-ttu-id="4ad27-167">tooview error.log, cliquez sur **afficher le journal d’erreur** sur hello **volet Propriétés** pour hello [Execute R Script] [ execute-r-script] contenant hello erreur.</span><span class="sxs-lookup"><span data-stu-id="4ad27-167">tooview error.log, click on **View error log** on hello **properties pane** for hello [Execute R Script][execute-r-script] containing hello error.</span></span>

<span data-ttu-id="4ad27-168">Par exemple, j’ai exécuté hello suit le code R, avec une variable non définie y dans une [Execute R Script] [ execute-r-script] module :</span><span class="sxs-lookup"><span data-stu-id="4ad27-168">For example, I ran hello following R code, with an undefined variable y, in an [Execute R Script][execute-r-script] module:</span></span>

    x <- 1.0
    z <- x + y

<span data-ttu-id="4ad27-169">Ce code échoue tooexecute, ce qui entraîne une condition d’erreur.</span><span class="sxs-lookup"><span data-stu-id="4ad27-169">This code fails tooexecute, resulting in an error condition.</span></span> <span data-ttu-id="4ad27-170">En cliquant sur **afficher le journal d’erreur** sur hello **volet Propriétés** produit hello affichage indiqué dans la Figure 2.</span><span class="sxs-lookup"><span data-stu-id="4ad27-170">Clicking on **View error log** on hello **properties pane** produces hello display shown in Figure 2.</span></span>

  ![fenêtre contextuelle de message d’erreur][2]

<span data-ttu-id="4ad27-172">*Figure 2 : fenêtre contextuelle de message d’erreur.*</span><span class="sxs-lookup"><span data-stu-id="4ad27-172">*Figure 2. Error message pop-up.*</span></span>

<span data-ttu-id="4ad27-173">Il semble que nous devons toolook dans le message d’erreur de fichier sortie.log toosee hello R.</span><span class="sxs-lookup"><span data-stu-id="4ad27-173">It looks like we need toolook in output.log toosee hello R error message.</span></span> <span data-ttu-id="4ad27-174">Cliquez sur hello [Execute R Script] [ execute-r-script] , puis cliquez sur hello **afficher le fichier sortie.log** élément sur hello **volet Propriétés** toohello droite.</span><span class="sxs-lookup"><span data-stu-id="4ad27-174">Click on hello [Execute R Script][execute-r-script] and then click on hello **View output.log** item on hello **properties pane** toohello right.</span></span> <span data-ttu-id="4ad27-175">Une nouvelle fenêtre de navigateur s’ouvre, et je voir hello.</span><span class="sxs-lookup"><span data-stu-id="4ad27-175">A new browser window opens, and I see hello following.</span></span>

    [Critical]     Error: Error 0063: hello following error occurred during evaluation of R script:
    ---------- Start of error message from R ----------
    object 'y' not found


    object 'y' not found
    ----------- End of error message from R -----------

<span data-ttu-id="4ad27-176">Ce message d’erreur ne contient aucuns surprises et identifie clairement le problème de hello.</span><span class="sxs-lookup"><span data-stu-id="4ad27-176">This error message contains no surprises and clearly identifies hello problem.</span></span>

<span data-ttu-id="4ad27-177">valeur de hello tooinspect de n’importe quel objet dans R, vous pouvez imprimer le fichier fichier sortie.log toohello de ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="4ad27-177">tooinspect hello value of any object in R, you can print these values toohello output.log file.</span></span> <span data-ttu-id="4ad27-178">règles Hello pour examiner l’objet les valeurs sont essentiellement même hello comme dans une session interactive de R.</span><span class="sxs-lookup"><span data-stu-id="4ad27-178">hello rules for examining object values are essentially hello same as in an interactive R session.</span></span> <span data-ttu-id="4ad27-179">Par exemple, si vous tapez un nom de variable sur une ligne, valeur hello d’objet de hello sera imprimé toohello fichier sortie.log fichier.</span><span class="sxs-lookup"><span data-stu-id="4ad27-179">For example, if you type a variable name on a line, hello value of hello object will be printed toohello output.log file.</span></span>  

#### <a name="packages-in-machine-learning-studio"></a><span data-ttu-id="4ad27-180">Packages dans Azure Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="4ad27-180">Packages in Machine Learning Studio</span></span>
<span data-ttu-id="4ad27-181">Azure Machine Learning est fourni avec plus de 350 packages de langage R préinstallés.</span><span class="sxs-lookup"><span data-stu-id="4ad27-181">Azure Machine Learning comes with over 350 preinstalled R language packages.</span></span> <span data-ttu-id="4ad27-182">Vous pouvez utiliser hello suivant code Bonjour [Execute R Script] [ execute-r-script] module tooretrieve une liste de hello préinstallé packages.</span><span class="sxs-lookup"><span data-stu-id="4ad27-182">You can use hello following code in hello [Execute R Script][execute-r-script] module tooretrieve a list of hello preinstalled packages.</span></span>

    data.set <- data.frame(installed.packages())
    maml.mapOutputPort("data.set")

<span data-ttu-id="4ad27-183">Si vous ne comprenez pas hello dernière ligne de ce code au moment de hello, lisez la suite.</span><span class="sxs-lookup"><span data-stu-id="4ad27-183">If you don't understand hello last line of this code at hello moment, read on.</span></span> <span data-ttu-id="4ad27-184">Dans le reste de hello de ce document, nous aborderons largement à l’aide de R dans l’environnement d’Azure Machine Learning hello.</span><span class="sxs-lookup"><span data-stu-id="4ad27-184">In hello rest of this document we will extensively discuss using R in hello Azure Machine Learning environment.</span></span>

### <a name="introduction-toorstudio"></a><span data-ttu-id="4ad27-185">Introduction tooRStudio</span><span class="sxs-lookup"><span data-stu-id="4ad27-185">Introduction tooRStudio</span></span>
<span data-ttu-id="4ad27-186">RStudio est un IDE largement utilisée pour R. Je vais utiliser RStudio pour modification, de test et de débogage de code hello R utilisés dans ce guide de démarrage rapide.</span><span class="sxs-lookup"><span data-stu-id="4ad27-186">RStudio is a widely used IDE for R. I will use RStudio for editing, testing and debugging some of hello R code used in this quick start guide.</span></span> <span data-ttu-id="4ad27-187">Une fois que le code R est testé et prêt, vous simplement couper et coller à partir de l’éditeur RStudio hello dans une Machine Learning Studio [Execute R Script] [ execute-r-script] module.</span><span class="sxs-lookup"><span data-stu-id="4ad27-187">Once R code is tested and ready, you simply cut and paste from hello RStudio editor into a Machine Learning Studio [Execute R Script][execute-r-script] module.</span></span>  

<span data-ttu-id="4ad27-188">Si vous n’avez pas de langage de programmation hello R installé sur votre ordinateur de bureau, je vous recommande de le que faire maintenant.</span><span class="sxs-lookup"><span data-stu-id="4ad27-188">If you do not have hello R programming language installed on your desktop machine, I recommend you do so now.</span></span> <span data-ttu-id="4ad27-189">Téléchargements gratuits de langage R open source sont disponibles à hello réseau de Archive complète R (CRAN) à [http://www.r-project.org/](http://www.r-project.org/).</span><span class="sxs-lookup"><span data-stu-id="4ad27-189">Free downloads of open source R language are available at hello Comprehensive R Archive Network (CRAN) at [http://www.r-project.org/](http://www.r-project.org/).</span></span> <span data-ttu-id="4ad27-190">Il existe des versions Windows, Mac OS et Linux/UNIX.</span><span class="sxs-lookup"><span data-stu-id="4ad27-190">There are downloads available for Windows, Mac OS, and Linux/UNIX.</span></span> <span data-ttu-id="4ad27-191">Choisissez un miroir à proximité et suivez les instructions de téléchargement hello.</span><span class="sxs-lookup"><span data-stu-id="4ad27-191">Choose a nearby mirror and follow hello download directions.</span></span> <span data-ttu-id="4ad27-192">Par ailleurs, le section CRAN contient de nombreux packages d'analyse et de manipulation de données fort utiles.</span><span class="sxs-lookup"><span data-stu-id="4ad27-192">In addition, CRAN contains a wealth of useful analytics and data manipulation packages.</span></span>

<span data-ttu-id="4ad27-193">Si vous êtes tooRStudio nouveau, vous téléchargez et installez la version de bureau hello.</span><span class="sxs-lookup"><span data-stu-id="4ad27-193">If you are new tooRStudio, you should download and install hello desktop version.</span></span> <span data-ttu-id="4ad27-194">Vous pouvez trouver hello que rstudio télécharge pour Windows, Mac OS et Linux/UNIX à http://www.rstudio.com/products/RStudio/.</span><span class="sxs-lookup"><span data-stu-id="4ad27-194">You can find hello RStudio downloads for Windows, Mac OS, and Linux/UNIX at http://www.rstudio.com/products/RStudio/.</span></span> <span data-ttu-id="4ad27-195">Suivez les instructions hello tooinstall RStudio sur votre ordinateur de bureau.</span><span class="sxs-lookup"><span data-stu-id="4ad27-195">Follow hello directions provided tooinstall RStudio on your desktop machine.</span></span>  

<span data-ttu-id="4ad27-196">Un tooRStudio introduction au didacticiel est disponible à l’adresse https://support.rstudio.com/hc/sections/200107586-Using-RStudio.</span><span class="sxs-lookup"><span data-stu-id="4ad27-196">A tutorial introduction tooRStudio is available at https://support.rstudio.com/hc/sections/200107586-Using-RStudio.</span></span>

<span data-ttu-id="4ad27-197">Vous trouverez des informations complémentaires sur l’utilisation de RStudio dans [l’Annexe A][appendixa].</span><span class="sxs-lookup"><span data-stu-id="4ad27-197">I provide some additional information on using RStudio in [Appendix A][appendixa].</span></span>  

## <span data-ttu-id="4ad27-198"><a id="scriptmodule"></a>Obtenir des données vers et depuis le module Execute R Script de hello</span><span class="sxs-lookup"><span data-stu-id="4ad27-198"><a id="scriptmodule"></a>Get data in and out of hello Execute R Script module</span></span>
<span data-ttu-id="4ad27-199">Dans cette section, nous aborderons comment d’obtenir des données dans et hors hello [Execute R Script] [ execute-r-script] module.</span><span class="sxs-lookup"><span data-stu-id="4ad27-199">In this section we will discuss how you get data into and out of hello [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="4ad27-200">Nous allons examiner comment toohandle différents types de données lues dans et hors hello [Execute R Script] [ execute-r-script] module.</span><span class="sxs-lookup"><span data-stu-id="4ad27-200">We will review how toohandle various data types read into and out of hello [Execute R Script][execute-r-script] module.</span></span>

<span data-ttu-id="4ad27-201">code complet de Hello pour cette section est dans un fichier zip de hello téléchargé précédemment.</span><span class="sxs-lookup"><span data-stu-id="4ad27-201">hello complete code for this section is in hello zip file you downloaded earlier.</span></span>

### <a name="load-and-check-data-in-machine-learning-studio"></a><span data-ttu-id="4ad27-202">Chargement et vérification des données dans Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="4ad27-202">Load and check data in Machine Learning Studio</span></span>
#### <span data-ttu-id="4ad27-203"><a id="loading"></a>Jeu de données charge hello</span><span class="sxs-lookup"><span data-stu-id="4ad27-203"><a id="loading"></a>Load hello dataset</span></span>
<span data-ttu-id="4ad27-204">Nous allons commencer en chargeant hello **csdairydata.csv** fichier dans Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="4ad27-204">We will start by loading hello **csdairydata.csv** file into Azure Machine Learning Studio.</span></span>

* <span data-ttu-id="4ad27-205">Démarrez votre environnement Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="4ad27-205">Start your Azure Machine Learning Studio environment.</span></span>
* <span data-ttu-id="4ad27-206">Cliquez sur **+ nouveau** à hello bas à gauche de votre écran, puis sélectionnez **Dataset**.</span><span class="sxs-lookup"><span data-stu-id="4ad27-206">Click on **+ NEW** at hello lower left of your screen and select **Dataset**.</span></span>
* <span data-ttu-id="4ad27-207">Sélectionnez **à partir d’un fichier Local**, puis **Parcourir** fichier hello de tooselect.</span><span class="sxs-lookup"><span data-stu-id="4ad27-207">Select **From Local File**, and then **Browse** tooselect hello file.</span></span>
* <span data-ttu-id="4ad27-208">Vérifiez que vous avez sélectionné **fichier CSV générique avec l’en-tête (.csv)** en tant que type hello pour hello le jeu de données.</span><span class="sxs-lookup"><span data-stu-id="4ad27-208">Make sure you have selected **Generic CSV file with header (.csv)** as hello type for hello dataset.</span></span>
* <span data-ttu-id="4ad27-209">Cliquez sur case à cocher hello.</span><span class="sxs-lookup"><span data-stu-id="4ad27-209">Click hello check mark.</span></span>
* <span data-ttu-id="4ad27-210">Après hello dataset a été téléchargé, vous devez voir hello le nouveau jeu de données en cliquant sur hello **Datasets** onglet.</span><span class="sxs-lookup"><span data-stu-id="4ad27-210">After hello dataset has been uploaded, you should see hello new dataset by clicking on hello **Datasets** tab.</span></span>  

#### <a name="create-an-experiment"></a><span data-ttu-id="4ad27-211">Création d'une expérience</span><span class="sxs-lookup"><span data-stu-id="4ad27-211">Create an experiment</span></span>
<span data-ttu-id="4ad27-212">Maintenant que nous avons des données dans Machine Learning Studio, nous devons toocreate une analyse de hello toodo expérience.</span><span class="sxs-lookup"><span data-stu-id="4ad27-212">Now that we have some data in Machine Learning Studio, we need toocreate an experiment toodo hello analysis.</span></span>  

* <span data-ttu-id="4ad27-213">Cliquez sur **+ nouveau** à hello coin inférieur gauche et sélectionnez **expérience**, puis **expérience vide**.</span><span class="sxs-lookup"><span data-stu-id="4ad27-213">Click on **+ NEW** at hello lower left and select **Experiment**, then **Blank Experiment**.</span></span>
* <span data-ttu-id="4ad27-214">Vous pouvez nommer votre expérience en sélectionnant et en modification, hello **expérience créé sur...**  titre en hello haut hello.</span><span class="sxs-lookup"><span data-stu-id="4ad27-214">You can name your experiment by selecting, and modifying, hello **Experiment created on ...** title at hello top of hello page.</span></span> <span data-ttu-id="4ad27-215">Par exemple, la modification trop**autorité de certification laiterie analyse**.</span><span class="sxs-lookup"><span data-stu-id="4ad27-215">For example, changing it too**CA Dairy Analysis**.</span></span>
* <span data-ttu-id="4ad27-216">Sur la gauche hello de page d’expérience hello, développez **jeux de données enregistrés**, puis **mes Datasets**.</span><span class="sxs-lookup"><span data-stu-id="4ad27-216">On hello left of hello experiment page, expand **Saved Datasets**, and then **My Datasets**.</span></span> <span data-ttu-id="4ad27-217">Vous devez voir hello **cadairydata.csv** que vous avez téléchargé précédemment.</span><span class="sxs-lookup"><span data-stu-id="4ad27-217">You should see hello **cadairydata.csv** that you uploaded earlier.</span></span>
* <span data-ttu-id="4ad27-218">Glisser- déposer hello **csdairydata.csv dataset** sur l’expérience de hello.</span><span class="sxs-lookup"><span data-stu-id="4ad27-218">Drag and drop hello **csdairydata.csv dataset** onto hello experiment.</span></span>
* <span data-ttu-id="4ad27-219">Bonjour **recherche expérimenter éléments** zone en haut de hello du volet gauche hello, type [Execute R Script][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="4ad27-219">In hello **Search experiment items** box on hello top of hello left pane, type [Execute R Script][execute-r-script].</span></span> <span data-ttu-id="4ad27-220">Module de hello s’affiche dans la liste de recherche hello.</span><span class="sxs-lookup"><span data-stu-id="4ad27-220">You will see hello module appear in hello search list.</span></span>
* <span data-ttu-id="4ad27-221">Glisser- déposer hello [Execute R Script] [ execute-r-script] module sur votre palette.</span><span class="sxs-lookup"><span data-stu-id="4ad27-221">Drag and drop hello [Execute R Script][execute-r-script] module onto your pallet.</span></span>  
* <span data-ttu-id="4ad27-222">Connectez la sortie hello Hello **csdairydata.csv dataset** entrée à l’extrême gauche de toohello (**Dataset1**) de hello [Execute R Script][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="4ad27-222">Connect hello output of hello **csdairydata.csv dataset** toohello leftmost input (**Dataset1**) of hello [Execute R Script][execute-r-script].</span></span>
* <span data-ttu-id="4ad27-223">**N’oubliez pas tooclick sur « Enregistrer ».**</span><span class="sxs-lookup"><span data-stu-id="4ad27-223">**Don't forget tooclick on 'Save'!**</span></span>  

<span data-ttu-id="4ad27-224">À ce stade, votre expérimentation doit être similaire à la figure 3.</span><span class="sxs-lookup"><span data-stu-id="4ad27-224">At this point your experiment should look something like Figure 3.</span></span>

![Hello autorité de certification laiterie analyse faire des essais avec le jeu de données et le module Execute R Script][3]

<span data-ttu-id="4ad27-226">*La figure 3. Hello autorité de certification laiterie analyse faire des essais avec le jeu de données et le module Execute R Script.*</span><span class="sxs-lookup"><span data-stu-id="4ad27-226">*Figure 3. hello CA Dairy Analysis experiment with dataset and Execute R Script module.*</span></span>

#### <a name="check-on-hello-data"></a><span data-ttu-id="4ad27-227">Vérifier les données de salutation</span><span class="sxs-lookup"><span data-stu-id="4ad27-227">Check on hello data</span></span>
<span data-ttu-id="4ad27-228">Nous allons avoir un aspect des données hello que nous avons chargé dans notre expérience.</span><span class="sxs-lookup"><span data-stu-id="4ad27-228">Let's have a look at hello data we have loaded into our experiment.</span></span> <span data-ttu-id="4ad27-229">Dans l’expérience hello, cliquez sur sortie hello Hello **cadairydata.csv dataset** et sélectionnez **visualiser**.</span><span class="sxs-lookup"><span data-stu-id="4ad27-229">In hello experiment, click on hello output of hello **cadairydata.csv dataset** and select **visualize**.</span></span> <span data-ttu-id="4ad27-230">Vous obtenez un résultat analogue à la figure 4.</span><span class="sxs-lookup"><span data-stu-id="4ad27-230">You should see something like Figure 4.</span></span>  

![Résumé du jeu de données hello cadairydata.csv][4]

<span data-ttu-id="4ad27-232">*Figure 4 : Résumé du jeu de données cadairydata.csv hello.*</span><span class="sxs-lookup"><span data-stu-id="4ad27-232">*Figure 4. Summary of hello cadairydata.csv dataset.*</span></span>

<span data-ttu-id="4ad27-233">Cette vue contient de nombreuses informations utiles.</span><span class="sxs-lookup"><span data-stu-id="4ad27-233">In this view we see a lot of useful information.</span></span> <span data-ttu-id="4ad27-234">Nous pouvons voir hello première plusieurs lignes du jeu de données.</span><span class="sxs-lookup"><span data-stu-id="4ad27-234">We can see hello first several rows of that dataset.</span></span> <span data-ttu-id="4ad27-235">Si vous sélectionnez une colonne, hello section des statistiques s’affiche plus d’informations sur la colonne de hello.</span><span class="sxs-lookup"><span data-stu-id="4ad27-235">If we select a column, hello Statistics section shows more information about hello column.</span></span> <span data-ttu-id="4ad27-236">Par exemple, ligne du Type de fonctionnalité hello montre quels types de données Azure Machine Learning Studio affecté toohello colonne.</span><span class="sxs-lookup"><span data-stu-id="4ad27-236">For example, hello Feature Type row shows us what data types Azure Machine Learning Studio assigned toohello column.</span></span> <span data-ttu-id="4ad27-237">Un coup de œil rapide à ceci est un contrôle de validité correct avant de commencer à n’importe quel travail grave toodo.</span><span class="sxs-lookup"><span data-stu-id="4ad27-237">Having a quick look like this is a good sanity check before we start toodo any serious work.</span></span>

### <a name="first-r-script"></a><span data-ttu-id="4ad27-238">Premier script R</span><span class="sxs-lookup"><span data-stu-id="4ad27-238">First R script</span></span>
<span data-ttu-id="4ad27-239">Nous allons créer une simple tooexperiment de script R première avec dans Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="4ad27-239">Let's create a simple first R script tooexperiment with in Azure Machine Learning Studio.</span></span> <span data-ttu-id="4ad27-240">J’ai créé et testé hello script dans RStudio suivant.</span><span class="sxs-lookup"><span data-stu-id="4ad27-240">I have created and tested hello following script in RStudio.</span></span>  

    ## Only one of hello following two lines should be used
    ## If running in Machine Learning Studio, use hello first line with maml.mapInputPort()
    ## If in RStudio, use hello second line with read.csv()
    cadairydata <- maml.mapInputPort(1)
    # cadairydata  <- read.csv("cadairydata.csv", header = TRUE, stringsAsFactors = FALSE)
    str(cadairydata)
    pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = cadairydata)
    ## hello following line should be executed only when running in
    ## Azure Machine Learning Studio
    maml.mapOutputPort('cadairydata')

<span data-ttu-id="4ad27-241">J’ai besoin maintenant tootransfer cette tooAzure script Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="4ad27-241">Now I need tootransfer this script tooAzure Machine Learning Studio.</span></span> <span data-ttu-id="4ad27-242">Je pourrais simplement effectuer un couper-coller.</span><span class="sxs-lookup"><span data-stu-id="4ad27-242">I could simply cut and paste.</span></span> <span data-ttu-id="4ad27-243">Mais je vais ici transférer le script R via un fichier zip.</span><span class="sxs-lookup"><span data-stu-id="4ad27-243">However, in this case, I will transfer my R script via a zip file.</span></span>

### <a name="data-input-toohello-execute-r-script-module"></a><span data-ttu-id="4ad27-244">Module de données d’entrée toohello Execute R Script</span><span class="sxs-lookup"><span data-stu-id="4ad27-244">Data input toohello Execute R Script module</span></span>
<span data-ttu-id="4ad27-245">Nous allons avez hello entrées toohello [Execute R Script] [ execute-r-script] module.</span><span class="sxs-lookup"><span data-stu-id="4ad27-245">Let's have a look at hello inputs toohello [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="4ad27-246">Dans cet exemple, nous lira des données laitières de Californie hello en hello [Execute R Script] [ execute-r-script] module.</span><span class="sxs-lookup"><span data-stu-id="4ad27-246">In this example we will read hello California dairy data into hello [Execute R Script][execute-r-script] module.</span></span>  

<span data-ttu-id="4ad27-247">Il existe trois entrées possibles pour hello [Execute R Script] [ execute-r-script] module.</span><span class="sxs-lookup"><span data-stu-id="4ad27-247">There are three possible inputs for hello [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="4ad27-248">Selon votre application, vous pouvez utiliser une ou toutes ces entrées.</span><span class="sxs-lookup"><span data-stu-id="4ad27-248">You may use any one or all of these inputs, depending on your application.</span></span> <span data-ttu-id="4ad27-249">Il est également parfaitement raisonnable toouse R qui n’accepte aucune entrée du tout.</span><span class="sxs-lookup"><span data-stu-id="4ad27-249">It is also perfectly reasonable toouse an R script that takes no input at all.</span></span>  

<span data-ttu-id="4ad27-250">Examinons chacune de ces entrées, allant de gauche tooright.</span><span class="sxs-lookup"><span data-stu-id="4ad27-250">Let's look at each of these inputs, going from left tooright.</span></span> <span data-ttu-id="4ad27-251">Vous pouvez voir les noms de hello de chacune des entrées de hello en positionnant le curseur à l’entrée de hello et en lisant les info-bulle hello.</span><span class="sxs-lookup"><span data-stu-id="4ad27-251">You can see hello names of each of hello inputs by placing your cursor over hello input and reading hello tooltip.</span></span>  

#### <a name="script-bundle"></a><span data-ttu-id="4ad27-252">Script groupé</span><span class="sxs-lookup"><span data-stu-id="4ad27-252">Script Bundle</span></span>
<span data-ttu-id="4ad27-253">Hello entrée de regroupement de Script vous permet de contenu de hello toopass d’un fichier zip dans [Execute R Script] [ execute-r-script] module.</span><span class="sxs-lookup"><span data-stu-id="4ad27-253">hello Script Bundle input allows you toopass hello contents of a zip file into [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="4ad27-254">Vous pouvez utiliser une des hello suivant le contenu de hello tooread commandes du fichier zip de hello dans votre code R.</span><span class="sxs-lookup"><span data-stu-id="4ad27-254">You can use one of hello following commands tooread hello contents of hello zip file into your R code.</span></span>

    source("src/yourfile.R") # Reads a zipped R script
    load("src/yourData.rdata") # Reads a zipped R data file

> [!NOTE]
> <span data-ttu-id="4ad27-255">Azure Machine Learning traite les fichiers zip de hello comme s’ils étaient hello src / directory, vous devez tooprefix les noms de votre fichier avec ce nom de répertoire.</span><span class="sxs-lookup"><span data-stu-id="4ad27-255">Azure Machine Learning treats files in hello zip as if they are in hello src/ directory, so you need tooprefix your file names with this directory name.</span></span> <span data-ttu-id="4ad27-256">Par exemple, si hello zip contient des fichiers de hello `yourfile.R` et `yourData.rdata` dans racine hello zip de hello, vous devez vous occuper en tant que `src/yourfile.R` et `src/yourData.rdata` lors de l’utilisation `source` et `load`.</span><span class="sxs-lookup"><span data-stu-id="4ad27-256">For example, if hello zip contains hello files `yourfile.R` and `yourData.rdata` in hello root of hello zip, you would address these as `src/yourfile.R` and `src/yourData.rdata` when using `source` and `load`.</span></span>
> 
> 

<span data-ttu-id="4ad27-257">Nous avons déjà mentionné lors du chargement de jeux de données dans [chargement hello dataset](#loading).</span><span class="sxs-lookup"><span data-stu-id="4ad27-257">We already discussed loading datasets in [Loading hello dataset](#loading).</span></span> <span data-ttu-id="4ad27-258">Une fois que vous avez créé et testé le script hello R indiqué dans la section précédente de hello, procédez comme hello suivant :</span><span class="sxs-lookup"><span data-stu-id="4ad27-258">Once you have created and tested hello R script shown in hello previous section, do hello following:</span></span>

1. <span data-ttu-id="4ad27-259">Enregistrer le script hello R dans un. Fichier de R.</span><span class="sxs-lookup"><span data-stu-id="4ad27-259">Save hello R script into a .R file.</span></span> <span data-ttu-id="4ad27-260">J'appelle mon fichier de script « simpleplot.R ».</span><span class="sxs-lookup"><span data-stu-id="4ad27-260">I call my script file "simpleplot.R".</span></span> <span data-ttu-id="4ad27-261">Voici le contenu de hello.</span><span class="sxs-lookup"><span data-stu-id="4ad27-261">Here's hello contents.</span></span>
   
        ## Only one of hello following two lines should be used
        ## If running in Machine Learning Studio, use hello first line with maml.mapInputPort()
        ## If in RStudio, use hello second line with read.csv()
        cadairydata <- maml.mapInputPort(1)
        # cadairydata  <- read.csv("cadairydata.csv", header = TRUE, stringsAsFactors = FALSE)
        str(cadairydata)
        pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = cadairydata)
        ## hello following line should be executed only when running in
        ## Azure Machine Learning Studio
        maml.mapOutputPort('cadairydata')
2. <span data-ttu-id="4ad27-262">Créez un fichier zip et copiez votre script dans ce fichier.</span><span class="sxs-lookup"><span data-stu-id="4ad27-262">Create a zip file and copy your script into this zip file.</span></span> <span data-ttu-id="4ad27-263">Sous Windows, vous pouvez avec le bouton droit sur le fichier de hello et sélectionnez **envoyer à**, puis **dossier compressé**.</span><span class="sxs-lookup"><span data-stu-id="4ad27-263">On Windows, you can right-click on hello file and select **Send to**, and then **Compressed folder**.</span></span> <span data-ttu-id="4ad27-264">Cela crée un nouveau fichier zip contenant hello « simpleplot. Fichier de R ».</span><span class="sxs-lookup"><span data-stu-id="4ad27-264">This will create a new zip file containing hello "simpleplot.R" file.</span></span>
3. <span data-ttu-id="4ad27-265">Ajouter votre fichier toohello **datasets** dans Machine Learning Studio, la spécification de type hello en tant que **zip**.</span><span class="sxs-lookup"><span data-stu-id="4ad27-265">Add your file toohello **datasets** in Machine Learning Studio, specifying hello type as **zip**.</span></span> <span data-ttu-id="4ad27-266">Vous devez maintenant voir le fichier zip de hello dans vos jeux de données.</span><span class="sxs-lookup"><span data-stu-id="4ad27-266">You should now see hello zip file in your datasets.</span></span>
4. <span data-ttu-id="4ad27-267">Fichier zip de hello du glisser -déplacer à partir de **datasets** sur hello **canevas de ML Studio**.</span><span class="sxs-lookup"><span data-stu-id="4ad27-267">Drag and drop hello zip file from **datasets** onto hello **ML Studio canvas**.</span></span>
5. <span data-ttu-id="4ad27-268">Connectez la sortie hello Hello **zip données** icône toohello **regroupement de Script** d’entrée de hello [Execute R Script] [ execute-r-script] module.</span><span class="sxs-lookup"><span data-stu-id="4ad27-268">Connect hello output of hello **zip data** icon toohello **Script Bundle** input of hello [Execute R Script][execute-r-script] module.</span></span>
6. <span data-ttu-id="4ad27-269">Hello de type `source()` fonction avec le nom du fichier zip dans la fenêtre de code hello pour hello [Execute R Script] [ execute-r-script] module.</span><span class="sxs-lookup"><span data-stu-id="4ad27-269">Type hello `source()` function with your zip file name into hello code window for hello [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="4ad27-270">Dans mon cas, j’ai saisi `source("src/simpleplot.R")`.</span><span class="sxs-lookup"><span data-stu-id="4ad27-270">In my case I typed `source("src/simpleplot.R")`.</span></span>  
7. <span data-ttu-id="4ad27-271">Pensez à cliquer sur **Save**(Enregistrer).</span><span class="sxs-lookup"><span data-stu-id="4ad27-271">Make sure you click **Save**.</span></span>

<span data-ttu-id="4ad27-272">Une fois ces étapes terminées, hello [Execute R Script] [ execute-r-script] module entraîne l’exécution hello R script dans le fichier zip de hello lors de l’expérience de hello est exécuté.</span><span class="sxs-lookup"><span data-stu-id="4ad27-272">Once these steps are complete, hello [Execute R Script][execute-r-script] module will execute hello R script in hello zip file when hello experiment is run.</span></span> <span data-ttu-id="4ad27-273">À ce stade, votre expérimentation doit être similaire à la figure 5.</span><span class="sxs-lookup"><span data-stu-id="4ad27-273">At this point your experiment should look something like Figure 5.</span></span>

![expérimentation utilisant le script R compressé][6]

<span data-ttu-id="4ad27-275">*Figure 5 : expérimentation utilisant le script R compressé.*</span><span class="sxs-lookup"><span data-stu-id="4ad27-275">*Figure 5. Experiment using zipped R script.*</span></span>

#### <a name="dataset1"></a><span data-ttu-id="4ad27-276">Jeu de données 1</span><span class="sxs-lookup"><span data-stu-id="4ad27-276">Dataset1</span></span>
<span data-ttu-id="4ad27-277">Vous pouvez passer un tableau rectangulaire de code tooyour R de données à l’aide d’entrée de hello Dataset1.</span><span class="sxs-lookup"><span data-stu-id="4ad27-277">You can pass a rectangular table of data tooyour R code by using hello Dataset1 input.</span></span> <span data-ttu-id="4ad27-278">Dans notre hello script simple `maml.mapInputPort(1)` fonction lit les données de hello dans le port 1.</span><span class="sxs-lookup"><span data-stu-id="4ad27-278">In our simple script hello `maml.mapInputPort(1)` function reads hello data from port 1.</span></span> <span data-ttu-id="4ad27-279">Ces données sont ensuite assignées tooa trame de données nom de la variable dans votre code.</span><span class="sxs-lookup"><span data-stu-id="4ad27-279">This data is then assigned tooa dataframe variable name in your code.</span></span> <span data-ttu-id="4ad27-280">Dans notre script simple hello première ligne de code effectue des assignations de hello.</span><span class="sxs-lookup"><span data-stu-id="4ad27-280">In our simple script hello first line of code performs hello assignment.</span></span>

    cadairydata <- maml.mapInputPort(1)

<span data-ttu-id="4ad27-281">Exécuter votre expérience en cliquant sur hello **exécuter** bouton.</span><span class="sxs-lookup"><span data-stu-id="4ad27-281">Execute your experiment by clicking on hello **Run** button.</span></span> <span data-ttu-id="4ad27-282">Lors de l’exécution de hello est terminée, cliquez sur hello [Execute R Script] [ execute-r-script] module, puis cliquez sur **afficher le journal de sortie** sur le volet de propriétés hello.</span><span class="sxs-lookup"><span data-stu-id="4ad27-282">When hello execution finishes, click on hello [Execute R Script][execute-r-script] module and then click **View output log** on hello properties pane.</span></span> <span data-ttu-id="4ad27-283">Une nouvelle page doit apparaître dans votre navigateur, affichage du contenu du fichier du fichier sortie.log hello hello.</span><span class="sxs-lookup"><span data-stu-id="4ad27-283">A new page should appear in your browser showing hello contents of hello output.log file.</span></span> <span data-ttu-id="4ad27-284">Lorsque vous faites défiler vers le bas, vous devez voir quelque chose comme hello suivant.</span><span class="sxs-lookup"><span data-stu-id="4ad27-284">When you scroll down you should see something like hello following.</span></span>

    [ModuleOutput] InputDataStructure
    [ModuleOutput]
    [ModuleOutput] {
    [ModuleOutput]  "InputName":Dataset1
    [ModuleOutput]  "Rows":228
    [ModuleOutput]  "Cols":9
    [ModuleOutput]  "ColumnTypes":System.Int32,3,System.Double,5,System.String,1
    [ModuleOutput] }

<span data-ttu-id="4ad27-285">Plus loin vers le bas hello page est plus d’informations sur les colonnes hello, qui ressemble à hello suivant.</span><span class="sxs-lookup"><span data-stu-id="4ad27-285">Farther down hello page is more detailed information on hello columns, which will look something like hello following.</span></span>

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

<span data-ttu-id="4ad27-286">Ces résultats sont principalement comme prévu, des 228 observations 9 colonnes et dans hello trame de données.</span><span class="sxs-lookup"><span data-stu-id="4ad27-286">These results are mostly as expected, with 228 observations and 9 columns in hello dataframe.</span></span> <span data-ttu-id="4ad27-287">Nous pouvons voir les noms de colonne hello, type de données hello R et un exemple de chaque colonne.</span><span class="sxs-lookup"><span data-stu-id="4ad27-287">We can see hello column names, hello R data type and a sample of each column.</span></span>

> [!NOTE]
> <span data-ttu-id="4ad27-288">Cette sortie imprimée même est facilement disponible à partir de hello sortie appareil R Hello [Execute R Script] [ execute-r-script] module.</span><span class="sxs-lookup"><span data-stu-id="4ad27-288">This same printed output is conveniently available from hello R Device output of hello [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="4ad27-289">Nous allons décrire les sorties hello Hello [Execute R Script] [ execute-r-script] module dans la section suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="4ad27-289">We will discuss hello outputs of hello [Execute R Script][execute-r-script] module in hello next section.</span></span>  
> 
> 

#### <a name="dataset2"></a><span data-ttu-id="4ad27-290">Jeu de données 2</span><span class="sxs-lookup"><span data-stu-id="4ad27-290">Dataset2</span></span>
<span data-ttu-id="4ad27-291">Bonjour le comportement de l’entrée de hello Dataset2 est toothat identiques de Dataset1.</span><span class="sxs-lookup"><span data-stu-id="4ad27-291">hello behavior of hello Dataset2 input is identical toothat of Dataset1.</span></span> <span data-ttu-id="4ad27-292">Avec cette entrée, vous pouvez transmettre une deuxième table de données rectangulaire à votre code R.</span><span class="sxs-lookup"><span data-stu-id="4ad27-292">Using this input you can pass a second rectangular table of data into your R code.</span></span> <span data-ttu-id="4ad27-293">Hello fonction `maml.mapInputPort(2)`, avec l’argument hello 2, est utilisé toopass ces données.</span><span class="sxs-lookup"><span data-stu-id="4ad27-293">hello function `maml.mapInputPort(2)`, with hello argument 2, is used toopass this data.</span></span>  

### <a name="execute-r-script-outputs"></a><span data-ttu-id="4ad27-294">Sorties du module d'exécution de script R</span><span class="sxs-lookup"><span data-stu-id="4ad27-294">Execute R Script outputs</span></span>
#### <a name="output-a-dataframe"></a><span data-ttu-id="4ad27-295">Sortie d'un tableau de données</span><span class="sxs-lookup"><span data-stu-id="4ad27-295">Output a dataframe</span></span>
<span data-ttu-id="4ad27-296">Vous pouvez sortie contenu hello d’une trame de données R comme un tableau rectangulaire via le port de hello Dataset1 de résultat à l’aide de hello `maml.mapOutputPort()` (fonction).</span><span class="sxs-lookup"><span data-stu-id="4ad27-296">You can output hello contents of an R dataframe as a rectangular table through hello Result Dataset1 port by using hello `maml.mapOutputPort()` function.</span></span> <span data-ttu-id="4ad27-297">Dans notre script R simple cette opération est effectuée par hello ligne suivante.</span><span class="sxs-lookup"><span data-stu-id="4ad27-297">In our simple R script this is performed by hello following line.</span></span>

    maml.mapOutputPort('cadairydata')

<span data-ttu-id="4ad27-298">Après l’expérience hello en cours d’exécution, cliquez sur hello port de sortie des résultats Dataset1, puis cliquez sur **visualiser**.</span><span class="sxs-lookup"><span data-stu-id="4ad27-298">After running hello experiment, click on hello Result Dataset1 output port and then click on **Visualize**.</span></span> <span data-ttu-id="4ad27-299">Vous obtenez un résultat analogue à la figure 6.</span><span class="sxs-lookup"><span data-stu-id="4ad27-299">You should see something like Figure 6.</span></span>

![visualisation de Hello de sortie hello Hello données laitières de Californie][7]

<span data-ttu-id="4ad27-301">*La figure 6. visualisation de Hello de sortie hello Hello données laitières de Californie.*</span><span class="sxs-lookup"><span data-stu-id="4ad27-301">*Figure 6. hello visualization of hello output of hello California dairy data.*</span></span>

<span data-ttu-id="4ad27-302">Cette sortie ressemble toohello identiques entrée, exactement comme nous attendions.</span><span class="sxs-lookup"><span data-stu-id="4ad27-302">This output looks identical toohello input, exactly as we expected.</span></span>  

### <a name="r-device-output"></a><span data-ttu-id="4ad27-303">Sortie de l’appareil R</span><span class="sxs-lookup"><span data-stu-id="4ad27-303">R Device output</span></span>
<span data-ttu-id="4ad27-304">Hello sorties sur des périphériques de hello [Execute R Script] [ execute-r-script] module contient la sortie des messages et des graphiques.</span><span class="sxs-lookup"><span data-stu-id="4ad27-304">hello Device output of hello [Execute R Script][execute-r-script] module contains messages and graphics output.</span></span> <span data-ttu-id="4ad27-305">Les deux messages de sortie et l’erreur standard standards à partir de R sont envoyés toohello port de sortie de périphérique R.</span><span class="sxs-lookup"><span data-stu-id="4ad27-305">Both standard output and standard error messages from R are sent toohello R Device output port.</span></span>  

<span data-ttu-id="4ad27-306">tooview hello R périphérique de sortie, cliquez sur le port hello puis sur **visualiser**.</span><span class="sxs-lookup"><span data-stu-id="4ad27-306">tooview hello R Device output, click on hello port and then on **Visualize**.</span></span> <span data-ttu-id="4ad27-307">Nous voyons sortie standard de hello et d’erreur standard à partir du script hello R dans la Figure 7.</span><span class="sxs-lookup"><span data-stu-id="4ad27-307">We see hello standard output and standard error from hello R script in Figure 7.</span></span>

![Sortie standard et l’erreur standard de hello port du périphérique R][8]

<span data-ttu-id="4ad27-309">*Figure 7 : Sortie standard et l’erreur standard de hello port du périphérique R.*</span><span class="sxs-lookup"><span data-stu-id="4ad27-309">*Figure 7. Standard output and standard error from hello R Device port.*</span></span>

<span data-ttu-id="4ad27-310">Le défilement vers le bas nous, consultez la sortie de graphiques hello à partir de notre script R dans la Figure 8.</span><span class="sxs-lookup"><span data-stu-id="4ad27-310">Scrolling down we see hello graphics output from our R script in Figure 8.</span></span>  

![Sortie graphique à partir de hello port du périphérique R][9]

<span data-ttu-id="4ad27-312">*Figure 8 : Graphique de sortie de hello port du périphérique R.*</span><span class="sxs-lookup"><span data-stu-id="4ad27-312">*Figure 8. Graphics output from hello R Device port.*</span></span>  

## <span data-ttu-id="4ad27-313"><a id="filtering"></a>Filtrage et transformation des données</span><span class="sxs-lookup"><span data-stu-id="4ad27-313"><a id="filtering"></a>Data filtering and transformation</span></span>
<span data-ttu-id="4ad27-314">Dans cette section, nous allons effectuer certains le filtrage de données de base et les opérations de transformation sur hello données laitières de Californie.</span><span class="sxs-lookup"><span data-stu-id="4ad27-314">In this section we will perform some basic data filtering and transformation operations on hello California dairy data.</span></span> <span data-ttu-id="4ad27-315">En fin de hello de cette section, nous auront des données dans un format approprié pour la création d’un modèle d’analyse.</span><span class="sxs-lookup"><span data-stu-id="4ad27-315">By hello end of this section we will have data in a format suitable for building an analytic model.</span></span>  

<span data-ttu-id="4ad27-316">Plus particulièrement, nous allons effectuer dans cette section plusieurs tâches courantes de nettoyage et de transformation de données ; de transformation de types, de filtrage sur des tableaux de données, d’ajout de nouvelles colonnes calculées et de transformation de valeurs.</span><span class="sxs-lookup"><span data-stu-id="4ad27-316">More specifically, in this section we will perform several common data cleaning and transformation tasks: type transformation, filtering on dataframes, adding new computed columns, and value transformations.</span></span> <span data-ttu-id="4ad27-317">Cet arrière-plan doit vous permettre de traiter de nombreuses variations a rencontré des problèmes réels hello.</span><span class="sxs-lookup"><span data-stu-id="4ad27-317">This background should help you deal with hello many variations encountered in real-world problems.</span></span>

<span data-ttu-id="4ad27-318">Hello R code complet pour cette section est disponible dans le fichier zip de hello téléchargé précédemment.</span><span class="sxs-lookup"><span data-stu-id="4ad27-318">hello complete R code for this section is available in hello zip file you downloaded earlier.</span></span>

### <a name="type-transformations"></a><span data-ttu-id="4ad27-319">Transformations de types</span><span class="sxs-lookup"><span data-stu-id="4ad27-319">Type transformations</span></span>
<span data-ttu-id="4ad27-320">Maintenant que nous pouvons lire les données de laitier de Californie hello dans code hello R hello [Execute R Script] [ execute-r-script] module, nous devons tooensure que les données hello dans les colonnes hello ont hello destiné type et le format.</span><span class="sxs-lookup"><span data-stu-id="4ad27-320">Now that we can read hello California dairy data into hello R code in hello [Execute R Script][execute-r-script] module, we need tooensure that hello data in hello columns has hello intended type and format.</span></span>  

<span data-ttu-id="4ad27-321">R est un langage typé dynamiquement, ce qui signifie que les types de données sont convertis à partir d’un tooanother en fonction des besoins.</span><span class="sxs-lookup"><span data-stu-id="4ad27-321">R is a dynamically typed language, which means that data types are coerced from one tooanother as required.</span></span> <span data-ttu-id="4ad27-322">types de données atomiques Hello dans R incluent numérique, logique et de caractères.</span><span class="sxs-lookup"><span data-stu-id="4ad27-322">hello atomic data types in R include numeric, logical and character.</span></span> <span data-ttu-id="4ad27-323">type de facteur de Hello est toocompactly utilisés stocker des données catégorielles.</span><span class="sxs-lookup"><span data-stu-id="4ad27-323">hello factor type is used toocompactly store categorical data.</span></span> <span data-ttu-id="4ad27-324">Vous trouverez plus d’informations sur les types de données dans les références de hello dans [annexe B - informations supplémentaires](#appendixb).</span><span class="sxs-lookup"><span data-stu-id="4ad27-324">You can find much more information on data types in hello references in [Appendix B - Further reading](#appendixb).</span></span>

<span data-ttu-id="4ad27-325">Lors de la lecture des données tabulaires dans R à partir d’une source externe, il est toujours une bonne idée toocheck hello résultant des types dans les colonnes hello.</span><span class="sxs-lookup"><span data-stu-id="4ad27-325">When tabular data is read into R from an external source, it is always a good idea toocheck hello resulting types in hello columns.</span></span> <span data-ttu-id="4ad27-326">Vous pouvez espérer obtenir une colonne de type caractère, mais dans de nombreux cas, elle se présentera sous forme de facteur ou inversement.</span><span class="sxs-lookup"><span data-stu-id="4ad27-326">You may want a column of type character, but in many cases this will show up as factor or vice versa.</span></span> <span data-ttu-id="4ad27-327">Dans d’autres cas, une colonne qui selon vous devrait être de type numérique pourra être représentée par des données caractères, par exemple, « 1,23 » au lieu du nombre à virgule flottante 1,23.</span><span class="sxs-lookup"><span data-stu-id="4ad27-327">In other cases a column you think should be numeric is represented by character data, e.g. '1.23' rather than 1.23 as a floating point number.</span></span>  

<span data-ttu-id="4ad27-328">Heureusement, il est facile tooconvert un tooanother de type, tant que mappage est possible.</span><span class="sxs-lookup"><span data-stu-id="4ad27-328">Fortunately, it is easy tooconvert one type tooanother, as long as mapping is possible.</span></span> <span data-ttu-id="4ad27-329">Par exemple, vous ne peut pas convertir 'Nevada' en valeur numérique, mais vous pouvez le convertir tooa facteur (variable catégorielle).</span><span class="sxs-lookup"><span data-stu-id="4ad27-329">For example, you cannot convert 'Nevada' into a numeric value, but you can convert it tooa factor (categorical variable).</span></span> <span data-ttu-id="4ad27-330">De même, vous pouvez convertir la valeur numérique 1 en caractère « 1 » ou en facteur.</span><span class="sxs-lookup"><span data-stu-id="4ad27-330">As another example, you can convert a numeric 1 into a character '1' or a factor.</span></span>  

<span data-ttu-id="4ad27-331">syntaxe Hello pour une de ces conversions est simple : `as.datatype()`.</span><span class="sxs-lookup"><span data-stu-id="4ad27-331">hello syntax for any of these conversions is simple: `as.datatype()`.</span></span> <span data-ttu-id="4ad27-332">Ces fonctions de conversion de type hello suivants.</span><span class="sxs-lookup"><span data-stu-id="4ad27-332">These type conversion functions include hello following.</span></span>

* `as.numeric()`
* `as.character()`
* `as.logical()`
* `as.factor()`

<span data-ttu-id="4ad27-333">Examinez les types de données hello des colonnes de hello nous entrées dans la section précédente de hello : toutes les colonnes sont de type numérique, à l’exception de hello intitulé « Mois », qui est de caractère de type.</span><span class="sxs-lookup"><span data-stu-id="4ad27-333">Looking at hello data types of hello columns we input in hello previous section: all columns are of type numeric, except for hello column labeled 'Month', which is of type character.</span></span> <span data-ttu-id="4ad27-334">Nous allons convertir ce facteur tooa et hello résultats des tests.</span><span class="sxs-lookup"><span data-stu-id="4ad27-334">Let's convert this tooa factor and test hello results.</span></span>  

<span data-ttu-id="4ad27-335">J’ai supprimé ligne hello créé hello scatterplot matrice et ajouté une ligne conversion facteur de hello 'Month' colonne tooa.</span><span class="sxs-lookup"><span data-stu-id="4ad27-335">I have deleted hello line that created hello scatterplot matrix and added a line converting hello 'Month' column tooa factor.</span></span> <span data-ttu-id="4ad27-336">Dans mon expérience je sera simplement couper et coller le code de hello R dans la fenêtre de code hello Hello [Execute R Script] [ execute-r-script] Module.</span><span class="sxs-lookup"><span data-stu-id="4ad27-336">In my experiment I will just cut and paste hello R code into hello code window of hello [Execute R Script][execute-r-script] Module.</span></span> <span data-ttu-id="4ad27-337">Vous pouvez également mettre à jour le fichier zip de hello et téléchargez-le tooAzure Machine Learning Studio, mais cette opération prend plusieurs étapes.</span><span class="sxs-lookup"><span data-stu-id="4ad27-337">You could also update hello zip file and upload it tooAzure Machine Learning Studio, but this takes several steps.</span></span>  

    ## Only one of hello following two lines should be used
    ## If running in Machine Learning Studio, use hello first line with maml.mapInputPort()
    ## If in RStudio, use hello second line with read.csv()
    cadairydata <- maml.mapInputPort(1)
    # cadairydata  <- read.csv("cadairydata.csv", header = TRUE, stringsAsFactors = FALSE)
    ## Ensure hello coding is consistent and convert column tooa factor
    cadairydata$Month <- as.factor(cadairydata$Month)
    str(cadairydata) # Check hello result
    ## hello following line should be executed only when running in
    ## Azure Machine Learning Studio
    maml.mapOutputPort('cadairydata')

<span data-ttu-id="4ad27-338">Nous allons exécuter ce code et examinez le journal de sortie hello pour hello script R.</span><span class="sxs-lookup"><span data-stu-id="4ad27-338">Let's execute this code and look at hello output log for hello R script.</span></span> <span data-ttu-id="4ad27-339">Hello les données pertinentes à partir du journal de hello sont indiquées dans la Figure 9.</span><span class="sxs-lookup"><span data-stu-id="4ad27-339">hello relevant data from hello log is shown in Figure 9.</span></span>

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
    [ModuleOutput] [1] "Saving hello following item(s):  .maml.oport1"

<span data-ttu-id="4ad27-340">*Figure 9 : Résumé de la trame de données hello avec une variable de facteur.*</span><span class="sxs-lookup"><span data-stu-id="4ad27-340">*Figure 9. Summary of hello dataframe with a factor variable.*</span></span>

<span data-ttu-id="4ad27-341">type Hello pour le mois doit maintenant indiquer «**facteur avec 14 niveaux**'.</span><span class="sxs-lookup"><span data-stu-id="4ad27-341">hello type for Month should now say '**Factor w/ 14 levels**'.</span></span> <span data-ttu-id="4ad27-342">Il s’agit d’un problème étant donné que les 12 mois dans l’année de hello.</span><span class="sxs-lookup"><span data-stu-id="4ad27-342">This is a problem since there are only 12 months in hello year.</span></span> <span data-ttu-id="4ad27-343">Vous pouvez également vérifier toosee qui hello type dans **visualiser** de jeu de données de résultat de hello port est '**catégorie**'.</span><span class="sxs-lookup"><span data-stu-id="4ad27-343">You can also check toosee that hello type in **Visualize** of hello Result Dataset port is '**Categorical**'.</span></span>

<span data-ttu-id="4ad27-344">problème de Hello est que hello 'Month', colonne n’a pas été codée systématiquement.</span><span class="sxs-lookup"><span data-stu-id="4ad27-344">hello problem is that hello 'Month' column has not been coded systematically.</span></span> <span data-ttu-id="4ad27-345">Le nom du mois sera dans certains cas affiché en toutes lettres (avril) et dans d’autres, il sera abrégé (avr.). Nous pouvons résoudre ce problème par la suppression des caractères de too3 chaîne hello.</span><span class="sxs-lookup"><span data-stu-id="4ad27-345">In some cases a month is called April and in others it is abbreviated as Apr. We can solve this problem by trimming hello string too3 characters.</span></span> <span data-ttu-id="4ad27-346">ligne Hello de code ressemble maintenant à hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="4ad27-346">hello line of code now looks like hello following:</span></span>

    ## Ensure hello coding is consistent and convert column tooa factor
    cadairydata$Month <- as.factor(substr(cadairydata$Month, 1, 3))

<span data-ttu-id="4ad27-347">Réexécutez l’expérience de hello et afficher le journal de sortie hello.</span><span class="sxs-lookup"><span data-stu-id="4ad27-347">Rerun hello experiment and view hello output log.</span></span> <span data-ttu-id="4ad27-348">Hello attendu les résultats s’affichent dans la Figure 10.</span><span class="sxs-lookup"><span data-stu-id="4ad27-348">hello expected results are shown in Figure 10.</span></span>  

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
    [ModuleOutput] [1] "Saving hello following item(s):  .maml.oport1"

<span data-ttu-id="4ad27-349">*Figure 10 : Résumé de la trame de données hello avec le nombre correct de niveaux de facteur.*</span><span class="sxs-lookup"><span data-stu-id="4ad27-349">*Figure 10. Summary of hello dataframe with correct number of factor levels.*</span></span>

<span data-ttu-id="4ad27-350">Notre variable facteur a maintenant hello souhaité 12 niveaux.</span><span class="sxs-lookup"><span data-stu-id="4ad27-350">Our factor variable now has hello desired 12 levels.</span></span>

### <a name="basic-data-frame-filtering"></a><span data-ttu-id="4ad27-351">Filtrage de base des tableaux de données</span><span class="sxs-lookup"><span data-stu-id="4ad27-351">Basic data frame filtering</span></span>
<span data-ttu-id="4ad27-352">Les tableaux de données R prennent en charge des fonctionnalités de filtrage efficaces.</span><span class="sxs-lookup"><span data-stu-id="4ad27-352">R dataframes support powerful filtering capabilities.</span></span> <span data-ttu-id="4ad27-353">Il est possible de créer des sous-ensembles de jeux de données en appliquant des filtres logiques aux lignes ou colonnes.</span><span class="sxs-lookup"><span data-stu-id="4ad27-353">Datasets can be subsetted by using logical filters on either rows or columns.</span></span> <span data-ttu-id="4ad27-354">Dans de nombreux cas, des critères de filtre complexes sont nécessaires.</span><span class="sxs-lookup"><span data-stu-id="4ad27-354">In many cases, complex filter criteria will be required.</span></span> <span data-ttu-id="4ad27-355">références de Hello dans [annexe B - informations supplémentaires](#appendixb) contiennent des exemples détaillés de filtrage des trames de données.</span><span class="sxs-lookup"><span data-stu-id="4ad27-355">hello references in [Appendix B - Further reading](#appendixb) contain extensive examples of filtering dataframes.</span></span>  

<span data-ttu-id="4ad27-356">Notre jeu de données a besoin d'être filtré.</span><span class="sxs-lookup"><span data-stu-id="4ad27-356">There is one bit of filtering we should do on our dataset.</span></span> <span data-ttu-id="4ad27-357">Si vous examinez les colonnes hello dans hello cadairydata trame de données, vous verrez deux colonnes inutiles.</span><span class="sxs-lookup"><span data-stu-id="4ad27-357">If you look at hello columns in hello cadairydata dataframe, you will see two unnecessary columns.</span></span> <span data-ttu-id="4ad27-358">première colonne de Hello conserve uniquement un numéro de ligne, ce qui n’est pas très utile.</span><span class="sxs-lookup"><span data-stu-id="4ad27-358">hello first column just holds a row number, which is not very useful.</span></span> <span data-ttu-id="4ad27-359">deuxième colonne Hello, Year.Month, contienne des informations redondantes.</span><span class="sxs-lookup"><span data-stu-id="4ad27-359">hello second column, Year.Month, contains redundant information.</span></span> <span data-ttu-id="4ad27-360">Nous pouvons facilement exclure ces colonnes à l’aide de hello suivant le code R.</span><span class="sxs-lookup"><span data-stu-id="4ad27-360">We can easily exclude these columns by using hello following R code.</span></span>

> [!NOTE]
> <span data-ttu-id="4ad27-361">À partir de maintenant sur dans cette section, vous montrera simplement vous hello code supplémentaire ajoute Bonjour [Execute R Script] [ execute-r-script] module.</span><span class="sxs-lookup"><span data-stu-id="4ad27-361">From now on in this section, I will just show you hello additional code I am adding in hello [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="4ad27-362">Je vais ajouter chaque nouvelle ligne **avant** hello `str()` (fonction).</span><span class="sxs-lookup"><span data-stu-id="4ad27-362">I will add each new line **before** hello `str()` function.</span></span> <span data-ttu-id="4ad27-363">Utiliser cette fonction tooverify mes résultats dans Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="4ad27-363">I use this function tooverify my results in Azure Machine Learning Studio.</span></span>
> 
> 

<span data-ttu-id="4ad27-364">Ajouter hello après ligne de code toomy R Bonjour [Execute R Script] [ execute-r-script] module.</span><span class="sxs-lookup"><span data-stu-id="4ad27-364">I add hello following line toomy R code in hello [Execute R Script][execute-r-script] module.</span></span>

    # Remove two columns we do not need
    cadairydata <- cadairydata[, c(-1, -2)]

<span data-ttu-id="4ad27-365">Exécutez ce code dans votre expérience et vérifier les résultats hello à partir du journal de sortie hello.</span><span class="sxs-lookup"><span data-stu-id="4ad27-365">Run this code in your experiment and check hello result from hello output log.</span></span> <span data-ttu-id="4ad27-366">Ces résultats sont présentés dans la figure 11.</span><span class="sxs-lookup"><span data-stu-id="4ad27-366">These results are shown in Figure 11.</span></span>

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
    [ModuleOutput] [1] "Saving hello following item(s):  .maml.oport1"

<span data-ttu-id="4ad27-367">*Figure 11 : Résumé de la trame de données hello avec deux colonnes supprimées.*</span><span class="sxs-lookup"><span data-stu-id="4ad27-367">*Figure 11. Summary of hello dataframe with two columns removed.*</span></span>

<span data-ttu-id="4ad27-368">Bonne nouvelle !</span><span class="sxs-lookup"><span data-stu-id="4ad27-368">Good news!</span></span> <span data-ttu-id="4ad27-369">Nous obtenons les résultats hello attendu.</span><span class="sxs-lookup"><span data-stu-id="4ad27-369">We get hello expected results.</span></span>

### <a name="add-a-new-column"></a><span data-ttu-id="4ad27-370">Ajout d'une nouvelle colonne</span><span class="sxs-lookup"><span data-stu-id="4ad27-370">Add a new column</span></span>
<span data-ttu-id="4ad27-371">modèles de série chronologique toocreate, il sera toohave pratique, une colonne contenant hello mois depuis le démarrage de hello de MTS hello.</span><span class="sxs-lookup"><span data-stu-id="4ad27-371">toocreate time series models it will be convenient toohave a column containing hello months since hello start of hello time series.</span></span> <span data-ttu-id="4ad27-372">À cet effet, nous allons créer la colonne « Month.Count ».</span><span class="sxs-lookup"><span data-stu-id="4ad27-372">We will create a new column 'Month.Count'.</span></span>

<span data-ttu-id="4ad27-373">toohelp organiser le code hello nous allons créer notre première fonction simple, `num.month()`.</span><span class="sxs-lookup"><span data-stu-id="4ad27-373">toohelp organize hello code we will create our first simple function, `num.month()`.</span></span> <span data-ttu-id="4ad27-374">Nous allons ensuite appliquer cette fonction de toocreate une nouvelle colonne dans la trame de données hello.</span><span class="sxs-lookup"><span data-stu-id="4ad27-374">We will then apply this function toocreate a new column in hello dataframe.</span></span> <span data-ttu-id="4ad27-375">nouveau code de Hello est comme suit.</span><span class="sxs-lookup"><span data-stu-id="4ad27-375">hello new code is as follows.</span></span>

    ## Create a new column with hello month count
    ## Function toofind hello number of months from hello first
    ## month of hello time series
    num.month <- function(Year, Month) {
      ## Find hello starting year
      min.year  <- min(Year)

      ## Compute hello number of months from hello start of hello time series
      12 * (Year - min.year) + Month - 1
    }

    ## Compute hello new column for hello dataframe
    cadairydata$Month.Count <- num.month(cadairydata$Year, cadairydata$Month.Number)

<span data-ttu-id="4ad27-376">Maintenant, exécutez l’expérience de mise à jour de hello et utiliser hello journal tooview hello un résultat.</span><span class="sxs-lookup"><span data-stu-id="4ad27-376">Now run hello updated experiment and use hello output log tooview hello results.</span></span> <span data-ttu-id="4ad27-377">Ces résultats sont présentés dans la figure 12.</span><span class="sxs-lookup"><span data-stu-id="4ad27-377">These results are shown in Figure 12.</span></span>

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
    [ModuleOutput] [1] "Saving hello following item(s):  .maml.oport1"

<span data-ttu-id="4ad27-378">*Figure 12 : Résumé de la trame de données hello avec une colonne supplémentaire de hello.*</span><span class="sxs-lookup"><span data-stu-id="4ad27-378">*Figure 12. Summary of hello dataframe with hello additional column.*</span></span>

<span data-ttu-id="4ad27-379">Tout semble fonctionner.</span><span class="sxs-lookup"><span data-stu-id="4ad27-379">It looks like everything is working.</span></span> <span data-ttu-id="4ad27-380">Nous avons hello nouvelle colonne avec les valeurs attendues hello dans notre trame de données.</span><span class="sxs-lookup"><span data-stu-id="4ad27-380">We have hello new column with hello expected values in our dataframe.</span></span>

### <a name="value-transformations"></a><span data-ttu-id="4ad27-381">Transformations de valeurs</span><span class="sxs-lookup"><span data-stu-id="4ad27-381">Value transformations</span></span>
<span data-ttu-id="4ad27-382">Dans cette section, nous allons effectuer certaines transformations simples sur les valeurs hello dans certaines colonnes hello de notre trame de données.</span><span class="sxs-lookup"><span data-stu-id="4ad27-382">In this section we will perform some simple transformations on hello values in some of hello columns of our dataframe.</span></span> <span data-ttu-id="4ad27-383">langage de Hello R prend en charge les transformations de valeur presque arbitraire.</span><span class="sxs-lookup"><span data-stu-id="4ad27-383">hello R language supports nearly arbitrary value transformations.</span></span> <span data-ttu-id="4ad27-384">références de Hello dans [annexe B : obtenir des informations supplémentaires](#appendixb) contiennent des exemples détaillés.</span><span class="sxs-lookup"><span data-stu-id="4ad27-384">hello references in [Appendix B - Further Reading](#appendixb) contain extensive examples.</span></span>

<span data-ttu-id="4ad27-385">Si vous examinez les valeurs hello dans des résumés de hello de notre trame de données que vous devez voir quelque chose impair ici.</span><span class="sxs-lookup"><span data-stu-id="4ad27-385">If you look at hello values in hello summaries of our dataframe you should see something odd here.</span></span> <span data-ttu-id="4ad27-386">Par exemple, produit-on vraiment plus de crème glacée que de lait en Californie ?</span><span class="sxs-lookup"><span data-stu-id="4ad27-386">Is more ice cream than milk produced in California?</span></span> <span data-ttu-id="4ad27-387">Non, bien entendu pas, comme cela n’est pas justifiée, sad comme cela peut être toosome nous amoureux de glace.</span><span class="sxs-lookup"><span data-stu-id="4ad27-387">No, of course not, as this makes no sense, sad as this fact may be toosome of us ice cream lovers.</span></span> <span data-ttu-id="4ad27-388">unités de Hello sont différentes.</span><span class="sxs-lookup"><span data-stu-id="4ad27-388">hello units are different.</span></span> <span data-ttu-id="4ad27-389">les prix Hello sont nous exprimée en livres, lait est en unités de 1 million US livres, glace est en unités de 1 000 nous gallons et blanc cheese est exprimé en unités de 1 000 US kg.</span><span class="sxs-lookup"><span data-stu-id="4ad27-389">hello price is in units of US pounds, milk is in units of 1 M US pounds, ice cream is in units of 1,000 US gallons, and cottage cheese is in units of 1,000 US pounds.</span></span> <span data-ttu-id="4ad27-390">En supposant que glace pèse environ 6,5 livres par gallon, nous pouvons facilement hello tooconvert multiplication ces valeurs afin qu’ils soient dans des unités égales de 1 000 euros.</span><span class="sxs-lookup"><span data-stu-id="4ad27-390">Assuming ice cream weighs about 6.5 pounds per gallon, we can easily do hello multiplication tooconvert these values so they are all in equal units of 1,000 pounds.</span></span>

<span data-ttu-id="4ad27-391">Pour notre modèle de prévision, nous utilisons un modèle multiplicatif de façon à ajuster ces données en fonction des variations saisonnières et tendancielles.</span><span class="sxs-lookup"><span data-stu-id="4ad27-391">For our forecasting model we use a multiplicative model for trend and seasonal adjustment of this data.</span></span> <span data-ttu-id="4ad27-392">Une transformation de journal permet de toouse un modèle linéaire, ce qui simplifie ce processus.</span><span class="sxs-lookup"><span data-stu-id="4ad27-392">A log transformation allows us toouse a linear model, simplifying this process.</span></span> <span data-ttu-id="4ad27-393">Nous pouvons appliquer une transformation de journal hello dans hello même fonction où un multiplicateur de hello est appliqué.</span><span class="sxs-lookup"><span data-stu-id="4ad27-393">We can apply hello log transformation in hello same function where hello multiplier is applied.</span></span>

<span data-ttu-id="4ad27-394">Bonjour suivant de code, définir une nouvelle fonction, `log.transform()`et l’appliquer toohello les lignes contenant des valeurs numériques hello.</span><span class="sxs-lookup"><span data-stu-id="4ad27-394">In hello following code, I define a new function, `log.transform()`, and apply it toohello rows containing hello numerical values.</span></span> <span data-ttu-id="4ad27-395">Hello R `Map()` fonction est utilisée tooapply hello `log.transform()` fonction toohello sélectionné des colonnes de la trame de données hello.</span><span class="sxs-lookup"><span data-stu-id="4ad27-395">hello R `Map()` function is used tooapply hello `log.transform()` function toohello selected columns of hello dataframe.</span></span> <span data-ttu-id="4ad27-396">`Map()`est semblable trop`apply()` mais permet plus d’une liste de la fonction de toohello d’arguments.</span><span class="sxs-lookup"><span data-stu-id="4ad27-396">`Map()` is similar too`apply()` but allows for more than one list of arguments toohello function.</span></span> <span data-ttu-id="4ad27-397">Notez qu’une liste des multiplicateurs fournit hello deuxième argument toohello `log.transform()` (fonction).</span><span class="sxs-lookup"><span data-stu-id="4ad27-397">Note that a list of multipliers supplies hello second argument toohello `log.transform()` function.</span></span> <span data-ttu-id="4ad27-398">Hello `na.omit()` fonction est utilisée, un peu de nettoyage tooensure nous n’avons manquant ou des valeurs non définies dans hello trame de données.</span><span class="sxs-lookup"><span data-stu-id="4ad27-398">hello `na.omit()` function is used as a bit of cleanup tooensure we do not have missing or undefined values in hello dataframe.</span></span>

    log.transform <- function(invec, multiplier = 1) {
      ## Function for hello transformation, which is hello log
      ## of hello input value times a multiplier

      warningmessages <- c("ERROR: Non-numeric argument encountered in function log.transform",
                           "ERROR: Arguments toofunction log.transform must be greate than zero",
                           "ERROR: Aggurment multiplier toofuncition log.transform must be a scaler",
                           "ERROR: Invalid time seies value encountered in function log.transform"
                           )

      ## Check hello input arguments
      if(!is.numeric(invec) | !is.numeric(multiplier)) {warning(warningmessages[1]); return(NA)}  
      if(any(invec < 0.0) | any(multiplier < 0.0)) {warning(warningmessages[2]); return(NA)}
      if(length(multiplier) != 1) {{warning(warningmessages[3]); return(NA)}}

      ## Wrap hello multiplication in tryCatch
      ## If there is an exception, print hello warningmessage to
      ## standard error and return NA
      tryCatch(log(multiplier * invec),
               error = function(e){warning(warningmessages[4]); NA})
    }


    ## Apply hello transformation function toohello 4 columns
    ## of hello dataframe with production data
    multipliers  <- list(1.0, 6.5, 1000.0, 1000.0)
    cadairydata[, 4:7] <- Map(log.transform, cadairydata[, 4:7], multipliers)

    ## Get rid of any rows with NA values
    cadairydata <- na.omit(cadairydata)  

<span data-ttu-id="4ad27-399">Il existe un problème de bit Bonjour `log.transform()` (fonction).</span><span class="sxs-lookup"><span data-stu-id="4ad27-399">There is quite a bit happening in hello `log.transform()` function.</span></span> <span data-ttu-id="4ad27-400">La majeure partie de ce code est la vérification des problèmes potentiels avec des arguments de hello ou traiter les exceptions qui peuvent toujours se produire au cours des calculs de hello.</span><span class="sxs-lookup"><span data-stu-id="4ad27-400">Most of this code is checking for potential problems with hello arguments or dealing with exceptions, which can still arise during hello computations.</span></span> <span data-ttu-id="4ad27-401">Uniquement quelques lignes de ce code réellement hello des calculs.</span><span class="sxs-lookup"><span data-stu-id="4ad27-401">Only a few lines of this code actually do hello computations.</span></span>

<span data-ttu-id="4ad27-402">objectif de Hello de la programmation de défense hello est Échec de hello tooprevent d’une fonction unique qui empêche le traitement de continuer.</span><span class="sxs-lookup"><span data-stu-id="4ad27-402">hello goal of hello defensive programming is tooprevent hello failure of a single function that prevents processing from continuing.</span></span> <span data-ttu-id="4ad27-403">L’échec soudain d’une analyse au long cours peut s’avérer très contrariant pour les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="4ad27-403">An abrupt failure of a long-running analysis can be quite frustrating for users.</span></span> <span data-ttu-id="4ad27-404">tooavoid cette situation, par défaut les valeurs de retour doivent être choisis limitera gravement toodownstream traitement.</span><span class="sxs-lookup"><span data-stu-id="4ad27-404">tooavoid this situation, default return values must be chosen that will limit damage toodownstream processing.</span></span> <span data-ttu-id="4ad27-405">Un message est également aux utilisateurs de produits tooalert qui est passé quelque chose incorrect.</span><span class="sxs-lookup"><span data-stu-id="4ad27-405">A message is also produced tooalert users that something has gone wrong.</span></span>

<span data-ttu-id="4ad27-406">Si vous n’êtes pas programmation toodefensive utilisés dans R, ce code peut sembler un peu trop importante.</span><span class="sxs-lookup"><span data-stu-id="4ad27-406">If you are not used toodefensive programming in R, all this code may seem a bit overwhelming.</span></span> <span data-ttu-id="4ad27-407">Je vous guidera à travers les étapes majeures hello :</span><span class="sxs-lookup"><span data-stu-id="4ad27-407">I will walk you through hello major steps:</span></span>

1. <span data-ttu-id="4ad27-408">Un vecteur de quatre messages est défini.</span><span class="sxs-lookup"><span data-stu-id="4ad27-408">A vector of four messages is defined.</span></span> <span data-ttu-id="4ad27-409">Ces messages sont toocommunicate utilisé plus d’informations sur certaines des erreurs possibles de hello et des exceptions qui peuvent se produire avec ce code.</span><span class="sxs-lookup"><span data-stu-id="4ad27-409">These messages are used toocommunicate information about some of hello possible errors and exceptions that can occur with this code.</span></span>
2. <span data-ttu-id="4ad27-410">Dans chaque cas, la valeur NA est renvoyée.</span><span class="sxs-lookup"><span data-stu-id="4ad27-410">I return a value of NA for each case.</span></span> <span data-ttu-id="4ad27-411">Il existe de nombreuses autres possibilités susceptibles de produire moins d’effets secondaires.</span><span class="sxs-lookup"><span data-stu-id="4ad27-411">There are many other possibilities that might have fewer side effects.</span></span> <span data-ttu-id="4ad27-412">Je pourrais retourne un vecteur de zéros ou d’un vecteur d’entrée d’origine de hello, par exemple.</span><span class="sxs-lookup"><span data-stu-id="4ad27-412">I could return a vector of zeroes, or hello original input vector, for example.</span></span>
3. <span data-ttu-id="4ad27-413">Vérifications sont exécutées sur hello arguments toohello (fonction).</span><span class="sxs-lookup"><span data-stu-id="4ad27-413">Checks are run on hello arguments toohello function.</span></span> <span data-ttu-id="4ad27-414">Dans chaque cas, si une erreur est détectée, une valeur par défaut est retournée et un message est généré par hello `warning()` (fonction).</span><span class="sxs-lookup"><span data-stu-id="4ad27-414">In each case, if an error is detected, a default value is returned and a message is produced by hello `warning()` function.</span></span> <span data-ttu-id="4ad27-415">J’utilise `warning()` plutôt que `stop()` comme hello ce dernier mettra fin à l’exécution, exactement ce que j’essaie de tooavoid.</span><span class="sxs-lookup"><span data-stu-id="4ad27-415">I am using `warning()` rather than `stop()` as hello latter will terminate execution, exactly what I am trying tooavoid.</span></span> <span data-ttu-id="4ad27-416">À noter que j'ai écrit ce code dans un style procédural, car dans ce cas, une approche fonctionnelle paraissait complexe et obscure.</span><span class="sxs-lookup"><span data-stu-id="4ad27-416">Note that I have written this code in a procedural style, as in this case a functional approach seemed complex and obscure.</span></span>
4. <span data-ttu-id="4ad27-417">calculs de journal Hello sont encapsulées dans `tryCatch()` afin que les exceptions n’entraîne pas un arrêt brutal de tooprocessing.</span><span class="sxs-lookup"><span data-stu-id="4ad27-417">hello log computations are wrapped in `tryCatch()` so that exceptions will not cause an abrupt halt tooprocessing.</span></span> <span data-ttu-id="4ad27-418">Sans `tryCatch()` , la plupart des erreurs déclenchées par les fonctions R engendrent un signal d’arrêt, qui est suivi d’un arrêt.</span><span class="sxs-lookup"><span data-stu-id="4ad27-418">Without `tryCatch()` most errors raised by R functions result in a stop signal, which does just that.</span></span>

<span data-ttu-id="4ad27-419">Exécutez ce code R dans votre expérience et examiner hello imprimer la sortie dans le fichier du fichier sortie.log hello.</span><span class="sxs-lookup"><span data-stu-id="4ad27-419">Execute this R code in your experiment and have a look at hello printed output in hello output.log file.</span></span> <span data-ttu-id="4ad27-420">Vous voyez maintenant les valeurs hello transformé de hello quatre colonnes hello ouvrir une session, comme indiqué dans la Figure 13.</span><span class="sxs-lookup"><span data-stu-id="4ad27-420">You will now see hello transformed values of hello four columns in hello log, as shown in Figure 13.</span></span>

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
    [ModuleOutput] [1] "Saving hello following item(s):  .maml.oport1"

<span data-ttu-id="4ad27-421">*Figure 13 : Résumé de hello transformés les valeurs dans une trame de données hello.*</span><span class="sxs-lookup"><span data-stu-id="4ad27-421">*Figure 13. Summary of hello transformed values in hello dataframe.*</span></span>

<span data-ttu-id="4ad27-422">Nous constatons que les valeurs hello ont été transformées.</span><span class="sxs-lookup"><span data-stu-id="4ad27-422">We see hello values have been transformed.</span></span> <span data-ttu-id="4ad27-423">À présent, la production de lait dépasse nettement la production de tous les autres produits laitiers, ce qui nous rappelle que nous avons maintenant sous nos yeux une échelle logarithmique.</span><span class="sxs-lookup"><span data-stu-id="4ad27-423">Milk production now greatly exceeds all other dairy product production, recalling that we are now looking at a log scale.</span></span>

<span data-ttu-id="4ad27-424">À ce stade, nos données sont nettoyées et nous sommes prêts à procéder à une modélisation.</span><span class="sxs-lookup"><span data-stu-id="4ad27-424">At this point our data is cleaned up and we are ready for some modeling.</span></span> <span data-ttu-id="4ad27-425">Examinez la visualisation hello pour hello Dataset des résultats de sortie de notre [Execute R Script] [ execute-r-script] module, vous verrez hello 'Month' colonne est « Catégorie » avec des 12 valeurs uniques, à nouveau, tout comme nous le souhaitions .</span><span class="sxs-lookup"><span data-stu-id="4ad27-425">Looking at hello visualization summary for hello Result Dataset output of our [Execute R Script][execute-r-script] module, you will see hello 'Month' column is 'Categorical' with 12 unique values, again, just as we wanted.</span></span>

## <span data-ttu-id="4ad27-426"><a id="timeseries"></a>Objets de série chronologique et analyse des corrélations</span><span class="sxs-lookup"><span data-stu-id="4ad27-426"><a id="timeseries"></a>Time series objects and correlation analysis</span></span>
<span data-ttu-id="4ad27-427">Dans cette section, nous Explorer quelques R temps série d’objets de base et analyser les corrélations hello entre des variables de hello.</span><span class="sxs-lookup"><span data-stu-id="4ad27-427">In this section we will explore a few basic R time series objects and analyze hello correlations between some of hello variables.</span></span> <span data-ttu-id="4ad27-428">Notre objectif est toooutput une trame de données contenant hello par paire de corrélation des informations sur les retards de plusieurs.</span><span class="sxs-lookup"><span data-stu-id="4ad27-428">Our goal is toooutput a dataframe containing hello pairwise correlation information at several lags.</span></span>

<span data-ttu-id="4ad27-429">Hello R code complet pour cette section est dans un fichier zip de hello téléchargé précédemment.</span><span class="sxs-lookup"><span data-stu-id="4ad27-429">hello complete R code for this section is in hello zip file you downloaded earlier.</span></span>

### <a name="time-series-objects-in-r"></a><span data-ttu-id="4ad27-430">Objets de série chronologique en langage R</span><span class="sxs-lookup"><span data-stu-id="4ad27-430">Time series objects in R</span></span>
<span data-ttu-id="4ad27-431">Comme nous l'avons déjà vu, une série chronologique est une série de valeurs de données indexées par le temps.</span><span class="sxs-lookup"><span data-stu-id="4ad27-431">As already mentioned, time series are a series of data values indexed by time.</span></span> <span data-ttu-id="4ad27-432">Objets série au moment de R sont utilisé toocreate et gérer des index de temps hello.</span><span class="sxs-lookup"><span data-stu-id="4ad27-432">R time series objects are used toocreate and manage hello time index.</span></span> <span data-ttu-id="4ad27-433">Il existe plusieurs avantages toousing temps série objets.</span><span class="sxs-lookup"><span data-stu-id="4ad27-433">There are several advantages toousing time series objects.</span></span> <span data-ttu-id="4ad27-434">Objets au moment de série libre à partir de hello nombreux détails de la gestion des valeurs d’index hello temps série qui sont encapsulées dans un objet de hello.</span><span class="sxs-lookup"><span data-stu-id="4ad27-434">Time series objects free you from hello many details of managing hello time series index values that are encapsulated in hello object.</span></span> <span data-ttu-id="4ad27-435">En outre, les objets de série heure permettent hello de toouse vous nombreuses méthodes de série de temps pour le traçage, l’impression, de modélisation, etc..</span><span class="sxs-lookup"><span data-stu-id="4ad27-435">In addition, time series objects allow you toouse hello many time series methods for plotting, printing, modeling, etc.</span></span>

<span data-ttu-id="4ad27-436">Hello classe série au moment de POSIXct est couramment utilisé et est relativement simple.</span><span class="sxs-lookup"><span data-stu-id="4ad27-436">hello POSIXct time series class is commonly used and is relatively simple.</span></span> <span data-ttu-id="4ad27-437">Cette classe série au moment de mesure le temps de démarrer hello d’époque hello, le 1er janvier 1970.</span><span class="sxs-lookup"><span data-stu-id="4ad27-437">This time series class measures time from hello start of hello epoch, January 1, 1970.</span></span> <span data-ttu-id="4ad27-438">Nous utiliserons dans cet exemple des objets de série chronologique POSIXct.</span><span class="sxs-lookup"><span data-stu-id="4ad27-438">We will use POSIXct time series objects in this example.</span></span> <span data-ttu-id="4ad27-439">Parmi les autres classes d'objet de série chronologique R souvent utilisées, citons zoo et xts, qui concernent les séries chronologiques extensibles.</span><span class="sxs-lookup"><span data-stu-id="4ad27-439">Other widely used R time series object classes include zoo and xts, extensible time series.</span></span>
<!-- Additional information on R time series objects is provided in hello references in Section 5.7. [commenting because this section doesn't exist, even in hello original] -->

### <a name="time-series-object-example"></a><span data-ttu-id="4ad27-440">Exemple d’objet de série chronologique</span><span class="sxs-lookup"><span data-stu-id="4ad27-440">Time series object example</span></span>
<span data-ttu-id="4ad27-441">Commençons notre exemple.</span><span class="sxs-lookup"><span data-stu-id="4ad27-441">Let's get started with our example.</span></span> <span data-ttu-id="4ad27-442">Glissez-déplacez un **nouveau** module [d’exécution de script R][execute-r-script] dans votre expérimentation.</span><span class="sxs-lookup"><span data-stu-id="4ad27-442">Drag and drop a **new** [Execute R Script][execute-r-script] module into your experiment.</span></span> <span data-ttu-id="4ad27-443">Connectez le port de sortie de hello Dataset1 du résultat de hello existant [Execute R Script] [ execute-r-script] module toohello Dataset1 d’entrée de port de hello nouvelle [Execute R Script] [ execute-r-script] module.</span><span class="sxs-lookup"><span data-stu-id="4ad27-443">Connect hello Result Dataset1 output port of hello existing [Execute R Script][execute-r-script] module toohello Dataset1 input port of hello new [Execute R Script][execute-r-script] module.</span></span>

<span data-ttu-id="4ad27-444">Comme pour les exemples de première hello, que nous avons sa progression via l’exemple hello, à certains moments, je vais montrer uniquement hello incrémentielle lignes supplémentaires de code R à chaque étape.</span><span class="sxs-lookup"><span data-stu-id="4ad27-444">As I did for hello first examples, as we progress through hello example, at some points I will show only hello incremental additional lines of R code at each step.</span></span>  

#### <a name="reading-hello-dataframe"></a><span data-ttu-id="4ad27-445">Lors de la lecture hello trame de données</span><span class="sxs-lookup"><span data-stu-id="4ad27-445">Reading hello dataframe</span></span>
<span data-ttu-id="4ad27-446">Dans un premier temps, nous allons lire dans une trame de données et assurez-vous que nous obtenons les résultats hello attendu.</span><span class="sxs-lookup"><span data-stu-id="4ad27-446">As a first step, let's read in a dataframe and make sure we get hello expected results.</span></span> <span data-ttu-id="4ad27-447">Hello suivant doit effectuer le travail de hello.</span><span class="sxs-lookup"><span data-stu-id="4ad27-447">hello following code should do hello job.</span></span>

    # Comment hello following if using RStudio
    cadairydata <- maml.mapInputPort(1)
    str(cadairydata) # Check hello results

<span data-ttu-id="4ad27-448">Exécutez maintenant l’expérience de hello.</span><span class="sxs-lookup"><span data-stu-id="4ad27-448">Now, run hello experiment.</span></span> <span data-ttu-id="4ad27-449">journal Hello de forme Execute R Script hello doit ressembler à la Figure 14.</span><span class="sxs-lookup"><span data-stu-id="4ad27-449">hello log of hello new Execute R Script shape should look like Figure 14.</span></span>

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

<span data-ttu-id="4ad27-450">*Figure 14 : Résumé de la trame de données hello dans le module Execute R Script de hello.*</span><span class="sxs-lookup"><span data-stu-id="4ad27-450">*Figure 14. Summary of hello dataframe in hello Execute R Script module.*</span></span>

<span data-ttu-id="4ad27-451">Ces données sont de format et des types de hello attendu.</span><span class="sxs-lookup"><span data-stu-id="4ad27-451">This data is of hello expected types and format.</span></span> <span data-ttu-id="4ad27-452">Notez que hello 'Month' colonne est le facteur de type hello devrait nombre de niveaux.</span><span class="sxs-lookup"><span data-stu-id="4ad27-452">Note that hello 'Month' column is of type factor and has hello expected number of levels.</span></span>

#### <a name="creating-a-time-series-object"></a><span data-ttu-id="4ad27-453">Création d’un objet de série chronologique</span><span class="sxs-lookup"><span data-stu-id="4ad27-453">Creating a time series object</span></span>
<span data-ttu-id="4ad27-454">Nous devons tooadd une trame de données de temps série objet tooour.</span><span class="sxs-lookup"><span data-stu-id="4ad27-454">We need tooadd a time series object tooour dataframe.</span></span> <span data-ttu-id="4ad27-455">Remplacez le code d’en cours de hello avec suivants de hello, qui ajoute une nouvelle colonne de la classe POSIXct.</span><span class="sxs-lookup"><span data-stu-id="4ad27-455">Replace hello current code with hello following, which adds a new column of class POSIXct.</span></span>

    # Comment hello following if using RStudio
    cadairydata <- maml.mapInputPort(1)

    ## Create a new column as a POSIXct object
    Sys.setenv(TZ = "PST8PDT")
    cadairydata$Time <- as.POSIXct(strptime(paste(as.character(cadairydata$Year), "-", as.character(cadairydata$Month.Number), "-01 00:00:00", sep = ""), "%Y-%m-%d %H:%M:%S"))

    str(cadairydata) # Check hello results

<span data-ttu-id="4ad27-456">À présent, vérifiez les journaux hello.</span><span class="sxs-lookup"><span data-stu-id="4ad27-456">Now, check hello log.</span></span> <span data-ttu-id="4ad27-457">Elle doit être similaire à la figure 15.</span><span class="sxs-lookup"><span data-stu-id="4ad27-457">It should look like Figure 15.</span></span>

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

<span data-ttu-id="4ad27-458">*Figure 15 : Résumé de la trame de données hello avec un objet de série de temps.*</span><span class="sxs-lookup"><span data-stu-id="4ad27-458">*Figure 15. Summary of hello dataframe with a time series object.*</span></span>

<span data-ttu-id="4ad27-459">À partir de hello résumé, nous pouvons voir que hello nouvelle colonne est en fait de la classe POSIXct.</span><span class="sxs-lookup"><span data-stu-id="4ad27-459">We can see from hello summary that hello new column is in fact of class POSIXct.</span></span>

### <a name="exploring-and-transforming-hello-data"></a><span data-ttu-id="4ad27-460">Exploration et la transformation des données de hello</span><span class="sxs-lookup"><span data-stu-id="4ad27-460">Exploring and transforming hello data</span></span>
<span data-ttu-id="4ad27-461">Examinons quelques-unes des variables hello dans ce jeu de données.</span><span class="sxs-lookup"><span data-stu-id="4ad27-461">Let's explore some of hello variables in this dataset.</span></span> <span data-ttu-id="4ad27-462">Une matrice scatterplot est un bon moyen de tooproduce un coup de œil rapide.</span><span class="sxs-lookup"><span data-stu-id="4ad27-462">A scatterplot matrix is a good way tooproduce a quick look.</span></span> <span data-ttu-id="4ad27-463">Je suis en remplaçant hello `str()` fonction dans du code R précédente hello avec hello ligne suivante.</span><span class="sxs-lookup"><span data-stu-id="4ad27-463">I am replacing hello `str()` function in hello previous R code with hello following line.</span></span>

    pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = cadairydata, main = "Pairwise Scatterplots of dairy time series")

<span data-ttu-id="4ad27-464">Exécutez ce code et regardez ce qu'il se passe.</span><span class="sxs-lookup"><span data-stu-id="4ad27-464">Run this code and see what happens.</span></span> <span data-ttu-id="4ad27-465">traçage Hello produit en hello port du périphérique R doit ressembler à la Figure 16.</span><span class="sxs-lookup"><span data-stu-id="4ad27-465">hello plot produced at hello R Device port should look like Figure 16.</span></span>

![matrice de nuage de points des variables sélectionnées][17]

<span data-ttu-id="4ad27-467">*Figure 16 : matrice de nuage de points des variables sélectionnées.*</span><span class="sxs-lookup"><span data-stu-id="4ad27-467">*Figure 16. Scatterplot matrix of selected variables.*</span></span>

<span data-ttu-id="4ad27-468">Il est une structure odd-looking dans les relations hello entre ces variables.</span><span class="sxs-lookup"><span data-stu-id="4ad27-468">There is some odd-looking structure in hello relationships between these variables.</span></span> <span data-ttu-id="4ad27-469">Cela se produit peut-être des tendances dans les données de salutation et fait hello que nous n’avons pas normalisés variables de hello.</span><span class="sxs-lookup"><span data-stu-id="4ad27-469">Perhaps this arises from trends in hello data and from hello fact that we have not standardized hello variables.</span></span>

### <a name="correlation-analysis"></a><span data-ttu-id="4ad27-470">Analyse des corrélations</span><span class="sxs-lookup"><span data-stu-id="4ad27-470">Correlation analysis</span></span>
<span data-ttu-id="4ad27-471">analyse de corrélation tooperform nous devons tooboth des tendances et normaliser les variables de hello.</span><span class="sxs-lookup"><span data-stu-id="4ad27-471">tooperform correlation analysis we need tooboth de-trend and standardize hello variables.</span></span> <span data-ttu-id="4ad27-472">Nous avons simplement utiliser hello R `scale()` (fonction), les centres et ajuste les variables.</span><span class="sxs-lookup"><span data-stu-id="4ad27-472">We could simply use hello R `scale()` function, which both centers and scales variables.</span></span> <span data-ttu-id="4ad27-473">D'autant que son exécution peut même s'avérer plus rapide.</span><span class="sxs-lookup"><span data-stu-id="4ad27-473">This function might well run faster.</span></span> <span data-ttu-id="4ad27-474">Toutefois, je veux tooshow vous un exemple de la programmation dans R.</span><span class="sxs-lookup"><span data-stu-id="4ad27-474">However, I want tooshow you an example of defensive programing in R.</span></span>

<span data-ttu-id="4ad27-475">Hello `ts.detrend()` fonction ci-dessous effectue ces deux opérations.</span><span class="sxs-lookup"><span data-stu-id="4ad27-475">hello `ts.detrend()` function shown below performs both of these operations.</span></span> <span data-ttu-id="4ad27-476">Hello deux lignes de code suivantes de tendance déduplication des données de hello et puis normaliser les valeurs hello.</span><span class="sxs-lookup"><span data-stu-id="4ad27-476">hello following two lines of code de-trend hello data and then standardize hello values.</span></span>

    ts.detrend <- function(ts, Time, min.length = 3){
      ## Function toode-trend and standardize a time series

      ## Define some messages if they are NULL  
      messages <- c('ERROR: ts.detrend requires arguments ts and Time toohave hello same length',
                    'ERROR: ts.detrend requires argument ts toobe of type numeric',
                    paste('WARNING: ts.detrend has encountered a time series with length less than', as.character(min.length)),
                    'ERROR: ts.detrend has encountered a Time argument not of class POSIXct',
                    'ERROR: Detrend regression has failed in ts.detrend',
                    'ERROR: Exception occurred in ts.detrend while standardizing time series in function ts.detrend'
      )
      # Create a vector of zeros tooreturn as a default in some cases
      zerovec  <- rep(length(ts), 0.0)

      # hello input arguments are not of hello same length, return ts and quit
      if(length(Time) != length(ts)) {warning(messages[1]); return(ts)}

      # If hello ts is not numeric, just return a zero vector and quit
      if(!is.numeric(ts)) {warning(messages[2]); return(zerovec)}

      # If hello ts is too short, just return it and quit
      if((ts.length <- length(ts)) < min.length) {warning(messages[3]); return(ts)}

      ## Check that hello Time variable is of class POSIXct
      if(class(cadairydata$Time)[[1]] != "POSIXct") {warning(messages[4]); return(ts)}

      ## De-trend hello time series by using a linear model
      ts.frame  <- data.frame(ts = ts, Time = Time)
      tryCatch({ts <- ts - fitted(lm(ts ~ Time, data = ts.frame))},
               error = function(e){warning(messages[5]); zerovec})

      tryCatch( {stdev <- sqrt(sum((ts - mean(ts))^2))/(ts.length - 1)
                 ts <- ts/stdev},
                error = function(e){warning(messages[6]); zerovec})

      ts
    }  
    ## Apply hello detrend.ts function toohello variables of interest
    df.detrend <- data.frame(lapply(cadairydata[, 4:7], ts.detrend, cadairydata$Time))

    ## Plot hello results toolook at hello relationships
    pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = df.detrend, main = "Pairwise Scatterplots of detrended standardized time series")

<span data-ttu-id="4ad27-477">Il existe un problème de bit Bonjour `ts.detrend()` (fonction).</span><span class="sxs-lookup"><span data-stu-id="4ad27-477">There is quite a bit happening in hello `ts.detrend()` function.</span></span> <span data-ttu-id="4ad27-478">La majeure partie de ce code est la vérification des problèmes potentiels avec des arguments de hello ou traiter les exceptions qui peuvent toujours se produire au cours des calculs de hello.</span><span class="sxs-lookup"><span data-stu-id="4ad27-478">Most of this code is checking for potential problems with hello arguments or dealing with exceptions, which can still arise during hello computations.</span></span> <span data-ttu-id="4ad27-479">Uniquement quelques lignes de ce code réellement hello des calculs.</span><span class="sxs-lookup"><span data-stu-id="4ad27-479">Only a few lines of this code actually do hello computations.</span></span>

<span data-ttu-id="4ad27-480">Nous avons déjà vu un exemple de programmation défensive dans la section [Transformations de valeurs](#valuetransformations).</span><span class="sxs-lookup"><span data-stu-id="4ad27-480">We have already discussed an example of defensive programming in [Value transformations](#valuetransformations).</span></span> <span data-ttu-id="4ad27-481">Les deux blocs de calcul sont circonscrits à `tryCatch()`.</span><span class="sxs-lookup"><span data-stu-id="4ad27-481">Both computation blocks are wrapped in `tryCatch()`.</span></span> <span data-ttu-id="4ad27-482">Pour certaines erreurs rend vecteur d’entrée d’origine tooreturn hello sens et dans d’autres cas, retourner un vecteur de zéros.</span><span class="sxs-lookup"><span data-stu-id="4ad27-482">For some errors it makes sense tooreturn hello original input vector, and in other cases, I return a vector of zeros.</span></span>  

<span data-ttu-id="4ad27-483">Notez que la régression linéaire hello utilisée pour annuler l’analyse de tendances est une régression de série de temps.</span><span class="sxs-lookup"><span data-stu-id="4ad27-483">Note that hello linear regression used for de-trending is a time series regression.</span></span> <span data-ttu-id="4ad27-484">variable de PRÉDICTEUR Hello est un objet de série de temps.</span><span class="sxs-lookup"><span data-stu-id="4ad27-484">hello predictor variable is a time series object.</span></span>  

<span data-ttu-id="4ad27-485">Une fois `ts.detrend()` est défini nous s’appliquent variables toohello d’intérêt dans notre trame de données.</span><span class="sxs-lookup"><span data-stu-id="4ad27-485">Once `ts.detrend()` is defined we apply it toohello variables of interest in our dataframe.</span></span> <span data-ttu-id="4ad27-486">Nous devons forcer la liste résultante de hello créé par `lapply()` toodata de trame de données à l’aide de `as.data.frame()`.</span><span class="sxs-lookup"><span data-stu-id="4ad27-486">We must coerce hello resulting list created by `lapply()` toodata dataframe by using `as.data.frame()`.</span></span> <span data-ttu-id="4ad27-487">En raison des aspects défensives de `ts.detrend()`, tooprocess échec une des variables de hello n’empêchera pas corriger le traitement de hello d’autres.</span><span class="sxs-lookup"><span data-stu-id="4ad27-487">Because of defensive aspects of `ts.detrend()`, failure tooprocess one of hello variables will not prevent correct processing of hello others.</span></span>  

<span data-ttu-id="4ad27-488">Hello dernière ligne de code crée un scatterplot par paire.</span><span class="sxs-lookup"><span data-stu-id="4ad27-488">hello final line of code creates a pairwise scatterplot.</span></span> <span data-ttu-id="4ad27-489">Après l’exécution de code de hello R, les résultats de hello de hello scatterplot sont affichés dans la Figure 17.</span><span class="sxs-lookup"><span data-stu-id="4ad27-489">After running hello R code, hello results of hello scatterplot are shown in Figure 17.</span></span>

![nuage de points par paire de la série chronologique après élimination de la tendance et standardisation][18]

<span data-ttu-id="4ad27-491">*Figure 17 : nuage de points par paire de la série chronologique après élimination de la tendance et standardisation.*</span><span class="sxs-lookup"><span data-stu-id="4ad27-491">*Figure 17. Pairwise scatterplot of de-trended and standardized time series.*</span></span>

<span data-ttu-id="4ad27-492">Vous pouvez comparer ces toothose résultats indiqué dans la Figure 16.</span><span class="sxs-lookup"><span data-stu-id="4ad27-492">You can compare these results toothose shown in Figure 16.</span></span> <span data-ttu-id="4ad27-493">Avec hello tendance supprimé et hello variables normalisés, nous constatons beaucoup moins de structure dans les relations entre ces variables hello.</span><span class="sxs-lookup"><span data-stu-id="4ad27-493">With hello trend removed and hello variables standardized, we see a lot less structure in hello relationships between these variables.</span></span>

<span data-ttu-id="4ad27-494">Hello code toocompute hello des corrélations en tant qu’objets de R ccf est comme suit.</span><span class="sxs-lookup"><span data-stu-id="4ad27-494">hello code toocompute hello correlations as R ccf objects is as follows.</span></span>

    ## A function toocompute pairwise correlations from a
    ## list of time series value vectors
    pair.cor <- function(pair.ind, ts.list, lag.max = 1, plot = FALSE){
      ccf(ts.list[[pair.ind[1]]], ts.list[[pair.ind[2]]], lag.max = lag.max, plot = plot)
    }

    ## A list of hello pairwise indices
    corpairs <- list(c(1,2), c(1,3), c(1,4), c(2,3), c(2,4), c(3,4))

    ## Compute hello list of ccf objects
    cadairycorrelations <- lapply(corpairs, pair.cor, df.detrend)  

    cadairycorrelations

<span data-ttu-id="4ad27-495">Exécution de ce code produit journal hello indiqué dans la Figure 18.</span><span class="sxs-lookup"><span data-stu-id="4ad27-495">Running this code produces hello log shown in Figure 18.</span></span>

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

<span data-ttu-id="4ad27-496">*Figure 18 : Liste de ccf objets d’analyse de corrélation par paire hello.*</span><span class="sxs-lookup"><span data-stu-id="4ad27-496">*Figure 18. List of ccf objects from hello pairwise correlation analysis.*</span></span>

<span data-ttu-id="4ad27-497">À chaque décalage correspond une valeur de corrélation.</span><span class="sxs-lookup"><span data-stu-id="4ad27-497">There is a correlation value for each lag.</span></span> <span data-ttu-id="4ad27-498">Aucune de ces valeurs de corrélation est suffisamment grande toobe significatifs.</span><span class="sxs-lookup"><span data-stu-id="4ad27-498">None of these correlation values is large enough toobe significant.</span></span> <span data-ttu-id="4ad27-499">Nous pouvons donc en conclure qu'il est possible de modéliser chaque variable de façon indépendante.</span><span class="sxs-lookup"><span data-stu-id="4ad27-499">We can therefore conclude that we can model each variable independently.</span></span>

### <a name="output-a-dataframe"></a><span data-ttu-id="4ad27-500">Sortie d'un tableau de données</span><span class="sxs-lookup"><span data-stu-id="4ad27-500">Output a dataframe</span></span>
<span data-ttu-id="4ad27-501">Nous avons calculé les corrélations par paire hello sous forme de liste d’objets de R ccf.</span><span class="sxs-lookup"><span data-stu-id="4ad27-501">We have computed hello pairwise correlations as a list of R ccf objects.</span></span> <span data-ttu-id="4ad27-502">Cela pose un bit d’un problème comme port de sortie de jeu de données de résultat de hello nécessite une trame de données.</span><span class="sxs-lookup"><span data-stu-id="4ad27-502">This presents a bit of a problem as hello Result Dataset output port really requires a dataframe.</span></span> <span data-ttu-id="4ad27-503">En outre, objet de ccf hello est lui-même une liste, et nous voulons uniquement les valeurs hello hello premier élément de cette liste, des corrélations hello en hello retards différents.</span><span class="sxs-lookup"><span data-stu-id="4ad27-503">Further, hello ccf object is itself a list and we want only hello values in hello first element of this list, hello correlations at hello various lags.</span></span>

<span data-ttu-id="4ad27-504">Hello suivant liste hello d’objets ccf, qui sont eux-mêmes des listes de valeurs de décalage de code extraits hello.</span><span class="sxs-lookup"><span data-stu-id="4ad27-504">hello following code extracts hello lag values from hello list of ccf objects, which are themselves lists.</span></span>

    df.correlations <- data.frame(do.call(rbind, lapply(cadairycorrelations, '[[', 1)))

    c.names <- c("correlation pair", "-1 lag", "0 lag", "+1 lag")
    r.names  <- c("Corr Cot Cheese - Ice Cream",
                  "Corr Cot Cheese - Milk Prod",
                  "Corr Cot Cheese - Fat Price",
                  "Corr Ice Cream - Mik Prod",
                  "Corr Ice Cream - Fat Price",
                  "Corr Milk Prod - Fat Price")

    ## Build a dataframe with hello row names column and the
    ## correlation data frame and assign hello column names
    outframe <- cbind(r.names, df.correlations)
    colnames(outframe) <- c.names
    outframe


    ## WARNING!
    ## hello following line works only in Azure Machine Learning
    ## When running in RStudio, this code will result in an error
    #maml.mapOutputPort('outframe')

<span data-ttu-id="4ad27-505">Hello première ligne de code est un peu difficile, et une explication peut vous aider à comprendre.</span><span class="sxs-lookup"><span data-stu-id="4ad27-505">hello first line of code is a bit tricky, and some explanation may help you understand it.</span></span> <span data-ttu-id="4ad27-506">Utilisation de hello intérieur/extérieur nous disposer de hello :</span><span class="sxs-lookup"><span data-stu-id="4ad27-506">Working from hello inside out we have hello following:</span></span>

1. <span data-ttu-id="4ad27-507">Hello '**[[**'opérateur avec un argument de hello'**1**' sélectionne hello vecteur de corrélations à des retards de hello de hello premier élément de liste d’objets ccf hello.</span><span class="sxs-lookup"><span data-stu-id="4ad27-507">hello '**[[**' operator with hello argument '**1**' selects hello vector of correlations at hello lags from hello first element of hello ccf object list.</span></span>
2. <span data-ttu-id="4ad27-508">Hello `do.call()` fonction applique hello `rbind()` fonction sur les éléments hello de liste de hello retourne en `lapply()`.</span><span class="sxs-lookup"><span data-stu-id="4ad27-508">hello `do.call()` function applies hello `rbind()` function over hello elements of hello list returns by `lapply()`.</span></span>
3. <span data-ttu-id="4ad27-509">Hello `data.frame()` fonction convertit le résultat hello produit par `do.call()` tooa la trame de données.</span><span class="sxs-lookup"><span data-stu-id="4ad27-509">hello `data.frame()` function coerces hello result produced by `do.call()` tooa dataframe.</span></span>

<span data-ttu-id="4ad27-510">Notez que les noms de lignes hello se trouvent dans une colonne de la trame de données hello.</span><span class="sxs-lookup"><span data-stu-id="4ad27-510">Note that hello row names are in a column of hello dataframe.</span></span> <span data-ttu-id="4ad27-511">Cela permet de conserver les noms de lignes hello lorsqu’ils sont générés à partir de hello [Execute R Script][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="4ad27-511">Doing so preserves hello row names when they are output from hello [Execute R Script][execute-r-script].</span></span>

<span data-ttu-id="4ad27-512">Exécution du code de hello produit une sortie hello indiqué dans la Figure 19 lorsque je **visualiser** hello sortie hello port de jeu de données de résultat.</span><span class="sxs-lookup"><span data-stu-id="4ad27-512">Running hello code produces hello output shown in Figure 19 when I **Visualize** hello output at hello Result Dataset port.</span></span> <span data-ttu-id="4ad27-513">les noms de lignes Hello sont dans la première colonne de hello, comme prévu.</span><span class="sxs-lookup"><span data-stu-id="4ad27-513">hello row names are in hello first column, as intended.</span></span>

![Sortie des résultats d’analyse de corrélation hello][20]

<span data-ttu-id="4ad27-515">*Figure 19 : Résultats de sortie de l’analyse de corrélation hello.*</span><span class="sxs-lookup"><span data-stu-id="4ad27-515">*Figure 19. Results output from hello correlation analysis.*</span></span>

## <span data-ttu-id="4ad27-516"><a id="seasonalforecasting"></a>Exemple de série chronologique : prévision saisonnière</span><span class="sxs-lookup"><span data-stu-id="4ad27-516"><a id="seasonalforecasting"></a>Time series example: seasonal forecasting</span></span>
<span data-ttu-id="4ad27-517">Nos données sont maintenant sous une forme appropriée pour l’analyse, et nous avons déterminé qu'il n’y a aucune corrélation significative entre les variables hello.</span><span class="sxs-lookup"><span data-stu-id="4ad27-517">Our data is now in a form suitable for analysis, and we have determined there are no significant correlations between hello variables.</span></span> <span data-ttu-id="4ad27-518">Continuons et créons un modèle de prévision chronologique.</span><span class="sxs-lookup"><span data-stu-id="4ad27-518">Let's move on and create a time series forecasting model.</span></span> <span data-ttu-id="4ad27-519">À l’aide de ce modèle nous sera prévision de production de lait Californie pour hello 12 mois de 2013.</span><span class="sxs-lookup"><span data-stu-id="4ad27-519">Using this model we will forecast California milk production for hello 12 months of 2013.</span></span>

<span data-ttu-id="4ad27-520">Notre modèle de prévision aura deux composantes : une tendancielle et une saisonnière.</span><span class="sxs-lookup"><span data-stu-id="4ad27-520">Our forecasting model will have two components, a trend component and a seasonal component.</span></span> <span data-ttu-id="4ad27-521">prévision de terminée Hello est produit hello de ces deux composants.</span><span class="sxs-lookup"><span data-stu-id="4ad27-521">hello complete forecast is hello product of these two components.</span></span> <span data-ttu-id="4ad27-522">Ce type de modèle est connu sous le nom de modèle multiplicatif.</span><span class="sxs-lookup"><span data-stu-id="4ad27-522">This type of model is known as a multiplicative model.</span></span> <span data-ttu-id="4ad27-523">alternative de Hello est un modèle additif.</span><span class="sxs-lookup"><span data-stu-id="4ad27-523">hello alternative is an additive model.</span></span> <span data-ttu-id="4ad27-524">Nous avons déjà appliqué un journal transformation toohello les variables d’intérêt, ce qui rend cette analyse souple.</span><span class="sxs-lookup"><span data-stu-id="4ad27-524">We have already applied a log transformation toohello variables of interest, which makes this analysis tractable.</span></span>

<span data-ttu-id="4ad27-525">Hello R code complet pour cette section est dans un fichier zip de hello téléchargé précédemment.</span><span class="sxs-lookup"><span data-stu-id="4ad27-525">hello complete R code for this section is in hello zip file you downloaded earlier.</span></span>

### <a name="creating-hello-dataframe-for-analysis"></a><span data-ttu-id="4ad27-526">Création de hello trame de données pour l’analyse</span><span class="sxs-lookup"><span data-stu-id="4ad27-526">Creating hello dataframe for analysis</span></span>
<span data-ttu-id="4ad27-527">Commencez par ajouter un **nouveau** [Execute R Script] [ execute-r-script] expérience tooyour de module.</span><span class="sxs-lookup"><span data-stu-id="4ad27-527">Start by adding a **new** [Execute R Script][execute-r-script] module tooyour experiment.</span></span> <span data-ttu-id="4ad27-528">Se connecter hello **Dataset des résultats** sortie hello existants [Execute R Script] [ execute-r-script] module toohello **Dataset1** d’entrée du nouveau module de hello.</span><span class="sxs-lookup"><span data-stu-id="4ad27-528">Connect hello **Result Dataset** output of hello existing [Execute R Script][execute-r-script] module toohello **Dataset1** input of hello new module.</span></span> <span data-ttu-id="4ad27-529">résultat de Hello ressemble à la Figure 20.</span><span class="sxs-lookup"><span data-stu-id="4ad27-529">hello result should look something like Figure 20.</span></span>

![Hello faire des essais avec le nouveau module Execute R Script hello d’ajouté][21]

<span data-ttu-id="4ad27-531">*Figure 20. Hello faire des essais avec le nouveau module Execute R Script hello d’ajouté.*</span><span class="sxs-lookup"><span data-stu-id="4ad27-531">*Figure 20. hello experiment with hello new Execute R Script module added.*</span></span>

<span data-ttu-id="4ad27-532">Comme avec l’analyse de corrélation hello que nous vient de se terminer, nous devons tooadd une colonne avec un objet de série heure POSIXct.</span><span class="sxs-lookup"><span data-stu-id="4ad27-532">As with hello correlation analysis we just completed, we need tooadd a column with a POSIXct time series object.</span></span> <span data-ttu-id="4ad27-533">Hello suivant code simplement cette opération.</span><span class="sxs-lookup"><span data-stu-id="4ad27-533">hello following code will do just this.</span></span>

    # If running in Machine Learning Studio, uncomment hello first line with maml.mapInputPort()
    cadairydata <- maml.mapInputPort(1)

    ## Create a new column as a POSIXct object
    Sys.setenv(TZ = "PST8PDT")
    cadairydata$Time <- as.POSIXct(strptime(paste(as.character(cadairydata$Year), "-", as.character(cadairydata$Month.Number), "-01 00:00:00", sep = ""), "%Y-%m-%d %H:%M:%S"))

    str(cadairydata)

<span data-ttu-id="4ad27-534">Exécutez ce code et examinez le journal de hello.</span><span class="sxs-lookup"><span data-stu-id="4ad27-534">Run this code and look at hello log.</span></span> <span data-ttu-id="4ad27-535">résultat de Hello doit ressembler à la Figure 21.</span><span class="sxs-lookup"><span data-stu-id="4ad27-535">hello result should look like Figure 21.</span></span>

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

<span data-ttu-id="4ad27-536">*Figure 21 : Un résumé de la trame de données hello.*</span><span class="sxs-lookup"><span data-stu-id="4ad27-536">*Figure 21. A summary of hello dataframe.*</span></span>

<span data-ttu-id="4ad27-537">Ce résultat, nous sommes prêt toostart notre analyse.</span><span class="sxs-lookup"><span data-stu-id="4ad27-537">With this result, we are ready toostart our analysis.</span></span>

### <a name="create-a-training-dataset"></a><span data-ttu-id="4ad27-538">Création d’un jeu de données d’apprentissage</span><span class="sxs-lookup"><span data-stu-id="4ad27-538">Create a training dataset</span></span>
<span data-ttu-id="4ad27-539">Avec la trame de données hello construit, nous devons toocreate un jeu de données d’apprentissage.</span><span class="sxs-lookup"><span data-stu-id="4ad27-539">With hello dataframe constructed we need toocreate a training dataset.</span></span> <span data-ttu-id="4ad27-540">Ces données incluent tous les observations hello sauf hello 12 dernières, de l’année hello 2013, qui est notre jeu de données de test.</span><span class="sxs-lookup"><span data-stu-id="4ad27-540">This data will include all of hello observations except hello last 12, of hello year 2013, which is our test dataset.</span></span> <span data-ttu-id="4ad27-541">suivante de Hello trame de données hello des sous-ensembles de code et crée des graphiques, des variables de production et le prix laitières hello.</span><span class="sxs-lookup"><span data-stu-id="4ad27-541">hello following code subsets hello dataframe and creates plots of hello dairy production and price variables.</span></span> <span data-ttu-id="4ad27-542">Puis créer les graphiques de hello quatre variables de production et le prix.</span><span class="sxs-lookup"><span data-stu-id="4ad27-542">I then create plots of hello four production and price variables.</span></span> <span data-ttu-id="4ad27-543">Une fonction anonyme est utilisé toodefine certains renforce pour le traçage et ensuite parcourir liste hello Hello deux autres arguments avec `Map()`.</span><span class="sxs-lookup"><span data-stu-id="4ad27-543">An anonymous function is used toodefine some augments for plot, and then iterate over hello list of hello other two arguments with `Map()`.</span></span> <span data-ttu-id="4ad27-544">Vous vous dites peut-être qu'une boucle for aurait ici fait l'affaire.</span><span class="sxs-lookup"><span data-stu-id="4ad27-544">If you are thinking that a for loop would have worked fine here, you are correct.</span></span> <span data-ttu-id="4ad27-545">Vous avez raison, mais comme le langage R est un langage fonctionnel, je vous montre une approche fonctionnelle.</span><span class="sxs-lookup"><span data-stu-id="4ad27-545">But, since R is a functional language I am showing you a functional approach.</span></span>

    cadairytrain <- cadairydata[1:216, ]

    Ylabs  <- list("Log CA Cotage Cheese Production, 1000s lb",
                   "Log CA Ice Cream Production, 1000s lb",
                   "Log CA Milk Production 1000s lb",
                   "Log North CA Milk Milk Fat Price per 1000 lb")

    Map(function(y, Ylabs){plot(cadairytrain$Time, y, xlab = "Time", ylab = Ylabs, type = "l")}, cadairytrain[, 4:7], Ylabs)

<span data-ttu-id="4ad27-546">Exécution du code de hello produit hello trace les séries de série chronologique de sortie de périphérique R hello indiqué dans la Figure 22.</span><span class="sxs-lookup"><span data-stu-id="4ad27-546">Running hello code produces hello series of time series plots from hello R Device output shown in Figure 22.</span></span> <span data-ttu-id="4ad27-547">Notez qu’axe du temps hello est exprimé en unités de dates, des avantages de temps hello série tracer la méthode.</span><span class="sxs-lookup"><span data-stu-id="4ad27-547">Note that hello time axis is in units of dates, a nice benefit of hello time series plot method.</span></span>

![premier graphique chronologique des données de production et de prix des produits laitiers californiens](./media/machine-learning-r-quickstart/unnamed-chunk-161.png)

![deuxième graphique chronologique des données de production et de prix des produits laitiers californiens](./media/machine-learning-r-quickstart/unnamed-chunk-162.png)

![troisième graphique chronologique des données de production et de prix des produits laitiers californiens](./media/machine-learning-r-quickstart/unnamed-chunk-163.png)

![quatrième graphique chronologique des données de production et de prix des produits laitiers californiens](./media/machine-learning-r-quickstart/unnamed-chunk-164.png)

<span data-ttu-id="4ad27-552">*Figure 22 : graphiques chronologiques des données de production et de prix des produits laitiers californiens.*</span><span class="sxs-lookup"><span data-stu-id="4ad27-552">*Figure 22. Time series plots of California dairy production and price data.*</span></span>

### <a name="a-trend-model"></a><span data-ttu-id="4ad27-553">Modèle de tendance</span><span class="sxs-lookup"><span data-stu-id="4ad27-553">A trend model</span></span>
<span data-ttu-id="4ad27-554">Après avoir créé un objet de série de temps et avoir examiné les données de salutation, nous pouvons commencer tooconstruct un modèle de tendance pour hello données de production de lait California.</span><span class="sxs-lookup"><span data-stu-id="4ad27-554">Having created a time series object and having had a look at hello data, let's start tooconstruct a trend model for hello California milk production data.</span></span> <span data-ttu-id="4ad27-555">Pour cela, nous pouvons utiliser une régression chronologique.</span><span class="sxs-lookup"><span data-stu-id="4ad27-555">We can do this with a time series regression.</span></span> <span data-ttu-id="4ad27-556">Toutefois, il est clair à partir de traçage de hello que nous allons peut-être plus d’un tooaccurately pente et l’ordonnée à l’origine modéliser hello observé les tendances dans les données d’apprentissage hello.</span><span class="sxs-lookup"><span data-stu-id="4ad27-556">However, it is clear from hello plot that we will need more than a slope and intercept tooaccurately model hello observed trend in hello training data.</span></span>

<span data-ttu-id="4ad27-557">Donné à petite échelle de hello de données de hello, je générera modèle hello pour tendance dans RStudio et puis couper et coller le modèle résultant de hello dans Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="4ad27-557">Given hello small scale of hello data, I will build hello model for trend in RStudio and then cut and paste hello resulting model into Azure Machine Learning.</span></span> <span data-ttu-id="4ad27-558">RStudio offre un environnement interactif pour ce type d'analyse interactive.</span><span class="sxs-lookup"><span data-stu-id="4ad27-558">RStudio provides an interactive environment for this type of interactive analysis.</span></span>

<span data-ttu-id="4ad27-559">Comme une première tentative, je vais essayer une régression polynomiale avec too3 sous tension.</span><span class="sxs-lookup"><span data-stu-id="4ad27-559">As a first attempt, I will try a polynomial regression with powers up too3.</span></span> <span data-ttu-id="4ad27-560">Il existe un risque réel de surapprentissage de ces types de modèles.</span><span class="sxs-lookup"><span data-stu-id="4ad27-560">There is a real danger of over-fitting these kinds of models.</span></span> <span data-ttu-id="4ad27-561">Par conséquent, il est de meilleures conditions d’ordre haut tooavoid.</span><span class="sxs-lookup"><span data-stu-id="4ad27-561">Therefore, it is best tooavoid high order terms.</span></span> <span data-ttu-id="4ad27-562">Hello `I()` fonction empêche l’interprétation du contenu de hello (interprète contenu hello « en l’état ») et vous permet de toowrite une fonction interprétée littéralement dans une équation de régression.</span><span class="sxs-lookup"><span data-stu-id="4ad27-562">hello `I()` function inhibits interpretation of hello contents (interprets hello contents 'as is') and allows you toowrite a literally interpreted function in a regression equation.</span></span>

    milk.lm <- lm(Milk.Prod ~ Time + I(Month.Count^2) + I(Month.Count^3), data = cadairytrain)
    summary(milk.lm)

<span data-ttu-id="4ad27-563">Cette opération génère suivant de hello.</span><span class="sxs-lookup"><span data-stu-id="4ad27-563">This generates hello following.</span></span>

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

<span data-ttu-id="4ad27-564">À partir des valeurs de P (Pr (> | t |)) dans cette sortie, nous pouvons voir que hello terme quadratique peut ne pas être significative.</span><span class="sxs-lookup"><span data-stu-id="4ad27-564">From P values (Pr(>|t|)) in this output, we can see that hello squared term may not be significant.</span></span> <span data-ttu-id="4ad27-565">Vous allez utiliser hello `update()` toomodify ce modèle en supprimant hello carré terme de fonction.</span><span class="sxs-lookup"><span data-stu-id="4ad27-565">I will use hello `update()` function toomodify this model by dropping hello squared term.</span></span>

    milk.lm <- update(milk.lm, . ~ . - I(Month.Count^2))
    summary(milk.lm)

<span data-ttu-id="4ad27-566">Cette opération génère suivant de hello.</span><span class="sxs-lookup"><span data-stu-id="4ad27-566">This generates hello following.</span></span>

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

<span data-ttu-id="4ad27-567">Cela semble mieux.</span><span class="sxs-lookup"><span data-stu-id="4ad27-567">This looks better.</span></span> <span data-ttu-id="4ad27-568">Tous les termes du contrat de hello sont significatifs.</span><span class="sxs-lookup"><span data-stu-id="4ad27-568">All of hello terms are significant.</span></span> <span data-ttu-id="4ad27-569">Toutefois, hello 2e-16 valeur est la valeur par défaut et ne doit pas être prise trop gravement.</span><span class="sxs-lookup"><span data-stu-id="4ad27-569">However, hello 2e-16 value is a default value, and should not be taken too seriously.</span></span>  

<span data-ttu-id="4ad27-570">Qu’un test de validité, nous allons en créer un tracé de série heure de données de production laitière Californie de hello avec courbe de tendance hello indiqué.</span><span class="sxs-lookup"><span data-stu-id="4ad27-570">As a sanity test, let's make a time series plot of hello California dairy production data with hello trend curve shown.</span></span> <span data-ttu-id="4ad27-571">J’ai ajouté hello suivant code Bonjour Azure Machine Learning [Execute R Script] [ execute-r-script] toocreate de modèle (pas RStudio) hello modèle et effectuer un traçage.</span><span class="sxs-lookup"><span data-stu-id="4ad27-571">I have added hello following code in hello Azure Machine Learning [Execute R Script][execute-r-script] model (not RStudio) toocreate hello model and make a plot.</span></span> <span data-ttu-id="4ad27-572">résultat de Hello est illustré dans la Figure 23.</span><span class="sxs-lookup"><span data-stu-id="4ad27-572">hello result is shown in Figure 23.</span></span>

    milk.lm <- lm(Milk.Prod ~ Time + I(Month.Count^3), data = cadairytrain)

    plot(cadairytrain$Time, cadairytrain$Milk.Prod, xlab = "Time", ylab = "Log CA Milk Production 1000s lb", type = "l")
    lines(cadairytrain$Time, predict(milk.lm, cadairytrain), lty = 2, col = 2)

![données de production laitière californienne avec affichage du modèle de tendance](./media/machine-learning-r-quickstart/unnamed-chunk-18.png)

<span data-ttu-id="4ad27-574">*Figure 23 : données de production laitière californienne avec affichage du modèle de tendance.*</span><span class="sxs-lookup"><span data-stu-id="4ad27-574">*Figure 23. California milk production data with trend model shown.*</span></span>

<span data-ttu-id="4ad27-575">Il semble que le modèle de tendance hello le mieux aux données de hello assez bien.</span><span class="sxs-lookup"><span data-stu-id="4ad27-575">It looks like hello trend model fits hello data fairly well.</span></span> <span data-ttu-id="4ad27-576">En outre, il ne semble pas preuve toobe de surapprentissage, telles qu’impair tremble dans la courbe du modèle hello.</span><span class="sxs-lookup"><span data-stu-id="4ad27-576">Further, there does not seem toobe evidence of over-fitting, such as odd wiggles in hello model curve.</span></span>  

### <a name="seasonal-model"></a><span data-ttu-id="4ad27-577">Modèle saisonnier</span><span class="sxs-lookup"><span data-stu-id="4ad27-577">Seasonal model</span></span>
<span data-ttu-id="4ad27-578">Avec un modèle de tendance dans main, nous devez toopush sur et inclure des effets saisonniers hello.</span><span class="sxs-lookup"><span data-stu-id="4ad27-578">With a trend model in hand, we need toopush on and include hello seasonal effects.</span></span> <span data-ttu-id="4ad27-579">Nous allons utiliser mois hello d’année de hello comme une variable factice en vigueur de hello modèle linéaire toocapture hello mois par mois.</span><span class="sxs-lookup"><span data-stu-id="4ad27-579">We will use hello month of hello year as a dummy variable in hello linear model toocapture hello month-by-month effect.</span></span> <span data-ttu-id="4ad27-580">Notez que lorsque vous introduisez des variables de facteur dans un modèle, intercept de hello ne doit pas être calculée.</span><span class="sxs-lookup"><span data-stu-id="4ad27-580">Note that when you introduce factor variables into a model, hello intercept must not be computed.</span></span> <span data-ttu-id="4ad27-581">Si vous ne le faites pas, formule de hello est spécifié de manière excessive et R entraînera l’abandon d’un des hello souhaité facteurs en conservant terme d’interception hello.</span><span class="sxs-lookup"><span data-stu-id="4ad27-581">If you do not do this, hello formula is over-specified and R will drop one of hello desired factors but keep hello intercept term.</span></span>

<span data-ttu-id="4ad27-582">Étant donné que nous disposons d’un modèle de tendance satisfaisante, nous pouvons utiliser hello `update()` hello de tooadd fonction nouveau modèle existant de toohello des termes du contrat.</span><span class="sxs-lookup"><span data-stu-id="4ad27-582">Since we have a satisfactory trend model we can use hello `update()` function tooadd hello new terms toohello existing model.</span></span> <span data-ttu-id="4ad27-583">Hello -1 dans la formule de mise à jour hello supprime le terme d’interception hello.</span><span class="sxs-lookup"><span data-stu-id="4ad27-583">hello -1 in hello update formula drops hello intercept term.</span></span> <span data-ttu-id="4ad27-584">Pour le moment de hello pour poursuivre dans RStudio :</span><span class="sxs-lookup"><span data-stu-id="4ad27-584">Continuing in RStudio for hello moment:</span></span>

    milk.lm2 <- update(milk.lm, . ~ . + Month - 1)
    summary(milk.lm2)

<span data-ttu-id="4ad27-585">Cette opération génère suivant de hello.</span><span class="sxs-lookup"><span data-stu-id="4ad27-585">This generates hello following.</span></span>

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

<span data-ttu-id="4ad27-586">Nous voyons ce modèle hello a un terme d’interception ne sont plus et présente des facteurs significatifs mois 12.</span><span class="sxs-lookup"><span data-stu-id="4ad27-586">We see that hello model no longer has an intercept term and has 12 significant month factors.</span></span> <span data-ttu-id="4ad27-587">C’est exactement ce que nous voulions toosee.</span><span class="sxs-lookup"><span data-stu-id="4ad27-587">This is exactly what we wanted toosee.</span></span>

<span data-ttu-id="4ad27-588">Nous allons en créer un autre tracé de série de temps de hello Californie production laitière données toosee degré modèle saisonnières de hello fonctionne.</span><span class="sxs-lookup"><span data-stu-id="4ad27-588">Let's make another time series plot of hello California dairy production data toosee how well hello seasonal model is working.</span></span> <span data-ttu-id="4ad27-589">J’ai ajouté hello suivant code Bonjour Azure Machine Learning [Execute R Script] [ execute-r-script] toocreate hello modèle et effectuer un traçage.</span><span class="sxs-lookup"><span data-stu-id="4ad27-589">I have added hello following code in hello Azure Machine Learning [Execute R Script][execute-r-script] toocreate hello model and make a plot.</span></span>

    milk.lm2 <- lm(Milk.Prod ~ Time + I(Month.Count^3) + Month - 1, data = cadairytrain)

    plot(cadairytrain$Time, cadairytrain$Milk.Prod, xlab = "Time", ylab = "Log CA Milk Production 1000s lb", type = "l")
    lines(cadairytrain$Time, predict(milk.lm2, cadairytrain), lty = 2, col = 2)

<span data-ttu-id="4ad27-590">Ce code en cours d’exécution dans Azure Machine Learning produit traçage hello illustré Figure 24.</span><span class="sxs-lookup"><span data-stu-id="4ad27-590">Running this code in Azure Machine Learning produces hello plot shown in Figure 24.</span></span>

![production laitière californienne avec le modèle incluant les effets saisonniers](./media/machine-learning-r-quickstart/unnamed-chunk-20.png)

<span data-ttu-id="4ad27-592">*Figure 24 : production laitière californienne avec le modèle incluant les effets saisonniers.*</span><span class="sxs-lookup"><span data-stu-id="4ad27-592">*Figure 24. California milk production with model including seasonal effects.*</span></span>

<span data-ttu-id="4ad27-593">Hello données adaptée toohello illustrées Figure 24 sont plutôt encourageants.</span><span class="sxs-lookup"><span data-stu-id="4ad27-593">hello fit toohello data shown in Figure 24 is rather encouraging.</span></span> <span data-ttu-id="4ad27-594">Tendance de hello et effet saisonnières de hello (variation mensuelle) semblent correctes.</span><span class="sxs-lookup"><span data-stu-id="4ad27-594">Both hello trend and hello seasonal effect (monthly variation) look reasonable.</span></span>

<span data-ttu-id="4ad27-595">En tant qu’une autre vérification de notre modèle, nous allons avez résiduels de hello.</span><span class="sxs-lookup"><span data-stu-id="4ad27-595">As another check on our model, let's have a look at hello residuals.</span></span> <span data-ttu-id="4ad27-596">Hello expression suivante calcule le code hello valeurs prédites entre nos deux modèles, calcule la moyenne des résiduels hello pour les modèles saisonnières hello et puis trace ces résiduels pour les données d’apprentissage hello.</span><span class="sxs-lookup"><span data-stu-id="4ad27-596">hello following code computes hello predicted values from our two models, computes hello residuals for hello seasonal model, and then plots these residuals for hello training data.</span></span>

    ## Compute predictions from our models
    predict1  <- predict(milk.lm, cadairydata)
    predict2  <- predict(milk.lm2, cadairydata)

    ## Compute and plot hello residuals
    residuals <- cadairydata$Milk.Prod - predict2
    plot(cadairytrain$Time, residuals[1:216], xlab = "Time", ylab ="Residuals of Seasonal Model")

<span data-ttu-id="4ad27-597">traçage de résiduelles Hello est illustrée dans la Figure 25.</span><span class="sxs-lookup"><span data-stu-id="4ad27-597">hello residual plot is shown in Figure 25.</span></span>

![Moyenne des résiduels du modèle de saisonnières hello pour les données d’apprentissage hello](./media/machine-learning-r-quickstart/unnamed-chunk-21.png)

<span data-ttu-id="4ad27-599">*Figure 25 : Résiduels du modèle de saisonnières hello pour les données d’apprentissage hello.*</span><span class="sxs-lookup"><span data-stu-id="4ad27-599">*Figure 25. Residuals of hello seasonal model for hello training data.*</span></span>

<span data-ttu-id="4ad27-600">Ces résidus semblent corrects.</span><span class="sxs-lookup"><span data-stu-id="4ad27-600">These residuals look reasonable.</span></span> <span data-ttu-id="4ad27-601">Il n’existe aucune structure particulière, à l’exception d’effet hello de crise hello 2008-2009, qui ne compte pas notre modèle particulièrement bien.</span><span class="sxs-lookup"><span data-stu-id="4ad27-601">There is no particular structure, except hello effect of hello 2008-2009 recession, which our model does not account for particularly well.</span></span>

<span data-ttu-id="4ad27-602">traçage Hello indiqué dans la Figure 25 est utile pour détecter des modèles dépendant du temps dans la moyenne des résiduels hello.</span><span class="sxs-lookup"><span data-stu-id="4ad27-602">hello plot shown in Figure 25 is useful for detecting any time-dependent patterns in hello residuals.</span></span> <span data-ttu-id="4ad27-603">approche explicite de Hello de calcul et le traçage des résiduels hello que j’ai utilisé place résiduels de hello dans un ordre chronologique sur de traçage hello.</span><span class="sxs-lookup"><span data-stu-id="4ad27-603">hello explicit approach of computing and plotting hello residuals I used places hello residuals in time order on hello plot.</span></span> <span data-ttu-id="4ad27-604">Si, sur hello autre part, j’avais tracées `milk.lm$residuals`, traçage de hello n’aurait pas été dans un ordre chronologique.</span><span class="sxs-lookup"><span data-stu-id="4ad27-604">If, on hello other hand, I had plotted `milk.lm$residuals`, hello plot would not have been in time order.</span></span>

<span data-ttu-id="4ad27-605">Vous pouvez également utiliser `plot.lm()` tooproduce une série de graphiques de diagnostic.</span><span class="sxs-lookup"><span data-stu-id="4ad27-605">You can also use `plot.lm()` tooproduce a series of diagnostic plots.</span></span>

    ## Show hello diagnostic plots for hello model
    plot(milk.lm2, ask = FALSE)

<span data-ttu-id="4ad27-606">Ce code génère une série de graphiques de diagnostic représentés dans la figure 26.</span><span class="sxs-lookup"><span data-stu-id="4ad27-606">This code produces a series of diagnostic plots shown in Figure 26.</span></span>

![Premier des graphiques de diagnostic pour le modèle saisonnières de hello](./media/machine-learning-r-quickstart/unnamed-chunk-221.png)

![Seconde de graphiques de diagnostic pour le modèle de saisonnières de hello](./media/machine-learning-r-quickstart/unnamed-chunk-222.png)

![Troisième des graphiques de diagnostic pour le modèle saisonnières de hello](./media/machine-learning-r-quickstart/unnamed-chunk-223.png)

![Quatrième des graphiques de diagnostic pour le modèle saisonnières de hello](./media/machine-learning-r-quickstart/unnamed-chunk-224.png)

<span data-ttu-id="4ad27-611">*Figure 26 : Trace de diagnostic pour le modèle saisonnières de hello.*</span><span class="sxs-lookup"><span data-stu-id="4ad27-611">*Figure 26. Diagnostic plots for hello seasonal model.*</span></span>

<span data-ttu-id="4ad27-612">Il existe quelques points hautement influents identifiées dans ces graphiques, mais aucune toocause une préoccupation importante.</span><span class="sxs-lookup"><span data-stu-id="4ad27-612">There are a few highly influential points identified in these plots, but nothing toocause great concern.</span></span> <span data-ttu-id="4ad27-613">En outre, nous constatons à partir de traçage Normal Q-Q hello que moyenne des résiduels hello sont toonormally fermer distribuée, une hypothèse importante pour les modèles linéaires.</span><span class="sxs-lookup"><span data-stu-id="4ad27-613">Further, we can see from hello Normal Q-Q plot that hello residuals are close toonormally distributed, an important assumption for linear models.</span></span>

### <a name="forecasting-and-model-evaluation"></a><span data-ttu-id="4ad27-614">Prévision et évaluation des modèles</span><span class="sxs-lookup"><span data-stu-id="4ad27-614">Forecasting and model evaluation</span></span>
<span data-ttu-id="4ad27-615">Il existe qu’un seul toocomplete de toodo chose plus notre exemple.</span><span class="sxs-lookup"><span data-stu-id="4ad27-615">There is just one more thing toodo toocomplete our example.</span></span> <span data-ttu-id="4ad27-616">Nous devez toocompute prévisions et mesurer l’erreur de hello par rapport aux données réelles de hello.</span><span class="sxs-lookup"><span data-stu-id="4ad27-616">We need toocompute forecasts and measure hello error against hello actual data.</span></span> <span data-ttu-id="4ad27-617">Nos prévisions seront pour hello 12 mois de 2013.</span><span class="sxs-lookup"><span data-stu-id="4ad27-617">Our forecast will be for hello 12 months of 2013.</span></span> <span data-ttu-id="4ad27-618">Nous pouvons calculer une mesure de l’erreur pour cette prévision toohello les données qui ne fait pas partie de notre jeu de données d’apprentissage.</span><span class="sxs-lookup"><span data-stu-id="4ad27-618">We can compute an error measure for this forecast toohello actual data that is not part of our training dataset.</span></span> <span data-ttu-id="4ad27-619">En outre, nous pouvons comparer les performances sur hello toohello des données d’apprentissage de 18 ans 12 mois de données de test.</span><span class="sxs-lookup"><span data-stu-id="4ad27-619">Additionally, we can compare performance on hello 18 years of training data toohello 12 months of test data.</span></span>  

<span data-ttu-id="4ad27-620">Servent d’un nombre de mesures de performances de hello toomeasure de modèles de série chronologique.</span><span class="sxs-lookup"><span data-stu-id="4ad27-620">A number of metrics are used toomeasure hello performance of time series models.</span></span> <span data-ttu-id="4ad27-621">Dans le cas présent, nous allons utiliser erreur du carré moyen de racine (RMS) hello.</span><span class="sxs-lookup"><span data-stu-id="4ad27-621">In our case we will use hello root mean square (RMS) error.</span></span> <span data-ttu-id="4ad27-622">Hello fonction suivante calcule erreur hello RMS entre deux séries.</span><span class="sxs-lookup"><span data-stu-id="4ad27-622">hello following function computes hello RMS error between two series.</span></span>  

    RMS.error <- function(series1, series2, is.log = TRUE, min.length = 2){
      ## Function toocompute hello RMS error or difference between two
      ## series or vectors

      messages <- c("ERROR: Input arguments toofunction RMS.error of wrong type encountered",
                    "ERROR: Input vector toofunction RMS.error is too short",
                    "ERROR: Input vectors toofunction RMS.error must be of same length",
                    "WARNING: Funtion rms.error has received invald input time series.")

      ## Check hello arguments
      if(!is.numeric(series1) | !is.numeric(series2) | !is.logical(is.log) | !is.numeric(min.length)) {
        warning(messages[1])
        return(NA)}

      if(length(series1) < min.length) {
        warning(messages[2])
        return(NA)}

      if((length(series1) != length(series2))) {
           warning(messages[3])
        return(NA)}

      ## If is.log is TRUE exponentiate hello values, else just copy
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

    ## Compute hello RMS error in a dataframe
      tryCatch( {
        sqrt(sum((temp1 - temp2)^2) / length(temp1))},
        error = function(e){warning(messages[4]); NA})
    }

<span data-ttu-id="4ad27-623">Comme avec hello `log.transform()` fonction évoqué dans hello « Valeur transformations » de section, il y a beaucoup de code erreur exception et de la vérification de la récupération dans cette fonction.</span><span class="sxs-lookup"><span data-stu-id="4ad27-623">As with hello `log.transform()` function we discussed in hello "Value transformations" section, there is quite a lot of error checking and exception recovery code in this function.</span></span> <span data-ttu-id="4ad27-624">principes de Hello employés sont hello même.</span><span class="sxs-lookup"><span data-stu-id="4ad27-624">hello principles employed are hello same.</span></span> <span data-ttu-id="4ad27-625">travail Hello est effectué dans deux emplacements encapsulés dans `tryCatch()`.</span><span class="sxs-lookup"><span data-stu-id="4ad27-625">hello work is done in two places wrapped in `tryCatch()`.</span></span> <span data-ttu-id="4ad27-626">Tout d’abord, MTS hello sont exponentiated, étant donné que nous avons travaillé avec des journaux de hello des valeurs de hello.</span><span class="sxs-lookup"><span data-stu-id="4ad27-626">First, hello time series are exponentiated, since we have been working with hello logs of hello values.</span></span> <span data-ttu-id="4ad27-627">En second lieu, l’erreur RMS hello est calculée.</span><span class="sxs-lookup"><span data-stu-id="4ad27-627">Second, hello actual RMS error is computed.</span></span>  

<span data-ttu-id="4ad27-628">Équipé d’un Bonjour toomeasure de fonction erreur RMS, nous allons générer et de sortie une trame de données contenant des erreurs de hello RMS.</span><span class="sxs-lookup"><span data-stu-id="4ad27-628">Equipped with a function toomeasure hello RMS error, let's build and output a dataframe containing hello RMS errors.</span></span> <span data-ttu-id="4ad27-629">Nous inclut les termes du contrat pour le modèle de tendance hello seul et le modèle complet de hello avec facteurs saisonniers.</span><span class="sxs-lookup"><span data-stu-id="4ad27-629">We will include terms for hello trend model alone and hello complete model with seasonal factors.</span></span> <span data-ttu-id="4ad27-630">Hello de code suivant hello travail à l’aide de modèles linéaires deux hello que nous avons construit.</span><span class="sxs-lookup"><span data-stu-id="4ad27-630">hello following code does hello job by using hello two linear models we have constructed.</span></span>

    ## Compute hello RMS error in a dataframe
    ## Include hello row names in hello first column so they will
    ## appear in hello output of hello Execute R Script
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

    ## hello following line should be executed only when running in
    ## Azure Machine Learning Studio
    maml.mapOutputPort('RMS.df')

<span data-ttu-id="4ad27-631">Exécution de ce code de produit la sortie de hello indiqué dans la Figure 27 au port de sortie de jeu de données de résultat de hello.</span><span class="sxs-lookup"><span data-stu-id="4ad27-631">Running this code produces hello output shown in Figure 27 at hello Result Dataset output port.</span></span>

![Comparaison des erreurs de RMS pour les modèles de hello][26]

<span data-ttu-id="4ad27-633">*Figure 27 : Comparaison des erreurs de RMS pour les modèles hello.*</span><span class="sxs-lookup"><span data-stu-id="4ad27-633">*Figure 27. Comparison of RMS errors for hello models.*</span></span>

<span data-ttu-id="4ad27-634">À partir de ces résultats, nous constatons que l’ajout hello facteurs saisonniers toohello modèle réduit erreur de RMS hello considérablement.</span><span class="sxs-lookup"><span data-stu-id="4ad27-634">From these results, we see that adding hello seasonal factors toohello model reduces hello RMS error significantly.</span></span> <span data-ttu-id="4ad27-635">Pas trop étonnamment, erreur hello RMS pour les données d’apprentissage de hello est un bit inférieur à pour hello prévisions.</span><span class="sxs-lookup"><span data-stu-id="4ad27-635">Not too surprisingly, hello RMS error for hello training data is a bit less than for hello forecast.</span></span>

## <span data-ttu-id="4ad27-636"><a id="appendixa"></a>ANNEXE a : Guide tooRStudio</span><span class="sxs-lookup"><span data-stu-id="4ad27-636"><a id="appendixa"></a>APPENDIX A: Guide tooRStudio</span></span>
<span data-ttu-id="4ad27-637">RStudio est très bien documenté, dans cette annexe je fournirai certaines toohello de liens des sections spécifiques de hello RStudio documentation tooget que vous avez démarré.</span><span class="sxs-lookup"><span data-stu-id="4ad27-637">RStudio is quite well documented, so in this appendix I will provide some links toohello key sections of hello RStudio documentation tooget you started.</span></span>

1. <span data-ttu-id="4ad27-638">Création de projets</span><span class="sxs-lookup"><span data-stu-id="4ad27-638">Creating projects</span></span>
   
   <span data-ttu-id="4ad27-639">Vous pouvez organiser et gérer votre code R dans les projets à l’aide de RStudio.</span><span class="sxs-lookup"><span data-stu-id="4ad27-639">You can organize and manage your R code into projects by using RStudio.</span></span> <span data-ttu-id="4ad27-640">Vous trouverez la documentation Hello qui utilise des projets à https://support.rstudio.com/hc/articles/200526207-Using-Projects.</span><span class="sxs-lookup"><span data-stu-id="4ad27-640">hello documentation that uses projects can be found at https://support.rstudio.com/hc/articles/200526207-Using-Projects.</span></span>
   
   <span data-ttu-id="4ad27-641">Je vous recommande de suivre ces instructions et de créer un projet pour des exemples de code hello R dans ce document.</span><span class="sxs-lookup"><span data-stu-id="4ad27-641">I recommend that you follow these directions and create a project for hello R code examples in this document.</span></span>  
2. <span data-ttu-id="4ad27-642">Modification et exécution de code R</span><span class="sxs-lookup"><span data-stu-id="4ad27-642">Editing and executing R code</span></span>
   
   <span data-ttu-id="4ad27-643">RStudio offre un environnement intégré qui permet de modifier et d'exécuter du code R.</span><span class="sxs-lookup"><span data-stu-id="4ad27-643">RStudio provides an integrated environment for editing and executing R code.</span></span> <span data-ttu-id="4ad27-644">Vous trouverez la documentation à l’adresse https://support.rstudio.com/hc/articles/200484448-Editing-and-Executing-Code.</span><span class="sxs-lookup"><span data-stu-id="4ad27-644">Documentation can be found at https://support.rstudio.com/hc/articles/200484448-Editing-and-Executing-Code.</span></span>
3. <span data-ttu-id="4ad27-645">Débogage</span><span class="sxs-lookup"><span data-stu-id="4ad27-645">Debugging</span></span>
   
   <span data-ttu-id="4ad27-646">RStudio intègre de puissantes fonctionnalités de débogage.</span><span class="sxs-lookup"><span data-stu-id="4ad27-646">RStudio includes powerful debugging capabilities.</span></span> <span data-ttu-id="4ad27-647">Vous trouverez la documentation relative à ces fonctionnalités à l’adresse https://support.rstudio.com/hc/articles/200713843-Debugging-with-RStudio.</span><span class="sxs-lookup"><span data-stu-id="4ad27-647">Documentation for these features is at https://support.rstudio.com/hc/articles/200713843-Debugging-with-RStudio.</span></span>
   
   <span data-ttu-id="4ad27-648">les fonctionnalités de dépannage de point d’arrêt Hello sont documentées dans https://support.rstudio.com/hc/articles/200534337-Breakpoint-Troubleshooting.</span><span class="sxs-lookup"><span data-stu-id="4ad27-648">hello breakpoint troubleshooting features are documented at https://support.rstudio.com/hc/articles/200534337-Breakpoint-Troubleshooting.</span></span>

## <span data-ttu-id="4ad27-649"><a id="appendixb"></a>ANNEXE B : informations supplémentaires</span><span class="sxs-lookup"><span data-stu-id="4ad27-649"><a id="appendixb"></a>APPENDIX B: Further reading</span></span>
<span data-ttu-id="4ad27-650">Cette R programmation didacticiel couvre hello de ce que vous avez besoin de toouse hello langage R avec Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="4ad27-650">This R programming tutorial covers hello basics of what you need toouse hello R language with Azure Machine Learning Studio.</span></span> <span data-ttu-id="4ad27-651">Si vous ne connaissez pas le langage R, deux présentations sont disponibles sur le site CRAN :</span><span class="sxs-lookup"><span data-stu-id="4ad27-651">If you are not familiar with R, two introductions are available on CRAN:</span></span>

* <span data-ttu-id="4ad27-652">R pour les débutants par Emmanuel Paradis est un toostart parfait à http://cran.r-project.org/doc/contrib/Paradis-rdebuts_en.pdf.</span><span class="sxs-lookup"><span data-stu-id="4ad27-652">R for Beginners by Emmanuel Paradis is a good place toostart at http://cran.r-project.org/doc/contrib/Paradis-rdebuts_en.pdf.</span></span>  
* <span data-ttu-id="4ad27-653">Un tooR Introduction par W. N.</span><span class="sxs-lookup"><span data-stu-id="4ad27-653">An Introduction tooR by W. N.</span></span> <span data-ttu-id="4ad27-654">Venables, et</span><span class="sxs-lookup"><span data-stu-id="4ad27-654">Venables et.</span></span> <span data-ttu-id="4ad27-655">al.</span><span class="sxs-lookup"><span data-stu-id="4ad27-655">al.</span></span> <span data-ttu-id="4ad27-656">approfondit un peu le sujet : http://cran.r-project.org/doc/manuals/R-intro.html.</span><span class="sxs-lookup"><span data-stu-id="4ad27-656">goes into a bit more depth, at http://cran.r-project.org/doc/manuals/R-intro.html.</span></span>

<span data-ttu-id="4ad27-657">Il existe de nombreux livres sur le langage R qui peuvent vous aider à vous lancer.</span><span class="sxs-lookup"><span data-stu-id="4ad27-657">There are many books on R that can help you get started.</span></span> <span data-ttu-id="4ad27-658">En voici quelques-uns que j'ai trouvés utiles :</span><span class="sxs-lookup"><span data-stu-id="4ad27-658">Here are a few I find useful:</span></span>

* <span data-ttu-id="4ad27-659">Hello Art de programmation de R : une visite guidée de statistique conception de logiciels par Norman Matloff est un tooprogramming excellente introduction dans R.</span><span class="sxs-lookup"><span data-stu-id="4ad27-659">hello Art of R Programming: A Tour of Statistical Software Design by Norman Matloff is an excellent introduction tooprogramming in R.</span></span>  
* <span data-ttu-id="4ad27-660">Livre de recettes R par Paul Teetor fournit une approche problème et solution toousing R.</span><span class="sxs-lookup"><span data-stu-id="4ad27-660">R Cookbook by Paul Teetor provides a problem and solution approach toousing R.</span></span>  
* <span data-ttu-id="4ad27-661">« R in Action » de Robert Kabacoff est un autre ouvrage introductif utile.</span><span class="sxs-lookup"><span data-stu-id="4ad27-661">R in Action by Robert Kabacoff is another useful introductory book.</span></span> <span data-ttu-id="4ad27-662">site Web de Hello accompagnement R rapide est une ressource utile à http://www.statmethods.net/.</span><span class="sxs-lookup"><span data-stu-id="4ad27-662">hello companion Quick R website is a useful resource at http://www.statmethods.net/.</span></span>
* <span data-ttu-id="4ad27-663">Inferno R par Patrick Burns est un livre étonnamment humoristique qui négocie avec un nombre de rubriques complexe et difficiles qui peuvent être rencontrés lors de la programmation dans le livre de r. hello est disponible gratuitement sur http://www.burns-stat.com/documents/books/the-r-inferno/.</span><span class="sxs-lookup"><span data-stu-id="4ad27-663">R Inferno by Patrick Burns is a surprisingly humorous book that deals with a number of tricky and difficult topics that can be encountered when programming in R. hello book is available for free at http://www.burns-stat.com/documents/books/the-r-inferno/.</span></span>
* <span data-ttu-id="4ad27-664">Si vous souhaitez une présentation approfondie de rubriques avancées dans R, jetez un œil au livre de hello avancé R par Hadley Wickham.</span><span class="sxs-lookup"><span data-stu-id="4ad27-664">If you want a deep dive into advanced topics in R, have a look at hello book Advanced R by Hadley Wickham.</span></span> <span data-ttu-id="4ad27-665">version en ligne de Hello de cette documentation est disponible gratuitement à http://adv-r.had.co.nz/.</span><span class="sxs-lookup"><span data-stu-id="4ad27-665">hello online version of this book is available for free at http://adv-r.had.co.nz/.</span></span>

<span data-ttu-id="4ad27-666">Un catalogue de packages de série de temps R se trouvent dans hello CRAN affichage de la tâche d’analyse de série chronologique : http://cran.r-project.org/web/views/TimeSeries.html.</span><span class="sxs-lookup"><span data-stu-id="4ad27-666">A catalogue of R time series packages can be found in hello CRAN Task View for time series analysis: http://cran.r-project.org/web/views/TimeSeries.html.</span></span> <span data-ttu-id="4ad27-667">Pour plus d’informations sur les packages d’objet série de temps spécifique, vous devez consultez la documentation de toohello pour ce package.</span><span class="sxs-lookup"><span data-stu-id="4ad27-667">For information on specific time series object packages, you should refer toohello documentation for that package.</span></span>

<span data-ttu-id="4ad27-668">Hello carnet d’introduction de série chronologique avec R par Paul Cowpertwait et Andrew Metcalfe fournit une introduction de toousing R pour l’analyse de série chronologique.</span><span class="sxs-lookup"><span data-stu-id="4ad27-668">hello book Introductory Time Series with R by Paul Cowpertwait and Andrew Metcalfe provides an introduction toousing R for time series analysis.</span></span> <span data-ttu-id="4ad27-669">Divers textes théoriques proposent des exemples R.</span><span class="sxs-lookup"><span data-stu-id="4ad27-669">Many more theoretical texts provide R examples.</span></span>

<span data-ttu-id="4ad27-670">Quelques ressources Internet particulièrement utiles :</span><span class="sxs-lookup"><span data-stu-id="4ad27-670">Some great internet resources:</span></span>

* <span data-ttu-id="4ad27-671">DataCamp : DataCamp enseigne R dans le confort de hello de votre navigateur avec des leçons vidéos et des exercices de codage.</span><span class="sxs-lookup"><span data-stu-id="4ad27-671">DataCamp: DataCamp teaches R in hello comfort of your browser with video lessons and coding exercises.</span></span> <span data-ttu-id="4ad27-672">Il existe des didacticiels interactifs sur les techniques de R hello plus récentes et les packages.</span><span class="sxs-lookup"><span data-stu-id="4ad27-672">There are interactive tutorials on hello latest R techniques and packages.</span></span> <span data-ttu-id="4ad27-673">Suivez hello libre interactive R didacticiel consacré à https://www.datacamp.com/courses/introduction-to-r</span><span class="sxs-lookup"><span data-stu-id="4ad27-673">Take hello free interactive R tutorial at https://www.datacamp.com/courses/introduction-to-r</span></span>
* <span data-ttu-id="4ad27-674">Guide de prise en main de R à partir de Programiz https://www.programiz.com/r-programming</span><span class="sxs-lookup"><span data-stu-id="4ad27-674">A guide on Getting started with R from Programiz https://www.programiz.com/r-programming</span></span>
* <span data-ttu-id="4ad27-675">Un bref didacticiel sur le langage R par Kelly Black de l’Université de Clarkson : http://www.cyclismo.org/tutorial/R/</span><span class="sxs-lookup"><span data-stu-id="4ad27-675">A quick R tutorial by Kelly Black from Clarkson University http://www.cyclismo.org/tutorial/R/</span></span>
* <span data-ttu-id="4ad27-676">Plus de 60 ressources sur le langage R : http://www.computerworld.com/article/2497464/business-intelligence-60-r-resources-to-improve-your-data-skills.html</span><span class="sxs-lookup"><span data-stu-id="4ad27-676">60+ R resources listed at http://www.computerworld.com/article/2497464/business-intelligence-60-r-resources-to-improve-your-data-skills.html</span></span>

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
