---
title: "aaaImport des données à partir d’un fichier dans Azure Machine Learning Studio | Documents Microsoft"
description: "Découvrez comment tooupload données d’apprentissage de fichiers à partir de votre disque dur de tooAzure Machine Learning Studio. Cette opération crée un module de jeu de données dans l’espace de travail hello."
keywords: "importer des données, format de données, types de données, sources de données, données d'apprentissage"
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
ms.openlocfilehash: 636facd9042145382c953a1c75969149ede6f6fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="import-training-data-from-a-file-on-your-hard-drive-into-machine-learning-studio"></a><span data-ttu-id="9f296-105">Importer des données d’apprentissage à partir d’un fichier situé sur votre disque dur dans Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="9f296-105">Import training data from a file on your hard drive into Machine Learning Studio</span></span>
[!INCLUDE [import-data-into-aml-studio-selector](../../includes/machine-learning-import-data-into-aml-studio.md)]

<span data-ttu-id="9f296-106">Découvrez comment tooupload des données de fichiers à partir de votre toouse de disque dur en tant que données d’apprentissage dans Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="9f296-106">Learn how tooupload a data file from your hard drive toouse as training data in Azure Machine Learning Studio.</span></span> <span data-ttu-id="9f296-107">En important un fichier de données hello, vous avez un module de jeu de données prêt à être utilisé dans votre espace de travail.</span><span class="sxs-lookup"><span data-stu-id="9f296-107">By importing hello data file, you have a dataset module ready for use in your workspace.</span></span>

## <a name="steps-tooimport-data-from-a-local-file"></a><span data-ttu-id="9f296-108">Données de tooimport étapes à partir d’un fichier local</span><span class="sxs-lookup"><span data-stu-id="9f296-108">Steps tooimport data from a local file</span></span>
<span data-ttu-id="9f296-109">tooimport des données à partir d’un disque dur local, procédez comme hello suivant :</span><span class="sxs-lookup"><span data-stu-id="9f296-109">tooimport data from a local hard drive, do hello following:</span></span>

1. <span data-ttu-id="9f296-110">Cliquez sur **+ nouveau** bas hello de fenêtre de Machine Learning Studio hello.</span><span class="sxs-lookup"><span data-stu-id="9f296-110">Click **+NEW** at hello bottom of hello Machine Learning Studio window.</span></span>
2. <span data-ttu-id="9f296-111">Sélectionnez **JEU DE DONNÉES** et **DEPUIS UN FICHIER LOCAL**.</span><span class="sxs-lookup"><span data-stu-id="9f296-111">Select **DATASET** and **FROM LOCAL FILE**.</span></span>
3. <span data-ttu-id="9f296-112">Bonjour **télécharger un nouveau dataset** boîte de dialogue Parcourir toohello fichier tooupload</span><span class="sxs-lookup"><span data-stu-id="9f296-112">In hello **Upload a new dataset** dialog, browse toohello file you want tooupload</span></span>
4. <span data-ttu-id="9f296-113">Entrez un nom, identifiez le type de données hello et entrez éventuellement une description.</span><span class="sxs-lookup"><span data-stu-id="9f296-113">Enter a name, identify hello data type, and optionally enter a description.</span></span> <span data-ttu-id="9f296-114">Une description est recommandée : il vous permet de toorecord les caractéristiques données hello que vous souhaitez tooremember lors de l’utilisation des données de hello dans les futures hello.</span><span class="sxs-lookup"><span data-stu-id="9f296-114">A description is recommended - it allows you toorecord any characteristics about hello data that you want tooremember when using hello data in hello future.</span></span>
5. <span data-ttu-id="9f296-115">case à cocher de Hello **c’est hello une nouvelle version d’un dataset existant** vous permet de tooupdate un dataset existant avec les nouvelles données.</span><span class="sxs-lookup"><span data-stu-id="9f296-115">hello checkbox **This is hello new version of an existing dataset** allows you tooupdate an existing dataset with new data.</span></span> <span data-ttu-id="9f296-116">Cliquez sur cette case à cocher, puis entrez les nom hello d’un dataset existant.</span><span class="sxs-lookup"><span data-stu-id="9f296-116">Click this checkbox and then enter hello name of an existing dataset.</span></span>

![Charger un nouveau jeu de données](media/machine-learning-import-data-from-local-file/upload-dataset.png)

<span data-ttu-id="9f296-118">Pendant le téléchargement, vous verrez un message indiquant que votre fichier est en cours de téléchargement.</span><span class="sxs-lookup"><span data-stu-id="9f296-118">During upload, you'll see a message that your file is being uploaded.</span></span> <span data-ttu-id="9f296-119">Télécharger temps dépend de la taille de hello de vos données et hello la vitesse de votre service de toohello de connexion.</span><span class="sxs-lookup"><span data-stu-id="9f296-119">Upload time depends on hello size of your data and hello speed of your connection toohello service.</span></span> <span data-ttu-id="9f296-120">Si vous connaissez les fichier hello prendra un certain temps, vous pouvez effectuer d’autres opérations à l’intérieur de Machine Learning Studio pendant que vous attendez.</span><span class="sxs-lookup"><span data-stu-id="9f296-120">If you know hello file will take a long time, you can do other things inside Machine Learning Studio while you wait.</span></span> <span data-ttu-id="9f296-121">Toutefois, la fermeture du navigateur de hello, toofail de téléchargement de données hello.</span><span class="sxs-lookup"><span data-stu-id="9f296-121">However, closing hello browser causes hello data upload toofail.</span></span>

## <a name="dataset-module-is-ready-for-use"></a><span data-ttu-id="9f296-122">Module de jeu de données prêt à l’emploi</span><span class="sxs-lookup"><span data-stu-id="9f296-122">Dataset module is ready for use</span></span>
<span data-ttu-id="9f296-123">Une fois téléchargées vos données, il est stocké dans un module de jeu de données et est expérience tooany disponibles dans votre espace de travail.</span><span class="sxs-lookup"><span data-stu-id="9f296-123">Once your data is uploaded, it's stored in a dataset module and is available tooany experiment in your workspace.</span></span>

<span data-ttu-id="9f296-124">Lorsque vous modifiez une expérience, vous pouvez trouver hello de jeux de données que vous avez créé dans hello **mes Datasets** liste sous hello **jeux de données enregistrés** liste dans la palette de module hello.</span><span class="sxs-lookup"><span data-stu-id="9f296-124">When you're editing an experiment, you can find hello datasets you've created in hello **My Datasets** list under hello **Saved Datasets** list in hello module palette.</span></span> <span data-ttu-id="9f296-125">Vous pouvez glisser -déplacer hello le jeu de données sur le canevas de l’expérience hello lorsque vous souhaitez toouse hello dataset pour davantage d’analytique et l’apprentissage.</span><span class="sxs-lookup"><span data-stu-id="9f296-125">You can drag and drop hello dataset onto hello experiment canvas when you want toouse hello dataset for further analytics and machine learning.</span></span>
