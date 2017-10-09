---
title: "l’équipe d’ingénierie de science des données aaaFeature | Documents Microsoft"
description: "Explique à des fins de hello d’ingénierie de fonctionnalité et fournit des exemples de son rôle dans le processus d’amélioration de données hello de l’apprentissage."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 3fde69e8-5e7b-49ad-b3fb-ab8ef6503a4d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: zhangya;bradsev
ms.openlocfilehash: af40ea9cc9395bc87fe695eeaef26aa71e0ec9e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="feature-engineering-in-data-science"></a>Ingénierie des caractéristiques dans la science des données
Cette rubrique explique à des fins de hello d’ingénierie de fonctionnalité et fournit des exemples de son rôle dans le processus d’amélioration de données hello de l’apprentissage. les exemples de Hello utilisés tooillustrate ce processus sont dessinées à partir d’Azure Machine Learning Studio. 

[!INCLUDE [cap-create-features-data-selector](../../includes/cap-create-features-selector.md)]

Cela **menu** lie tootopics qui décrivent comment toocreate pour les données dans différents environnements. Cette tâche est une étape Bonjour [processus de science des données équipe (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).

Fonctionnalité ingénierie tentatives tooincrease hello prédictif d’algorithmes d’apprentissage en créant des fonctionnalités à partir des données brutes qui facilitent le processus d’apprentissage de hello. Hello d’ingénierie et sélection de fonctionnalités est un composant d’hello TDSP décrites dans hello [quel est le cycle de vie des processus de science des données équipe hello ?](data-science-process-overview.md) Ingénierie de fonctionnalité et de sélection sont les parties de hello **développer les fonctionnalités** étape Hello TDSP. 

* **l’équipe d’ingénierie de fonctionnalité**: ce processus tente d’exécuter des fonctionnalités supplémentaires pertinentes toocreate dans les fonctionnalités existantes brutes hello dans les données de salutation et tooincrease hello prédictif de l’algorithme d’apprentissage hello.
* **sélection des fonctionnalités**: ce processus sélectionne un sous-ensemble de clés de hello des fonctionnalités de données d’origine dans une dimensionnalité de hello tooreduce tentative de problème de formation hello.

Normalement **l’équipe d’ingénierie de fonctionnalité** est appliqué première toogenerate des fonctionnalités supplémentaires, puis hello **sélection des fonctionnalités** étape est effectuée tooeliminate hautement corrélée inutile ou redondante fonctionnalités.

données d’apprentissage Hello en apprentissage peuvent souvent être améliorées par extraction de fonctionnalités à partir des données brutes de hello collectées. Un exemple d’une fonction d’ingénierie dans le contexte hello d’apprendre comment tooclassify les images de hello de caractères manuscrites est la création d’un peu de mappage de densité construite à partir de données de distribution bits bruts hello. Ce mappage permet de rechercher des bords hello de caractères de hello plus efficacement que simplement à l’aide distribution brutes de hello directement.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="creating-features-from-your-data---feature-engineering"></a>Création de caractéristiques à partir de vos données - Conception de caractéristiques
données d’apprentissage Hello se comprennent d’une matrice composée d’exemples (enregistrements ou observations stockées dans les lignes), chacun d’eux a un ensemble de fonctionnalités (variables ou stockées dans des colonnes de champs). fonctionnalités de Hello spécifiées dans expérimental hello sont des modèles de hello toocharacterize attendu dans les données de salutation. Bien que la plupart des champs peuvent être inclus directement dans des données brutes hello hello fonctionnalité sélectionnée jeu utilisé tootrain un modèle, il arrive souvent hello (ingénieries) des fonctionnalités supplémentaires nécessitant toobe construite à partir de fonctions hello dans toogenerate des données brutes hello une version améliorée jeu de données d’apprentissage.

Le type de fonctionnalités doit être créé tooenhance hello dataset lors de l’apprentissage d’un modèle ? Ingénierie fonctionnalités qui améliorent la formation de hello fournissent des informations qui différencie mieux les modèles hello dans les données de salutation. Nous pensons que hello nouvelles fonctionnalités tooprovide des informations supplémentaires qui ne sont pas clairement capturé ou facile à détecter dans hello fonctionnalité d’origine ou existante ensemble. Mais ce processus est tout un art. Des décisions réfléchies et productives nécessitent souvent une spécialisation dans le domaine.

Lorsque vous démarrez avec Azure Machine Learning, il est plus simple toograsp ce processus à l’aide de concrètement les exemples fourni dans hello Studio. Deux exemples sont présentés ici :

* Un exemple de régression [prédiction du nombre de hello de locations de vélo](http://gallery.cortanaintelligence.com/Experiment/Regression-Demand-estimation-4) dans une expérience contrôlée, où les valeurs cibles de hello sont connus
* un exemple de classification d'exploration de texte utilisant le [hachage de caractéristiques](https://msdn.microsoft.com/library/azure/c9a82660-2d9c-411d-8122-4d9e0b3ce92a/)

## <a name="example-1-adding-temporal-features-for-regression-model"></a>Exemple 1 : ajout de caractéristiques temporelles pour le modèle de régression
Nous allons utiliser hello expérience « prévision de la demande de bicyclettes » dans toodemonstrate Azure Machine Learning Studio comment tooengineer fonctionnalités pour une tâche de régression. Hello cette expérience vise à la demande de hello toopredict des vélos hello, autrement dit, le numéro de hello de Locations bike au sein d’une mois/jour/heure spécifique. Hello du jeu de données « Bike location UCI dataset » est utilisé en tant que données d’entrée brutes de hello. Ce jeu de données est basée sur des données réelles provenant d’hello entreprise majuscule Bikeshare qui tient à jour un réseau de location de vélo dans Washington DC Bonjour États-Unis. Hello dataset représente le nombre de hello de locations de vélo au sein d’une heure spécifique d’un jour dans les années hello 2011 et année 2012 et contient 17379 lignes et 17 colonnes. ensemble de fonctionnalités brutes de Hello contient des conditions météorologiques (température/humidité/vent) et type hello du jour de hello (vacances/jour ouvrable). Hello champ toopredict est « cnt », un nombre qui représente des locations de vélo hello au sein d’une heure spécifique et qui est comprise entre 1 too977 les plages.

Avec comme objectif hello construction de fonctionnalités efficaces dans les données d’apprentissage hello, quatre modèles de régression sont générés à l’aide de hello même algorithme, mais avec quatre jeux de données d’apprentissage différentes. Hello quatre jeux de données représentent hello les mêmes données d’entrée brutes, mais avec un nombre croissant de fonctionnalités défini. Ces caractéristiques sont regroupées en quatre catégories :

1. A = météo, congé + weekday + week-end fonctionnalités jour prédite de hello
2. B = nombre de bicyclettes qui ont été louées dans chacun des hello 12 dernières heures
3. C = nombre de bicyclettes qui ont été louées dans chacun des hello précédentes 12 jours à hello même heure
4. D = nombre de bicyclettes qui ont été louées dans chacun des hello 12 semaines précédentes hello même heure et hello même jour

Outre la fonctionnalité set A, qui existent déjà dans les données brutes d’origine hello, hello autres trois ensembles de fonctionnalités sont créés via la fonctionnalité hello processus d’ingénierie. Ensemble de fonctionnalités B captures très récente à la demande pour les vélos hello. Fonctionnalité définie C captures à la demande de hello pour vélos à une heure spécifique. Fonctionnalité définie à la demande de capture D pour bicyclettes à l’heure et jour de semaine de hello particulier. Hello quatre formation datasets chaque inclut un ensemble de fonctionnalités, A + B, A + B + C et A + B + C + D, respectivement.

Bonjour expérience Azure Machine Learning, ces quatre jeux de données d’apprentissage est formées par quatre branches à partir du jeu de données d’entrée prétraitées hello. Sauf hello gauche la plupart des succursales, chacune de ces branches contient un [Execute R Script](https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/) module, dans lequel un ensemble de fonctionnalités dérivées (définie de fonctionnalité B, C et D) sont respectivement construit et ajouté toohello importé le jeu de données. Hello figure suivante illustre les script hello R ensemble de fonctionnalités toocreate B dans la deuxième branche de gauche hello.

![création de caractéristiques](./media/machine-learning-data-science-create-features/addFeature-Rscripts.png)

Bonjour la comparaison des résultats de performance hello Hello quatre modèles sont résumés dans hello tableau suivant. obtenir les meilleurs résultats Hello sont affichés par les fonctionnalités A + B + C. Notez que hello diminue de taux d’erreur lors de l’ensemble des fonctionnalités supplémentaires sont inclus dans les données d’apprentissage hello. Il vérifie notre présomption que jeu de fonctionnalités hello B, C fournissent des informations supplémentaires pertinentes pour la tâche de régression hello. Mais la fonctionnalité d’ajout hello D ne semble pas tooprovide toute réduction supplémentaire de taux d’erreur hello.

![comparaison des résultats](./media/machine-learning-data-science-create-features/result1.png)

## <a name="example2"></a> Exemple 2 : création de caractéristiques dans l'exploration de texte
Ingénierie de fonctionnalité est largement appliquée dans tootext associées à des tâches d’exploration de données, tels que l’analyse de classification et l’opinion de document. Par exemple, quand nous souhaitons tooclassify documents en plusieurs catégories, une hypothèse classique est que word hello ou incluses dans la catégorie d’un document d’expressions sont moins susceptibles de toooccur dans une autre catégorie de document. Autrement dit, fréquence hello de distribution des mots ou d’expressions hello doit être toocharacterize en mesure de document différentes catégories. Dans les applications d’exploration de données de texte, des parties du contenu de texte servent généralement les données d’entrée hello, fonctionnalité hello processus d’ingénierie étant fonctionnalités hello toocreate nécessaires de fréquences de mot/expression.

tooachieve cette tâche, une technique appelée **fonctionnalité hachage** est appliqué tooefficiently activer les fonctionnalités de texte arbitraire dans l’index. Au lieu d’associer chaque fonctionnalité (mots ou d’expressions) tooa particulier index de texte, cette méthode fonctionne en appliquant une fonctionnalités de toohello de fonction de hachage et de directement à l’aide de leurs valeurs de hachage en tant qu’index.

Dans Azure Machine Learning, il existe un module de [hachage de caractéristiques](https://msdn.microsoft.com/library/azure/c9a82660-2d9c-411d-8122-4d9e0b3ce92a/) qui crée en toute facilité ces caractéristiques de mot ou expression. La figure suivante montre un exemple d'utilisation de ce module. jeu de données d’entrée Hello contient deux colonnes : hello évaluation book allant de 1 too5 et hello contenu de révision proprement dite. objectif Hello de cette [Feature Hashing](https://msdn.microsoft.com/library/azure/c9a82660-2d9c-411d-8122-4d9e0b3ce92a/) module est tooretrieve un certain nombre de nouvelles fonctionnalités qui indiquent la fréquence d’occurrence hello Hello correspondant ou les mots / phrase au sein de la révision de livre spécifique hello. toouse ce module, nous devons hello toocomplete comme suit :

* Tout d’abord, sélectionnez les colonnes hello qui contient le texte d’entrée hello (« Col2 » dans cet exemple).
* Ensuite, définissez hello too8 de « Taille de bit hachage », ce qui signifie que 2 ^ 8 = 256 fonctionnalités seront créées. Hello word ou une phase dans tout le texte hello sera too256 haché indices. le paramètre Hello « Taille de bit hachage » varie de 1 too31. Hello ou les mots ou les phrases sont moins susceptibles de toobe hachée en hello même si elle toobe un plus grand nombre d’index.
* Troisièmement, définissez too2 de paramètre « N-grammes » hello. Il obtient la fréquence d’occurrence hello d’unigrammes (il s’agit d’une fonctionnalité pour tous les mots) et les bigrammes (il s’agit d’une fonctionnalité pour chaque paire de mots adjacents) hello texte d’entrée. Hello paramètre « N-grammes » comprise too10 0, ce qui indique le nombre maximal de hello de mots séquentiel toobe inclus dans une fonctionnalité.  

![Module « hachage de caractéristiques »](./media/machine-learning-data-science-create-features/feature-Hashing1.png)

Hello figure suivante montre ce que hello ces nouvelles fonctionnalités ressemble.

![Exemple « hachage de caractéristiques »](./media/machine-learning-data-science-create-features/feature-Hashing2.png)

## <a name="conclusion"></a>Conclusion
Fonctionnalités d’ingénierie et sélectionnées accroître l’efficacité de hello du processus d’apprentissage hello qui essaie d’informations de clé de hello tooextract contenues dans les données de salutation. Ils améliorent également power hello de ces modèles tooclassify hello d’entrée de données avec précision et toopredict des résultats d’intéressent plus efficacement. Ingénierie de fonctionnalité et de sélection peuvent également combiner des toomake d’apprentissage automatique hello en plus de calculs souple. Il le fait en améliorant et réduction de plusieurs fonctionnalités hello nécessaires toocalibrate ou effectuer l’apprentissage d’un modèle. Strictement mathématique, modèle de hello hello fonctionnalités tootrain sélectionné sont un ensemble minimal de variables indépendantes qui expliquent les schémas hello dans les données de salutation et puis prédire les résultats avec succès.

Notez qu’il n’est pas toujours nécessairement sélection de fonctionnalité ou de l’équipe d’ingénierie de fonctionnalité tooperform. Si elle est nécessaire ou non dépend des données hello nous avons ou collecter, algorithme hello que prendre, et hello l’objectif de l’expérience de hello.

