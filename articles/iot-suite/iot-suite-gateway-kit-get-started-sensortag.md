---
title: "Connecter une passerelle à Azure IoT Suite à l’aide d’un Intel NUC | Documents Microsoft"
description: "Utilisez le Kit de passerelle commerciale Microsoft IoT et la solution préconfigurée de surveillance à distance. Utilisez la passerelle Azure IoT Edge afin d’activer un dispositif SensorTag pour vous connecter à la solution de surveillance à distance, envoyer la télémétrie vers le cloud et répondre aux méthodes appelées à partir du tableau de bord de la solution."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-suite
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/24/2017
ms.author: dobett
ms.openlocfilehash: bda16be1094276fcecef1e708f9d7db307d94a89
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="connect-your-azure-iot-edge-gateway-to-the-remote-monitoring-preconfigured-solution-and-send-telemetry-from-a-sensortag"></a><span data-ttu-id="5df80-104">Connecter votre passerelle Azure IoT Edge à la solution préconfigurée de surveillance à distance et envoyer la télémétrie à partir d’un SensorTag</span><span class="sxs-lookup"><span data-stu-id="5df80-104">Connect your Azure IoT Edge gateway to the remote monitoring preconfigured solution and send telemetry from a SensorTag</span></span>

[!INCLUDE [iot-suite-gateway-kit-selector](../../includes/iot-suite-gateway-kit-selector.md)]

<span data-ttu-id="5df80-105">Ce didacticiel explique comment utiliser Azure IoT Edge pour envoyer les données de température et d’humidité d’un dispositif SensorTag à la solution préconfigurée de surveillance à distance.</span><span class="sxs-lookup"><span data-stu-id="5df80-105">This tutorial shows you how to use Azure IoT Edge to send temperature and humidity data from SensorTag device to the remote monitoring preconfigured solution.</span></span> <span data-ttu-id="5df80-106">Le SensorTag se connecte à la passerelle Intel NUC en utilisant Bluetooth.</span><span class="sxs-lookup"><span data-stu-id="5df80-106">The SensorTag connects to the Intel NUC gateway using Bluetooth.</span></span> <span data-ttu-id="5df80-107">Le tutoriel utilise :</span><span class="sxs-lookup"><span data-stu-id="5df80-107">The tutorial uses:</span></span>

- <span data-ttu-id="5df80-108">Azure IoT Edge pour implémenter un exemple de passerelle.</span><span class="sxs-lookup"><span data-stu-id="5df80-108">Azure IoT Edge to implement a sample gateway.</span></span>
- <span data-ttu-id="5df80-109">la solution préconfigurée de surveillance à distance Azure IoT Suite comme serveur principal basé sur le cloud.</span><span class="sxs-lookup"><span data-stu-id="5df80-109">The IoT Suite remote monitoring preconfigured solution as the cloud-based back end.</span></span>

## <a name="overview"></a><span data-ttu-id="5df80-110">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="5df80-110">Overview</span></span>

<span data-ttu-id="5df80-111">Dans ce didacticiel, vous allez effectuer les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="5df80-111">In this tutorial, you complete the following steps:</span></span>

- <span data-ttu-id="5df80-112">Déployer une instance de la solution préconfigurée de surveillance à distance dans votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="5df80-112">Deploy an instance of the remote monitoring preconfigured solution to your Azure subscription.</span></span> <span data-ttu-id="5df80-113">Cette étape déploie et configure automatiquement plusieurs services Azure.</span><span class="sxs-lookup"><span data-stu-id="5df80-113">This step automatically deploys and configures multiple Azure services.</span></span>
- <span data-ttu-id="5df80-114">Configurez votre périphérique de passerelle Intel NUC pour qu’il communique avec votre ordinateur et la solution de surveillance à distance.</span><span class="sxs-lookup"><span data-stu-id="5df80-114">Set up your Intel NUC gateway device to communicate with your computer and the remote monitoring solution.</span></span>
- <span data-ttu-id="5df80-115">Configurez votre passerelle Intel NUC pour recevoir la télémétrie d’un dispositif SensorTag et envoyer celle-ci au tableau de bord de surveillance à distance.</span><span class="sxs-lookup"><span data-stu-id="5df80-115">Set up your Intel NUC gateway to receive telemetry from a SensorTag device and send it to the remote monitoring dashboard.</span></span>

[!INCLUDE [iot-suite-gateway-kit-prerequisites](../../includes/iot-suite-gateway-kit-prerequisites.md)]

<span data-ttu-id="5df80-116">[Texas Instruments BLE SensorTag][lnk-sensortag].</span><span class="sxs-lookup"><span data-stu-id="5df80-116">[Texas Instruments BLE SensorTag][lnk-sensortag].</span></span> <span data-ttu-id="5df80-117">Ce didacticiel montre comment récupérer les données de télémétrie d’un dispositif SensorTag via Bluetooth.</span><span class="sxs-lookup"><span data-stu-id="5df80-117">This tutorial retrieves telemetry data over Bluetooth from the SensorTag device.</span></span>

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="5df80-118">La solution de surveillance à distance configure un ensemble de services Azure dans votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="5df80-118">The remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="5df80-119">Le déploiement reflète une architecture d’entreprise réelle.</span><span class="sxs-lookup"><span data-stu-id="5df80-119">The deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="5df80-120">Pour éviter des frais de consommation Azure inutiles, supprimez votre instance de la solution préconfigurée dans azureiotsuite.com quand vous ne l’utilisez plus.</span><span class="sxs-lookup"><span data-stu-id="5df80-120">To avoid unnecessary Azure consumption charges, delete your instance of the preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="5df80-121">Si vous avez à nouveau besoin de la solution préconfigurée, vous pouvez la recréer facilement.</span><span class="sxs-lookup"><span data-stu-id="5df80-121">If you need the preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="5df80-122">Pour plus d’informations sur la manière de réduire votre consommation pendant l’exécution de la solution de surveillance à distance, consultez [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config] (Configuration des solutions préconfigurées Azure IoT Suite à des fins de démonstration).</span><span class="sxs-lookup"><span data-stu-id="5df80-122">For more information about reducing consumption while the remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-gateway-kit-view-solution](../../includes/iot-suite-gateway-kit-view-solution.md)]

[!INCLUDE [iot-suite-gateway-kit-prepare-nuc-connectivity](../../includes/iot-suite-gateway-kit-prepare-nuc-connectivity.md)]

## <a name="configure-bluetooth-connectivity"></a><span data-ttu-id="5df80-123">Configurer la connectivité Bluetooth</span><span class="sxs-lookup"><span data-stu-id="5df80-123">Configure Bluetooth connectivity</span></span>

<span data-ttu-id="5df80-124">Configurez Bluetooth sur l’Intel NUC pour permettre au dispositif SensorTag de se connecter et d’envoyer la télémétrie.</span><span class="sxs-lookup"><span data-stu-id="5df80-124">Configure Bluetooth on the Intel NUC to enable the SensorTag device to connect and send telemetry.</span></span>

### <a name="find-the-mac-address-of-the-sensortag"></a><span data-ttu-id="5df80-125">Rechercher l’adresse MAC du SensorTag</span><span class="sxs-lookup"><span data-stu-id="5df80-125">Find the MAC address of the SensorTag</span></span>

1. <span data-ttu-id="5df80-126">Dans le shell sur l’Intel NUC, exécutez la commande suivante pour débloquer le service Bluetooth :</span><span class="sxs-lookup"><span data-stu-id="5df80-126">In the shell on the Intel NUC, run the following command to unblock the Bluetooth service:</span></span>

    ```bash
    sudo rfkill unblock bluetooth
    ```

1. <span data-ttu-id="5df80-127">Exécutez les commandes suivantes pour démarrer le service Bluetooth sur l’Intel NUC, puis entrez dans le shell Bluetooth :</span><span class="sxs-lookup"><span data-stu-id="5df80-127">Run the following commands to start the Bluetooth service on the Intel NUC and enter the Bluetooth shell:</span></span>

    ```bash
    sudo systemctl start bluetooth
    bluetoothctl
    ```

1. <span data-ttu-id="5df80-128">Exécutez la commande suivante pour activer le contrôleur Bluetooth :</span><span class="sxs-lookup"><span data-stu-id="5df80-128">Run the following command to power on the Bluetooth controller:</span></span>

    ```bash
    power on
    ```

    <span data-ttu-id="5df80-129">Lorsque le contrôleur est activé, vous voyez un message indiquant que l’**activation a réussi**.</span><span class="sxs-lookup"><span data-stu-id="5df80-129">When the controller is on, you see a message **Changing power on succeeded**.</span></span>

1. <span data-ttu-id="5df80-130">Exécutez la commande suivante pour rechercher des périphériques Bluetooth à proximité :</span><span class="sxs-lookup"><span data-stu-id="5df80-130">Run the following command to scan for nearby Bluetooth devices:</span></span>

    ```bash
    scan on
    ```

1. <span data-ttu-id="5df80-131">Appuyez sur le bouton d’alimentation du SensorTag pour le rendre détectable.</span><span class="sxs-lookup"><span data-stu-id="5df80-131">Press the power button on the SensorTag to make it discoverable.</span></span> <span data-ttu-id="5df80-132">La DEL verte clignote.</span><span class="sxs-lookup"><span data-stu-id="5df80-132">The green LED flashes.</span></span>

1. <span data-ttu-id="5df80-133">Lorsque vous voyez un message dans le shell indiquant que le contrôleur a détecté le SensorTag, prenez note de l’adresse MAC du périphérique.</span><span class="sxs-lookup"><span data-stu-id="5df80-133">When you see a message in the shell that the controller has discovered the SensorTag, make a note of the MAC address of the device.</span></span> <span data-ttu-id="5df80-134">L’adresse MAC ressemble à **A0:E6:F8:B5:F6:00**.</span><span class="sxs-lookup"><span data-stu-id="5df80-134">The MAC address looks like **A0:E6:F8:B5:F6:00**.</span></span> <span data-ttu-id="5df80-135">Vous aurez besoin de l’adresse MAC ultérieurement dans ce didacticiel pour configurer la passerelle.</span><span class="sxs-lookup"><span data-stu-id="5df80-135">You need the MAC address later in the tutorial when you configure the gateway.</span></span>

1. <span data-ttu-id="5df80-136">Exécutez la commande suivante pour désactiver l’analyse Bluetooth :</span><span class="sxs-lookup"><span data-stu-id="5df80-136">Run the following command to turn off Bluetooth scanning:</span></span>

    ```bash
    scan off
    ```

1. <span data-ttu-id="5df80-137">Exécutez la commande suivante pour vérifier que vous pouvez vous connecter au dispositif SensorTag :</span><span class="sxs-lookup"><span data-stu-id="5df80-137">Run the following command to verify that you can connect to the SensorTag device:</span></span>

    ```bash
    connect <SensorTag MAC address>
    ```

    <span data-ttu-id="5df80-138">Si la connexion aboutit, la shell affiche le message **Connexion réussie** et imprime des informations concernant le dispositif SensorTag.</span><span class="sxs-lookup"><span data-stu-id="5df80-138">If you connect successfully, the shell shows the message **Connection successful** and prints information about the SensorTag device.</span></span> <span data-ttu-id="5df80-139">Si vous ne pouvez pas vous connecter, vérifiez que le SensorTag est toujours sous tension.</span><span class="sxs-lookup"><span data-stu-id="5df80-139">If you cannot connect, check the SensorTag is still powered on.</span></span>

1. <span data-ttu-id="5df80-140">Vous pouvez vous déconnecter du SensorTag et quitter la shell Bluetooth en exécutant les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="5df80-140">You can now disconnect from the SensorTag and exit the Bluetooth shell by running the following commands:</span></span>

    ```bash
    disconnect
    exit
    ```

[!INCLUDE [iot-suite-gateway-kit-prepare-nuc-software](../../includes/iot-suite-gateway-kit-prepare-nuc-software.md)]

## <a name="build-the-custom-iot-edge-module"></a><span data-ttu-id="5df80-141">Générer le module IoT Edge personnalisé</span><span class="sxs-lookup"><span data-stu-id="5df80-141">Build the custom IoT Edge module</span></span>

<span data-ttu-id="5df80-142">Vous pouvez maintenant générer le module IoT personnalisé qui permet à la passerelle d’envoyer des messages à la solution de surveillance à distance.</span><span class="sxs-lookup"><span data-stu-id="5df80-142">You can now build the custom IoT Edge module that enables the gateway to send messages to the remote monitoring solution.</span></span> <span data-ttu-id="5df80-143">Pour plus d’informations sur la configuration d’une passerelle et des modules IoT Edge, voir [Concepts relatifs à Azure IoT Edge][lnk-gateway-concepts].</span><span class="sxs-lookup"><span data-stu-id="5df80-143">For more information about configuring a gateway and IoT Edge modules, see [Azure IoT Edge concepts][lnk-gateway-concepts].</span></span>

<span data-ttu-id="5df80-144">Téléchargez le code source pour les modules IoT Edge personnalisés à partir de GitHub à l’aide des commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="5df80-144">Download the source code for the custom IoT Edge modules from GitHub using the following commands:</span></span>

```bash
cd ~
git clone https://github.com/Azure-Samples/iot-remote-monitoring-c-intel-nuc-gateway-getting-started.git
```

<span data-ttu-id="5df80-145">Générez le module IoT Edge personnalisé à l’aide des commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="5df80-145">Build the custom IoT Edge module using the following commands:</span></span>

```bash
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/basic
chmod u+x build.sh
sed -i -e 's/\r$//' build.sh
./build.sh
```

<span data-ttu-id="5df80-146">Le script de génération place le module IoT Edge personnalisé libsensor2remotemonitoring.so dans le dossier de génération.</span><span class="sxs-lookup"><span data-stu-id="5df80-146">The build script places the libsensor2remotemonitoring.so custom IoT Edge module in the build folder.</span></span>

## <a name="configure-and-run-the-iot-edge-gateway"></a><span data-ttu-id="5df80-147">Configurer et exécuter la passerelle IoT Edge</span><span class="sxs-lookup"><span data-stu-id="5df80-147">Configure and run the IoT Edge gateway</span></span>

<span data-ttu-id="5df80-148">Vous pouvez à présent configurer la passerelle IoT Edge pour envoyer la télémétrie de votre dispositif SensorTag à votre tableau de bord de surveillance à distance.</span><span class="sxs-lookup"><span data-stu-id="5df80-148">You can now configure the IoT Edge gateway to send telemetry from your SensorTag device to your remote monitoring dashboard.</span></span> <span data-ttu-id="5df80-149">Pour plus d’informations sur la configuration d’une passerelle et des modules IoT Edge, voir [Concepts relatifs à Azure IoT Edge][lnk-gateway-concepts].</span><span class="sxs-lookup"><span data-stu-id="5df80-149">For more information about configuring a gateway and IoT Edge modules, see [Azure IoT Edge concepts][lnk-gateway-concepts].</span></span>

> [!TIP]
> <span data-ttu-id="5df80-150">Dans ce didacticiel, vous utilisez l’éditeur de texte `vi` standard sur l’Intel Nuc.</span><span class="sxs-lookup"><span data-stu-id="5df80-150">In this tutorial, you use the standard `vi` text editor on the Intel NUC.</span></span> <span data-ttu-id="5df80-151">Si vous n’avez pas utilisé `vi` précédemment, vous devez suivre un didacticiel d’introduction, tel que [Unix - Didacticiel de l’éditeur vi][lnk-vi-tutorial], pour vous familiariser avec cet éditeur.</span><span class="sxs-lookup"><span data-stu-id="5df80-151">If you have not used `vi` before, you should complete an introductory tutorial, such as [Unix - The vi Editor Tutorial][lnk-vi-tutorial] to familiarize yourself with this editor.</span></span> <span data-ttu-id="5df80-152">Vous pouvez également installer l’éditeur [nano](https://www.nano-editor.org/), plus convivial, à l’aide de la commande `smart install nano -y`.</span><span class="sxs-lookup"><span data-stu-id="5df80-152">Alternatively, you can install the more user-friendly [nano](https://www.nano-editor.org/) editor using the command `smart install nano -y`.</span></span>

<span data-ttu-id="5df80-153">Ouvrez l’exemple de fichier de configuration dans l’éditeur **vi** à l’aide de la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="5df80-153">Open the sample configuration file in the **vi** editor using the following command:</span></span>

```bash
vi ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/basic/remote_monitoring.json
```

<span data-ttu-id="5df80-154">Recherchez les lignes suivantes dans la configuration pour le module IoTHub :</span><span class="sxs-lookup"><span data-stu-id="5df80-154">Locate the following lines in the configuration for the IoTHub module:</span></span>

```json
"args": {
  "IoTHubName": "<<Azure IoT Hub Name>>",
  "IoTHubSuffix": "<<Azure IoT Hub Suffix>>",
  "Transport": "http"
}
```

<span data-ttu-id="5df80-155">Remplacez les valeurs de l’espace réservé par les informations sur l’IoT Hub que vous avez créées et enregistrées au début de ce tutoriel.</span><span class="sxs-lookup"><span data-stu-id="5df80-155">Replace the placeholder values with the IoT Hub information you created and saved at the start of this tutorial.</span></span> <span data-ttu-id="5df80-156">La valeur de IoTHubName ressemble à **yourrmsolution37e08** et la valeur de IoTSuffix est généralement **azure-devices.net**.</span><span class="sxs-lookup"><span data-stu-id="5df80-156">The value for IoTHubName looks like **yourrmsolution37e08**, and the value for IoTSuffix is typically **azure-devices.net**.</span></span>

<span data-ttu-id="5df80-157">Recherchez les lignes suivantes dans la configuration du module de mappage :</span><span class="sxs-lookup"><span data-stu-id="5df80-157">Locate the following lines in the configuration for the mapping module:</span></span>

```json
args": [
  {
    "macAddress": "<<AA:BB:CC:DD:EE:FF>>",
    "deviceId": "<<Azure IoT Hub Device ID>>",
    "deviceKey": "<<Azure IoT Hub Device Key>>"
  }
]
```

<span data-ttu-id="5df80-158">Remplacez l’espace réservé **macAddress** par l’adresse MAC du SensorTag, que vous avez notée précédemment.</span><span class="sxs-lookup"><span data-stu-id="5df80-158">Replace the **macAddress** placeholder with the MAC address of your SensorTag you noted previously.</span></span> <span data-ttu-id="5df80-159">Remplacez les espaces réservés **deviceID** et **deviceKey** par les ID et les clés des deux appareils que vous avez créés précédemment dans la solution de surveillance à distance.</span><span class="sxs-lookup"><span data-stu-id="5df80-159">Replace the **deviceID** and **deviceKey** placeholders with the IDs and keys for the two devices you created in the remote monitoring solution previously.</span></span>

<span data-ttu-id="5df80-160">Recherchez les lignes suivantes dans la configuration du module SensorTag :</span><span class="sxs-lookup"><span data-stu-id="5df80-160">Locate the following lines in the configuration for the SensorTag module:</span></span>

```json
"args": {
  "controller_index": 0,
  "device_mac_address": "<<AA:BB:CC:DD:EE:FF>>",
  ...
}
```

<span data-ttu-id="5df80-161">Remplacez l’espace réservé **device\_mac\_address** par l’adresse MAC du SensorTag, que vous avez notée précédemment.</span><span class="sxs-lookup"><span data-stu-id="5df80-161">Replace the **device\_mac\_address** placeholder  with the MAC address of your SensorTag you noted previously.</span></span>

<span data-ttu-id="5df80-162">Enregistrez vos modifications.</span><span class="sxs-lookup"><span data-stu-id="5df80-162">Save your changes.</span></span>

<span data-ttu-id="5df80-163">Vous pouvez maintenant exécuter la passerelle en utilisant les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="5df80-163">You can now run the gateway using the following commands:</span></span>

```bash
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/basic
/usr/share/azureiotgatewaysdk/samples/ble_gateway/ble_gateway remote_monitoring.json
```

<span data-ttu-id="5df80-164">La passerelle IoT Edge démarre sur l’Intel NUC et envoie la télémétrie du SensorTag à la solution de surveillance à distance :</span><span class="sxs-lookup"><span data-stu-id="5df80-164">The IoT Edge gateway starts on the Intel NUC and sends telemetry from the SensorTag to the remote monitoring solution:</span></span>

![La passerelle IoT Edge envoie la télémétrie du SensorTag][img-telemetry]

<span data-ttu-id="5df80-166">Appuyez sur **Ctrl-C** pour quitter le programme à tout moment.</span><span class="sxs-lookup"><span data-stu-id="5df80-166">Press **Ctrl-C** to exit the program at any time.</span></span>

## <a name="view-the-telemetry"></a><span data-ttu-id="5df80-167">Afficher les données de télémétrie</span><span class="sxs-lookup"><span data-stu-id="5df80-167">View the telemetry</span></span>

<span data-ttu-id="5df80-168">La passerelle envoie désormais la télémétrie du dispositif SensorTag à la solution de surveillance à distance.</span><span class="sxs-lookup"><span data-stu-id="5df80-168">The gateway is now sending telemetry from the SensorTag device to the remote monitoring solution.</span></span> <span data-ttu-id="5df80-169">Vous pouvez afficher les données de télémétrie sur le tableau de bord de la solution.</span><span class="sxs-lookup"><span data-stu-id="5df80-169">You can view the telemetry on the solution dashboard.</span></span> <span data-ttu-id="5df80-170">Vous pouvez également envoyer des commandes à votre dispositif SensorTag via la passerelle à partir du tableau de bord de la solution.</span><span class="sxs-lookup"><span data-stu-id="5df80-170">You can also send commands to your SensorTag device through the gateway from the solution dashboard.</span></span>

- <span data-ttu-id="5df80-171">Accédez au tableau de bord de la solution.</span><span class="sxs-lookup"><span data-stu-id="5df80-171">Navigate to the solution dashboard.</span></span>
- <span data-ttu-id="5df80-172">Sélectionnez le périphérique que vous avez configuré dans la passerelle, qui représente le SensorTag dans la liste déroulante **Appareil à afficher**.</span><span class="sxs-lookup"><span data-stu-id="5df80-172">Select the device you configured in the gateway that represents the SensorTag in the **Device to View** dropdown.</span></span>
- <span data-ttu-id="5df80-173">La télémétrie du dispositif SensorTag s’affiche sur le tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="5df80-173">The telemetry from the SensorTag device displays on the dashboard.</span></span>

![Afficher la télémétrie des dispositifs SensorTag][img-telemetry-display]

> [!WARNING]
> <span data-ttu-id="5df80-175">Si vous quittez la solution de surveillance à distance en cours d’exécution dans votre compte Azure, vous êtes facturé en fonction du temps d’exécution.</span><span class="sxs-lookup"><span data-stu-id="5df80-175">If you leave the remote monitoring solution running in your Azure account, you are billed for the time it runs.</span></span> <span data-ttu-id="5df80-176">Pour plus d’informations sur la manière de réduire votre consommation pendant l’exécution de la solution de surveillance à distance, consultez [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config] (Configuration des solutions préconfigurées Azure IoT Suite à des fins de démonstration).</span><span class="sxs-lookup"><span data-stu-id="5df80-176">For more information about reducing consumption while the remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span> <span data-ttu-id="5df80-177">Supprimez la solution préconfigurée de votre compte Azure lorsque vous avez fini de l’utiliser.</span><span class="sxs-lookup"><span data-stu-id="5df80-177">Delete the preconfigured solution from your Azure account when you have finished using it.</span></span>


## <a name="next-steps"></a><span data-ttu-id="5df80-178">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5df80-178">Next steps</span></span>

<span data-ttu-id="5df80-179">Visitez le [Centre de développement Azure IoT](https://azure.microsoft.com/develop/iot/) pour d’autres exemples et de la documentation complémentaire sur Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="5df80-179">Visit the [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>

[img-telemetry]: ./media/iot-suite-gateway-kit-get-started-sensortag/appoutput.png


[img-telemetry-display]: ./media/iot-suite-gateway-kit-get-started-sensortag/telemetry.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
[lnk-vi-tutorial]: http://www.tutorialspoint.com/unix/unix-vi-editor.htm
[lnk-sensortag]: http://www.ti.com/ww/en/wireless_connectivity/sensortag/
[lnk-gateway-concepts]: https://docs.microsoft.com/azure/iot-hub/iot-hub-linux-iot-edge-get-started