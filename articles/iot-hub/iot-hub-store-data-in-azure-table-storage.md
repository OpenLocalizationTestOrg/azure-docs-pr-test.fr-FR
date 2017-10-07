---
title: "aaaSave tooAzure le stockage de données des messages de votre hub IoT | Documents Microsoft"
description: "Utiliser un toosave d’application Azure fonction votre tooyour de messages de hub IoT stockage de table Windows Azure. messages de hub IoT Hello contiennent des informations, telles que les données de capteur, qui sont envoyées à partir de votre appareil IoT."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "stockage de données iot, stockage de données de capteur iot"
ms.assetid: 62fd14fd-aaaa-4b3d-8367-75c1111b6269
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/16/2017
ms.author: xshi
ms.openlocfilehash: be72d9ba9a781822926364351b50f58f5d96e94a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="save-iot-hub-messages-that-contain-sensor-data-tooyour-azure-table-storage"></a>Enregistrer les messages de hub IoT qui contiennent le stockage de table Azure capteur données tooyour

![Diagramme de bout en bout](media/iot-hub-get-started-e2e-diagram/3.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

## <a name="what-you-learn"></a>Contenu

Vous allez apprendre comment toocreate un compte de stockage Azure et Azure fonctionnent des messages de hub IoT toostore l’application dans votre stockage de table.

## <a name="what-you-do"></a>Procédure

- Créez un compte de stockage Azure.
- Préparez votre hub IoT messages tooread de connexion.
- Créez et déployez une application de fonction Azure.

## <a name="what-you-need"></a>Ce dont vous avez besoin

- [Configurer votre périphérique](iot-hub-raspberry-pi-kit-node-get-started.md) hello toocover suivant les exigences :
  - Un abonnement Azure actif
  - Un hub IoT associé à votre abonnement 
  - Une application en cours d’exécution qui envoie des IoT hub tooyour de messages

## <a name="create-an-azure-storage-account"></a>Création d'un compte de stockage Azure

1. Bonjour [portail Azure](https://portal.azure.com/), cliquez sur **nouveau** > **stockage** > **compte de stockage**  >   **Créer**.

2. Entrez les informations nécessaires hello hello compte de stockage :

   ![Créer un compte de stockage Bonjour portail Azure](media\iot-hub-store-data-in-azure-table-storage\1_azure-portal-create-storage-account.png)

   * **Nom**: nom hello hello du compte de stockage. nom de Hello doit être globalement unique.

   * **Groupe de ressources**: utilisez hello même groupe de ressources qui utilise de votre hub IoT.

   * **Code confidentiel toodashboard**: sélectionnez cette option pour le hub de IoT tooyour accéder facilement à partir du tableau de bord hello.

3. Cliquez sur **Créer**.

## <a name="prepare-your-iot-hub-connection-tooread-messages"></a>Préparer votre hub IoT messages tooread de connexion

IoT hub expose une événement intégré concentrateur compatible avec le point de terminaison tooenable applications tooread IoT hub les messages. Pendant ce temps, les applications utilisent consommateur regroupe tooread les données à partir de votre hub IoT. Avant de créer un fonction Azure application tooread de données à partir de votre hub IoT, hello suivant :

- Obtenir la chaîne de connexion de hello de votre point de terminaison de hub IoT.
- Créer un groupe de consommateurs pour votre IoT Hub.

### <a name="get-hello-connection-string-of-your-iot-hub-endpoint"></a>Obtenir la chaîne de connexion hello de votre point de terminaison IoT hub

1. Ouvrez votre IoT Hub.

2. Sur hello **IoT Hub** volet, sous **messagerie**, cliquez sur **points de terminaison**.

3. Bonjour avec le bouton droit volet, sous **des points de terminaison intégrés**, cliquez sur **événements**.

4. Bonjour **propriétés** volet, hello Remarque valeurs suivantes :
   - Point de terminaison compatible avec Event Hub
   - Nom compatible avec Event Hub

   ![Obtenir la chaîne de connexion hello de votre point de terminaison de hub IoT Bonjour portail Azure](media\iot-hub-store-data-in-azure-table-storage\2_azure-portal-iot-hub-endpoint-connection-string.png)

5. Bonjour **IoT Hub** volet, sous **paramètres**, cliquez sur **les stratégies d’accès partagé**.

6. Cliquez sur **iothubowner**.

7. Hello de note **clé primaire** valeur.

8. Créez la chaîne de connexion hello de votre point de terminaison de hub IoT comme suit :

   `Endpoint=<Event Hub-compatible endpoint>;SharedAccessKeyName=iothubowner;SharedAccessKey=<Primary key>`

   > [!NOTE]
   > Remplacez `<Event Hub-compatible endpoint>` et `<Primary key>` avec les valeurs hello que vous avez notée précédemment.

### <a name="create-a-consumer-group-for-your-iot-hub"></a>Créer un groupe de consommateurs pour votre IoT Hub

1. Ouvrez votre IoT Hub.

2. Bonjour **IoT Hub** volet, sous **messagerie**, cliquez sur **points de terminaison**.

3. Bonjour avec le bouton droit volet, sous **des points de terminaison intégrés**, cliquez sur **événements**.

4. Bonjour **propriétés** volet, sous **groupes de consommateurs**, entrez un nom, puis prenez note de celui-ci.

5. Cliquez sur **Enregistrer**.

## <a name="create-and-deploy-an-azure-function-app"></a>Créer et déployer une application de fonction Azure

1. Bonjour [portail Azure](https://portal.azure.com/), cliquez sur **nouveau** > **de calcul** > **fonction application**  >   **Créer**.

2. Entrez hello les informations nécessaires pour l’application de fonction hello.

   ![Créer une application de la fonction Bonjour portail Azure](media\iot-hub-store-data-in-azure-table-storage\3_azure-portal-create-function-app.png)

   * **Nom de l’application**: nom hello d’application de fonction hello. nom de Hello doit être globalement unique.

   * **Groupe de ressources**: utilisez hello même groupe de ressources qui utilise de votre hub IoT.

   * **Compte de stockage**: hello compte de stockage que vous avez créé.

   * **Code confidentiel toodashboard**: Activez cette option pour l’application de fonction toohello accéder facilement à partir du tableau de bord hello.

3. Cliquez sur **Créer**.

4. Une fois que l’application de fonction hello a été créée, l’ouvrir.

5. Dans l’application de fonction hello, créez une fonction de manière hello suivante :

   a. Cliquez sur **Nouvelle fonction**.

   b. Sélectionnez **JavaScript** pour **Langage** et **Data Processing** (Traitement de données) pour **Scénario**.

   c. Cliquez sur **Créer cette fonction**, puis sur **Nouvelle fonction**.

   d. Sélectionnez **JavaScript** langage hello et **le traitement des données** pour le scénario de hello.

   e. Cliquez sur hello **EventHubTrigger-JavaScript** modèle.

   f. Entrez les informations nécessaires hello pour le modèle de hello.

      * **Nom de votre fonction**: nom hello de fonction hello.

      * **Nom de Hub d’événements**: nom de hub compatible avec l’événement hello que vous avez notée précédemment.

      * **Connexion de concentrateur d’événements**: chaîne de connexion tooadd hello du point de terminaison de hub IoT hello que vous avez créé, cliquez sur **nouveau**.

   g. Cliquez sur **Créer**.

6. Configurer une sortie de fonction hello de manière hello suivante :

   a. Cliquez sur **Intégrer** > **Nouvelle sortie** > **tockage Table Azure** > **Sélectionner**.

      ![Ajouter une application de fonction de table stockage tooyour Bonjour portail Azure](media\iot-hub-store-data-in-azure-table-storage\4_azure-portal-function-app-add-output-table-storage.png)

   b. Entrez les informations nécessaires hello.

      * **Nom du paramètre table**: utilisez `outputTable`, qui sera utilisée dans hello Azure code de la fonction.
      
      * **Nom de la table** : utilisez `deviceData`.

      * **Connexion au compte de stockage** : cliquez sur **Nouveau**, puis sélectionnez ou entrez votre compte de stockage. Si le compte de stockage hello n’est pas affichée, consultez [exigences relatives aux comptes de stockage](https://docs.microsoft.com/azure/azure-functions/functions-create-function-app-portal#storage-account-requirements).
      
   c. Cliquez sur **Enregistrer**.

7. Sous **Déclencheurs**, cliquez sur **Azure Event Hub (eventHubMessages)**.

8. Sous **groupe de consommateurs du Hub d’événements**, entrez le nom hello du groupe de consommateurs hello créé, puis cliquez sur **enregistrer**.

9. Fonction hello que vous avez créé sur hello gauche, puis cliquez sur **afficher les fichiers** sur hello droite.

10. Remplacez le code hello dans `index.js` avec les éléments suivants de hello :

   ```javascript
   'use strict';

   // This function is triggered each time a message is received in hello IoT hub.
   // hello message payload is persisted in an Azure storage table
 
   module.exports = function (context, iotHubMessage) {
    context.log('Message received: ' + JSON.stringify(iotHubMessage));
    var date = Date.now();
    var partitionKey = Math.floor(date / (24 * 60 * 60 * 1000)) + '';
    var rowKey = date + '';
    context.bindings.outputTable = {
     "partitionKey": partitionKey,
     "rowKey": rowKey,
     "message": JSON.stringify(iotHubMessage)
    };
    context.done();
   };
   ```

11. Cliquez sur **Enregistrer**.

Vous venez de créer application de fonction hello. Elle stocke les messages reçus par votre hub IoT dans votre Stockage Table.

> [!NOTE]
> Vous pouvez utiliser hello **exécuter** bouton tootest hello fonction app. Lorsque vous cliquez sur **exécuter**, hello test envoyé tooyour IoT hub. arrivée Hello de message de type hello doit déclencher hello fonction application toostart, puis enregistrez stockage de table tooyour hello message. Hello **journaux** volet enregistre des détails de hello du processus de hello.

## <a name="verify-your-message-in-your-table-storage"></a>Vérifier votre message dans votre stockage de table

1. Exécuter l’exemple d’application hello sur votre concentrateur de périphérique toosend messages tooyour IoT.

2. [Téléchargez et installez l’Explorateur de Stockage Azure](http://storageexplorer.com/).

3. Ouvrez l’Explorateur de stockage, cliquez sur **ajouter un compte Azure** > **connecter**, puis connectez-vous à tooyour compte Azure.

4. Cliquez sur votre abonnement Azure > **Comptes de stockage** > votre compte de stockage > **Tables** > **deviceData**.

   Vous devez voir les messages envoyés à partir de votre hub IoT de tooyour périphérique connecté hello `deviceData` table.

## <a name="next-steps"></a>Étapes suivantes

Vous avez créé votre compte de stockage Azure et votre application de fonction Azure, qui stocke les messages reçus par votre hub IoT dans votre Stockage Table Azure.

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
