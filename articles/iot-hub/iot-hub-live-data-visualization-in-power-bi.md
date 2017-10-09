---
title: "temps d’aaaReal visualisation des données de capteur à partir d’Azure IoT Hub – Power BI | Documents Microsoft"
description: "Utilisez les données de température et humidité de toovisualize Power BI qui sont collectées à partir de capteur de hello et envoyées tooyour Azure IoT hub."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "visualisation de données en temps réel, visualisation de données en direct, visualisation de données de capteurs"
ms.assetid: e67c9c09-6219-4f0f-ad42-58edaaa74f61
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: xshi
ms.openlocfilehash: d79ce757a9f2ab7a4744e8a0c523106e0f72cecd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-real-time-sensor-data-from-azure-iot-hub-using-power-bi"></a>Visualiser des données de capteur en temps réel depuis Azure IoT Hub, à l’aide de Power BI

![Diagramme de bout en bout](media/iot-hub-get-started-e2e-diagram/4.png)


[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

## <a name="what-you-learn"></a>Contenu

Vous apprendrez comment les données des capteurs en temps réel toovisualize votre concentrateur Azure IoT reçoit par Power BI. Si vous souhaitez tootry visualiser les données de hello dans votre IoT hub avec des applications Web, consultez [données de capteur en temps réel toovisualize utilisation Azure Web Apps dans Azure IoT Hub](iot-hub-live-data-visualization-in-web-apps.md).

## <a name="what-you-do"></a>Procédure

- Préparez votre instance IoT Hub pour l’accès aux données via l’ajout d’un groupe de consommateurs.
- Créer, configurer et exécuter une tâche de flux de données Analytique pour le transfert de données à partir de votre tooyour de hub IoT compte Power BI.
- Créer et publier des données hello toovisualize d’un rapport Power BI.

## <a name="what-you-need"></a>Ce dont vous avez besoin

- Didacticiel [configurer votre appareil](iot-hub-raspberry-pi-kit-node-get-started.md) terminé qui couvre hello suivant les exigences :
  - Un abonnement Azure actif.
  - Une instance Azure IoT Hub associée à votre abonnement.
  - Une application cliente qui envoie le concentrateur de messages tooyour Azure IoT.
- Un compte Microsoft Power BI. ([Essayez Power BI gratuitement](https://powerbi.microsoft.com/)).

[!INCLUDE [iot-hub-get-started-create-consumer-group](../../includes/iot-hub-get-started-create-consumer-group.md)]

## <a name="create-configure-and-run-a-stream-analytics-job"></a>Créer, configurer et exécuter un travail Stream Analytics

### <a name="create-a-stream-analytics-job"></a>Création d’un travail Stream Analytics

1. Dans l’hello portail Azure, cliquez sur Nouveau > Internet of Things > tâche de flux de données Analytique.
1. Entrez hello informations pour le travail de hello suivantes.

   **Nom de la tâche**: nom hello du travail de hello. nom de Hello doit être globalement unique.

   **Groupe de ressources**: utilisez hello même groupe de ressources qui utilise de votre hub IoT.

   **Emplacement**: utilisez hello même emplacement que votre groupe de ressources.

   **Code confidentiel toodashboard**: Activez cette option pour le hub de IoT tooyour accéder facilement à partir du tableau de bord hello.

   ![Créer un travail Stream Analytics dans Azure](media/iot-hub-live-data-visualization-in-power-bi/2_create-stream-analytics-job-azure.png)

1. Cliquez sur **Créer**.

### <a name="add-an-input-toohello-stream-analytics-job"></a>Ajouter une tâche de flux de données Analytique toohello d’entrée

1. Tâche de flux de données Analytique hello ouvert.
1. Sous **Topologie du travail**, cliquez sur **Entrées**.
1. Bonjour **entrées** volet, cliquez sur **ajouter**, puis entrez hello informations suivantes :

   **Alias d’entrée**: alias unique de hello pour l’entrée de hello.

   **Source** : sélectionnez **IoT Hub**.

   **Groupe de consommateurs**: groupe de consommateurs hello sélectionnez vous venez de créer.
1. Cliquez sur **Créer**.

   ![Ajouter une tâche de flux de données Analytique tooa d’entrée dans Azure](media/iot-hub-live-data-visualization-in-power-bi/3_add-input-to-stream-analytics-job-azure.png)

### <a name="add-an-output-toohello-stream-analytics-job"></a>Ajouter une tâche de flux de données Analytique toohello sortie

1. Sous **Topologie du travail**, cliquez sur **Sorties**.
1. Bonjour **sorties** volet, cliquez sur **ajouter**, puis entrez hello informations suivantes :

   **Alias de sortie**: alias unique de hello pour la sortie de hello.

   **Section sink**: sélectionnez **Power BI**.
1. Cliquez sur **Autoriser**, puis connectez-vous à votre compte Power BI.
1. Une fois autorisé, entrez hello informations suivantes :

   **Espace de travail de groupe** : sélectionnez l’espace de travail de groupe cible.

   **Nom du jeu de données** : saisissez le nom de jeu de données.

   **Nom de la table** : saisissez le nom de la table.
1. Cliquez sur **Créer**.

   ![Ajouter une tâche de flux de données Analytique sortie tooa dans Azure](media/iot-hub-live-data-visualization-in-power-bi/4_add-output-to-stream-analytics-job-azure.png)

### <a name="configure-hello-query-of-hello-stream-analytics-job"></a>Configurer la requête hello de tâche de flux de données Analytique hello

1. Sous **Topologie du travail**, cliquez sur **Requête**.
1. Remplacez `[YourInputAlias]` avec alias hello d’entrée de tâche de hello.
1. Remplacez `[YourOutputAlias]` avec l’alias de sortie hello du travail de hello.
1. Cliquez sur **Enregistrer**.

   ![Ajouter une tâche de flux de données Analytique requête tooa dans Azure](media/iot-hub-live-data-visualization-in-power-bi/5_add-query-stream-analytics-job-azure.png)

### <a name="run-hello-stream-analytics-job"></a>Exécuter la tâche de flux de données Analytique hello

Dans la tâche de flux de données Analytique hello, cliquez sur **Démarrer** > **maintenant** > **Démarrer**. Une fois le travail de hello démarre avec succès, état de la tâche hello passe de **arrêté** trop**en cours d’exécution**.

![Exécuter un travail Stream Analytics dans Azure](media/iot-hub-live-data-visualization-in-power-bi/6_run-stream-analytics-job-azure.png)

## <a name="create-and-publish-a-power-bi-report-toovisualize-hello-data"></a>Créer et publier des données hello toovisualize d’un rapport Power BI

1. Vérifiez l’application d’exemple hello est en cours d’exécution sur votre appareil. Si non, vous pouvez faire référence à des didacticiels toohello sous [configurer votre appareil](https://docs.microsoft.com/azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started).
1. Connectez-vous à tooyour [Power BI](https://powerbi.microsoft.com/en-us/) compte.
1. Atteindre l’espace de travail toohello groupe que vous définissez lors de la création de la sortie de hello pour la tâche de flux de données Analytique hello.
1. Cliquez sur **Jeux de données de diffusion en continu**.

   Vous devez voir hello répertorié de jeu de données que vous avez spécifié lors de la création de hello de sortie pour la tâche de flux de données Analytique hello.
1. Sous **ACTIONS**, cliquez sur hello première icône toocreate un rapport.

   ![Créer un rapport Microsoft Power BI](media/iot-hub-live-data-visualization-in-power-bi/7_create-power-bi-report-microsoft.png)

1. Créer une ligne graphique tooshow en temps réel de la température au fil du temps.
   1. Sur la page de création de rapports hello, ajoutez un graphique en courbes.
   1. Sur hello **champs** volet, développez la table hello que vous avez spécifié lors de la création de sortie hello pour la tâche de flux de données Analytique hello.
   1. Faites glisser **EventEnqueuedUtcTime** trop**axe** sur hello **visualisations** volet.
   1. Faites glisser **température** trop**valeurs**.

      Le graphique en courbes est désormais créé. axe des abscisses Hello affiche la date et heure dans le fuseau horaire de hello UTC. l’axe des y Hello affiche la température du capteur de hello.

      ![Ajouter un graphique en courbes pour température tooa rapport Microsoft Power BI](media/iot-hub-live-data-visualization-in-power-bi/8_add-line-chart-for-temperature-to-power-bi-report-microsoft.png)

1. Créer un autre humidité en temps réel ligne graphique tooshow au fil du temps. toodo, suivez hello même les étapes ci-dessus et placez **EventEnqueuedUtcTime** sur l’axe des abscisses hello et **humidité** sur l’axe des y hello.

   ![Ajouter un graphique en courbes pour humidité tooa rapport Microsoft Power BI](media/iot-hub-live-data-visualization-in-power-bi/9_add-line-chart-for-humidity-to-power-bi-report-microsoft.png)

1. Cliquez sur **enregistrer** rapport de hello toosave.
1. Cliquez sur **fichier** > **publier tooweb**.
1. Cliquez sur **Créer le code incorporé**, puis cliquez sur **Publier**.

Vous bénéficiez de lien de rapport hello que vous pouvez partager avec quiconque pour accéder au rapport et un rapport de hello toointegrate code extrait de code dans votre blog ou d’un site Web.

![Publier un rapport Microsoft Power BI](media/iot-hub-live-data-visualization-in-power-bi/10_publish-power-bi-report-microsoft.png)

Microsoft propose également hello [applications mobiles Power BI](https://powerbi.microsoft.com/en-us/documentation/powerbi-power-bi-apps-for-mobile-devices/) pour afficher et interagir avec vos tableaux de bord Power BI et les rapports sur votre appareil mobile.

## <a name="next-steps"></a>Étapes suivantes

Vous avez utilisé avec succès données de capteur en temps réel toovisualize Power BI à partir de votre concentrateur Azure IoT.
Donnée une autre façon toovisualize à partir d’Azure IoT Hub. Consultez [données de capteur en temps réel toovisualize utilisation Azure Web Apps dans Azure IoT Hub](iot-hub-live-data-visualization-in-web-apps.md).

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
