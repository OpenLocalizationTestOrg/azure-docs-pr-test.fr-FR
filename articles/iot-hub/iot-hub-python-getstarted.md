---
title: aaaGet en main Azure IoT Hub (Python) | Documents Microsoft
description: "Découvrez comment toosend appareil-à-cloud messages tooAzure IoT Hub à l’aide de kits de développement logiciel IoT pour Python. Créer appareil simulé et tooregister des applications de service de votre appareil, envoyer des messages et lire les messages de hub IoT."
services: iot-hub
author: dsk-2015
manager: timlt
editor: 
ms.service: iot-hub
ms.devlang: python
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: dkshir
ms.custom: na
ms.openlocfilehash: aa23e792fb144202e121274723bcfaeae0c04723
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-simulated-device-tooyour-iot-hub-using-python"></a><span data-ttu-id="56c5f-104">Connectez votre concentrateur de IoT tooyour appareil simulé à l’aide de Python</span><span class="sxs-lookup"><span data-stu-id="56c5f-104">Connect your simulated device tooyour IoT hub using Python</span></span>
[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

<span data-ttu-id="56c5f-105">À la fin de hello de ce didacticiel, vous aurez deux applications Python :</span><span class="sxs-lookup"><span data-stu-id="56c5f-105">At hello end of this tutorial, you will have two Python apps:</span></span>

* <span data-ttu-id="56c5f-106">**CreateDeviceIdentity.py**, ce qui crée une identité d’appareil et clé de sécurité associés tooconnect votre application d’appareil simulé.</span><span class="sxs-lookup"><span data-stu-id="56c5f-106">**CreateDeviceIdentity.py**, which creates a device identity and associated security key tooconnect your simulated device app.</span></span>
* <span data-ttu-id="56c5f-107">**SimulatedDevice.py**, qui connecte tooyour IoT hub avec l’identité de l’appareil hello créée précédemment, et régulièrement envoie une télémétrie de message à l’aide du protocole MQTT hello.</span><span class="sxs-lookup"><span data-stu-id="56c5f-107">**SimulatedDevice.py**, which connects tooyour IoT hub with hello device identity created earlier, and periodically sends a telemetry message using hello MQTT protocol.</span></span>

> [!NOTE]
> <span data-ttu-id="56c5f-108">article de Hello [kits de développement logiciel Azure IoT] [ lnk-hub-sdks] fournit des informations sur hello kits de développement logiciel Azure IoT que vous pouvez utiliser toobuild toorun de deux applications sur les périphériques et votre principal de la solution.</span><span class="sxs-lookup"><span data-stu-id="56c5f-108">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both applications toorun on devices and your solution back end.</span></span>
> 
> 

<span data-ttu-id="56c5f-109">toocomplete ce didacticiel, vous devez hello suivant :</span><span class="sxs-lookup"><span data-stu-id="56c5f-109">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="56c5f-110">[Python 2.x ou 3.x][lnk-python-download].</span><span class="sxs-lookup"><span data-stu-id="56c5f-110">[Python 2.x or 3.x][lnk-python-download].</span></span> <span data-ttu-id="56c5f-111">Assurez-vous que toouse hello 32 bits ou 64 bits l’installation en fonction des besoins de votre programme d’installation.</span><span class="sxs-lookup"><span data-stu-id="56c5f-111">Make sure toouse hello 32-bit or 64-bit installation as required by your setup.</span></span> <span data-ttu-id="56c5f-112">Lorsque vous y êtes invité pendant l’installation de hello, rendre la variable d’environnement spécifiques à la plateforme tooyour à des Python tooadd sûr.</span><span class="sxs-lookup"><span data-stu-id="56c5f-112">When prompted during hello installation, make sure tooadd Python tooyour platform-specific environment variable.</span></span> <span data-ttu-id="56c5f-113">Si vous utilisez Python 2.x, vous devrez peut-être trop[installer ou mettre à niveau *pip*, système de gestion de package hello Python][lnk-install-pip].</span><span class="sxs-lookup"><span data-stu-id="56c5f-113">If you are using Python 2.x, you may need too[install or upgrade *pip*, hello Python package management system][lnk-install-pip].</span></span>
* <span data-ttu-id="56c5f-114">Si vous utilisez le système d’exploitation Windows, puis [package redistribuable Visual C++] [ lnk-visual-c-redist] utilisation de hello tooallow de DLL natives à partir de Python.</span><span class="sxs-lookup"><span data-stu-id="56c5f-114">If you are using Windows OS, then [Visual C++ redistributable package][lnk-visual-c-redist] tooallow hello use of native DLLs from Python.</span></span>
* <span data-ttu-id="56c5f-115">[Node.js 4.0 ou version ultérieure][lnk-node-download].</span><span class="sxs-lookup"><span data-stu-id="56c5f-115">[Node.js 4.0 or later][lnk-node-download].</span></span> <span data-ttu-id="56c5f-116">Assurez-vous que toouse hello 32 bits ou 64 bits l’installation en fonction des besoins de votre programme d’installation.</span><span class="sxs-lookup"><span data-stu-id="56c5f-116">Make sure toouse hello 32-bit or 64-bit installation as required by your setup.</span></span> <span data-ttu-id="56c5f-117">Cela est nécessaire tooinstall hello [outil Explorateur de Hub IoT][lnk-iot-hub-explorer].</span><span class="sxs-lookup"><span data-stu-id="56c5f-117">This is needed tooinstall hello [IoT Hub Explorer tool][lnk-iot-hub-explorer].</span></span>
* <span data-ttu-id="56c5f-118">Un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="56c5f-118">An active Azure account.</span></span> <span data-ttu-id="56c5f-119">Si vous ne possédez pas de compte, vous pouvez créer un [compte gratuit][lnk-free-trial] en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="56c5f-119">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>

> [!NOTE]
> <span data-ttu-id="56c5f-120">Hello *pip* packages pour `azure-iothub-service-client` et `azure-iothub-device-client` sont actuellement disponibles uniquement pour le système d’exploitation Windows.</span><span class="sxs-lookup"><span data-stu-id="56c5f-120">hello *pip* packages for `azure-iothub-service-client` and `azure-iothub-device-client` are currently available only for Windows OS.</span></span> <span data-ttu-id="56c5f-121">Pour Linux/Mac OS, reportez-vous à toohello des sections de Linux et Mac OS spécifiques sur hello [préparer votre environnement de développement Python] [ lnk-python-devbox] valider.</span><span class="sxs-lookup"><span data-stu-id="56c5f-121">For Linux/Mac OS, please refer toohello Linux and Mac OS-specific sections on hello [Prepare your development environment for Python][lnk-python-devbox] post.</span></span>
> 

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

<span data-ttu-id="56c5f-122">Votre IoT Hub est maintenant créé.</span><span class="sxs-lookup"><span data-stu-id="56c5f-122">You have now created your IoT hub.</span></span> <span data-ttu-id="56c5f-123">Utilisez hello nom d’hôte IoT Hub et hello chaîne de connexion de IoT Hub reste hello de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="56c5f-123">Use hello IoT Hub host name and hello IoT Hub connection string in hello rest of this tutorial.</span></span>

> [!NOTE]
> <span data-ttu-id="56c5f-124">Vous pouvez également créer facilement votre hub IoT sur une ligne de commande, à l’aide de hello Python ou Node.js basé CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="56c5f-124">You can also easily create your IoT hub on a command line, using hello Python or Node.js based Azure CLI.</span></span> <span data-ttu-id="56c5f-125">article de Hello [créez un IoT hub à l’aide de hello Azure CLI 2.0] [ lnk-azure-cli-hub] montre vous hello étapes rapides toodo donc.</span><span class="sxs-lookup"><span data-stu-id="56c5f-125">hello article [Create an IoT hub using hello Azure CLI 2.0][lnk-azure-cli-hub] shows you hello quick steps toodo so.</span></span> 
> 

## <a name="create-a-device-identity"></a><span data-ttu-id="56c5f-126">Création d’une identité d’appareil</span><span class="sxs-lookup"><span data-stu-id="56c5f-126">Create a device identity</span></span>
<span data-ttu-id="56c5f-127">Cette section répertorie hello étapes toocreate une application de console Python, qui crée une identité d’appareil dans le Registre des identités de votre hub IoT hello.</span><span class="sxs-lookup"><span data-stu-id="56c5f-127">This section lists hello steps toocreate a Python console app, that creates a device identity in hello identity registry of your IoT hub.</span></span> <span data-ttu-id="56c5f-128">Appareils de se connecter uniquement tooIoT Hub si elle a une entrée dans le Registre des identités hello.</span><span class="sxs-lookup"><span data-stu-id="56c5f-128">A device can only connect tooIoT Hub if it has an entry in hello identity registry.</span></span> <span data-ttu-id="56c5f-129">Pour plus d’informations, consultez hello **Registre des identités** section Hello [guide du développeur IoT Hub][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="56c5f-129">For more information, see hello **Identity Registry** section of hello [IoT Hub developer guide][lnk-devguide-identity].</span></span> <span data-ttu-id="56c5f-130">Lorsque vous exécutez cette application console, il génère un ID d’appareil unique et clé que votre appareil peut utiliser tooidentify lui-même lorsqu’il envoie l’appareil-à-cloud messages tooIoT Hub.</span><span class="sxs-lookup"><span data-stu-id="56c5f-130">When you run this console app, it generates a unique device ID and key that your device can use tooidentify itself when it sends device-to-cloud messages tooIoT Hub.</span></span>

1. <span data-ttu-id="56c5f-131">Ouvrez une invite de commandes et installer hello **Azure IoT Hub Service SDK pour Python**.</span><span class="sxs-lookup"><span data-stu-id="56c5f-131">Open a command prompt and install hello **Azure IoT Hub Service SDK for Python**.</span></span> <span data-ttu-id="56c5f-132">Fermer l’invite de commandes hello après avoir installé hello SDK.</span><span class="sxs-lookup"><span data-stu-id="56c5f-132">Close hello command prompt after you install hello SDK.</span></span>

    ```
    pip install azure-iothub-service-client
    ```

2. <span data-ttu-id="56c5f-133">Créez un fichier Python nommé **CreateDeviceIdentity.py**.</span><span class="sxs-lookup"><span data-stu-id="56c5f-133">Create a Python file named **CreateDeviceIdentity.py**.</span></span> <span data-ttu-id="56c5f-134">Ouvrir dans [un éditeur/environnement IDE Python de votre choix][lnk-python-ide-list], par exemple, hello par défaut [inactif][lnk-idle].</span><span class="sxs-lookup"><span data-stu-id="56c5f-134">Open it in [a Python editor/IDE of your choice][lnk-python-ide-list], for example, hello default [IDLE][lnk-idle].</span></span>

3. <span data-ttu-id="56c5f-135">Ajoutez hello suivant des modules de code tooimport hello requis à partir du service de hello SDK :</span><span class="sxs-lookup"><span data-stu-id="56c5f-135">Add hello following code tooimport hello required modules from hello service SDK:</span></span>

    ```python
    import sys
    import iothub_service_client
    from iothub_service_client import IoTHubRegistryManager, IoTHubRegistryManagerAuthMethod
    from iothub_service_client import IoTHubDeviceStatus, IoTHubError
    ```
2. <span data-ttu-id="56c5f-136">Ajouter hello suivant de code, le remplacement d’espace réservé de hello pour `[IoTHub Connection String]` avec la chaîne de connexion hello pour hello IoT hub vous avez créé dans la section précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="56c5f-136">Add hello following code, replacing hello placeholder for `[IoTHub Connection String]` with hello connection string for hello IoT hub you created in hello previous section.</span></span> <span data-ttu-id="56c5f-137">Vous pouvez utiliser n’importe quel nom comme hello `DEVICE_ID`.</span><span class="sxs-lookup"><span data-stu-id="56c5f-137">You can use any name as hello `DEVICE_ID`.</span></span>
   
    ```python
    CONNECTION_STRING = "[IoTHub Connection String]"
    DEVICE_ID = "MyFirstPythonDevice"
    ```
   [!INCLUDE [iot-hub-pii-note-naming-device](../../includes/iot-hub-pii-note-naming-device.md)]

3. <span data-ttu-id="56c5f-138">Ajouter hello après la fonction tooprint certaines des informations sur l’appareil hello.</span><span class="sxs-lookup"><span data-stu-id="56c5f-138">Add hello following function tooprint some of hello device information.</span></span>

    ```python
    def print_device_info(title, iothub_device):
        print ( title + ":" )
        print ( "iothubDevice.deviceId                    = {0}".format(iothub_device.deviceId) )
        print ( "iothubDevice.primaryKey                  = {0}".format(iothub_device.primaryKey) )
        print ( "iothubDevice.secondaryKey                = {0}".format(iothub_device.secondaryKey) )
        print ( "iothubDevice.connectionState             = {0}".format(iothub_device.connectionState) )
        print ( "iothubDevice.status                      = {0}".format(iothub_device.status) )
        print ( "iothubDevice.lastActivityTime            = {0}".format(iothub_device.lastActivityTime) )
        print ( "iothubDevice.cloudToDeviceMessageCount   = {0}".format(iothub_device.cloudToDeviceMessageCount) )
        print ( "iothubDevice.isManaged                   = {0}".format(iothub_device.isManaged) )
        print ( "iothubDevice.authMethod                  = {0}".format(iothub_device.authMethod) )
        print ( "" )
    ```
3. <span data-ttu-id="56c5f-139">Ajoutez hello suivant fonction toocreate hello appareil d’identification à l’aide de hello Gestionnaire du Registre.</span><span class="sxs-lookup"><span data-stu-id="56c5f-139">Add hello following function toocreate hello device identification using hello Registry Manager.</span></span> 

    ```python
    def iothub_createdevice():
        try:
            iothub_registry_manager = IoTHubRegistryManager(CONNECTION_STRING)
            auth_method = IoTHubRegistryManagerAuthMethod.SHARED_PRIVATE_KEY
            new_device = iothub_registry_manager.create_device(DEVICE_ID, "", "", auth_method)
            print_device_info("CreateDevice", new_device)

        except IoTHubError as iothub_error:
            print ( "Unexpected error {0}".format(iothub_error) )
            return
        except KeyboardInterrupt:
            print ( "iothub_createdevice stopped" )
    ```
4. <span data-ttu-id="56c5f-140">Enfin, ajoutez fonction principale hello comme suit et enregistrer le fichier de hello.</span><span class="sxs-lookup"><span data-stu-id="56c5f-140">Finally, add hello main function as follows and save hello file.</span></span>

    ```python
    if __name__ == '__main__':
        print ( "" )
        print ( "Python {0}".format(sys.version) )
        print ( "Creating device using hello Azure IoT Hub Service SDK for Python" )
        print ( "" )
        print ( "    Connection string = {0}".format(CONNECTION_STRING) )
        print ( "    Device ID         = {0}".format(DEVICE_ID) )

        iothub_createdevice()
    ```
5. <span data-ttu-id="56c5f-141">Sur l’invite de commandes hello, exécutez hello **CreateDeviceIdentity.py** comme suit :</span><span class="sxs-lookup"><span data-stu-id="56c5f-141">On hello command prompt, run hello **CreateDeviceIdentity.py** as follows:</span></span>

    ```python
    python CreateDeviceIdentity.py
    ```
6. <span data-ttu-id="56c5f-142">Vous devez voir les appareil simulé hello créé.</span><span class="sxs-lookup"><span data-stu-id="56c5f-142">You should see hello simulated device getting created.</span></span> <span data-ttu-id="56c5f-143">Notez les hello **deviceId** et hello **primaryKey** de cet appareil.</span><span class="sxs-lookup"><span data-stu-id="56c5f-143">Note down hello **deviceId** and hello **primaryKey** of this device.</span></span> <span data-ttu-id="56c5f-144">Vous avez besoin de ces valeurs lorsque vous créez une application qui se connecte tooIoT Hub en tant que périphérique.</span><span class="sxs-lookup"><span data-stu-id="56c5f-144">You need these values later when you create an application that connects tooIoT Hub as a device.</span></span>

    ![Création réussie de l’appareil][1]

> [!NOTE]
> <span data-ttu-id="56c5f-146">Hello Registre des identités IoT Hub stocke uniquement toohello IoT hub de périphérique identités tooenable un accès sécurisé.</span><span class="sxs-lookup"><span data-stu-id="56c5f-146">hello IoT Hub identity registry only stores device identities tooenable secure access toohello IoT hub.</span></span> <span data-ttu-id="56c5f-147">Il stocke toouse ID et les clés de périphérique en tant qu’informations d’identification de sécurité et d’un indicateur activée/désactivée que vous pouvez utiliser l’accès toodisable pour un périphérique.</span><span class="sxs-lookup"><span data-stu-id="56c5f-147">It stores device IDs and keys toouse as security credentials and an enabled/disabled flag that you can use toodisable access for an individual device.</span></span> <span data-ttu-id="56c5f-148">Si votre application doit toostore autres métadonnées spécifiques au périphérique, elle doit utiliser un magasin spécifique à l’application.</span><span class="sxs-lookup"><span data-stu-id="56c5f-148">If your application needs toostore other device-specific metadata, it should use an application-specific store.</span></span> <span data-ttu-id="56c5f-149">Pour plus d’informations, consultez hello [guide du développeur IoT Hub][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="56c5f-149">For more information, see hello [IoT Hub developer guide][lnk-devguide-identity].</span></span>
> 
> 


## <a name="create-a-simulated-device-app"></a><span data-ttu-id="56c5f-150">Création d’une application de périphérique simulé</span><span class="sxs-lookup"><span data-stu-id="56c5f-150">Create a simulated device app</span></span>
<span data-ttu-id="56c5f-151">Cette section répertorie les étapes de hello toocreate une application de console Python, qui simule un appareil et envoie IoT hub tooyour de messages appareil-à-cloud.</span><span class="sxs-lookup"><span data-stu-id="56c5f-151">This section lists hello steps toocreate a Python console app, that simulates a device and sends device-to-cloud messages tooyour IoT hub.</span></span>

1. <span data-ttu-id="56c5f-152">Ouvrez une nouvelle invite de commande et installez hello Azure IoT Hub appareil SDK pour Python comme suit.</span><span class="sxs-lookup"><span data-stu-id="56c5f-152">Open a new command prompt and install hello Azure IoT Hub Device SDK for Python as follows.</span></span> <span data-ttu-id="56c5f-153">Fermez l’invite de commandes hello après l’installation de hello.</span><span class="sxs-lookup"><span data-stu-id="56c5f-153">Close hello command prompt after hello installation.</span></span>

    ```
    pip install azure-iothub-device-client
    ```
2. <span data-ttu-id="56c5f-154">Créez un fichier nommé **SimulatedDevice.py**.</span><span class="sxs-lookup"><span data-stu-id="56c5f-154">Create a file named **SimulatedDevice.py**.</span></span> <span data-ttu-id="56c5f-155">Ouvrez ce fichier dans un éditeur/IDE Python de votre choix (par exemple, IDLE).</span><span class="sxs-lookup"><span data-stu-id="56c5f-155">Open this file in a Python editor/IDE of your choice (for example, IDLE).</span></span>

3. <span data-ttu-id="56c5f-156">Ajoutez hello suivant des modules de code tooimport hello requis à partir de l’appareil hello SDK.</span><span class="sxs-lookup"><span data-stu-id="56c5f-156">Add hello following code tooimport hello required modules from hello device SDK.</span></span>

    ```python
    import random
    import time
    import sys
    import iothub_client
    from iothub_client import IoTHubClient, IoTHubClientError, IoTHubTransportProvider, IoTHubClientResult
    from iothub_client import IoTHubMessage, IoTHubMessageDispositionResult, IoTHubError, DeviceMethodReturnValue
    ```
4. <span data-ttu-id="56c5f-157">Ajouter le code suivant de hello et espace réservé de hello pour `[IoTHub Device Connection String]` avec la chaîne de connexion hello pour votre appareil.</span><span class="sxs-lookup"><span data-stu-id="56c5f-157">Add hello following code and replace hello placeholder for `[IoTHub Device Connection String]` with hello connection string for your device.</span></span> <span data-ttu-id="56c5f-158">chaîne de connexion de périphérique Hello est généralement au format hello de `HostName=<hostName>;DeviceId=<deviceId>;SharedAccessKey=<primaryKey>`.</span><span class="sxs-lookup"><span data-stu-id="56c5f-158">hello device connection string is usually in hello format of `HostName=<hostName>;DeviceId=<deviceId>;SharedAccessKey=<primaryKey>`.</span></span> <span data-ttu-id="56c5f-159">Hello d’utilisation **deviceId** et **primaryKey** du périphérique hello vous avez créé dans hello de hello précédente section tooreplace `<deviceId>` et `<primaryKey>` respectivement.</span><span class="sxs-lookup"><span data-stu-id="56c5f-159">Use hello **deviceId** and **primaryKey** of hello device you created in hello previous section tooreplace hello `<deviceId>` and `<primaryKey>` respectively.</span></span> <span data-ttu-id="56c5f-160">Remplacez `<hostName>` par le nom d’hôte de votre IoT Hub, généralement `<IoT hub name>.azure-devices.net`.</span><span class="sxs-lookup"><span data-stu-id="56c5f-160">Replace `<hostName>` with your IoT hub's host name, usually as `<IoT hub name>.azure-devices.net`.</span></span>

    ```python
    # String containing Hostname, Device Id & Device Key in hello format
    CONNECTION_STRING = "[IoTHub Device Connection String]"
    # choose HTTP, AMQP or MQTT as transport protocol
    PROTOCOL = IoTHubTransportProvider.MQTT
    MESSAGE_TIMEOUT = 10000
    AVG_WIND_SPEED = 10.0
    SEND_CALLBACKS = 0
    MSG_TXT = "{\"deviceId\": \"MyFirstPythonDevice\",\"windSpeed\": %.2f}"    
    ```
5. <span data-ttu-id="56c5f-161">Ajoutez hello suivant code toodefine un rappel de confirmation d’envoi.</span><span class="sxs-lookup"><span data-stu-id="56c5f-161">Add hello following code toodefine a send confirmation callback.</span></span> 

    ```python
    def send_confirmation_callback(message, result, user_context):
        global SEND_CALLBACKS
        print ( "Confirmation[%d] received for message with result = %s" % (user_context, result) )
        map_properties = message.properties()
        print ( "    message_id: %s" % message.message_id )
        print ( "    correlation_id: %s" % message.correlation_id )
        key_value_pair = map_properties.get_internals()
        print ( "    Properties: %s" % key_value_pair )
        SEND_CALLBACKS += 1
        print ( "    Total calls confirmed: %d" % SEND_CALLBACKS )
    ```
6. <span data-ttu-id="56c5f-162">Ajoutez hello suivant du client de périphérique code tooinitialize hello.</span><span class="sxs-lookup"><span data-stu-id="56c5f-162">Add hello following code tooinitialize hello device client.</span></span>

    ```python
    def iothub_client_init():
        # prepare iothub client
        client = IoTHubClient(CONNECTION_STRING, PROTOCOL)
        # set hello time until a message times out
        client.set_option("messageTimeout", MESSAGE_TIMEOUT)
        client.set_option("logtrace", 0)
        return client
    ```
7. <span data-ttu-id="56c5f-163">Ajouter suivant de hello fonction tooformat et envoyer un message à partir de votre appareil simulé tooyour IoT de supervision.</span><span class="sxs-lookup"><span data-stu-id="56c5f-163">Add hello following function tooformat and send a message from your simulated device tooyour IoT hub.</span></span>

    ```python
    def iothub_client_telemetry_sample_run():

        try:
            client = iothub_client_init()
            print ( "IoT Hub device sending periodic messages, press Ctrl-C tooexit" )
            message_counter = 0

            while True:
                msg_txt_formatted = MSG_TXT % (AVG_WIND_SPEED + (random.random() * 4 + 2))
                # messages can be encoded as string or bytearray
                if (message_counter & 1) == 1:
                    message = IoTHubMessage(bytearray(msg_txt_formatted, 'utf8'))
                else:
                    message = IoTHubMessage(msg_txt_formatted)
                # optional: assign ids
                message.message_id = "message_%d" % message_counter
                message.correlation_id = "correlation_%d" % message_counter
                # optional: assign properties
                prop_map = message.properties()
                prop_text = "PropMsg_%d" % message_counter
                prop_map.add("Property", prop_text)

                client.send_event_async(message, send_confirmation_callback, message_counter)
                print ( "IoTHubClient.send_event_async accepted message [%d] for transmission tooIoT Hub." % message_counter )

                status = client.get_send_status()
                print ( "Send status: %s" % status )
                time.sleep(30)

                status = client.get_send_status()
                print ( "Send status: %s" % status )

                message_counter += 1

        except IoTHubError as iothub_error:
            print ( "Unexpected error %s from IoTHub" % iothub_error )
            return
        except KeyboardInterrupt:
            print ( "IoTHubClient sample stopped" )
    ```
8. <span data-ttu-id="56c5f-164">Enfin, ajoutez les fonction principale hello.</span><span class="sxs-lookup"><span data-stu-id="56c5f-164">Finally, add hello main function.</span></span> 

    ```python
    if __name__ == '__main__':
        print ( "Simulating a device using hello Azure IoT Hub Device SDK for Python" )
        print ( "    Protocol %s" % PROTOCOL )
        print ( "    Connection string=%s" % CONNECTION_STRING )

        iothub_client_telemetry_sample_run()
    ```
9. <span data-ttu-id="56c5f-165">Enregistrez et fermez hello **SimulatedDevice.py** fichier.</span><span class="sxs-lookup"><span data-stu-id="56c5f-165">Save and close hello **SimulatedDevice.py** file.</span></span> <span data-ttu-id="56c5f-166">Vous est désormais prêt toorun cette application.</span><span class="sxs-lookup"><span data-stu-id="56c5f-166">You are now ready toorun this app.</span></span>

> [!NOTE]
> <span data-ttu-id="56c5f-167">tookeep les choses simples, ce didacticiel n’implémente pas de toute stratégie de nouvelle tentative.</span><span class="sxs-lookup"><span data-stu-id="56c5f-167">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="56c5f-168">Dans le code de production, vous devez implémenter des stratégies de nouvelle tentative (par exemple, une interruption exponentielle), comme indiqué dans l’article hello [gestion des pannes temporaires][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="56c5f-168">In production code, you should implement retry policies (such as an exponential backoff), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 

## <a name="receive-messages-from-your-simulated-device"></a><span data-ttu-id="56c5f-169">Réception de messages à partir de votre appareil simulé</span><span class="sxs-lookup"><span data-stu-id="56c5f-169">Receive messages from your simulated device</span></span>
<span data-ttu-id="56c5f-170">messages de télémétrie tooreceive à partir de votre appareil, vous devez toouse une [concentrateurs d’événements][lnk-event-hubs-overview]-point de terminaison compatible exposée par hello IoT Hub, qui lit les messages appareil-à-cloud hello.</span><span class="sxs-lookup"><span data-stu-id="56c5f-170">tooreceive telemetry messages from your device, you need toouse an [Event Hubs][lnk-event-hubs-overview]-compatible endpoint exposed by hello IoT Hub, which reads hello device-to-cloud messages.</span></span> <span data-ttu-id="56c5f-171">Hello de lecture [prise en main les concentrateurs d’événements] [ lnk-eventhubs-tutorial] didacticiel pour plus d’informations sur la manière dont les messages à partir de concentrateurs d’événements tooprocess pour le point de terminaison de votre hub IoT Hub d’événements compatibles.</span><span class="sxs-lookup"><span data-stu-id="56c5f-171">Read hello [Get Started with Event Hubs][lnk-eventhubs-tutorial] tutorial for information on how tooprocess messages from Event Hubs for your IoT hub's Event Hub-compatible endpoint.</span></span> <span data-ttu-id="56c5f-172">Concentrateurs d’événements ne prend pas en charge télémétrie dans Python encore, vous pouvez créer un [Node.js](iot-hub-node-node-getstarted.md#D2C_node) ou un [.NET](iot-hub-csharp-csharp-getstarted.md#D2C_csharp) console basée sur les concentrateurs d’événements application tooread hello messages appareil-à-cloud à partir de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="56c5f-172">Event Hubs does not support telemetry in Python yet, so you can either create a [Node.js](iot-hub-node-node-getstarted.md#D2C_node) or a [.NET](iot-hub-csharp-csharp-getstarted.md#D2C_csharp) Event Hubs-based console app tooread hello device-to-cloud messages from IoT Hub.</span></span> <span data-ttu-id="56c5f-173">Ce didacticiel montre comment vous pouvez utiliser hello [outil Explorateur de Hub IoT] [ lnk-iot-hub-explorer] tooread ces messages de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="56c5f-173">This tutorial shows how you can use hello [IoT Hub Explorer tool][lnk-iot-hub-explorer] tooread these device messages.</span></span>

1. <span data-ttu-id="56c5f-174">Ouvrez une invite de commandes et installer hello IoT Hub Explorer.</span><span class="sxs-lookup"><span data-stu-id="56c5f-174">Open a command prompt and install hello IoT Hub Explorer.</span></span> 

    ```
    npm install -g iothub-explorer
    ```

2. <span data-ttu-id="56c5f-175">Exécutez hello commande suivante sur l’invite de commandes hello, toobegin analyse hello messages appareil-à-cloud à partir de votre appareil.</span><span class="sxs-lookup"><span data-stu-id="56c5f-175">Run hello following command on hello command prompt, toobegin monitoring hello device-to-cloud messages from your device.</span></span> <span data-ttu-id="56c5f-176">Utilisez la chaîne de connexion de votre hub IoT dans l’espace réservé de hello après `--login`.</span><span class="sxs-lookup"><span data-stu-id="56c5f-176">Use your IoT hub's connection string in hello placeholder after `--login`.</span></span>

    ```
    iothub-explorer monitor-events MyFirstPythonDevice --login "[IoTHub connection string]"
    ```

3. <span data-ttu-id="56c5f-177">Ouvrez une nouvelle invite de commandes et accédez répertoire toohello contenant hello **SimulatedDevice.py** fichier.</span><span class="sxs-lookup"><span data-stu-id="56c5f-177">Open a new command prompt and navigate toohello directory containing hello **SimulatedDevice.py** file.</span></span>

4. <span data-ttu-id="56c5f-178">Exécutez hello **SimulatedDevice.py** fichier, qui envoie périodiquement tooyour IoT hub de télémétrie des données.</span><span class="sxs-lookup"><span data-stu-id="56c5f-178">Run hello **SimulatedDevice.py** file, which periodically sends telemetry data tooyour IoT hub.</span></span> 
   
    ```
    python SimulatedDevice.py
    ```
5. <span data-ttu-id="56c5f-179">Observez les messages d’appareil hello sur invite de commandes hello hello IoT Hub Explorer en cours d’exécution à partir de la section précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="56c5f-179">Observe hello device messages on hello command prompt running hello IoT Hub Explorer from hello previous section.</span></span> 

    ![Messages appareil-à-cloud Python][2]

## <a name="next-steps"></a><span data-ttu-id="56c5f-181">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="56c5f-181">Next steps</span></span>
<span data-ttu-id="56c5f-182">Dans ce didacticiel, vous configuré un IoT hub Bonjour portail Azure et ensuite créé une identité d’appareil dans le Registre des identités de hello IoT hub.</span><span class="sxs-lookup"><span data-stu-id="56c5f-182">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="56c5f-183">Vous avez utilisé ce périphérique identité tooenable hello simulée appareil application toosend messages appareil-à-cloud toohello hub IoT.</span><span class="sxs-lookup"><span data-stu-id="56c5f-183">You used this device identity tooenable hello simulated device app toosend device-to-cloud messages toohello IoT hub.</span></span> <span data-ttu-id="56c5f-184">Vous observé les messages hello reçus par hello IoT hub à l’aide de hello de hello IoT Hub Explorateur.</span><span class="sxs-lookup"><span data-stu-id="56c5f-184">You observed hello messages received by hello IoT hub with hello help of hello IoT Hub Explorer tool.</span></span> 

<span data-ttu-id="56c5f-185">tooexplore hello Python SDK pour l’utilisation d’Azure IoT Hub en profondeur, visitez [ce référentiel Git Hub][lnk-python-github].</span><span class="sxs-lookup"><span data-stu-id="56c5f-185">tooexplore hello Python SDK for Azure IoT Hub usage in depth, visit [this Git Hub repo][lnk-python-github].</span></span> <span data-ttu-id="56c5f-186">fonctionnalités de messagerie hello tooreview Hello Azure IoT Hub Service SDK pour Python, vous pouvez télécharger et exécuter [iothub_messaging_sample.py][lnk-messaging-sample].</span><span class="sxs-lookup"><span data-stu-id="56c5f-186">tooreview hello messaging capabilities of hello Azure IoT Hub Service SDK for Python, you can download and run [iothub_messaging_sample.py][lnk-messaging-sample].</span></span> <span data-ttu-id="56c5f-187">Pour la simulation de côté l’appareil à l’aide de hello Azure IoT Hub appareil SDK pour Python, vous pouvez télécharger et exécuter hello [iothub_client_sample.py][lnk-client-sample].</span><span class="sxs-lookup"><span data-stu-id="56c5f-187">For device side simulation using hello Azure IoT Hub Device SDK for Python, you can download and run hello [iothub_client_sample.py][lnk-client-sample].</span></span>

<span data-ttu-id="56c5f-188">toocontinue mise en route avec IoT Hub et tooexplore autres scénarios IoT, consultez :</span><span class="sxs-lookup"><span data-stu-id="56c5f-188">toocontinue getting started with IoT Hub and tooexplore other IoT scenarios, see:</span></span>

* <span data-ttu-id="56c5f-189">[Connexion de votre appareil][lnk-connect-device]</span><span class="sxs-lookup"><span data-stu-id="56c5f-189">[Connecting your device][lnk-connect-device]</span></span>
* <span data-ttu-id="56c5f-190">[Prise en main de la gestion d’appareils][lnk-device-management]</span><span class="sxs-lookup"><span data-stu-id="56c5f-190">[Getting started with device management][lnk-device-management]</span></span>
* <span data-ttu-id="56c5f-191">[Explore Azure IoT Edge architecture on Linux][lnk-iot-edge] (Découvrir l’architecture Azure IoT Edge sur Linux)</span><span class="sxs-lookup"><span data-stu-id="56c5f-191">[Getting started with Azure IoT Edge][lnk-iot-edge]</span></span>

<span data-ttu-id="56c5f-192">toolearn tooextend vos messages IoT solution et des processus de périphérique dans le cloud à grande échelle, voir hello [traiter les messages appareil-à-cloud] [ lnk-process-d2c-tutorial] didacticiel.</span><span class="sxs-lookup"><span data-stu-id="56c5f-192">toolearn how tooextend your IoT solution and process device-to-cloud messages at scale, see hello [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span></span>
[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]

<!-- Images. -->
[1]: ./media/iot-hub-python-getstarted/createdevice.png
[2]: ./media/iot-hub-python-getstarted/sendd2cmessage.png

<!-- Links -->
[lnk-python-download]: https://www.python.org/downloads/
[lnk-visual-c-redist]: http://www.microsoft.com/download/confirmation.aspx?id=48145
[lnk-node-download]: https://nodejs.org/en/download/
[lnk-install-pip]: https://pip.pypa.io/en/stable/installing/
[lnk-azure-cli-hub]: https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-create-using-cli
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[lnk-idle]: https://docs.python.org/3/library/idle.html
[lnk-python-ide-list]: https://wiki.python.org/moin/IntegratedDevelopmentEnvironments
[lnk-iot-hub-explorer]: https://github.com/Azure/iothub-explorer
[lnk-python-github]: https://github.com/Azure/azure-iot-sdk-python
[lnk-messaging-sample]: https://github.com/Azure/azure-iot-sdk-python/blob/master/service/samples/iothub_messaging_sample.py
[lnk-client-sample]: https://github.com/Azure/azure-iot-sdk-python/blob/master/device/samples/iothub_client_sample.py

[lnk-eventhubs-tutorial]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md
[lnk-devguide-identity]: iot-hub-devguide-identity-registry.md
[lnk-event-hubs-overview]: ../event-hubs/event-hubs-overview.md
[lnk-python-devbox]: https://github.com/Azure/azure-iot-sdk-python/blob/master/doc/python-devbox-setup.md

[lnk-process-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/
