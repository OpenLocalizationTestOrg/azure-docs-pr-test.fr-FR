---
title: "Présentation de la prise en charge de MQTT au niveau d’Azure IoT Hub | Microsoft Docs"
description: "Guide du développeur : prise en charge des appareils se connectant à un point de terminaison IoT Hub côté appareil en utilisant le protocole MQTT. Inclut des informations sur la prise en charge intégrée de MQTT dans les Azure IoT device SDK."
services: iot-hub
documentationcenter: .net
author: kdotchkoff
manager: timlt
editor: 
ms.assetid: 1d71c27c-b466-4a40-b95b-d6550cf85144
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/11/2017
ms.author: kdotchko
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: eab70c1aa9c49a137c2ac1012449d57915fb0d27
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="communicate-with-your-iot-hub-using-the-mqtt-protocol"></a><span data-ttu-id="4ae2b-104">Communication avec votre IoT Hub à l’aide du protocole MQTT</span><span class="sxs-lookup"><span data-stu-id="4ae2b-104">Communicate with your IoT hub using the MQTT protocol</span></span>

<span data-ttu-id="4ae2b-105">Grâce à IoT Hub, les appareils peuvent communiquer avec les points de terminaison d’appareil IoT Hub à l’aide du protocole [MQTT v3.1.1][lnk-mqtt-org] sur le port 8883 ou de MQTT v3.1.1 via le protocole WebSocket sur le port 443.</span><span class="sxs-lookup"><span data-stu-id="4ae2b-105">IoT Hub enables devices to communicate with the IoT Hub device endpoints using the [MQTT v3.1.1][lnk-mqtt-org] protocol on port 8883 or MQTT v3.1.1 over WebSocket protocol on port 443.</span></span> <span data-ttu-id="4ae2b-106">IoT Hub nécessite que toutes les communications de l’appareil soient sécurisées à l’aide de TLS/SSL (donc IoT Hub ne prend en charge les connexions non sécurisées sur le port 1883).</span><span class="sxs-lookup"><span data-stu-id="4ae2b-106">IoT Hub requires all device communication to be secured using TLS/SSL (hence, IoT Hub doesn’t support non-secure connections over port 1883).</span></span>

## <a name="connecting-to-iot-hub"></a><span data-ttu-id="4ae2b-107">Connexion à IoT Hub</span><span class="sxs-lookup"><span data-stu-id="4ae2b-107">Connecting to IoT Hub</span></span>

<span data-ttu-id="4ae2b-108">Un appareil peut utiliser le protocole MQTT pour se connecter à un IoT Hub, soit en utilisant les bibliothèques disponibles dans les [Kits de développement logiciel (SDK) Azure IoT][lnk-device-sdks], soit en utilisant directement le protocole MQTT.</span><span class="sxs-lookup"><span data-stu-id="4ae2b-108">A device can use the MQTT protocol to connect to an IoT hub either by using the libraries in the [Azure IoT SDKs][lnk-device-sdks] or by using the MQTT protocol directly.</span></span>

## <a name="using-the-device-sdks"></a><span data-ttu-id="4ae2b-109">Utilisation des Kits device SDK</span><span class="sxs-lookup"><span data-stu-id="4ae2b-109">Using the device SDKs</span></span>

<span data-ttu-id="4ae2b-110">Les [Kits device SDK][lnk-device-sdks] qui prennent en charge le protocole MQTT sont disponibles pour Java, Node.js, C, C# et Python.</span><span class="sxs-lookup"><span data-stu-id="4ae2b-110">[Device SDKs][lnk-device-sdks] that support the MQTT protocol are available for Java, Node.js, C, C#, and Python.</span></span> <span data-ttu-id="4ae2b-111">Les Kits device SDK utilisent la chaîne de connexion IoT Hub standard pour établir une connexion à un IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="4ae2b-111">The device SDKs use the standard IoT Hub connection string to establish a connection to an IoT hub.</span></span> <span data-ttu-id="4ae2b-112">Pour utiliser le protocole MQTT, le paramètre de protocole du client doit être défini sur **MQTT**.</span><span class="sxs-lookup"><span data-stu-id="4ae2b-112">To use the MQTT protocol, the client protocol parameter must be set to **MQTT**.</span></span> <span data-ttu-id="4ae2b-113">Par défaut, les Kits device SDK se connectent à un IoT Hub avec l’indicateur **CleanSession** défini sur **0**, et utilisent **QoS 1** pour l’échange de messages avec l’IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="4ae2b-113">By default, the device SDKs connect to an IoT Hub with the **CleanSession** flag set to **0** and use **QoS 1** for message exchange with the IoT hub.</span></span>

<span data-ttu-id="4ae2b-114">Quand un appareil est connecté à un IoT Hub, les Kits device SDK fournissent des méthodes qui permettent à l’appareil d’envoyer des messages et d’en recevoir à partir d’un IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="4ae2b-114">When a device is connected to an IoT hub, the device SDKs provide methods that enable the device to send messages to and receive messages from an IoT hub.</span></span>

<span data-ttu-id="4ae2b-115">Le tableau suivant contient des liens vers des exemples de code pour chaque langage pris en charge et spécifie les paramètres à utiliser pour établir une connexion à IoT Hub à l’aide du protocole MQTT.</span><span class="sxs-lookup"><span data-stu-id="4ae2b-115">The following table contains links to code samples for each supported language and specifies the parameter to use to establish a connection to IoT Hub using the MQTT protocol.</span></span>

| <span data-ttu-id="4ae2b-116">Langage</span><span class="sxs-lookup"><span data-stu-id="4ae2b-116">Language</span></span> | <span data-ttu-id="4ae2b-117">Paramètre de protocole</span><span class="sxs-lookup"><span data-stu-id="4ae2b-117">Protocol parameter</span></span> |
| --- | --- |
| <span data-ttu-id="4ae2b-118">[Node.js][lnk-sample-node]</span><span class="sxs-lookup"><span data-stu-id="4ae2b-118">[Node.js][lnk-sample-node]</span></span> |<span data-ttu-id="4ae2b-119">azure-iot-device-mqtt</span><span class="sxs-lookup"><span data-stu-id="4ae2b-119">azure-iot-device-mqtt</span></span> |
| <span data-ttu-id="4ae2b-120">[Java][lnk-sample-java]</span><span class="sxs-lookup"><span data-stu-id="4ae2b-120">[Java][lnk-sample-java]</span></span> |<span data-ttu-id="4ae2b-121">IotHubClientProtocol.MQTT</span><span class="sxs-lookup"><span data-stu-id="4ae2b-121">IotHubClientProtocol.MQTT</span></span> |
| <span data-ttu-id="4ae2b-122">[C][lnk-sample-c]</span><span class="sxs-lookup"><span data-stu-id="4ae2b-122">[C][lnk-sample-c]</span></span> |<span data-ttu-id="4ae2b-123">MQTT_Protocol</span><span class="sxs-lookup"><span data-stu-id="4ae2b-123">MQTT_Protocol</span></span> |
| <span data-ttu-id="4ae2b-124">[C#][lnk-sample-csharp]</span><span class="sxs-lookup"><span data-stu-id="4ae2b-124">[C#][lnk-sample-csharp]</span></span> |<span data-ttu-id="4ae2b-125">TransportType.Mqtt</span><span class="sxs-lookup"><span data-stu-id="4ae2b-125">TransportType.Mqtt</span></span> |
| <span data-ttu-id="4ae2b-126">[Python][lnk-sample-python]</span><span class="sxs-lookup"><span data-stu-id="4ae2b-126">[Python][lnk-sample-python]</span></span> |<span data-ttu-id="4ae2b-127">IoTHubTransportProvider.MQTT</span><span class="sxs-lookup"><span data-stu-id="4ae2b-127">IoTHubTransportProvider.MQTT</span></span> |

### <a name="migrating-a-device-app-from-amqp-to-mqtt"></a><span data-ttu-id="4ae2b-128">Migration d’une application d’appareil d’AMQP vers MQTT</span><span class="sxs-lookup"><span data-stu-id="4ae2b-128">Migrating a device app from AMQP to MQTT</span></span>

<span data-ttu-id="4ae2b-129">Si vous utilisez les [Kits device SDK][lnk-device-sdks], le passage du protocole AMQP au protocole MQTT nécessite de modifier le paramètre de protocole dans l’initialisation du client comme indiqué précédemment.</span><span class="sxs-lookup"><span data-stu-id="4ae2b-129">If you are using the [device SDKs][lnk-device-sdks], switching from using AMQP to MQTT requires changing the protocol parameter in the client initialization as stated previously.</span></span>

<span data-ttu-id="4ae2b-130">Lors de cette opération, vérifiez les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="4ae2b-130">When doing so, make sure to check the following items:</span></span>

* <span data-ttu-id="4ae2b-131">AMQP retourne des erreurs pour nombreuses conditions, tandis que MQTT met fin à la connexion.</span><span class="sxs-lookup"><span data-stu-id="4ae2b-131">AMQP returns errors for many conditions, while MQTT terminates the connection.</span></span> <span data-ttu-id="4ae2b-132">Par conséquent, votre logique de gestion des exceptions peut nécessiter certaines modifications.</span><span class="sxs-lookup"><span data-stu-id="4ae2b-132">As a result your exception handling logic might require some changes.</span></span>
* <span data-ttu-id="4ae2b-133">MQTT ne prend pas en charge les opérations *reject* lors de la réception de [messages cloud-à-appareil][lnk-messaging].</span><span class="sxs-lookup"><span data-stu-id="4ae2b-133">MQTT does not support the *reject* operations when receiving [cloud-to-device messages][lnk-messaging].</span></span> <span data-ttu-id="4ae2b-134">Si votre application de serveur principal doit recevoir une réponse de l’application pour appareil, envisagez d’utiliser des [méthodes directes][lnk-methods].</span><span class="sxs-lookup"><span data-stu-id="4ae2b-134">If your back-end app needs to receive a response from the device app, consider using [direct methods][lnk-methods].</span></span>

## <a name="using-the-mqtt-protocol-directly"></a><span data-ttu-id="4ae2b-135">Utilisation directe du protocole MQTT</span><span class="sxs-lookup"><span data-stu-id="4ae2b-135">Using the MQTT protocol directly</span></span>
<span data-ttu-id="4ae2b-136">Si un appareil ne peut pas utiliser les Kits device SDK, il peut toujours se connecter aux points de terminaison d’appareil publics à l’aide du protocole MQTT sur le port 8883.</span><span class="sxs-lookup"><span data-stu-id="4ae2b-136">If a device cannot use the device SDKs, it can still connect to the public device endpoints using the MQTT protocol on port 8883.</span></span> <span data-ttu-id="4ae2b-137">Dans le paquet **CONNECT** , l’appareil doit utiliser les valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="4ae2b-137">In the **CONNECT** packet the device should use the following values:</span></span>

* <span data-ttu-id="4ae2b-138">Pour le champ **ClientId**, utilisez le **deviceId**.</span><span class="sxs-lookup"><span data-stu-id="4ae2b-138">For the **ClientId** field, use the **deviceId**.</span></span>
* <span data-ttu-id="4ae2b-139">Dans le champ **Username**, utilisez `{iothubhostname}/{device_id}/api-version=2016-11-14`, où {iothubhostname} est l’enregistrement CName complet du IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="4ae2b-139">For the **Username** field, use `{iothubhostname}/{device_id}/api-version=2016-11-14`, where {iothubhostname} is the full CName of the IoT hub.</span></span>

    <span data-ttu-id="4ae2b-140">Par exemple, si le nom de votre IoT Hub est **contoso.azure-devices.net** et si le nom de votre appareil est **MyDevice01**, le champ **Username** complet doit contenir `contoso.azure-devices.net/MyDevice01/api-version=2016-11-14`.</span><span class="sxs-lookup"><span data-stu-id="4ae2b-140">For example, if the name of your IoT hub is **contoso.azure-devices.net** and if the name of your device is **MyDevice01**, the full **Username** field should contain `contoso.azure-devices.net/MyDevice01/api-version=2016-11-14`.</span></span>
* <span data-ttu-id="4ae2b-141">Dans le champ **Password**, utilisez un jeton SAP.</span><span class="sxs-lookup"><span data-stu-id="4ae2b-141">For the **Password** field, use a SAS token.</span></span> <span data-ttu-id="4ae2b-142">Le format du jeton SAP est identique pour les protocoles HTTP et AMQP : </span><span class="sxs-lookup"><span data-stu-id="4ae2b-142">The format of the SAS token is the same as for both the HTTP and AMQP protocols:</span></span><br/><span data-ttu-id="4ae2b-143">`SharedAccessSignature sig={signature-string}&se={expiry}&sr={URL-encoded-resourceURI}`.</span><span class="sxs-lookup"><span data-stu-id="4ae2b-143">`SharedAccessSignature sig={signature-string}&se={expiry}&sr={URL-encoded-resourceURI}`.</span></span>

    <span data-ttu-id="4ae2b-144">Pour plus d’informations sur la génération de jetons SAP, consultez la section consacrée aux appareils dans la rubrique [Utilisation de jetons de sécurité IoT Hub][lnk-sas-tokens].</span><span class="sxs-lookup"><span data-stu-id="4ae2b-144">For more information about how to generate SAS tokens, see the device section of [Using IoT Hub security tokens][lnk-sas-tokens].</span></span>

    <span data-ttu-id="4ae2b-145">Lors du test, vous pouvez également utiliser l’outil [Explorateur d’appareils][lnk-device-explorer] pour générer rapidement un jeton SAP à copier et coller dans votre propre code :</span><span class="sxs-lookup"><span data-stu-id="4ae2b-145">When testing, you can also use the [device explorer][lnk-device-explorer] tool to quickly generate a SAS token that you can copy and paste into your own code:</span></span>

  1. <span data-ttu-id="4ae2b-146">Accédez à l’onglet **Management** (Gestion) de **l’Explorateur d’appareils**.</span><span class="sxs-lookup"><span data-stu-id="4ae2b-146">Go to the **Management** tab in **Device Explorer**.</span></span>
  2. <span data-ttu-id="4ae2b-147">Cliquez sur **SAS Token** (Jeton SAP) en haut à droite.</span><span class="sxs-lookup"><span data-stu-id="4ae2b-147">Click **SAS Token** (top right).</span></span>
  3. <span data-ttu-id="4ae2b-148">Dans **SASTokenForm**, sélectionnez votre appareil dans la liste déroulante **DeviceID**.</span><span class="sxs-lookup"><span data-stu-id="4ae2b-148">On **SASTokenForm**, select your device in the **DeviceID** drop down.</span></span> <span data-ttu-id="4ae2b-149">Définissez votre **TTL**(Durée de vie).</span><span class="sxs-lookup"><span data-stu-id="4ae2b-149">Set your **TTL**.</span></span>
  4. <span data-ttu-id="4ae2b-150">Cliquez sur **Generate** (Générer) pour créer votre jeton.</span><span class="sxs-lookup"><span data-stu-id="4ae2b-150">Click **Generate** to create your token.</span></span>

     <span data-ttu-id="4ae2b-151">Le jeton SAP généré présente la structure suivante : `HostName={your hub name}.azure-devices.net;DeviceId=javadevice;SharedAccessSignature=SharedAccessSignature sr={your hub name}.azure-devices.net%2Fdevices%2FMyDevice01%2Fapi-version%3D2016-11-14&sig=vSgHBMUG.....Ntg%3d&se=1456481802`.</span><span class="sxs-lookup"><span data-stu-id="4ae2b-151">The SAS token that's generated has this structure: `HostName={your hub name}.azure-devices.net;DeviceId=javadevice;SharedAccessSignature=SharedAccessSignature sr={your hub name}.azure-devices.net%2Fdevices%2FMyDevice01%2Fapi-version%3D2016-11-14&sig=vSgHBMUG.....Ntg%3d&se=1456481802`.</span></span>

     <span data-ttu-id="4ae2b-152">La partie de ce jeton à utiliser dans le champ **Password** (Mot de passe) pour la connexion avec le protocole MQTT est : `SharedAccessSignature sr={your hub name}.azure-devices.net%2Fdevices%2FMyDevice01%2Fapi-version%3D2016-11-14&sig=vSgHBMUG.....Ntg%3d&se=1456481802`.</span><span class="sxs-lookup"><span data-stu-id="4ae2b-152">The part of this token to use as the **Password** field to connect using MQTT is: `SharedAccessSignature sr={your hub name}.azure-devices.net%2Fdevices%2FMyDevice01%2Fapi-version%3D2016-11-14&sig=vSgHBMUG.....Ntg%3d&se=1456481802`.</span></span>

<span data-ttu-id="4ae2b-153">Pour les paquets de connexion et de déconnexion MQTT, IoT Hub émet un événement sur le canal **Surveillance des opérations** avec des informations supplémentaires qui peuvent vous aider à résoudre les problèmes de connectivité.</span><span class="sxs-lookup"><span data-stu-id="4ae2b-153">For MQTT connect and disconnect packets, IoT Hub issues an event on the **Operations Monitoring** channel with additional information that can help you to troubleshoot connectivity issues.</span></span>

### <a name="sending-device-to-cloud-messages"></a><span data-ttu-id="4ae2b-154">Envoi de messages appareil-à-cloud</span><span class="sxs-lookup"><span data-stu-id="4ae2b-154">Sending device-to-cloud messages</span></span>

<span data-ttu-id="4ae2b-155">Après avoir correctement établi une connexion, un appareil peut envoyer des messages à IoT Hub en utilisant `devices/{device_id}/messages/events/` ou `devices/{device_id}/messages/events/{property_bag}` en tant que **Nom de la rubrique**.</span><span class="sxs-lookup"><span data-stu-id="4ae2b-155">After making a successful connection, a device can send messages to IoT Hub using `devices/{device_id}/messages/events/` or `devices/{device_id}/messages/events/{property_bag}` as a **Topic Name**.</span></span> <span data-ttu-id="4ae2b-156">L’élément `{property_bag}` permet à l’appareil d’envoyer des messages avec des propriétés supplémentaires dans un format codé URL.</span><span class="sxs-lookup"><span data-stu-id="4ae2b-156">The `{property_bag}` element enables the device to send messages with additional properties in a url-encoded format.</span></span> <span data-ttu-id="4ae2b-157">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="4ae2b-157">For example:</span></span>

```
RFC 2396-encoded(<PropertyName1>)=RFC 2396-encoded(<PropertyValue1>)&RFC 2396-encoded(<PropertyName2>)=RFC 2396-encoded(<PropertyValue2>)…
```

> [!NOTE]
> <span data-ttu-id="4ae2b-158">Cet élément `{property_bag}` utilise le même encodage que celui utilisé pour les chaînes de requête dans le protocole HTTP.</span><span class="sxs-lookup"><span data-stu-id="4ae2b-158">This `{property_bag}` element uses the same encoding as for query strings in the HTTP protocol.</span></span>
>
>

<span data-ttu-id="4ae2b-159">L’application de l’appareil peut également utiliser `devices/{device_id}/messages/events/{property_bag}` comme **nom de rubrique « Will »** pour définir des *messages « Will »* à transmettre en tant que message de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="4ae2b-159">The device app can also use `devices/{device_id}/messages/events/{property_bag}` as the **Will topic name** to define *Will messages* to be forwarded as a telemetry message.</span></span>

- <span data-ttu-id="4ae2b-160">IoT Hub ne prend pas en charge les messages QoS 2.</span><span class="sxs-lookup"><span data-stu-id="4ae2b-160">IoT Hub does not support QoS 2 messages.</span></span> <span data-ttu-id="4ae2b-161">Si un client d’appareil publie un message avec **QoS 2**, IoT Hub interrompt la connexion réseau.</span><span class="sxs-lookup"><span data-stu-id="4ae2b-161">If a device app publishes a message with **QoS 2**, IoT Hub closes the network connection.</span></span>
- <span data-ttu-id="4ae2b-162">IoT Hub ne conserve pas les messages Retain.</span><span class="sxs-lookup"><span data-stu-id="4ae2b-162">IoT Hub does not persist Retain messages.</span></span> <span data-ttu-id="4ae2b-163">Si un appareil envoie un message avec l’indicateur **RETAIN** défini sur 1, IoT Hub ajoute la propriété d’application **x-opt-retain** au message.</span><span class="sxs-lookup"><span data-stu-id="4ae2b-163">If a device sends a message with the **RETAIN** flag set to 1, IoT Hub adds the **x-opt-retain** application property to the message.</span></span> <span data-ttu-id="4ae2b-164">Dans ce cas, IoT Hub ne conserve pas le message, mais le transmet à l’application principale.</span><span class="sxs-lookup"><span data-stu-id="4ae2b-164">In this case, instead of persisting the retain message, IoT Hub passes it to the backend app.</span></span>
- <span data-ttu-id="4ae2b-165">IoT Hub ne prend en charge qu’une seule connexion MQTT active par appareil.</span><span class="sxs-lookup"><span data-stu-id="4ae2b-165">IoT Hub only supports one active MQTT connection per device.</span></span> <span data-ttu-id="4ae2b-166">Toute nouvelle connexion MQTT au nom du même ID d’appareil entraîne l’interruption de la connexion existante par IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="4ae2b-166">Any new MQTT connection on behalf of the same device ID causes IoT Hub to drop the existing connection.</span></span>

<span data-ttu-id="4ae2b-167">Pour en savoir plus, reportez-vous au [Guide du développeur de messages][lnk-messaging].</span><span class="sxs-lookup"><span data-stu-id="4ae2b-167">For more information, see [Messaging developer's guide][lnk-messaging].</span></span>

### <a name="receiving-cloud-to-device-messages"></a><span data-ttu-id="4ae2b-168">Réception de messages cloud-à-appareil</span><span class="sxs-lookup"><span data-stu-id="4ae2b-168">Receiving cloud-to-device messages</span></span>

<span data-ttu-id="4ae2b-169">Pour recevoir des messages d’IoT Hub, l’appareil doit s’abonner en utilisant un `devices/{device_id}/messages/devicebound/#` en tant que **Filtre de rubrique**.</span><span class="sxs-lookup"><span data-stu-id="4ae2b-169">To receive messages from IoT Hub, a device should subscribe using `devices/{device_id}/messages/devicebound/#` as a **Topic Filter**.</span></span> <span data-ttu-id="4ae2b-170">Le caractère générique à plusieurs niveaux **#** dans le Filtre de rubrique est utilisé uniquement pour autoriser l’appareil à recevoir des propriétés supplémentaires dans le nom de la rubrique.</span><span class="sxs-lookup"><span data-stu-id="4ae2b-170">The multi-level wildcard **#** in the Topic Filter is used only to allow the device to receive additional properties in the topic name.</span></span> <span data-ttu-id="4ae2b-171">IoT Hub n’autorise pas l’utilisation des caractères génériques **#** ou **?**</span><span class="sxs-lookup"><span data-stu-id="4ae2b-171">IoT Hub does not allow the usage of the **#** or **?**</span></span> <span data-ttu-id="4ae2b-172">pour filtrer les sous-rubriques.</span><span class="sxs-lookup"><span data-stu-id="4ae2b-172">wildcards for filtering of sub-topics.</span></span> <span data-ttu-id="4ae2b-173">Étant donné que IoT Hub n’est pas un broker de messagerie pub-sub à usage général, il prend uniquement en charge les noms de rubriques et les filtres de rubriques documentés.</span><span class="sxs-lookup"><span data-stu-id="4ae2b-173">Since IoT Hub is not a general purpose pub-sub messaging broker, it only supports the documented topic names and topic filters.</span></span>

<span data-ttu-id="4ae2b-174">L’appareil ne reçoit aucun message d’IoT Hub tant qu’il ne s’est pas abonné à son point de terminaison spécifique d’appareil, représenté par le filtre de rubrique `devices/{device_id}/messages/devicebound/#`.</span><span class="sxs-lookup"><span data-stu-id="4ae2b-174">The device does not receive any messages from IoT Hub, until it has successfully subscribed to its device-specific endpoint, represented by the `devices/{device_id}/messages/devicebound/#` topic filter.</span></span> <span data-ttu-id="4ae2b-175">Une fois l’abonnement réussi, l’appareil commence à recevoir uniquement les messages cloud-à-appareil qui lui ont été envoyés après l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="4ae2b-175">After successful subscription has been established, the device starts receiving only cloud-to-device messages that have been sent to it after the time of the subscription.</span></span> <span data-ttu-id="4ae2b-176">Si l’appareil se connecte avec l’indicateur **CleanSession** défini sur **0**, l’abonnement est rendu persistant entre les différentes sessions.</span><span class="sxs-lookup"><span data-stu-id="4ae2b-176">If the device connects with **CleanSession** flag set to **0**, the subscription is persisted across different sessions.</span></span> <span data-ttu-id="4ae2b-177">Dans ce cas, la prochaine fois qu’il se connecte avec **CleanSession 0**, l’appareil reçoit les messages en attente qui lui ont été envoyés quand il était déconnecté.</span><span class="sxs-lookup"><span data-stu-id="4ae2b-177">In this case, the next time it connects with **CleanSession 0** the device receives outstanding messages that have been sent to it while it was disconnected.</span></span> <span data-ttu-id="4ae2b-178">Si l’appareil utilise l’indicateur **CleanSession** défini sur **1**, il ne reçoit pas les messages à partir d’IoT Hub jusqu’à ce qu’il s’abonne à son point de terminaison d’appareil.</span><span class="sxs-lookup"><span data-stu-id="4ae2b-178">If the device uses **CleanSession** flag set to **1** though, it does not receive any messages from IoT Hub until it subscribes to its device-endpoint.</span></span>

<span data-ttu-id="4ae2b-179">IoT Hub remet les messages avec le **Nom de la rubrique** `devices/{device_id}/messages/devicebound/`, ou `devices/{device_id}/messages/devicebound/{property_bag}` s’il y a des propriétés de message.</span><span class="sxs-lookup"><span data-stu-id="4ae2b-179">IoT Hub delivers messages with the **Topic Name** `devices/{device_id}/messages/devicebound/`, or `devices/{device_id}/messages/devicebound/{property_bag}` if there are any message properties.</span></span> <span data-ttu-id="4ae2b-180">`{property_bag}` contient des paires clé/valeur codées URL de propriétés de message.</span><span class="sxs-lookup"><span data-stu-id="4ae2b-180">`{property_bag}` contains url-encoded key/value pairs of message properties.</span></span> <span data-ttu-id="4ae2b-181">Seules les propriétés d’application et les propriétés système définissables par l’utilisateur (comme **messageId** ou **correlationId**) sont incluses dans le jeu de propriétés.</span><span class="sxs-lookup"><span data-stu-id="4ae2b-181">Only application properties and user-settable system properties (such as **messageId** or **correlationId**) are included in the property bag.</span></span> <span data-ttu-id="4ae2b-182">Les noms de propriété système ont le préfixe **$**, tandis que les noms de propriété d’application ne sont précédés d’aucun préfixe.</span><span class="sxs-lookup"><span data-stu-id="4ae2b-182">System property names have the prefix **$**, application properties use the original property name with no prefix.</span></span>

<span data-ttu-id="4ae2b-183">Quand une application d’appareil s’abonne à une rubrique avec **QoS 2**, IoT Hub accorde le niveau QoS 1 maximal dans le paquet **SUBACK**.</span><span class="sxs-lookup"><span data-stu-id="4ae2b-183">When a device app subscribes to a topic with **QoS 2**, IoT Hub grants maximum QoS level 1 in the **SUBACK** packet.</span></span> <span data-ttu-id="4ae2b-184">Après cela, IoT Hub remet les messages à l’appareil à l’aide de QoS 1.</span><span class="sxs-lookup"><span data-stu-id="4ae2b-184">After that, IoT Hub delivers messages to the device using QoS 1.</span></span>

### <a name="retrieving-a-device-twins-properties"></a><span data-ttu-id="4ae2b-185">Récupération des propriétés d’un jumeau d’appareil</span><span class="sxs-lookup"><span data-stu-id="4ae2b-185">Retrieving a device twin's properties</span></span>

<span data-ttu-id="4ae2b-186">Tout d’abord, un appareil s’abonne à `$iothub/twin/res/#` pour recevoir les réponses de l’opération.</span><span class="sxs-lookup"><span data-stu-id="4ae2b-186">First, a device subscribes to `$iothub/twin/res/#`, to receive the operation's responses.</span></span> <span data-ttu-id="4ae2b-187">Ensuite, il envoie un message vide à la rubrique `$iothub/twin/GET/?$rid={request id}`, avec une valeur propagée pour **l’ID de la requête**.</span><span class="sxs-lookup"><span data-stu-id="4ae2b-187">Then, it sends an empty message to topic `$iothub/twin/GET/?$rid={request id}`, with a populated value for **request id**.</span></span> <span data-ttu-id="4ae2b-188">Le service envoie alors un message de réponse contenant les données de jumeau d’appareil sur la rubrique `$iothub/twin/res/{status}/?$rid={request id}`, en utilisant le même **ID de demande** que la demande.</span><span class="sxs-lookup"><span data-stu-id="4ae2b-188">The service then sends a response message containing the device twin data on topic `$iothub/twin/res/{status}/?$rid={request id}`, using the same **request id** as the request.</span></span>

<span data-ttu-id="4ae2b-189">L’ID de la requête peut avoir n’importe quelle valeur valide de propriété de message, conformément au [Guide du développeur de messages IoT Hub][lnk-messaging], et l’état est validé comme entier.</span><span class="sxs-lookup"><span data-stu-id="4ae2b-189">Request id can be any valid value for a message property value, as per [IoT Hub messaging developer's guide][lnk-messaging], and status is validated as an integer.</span></span>
<span data-ttu-id="4ae2b-190">Le corps de la réponse contient la section properties du jumeau d’appareil :</span><span class="sxs-lookup"><span data-stu-id="4ae2b-190">The response body contains the properties section of the device twin:</span></span>

<span data-ttu-id="4ae2b-191">Le corps du registre des identités est limité au membre « propriétés », par exemple :</span><span class="sxs-lookup"><span data-stu-id="4ae2b-191">The body of the identity registry entry limited to the “properties” member, for example:</span></span>

        {
            "properties": {
                "desired": {
                    "telemetrySendFrequency": "5m",
                    "$version": 12
                },
                "reported": {
                    "telemetrySendFrequency": "5m",
                    "batteryLevel": 55,
                    "$version": 123
                }
            }
        }

<span data-ttu-id="4ae2b-192">Les codes d’état possibles sont :</span><span class="sxs-lookup"><span data-stu-id="4ae2b-192">The possible status codes are:</span></span>

|<span data-ttu-id="4ae2b-193">État</span><span class="sxs-lookup"><span data-stu-id="4ae2b-193">Status</span></span> | <span data-ttu-id="4ae2b-194">Description</span><span class="sxs-lookup"><span data-stu-id="4ae2b-194">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="4ae2b-195">200</span><span class="sxs-lookup"><span data-stu-id="4ae2b-195">200</span></span> | <span data-ttu-id="4ae2b-196">Succès</span><span class="sxs-lookup"><span data-stu-id="4ae2b-196">Success</span></span> |
| <span data-ttu-id="4ae2b-197">429</span><span class="sxs-lookup"><span data-stu-id="4ae2b-197">429</span></span> | <span data-ttu-id="4ae2b-198">Trop de demandes (limité), selon la [Limitation IoT Hub][lnk-quotas]</span><span class="sxs-lookup"><span data-stu-id="4ae2b-198">Too many requests (throttled), as per [IoT Hub throttling][lnk-quotas]</span></span> |
| <span data-ttu-id="4ae2b-199">5**</span><span class="sxs-lookup"><span data-stu-id="4ae2b-199">5**</span></span> | <span data-ttu-id="4ae2b-200">Erreurs de serveur</span><span class="sxs-lookup"><span data-stu-id="4ae2b-200">Server errors</span></span> |

<span data-ttu-id="4ae2b-201">Pour en savoir plus, reportez-vous au [Guide du développeur de jumeaux d’appareil][lnk-devguide-twin].</span><span class="sxs-lookup"><span data-stu-id="4ae2b-201">For more information, see [Device twins developer's guide][lnk-devguide-twin].</span></span>

### <a name="update-device-twins-reported-properties"></a><span data-ttu-id="4ae2b-202">Mettre à jour les propriétés signalées du jumeau d’appareil</span><span class="sxs-lookup"><span data-stu-id="4ae2b-202">Update device twin's reported properties</span></span>

<span data-ttu-id="4ae2b-203">La séquence suivante décrit comment un appareil met à jour les propriétés déclarées dans le jumeau d’appareil IoT Hub :</span><span class="sxs-lookup"><span data-stu-id="4ae2b-203">The following sequence describes how a device updates the reported properties in the device twin in IoT Hub:</span></span>

1. <span data-ttu-id="4ae2b-204">Un appareil doit tout d’abord s’abonner à la rubrique `$iothub/twin/res/#` pour recevoir des réponses d’opération de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="4ae2b-204">A device must first subscribe to the `$iothub/twin/res/#` topic to receive the operation's responses from IoT Hub.</span></span>

1. <span data-ttu-id="4ae2b-205">Un appareil envoie un message qui contient la mise à jour de jumeau d’appareil pour la rubrique `$iothub/twin/PATCH/properties/reported/?$rid={request id}`.</span><span class="sxs-lookup"><span data-stu-id="4ae2b-205">A device sends a message that contains the device twin update to the `$iothub/twin/PATCH/properties/reported/?$rid={request id}` topic.</span></span> <span data-ttu-id="4ae2b-206">Ce message contient une valeur **ID de demande**.</span><span class="sxs-lookup"><span data-stu-id="4ae2b-206">This message includes a **request id** value.</span></span>

1. <span data-ttu-id="4ae2b-207">Le service envoie ensuite un message de réponse qui contient la nouvelle valeur ETag de la collection de propriétés déclarées dans la rubrique `$iothub/twin/res/{status}/?$rid={request id}`.</span><span class="sxs-lookup"><span data-stu-id="4ae2b-207">The service then sends a response message that contains the new ETag value for the reported properties collection on topic `$iothub/twin/res/{status}/?$rid={request id}`.</span></span> <span data-ttu-id="4ae2b-208">Ce message de réponse utilise le même **ID de demande** que la demande.</span><span class="sxs-lookup"><span data-stu-id="4ae2b-208">This response message uses the same **request id** as the request.</span></span>

<span data-ttu-id="4ae2b-209">Le corps du message contient un document JSON qui fournit de nouvelles valeurs pour les propriétés signalées (aucune autre propriété ou métadonnée ne peut être modifiée).</span><span class="sxs-lookup"><span data-stu-id="4ae2b-209">The request message body contains a JSON document, which provides new values for reported properties (no other property or metadata can be modified).</span></span>
<span data-ttu-id="4ae2b-210">Chaque membre du document JSON met à jour ou ajoute le membre correspondant dans le document du jumeau d’appareil.</span><span class="sxs-lookup"><span data-stu-id="4ae2b-210">Each member in the JSON document updates or add the corresponding member in the device twin’s document.</span></span> <span data-ttu-id="4ae2b-211">Un membre défini sur `null` supprime le membre de l’objet conteneur.</span><span class="sxs-lookup"><span data-stu-id="4ae2b-211">A member set to `null`, deletes the member from the containing object.</span></span> <span data-ttu-id="4ae2b-212">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="4ae2b-212">For example:</span></span>

        {
            "telemetrySendFrequency": "35m",
            "batteryLevel": 60
        }

<span data-ttu-id="4ae2b-213">Les codes d’état possibles sont :</span><span class="sxs-lookup"><span data-stu-id="4ae2b-213">The possible status codes are:</span></span>

|<span data-ttu-id="4ae2b-214">État</span><span class="sxs-lookup"><span data-stu-id="4ae2b-214">Status</span></span> | <span data-ttu-id="4ae2b-215">Description</span><span class="sxs-lookup"><span data-stu-id="4ae2b-215">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="4ae2b-216">200</span><span class="sxs-lookup"><span data-stu-id="4ae2b-216">200</span></span> | <span data-ttu-id="4ae2b-217">Succès</span><span class="sxs-lookup"><span data-stu-id="4ae2b-217">Success</span></span> |
| <span data-ttu-id="4ae2b-218">400</span><span class="sxs-lookup"><span data-stu-id="4ae2b-218">400</span></span> | <span data-ttu-id="4ae2b-219">Demande incorrecte.</span><span class="sxs-lookup"><span data-stu-id="4ae2b-219">Bad Request.</span></span> <span data-ttu-id="4ae2b-220">JSON incorrect</span><span class="sxs-lookup"><span data-stu-id="4ae2b-220">Malformed JSON</span></span> |
| <span data-ttu-id="4ae2b-221">429</span><span class="sxs-lookup"><span data-stu-id="4ae2b-221">429</span></span> | <span data-ttu-id="4ae2b-222">Trop de demandes (limité), selon la [Limitation IoT Hub][lnk-quotas]</span><span class="sxs-lookup"><span data-stu-id="4ae2b-222">Too many requests (throttled), as per [IoT Hub throttling][lnk-quotas]</span></span> |
| <span data-ttu-id="4ae2b-223">5**</span><span class="sxs-lookup"><span data-stu-id="4ae2b-223">5**</span></span> | <span data-ttu-id="4ae2b-224">Erreurs de serveur</span><span class="sxs-lookup"><span data-stu-id="4ae2b-224">Server errors</span></span> |

<span data-ttu-id="4ae2b-225">Pour en savoir plus, reportez-vous au [Guide du développeur de jumeaux d’appareil][lnk-devguide-twin].</span><span class="sxs-lookup"><span data-stu-id="4ae2b-225">For more information, see [Device twins developer's guide][lnk-devguide-twin].</span></span>

### <a name="receiving-desired-properties-update-notifications"></a><span data-ttu-id="4ae2b-226">Réception de notifications de mise à jour des propriétés souhaitées</span><span class="sxs-lookup"><span data-stu-id="4ae2b-226">Receiving desired properties update notifications</span></span>

<span data-ttu-id="4ae2b-227">Lorsqu’un appareil est connecté, IoT Hub envoie des notifications à la rubrique `$iothub/twin/PATCH/properties/desired/?$version={new version}`, qui contient le contenu de la mise à jour effectuée par le serveur principal de la solution.</span><span class="sxs-lookup"><span data-stu-id="4ae2b-227">When a device is connected, IoT Hub sends notifications to the topic `$iothub/twin/PATCH/properties/desired/?$version={new version}`, which contain the content of the update performed by the solution back end.</span></span> <span data-ttu-id="4ae2b-228">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="4ae2b-228">For example:</span></span>

        {
            "telemetrySendFrequency": "5m",
            "route": null
        }

<span data-ttu-id="4ae2b-229">Comme pour les mises à jour de propriétés, les valeurs `null` signifient que le membre de l’objet JSON est en cours de suppression.</span><span class="sxs-lookup"><span data-stu-id="4ae2b-229">As for property updates, `null` values means that the JSON object member is being deleted.</span></span>


> [!IMPORTANT] 
> <span data-ttu-id="4ae2b-230">IoT Hub génère des notifications de modification uniquement lorsque les appareils sont connectés.</span><span class="sxs-lookup"><span data-stu-id="4ae2b-230">IoT Hub generates change notifications only when devices are connected.</span></span> <span data-ttu-id="4ae2b-231">Veillez à implémenter le [flux de reconnexion des appareils][lnk-devguide-twin-reconnection] pour maintenir la synchronisation des propriétés souhaitées entre IoT Hub et l’application pour appareil.</span><span class="sxs-lookup"><span data-stu-id="4ae2b-231">Make sure to implement the [device reconnection flow][lnk-devguide-twin-reconnection] to keep the desired properties synchronized between IoT Hub and the device app.</span></span>

<span data-ttu-id="4ae2b-232">Pour en savoir plus, reportez-vous au [Guide du développeur de jumeaux d’appareil][lnk-devguide-twin].</span><span class="sxs-lookup"><span data-stu-id="4ae2b-232">For more information, see [Device twins developer's guide][lnk-devguide-twin].</span></span>

### <a name="respond-to-a-direct-method"></a><span data-ttu-id="4ae2b-233">Répondre à une méthode directe</span><span class="sxs-lookup"><span data-stu-id="4ae2b-233">Respond to a direct method</span></span>

<span data-ttu-id="4ae2b-234">Tout d’abord, un appareil doit s’abonner à `$iothub/methods/POST/#`.</span><span class="sxs-lookup"><span data-stu-id="4ae2b-234">First, a device has to subscribe to `$iothub/methods/POST/#`.</span></span> <span data-ttu-id="4ae2b-235">IoT Hub envoie des requêtes de méthodes à la rubrique `$iothub/methods/POST/{method name}/?$rid={request id}`, avec un corps vide ou un code JSON valide.</span><span class="sxs-lookup"><span data-stu-id="4ae2b-235">IoT Hub sends method requests to the topic `$iothub/methods/POST/{method name}/?$rid={request id}`, with either a valid JSON or an empty body.</span></span>

<span data-ttu-id="4ae2b-236">Pour répondre, l’appareil envoie un message avec un corps vide ou un code JSON valide à la rubrique `$iothub/methods/res/{status}/?$rid={request id}`, où **l’ID de la demande** doit correspondre à celui du message de la demande, et **l’état** doit être un entier.</span><span class="sxs-lookup"><span data-stu-id="4ae2b-236">To respond, the device sends a message with a valid JSON or empty body to the topic `$iothub/methods/res/{status}/?$rid={request id}`, where **request id** has to match the one in the request message, and **status** has to be an integer.</span></span>

<span data-ttu-id="4ae2b-237">Pour en savoir plus, reportez-vous au [Guide du développeur de méthodes directes][lnk-methods].</span><span class="sxs-lookup"><span data-stu-id="4ae2b-237">For more information, see [Direct method developer's guide][lnk-methods].</span></span>

### <a name="additional-considerations"></a><span data-ttu-id="4ae2b-238">Considérations supplémentaires</span><span class="sxs-lookup"><span data-stu-id="4ae2b-238">Additional considerations</span></span>

<span data-ttu-id="4ae2b-239">Enfin, si vous devez personnaliser le comportement du protocole MQTT du côté du cloud, il est important de consulter la section [Passerelle de protocole Azure IoT][lnk-azure-protocol-gateway], qui explique comment déployer une passerelle personnalisée hautes performances communiquant directement avec IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="4ae2b-239">As a final consideration, if you need to customize the MQTT protocol behavior on the cloud side, you should review the [Azure IoT protocol gateway][lnk-azure-protocol-gateway] that enables you to deploy a high-performance custom protocol gateway that interfaces directly with IoT Hub.</span></span> <span data-ttu-id="4ae2b-240">La passerelle de protocole Azure IoT vous permet de personnaliser le protocole de l’appareil pour prendre en charge des déploiements MQTT de type « brownfield » ou autres protocoles personnalisés.</span><span class="sxs-lookup"><span data-stu-id="4ae2b-240">The Azure IoT protocol gateway enables you to customize the device protocol to accommodate brownfield MQTT deployments or other custom protocols.</span></span> <span data-ttu-id="4ae2b-241">Toutefois, cette approche nécessite l’exécution et l’utilisation d’une passerelle de protocole personnalisée.</span><span class="sxs-lookup"><span data-stu-id="4ae2b-241">This approach does require, however, that you run and operate a custom protocol gateway.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4ae2b-242">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4ae2b-242">Next steps</span></span>

<span data-ttu-id="4ae2b-243">Pour en savoir plus sur le protocole MQTT, consultez la [documentation de MQTT][lnk-mqtt-docs].</span><span class="sxs-lookup"><span data-stu-id="4ae2b-243">To learn more about the MQTT protocol, see the [MQTT documentation][lnk-mqtt-docs].</span></span>

<span data-ttu-id="4ae2b-244">Pour en savoir plus sur la planification de votre déploiement IoT Hub, consultez :</span><span class="sxs-lookup"><span data-stu-id="4ae2b-244">To learn more about planning your IoT Hub deployment, see:</span></span>

* <span data-ttu-id="4ae2b-245">[Catalogue d’appareils certifiés Azure pour l’IoT][lnk-devices]</span><span class="sxs-lookup"><span data-stu-id="4ae2b-245">[Azure Certified for IoT device catalog][lnk-devices]</span></span>
* <span data-ttu-id="4ae2b-246">[Prendre en charge des protocoles supplémentaires][lnk-protocols]</span><span class="sxs-lookup"><span data-stu-id="4ae2b-246">[Support additional protocols][lnk-protocols]</span></span>
* <span data-ttu-id="4ae2b-247">[Comparer à Event Hubs][lnk-compare]</span><span class="sxs-lookup"><span data-stu-id="4ae2b-247">[Compare with Event Hubs][lnk-compare]</span></span>
* <span data-ttu-id="4ae2b-248">[Mise à l’échelle, HA et DR][lnk-scaling]</span><span class="sxs-lookup"><span data-stu-id="4ae2b-248">[Scaling, HA, and DR][lnk-scaling]</span></span>

<span data-ttu-id="4ae2b-249">Pour explorer davantage les capacités de IoT Hub, consultez :</span><span class="sxs-lookup"><span data-stu-id="4ae2b-249">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="4ae2b-250">[Guide du développeur IoT Hub][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="4ae2b-250">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="4ae2b-251">[Simulation d’un appareil avec Azure IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="4ae2b-251">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

[lnk-device-sdks]: https://github.com/Azure/azure-iot-sdks
[lnk-mqtt-org]: http://mqtt.org/
[lnk-mqtt-docs]: http://mqtt.org/documentation
[lnk-sample-node]: https://github.com/Azure/azure-iot-sdk-node/blob/master/device/samples/simple_sample_device.js
[lnk-sample-java]: https://github.com/Azure/azure-iot-sdk-java/tree/master/device/samples/send-receive-sample/src/main/java/samples/com/microsoft/azure/iothub/SendReceive.java
[lnk-sample-c]: https://github.com/Azure/azure-iot-sdk-c/tree/master/iothub_client/samples/iothub_client_sample_mqtt
[lnk-sample-csharp]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/device/samples
[lnk-sample-python]: https://github.com/Azure/azure-iot-sdk-python/tree/master/device/samples
[lnk-device-explorer]: https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer
[lnk-sas-tokens]: iot-hub-devguide-security.md#use-sas-tokens-in-a-device-app
[lnk-azure-protocol-gateway]: iot-hub-protocol-gateway.md

[lnk-devices]: https://catalog.azureiotsuite.com/
[lnk-protocols]: iot-hub-protocol-gateway.md
[lnk-compare]: iot-hub-compare-event-hubs.md
[lnk-scaling]: iot-hub-scaling.md
[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md

[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-messaging]: iot-hub-devguide-messaging.md

[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-devguide-twin-reconnection]: iot-hub-devguide-device-twins.md#device-reconnection-flow
[lnk-devguide-twin]: iot-hub-devguide-device-twins.md
