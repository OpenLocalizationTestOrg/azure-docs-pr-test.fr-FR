---
title: aaaUnderstand prise en charge Azure IoT Hub MQTT | Documents Microsoft
description: "Développeur guide - prise en charge des appareils qui se connectent tooan à l’aide de point de terminaison IoT Hub périphérique hello protocole MQTT. Contient des informations sur la prise en charge intégrée de MQTT Bonjour kits de développement logiciel Azure IoT appareil."
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
ms.openlocfilehash: e461687963138987acdf1f4e0e34c453744ea191
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="communicate-with-your-iot-hub-using-hello-mqtt-protocol"></a><span data-ttu-id="89fd6-104">Communiquer avec votre IoT hub à l’aide du protocole MQTT hello</span><span class="sxs-lookup"><span data-stu-id="89fd6-104">Communicate with your IoT hub using hello MQTT protocol</span></span>

<span data-ttu-id="89fd6-105">IoT Hub permet de périphériques toocommunicate avec points de terminaison appareil de Hub IoT hello à l’aide de hello [MQTT v3.1.1] [ lnk-mqtt-org] protocole sur le port 8883 ou v3.1.1 MQTT via le protocole WebSocket sur le port 443.</span><span class="sxs-lookup"><span data-stu-id="89fd6-105">IoT Hub enables devices toocommunicate with hello IoT Hub device endpoints using hello [MQTT v3.1.1][lnk-mqtt-org] protocol on port 8883 or MQTT v3.1.1 over WebSocket protocol on port 443.</span></span> <span data-ttu-id="89fd6-106">IoT Hub nécessite tous les toobe de communication de périphérique sécurisé à l’aide de TLS/SSL (donc IoT Hub ne prend en charge des connexions non sécurisées sur le port 1883).</span><span class="sxs-lookup"><span data-stu-id="89fd6-106">IoT Hub requires all device communication toobe secured using TLS/SSL (hence, IoT Hub doesn’t support non-secure connections over port 1883).</span></span>

## <a name="connecting-tooiot-hub"></a><span data-ttu-id="89fd6-107">Connexion tooIoT Hub</span><span class="sxs-lookup"><span data-stu-id="89fd6-107">Connecting tooIoT Hub</span></span>

<span data-ttu-id="89fd6-108">Un périphérique peut utiliser l’hello MQTT protocole tooconnect tooan IoT hub à l’aide de bibliothèques hello Bonjour [kits de développement logiciel Azure IoT] [ lnk-device-sdks] ou en utilisant le protocole MQTT hello directement.</span><span class="sxs-lookup"><span data-stu-id="89fd6-108">A device can use hello MQTT protocol tooconnect tooan IoT hub either by using hello libraries in hello [Azure IoT SDKs][lnk-device-sdks] or by using hello MQTT protocol directly.</span></span>

## <a name="using-hello-device-sdks"></a><span data-ttu-id="89fd6-109">À l’aide de l’appareil hello kits de développement logiciel</span><span class="sxs-lookup"><span data-stu-id="89fd6-109">Using hello device SDKs</span></span>

<span data-ttu-id="89fd6-110">[Kits de développement logiciel appareil] [ lnk-device-sdks] que hello prise en charge de protocole MQTT sont disponibles pour Java, Node.js, C, C# et Python.</span><span class="sxs-lookup"><span data-stu-id="89fd6-110">[Device SDKs][lnk-device-sdks] that support hello MQTT protocol are available for Java, Node.js, C, C#, and Python.</span></span> <span data-ttu-id="89fd6-111">l’appareil Hello kits de développement logiciel utiliser hello standard IoT Hub connexion chaîne tooestablish un IoT hub de connexion tooan.</span><span class="sxs-lookup"><span data-stu-id="89fd6-111">hello device SDKs use hello standard IoT Hub connection string tooestablish a connection tooan IoT hub.</span></span> <span data-ttu-id="89fd6-112">protocole MQTT toouse hello, paramètre de protocole de hello client doit être défini trop**MQTT**.</span><span class="sxs-lookup"><span data-stu-id="89fd6-112">toouse hello MQTT protocol, hello client protocol parameter must be set too**MQTT**.</span></span> <span data-ttu-id="89fd6-113">Par défaut, le périphérique hello kits de développement logiciel se connecter tooan IoT Hub hello **CleanSession** indicateur défini trop**0** et utiliser **QoS 1** pour l’échange de messages avec IoT hub de hello.</span><span class="sxs-lookup"><span data-stu-id="89fd6-113">By default, hello device SDKs connect tooan IoT Hub with hello **CleanSession** flag set too**0** and use **QoS 1** for message exchange with hello IoT hub.</span></span>

<span data-ttu-id="89fd6-114">Quand un appareil est connecté tooan IoT hub, le périphérique hello kits de développement logiciel fournissent des méthodes qui permettent de messages de toosend appareil hello tooand recevoir des messages à partir d’un hub IoT.</span><span class="sxs-lookup"><span data-stu-id="89fd6-114">When a device is connected tooan IoT hub, hello device SDKs provide methods that enable hello device toosend messages tooand receive messages from an IoT hub.</span></span>

<span data-ttu-id="89fd6-115">Hello tableau suivant contient des liens toocode exemples pour chaque langue prise en charge et spécifie hello paramètre toouse tooestablish un tooIoT connexion concentrateur à l’aide du protocole MQTT hello.</span><span class="sxs-lookup"><span data-stu-id="89fd6-115">hello following table contains links toocode samples for each supported language and specifies hello parameter toouse tooestablish a connection tooIoT Hub using hello MQTT protocol.</span></span>

| <span data-ttu-id="89fd6-116">language</span><span class="sxs-lookup"><span data-stu-id="89fd6-116">Language</span></span> | <span data-ttu-id="89fd6-117">Paramètre de protocole</span><span class="sxs-lookup"><span data-stu-id="89fd6-117">Protocol parameter</span></span> |
| --- | --- |
| <span data-ttu-id="89fd6-118">[Node.js][lnk-sample-node]</span><span class="sxs-lookup"><span data-stu-id="89fd6-118">[Node.js][lnk-sample-node]</span></span> |<span data-ttu-id="89fd6-119">azure-iot-device-mqtt</span><span class="sxs-lookup"><span data-stu-id="89fd6-119">azure-iot-device-mqtt</span></span> |
| <span data-ttu-id="89fd6-120">[Java][lnk-sample-java]</span><span class="sxs-lookup"><span data-stu-id="89fd6-120">[Java][lnk-sample-java]</span></span> |<span data-ttu-id="89fd6-121">IotHubClientProtocol.MQTT</span><span class="sxs-lookup"><span data-stu-id="89fd6-121">IotHubClientProtocol.MQTT</span></span> |
| <span data-ttu-id="89fd6-122">[C][lnk-sample-c]</span><span class="sxs-lookup"><span data-stu-id="89fd6-122">[C][lnk-sample-c]</span></span> |<span data-ttu-id="89fd6-123">MQTT_Protocol</span><span class="sxs-lookup"><span data-stu-id="89fd6-123">MQTT_Protocol</span></span> |
| <span data-ttu-id="89fd6-124">[C#][lnk-sample-csharp]</span><span class="sxs-lookup"><span data-stu-id="89fd6-124">[C#][lnk-sample-csharp]</span></span> |<span data-ttu-id="89fd6-125">TransportType.Mqtt</span><span class="sxs-lookup"><span data-stu-id="89fd6-125">TransportType.Mqtt</span></span> |
| <span data-ttu-id="89fd6-126">[Python][lnk-sample-python]</span><span class="sxs-lookup"><span data-stu-id="89fd6-126">[Python][lnk-sample-python]</span></span> |<span data-ttu-id="89fd6-127">IoTHubTransportProvider.MQTT</span><span class="sxs-lookup"><span data-stu-id="89fd6-127">IoTHubTransportProvider.MQTT</span></span> |

### <a name="migrating-a-device-app-from-amqp-toomqtt"></a><span data-ttu-id="89fd6-128">Migration d’une application de périphérique à partir de AMQP tooMQTT</span><span class="sxs-lookup"><span data-stu-id="89fd6-128">Migrating a device app from AMQP tooMQTT</span></span>

<span data-ttu-id="89fd6-129">Si vous utilisez hello [appareil kits de développement logiciel][lnk-device-sdks], passer de l’utilisation d’AMQP tooMQTT requiert la modification des paramètres de protocole hello dans l’initialisation du client hello comme indiqué précédemment.</span><span class="sxs-lookup"><span data-stu-id="89fd6-129">If you are using hello [device SDKs][lnk-device-sdks], switching from using AMQP tooMQTT requires changing hello protocol parameter in hello client initialization as stated previously.</span></span>

<span data-ttu-id="89fd6-130">Dans ce cas, assurez-vous que toocheck hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="89fd6-130">When doing so, make sure toocheck hello following items:</span></span>

* <span data-ttu-id="89fd6-131">AMQP retourne des erreurs pour nombreuses conditions, tandis que MQTT met fin à la connexion de hello.</span><span class="sxs-lookup"><span data-stu-id="89fd6-131">AMQP returns errors for many conditions, while MQTT terminates hello connection.</span></span> <span data-ttu-id="89fd6-132">Par conséquent, votre logique de gestion des exceptions peut nécessiter certaines modifications.</span><span class="sxs-lookup"><span data-stu-id="89fd6-132">As a result your exception handling logic might require some changes.</span></span>
* <span data-ttu-id="89fd6-133">MQTT ne prend pas en charge hello *rejeter* opérations lors de la réception [messages cloud-à-appareil][lnk-messaging].</span><span class="sxs-lookup"><span data-stu-id="89fd6-133">MQTT does not support hello *reject* operations when receiving [cloud-to-device messages][lnk-messaging].</span></span> <span data-ttu-id="89fd6-134">Si votre application back-end doit tooreceive une réponse à partir de l’application hello, envisagez d’utiliser [direct de méthodes][lnk-methods].</span><span class="sxs-lookup"><span data-stu-id="89fd6-134">If your back-end app needs tooreceive a response from hello device app, consider using [direct methods][lnk-methods].</span></span>

## <a name="using-hello-mqtt-protocol-directly"></a><span data-ttu-id="89fd6-135">À l’aide de protocole MQTT hello directement</span><span class="sxs-lookup"><span data-stu-id="89fd6-135">Using hello MQTT protocol directly</span></span>
<span data-ttu-id="89fd6-136">Si un appareil ne peut pas utiliser l’appareil hello kits de développement logiciel, il peut toujours se connecter les points de terminaison toohello périphérique public à l’aide du protocole MQTT hello sur le port 8883.</span><span class="sxs-lookup"><span data-stu-id="89fd6-136">If a device cannot use hello device SDKs, it can still connect toohello public device endpoints using hello MQTT protocol on port 8883.</span></span> <span data-ttu-id="89fd6-137">Bonjour **CONNECT** dispositif de paquets hello doit utiliser hello valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="89fd6-137">In hello **CONNECT** packet hello device should use hello following values:</span></span>

* <span data-ttu-id="89fd6-138">Pourquoi **ClientId** champ, utilisez hello **deviceId**.</span><span class="sxs-lookup"><span data-stu-id="89fd6-138">For hello **ClientId** field, use hello **deviceId**.</span></span>
* <span data-ttu-id="89fd6-139">Pourquoi **nom d’utilisateur** champ, utilisez `{iothubhostname}/{device_id}/api-version=2016-11-14`, où {iothubhostname} est hello CName complète de hub IoT de hello.</span><span class="sxs-lookup"><span data-stu-id="89fd6-139">For hello **Username** field, use `{iothubhostname}/{device_id}/api-version=2016-11-14`, where {iothubhostname} is hello full CName of hello IoT hub.</span></span>

    <span data-ttu-id="89fd6-140">Par exemple, si hello nom de votre hub IoT est **contoso.azure-devices.net** et si le nom de votre appareil hello est **MyDevice01**, hello complète **nom d’utilisateur** champ doit contenir. `contoso.azure-devices.net/MyDevice01/api-version=2016-11-14`.</span><span class="sxs-lookup"><span data-stu-id="89fd6-140">For example, if hello name of your IoT hub is **contoso.azure-devices.net** and if hello name of your device is **MyDevice01**, hello full **Username** field should contain `contoso.azure-devices.net/MyDevice01/api-version=2016-11-14`.</span></span>
* <span data-ttu-id="89fd6-141">Pourquoi **mot de passe** champ, utilisez un jeton SAP.</span><span class="sxs-lookup"><span data-stu-id="89fd6-141">For hello **Password** field, use a SAS token.</span></span> <span data-ttu-id="89fd6-142">format Hello Hello jeton SAP est même hello hello HTTP et les protocoles AMQP :</span><span class="sxs-lookup"><span data-stu-id="89fd6-142">hello format of hello SAS token is hello same as for both hello HTTP and AMQP protocols:</span></span><br/><span data-ttu-id="89fd6-143">`SharedAccessSignature sig={signature-string}&se={expiry}&sr={URL-encoded-resourceURI}`.</span><span class="sxs-lookup"><span data-stu-id="89fd6-143">`SharedAccessSignature sig={signature-string}&se={expiry}&sr={URL-encoded-resourceURI}`.</span></span>

    <span data-ttu-id="89fd6-144">Pour plus d’informations sur la façon toogenerate des jetons SAS, consultez la section de périphérique de hello de [des jetons de sécurité à l’aide de IoT Hub][lnk-sas-tokens].</span><span class="sxs-lookup"><span data-stu-id="89fd6-144">For more information about how toogenerate SAS tokens, see hello device section of [Using IoT Hub security tokens][lnk-sas-tokens].</span></span>

    <span data-ttu-id="89fd6-145">Lors du test, vous pouvez également utiliser hello [Explorateur de périphérique] [ lnk-device-explorer] tooquickly de l’outil génère un jeton SAP que vous pouvez copier et coller dans votre propre code :</span><span class="sxs-lookup"><span data-stu-id="89fd6-145">When testing, you can also use hello [device explorer][lnk-device-explorer] tool tooquickly generate a SAS token that you can copy and paste into your own code:</span></span>

  1. <span data-ttu-id="89fd6-146">Accédez toohello **gestion** onglet **appareil Explorer**.</span><span class="sxs-lookup"><span data-stu-id="89fd6-146">Go toohello **Management** tab in **Device Explorer**.</span></span>
  2. <span data-ttu-id="89fd6-147">Cliquez sur **SAS Token** (Jeton SAP) en haut à droite.</span><span class="sxs-lookup"><span data-stu-id="89fd6-147">Click **SAS Token** (top right).</span></span>
  3. <span data-ttu-id="89fd6-148">Sur **SASTokenForm**, sélectionnez votre appareil dans hello **DeviceID** liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="89fd6-148">On **SASTokenForm**, select your device in hello **DeviceID** drop down.</span></span> <span data-ttu-id="89fd6-149">Définissez votre **TTL**(Durée de vie).</span><span class="sxs-lookup"><span data-stu-id="89fd6-149">Set your **TTL**.</span></span>
  4. <span data-ttu-id="89fd6-150">Cliquez sur **générer** toocreate votre jeton.</span><span class="sxs-lookup"><span data-stu-id="89fd6-150">Click **Generate** toocreate your token.</span></span>

     <span data-ttu-id="89fd6-151">Cette structure a Hello jeton SAS qui est généré : `HostName={your hub name}.azure-devices.net;DeviceId=javadevice;SharedAccessSignature=SharedAccessSignature sr={your hub name}.azure-devices.net%2Fdevices%2FMyDevice01%2Fapi-version%3D2016-11-14&sig=vSgHBMUG.....Ntg%3d&se=1456481802`.</span><span class="sxs-lookup"><span data-stu-id="89fd6-151">hello SAS token that's generated has this structure: `HostName={your hub name}.azure-devices.net;DeviceId=javadevice;SharedAccessSignature=SharedAccessSignature sr={your hub name}.azure-devices.net%2Fdevices%2FMyDevice01%2Fapi-version%3D2016-11-14&sig=vSgHBMUG.....Ntg%3d&se=1456481802`.</span></span>

     <span data-ttu-id="89fd6-152">Hello partie de ce jeton toouse comme hello **mot de passe** tooconnect de champ à l’aide de MQTT est : `SharedAccessSignature sr={your hub name}.azure-devices.net%2Fdevices%2FMyDevice01%2Fapi-version%3D2016-11-14&sig=vSgHBMUG.....Ntg%3d&se=1456481802`.</span><span class="sxs-lookup"><span data-stu-id="89fd6-152">hello part of this token toouse as hello **Password** field tooconnect using MQTT is: `SharedAccessSignature sr={your hub name}.azure-devices.net%2Fdevices%2FMyDevice01%2Fapi-version%3D2016-11-14&sig=vSgHBMUG.....Ntg%3d&se=1456481802`.</span></span>

<span data-ttu-id="89fd6-153">Pour MQTT se connecter et se déconnecter de paquets, IoT Hub émet un événement sur hello **opérations analyse** canal avec des informations supplémentaires qui peuvent vous aider à tootroubleshoot des problèmes de connectivité.</span><span class="sxs-lookup"><span data-stu-id="89fd6-153">For MQTT connect and disconnect packets, IoT Hub issues an event on hello **Operations Monitoring** channel with additional information that can help you tootroubleshoot connectivity issues.</span></span>

### <a name="sending-device-to-cloud-messages"></a><span data-ttu-id="89fd6-154">Envoi de messages appareil-à-cloud</span><span class="sxs-lookup"><span data-stu-id="89fd6-154">Sending device-to-cloud messages</span></span>

<span data-ttu-id="89fd6-155">Après avoir établi une connexion réussie, un appareil peut envoyer à l’aide de messages tooIoT Hub `devices/{device_id}/messages/events/` ou `devices/{device_id}/messages/events/{property_bag}` comme un **nom de la rubrique**.</span><span class="sxs-lookup"><span data-stu-id="89fd6-155">After making a successful connection, a device can send messages tooIoT Hub using `devices/{device_id}/messages/events/` or `devices/{device_id}/messages/events/{property_bag}` as a **Topic Name**.</span></span> <span data-ttu-id="89fd6-156">Hello `{property_bag}` élément permet de messages de toosend hello appareil avec des propriétés supplémentaires dans un format encodé en url.</span><span class="sxs-lookup"><span data-stu-id="89fd6-156">hello `{property_bag}` element enables hello device toosend messages with additional properties in a url-encoded format.</span></span> <span data-ttu-id="89fd6-157">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="89fd6-157">For example:</span></span>

```
RFC 2396-encoded(<PropertyName1>)=RFC 2396-encoded(<PropertyValue1>)&RFC 2396-encoded(<PropertyName2>)=RFC 2396-encoded(<PropertyValue2>)…
```

> [!NOTE]
> <span data-ttu-id="89fd6-158">Cela `{property_bag}` élément utilise hello même encodage que pour les chaînes de requête dans le protocole de hello HTTP.</span><span class="sxs-lookup"><span data-stu-id="89fd6-158">This `{property_bag}` element uses hello same encoding as for query strings in hello HTTP protocol.</span></span>
>
>

<span data-ttu-id="89fd6-159">permet également d’application Hello `devices/{device_id}/messages/events/{property_bag}` comme hello **nom de la rubrique seront** toodefine *ne les messages* toobe transmis en tant qu’un message de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="89fd6-159">hello device app can also use `devices/{device_id}/messages/events/{property_bag}` as hello **Will topic name** toodefine *Will messages* toobe forwarded as a telemetry message.</span></span>

- <span data-ttu-id="89fd6-160">IoT Hub ne prend pas en charge les messages QoS 2.</span><span class="sxs-lookup"><span data-stu-id="89fd6-160">IoT Hub does not support QoS 2 messages.</span></span> <span data-ttu-id="89fd6-161">Si une application de périphérique publie un message avec **QoS 2**, IoT Hub ferme la connexion de réseau hello.</span><span class="sxs-lookup"><span data-stu-id="89fd6-161">If a device app publishes a message with **QoS 2**, IoT Hub closes hello network connection.</span></span>
- <span data-ttu-id="89fd6-162">IoT Hub ne conserve pas les messages Retain.</span><span class="sxs-lookup"><span data-stu-id="89fd6-162">IoT Hub does not persist Retain messages.</span></span> <span data-ttu-id="89fd6-163">Si un périphérique envoie un message avec hello **conserver** indicateur défini too1, IoT Hub ajoute hello **x-opt-conserver** toohello message de la propriété application.</span><span class="sxs-lookup"><span data-stu-id="89fd6-163">If a device sends a message with hello **RETAIN** flag set too1, IoT Hub adds hello **x-opt-retain** application property toohello message.</span></span> <span data-ttu-id="89fd6-164">Dans ce cas, au lieu de persistance hello conserver le message, le IoT Hub passe toohello principal application.</span><span class="sxs-lookup"><span data-stu-id="89fd6-164">In this case, instead of persisting hello retain message, IoT Hub passes it toohello backend app.</span></span>
- <span data-ttu-id="89fd6-165">IoT Hub ne prend en charge qu’une seule connexion MQTT active par appareil.</span><span class="sxs-lookup"><span data-stu-id="89fd6-165">IoT Hub only supports one active MQTT connection per device.</span></span> <span data-ttu-id="89fd6-166">Toute connexion MQTT pour le compte hello même ID de périphérique entraîne IoT Hub hello toodrop la connexion existante.</span><span class="sxs-lookup"><span data-stu-id="89fd6-166">Any new MQTT connection on behalf of hello same device ID causes IoT Hub toodrop hello existing connection.</span></span>

<span data-ttu-id="89fd6-167">Pour en savoir plus, reportez-vous au [Guide du développeur de messages][lnk-messaging].</span><span class="sxs-lookup"><span data-stu-id="89fd6-167">For more information, see [Messaging developer's guide][lnk-messaging].</span></span>

### <a name="receiving-cloud-to-device-messages"></a><span data-ttu-id="89fd6-168">Réception de messages cloud-à-appareil</span><span class="sxs-lookup"><span data-stu-id="89fd6-168">Receiving cloud-to-device messages</span></span>

<span data-ttu-id="89fd6-169">tooreceive des messages à partir de IoT Hub, un appareil doit s’abonner à l’aide de `devices/{device_id}/messages/devicebound/#` comme un **rubrique filtre**.</span><span class="sxs-lookup"><span data-stu-id="89fd6-169">tooreceive messages from IoT Hub, a device should subscribe using `devices/{device_id}/messages/devicebound/#` as a **Topic Filter**.</span></span> <span data-ttu-id="89fd6-170">Hello génériques multiniveaux  **#**  Bonjour filtre de rubrique est utilisée uniquement tooallow hello appareil tooreceive des propriétés supplémentaires dans le nom de la rubrique hello.</span><span class="sxs-lookup"><span data-stu-id="89fd6-170">hello multi-level wildcard **#** in hello Topic Filter is used only tooallow hello device tooreceive additional properties in hello topic name.</span></span> <span data-ttu-id="89fd6-171">IoT Hub n’autorise pas l’utilisation de hello Hello  **#**  ou **?**</span><span class="sxs-lookup"><span data-stu-id="89fd6-171">IoT Hub does not allow hello usage of hello **#** or **?**</span></span> <span data-ttu-id="89fd6-172">pour filtrer les sous-rubriques.</span><span class="sxs-lookup"><span data-stu-id="89fd6-172">wildcards for filtering of sub-topics.</span></span> <span data-ttu-id="89fd6-173">IoT Hub n’étant pas un broker de messagerie pub-sub à usage général, il prend uniquement en charge les noms de rubrique hello documentée et les filtres de la rubrique.</span><span class="sxs-lookup"><span data-stu-id="89fd6-173">Since IoT Hub is not a general purpose pub-sub messaging broker, it only supports hello documented topic names and topic filters.</span></span>

<span data-ttu-id="89fd6-174">Hello ne reçoit des messages à partir de IoT Hub, jusqu'à ce qu’il a ouvert le point de terminaison tooits spécifique au périphérique, représenté par hello `devices/{device_id}/messages/devicebound/#` filtre de rubrique.</span><span class="sxs-lookup"><span data-stu-id="89fd6-174">hello device does not receive any messages from IoT Hub, until it has successfully subscribed tooits device-specific endpoint, represented by hello `devices/{device_id}/messages/devicebound/#` topic filter.</span></span> <span data-ttu-id="89fd6-175">Une fois l’abonnement réussie a été établie, appareil de hello commence à recevoir des messages uniquement cloud-à-appareil qui ont été envoyés tooit tard hello d’abonnement de hello.</span><span class="sxs-lookup"><span data-stu-id="89fd6-175">After successful subscription has been established, hello device starts receiving only cloud-to-device messages that have been sent tooit after hello time of hello subscription.</span></span> <span data-ttu-id="89fd6-176">Appareil de hello qui se connecte avec **CleanSession** indicateur défini trop**0**, abonnement de hello est conservée entre les différentes sessions.</span><span class="sxs-lookup"><span data-stu-id="89fd6-176">If hello device connects with **CleanSession** flag set too**0**, hello subscription is persisted across different sessions.</span></span> <span data-ttu-id="89fd6-177">Dans ce cas, hello prochaine fois qu’il se connecte avec **CleanSession 0** périphérique de hello reçoit des messages en attente qui ont été envoyés tooit pendant qu’il a été déconnecté.</span><span class="sxs-lookup"><span data-stu-id="89fd6-177">In this case, hello next time it connects with **CleanSession 0** hello device receives outstanding messages that have been sent tooit while it was disconnected.</span></span> <span data-ttu-id="89fd6-178">Si le périphérique de hello utilise **CleanSession** indicateur défini trop**1** , il ne reçoit pas les messages à partir de IoT Hub jusqu'à ce qu’elle s’abonne tooits périphérique-point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="89fd6-178">If hello device uses **CleanSession** flag set too**1** though, it does not receive any messages from IoT Hub until it subscribes tooits device-endpoint.</span></span>

<span data-ttu-id="89fd6-179">IoT Hub remet les messages avec hello **nom de la rubrique** `devices/{device_id}/messages/devicebound/`, ou `devices/{device_id}/messages/devicebound/{property_bag}` s’il existe des propriétés de message.</span><span class="sxs-lookup"><span data-stu-id="89fd6-179">IoT Hub delivers messages with hello **Topic Name** `devices/{device_id}/messages/devicebound/`, or `devices/{device_id}/messages/devicebound/{property_bag}` if there are any message properties.</span></span> <span data-ttu-id="89fd6-180">`{property_bag}` contient des paires clé/valeur codées URL de propriétés de message.</span><span class="sxs-lookup"><span data-stu-id="89fd6-180">`{property_bag}` contains url-encoded key/value pairs of message properties.</span></span> <span data-ttu-id="89fd6-181">Uniquement les propriétés de l’application et les propriétés système définissable par l’utilisateur (tel que **messageId** ou **correlationId**) sont inclus dans le jeu de propriétés hello.</span><span class="sxs-lookup"><span data-stu-id="89fd6-181">Only application properties and user-settable system properties (such as **messageId** or **correlationId**) are included in hello property bag.</span></span> <span data-ttu-id="89fd6-182">Les noms de propriété système ont le préfixe de hello  **$** , propriétés de l’application utilisent le nom de la propriété d’origine hello sans le préfixe.</span><span class="sxs-lookup"><span data-stu-id="89fd6-182">System property names have hello prefix **$**, application properties use hello original property name with no prefix.</span></span>

<span data-ttu-id="89fd6-183">Lorsqu’une application de périphérique s’abonne rubrique tooa avec **QoS 2**, IoT Hub accorde niveau QoS maximal 1 Bonjour **SUBACK** paquet.</span><span class="sxs-lookup"><span data-stu-id="89fd6-183">When a device app subscribes tooa topic with **QoS 2**, IoT Hub grants maximum QoS level 1 in hello **SUBACK** packet.</span></span> <span data-ttu-id="89fd6-184">Après cela, IoT Hub remet appareil de toohello de messages à l’aide de la qualité de service 1.</span><span class="sxs-lookup"><span data-stu-id="89fd6-184">After that, IoT Hub delivers messages toohello device using QoS 1.</span></span>

### <a name="retrieving-a-device-twins-properties"></a><span data-ttu-id="89fd6-185">Récupération des propriétés d’un jumeau d’appareil</span><span class="sxs-lookup"><span data-stu-id="89fd6-185">Retrieving a device twin's properties</span></span>

<span data-ttu-id="89fd6-186">Tout d’abord, un appareil s’abonne trop`$iothub/twin/res/#`, les réponses de l’opération tooreceive hello.</span><span class="sxs-lookup"><span data-stu-id="89fd6-186">First, a device subscribes too`$iothub/twin/res/#`, tooreceive hello operation's responses.</span></span> <span data-ttu-id="89fd6-187">Ensuite, il envoie un message vide de tootopic `$iothub/twin/GET/?$rid={request id}`, avec une valeur par défaut pour **id de demande**. service de hello puis envoie un message de réponse contenant les données de double périphérique hello sur rubrique `$iothub/twin/res/{status}/?$rid={request id}`, à l’aide de hello même  **id de demande** en tant que requête de hello.</span><span class="sxs-lookup"><span data-stu-id="89fd6-187">Then, it sends an empty message tootopic `$iothub/twin/GET/?$rid={request id}`, with a populated value for **request id**. hello service then sends a response message containing hello device twin data on topic `$iothub/twin/res/{status}/?$rid={request id}`, using hello same **request id** as hello request.</span></span>

<span data-ttu-id="89fd6-188">L’ID de la requête peut avoir n’importe quelle valeur valide de propriété de message, conformément au [Guide du développeur de messages IoT Hub][lnk-messaging], et l’état est validé comme entier.</span><span class="sxs-lookup"><span data-stu-id="89fd6-188">Request id can be any valid value for a message property value, as per [IoT Hub messaging developer's guide][lnk-messaging], and status is validated as an integer.</span></span>
<span data-ttu-id="89fd6-189">les corps de réponse de Hello contient la section des propriétés de double de périphérique hello hello :</span><span class="sxs-lookup"><span data-stu-id="89fd6-189">hello response body contains hello properties section of hello device twin:</span></span>

<span data-ttu-id="89fd6-190">corps Hello hello identité entrée de Registre limitée toohello membre de « propriétés », par exemple :</span><span class="sxs-lookup"><span data-stu-id="89fd6-190">hello body of hello identity registry entry limited toohello “properties” member, for example:</span></span>

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

<span data-ttu-id="89fd6-191">Hello codes d’état possibles sont :</span><span class="sxs-lookup"><span data-stu-id="89fd6-191">hello possible status codes are:</span></span>

|<span data-ttu-id="89fd6-192">État</span><span class="sxs-lookup"><span data-stu-id="89fd6-192">Status</span></span> | <span data-ttu-id="89fd6-193">Description</span><span class="sxs-lookup"><span data-stu-id="89fd6-193">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="89fd6-194">200</span><span class="sxs-lookup"><span data-stu-id="89fd6-194">200</span></span> | <span data-ttu-id="89fd6-195">Succès</span><span class="sxs-lookup"><span data-stu-id="89fd6-195">Success</span></span> |
| <span data-ttu-id="89fd6-196">429</span><span class="sxs-lookup"><span data-stu-id="89fd6-196">429</span></span> | <span data-ttu-id="89fd6-197">Trop de demandes (limité), selon la [Limitation IoT Hub][lnk-quotas]</span><span class="sxs-lookup"><span data-stu-id="89fd6-197">Too many requests (throttled), as per [IoT Hub throttling][lnk-quotas]</span></span> |
| <span data-ttu-id="89fd6-198">5**</span><span class="sxs-lookup"><span data-stu-id="89fd6-198">5**</span></span> | <span data-ttu-id="89fd6-199">Erreurs de serveur</span><span class="sxs-lookup"><span data-stu-id="89fd6-199">Server errors</span></span> |

<span data-ttu-id="89fd6-200">Pour en savoir plus, reportez-vous au [Guide du développeur de jumeaux d’appareil][lnk-devguide-twin].</span><span class="sxs-lookup"><span data-stu-id="89fd6-200">For more information, see [Device twins developer's guide][lnk-devguide-twin].</span></span>

### <a name="update-device-twins-reported-properties"></a><span data-ttu-id="89fd6-201">Mettre à jour les propriétés signalées du jumeau d’appareil</span><span class="sxs-lookup"><span data-stu-id="89fd6-201">Update device twin's reported properties</span></span>

<span data-ttu-id="89fd6-202">Hello séquence suivante décrit comment un appareil met à jour hello a signalé des propriétés en double d’appareil hello dans IoT Hub :</span><span class="sxs-lookup"><span data-stu-id="89fd6-202">hello following sequence describes how a device updates hello reported properties in hello device twin in IoT Hub:</span></span>

1. <span data-ttu-id="89fd6-203">Un appareil Abonnez-vous d’abord toohello `$iothub/twin/res/#` les réponses de l’opération de rubrique tooreceive hello du IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="89fd6-203">A device must first subscribe toohello `$iothub/twin/res/#` topic tooreceive hello operation's responses from IoT Hub.</span></span>

1. <span data-ttu-id="89fd6-204">Un périphérique envoie un message qui contient hello appareil double mise à jour toohello `$iothub/twin/PATCH/properties/reported/?$rid={request id}` rubrique.</span><span class="sxs-lookup"><span data-stu-id="89fd6-204">A device sends a message that contains hello device twin update toohello `$iothub/twin/PATCH/properties/reported/?$rid={request id}` topic.</span></span> <span data-ttu-id="89fd6-205">Ce message contient une valeur **ID de demande**.</span><span class="sxs-lookup"><span data-stu-id="89fd6-205">This message includes a **request id** value.</span></span>

1. <span data-ttu-id="89fd6-206">Hello service puis envoie un message de réponse contenant hello nouvelle valeur d’ETag pour hello collection de propriétés déclarées sur la rubrique `$iothub/twin/res/{status}/?$rid={request id}`.</span><span class="sxs-lookup"><span data-stu-id="89fd6-206">hello service then sends a response message that contains hello new ETag value for hello reported properties collection on topic `$iothub/twin/res/{status}/?$rid={request id}`.</span></span> <span data-ttu-id="89fd6-207">Ce message de réponse utilise hello même **id de demande** en tant que requête de hello.</span><span class="sxs-lookup"><span data-stu-id="89fd6-207">This response message uses hello same **request id** as hello request.</span></span>

<span data-ttu-id="89fd6-208">corps du message de demande de Hello contient un document JSON, qui fournit les nouvelles valeurs pour les propriétés déclarées (aucune autre propriété ou les métadonnées ne peuvent être modifiées).</span><span class="sxs-lookup"><span data-stu-id="89fd6-208">hello request message body contains a JSON document, which provides new values for reported properties (no other property or metadata can be modified).</span></span>
<span data-ttu-id="89fd6-209">Chaque membre dans le document JSON de hello met à jour ou ajouter des membres correspondants de hello dans les documents de double hello appareil.</span><span class="sxs-lookup"><span data-stu-id="89fd6-209">Each member in hello JSON document updates or add hello corresponding member in hello device twin’s document.</span></span> <span data-ttu-id="89fd6-210">Un membre défini trop`null`, suppressions hello membre à partir de hello contenant l’objet.</span><span class="sxs-lookup"><span data-stu-id="89fd6-210">A member set too`null`, deletes hello member from hello containing object.</span></span> <span data-ttu-id="89fd6-211">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="89fd6-211">For example:</span></span>

        {
            "telemetrySendFrequency": "35m",
            "batteryLevel": 60
        }

<span data-ttu-id="89fd6-212">Hello codes d’état possibles sont :</span><span class="sxs-lookup"><span data-stu-id="89fd6-212">hello possible status codes are:</span></span>

|<span data-ttu-id="89fd6-213">État</span><span class="sxs-lookup"><span data-stu-id="89fd6-213">Status</span></span> | <span data-ttu-id="89fd6-214">Description</span><span class="sxs-lookup"><span data-stu-id="89fd6-214">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="89fd6-215">200</span><span class="sxs-lookup"><span data-stu-id="89fd6-215">200</span></span> | <span data-ttu-id="89fd6-216">Succès</span><span class="sxs-lookup"><span data-stu-id="89fd6-216">Success</span></span> |
| <span data-ttu-id="89fd6-217">400</span><span class="sxs-lookup"><span data-stu-id="89fd6-217">400</span></span> | <span data-ttu-id="89fd6-218">Demande incorrecte.</span><span class="sxs-lookup"><span data-stu-id="89fd6-218">Bad Request.</span></span> <span data-ttu-id="89fd6-219">JSON incorrect</span><span class="sxs-lookup"><span data-stu-id="89fd6-219">Malformed JSON</span></span> |
| <span data-ttu-id="89fd6-220">429</span><span class="sxs-lookup"><span data-stu-id="89fd6-220">429</span></span> | <span data-ttu-id="89fd6-221">Trop de demandes (limité), selon la [Limitation IoT Hub][lnk-quotas]</span><span class="sxs-lookup"><span data-stu-id="89fd6-221">Too many requests (throttled), as per [IoT Hub throttling][lnk-quotas]</span></span> |
| <span data-ttu-id="89fd6-222">5**</span><span class="sxs-lookup"><span data-stu-id="89fd6-222">5**</span></span> | <span data-ttu-id="89fd6-223">Erreurs de serveur</span><span class="sxs-lookup"><span data-stu-id="89fd6-223">Server errors</span></span> |

<span data-ttu-id="89fd6-224">Pour en savoir plus, reportez-vous au [Guide du développeur de jumeaux d’appareil][lnk-devguide-twin].</span><span class="sxs-lookup"><span data-stu-id="89fd6-224">For more information, see [Device twins developer's guide][lnk-devguide-twin].</span></span>

### <a name="receiving-desired-properties-update-notifications"></a><span data-ttu-id="89fd6-225">Réception de notifications de mise à jour des propriétés souhaitées</span><span class="sxs-lookup"><span data-stu-id="89fd6-225">Receiving desired properties update notifications</span></span>

<span data-ttu-id="89fd6-226">Quand un appareil est connecté, IoT Hub envoie rubrique toohello de notifications `$iothub/twin/PATCH/properties/desired/?$version={new version}`, qui contiennent le contenu de mise à jour hello effectuée par hello solution back-end hello.</span><span class="sxs-lookup"><span data-stu-id="89fd6-226">When a device is connected, IoT Hub sends notifications toohello topic `$iothub/twin/PATCH/properties/desired/?$version={new version}`, which contain hello content of hello update performed by hello solution back end.</span></span> <span data-ttu-id="89fd6-227">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="89fd6-227">For example:</span></span>

        {
            "telemetrySendFrequency": "5m",
            "route": null
        }

<span data-ttu-id="89fd6-228">Comme pour les mises à jour de la propriété, `null` signifie que les valeurs qui hello JSON est en cours de suppression des membres de l’objet.</span><span class="sxs-lookup"><span data-stu-id="89fd6-228">As for property updates, `null` values means that hello JSON object member is being deleted.</span></span>


> [!IMPORTANT] 
> <span data-ttu-id="89fd6-229">IoT Hub génère des notifications de modification uniquement lorsque les appareils sont connectés.</span><span class="sxs-lookup"><span data-stu-id="89fd6-229">IoT Hub generates change notifications only when devices are connected.</span></span> <span data-ttu-id="89fd6-230">Assurez-vous que tooimplement hello [flux reconnexion de périphérique] [ lnk-devguide-twin-reconnection] tookeep hello souhaité propriétés synchronisées entre IoT Hub et application d’appareil hello.</span><span class="sxs-lookup"><span data-stu-id="89fd6-230">Make sure tooimplement hello [device reconnection flow][lnk-devguide-twin-reconnection] tookeep hello desired properties synchronized between IoT Hub and hello device app.</span></span>

<span data-ttu-id="89fd6-231">Pour en savoir plus, reportez-vous au [Guide du développeur de jumeaux d’appareil][lnk-devguide-twin].</span><span class="sxs-lookup"><span data-stu-id="89fd6-231">For more information, see [Device twins developer's guide][lnk-devguide-twin].</span></span>

### <a name="respond-tooa-direct-method"></a><span data-ttu-id="89fd6-232">Méthode directe de répondre tooa</span><span class="sxs-lookup"><span data-stu-id="89fd6-232">Respond tooa direct method</span></span>

<span data-ttu-id="89fd6-233">Tout d’abord, un appareil a toosubscribe trop`$iothub/methods/POST/#`.</span><span class="sxs-lookup"><span data-stu-id="89fd6-233">First, a device has toosubscribe too`$iothub/methods/POST/#`.</span></span> <span data-ttu-id="89fd6-234">IoT Hub envoie la rubrique de méthode demandes toohello `$iothub/methods/POST/{method name}/?$rid={request id}`, avec un corps vide ou un JSON valid.</span><span class="sxs-lookup"><span data-stu-id="89fd6-234">IoT Hub sends method requests toohello topic `$iothub/methods/POST/{method name}/?$rid={request id}`, with either a valid JSON or an empty body.</span></span>

<span data-ttu-id="89fd6-235">toorespond, appareil de hello envoie un message avec un JSON valid ou une rubrique de toohello de corps vide `$iothub/methods/res/{status}/?$rid={request id}`, où **id de demande** a toomatch un dans le message de demande hello, hello et **état** a toobe entier .</span><span class="sxs-lookup"><span data-stu-id="89fd6-235">toorespond, hello device sends a message with a valid JSON or empty body toohello topic `$iothub/methods/res/{status}/?$rid={request id}`, where **request id** has toomatch hello one in hello request message, and **status** has toobe an integer.</span></span>

<span data-ttu-id="89fd6-236">Pour en savoir plus, reportez-vous au [Guide du développeur de méthodes directes][lnk-methods].</span><span class="sxs-lookup"><span data-stu-id="89fd6-236">For more information, see [Direct method developer's guide][lnk-methods].</span></span>

### <a name="additional-considerations"></a><span data-ttu-id="89fd6-237">Considérations supplémentaires</span><span class="sxs-lookup"><span data-stu-id="89fd6-237">Additional considerations</span></span>

<span data-ttu-id="89fd6-238">En termes de finale, si vous avez besoin de comportement du protocole toocustomize hello MQTT côté hello cloud, vous devez passer en revue hello [passerelle de protocole Azure IoT] [ lnk-azure-protocol-gateway] qui vous permet de toodeploy hautes performances passerelle de protocole personnalisé qui interagit directement avec l’IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="89fd6-238">As a final consideration, if you need toocustomize hello MQTT protocol behavior on hello cloud side, you should review hello [Azure IoT protocol gateway][lnk-azure-protocol-gateway] that enables you toodeploy a high-performance custom protocol gateway that interfaces directly with IoT Hub.</span></span> <span data-ttu-id="89fd6-239">passerelle de protocole Hello Azure IoT permet de vous toocustomize hello appareil protocole tooaccommodate brownfield MQTT déploiements ou autres protocoles personnalisés.</span><span class="sxs-lookup"><span data-stu-id="89fd6-239">hello Azure IoT protocol gateway enables you toocustomize hello device protocol tooaccommodate brownfield MQTT deployments or other custom protocols.</span></span> <span data-ttu-id="89fd6-240">Toutefois, cette approche nécessite l’exécution et l’utilisation d’une passerelle de protocole personnalisée.</span><span class="sxs-lookup"><span data-stu-id="89fd6-240">This approach does require, however, that you run and operate a custom protocol gateway.</span></span>

## <a name="next-steps"></a><span data-ttu-id="89fd6-241">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="89fd6-241">Next steps</span></span>

<span data-ttu-id="89fd6-242">toolearn en savoir plus sur le protocole MQTT hello, consultez hello [documentation de MQTT][lnk-mqtt-docs].</span><span class="sxs-lookup"><span data-stu-id="89fd6-242">toolearn more about hello MQTT protocol, see hello [MQTT documentation][lnk-mqtt-docs].</span></span>

<span data-ttu-id="89fd6-243">toolearn savoir plus sur la planification de votre déploiement IoT Hub, consultez :</span><span class="sxs-lookup"><span data-stu-id="89fd6-243">toolearn more about planning your IoT Hub deployment, see:</span></span>

* <span data-ttu-id="89fd6-244">[Catalogue d’appareils certifiés Azure pour l’IoT][lnk-devices]</span><span class="sxs-lookup"><span data-stu-id="89fd6-244">[Azure Certified for IoT device catalog][lnk-devices]</span></span>
* <span data-ttu-id="89fd6-245">[Prendre en charge des protocoles supplémentaires][lnk-protocols]</span><span class="sxs-lookup"><span data-stu-id="89fd6-245">[Support additional protocols][lnk-protocols]</span></span>
* <span data-ttu-id="89fd6-246">[Comparer à Event Hubs][lnk-compare]</span><span class="sxs-lookup"><span data-stu-id="89fd6-246">[Compare with Event Hubs][lnk-compare]</span></span>
* <span data-ttu-id="89fd6-247">[Mise à l’échelle, HA et DR][lnk-scaling]</span><span class="sxs-lookup"><span data-stu-id="89fd6-247">[Scaling, HA, and DR][lnk-scaling]</span></span>

<span data-ttu-id="89fd6-248">toofurther Explorez les fonctionnalités de hello d’IoT Hub, consultez :</span><span class="sxs-lookup"><span data-stu-id="89fd6-248">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="89fd6-249">[Guide du développeur IoT Hub][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="89fd6-249">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="89fd6-250">[Simulation d’un appareil avec Azure IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="89fd6-250">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

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
