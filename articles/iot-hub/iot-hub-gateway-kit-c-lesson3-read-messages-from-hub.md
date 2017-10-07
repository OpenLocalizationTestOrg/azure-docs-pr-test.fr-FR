---
title: "Appareil SensorTag et passerelle Azure IoT - Leçon 3 : Lire des messages | Microsoft Docs"
description: "Exécuter un exemple de code sur votre hôte ordinateur tooread hello des messages à partir de votre hub IoT."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "données dans le cloud de hello, collecte de données de cloud, le service cloud iot, iot données"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: cc88be24-b5c0-4ef2-ba21-4e8f77f3e167
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: d3ffbe2e83f9d61c0088b8876a7f0eea62c1fbe1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="read-messages-from-your-iot-hub"></a>Lire des messages à partir de votre IoT Hub

## <a name="what-you-will-do"></a>Procédure à suivre

- Exécutez exemple de code sur votre hôte tooread ordinateur des messages à partir de votre hub IoT.

Si vous rencontrez des problèmes, recherchez des solutions sur hello [page Résolution des problèmes](iot-hub-gateway-kit-c-troubleshooting.md).

## <a name="what-you-will-learn"></a>Contenu

Comment toouse hello gulp tooread messages de l’outil à partir de votre hub IoT.

## <a name="what-you-need"></a>Ce dont vous avez besoin

- Hello exemple d’application BLE qui vous a été correctement exécuté dans la leçon 3.

## <a name="get-your-iot-hub-and-device-connection-strings"></a>Obtenir vos chaînes de connexion d’IoT Hub et d’appareil

chaîne de connexion de périphérique Hello est utilisé par votre appareil (TI SensorTag ou appareil simulé) tooconnect tooyour IoT de supervision. Hello chaîne de connexion de hub IoT est un registre des identités toohello tooconnect utilisés dans vos appareils IoT hub toomanage hello autorisées tooconnect tooyour IoT hub.

- Liste de tous vos hubs IoT dans votre groupe de ressources en exécutant hello de commande suivante :

   ```bash
   az iot hub list -g iot-gateway --query [].name
   ```

   Utilisez `iot-gateway` en tant que valeur hello `{resource group name}` si vous n’avez modifié la valeur de hello.
- Obtenir la chaîne de connexion de hub IoT hello en exécutant hello de commande suivante :

   ```bash
   az iot hub show-connection-string --name {my hub name} -g iot-gateway
   ```

   `{my hub name}`est le nom hello que vous avez spécifié dans la leçon 2.

## <a name="configure-hello-device-connection-for-hello-sample-code"></a>Configurer la connexion du périphérique pour l’exemple de code hello hello

Fichier de configuration de mise à jour hello périphérique `config-azure.json` afin que vous pouvez lire les messages de votre hub IoT sur votre ordinateur hôte. toodo, procédez comme suit :

1. Ouvrez `config-azure.json` dans le Code de Visual Studio en exécutant hello commande dans une fenêtre de console suivante :

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-azure.json
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-azure.json
   ```

2. Rendre hello suivant remplacements Bonjour `config-azure.json` fichier :

   ![capture d’écran de configuration azure](media/iot-hub-gateway-kit-lessons/lesson3/config_azure.png)

   Remplacez `[IoT hub connection string]` par hello chaîne de connexion de hub IoT que vous avez obtenu.

## <a name="read-messages-from-your-iot-hub"></a>Lire des messages à partir de votre IoT Hub

Si vous avez un TI SensorTag, assurez-vous que vous avez déjà démarré votre SensorTag. Exécuter l’application d’exemple hello passerelle et lire des messages de IoT Hub par hello de commande suivante :

```bash
gulp run --iot-hub
```

commande Hello exécute hello BLE exemple d’application qui lit et packages de données de température de votre SensorTag ou d’un appareil simulé et envoie tooyour IoT hub hello message toutes les 2 secondes. Il génère également un message de salutation tooreceive processus enfant.

messages de type Hello qui sont envoyés et reçus sont tous les hello afficher instantanément à même de fenêtre dans la console hello machine hôte. instance de l’application exemple Hello se termine automatiquement au bout de 40 secondes.

![Exemple d’application BLE avec des messages envoyés et reçus](media/iot-hub-gateway-kit-lessons/lesson3/gulp_run_read_hub.png)

## <a name="summary"></a>Résumé

Vous avez exécuté un tooread de code d’exemple de messages à partir de votre hub IoT. Vous êtes prêt tooread les messages hello qui sont stockés dans votre stockage de table Windows Azure.

## <a name="next-steps"></a>Étapes suivantes
[Créer une application de fonction Azure et un compte de stockage Azure](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md)


