---
title: "aaaManage expérimenter des itérations dans Machine Learning Studio | Documents Microsoft"
description: "Comment toomanage expérimenter des itérations dans Azure Machine Learning Studio"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 6a53530f-20d5-40ae-9b49-7b499ccb44b7
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye
ms.openlocfilehash: bd30c048ce063811b1b2de8ce6d71e99ba975713
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-experiment-iterations-in-azure-machine-learning-studio"></a>Gestion des itérations d'expériences dans Azure Machine Learning Studio
Développement d’un modèle d’analyse prédictive est un processus itératif - lorsque vous modifiez des hello diverses fonctions et les paramètres de votre expérience, vos résultats de faire converger jusqu'à ce que vous êtes satisfait que vous disposez d’un modèle formé et efficace. Processus de toothis de clé est suivi hello différentes itérations de vos paramètres de l’expérience et les configurations.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

Vous pouvez passer en revue les exécutions précédentes de vos expériences à tout moment dans l’ordre toochallenge, réexaminer et enfin confirmer ou affiner les hypothèses précédentes. Lorsque vous exécutez une expérience, Machine Learning Studio conserve un historique de hello exécuter, y compris le jeu de données, ce module et les connexions de port et les paramètres. Cet historique capture également les résultats, les informations d'exécution telles que les heures de démarrage et d'arrêt, les messages de journal et l'état d'exécution. Vous pouvez de revenir à un de ces séries à n’importe quel chronologie de hello tooreview heure de votre expérience et les résultats intermédiaires. Vous pouvez même utiliser une exécution précédente de votre expérience de toolaunch dans une nouvelle phase de consultation et de découverte sur votre chemin d’accès toocreating simple, complexe ou même d’ensemble des solutions de modélisation.

> [!NOTE]
> Lorsque vous affichez une exécution précédente d’une expérience, que la version de l’expérience de hello est verrouillée et ne peut pas être modifiée. Vous pouvez, toutefois, enregistrer une copie de celle-ci en cliquant sur **SAVE AS** et en fournissant un nouveau nom pour la copie de hello. Machine Learning Studio s’ouvre hello nouvelle copie, que vous pouvez ensuite modifier et exécuter. Cette copie de votre expérience est disponible dans hello **expériences** liste, ainsi que vos autres expériences.
> 
> 

## <a name="viewing-hello-prior-run"></a>Hello affichage exécuter préalable
Lorsque vous avez ouvert expérience que vous avez exécutés au moins une fois, vous pouvez afficher hello précédant l’exécution de l’expérience de hello en cliquant sur **exécuter préalable** dans le volet de propriétés hello.

Supposons par exemple que vous créez une expérience et que vous exécutez des versions de celle-ci à 11:23, 11:42 et 11:55. Si vous ouvrez hello dernière exécution de l’expérience hello (11:55) et cliquez sur **exécuter préalable**, version hello vous exécutés à 11:42 est ouvert.

## <a name="viewing-hello-run-history"></a>Affichage hello historique d’exécution
Vous pouvez afficher toutes les exécutions précédentes hello d’une expérience en cliquant **afficher l’historique d’exécution** dans une expérience ouverte.

Par exemple, supposons que vous créez une expérience avec hello [régression linéaire] [ linear-regression] module et que vous souhaitez effet de hello tooobserve de modification de valeur hello de **taux d’apprentissage** sur résultats de votre expérience. Vous exécutez hello expérience plusieurs fois avec différentes valeurs pour ce paramètre, comme suit :

| Valeur du taux d'apprentissage | Heure de début de l'exécution |
| --- | --- |
| 0.1 |11/9/2014 16:18:58 |
| 0.2 |11/9/2014 16:24:33 |
| 0.4 |11/9/2014 16:28:36 |
| 0.5 |11/9/2014 16:33:31 |

Si vous cliquez sur **AFFICHER L'HISTORIQUE D'EXÉCUTION**, une liste de toutes ces exécutions apparaîtra :

![Exemple d'historique d'exécution][runhistory]

Cliquez sur un de ces tooview s’exécute un instantané de hello faire des essais au moment de hello vous l’exécutez. Hello configuration, les valeurs de paramètre, les commentaires et les résultats sont tous conservé toogive vous un enregistrement complet de cette exécution de votre expérience.

> [!TIP]
> toodocument des itérations de l’expérience de hello, vous pouvez modifier le titre de hello chaque fois que vous l’exécutez, vous pouvez mettre à jour hello **Résumé** de hello expérience suivant dans le volet de propriétés hello, vous pouvez ajouter ou mettre à jour des commentaires sur les modules individuels toorecord vos modifications. commentaires de titre, résumé et module Hello sont enregistrés avec chaque exécution de l’expérience de hello.
> 
> 

liste Hello d’expériences dans hello **expériences** onglet dans Machine Learning Studio affiche toujours la version la plus récente d’une expérimentation hello. Si vous ouvrez une exécution précédente de l’expérience de hello (à l’aide de **exécuter préalable** ou **afficher l’historique d’exécution**), vous pouvez retourner toohello brouillon en cliquant sur **afficher l’historique d’exécution** et en sélectionnant Hello itération a un **état** de **modifiable**.

## <a name="iterating-on-a-previous-run"></a>Itération sur une exécution précédente
Lorsque vous cliquez sur **Exécution précédente** ou **AFFICHER L'HISTORIQUE D'EXÉCUTION** et que vous ouvrez une exécution précédente, vous pouvez afficher une expérience terminée en mode lecture seule.

Si vous souhaitez toobegin une itération de votre expérience en commençant par la méthode hello vous l’avez configurée pour une exécution précédente, cela en hello ouverture exécuter en cliquant sur **SAVE AS**. Cette opération crée une nouvelle expérience, avec un nouveau titre, un historique d’exécution vide et tous les composants de hello et valeurs de paramètre de hello précédente exécution. Cette nouvelle expérience est répertoriée dans hello **d’expériences** onglet dans la page d’accueil hello Machine Learning Studio et vous pouvez modifier et exécuter, lancer une nouvelle l’historique pour cette itération de votre expérience d’exécution. 

Par exemple, supposons que vous avez expérience hello indiqué dans la section précédente de hello de l’historique d’exécution. Vous souhaitez tooobserve que se passe-t-il lorsque vous définissez hello **taux d’apprentissage** too0.4 de paramètre et essayez différentes valeurs pour hello **nombre d’époques d’apprentissage** paramètre.

1. Cliquez sur **afficher l’historique d’exécution** et ouvrez itération hello d’expérimentation hello que vous avez exécutés à 4:28:36 (dans lequel vous définissez too0.4 de valeur de paramètre hello).
2. Cliquez sur **ENREGISTRER SOUS**.
3. Entrez un nouveau titre et cliquez sur hello **OK** coche. Une nouvelle copie de l’expérience de hello est créée.
4. Modifier hello **nombre d’époques d’apprentissage** paramètre.
5. Cliquez sur **EXÉCUTER**.

Vous pouvez maintenant continuer toomodify et exécuter cette version de votre expérience, générer un nouveau toorecord de l’historique d’exécution de votre travail.

<!-- Images -->
[runhistory]:./media/machine-learning-manage-experiment-iterations/viewrunhistory.jpg


<!-- Module References -->
[linear-regression]: https://msdn.microsoft.com/library/azure/31960a6f-789b-4cf7-88d6-2e1152c0bd1a/
