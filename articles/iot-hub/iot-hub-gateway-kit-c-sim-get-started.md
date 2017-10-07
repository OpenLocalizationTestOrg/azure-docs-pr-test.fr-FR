---
title: "Appareil simulé et passerelle Azure IoT - Prise en main | Microsoft Docs"
description: "Prise en main IoT passerelle Starter Kit, créez votre hub Azure IoT et connectez IoT hub toohello de passerelle"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: Azure iot hub, passerelle iot, prise en main de hello internet des objets, iot toolkit
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 0c110b8b-bee4-4aec-a18a-dfc292aa17a3
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 1a54a5e5f1c1d9b2e657c9e4448274256e2533f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-iot-gateway-starter-kit-with-a-simulated-device"></a>Prise en main du Kit de démarrage de la passerelle IoT avec un appareil simulé

> [!div class="op_single_selector"]
> * [SensorTag](iot-hub-gateway-kit-c-get-started.md)
> * [Appareil simulé](iot-hub-gateway-kit-c-sim-get-started.md)

Dans ce didacticiel, commencer par découvrir hello les bases de l’utilisation de [IoT passerelle Starter Kit](https://aka.ms/gateway-kit). Vous allez travailler avec Intel NUC exécutant Wind River Linux. Vous allez apprendre comment tooseamleesly connecter votre cloud toohello de périphériques à l’aide d’Azure IoT Hub.

***
**Vous n’avez pas encore de kit ?** Cliquez [ici](https://aka.ms/gateway-kit).
***

## <a name="lesson-1-configure-your-nuc"></a>Leçon 1 : Configuration de votre NUC
![Diagramme de bout en bout pour la leçon 1](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson1.png)

Dans cette leçon, vous pouvez paramétrer des NUC Intel (suivant unité de calcul) Bonjour Kit comme passerelle Azure IoT, hello Azure IoT bord installer sur NUC et exécuter une fonctionnalité de passerelle exemple application tooverify hello.

*Estimation du temps toocomplete : 15 minutes*

Accédez trop[configurer NUC Intel comme passerelle IoT](iot-hub-gateway-kit-c-sim-lesson1-set-up-nuc.md)

## <a name="lesson-2-create-your-iot-hub"></a>Leçon 2 : Création de votre IoT Hub
![Diagramme de bout en bout pour la leçon 2](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson2.png)

Dans cette leçon, vous installez les outils de hello et des logiciels sur votre ordinateur hôte. Puis vous créez gratuitement un compte Azure, configurez votre concentrateur Azure IoT et créez votre premier appareil dans le hub IoT de hello.

Avant de commencer cette leçon, terminez la Leçon 1.

### <a name="get-hello-tools"></a>Obtenir les outils de hello
Installez les outils hello et logiciels sur votre ordinateur hôte.

*Estimation du temps toocomplete : 20 minutes*

Accédez trop[obtenir hello tools](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)

### <a name="create-an-iot-hub-and-register-your-device"></a>Créer un IoT hub et enregistrer votre appareil
Créer votre groupe de ressources et configurer votre concentrateur Azure IoT première ajouter votre premier appareil toohello IoT hub à l’aide de hello CLI d’Azure.

*Estimation du temps toocomplete : 10 minutes*

Accédez trop[créez un IoT hub et inscrire votre appareil](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)

## <a name="lesson-3-receive-messages-from-hello-simulated-device-and-read-messages-from-your-iot-hub"></a>Leçon 3 : Recevoir des messages à partir de l’appareil simulé de hello et lire des messages à partir de votre hub IoT
Dans cette leçon, vous allez utiliser la configuration de scripts tooautomate hello et l’exécution d’une application d’appareil simulé dans votre passerelle. application d’appareil simulé Hello génère les exemples de données de température et il envoie le module de hub IoT tooan. Bonjour les packages de module de hub IoT les données de salutation reçu et l’envoie tooyour IoT hub via l’infrastructure de passerelle hello fournie dans Azure IoT Edge.

![Diagramme de bout en bout pour la leçon 3](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson3.png)

### <a name="configure-and-run-a-simulated-device"></a>Configurer et exécuter un appareil simulé
Préparer les exemples de code hello. Puis configurez et exécutez hello simulée appareil exemple d’application.

*Estimation du temps toocomplete : 15 minutes*

Accédez trop[configurer et exécuter un appareil simulé](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md)

### <a name="read-messages-from-your-iot-hub"></a>Lire des messages à partir de votre IoT Hub
Exécuter un exemple de code sur votre hôte ordinateur tooread hello des messages à partir de votre hub IoT.

*Estimation du temps toocomplete : 15 minutes*

Accédez trop[lire les messages de votre hub IoT](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md)

## <a name="lesson-4-save-messages-tooazure-table-storage"></a>Leçon 4 : Enregistrer des messages tooAzure le stockage de Table
Créer une application Azure de fonction qui obtient les messages entrants à partir de votre IoT hub et les écrit tooAzure le stockage de Table.

![Diagramme de bout en bout pour la leçon 4](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson4.png)

### <a name="create-an-azure-function-app-and-azure-storage-account"></a>Création d’une application de fonction Azure et d’un compte de stockage Azure
Utilisez un toocreate de modèle Azure Resource Manager une application Azure (fonction) et un compte de stockage Azure.

*Estimation du temps toocomplete : 10 minutes*

Accédez trop[créer une application de la fonction Azure et d’un compte de stockage Azure](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md)

### <a name="read-messages-persisted-in-azure-table-storage"></a>Lire des messages conservés dans le stockage Table Azure
Surveiller les messages de passerelle dans le cloud hello qu’ils sont écrits tooAzure le stockage de Table.

*Estimation du temps toocomplete : 5 minutes*

Accédez trop[lire les messages conservés dans le stockage Azure Table](iot-hub-gateway-kit-c-sim-lesson4-read-table-storage.md).

## <a name="troubleshooting"></a>Résolution des problèmes
Si vous rencontrez des problèmes au cours des leçons de hello, rechercher des solutions dans hello [dépannage](iot-hub-gateway-kit-c-sim-troubleshooting.md) l’article.

## <a name="explore-more"></a>Aller plus loin
Visitez hello [zone pour développeurs Intel IoT passerelle Kit](https://software.intel.com/en-us/iot/hardware/gateways/dev-kit) toolearn plus.
