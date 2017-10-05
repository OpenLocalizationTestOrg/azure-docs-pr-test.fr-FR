---
title: "Connecter Intel Edison (Node) à Azure IoT - Leçon 3 : Créer un conteneur de fonctions | Microsoft Docs"
description: "L’application de fonction Azure écoute les événements d’Azure IoT Hub, traite les messages entrants et les écrit dans le stockage Table Azure."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "stockage de données dans le cloud, les données stockées dans le cloud, service cloud iot"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: 37ee5962-95ce-40e8-8162-17e735eaec21
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 6ada1cbbb560f1373346eca561dceb28d7ca7242
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-function-app-and-azure-storage-account"></a>Créer une application de fonction Azure et un compte de Stockage Azure
[Azure Functions](../../articles/azure-functions/functions-overview.md) est une solution conçue pour exécuter facilement des petits morceaux de code (« *functions* ») dans le cloud. Une application de fonction Azure héberge l’exécution de vos fonctions dans Azure.

## <a name="what-will-you-do"></a>Ce que vous allez faire
Utilisez un modèle Azure Resource Manager pour créer une application de fonction Azure et un compte de Stockage Azure. L’application de fonction Azure écoute les événements d’Azure IoT Hub, traite les messages entrants et les écrit dans le stockage Table Azure. Le compte de stockage est utilisé pour la lecture des copies persistantes des messages à partir de la table Azure. Si vous rencontrez des problèmes, recherchez des solutions sur la [page de résolution des problèmes][troubleshooting].

## <a name="what-will-you-learn"></a>Ce que vous allez apprendre
Cet article portera sur les éléments suivants :
* Commet utiliser [Azure Resource Manager](../../articles/azure-resource-manager/resource-group-overview.md) pour déployer des ressources Azure.
* Comment utiliser une application de fonction Azure pour traiter les messages de l’IoT Hub et les écrire dans une table du stockage Table Azure.

## <a name="what-do-you-need"></a>Ce dont vous avez besoin
Vous devez avoir accompli avec succès les étapes :
- [Prise en main d’Intel Edison][get-started-with-your-intel-edison]
- [Créer votre Azure IoT Hub][create-your-azure-iot-hub]

## <a name="open-the-sample-app"></a>Ouvrir l’exemple d’application
Ouvrez l’exemple de projet dans Visual Studio Code en exécutant les commandes suivantes :

```bash
cd Lesson3
code .
```

![Structure du référentiel][repo-structure]

* Le fichier se trouvant dans le sous-dossier `app` est le fichier source clé. Ce fichier source contient le code pour envoyer un message 20 fois à votre IoT hub et faire clignoter la LED pour chaque message envoyé.
* Le fichier `arm-template.json` est le modèle Azure Resource Manager qui contient une application de fonction Azure et un compte de Stockage Azure.
* Le fichier `arm-template-param.json` est le fichier de configuration utilisé par le modèle Azure Resource Manager.
* Le sous-dossier `ReceiveDeviceMessages` contient le code Node.js pour la fonction Azure.

## <a name="configure-azure-resource-manager-templates-and-create-resources-in-azure"></a>Configurer des modèles Azure Resource Manager et créer des ressources dans Azure
Mettez à jour le fichier `arm-template-param.json` dans Visual Studio Code.

![Paramètres de modèle Azure Resource Manager][arm-template-parameters]

* Remplacez **[nom de votre IoT Hub]** par **{nom de mon hub}**, que vous avez spécifié lorsque vous [avez créé votre IoT Hub et inscrit Intel Edison][created-your-iot-hub-and-registered-intel-edison].
* Remplacez la **[chaîne de préfixe pour les nouvelles ressources]** par un préfixe de votre choix quelconque. Le préfixe vous assure que le nom de ressource est globalement unique pour éviter tout conflit. N’utilisez pas de tiret ni de chiffre initial dans le préfixe.

Une fois que vous avez mis à jour le fichier `arm-template-param.json`, déployez les ressources dans Azure en exécutant la commande suivante :

```bash
az group deployment create --template-file arm-template.json --parameters @arm-template-param.json -g iot-sample
```

La création de ces ressources prend environ cinq minutes. Pendant la création de ressources, vous pouvez passer à l’article suivant.

## <a name="summary"></a>Résumé
Vous avez créé votre application de fonction Azure pour traiter les messages de l’IoT Hub et un compte de Stockage Azure pour stocker ces messages. Vous pouvez désormais déployer et exécuter l’exemple pour envoyer des messages appareil-à-cloud sur Edison.

## <a name="next-steps"></a>Étapes suivantes
[Exécuter un exemple d’application pour envoyer des messages appareil-à-cloud sur Intel Edison][send-device-to-cloud-messages].
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[get-started-with-your-intel-edison]: iot-hub-intel-edison-kit-node-get-started.md
[create-your-azure-iot-hub]: iot-hub-intel-edison-kit-node-get-started.md
[repo-structure]: media/iot-hub-intel-edison-lessons/lesson3/repo_structure.png
[arm-template-parameters]: media/iot-hub-intel-edison-lessons/lesson3/arm_para.png
[created-your-iot-hub-and-registered-intel-edison]: iot-hub-intel-edison-kit-node-lesson2-prepare-azure-iot-hub.md
[send-device-to-cloud-messages]: iot-hub-intel-edison-kit-node-lesson3-run-azure-blink.md