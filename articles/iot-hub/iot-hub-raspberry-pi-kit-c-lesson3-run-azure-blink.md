---
title: "Connecter Raspberry Pi (C) à Azure IoT - Leçon 3 : Exécuter les exemples | Microsoft Docs"
description: "Déployez et exécutez sur Raspberry Pi 3 un exemple d’application qui envoie des messages à votre IoT Hub et fait clignoter la LED."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "led clignotante cloud pi, clignotement led à partir du cloud"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: e38df29f-f77f-435f-9add-46814297564f
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: e583ba455a94f9afcc7b31e49425b518d7968919
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="run-a-sample-application-to-send-device-to-cloud-messages"></a>Exécution d’un exemple d’application pour envoyer des messages appareil-à-cloud
## <a name="what-you-will-do"></a>Procédure à suivre
Cet article vous explique comment déployer et exécuter sur Raspberry Pi 3 un exemple d’application qui envoie des messages à votre IoT Hub. Si vous rencontrez des problèmes, recherchez des solutions dans la [page de résolution des problèmes](iot-hub-raspberry-pi-kit-c-troubleshooting.md).

## <a name="what-you-will-learn"></a>Contenu
Vous apprendrez à utiliser l’outil gulp pour déployer et exécuter l’exemple d’application Node.js sur Pi.

## <a name="what-you-need"></a>Ce dont vous avez besoin
* Avant de commencer cette tâche, vous devez avoir correctement suivi la section [Création d’une application de fonction Azure et d’un compte de stockage pour traiter et stocker des messages du IoT Hub](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md).

## <a name="get-your-iot-hub-and-device-connection-strings"></a>Obtenir vos chaînes de connexion d’IoT Hub et d’appareil
La chaîne de connexion de l’appareil permet de connecter votre Pi à votre IoT Hub. La chaîne de connexion IoT Hub sert à se connecter au registre des identités de votre IoT Hub pour gérer les appareils autorisés à se connecter à votre IoT Hub. 

* Répertorier tous les IoT Hubs de votre groupe de ressources en exécutant la commande suivante de l’interface de ligne de commande Azure :

```bash
az iot hub list -g iot-sample --query [].name
```

Si vous n’avez pas modifié la valeur, utilisez `iot-sample` en tant que valeur de `{resource group name}`.

* Obtenez la chaîne de connexion de l’IoT Hub en exécutant la commande de l’interface de ligne de commande Azure suivante :

```bash
az iot hub show-connection-string --name {my hub name} -g iot-sample
```

`{my hub name}` est le nom que vous avez spécifié lorsque vous avez créé votre IoT Hub et inscrit Pi.

* Obtenez la chaîne de connexion de l’appareil en exécutant la commande suivante :

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id myraspberrypi -g iot-sample
```

Si vous n’avez pas modifié la valeur, utilisez `myraspberrypi` en tant que valeur de `{device id}`.

## <a name="configure-the-device-connection"></a>Configuration de la connexion de l’appareil
1. Initialisez le fichier de configuration en exécutant les commandes suivantes :
   
   ```bash
   npm install
   gulp init
   ```

> [!NOTE]
> Exécutez également **gulp install-tools**, si vous ne l’avez pas fait dans la leçon 1.

2. Ouvrez le fichier de configuration de l’appareil `config-raspberrypi.json` dans Visual Studio Code en exécutant la commande suivante :
   
   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-raspberrypi.json
   
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-raspberrypi.json
   ```
   
   ![config.json](media/iot-hub-raspberry-pi-lessons/lesson3/config.png)
3. Dans le fichier `config-raspberrypi.json`, effectuez les remplacements suivants :
   
   * Remplacez **[nom d’hôte ou adresse IP de l’appareil]** par l’adresse IP ou le nom d’hôte d’appareil obtenu(e) à l’aide de la commande `device-discovery-cli`, ou par la valeur héritée lorsque vous avez configuré votre appareil.
   * Remplacez **[chaîne de connexion de l’appareil IoT]** par la `device connection string` obtenue.
   * Remplacez **[chaîne de connexion d’IoT Hub]** par la `iot hub connection string` obtenue.

> [!NOTE]
> Vous n’avez pas besoin de `azure_storage_connection_string` dans cet article. Gardez-le tel quel.

Mettez à jour le fichier `config-raspberrypi.json` afin de pouvoir déployer l’exemple d’application à partir de votre ordinateur.

## <a name="deploy-and-run-the-sample-application"></a>Déploiement et exécution de l’exemple d’application
Déployez et exécutez l’exemple d’application sur Pi en exécutant la commande suivante :

```bash
gulp deploy && gulp run
```

## <a name="verify-that-the-sample-application-works"></a>Vérification du bon fonctionnement de l’exemple d’application
Vous devez voir la LED connectée à Pi clignoter toutes les deux secondes. Chaque fois que la LED clignote, l’exemple d’application envoie un message à votre IoT Hub et vérifie que le message a été correctement envoyé. De plus, chaque message reçu par l’IoT Hub apparaît dans la fenêtre de console. L’exemple d’application se termine automatiquement après l’envoi de 20 messages.

![Exemple d’application avec des messages envoyés et reçus](media/iot-hub-raspberry-pi-lessons/lesson3/gulp_run_c.png)

## <a name="summary"></a>Résumé
Vous avez déployé et exécuté le nouvel exemple d’application de clignotement sur Pi pour l’envoi de messages appareil-à-cloud à votre IoT Hub. Vous surveillez désormais les messages à mesure qu’ils sont écrits dans le compte de stockage.

## <a name="next-steps"></a>Étapes suivantes
[Lecture des messages conservés dans le Stockage Azure](iot-hub-raspberry-pi-kit-c-lesson3-read-table-storage.md)

