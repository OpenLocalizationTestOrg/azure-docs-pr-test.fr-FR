---
title: "aaaExtend votre expérience avec R | Documents Microsoft"
description: "La fonctionnalité de hello tooextend d’Azure Machine Learning Studio via le langage hello R à l’aide de hello module Execute R Script."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 2c038a45-ba4d-42ea-9a88-e67391ef8c0a
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye
ms.openlocfilehash: 396489f26f367a744922af65e04f056c7afa1399
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="extend-your-experiment-with-r"></a>Prolongez votre expérience avec R
Vous pouvez étendre les fonctionnalités de hello d’Azure Machine Learning Studio via le langage de hello R à l’aide de hello [Execute R Script] [ execute-r-script] module.

Ce module accepte plusieurs jeux de données d’entrée et génère un jeu de données unique en sortie. Vous pouvez taper un script R dans hello **Script R** paramètre Hello [Execute R Script] [ execute-r-script] module.

Pour accéder à chaque port d’entrée du module de hello à l’aide de code similaire toohello suivant :

    dataset1 <- maml.mapInputPort(1)

## <a name="listing-all-currently-installed-packages"></a>Liste de tous les packages actuellement installés
liste Hello des packages installés peut modifier. Vous trouverez une liste des packages actuellement installés dans [R Packages Supported by Azure Machine Learning](https://msdn.microsoft.com/library/azure/mt741980.aspx) (Packages R pris en charge par Azure Machine Learning).

Vous pouvez également obtenir hello liste complète et actuelle des packages installés en entrant hello après le code dans hello [Execute R Script] [ execute-r-script] module :

    out <- data.frame(installed.packages(,,,fields="Description"))
    maml.mapOutputPort("out")

Cela envoie la liste hello du port de sortie toohello packages Hello [Execute R Script] [ execute-r-script] module.
package de hello tooview liste, la connexion d’un module de conversion telles que [convertir tooCSV] [ convert-to-csv] toohello gauche sortie Hello [Execute R Script] [ execute-r-script]module, exécutez hello expérience, puis cliquez sur sortie hello de module de conversion hello et sélectionnez **télécharger**. 

![Télécharger la sortie de module de « Convertir tooCSV »](./media/machine-learning-extend-your-experiment-with-r/download-package-list.png)


<!--
For convenience, here is hello [current full list with version numbers in Excel format](http://az754797.vo.msecnd.net/docs/RPackages.xlsx).
-->

## <a name="importing-packages"></a>Importation de packages
Vous pouvez importer des packages qui ne sont pas déjà installés à l’aide de hello suivant les commandes Bonjour [Execute R Script] [ execute-r-script] module :

    install.packages("src/my_favorite_package.zip", lib = ".", repos = NULL, verbose = TRUE)
    success <- library("my_favorite_package", lib.loc = ".", logical.return = TRUE, verbose = TRUE)

où hello `my_favorite_package.zip` fichier contient votre package.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[convert-to-csv]: https://msdn.microsoft.com/library/azure/faa6ba63-383c-4086-ba58-7abf26b85814/
