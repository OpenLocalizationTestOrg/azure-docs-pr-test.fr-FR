---
title: "Régression linéaire dans l’apprentissage d’aaaUsing | Documents Microsoft"
description: "Une comparaison des modèles de régression linéaire dans Excel et dans Azure Machine Learning Studio"
metakeywords: 
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 417ae6ab-de4f-4bdd-957a-d96133234656
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: kbaroni;garye
ms.openlocfilehash: 8716040ad296053a72fb06c7c9660a186123ac15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-linear-regression-in-azure-machine-learning"></a>Utilisation de la régression linéaire dans Azure Machine Learning
> *Kate Baroni* et *Ben Boatman* sont des architectes de solution du Data Insights Center of Excellence de Microsoft. Dans cet article, ils décrivent leur expérience de migration d’une régression analysis suite tooa nuage solution existante à l’aide d’Azure Machine Learning. 
> 
> 

&nbsp; 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="goal"></a>Objectif
Notre projet a commencé avec deux objectifs : 

1. Utiliser analytique prédictive tooimprove hello précision des projections de chiffre d’affaires de notre organisation mensuel 
2. Utilisez Azure Machine Learning tooconfirm, optimiser, augmenter la rapidité et l’échelle de nos résultats. 

Comme beaucoup d’entreprises, notre organisation connaît un processus de prévision des recettes mensuelles. Notre petite équipe d’analystes d’entreprise a été chargé à l’aide d’Azure Machine Learning toosupport hello processus et améliorer la précision des prévisions. équipe de Hello passé plusieurs mois de collecte de données à partir de plusieurs sources et les attributs de données hello en cours d’exécution via l’analyse statistique, identification des attributs de clé approprié tooservices ventes prévisionnelles. étape suivante de Hello a été toobegin des modèles de régression statistique de prototypage sur données hello dans Excel. Quelques semaines, nous avons eu un modèle de régression Excel qui a été devançant ainsi champ actuel de hello et finance prévision des processus. C’est le résultat de prédiction hello de ligne de base. 

Nous avons ensuite pris hello prochaine étape toomoving notre analytique prédictive sur toofind d’apprentissage tooAzure out comment améliorer apprentissage sur les performances prédictive.

## <a name="achieving-predictive-performance-parity"></a>Atteinte de la parité des performances de prédiction
Notre priorité a été parité tooachieve entre les modèles de régression d’apprentissage automatique et Excel. Fonction hello les mêmes données et hello même fractionner pour l’apprentissage et de données de test, nous voulions parité de performances prédictive tooachieve entre Excel et l’apprentissage. Au départ, nous a échoué. modèle d’apprentissage hello Hello Excel modèle obtenu les meilleures performances. Échec de Hello était en raison du manque de tooa de compréhension des outils de base hello définissant dans l’apprentissage. Après une synchronisation avec l’équipe de produit hello Machine Learning, nous acquise une meilleure compréhension de hello base paramètre nécessaire pour notre jeux de données et atteint la parité entre deux modèles de hello. 

### <a name="create-regression-model-in-excel"></a>Création d’un modèle de régression dans Excel
Notre régression Excel utilisé le modèle de régression linéaire standard hello Bonjour Excel Analysis ToolPak. 

Nous avons calculé *% absolue moyenne erreur* et utilisé en tant que mesure de performances hello pour le modèle de hello. Il a fallu tooarrive de 3 mois à un modèle de travail à l’aide d’Excel. Nous avons une grande partie de la formation de hello en hello expérience Machine Learning Studio qui finalement était utile de comprendre les impératifs.

### <a name="create-comparable-experiment-in-azure-machine-learning"></a>Création d’une expérience comparable dans Azure Machine Learning
Nous avons suivies toocreate de ces étapes de notre expérience dans Machine Learning Studio : 

1. Dataset hello chargé comme un tooMachine de fichier csv Learning Studio (fichier très petite)
2. Création d’une nouvelle expérience et utilisé hello [sélectionner les colonnes dans le jeu de données] [ select-columns] module tooselect hello les mêmes fonctionnalités de données utilisées dans Excel 
3. Hello utilisé [données fractionnées] [ split] module (avec *Expression Relative* mode) données hello toodivide hello jeux de données d’apprentissage comme avait été effectuée dans Excel 
4. Transposez hello [régression linéaire] [ linear-regression] module (options par défaut uniquement), documenté et comparé les modèle de régression hello résultats tooour Excel

### <a name="review-initial-results"></a>Examen des résultats initiaux
Dans un premier temps, modèle de Excel hello clairement obtenu les meilleures performances modèle de Machine Learning Studio hello : 

|  | Excel | Studio |
| --- |:---:|:---:|
| Performances | | |
| <ul style="list-style-type: none;"><li>Carré R ajusté</li></ul> |0,96 |N/A |
| <ul style="list-style-type: none;"><li>Coefficient de <br />détermination</li></ul> |N/A |0,78<br />(faible précision) |
| Erreur d'absolue moyenne |9,5 M $ |19,4 M $ |
| Erreur d’absolue moyenne (%) |6,03 % |12,2 % |

Lorsque nous avons nos processus et les résultats obtenus par les développeurs de hello et des chercheurs de données sur l’équipe de Machine Learning hello, elles fournies rapidement des conseils utiles. 

* Lorsque vous utilisez hello [régression linéaire] [ linear-regression] module dans Machine Learning Studio, deux méthodes sont fournies :
  * descente dégradée en ligne : plus adapté aux problèmes de plus grande échelle ;
  * Moindres carrés ordinaires : Il s’agit de méthode hello que considérer la plupart des utilisateurs lorsqu’ils entendent régression linéaire. Pour les petits groupes de données, les moindres carrés ordinaires peuvent être un meilleur choix.
* Envisagez d’ajuster les performances de tooimprove de paramètre de poids de régularisation L2 hello. Il a la valeur too0.001 par défaut, mais pour notre petit jeu de données, nous il définies too0.005 tooimprove performances. 

### <a name="mystery-solved"></a>Mystère résolu !
Lorsque nous avons appliqué les recommandations hello, nous avons obtenu hello même étalonner les performances dans Machine Learning Studio comme avec Excel : 

|  | Excel | Studio (Initial) | Studio avec moindres carrés |
| --- |:---:|:---:|:---:|
| Valeur étiquetée |Chiffres réels (numérique) |identique |identique |
| Apprenant |Excel -> Analyse des données -> Régression |Régression linéaire. |régression linéaire |
| Options de l’apprenant |N/A |Valeurs par défaut |moindres carrés ordinaires<br />L2 = 0,005 |
| Jeu de données |26 lignes, 3 fonctionnalités, 1 étiquette. Tout au format numérique. |identique |identique |
| Fractionnement : Formation |Excel formés sur hello tout d’abord 18 lignes, testé sur hello 8 dernières lignes. |identique |identique |
| Fractionnement : Test |Excel appliquée la formule de régression de la dernière toohello 8 lignes |identique |identique |
| **Performances** | | | |
| Carré R ajusté |0,96 |N/A | |
| Coefficient de détermination |N/A |0,78 |0,952049 |
| Erreur d'absolue moyenne |9,5 M $ |19,4 M $ |9,5 M $ |
| Erreur d’absolue moyenne (%) |<span style="background-color: 00FF00;"> 6,03 %</span> |12,2 % |<span style="background-color: 00FF00;"> 6,03 %</span> |

En outre, coefficients de Excel hello par rapport bien poids de fonctionnalité toohello Bonjour formé Azure :

|  | Coefficients Excel | Poids des fonctionnalités Azure |
| --- |:---:|:---:|
| Interception/Décalage |19470209,88 |19328500 |
| Fonctionnalité A |0,832653063 |0,834156 |
| Fonctionnalité B |11071967,08 |11007300 |
| Fonctionnalité C |25383318,09 |25140800 |

## <a name="next-steps"></a>Étapes suivantes
Nous voulions service tooconsume hello apprentissage web Excel. Analystes d’entreprise s’appuient sur Excel et nous nécessaire un Bonjour toocall de façon apprentissage web service avec une ligne de données Excel et la rétablir hello prédit la valeur tooExcel. 

Nous avons également souhaité toooptimize notre modèle, à l’aide des options de hello et les algorithmes disponibles dans Machine Learning Studio.

### <a name="integration-with-excel"></a>Intégration à Excel
Notre solution a été toooperationalize notre régression d’apprentissage de modèle en créant un service web à partir du modèle formé de hello. Dans quelques minutes, hello web service a été créé, et nous pouvons appeler directement à partir d’Excel tooreturn une valeur prédite chiffre d’affaires. 

Hello *tableau de bord de Services Web* section comprend un classeur Excel à télécharger. classeur de Hello accompagne préformatée hello informations service web API et du schéma incorporées. Lorsque vous cliquez sur *télécharger un classeur Excel*, hello classeur s’ouvre et vous pouvez l’enregistrer tooyour les ordinateur local. 

![][1]

Le classeur hello ouvert, copiez vos paramètres prédéfinis dans la section de paramètre hello bleu comme indiqué ci-dessous. Une fois que les paramètres de hello sont entrés, Excel appelle toohello service web Machine Learning et étiquettes évaluées prédites hello seront affiche dans la section des valeurs prédites hello vert. classeur de Hello continue toocreate des prédictions pour les paramètres en fonction de votre modèle formé pour tous les éléments de ligne entré sous l’onglet Paramètres. Pour plus d’informations sur la façon dont les toouse cette fonctionnalité, consultez [utilisation d’un Service Web de Azure Machine Learning à partir d’Excel](machine-learning-consuming-from-excel.md). 

![][2]

### <a name="optimization-and-further-experiments"></a>Optimisation et autres expériences
Maintenant que nous avons eu une ligne de base avec notre modèle Excel, nous avons déplacé toooptimize anticipée notre modèle de régression linéaire Machine Learning. Nous avons utilisé le module de hello [sélection des fonctionnalités par filtrage] [ filter-based-feature-selection] tooimprove sur notre sélection des éléments de données initiales et il aidé à obtenir une amélioration des performances de 4.6 % signifie que l’erreur absolue. Pour les futurs projets, nous allons utiliser cette fonctionnalité que nous pourrait enregistrer semaines dans l’itération au sein des données attributs toofind hello ensemble approprié de toouse des fonctionnalités de modélisation. 

Ensuite, nous prévoyons tooinclude des algorithmes supplémentaires comme [bayésien] [ bayesian-linear-regression] ou [arbres de décision augmentés] [ boosted-decision-tree-regression] dans toocompare de notre expérience performances. 

Si vous souhaitez tooexperiment avec la régression, un tootry bon jeu de données est hello régression de l’efficacité énergétique échantillon de dataset, ce qui a un grand nombre d’attributs numériques. jeu de données Hello est fournie en tant que partie des groupes de données exemple hello dans Machine Learning Studio. Vous pouvez utiliser diverses toopredict de modules d’apprentissage chauffage de chargement ou de charge de refroidissement. graphique de Hello ci-dessous est qu'une comparaison des performances de régression différents apprend contre hello l’efficacité énergétique dataset prédiction pour hello cibles charge refroidissement de variable : 

| Modèle | Erreur d'absolue moyenne | Erreur du carré moyen racine | Erreur d’absolue relative | Erreur carrée relative | Coefficient de détermination |
| --- | --- | --- | --- | --- | --- |
| Arbre de décision optimisé |0,930113 |1,4239 |0,106647 |0,021662 |0,978338 |
| Régression linéaire (descente dégradée) |2,035693 |2,98006 |0,233414 |0,094881 |0,905119 |
| Régression de réseau neuronal |1,548195 |2,114617 |0,177517 |0,047774 |0,952226 |
| Régression linéaire (moindres carrés ordinaires) |1,428273 |1,984461 |0,163767 |0,042074 |0,957926 |

## <a name="key-takeaways"></a>Points clés
Nous avons beaucoup appris en exécutant la régression Excel et les expériences Azure Machine Learning en parallèle. Modèle de ligne de base hello création dans Excel et en la comparant toomodels à l’aide de la Machine Learning [régression linéaire] [ linear-regression] permis nous savoir Azure Machine Learning, et nous avons découvert les données de tooimprove d’opportunités performances de sélection et le modèle. 

Nous avons trouvé également qu’il est conseillé de toouse [sélection des fonctionnalités par filtrage] [ filter-based-feature-selection] tooaccelerate les projets futurs de prédiction. En appliquant des données de tooyour de sélection de fonctionnalités, vous pouvez créer un modèle amélioré dans l’apprentissage avec de meilleures performances globales. 

hello tootransfer à capacité de Hello prédictive analyse de prévision à partir de la Machine Learning tooExcel systémiques permet une augmentation significative dans hello capacité toosuccessfully fournir des résultats audience tooa opérationnelles de l’utilisateur. 

## <a name="resources"></a>Ressources
Voici des ressources pour vous aider à utiliser la régression : 

* Régression dans Excel. Si vous n’avez jamais essayé la régression dans Excel, ce didacticiel vous aidera beaucoup : [http://www.excel-easy.com/examples/regression.html](http://www.excel-easy.com/examples/regression.html)
* Régression et prévisions. Tyler Chessman a écrit un article de blog expliquant comment toodo temps série prévision dans Excel, qui contient la description du débutant correcte d’une régression linéaire. [http://sqlmag.com/sql-server-analysis-services/understanding-time-series-forecasting-concepts](http://sqlmag.com/sql-server-analysis-services/understanding-time-series-forecasting-concepts) 
* Régression linéaire et moindres carrés ordinaires : défauts, problèmes et pièges. Pour une introduction et une discussion relatives à la régression : [http://www.clockbackward.com/2009/06/18/ordinary-least-squares-linear-regression-flaws-problems-and-pitfalls/ ](http://www.clockbackward.com/2009/06/18/ordinary-least-squares-linear-regression-flaws-problems-and-pitfalls/)

[1]: ./media/machine-learning-linear-regression-in-azure/machine-learning-linear-regression-in-azure-1.png
[2]: ./media/machine-learning-linear-regression-in-azure/machine-learning-linear-regression-in-azure-2.png


<!-- Module References -->
[bayesian-linear-regression]: https://msdn.microsoft.com/library/azure/ee12de50-2b34-4145-aec0-23e0485da308/
[boosted-decision-tree-regression]: https://msdn.microsoft.com/library/azure/0207d252-6c41-4c77-84c3-73bdf1ac5960/
[filter-based-feature-selection]: https://msdn.microsoft.com/library/azure/918b356b-045c-412b-aa12-94a1d2dad90f/
[linear-regression]: https://msdn.microsoft.com/library/azure/31960a6f-789b-4cf7-88d6-2e1152c0bd1a/
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/

