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
# <a name="import-training-data-from-a-file-on-your-hard-drive-into-machine-learning-studio"></a>Importer des données d’apprentissage à partir d’un fichier situé sur votre disque dur dans Machine Learning Studio
[!INCLUDE [import-data-into-aml-studio-selector](../../includes/machine-learning-import-data-into-aml-studio.md)]

Découvrez comment tooupload des données de fichiers à partir de votre toouse de disque dur en tant que données d’apprentissage dans Azure Machine Learning Studio. En important un fichier de données hello, vous avez un module de jeu de données prêt à être utilisé dans votre espace de travail.

## <a name="steps-tooimport-data-from-a-local-file"></a>Données de tooimport étapes à partir d’un fichier local
tooimport des données à partir d’un disque dur local, procédez comme hello suivant :

1. Cliquez sur **+ nouveau** bas hello de fenêtre de Machine Learning Studio hello.
2. Sélectionnez **JEU DE DONNÉES** et **DEPUIS UN FICHIER LOCAL**.
3. Bonjour **télécharger un nouveau dataset** boîte de dialogue Parcourir toohello fichier tooupload
4. Entrez un nom, identifiez le type de données hello et entrez éventuellement une description. Une description est recommandée : il vous permet de toorecord les caractéristiques données hello que vous souhaitez tooremember lors de l’utilisation des données de hello dans les futures hello.
5. case à cocher de Hello **c’est hello une nouvelle version d’un dataset existant** vous permet de tooupdate un dataset existant avec les nouvelles données. Cliquez sur cette case à cocher, puis entrez les nom hello d’un dataset existant.

![Charger un nouveau jeu de données](media/machine-learning-import-data-from-local-file/upload-dataset.png)

Pendant le téléchargement, vous verrez un message indiquant que votre fichier est en cours de téléchargement. Télécharger temps dépend de la taille de hello de vos données et hello la vitesse de votre service de toohello de connexion. Si vous connaissez les fichier hello prendra un certain temps, vous pouvez effectuer d’autres opérations à l’intérieur de Machine Learning Studio pendant que vous attendez. Toutefois, la fermeture du navigateur de hello, toofail de téléchargement de données hello.

## <a name="dataset-module-is-ready-for-use"></a>Module de jeu de données prêt à l’emploi
Une fois téléchargées vos données, il est stocké dans un module de jeu de données et est expérience tooany disponibles dans votre espace de travail.

Lorsque vous modifiez une expérience, vous pouvez trouver hello de jeux de données que vous avez créé dans hello **mes Datasets** liste sous hello **jeux de données enregistrés** liste dans la palette de module hello. Vous pouvez glisser -déplacer hello le jeu de données sur le canevas de l’expérience hello lorsque vous souhaitez toouse hello dataset pour davantage d’analytique et l’apprentissage.
