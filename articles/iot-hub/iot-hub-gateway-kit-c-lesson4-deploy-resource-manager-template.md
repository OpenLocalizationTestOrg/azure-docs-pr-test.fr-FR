---
title: "Appareil SensorTag et passerelle Azure IoT - Leçon 4 : Créer un conteneur d’application | Microsoft Docs"
description: "Enregistrer des messages à partir de hub IoT de tooyour Intel NUC, notez-les tooAzure le stockage de Table et puis de les lire à partir du cloud de hello."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "le stockage des données dans le cloud hello, les données stockées dans le cloud, service de cloud computing iot"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: f84f9a85-e2c4-4a92-8969-f65eb34c194e
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: efee3bdc15ced104651f4a500311a5fe614267c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-function-app-and-storage-account"></a>Créer une application de fonction Azure et un compte de stockage

Les fonctions Azure est une solution pour l’exécution de facilement _fonctions_ (petits segments de code) dans le cloud de hello. Une application de la fonction Azure héberge l’exécution de hello de vos fonctions dans Azure. 

## <a name="what-you-will-do"></a>Procédure à suivre

- Utiliser un toocreate de modèle Azure Resource Manager, une application de la fonction Azure et un compte de stockage Azure. application de fonction Azure Hello écoute les événements de hub IoT tooAzure, traite les messages entrants et les écrit tooAzure le stockage de Table.

Si vous rencontrez des problèmes, recherchez des solutions sur hello [page Résolution des problèmes](iot-hub-gateway-kit-c-troubleshooting.md).


## <a name="what-you-will-learn"></a>Contenu

Dans cette leçon, vous allez apprendre :

- Comment toouse Azure Resource Manager toodeploy ressources Azure.
- Comment toouse Azure fonction application tooprocess les messages IoT Hub et les écrire tooa table dans le stockage Azure Table.

## <a name="what-you-need"></a>Ce dont vous avez besoin

Avec succès, vous devez avoir terminé les leçons précédentes hello :

- [Leçon 1 : Configurer l’Intel NUC comme passerelle IoT](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)
- [Leçon 2 : Préparer votre ordinateur hôte et Azure IoT Hub](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md)
- [Leçon 3 : Recevoir des messages à partir de SensorTag et lire des messages à partir de votre IoT Hub](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md)

## <a name="open-a-sample-app"></a>Ouvrir un exemple d’application

Accédez tooyour `iot-hub-c-intel-nuc-gateway-getting-started` dossier de dépôt, les fichiers de configuration de hello initialize et puis ouvrez hello exemple de projet dans Visual Studio Code en exécutant hello commande suivante :

```bash
cd Lesson4
npm install
gulp init
code .
```

![structure du référentiel](media/iot-hub-gateway-kit-lessons/lesson4/arm_template.png)

- Hello `arm-template.json` fichier est le modèle Azure Resource Manager hello qui contient une application de la fonction Azure et un compte de stockage Azure.
- Hello `arm-template-param.json` fichier est hello configuration utilisé par le modèle de gestionnaire de ressources Azure hello.
- Hello `ReceiveDeviceMessages` sous-dossier contient du code de Node.js hello pour hello fonction Azure.

## <a name="configure-azure-resource-manager-templates-and-create-resources-in-azure"></a>Configurer des modèles Azure Resource Manager et créer des ressources dans Azure

Hello de mise à jour `arm-template-param.json` fichier dans Visual Studio Code.

![modèle arm json](media/iot-hub-gateway-kit-lessons/lesson4/arm_template_param.png)

- Remplacez `[your IoT Hub name]` par `{my hub name}` que vous avez spécifié à la leçon 2.

Une fois que vous mettez à jour hello `arm-template-param.json` file, déployer hello ressources tooAzure en exécutant hello de commande suivante :

```bash
az group deployment create --template-file arm-template.json --parameters @arm-template-param.json -g iot-gateway
```

Utilisez `iot-gateway` en tant que valeur hello `{resource group name}` si vous n’avez pas modifier la valeur hello dans la leçon 2.

## <a name="summary"></a>Résumé

Vous avez créé votre tooprocess d’application Azure fonction messages de hub IoT et un stockage Azure compte toostore ces messages. Vous pouvez maintenant lire les messages envoyés par votre IoT hub de passerelle tooyour.

## <a name="next-steps"></a>Étapes suivantes
[Lire des messages conservés dans le stockage Azure](iot-hub-gateway-kit-c-lesson4-read-table-storage.md).
