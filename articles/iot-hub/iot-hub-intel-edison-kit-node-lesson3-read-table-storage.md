---
title: "Se connecter tooAzure Intel Edison (nœud) IoT - leçon 3 : surveiller les messages | Documents Microsoft"
description: "Surveiller les messages appareil-à-cloud hello qu’ils sont écrits de stockage de Table Azure tooyour."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "données dans le cloud de hello, collecte de données de cloud, le service cloud iot, iot données"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: fa2c7efe-7e34-4e39-bb70-015c15ac69ed
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 8f6371482123bc9aa12db55b38d3e8863645f981
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="read-messages-persisted-in-azure-storage"></a>Lecture des messages conservés dans le stockage Azure
## <a name="what-you-will-do"></a>Procédure à suivre
Moniteur hello appareil-à-cloud les messages sont envoyés à partir de hub IoT de tooyour Intel Edison en tant que messages hello sont écrits tooyour stockage de Table Azure. Si vous rencontrez des problèmes, recherchez des solutions sur hello [page Résolution des problèmes][troubleshooting].

## <a name="what-you-will-learn"></a>Contenu
Dans cet article, vous allez apprendre le mode de conservation des messages de tooread toouse hello gulp tâche de lecture du message dans votre stockage de Table Azure.

## <a name="what-you-need"></a>Ce dont vous avez besoin
Avant de commencer ce processus, vous devez avoir terminé avec succès [exécuter hello blink Azure exemple d’application sur Intel Edison][run-the-azure-blink-sample-application-on-intel-edison].

## <a name="read-new-messages-from-your-storage-account"></a>Lecture des nouveaux messages à partir de votre compte de stockage
Dans l’article précédent de hello, vous avez exécuté un exemple d’application sur Edison. exemple d’application Hello envoyé concentrateur de messages tooyour Azure IoT. messages d’appel envoyés tooyour IoT hub sont stockés dans votre stockage de Table Azure via l’application de fonction Azure hello. Vous devez les messages tooread chaîne hello stockage Azure connexion à partir de votre stockage de Table Azure.

les messages tooread stockés dans votre stockage de Table Azure, procédez comme suit :

1. Obtenir la chaîne de connexion hello en exécutant hello suivant les commandes :

   ```bash
   az storage account list -g iot-sample --query [].name
   az storage account show-connection-string -g iot-sample -n {storage name}
   ```

   Hello première commande extrait hello `storage name` qui est utilisée dans la chaîne de connexion hello deuxième commande tooget hello. Utilisez `iot-sample` en tant que valeur hello `{resource group name}` si vous n’avez modifié la valeur de hello.
2. Fichier de configuration Open hello `config-edison.json` dans le Code de Visual Studio en exécutant hello de commande suivante :

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-edison.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-edison.json
   ```
3. Remplacez `[Azure storage connection string]` avec la chaîne de connexion hello que vous avez obtenu à l’étape 1.
4. Enregistrer hello `config-edison.json` fichier.
5. Envoyer des messages à nouveau et les lire à partir de votre stockage de Table Azure en exécutant hello de commande suivante :

   ```bash
   gulp run --read-storage
   ```

   Bonjour logique pour la lecture à partir du stockage de Table Azure est Bonjour `azure-table.js` fichier.

   ![exécutez gulp --lire-stockage][gulp run]

## <a name="summary"></a>Résumé
Vous avez correctement connecté hub IoT Edison tooyour cloud de hello et utilisé hello blink exemples application toosend appareil-à-cloud de messages. Vous avez également utilisé hello fonction Azure application toostore entrant IoT hub messages tooyour stockage de Table Azure. Vous pouvez maintenant envoyer des messages cloud-à-appareil de votre tooEdison de hub IoT.

## <a name="next-steps"></a>Étapes suivantes
[Exécuter un tooreceive d’application exemple messages cloud-à-appareil][receive-cloud-to-device-messages]
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[run-the-azure-blink-sample-application-on-intel-edison]: iot-hub-intel-edison-kit-node-lesson3-run-azure-blink.md
[gulp run]: media/iot-hub-intel-edison-lessons/lesson3/gulp_read_message.png
[receive-cloud-to-device-messages]: iot-hub-intel-edison-kit-node-lesson4-send-cloud-to-device-messages.md