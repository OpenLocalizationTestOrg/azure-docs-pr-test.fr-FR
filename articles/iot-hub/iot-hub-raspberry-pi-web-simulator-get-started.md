---
title: toocloud aaaSimulated framboises Pi (Node.js) - simulateur tooAzure IoT Hub de connecter un Pi framboises web | Documents Microsoft
description: "Se connecter framboises Pi web simulateur tooAzure IoT Hub pour framboises Pi toosend données toohello cloud Azure."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "pi raspberry Raspberry pi simulateur, azure raspberry pi, raspberry pi iot hub iot, envoyer des données toocloud, raspberry pi toocloud"
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 7/28/2017
ms.author: xshi
ms.openlocfilehash: 83736caf6ce723a49001058495a780f7f51946a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-raspberry-pi-online-simulator-tooazure-iot-hub-nodejs"></a>Se connecter framboises Pi en ligne simulateur tooAzure IoT Hub (Node.js)

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

Dans ce didacticiel, commencer par découvrir hello les bases de l’utilisation de simulateur en ligne de framboises Pi. Vous apprendrez ensuite comment tooseamlessly connecter le cloud de toohello hello Pi simulateur à l’aide de [Azure IoT Hub](iot-hub-what-is-iot-hub.md). 

Si vous avez des périphériques physiques, visitez [tooAzure de connecter un Pi framboises IoT Hub](iot-hub-raspberry-pi-kit-node-get-started.md) tooget a démarré. 

<p>
<div id="diag" style="width:100%; text-align:center">
<a href="https://azure-samples.github.io/raspberry-pi-web-simulator/#getstarted" target="_blank">
<img src="media/iot-hub-raspberry-pi-web-simulator/3_banner.png" alt="Connect Raspberry Pi web simulator tooAzure IoT Hub" width="400">
</div>
<p>
<div id="button" style="width:100%; text-align:center">
<a href="https://azure-samples.github.io/raspberry-pi-web-simulator/#Getstarted" target="_blank">
<img src="media/iot-hub-raspberry-pi-web-simulator/6_button_default.png" alt="Start Raspberry Pi simulator" width="400" onmouseover="this.src='media/iot-hub-raspberry-pi-web-simulator/5_button_click.png';" onmouseout="this.src='media/iot-hub-raspberry-pi-web-simulator/6_button_default.png';">
</div>

## <a name="what-you-do"></a>Procédure

* Découvrez les principes de base de hello du simulateur en ligne de framboises Pi.
* Créez un hub IoT.
* Inscrivez un appareil pour Pi dans votre IoT Hub.
* Exécuter un exemple d’application sur Pi toosend simulée capteur données tooyour IoT hub.

Se connecter simulé framboises Pi tooan IoT hub que vous créez. Puis, vous exécutez un exemple d’application avec des données de capteur toogenerate hello simulateur. Enfin, vous envoyez le hub IoT tooyour hello capteur données.

## <a name="what-you-learn"></a>Contenu

* Comment toocreate un Azure IoT hub et obtenir votre nouvelle chaîne de connexion de périphérique. Si vous ne possédez pas de compte Azure, vous pouvez [créer un compte d’évaluation Azure gratuit](https://azure.microsoft.com/free/) en quelques minutes.
* Comment toowork au Simulateur framboises Pi en ligne.
* Comment le hub IoT tooyour toosend capteur données.

## <a name="overview-of-raspberry-pi-web-simulator"></a>Vue d’ensemble du simulateur web Raspberry Pi

Cliquez sur le simulateur en ligne de hello bouton toolaunch framboises Pi.

> [!div class="button"]
<a href="https://azure-samples.github.io/raspberry-pi-web-simulator/#GetStarted" target="_blank">Démarrer le simulateur Raspberry Pi</a>

Il existe trois domaines dans le simulateur de web hello.
1. Zone d’assemblage - hello par défaut est qu’un Pi se connecte avec un capteur BME280 et une DEL. zone de Hello est verrouillée dans la version d’évaluation donc actuellement, vous ne pouvez pas faire personnalisation.
2. Codage zone - un éditeur de code en ligne pour vous toocode avec framboises Pi. application d’exemple Hello par défaut permet de données de capteur toocollect BME280 capteur et envoie tooyour Azure IoT Hub. application Hello est entièrement compatible avec les appareils Pi réels. 
3. Fenêtre de console intégrée - il montre sortie hello de votre code. Hello en haut de cette fenêtre, il existe trois boutons.
   * **Exécutez** -exécuter l’application hello Bonjour zone de codage.
   * **Réinitialiser** -hello réinitialisation exemple d’application de zone toohello par défaut de codage.
   * **Pli/développement** - sur hello droite côté il existe un bouton pour vous toofold/développement hello fenêtre de console.

> [!NOTE] 
Simulateur de web Pi de framboises Hello est désormais disponible en version préliminaire. Nous aimerions toohear votre voix Bonjour [Gitter un accroissement](https://gitter.im/Microsoft/raspberry-pi-web-simulator). code source de Hello est public sur [Github](https://github.com/Azure-Samples/raspberry-pi-web-simulator).

![Vue d’ensemble du simulateur en ligne Pi](media/iot-hub-raspberry-pi-web-simulator/0_overview.png)

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]


## <a name="run-a-sample-application-on-pi-web-simulator"></a>Exécuter un exemple d’application sur le simulateur web Pi

1. Dans la zone de codage, assurez-vous que vous travaillez sur l’application d’exemple hello par défaut. Remplacez espace réservé de hello dans la ligne 15 hello chaîne de connexion de périphérique Azure IoT hub.
   ![Remplacez la chaîne de connexion de périphérique hello](media/iot-hub-raspberry-pi-web-simulator/1_connectionstring.png)

2. Cliquez sur **exécuter** ou type `npm start` application hello de toorun.


Vous devez voir hello suivant de sortie qui affiche les données de capteur hello et messages hello envoyés tooyour IoT hub ![sortie - données de capteur envoyés à partir de hub IoT de tooyour framboises Pi](media/iot-hub-raspberry-pi-web-simulator/2_run_application.png)


## <a name="next-steps"></a>Étapes suivantes

Vous avez exécuté un exemple de données de capteur application toocollect et envoyez tooyour IoT hub.

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
