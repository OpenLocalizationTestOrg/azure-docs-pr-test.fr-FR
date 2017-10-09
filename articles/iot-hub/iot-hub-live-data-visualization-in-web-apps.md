---
title: "visualisation aaaReal au moment des données de capteur à partir de votre concentrateur Azure IoT – applications Web | Documents Microsoft"
description: "Utilisez la fonctionnalité de Web Apps de hello de Microsoft Azure App Service toovisualize température et humidité données sont collectées à partir de capteur de hello et envoyées tooyour Iot hub."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "visualisation de données en temps réel, visualisation de données en direct, visualisation de données de capteurs"
ms.assetid: e42b07a8-ddd4-476e-9bfb-903d6b033e91
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/16/2017
ms.author: xshi
ms.openlocfilehash: 72f2dffee1c2f975948820eee9f2e287c3f77255
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-real-time-sensor-data-from-your-azure-iot-hub-by-using-hello-web-apps-feature-of-azure-app-service"></a>Visualiser les données de capteur en temps réel à partir de votre concentrateur Azure IoT par à l’aide de la fonctionnalité d’applications Web hello du Service d’applications Azure

![Diagramme de bout en bout](media/iot-hub-get-started-e2e-diagram/5.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

## <a name="what-you-learn"></a>Contenu

Dans ce didacticiel, vous découvrez comment les données de capteur en temps réel de toovisualize votre hub IoT reçoit en exécutant une application web qui sont hébergées sur une application web. Si vous souhaitez que les données de salutation toovisualize tootry dans votre IoT hub à l’aide de Power BI, consultez [données de capteur en temps réel toovisualize utiliser Power BI à partir d’Azure IoT Hub](iot-hub-live-data-visualization-in-power-bi.md).

## <a name="what-you-do"></a>Procédure

- Bonjour portail Azure, créez une application web.
- Préparez votre instance IoT Hub pour l’accès aux données via l’ajout d’un groupe de consommateurs.
- Configurer les données de capteur hello web application tooread à partir de votre hub IoT.
- Télécharger un toobe d’application web hébergée par l’application web hello.
- Ouvrez hello web toosee en temps réel température et humidité données d’application à partir de votre hub IoT.

## <a name="what-you-need"></a>Ce dont vous avez besoin

- [Configurer votre périphérique](iot-hub-raspberry-pi-kit-node-get-started.md), qui couvre hello suivant les exigences :
  - Un abonnement Azure actif
  - Un IoT Hub associé à votre abonnement
  - Une application cliente qui envoie l’Iot hub tooyour de messages
- [Télécharger Git](https://www.git-scm.com/downloads)

## <a name="create-a-web-app"></a>Créer une application web

1. Bonjour [portail Azure](https://ms.portal.azure.com/), cliquez sur **nouveau** > **Web + Mobile** > **application Web**.
2. Entrez un nom unique de la tâche, vérifier hello abonnement, spécifiez un groupe de ressources et un emplacement, sélectionnez **code confidentiel toodashboard**, puis cliquez sur **créer**.

   Nous vous recommandons de sélectionner hello même emplacement que celui de votre groupe de ressources. Cela aide à la vitesse de traitement et réduit le coût de hello de transfert de données.

   ![Créer une application web](media/iot-hub-live-data-visualization-in-web-apps/2_create-web-app-azure.png)

[!INCLUDE [iot-hub-get-started-create-consumer-group](../../includes/iot-hub-get-started-create-consumer-group.md)]

## <a name="configure-hello-web-app-tooread-data-from-your-iot-hub"></a>Configurer application web hello tooread des données à partir de votre hub IoT

1. Ouvrez hello uniquement, vous avez configuré l’application web.
2. Cliquez sur **paramètres de l’Application**, puis, sous **paramètres de l’application**, ajouter hello suivant des paires clé/valeur :

   | Clé                                   | Valeur                                                        |
   |---------------------------------------|--------------------------------------------------------------|
   | Azure.IoT.IoTHub.ConnectionString     | Obtenu à partir de iothub-explorer                                |
   | Azure.IoT.IoTHub.ConsumerGroup        | nom de Hello du groupe de consommateurs hello que vous ajoutez tooyour IoT hub  |

   ![Ajouter des paramètres tooyour web application avec des paires clé/valeur](media/iot-hub-live-data-visualization-in-web-apps/4_web-app-settings-key-value-azure.png)

3. Cliquez sur **paramètres de l’Application**, sous **paramètres généraux**, hello de bascule **WebSockets** option, puis cliquez sur **enregistrer**.

   ![Basculer hello Web sockets (option)](media/iot-hub-live-data-visualization-in-web-apps/10_toggle_web_sockets.png)

## <a name="upload-a-web-application-toobe-hosted-by-hello-web-app"></a>Télécharger un toobe d’application web hébergée par l’application web hello

Sur GitHub, nous avons mis à disposition une application web qui affiche des données de capteur en temps réel à partir de votre IoT Hub. Vous devez toodo est configurer hello web application toowork avec un référentiel Git, télécharger des hello d’application web à partir de GitHub et téléchargez-le tooAzure pour hello web application toohost.

1. Dans l’application web de hello, cliquez sur **Options de déploiement** > **choisir la Source de** > **référentiel Git Local**, puis cliquez sur **OK**.

   ![Configurer votre web application déploiement toouse hello référentiel Git local](media/iot-hub-live-data-visualization-in-web-apps/5_configure-web-app-deployment-local-git-repository-azure.png)

2. Cliquez sur **informations d’identification de déploiement**, créez un utilisateur et mot de passe toouse tooconnect toohello référentiel Git dans Azure, puis cliquez sur **enregistrer**.

3. Cliquez sur **vue d’ensemble**et notez la valeur hello **url de clone Git**.

   ![Obtenir l’URL de clone Git hello de votre application web](media/iot-hub-live-data-visualization-in-web-apps/7_web-app-git-clone-url-azure.png)

4. Ouvrez une commande ou une fenêtre de terminal sur votre ordinateur local.

5. Télécharger l’application hello web à partir de GitHub et télécharger tooAzure pour hello web application toohost. toodo, c’est le cas, exécutez hello commandes suivantes :

   ```bash
   git clone https://github.com/Azure-Samples/web-apps-node-iot-hub-data-visualization.git
   cd web-apps-node-iot-hub-data-visualization
   git remote add webapp <Git clone URL>
   git push webapp master:master
   ```

   > [!NOTE]
   > \<URL de clone GIT\> URL hello du référentiel Git de hello trouvé sur hello **vue d’ensemble** page de l’application web hello.

## <a name="open-hello-web-app-toosee-real-time-temperature-and-humidity-data-from-your-iot-hub"></a>Ouvrez hello web toosee en temps réel température et humidité données d’application à partir de votre hub IoT

Sur hello **vue d’ensemble** page de votre application web, cliquez sur l’application web hello URL tooopen hello.

![Obtenir l’URL de hello de votre application web](media/iot-hub-live-data-visualization-in-web-apps/8_web-app-url-azure.png)

Vous devez voir la température en temps réel de hello et les données de l’humidité à partir de votre hub IoT.

![Page d’application web affichant l’humidité et la température en temps réel](media/iot-hub-live-data-visualization-in-web-apps/9_web-app-page-show-real-time-temperature-humidity-azure.png)

> [!NOTE]
> Vérifiez l’application d’exemple hello est en cours d’exécution sur votre appareil. Si non, vous obtenez un graphique vide, vous pouvez consulter des didacticiels toohello sous [configurer votre appareil](iot-hub-raspberry-pi-kit-node-get-started.md).

## <a name="next-steps"></a>Étapes suivantes
Vous avez utilisé avec succès vos données de capteur en temps réel de toovisualize application web à partir de votre hub IoT.

Pour une autre façon toovisualize des données depuis Azure IoT Hub, consultez [données de capteur en temps réel toovisualize utiliser Power BI à partir de votre hub IoT](iot-hub-live-data-visualization-in-power-bi.md).

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
