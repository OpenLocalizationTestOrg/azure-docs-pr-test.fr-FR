---
title: "aaaGet en main Azure IoT Hub (nœud) | Documents Microsoft"
description: "Découvrez comment toosend appareil-à-cloud messages tooAzure IoT Hub à l’aide de kits de développement logiciel IoT pour Node.js. Créer appareil simulé et tooregister des applications de service de votre appareil, envoyer des messages et lire les messages de hub IoT."
services: iot-hub
documentationcenter: nodejs
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 56618522-9a31-42c6-94bf-55e2233b39ac
ms.service: iot-hub
ms.devlang: javascript
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/22/2017
ms.author: dobett
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d0747895365f2359a9c38ea1e85a5881d6efec0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-simulated-device-tooyour-iot-hub-using-node"></a><span data-ttu-id="1b789-104">Connectez votre concentrateur de IoT tooyour appareil simulé à l’aide du nœud</span><span class="sxs-lookup"><span data-stu-id="1b789-104">Connect your simulated device tooyour IoT hub using Node</span></span>
[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

<span data-ttu-id="1b789-105">À la fin de hello de ce didacticiel, vous avez trois applications de console Node.js :</span><span class="sxs-lookup"><span data-stu-id="1b789-105">At hello end of this tutorial, you have three Node.js console apps:</span></span>

* <span data-ttu-id="1b789-106">**CreateDeviceIdentity.js**, ce qui crée une identité d’appareil et clé de sécurité associés tooconnect votre application d’appareil simulé.</span><span class="sxs-lookup"><span data-stu-id="1b789-106">**CreateDeviceIdentity.js**, which creates a device identity and associated security key tooconnect your simulated device app.</span></span>
* <span data-ttu-id="1b789-107">**ReadDeviceToCloudMessages.js**, qui affiche la télémétrie hello envoyée par votre application d’appareil simulé.</span><span class="sxs-lookup"><span data-stu-id="1b789-107">**ReadDeviceToCloudMessages.js**, which displays hello telemetry sent by your simulated device app.</span></span>
* <span data-ttu-id="1b789-108">**SimulatedDevice.js**, qui se connecte tooyour IoT hub avec l’identité de l’appareil hello créée précédemment et envoie un message de télémétrie chaque seconde à l’aide de hello le protocole MQTT.</span><span class="sxs-lookup"><span data-stu-id="1b789-108">**SimulatedDevice.js**, which connects tooyour IoT hub with hello device identity created earlier, and sends a telemetry message every second using hello MQTT protocol.</span></span>

> [!NOTE]
> <span data-ttu-id="1b789-109">article de Hello [kits de développement logiciel Azure IoT] [ lnk-hub-sdks] fournit des informations sur hello kits de développement logiciel Azure IoT que vous pouvez utiliser toobuild toorun de deux applications sur les périphériques et votre principal de la solution.</span><span class="sxs-lookup"><span data-stu-id="1b789-109">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both applications toorun on devices and your solution back end.</span></span>
> 
> 

<span data-ttu-id="1b789-110">toocomplete ce didacticiel, vous devez hello suivant :</span><span class="sxs-lookup"><span data-stu-id="1b789-110">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="1b789-111">Node.js version 0.10.x ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="1b789-111">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="1b789-112">Un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="1b789-112">An active Azure account.</span></span> <span data-ttu-id="1b789-113">(Si vous ne possédez pas de compte, vous pouvez créer un [compte gratuit][lnk-free-trial] en quelques minutes.)</span><span class="sxs-lookup"><span data-stu-id="1b789-113">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

<span data-ttu-id="1b789-114">Votre IoT Hub est maintenant créé.</span><span class="sxs-lookup"><span data-stu-id="1b789-114">You have now created your IoT hub.</span></span> <span data-ttu-id="1b789-115">Vous avez hello nom d’hôte IoT Hub et hello chaîne de connexion IoT Hub que vous avez besoin reste de hello toocomplete de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="1b789-115">You have hello IoT Hub host name and hello IoT Hub connection string that you need toocomplete hello rest of this tutorial.</span></span>

## <a name="create-a-device-identity"></a><span data-ttu-id="1b789-116">Création d’une identité d’appareil</span><span class="sxs-lookup"><span data-stu-id="1b789-116">Create a device identity</span></span>
<span data-ttu-id="1b789-117">Dans cette section, vous créer une application de console Node.js qui crée une identité d’appareil dans le Registre des identités hello dans votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="1b789-117">In this section, you create a Node.js console app that creates a device identity in hello identity registry in your IoT hub.</span></span> <span data-ttu-id="1b789-118">Appareils de se connecter uniquement tooIoT hub si elle a une entrée dans le Registre des identités hello.</span><span class="sxs-lookup"><span data-stu-id="1b789-118">A device can only connect tooIoT hub if it has an entry in hello identity registry.</span></span> <span data-ttu-id="1b789-119">Pour plus d’informations, consultez hello **Registre des identités** section Hello [guide du développeur IoT Hub][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="1b789-119">For more information, see hello **Identity Registry** section of hello [IoT Hub developer guide][lnk-devguide-identity].</span></span> <span data-ttu-id="1b789-120">Lorsque vous exécutez cette application console, il génère un ID d’appareil unique et clé que votre appareil peut utiliser tooidentify lui-même lorsqu’il envoie l’appareil-à-cloud messages tooIoT Hub.</span><span class="sxs-lookup"><span data-stu-id="1b789-120">When you run this console app, it generates a unique device ID and key that your device can use tooidentify itself when it sends device-to-cloud messages tooIoT Hub.</span></span>

1. <span data-ttu-id="1b789-121">Créez un dossier vide appelé **createdeviceidentity**.</span><span class="sxs-lookup"><span data-stu-id="1b789-121">Create a new empty folder called **createdeviceidentity**.</span></span> <span data-ttu-id="1b789-122">Bonjour **createdeviceidentity** dossier, créez un fichier package.json à l’aide de hello, la commande suivante à l’invite suivante.</span><span class="sxs-lookup"><span data-stu-id="1b789-122">In hello **createdeviceidentity** folder, create a package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="1b789-123">Acceptez les valeurs par défaut hello :</span><span class="sxs-lookup"><span data-stu-id="1b789-123">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="1b789-124">Votre invite de commandes Bonjour **createdeviceidentity** dossier, exécutez hello suivant commande tooinstall hello **azure-iothub** package SDK de Service :</span><span class="sxs-lookup"><span data-stu-id="1b789-124">At your command prompt in hello **createdeviceidentity** folder, run hello following command tooinstall hello **azure-iothub** Service SDK package:</span></span>
   
    ```
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="1b789-125">À l’aide d’un éditeur de texte, créez un **CreateDeviceIdentity.js** fichier Bonjour **createdeviceidentity** dossier.</span><span class="sxs-lookup"><span data-stu-id="1b789-125">Using a text editor, create a **CreateDeviceIdentity.js** file in hello **createdeviceidentity** folder.</span></span>
4. <span data-ttu-id="1b789-126">Ajoutez hello suivant `require` instruction au début de hello de hello **CreateDeviceIdentity.js** fichier :</span><span class="sxs-lookup"><span data-stu-id="1b789-126">Add hello following `require` statement at hello start of hello **CreateDeviceIdentity.js** file:</span></span>
   
    ```
    'use strict';
   
    var iothub = require('azure-iothub');
    ```
5. <span data-ttu-id="1b789-127">Ajouter hello suivant code toohello **CreateDeviceIdentity.js** de fichiers et de remplacer la valeur d’espace réservé hello avec hello chaîne de connexion de IoT Hub hub hello vous avez créé dans la section précédente de hello de :</span><span class="sxs-lookup"><span data-stu-id="1b789-127">Add hello following code toohello **CreateDeviceIdentity.js** file and replace hello placeholder value with hello IoT Hub connection string for hello hub you created in hello previous section:</span></span> 
   
    ```
    var connectionString = '{iothub connection string}';
   
    var registry = iothub.Registry.fromConnectionString(connectionString);
    ```
6. <span data-ttu-id="1b789-128">Ajoutez hello suivant code toocreate une définition de périphérique dans le Registre des identités hello dans votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="1b789-128">Add hello following code toocreate a device definition in hello identity registry in your IoT hub.</span></span> <span data-ttu-id="1b789-129">Ce code crée un appareil si l’ID de périphérique hello n’existe pas dans le Registre des identités hello, sinon elle retourne la clé hello d’unité de hello existante :</span><span class="sxs-lookup"><span data-stu-id="1b789-129">This code creates a device if hello device ID does not exist in hello identity registry, otherwise it returns hello key of hello existing device:</span></span>
   
    ```
    var device = {
      deviceId: 'myFirstNodeDevice'
    }
    registry.create(device, function(err, deviceInfo, res) {
      if (err) {
        registry.get(device.deviceId, printDeviceInfo);
      }
      if (deviceInfo) {
        printDeviceInfo(err, deviceInfo, res)
      }
    });
   
    function printDeviceInfo(err, deviceInfo, res) {
      if (deviceInfo) {
        console.log('Device ID: ' + deviceInfo.deviceId);
        console.log('Device key: ' + deviceInfo.authentication.symmetricKey.primaryKey);
      }
    }
    ```
   [!INCLUDE [iot-hub-pii-note-naming-device](../../includes/iot-hub-pii-note-naming-device.md)]

7. <span data-ttu-id="1b789-130">Enregistrez et fermez le fichier **CreateDeviceIdentity.js** .</span><span class="sxs-lookup"><span data-stu-id="1b789-130">Save and close **CreateDeviceIdentity.js** file.</span></span>
8. <span data-ttu-id="1b789-131">toorun hello **createdeviceidentity** application, exécutez hello commande à l’invite de commandes hello dans le dossier de createdeviceidentity hello suivante :</span><span class="sxs-lookup"><span data-stu-id="1b789-131">toorun hello **createdeviceidentity** application, execute hello following command at hello command prompt in hello createdeviceidentity folder:</span></span>
   
    ```
    node CreateDeviceIdentity.js 
    ```
9. <span data-ttu-id="1b789-132">Prenez note de hello **ID de périphérique** et **clé de périphérique**.</span><span class="sxs-lookup"><span data-stu-id="1b789-132">Make a note of hello **Device ID** and **Device key**.</span></span> <span data-ttu-id="1b789-133">Vous avez besoin de ces valeurs lorsque vous créez une application qui se connecte tooIoT Hub en tant que périphérique.</span><span class="sxs-lookup"><span data-stu-id="1b789-133">You need these values later when you create an application that connects tooIoT Hub as a device.</span></span>

> [!NOTE]
> <span data-ttu-id="1b789-134">Hello Registre des identités IoT Hub stocke uniquement toohello IoT hub de périphérique identités tooenable un accès sécurisé.</span><span class="sxs-lookup"><span data-stu-id="1b789-134">hello IoT Hub identity registry only stores device identities tooenable secure access toohello IoT hub.</span></span> <span data-ttu-id="1b789-135">Il stocke toouse ID et les clés de périphérique en tant qu’informations d’identification de sécurité et d’un indicateur activée/désactivée que vous pouvez utiliser l’accès toodisable pour un périphérique.</span><span class="sxs-lookup"><span data-stu-id="1b789-135">It stores device IDs and keys toouse as security credentials and an enabled/disabled flag that you can use toodisable access for an individual device.</span></span> <span data-ttu-id="1b789-136">Si votre application doit toostore autres métadonnées spécifiques au périphérique, elle doit utiliser un magasin spécifique à l’application.</span><span class="sxs-lookup"><span data-stu-id="1b789-136">If your application needs toostore other device-specific metadata, it should use an application-specific store.</span></span> <span data-ttu-id="1b789-137">Pour plus d’informations, consultez hello [guide du développeur IoT Hub][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="1b789-137">For more information, see hello [IoT Hub developer guide][lnk-devguide-identity].</span></span>
> 
> 

<a id="D2C_node"></a>
## <a name="receive-device-to-cloud-messages"></a><span data-ttu-id="1b789-138">Recevoir des messages appareil-à-cloud</span><span class="sxs-lookup"><span data-stu-id="1b789-138">Receive device-to-cloud messages</span></span>
<span data-ttu-id="1b789-139">Dans cette section, vous créez une application console Node.js qui lit les messages appareil-à-cloud à partir d’IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="1b789-139">In this section, you create a Node.js console app that reads device-to-cloud messages from IoT Hub.</span></span> <span data-ttu-id="1b789-140">Un hub IoT expose un [concentrateurs d’événements][lnk-event-hubs-overview]-point de terminaison compatible tooenable vous tooread les messages appareil-à-cloud.</span><span class="sxs-lookup"><span data-stu-id="1b789-140">An IoT hub exposes an [Event Hubs][lnk-event-hubs-overview]-compatible endpoint tooenable you tooread device-to-cloud messages.</span></span> <span data-ttu-id="1b789-141">tookeep les choses simples, ce didacticiel crée un lecteur de base qui n’est pas approprié pour un déploiement d’un débit élevé.</span><span class="sxs-lookup"><span data-stu-id="1b789-141">tookeep things simple, this tutorial creates a basic reader that is not suitable for a high throughput deployment.</span></span> <span data-ttu-id="1b789-142">Hello [traiter les messages appareil-à-cloud] [ lnk-process-d2c-tutorial] didacticiel vous montre comment les messages tooprocess appareil-à-cloud à grande échelle.</span><span class="sxs-lookup"><span data-stu-id="1b789-142">hello [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial shows you how tooprocess device-to-cloud messages at scale.</span></span> <span data-ttu-id="1b789-143">Hello [prise en main les concentrateurs d’événements] [ lnk-eventhubs-tutorial] didacticiel fournit des informations supplémentaires sur le tooprocess des messages à partir de concentrateurs d’événements et est applicable toohello points de terminaison de Hub IoT Hub événement compatible.</span><span class="sxs-lookup"><span data-stu-id="1b789-143">hello [Get Started with Event Hubs][lnk-eventhubs-tutorial] tutorial provides further information on how tooprocess messages from Event Hubs and is applicable toohello IoT Hub Event Hub-compatible endpoints.</span></span>

> [!NOTE]
> <span data-ttu-id="1b789-144">Hello point de terminaison de Hub d’événements compatibles pour la lecture des messages appareil-à-cloud toujours utilise le protocole AMQP hello.</span><span class="sxs-lookup"><span data-stu-id="1b789-144">hello Event Hub-compatible endpoint for reading device-to-cloud messages always uses hello AMQP protocol.</span></span>
> 
> 

1. <span data-ttu-id="1b789-145">Créez un dossier vide appelé **readdevicetocloudmessages**.</span><span class="sxs-lookup"><span data-stu-id="1b789-145">Create an empty folder called **readdevicetocloudmessages**.</span></span> <span data-ttu-id="1b789-146">Bonjour **readdevicetocloudmessages** dossier, créez un fichier package.json à l’aide de hello, la commande suivante à l’invite suivante.</span><span class="sxs-lookup"><span data-stu-id="1b789-146">In hello **readdevicetocloudmessages** folder, create a package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="1b789-147">Acceptez les valeurs par défaut hello :</span><span class="sxs-lookup"><span data-stu-id="1b789-147">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="1b789-148">Votre invite de commandes Bonjour **readdevicetocloudmessages** dossier, exécutez hello suivant commande tooinstall hello **concentrateurs d’événements azure** package :</span><span class="sxs-lookup"><span data-stu-id="1b789-148">At your command prompt in hello **readdevicetocloudmessages** folder, run hello following command tooinstall hello **azure-event-hubs** package:</span></span>
   
    ```
    npm install azure-event-hubs --save
    ```
3. <span data-ttu-id="1b789-149">À l’aide d’un éditeur de texte, créez un **ReadDeviceToCloudMessages.js** fichier Bonjour **readdevicetocloudmessages** dossier.</span><span class="sxs-lookup"><span data-stu-id="1b789-149">Using a text editor, create a **ReadDeviceToCloudMessages.js** file in hello **readdevicetocloudmessages** folder.</span></span>
4. <span data-ttu-id="1b789-150">Ajoutez hello suivant `require` instructions au hello démarrent Hello **ReadDeviceToCloudMessages.js** fichier :</span><span class="sxs-lookup"><span data-stu-id="1b789-150">Add hello following `require` statements at hello start of hello **ReadDeviceToCloudMessages.js** file:</span></span>
   
    ```
    'use strict';
   
    var EventHubClient = require('azure-event-hubs').Client;
    ```
5. <span data-ttu-id="1b789-151">Ajouter hello après la déclaration de variable et remplacer la valeur d’espace réservé de hello par hello chaîne de connexion de IoT Hub pour votre concentrateur :</span><span class="sxs-lookup"><span data-stu-id="1b789-151">Add hello following variable declaration and replace hello placeholder value with hello IoT Hub connection string for your hub:</span></span>
   
    ```
    var connectionString = '{iothub connection string}';
    ```
6. <span data-ttu-id="1b789-152">Ajoutez hello suivant deux fonctions de la console de sortie toohello impression :</span><span class="sxs-lookup"><span data-stu-id="1b789-152">Add hello following two functions that print output toohello console:</span></span>
   
    ```
    var printError = function (err) {
      console.log(err.message);
    };
   
    var printMessage = function (message) {
      console.log('Message received: ');
      console.log(JSON.stringify(message.body));
      console.log('');
    };
    ```
7. <span data-ttu-id="1b789-153">Ajouter hello suivant hello toocreate de code **EventHubClient**, ouvrez hello connexion tooyour IoT Hub et créer un récepteur pour chaque partition.</span><span class="sxs-lookup"><span data-stu-id="1b789-153">Add hello following code toocreate hello **EventHubClient**, open hello connection tooyour IoT Hub, and create a receiver for each partition.</span></span> <span data-ttu-id="1b789-154">Cette application utilise un filtre lorsqu’il crée un récepteur afin que hello récepteur lit uniquement les messages envoyés tooIoT Hub après que le récepteur de hello commence à s’exécuter.</span><span class="sxs-lookup"><span data-stu-id="1b789-154">This application uses a filter when it creates a receiver so that hello receiver only reads messages sent tooIoT Hub after hello receiver starts running.</span></span> <span data-ttu-id="1b789-155">Ce filtre est utile dans un environnement de test afin de voir simplement hello ensemble actuel de messages.</span><span class="sxs-lookup"><span data-stu-id="1b789-155">This filter is useful in a test environment so you see just hello current set of messages.</span></span> <span data-ttu-id="1b789-156">Dans un environnement de production, votre code doit Assurez-vous qu’elle traite tous les messages de type hello.</span><span class="sxs-lookup"><span data-stu-id="1b789-156">In a production environment, your code should make sure that it processes all hello messages.</span></span> <span data-ttu-id="1b789-157">Pour plus d’informations, consultez hello [comment tooprocess les messages appareil-à-cloud IoT Hub] [ lnk-process-d2c-tutorial] didacticiel :</span><span class="sxs-lookup"><span data-stu-id="1b789-157">For more information, see hello [How tooprocess IoT Hub device-to-cloud messages][lnk-process-d2c-tutorial] tutorial:</span></span>
   
    ```
    var client = EventHubClient.fromConnectionString(connectionString);
    client.open()
        .then(client.getPartitionIds.bind(client))
        .then(function (partitionIds) {
            return partitionIds.map(function (partitionId) {
                return client.createReceiver('$Default', partitionId, { 'startAfterTime' : Date.now()}).then(function(receiver) {
                    console.log('Created partition receiver: ' + partitionId)
                    receiver.on('errorReceived', printError);
                    receiver.on('message', printMessage);
                });
            });
        })
        .catch(printError);
    ```
8. <span data-ttu-id="1b789-158">Enregistrez et fermez hello **ReadDeviceToCloudMessages.js** fichier.</span><span class="sxs-lookup"><span data-stu-id="1b789-158">Save and close hello **ReadDeviceToCloudMessages.js** file.</span></span>

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="1b789-159">Création d’une application de périphérique simulé</span><span class="sxs-lookup"><span data-stu-id="1b789-159">Create a simulated device app</span></span>
<span data-ttu-id="1b789-160">Dans cette section, vous créez une application console Node.js qui simule un appareil qui envoie l’IoT hub tooan de messages appareil-à-cloud.</span><span class="sxs-lookup"><span data-stu-id="1b789-160">In this section, you create a Node.js console app that simulates a device that sends device-to-cloud messages tooan IoT hub.</span></span>

1. <span data-ttu-id="1b789-161">Créez un dossier vide appelé **simulateddevice**.</span><span class="sxs-lookup"><span data-stu-id="1b789-161">Create an empty folder called **simulateddevice**.</span></span> <span data-ttu-id="1b789-162">Bonjour **simulateddevice** dossier, créez un fichier package.json à l’aide de hello, la commande suivante à l’invite suivante.</span><span class="sxs-lookup"><span data-stu-id="1b789-162">In hello **simulateddevice** folder, create a package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="1b789-163">Acceptez les valeurs par défaut hello :</span><span class="sxs-lookup"><span data-stu-id="1b789-163">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="1b789-164">Votre invite de commandes Bonjour **simulateddevice** dossier, exécutez hello suivant commande tooinstall hello **azure iot-appareil** package SDK de l’appareil et **azure-iot-périphérique-mqtt**package :</span><span class="sxs-lookup"><span data-stu-id="1b789-164">At your command prompt in hello **simulateddevice** folder, run hello following command tooinstall hello **azure-iot-device** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="1b789-165">À l’aide d’un éditeur de texte, créez un **SimulatedDevice.js** fichier Bonjour **simulateddevice** dossier.</span><span class="sxs-lookup"><span data-stu-id="1b789-165">Using a text editor, create a **SimulatedDevice.js** file in hello **simulateddevice** folder.</span></span>
4. <span data-ttu-id="1b789-166">Ajoutez hello suivant `require` instructions au hello démarrent Hello **SimulatedDevice.js** fichier :</span><span class="sxs-lookup"><span data-stu-id="1b789-166">Add hello following `require` statements at hello start of hello **SimulatedDevice.js** file:</span></span>
   
    ```
    'use strict';
   
    var clientFromConnectionString = require('azure-iot-device-mqtt').clientFromConnectionString;
    var Message = require('azure-iot-device').Message;
    ```
5. <span data-ttu-id="1b789-167">Ajouter un **connectionString** variable et l’utiliser toocreate un **Client** instance.</span><span class="sxs-lookup"><span data-stu-id="1b789-167">Add a **connectionString** variable and use it toocreate a **Client** instance.</span></span> <span data-ttu-id="1b789-168">Remplacez **{youriothostname}** avec nom hello de hub IoT de hello, vous avez créé hello *créez un IoT Hub* section.</span><span class="sxs-lookup"><span data-stu-id="1b789-168">Replace **{youriothostname}** with hello name of hello IoT hub you created hello *Create an IoT Hub* section.</span></span> <span data-ttu-id="1b789-169">Remplacez **{yourdevicekey}** avec la valeur de clé de périphérique hello générées dans hello *créer une identité d’appareil* section :</span><span class="sxs-lookup"><span data-stu-id="1b789-169">Replace **{yourdevicekey}** with hello device key value you generated in hello *Create a device identity* section:</span></span>
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId=myFirstNodeDevice;SharedAccessKey={yourdevicekey}';
   
    var client = clientFromConnectionString(connectionString);
    ```
6. <span data-ttu-id="1b789-170">Ajoutez hello suivant sortie toodisplay de fonction à partir de l’application hello :</span><span class="sxs-lookup"><span data-stu-id="1b789-170">Add hello following function toodisplay output from hello application:</span></span>
   
    ```
    function printResultFor(op) {
      return function printResult(err, res) {
        if (err) console.log(op + ' error: ' + err.toString());
        if (res) console.log(op + ' status: ' + res.constructor.name);
      };
    }
    ```
7. <span data-ttu-id="1b789-171">Créer un rappel et utiliser hello **setInterval** fonction toosend un IoT hub de message tooyour chaque seconde :</span><span class="sxs-lookup"><span data-stu-id="1b789-171">Create a callback and use hello **setInterval** function toosend a message tooyour IoT hub every second:</span></span>
   
    ```
    var connectCallback = function (err) {
      if (err) {
        console.log('Could not connect: ' + err);
      } else {
        console.log('Client connected');
   
        // Create a message and send it toohello IoT Hub every second
        setInterval(function(){
            var temperature = 20 + (Math.random() * 15);
            var humidity = 60 + (Math.random() * 20);            
            var data = JSON.stringify({ deviceId: 'myFirstNodeDevice', temperature: temperature, humidity: humidity });
            var message = new Message(data);
            message.properties.add('temperatureAlert', (temperature > 30) ? 'true' : 'false');
            console.log("Sending message: " + message.getData());
            client.sendEvent(message, printResultFor('send'));
        }, 1000);
      }
    };
    ```
8. <span data-ttu-id="1b789-172">Ouvrez hello connexion tooyour IoT Hub et démarrer l’envoi de messages :</span><span class="sxs-lookup"><span data-stu-id="1b789-172">Open hello connection tooyour IoT Hub and start sending messages:</span></span>
   
    ```
    client.open(connectCallback);
    ```
9. <span data-ttu-id="1b789-173">Enregistrez et fermez hello **SimulatedDevice.js** fichier.</span><span class="sxs-lookup"><span data-stu-id="1b789-173">Save and close hello **SimulatedDevice.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="1b789-174">tookeep les choses simples, ce didacticiel n’implémente pas de toute stratégie de nouvelle tentative.</span><span class="sxs-lookup"><span data-stu-id="1b789-174">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="1b789-175">Dans le code de production, vous devez implémenter des stratégies de nouvelle tentative (par exemple, une interruption exponentielle), comme indiqué dans l’article hello [gestion des pannes temporaires][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="1b789-175">In production code, you should implement retry policies (such as an exponential backoff), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 

## <a name="run-hello-apps"></a><span data-ttu-id="1b789-176">Exécuter des applications de hello</span><span class="sxs-lookup"><span data-stu-id="1b789-176">Run hello apps</span></span>
<span data-ttu-id="1b789-177">Vous êtes maintenant prêt toorun hello applications.</span><span class="sxs-lookup"><span data-stu-id="1b789-177">You are now ready toorun hello apps.</span></span>

1. <span data-ttu-id="1b789-178">À l’invite de commande Bonjour **readdevicetocloudmessages** dossier, exécutez hello suivant toobegin commande analyse votre IoT hub :</span><span class="sxs-lookup"><span data-stu-id="1b789-178">At a command prompt in hello **readdevicetocloudmessages** folder, run hello following command toobegin monitoring your IoT hub:</span></span>
   
    ```
    node ReadDeviceToCloudMessages.js 
    ```
   
    ![Messages de l’appareil-à-cloud Node.js IoT Hub service application toomonitor][7]
2. <span data-ttu-id="1b789-180">À l’invite de commande Bonjour **simulateddevice** dossier, exécutez hello suivant toobegin commande envoi tooyour IoT hub de télémétrie des données :</span><span class="sxs-lookup"><span data-stu-id="1b789-180">At a command prompt in hello **simulateddevice** folder, run hello following command toobegin sending telemetry data tooyour IoT hub:</span></span>
   
    ```
    node SimulatedDevice.js
    ```
   
    ![Messages de l’appareil-à-cloud Node.js IoT Hub appareil application toosend][8]
3. <span data-ttu-id="1b789-182">Hello **utilisation** vignette Bonjour [portail Azure] [ lnk-portal] affiche hello le nombre de messages envoyés toohello IoT hub :</span><span class="sxs-lookup"><span data-stu-id="1b789-182">hello **Usage** tile in hello [Azure portal][lnk-portal] shows hello number of messages sent toohello IoT hub:</span></span>
   
    ![Azure portail d’utilisation vignette affichage du nombre de messages envoyés tooIoT Hub][43]

## <a name="next-steps"></a><span data-ttu-id="1b789-184">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1b789-184">Next steps</span></span>
<span data-ttu-id="1b789-185">Dans ce didacticiel, vous configuré un IoT hub Bonjour portail Azure et ensuite créé une identité d’appareil dans le Registre des identités de hello IoT hub.</span><span class="sxs-lookup"><span data-stu-id="1b789-185">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="1b789-186">Vous avez utilisé ce périphérique identité tooenable hello simulée appareil application toosend messages appareil-à-cloud toohello hub IoT.</span><span class="sxs-lookup"><span data-stu-id="1b789-186">You used this device identity tooenable hello simulated device app toosend device-to-cloud messages toohello IoT hub.</span></span> <span data-ttu-id="1b789-187">Vous avez créé également une application qui affiche les messages hello reçus par IoT hub de hello.</span><span class="sxs-lookup"><span data-stu-id="1b789-187">You also created an app that displays hello messages received by hello IoT hub.</span></span> 

<span data-ttu-id="1b789-188">toocontinue mise en route avec IoT Hub et tooexplore autres scénarios IoT, consultez :</span><span class="sxs-lookup"><span data-stu-id="1b789-188">toocontinue getting started with IoT Hub and tooexplore other IoT scenarios, see:</span></span>

* <span data-ttu-id="1b789-189">[Connexion de votre appareil][lnk-connect-device]</span><span class="sxs-lookup"><span data-stu-id="1b789-189">[Connecting your device][lnk-connect-device]</span></span>
* <span data-ttu-id="1b789-190">[Prise en main de la gestion d’appareils][lnk-device-management]</span><span class="sxs-lookup"><span data-stu-id="1b789-190">[Getting started with device management][lnk-device-management]</span></span>
* <span data-ttu-id="1b789-191">[Explore Azure IoT Edge architecture on Linux][lnk-iot-edge] (Découvrir l’architecture Azure IoT Edge sur Linux)</span><span class="sxs-lookup"><span data-stu-id="1b789-191">[Getting started with Azure IoT Edge][lnk-iot-edge]</span></span>

<span data-ttu-id="1b789-192">toolearn tooextend vos messages IoT solution et des processus de périphérique dans le cloud à grande échelle, voir hello [traiter les messages appareil-à-cloud] [ lnk-process-d2c-tutorial] didacticiel.</span><span class="sxs-lookup"><span data-stu-id="1b789-192">toolearn how tooextend your IoT solution and process device-to-cloud messages at scale, see hello [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span></span>
[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]


<!-- Images. -->
[7]: ./media/iot-hub-node-node-getstarted/runapp1.png
[8]: ./media/iot-hub-node-node-getstarted/runapp2.png
[43]: ./media/iot-hub-csharp-csharp-getstarted/usage.png

<!-- Links -->
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[lnk-eventhubs-tutorial]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md
[lnk-devguide-identity]: iot-hub-devguide-identity-registry.md
[lnk-event-hubs-overview]: ../event-hubs/event-hubs-overview.md

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md
[lnk-process-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-portal]: https://portal.azure.com/

[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/
