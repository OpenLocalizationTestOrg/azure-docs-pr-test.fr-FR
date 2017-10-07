---
title: "aaaClean et préparer les données pour Azure Machine Learning | Documents Microsoft"
description: "Tooprepare de prétraitement et de nettoyer les données pour l’apprentissage."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: bdf659ec-4881-4324-8b9c-747cbfa0c3cd
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: 3e3c3e4b0cfb9187f5820d7165e6ee1ea013ba02
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tasks-tooprepare-data-for-enhanced-machine-learning"></a>Données de tooprepare de tâches pour l’apprentissage améliorée
Le prétraitement et le nettoyage des données sont des tâches importantes qui doivent intervenir avant d'utiliser un jeu de données à des fins d'apprentissage automatique. Les données brutes sont souvent bruyantes, peu fiables et incomplètes. Leur utilisation pour la modélisation peut générer des résultats trompeurs. Ces tâches font partie du processus de science des données équipe (TDSP) de hello et suivent généralement une exploration initiale d’une toodiscover de jeu de données utilisé et le plan hello pré-traitement requis. Pour plus d’instructions sur le processus TDSP hello, consultez les étapes hello hello [processus de science des données équipe](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).

De pré-traitement et de tâches de nettoyage, comme la tâche exploration de données hello, peuvent être effectuées dans un large éventail d’environnements, tels que SQL ou d’une ruche ou d’Azure Machine Learning Studio et avec plusieurs outils et langages, tels que R ou Python, en fonction de ces données stockées et la mise en forme. Étant donné que TDSP est itératif par nature, ces tâches peuvent avoir lieu à différentes étapes d’un flux de travail hello du processus de hello.

Cet article présente différents concepts et tâches de prétraitement des données, à effectuer avant ou après l'intégration de ces données dans Azure Machine Learning.

Pour obtenir un exemple d’exploration de données et de prétraitement effectué dans Azure Machine Learning studio, consultez hello [prétraitement des données dans Azure Machine Learning Studio](https://azure.microsoft.com/documentation/videos/preprocessing-data-in-azure-ml-studio/) vidéo.

## <a name="why-pre-process-and-clean-data"></a>Pourquoi prétraiter et nettoyer les données ?
Données du monde réel sont rassemblées à partir de différentes sources et processus et il peuvent contenir des irrégularités ou données endommagées compromettre la qualité de hello du jeu de données hello. problèmes de qualité des données par défaut Hello qui surviennent sont :

* **Caractère incomplet :**des valeurs ou des attributs sont manquants.
* **Bruit :**les données contiennent des enregistrements erronés ou des aberrations.
* **Incohérence :**les données contiennent des enregistrements en conflit ou des contradictions.

La qualité des données est essentielle pour obtenir des modèles prédictifs performants. tooavoid « garbage dans garbage out » et améliorer la qualité des données et par conséquent, les performances de modèle, il est impératif tooconduct un toospot d’écran de contrôle d’intégrité données données émet tôt et décider de hello correspondant le traitement des données et de nettoyage des étapes.

## <a name="what-are-some-typical-data-health-screens-that-are-employed"></a>Quels sont les critères d’intégrité des données généralement employés ?
Nous pouvons vérifier hello général de qualité de données en activant :

* Hello nombre de **enregistrements**.
* Hello nombre de **attributs** (ou **fonctionnalités**).
* attribut de Hello **des types de données** (nominal, ordinale ou continu).
* Hello nombre de **les valeurs manquantes**.
* **Du code** de données de hello.
  * Si les données de salutation sont TSV ou volume partagé de cluster, vérifiez que les séparateurs de colonnes hello et les séparateurs de ligne toujours correctement séparent les colonnes et lignes.
  * Si les données de salutation sont au format HTML ou XML, vérifiez si les données de salutation sont correct en fonction sur leurs normes respectifs.
  * L’analyse peut également être nécessaire dans les informations sur les commandes tooextract structuré à partir des données structurées ou semi-structurées.
* **Enregistrements de données incohérents**. Vérifiez la plage hello de valeurs sont autorisées. par exemple, si les données de salutation contient amp étudiant, vérifiez si hello amp est Bonjour désigné de plage, par exemple 0 ~ 4.

Lorsque vous rencontrez des problèmes liés aux données, **étapes de traitement** sont nécessaires, ce qui implique souvent un nettoyage des valeurs manquantes, normalisation des données, discrétisation, tooremove de traitement de texte et/ou de remplacer des caractères incorporés, ce qui peuvent affecter alignement des données, mixtes types de données en commun les champs et autres.

**Azure Machine Learning n'exploite que les données tabulaires bien formées**.  Si les données de salutation sont déjà dans un format tabulaire, avant le traitement des données peut être effectué directement avec Azure Machine Learning Bonjour Machine Learning Studio.  Si les données ne sont pas dans un format tabulaire, son mot à dire qu’il est au format XML, l’analyse peut être nécessaire dans le formulaire tootabular données commande tooconvert hello.  

## <a name="what-are-some-of-hello-major-tasks-in-data-pre-processing"></a>Quelles sont des tâches importantes hello dans avant le traitement des données ?
* **Nettoyage des données :**compléter les valeurs manquantes, détecter et supprimer les données bruyantes et les aberrations.
* **Transformation de données**: normaliser le bruit et des dimensions de tooreduce de données.
* **Réduction des données :**échantillonner les enregistrements de données ou les attributs pour faciliter la manipulation des données.
* **Discrétisation des données**: attributs toocategorical pour faciliter l’utilisation d’attributs Convert continue avec certaines méthodes d’apprentissage.
* **Nettoyage du texte :**supprimer les caractères intégrés pouvant perturber l’alignement des données (comme les tabulations dans un fichier TSV), les nouvelles lignes qui peuvent interrompre des enregistrements, etc.

les sections Hello ci-dessous décrit en détail certaines de ces étapes de traitement des données.

## <a name="how-toodeal-with-missing-values"></a>Comment toodeal sans les valeurs ?
toodeal avec des valeurs manquantes, il est préférable de toofirst identifier la raison de hello pour hello manquant de valeurs problème de hello toobetter handle. Les méthodes les plus courantes de traitement des valeurs manquantes sont les suivantes :

* **Suppression :**supprimer les enregistrements ayant des valeurs manquantes.
* **Remplacement par une valeur factice :** remplacer des valeurs manquantes par une valeur factice : par exemple, *inconnu* pour les valeurs catégorielles ou 0 pour les valeurs numériques.
* **Moyenne de substitution**: si les données manquantes hello sont numériques, remplacez les valeurs manquantes hello moyenne de hello.
* **Substitution de fréquentes**: si les données manquantes hello sont catégoriques, remplacez les valeurs manquantes hello par élément plus fréquente de hello
* **Substitution de régression**: utilisation de régression méthode tooreplace absence de valeurs avec des valeurs de régressions.  

## <a name="how-toonormalize-data"></a>Comment les données toonormalize ?
Données normalisation nouveau met à l’échelle des valeurs numériques tooa spécifié de plage. Les méthodes de normalisation les plus courantes sont les suivantes :

* **Normalisation Min-Max**: linéairement transforment hello données tooa plage, vous pouvez dire comprise entre 0 et 1, où hello la valeur minimale est mis à l’échelle too0 et too1 de la valeur maximale.
* **Normalisation Z-score**: l’échelle en fonction de la moyenne et l’écart-type de données : diviser hello différencie les données de salutation hello moyenne par écart type hello.
* **Mise à l’échelle décimal**: l’échelle des données de hello mobile décimal hello de valeur d’attribut hello.  

## <a name="how-toodiscretize-data"></a>Comment les données toodiscretize ?
Données peuvent être discrétisées en convertissant les attributs de toonominal des valeurs continues ou des intervalles. Plusieurs méthodes permettent d’effectuer cette opération :

* **Placement de largeur égale**: diviser plage hello de toutes les valeurs possibles d’un attribut en groupes N Hello même taille et assigner des valeurs de hello qui se trouvent dans un emplacement avec un numéro d’emplacement hello.
* **Placement de hauteur égale**: diviser hello plage de toutes les valeurs possibles d’un attribut en groupes de N, contenant chacune hello même nombre d’instances, puis affecter de valeurs de hello qui se trouvent dans un emplacement avec hello au numéro d’emplacement.  

## <a name="how-tooreduce-data"></a>Comment les données tooreduce ?
Il existe de taille des données tooreduce méthodes différentes pour la gestion des données plus faciles. Selon la taille et hello domaine de données hello méthodes suivantes peut être appliquée :

* **Enregistrement d’échantillonnage**: exemple hello les enregistrements de données et à ne choisir qu’à partir des données de hello sous-ensemble représentatif de hello.
* **Attribut d’échantillonnage**: sélectionner uniquement un sous-ensemble des attributs les plus importants hello à partir des données de hello.  
* **Agrégation**: diviser les données hello en groupes et de stocker les nombres hello pour chaque groupe. Par exemple, hello chiffre d’affaires quotidien nombres d’une chaîne de restaurant sur hello 20 années peuvent être agrégées taille hello tooreduce du chiffre d’affaires toomonthly de données de hello.  

## <a name="how-tooclean-text-data"></a>Comment les données de texte tooclean ?
**Les champs de texte au format tabulaire** peuvent contenir des caractères qui perturbent l’alignement des données et/ou les limites des enregistrements. Par exemple, des tabulations intégrées dans un fichier TSV peuvent décaler les colonnes, et des caractères de nouvelle ligne peuvent déstructurer des enregistrements. Gestion lors de l’écriture/lecture texte l’encodage de texte incorrect entraîne une perte de tooinformation, par inadvertance introduction de caractères illisibles, par exemple, les valeurs NULL, et peut également affectent l’analyse. Analyse minutieuse et modification peuvent être nécessaires dans les champs de texte de commande tooclean pour alignement correct et/ou tooextract structurée les données à partir des données de texte non structurées ou semi-structurées.

**Exploration de données** propose une vue anticipée des données de salutation. Un nombre de problèmes de données soient détecté au cours de cette étape et méthodes correspondantes peuvent être appliqués tooaddress ces problèmes.  Il est important tooask des questions comme origine hello du problème de hello et comment les problème hello peuvent avoir été introduite. Cela vous permet également de décider sur les étapes de traitement des données hello que toobe besoin prise tooresolve les. type Hello d’aperçus un envisage tooderive à partir des données de hello peut également être utilisé tooprioritize hello le traitement des données.

## <a name="references"></a>Références
> *Data Mining : Concepts et Techniques*, 3e édition, Morgan Kaufmann, 2011, Jiawei Han, Micheline Kamber et Jian Pei
> 
> 

