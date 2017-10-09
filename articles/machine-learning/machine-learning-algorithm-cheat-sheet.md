---
title: "aide-mémoire de l’algorithme d’apprentissage d’aaaMachine | Documents Microsoft"
description: "Un aide-mémoire de l’algorithme d’apprentissage imprimable vous permet de choisir un algorithme de droite hello pour votre modèle de prévision dans Azure Machine Learning Studio."
keywords: "aide mémoire d’algorithme, aide mémoire, algorithme d’apprentissage automatique"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: e1dc31ec-1acb-463f-ba77-de565d4ddf4d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: garye
ms.openlocfilehash: 2bedd77bfc65128a90c6128743016415dd8609d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="machine-learning-algorithm-cheat-sheet-for-microsoft-azure-machine-learning-studio"></a>Aide-mémoire d'algorithme d'apprentissage automatique pour Microsoft Azure Machine Learning Studio
Hello **Microsoft Azure Machine Learning algorithme Cheat Sheet** vous permet de choisir l’algorithme adapté de hello pour un modèle prédictif analytique.

[Azure Machine Learning Studio](https://studio.azureml.net/) a une grande bibliothèque d’algorithmes hello ***régression***, ***classification***, ***clustering***et ***détection d’anomalie*** familles. Chacun est conçu tooaddress un autre type de problème d’apprentissage machine.

## <a name="download-machine-learning-algorithm-cheat-sheet"></a>Télécharger l’aide-mémoire d’algorithme Machine Learning
**Télécharger hello aide-mémoire ici : [Machine Learning algorithme Cheat Sheet (11 x 17 pouces)](http://download.microsoft.com/download/A/6/1/A613E11E-8F9C-424A-B99D-65344785C288/microsoft-machine-learning-algorithm-cheat-sheet-v6.pdf)**

![Aide-mémoire de configuration machine algorithme d’apprentissage : en savoir comment toochoose un algorithme d’apprentissage.][cheat-sheet]

[cheat-sheet]: ./media/machine-learning-algorithm-cheat-sheet/machine-learning-algorithm-cheat-sheet-small_v_0_6-01.png

Télécharger et l’imprimer hello Machine Learning algorithme Cheat Sheet dans Tabloïd taille tookeep pratique aide get choix d’un algorithme.

> [!NOTE]
> Consultez l’article hello [comment toochoose des algorithmes pour Microsoft Azure Machine Learning](machine-learning-algorithm-choice.md) pour un guide détaillé de toousing cette feuille de graphique.
> 
> 

## <a name="more-help-with-algorithms"></a>Aide supplémentaire sur les algorithmes
* Pour vous aider à l’aide de cette feuille de graphique pour choisir l’algorithme adapté de hello, ainsi qu’une discussion plus approfondie de hello différents types d’algorithmes d’apprentissage automatique et comment ils sont utilisés, consultez [comment toochoose des algorithmes pour Microsoft Azure Machine Learning](machine-learning-algorithm-choice.md).
* Pour obtenir une infographie téléchargeable décrivant les algorithmes et fournissant des exemples, consultez [Infographie téléchargeable : Principes de base de l’apprentissage automatique avec exemples d’algorithmes](machine-learning-basics-infographic-with-algorithm-examples.md).
* Pour obtenir une liste par catégorie de tous les algorithmes d’apprentissage automatique hello ordinateur disponibles dans Machine Learning Studio, consultez [initialiser le modèle] [ initialize-model] hello Machine Learning Studio algorithme et aide du Module.
* Pour obtenir la liste alphabétique complète des algorithmes et des modules de Machine Learning Studio, consultez [Liste alphabétique des modules de Machine Learning Studio][a-z-list] dans Machine Learning Studio : aide sur les algorithmes et les modules.
* toodownload et imprimer un diagramme qui donne une vue d’ensemble des fonctionnalités de hello de Machine Learning Studio, consultez [diagramme de vue d’ensemble des fonctionnalités d’Azure Machine Learning Studio](machine-learning-studio-overview-diagram.md).

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="notes-and-terminology-definitions-for-hello-machine-learning-algorithm-cheat-sheet"></a>Notes de publication et de définitions pour l’algorithme d’apprentissage hello feuille de graphique

* suggestions de Hello proposées dans cette feuille de graphique algorithme sont approximatives de règles de base. Certaines peuvent être contournées et d’autres ignorées. Il s’agit d’un point de départ de toosuggest prévue. N’ayez pas peur toorun une concurrence emportée entre plusieurs algorithmes sur vos données. Il n’est simplement aucune substitution pour la compréhension des principes hello de chaque algorithme et compréhension hello système qui a généré de vos données.

* Chaque algorithme d’apprentissage automatique a son propre style ou *décalage inductif*. Plusieurs algorithmes peuvent être appropriés pour un problème spécifique et un algorithme peut être un meilleur choix que d’autres. Mais il n’est pas toujours tooknow de possible au préalable qui convient le mieux hello. Dans ce cas, plusieurs algorithmes sont affichées dans la feuille de graphique hello. Une stratégie appropriée serait être tootry un algorithme et si les résultats de hello ne sont pas encore satisfaisants, essayez d’autres hello. Voici un exemple de hello [Cortana Intelligence galerie](http://gallery.cortanaintelligence.com/) d’une expérience qui tente de plusieurs algorithmes contre hello les mêmes données et les compare hello résultats : [comparer des classifieurs multi-class : lettre reconnaissance ](http://gallery.cortanaintelligence.com/Details/a635502fc98b402a890efe21cec65b92).

* Il existe trois catégories principales d’apprentissage automatique : l’**apprentissage supervisé**, l’**apprentissage non supervisé** et l’**apprentissage par renforcement**.

  * Dans l’**apprentissage supervisé**, chaque point de données est étiqueté ou associé à une catégorie ou une valeur qui vous intéresse.  La définition d’une image comme un « chat » ou un « chien » est un exemple d’étiquette de catégorie.  Un exemple d’une étiquette de la valeur est le prix de vente hello associé à une voiture utilisée. Hello apprentissage supervisé vise toostudy nombreux étiqueté exemples ces, puis toobe toomake en mesure des prédictions à propos des points de données futures. Par exemple, identifier nouvelles photos avec hello correct animal ou l’affectation de tooother des prix de vente précise utilisé voitures. Il s’agit d’un type d’apprentissage automatique utile et apprécié. Tous les modules hello dans Azure Machine Learning surveillées, sauf pour les algorithmes d’apprentissage [Clustering K-Means][k-means-clustering].

  * Dans l’**apprentissage non supervisé**, les points de données n’ont aucune étiquette associée. Au lieu de cela, hello objectif d’un algorithme d’apprentissage non supervisé donnée tooorganize hello d’une manière ou de toodescribe sa structure. Cela peut signifier un regroupement en clusters, comme le fait l’algorithme des k-moyennes ou la recherche de différentes manières de visualiser des données complexes afin d’en simplifier l’affichage.

  * Dans **learning de renforcement**, algorithme de hello obtient toochoose une action de point de données de réponse tooeach. Il s’agit d’une approche commune robotique, où hello ensemble de lectures de capteur à un moment donné dans le temps est un point de données, et algorithme de hello devez choisir l’action de suivant du robot hello. Il est également adapté aux applications d’Internet des objets. algorithme d’apprentissage Hello reçoit également un signal de récompense quelques instants plus tard, indiquant la bonne décision de hello a été. En fonction de cela, algorithme de hello modifie sa stratégie de récompense de commande tooachieve hello la plus élevée. Il n’existe actuellement aucun module d’apprentissage de renforcement dans Azure ML.

* **Méthodes bayésiennes** hypothèse de hello de points de données statistiquement indépendant. Cela signifie que hello variabilité sans modèle dans un point de données est corrélée avec d’autres, autrement dit, il n’est pas prévisible. Par exemple, si les données hello enregistrées nombre de hello de minutes jusqu'à ce que l’apprentissage de métro suivant hello arrive, deux mesures par jour éloignés sont statistiquement indépendant. Toutefois, les deux mesures une minute éloignés ne sont pas statistiquement indépendants : hello la valeur de l’un est hautement prédictive de valeur hello Hello autres.

* **La régression de l’arbre de décision optimisé** tire parti du chevauchement de fonctionnalités ou de l’interaction entre les fonctionnalités. Que signifie que, dans toutes les données point, hello la valeur d’une fonctionnalité est quelque peu prédictive de valeur hello d’un autre. Par exemple, dans les données haute/basse température quotidiennes, savoir froid hello pour le jour de hello vous permet toomake une estimation raisonnable à hello haute. les informations de Hello contenues dans les deux fonctionnalités de hello sont quelque peu redondantes.

* La classification des données en plus de deux catégories peut être effectuée en utilisant un classifieur à plusieurs classes par nature ou en combinant un ensemble de classifieurs à deux classes dans un **ensemble**. Dans l’approche d’ensemble de hello, il est un classifieur de deux classes distinct pour chaque classe - chacune d’elles sépare les données de hello en deux catégories : « cette classe » et « pas cette classe. » Puis ces classifieurs votent sur l’affectation correcte de hello hello du point de données. Cela est le principe de fonctionnement de hello derrière [One-vs-All Multiclass][one-vs-all-multiclass].

* Plusieurs méthodes, notamment la régression logistique et hello Bayes point machine, supposons que **des limites de la classe linéaire**. Autrement dit, ils supposent que hello des limites entre les classes sont environ des lignes droites (ou hyperplanes dans hello plus générale). Il s’agit souvent d’une caractéristique des données de hello que vous ne connaissez pas jusqu'à une fois que vous avez essayé de tooseparate, mais il est généralement pouvant être appris à visualiser au préalable. Si des limites de classes hello ressemble très irrégulières, suivez les arbres de décision, Jungle d’arbres de décision, prennent en charge les machines à vecteurs de réseaux neuronaux.

* Réseaux neuronaux sont utilisables avec des variables de catégorie en créant un **variable factice** pour chaque catégorie, définissant too1 dans le cas où hello catégorie s’applique, 0 où ce n’est pas.


<!-- This is how you can embed a link in an image in HTML. Don't know how toodo this in markdown.
<a href="http://download.microsoft.com/download/A/6/1/A613E11E-8F9C-424A-B99D-65344785C288/microsoft-machine-learning-algorithm-cheat-sheet.pdf">
<img src="C:\Users\garye\azure-docs-pr\articles\media\machine-learning-algorithm-cheat-sheet\cheat-sheet-small.png">
</a>
-->

<!-- Module References -->
[a-z-list]: https://msdn.microsoft.com/library/azure/dn906033.aspx
[initialize-model]: https://msdn.microsoft.com/library/azure/0c67013c-bfbc-428b-87f3-f552d8dd41f6/
[k-means-clustering]: https://msdn.microsoft.com/library/azure/5049a09b-bd90-4c4e-9b46-7c87e3a36810/
[one-vs-all-multiclass]: https://msdn.microsoft.com/library/azure/7191efae-b4b1-4d03-a6f8-7205f87be664/
