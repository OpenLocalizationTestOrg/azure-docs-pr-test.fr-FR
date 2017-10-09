---
title: "Se connecter tooAzure Intel Edison (nœud) IoT - leçon 3 : envoyer des messages | Documents Microsoft"
description: "Déployer et exécuter un tooIntel d’application exemple Edison qui envoie l’IoT hub tooyour de messages et clignote hello DEL."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "service de cloud IOT, arduino envoyer des données toocloud"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: 1b3b1074-f4d4-42ac-b32c-55f18b304b44
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: ebd4c7558544d64086fb4cd615cee546aeed2fc1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-toosend-device-to-cloud-messages"></a>Exécuter un toosend d’application exemple messages appareil-à-cloud
## <a name="what-you-will-do"></a>Procédure à suivre
Cet article vous explique comment toodeploy et exécuter un exemple d’application sur Edison Intel qui envoie des messages tooyour IoT hub. Si vous rencontrez des problèmes, recherchez des solutions sur hello [page Résolution des problèmes][troubleshooting].

## <a name="what-you-will-learn"></a>Contenu
Vous découvrez comment toouse hello gulp outil toodeploy et exécuter l’exemple d’application de C hello sur Edison.

## <a name="what-you-need"></a>Ce dont vous avez besoin
* Avant de commencer cette tâche, vous devez avoir terminé avec succès [créer une application de la fonction Azure et un stockage compte tooprocess et magasin IoT hub messages][process-and-store-iot-hub-messages].

## <a name="get-your-iot-hub-and-device-connection-strings"></a>Obtenir vos chaînes de connexion d’IoT Hub et d’appareil
chaîne de connexion de périphérique Hello est utilisé tooconnect hub IoT de tooyour Edison. Hello la chaîne de connexion de hub IoT est tooconnect utilisé votre identité d’appareil IoT hub toohello représentant Edison dans le hub IoT de hello.

* Liste de tous vos hubs IoT dans votre groupe de ressources en exécutant hello suivant commande CLI d’Azure :

```bash
az iot hub list -g iot-sample --query [].name
```

Utilisez `iot-sample` en tant que valeur hello `{resource group name}` si vous n’avez modifié la valeur de hello.

* Obtenir la chaîne de connexion de hub IoT hello en exécutant hello suivant commande CLI d’Azure :

```bash
az iot hub show-connection-string --name {my hub name}
```

`{my hub name}`est le nom hello que vous avez spécifié lorsque vous créez votre hub IoT et inscrit Edison.

* Obtenir la chaîne de connexion de périphérique de hello en exécutant hello de commande suivante :

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id myinteledison
```

Utilisez `myinteledison` en tant que valeur hello `{device id}` si vous n’avez modifié la valeur de hello.

## <a name="configure-hello-device-connection"></a>Configurer la connexion du périphérique hello
1. Initialisation du fichier de configuration de hello en hello suivant les commandes en cours d’exécution :

   ```bash
   npm install
   gulp init
   ```

2. Fichier de configuration de périphérique ouvert hello `config-edison.json` dans le Code de Visual Studio en exécutant hello de commande suivante :

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-edison.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-edison.json
   ```

   ![config.json](media/iot-hub-intel-edison-lessons/lesson3/config.png)
3. Rendre hello suivant remplacements Bonjour `config-edison.json` fichier :

   * Remplacez **[nom d’hôte du périphérique ou adresse IP]** avec l’adresse IP du périphérique hello démarquer lorsque vous avez configuré votre appareil.
   * Remplacez **[chaîne de connexion de périphérique IoT]** avec hello `device connection string` obtenues.
   * Remplacez **[chaîne de connexion de hub IoT]** avec hello `iot hub connection string` obtenues.

   > [!NOTE]
   > Vous n’avez pas besoin de `azure_storage_connection_string` dans cet article. Gardez-le tel quel.

## <a name="deploy-and-run-hello-sample-application"></a>Déployer et exécuter l’exemple d’application hello
Déployer et exécuter l’exemple d’application hello sur Edison en exécutant hello de commande suivante :

```bash
gulp deploy && gulp run
```

## <a name="verify-that-hello-sample-application-works"></a>Vérifiez que hello exemple application fonctionne
Vous devez voir hello DEL qui est connecté tooEdison clignote toutes les deux secondes. Chaque fois que hello LED clignote, exemple d’application hello envoie un hub IoT de tooyour message et vérifie que ce message de type hello a été envoyé avec succès tooyour IoT hub. En outre, chaque message reçu par IoT hub de hello est imprimé dans la fenêtre de console hello. exemple d’application Hello se termine automatiquement après l’envoi des messages de 20.

![Exemple d’application avec des messages envoyés et reçus][sample-application-with-sent-and-received-messages]

## <a name="summary"></a>Résumé
Vous avez déployé et exécuté de hello nouvelle blink exemple d’application sur Edison tooyour IoT hub toosend messages appareil-à-cloud. Vous surveillez maintenant vos messages qu’ils sont écrits de compte de stockage toohello.

## <a name="next-steps"></a>Étapes suivantes
[Lecture des messages conservés dans le stockage Azure][read-messages-persisted-in-azure-storage]
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-intel-edison-kit-node-lesson3-deploy-resource-manager-template.md
[sample-application-with-sent-and-received-messages]: media/iot-hub-intel-edison-lessons/lesson3/gulp_run.png
[read-messages-persisted-in-azure-storage]: iot-hub-intel-edison-kit-node-lesson3-read-table-storage.md