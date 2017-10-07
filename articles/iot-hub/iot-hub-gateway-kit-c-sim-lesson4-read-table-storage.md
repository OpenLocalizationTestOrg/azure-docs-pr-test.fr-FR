---
title: "Appareil simulé et passerelle Azure IoT - Leçon 4 : Stockage de table | Microsoft Docs"
description: "Enregistrer des messages à partir de hub IoT de tooyour Intel NUC, notez-les tooAzure le stockage de Table et puis de les lire à partir du cloud de hello."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "récupérer des données du cloud, service cloud iot"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 78e4b6ea-968d-401e-a7dc-8f9acdb3ec1a
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 43e299d63bbbe10d4d867af25e700c3a7cc07c53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="read-messages-persisted-in-azure-table-storage"></a>Lire des messages conservés dans le stockage Table Azure

## <a name="what-you-will-do"></a>Procédure à suivre

- Exécutez hello passerelle exemple d’application sur votre passerelle qui envoie l’IoT hub tooyour de messages.
- Exécutez l’exemple de code sur votre hôte ordinateur tooread les messages dans votre stockage de Table Azure.

Si vous rencontrez des problèmes, recherchez des solutions sur hello [page Résolution des problèmes](iot-hub-gateway-kit-c-sim-troubleshooting.md).

## <a name="what-you-will-learn"></a>Contenu

Comment toouse hello gulp outil toorun hello exemples code tooread de messages dans votre stockage de Table Azure.

## <a name="what-you-need"></a>Ce dont vous avez besoin

Vous avez correctement hello tâche suivantes :

- [Créé une application de fonction Azure hello et compte de stockage Azure hello](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md).
- [Exécuter l’application d’exemple hello passerelle](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md).
- [lire des messages à partir de votre IoT Hub](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md).

## <a name="get-your-azure-storage-connection-strings"></a>Obtenir vos chaînes de connexion de stockage Azure

Au début de cette leçon, vous avez créé un compte de stockage Azure. chaîne de connexion tooget hello hello Azure du compte de stockage, exécutez hello suivant de commandes :

* Répertoriez tous vos comptes de stockage.

```bash
az storage account list -g iot-gateway --query [].name
```

* Obtenez la chaîne de connexion de stockage Azure.

```bash
az storage account show-connection-string -g iot-gateway -n {storage name}
```

Utilisez `iot-gateway` en tant que valeur hello `{resource group name}` si vous n’avez pas modifier la valeur hello dans la leçon 2.

## <a name="configure-hello-device-connection"></a>Configurer la connexion du périphérique hello

Hello de mise à jour `config-azure.json` fichiers afin que les exemples de code hello qui s’exécute sur l’ordinateur hôte hello peut lire le message dans votre stockage de Table Azure. tooconfigure hello connexion du périphérique, procédez comme suit :

1. Fichier de configuration de périphérique ouvert hello `config-azure.json` par hello suivant les commandes en cours d’exécution :

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-azure.json
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-azure.json
   ```

   ![configuration](media/iot-hub-gateway-kit-lessons/lesson4/config_azure.png)

2. Remplacez `[Azure storage connection string]` par hello chaîne de connexion de stockage Azure que vous avez obtenu.

   `[IoT hub connection string]` doit déjà être remplacé dans la section [Lire des messages à partir d’Azure IoT Hub](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md) de la leçon 3.

## <a name="read-messages-in-your-azure-table-storage"></a>Lire des messages dans votre stockage Table Azure

Exécuter l’application d’exemple hello passerelle et lire les messages de stockage Azure Table par hello de commande suivante :

```bash
gulp run --table-storage
```

Votre hub IoT déclenche votre message toosave d’application Azure fonction dans votre stockage de Table Azure quand le nouveau message arrive.
Hello `gulp run` commande exécute l’exemple d’application passerelle envoie IoT hub tooyour de messages. Avec `table-storage` paramètre, il génère également un Bonjour tooreceive de processus enfant enregistré des messages dans votre stockage de Table Azure.

messages de type Hello qui sont envoyés et reçus sont tous les hello afficher instantanément à même de fenêtre dans la console hello machine hôte. instance de l’application exemple Hello se termine automatiquement au bout de 40 secondes.

   ![lecture de gulp](media/iot-hub-gateway-kit-lessons/lesson4/gulp_run_read_table_simudev.png)


## <a name="summary"></a>Résumé

Vous avez exécuté des messages hello tooread de code d’exemple hello dans votre stockage de Table Azure enregistré par votre application Azure (fonction).
