---
title: "Importer des données dans Machine Learning Studio à partir d’une autre expérience | Microsoft Docs"
description: "Comment enregistrer des données d’apprentissage dans Azure Machine Learning Studio et les utiliser dans une autre expérience"
keywords: "importer des données,données,sources de données,données d’apprentissage"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 7da9dcec-5693-4bb6-8166-15904e7f75c3
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye;bradsev
ms.openlocfilehash: ecfa2110d0d51511ceb5bd07b730732ecfa2e9e0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="import-your-data-into-azure-machine-learning-studio-from-another-experiment"></a><span data-ttu-id="d74a5-104">Importer vos données dans Azure Machine Learning Studio à partir d’une autre expérience</span><span class="sxs-lookup"><span data-stu-id="d74a5-104">Import your data into Azure Machine Learning Studio from another experiment</span></span>
[!INCLUDE [import-data-into-aml-studio-selector](../../includes/machine-learning-import-data-into-aml-studio.md)]

<span data-ttu-id="d74a5-105">Il se peut que vous ayez parfois besoin d’obtenir un résultat intermédiaire à partir d’une expérience et de l’utiliser dans le cadre d’une autre expérience.</span><span class="sxs-lookup"><span data-stu-id="d74a5-105">There will be times when you'll want to take an intermediate result from one experiment and use it as part of another experiment.</span></span> <span data-ttu-id="d74a5-106">Pour ce faire, vous enregistrez le module en tant que jeu de données :</span><span class="sxs-lookup"><span data-stu-id="d74a5-106">To do this, you save the module as a dataset:</span></span>

1. <span data-ttu-id="d74a5-107">Cliquez sur la sortie du module que vous souhaitez enregistrer en tant que jeu de données.</span><span class="sxs-lookup"><span data-stu-id="d74a5-107">Click the output of the module that you want to save as a dataset.</span></span>
2. <span data-ttu-id="d74a5-108">Cliquez sur **Enregistrer comme jeu de données**.</span><span class="sxs-lookup"><span data-stu-id="d74a5-108">Click **Save as Dataset**.</span></span>
3. <span data-ttu-id="d74a5-109">Lorsque vous y êtes invité, saisissez un nom et une description qui vous permet d'identifier facilement le jeu de données.</span><span class="sxs-lookup"><span data-stu-id="d74a5-109">When prompted, enter a name and a description that would allow you to identify the dataset easily.</span></span>
4. <span data-ttu-id="d74a5-110">Cliquez sur la coche **OK** .</span><span class="sxs-lookup"><span data-stu-id="d74a5-110">Click the **OK** checkmark.</span></span>

<span data-ttu-id="d74a5-111">Lorsque l'enregistrement est terminé, le jeu de données sera disponible pour être utilisé dans n'importe quelle expérience dans votre espace de travail.</span><span class="sxs-lookup"><span data-stu-id="d74a5-111">When the save finishes, the dataset will be available for use within any experiment in your workspace.</span></span> <span data-ttu-id="d74a5-112">Vous pouvez le trouver dans la liste **Jeux de données enregistrés** dans la palette des modules.</span><span class="sxs-lookup"><span data-stu-id="d74a5-112">You can find it in the **Saved Datasets** list in the module palette.</span></span>

