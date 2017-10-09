---
title: aaaUse un tooconnect de passerelle un tooAzure appareil IoT Hub IoT | Documents Microsoft
description: "Découvrez comment toouse NUC Intel comme un tooconnect de passerelle IoT un SensorTag TI et envoi capteur données tooAzure IoT Hub Bonjour cloud."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "la passerelle est IOT connexion toocloud de périphérique"
ms.assetid: cb851648-018c-4a7e-860f-b62ed3b493a5
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/25/2017
ms.author: xshi
ms.openlocfilehash: 418af34bf29992d46b76ae59ef548744808664c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-iot-gateway-tooconnect-things-toohello-cloud---sensortag-tooazure-iot-hub"></a><span data-ttu-id="aee56-104">Utilisez IoT passerelle tooconnect choses toohello cloud - SensorTag tooAzure IoT Hub</span><span class="sxs-lookup"><span data-stu-id="aee56-104">Use IoT gateway tooconnect things toohello cloud - SensorTag tooAzure IoT Hub</span></span>

> [!NOTE]
> <span data-ttu-id="aee56-105">Avant de commencer ce didacticiel, vérifiez que vous avez suivi le didacticiel [Configurer l’Intel NUC comme passerelle IoT](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md).</span><span class="sxs-lookup"><span data-stu-id="aee56-105">Before you start this tutorial, make sure you’ve completed [Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md).</span></span> <span data-ttu-id="aee56-106">Dans [configurer NUC Intel comme passerelle IoT](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md), vous configurez appareil d’Intel NUC hello comme passerelle IoT.</span><span class="sxs-lookup"><span data-stu-id="aee56-106">In [Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md), you set up hello Intel NUC device as an IoT gateway.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="aee56-107">Contenu</span><span class="sxs-lookup"><span data-stu-id="aee56-107">What you will learn</span></span>

<span data-ttu-id="aee56-108">Vous apprendrez comment toouse un tooconnect de passerelle un tooAzure Texas Instruments SensorTag (CC2650STK) IoT Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="aee56-108">You learn how toouse an IoT gateway tooconnect a Texas Instruments SensorTag (CC2650STK) tooAzure IoT Hub.</span></span> <span data-ttu-id="aee56-109">passerelle de IoT Hello envoie la température et de données de l’humidité collectés hello SensorTag tooAzure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="aee56-109">hello IoT gateway sends temperature and humidity data collected from hello SensorTag tooAzure IoT Hub.</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="aee56-110">Procédure à suivre</span><span class="sxs-lookup"><span data-stu-id="aee56-110">What you will do</span></span>

- <span data-ttu-id="aee56-111">Créez un hub IoT.</span><span class="sxs-lookup"><span data-stu-id="aee56-111">Create an IoT hub.</span></span>
- <span data-ttu-id="aee56-112">Inscrire un appareil dans hello IoT hub pour hello SensorTag.</span><span class="sxs-lookup"><span data-stu-id="aee56-112">Register a device in hello IoT hub for hello SensorTag.</span></span>
- <span data-ttu-id="aee56-113">Activer des connexions entre la passerelle de IoT hello et hello SensorTag hello.</span><span class="sxs-lookup"><span data-stu-id="aee56-113">Enable hello connection between hello IoT gateway and hello SensorTag.</span></span>
- <span data-ttu-id="aee56-114">Exécutez un ver exemple application toosend SensorTag tooyour IoT concentrateur de données.</span><span class="sxs-lookup"><span data-stu-id="aee56-114">Run a BLE sample application toosend SensorTag data tooyour IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="aee56-115">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="aee56-115">What you need</span></span>

- <span data-ttu-id="aee56-116">Didacticiel [Configurer l’Intel NUC comme passerelle IoT](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md) suivi dans lequel vous configurez l’Intel NUC comme passerelle IoT.</span><span class="sxs-lookup"><span data-stu-id="aee56-116">Tutorial [Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md) completed in which you set up Intel NUC as an IoT gateway.</span></span>
- * <span data-ttu-id="aee56-117">Un abonnement Azure actif.</span><span class="sxs-lookup"><span data-stu-id="aee56-117">An active Azure subscription.</span></span> <span data-ttu-id="aee56-118">Si vous ne possédez pas de compte Azure, vous pouvez [créer un compte d’évaluation Azure gratuit](https://azure.microsoft.com/free/) en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="aee56-118">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
- <span data-ttu-id="aee56-119">Un client SSH qui s’exécute sur votre ordinateur hôte.</span><span class="sxs-lookup"><span data-stu-id="aee56-119">An SSH client that runs on your host computer.</span></span> <span data-ttu-id="aee56-120">PuTTY est recommandé sur Windows.</span><span class="sxs-lookup"><span data-stu-id="aee56-120">PuTTY is recommended on Windows.</span></span> <span data-ttu-id="aee56-121">Linux et macOS sont déjà accompagnés d’un client SSH.</span><span class="sxs-lookup"><span data-stu-id="aee56-121">Linux and macOS already come with an SSH client.</span></span>
- <span data-ttu-id="aee56-122">adresse IP de Hello et hello nom d’utilisateur et mot de passe tooaccess hello passerelle à partir du client SSH hello.</span><span class="sxs-lookup"><span data-stu-id="aee56-122">hello IP address and hello username and password tooaccess hello gateway from hello SSH client.</span></span>
- <span data-ttu-id="aee56-123">Une connexion Internet.</span><span class="sxs-lookup"><span data-stu-id="aee56-123">An Internet connection.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

> [!NOTE]
> <span data-ttu-id="aee56-124">Ici vous inscrivez ce nouvel appareil pour votre SensorTag</span><span class="sxs-lookup"><span data-stu-id="aee56-124">Here you register this new device for your SensorTag</span></span>

## <a name="enable-hello-connection-between-hello-iot-gateway-and-hello-sensortag"></a><span data-ttu-id="aee56-125">Activer la connexion hello entre la passerelle de IoT hello et hello SensorTag</span><span class="sxs-lookup"><span data-stu-id="aee56-125">Enable hello connection between hello IoT gateway and hello SensorTag</span></span>

<span data-ttu-id="aee56-126">Dans cette section, vous effectuez hello tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="aee56-126">In this section, you perform hello following tasks:</span></span>

- <span data-ttu-id="aee56-127">Obtenir l’adresse MAC de hello Hello SensorTag pour connexion Bluetooth.</span><span class="sxs-lookup"><span data-stu-id="aee56-127">Get hello MAC address of hello SensorTag for Bluetooth connection.</span></span>
- <span data-ttu-id="aee56-128">Établir une connexion Bluetooth à partir de la passerelle toohello SensorTag de hello IoT.</span><span class="sxs-lookup"><span data-stu-id="aee56-128">Initiate a Bluetooth connection from hello IoT gateway toohello SensorTag.</span></span>

### <a name="get-hello-mac-address-of-hello-sensortag-for-bluetooth-connection"></a><span data-ttu-id="aee56-129">Obtenir l’adresse MAC de hello Hello SensorTag pour connexion Bluetooth</span><span class="sxs-lookup"><span data-stu-id="aee56-129">Get hello MAC address of hello SensorTag for Bluetooth connection</span></span>

1. <span data-ttu-id="aee56-130">Sur l’ordinateur hôte hello, exécutez hello SSH client et toohello IoT passerelle de connexion.</span><span class="sxs-lookup"><span data-stu-id="aee56-130">On hello host computer, run hello SSH client and connect toohello IoT gateway.</span></span>
1. <span data-ttu-id="aee56-131">Débloquer Bluetooth en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="aee56-131">Unblock Bluetooth by running hello following command:</span></span>

   ```bash
   sudo rfkill unblock bluetooth
   ```

1. <span data-ttu-id="aee56-132">Démarrer le service de Bluetooth hello sur la passerelle IoT hello et entrez un tooconfigure de shell Bluetooth Bluetooth en exécutant hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="aee56-132">Start hello Bluetooth service on hello IoT gateway and enter a Bluetooth shell tooconfigure Bluetooth by running hello following commands:</span></span>

   ```bash
   sudo systemctl start bluetooth
   bluetoothctl
   ```

1. <span data-ttu-id="aee56-133">Contrôleur Bluetooth hello en cours d’exécution de mise sous tension hello commande à hello Bluetooth shell suivante :</span><span class="sxs-lookup"><span data-stu-id="aee56-133">Power on hello Bluetooth controller by running hello following command at hello Bluetooth shell:</span></span>

   ```bash
   power on
   ```

   ![contrôleur de Bluetooth hello sur la passerelle IoT hello avec bluetoothctl mise sous tension](./media/iot-hub-iot-gateway-connect-device-to-cloud/8_power-on-bluetooth-controller-at-bluetooth-shell-bluetoothctl.png)

1. <span data-ttu-id="aee56-135">Démarrer l’analyse pour à proximité d’appareils Bluetooth en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="aee56-135">Start scanning for nearby Bluetooth devices by running hello following command:</span></span>

   ```bash
   scan on
   ```

   ![Analyser les périphériques Bluetooth proches avec bluetoothctl](./media/iot-hub-iot-gateway-connect-device-to-cloud/9_start-scan-nearby-bluetooth-devices-at-bluetooth-shell-bluetoothctl.png)

1. <span data-ttu-id="aee56-137">Appuyez sur hello bouton sur hello SensorTag d’appariement.</span><span class="sxs-lookup"><span data-stu-id="aee56-137">Press hello pairing button on hello SensorTag.</span></span> <span data-ttu-id="aee56-138">Hello vert LED sur hello SensorTag clignote.</span><span class="sxs-lookup"><span data-stu-id="aee56-138">hello green LED on hello SensorTag flashes.</span></span>
1. <span data-ttu-id="aee56-139">À hello Bluetooth shell, vous devez voir hello que sensortag est trouvé.</span><span class="sxs-lookup"><span data-stu-id="aee56-139">At hello Bluetooth shell, you should see hello SensorTag is found.</span></span> <span data-ttu-id="aee56-140">Prenez note de hello adresse MAC de hello SensorTag.</span><span class="sxs-lookup"><span data-stu-id="aee56-140">Make a note of hello MAC address of hello SensorTag.</span></span> <span data-ttu-id="aee56-141">Dans cet exemple, hello adresse MAC de hello SensorTag est `24:71:89:C0:7F:82`.</span><span class="sxs-lookup"><span data-stu-id="aee56-141">In this example, hello MAC address of hello SensorTag is `24:71:89:C0:7F:82`.</span></span>
1. <span data-ttu-id="aee56-142">Désactiver hello analyse en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="aee56-142">Turn off hello scan by running hello following command:</span></span>

   ```bash
   scan off
   ```

   ![Arrêter l’analyse des périphériques Bluetooth proches avec bluetoothctl](./media/iot-hub-iot-gateway-connect-device-to-cloud/10_stop-scanning-nearby-bluetooth-devices-at-bluetooth-shell-bluetoothctl.png)

### <a name="initiate-a-bluetooth-connection-from-hello-iot-gateway-toohello-sensortag"></a><span data-ttu-id="aee56-144">Établir une connexion Bluetooth à partir de la passerelle toohello SensorTag de hello IoT</span><span class="sxs-lookup"><span data-stu-id="aee56-144">Initiate a Bluetooth connection from hello IoT gateway toohello SensorTag</span></span>

1. <span data-ttu-id="aee56-145">Se connecter toohello SensorTag en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="aee56-145">Connect toohello SensorTag by running hello following command:</span></span>

   ```bash
   connect <MAC address>
   ```

   ![Rejoignez toohello SensorTag bluetoothctl](./media/iot-hub-iot-gateway-connect-device-to-cloud/11_connect-to-sensortag-at-bluetooth-shell-bluetoothctl.png)

1. <span data-ttu-id="aee56-147">Déconnectez hello SensorTag et quitter le shell de Bluetooth hello en hello suivant les commandes en cours d’exécution :</span><span class="sxs-lookup"><span data-stu-id="aee56-147">Disconnect from hello SensorTag and exit hello Bluetooth shell by running hello following commands:</span></span>

   ```bash
   disconnect
   exit
   ```

   ![Déconnectez hello SensorTag avec bluetoothctl](./media/iot-hub-iot-gateway-connect-device-to-cloud/12_disconnect-from-sensortag-at-bluetooth-shell-bluetoothctl.png)

<span data-ttu-id="aee56-149">Vous avez activé connexion hello entre hello SensorTag et passerelle de IoT hello.</span><span class="sxs-lookup"><span data-stu-id="aee56-149">You've successfully enabled hello connection between hello SensorTag and hello IoT gateway.</span></span>

## <a name="run-a-ble-sample-application-toosend-sensortag-data-tooyour-iot-hub"></a><span data-ttu-id="aee56-150">Exécuter un ver exemple application toosend SensorTag tooyour IoT concentrateur de données</span><span class="sxs-lookup"><span data-stu-id="aee56-150">Run a BLE sample application toosend SensorTag data tooyour IoT hub</span></span>

<span data-ttu-id="aee56-151">Hello, exemple d’application Bluetooth faible énergie (tableau) est fournie par Azure IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="aee56-151">hello Bluetooth Low Energy (BLE) sample application is provided by Azure IoT Edge.</span></span> <span data-ttu-id="aee56-152">exemple d’application Hello collecte les données de connexion de l’activer et envoyer tooyou IoT hub hello données.</span><span class="sxs-lookup"><span data-stu-id="aee56-152">hello sample application collects data from BLE connection and send hello data tooyou IoT hub.</span></span> <span data-ttu-id="aee56-153">toorun hello exemple d’application, vous devez :</span><span class="sxs-lookup"><span data-stu-id="aee56-153">toorun hello sample application, you need to:</span></span>

1. <span data-ttu-id="aee56-154">Configurer l’application d’exemple hello.</span><span class="sxs-lookup"><span data-stu-id="aee56-154">Configure hello sample application.</span></span>
1. <span data-ttu-id="aee56-155">Exécutez l’exemple d’application hello sur la passerelle IoT hello.</span><span class="sxs-lookup"><span data-stu-id="aee56-155">Run hello sample application on hello IoT gateway.</span></span>

### <a name="configure-hello-sample-application"></a><span data-ttu-id="aee56-156">Configurer l’application d’exemple hello</span><span class="sxs-lookup"><span data-stu-id="aee56-156">Configure hello sample application</span></span>

1. <span data-ttu-id="aee56-157">Accédez toohello le dossier de l’application d’exemple hello en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="aee56-157">Go toohello folder of hello sample application by running hello following command:</span></span>

   ```bash
   cd /usr/share/azureiotgatewaysdk/samples/ble_gateway
   ```

1. <span data-ttu-id="aee56-158">Ouvrez le fichier de configuration de hello en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="aee56-158">Open hello configuration file by running hello following command:</span></span>

   ```bash
   vi ble_gateway.json
   ```

1. <span data-ttu-id="aee56-159">Dans le fichier de configuration de hello, renseignez hello valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="aee56-159">In hello configuration file, fill in hello following values:</span></span>

   <span data-ttu-id="aee56-160">**IoTHubName**: nom hello de votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="aee56-160">**IoTHubName**: hello name of your IoT hub.</span></span>

   <span data-ttu-id="aee56-161">**IoTHubSuffix**: obtenir un IoTHubSuffix à partir de la clé primaire hello hello appareil de chaîne de connexion que vous avez notée vers le bas.</span><span class="sxs-lookup"><span data-stu-id="aee56-161">**IoTHubSuffix**: Get IoTHubSuffix from hello primary key of hello device connection string that you noted down.</span></span> <span data-ttu-id="aee56-162">Assurez-vous d’obtenir la clé primaire de hello de chaîne de connexion de périphérique hello, hello pas de clé primaire de votre chaîne de connexion de hub IoT.</span><span class="sxs-lookup"><span data-stu-id="aee56-162">Ensure that you get hello primary key of hello device connection string, not hello primary key of your IoT hub connection string.</span></span> <span data-ttu-id="aee56-163">clé primaire de Hello de chaîne de connexion de périphérique hello est au format hello de `HostName=IOTHUBNAME.IOTHUBSUFFIX;DeviceId=DEVICEID;SharedAccessKey=SHAREDACCESSKEY`.</span><span class="sxs-lookup"><span data-stu-id="aee56-163">hello primary key of hello device connection string is in hello format of `HostName=IOTHUBNAME.IOTHUBSUFFIX;DeviceId=DEVICEID;SharedAccessKey=SHAREDACCESSKEY`.</span></span>

   <span data-ttu-id="aee56-164">**Transport**: hello la valeur par défaut est `amqp`.</span><span class="sxs-lookup"><span data-stu-id="aee56-164">**Transport**: hello default value is `amqp`.</span></span> <span data-ttu-id="aee56-165">Cette valeur indique le protocole de hello au cours de transpotation.</span><span class="sxs-lookup"><span data-stu-id="aee56-165">This value shows hello protocol during transpotation.</span></span> <span data-ttu-id="aee56-166">Elle peut être `http`, `amqp` ou `mqtt`.</span><span class="sxs-lookup"><span data-stu-id="aee56-166">It could be `http`, `amqp`, or `mqtt`.</span></span>

   <span data-ttu-id="aee56-167">**adresse Mac**: hello adresse MAC de hello SensorTag que vous avez notée vers le bas.</span><span class="sxs-lookup"><span data-stu-id="aee56-167">**macAddress**: hello MAC address of hello SensorTag that you noted down.</span></span>

   <span data-ttu-id="aee56-168">**deviceID**: ID de périphérique hello que vous avez créé dans votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="aee56-168">**deviceID**: ID of hello device that you created in your IoT hub.</span></span>

   <span data-ttu-id="aee56-169">**deviceKey**: clé primaire de hello de chaîne de connexion de périphérique hello.</span><span class="sxs-lookup"><span data-stu-id="aee56-169">**deviceKey**: hello primary key of hello device connection string.</span></span>

   ![Fichier de configuration complet hello Hello, exemple d’application BLE](./media/iot-hub-iot-gateway-connect-device-to-cloud/13_edit-config-file-of-ble-sample.png)

1. <span data-ttu-id="aee56-171">Appuyez sur `ESC` et type `:wq` fichier hello de toosave.</span><span class="sxs-lookup"><span data-stu-id="aee56-171">Press `ESC` and type `:wq` toosave hello file.</span></span>

### <a name="run-hello-sample-application"></a><span data-ttu-id="aee56-172">Exécutez l’exemple d’application hello</span><span class="sxs-lookup"><span data-stu-id="aee56-172">Run hello sample application</span></span>

1. <span data-ttu-id="aee56-173">Vérifiez que hello que sensortag est sous tension.</span><span class="sxs-lookup"><span data-stu-id="aee56-173">Make sure hello SensorTag is powered on.</span></span>
1. <span data-ttu-id="aee56-174">Exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="aee56-174">Run hello following command:</span></span>

   ```bash
   ./ble_gateway ble_gateway.json
   ```

## <a name="next-steps"></a><span data-ttu-id="aee56-175">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="aee56-175">Next steps</span></span>

[<span data-ttu-id="aee56-176">Utiliser une passerelle IoT pour la transformation des données de capteur avec Azure IoT Edge</span><span class="sxs-lookup"><span data-stu-id="aee56-176">Use IoT gateway for sensor data transformation with Azure IoT Edge</span></span>](iot-hub-gateway-kit-c-use-iot-gateway-for-data-conversion.md)
