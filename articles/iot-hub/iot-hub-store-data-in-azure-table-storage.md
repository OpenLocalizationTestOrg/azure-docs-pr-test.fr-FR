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
# <a name="save-iot-hub-messages-that-contain-sensor-data-tooyour-azure-table-storage"></a><span data-ttu-id="95608-105">Enregistrer les messages de hub IoT qui contiennent le stockage de table Azure capteur données tooyour</span><span class="sxs-lookup"><span data-stu-id="95608-105">Save IoT hub messages that contain sensor data tooyour Azure table storage</span></span>

![Diagramme de bout en bout](media/iot-hub-get-started-e2e-diagram/3.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

## <a name="what-you-learn"></a><span data-ttu-id="95608-107">Contenu</span><span class="sxs-lookup"><span data-stu-id="95608-107">What you learn</span></span>

<span data-ttu-id="95608-108">Vous allez apprendre comment toocreate un compte de stockage Azure et Azure fonctionnent des messages de hub IoT toostore l’application dans votre stockage de table.</span><span class="sxs-lookup"><span data-stu-id="95608-108">You learn how toocreate an Azure storage account and an Azure function app toostore IoT hub messages in your table storage.</span></span>

## <a name="what-you-do"></a><span data-ttu-id="95608-109">Procédure</span><span class="sxs-lookup"><span data-stu-id="95608-109">What you do</span></span>

- <span data-ttu-id="95608-110">Créez un compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="95608-110">Create an Azure storage account.</span></span>
- <span data-ttu-id="95608-111">Préparez votre hub IoT messages tooread de connexion.</span><span class="sxs-lookup"><span data-stu-id="95608-111">Prepare your IoT hub connection tooread messages.</span></span>
- <span data-ttu-id="95608-112">Créez et déployez une application de fonction Azure.</span><span class="sxs-lookup"><span data-stu-id="95608-112">Create and deploy an Azure function app.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="95608-113">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="95608-113">What you need</span></span>

- <span data-ttu-id="95608-114">[Configurer votre périphérique](iot-hub-raspberry-pi-kit-node-get-started.md) hello toocover suivant les exigences :</span><span class="sxs-lookup"><span data-stu-id="95608-114">[Set up your device](iot-hub-raspberry-pi-kit-node-get-started.md) toocover hello following requirements:</span></span>
  - <span data-ttu-id="95608-115">Un abonnement Azure actif</span><span class="sxs-lookup"><span data-stu-id="95608-115">An active Azure subscription</span></span>
  - <span data-ttu-id="95608-116">Un hub IoT associé à votre abonnement</span><span class="sxs-lookup"><span data-stu-id="95608-116">An IoT hub under your subscription</span></span> 
  - <span data-ttu-id="95608-117">Une application en cours d’exécution qui envoie des IoT hub tooyour de messages</span><span class="sxs-lookup"><span data-stu-id="95608-117">A running application that sends messages tooyour IoT hub</span></span>

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="95608-118">Création d'un compte de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="95608-118">Create an Azure storage account</span></span>

1. <span data-ttu-id="95608-119">Bonjour [portail Azure](https://portal.azure.com/), cliquez sur **nouveau** > **stockage** > **compte de stockage**  >   **Créer**.</span><span class="sxs-lookup"><span data-stu-id="95608-119">In hello [Azure portal](https://portal.azure.com/), click **New** > **Storage** > **Storage account** > **Create**.</span></span>

2. <span data-ttu-id="95608-120">Entrez les informations nécessaires hello hello compte de stockage :</span><span class="sxs-lookup"><span data-stu-id="95608-120">Enter hello necessary information for hello storage account:</span></span>

   ![Créer un compte de stockage Bonjour portail Azure](media\iot-hub-store-data-in-azure-table-storage\1_azure-portal-create-storage-account.png)

   * <span data-ttu-id="95608-122">**Nom**: nom hello hello du compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="95608-122">**Name**: hello name of hello storage account.</span></span> <span data-ttu-id="95608-123">nom de Hello doit être globalement unique.</span><span class="sxs-lookup"><span data-stu-id="95608-123">hello name must be globally unique.</span></span>

   * <span data-ttu-id="95608-124">**Groupe de ressources**: utilisez hello même groupe de ressources qui utilise de votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="95608-124">**Resource group**: Use hello same resource group that your IoT hub uses.</span></span>

   * <span data-ttu-id="95608-125">**Code confidentiel toodashboard**: sélectionnez cette option pour le hub de IoT tooyour accéder facilement à partir du tableau de bord hello.</span><span class="sxs-lookup"><span data-stu-id="95608-125">**Pin toodashboard**: Select this option for easy access tooyour IoT hub from hello dashboard.</span></span>

3. <span data-ttu-id="95608-126">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="95608-126">Click **Create**.</span></span>

## <a name="prepare-your-iot-hub-connection-tooread-messages"></a><span data-ttu-id="95608-127">Préparer votre hub IoT messages tooread de connexion</span><span class="sxs-lookup"><span data-stu-id="95608-127">Prepare your IoT hub connection tooread messages</span></span>

<span data-ttu-id="95608-128">IoT hub expose une événement intégré concentrateur compatible avec le point de terminaison tooenable applications tooread IoT hub les messages.</span><span class="sxs-lookup"><span data-stu-id="95608-128">IoT hub exposes a built-in event hub-compatible endpoint tooenable applications tooread IoT hub messages.</span></span> <span data-ttu-id="95608-129">Pendant ce temps, les applications utilisent consommateur regroupe tooread les données à partir de votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="95608-129">Meanwhile, applications use consumer groups tooread data from your IoT hub.</span></span> <span data-ttu-id="95608-130">Avant de créer un fonction Azure application tooread de données à partir de votre hub IoT, hello suivant :</span><span class="sxs-lookup"><span data-stu-id="95608-130">Before you create an Azure function app tooread data from your IoT hub, do hello following:</span></span>

- <span data-ttu-id="95608-131">Obtenir la chaîne de connexion de hello de votre point de terminaison de hub IoT.</span><span class="sxs-lookup"><span data-stu-id="95608-131">Get hello connection string of your IoT hub endpoint.</span></span>
- <span data-ttu-id="95608-132">Créer un groupe de consommateurs pour votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="95608-132">Create a consumer group for your IoT hub.</span></span>

### <a name="get-hello-connection-string-of-your-iot-hub-endpoint"></a><span data-ttu-id="95608-133">Obtenir la chaîne de connexion hello de votre point de terminaison IoT hub</span><span class="sxs-lookup"><span data-stu-id="95608-133">Get hello connection string of your IoT hub endpoint</span></span>

1. <span data-ttu-id="95608-134">Ouvrez votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="95608-134">Open your IoT hub.</span></span>

2. <span data-ttu-id="95608-135">Sur hello **IoT Hub** volet, sous **messagerie**, cliquez sur **points de terminaison**.</span><span class="sxs-lookup"><span data-stu-id="95608-135">On hello **IoT Hub** pane, under **Messaging**, click **Endpoints**.</span></span>

3. <span data-ttu-id="95608-136">Bonjour avec le bouton droit volet, sous **des points de terminaison intégrés**, cliquez sur **événements**.</span><span class="sxs-lookup"><span data-stu-id="95608-136">In hello right pane, under **Built-in endpoints**, click **Events**.</span></span>

4. <span data-ttu-id="95608-137">Bonjour **propriétés** volet, hello Remarque valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="95608-137">In hello **Properties** pane, note hello following values:</span></span>
   - <span data-ttu-id="95608-138">Point de terminaison compatible avec Event Hub</span><span class="sxs-lookup"><span data-stu-id="95608-138">Event hub-compatible endpoint</span></span>
   - <span data-ttu-id="95608-139">Nom compatible avec Event Hub</span><span class="sxs-lookup"><span data-stu-id="95608-139">Event hub-compatible name</span></span>

   ![Obtenir la chaîne de connexion hello de votre point de terminaison de hub IoT Bonjour portail Azure](media\iot-hub-store-data-in-azure-table-storage\2_azure-portal-iot-hub-endpoint-connection-string.png)

5. <span data-ttu-id="95608-141">Bonjour **IoT Hub** volet, sous **paramètres**, cliquez sur **les stratégies d’accès partagé**.</span><span class="sxs-lookup"><span data-stu-id="95608-141">In hello **IoT Hub** pane, under **Settings**, click **Shared access policies**.</span></span>

6. <span data-ttu-id="95608-142">Cliquez sur **iothubowner**.</span><span class="sxs-lookup"><span data-stu-id="95608-142">Click **iothubowner**.</span></span>

7. <span data-ttu-id="95608-143">Hello de note **clé primaire** valeur.</span><span class="sxs-lookup"><span data-stu-id="95608-143">Note hello **Primary key** value.</span></span>

8. <span data-ttu-id="95608-144">Créez la chaîne de connexion hello de votre point de terminaison de hub IoT comme suit :</span><span class="sxs-lookup"><span data-stu-id="95608-144">Create hello connection string of your IoT hub endpoint as follows:</span></span>

   `Endpoint=<Event Hub-compatible endpoint>;SharedAccessKeyName=iothubowner;SharedAccessKey=<Primary key>`

   > [!NOTE]
   > <span data-ttu-id="95608-145">Remplacez `<Event Hub-compatible endpoint>` et `<Primary key>` avec les valeurs hello que vous avez notée précédemment.</span><span class="sxs-lookup"><span data-stu-id="95608-145">Replace `<Event Hub-compatible endpoint>` and `<Primary key>` with hello values that you noted earlier.</span></span>

### <a name="create-a-consumer-group-for-your-iot-hub"></a><span data-ttu-id="95608-146">Créer un groupe de consommateurs pour votre IoT Hub</span><span class="sxs-lookup"><span data-stu-id="95608-146">Create a consumer group for your IoT hub</span></span>

1. <span data-ttu-id="95608-147">Ouvrez votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="95608-147">Open your IoT hub.</span></span>

2. <span data-ttu-id="95608-148">Bonjour **IoT Hub** volet, sous **messagerie**, cliquez sur **points de terminaison**.</span><span class="sxs-lookup"><span data-stu-id="95608-148">In hello **IoT Hub** pane, under **Messaging**, click **Endpoints**.</span></span>

3. <span data-ttu-id="95608-149">Bonjour avec le bouton droit volet, sous **des points de terminaison intégrés**, cliquez sur **événements**.</span><span class="sxs-lookup"><span data-stu-id="95608-149">In hello right pane, under **Built-in endpoints**, click **Events**.</span></span>

4. <span data-ttu-id="95608-150">Bonjour **propriétés** volet, sous **groupes de consommateurs**, entrez un nom, puis prenez note de celui-ci.</span><span class="sxs-lookup"><span data-stu-id="95608-150">In hello **Properties** pane, under **Consumer groups**, enter a name, and then make a note of it.</span></span>

5. <span data-ttu-id="95608-151">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="95608-151">Click **Save**.</span></span>

## <a name="create-and-deploy-an-azure-function-app"></a><span data-ttu-id="95608-152">Créer et déployer une application de fonction Azure</span><span class="sxs-lookup"><span data-stu-id="95608-152">Create and deploy an Azure function app</span></span>

1. <span data-ttu-id="95608-153">Bonjour [portail Azure](https://portal.azure.com/), cliquez sur **nouveau** > **de calcul** > **fonction application**  >   **Créer**.</span><span class="sxs-lookup"><span data-stu-id="95608-153">In hello [Azure portal](https://portal.azure.com/), click **New** > **Compute** > **Function App** > **Create**.</span></span>

2. <span data-ttu-id="95608-154">Entrez hello les informations nécessaires pour l’application de fonction hello.</span><span class="sxs-lookup"><span data-stu-id="95608-154">Enter hello necessary information for hello function app.</span></span>

   ![Créer une application de la fonction Bonjour portail Azure](media\iot-hub-store-data-in-azure-table-storage\3_azure-portal-create-function-app.png)

   * <span data-ttu-id="95608-156">**Nom de l’application**: nom hello d’application de fonction hello.</span><span class="sxs-lookup"><span data-stu-id="95608-156">**App name**: hello name of hello function app.</span></span> <span data-ttu-id="95608-157">nom de Hello doit être globalement unique.</span><span class="sxs-lookup"><span data-stu-id="95608-157">hello name must be globally unique.</span></span>

   * <span data-ttu-id="95608-158">**Groupe de ressources**: utilisez hello même groupe de ressources qui utilise de votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="95608-158">**Resource group**: Use hello same resource group that your IoT hub uses.</span></span>

   * <span data-ttu-id="95608-159">**Compte de stockage**: hello compte de stockage que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="95608-159">**Storage Account**: hello storage account that you created.</span></span>

   * <span data-ttu-id="95608-160">**Code confidentiel toodashboard**: Activez cette option pour l’application de fonction toohello accéder facilement à partir du tableau de bord hello.</span><span class="sxs-lookup"><span data-stu-id="95608-160">**Pin toodashboard**: Check this option for easy access toohello function app from hello dashboard.</span></span>

3. <span data-ttu-id="95608-161">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="95608-161">Click **Create**.</span></span>

4. <span data-ttu-id="95608-162">Une fois que l’application de fonction hello a été créée, l’ouvrir.</span><span class="sxs-lookup"><span data-stu-id="95608-162">After hello function app has been created, open it.</span></span>

5. <span data-ttu-id="95608-163">Dans l’application de fonction hello, créez une fonction de manière hello suivante :</span><span class="sxs-lookup"><span data-stu-id="95608-163">In hello function app, create a new function by doing hello following:</span></span>

   <span data-ttu-id="95608-164">a.</span><span class="sxs-lookup"><span data-stu-id="95608-164">a.</span></span> <span data-ttu-id="95608-165">Cliquez sur **Nouvelle fonction**.</span><span class="sxs-lookup"><span data-stu-id="95608-165">Click **New Function**.</span></span>

   <span data-ttu-id="95608-166">b.</span><span class="sxs-lookup"><span data-stu-id="95608-166">b.</span></span> <span data-ttu-id="95608-167">Sélectionnez **JavaScript** pour **Langage** et **Data Processing** (Traitement de données) pour **Scénario**.</span><span class="sxs-lookup"><span data-stu-id="95608-167">Select **JavaScript** for **Language**, and **Data Processing** for **Scenario**.</span></span>

   <span data-ttu-id="95608-168">c.</span><span class="sxs-lookup"><span data-stu-id="95608-168">c.</span></span> <span data-ttu-id="95608-169">Cliquez sur **Créer cette fonction**, puis sur **Nouvelle fonction**.</span><span class="sxs-lookup"><span data-stu-id="95608-169">Click **Create this function**, and then click **New Function**.</span></span>

   <span data-ttu-id="95608-170">d.</span><span class="sxs-lookup"><span data-stu-id="95608-170">d.</span></span> <span data-ttu-id="95608-171">Sélectionnez **JavaScript** langage hello et **le traitement des données** pour le scénario de hello.</span><span class="sxs-lookup"><span data-stu-id="95608-171">Select **JavaScript** for hello language, and **Data Processing** for hello scenario.</span></span>

   <span data-ttu-id="95608-172">e.</span><span class="sxs-lookup"><span data-stu-id="95608-172">e.</span></span> <span data-ttu-id="95608-173">Cliquez sur hello **EventHubTrigger-JavaScript** modèle.</span><span class="sxs-lookup"><span data-stu-id="95608-173">Click hello **EventHubTrigger-JavaScript** template.</span></span>

   <span data-ttu-id="95608-174">f.</span><span class="sxs-lookup"><span data-stu-id="95608-174">f.</span></span> <span data-ttu-id="95608-175">Entrez les informations nécessaires hello pour le modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="95608-175">Enter hello necessary information for hello template.</span></span>

      * <span data-ttu-id="95608-176">**Nom de votre fonction**: nom hello de fonction hello.</span><span class="sxs-lookup"><span data-stu-id="95608-176">**Name your function**: hello name of hello function.</span></span>

      * <span data-ttu-id="95608-177">**Nom de Hub d’événements**: nom de hub compatible avec l’événement hello que vous avez notée précédemment.</span><span class="sxs-lookup"><span data-stu-id="95608-177">**Event Hub name**: hello event hub-compatible name that you noted earlier.</span></span>

      * <span data-ttu-id="95608-178">**Connexion de concentrateur d’événements**: chaîne de connexion tooadd hello du point de terminaison de hub IoT hello que vous avez créé, cliquez sur **nouveau**.</span><span class="sxs-lookup"><span data-stu-id="95608-178">**Event Hub connection**: tooadd hello connection string of hello IoT hub endpoint that you created, click **New**.</span></span>

   <span data-ttu-id="95608-179">g.</span><span class="sxs-lookup"><span data-stu-id="95608-179">g.</span></span> <span data-ttu-id="95608-180">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="95608-180">Click **Create**.</span></span>

6. <span data-ttu-id="95608-181">Configurer une sortie de fonction hello de manière hello suivante :</span><span class="sxs-lookup"><span data-stu-id="95608-181">Configure an output of hello function by doing hello following:</span></span>

   <span data-ttu-id="95608-182">a.</span><span class="sxs-lookup"><span data-stu-id="95608-182">a.</span></span> <span data-ttu-id="95608-183">Cliquez sur **Intégrer** > **Nouvelle sortie** > **tockage Table Azure** > **Sélectionner**.</span><span class="sxs-lookup"><span data-stu-id="95608-183">Click **Integrate** > **New Output** > **Azure Table Storage** > **Select**.</span></span>

      ![Ajouter une application de fonction de table stockage tooyour Bonjour portail Azure](media\iot-hub-store-data-in-azure-table-storage\4_azure-portal-function-app-add-output-table-storage.png)

   <span data-ttu-id="95608-185">b.</span><span class="sxs-lookup"><span data-stu-id="95608-185">b.</span></span> <span data-ttu-id="95608-186">Entrez les informations nécessaires hello.</span><span class="sxs-lookup"><span data-stu-id="95608-186">Enter hello necessary information.</span></span>

      * <span data-ttu-id="95608-187">**Nom du paramètre table**: utilisez `outputTable`, qui sera utilisée dans hello Azure code de la fonction.</span><span class="sxs-lookup"><span data-stu-id="95608-187">**Table parameter name**: Use `outputTable`, which will be used in hello Azure function's code.</span></span>
      
      * <span data-ttu-id="95608-188">**Nom de la table** : utilisez `deviceData`.</span><span class="sxs-lookup"><span data-stu-id="95608-188">**Table name**: Use `deviceData`.</span></span>

      * <span data-ttu-id="95608-189">**Connexion au compte de stockage** : cliquez sur **Nouveau**, puis sélectionnez ou entrez votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="95608-189">**Storage account connection**: Click **New**, and then select or enter your storage account.</span></span> <span data-ttu-id="95608-190">Si le compte de stockage hello n’est pas affichée, consultez [exigences relatives aux comptes de stockage](https://docs.microsoft.com/azure/azure-functions/functions-create-function-app-portal#storage-account-requirements).</span><span class="sxs-lookup"><span data-stu-id="95608-190">If hello storage account is not displayed, see [Storage account requirements](https://docs.microsoft.com/azure/azure-functions/functions-create-function-app-portal#storage-account-requirements).</span></span>
      
   <span data-ttu-id="95608-191">c.</span><span class="sxs-lookup"><span data-stu-id="95608-191">c.</span></span> <span data-ttu-id="95608-192">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="95608-192">Click **Save**.</span></span>

7. <span data-ttu-id="95608-193">Sous **Déclencheurs**, cliquez sur **Azure Event Hub (eventHubMessages)**.</span><span class="sxs-lookup"><span data-stu-id="95608-193">Under **Triggers**, click **Azure Event Hub (eventHubMessages)**.</span></span>

8. <span data-ttu-id="95608-194">Sous **groupe de consommateurs du Hub d’événements**, entrez le nom hello du groupe de consommateurs hello créé, puis cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="95608-194">Under **Event Hub consumer group**, enter hello name of hello consumer group that you created, and then click **Save**.</span></span>

9. <span data-ttu-id="95608-195">Fonction hello que vous avez créé sur hello gauche, puis cliquez sur **afficher les fichiers** sur hello droite.</span><span class="sxs-lookup"><span data-stu-id="95608-195">Click hello function you've created on hello left and then click **View Files** on hello right.</span></span>

10. <span data-ttu-id="95608-196">Remplacez le code hello dans `index.js` avec les éléments suivants de hello :</span><span class="sxs-lookup"><span data-stu-id="95608-196">Replace hello code in `index.js` with hello following:</span></span>

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

11. <span data-ttu-id="95608-197">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="95608-197">Click **Save**.</span></span>

<span data-ttu-id="95608-198">Vous venez de créer application de fonction hello.</span><span class="sxs-lookup"><span data-stu-id="95608-198">You have now created hello function app.</span></span> <span data-ttu-id="95608-199">Elle stocke les messages reçus par votre hub IoT dans votre Stockage Table.</span><span class="sxs-lookup"><span data-stu-id="95608-199">It stores messages that your IoT hub receives in your table storage.</span></span>

> [!NOTE]
> <span data-ttu-id="95608-200">Vous pouvez utiliser hello **exécuter** bouton tootest hello fonction app.</span><span class="sxs-lookup"><span data-stu-id="95608-200">You can use hello **Run** button tootest hello function app.</span></span> <span data-ttu-id="95608-201">Lorsque vous cliquez sur **exécuter**, hello test envoyé tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="95608-201">When you click **Run**, hello test message is sent tooyour IoT hub.</span></span> <span data-ttu-id="95608-202">arrivée Hello de message de type hello doit déclencher hello fonction application toostart, puis enregistrez stockage de table tooyour hello message.</span><span class="sxs-lookup"><span data-stu-id="95608-202">hello arrival of hello message should trigger hello function app toostart and then save hello message tooyour table storage.</span></span> <span data-ttu-id="95608-203">Hello **journaux** volet enregistre des détails de hello du processus de hello.</span><span class="sxs-lookup"><span data-stu-id="95608-203">hello **Logs** pane records hello details of hello process.</span></span>

## <a name="verify-your-message-in-your-table-storage"></a><span data-ttu-id="95608-204">Vérifier votre message dans votre stockage de table</span><span class="sxs-lookup"><span data-stu-id="95608-204">Verify your message in your table storage</span></span>

1. <span data-ttu-id="95608-205">Exécuter l’exemple d’application hello sur votre concentrateur de périphérique toosend messages tooyour IoT.</span><span class="sxs-lookup"><span data-stu-id="95608-205">Run hello sample application on your device toosend messages tooyour IoT hub.</span></span>

2. <span data-ttu-id="95608-206">[Téléchargez et installez l’Explorateur de Stockage Azure](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="95608-206">[Download and install Azure Storage Explorer](http://storageexplorer.com/).</span></span>

3. <span data-ttu-id="95608-207">Ouvrez l’Explorateur de stockage, cliquez sur **ajouter un compte Azure** > **connecter**, puis connectez-vous à tooyour compte Azure.</span><span class="sxs-lookup"><span data-stu-id="95608-207">Open Storage Explorer, click **Add an Azure Account** > **Sign in**, and then sign in tooyour Azure account.</span></span>

4. <span data-ttu-id="95608-208">Cliquez sur votre abonnement Azure > **Comptes de stockage** > votre compte de stockage > **Tables** > **deviceData**.</span><span class="sxs-lookup"><span data-stu-id="95608-208">Click your Azure subscription > **Storage Accounts** > your storage account > **Tables** > **deviceData**.</span></span>

   <span data-ttu-id="95608-209">Vous devez voir les messages envoyés à partir de votre hub IoT de tooyour périphérique connecté hello `deviceData` table.</span><span class="sxs-lookup"><span data-stu-id="95608-209">You should see messages sent from your device tooyour IoT hub logged in hello `deviceData` table.</span></span>

## <a name="next-steps"></a><span data-ttu-id="95608-210">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="95608-210">Next steps</span></span>

<span data-ttu-id="95608-211">Vous avez créé votre compte de stockage Azure et votre application de fonction Azure, qui stocke les messages reçus par votre hub IoT dans votre Stockage Table Azure.</span><span class="sxs-lookup"><span data-stu-id="95608-211">You’ve successfully created your Azure storage account and Azure function app, which stores messages that your IoT hub receives in your table storage.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
