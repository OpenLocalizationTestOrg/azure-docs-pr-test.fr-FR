---
title: "surveillance à distance aaaIoT et notifications avec Azure Logic Apps | Documents Microsoft"
description: "Utilisez Azure Logic Apps pour surveiller la température IoT sur votre IoT hub et automatiquement envoyer par courrier électronique des notifications tooyour boîte aux lettres pour toute anomalie détectée."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "surveillance iot, notifications iot, surveillance de température iot"
ms.assetid: 43043067-2e1f-42c9-953d-e2dce8fd86df
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: xshi
ms.openlocfilehash: 89396528ed63c37258e1b49f342f0723e686ecb3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="iot-remote-monitoring-and-notifications-with-azure-logic-apps-connecting-your-iot-hub-and-mailbox"></a>Surveillance à distance IoT et notifications avec Azure Logic Apps connectant votre IoT Hub et votre boîte aux lettres

![Diagramme de bout en bout](media/iot-hub-get-started-e2e-diagram/7.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

Azure Logic Apps fournit un moyen de processus tooautomate comme une série d’étapes. Une application logique peut établir une connexion via divers services et protocoles. Elle commence par un déclencheur tel que « Lorsqu’un compte est ajouté », suivie d’une combinaison d’actions, similaire à « envoi d’une notification Push ». Cette fonctionnalité rend Logic Apps idéale pour la surveillance IoT, telle que la vigilance face aux anomalies, parmi d’autres scénarios d’utilisation.

## <a name="what-you-learn"></a>Contenu

Vous apprendrez comment toocreate une application de la logique qui se connecte votre IoT hub et votre boîte aux lettres pour la surveillance de la température et de notifications. Lors de la température de hello est supérieure à 30 C, hello client application marques `temperatureAlert = "true"` dans le message de type hello, il envoie tooyour IoT hub. message de type Hello déclencheurs hello logique application toosend vous une notification par courrier électronique.

## <a name="what-you-do"></a>Procédure

* Créer un espace de noms service bus et ajouter un tooit de file d’attente.
* Ajouter un point de terminaison et un routage IoT hub règle tooyour.
* Créez, configurez et testez une application logique.

## <a name="what-you-need"></a>Ce dont vous avez besoin

* Didacticiel [configurer votre appareil](iot-hub-raspberry-pi-kit-node-get-started.md) terminé qui couvre hello suivant les exigences :
  * Un abonnement Azure actif.
  * Une instance Azure IoT Hub associée à votre abonnement.
  * Une application cliente qui envoie le concentrateur de messages tooyour Azure IoT.

## <a name="create-service-bus-namespace-and-add-a-queue-tooit"></a>Créer l’espace de noms service bus et ajouter un tooit de file d’attente

### <a name="create-a-service-bus-namespace"></a>Création d'un espace de noms Service Bus

1. Sur hello [portail Azure](https://portal.azure.com/), cliquez sur **nouveau** > **intégration** > **Service Bus**.
1. Fournir hello informations suivantes :

   **Nom**: nom hello du bus de service hello.

   **Niveau tarifaire**: cliquez sur **De base** > **Sélectionnez**. niveau de base Hello est suffisant pour ce didacticiel.

   **Groupe de ressources**: utilisez hello même groupe de ressources qui utilise de votre hub IoT.

   **Emplacement**: utilisez hello même emplacement que votre hub IoT utilise.
1. Cliquez sur **Créer**.

   ![Créer un espace de noms service bus Bonjour portail Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/1_create-service-bus-namespace-azure-portal.png)

### <a name="add-a-service-bus-queue"></a>Ajouter une file d’attente Service Bus

1. Ouvrez l’espace de noms hello service bus, puis cliquez sur **+ file d’attente**.
1. Entrez un nom pour la file d’attente hello, puis cliquez sur **créer**.
1. Ouvrir la file d’attente de bus de service hello, puis cliquez sur **les stratégies d’accès partagé** > **+ ajouter**.
1. Entrez un nom pour la stratégie de hello, cocher **gérer**, puis cliquez sur **créer**.

   ![Ajouter une file d’attente du bus de service Bonjour portail Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/2_add-service-bus-queue-azure-portal.png)

## <a name="add-an-endpoint-and-a-routing-rule-tooyour-iot-hub"></a>Ajouter un point de terminaison et un routage IoT hub règle tooyour

### <a name="add-an-endpoint"></a>Ajout d’un point de terminaison

1. Ouvrez votre IoT Hub et cliquez sur Points de terminaison > + Ajouter.
1. Entrez hello informations suivantes :

   **Nom**: nom hello du point de terminaison hello.

   **Type de point de terminaison** : sélectionnez **File d’attente Service Bus**.

   **Espace de noms Service Bus**: sélectionnez l’espace de noms hello vous avez créé.

   **File d’attente Service Bus**: vous avez créé de la file d’attente hello Select.
1. Cliquez sur **OK**.

   ![Ajouter un IoT hub de point de terminaison tooyour Bonjour portail Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/3_add-iot-hub-endpoint-azure-portal.png)

### <a name="add-a-routing-rule"></a>Ajouter une règle de routage

1. Dans votre Iot Hub, cliquez sur **Itinéraires** > **+ Ajouter**.
1. Entrez hello informations suivantes :

   **Nom**: nom hello de règle de routage hello.

   **Source de données** : sélectionnez **DeviceMessages**.

   **Point de terminaison**: sélectionnez le point de terminaison hello vous avez créé.

   **Chaîne de requête** : entrez `temperatureAlert = "true"`.
1. Cliquez sur **Enregistrer**.

   ![Ajouter une règle de routage Bonjour portail Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/4_add-routing-rule-azure-portal.png)

## <a name="create-and-configure-a-logic-app"></a>Créer et configurer une application logique

### <a name="create-a-logic-app"></a>Créer une application logique

1. Bonjour [portail Azure](https://portal.azure.com/), cliquez sur **nouveau** > **intégration** > **application logique**.
1. Entrez hello informations suivantes :

   **Nom**: nom hello d’application logique de hello.

   **Groupe de ressources**: utilisez hello même groupe de ressources qui utilise de votre hub IoT.

   **Emplacement**: utilisez hello même emplacement que votre hub IoT utilise.
1. Cliquez sur **Créer**.

### <a name="configure-hello-logic-app"></a>Configurer l’application logique de hello

1. Ouvrez l’application hello logique qui s’ouvre dans hello logique de concepteur d’applications.
1. Bonjour logique de concepteur d’applications, cliquez sur **application logique vide**.

   ![Démarrez avec une application vide logique Bonjour portail Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/5_start-with-blank-logic-app-azure-portal.png)

1. Cliquez sur **Service Bus**.

   ![Sélectionnez toostart Service Bus création de votre application logique Bonjour portail Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/6_select-service-bus-when-creating-blank-logic-app-azure-portal.png)

1. Cliquez sur **Service Bus – lorsqu’un ou plusieurs messages arrivent dans une file d’attente (saisie semi-automatique)**.
1. Créez une connexion Service Bus.
   1. Entrez un nom de connexion.
   1. Cliquez sur hello espace de noms bus > hello stratégie de bus de service > **créer**.

      ![Créer une connexion de service bus pour votre application logique Bonjour portail Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/7_create-service-bus-connection-in-logic-app-azure-portal.png)

   1. Cliquez sur **continuer** après la création de connexion de service bus hello.
   1. Sélectionnez une file d’attente hello que vous avez créé, puis entrez `175` pour **nombre de messages au Maximum**

      ![Spécifiez le nombre de message maximale de hello hello connexion de service bus dans votre logique d’application](media/iot-hub-monitoring-notifications-with-azure-logic-apps/8_specify-maximum-message-count-for-service-bus-connection-logic-app-azure-portal.png)
   1. Cliquez sur « Enregistrer » hello toosave du bouton change.

1. Créez une connexion de service SMTP.
   1. Choisissez **Nouvelle étape** > **Ajouter une action**.
   1. Type `SMTP`, cliquez sur hello **SMTP** hello le résultat de recherche de service, puis cliquez sur **SMTP - envoyer un courrier électronique**.

      ![Créer une connexion SMTP dans votre application logique Bonjour portail Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/9_create-smtp-connection-logic-app-azure-portal.png)

   1. Entrez les informations de hello SMTP de votre boîte aux lettres, puis cliquez sur **créer**.

      ![Entrez les informations de connexion SMTP dans votre application logique Bonjour portail Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/10_enter-smtp-connection-info-logic-app-azure-portal.png)

      Obtenir des informations de hello SMTP pour [Hotmail/Outlook.com](https://support.office.com/en-us/article/Add-your-Outlook-com-account-to-another-mail-app-73f3b178-0009-41ae-aab1-87b80fa94970), [Gmail](https://support.google.com/a/answer/176600?hl=en), et [messagerie Yahoo](https://help.yahoo.com/kb/SLN4075.html).
   1. Entrez votre adresse de messagerie pour **De** et **À**, et `High temperature detected` pour **Objet** et **Corps**.
   1. Cliquez sur **Enregistrer**.

application de la logique de Hello est en marche lors de son enregistrement.

## <a name="test-hello-logic-app"></a>Application de test hello logique

1. Démarrer l’application hello client que vous déployez appareil tooyour dans [ESP8266 de se connecter tooAzure IoT Hub](iot-hub-arduino-huzzah-esp8266-get-started.md).
1. Augmenter la température de l’environnement hello autour de toobe de SensorTag hello ci-dessus c de 30. Par exemple, la lumière une bougie autour de votre SensorTag.
1. Vous devriez recevoir une notification par courrier électronique envoyée par l’application de la logique de hello.

   > [!NOTE]
   > Votre fournisseur de services de messagerie peut-être tooverify hello expéditeur identité toomake que c’est vous qui envoie par courrier électronique hello.

## <a name="next-steps"></a>Étapes suivantes

Vous avez créé avec succès une application logique qui connecte votre IoT Hub et votre boîte aux lettres pour la surveillance de la température et les notifications.

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
