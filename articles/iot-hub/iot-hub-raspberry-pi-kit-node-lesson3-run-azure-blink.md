---
title: "Se connecter framboises Pi (nœud) tooAzure IoT - leçon 3 : exécuter l’exemple | Documents Microsoft"
description: "Déployer et exécuter un tooRaspberry d’application exemple Pi 3 qui envoie l’IoT hub tooyour de messages et clignote hello DEL."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "led clignotante cloud pi, clignotement led à partir du cloud"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 427d8e5e-8af8-4249-8607-44edc90a4972
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 991c64e0b1b6f965b029560cdc6403e557841e30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-toosend-device-to-cloud-messages"></a>Exécuter un toosend d’application exemple messages appareil-à-cloud
## <a name="what-you-will-do"></a>Procédure à suivre
Cet article vous explique comment toodeploy et exécuter un exemple d’application sur framboises Pi 3 qui envoie des messages tooyour IoT hub. Si vous rencontrez des problèmes, recherchez des solutions sur hello [page Résolution des problèmes](iot-hub-raspberry-pi-kit-node-troubleshooting.md).

## <a name="what-you-will-learn"></a>Contenu
Vous allez apprendre comment toouse hello gulp outil toodeploy et exécuter l’exemple d’application de Node.js hello sur Pi.

## <a name="what-you-need"></a>Ce dont vous avez besoin
* Avant de commencer cette tâche, vous devez avoir terminé avec succès [créer une application de la fonction Azure et un stockage compte tooprocess et magasin IoT hub messages](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md).

## <a name="get-your-iot-hub-and-device-connection-strings"></a>Obtenir vos chaînes de connexion d’IoT Hub et d’appareil
chaîne de connexion de périphérique Hello est utilisé par votre concentrateur de Pi tooconnect tooyour IoT. Hello chaîne de connexion de hub IoT est un registre des identités toohello tooconnect utilisés dans vos appareils IoT hub toomanage hello autorisées tooconnect tooyour IoT hub. 

* Liste de tous vos hubs IoT dans votre groupe de ressources en exécutant hello suivant commande CLI d’Azure :

```bash
az iot hub list -g iot-sample --query [].name
```

Utilisez `iot-sample` en tant que valeur hello `{resource group name}` si vous n’avez modifié la valeur de hello.

* Obtenir la chaîne de connexion de hub IoT hello en exécutant hello suivant commande CLI d’Azure :

```bash
az iot hub show-connection-string --name {my hub name} -g iot-sample
```

`{my hub name}`est le nom hello que vous avez spécifié lorsque vous créez votre hub IoT et inscrit Pi.

* Obtenir la chaîne de connexion de périphérique de hello en exécutant hello de commande suivante :

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id myraspberrypi -g iot-sample
```

Utilisez `myraspberrypi` en tant que valeur hello `{device id}` si vous n’avez modifié la valeur de hello.

## <a name="configure-hello-device-connection"></a>Configurer la connexion du périphérique hello
1. Initialisation du fichier de configuration de hello en hello suivant les commandes en cours d’exécution :
   
   ```bash
   npm install
   gulp init
   ```
2. Fichier de configuration de périphérique ouvert hello `config-raspberrypi.json` dans le Code de Visual Studio en exécutant hello de commande suivante :
   
   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-raspberrypi.json
  
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-raspberrypi.json
   ```
  
   ![config.json](media/iot-hub-raspberry-pi-lessons/lesson3/config.png)
3. Rendre hello suivant remplacements Bonjour `config-raspberrypi.json` fichier :
   
   * Remplacez **[nom d’hôte du périphérique ou adresse IP]** avec hello appareil IP adresse ou nom d’hôte que vous avez obtenu à partir de `device-discovery-cli` ou avec la valeur hello héritée lors de la configuration de votre appareil.
   * Remplacez **[chaîne de connexion de périphérique IoT]** avec hello `device connection string` obtenues.
   * Remplacez **[chaîne de connexion de hub IoT]** avec hello `iot hub connection string` obtenues.

Hello de mise à jour `config-raspberrypi.json` de fichiers afin que vous pouvez déployer des hello exemple d’application à partir de votre ordinateur.

## <a name="deploy-and-run-hello-sample-application"></a>Déployer et exécuter l’exemple d’application hello
Déployer et exécuter l’exemple d’application hello sur Pi en exécutant hello de commande suivante :

```bash
gulp deploy && gulp run
```

## <a name="verify-that-hello-sample-application-works"></a>Vérifiez que hello exemple application fonctionne
Vous devez voir hello DEL qui est connecté tooPi clignote toutes les deux secondes. Chaque fois que hello LED clignote, exemple d’application hello envoie un hub IoT de tooyour message et vérifie que ce message de type hello a été envoyé avec succès tooyour IoT hub. En outre, chaque message reçu par IoT hub de hello est imprimé dans la fenêtre de console hello. exemple d’application Hello se termine automatiquement après l’envoi des messages de 20.

![Exemple d’application avec des messages envoyés et reçus](media/iot-hub-raspberry-pi-lessons/lesson3/gulp_run.png)

## <a name="summary"></a>Résumé
Vous avez déployé et exécuter hello nouvelle blink exemple d’application sur le hub IoT tooyour Pi toosend messages appareil-à-cloud. Vous pouvez désormais surveiller vos messages qu’ils sont écrits de compte de stockage toohello.

## <a name="next-steps"></a>Étapes suivantes
[Lecture des messages conservés dans le Stockage Azure](iot-hub-raspberry-pi-kit-node-lesson3-read-table-storage.md)

