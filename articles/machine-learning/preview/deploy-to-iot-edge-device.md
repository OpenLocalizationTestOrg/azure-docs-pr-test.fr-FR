---
title: "Déployer un modèle Azure Machine Learning sur un appareil Azure IoT Edge | Microsoft Docs"
description: "Ce document décrit comment les modèles Azure Machine Learning peuvent être déployés sur des appareils Azure IoT Edge."
services: machine-learning
author: tedway
ms.author: tedway
manager: mwinkle
ms.reviewer: garyericson, jasonwhowell, mldocs
ms.service: machine-learning
ms.workload: data-services
ms.topic: article
ms.date: 11/10/2017
ms.openlocfilehash: f83e4b17a3209adeb655723362e6882e38bfaf49
ms.sourcegitcommit: 68aec76e471d677fd9a6333dc60ed098d1072cfc
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/18/2017
---
# <a name="deploy-an-azure-machine-learning-model-to-an-azure-iot-edge-device"></a>Déployer un modèle Azure Machine Learning sur un appareil Azure IoT Edge

Tous les modèles Azure Machine Learning placés dans des conteneurs en tant que services web Docker peuvent également s’exécuter sur des appareils Azure IoT Edge. Vous trouverez des scripts et des instructions supplémentaires dans le [Kit AI pour Azure IoT Edge](http://aka.ms/AI-toolkit).

## <a name="operationalize-the-model"></a>Opérationnaliser le modèle
Opérationnalisez votre modèle en suivant les instructions fournies dans [Déploiement d’un modèle d’apprentissage automatique comme service web](https://docs.microsoft.com/azure/machine-learning/preview/model-management-service-deploy) afin de créer une image Docker avec votre modèle.

## <a name="deploy-to-azure-iot-edge"></a>Déployer sur Azure IoT Edge
Azure IoT Edge déplace l’analytique et la logique métier personnalisée du cloud vers les appareils. Tous les modèles Machine Learning peuvent s’exécuter sur des appareils IoT Edge. La documentation pour configurer un appareil IoT Edge et créer un déploiement est disponible à l’adresse [aka.ms/azure-iot-edge-doc](https://aka.ms/azure-iot-edge-doc).

Voici quelques points supplémentaires à noter.

### <a name="add-registry-credentials-to-the-edge-runtime-on-your-edge-device"></a>Ajouter des informations d’identification du registre au runtime Edge sur votre appareil Edge
Sur l’ordinateur sur lequel vous exécutez IoT Edge, ajoutez les informations d’identification de votre registre afin que le runtime puisse avoir accès pour extraire le conteneur.

Pour Windows, exécutez la commande suivante :
```cmd/sh
iotedgectl login --address <docker-registry-address> --username <docker-username> --password <docker-password>
```
Pour Linux, exécutez la commande suivante :
```cmd/sh
sudo iotedgectl login --address <docker-registry-address> --username <docker-username> --password <docker-password>
```

### <a name="find-the-machine-learning-container-image-location"></a>Rechercher l’emplacement d’image de conteneur Machine Learning
Vous avez besoin de l’emplacement de votre image de conteneur Machine Learning. Pour rechercher l’emplacement de l’image de conteneur :

1. Connectez-vous au [portail Azure](http://portal.azure.com/).
2. Dans **Azure Container Registry**, sélectionnez le registre que vous souhaitez inspecter.
3. Dans le registre, cliquez sur **Dépôts** pour afficher la liste de tous les dépôts et leurs images.













