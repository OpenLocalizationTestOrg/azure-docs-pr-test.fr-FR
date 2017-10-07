---
title: Appareil SensorTag et passerelle Azure IoT - Prise en main | Microsoft Docs
description: "Prise en main IoT passerelle Starter Kit, créez votre hub Azure IoT et connectez SensorTag et passerelle toohello IoT hub"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: Azure iot hub, passerelle iot, prise en main de hello internet des objets, iot toolkit
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 56d05f4e-f2c1-4b22-8701-f01e14deead6
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: d8e4057e7774e43c069dd3f2f2e03f098c1ac844
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-iot-gateway-starter-kit-with-a-sensortag"></a>Prise en main du Kit de démarrage de la passerelle IoT avec un SensorTag

> [!div class="op_single_selector"]
> * [SensorTag](iot-hub-gateway-kit-c-get-started.md)
> * [Appareil simulé](iot-hub-gateway-kit-c-sim-get-started.md)

Dans ce didacticiel, commencer par découvrir hello les bases de l’utilisation de [IoT passerelle Starter Kit](https://aka.ms/gateway-kit). Vous allez travailler avec NUC Intel qui exécute Linux de vent district et hello [TI SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/index.html#main). Vous allez apprendre comment tooseamleesly connecter votre cloud toohello de périphériques à l’aide d’Azure IoT Hub.

***
**Vous n’avez pas encore de kit ?** Cliquez [ici](https://aka.ms/gateway-kit). **Vous n’avez pas de SensorTag ?**[Commencez avec un appareil simulé](iot-hub-gateway-kit-c-sim-get-started.md) ou [achetez un SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/?INTC=SensorTag&HQS=sensortag)
***

## <a name="lesson-1-configure-your-nuc"></a>Leçon 1 : Configuration de votre NUC
![Diagramme de bout en bout pour la leçon 1](media/iot-hub-gateway-kit-lessons/e2e-lesson1.png)

Dans cette leçon, vous pouvez paramétrer des NUC Intel (suivant unité de calcul) Bonjour Kit comme passerelle Azure IoT, hello Azure IoT bord installer sur NUC et exécuter une fonctionnalité de passerelle exemple application tooverify hello.

*Estimation du temps toocomplete : 15 minutes*

Accédez trop[configurer NUC Intel comme passerelle IoT](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)

## <a name="lesson-2-create-your-iot-hub"></a>Leçon 2 : Création de votre IoT Hub
![Diagramme de bout en bout pour la leçon 2](media/iot-hub-gateway-kit-lessons/e2e-lesson2.png)

Dans cette leçon, vous installez les outils de hello et des logiciels sur votre ordinateur hôte. Puis vous créez gratuitement un compte Azure, configurez votre concentrateur Azure IoT et créez votre premier appareil dans le hub IoT de hello.

Avant de commencer cette leçon, terminez la Leçon 1.

### <a name="get-hello-tools"></a>Obtenir les outils de hello
Installez les outils hello et logiciels sur votre ordinateur hôte.

*Estimation du temps toocomplete : 20 minutes*

Accédez trop[obtenir hello tools](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md)

### <a name="create-an-iot-hub-and-register-your-device"></a>Créer un IoT hub et enregistrer votre appareil
Créer votre groupe de ressources et configurer votre concentrateur Azure IoT première ajouter votre premier appareil toohello IoT hub à l’aide de hello CLI d’Azure.

*Estimation du temps toocomplete : 10 minutes*

Accédez trop[créez un IoT hub et inscrire votre appareil](iot-hub-gateway-kit-c-lesson2-register-device.md)

## <a name="lesson-3-receive-messages-from-sensortag-and-read-messages-from-your-iot-hub"></a>Leçon 3 : Recevoir des messages à partir de SensorTag et lire des messages à partir de votre IoT Hub
Dans cette leçon, vous allez utiliser la configuration de scripts tooautomate hello et l’exécution d’un exemple d’application BLE dans votre passerelle. Ces applications utilisent une collection de modules tooaggregate et transformer des données, traitent les commandes ou effectuer des tâches associées. Les modules communiquent entre eux par le bais d’un courtier de messages. exemple d’application Hello a un module d’activer et d’un module de hub IoT. module BLE Hello reçoit les données BLE SensorTag. Bonjour les packages de module de hub IoT les données de salutation reçu et l’envoie tooyour IoT hub via l’infrastructure de passerelle hello fournie dans Azure IoT Edge.

![Diagramme de bout en bout pour la leçon 3](media/iot-hub-gateway-kit-lessons/e2e-lesson3.png)

### <a name="configure-and-run-hello-ble-sample-app"></a>Configurer et exécuter l’application d’exemple hello BLE
Configurer une connectivité hello entre SensorTag et votre passerelle. Terminer la configuration de hello, puis exécutez hello BLE exemple d’application.

*Estimation du temps toocomplete : 15 minutes*

Accédez trop[configurer et l’exécution hello BLE exemple d’application](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md)

### <a name="read-messages-from-your-iot-hub"></a>Lire des messages à partir de votre IoT Hub
Exécutez exemple de code sur votre hôte tooread ordinateur des messages à partir de votre hub IoT.

*Estimation du temps toocomplete : 15 minutes*

Accédez trop[lire les messages de votre hub IoT](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md)

## <a name="lesson-4-save-messages-tooazure-table-storage"></a>Leçon 4 : Enregistrer des messages tooAzure le stockage de Table
Créer une application Azure de fonction qui obtient les messages entrants à partir de votre IoT hub et les écrit tooAzure le stockage de Table.

![Diagramme de bout en bout pour la leçon 4](media/iot-hub-gateway-kit-lessons/e2e-lesson4.png)

### <a name="create-an-azure-function-app-and-azure-storage-account"></a>Création d’une application de fonction Azure et d’un compte de stockage Azure
Utilisez un toocreate de modèle Azure Resource Manager une application Azure (fonction) et un compte de stockage Azure.

*Estimation du temps toocomplete : 10 minutes*

Accédez trop[créer une application de la fonction Azure et d’un compte de stockage Azure](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md)

### <a name="read-messages-persisted-in-azure-table-storage"></a>Lire des messages conservés dans le stockage Table Azure
Surveiller les messages de passerelle dans le cloud hello qu’ils sont écrits tooAzure le stockage de Table.

*Estimation du temps toocomplete : 5 minutes*

Accédez trop[lire les messages conservés dans le stockage Azure Table](iot-hub-gateway-kit-c-lesson4-read-table-storage.md).

## <a name="troubleshooting"></a>Résolution des problèmes
Si vous rencontrez des problèmes au cours des leçons de hello, rechercher des solutions dans hello [dépannage](iot-hub-gateway-kit-c-troubleshooting.md) l’article.

## <a name="explore-more"></a>Aller plus loin
Visitez hello [zone pour développeurs Intel IoT passerelle Kit](http://software.intel.com/iot/microsoft-azure) toolearn plus.
