---
title: "Enregistrer des messages IoT Hub dans le stockage de données Azure | Microsoft Docs"
description: "Utilisez une application de fonction Azure pour enregistrer les messages de votre hub IoT dans un Stockage Table Azure. Les messages IoT Hub contiennent des informations, notamment des données de capteurs, envoyées par l’appareil IoT."
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
ms.openlocfilehash: 06503f9564e00ef62587d02f2da4778974e246c5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="save-iot-hub-messages-that-contain-sensor-data-to-your-azure-table-storage"></a><span data-ttu-id="853e3-105">Enregistrer les messages IoT Hub qui contiennent des données de capteurs dans un Stockage Table Azure</span><span class="sxs-lookup"><span data-stu-id="853e3-105">Save IoT hub messages that contain sensor data to your Azure table storage</span></span>

![Diagramme de bout en bout](media/iot-hub-get-started-e2e-diagram/3.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

## <a name="what-you-learn"></a><span data-ttu-id="853e3-107">Contenu</span><span class="sxs-lookup"><span data-stu-id="853e3-107">What you learn</span></span>

<span data-ttu-id="853e3-108">Vous allez découvrir comment créer un compte de stockage Azure et une application de fonction Azure pour stocker des messages IoT Hub dans votre Stockage Table.</span><span class="sxs-lookup"><span data-stu-id="853e3-108">You learn how to create an Azure storage account and an Azure function app to store IoT hub messages in your table storage.</span></span>

## <a name="what-you-do"></a><span data-ttu-id="853e3-109">Procédure</span><span class="sxs-lookup"><span data-stu-id="853e3-109">What you do</span></span>

- <span data-ttu-id="853e3-110">Créez un compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="853e3-110">Create an Azure storage account.</span></span>
- <span data-ttu-id="853e3-111">Préparez la connexion de votre hub IoT à lire des messages.</span><span class="sxs-lookup"><span data-stu-id="853e3-111">Prepare your IoT hub connection to read messages.</span></span>
- <span data-ttu-id="853e3-112">Créez et déployez une application de fonction Azure.</span><span class="sxs-lookup"><span data-stu-id="853e3-112">Create and deploy an Azure function app.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="853e3-113">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="853e3-113">What you need</span></span>

- <span data-ttu-id="853e3-114">[Configurez votre appareil](iot-hub-raspberry-pi-kit-node-get-started.md) de façon à couvrir les exigences suivantes :</span><span class="sxs-lookup"><span data-stu-id="853e3-114">[Set up your device](iot-hub-raspberry-pi-kit-node-get-started.md) to cover the following requirements:</span></span>
  - <span data-ttu-id="853e3-115">Un abonnement Azure actif</span><span class="sxs-lookup"><span data-stu-id="853e3-115">An active Azure subscription</span></span>
  - <span data-ttu-id="853e3-116">Un hub IoT associé à votre abonnement</span><span class="sxs-lookup"><span data-stu-id="853e3-116">An IoT hub under your subscription</span></span> 
  - <span data-ttu-id="853e3-117">Une application fonctionnelle qui envoie des messages à votre hub IoT</span><span class="sxs-lookup"><span data-stu-id="853e3-117">A running application that sends messages to your IoT hub</span></span>

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="853e3-118">Création d'un compte de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="853e3-118">Create an Azure storage account</span></span>

1. <span data-ttu-id="853e3-119">Sur le [Portail Azure](https://portal.azure.com/), cliquez sur **Nouveau** > **Stockage** > **Compte de stockage** > **Créer**.</span><span class="sxs-lookup"><span data-stu-id="853e3-119">In the [Azure portal](https://portal.azure.com/), click **New** > **Storage** > **Storage account** > **Create**.</span></span>

2. <span data-ttu-id="853e3-120">Entrez les informations nécessaires sur le compte de stockage :</span><span class="sxs-lookup"><span data-stu-id="853e3-120">Enter the necessary information for the storage account:</span></span>

   ![Créer un compte de stockage sur le Portail Azure](media\iot-hub-store-data-in-azure-table-storage\1_azure-portal-create-storage-account.png)

   * <span data-ttu-id="853e3-122">**Name** : nom du compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="853e3-122">**Name**: The name of the storage account.</span></span> <span data-ttu-id="853e3-123">Le nom doit être globalement unique.</span><span class="sxs-lookup"><span data-stu-id="853e3-123">The name must be globally unique.</span></span>

   * <span data-ttu-id="853e3-124">**Groupe de ressources** : utilisez le même groupe de ressources que celui de votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="853e3-124">**Resource group**: Use the same resource group that your IoT hub uses.</span></span>

   * <span data-ttu-id="853e3-125">**Épingler au tableau de bord** : Sélectionnez cette option pour pouvoir accéder facilement à votre instance IoT Hub à partir du tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="853e3-125">**Pin to dashboard**: Select this option for easy access to your IoT hub from the dashboard.</span></span>

3. <span data-ttu-id="853e3-126">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="853e3-126">Click **Create**.</span></span>

## <a name="prepare-your-iot-hub-connection-to-read-messages"></a><span data-ttu-id="853e3-127">Préparer une connexion IoT à lire des messages</span><span class="sxs-lookup"><span data-stu-id="853e3-127">Prepare your IoT hub connection to read messages</span></span>

<span data-ttu-id="853e3-128">IoT Hub expose un point de terminaison intégré compatible avec Event Hub pour permettre aux applications de lire les messages IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="853e3-128">IoT hub exposes a built-in event hub-compatible endpoint to enable applications to read IoT hub messages.</span></span> <span data-ttu-id="853e3-129">Dans le même temps, les applications utilisent des groupes de consommateurs pour lire les données provenant du hub IoT.</span><span class="sxs-lookup"><span data-stu-id="853e3-129">Meanwhile, applications use consumer groups to read data from your IoT hub.</span></span> <span data-ttu-id="853e3-130">Avant de créer une application de fonction Azure pour lire les données provenant de votre hub IoT, effectuez les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="853e3-130">Before you create an Azure function app to read data from your IoT hub, do the following:</span></span>

- <span data-ttu-id="853e3-131">Obtenir la chaîne de connexion du point de terminaison de votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="853e3-131">Get the connection string of your IoT hub endpoint.</span></span>
- <span data-ttu-id="853e3-132">Créer un groupe de consommateurs pour votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="853e3-132">Create a consumer group for your IoT hub.</span></span>

### <a name="get-the-connection-string-of-your-iot-hub-endpoint"></a><span data-ttu-id="853e3-133">Obtenir la chaîne de connexion du point de terminaison de votre IoT Hub</span><span class="sxs-lookup"><span data-stu-id="853e3-133">Get the connection string of your IoT hub endpoint</span></span>

1. <span data-ttu-id="853e3-134">Ouvrez votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="853e3-134">Open your IoT hub.</span></span>

2. <span data-ttu-id="853e3-135">Dans le volet **IoT Hub**, sous **Messagerie**, cliquez sur **Points de terminaison**.</span><span class="sxs-lookup"><span data-stu-id="853e3-135">On the **IoT Hub** pane, under **Messaging**, click **Endpoints**.</span></span>

3. <span data-ttu-id="853e3-136">Dans le volet de droite, sous **Points de terminaison intégrés**, cliquez sur **Événements**.</span><span class="sxs-lookup"><span data-stu-id="853e3-136">In the right pane, under **Built-in endpoints**, click **Events**.</span></span>

4. <span data-ttu-id="853e3-137">Dans le volet **Propriétés**, notez les valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="853e3-137">In the **Properties** pane, note the following values:</span></span>
   - <span data-ttu-id="853e3-138">Point de terminaison compatible avec Event Hub</span><span class="sxs-lookup"><span data-stu-id="853e3-138">Event hub-compatible endpoint</span></span>
   - <span data-ttu-id="853e3-139">Nom compatible avec Event Hub</span><span class="sxs-lookup"><span data-stu-id="853e3-139">Event hub-compatible name</span></span>

   ![Obtenir la chaîne de connexion du point de terminaison de votre IoT Hub dans le portail Azure](media\iot-hub-store-data-in-azure-table-storage\2_azure-portal-iot-hub-endpoint-connection-string.png)

5. <span data-ttu-id="853e3-141">Dans le volet **IoT Hub**, sous **Paramètres**, cliquez sur **Stratégies d’accès partagé**.</span><span class="sxs-lookup"><span data-stu-id="853e3-141">In the **IoT Hub** pane, under **Settings**, click **Shared access policies**.</span></span>

6. <span data-ttu-id="853e3-142">Cliquez sur **iothubowner**.</span><span class="sxs-lookup"><span data-stu-id="853e3-142">Click **iothubowner**.</span></span>

7. <span data-ttu-id="853e3-143">Notez la valeur **Primary key**.</span><span class="sxs-lookup"><span data-stu-id="853e3-143">Note the **Primary key** value.</span></span>

8. <span data-ttu-id="853e3-144">Créez la chaîne de connexion du point de terminaison de votre hub IoT, de la façon suivante :</span><span class="sxs-lookup"><span data-stu-id="853e3-144">Create the connection string of your IoT hub endpoint as follows:</span></span>

   `Endpoint=<Event Hub-compatible endpoint>;SharedAccessKeyName=iothubowner;SharedAccessKey=<Primary key>`

   > [!NOTE]
   > <span data-ttu-id="853e3-145">Remplacez `<Event Hub-compatible endpoint>` et `<Primary key>` par les valeurs que vous avez notées précédemment.</span><span class="sxs-lookup"><span data-stu-id="853e3-145">Replace `<Event Hub-compatible endpoint>` and `<Primary key>` with the values that you noted earlier.</span></span>

### <a name="create-a-consumer-group-for-your-iot-hub"></a><span data-ttu-id="853e3-146">Créer un groupe de consommateurs pour votre IoT Hub</span><span class="sxs-lookup"><span data-stu-id="853e3-146">Create a consumer group for your IoT hub</span></span>

1. <span data-ttu-id="853e3-147">Ouvrez votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="853e3-147">Open your IoT hub.</span></span>

2. <span data-ttu-id="853e3-148">Dans le volet **IoT Hub**, sous **Messagerie**, cliquez sur **Points de terminaison**.</span><span class="sxs-lookup"><span data-stu-id="853e3-148">In the **IoT Hub** pane, under **Messaging**, click **Endpoints**.</span></span>

3. <span data-ttu-id="853e3-149">Dans le volet de droite, sous **Points de terminaison intégrés**, cliquez sur **Événements**.</span><span class="sxs-lookup"><span data-stu-id="853e3-149">In the right pane, under **Built-in endpoints**, click **Events**.</span></span>

4. <span data-ttu-id="853e3-150">Dans le volet **Propriétés**, sous **Groupes de consommateurs**, entrez un nom et prenez-en note.</span><span class="sxs-lookup"><span data-stu-id="853e3-150">In the **Properties** pane, under **Consumer groups**, enter a name, and then make a note of it.</span></span>

5. <span data-ttu-id="853e3-151">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="853e3-151">Click **Save**.</span></span>

## <a name="create-and-deploy-an-azure-function-app"></a><span data-ttu-id="853e3-152">Créer et déployer une application de fonction Azure</span><span class="sxs-lookup"><span data-stu-id="853e3-152">Create and deploy an Azure function app</span></span>

1. <span data-ttu-id="853e3-153">Sur le [Portail Azure](https://portal.azure.com/), cliquez sur **Nouveau** > **Compute** > **Function App** > **Créer**.</span><span class="sxs-lookup"><span data-stu-id="853e3-153">In the [Azure portal](https://portal.azure.com/), click **New** > **Compute** > **Function App** > **Create**.</span></span>

2. <span data-ttu-id="853e3-154">Entrez les informations nécessaires sur l’application de fonction.</span><span class="sxs-lookup"><span data-stu-id="853e3-154">Enter the necessary information for the function app.</span></span>

   ![Créer une application de fonction sur le Portail Azure](media\iot-hub-store-data-in-azure-table-storage\3_azure-portal-create-function-app.png)

   * <span data-ttu-id="853e3-156">**Nom de l’application** : nom de l’application de fonction.</span><span class="sxs-lookup"><span data-stu-id="853e3-156">**App name**: The name of the function app.</span></span> <span data-ttu-id="853e3-157">Le nom doit être globalement unique.</span><span class="sxs-lookup"><span data-stu-id="853e3-157">The name must be globally unique.</span></span>

   * <span data-ttu-id="853e3-158">**Groupe de ressources** : utilisez le même groupe de ressources que celui de votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="853e3-158">**Resource group**: Use the same resource group that your IoT hub uses.</span></span>

   * <span data-ttu-id="853e3-159">**Compte de stockage** : nom du compte de stockage que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="853e3-159">**Storage Account**: The storage account that you created.</span></span>

   * <span data-ttu-id="853e3-160">**Épingler au tableau de bord** : cochez cette option pour pouvoir accéder facilement à l’application de fonction à partir du tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="853e3-160">**Pin to dashboard**: Check this option for easy access to the function app from the dashboard.</span></span>

3. <span data-ttu-id="853e3-161">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="853e3-161">Click **Create**.</span></span>

4. <span data-ttu-id="853e3-162">Une fois l’application de fonction créée, ouvrez-la.</span><span class="sxs-lookup"><span data-stu-id="853e3-162">After the function app has been created, open it.</span></span>

5. <span data-ttu-id="853e3-163">Dans l’application de fonction, créez une fonction de la façon suivante :</span><span class="sxs-lookup"><span data-stu-id="853e3-163">In the function app, create a new function by doing the following:</span></span>

   <span data-ttu-id="853e3-164">a.</span><span class="sxs-lookup"><span data-stu-id="853e3-164">a.</span></span> <span data-ttu-id="853e3-165">Cliquez sur **Nouvelle fonction**.</span><span class="sxs-lookup"><span data-stu-id="853e3-165">Click **New Function**.</span></span>

   <span data-ttu-id="853e3-166">b.</span><span class="sxs-lookup"><span data-stu-id="853e3-166">b.</span></span> <span data-ttu-id="853e3-167">Sélectionnez **JavaScript** pour **Langage** et **Data Processing** (Traitement de données) pour **Scénario**.</span><span class="sxs-lookup"><span data-stu-id="853e3-167">Select **JavaScript** for **Language**, and **Data Processing** for **Scenario**.</span></span>

   <span data-ttu-id="853e3-168">c.</span><span class="sxs-lookup"><span data-stu-id="853e3-168">c.</span></span> <span data-ttu-id="853e3-169">Cliquez sur **Créer cette fonction**, puis sur **Nouvelle fonction**.</span><span class="sxs-lookup"><span data-stu-id="853e3-169">Click **Create this function**, and then click **New Function**.</span></span>

   <span data-ttu-id="853e3-170">d.</span><span class="sxs-lookup"><span data-stu-id="853e3-170">d.</span></span> <span data-ttu-id="853e3-171">Sélectionnez **JavaScript** comme langage et **Traitement de données** comme scénario.</span><span class="sxs-lookup"><span data-stu-id="853e3-171">Select **JavaScript** for the language, and **Data Processing** for the scenario.</span></span>

   <span data-ttu-id="853e3-172">e.</span><span class="sxs-lookup"><span data-stu-id="853e3-172">e.</span></span> <span data-ttu-id="853e3-173">Cliquez sur le modèle **EventHubTrigger-JavaScript**.</span><span class="sxs-lookup"><span data-stu-id="853e3-173">Click the **EventHubTrigger-JavaScript** template.</span></span>

   <span data-ttu-id="853e3-174">f.</span><span class="sxs-lookup"><span data-stu-id="853e3-174">f.</span></span> <span data-ttu-id="853e3-175">Entrez les informations nécessaires pour le modèle.</span><span class="sxs-lookup"><span data-stu-id="853e3-175">Enter the necessary information for the template.</span></span>

      * <span data-ttu-id="853e3-176">**Nommez votre fonction** : nom de la fonction.</span><span class="sxs-lookup"><span data-stu-id="853e3-176">**Name your function**: The name of the function.</span></span>

      * <span data-ttu-id="853e3-177">**Nom du hub d’événements** : nom compatible avec Event Hub que vous avez noté précédemment.</span><span class="sxs-lookup"><span data-stu-id="853e3-177">**Event Hub name**: The event hub-compatible name that you noted earlier.</span></span>

      * <span data-ttu-id="853e3-178">**Connexion Event Hub** : pour ajouter la chaîne de connexion du point de terminaison de votre hub IoT que vous avez créée, cliquez sur **Nouveau**.</span><span class="sxs-lookup"><span data-stu-id="853e3-178">**Event Hub connection**: To add the connection string of the IoT hub endpoint that you created, click **New**.</span></span>

   <span data-ttu-id="853e3-179">g.</span><span class="sxs-lookup"><span data-stu-id="853e3-179">g.</span></span> <span data-ttu-id="853e3-180">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="853e3-180">Click **Create**.</span></span>

6. <span data-ttu-id="853e3-181">Configurez une sortie de la fonction de la façon suivante :</span><span class="sxs-lookup"><span data-stu-id="853e3-181">Configure an output of the function by doing the following:</span></span>

   <span data-ttu-id="853e3-182">a.</span><span class="sxs-lookup"><span data-stu-id="853e3-182">a.</span></span> <span data-ttu-id="853e3-183">Cliquez sur **Intégrer** > **Nouvelle sortie** > **tockage Table Azure** > **Sélectionner**.</span><span class="sxs-lookup"><span data-stu-id="853e3-183">Click **Integrate** > **New Output** > **Azure Table Storage** > **Select**.</span></span>

      ![Ajouter un Stockage Table à une application de fonction sur le Portail Azure](media\iot-hub-store-data-in-azure-table-storage\4_azure-portal-function-app-add-output-table-storage.png)

   <span data-ttu-id="853e3-185">b.</span><span class="sxs-lookup"><span data-stu-id="853e3-185">b.</span></span> <span data-ttu-id="853e3-186">Entrez les informations nécessaires.</span><span class="sxs-lookup"><span data-stu-id="853e3-186">Enter the necessary information.</span></span>

      * <span data-ttu-id="853e3-187">**Nom du paramètre de table** : choisissez `outputTable`, qui sera utilisé dans le code de la fonction Azure.</span><span class="sxs-lookup"><span data-stu-id="853e3-187">**Table parameter name**: Use `outputTable`, which will be used in the Azure function's code.</span></span>
      
      * <span data-ttu-id="853e3-188">**Nom de la table** : utilisez `deviceData`.</span><span class="sxs-lookup"><span data-stu-id="853e3-188">**Table name**: Use `deviceData`.</span></span>

      * <span data-ttu-id="853e3-189">**Connexion au compte de stockage** : cliquez sur **Nouveau**, puis sélectionnez ou entrez votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="853e3-189">**Storage account connection**: Click **New**, and then select or enter your storage account.</span></span> <span data-ttu-id="853e3-190">Si le compte de stockage ne s’affiche pas, consultez la page [Exigences relatives aux comptes de stockage](https://docs.microsoft.com/azure/azure-functions/functions-create-function-app-portal#storage-account-requirements).</span><span class="sxs-lookup"><span data-stu-id="853e3-190">If the storage account is not displayed, see [Storage account requirements](https://docs.microsoft.com/azure/azure-functions/functions-create-function-app-portal#storage-account-requirements).</span></span>
      
   <span data-ttu-id="853e3-191">c.</span><span class="sxs-lookup"><span data-stu-id="853e3-191">c.</span></span> <span data-ttu-id="853e3-192">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="853e3-192">Click **Save**.</span></span>

7. <span data-ttu-id="853e3-193">Sous **Déclencheurs**, cliquez sur **Azure Event Hub (eventHubMessages)**.</span><span class="sxs-lookup"><span data-stu-id="853e3-193">Under **Triggers**, click **Azure Event Hub (eventHubMessages)**.</span></span>

8. <span data-ttu-id="853e3-194">Sous **Groupe de consommateurs du hub d’événements**, entrez le nom du groupe de consommateurs créé précédemment, puis cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="853e3-194">Under **Event Hub consumer group**, enter the name of the consumer group that you created, and then click **Save**.</span></span>

9. <span data-ttu-id="853e3-195">Cliquez sur la fonction que vous avez créée sur la gauche, puis sur **Afficher les fichiers** sur la droite.</span><span class="sxs-lookup"><span data-stu-id="853e3-195">Click the function you've created on the left and then click **View Files** on the right.</span></span>

10. <span data-ttu-id="853e3-196">Remplacez le code de `index.js` par le suivant :</span><span class="sxs-lookup"><span data-stu-id="853e3-196">Replace the code in `index.js` with the following:</span></span>

   ```javascript
   'use strict';

   // This function is triggered each time a message is received in the IoT hub.
   // The message payload is persisted in an Azure storage table
 
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

11. <span data-ttu-id="853e3-197">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="853e3-197">Click **Save**.</span></span>

<span data-ttu-id="853e3-198">Vous avez à présent créé l’application de fonction.</span><span class="sxs-lookup"><span data-stu-id="853e3-198">You have now created the function app.</span></span> <span data-ttu-id="853e3-199">Elle stocke les messages reçus par votre hub IoT dans votre Stockage Table.</span><span class="sxs-lookup"><span data-stu-id="853e3-199">It stores messages that your IoT hub receives in your table storage.</span></span>

> [!NOTE]
> <span data-ttu-id="853e3-200">Vous pouvez utiliser le bouton **Exécuter** pour tester l’application de fonction.</span><span class="sxs-lookup"><span data-stu-id="853e3-200">You can use the **Run** button to test the function app.</span></span> <span data-ttu-id="853e3-201">Lorsque vous cliquez sur **Exécuter**, le message de test est envoyé à votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="853e3-201">When you click **Run**, the test message is sent to your IoT hub.</span></span> <span data-ttu-id="853e3-202">À l’arrivée du message, l’application de fonction devrait démarrer, puis enregistrer le message dans votre Stockage Table.</span><span class="sxs-lookup"><span data-stu-id="853e3-202">The arrival of the message should trigger the function app to start and then save the message to your table storage.</span></span> <span data-ttu-id="853e3-203">Le volet **Journaux** enregistre les détails du processus.</span><span class="sxs-lookup"><span data-stu-id="853e3-203">The **Logs** pane records the details of the process.</span></span>

## <a name="verify-your-message-in-your-table-storage"></a><span data-ttu-id="853e3-204">Vérifier votre message dans votre stockage de table</span><span class="sxs-lookup"><span data-stu-id="853e3-204">Verify your message in your table storage</span></span>

1. <span data-ttu-id="853e3-205">Exécutez l’exemple d’application sur votre appareil pour envoyer des messages à votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="853e3-205">Run the sample application on your device to send messages to your IoT hub.</span></span>

2. <span data-ttu-id="853e3-206">[Téléchargez et installez l’Explorateur de Stockage Azure](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="853e3-206">[Download and install Azure Storage Explorer](http://storageexplorer.com/).</span></span>

3. <span data-ttu-id="853e3-207">Ouvrez l’Explorateur de Stockage, cliquez sur **Ajouter un compte Azure** > **Se connecter**, puis connectez-vous à votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="853e3-207">Open Storage Explorer, click **Add an Azure Account** > **Sign in**, and then sign in to your Azure account.</span></span>

4. <span data-ttu-id="853e3-208">Cliquez sur votre abonnement Azure > **Comptes de stockage** > votre compte de stockage > **Tables** > **deviceData**.</span><span class="sxs-lookup"><span data-stu-id="853e3-208">Click your Azure subscription > **Storage Accounts** > your storage account > **Tables** > **deviceData**.</span></span>

   <span data-ttu-id="853e3-209">Vous devriez voir les messages envoyés par votre appareil à votre IoT Hub consigné dans la table `deviceData`.</span><span class="sxs-lookup"><span data-stu-id="853e3-209">You should see messages sent from your device to your IoT hub logged in the `deviceData` table.</span></span>

## <a name="next-steps"></a><span data-ttu-id="853e3-210">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="853e3-210">Next steps</span></span>

<span data-ttu-id="853e3-211">Vous avez créé votre compte de stockage Azure et votre application de fonction Azure, qui stocke les messages reçus par votre hub IoT dans votre Stockage Table Azure.</span><span class="sxs-lookup"><span data-stu-id="853e3-211">You’ve successfully created your Azure storage account and Azure function app, which stores messages that your IoT hub receives in your table storage.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
