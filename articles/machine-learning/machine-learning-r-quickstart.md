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
# <a name="quickstart-tutorial-for-hello-r-programming-language-for-azure-machine-learning"></a>Didacticiel de démarrage rapide pour le langage de programmation hello R pour Azure Machine Learning

<!-- Stephen F Elston, Ph.D. -->

## <a name="introduction"></a>Introduction
Ce didacticiel de démarrage rapide vous permet de commencer rapidement l’extension Azure Machine Learning à l’aide du langage de programmation hello R. Suivez ce didacticiel toocreate de programmation de R, tester et exécuter le code R dans Azure Machine Learning. Lorsque vous travaillez dans le didacticiel, vous allez créer une solution complète de prévision à l’aide du langage de hello R dans Azure Machine Learning.  

Si Microsoft Azure Machine Learning intègre divers modules d’apprentissage automatique et de manipulation de données très efficaces, puissant langage R de Hello a été décrite comme hello langue véhiculaire d’analytique. Heureusement, la manipulation des données et d’analytique dans Azure Machine Learning peut être étendue à l’aide de R. Cette combinaison offre l’évolutivité de hello et faciliter le déploiement d’Azure Machine Learning avec une grande souplesse hello et analytique approfondie de R.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

### <a name="forecasting-and-hello-dataset"></a>Jeu de données de prévision et hello
La prévision est une méthode analytique largement répandue et très utile. Plage de prédire les ventes saisonnières d’éléments de, déterminer les niveaux de stock optimaux, les variables macroéconomiques toopredicting d’utilisations courantes. La prévision s'appuie généralement sur des modèles chronologiques.

Données de série chronologique sont données dans laquelle les valeurs hello ont un index de temps. index de temps Hello peut être normal, par exemple, tous les mois ou chaque minute, ou irréguliers. Un modèle chronologique repose sur des données chronologiques. langage de programmation Hello R contient un cadre souple et l’analytique très bien pour les données de série chronologique.

Dans ce guide de démarrage rapide, nous allons utiliser les données de production et de tarification des produits laitiers en Californie. Ces données incluent tous les mois d’informations sur la production hello de plusieurs produits laitiers et prix hello des matières grasses, un produit d’évaluation.

Hello les données utilisées dans cet article, ainsi que des scripts R, peuvent être [téléchargé ici][download]. Ces données a été initialement synthétisées à partir des informations disponibles à partir de hello Université de Wisconsin à http://future.aae.wisc.edu/tab/production.html.

### <a name="organization"></a>Organisation
Nous traiterons à travers plusieurs étapes comme vous apprendre comment toocreate, tester et exécuter du code de manipulation R analytique et les données dans un environnement d’Azure Machine Learning hello.  

* Tout d’abord, nous allons examiner les bases de hello de l’utilisation de la langue de hello R dans l’environnement d’Azure Machine Learning Studio hello.
* Puis nous avançons toodiscussing divers aspects d’e/s de données, de code R et de graphiques dans l’environnement d’Azure Machine Learning hello.
* Nous allons ensuite construire hello première partie de notre solution prévision en créant le code de nettoyage des données et la transformation.
* Avec nos données préparées, nous allons effectuer une analyse de corrélations hello entre plusieurs variables hello dans notre jeu de données.
* Enfin, nous créerons un modèle de prévision chronologique saisonnier pour la production de lait.

## <a id="mlstudio"></a>Interaction avec le langage R dans Machine Learning Studio
Cette section présente les notions de base de l’interaction avec le langage de programmation hello R dans un environnement de Machine Learning Studio hello. langue de Hello R fournit un outil puissant toocreate personnalisé analytique et les données manipulation modules au sein de l’environnement d’Azure Machine Learning hello.

Je vais utiliser RStudio toodevelop, tester et déboguer du code R à petite échelle. Ce code est puis couper et coller dans un [Execute R Script] [ execute-r-script] module toorun prêt de Machine Learning Studio.  

### <a name="hello-execute-r-script-module"></a>module Execute R Script de Hello
Au sein de la Machine Learning Studio, les scripts R sont exécutés au sein de hello [Execute R Script] [ execute-r-script] module. Un exemple de hello [Execute R Script] [ execute-r-script] module dans Machine Learning Studio est indiqué dans la Figure 1.

 ![Langage de programmation de R : module Execute R Script hello dans Machine Learning Studio][1]

*Figure 1. environnement de Machine Learning Studio Hello montrant le module Execute R Script de hello sélectionné.*

Référence tooFigure 1, examinons certains des éléments clés de hello d’environnement de Machine Learning Studio hello pour travailler avec hello [Execute R Script] [ execute-r-script] module.

* modules Hello dans expérience de hello sont affichés dans le volet central de hello.
* Hello partie supérieure droite hello contient une fenêtre tooview et modifier vos scripts R.  
* partie inférieure de Hello du volet de droite montre certaines propriétés de hello [Execute R Script][execute-r-script]. Vous pouvez afficher les journaux d’erreur et de sortie de hello en cliquant sur l’endroit approprié de hello de ce volet.

Nous, bien entendu, aborderons hello [Execute R Script] [ execute-r-script] plus en détail dans le reste de hello de ce document.

Lorsqu'il s'agit d'utiliser des fonctions R complexes, je vous recommande de modifier, tester et déboguer dans RStudio. Comme pour tout projet de développement logiciel, développez votre code graduellement et testez-le dans un petit cas de test simple. Coupez et collez vos fonctions dans la fenêtre de script hello R Hello [Execute R Script] [ execute-r-script] module. Cette approche permet de vous tooharness hello RStudio, environnement de développement intégré (IDE) et hello puissance d’Azure Machine Learning.  

#### <a name="execute-r-code"></a>Exécution du code R
Tout code hello R [Execute R Script] [ execute-r-script] module s’exécute lorsque vous exécutez hello expérience en cliquant sur hello **exécuter** bouton. Une fois l’exécution terminée, une coche s’affiche sur hello [Execute R Script] [ execute-r-script] icône.

#### <a name="defensive-r-coding-for-azure-machine-learning"></a>Codage R défensif pour Azure Machine Learning
Si vous développez du code R pour, par exemple, un service Web à l’aide d’Azure Machine Learning, vous devez absolument prévoir la façon dont votre code traitera une entrée de données inattendue et les exceptions. toomaintain plus de clarté, je n'ai pas inclus une grande partie de façon hello de la vérification ou la gestion des exceptions dans la plupart des exemples de code hello indiqués. Cependant, je vous montrerai par la suite plusieurs exemples de fonctions qui font appel à la fonctionnalité de gestion des exceptions du langage R.  

Si vous avez besoin d’un traitement plus complète de gestion des exceptions de R, je vous conseillons de lire sections appropriées hello livre hello Wickham répertorié dans [annexe B : obtenir des informations supplémentaires](#appendixb).

#### <a name="debug-and-test-r-in-machine-learning-studio"></a>Débogage et test du langage R dans Machine Learning Studio
tooreiterate, je vous recommande de tester et de déboguer votre code R à petite échelle dans RStudio. Toutefois, il existe des cas où vous devez tootrack les problèmes de code R Bonjour [Execute R Script] [ execute-r-script] lui-même. En outre, il est conseillé toocheck vos résultats dans Machine Learning Studio.

Sortie de l’exécution de hello de votre code R et sur la plateforme Azure Machine Learning de hello se trouve principalement dans le fichier sortie.log. Vous pourrez trouver des informations complémentaires dans le fichier error.log.  

Si une erreur se produit dans Machine Learning Studio lors de l’exécution de votre code R, votre premier plan d’action doit être toolook à error.log. Ce fichier peut contenir toohelp de messages d’erreur utiles comprendre et de corriger votre erreur. tooview error.log, cliquez sur **afficher le journal d’erreur** sur hello **volet Propriétés** pour hello [Execute R Script] [ execute-r-script] contenant hello erreur.

Par exemple, j’ai exécuté hello suit le code R, avec une variable non définie y dans une [Execute R Script] [ execute-r-script] module :

    x <- 1.0
    z <- x + y

Ce code échoue tooexecute, ce qui entraîne une condition d’erreur. En cliquant sur **afficher le journal d’erreur** sur hello **volet Propriétés** produit hello affichage indiqué dans la Figure 2.

  ![fenêtre contextuelle de message d’erreur][2]

*Figure 2 : fenêtre contextuelle de message d’erreur.*

Il semble que nous devons toolook dans le message d’erreur de fichier sortie.log toosee hello R. Cliquez sur hello [Execute R Script] [ execute-r-script] , puis cliquez sur hello **afficher le fichier sortie.log** élément sur hello **volet Propriétés** toohello droite. Une nouvelle fenêtre de navigateur s’ouvre, et je voir hello.

    [Critical]     Error: Error 0063: hello following error occurred during evaluation of R script:
    ---------- Start of error message from R ----------
    object 'y' not found


    object 'y' not found
    ----------- End of error message from R -----------

Ce message d’erreur ne contient aucuns surprises et identifie clairement le problème de hello.

valeur de hello tooinspect de n’importe quel objet dans R, vous pouvez imprimer le fichier fichier sortie.log toohello de ces valeurs. règles Hello pour examiner l’objet les valeurs sont essentiellement même hello comme dans une session interactive de R. Par exemple, si vous tapez un nom de variable sur une ligne, valeur hello d’objet de hello sera imprimé toohello fichier sortie.log fichier.  

#### <a name="packages-in-machine-learning-studio"></a>Packages dans Azure Machine Learning Studio
Azure Machine Learning est fourni avec plus de 350 packages de langage R préinstallés. Vous pouvez utiliser hello suivant code Bonjour [Execute R Script] [ execute-r-script] module tooretrieve une liste de hello préinstallé packages.

    data.set <- data.frame(installed.packages())
    maml.mapOutputPort("data.set")

Si vous ne comprenez pas hello dernière ligne de ce code au moment de hello, lisez la suite. Dans le reste de hello de ce document, nous aborderons largement à l’aide de R dans l’environnement d’Azure Machine Learning hello.

### <a name="introduction-toorstudio"></a>Introduction tooRStudio
RStudio est un IDE largement utilisée pour R. Je vais utiliser RStudio pour modification, de test et de débogage de code hello R utilisés dans ce guide de démarrage rapide. Une fois que le code R est testé et prêt, vous simplement couper et coller à partir de l’éditeur RStudio hello dans une Machine Learning Studio [Execute R Script] [ execute-r-script] module.  

Si vous n’avez pas de langage de programmation hello R installé sur votre ordinateur de bureau, je vous recommande de le que faire maintenant. Téléchargements gratuits de langage R open source sont disponibles à hello réseau de Archive complète R (CRAN) à [http://www.r-project.org/](http://www.r-project.org/). Il existe des versions Windows, Mac OS et Linux/UNIX. Choisissez un miroir à proximité et suivez les instructions de téléchargement hello. Par ailleurs, le section CRAN contient de nombreux packages d'analyse et de manipulation de données fort utiles.

Si vous êtes tooRStudio nouveau, vous téléchargez et installez la version de bureau hello. Vous pouvez trouver hello que rstudio télécharge pour Windows, Mac OS et Linux/UNIX à http://www.rstudio.com/products/RStudio/. Suivez les instructions hello tooinstall RStudio sur votre ordinateur de bureau.  

Un tooRStudio introduction au didacticiel est disponible à l’adresse https://support.rstudio.com/hc/sections/200107586-Using-RStudio.

Vous trouverez des informations complémentaires sur l’utilisation de RStudio dans [l’Annexe A][appendixa].  

## <a id="scriptmodule"></a>Obtenir des données vers et depuis le module Execute R Script de hello
Dans cette section, nous aborderons comment d’obtenir des données dans et hors hello [Execute R Script] [ execute-r-script] module. Nous allons examiner comment toohandle différents types de données lues dans et hors hello [Execute R Script] [ execute-r-script] module.

code complet de Hello pour cette section est dans un fichier zip de hello téléchargé précédemment.

### <a name="load-and-check-data-in-machine-learning-studio"></a>Chargement et vérification des données dans Machine Learning Studio
#### <a id="loading"></a>Jeu de données charge hello
Nous allons commencer en chargeant hello **csdairydata.csv** fichier dans Azure Machine Learning Studio.

* Démarrez votre environnement Azure Machine Learning Studio.
* Cliquez sur **+ nouveau** à hello bas à gauche de votre écran, puis sélectionnez **Dataset**.
* Sélectionnez **à partir d’un fichier Local**, puis **Parcourir** fichier hello de tooselect.
* Vérifiez que vous avez sélectionné **fichier CSV générique avec l’en-tête (.csv)** en tant que type hello pour hello le jeu de données.
* Cliquez sur case à cocher hello.
* Après hello dataset a été téléchargé, vous devez voir hello le nouveau jeu de données en cliquant sur hello **Datasets** onglet.  

#### <a name="create-an-experiment"></a>Création d'une expérience
Maintenant que nous avons des données dans Machine Learning Studio, nous devons toocreate une analyse de hello toodo expérience.  

* Cliquez sur **+ nouveau** à hello coin inférieur gauche et sélectionnez **expérience**, puis **expérience vide**.
* Vous pouvez nommer votre expérience en sélectionnant et en modification, hello **expérience créé sur...**  titre en hello haut hello. Par exemple, la modification trop**autorité de certification laiterie analyse**.
* Sur la gauche hello de page d’expérience hello, développez **jeux de données enregistrés**, puis **mes Datasets**. Vous devez voir hello **cadairydata.csv** que vous avez téléchargé précédemment.
* Glisser- déposer hello **csdairydata.csv dataset** sur l’expérience de hello.
* Bonjour **recherche expérimenter éléments** zone en haut de hello du volet gauche hello, type [Execute R Script][execute-r-script]. Module de hello s’affiche dans la liste de recherche hello.
* Glisser- déposer hello [Execute R Script] [ execute-r-script] module sur votre palette.  
* Connectez la sortie hello Hello **csdairydata.csv dataset** entrée à l’extrême gauche de toohello (**Dataset1**) de hello [Execute R Script][execute-r-script].
* **N’oubliez pas tooclick sur « Enregistrer ».**  

À ce stade, votre expérimentation doit être similaire à la figure 3.

![Hello autorité de certification laiterie analyse faire des essais avec le jeu de données et le module Execute R Script][3]

*La figure 3. Hello autorité de certification laiterie analyse faire des essais avec le jeu de données et le module Execute R Script.*

#### <a name="check-on-hello-data"></a>Vérifier les données de salutation
Nous allons avoir un aspect des données hello que nous avons chargé dans notre expérience. Dans l’expérience hello, cliquez sur sortie hello Hello **cadairydata.csv dataset** et sélectionnez **visualiser**. Vous obtenez un résultat analogue à la figure 4.  

![Résumé du jeu de données hello cadairydata.csv][4]

*Figure 4 : Résumé du jeu de données cadairydata.csv hello.*

Cette vue contient de nombreuses informations utiles. Nous pouvons voir hello première plusieurs lignes du jeu de données. Si vous sélectionnez une colonne, hello section des statistiques s’affiche plus d’informations sur la colonne de hello. Par exemple, ligne du Type de fonctionnalité hello montre quels types de données Azure Machine Learning Studio affecté toohello colonne. Un coup de œil rapide à ceci est un contrôle de validité correct avant de commencer à n’importe quel travail grave toodo.

### <a name="first-r-script"></a>Premier script R
Nous allons créer une simple tooexperiment de script R première avec dans Azure Machine Learning Studio. J’ai créé et testé hello script dans RStudio suivant.  

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

J’ai besoin maintenant tootransfer cette tooAzure script Machine Learning Studio. Je pourrais simplement effectuer un couper-coller. Mais je vais ici transférer le script R via un fichier zip.

### <a name="data-input-toohello-execute-r-script-module"></a>Module de données d’entrée toohello Execute R Script
Nous allons avez hello entrées toohello [Execute R Script] [ execute-r-script] module. Dans cet exemple, nous lira des données laitières de Californie hello en hello [Execute R Script] [ execute-r-script] module.  

Il existe trois entrées possibles pour hello [Execute R Script] [ execute-r-script] module. Selon votre application, vous pouvez utiliser une ou toutes ces entrées. Il est également parfaitement raisonnable toouse R qui n’accepte aucune entrée du tout.  

Examinons chacune de ces entrées, allant de gauche tooright. Vous pouvez voir les noms de hello de chacune des entrées de hello en positionnant le curseur à l’entrée de hello et en lisant les info-bulle hello.  

#### <a name="script-bundle"></a>Script groupé
Hello entrée de regroupement de Script vous permet de contenu de hello toopass d’un fichier zip dans [Execute R Script] [ execute-r-script] module. Vous pouvez utiliser une des hello suivant le contenu de hello tooread commandes du fichier zip de hello dans votre code R.

    source("src/yourfile.R") # Reads a zipped R script
    load("src/yourData.rdata") # Reads a zipped R data file

> [!NOTE]
> Azure Machine Learning traite les fichiers zip de hello comme s’ils étaient hello src / directory, vous devez tooprefix les noms de votre fichier avec ce nom de répertoire. Par exemple, si hello zip contient des fichiers de hello `yourfile.R` et `yourData.rdata` dans racine hello zip de hello, vous devez vous occuper en tant que `src/yourfile.R` et `src/yourData.rdata` lors de l’utilisation `source` et `load`.
> 
> 

Nous avons déjà mentionné lors du chargement de jeux de données dans [chargement hello dataset](#loading). Une fois que vous avez créé et testé le script hello R indiqué dans la section précédente de hello, procédez comme hello suivant :

1. Enregistrer le script hello R dans un. Fichier de R. J'appelle mon fichier de script « simpleplot.R ». Voici le contenu de hello.
   
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
2. Créez un fichier zip et copiez votre script dans ce fichier. Sous Windows, vous pouvez avec le bouton droit sur le fichier de hello et sélectionnez **envoyer à**, puis **dossier compressé**. Cela crée un nouveau fichier zip contenant hello « simpleplot. Fichier de R ».
3. Ajouter votre fichier toohello **datasets** dans Machine Learning Studio, la spécification de type hello en tant que **zip**. Vous devez maintenant voir le fichier zip de hello dans vos jeux de données.
4. Fichier zip de hello du glisser -déplacer à partir de **datasets** sur hello **canevas de ML Studio**.
5. Connectez la sortie hello Hello **zip données** icône toohello **regroupement de Script** d’entrée de hello [Execute R Script] [ execute-r-script] module.
6. Hello de type `source()` fonction avec le nom du fichier zip dans la fenêtre de code hello pour hello [Execute R Script] [ execute-r-script] module. Dans mon cas, j’ai saisi `source("src/simpleplot.R")`.  
7. Pensez à cliquer sur **Save**(Enregistrer).

Une fois ces étapes terminées, hello [Execute R Script] [ execute-r-script] module entraîne l’exécution hello R script dans le fichier zip de hello lors de l’expérience de hello est exécuté. À ce stade, votre expérimentation doit être similaire à la figure 5.

![expérimentation utilisant le script R compressé][6]

*Figure 5 : expérimentation utilisant le script R compressé.*

#### <a name="dataset1"></a>Jeu de données 1
Vous pouvez passer un tableau rectangulaire de code tooyour R de données à l’aide d’entrée de hello Dataset1. Dans notre hello script simple `maml.mapInputPort(1)` fonction lit les données de hello dans le port 1. Ces données sont ensuite assignées tooa trame de données nom de la variable dans votre code. Dans notre script simple hello première ligne de code effectue des assignations de hello.

    cadairydata <- maml.mapInputPort(1)

Exécuter votre expérience en cliquant sur hello **exécuter** bouton. Lors de l’exécution de hello est terminée, cliquez sur hello [Execute R Script] [ execute-r-script] module, puis cliquez sur **afficher le journal de sortie** sur le volet de propriétés hello. Une nouvelle page doit apparaître dans votre navigateur, affichage du contenu du fichier du fichier sortie.log hello hello. Lorsque vous faites défiler vers le bas, vous devez voir quelque chose comme hello suivant.

    [ModuleOutput] InputDataStructure
    [ModuleOutput]
    [ModuleOutput] {
    [ModuleOutput]  "InputName":Dataset1
    [ModuleOutput]  "Rows":228
    [ModuleOutput]  "Cols":9
    [ModuleOutput]  "ColumnTypes":System.Int32,3,System.Double,5,System.String,1
    [ModuleOutput] }

Plus loin vers le bas hello page est plus d’informations sur les colonnes hello, qui ressemble à hello suivant.

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

Ces résultats sont principalement comme prévu, des 228 observations 9 colonnes et dans hello trame de données. Nous pouvons voir les noms de colonne hello, type de données hello R et un exemple de chaque colonne.

> [!NOTE]
> Cette sortie imprimée même est facilement disponible à partir de hello sortie appareil R Hello [Execute R Script] [ execute-r-script] module. Nous allons décrire les sorties hello Hello [Execute R Script] [ execute-r-script] module dans la section suivante de hello.  
> 
> 

#### <a name="dataset2"></a>Jeu de données 2
Bonjour le comportement de l’entrée de hello Dataset2 est toothat identiques de Dataset1. Avec cette entrée, vous pouvez transmettre une deuxième table de données rectangulaire à votre code R. Hello fonction `maml.mapInputPort(2)`, avec l’argument hello 2, est utilisé toopass ces données.  

### <a name="execute-r-script-outputs"></a>Sorties du module d'exécution de script R
#### <a name="output-a-dataframe"></a>Sortie d'un tableau de données
Vous pouvez sortie contenu hello d’une trame de données R comme un tableau rectangulaire via le port de hello Dataset1 de résultat à l’aide de hello `maml.mapOutputPort()` (fonction). Dans notre script R simple cette opération est effectuée par hello ligne suivante.

    maml.mapOutputPort('cadairydata')

Après l’expérience hello en cours d’exécution, cliquez sur hello port de sortie des résultats Dataset1, puis cliquez sur **visualiser**. Vous obtenez un résultat analogue à la figure 6.

![visualisation de Hello de sortie hello Hello données laitières de Californie][7]

*La figure 6. visualisation de Hello de sortie hello Hello données laitières de Californie.*

Cette sortie ressemble toohello identiques entrée, exactement comme nous attendions.  

### <a name="r-device-output"></a>Sortie de l’appareil R
Hello sorties sur des périphériques de hello [Execute R Script] [ execute-r-script] module contient la sortie des messages et des graphiques. Les deux messages de sortie et l’erreur standard standards à partir de R sont envoyés toohello port de sortie de périphérique R.  

tooview hello R périphérique de sortie, cliquez sur le port hello puis sur **visualiser**. Nous voyons sortie standard de hello et d’erreur standard à partir du script hello R dans la Figure 7.

![Sortie standard et l’erreur standard de hello port du périphérique R][8]

*Figure 7 : Sortie standard et l’erreur standard de hello port du périphérique R.*

Le défilement vers le bas nous, consultez la sortie de graphiques hello à partir de notre script R dans la Figure 8.  

![Sortie graphique à partir de hello port du périphérique R][9]

*Figure 8 : Graphique de sortie de hello port du périphérique R.*  

## <a id="filtering"></a>Filtrage et transformation des données
Dans cette section, nous allons effectuer certains le filtrage de données de base et les opérations de transformation sur hello données laitières de Californie. En fin de hello de cette section, nous auront des données dans un format approprié pour la création d’un modèle d’analyse.  

Plus particulièrement, nous allons effectuer dans cette section plusieurs tâches courantes de nettoyage et de transformation de données ; de transformation de types, de filtrage sur des tableaux de données, d’ajout de nouvelles colonnes calculées et de transformation de valeurs. Cet arrière-plan doit vous permettre de traiter de nombreuses variations a rencontré des problèmes réels hello.

Hello R code complet pour cette section est disponible dans le fichier zip de hello téléchargé précédemment.

### <a name="type-transformations"></a>Transformations de types
Maintenant que nous pouvons lire les données de laitier de Californie hello dans code hello R hello [Execute R Script] [ execute-r-script] module, nous devons tooensure que les données hello dans les colonnes hello ont hello destiné type et le format.  

R est un langage typé dynamiquement, ce qui signifie que les types de données sont convertis à partir d’un tooanother en fonction des besoins. types de données atomiques Hello dans R incluent numérique, logique et de caractères. type de facteur de Hello est toocompactly utilisés stocker des données catégorielles. Vous trouverez plus d’informations sur les types de données dans les références de hello dans [annexe B - informations supplémentaires](#appendixb).

Lors de la lecture des données tabulaires dans R à partir d’une source externe, il est toujours une bonne idée toocheck hello résultant des types dans les colonnes hello. Vous pouvez espérer obtenir une colonne de type caractère, mais dans de nombreux cas, elle se présentera sous forme de facteur ou inversement. Dans d’autres cas, une colonne qui selon vous devrait être de type numérique pourra être représentée par des données caractères, par exemple, « 1,23 » au lieu du nombre à virgule flottante 1,23.  

Heureusement, il est facile tooconvert un tooanother de type, tant que mappage est possible. Par exemple, vous ne peut pas convertir 'Nevada' en valeur numérique, mais vous pouvez le convertir tooa facteur (variable catégorielle). De même, vous pouvez convertir la valeur numérique 1 en caractère « 1 » ou en facteur.  

syntaxe Hello pour une de ces conversions est simple : `as.datatype()`. Ces fonctions de conversion de type hello suivants.

* `as.numeric()`
* `as.character()`
* `as.logical()`
* `as.factor()`

Examinez les types de données hello des colonnes de hello nous entrées dans la section précédente de hello : toutes les colonnes sont de type numérique, à l’exception de hello intitulé « Mois », qui est de caractère de type. Nous allons convertir ce facteur tooa et hello résultats des tests.  

J’ai supprimé ligne hello créé hello scatterplot matrice et ajouté une ligne conversion facteur de hello 'Month' colonne tooa. Dans mon expérience je sera simplement couper et coller le code de hello R dans la fenêtre de code hello Hello [Execute R Script] [ execute-r-script] Module. Vous pouvez également mettre à jour le fichier zip de hello et téléchargez-le tooAzure Machine Learning Studio, mais cette opération prend plusieurs étapes.  

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

Nous allons exécuter ce code et examinez le journal de sortie hello pour hello script R. Hello les données pertinentes à partir du journal de hello sont indiquées dans la Figure 9.

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

*Figure 9 : Résumé de la trame de données hello avec une variable de facteur.*

type Hello pour le mois doit maintenant indiquer «**facteur avec 14 niveaux**'. Il s’agit d’un problème étant donné que les 12 mois dans l’année de hello. Vous pouvez également vérifier toosee qui hello type dans **visualiser** de jeu de données de résultat de hello port est '**catégorie**'.

problème de Hello est que hello 'Month', colonne n’a pas été codée systématiquement. Le nom du mois sera dans certains cas affiché en toutes lettres (avril) et dans d’autres, il sera abrégé (avr.). Nous pouvons résoudre ce problème par la suppression des caractères de too3 chaîne hello. ligne Hello de code ressemble maintenant à hello suivantes :

    ## Ensure hello coding is consistent and convert column tooa factor
    cadairydata$Month <- as.factor(substr(cadairydata$Month, 1, 3))

Réexécutez l’expérience de hello et afficher le journal de sortie hello. Hello attendu les résultats s’affichent dans la Figure 10.  

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

*Figure 10 : Résumé de la trame de données hello avec le nombre correct de niveaux de facteur.*

Notre variable facteur a maintenant hello souhaité 12 niveaux.

### <a name="basic-data-frame-filtering"></a>Filtrage de base des tableaux de données
Les tableaux de données R prennent en charge des fonctionnalités de filtrage efficaces. Il est possible de créer des sous-ensembles de jeux de données en appliquant des filtres logiques aux lignes ou colonnes. Dans de nombreux cas, des critères de filtre complexes sont nécessaires. références de Hello dans [annexe B - informations supplémentaires](#appendixb) contiennent des exemples détaillés de filtrage des trames de données.  

Notre jeu de données a besoin d'être filtré. Si vous examinez les colonnes hello dans hello cadairydata trame de données, vous verrez deux colonnes inutiles. première colonne de Hello conserve uniquement un numéro de ligne, ce qui n’est pas très utile. deuxième colonne Hello, Year.Month, contienne des informations redondantes. Nous pouvons facilement exclure ces colonnes à l’aide de hello suivant le code R.

> [!NOTE]
> À partir de maintenant sur dans cette section, vous montrera simplement vous hello code supplémentaire ajoute Bonjour [Execute R Script] [ execute-r-script] module. Je vais ajouter chaque nouvelle ligne **avant** hello `str()` (fonction). Utiliser cette fonction tooverify mes résultats dans Azure Machine Learning Studio.
> 
> 

Ajouter hello après ligne de code toomy R Bonjour [Execute R Script] [ execute-r-script] module.

    # Remove two columns we do not need
    cadairydata <- cadairydata[, c(-1, -2)]

Exécutez ce code dans votre expérience et vérifier les résultats hello à partir du journal de sortie hello. Ces résultats sont présentés dans la figure 11.

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

*Figure 11 : Résumé de la trame de données hello avec deux colonnes supprimées.*

Bonne nouvelle ! Nous obtenons les résultats hello attendu.

### <a name="add-a-new-column"></a>Ajout d'une nouvelle colonne
modèles de série chronologique toocreate, il sera toohave pratique, une colonne contenant hello mois depuis le démarrage de hello de MTS hello. À cet effet, nous allons créer la colonne « Month.Count ».

toohelp organiser le code hello nous allons créer notre première fonction simple, `num.month()`. Nous allons ensuite appliquer cette fonction de toocreate une nouvelle colonne dans la trame de données hello. nouveau code de Hello est comme suit.

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

Maintenant, exécutez l’expérience de mise à jour de hello et utiliser hello journal tooview hello un résultat. Ces résultats sont présentés dans la figure 12.

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

*Figure 12 : Résumé de la trame de données hello avec une colonne supplémentaire de hello.*

Tout semble fonctionner. Nous avons hello nouvelle colonne avec les valeurs attendues hello dans notre trame de données.

### <a name="value-transformations"></a>Transformations de valeurs
Dans cette section, nous allons effectuer certaines transformations simples sur les valeurs hello dans certaines colonnes hello de notre trame de données. langage de Hello R prend en charge les transformations de valeur presque arbitraire. références de Hello dans [annexe B : obtenir des informations supplémentaires](#appendixb) contiennent des exemples détaillés.

Si vous examinez les valeurs hello dans des résumés de hello de notre trame de données que vous devez voir quelque chose impair ici. Par exemple, produit-on vraiment plus de crème glacée que de lait en Californie ? Non, bien entendu pas, comme cela n’est pas justifiée, sad comme cela peut être toosome nous amoureux de glace. unités de Hello sont différentes. les prix Hello sont nous exprimée en livres, lait est en unités de 1 million US livres, glace est en unités de 1 000 nous gallons et blanc cheese est exprimé en unités de 1 000 US kg. En supposant que glace pèse environ 6,5 livres par gallon, nous pouvons facilement hello tooconvert multiplication ces valeurs afin qu’ils soient dans des unités égales de 1 000 euros.

Pour notre modèle de prévision, nous utilisons un modèle multiplicatif de façon à ajuster ces données en fonction des variations saisonnières et tendancielles. Une transformation de journal permet de toouse un modèle linéaire, ce qui simplifie ce processus. Nous pouvons appliquer une transformation de journal hello dans hello même fonction où un multiplicateur de hello est appliqué.

Bonjour suivant de code, définir une nouvelle fonction, `log.transform()`et l’appliquer toohello les lignes contenant des valeurs numériques hello. Hello R `Map()` fonction est utilisée tooapply hello `log.transform()` fonction toohello sélectionné des colonnes de la trame de données hello. `Map()`est semblable trop`apply()` mais permet plus d’une liste de la fonction de toohello d’arguments. Notez qu’une liste des multiplicateurs fournit hello deuxième argument toohello `log.transform()` (fonction). Hello `na.omit()` fonction est utilisée, un peu de nettoyage tooensure nous n’avons manquant ou des valeurs non définies dans hello trame de données.

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

Il existe un problème de bit Bonjour `log.transform()` (fonction). La majeure partie de ce code est la vérification des problèmes potentiels avec des arguments de hello ou traiter les exceptions qui peuvent toujours se produire au cours des calculs de hello. Uniquement quelques lignes de ce code réellement hello des calculs.

objectif de Hello de la programmation de défense hello est Échec de hello tooprevent d’une fonction unique qui empêche le traitement de continuer. L’échec soudain d’une analyse au long cours peut s’avérer très contrariant pour les utilisateurs. tooavoid cette situation, par défaut les valeurs de retour doivent être choisis limitera gravement toodownstream traitement. Un message est également aux utilisateurs de produits tooalert qui est passé quelque chose incorrect.

Si vous n’êtes pas programmation toodefensive utilisés dans R, ce code peut sembler un peu trop importante. Je vous guidera à travers les étapes majeures hello :

1. Un vecteur de quatre messages est défini. Ces messages sont toocommunicate utilisé plus d’informations sur certaines des erreurs possibles de hello et des exceptions qui peuvent se produire avec ce code.
2. Dans chaque cas, la valeur NA est renvoyée. Il existe de nombreuses autres possibilités susceptibles de produire moins d’effets secondaires. Je pourrais retourne un vecteur de zéros ou d’un vecteur d’entrée d’origine de hello, par exemple.
3. Vérifications sont exécutées sur hello arguments toohello (fonction). Dans chaque cas, si une erreur est détectée, une valeur par défaut est retournée et un message est généré par hello `warning()` (fonction). J’utilise `warning()` plutôt que `stop()` comme hello ce dernier mettra fin à l’exécution, exactement ce que j’essaie de tooavoid. À noter que j'ai écrit ce code dans un style procédural, car dans ce cas, une approche fonctionnelle paraissait complexe et obscure.
4. calculs de journal Hello sont encapsulées dans `tryCatch()` afin que les exceptions n’entraîne pas un arrêt brutal de tooprocessing. Sans `tryCatch()` , la plupart des erreurs déclenchées par les fonctions R engendrent un signal d’arrêt, qui est suivi d’un arrêt.

Exécutez ce code R dans votre expérience et examiner hello imprimer la sortie dans le fichier du fichier sortie.log hello. Vous voyez maintenant les valeurs hello transformé de hello quatre colonnes hello ouvrir une session, comme indiqué dans la Figure 13.

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

*Figure 13 : Résumé de hello transformés les valeurs dans une trame de données hello.*

Nous constatons que les valeurs hello ont été transformées. À présent, la production de lait dépasse nettement la production de tous les autres produits laitiers, ce qui nous rappelle que nous avons maintenant sous nos yeux une échelle logarithmique.

À ce stade, nos données sont nettoyées et nous sommes prêts à procéder à une modélisation. Examinez la visualisation hello pour hello Dataset des résultats de sortie de notre [Execute R Script] [ execute-r-script] module, vous verrez hello 'Month' colonne est « Catégorie » avec des 12 valeurs uniques, à nouveau, tout comme nous le souhaitions .

## <a id="timeseries"></a>Objets de série chronologique et analyse des corrélations
Dans cette section, nous Explorer quelques R temps série d’objets de base et analyser les corrélations hello entre des variables de hello. Notre objectif est toooutput une trame de données contenant hello par paire de corrélation des informations sur les retards de plusieurs.

Hello R code complet pour cette section est dans un fichier zip de hello téléchargé précédemment.

### <a name="time-series-objects-in-r"></a>Objets de série chronologique en langage R
Comme nous l'avons déjà vu, une série chronologique est une série de valeurs de données indexées par le temps. Objets série au moment de R sont utilisé toocreate et gérer des index de temps hello. Il existe plusieurs avantages toousing temps série objets. Objets au moment de série libre à partir de hello nombreux détails de la gestion des valeurs d’index hello temps série qui sont encapsulées dans un objet de hello. En outre, les objets de série heure permettent hello de toouse vous nombreuses méthodes de série de temps pour le traçage, l’impression, de modélisation, etc..

Hello classe série au moment de POSIXct est couramment utilisé et est relativement simple. Cette classe série au moment de mesure le temps de démarrer hello d’époque hello, le 1er janvier 1970. Nous utiliserons dans cet exemple des objets de série chronologique POSIXct. Parmi les autres classes d'objet de série chronologique R souvent utilisées, citons zoo et xts, qui concernent les séries chronologiques extensibles.
<!-- Additional information on R time series objects is provided in hello references in Section 5.7. [commenting because this section doesn't exist, even in hello original] -->

### <a name="time-series-object-example"></a>Exemple d’objet de série chronologique
Commençons notre exemple. Glissez-déplacez un **nouveau** module [d’exécution de script R][execute-r-script] dans votre expérimentation. Connectez le port de sortie de hello Dataset1 du résultat de hello existant [Execute R Script] [ execute-r-script] module toohello Dataset1 d’entrée de port de hello nouvelle [Execute R Script] [ execute-r-script] module.

Comme pour les exemples de première hello, que nous avons sa progression via l’exemple hello, à certains moments, je vais montrer uniquement hello incrémentielle lignes supplémentaires de code R à chaque étape.  

#### <a name="reading-hello-dataframe"></a>Lors de la lecture hello trame de données
Dans un premier temps, nous allons lire dans une trame de données et assurez-vous que nous obtenons les résultats hello attendu. Hello suivant doit effectuer le travail de hello.

    # Comment hello following if using RStudio
    cadairydata <- maml.mapInputPort(1)
    str(cadairydata) # Check hello results

Exécutez maintenant l’expérience de hello. journal Hello de forme Execute R Script hello doit ressembler à la Figure 14.

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

*Figure 14 : Résumé de la trame de données hello dans le module Execute R Script de hello.*

Ces données sont de format et des types de hello attendu. Notez que hello 'Month' colonne est le facteur de type hello devrait nombre de niveaux.

#### <a name="creating-a-time-series-object"></a>Création d’un objet de série chronologique
Nous devons tooadd une trame de données de temps série objet tooour. Remplacez le code d’en cours de hello avec suivants de hello, qui ajoute une nouvelle colonne de la classe POSIXct.

    # Comment hello following if using RStudio
    cadairydata <- maml.mapInputPort(1)

    ## Create a new column as a POSIXct object
    Sys.setenv(TZ = "PST8PDT")
    cadairydata$Time <- as.POSIXct(strptime(paste(as.character(cadairydata$Year), "-", as.character(cadairydata$Month.Number), "-01 00:00:00", sep = ""), "%Y-%m-%d %H:%M:%S"))

    str(cadairydata) # Check hello results

À présent, vérifiez les journaux hello. Elle doit être similaire à la figure 15.

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

*Figure 15 : Résumé de la trame de données hello avec un objet de série de temps.*

À partir de hello résumé, nous pouvons voir que hello nouvelle colonne est en fait de la classe POSIXct.

### <a name="exploring-and-transforming-hello-data"></a>Exploration et la transformation des données de hello
Examinons quelques-unes des variables hello dans ce jeu de données. Une matrice scatterplot est un bon moyen de tooproduce un coup de œil rapide. Je suis en remplaçant hello `str()` fonction dans du code R précédente hello avec hello ligne suivante.

    pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = cadairydata, main = "Pairwise Scatterplots of dairy time series")

Exécutez ce code et regardez ce qu'il se passe. traçage Hello produit en hello port du périphérique R doit ressembler à la Figure 16.

![matrice de nuage de points des variables sélectionnées][17]

*Figure 16 : matrice de nuage de points des variables sélectionnées.*

Il est une structure odd-looking dans les relations hello entre ces variables. Cela se produit peut-être des tendances dans les données de salutation et fait hello que nous n’avons pas normalisés variables de hello.

### <a name="correlation-analysis"></a>Analyse des corrélations
analyse de corrélation tooperform nous devons tooboth des tendances et normaliser les variables de hello. Nous avons simplement utiliser hello R `scale()` (fonction), les centres et ajuste les variables. D'autant que son exécution peut même s'avérer plus rapide. Toutefois, je veux tooshow vous un exemple de la programmation dans R.

Hello `ts.detrend()` fonction ci-dessous effectue ces deux opérations. Hello deux lignes de code suivantes de tendance déduplication des données de hello et puis normaliser les valeurs hello.

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

Il existe un problème de bit Bonjour `ts.detrend()` (fonction). La majeure partie de ce code est la vérification des problèmes potentiels avec des arguments de hello ou traiter les exceptions qui peuvent toujours se produire au cours des calculs de hello. Uniquement quelques lignes de ce code réellement hello des calculs.

Nous avons déjà vu un exemple de programmation défensive dans la section [Transformations de valeurs](#valuetransformations). Les deux blocs de calcul sont circonscrits à `tryCatch()`. Pour certaines erreurs rend vecteur d’entrée d’origine tooreturn hello sens et dans d’autres cas, retourner un vecteur de zéros.  

Notez que la régression linéaire hello utilisée pour annuler l’analyse de tendances est une régression de série de temps. variable de PRÉDICTEUR Hello est un objet de série de temps.  

Une fois `ts.detrend()` est défini nous s’appliquent variables toohello d’intérêt dans notre trame de données. Nous devons forcer la liste résultante de hello créé par `lapply()` toodata de trame de données à l’aide de `as.data.frame()`. En raison des aspects défensives de `ts.detrend()`, tooprocess échec une des variables de hello n’empêchera pas corriger le traitement de hello d’autres.  

Hello dernière ligne de code crée un scatterplot par paire. Après l’exécution de code de hello R, les résultats de hello de hello scatterplot sont affichés dans la Figure 17.

![nuage de points par paire de la série chronologique après élimination de la tendance et standardisation][18]

*Figure 17 : nuage de points par paire de la série chronologique après élimination de la tendance et standardisation.*

Vous pouvez comparer ces toothose résultats indiqué dans la Figure 16. Avec hello tendance supprimé et hello variables normalisés, nous constatons beaucoup moins de structure dans les relations entre ces variables hello.

Hello code toocompute hello des corrélations en tant qu’objets de R ccf est comme suit.

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

Exécution de ce code produit journal hello indiqué dans la Figure 18.

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

*Figure 18 : Liste de ccf objets d’analyse de corrélation par paire hello.*

À chaque décalage correspond une valeur de corrélation. Aucune de ces valeurs de corrélation est suffisamment grande toobe significatifs. Nous pouvons donc en conclure qu'il est possible de modéliser chaque variable de façon indépendante.

### <a name="output-a-dataframe"></a>Sortie d'un tableau de données
Nous avons calculé les corrélations par paire hello sous forme de liste d’objets de R ccf. Cela pose un bit d’un problème comme port de sortie de jeu de données de résultat de hello nécessite une trame de données. En outre, objet de ccf hello est lui-même une liste, et nous voulons uniquement les valeurs hello hello premier élément de cette liste, des corrélations hello en hello retards différents.

Hello suivant liste hello d’objets ccf, qui sont eux-mêmes des listes de valeurs de décalage de code extraits hello.

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

Hello première ligne de code est un peu difficile, et une explication peut vous aider à comprendre. Utilisation de hello intérieur/extérieur nous disposer de hello :

1. Hello '**[[**'opérateur avec un argument de hello'**1**' sélectionne hello vecteur de corrélations à des retards de hello de hello premier élément de liste d’objets ccf hello.
2. Hello `do.call()` fonction applique hello `rbind()` fonction sur les éléments hello de liste de hello retourne en `lapply()`.
3. Hello `data.frame()` fonction convertit le résultat hello produit par `do.call()` tooa la trame de données.

Notez que les noms de lignes hello se trouvent dans une colonne de la trame de données hello. Cela permet de conserver les noms de lignes hello lorsqu’ils sont générés à partir de hello [Execute R Script][execute-r-script].

Exécution du code de hello produit une sortie hello indiqué dans la Figure 19 lorsque je **visualiser** hello sortie hello port de jeu de données de résultat. les noms de lignes Hello sont dans la première colonne de hello, comme prévu.

![Sortie des résultats d’analyse de corrélation hello][20]

*Figure 19 : Résultats de sortie de l’analyse de corrélation hello.*

## <a id="seasonalforecasting"></a>Exemple de série chronologique : prévision saisonnière
Nos données sont maintenant sous une forme appropriée pour l’analyse, et nous avons déterminé qu'il n’y a aucune corrélation significative entre les variables hello. Continuons et créons un modèle de prévision chronologique. À l’aide de ce modèle nous sera prévision de production de lait Californie pour hello 12 mois de 2013.

Notre modèle de prévision aura deux composantes : une tendancielle et une saisonnière. prévision de terminée Hello est produit hello de ces deux composants. Ce type de modèle est connu sous le nom de modèle multiplicatif. alternative de Hello est un modèle additif. Nous avons déjà appliqué un journal transformation toohello les variables d’intérêt, ce qui rend cette analyse souple.

Hello R code complet pour cette section est dans un fichier zip de hello téléchargé précédemment.

### <a name="creating-hello-dataframe-for-analysis"></a>Création de hello trame de données pour l’analyse
Commencez par ajouter un **nouveau** [Execute R Script] [ execute-r-script] expérience tooyour de module. Se connecter hello **Dataset des résultats** sortie hello existants [Execute R Script] [ execute-r-script] module toohello **Dataset1** d’entrée du nouveau module de hello. résultat de Hello ressemble à la Figure 20.

![Hello faire des essais avec le nouveau module Execute R Script hello d’ajouté][21]

*Figure 20. Hello faire des essais avec le nouveau module Execute R Script hello d’ajouté.*

Comme avec l’analyse de corrélation hello que nous vient de se terminer, nous devons tooadd une colonne avec un objet de série heure POSIXct. Hello suivant code simplement cette opération.

    # If running in Machine Learning Studio, uncomment hello first line with maml.mapInputPort()
    cadairydata <- maml.mapInputPort(1)

    ## Create a new column as a POSIXct object
    Sys.setenv(TZ = "PST8PDT")
    cadairydata$Time <- as.POSIXct(strptime(paste(as.character(cadairydata$Year), "-", as.character(cadairydata$Month.Number), "-01 00:00:00", sep = ""), "%Y-%m-%d %H:%M:%S"))

    str(cadairydata)

Exécutez ce code et examinez le journal de hello. résultat de Hello doit ressembler à la Figure 21.

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

*Figure 21 : Un résumé de la trame de données hello.*

Ce résultat, nous sommes prêt toostart notre analyse.

### <a name="create-a-training-dataset"></a>Création d’un jeu de données d’apprentissage
Avec la trame de données hello construit, nous devons toocreate un jeu de données d’apprentissage. Ces données incluent tous les observations hello sauf hello 12 dernières, de l’année hello 2013, qui est notre jeu de données de test. suivante de Hello trame de données hello des sous-ensembles de code et crée des graphiques, des variables de production et le prix laitières hello. Puis créer les graphiques de hello quatre variables de production et le prix. Une fonction anonyme est utilisé toodefine certains renforce pour le traçage et ensuite parcourir liste hello Hello deux autres arguments avec `Map()`. Vous vous dites peut-être qu'une boucle for aurait ici fait l'affaire. Vous avez raison, mais comme le langage R est un langage fonctionnel, je vous montre une approche fonctionnelle.

    cadairytrain <- cadairydata[1:216, ]

    Ylabs  <- list("Log CA Cotage Cheese Production, 1000s lb",
                   "Log CA Ice Cream Production, 1000s lb",
                   "Log CA Milk Production 1000s lb",
                   "Log North CA Milk Milk Fat Price per 1000 lb")

    Map(function(y, Ylabs){plot(cadairytrain$Time, y, xlab = "Time", ylab = Ylabs, type = "l")}, cadairytrain[, 4:7], Ylabs)

Exécution du code de hello produit hello trace les séries de série chronologique de sortie de périphérique R hello indiqué dans la Figure 22. Notez qu’axe du temps hello est exprimé en unités de dates, des avantages de temps hello série tracer la méthode.

![premier graphique chronologique des données de production et de prix des produits laitiers californiens](./media/machine-learning-r-quickstart/unnamed-chunk-161.png)

![deuxième graphique chronologique des données de production et de prix des produits laitiers californiens](./media/machine-learning-r-quickstart/unnamed-chunk-162.png)

![troisième graphique chronologique des données de production et de prix des produits laitiers californiens](./media/machine-learning-r-quickstart/unnamed-chunk-163.png)

![quatrième graphique chronologique des données de production et de prix des produits laitiers californiens](./media/machine-learning-r-quickstart/unnamed-chunk-164.png)

*Figure 22 : graphiques chronologiques des données de production et de prix des produits laitiers californiens.*

### <a name="a-trend-model"></a>Modèle de tendance
Après avoir créé un objet de série de temps et avoir examiné les données de salutation, nous pouvons commencer tooconstruct un modèle de tendance pour hello données de production de lait California. Pour cela, nous pouvons utiliser une régression chronologique. Toutefois, il est clair à partir de traçage de hello que nous allons peut-être plus d’un tooaccurately pente et l’ordonnée à l’origine modéliser hello observé les tendances dans les données d’apprentissage hello.

Donné à petite échelle de hello de données de hello, je générera modèle hello pour tendance dans RStudio et puis couper et coller le modèle résultant de hello dans Azure Machine Learning. RStudio offre un environnement interactif pour ce type d'analyse interactive.

Comme une première tentative, je vais essayer une régression polynomiale avec too3 sous tension. Il existe un risque réel de surapprentissage de ces types de modèles. Par conséquent, il est de meilleures conditions d’ordre haut tooavoid. Hello `I()` fonction empêche l’interprétation du contenu de hello (interprète contenu hello « en l’état ») et vous permet de toowrite une fonction interprétée littéralement dans une équation de régression.

    milk.lm <- lm(Milk.Prod ~ Time + I(Month.Count^2) + I(Month.Count^3), data = cadairytrain)
    summary(milk.lm)

Cette opération génère suivant de hello.

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

À partir des valeurs de P (Pr (> | t |)) dans cette sortie, nous pouvons voir que hello terme quadratique peut ne pas être significative. Vous allez utiliser hello `update()` toomodify ce modèle en supprimant hello carré terme de fonction.

    milk.lm <- update(milk.lm, . ~ . - I(Month.Count^2))
    summary(milk.lm)

Cette opération génère suivant de hello.

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

Cela semble mieux. Tous les termes du contrat de hello sont significatifs. Toutefois, hello 2e-16 valeur est la valeur par défaut et ne doit pas être prise trop gravement.  

Qu’un test de validité, nous allons en créer un tracé de série heure de données de production laitière Californie de hello avec courbe de tendance hello indiqué. J’ai ajouté hello suivant code Bonjour Azure Machine Learning [Execute R Script] [ execute-r-script] toocreate de modèle (pas RStudio) hello modèle et effectuer un traçage. résultat de Hello est illustré dans la Figure 23.

    milk.lm <- lm(Milk.Prod ~ Time + I(Month.Count^3), data = cadairytrain)

    plot(cadairytrain$Time, cadairytrain$Milk.Prod, xlab = "Time", ylab = "Log CA Milk Production 1000s lb", type = "l")
    lines(cadairytrain$Time, predict(milk.lm, cadairytrain), lty = 2, col = 2)

![données de production laitière californienne avec affichage du modèle de tendance](./media/machine-learning-r-quickstart/unnamed-chunk-18.png)

*Figure 23 : données de production laitière californienne avec affichage du modèle de tendance.*

Il semble que le modèle de tendance hello le mieux aux données de hello assez bien. En outre, il ne semble pas preuve toobe de surapprentissage, telles qu’impair tremble dans la courbe du modèle hello.  

### <a name="seasonal-model"></a>Modèle saisonnier
Avec un modèle de tendance dans main, nous devez toopush sur et inclure des effets saisonniers hello. Nous allons utiliser mois hello d’année de hello comme une variable factice en vigueur de hello modèle linéaire toocapture hello mois par mois. Notez que lorsque vous introduisez des variables de facteur dans un modèle, intercept de hello ne doit pas être calculée. Si vous ne le faites pas, formule de hello est spécifié de manière excessive et R entraînera l’abandon d’un des hello souhaité facteurs en conservant terme d’interception hello.

Étant donné que nous disposons d’un modèle de tendance satisfaisante, nous pouvons utiliser hello `update()` hello de tooadd fonction nouveau modèle existant de toohello des termes du contrat. Hello -1 dans la formule de mise à jour hello supprime le terme d’interception hello. Pour le moment de hello pour poursuivre dans RStudio :

    milk.lm2 <- update(milk.lm, . ~ . + Month - 1)
    summary(milk.lm2)

Cette opération génère suivant de hello.

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

Nous voyons ce modèle hello a un terme d’interception ne sont plus et présente des facteurs significatifs mois 12. C’est exactement ce que nous voulions toosee.

Nous allons en créer un autre tracé de série de temps de hello Californie production laitière données toosee degré modèle saisonnières de hello fonctionne. J’ai ajouté hello suivant code Bonjour Azure Machine Learning [Execute R Script] [ execute-r-script] toocreate hello modèle et effectuer un traçage.

    milk.lm2 <- lm(Milk.Prod ~ Time + I(Month.Count^3) + Month - 1, data = cadairytrain)

    plot(cadairytrain$Time, cadairytrain$Milk.Prod, xlab = "Time", ylab = "Log CA Milk Production 1000s lb", type = "l")
    lines(cadairytrain$Time, predict(milk.lm2, cadairytrain), lty = 2, col = 2)

Ce code en cours d’exécution dans Azure Machine Learning produit traçage hello illustré Figure 24.

![production laitière californienne avec le modèle incluant les effets saisonniers](./media/machine-learning-r-quickstart/unnamed-chunk-20.png)

*Figure 24 : production laitière californienne avec le modèle incluant les effets saisonniers.*

Hello données adaptée toohello illustrées Figure 24 sont plutôt encourageants. Tendance de hello et effet saisonnières de hello (variation mensuelle) semblent correctes.

En tant qu’une autre vérification de notre modèle, nous allons avez résiduels de hello. Hello expression suivante calcule le code hello valeurs prédites entre nos deux modèles, calcule la moyenne des résiduels hello pour les modèles saisonnières hello et puis trace ces résiduels pour les données d’apprentissage hello.

    ## Compute predictions from our models
    predict1  <- predict(milk.lm, cadairydata)
    predict2  <- predict(milk.lm2, cadairydata)

    ## Compute and plot hello residuals
    residuals <- cadairydata$Milk.Prod - predict2
    plot(cadairytrain$Time, residuals[1:216], xlab = "Time", ylab ="Residuals of Seasonal Model")

traçage de résiduelles Hello est illustrée dans la Figure 25.

![Moyenne des résiduels du modèle de saisonnières hello pour les données d’apprentissage hello](./media/machine-learning-r-quickstart/unnamed-chunk-21.png)

*Figure 25 : Résiduels du modèle de saisonnières hello pour les données d’apprentissage hello.*

Ces résidus semblent corrects. Il n’existe aucune structure particulière, à l’exception d’effet hello de crise hello 2008-2009, qui ne compte pas notre modèle particulièrement bien.

traçage Hello indiqué dans la Figure 25 est utile pour détecter des modèles dépendant du temps dans la moyenne des résiduels hello. approche explicite de Hello de calcul et le traçage des résiduels hello que j’ai utilisé place résiduels de hello dans un ordre chronologique sur de traçage hello. Si, sur hello autre part, j’avais tracées `milk.lm$residuals`, traçage de hello n’aurait pas été dans un ordre chronologique.

Vous pouvez également utiliser `plot.lm()` tooproduce une série de graphiques de diagnostic.

    ## Show hello diagnostic plots for hello model
    plot(milk.lm2, ask = FALSE)

Ce code génère une série de graphiques de diagnostic représentés dans la figure 26.

![Premier des graphiques de diagnostic pour le modèle saisonnières de hello](./media/machine-learning-r-quickstart/unnamed-chunk-221.png)

![Seconde de graphiques de diagnostic pour le modèle de saisonnières de hello](./media/machine-learning-r-quickstart/unnamed-chunk-222.png)

![Troisième des graphiques de diagnostic pour le modèle saisonnières de hello](./media/machine-learning-r-quickstart/unnamed-chunk-223.png)

![Quatrième des graphiques de diagnostic pour le modèle saisonnières de hello](./media/machine-learning-r-quickstart/unnamed-chunk-224.png)

*Figure 26 : Trace de diagnostic pour le modèle saisonnières de hello.*

Il existe quelques points hautement influents identifiées dans ces graphiques, mais aucune toocause une préoccupation importante. En outre, nous constatons à partir de traçage Normal Q-Q hello que moyenne des résiduels hello sont toonormally fermer distribuée, une hypothèse importante pour les modèles linéaires.

### <a name="forecasting-and-model-evaluation"></a>Prévision et évaluation des modèles
Il existe qu’un seul toocomplete de toodo chose plus notre exemple. Nous devez toocompute prévisions et mesurer l’erreur de hello par rapport aux données réelles de hello. Nos prévisions seront pour hello 12 mois de 2013. Nous pouvons calculer une mesure de l’erreur pour cette prévision toohello les données qui ne fait pas partie de notre jeu de données d’apprentissage. En outre, nous pouvons comparer les performances sur hello toohello des données d’apprentissage de 18 ans 12 mois de données de test.  

Servent d’un nombre de mesures de performances de hello toomeasure de modèles de série chronologique. Dans le cas présent, nous allons utiliser erreur du carré moyen de racine (RMS) hello. Hello fonction suivante calcule erreur hello RMS entre deux séries.  

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

Comme avec hello `log.transform()` fonction évoqué dans hello « Valeur transformations » de section, il y a beaucoup de code erreur exception et de la vérification de la récupération dans cette fonction. principes de Hello employés sont hello même. travail Hello est effectué dans deux emplacements encapsulés dans `tryCatch()`. Tout d’abord, MTS hello sont exponentiated, étant donné que nous avons travaillé avec des journaux de hello des valeurs de hello. En second lieu, l’erreur RMS hello est calculée.  

Équipé d’un Bonjour toomeasure de fonction erreur RMS, nous allons générer et de sortie une trame de données contenant des erreurs de hello RMS. Nous inclut les termes du contrat pour le modèle de tendance hello seul et le modèle complet de hello avec facteurs saisonniers. Hello de code suivant hello travail à l’aide de modèles linéaires deux hello que nous avons construit.

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

Exécution de ce code de produit la sortie de hello indiqué dans la Figure 27 au port de sortie de jeu de données de résultat de hello.

![Comparaison des erreurs de RMS pour les modèles de hello][26]

*Figure 27 : Comparaison des erreurs de RMS pour les modèles hello.*

À partir de ces résultats, nous constatons que l’ajout hello facteurs saisonniers toohello modèle réduit erreur de RMS hello considérablement. Pas trop étonnamment, erreur hello RMS pour les données d’apprentissage de hello est un bit inférieur à pour hello prévisions.

## <a id="appendixa"></a>ANNEXE a : Guide tooRStudio
RStudio est très bien documenté, dans cette annexe je fournirai certaines toohello de liens des sections spécifiques de hello RStudio documentation tooget que vous avez démarré.

1. Création de projets
   
   Vous pouvez organiser et gérer votre code R dans les projets à l’aide de RStudio. Vous trouverez la documentation Hello qui utilise des projets à https://support.rstudio.com/hc/articles/200526207-Using-Projects.
   
   Je vous recommande de suivre ces instructions et de créer un projet pour des exemples de code hello R dans ce document.  
2. Modification et exécution de code R
   
   RStudio offre un environnement intégré qui permet de modifier et d'exécuter du code R. Vous trouverez la documentation à l’adresse https://support.rstudio.com/hc/articles/200484448-Editing-and-Executing-Code.
3. Débogage
   
   RStudio intègre de puissantes fonctionnalités de débogage. Vous trouverez la documentation relative à ces fonctionnalités à l’adresse https://support.rstudio.com/hc/articles/200713843-Debugging-with-RStudio.
   
   les fonctionnalités de dépannage de point d’arrêt Hello sont documentées dans https://support.rstudio.com/hc/articles/200534337-Breakpoint-Troubleshooting.

## <a id="appendixb"></a>ANNEXE B : informations supplémentaires
Cette R programmation didacticiel couvre hello de ce que vous avez besoin de toouse hello langage R avec Azure Machine Learning Studio. Si vous ne connaissez pas le langage R, deux présentations sont disponibles sur le site CRAN :

* R pour les débutants par Emmanuel Paradis est un toostart parfait à http://cran.r-project.org/doc/contrib/Paradis-rdebuts_en.pdf.  
* Un tooR Introduction par W. N. Venables, et al. approfondit un peu le sujet : http://cran.r-project.org/doc/manuals/R-intro.html.

Il existe de nombreux livres sur le langage R qui peuvent vous aider à vous lancer. En voici quelques-uns que j'ai trouvés utiles :

* Hello Art de programmation de R : une visite guidée de statistique conception de logiciels par Norman Matloff est un tooprogramming excellente introduction dans R.  
* Livre de recettes R par Paul Teetor fournit une approche problème et solution toousing R.  
* « R in Action » de Robert Kabacoff est un autre ouvrage introductif utile. site Web de Hello accompagnement R rapide est une ressource utile à http://www.statmethods.net/.
* Inferno R par Patrick Burns est un livre étonnamment humoristique qui négocie avec un nombre de rubriques complexe et difficiles qui peuvent être rencontrés lors de la programmation dans le livre de r. hello est disponible gratuitement sur http://www.burns-stat.com/documents/books/the-r-inferno/.
* Si vous souhaitez une présentation approfondie de rubriques avancées dans R, jetez un œil au livre de hello avancé R par Hadley Wickham. version en ligne de Hello de cette documentation est disponible gratuitement à http://adv-r.had.co.nz/.

Un catalogue de packages de série de temps R se trouvent dans hello CRAN affichage de la tâche d’analyse de série chronologique : http://cran.r-project.org/web/views/TimeSeries.html. Pour plus d’informations sur les packages d’objet série de temps spécifique, vous devez consultez la documentation de toohello pour ce package.

Hello carnet d’introduction de série chronologique avec R par Paul Cowpertwait et Andrew Metcalfe fournit une introduction de toousing R pour l’analyse de série chronologique. Divers textes théoriques proposent des exemples R.

Quelques ressources Internet particulièrement utiles :

* DataCamp : DataCamp enseigne R dans le confort de hello de votre navigateur avec des leçons vidéos et des exercices de codage. Il existe des didacticiels interactifs sur les techniques de R hello plus récentes et les packages. Suivez hello libre interactive R didacticiel consacré à https://www.datacamp.com/courses/introduction-to-r
* Guide de prise en main de R à partir de Programiz https://www.programiz.com/r-programming
* Un bref didacticiel sur le langage R par Kelly Black de l’Université de Clarkson : http://www.cyclismo.org/tutorial/R/
* Plus de 60 ressources sur le langage R : http://www.computerworld.com/article/2497464/business-intelligence-60-r-resources-to-improve-your-data-skills.html

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
