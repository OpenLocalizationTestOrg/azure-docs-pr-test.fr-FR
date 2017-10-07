---
title: "expérience simple d’aaaA dans Machine Learning Studio | Documents Microsoft"
description: "Ce didacticiel sur l’apprentissage automatique vous guidera tout au long d’une expérience de science des données simple. Nous allons prédire prix hello d’une voiture à l’aide d’un algorithme de régression."
keywords: "expérience,régression linéaire,algorithmes d’apprentissage automatique,didacticiel d’apprentissage automatique,techniques de modélisation prédictive,expérience de science de données"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: b6176bb2-3bb6-4ebf-84d1-3598ee6e01c6
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 03/20/2017
ms.author: garye
ms.openlocfilehash: fb215851d380acf7d0f4934a426283369f9c4ccb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="machine-learning-tutorial-create-your-first-data-science-experiment-in-azure-machine-learning-studio"></a>Didacticiel sur l’apprentissage automatique : Création de votre première expérience de science des données dans Azure Machine Learning Studio

Si vous n’avez encore jamais utilisé **Azure Machine Learning Studio**, ce didacticiel est pour vous.

Dans ce didacticiel, nous examinerons procédure toouse Studio pourquoi la première fois toocreate une expérience d’apprentissage. expérience de Hello allez tester un modèle d’analyse qui prédit le prix d’une voiture en fonction des différentes variables telles que les spécifications techniques et assurez-vous de hello.

> [!NOTE]
> Ce didacticiel vous montre hello principes de base des modules comment toodrag glisser-déplacer sur votre expérience, connectez-les, exécutez hello expérience et examiner les résultats de hello. Nous n’allons pas toodiscuss hello rubrique générale de l’apprentissage ou comment tooselect et utilisez hello 100 + données et des algorithmes manipulation modules intégrés inclus dans Studio.
>
>Si vous êtes toomachine formation, hello série de vidéos [Science des données pour les débutants](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) peut être un toostart parfait. Cette série de vidéos est une formation de toomachine bonne introduction à l’aide de concepts et le langage courant.
>
>Si vous êtes familiarisé avec machine learning, mais que vous recherchez plus d’informations sur la Machine Learning Studio et il contient des algorithmes d’apprentissage hello, voici quelques bonnes ressources :
>
- [Qu'est-ce que Machine Learning Studio ?](machine-learning-what-is-ml-studio.md) : il s’agit d’une vue d’ensemble de Studio.
- [Principes de base avec des exemples de l’algorithme d’apprentissage des ordinateurs](machine-learning-basics-infographic-with-algorithm-examples.md) -ce graphisme d’information est utile si vous souhaitez toolearn plus hello différents types d’algorithmes d’apprentissage automatique inclus avec Machine Learning Studio.
- [Guide de formation de l’ordinateur](https://gallery.cortanaintelligence.com/Tutorial/Machine-Learning-Guide-1) -ce guide couvre des informations similaires hello graphisme d’information ci-dessus, mais dans un format interactif.
- [Machine learning aide-mémoire algorithme](machine-learning-algorithm-cheat-sheet.md) et [comment toochoose des algorithmes pour Microsoft Azure Machine Learning](machine-learning-algorithm-choice.md) -ce poster téléchargeable et l’article connexe discutent des algorithmes de Studio hello en profondeur.
- [Machine Learning Studio : Algorithme et aide du Module](https://msdn.microsoft.com/library/azure/dn905974.aspx) -il s’agit d’informations de référence complètes hello pour tous les modules de Studio, y compris les algorithmes d’apprentissage automatique,

<!-- -->

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="how-does-machine-learning-studio-help"></a>En quoi Machine Learning Studio est-il utile ?

Machine Learning Studio rend facile tooset d’une expérience à l’aide des modules de glisser-déposer préprogrammées avec les techniques de modélisation prédictive.

Dans un espace de travail interactif visuel, vous effectuer un glisser-déplacer de ***jeux de données*** et de ***modules*** d’analyse vers un canevas interactif. Vous les connectez ensemble tooform un ***expérimenter*** que vous exécutez dans Machine Learning Studio.
Vous ***créer un modèle***, ***l’apprentissage du modèle de hello***, et ***score et test de modèle hello***.

Vous pouvez itérer sur la conception du modèle, de modifier l’expérience de hello et son exécution jusqu'à ce qu’il donne vous hello résultats que vous recherchez. Lorsque votre modèle est prêt, vous pouvez le publier en tant que ***service web*** afin que d’autres utilisateurs puissent envoyer de nouvelles données et recevoir des prédictions en retour.

## <a name="open-machine-learning-studio"></a>Ouverture de Machine Learning Studio

tooget main Studio, accédez trop[https://studio.azureml.net](https://studio.azureml.net). Si vous vous êtes déjà connecté à Machine Learning Studio par le passé, cliquez sur **Sign In** (Se connecter). Sinon, cliquez sur **Sign up here** (S’inscrire) et faites votre choix parmi les options gratuites et payantes.

![Connectez-vous à tooMachine Learning Studio][sign-in-to-studio]
<br/>
***Connectez-vous à tooMachine Learning Studio***

## <a name="five-steps-toocreate-an-experiment"></a>Cinq étapes toocreate une expérience

Dans ce didacticiel d’apprentissage machine, vous suivez les cinq étapes de base toobuild une expérience dans Machine Learning Studio toocreate, effectuer l’apprentissage et un score de votre modèle :

- **Création d’un modèle**
    - [Étape 1 : obtention des données]
    - [Étape 2 : Préparer les données de salutation]
    - [Étape 3 : définition des fonctionnalités]
- **Modèle de hello train**
    - [Étape 4 : sélection et application d’un algorithme d’apprentissage]
- **Score et test de modèle hello**
    - [Étape 5 : prédiction des nouveaux prix des voitures]

[Étape 1 : obtention des données]: #step-1-get-data
[Étape 2 : Préparer les données de salutation]: #step-2-prepare-the-data
[Étape 3 : définition des fonctionnalités]: #step-3-define-features
[Étape 4 : sélection et application d’un algorithme d’apprentissage]: #step-4-choose-and-apply-a-learning-algorithm
[Étape 5 : prédiction des nouveaux prix des voitures]: #step-5-predict-new-automobile-prices

> [!TIP] 
> Vous trouverez une copie de travail de hello suivants expérience Bonjour [Cortana Intelligence galerie](https://gallery.cortanaintelligence.com). Accédez trop**[essais de votre première pour la science des données - prévision de prix Automobile](https://gallery.cortanaintelligence.com/Experiment/Your-first-data-science-experiment-Automobile-price-prediction-1)**  et cliquez sur **ouvrir dans Studio** toodownload une copie de l’expérience hello dans votre Machine Learning Espace de travail Studio.


## <a name="step-1-get-data"></a>Étape 1 : obtention des données

Hello première chose apprentissage tooperform donnée.
Vous pouvez utiliser plusieurs exemples de jeux de données inclus dans Machine Learning Studio ou importer des données à partir de sources diverses. Pour cet exemple, nous allons utiliser le jeu de données exemple hello, **(Raw) les données de prix Automobile**, qui est inclus dans votre espace de travail.
Ce jeu de données comprend des entrées relatives à plusieurs véhicules, notamment des informations sur la marque, le modèle, les caractéristiques techniques et le prix.

Voici comment tooget hello dataset dans votre expérience.

1. Créer une nouvelle expérience en cliquant sur **+ nouveau** bas hello de fenêtre de Machine Learning Studio hello, sélectionnez **EXPÉRIMENTER**, puis sélectionnez **expérimenter vide**.

2. expérience de Hello reçoit un nom par défaut que vous pouvez voir en haut hello de zone de dessin hello. Sélectionnez ce texte et renommez-la toosomething explicite, par exemple, **prédiction de prix Automobile**. nom de Hello n’a pas besoin toobe unique.

    ![Renommer l’expérience de hello][rename-experiment]

2. gauche toohello du canevas de l’expérience hello est une palette des jeux de données et des modules. Type **automobile** dans zone de recherche hello haut hello de ce jeu de données toofind palette hello étiqueté **(Raw) les données de prix Automobile**. Faites glisser ce canevas de l’expérience toohello jeu de données.

    ![Rechercher le jeu de données automobile hello et faites glisser sur le canevas de l’expérience hello][type-automobile]
    <br/>
    ***Rechercher le jeu de données automobile hello et faites glisser sur le canevas de l’expérience hello***

toosee quoi ces données ressemble, cliquez sur le port de sortie hello bas hello du jeu de données automobile hello et sélectionnez **visualiser**.

![Cliquez sur le port de sortie hello et sélectionnez « Visualiser »][select-visualize]
<br/>
***Cliquez sur le port de sortie hello et sélectionnez « Visualiser »***

> [!TIP]
> Jeux de données et les modules ont d’entrée et les ports de sortie représentés par petits cercles - ports d’entrée en haut hello, sortie des ports bas hello.
toocreate un flux de données dans votre expérience, vous vous connectez un port de sortie du port d’entrée d’un module tooan d’un autre.
À tout moment, vous pouvez cliquer hello port de sortie d’un toosee de jeu de données ou un module à quelles données hello ressemble à ce stade dans le flux de données hello.

Dans ce jeu de données d’exemple, chaque instance d’une voiture apparaît sous la forme d’une ligne et variables hello associées à chaque automobile apparaissent en tant que colonnes. Étant donné les variables hello pour une automobile spécifique, nous allons prix hello tootry toopredict à droite, colonne (colonne 26, intitulée « price »).

![Afficher les données automobiles hello dans la fenêtre de visualisation de données hello][visualize-auto-data]
<br/>
***Afficher les données automobiles hello dans la fenêtre de visualisation de données hello***

Fenêtre de visualisation hello fermer en cliquant sur hello »**x**» dans le coin supérieur droit de hello.

## <a name="step-2-prepare-hello-data"></a>Étape 2 : Préparer les données de salutation

Pour pouvoir être analysé, un jeu de données nécessite généralement un traitement préalable. Par exemple, vous avez peut-être remarqué hello pas les valeurs présentes dans les colonnes hello de plusieurs lignes. Ces valeurs manquantes doivent toobe nettoyé afin de modèle de hello peut analyser les données de salutation correctement. Dans le cas qui nous occupe, nous allons supprimer toutes les lignes dans lesquelles des valeurs sont manquantes. En outre, hello **pertes normalisées** colonne possède une proportion importante de valeurs manquantes, donc nous allons l’exclure cette colonne à partir du modèle de hello complètement.

> [!TIP]
> Nettoyage hello pas les valeurs à partir des données d’entrée est une condition préalable à l’aide de la plupart des modules de hello.

Tout d’abord, nous ajoutons un module qui supprime hello **pertes normalisées** colonne complètement, et puis nous ajoutons un autre module qui supprime toute ligne qui a des données manquantes.

1. Type **sélectionner des colonnes** dans la zone de recherche hello haut hello Bonjour module palette toofind Bonjour [sélectionner les colonnes dans le jeu de données] [ select-columns] module, puis faites-le glisser canevas de l’expérience toohello . Ce module permet de tooselect les colonnes de données, nous souhaitez tooinclude ou à exclure de hello modèle.

2. Connectez le port de sortie de hello de hello **(Raw) les données de prix Automobile** toohello du jeu de données d’entrée de port de hello [sélectionner les colonnes dans le jeu de données] [ select-columns] module.

    ![Ajoutez le canevas de l’expérience toohello module « Sélectionner les colonnes dans Dataset » hello et connectez-la][type-select-columns]
    <br/>
    ***Ajoutez le canevas de l’expérience toohello module « Sélectionner les colonnes dans Dataset » hello et connectez-la***

3. Cliquez sur hello [sélectionner les colonnes dans le jeu de données] [ select-columns] module et cliquez sur **sélecteur de colonne lancement** Bonjour **propriétés** volet.

    - Sur hello gauche, cliquez sur **avec des règles**
    - Sous **Commencer par**, cliquez sur **Toutes les colonnes**. Cette fonction [sélectionner les colonnes dans le jeu de données] [ select-columns] toopass à toutes les colonnes hello (à l’exception de ces colonnes, nous sommes tooexclude).
    - À partir de hello listes déroulantes, sélectionnez **exclure** et **les noms de colonne**, puis cliquez dans la zone de texte hello. Une liste de colonnes s’affiche. Sélectionnez **pertes normalisées**, et il est la zone de texte toohello ajouté.
    - Cliquez sur hello coche (OK) bouton tooclose hello colonne sélecteur (sur hello inférieur droit).

    ![Lancer le sélecteur de colonne hello et exclure la colonne de hello « pertes normalisées »][launch-column-selector]
    <br/>
    ***Lancer le sélecteur de colonne hello et exclure la colonne de hello « pertes normalisées »***

    Volet de propriétés maintenant hello pour **sélectionner les colonnes dans le jeu de données** indique que celui-ci passe toutes les colonnes à partir du dataset hello sauf **pertes normalisées**.

    ![volet de propriétés Hello montre que cette colonne hello « pertes normalisées » est exclue.][showing-excluded-column]
    <br/>
    ***volet de propriétés Hello montre que cette colonne hello « pertes normalisées » est exclue.***

    > [!TIP]
    Vous pouvez ajouter un module de tooa de commentaire par module de hello en double-cliquant sur et la saisie de texte. Vous pouvez ainsi voir en un coup de œil quel module hello effectue dans votre expérience. Dans ce cas double-cliquez sur hello [sélectionner les colonnes dans le jeu de données] [ select-columns] module et type hello commentaire « Exclure normalisées pertes. »
    >
    >


    ![Double-cliquez sur un module de tooadd un commentaire][add-comment]
    <br/>
    ***Double-cliquez sur un module de tooadd un commentaire***

3. Hello de glisser [Clean Missing Data] [ clean-missing-data] module toohello tester la zone de dessin et le connecter toohello [sélectionner les colonnes dans le jeu de données] [ select-columns] module. Bonjour **propriétés** volet, sélectionnez **supprimer toute ligne** sous **mode de nettoyage**. Cette fonction [Clean Missing Data] [ clean-missing-data] tooclean les données de salutation en supprimant les lignes qui ont des valeurs manquantes. Double-cliquez sur le module de hello et tapez le commentaire hello « Supprimer les lignes de valeur manquant ».

    ![Définir le mode de nettoyage hello trop « supprimer la ligne entière » pour le module de « Nettoyage des données manquantes » hello][set-remove-entire-row]
    <br/>
    ***Définir le mode de nettoyage hello trop « supprimer la ligne entière » pour le module de « Nettoyage des données manquantes » hello***

4. Exécutez hello expérience en cliquant sur **exécuter** bas hello de page de hello.

    Lors de l’expérience de hello est terminée, tous les modules de hello ont tooindicate une coche verte qui ils se sont terminées avec succès. Notez également hello **en cours d’exécution terminé** état dans le coin supérieur droit de hello.

![Après l’avoir exécuté, expérience de hello doit ressembler à ceci][early-experiment-run]
<br/>
***Après l’avoir exécuté, expérience de hello doit ressembler à ceci***

> [!TIP]
> Pourquoi nous exécutez hello expérience maintenant ? Par l’expérience hello en cours d’exécution, les définitions de colonne hello pour nos données passent à partir du dataset hello, via hello [sélectionner les colonnes dans le jeu de données] [ select-columns] module et par le biais hello [Clean Missing Data] [ clean-missing-data] module. Cela signifie que tous les modules de nous connecter trop[Clean Missing Data] [ clean-missing-data] aura également ces mêmes informations.

Nous avons effectué dans expérience hello toothis point hello nouvelle donnée. Si vous souhaitez tooview hello nettoyé dataset, cliquez sur hello gauche du port de sortie de hello [Clean Missing Data] [ clean-missing-data] module et sélectionnez **visualiser**. Notez que hello **pertes normalisées** colonne n’est plus incluse, et aucune valeur manquante.

Maintenant que les données de salutation sont propre, nous sommes prêt toospecify les fonctionnalités que nous vous allez toouse dans le modèle de prévision hello.

## <a name="step-3-define-features"></a>Étape 3 : définition des fonctionnalités

Dans Machine Learning, les *fonctionnalités* sont des propriétés individuelles mesurables d’un élément qui vous intéresse. Dans notre jeu de données, chaque ligne représente un véhicule et chaque colonne une fonctionnalité de ce véhicule.

Recherche d’un bon jeu de fonctionnalités pour la création d’un modèle de prévision requiert expérimentation et la base de connaissances sur le problème de hello souhaité toosolve. Certaines fonctionnalités sont mieux adaptées pour la prédiction cible hello que d’autres. En outre, certaines fonctionnalités ont une forte corrélation avec d’autres fonctionnalités et peuvent être supprimées. Par exemple, ville-mpg et mpg de bus sont étroitement liés afin que nous pouvons conserver l’un et supprimer hello autres sans trop affecter la prédiction de hello.

Commençons par créer un modèle qui utilise un sous-ensemble de fonctionnalités de hello dans notre jeu de données. Vous pouvez revenir plus tard et sélectionner des fonctionnalités différentes, réexécutez l’expérience de hello et voir si vous obtenez les meilleurs résultats. Mais toostart, essayons hello suivant de fonctionnalités :

    make, body-style, wheel-base, engine-size, horsepower, peak-rpm, highway-mpg, price


1. Faites glisser une autre [sélectionner les colonnes dans le jeu de données] [ select-columns] module toohello expérimenter la zone de dessin. Se connecter hello gauche du port de sortie de hello [Clean Missing Data] [ clean-missing-data] entrée toohello de module de hello [sélectionner les colonnes dans le jeu de données] [ select-columns] module.

    ![Se connecter hello « Sélectionner les colonnes dans Dataset » toohello « Nettoyage des données manquantes » un module][connect-clean-to-select]
    <br/>
    ***Se connecter hello « Sélectionner les colonnes dans Dataset » toohello « Nettoyage des données manquantes » un module***

2. Double-cliquez sur le module de hello et tapez « Sélectionner les fonctionnalités pour la prédiction. »

2. Cliquez sur **sélecteur de colonne lancement** Bonjour **propriétés** volet.

3. Cliquez sur **With rules**(À l’aide de règles).

4. Sous **Commencer par**, cliquez sur **Aucune colonne**. Dans la ligne de filtre hello, sélectionnez **Include** et **les noms de colonnes** et sélectionnez la liste des noms de colonne dans la zone de texte hello. Cette fonction hello module toonot pass-through toutes les colonnes (fonctions), sauf ceux qui nous spécifions hello.

5. Cliquez sur le bouton de case à cocher (OK) hello.

    ![Sélectionnez tooinclude de colonnes (fonctions) hello dans une prédiction de hello][select-columns-to-include]
    <br/>
    ***Sélectionnez tooinclude de colonnes (fonctions) hello dans une prédiction de hello***

Cela produit un jeu de données filtré contenant uniquement pour les fonctions hello que nous souhaitons toohello toopass algorithme, que nous allons utiliser à l’étape suivante de hello d’apprentissage. Plus tard, vous pouvez reprendre la procédure en utilisant une autre sélection de fonctionnalités.

## <a name="step-4-choose-and-apply-a-learning-algorithm"></a>Étape 4 : sélection et application d’un algorithme d’apprentissage

Maintenant que les données de salutation sont prêtes, la construction d’un modèle de prévision se compose de formation et de test. Nous allons utiliser notre modèle de hello tootrain données, puis nous testerons hello modèle toosee plus proche, il est en mesure de toopredict prix.
<!-- For now, don't worry about *why* we need tootrain and then test a model.-->

La *classification* et la *régression* sont deux types d’algorithmes de machine learning supervisé. La classification permet de prédire une réponse à partir d'un jeu de catégories défini, comme une couleur (rouge, bleu ou vert). La régression est toopredict utilisé un nombre.

Étant donné que nous souhaitons prix toopredict, qui est un nombre, nous allons utiliser un algorithme de régression. Dans cet exemple, nous allons utiliser un modèle simple de *régression linéaire*.

> [!TIP]
> Si vous souhaitez toolearn plus d’informations sur les différents types d’algorithmes d’apprentissage automatique et lorsque toouse les, vous pourrez afficher la première vidéo de hello Bonjour science des données pour la série de débutants, [hello cinq questions réponses de science des données](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md). Vous pouvez également consulter graphisme d’information hello [Machine principes de base avec des exemples de l’algorithme d’apprentissage](machine-learning-basics-infographic-with-algorithm-examples.md), ou extrayez hello [Machine learning aide-mémoire algorithme](machine-learning-algorithm-cheat-sheet.md).

Nous former le modèle de hello en lui donnant un jeu de données qui inclut les prix hello. modèle de Hello analyse les données de salutation et recherchez des corrélations entre les fonctionnalités d’une voiture et son prix. Puis nous allons le tester le modèle de hello - nous allons lui donner un ensemble de fonctionnalités pour automobiles que nous connaissons et voir comment fermer modèle de hello proviennent des prix de toopredicting hello connus.

Nous allons utiliser nos données pour l’apprentissage du modèle de hello et tester en fractionnant les données de salutation en distinct d’apprentissage et jeux de données de test.

1. Sélectionnez et faites glisser hello [données fractionnées] [ split] module toohello tester la zone de dessin et le connecter toohello dernière [sélectionner les colonnes dans le jeu de données] [ select-columns] module.

2. Cliquez sur hello [données fractionnées] [ split] module tooselect il. Recherche hello **Fraction de lignes Bonjour tout d’abord de sortie dataset** (Bonjour **propriétés** toohello volet à droite de la zone de dessin hello) et la définir too0.75. Ainsi, nous allons utiliser 75 pour cent hello tootrain hello un modèle de données et maintenez la touche Retour 25 pour cent de test (une version ultérieure, vous pouvez expérimenter l’utilisation de différents pourcentages).

    ![Hello ensemble fractionner la fraction de hello « Données fractionnées » module too0.75][set-split-data-percentage]
    <br/>
    ***Hello ensemble fractionner la fraction de hello « Données fractionnées » module too0.75***

    > [!TIP]
    > En modifiant hello **valeur initiale aléatoire** paramètre, vous pouvez générer des échantillons aléatoires différents pour l’apprentissage et de test. Ce paramètre contrôle hello l’amorçage du Générateur de nombres pseudo-aléatoires hello.

2. Exécutez l’expérience de hello. Lors de l’expérience de hello est exécuté, hello [sélectionner les colonnes dans le jeu de données] [ select-columns] et [données fractionnées] [ split] modules passer toohello des définitions de colonne Nous allons ensuite ajouter les modules.  

3. hello tooselect algorithme d’apprentissage développez hello **Machine Learning** catégorie dans hello module toohello palette gauche de hello canevas, puis développez **initialiser le modèle**. Cela affiche plusieurs catégories de modules qui peuvent être des algorithmes d’apprentissage tooinitialize utilisé. Pour cette expérience, sélectionnez hello [régression linéaire] [ linear-regression] module sous hello **régression** catégorie et faites-le glisser toohello canevas de l’expérience.
(Vous pouvez également trouver module de hello en tapant « régression linéaire » dans la zone de recherche de palette hello).

4. Rechercher et faites glisser hello [Train Model] [ train-model] module toohello expérimenter la zone de dessin. Connectez la sortie hello Hello [régression linéaire] [ linear-regression] module toohello gauche entrée Hello [Train Model] [ train-model] module et connectez-vous hello apprentissage de sortie des données (port de gauche) de hello [données fractionnées] [ split] entrée droite de module toohello Hello [Train Model] [ train-model] module.

    ![Connectez les hello « Train Model » module tooboth hello « Régression linéaire » et « Données fractionnées » modules][connect-train-model]
    <br/>
    ***Connectez les hello « Train Model » module tooboth hello « Régression linéaire » et « Données fractionnées » modules***

5. Cliquez sur hello [Train Model] [ train-model] module, cliquez sur **sélecteur de colonne lancement** Bonjour **propriétés** volet, puis sélectionnez hello **prix** colonne. Il s’agit de valeur hello que notre modèle est continu toopredict.

    Vous sélectionnez hello **prix** colonne dans le sélecteur de colonne hello en le déplaçant de hello **colonnes disponibles** liste toohello **colonnes sélectionnées** liste.

    ![Sélectionnez la colonne du prix hello pour le module de « Train Model » hello][select-price-column]
    <br/>
    ***Sélectionnez la colonne du prix hello pour le module de « Train Model » hello***

6. Exécutez l’expérience de hello.

Nous disposons désormais d’un modèle de régression formé qui peut être utilisé tooscore nouvelles données automobile toomake prix prédictions.

![Après l’exécution, expérience de hello doit maintenant ressembler à ceci][second-experiment-run]
<br/>
***Après l’exécution, expérience de hello doit maintenant ressembler à ceci***

## <a name="step-5-predict-new-automobile-prices"></a>Étape 5 : prédiction des nouveaux prix des voitures

Maintenant que nous avons formé le modèle de hello à l’aide de 75 pour cent de nos données, nous pouvons utiliser tooscore hello autres 25 pour cent de toosee de données hello degré nos fonctions de modèle.

1. Rechercher et faites glisser hello [Score Model] [ score-model] module toohello expérimenter la zone de dessin. Connectez la sortie hello Hello [Train Model] [ train-model] toohello module gauche d’un port d’entrée de [Score Model][score-model]. Se connecter hello test sortie des données (port de droite) de hello [données fractionnées] [ split] toohello module droit d’entrée de port de [Score Model][score-model].

    ![Se connecter hello « Modèle de Score » module tooboth hello « Train Model » et « Données fractionnées » modules][connect-score-model]
    <br/>
    ***Se connecter hello « Modèle de Score » module tooboth hello « Train Model » et « Données fractionnées » modules***

2. Exécutez hello expérience et affichage de la sortie à partir de hello hello [Score Model] [ score-model] module (cliquez sur le port de sortie hello du [Score Model] [ score-model] et sélectionnez **Visualiser**). montre la sortie Hello hello valeurs prédites pour un prix et hello des valeurs connues à partir des données de test hello.  

    ![Sortie de module de « Modèle de Score » hello][score-model-output]
    <br/>
    ***Sortie de module de « Modèle de Score » hello***

3. Enfin, nous testons la qualité des résultats de hello hello. Sélectionnez et faites glisser hello [modèle Evaluate] [ evaluate-model] toohello de module d’expérimenter canevas et connectez sortie hello Hello [Score Model] [ score-model] toohello module gauche de l’entrée de [modèle Evaluate][evaluate-model].

    > [!TIP]
    > Il existe deux ports d’entrée sur hello [modèle Evaluate] [ evaluate-model] module, car il peut être utilisé toocompare deux modèles côte à côte. Une version ultérieure, vous pouvez ajouter une autre expérience de toohello algorithme et utiliser [modèle Evaluate] [ evaluate-model] toosee celui qui donne de meilleurs résultats.

4. Exécutez l’expérience de hello.

sortie hello tooview hello [modèle Evaluate] [ evaluate-model] module, cliquez sur le port de sortie hello et sélectionnez **visualiser**.

![Résultats d’évaluation pour une expérience de hello][evaluation-results]
<br/>
***Résultats d’évaluation pour une expérience de hello***

Hello suit les statistiques est affiché pour notre modèle :

- **Erreur d’absolue moyenne** (MAE) : hello moyenne des erreurs absolus (un *erreur* est la différence de hello hello prédit la valeur et la valeur réelle de hello).
- **Erreur quadratique moyenne de racine** (RMSE) : hello racine carrée moyenne hello d’erreurs au carré de prédictions effectués sur le jeu de données de test hello.
- **Erreur absolue relative**: hello moyenne des erreurs absolu relatif toohello absolue de la différence entre les valeurs réelles et moyenne hello de toutes les valeurs réelles.
- **Erreur quadratique relative**: toohello relatif d’erreur quadratique moyenne hello carré de la différence entre les valeurs réelles hello et moyenne hello de toutes les valeurs réelles.
- **Coefficient de détermination**: hello également appelé **carré de la valeur R**, il s’agit d’une mesure statistique qui indique comment un modèle correspond à des données de hello.

Pour chaque erreur de hello statistiques, la plus petite sont préférable. Une valeur inférieure indique que les prédictions hello plus proche les valeurs réelles hello. Pour **Coefficient de détermination**, hello proche sa valeur est tooone (1.0), meilleures prédictions de hello hello.

## <a name="final-experiment"></a>Expérience finale

expérience finale de Hello doit ressembler à ceci :

![expérience de final Hello][complete-linear-regression-experiment]
<br/>
***expérience de final Hello***

## <a name="next-steps"></a>Étapes suivantes

Maintenant que vous avez terminé hello première machine learning didacticiel et que vous avez votre expérience de configuration, vous pouvez continuer de modèle de hello tooimprove et ensuite le déployer en tant qu’un service web prédictif.

- **Itérer au sein du modèle de hello tootry tooimprove** -par exemple, vous pouvez modifier les fonctionnalités de hello vous utilisez dans votre prédiction. Ou vous pouvez modifier les propriétés de hello Hello [régression linéaire] [ linear-regression] algorithme ou essayez un autre algorithme complètement. Vous pouvez même ajouter plusieurs expérience d’apprentissage algorithmes tooyour en même temps et comparer deux d'entre eux à l’aide de hello [modèle Evaluate] [ evaluate-model] module.
Pour obtenir un exemple de toocompare plusieurs modèles dans une expérience unique, voir [Compare Regressors](https://gallery.cortanaintelligence.com/Experiment/Compare-Regressors-5) Bonjour [Cortana Intelligence galerie](https://gallery.cortanaintelligence.com).

    > [!TIP]
    > toocopy une itération de votre expérience, utilisez hello **SAVE AS** bouton bas hello de page de hello. Vous pouvez voir toutes les itérations hello de votre expérience en cliquant sur **afficher l’historique d’exécution** bas hello de page de hello. Pour en savoir plus, consultez la section [Gérer les itérations des expériences dans Microsoft Azure Machine Learning Studio][runhistory].

[runhistory]: machine-learning-manage-experiment-iterations.md

- **Déployer le modèle hello comme un service web prédictif** : quand vous êtes satisfait de votre modèle, vous pouvez le déployer comme un toobe de service web utilisé toopredict « prix automobile » à l’aide de nouvelles données. Consultez la section [Déployer un service web Microsoft Azure Machine Learning][publish] pour en savoir plus.

[publish]: machine-learning-publish-a-machine-learning-web-service.md

Vous souhaitez toolearn plus ? Pour une présentation plus complète et détaillée du processus de création, la formation, calculer les scores et déploiement d’un modèle de hello, consultez [développer une solution prédictive à l’aide d’Azure Machine Learning][walkthrough].

[walkthrough]: machine-learning-walkthrough-develop-predictive-solution.md

<!-- Images -->
[sign-in-to-studio]: ./media/machine-learning-create-experiment/sign-in-to-studio.png
[rename-experiment]: ./media/machine-learning-create-experiment/rename-experiment.png
[visualize-auto-data]:./media/machine-learning-create-experiment/visualize-auto-data.png
[select-visualize]: ./media/machine-learning-create-experiment/select-visualize.png
[showing-excluded-column]:./media/machine-learning-create-experiment/showing-excluded-column.png
[set-remove-entire-row]:./media/machine-learning-create-experiment/set-remove-entire-row.png
[early-experiment-run]:./media/machine-learning-create-experiment/early-experiment-run.png
[select-columns-to-include]:./media/machine-learning-create-experiment/select-columns-to-include.png
[second-experiment-run]:./media/machine-learning-create-experiment/second-experiment-run.png
[connect-score-model]:./media/machine-learning-create-experiment/connect-score-model.png
[evaluation-results]:./media/machine-learning-create-experiment/evaluation-results.png
[complete-linear-regression-experiment]:./media/machine-learning-create-experiment/complete-linear-regression-experiment.png

<!-- temporarily switching GIFs tooPNGs tooremove animation --> 
[type-automobile]:./media/machine-learning-create-experiment/type-automobile.png
[type-select-columns]:./media/machine-learning-create-experiment/type-select-columns.png
[launch-column-selector]:./media/machine-learning-create-experiment/launch-column-selector.png
[add-comment]:./media/machine-learning-create-experiment/add-comment.png
[connect-clean-to-select]:./media/machine-learning-create-experiment/connect-clean-to-select.png

[set-split-data-percentage]:./media/machine-learning-create-experiment/set-split-data-percentage.png

<!-- temporarily switching GIFs tooPNGs tooremove animation --> 
[connect-train-model]:./media/machine-learning-create-experiment/connect-train-model.png
[select-price-column]:./media/machine-learning-create-experiment/select-price-column.png

[score-model-output]:./media/machine-learning-create-experiment/score-model-output.png

<!-- Module References -->
[evaluate-model]: https://msdn.microsoft.com/library/azure/927d65ac-3b50-4694-9903-20f6c1672089/
[linear-regression]: https://msdn.microsoft.com/library/azure/31960a6f-789b-4cf7-88d6-2e1152c0bd1a/
[clean-missing-data]: https://msdn.microsoft.com/library/azure/d2c5ca2f-7323-41a3-9b7e-da917c99f0c4/
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
