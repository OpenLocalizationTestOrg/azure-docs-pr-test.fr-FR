---
title: "Surveillance à distance IoT et notifications avec Azure Logic Apps | Microsoft Docs"
description: "Utilisez Azure Logic Apps pour surveiller la température IoT sur votre hub IoT et envoyer automatiquement des notifications par courrier électronique dans votre boîte aux lettres en cas de détection d’anomalies."
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
ms.openlocfilehash: 7a611912ae55eb22103539dbba9f1a06aaa543b7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="iot-remote-monitoring-and-notifications-with-azure-logic-apps-connecting-your-iot-hub-and-mailbox"></a><span data-ttu-id="6756b-104">Surveillance à distance IoT et notifications avec Azure Logic Apps connectant votre IoT Hub et votre boîte aux lettres</span><span class="sxs-lookup"><span data-stu-id="6756b-104">IoT remote monitoring and notifications with Azure Logic Apps connecting your IoT hub and mailbox</span></span>

![Diagramme de bout en bout](media/iot-hub-get-started-e2e-diagram/7.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

<span data-ttu-id="6756b-106">Azure Logic Apps permet d’automatiser des processus comme une série d’étapes.</span><span class="sxs-lookup"><span data-stu-id="6756b-106">Azure Logic Apps provides a way to automate processes as a series of steps.</span></span> <span data-ttu-id="6756b-107">Une application logique peut établir une connexion via divers services et protocoles.</span><span class="sxs-lookup"><span data-stu-id="6756b-107">A logic app can connect across various services and protocols.</span></span> <span data-ttu-id="6756b-108">Elle commence par un déclencheur tel que « Lorsqu’un compte est ajouté », suivie d’une combinaison d’actions, similaire à « envoi d’une notification Push ».</span><span class="sxs-lookup"><span data-stu-id="6756b-108">It begins with a trigger such as 'When an account is added', and followed by a combination of actions, one like 'sending a push notification'.</span></span> <span data-ttu-id="6756b-109">Cette fonctionnalité rend Logic Apps idéale pour la surveillance IoT, telle que la vigilance face aux anomalies, parmi d’autres scénarios d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="6756b-109">This feature makes Logic Apps a perfect IoT solution for IoT monitoring, such as staying alert for anomalies, among other usage scenarios.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="6756b-110">Contenu</span><span class="sxs-lookup"><span data-stu-id="6756b-110">What you learn</span></span>

<span data-ttu-id="6756b-111">Vous apprenez à créer une application logique qui connecte votre IoT Hub et votre boîte aux lettres pour la surveillance de la température et les notifications.</span><span class="sxs-lookup"><span data-stu-id="6756b-111">You learn how to create a logic app that connects your IoT hub and your mailbox for temperature monitoring and notifications.</span></span> <span data-ttu-id="6756b-112">Lorsque la température est supérieure à 30 °C, l’application cliente indique `temperatureAlert = "true"` dans le message qu’elle envoie à votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="6756b-112">When the temperature is above 30 C, the client application marks `temperatureAlert = "true"` in the message it sends to your IoT hub.</span></span> <span data-ttu-id="6756b-113">Suite à ce message, l’application logique vous envoie un e-mail de notification.</span><span class="sxs-lookup"><span data-stu-id="6756b-113">The message triggers the logic app to send you an email notification.</span></span>

## <a name="what-you-do"></a><span data-ttu-id="6756b-114">Procédure</span><span class="sxs-lookup"><span data-stu-id="6756b-114">What you do</span></span>

* <span data-ttu-id="6756b-115">Créez un espace de noms Service Bus et ajoutez-lui une file d’attente.</span><span class="sxs-lookup"><span data-stu-id="6756b-115">Create a service bus namespace and add a queue to it.</span></span>
* <span data-ttu-id="6756b-116">Ajoutez un point de terminaison et une règle de routage à votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="6756b-116">Add an endpoint and a routing rule to your IoT hub.</span></span>
* <span data-ttu-id="6756b-117">Créez, configurez et testez une application logique.</span><span class="sxs-lookup"><span data-stu-id="6756b-117">Create, configure, and test a logic app.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="6756b-118">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="6756b-118">What you need</span></span>

* <span data-ttu-id="6756b-119">Le didacticiel [Configurer votre appareil](iot-hub-raspberry-pi-kit-node-get-started.md) terminé, qui traite des exigences suivantes :</span><span class="sxs-lookup"><span data-stu-id="6756b-119">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers the following requirements:</span></span>
  * <span data-ttu-id="6756b-120">Un abonnement Azure actif.</span><span class="sxs-lookup"><span data-stu-id="6756b-120">An active Azure subscription.</span></span>
  * <span data-ttu-id="6756b-121">Une instance Azure IoT Hub associée à votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="6756b-121">An Azure IoT hub under your subscription.</span></span>
  * <span data-ttu-id="6756b-122">Une application cliente qui envoie des messages à votre instance Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="6756b-122">A client application that sends messages to your Azure IoT hub.</span></span>

## <a name="create-service-bus-namespace-and-add-a-queue-to-it"></a><span data-ttu-id="6756b-123">Créer un espace de noms Service Bus et lui ajouter une file d’attente</span><span class="sxs-lookup"><span data-stu-id="6756b-123">Create service bus namespace and add a queue to it</span></span>

### <a name="create-a-service-bus-namespace"></a><span data-ttu-id="6756b-124">Création d'un espace de noms Service Bus</span><span class="sxs-lookup"><span data-stu-id="6756b-124">Create a service bus namespace</span></span>

1. <span data-ttu-id="6756b-125">Sur le [portail Azure](https://portal.azure.com/), cliquez sur **Nouveau** > **Enterprise Integration** > **Service Bus**.</span><span class="sxs-lookup"><span data-stu-id="6756b-125">On the [Azure portal](https://portal.azure.com/), click **New** > **Enterprise Integration** > **Service Bus**.</span></span>
1. <span data-ttu-id="6756b-126">Fournissez les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="6756b-126">Provide the following information:</span></span>

   <span data-ttu-id="6756b-127">**Nom** : le nom du Service Bus.</span><span class="sxs-lookup"><span data-stu-id="6756b-127">**Name**: The name of the service bus.</span></span>

   <span data-ttu-id="6756b-128">**Niveau tarifaire**: cliquez sur **De base** > **Sélectionnez**.</span><span class="sxs-lookup"><span data-stu-id="6756b-128">**Pricing tier**: Click **Basic** > **Select**.</span></span> <span data-ttu-id="6756b-129">Le niveau de base est suffisant pour ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="6756b-129">The Basic tier is sufficient for this tutorial.</span></span>

   <span data-ttu-id="6756b-130">**Groupe de ressources** : utilisez le groupe de ressources que votre instance IoT Hub exploite.</span><span class="sxs-lookup"><span data-stu-id="6756b-130">**Resource group**: Use the same resource group that your IoT hub uses.</span></span>

   <span data-ttu-id="6756b-131">**Emplacement** : utilisez le même emplacement que celui utilisé par votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="6756b-131">**Location**: Use the same location that your IoT hub uses.</span></span>
1. <span data-ttu-id="6756b-132">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="6756b-132">Click **Create**.</span></span>

   ![Créer un espace de noms Service Bus dans le portail Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/1_create-service-bus-namespace-azure-portal.png)

### <a name="add-a-service-bus-queue"></a><span data-ttu-id="6756b-134">Ajouter une file d’attente Service Bus</span><span class="sxs-lookup"><span data-stu-id="6756b-134">Add a service bus queue</span></span>

1. <span data-ttu-id="6756b-135">Ouvrez l’espace de noms Service Bus, puis cliquez sur **+ file d’attente**.</span><span class="sxs-lookup"><span data-stu-id="6756b-135">Open the service bus namespace, and then click **+ Queue**.</span></span>
1. <span data-ttu-id="6756b-136">Entrez un nom pour la file d’attente, puis cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="6756b-136">Enter a name for the queue and then click **Create**.</span></span>
1. <span data-ttu-id="6756b-137">Ouvrez la file d’attente Service Bus, puis cliquez sur **Stratégies d’accès partagé** > **+ Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="6756b-137">Open the service bus queue, and then click **Shared access policies** > **+ Add**.</span></span>
1. <span data-ttu-id="6756b-138">Entrez un nom pour la stratégie, cochez **Gérer**, puis cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="6756b-138">Enter a name for the policy, check **Manage**, and then click **Create**.</span></span>

   ![Ajouter une file d’attente Service Bus dans le portail Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/2_add-service-bus-queue-azure-portal.png)

## <a name="add-an-endpoint-and-a-routing-rule-to-your-iot-hub"></a><span data-ttu-id="6756b-140">Ajouter un point de terminaison et une règle de routage à votre IoT Hub</span><span class="sxs-lookup"><span data-stu-id="6756b-140">Add an endpoint and a routing rule to your IoT hub</span></span>

### <a name="add-an-endpoint"></a><span data-ttu-id="6756b-141">Ajout d’un point de terminaison</span><span class="sxs-lookup"><span data-stu-id="6756b-141">Add an endpoint</span></span>

1. <span data-ttu-id="6756b-142">Ouvrez votre IoT Hub et cliquez sur Points de terminaison > + Ajouter.</span><span class="sxs-lookup"><span data-stu-id="6756b-142">Open your IoT hub, click Endpoints > + Add.</span></span>
1. <span data-ttu-id="6756b-143">Entrez les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="6756b-143">Enter the following information:</span></span>

   <span data-ttu-id="6756b-144">**Nom** : le nom du point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="6756b-144">**Name**: The name of the endpoint.</span></span>

   <span data-ttu-id="6756b-145">**Type de point de terminaison** : sélectionnez **File d’attente Service Bus**.</span><span class="sxs-lookup"><span data-stu-id="6756b-145">**Endpoint type**: Select **Service Bus Queue**.</span></span>

   <span data-ttu-id="6756b-146">**Espace de noms Service Bus** : sélectionnez l’espace de noms que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="6756b-146">**Service Bus namespace**: Select the namespace you created.</span></span>

   <span data-ttu-id="6756b-147">**File d’attente Service Bus** : sélectionnez la file d’attente que vous avez créée.</span><span class="sxs-lookup"><span data-stu-id="6756b-147">**Service Bus queue**: Select the queue you created.</span></span>
1. <span data-ttu-id="6756b-148">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="6756b-148">Click **OK**.</span></span>

   ![Ajouter un point de terminaison à votre IoT Hub dans le portail Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/3_add-iot-hub-endpoint-azure-portal.png)

### <a name="add-a-routing-rule"></a><span data-ttu-id="6756b-150">Ajouter une règle de routage</span><span class="sxs-lookup"><span data-stu-id="6756b-150">Add a routing rule</span></span>

1. <span data-ttu-id="6756b-151">Dans votre Iot Hub, cliquez sur **Itinéraires** > **+ Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="6756b-151">In your IoT hub, click **Routes** > **+ Add**.</span></span>
1. <span data-ttu-id="6756b-152">Entrez les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="6756b-152">Enter the following information:</span></span>

   <span data-ttu-id="6756b-153">**Nom** : le nom de la règle de routage.</span><span class="sxs-lookup"><span data-stu-id="6756b-153">**Name**: The name of the routing rule.</span></span>

   <span data-ttu-id="6756b-154">**Source de données** : sélectionnez **DeviceMessages**.</span><span class="sxs-lookup"><span data-stu-id="6756b-154">**Data source**: Select **DeviceMessages**.</span></span>

   <span data-ttu-id="6756b-155">**Point de terminaison** : sélectionnez le point de terminaison que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="6756b-155">**Endpoint**: Select the endpoint you created.</span></span>

   <span data-ttu-id="6756b-156">**Chaîne de requête** : entrez `temperatureAlert = "true"`.</span><span class="sxs-lookup"><span data-stu-id="6756b-156">**Query string**: Enter `temperatureAlert = "true"`.</span></span>
1. <span data-ttu-id="6756b-157">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="6756b-157">Click **Save**.</span></span>

   ![Ajouter une règle de routage dans le portail Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/4_add-routing-rule-azure-portal.png)

## <a name="create-and-configure-a-logic-app"></a><span data-ttu-id="6756b-159">Créer et configurer une application logique</span><span class="sxs-lookup"><span data-stu-id="6756b-159">Create and configure a logic app</span></span>

### <a name="create-a-logic-app"></a><span data-ttu-id="6756b-160">Créer une application logique</span><span class="sxs-lookup"><span data-stu-id="6756b-160">Create a logic app</span></span>

1. <span data-ttu-id="6756b-161">Dans le [portail Azure](https://portal.azure.com/), cliquez sur **Nouveau** > **Enterprise Integration** > **Application logique**.</span><span class="sxs-lookup"><span data-stu-id="6756b-161">In the [Azure portal](https://portal.azure.com/), click **New** > **Enterprise Integration** > **Logic App**.</span></span>
1. <span data-ttu-id="6756b-162">Entrez les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="6756b-162">Enter the following information:</span></span>

   <span data-ttu-id="6756b-163">**Nome** : le nom de l’application logique.</span><span class="sxs-lookup"><span data-stu-id="6756b-163">**Name**: The name of the logic app.</span></span>

   <span data-ttu-id="6756b-164">**Groupe de ressources** : utilisez le groupe de ressources que votre instance IoT Hub exploite.</span><span class="sxs-lookup"><span data-stu-id="6756b-164">**Resource group**: Use the same resource group that your IoT hub uses.</span></span>

   <span data-ttu-id="6756b-165">**Emplacement** : utilisez le même emplacement que celui utilisé par votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="6756b-165">**Location**: Use the same location that your IoT hub uses.</span></span>
1. <span data-ttu-id="6756b-166">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="6756b-166">Click **Create**.</span></span>

### <a name="configure-the-logic-app"></a><span data-ttu-id="6756b-167">Configurer l’application logique</span><span class="sxs-lookup"><span data-stu-id="6756b-167">Configure the logic app</span></span>

1. <span data-ttu-id="6756b-168">Ouvrez l’application logique qui s’ouvre dans le Concepteur d’applications logiques.</span><span class="sxs-lookup"><span data-stu-id="6756b-168">Open the logic app that opens into the Logic Apps Designer.</span></span>
1. <span data-ttu-id="6756b-169">Dans le Concepteur d’applications logiques, cliquez sur **Application logique vide**.</span><span class="sxs-lookup"><span data-stu-id="6756b-169">In the Logic Apps Designer, click **Blank Logic App**.</span></span>

   ![Commencer avec une application logique vide dans le portail Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/5_start-with-blank-logic-app-azure-portal.png)

1. <span data-ttu-id="6756b-171">Cliquez sur **Service Bus**.</span><span class="sxs-lookup"><span data-stu-id="6756b-171">Click **Service Bus**.</span></span>

   ![Sélectionner Service Bus pour commencer à créer votre application logique dans le portail Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/6_select-service-bus-when-creating-blank-logic-app-azure-portal.png)

1. <span data-ttu-id="6756b-173">Cliquez sur **Service Bus – lorsqu’un ou plusieurs messages arrivent dans une file d’attente (saisie semi-automatique)**.</span><span class="sxs-lookup"><span data-stu-id="6756b-173">Click **Service Bus – When one or more messages arrive in a queue (auto-complete)**.</span></span>
1. <span data-ttu-id="6756b-174">Créez une connexion Service Bus.</span><span class="sxs-lookup"><span data-stu-id="6756b-174">Create a service bus connection.</span></span>
   1. <span data-ttu-id="6756b-175">Entrez un nom de connexion.</span><span class="sxs-lookup"><span data-stu-id="6756b-175">Enter a connection name.</span></span>
   1. <span data-ttu-id="6756b-176">Cliquez sur l’espace de noms Service Bus > la stratégie Service Bus > **Créer**.</span><span class="sxs-lookup"><span data-stu-id="6756b-176">Click the service bus namespace > the service bus policy > **Create**.</span></span>

      ![Créer une connexion Service Bus pour votre application logique dans le portail Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/7_create-service-bus-connection-in-logic-app-azure-portal.png)

   1. <span data-ttu-id="6756b-178">Cliquez sur **Continuer** après avoir créé la connexion Service Bus.</span><span class="sxs-lookup"><span data-stu-id="6756b-178">Click **Continue** after the service bus connection is created.</span></span>
   1. <span data-ttu-id="6756b-179">Sélectionnez la file d’attente que vous avez créée, puis entrez `175` pour **Nombre maximal de messages**</span><span class="sxs-lookup"><span data-stu-id="6756b-179">Select the queue that you created and enter `175` for **Maximum message count**</span></span>

      ![Spécifier le nombre maximal de messages pour les connexions Service Bus dans votre application logique](media/iot-hub-monitoring-notifications-with-azure-logic-apps/8_specify-maximum-message-count-for-service-bus-connection-logic-app-azure-portal.png)
   1. <span data-ttu-id="6756b-181">Cliquez sur le bouton « Enregistrer » pour enregistrer les modifications.</span><span class="sxs-lookup"><span data-stu-id="6756b-181">Click "Save" button to save the changes.</span></span>

1. <span data-ttu-id="6756b-182">Créez une connexion de service SMTP.</span><span class="sxs-lookup"><span data-stu-id="6756b-182">Create an SMTP service connection.</span></span>
   1. <span data-ttu-id="6756b-183">Choisissez **Nouvelle étape** > **Ajouter une action**.</span><span class="sxs-lookup"><span data-stu-id="6756b-183">Click **New step** > **Add an action**.</span></span>
   1. <span data-ttu-id="6756b-184">Entrez `SMTP`, cliquez sur le service **SMTP** dans les résultats de la recherche, puis cliquez sur **SMTP - Envoyer un e-mail**.</span><span class="sxs-lookup"><span data-stu-id="6756b-184">Type `SMTP`, click the **SMTP** service in the search result, and then click **SMTP - Send Email**.</span></span>

      ![Créer une connexion SMTP dans votre application logique dans le portail Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/9_create-smtp-connection-logic-app-azure-portal.png)

   1. <span data-ttu-id="6756b-186">Entrez les informations SMTP de votre boîte aux lettres, puis cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="6756b-186">Enter the SMTP information of your mailbox, and then click **Create**.</span></span>

      ![Entrer les informations de connexion SMTP dans votre application logique dans le portail Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/10_enter-smtp-connection-info-logic-app-azure-portal.png)

      <span data-ttu-id="6756b-188">Obtenez les informations SMTP pour [Hotmail/Outlook.com](https://support.office.com/en-us/article/Add-your-Outlook-com-account-to-another-mail-app-73f3b178-0009-41ae-aab1-87b80fa94970), [Gmail](https://support.google.com/a/answer/176600?hl=en) et [Yahoo Mail](https://help.yahoo.com/kb/SLN4075.html).</span><span class="sxs-lookup"><span data-stu-id="6756b-188">Get the SMTP information for [Hotmail/Outlook.com](https://support.office.com/en-us/article/Add-your-Outlook-com-account-to-another-mail-app-73f3b178-0009-41ae-aab1-87b80fa94970), [Gmail](https://support.google.com/a/answer/176600?hl=en), and [Yahoo Mail](https://help.yahoo.com/kb/SLN4075.html).</span></span>
   1. <span data-ttu-id="6756b-189">Entrez votre adresse de messagerie pour **De** et **À**, et `High temperature detected` pour **Objet** et **Corps**.</span><span class="sxs-lookup"><span data-stu-id="6756b-189">Enter your email address for **From** and **To**, and `High temperature detected` for **Subject** and **Body**.</span></span>
   1. <span data-ttu-id="6756b-190">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="6756b-190">Click **Save**.</span></span>

<span data-ttu-id="6756b-191">L’application logique est en état de marche lorsque vous l’enregistrez.</span><span class="sxs-lookup"><span data-stu-id="6756b-191">The logic app is in working order when you save it.</span></span>

## <a name="test-the-logic-app"></a><span data-ttu-id="6756b-192">Tester l’application logique</span><span class="sxs-lookup"><span data-stu-id="6756b-192">Test the logic app</span></span>

1. <span data-ttu-id="6756b-193">Démarrez l’application cliente que vous déployez sur votre appareil dans [Connecter la carte ESP8266 à Azure IoT Hub](iot-hub-arduino-huzzah-esp8266-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="6756b-193">Start the client application that you deploy to your device in [Connect ESP8266 to Azure IoT Hub](iot-hub-arduino-huzzah-esp8266-get-started.md).</span></span>
1. <span data-ttu-id="6756b-194">Faites en sorte que la température ambiante autour du SensorTag soit supérieure à 30 °C. Par exemple, allumez une bougie à côté de votre SensorTag.</span><span class="sxs-lookup"><span data-stu-id="6756b-194">Increase the environment temperature around the SensorTag to be above 30 C. For example, light a candle around your SensorTag.</span></span>
1. <span data-ttu-id="6756b-195">Vous devriez recevoir un e-mail de notification envoyé par l’application logique.</span><span class="sxs-lookup"><span data-stu-id="6756b-195">You should receive an email notification sent by the logic app.</span></span>

   > [!NOTE]
   > <span data-ttu-id="6756b-196">Il se peut que votre fournisseur de services de messagerie doive vérifier l’identité de l’expéditeur pour s’assurer que vous êtes bien celui qui envoie l’e-mail.</span><span class="sxs-lookup"><span data-stu-id="6756b-196">Your email service provider may need to verify the sender identity to make sure it is you who sends the email.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6756b-197">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6756b-197">Next steps</span></span>

<span data-ttu-id="6756b-198">Vous avez créé avec succès une application logique qui connecte votre IoT Hub et votre boîte aux lettres pour la surveillance de la température et les notifications.</span><span class="sxs-lookup"><span data-stu-id="6756b-198">You have successfully created a logic app that connects your IoT hub and your mailbox for temperature monitoring and notifications.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
