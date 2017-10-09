---
title: "Se connecter framboises Pi (nœud) tooAzure IoT - leçon 3 : déploiement d’un modèle | Documents Microsoft"
description: "application de fonction Azure Hello écoute les événements de hub IoT tooAzure, traite les messages entrants et les écrit tooAzure le stockage de Table."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "le stockage des données dans le cloud hello, les données stockées dans le cloud, service de cloud computing iot"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 6c58de85-c5c4-4989-bb5e-08c45c549966
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: b6c0a9530cb80e3f78c0e96037f6f3942b602aea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-function-app-and-azure-storage-account"></a>Créer une application de fonction Azure et un compte de Stockage Azure
[Les fonctions Azure](../azure-functions/functions-overview.md) est une solution pour l’exécution de facilement *fonctions* (petits segments de code) dans le cloud de hello. Une application de la fonction Azure héberge l’exécution de hello de vos fonctions dans Azure.

## <a name="what-you-will-do"></a>Procédure à suivre
Utiliser un toocreate de modèle Azure Resource Manager, une application de la fonction Azure et un compte de stockage Azure. application de fonction Azure Hello écoute les événements de hub IoT tooAzure, traite les messages entrants et les écrit tooAzure le stockage de Table. Si vous rencontrez des problèmes, rechercher des solutions sur hello [page Résolution des problèmes](iot-hub-raspberry-pi-kit-node-troubleshooting.md).

## <a name="what-you-will-learn"></a>Contenu
Cet article portera sur les éléments suivants :

* Comment toouse [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) toodeploy Azure ressources.
* Comment toouse Azure application tooprocess messages de hub IoT de fonction et les écrire tooa table dans le stockage Azure Table.

## <a name="what-you-need"></a>Ce dont vous avez besoin
Vous devez avoir accompli avec succès les étapes :
* [Prise en main de Raspberry Pi 3](iot-hub-raspberry-pi-kit-node-get-started.md)
* [Créer votre Azure IoT Hub](iot-hub-raspberry-pi-kit-node-get-started.md)

## <a name="open-hello-sample-app"></a>Exemple d’application hello ouvert
Ouvrez hello exemple de projet dans Visual Studio Code en exécutant hello suivant de commandes :

```bash
cd Lesson3
code .
```

![Structure du référentiel](media/iot-hub-raspberry-pi-lessons/lesson3/repo_structure.png)

* Hello `app.js` fichier Bonjour `app` sous-dossier est le fichier de source de la clé hello. Ce fichier source contient hello code toosend un message 20 fois tooyour IoT hub et blink hello DEL pour chaque message qu’elle envoie.
* Hello `arm-template.json` fichier est le modèle Azure Resource Manager hello qui contient une application de la fonction Azure et un compte de stockage Azure.
* Hello `arm-template-param.json` fichier est hello configuration utilisé par le modèle de gestionnaire de ressources Azure hello.
* Hello `ReceiveDeviceMessages` sous-dossier contient du code de Node.js hello pour hello fonction Azure.

## <a name="configure-azure-resource-manager-templates-and-create-resources-in-azure"></a>Configurer des modèles Azure Resource Manager et créer des ressources dans Azure
Hello de mise à jour `arm-template-param.json` fichier dans Visual Studio Code.

![Paramètres de modèle Azure Resource Manager](media/iot-hub-raspberry-pi-lessons/lesson3/arm_para.png)

* Remplacez **[nom de votre IoT Hub]** par **{nom de mon hub}** que vous avez spécifié lorsque vous [avez créé votre IoT Hub et inscrit Raspberry Pi 3](iot-hub-raspberry-pi-kit-node-lesson2-prepare-azure-iot-hub.md).
* Remplacez la **[chaîne de préfixe pour les nouvelles ressources]** par un préfixe de votre choix quelconque. préfixe de Hello garantit que ce nom de ressource hello est globalement unique tooavoid conflit. N’utilisez pas un numéro initial en préfixe de hello ou un tiret.

Une fois que vous mettez à jour hello `arm-template-param.json` file, déployer hello ressources tooAzure en exécutant hello de commande suivante :

```bash
az group deployment create --template-file arm-template.json --parameters @arm-template-param.json -g iot-sample
```

Il prend environ cinq minutes toocreate ces ressources. Lors de la création de la ressource hello est en cours d’exécution, vous pouvez déplacer sur l’article suivant de toohello.

## <a name="summary"></a>Résumé
Vous avez créé votre tooprocess d’application Azure fonction messages de hub IoT et un stockage Azure compte toostore ces messages. Vous pouvez désormais déployer et exécuter des messages appareil-à-cloud de hello exemple toosend sur Pi.

## <a name="next-steps"></a>Étapes suivantes
[Exécuter un toosend d’application exemple messages appareil-à-cloud sur framboises Pi 3](iot-hub-raspberry-pi-kit-node-lesson3-run-azure-blink.md)

