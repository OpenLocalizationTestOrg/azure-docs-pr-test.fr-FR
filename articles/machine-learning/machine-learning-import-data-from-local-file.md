---
title: "Importer des données à partir d’un fichier dans Azure Machine Learning Studio | Microsoft Docs"
description: "Découvrez comment charger un fichier de données d’apprentissage de votre disque dur sur Azure Machine Learning Studio. Un module de jeu de données est ainsi créé dans l’espace de travail."
keywords: "importer des données, format de données, types de données, sources de données, données d’apprentissage"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: c0dd9e90-23c4-4f64-8b8f-489ad79f047b
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye;bradsev
ms.openlocfilehash: 18010864160ceb2d76aea37196e6944bbe426457
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="import-training-data-from-a-file-on-your-hard-drive-into-machine-learning-studio"></a><span data-ttu-id="9c6bf-105">Importer des données d’apprentissage à partir d’un fichier situé sur votre disque dur dans Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="9c6bf-105">Import training data from a file on your hard drive into Machine Learning Studio</span></span>
[!INCLUDE [import-data-into-aml-studio-selector](../../includes/machine-learning-import-data-into-aml-studio.md)]

<span data-ttu-id="9c6bf-106">Découvrez comment charger un fichier de données de votre disque dur pour vous en servir comme données d’apprentissage dans Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="9c6bf-106">Learn how to upload a data file from your hard drive to use as training data in Azure Machine Learning Studio.</span></span> <span data-ttu-id="9c6bf-107">En important le fichier de données, vous disposez d’un module de jeu de données prêt à l’emploi dans votre espace de travail.</span><span class="sxs-lookup"><span data-stu-id="9c6bf-107">By importing the data file, you have a dataset module ready for use in your workspace.</span></span>

## <a name="steps-to-import-data-from-a-local-file"></a><span data-ttu-id="9c6bf-108">Étapes d’importation des données à partir d’un fichier local</span><span class="sxs-lookup"><span data-stu-id="9c6bf-108">Steps to import data from a local file</span></span>
<span data-ttu-id="9c6bf-109">Pour importer des données à partir d’un disque dur local, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="9c6bf-109">To import data from a local hard drive, do the following:</span></span>

1. <span data-ttu-id="9c6bf-110">Cliquez sur **+NOUVEAU** en bas de la fenêtre de Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="9c6bf-110">Click **+NEW** at the bottom of the Machine Learning Studio window.</span></span>
2. <span data-ttu-id="9c6bf-111">Sélectionnez **JEU DE DONNÉES** et **DEPUIS UN FICHIER LOCAL**.</span><span class="sxs-lookup"><span data-stu-id="9c6bf-111">Select **DATASET** and **FROM LOCAL FILE**.</span></span>
3. <span data-ttu-id="9c6bf-112">Dans la boîte de dialogue **Télécharger un nouveau jeu de données** , recherchez le fichier que vous souhaitez télécharger</span><span class="sxs-lookup"><span data-stu-id="9c6bf-112">In the **Upload a new dataset** dialog, browse to the file you want to upload</span></span>
4. <span data-ttu-id="9c6bf-113">Saisissez un nom, identifiez le type de données puis saisissez éventuellement une description.</span><span class="sxs-lookup"><span data-stu-id="9c6bf-113">Enter a name, identify the data type, and optionally enter a description.</span></span> <span data-ttu-id="9c6bf-114">Une description est recommandée : elle vous permet d’enregistrer des caractéristiques relatives aux données que vous souhaitez mémoriser pour une utilisation future.</span><span class="sxs-lookup"><span data-stu-id="9c6bf-114">A description is recommended - it allows you to record any characteristics about the data that you want to remember when using the data in the future.</span></span>
5. <span data-ttu-id="9c6bf-115">La case à cocher **Il s'agit de la nouvelle version d'un jeu de donnée existant** vous permet de mettre à jour un jeu de données existant avec de nouvelles données.</span><span class="sxs-lookup"><span data-stu-id="9c6bf-115">The checkbox **This is the new version of an existing dataset** allows you to update an existing dataset with new data.</span></span> <span data-ttu-id="9c6bf-116">Cliquez sur cette case à cocher, puis saisissez le nom d’un jeu de données existant.</span><span class="sxs-lookup"><span data-stu-id="9c6bf-116">Click this checkbox and then enter the name of an existing dataset.</span></span>

![Charger un nouveau jeu de données](media/machine-learning-import-data-from-local-file/upload-dataset.png)

<span data-ttu-id="9c6bf-118">Pendant le téléchargement, vous verrez un message indiquant que votre fichier est en cours de téléchargement.</span><span class="sxs-lookup"><span data-stu-id="9c6bf-118">During upload, you'll see a message that your file is being uploaded.</span></span> <span data-ttu-id="9c6bf-119">Le temps de téléchargement dépend de la taille de vos données et de la vitesse de votre connexion au service.</span><span class="sxs-lookup"><span data-stu-id="9c6bf-119">Upload time depends on the size of your data and the speed of your connection to the service.</span></span> <span data-ttu-id="9c6bf-120">Si vous savez que le fichier prendra du temps, vous pouvez faire autre chose dans Machine Learning Studio en attendant.</span><span class="sxs-lookup"><span data-stu-id="9c6bf-120">If you know the file will take a long time, you can do other things inside Machine Learning Studio while you wait.</span></span> <span data-ttu-id="9c6bf-121">Cependant, la fermeture du navigateur entraîne l’échec du téléchargement.</span><span class="sxs-lookup"><span data-stu-id="9c6bf-121">However, closing the browser causes the data upload to fail.</span></span>

## <a name="dataset-module-is-ready-for-use"></a><span data-ttu-id="9c6bf-122">Module de jeu de données prêt à l’emploi</span><span class="sxs-lookup"><span data-stu-id="9c6bf-122">Dataset module is ready for use</span></span>
<span data-ttu-id="9c6bf-123">Une fois que vos données sont téléchargées, elles sont stockées dans un module de jeu de données et sont disponibles pour n'importe quelle expérience dans votre espace de travail.</span><span class="sxs-lookup"><span data-stu-id="9c6bf-123">Once your data is uploaded, it's stored in a dataset module and is available to any experiment in your workspace.</span></span>

<span data-ttu-id="9c6bf-124">Quand vous éditez une expérimentation, les jeux de données que vous avez créés apparaissent sous **Mes jeux de données** dans la liste **Jeux de données enregistrés** de la palette des modules.</span><span class="sxs-lookup"><span data-stu-id="9c6bf-124">When you're editing an experiment, you can find the datasets you've created in the **My Datasets** list under the **Saved Datasets** list in the module palette.</span></span> <span data-ttu-id="9c6bf-125">Vous pouvez glisser-déplacer le jeu de données dans le canevas de l’expérience en vue d’affiner l’analyse et Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="9c6bf-125">You can drag and drop the dataset onto the experiment canvas when you want to use the dataset for further analytics and machine learning.</span></span>
