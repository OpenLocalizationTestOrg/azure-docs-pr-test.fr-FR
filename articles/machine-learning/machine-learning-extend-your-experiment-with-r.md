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
# <a name="extend-your-experiment-with-r"></a><span data-ttu-id="d8927-103">Prolongez votre expérience avec R</span><span class="sxs-lookup"><span data-stu-id="d8927-103">Extend your experiment with R</span></span>
<span data-ttu-id="d8927-104">Vous pouvez étendre les fonctionnalités de hello d’Azure Machine Learning Studio via le langage de hello R à l’aide de hello [Execute R Script] [ execute-r-script] module.</span><span class="sxs-lookup"><span data-stu-id="d8927-104">You can extend hello functionality of Azure Machine Learning Studio through hello R language by using hello [Execute R Script][execute-r-script] module.</span></span>

<span data-ttu-id="d8927-105">Ce module accepte plusieurs jeux de données d’entrée et génère un jeu de données unique en sortie.</span><span class="sxs-lookup"><span data-stu-id="d8927-105">This module accepts multiple input datasets and yields a single dataset as output.</span></span> <span data-ttu-id="d8927-106">Vous pouvez taper un script R dans hello **Script R** paramètre Hello [Execute R Script] [ execute-r-script] module.</span><span class="sxs-lookup"><span data-stu-id="d8927-106">You can type an R script into hello **R Script** parameter of hello [Execute R Script][execute-r-script] module.</span></span>

<span data-ttu-id="d8927-107">Pour accéder à chaque port d’entrée du module de hello à l’aide de code similaire toohello suivant :</span><span class="sxs-lookup"><span data-stu-id="d8927-107">You access each input port of hello module by using code similar toohello following:</span></span>

    dataset1 <- maml.mapInputPort(1)

## <a name="listing-all-currently-installed-packages"></a><span data-ttu-id="d8927-108">Liste de tous les packages actuellement installés</span><span class="sxs-lookup"><span data-stu-id="d8927-108">Listing all currently-installed packages</span></span>
<span data-ttu-id="d8927-109">liste Hello des packages installés peut modifier.</span><span class="sxs-lookup"><span data-stu-id="d8927-109">hello list of installed packages can change.</span></span> <span data-ttu-id="d8927-110">Vous trouverez une liste des packages actuellement installés dans [R Packages Supported by Azure Machine Learning](https://msdn.microsoft.com/library/azure/mt741980.aspx) (Packages R pris en charge par Azure Machine Learning).</span><span class="sxs-lookup"><span data-stu-id="d8927-110">A list of currently installed packages can be found in [R Packages Supported by Azure Machine Learning](https://msdn.microsoft.com/library/azure/mt741980.aspx).</span></span>

<span data-ttu-id="d8927-111">Vous pouvez également obtenir hello liste complète et actuelle des packages installés en entrant hello après le code dans hello [Execute R Script] [ execute-r-script] module :</span><span class="sxs-lookup"><span data-stu-id="d8927-111">You also can get hello complete, current list of installed packages by entering hello following code into hello [Execute R Script][execute-r-script] module:</span></span>

    out <- data.frame(installed.packages(,,,fields="Description"))
    maml.mapOutputPort("out")

<span data-ttu-id="d8927-112">Cela envoie la liste hello du port de sortie toohello packages Hello [Execute R Script] [ execute-r-script] module.</span><span class="sxs-lookup"><span data-stu-id="d8927-112">This sends hello list of packages toohello output port of hello [Execute R Script][execute-r-script] module.</span></span>
<span data-ttu-id="d8927-113">package de hello tooview liste, la connexion d’un module de conversion telles que [convertir tooCSV] [ convert-to-csv] toohello gauche sortie Hello [Execute R Script] [ execute-r-script]module, exécutez hello expérience, puis cliquez sur sortie hello de module de conversion hello et sélectionnez **télécharger**.</span><span class="sxs-lookup"><span data-stu-id="d8927-113">tooview hello package list, connect a conversion module such as [Convert tooCSV][convert-to-csv] toohello left output of hello [Execute R Script][execute-r-script] module, run hello experiment, then click hello output of hello conversion module and select **Download**.</span></span> 

![Télécharger la sortie de module de « Convertir tooCSV »](./media/machine-learning-extend-your-experiment-with-r/download-package-list.png)


<!--
For convenience, here is hello [current full list with version numbers in Excel format](http://az754797.vo.msecnd.net/docs/RPackages.xlsx).
-->

## <a name="importing-packages"></a><span data-ttu-id="d8927-115">Importation de packages</span><span class="sxs-lookup"><span data-stu-id="d8927-115">Importing packages</span></span>
<span data-ttu-id="d8927-116">Vous pouvez importer des packages qui ne sont pas déjà installés à l’aide de hello suivant les commandes Bonjour [Execute R Script] [ execute-r-script] module :</span><span class="sxs-lookup"><span data-stu-id="d8927-116">You can import packages that are not already installed by using hello following commands in hello [Execute R Script][execute-r-script] module:</span></span>

    install.packages("src/my_favorite_package.zip", lib = ".", repos = NULL, verbose = TRUE)
    success <- library("my_favorite_package", lib.loc = ".", logical.return = TRUE, verbose = TRUE)

<span data-ttu-id="d8927-117">où hello `my_favorite_package.zip` fichier contient votre package.</span><span class="sxs-lookup"><span data-stu-id="d8927-117">where hello `my_favorite_package.zip` file contains your package.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[convert-to-csv]: https://msdn.microsoft.com/library/azure/faa6ba63-383c-4086-ba58-7abf26b85814/
