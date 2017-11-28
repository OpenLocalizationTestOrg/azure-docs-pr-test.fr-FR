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
# <a name="iot-remote-monitoring-and-notifications-with-azure-logic-apps-connecting-your-iot-hub-and-mailbox"></a><span data-ttu-id="51ebb-104">Surveillance à distance IoT et notifications avec Azure Logic Apps connectant votre IoT Hub et votre boîte aux lettres</span><span class="sxs-lookup"><span data-stu-id="51ebb-104">IoT remote monitoring and notifications with Azure Logic Apps connecting your IoT hub and mailbox</span></span>

![Diagramme de bout en bout](media/iot-hub-get-started-e2e-diagram/7.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

<span data-ttu-id="51ebb-106">Azure Logic Apps fournit un moyen de processus tooautomate comme une série d’étapes.</span><span class="sxs-lookup"><span data-stu-id="51ebb-106">Azure Logic Apps provides a way tooautomate processes as a series of steps.</span></span> <span data-ttu-id="51ebb-107">Une application logique peut établir une connexion via divers services et protocoles.</span><span class="sxs-lookup"><span data-stu-id="51ebb-107">A logic app can connect across various services and protocols.</span></span> <span data-ttu-id="51ebb-108">Elle commence par un déclencheur tel que « Lorsqu’un compte est ajouté », suivie d’une combinaison d’actions, similaire à « envoi d’une notification Push ».</span><span class="sxs-lookup"><span data-stu-id="51ebb-108">It begins with a trigger such as 'When an account is added', and followed by a combination of actions, one like 'sending a push notification'.</span></span> <span data-ttu-id="51ebb-109">Cette fonctionnalité rend Logic Apps idéale pour la surveillance IoT, telle que la vigilance face aux anomalies, parmi d’autres scénarios d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="51ebb-109">This feature makes Logic Apps a perfect IoT solution for IoT monitoring, such as staying alert for anomalies, among other usage scenarios.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="51ebb-110">Contenu</span><span class="sxs-lookup"><span data-stu-id="51ebb-110">What you learn</span></span>

<span data-ttu-id="51ebb-111">Vous apprendrez comment toocreate une application de la logique qui se connecte votre IoT hub et votre boîte aux lettres pour la surveillance de la température et de notifications.</span><span class="sxs-lookup"><span data-stu-id="51ebb-111">You learn how toocreate a logic app that connects your IoT hub and your mailbox for temperature monitoring and notifications.</span></span> <span data-ttu-id="51ebb-112">Lors de la température de hello est supérieure à 30 C, hello client application marques `temperatureAlert = "true"` dans le message de type hello, il envoie tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="51ebb-112">When hello temperature is above 30 C, hello client application marks `temperatureAlert = "true"` in hello message it sends tooyour IoT hub.</span></span> <span data-ttu-id="51ebb-113">message de type Hello déclencheurs hello logique application toosend vous une notification par courrier électronique.</span><span class="sxs-lookup"><span data-stu-id="51ebb-113">hello message triggers hello logic app toosend you an email notification.</span></span>

## <a name="what-you-do"></a><span data-ttu-id="51ebb-114">Procédure</span><span class="sxs-lookup"><span data-stu-id="51ebb-114">What you do</span></span>

* <span data-ttu-id="51ebb-115">Créer un espace de noms service bus et ajouter un tooit de file d’attente.</span><span class="sxs-lookup"><span data-stu-id="51ebb-115">Create a service bus namespace and add a queue tooit.</span></span>
* <span data-ttu-id="51ebb-116">Ajouter un point de terminaison et un routage IoT hub règle tooyour.</span><span class="sxs-lookup"><span data-stu-id="51ebb-116">Add an endpoint and a routing rule tooyour IoT hub.</span></span>
* <span data-ttu-id="51ebb-117">Créez, configurez et testez une application logique.</span><span class="sxs-lookup"><span data-stu-id="51ebb-117">Create, configure, and test a logic app.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="51ebb-118">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="51ebb-118">What you need</span></span>

* <span data-ttu-id="51ebb-119">Didacticiel [configurer votre appareil](iot-hub-raspberry-pi-kit-node-get-started.md) terminé qui couvre hello suivant les exigences :</span><span class="sxs-lookup"><span data-stu-id="51ebb-119">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers hello following requirements:</span></span>
  * <span data-ttu-id="51ebb-120">Un abonnement Azure actif.</span><span class="sxs-lookup"><span data-stu-id="51ebb-120">An active Azure subscription.</span></span>
  * <span data-ttu-id="51ebb-121">Une instance Azure IoT Hub associée à votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="51ebb-121">An Azure IoT hub under your subscription.</span></span>
  * <span data-ttu-id="51ebb-122">Une application cliente qui envoie le concentrateur de messages tooyour Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="51ebb-122">A client application that sends messages tooyour Azure IoT hub.</span></span>

## <a name="create-service-bus-namespace-and-add-a-queue-tooit"></a><span data-ttu-id="51ebb-123">Créer l’espace de noms service bus et ajouter un tooit de file d’attente</span><span class="sxs-lookup"><span data-stu-id="51ebb-123">Create service bus namespace and add a queue tooit</span></span>

### <a name="create-a-service-bus-namespace"></a><span data-ttu-id="51ebb-124">Création d'un espace de noms Service Bus</span><span class="sxs-lookup"><span data-stu-id="51ebb-124">Create a service bus namespace</span></span>

1. <span data-ttu-id="51ebb-125">Sur hello [portail Azure](https://portal.azure.com/), cliquez sur **nouveau** > **intégration** > **Service Bus**.</span><span class="sxs-lookup"><span data-stu-id="51ebb-125">On hello [Azure portal](https://portal.azure.com/), click **New** > **Enterprise Integration** > **Service Bus**.</span></span>
1. <span data-ttu-id="51ebb-126">Fournir hello informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="51ebb-126">Provide hello following information:</span></span>

   <span data-ttu-id="51ebb-127">**Nom**: nom hello du bus de service hello.</span><span class="sxs-lookup"><span data-stu-id="51ebb-127">**Name**: hello name of hello service bus.</span></span>

   <span data-ttu-id="51ebb-128">**Niveau tarifaire**: cliquez sur **De base** > **Sélectionnez**.</span><span class="sxs-lookup"><span data-stu-id="51ebb-128">**Pricing tier**: Click **Basic** > **Select**.</span></span> <span data-ttu-id="51ebb-129">niveau de base Hello est suffisant pour ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="51ebb-129">hello Basic tier is sufficient for this tutorial.</span></span>

   <span data-ttu-id="51ebb-130">**Groupe de ressources**: utilisez hello même groupe de ressources qui utilise de votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="51ebb-130">**Resource group**: Use hello same resource group that your IoT hub uses.</span></span>

   <span data-ttu-id="51ebb-131">**Emplacement**: utilisez hello même emplacement que votre hub IoT utilise.</span><span class="sxs-lookup"><span data-stu-id="51ebb-131">**Location**: Use hello same location that your IoT hub uses.</span></span>
1. <span data-ttu-id="51ebb-132">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="51ebb-132">Click **Create**.</span></span>

   ![Créer un espace de noms service bus Bonjour portail Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/1_create-service-bus-namespace-azure-portal.png)

### <a name="add-a-service-bus-queue"></a><span data-ttu-id="51ebb-134">Ajouter une file d’attente Service Bus</span><span class="sxs-lookup"><span data-stu-id="51ebb-134">Add a service bus queue</span></span>

1. <span data-ttu-id="51ebb-135">Ouvrez l’espace de noms hello service bus, puis cliquez sur **+ file d’attente**.</span><span class="sxs-lookup"><span data-stu-id="51ebb-135">Open hello service bus namespace, and then click **+ Queue**.</span></span>
1. <span data-ttu-id="51ebb-136">Entrez un nom pour la file d’attente hello, puis cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="51ebb-136">Enter a name for hello queue and then click **Create**.</span></span>
1. <span data-ttu-id="51ebb-137">Ouvrir la file d’attente de bus de service hello, puis cliquez sur **les stratégies d’accès partagé** > **+ ajouter**.</span><span class="sxs-lookup"><span data-stu-id="51ebb-137">Open hello service bus queue, and then click **Shared access policies** > **+ Add**.</span></span>
1. <span data-ttu-id="51ebb-138">Entrez un nom pour la stratégie de hello, cocher **gérer**, puis cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="51ebb-138">Enter a name for hello policy, check **Manage**, and then click **Create**.</span></span>

   ![Ajouter une file d’attente du bus de service Bonjour portail Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/2_add-service-bus-queue-azure-portal.png)

## <a name="add-an-endpoint-and-a-routing-rule-tooyour-iot-hub"></a><span data-ttu-id="51ebb-140">Ajouter un point de terminaison et un routage IoT hub règle tooyour</span><span class="sxs-lookup"><span data-stu-id="51ebb-140">Add an endpoint and a routing rule tooyour IoT hub</span></span>

### <a name="add-an-endpoint"></a><span data-ttu-id="51ebb-141">Ajout d’un point de terminaison</span><span class="sxs-lookup"><span data-stu-id="51ebb-141">Add an endpoint</span></span>

1. <span data-ttu-id="51ebb-142">Ouvrez votre IoT Hub et cliquez sur Points de terminaison > + Ajouter.</span><span class="sxs-lookup"><span data-stu-id="51ebb-142">Open your IoT hub, click Endpoints > + Add.</span></span>
1. <span data-ttu-id="51ebb-143">Entrez hello informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="51ebb-143">Enter hello following information:</span></span>

   <span data-ttu-id="51ebb-144">**Nom**: nom hello du point de terminaison hello.</span><span class="sxs-lookup"><span data-stu-id="51ebb-144">**Name**: hello name of hello endpoint.</span></span>

   <span data-ttu-id="51ebb-145">**Type de point de terminaison** : sélectionnez **File d’attente Service Bus**.</span><span class="sxs-lookup"><span data-stu-id="51ebb-145">**Endpoint type**: Select **Service Bus Queue**.</span></span>

   <span data-ttu-id="51ebb-146">**Espace de noms Service Bus**: sélectionnez l’espace de noms hello vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="51ebb-146">**Service Bus namespace**: Select hello namespace you created.</span></span>

   <span data-ttu-id="51ebb-147">**File d’attente Service Bus**: vous avez créé de la file d’attente hello Select.</span><span class="sxs-lookup"><span data-stu-id="51ebb-147">**Service Bus queue**: Select hello queue you created.</span></span>
1. <span data-ttu-id="51ebb-148">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="51ebb-148">Click **OK**.</span></span>

   ![Ajouter un IoT hub de point de terminaison tooyour Bonjour portail Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/3_add-iot-hub-endpoint-azure-portal.png)

### <a name="add-a-routing-rule"></a><span data-ttu-id="51ebb-150">Ajouter une règle de routage</span><span class="sxs-lookup"><span data-stu-id="51ebb-150">Add a routing rule</span></span>

1. <span data-ttu-id="51ebb-151">Dans votre Iot Hub, cliquez sur **Itinéraires** > **+ Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="51ebb-151">In your IoT hub, click **Routes** > **+ Add**.</span></span>
1. <span data-ttu-id="51ebb-152">Entrez hello informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="51ebb-152">Enter hello following information:</span></span>

   <span data-ttu-id="51ebb-153">**Nom**: nom hello de règle de routage hello.</span><span class="sxs-lookup"><span data-stu-id="51ebb-153">**Name**: hello name of hello routing rule.</span></span>

   <span data-ttu-id="51ebb-154">**Source de données** : sélectionnez **DeviceMessages**.</span><span class="sxs-lookup"><span data-stu-id="51ebb-154">**Data source**: Select **DeviceMessages**.</span></span>

   <span data-ttu-id="51ebb-155">**Point de terminaison**: sélectionnez le point de terminaison hello vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="51ebb-155">**Endpoint**: Select hello endpoint you created.</span></span>

   <span data-ttu-id="51ebb-156">**Chaîne de requête** : entrez `temperatureAlert = "true"`.</span><span class="sxs-lookup"><span data-stu-id="51ebb-156">**Query string**: Enter `temperatureAlert = "true"`.</span></span>
1. <span data-ttu-id="51ebb-157">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="51ebb-157">Click **Save**.</span></span>

   ![Ajouter une règle de routage Bonjour portail Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/4_add-routing-rule-azure-portal.png)

## <a name="create-and-configure-a-logic-app"></a><span data-ttu-id="51ebb-159">Créer et configurer une application logique</span><span class="sxs-lookup"><span data-stu-id="51ebb-159">Create and configure a logic app</span></span>

### <a name="create-a-logic-app"></a><span data-ttu-id="51ebb-160">Créer une application logique</span><span class="sxs-lookup"><span data-stu-id="51ebb-160">Create a logic app</span></span>

1. <span data-ttu-id="51ebb-161">Bonjour [portail Azure](https://portal.azure.com/), cliquez sur **nouveau** > **intégration** > **application logique**.</span><span class="sxs-lookup"><span data-stu-id="51ebb-161">In hello [Azure portal](https://portal.azure.com/), click **New** > **Enterprise Integration** > **Logic App**.</span></span>
1. <span data-ttu-id="51ebb-162">Entrez hello informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="51ebb-162">Enter hello following information:</span></span>

   <span data-ttu-id="51ebb-163">**Nom**: nom hello d’application logique de hello.</span><span class="sxs-lookup"><span data-stu-id="51ebb-163">**Name**: hello name of hello logic app.</span></span>

   <span data-ttu-id="51ebb-164">**Groupe de ressources**: utilisez hello même groupe de ressources qui utilise de votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="51ebb-164">**Resource group**: Use hello same resource group that your IoT hub uses.</span></span>

   <span data-ttu-id="51ebb-165">**Emplacement**: utilisez hello même emplacement que votre hub IoT utilise.</span><span class="sxs-lookup"><span data-stu-id="51ebb-165">**Location**: Use hello same location that your IoT hub uses.</span></span>
1. <span data-ttu-id="51ebb-166">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="51ebb-166">Click **Create**.</span></span>

### <a name="configure-hello-logic-app"></a><span data-ttu-id="51ebb-167">Configurer l’application logique de hello</span><span class="sxs-lookup"><span data-stu-id="51ebb-167">Configure hello logic app</span></span>

1. <span data-ttu-id="51ebb-168">Ouvrez l’application hello logique qui s’ouvre dans hello logique de concepteur d’applications.</span><span class="sxs-lookup"><span data-stu-id="51ebb-168">Open hello logic app that opens into hello Logic Apps Designer.</span></span>
1. <span data-ttu-id="51ebb-169">Bonjour logique de concepteur d’applications, cliquez sur **application logique vide**.</span><span class="sxs-lookup"><span data-stu-id="51ebb-169">In hello Logic Apps Designer, click **Blank Logic App**.</span></span>

   ![Démarrez avec une application vide logique Bonjour portail Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/5_start-with-blank-logic-app-azure-portal.png)

1. <span data-ttu-id="51ebb-171">Cliquez sur **Service Bus**.</span><span class="sxs-lookup"><span data-stu-id="51ebb-171">Click **Service Bus**.</span></span>

   ![Sélectionnez toostart Service Bus création de votre application logique Bonjour portail Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/6_select-service-bus-when-creating-blank-logic-app-azure-portal.png)

1. <span data-ttu-id="51ebb-173">Cliquez sur **Service Bus – lorsqu’un ou plusieurs messages arrivent dans une file d’attente (saisie semi-automatique)**.</span><span class="sxs-lookup"><span data-stu-id="51ebb-173">Click **Service Bus – When one or more messages arrive in a queue (auto-complete)**.</span></span>
1. <span data-ttu-id="51ebb-174">Créez une connexion Service Bus.</span><span class="sxs-lookup"><span data-stu-id="51ebb-174">Create a service bus connection.</span></span>
   1. <span data-ttu-id="51ebb-175">Entrez un nom de connexion.</span><span class="sxs-lookup"><span data-stu-id="51ebb-175">Enter a connection name.</span></span>
   1. <span data-ttu-id="51ebb-176">Cliquez sur hello espace de noms bus > hello stratégie de bus de service > **créer**.</span><span class="sxs-lookup"><span data-stu-id="51ebb-176">Click hello service bus namespace > hello service bus policy > **Create**.</span></span>

      ![Créer une connexion de service bus pour votre application logique Bonjour portail Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/7_create-service-bus-connection-in-logic-app-azure-portal.png)

   1. <span data-ttu-id="51ebb-178">Cliquez sur **continuer** après la création de connexion de service bus hello.</span><span class="sxs-lookup"><span data-stu-id="51ebb-178">Click **Continue** after hello service bus connection is created.</span></span>
   1. <span data-ttu-id="51ebb-179">Sélectionnez une file d’attente hello que vous avez créé, puis entrez `175` pour **nombre de messages au Maximum**</span><span class="sxs-lookup"><span data-stu-id="51ebb-179">Select hello queue that you created and enter `175` for **Maximum message count**</span></span>

      ![Spécifiez le nombre de message maximale de hello hello connexion de service bus dans votre logique d’application](media/iot-hub-monitoring-notifications-with-azure-logic-apps/8_specify-maximum-message-count-for-service-bus-connection-logic-app-azure-portal.png)
   1. <span data-ttu-id="51ebb-181">Cliquez sur « Enregistrer » hello toosave du bouton change.</span><span class="sxs-lookup"><span data-stu-id="51ebb-181">Click "Save" button toosave hello changes.</span></span>

1. <span data-ttu-id="51ebb-182">Créez une connexion de service SMTP.</span><span class="sxs-lookup"><span data-stu-id="51ebb-182">Create an SMTP service connection.</span></span>
   1. <span data-ttu-id="51ebb-183">Choisissez **Nouvelle étape** > **Ajouter une action**.</span><span class="sxs-lookup"><span data-stu-id="51ebb-183">Click **New step** > **Add an action**.</span></span>
   1. <span data-ttu-id="51ebb-184">Type `SMTP`, cliquez sur hello **SMTP** hello le résultat de recherche de service, puis cliquez sur **SMTP - envoyer un courrier électronique**.</span><span class="sxs-lookup"><span data-stu-id="51ebb-184">Type `SMTP`, click hello **SMTP** service in hello search result, and then click **SMTP - Send Email**.</span></span>

      ![Créer une connexion SMTP dans votre application logique Bonjour portail Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/9_create-smtp-connection-logic-app-azure-portal.png)

   1. <span data-ttu-id="51ebb-186">Entrez les informations de hello SMTP de votre boîte aux lettres, puis cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="51ebb-186">Enter hello SMTP information of your mailbox, and then click **Create**.</span></span>

      ![Entrez les informations de connexion SMTP dans votre application logique Bonjour portail Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/10_enter-smtp-connection-info-logic-app-azure-portal.png)

      <span data-ttu-id="51ebb-188">Obtenir des informations de hello SMTP pour [Hotmail/Outlook.com](https://support.office.com/en-us/article/Add-your-Outlook-com-account-to-another-mail-app-73f3b178-0009-41ae-aab1-87b80fa94970), [Gmail](https://support.google.com/a/answer/176600?hl=en), et [messagerie Yahoo](https://help.yahoo.com/kb/SLN4075.html).</span><span class="sxs-lookup"><span data-stu-id="51ebb-188">Get hello SMTP information for [Hotmail/Outlook.com](https://support.office.com/en-us/article/Add-your-Outlook-com-account-to-another-mail-app-73f3b178-0009-41ae-aab1-87b80fa94970), [Gmail](https://support.google.com/a/answer/176600?hl=en), and [Yahoo Mail](https://help.yahoo.com/kb/SLN4075.html).</span></span>
   1. <span data-ttu-id="51ebb-189">Entrez votre adresse de messagerie pour **De** et **À**, et `High temperature detected` pour **Objet** et **Corps**.</span><span class="sxs-lookup"><span data-stu-id="51ebb-189">Enter your email address for **From** and **To**, and `High temperature detected` for **Subject** and **Body**.</span></span>
   1. <span data-ttu-id="51ebb-190">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="51ebb-190">Click **Save**.</span></span>

<span data-ttu-id="51ebb-191">application de la logique de Hello est en marche lors de son enregistrement.</span><span class="sxs-lookup"><span data-stu-id="51ebb-191">hello logic app is in working order when you save it.</span></span>

## <a name="test-hello-logic-app"></a><span data-ttu-id="51ebb-192">Application de test hello logique</span><span class="sxs-lookup"><span data-stu-id="51ebb-192">Test hello logic app</span></span>

1. <span data-ttu-id="51ebb-193">Démarrer l’application hello client que vous déployez appareil tooyour dans [ESP8266 de se connecter tooAzure IoT Hub](iot-hub-arduino-huzzah-esp8266-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="51ebb-193">Start hello client application that you deploy tooyour device in [Connect ESP8266 tooAzure IoT Hub](iot-hub-arduino-huzzah-esp8266-get-started.md).</span></span>
1. <span data-ttu-id="51ebb-194">Augmenter la température de l’environnement hello autour de toobe de SensorTag hello ci-dessus c de 30. Par exemple, la lumière une bougie autour de votre SensorTag.</span><span class="sxs-lookup"><span data-stu-id="51ebb-194">Increase hello environment temperature around hello SensorTag toobe above 30 C. For example, light a candle around your SensorTag.</span></span>
1. <span data-ttu-id="51ebb-195">Vous devriez recevoir une notification par courrier électronique envoyée par l’application de la logique de hello.</span><span class="sxs-lookup"><span data-stu-id="51ebb-195">You should receive an email notification sent by hello logic app.</span></span>

   > [!NOTE]
   > <span data-ttu-id="51ebb-196">Votre fournisseur de services de messagerie peut-être tooverify hello expéditeur identité toomake que c’est vous qui envoie par courrier électronique hello.</span><span class="sxs-lookup"><span data-stu-id="51ebb-196">Your email service provider may need tooverify hello sender identity toomake sure it is you who sends hello email.</span></span>

## <a name="next-steps"></a><span data-ttu-id="51ebb-197">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="51ebb-197">Next steps</span></span>

<span data-ttu-id="51ebb-198">Vous avez créé avec succès une application logique qui connecte votre IoT Hub et votre boîte aux lettres pour la surveillance de la température et les notifications.</span><span class="sxs-lookup"><span data-stu-id="51ebb-198">You have successfully created a logic app that connects your IoT hub and your mailbox for temperature monitoring and notifications.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
