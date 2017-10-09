---
title: "aaaConnect un tooAzure passerelle IoT Suite à l’aide d’un NUC Intel | Documents Microsoft"
description: "Utilisez hello Microsoft IoT Commercial passerelle Kit et hello distant préconfigurée solution d’analyse. Utilisez hello Azure IoT bord passerelle tooenable un SensorTag périphérique tooconnect toohello solution de surveillance à distance, envoyer cloud toohello de télémétrie et répondre toomethods appelée à partir du tableau de bord de solution hello."
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
ms.openlocfilehash: 6f98ee3c1e2311a8644da9d72d40e671e7cbcf00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-azure-iot-edge-gateway-toohello-remote-monitoring-preconfigured-solution-and-send-telemetry-from-a-sensortag"></a><span data-ttu-id="66ae5-104">Se connecter à votre toohello de passerelle Azure IoT bord solution préconfigurée de surveillance à distance et d’envoyer la télémétrie à partir d’un SensorTag</span><span class="sxs-lookup"><span data-stu-id="66ae5-104">Connect your Azure IoT Edge gateway toohello remote monitoring preconfigured solution and send telemetry from a SensorTag</span></span>

[!INCLUDE [iot-suite-gateway-kit-selector](../../includes/iot-suite-gateway-kit-selector.md)]

<span data-ttu-id="66ae5-105">Ce didacticiel vous montre comment toouse Azure IoT toosend température et humidité données à partir de la surveillance à distance de SensorTag périphérique toohello solution préconfigurée.</span><span class="sxs-lookup"><span data-stu-id="66ae5-105">This tutorial shows you how toouse Azure IoT Edge toosend temperature and humidity data from SensorTag device toohello remote monitoring preconfigured solution.</span></span> <span data-ttu-id="66ae5-106">Hello SensorTag connecte la passerelle d’Intel NUC toohello à l’aide de Bluetooth.</span><span class="sxs-lookup"><span data-stu-id="66ae5-106">hello SensorTag connects toohello Intel NUC gateway using Bluetooth.</span></span> <span data-ttu-id="66ae5-107">didacticiel de Hello utilise :</span><span class="sxs-lookup"><span data-stu-id="66ae5-107">hello tutorial uses:</span></span>

- <span data-ttu-id="66ae5-108">Un exemple de passerelle du tooimplement IoT bord Azure.</span><span class="sxs-lookup"><span data-stu-id="66ae5-108">Azure IoT Edge tooimplement a sample gateway.</span></span>
- <span data-ttu-id="66ae5-109">la surveillance à distance Hello IoT Suite, solution préconfigurée comme hello nuage back-end.</span><span class="sxs-lookup"><span data-stu-id="66ae5-109">hello IoT Suite remote monitoring preconfigured solution as hello cloud-based back end.</span></span>

## <a name="overview"></a><span data-ttu-id="66ae5-110">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="66ae5-110">Overview</span></span>

<span data-ttu-id="66ae5-111">Dans ce didacticiel, vous effectuez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="66ae5-111">In this tutorial, you complete hello following steps:</span></span>

- <span data-ttu-id="66ae5-112">Déployer une instance de hello distant tooyour solution préconfigurée analyse abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="66ae5-112">Deploy an instance of hello remote monitoring preconfigured solution tooyour Azure subscription.</span></span> <span data-ttu-id="66ae5-113">Cette étape déploie et configure automatiquement plusieurs services Azure.</span><span class="sxs-lookup"><span data-stu-id="66ae5-113">This step automatically deploys and configures multiple Azure services.</span></span>
- <span data-ttu-id="66ae5-114">Configurer votre toocommunicate de périphérique de passerelle Intel NUC avec votre ordinateur et de la solution d’analyse à distance hello.</span><span class="sxs-lookup"><span data-stu-id="66ae5-114">Set up your Intel NUC gateway device toocommunicate with your computer and hello remote monitoring solution.</span></span>
- <span data-ttu-id="66ae5-115">Configurer vos données de télémétrie Intel NUC passerelle tooreceive à partir d’un appareil SensorTag et envoyez-le toohello du tableau de bord de surveillance à distance.</span><span class="sxs-lookup"><span data-stu-id="66ae5-115">Set up your Intel NUC gateway tooreceive telemetry from a SensorTag device and send it toohello remote monitoring dashboard.</span></span>

[!INCLUDE [iot-suite-gateway-kit-prerequisites](../../includes/iot-suite-gateway-kit-prerequisites.md)]

<span data-ttu-id="66ae5-116">[Texas Instruments BLE SensorTag][lnk-sensortag].</span><span class="sxs-lookup"><span data-stu-id="66ae5-116">[Texas Instruments BLE SensorTag][lnk-sensortag].</span></span> <span data-ttu-id="66ae5-117">Ce didacticiel récupère les données de télémétrie par Bluetooth à partir de l’appareil de SensorTag hello.</span><span class="sxs-lookup"><span data-stu-id="66ae5-117">This tutorial retrieves telemetry data over Bluetooth from hello SensorTag device.</span></span>

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="66ae5-118">Bonjour dispositions de solution de surveillance à distance à un ensemble de services Azure dans votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="66ae5-118">hello remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="66ae5-119">déploiement de Hello reflète une architecture d’entreprise réel.</span><span class="sxs-lookup"><span data-stu-id="66ae5-119">hello deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="66ae5-120">frais de la consommation Azure inutile tooavoid, supprimer votre instance de la solution de hello préconfiguré dans azureiotsuite.com lorsque vous avez terminé avec lui.</span><span class="sxs-lookup"><span data-stu-id="66ae5-120">tooavoid unnecessary Azure consumption charges, delete your instance of hello preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="66ae5-121">Si vous avez besoin de hello solution préconfigurée à nouveau, vous pouvez le recréer facilement.</span><span class="sxs-lookup"><span data-stu-id="66ae5-121">If you need hello preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="66ae5-122">Pour plus d’informations sur la réduction de la consommation lors hello s’exécute la solution de surveillance à distance, consultez [configuration Azure IoT Suite préconfiguré des solutions à des fins de démonstration][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="66ae5-122">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-gateway-kit-view-solution](../../includes/iot-suite-gateway-kit-view-solution.md)]

[!INCLUDE [iot-suite-gateway-kit-prepare-nuc-connectivity](../../includes/iot-suite-gateway-kit-prepare-nuc-connectivity.md)]

## <a name="configure-bluetooth-connectivity"></a><span data-ttu-id="66ae5-123">Configurer la connectivité Bluetooth</span><span class="sxs-lookup"><span data-stu-id="66ae5-123">Configure Bluetooth connectivity</span></span>

<span data-ttu-id="66ae5-124">Configurer le Bluetooth sur hello Intel NUC tooenable hello SensorTag périphérique tooconnect et envoyer la télémétrie.</span><span class="sxs-lookup"><span data-stu-id="66ae5-124">Configure Bluetooth on hello Intel NUC tooenable hello SensorTag device tooconnect and send telemetry.</span></span>

### <a name="find-hello-mac-address-of-hello-sensortag"></a><span data-ttu-id="66ae5-125">Rechercher l’adresse MAC de hello Hello SensorTag</span><span class="sxs-lookup"><span data-stu-id="66ae5-125">Find hello MAC address of hello SensorTag</span></span>

1. <span data-ttu-id="66ae5-126">Dans l’interface hello sur hello Intel NUC, exécutez hello après commande toounblock hello Bluetooth service :</span><span class="sxs-lookup"><span data-stu-id="66ae5-126">In hello shell on hello Intel NUC, run hello following command toounblock hello Bluetooth service:</span></span>

    ```bash
    sudo rfkill unblock bluetooth
    ```

1. <span data-ttu-id="66ae5-127">Suivante d’exécution hello commandes service Bluetooth hello Intel NUC toostart hello et entrez l’interpréteur de commandes hello Bluetooth :</span><span class="sxs-lookup"><span data-stu-id="66ae5-127">Run hello following commands toostart hello Bluetooth service on hello Intel NUC and enter hello Bluetooth shell:</span></span>

    ```bash
    sudo systemctl start bluetooth
    bluetoothctl
    ```

1. <span data-ttu-id="66ae5-128">Exécutez hello suivant toopower de commande sur le contrôleur de hello Bluetooth :</span><span class="sxs-lookup"><span data-stu-id="66ae5-128">Run hello following command toopower on hello Bluetooth controller:</span></span>

    ```bash
    power on
    ```

    <span data-ttu-id="66ae5-129">Lorsque le contrôleur de hello est activé, vous voyez un message **réussi de la modification de la puissance sur**.</span><span class="sxs-lookup"><span data-stu-id="66ae5-129">When hello controller is on, you see a message **Changing power on succeeded**.</span></span>

1. <span data-ttu-id="66ae5-130">Exécutez hello suivant tooscan de commande pour les périphériques Bluetooth à proximité :</span><span class="sxs-lookup"><span data-stu-id="66ae5-130">Run hello following command tooscan for nearby Bluetooth devices:</span></span>

    ```bash
    scan on
    ```

1. <span data-ttu-id="66ae5-131">Appuyez sur hello bouton d’alimentation sur hello SensorTag toomake il détectable.</span><span class="sxs-lookup"><span data-stu-id="66ae5-131">Press hello power button on hello SensorTag toomake it discoverable.</span></span> <span data-ttu-id="66ae5-132">DEL de Hello vert clignote.</span><span class="sxs-lookup"><span data-stu-id="66ae5-132">hello green LED flashes.</span></span>

1. <span data-ttu-id="66ae5-133">Lorsque vous voyez un message dans le shell hello ce contrôleur hello a découvert hello SensorTag, prenez note de l’adresse MAC du périphérique de hello de hello.</span><span class="sxs-lookup"><span data-stu-id="66ae5-133">When you see a message in hello shell that hello controller has discovered hello SensorTag, make a note of hello MAC address of hello device.</span></span> <span data-ttu-id="66ae5-134">adresse MAC de Hello ressemble à **A0:E6:F8:B5:F6:00**.</span><span class="sxs-lookup"><span data-stu-id="66ae5-134">hello MAC address looks like **A0:E6:F8:B5:F6:00**.</span></span> <span data-ttu-id="66ae5-135">Vous devez adresse MAC de hello plus loin dans le didacticiel de hello lorsque vous configurez la passerelle de hello.</span><span class="sxs-lookup"><span data-stu-id="66ae5-135">You need hello MAC address later in hello tutorial when you configure hello gateway.</span></span>

1. <span data-ttu-id="66ae5-136">Exécutez hello suivant tooturn commande Désactiver Bluetooth analyse :</span><span class="sxs-lookup"><span data-stu-id="66ae5-136">Run hello following command tooturn off Bluetooth scanning:</span></span>

    ```bash
    scan off
    ```

1. <span data-ttu-id="66ae5-137">Exécutez hello suivant tooverify de commande que vous pouvez vous connecter à toohello SensorTag appareil :</span><span class="sxs-lookup"><span data-stu-id="66ae5-137">Run hello following command tooverify that you can connect toohello SensorTag device:</span></span>

    ```bash
    connect <SensorTag MAC address>
    ```

    <span data-ttu-id="66ae5-138">Si vous vous connectez avec succès, interpréteur de commandes hello affiche le message de type hello **connexion réussie** et imprime les informations sur l’appareil de SensorTag hello.</span><span class="sxs-lookup"><span data-stu-id="66ae5-138">If you connect successfully, hello shell shows hello message **Connection successful** and prints information about hello SensorTag device.</span></span> <span data-ttu-id="66ae5-139">Si vous ne pouvez pas vous connecter, vérifiez hello que sensortag est toujours sous tension.</span><span class="sxs-lookup"><span data-stu-id="66ae5-139">If you cannot connect, check hello SensorTag is still powered on.</span></span>

1. <span data-ttu-id="66ae5-140">Vous pouvez maintenant déconnecter hello SensorTag et quitter le shell de Bluetooth hello en hello suivant les commandes en cours d’exécution :</span><span class="sxs-lookup"><span data-stu-id="66ae5-140">You can now disconnect from hello SensorTag and exit hello Bluetooth shell by running hello following commands:</span></span>

    ```bash
    disconnect
    exit
    ```

[!INCLUDE [iot-suite-gateway-kit-prepare-nuc-software](../../includes/iot-suite-gateway-kit-prepare-nuc-software.md)]

## <a name="build-hello-custom-iot-edge-module"></a><span data-ttu-id="66ae5-141">Génération du module de IoT bord hello personnalisé</span><span class="sxs-lookup"><span data-stu-id="66ae5-141">Build hello custom IoT Edge module</span></span>

<span data-ttu-id="66ae5-142">Vous pouvez à présent générer hello IoT bord module personnalisé qui permet de hello passerelle toosend messages toohello distant solution d’analyse.</span><span class="sxs-lookup"><span data-stu-id="66ae5-142">You can now build hello custom IoT Edge module that enables hello gateway toosend messages toohello remote monitoring solution.</span></span> <span data-ttu-id="66ae5-143">Pour plus d’informations sur la configuration d’une passerelle et des modules IoT Edge, voir [Concepts relatifs à Azure IoT Edge][lnk-gateway-concepts].</span><span class="sxs-lookup"><span data-stu-id="66ae5-143">For more information about configuring a gateway and IoT Edge modules, see [Azure IoT Edge concepts][lnk-gateway-concepts].</span></span>

<span data-ttu-id="66ae5-144">Télécharger le code de source de hello pour les modules de IoT bord hello personnalisés à partir de GitHub à l’aide de hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="66ae5-144">Download hello source code for hello custom IoT Edge modules from GitHub using hello following commands:</span></span>

```bash
cd ~
git clone https://github.com/Azure-Samples/iot-remote-monitoring-c-intel-nuc-gateway-getting-started.git
```

<span data-ttu-id="66ae5-145">Génération du module IoT bord personnalisé de hello, à l’aide de hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="66ae5-145">Build hello custom IoT Edge module using hello following commands:</span></span>

```bash
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/basic
chmod u+x build.sh
sed -i -e 's/\r$//' build.sh
./build.sh
```

<span data-ttu-id="66ae5-146">script de compilation Hello place le module de IoT bord personnalisé hello libsensor2remotemonitoring.so dans le dossier de génération hello.</span><span class="sxs-lookup"><span data-stu-id="66ae5-146">hello build script places hello libsensor2remotemonitoring.so custom IoT Edge module in hello build folder.</span></span>

## <a name="configure-and-run-hello-iot-edge-gateway"></a><span data-ttu-id="66ae5-147">Configurer et exécuter hello IoT passerelle</span><span class="sxs-lookup"><span data-stu-id="66ae5-147">Configure and run hello IoT Edge gateway</span></span>

<span data-ttu-id="66ae5-148">Vous pouvez désormais configurer hello télémétrie de toosend passerelle IoT bord à partir de votre tooyour de périphérique SensorTag du tableau de bord de surveillance à distance.</span><span class="sxs-lookup"><span data-stu-id="66ae5-148">You can now configure hello IoT Edge gateway toosend telemetry from your SensorTag device tooyour remote monitoring dashboard.</span></span> <span data-ttu-id="66ae5-149">Pour plus d’informations sur la configuration d’une passerelle et des modules IoT Edge, voir [Concepts relatifs à Azure IoT Edge][lnk-gateway-concepts].</span><span class="sxs-lookup"><span data-stu-id="66ae5-149">For more information about configuring a gateway and IoT Edge modules, see [Azure IoT Edge concepts][lnk-gateway-concepts].</span></span>

> [!TIP]
> <span data-ttu-id="66ae5-150">Dans ce didacticiel, vous utilisez standard de hello `vi` éditeur de texte sur hello NUC d’Intel.</span><span class="sxs-lookup"><span data-stu-id="66ae5-150">In this tutorial, you use hello standard `vi` text editor on hello Intel NUC.</span></span> <span data-ttu-id="66ae5-151">Si vous n’avez pas utilisé `vi` auparavant, vous devez effectuer un didacticiel d’introduction, telles que [Unix - hello vi didacticiel de l’éditeur] [ lnk-vi-tutorial] toofamiliarize vous-même avec cet éditeur.</span><span class="sxs-lookup"><span data-stu-id="66ae5-151">If you have not used `vi` before, you should complete an introductory tutorial, such as [Unix - hello vi Editor Tutorial][lnk-vi-tutorial] toofamiliarize yourself with this editor.</span></span> <span data-ttu-id="66ae5-152">Vous pouvez également installer hello plus conviviaux [nano](https://www.nano-editor.org/) éditeur à l’aide de la commande hello `smart install nano -y`.</span><span class="sxs-lookup"><span data-stu-id="66ae5-152">Alternatively, you can install hello more user-friendly [nano](https://www.nano-editor.org/) editor using hello command `smart install nano -y`.</span></span>

<span data-ttu-id="66ae5-153">Fichier de configuration d’exemple hello ouvrir Bonjour **vi** éditeur à l’aide de hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="66ae5-153">Open hello sample configuration file in hello **vi** editor using hello following command:</span></span>

```bash
vi ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/basic/remote_monitoring.json
```

<span data-ttu-id="66ae5-154">Recherchez hello lignes dans la configuration de hello pour le module de IoTHub hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="66ae5-154">Locate hello following lines in hello configuration for hello IoTHub module:</span></span>

```json
"args": {
  "IoTHubName": "<<Azure IoT Hub Name>>",
  "IoTHubSuffix": "<<Azure IoT Hub Suffix>>",
  "Transport": "http"
}
```

<span data-ttu-id="66ae5-155">Remplacez l’espace réservé de hello valeurs hello informations IoT Hub vous avez créé et enregistré à hello Démarrer de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="66ae5-155">Replace hello placeholder values with hello IoT Hub information you created and saved at hello start of this tutorial.</span></span> <span data-ttu-id="66ae5-156">valeur Hello pour IoTHubName ressemble à **yourrmsolution37e08**, et la valeur hello pour IoTSuffix est généralement **azure-devices.net**.</span><span class="sxs-lookup"><span data-stu-id="66ae5-156">hello value for IoTHubName looks like **yourrmsolution37e08**, and hello value for IoTSuffix is typically **azure-devices.net**.</span></span>

<span data-ttu-id="66ae5-157">Recherchez hello lignes dans la configuration de hello pour le module de mappage hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="66ae5-157">Locate hello following lines in hello configuration for hello mapping module:</span></span>

```json
args": [
  {
    "macAddress": "<<AA:BB:CC:DD:EE:FF>>",
    "deviceId": "<<Azure IoT Hub Device ID>>",
    "deviceKey": "<<Azure IoT Hub Device Key>>"
  }
]
```

<span data-ttu-id="66ae5-158">Remplacez hello **macAddress** espace réservé par hello adresse MAC de votre SensorTag que vous avez notée précédemment.</span><span class="sxs-lookup"><span data-stu-id="66ae5-158">Replace hello **macAddress** placeholder with hello MAC address of your SensorTag you noted previously.</span></span> <span data-ttu-id="66ae5-159">Remplacez hello **deviceID** et **deviceKey** des espaces réservés avec les identificateurs hello et des clés pour les appareils hello deux créé précédemment dans la solution d’analyse à distance hello.</span><span class="sxs-lookup"><span data-stu-id="66ae5-159">Replace hello **deviceID** and **deviceKey** placeholders with hello IDs and keys for hello two devices you created in hello remote monitoring solution previously.</span></span>

<span data-ttu-id="66ae5-160">Recherchez hello lignes dans la configuration de hello pour le module de SensorTag hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="66ae5-160">Locate hello following lines in hello configuration for hello SensorTag module:</span></span>

```json
"args": {
  "controller_index": 0,
  "device_mac_address": "<<AA:BB:CC:DD:EE:FF>>",
  ...
}
```

<span data-ttu-id="66ae5-161">Remplacez hello **périphérique\_mac\_adresse** espace réservé par hello adresse MAC de votre SensorTag que vous avez notée précédemment.</span><span class="sxs-lookup"><span data-stu-id="66ae5-161">Replace hello **device\_mac\_address** placeholder  with hello MAC address of your SensorTag you noted previously.</span></span>

<span data-ttu-id="66ae5-162">Enregistrez vos modifications.</span><span class="sxs-lookup"><span data-stu-id="66ae5-162">Save your changes.</span></span>

<span data-ttu-id="66ae5-163">Vous pouvez maintenant exécuter passerelle hello hello suivant les commandes à l’aide de :</span><span class="sxs-lookup"><span data-stu-id="66ae5-163">You can now run hello gateway using hello following commands:</span></span>

```bash
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/basic
/usr/share/azureiotgatewaysdk/samples/ble_gateway/ble_gateway remote_monitoring.json
```

<span data-ttu-id="66ae5-164">Hello IoT passerelle démarre sur hello Intel NUC et envoie des données de télémétrie à partir de hello SensorTag toohello une solution d’analyse à distance :</span><span class="sxs-lookup"><span data-stu-id="66ae5-164">hello IoT Edge gateway starts on hello Intel NUC and sends telemetry from hello SensorTag toohello remote monitoring solution:</span></span>

![Passerelle IoT envoie des données de télémétrie à partir de hello SensorTag][img-telemetry]

<span data-ttu-id="66ae5-166">Appuyez sur **Ctrl-C** programme de hello tooexit à tout moment.</span><span class="sxs-lookup"><span data-stu-id="66ae5-166">Press **Ctrl-C** tooexit hello program at any time.</span></span>

## <a name="view-hello-telemetry"></a><span data-ttu-id="66ae5-167">Télémétrie des consultations de hello</span><span class="sxs-lookup"><span data-stu-id="66ae5-167">View hello telemetry</span></span>

<span data-ttu-id="66ae5-168">passerelle de Hello envoie maintenant télémétrie à partir de hello SensorTag périphérique toohello distante solution d’analyse.</span><span class="sxs-lookup"><span data-stu-id="66ae5-168">hello gateway is now sending telemetry from hello SensorTag device toohello remote monitoring solution.</span></span> <span data-ttu-id="66ae5-169">Vous pouvez afficher les données de télémétrie hello sur le tableau de bord de solution hello.</span><span class="sxs-lookup"><span data-stu-id="66ae5-169">You can view hello telemetry on hello solution dashboard.</span></span> <span data-ttu-id="66ae5-170">Vous pouvez également envoyer des périphériques de SensorTag tooyour commandes via la passerelle de hello à partir du tableau de bord de solution hello.</span><span class="sxs-lookup"><span data-stu-id="66ae5-170">You can also send commands tooyour SensorTag device through hello gateway from hello solution dashboard.</span></span>

- <span data-ttu-id="66ae5-171">Accédez à tableau de bord toohello solution.</span><span class="sxs-lookup"><span data-stu-id="66ae5-171">Navigate toohello solution dashboard.</span></span>
- <span data-ttu-id="66ae5-172">APPAREIL hello sélectionnez vous avez configuré dans la passerelle hello représentant hello SensorTag Bonjour **tooView de périphérique** liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="66ae5-172">Select hello device you configured in hello gateway that represents hello SensorTag in hello **Device tooView** dropdown.</span></span>
- <span data-ttu-id="66ae5-173">télémétrie Hello à partir de l’appareil de SensorTag hello s’affiche sur le tableau de bord hello.</span><span class="sxs-lookup"><span data-stu-id="66ae5-173">hello telemetry from hello SensorTag device displays on hello dashboard.</span></span>

![Afficher les données de télémétrie des appareils de SensorTag hello][img-telemetry-display]

> [!WARNING]
> <span data-ttu-id="66ae5-175">Si vous laissez hello solution en cours d’exécution dans votre compte Azure de surveillance à distance, vous êtes facturé pour hello exécution.</span><span class="sxs-lookup"><span data-stu-id="66ae5-175">If you leave hello remote monitoring solution running in your Azure account, you are billed for hello time it runs.</span></span> <span data-ttu-id="66ae5-176">Pour plus d’informations sur la réduction de la consommation lors hello s’exécute la solution de surveillance à distance, consultez [configuration Azure IoT Suite préconfiguré des solutions à des fins de démonstration][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="66ae5-176">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span> <span data-ttu-id="66ae5-177">Supprimer la solution de hello préconfiguré à partir de votre compte Azure lorsque vous avez terminé.</span><span class="sxs-lookup"><span data-stu-id="66ae5-177">Delete hello preconfigured solution from your Azure account when you have finished using it.</span></span>


## <a name="next-steps"></a><span data-ttu-id="66ae5-178">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="66ae5-178">Next steps</span></span>

<span data-ttu-id="66ae5-179">Visitez hello [centre de développement Azure IoT](https://azure.microsoft.com/develop/iot/) pour plus d’exemples et documentation sur Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="66ae5-179">Visit hello [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>

[img-telemetry]: ./media/iot-suite-gateway-kit-get-started-sensortag/appoutput.png


[img-telemetry-display]: ./media/iot-suite-gateway-kit-get-started-sensortag/telemetry.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
[lnk-vi-tutorial]: http://www.tutorialspoint.com/unix/unix-vi-editor.htm
[lnk-sensortag]: http://www.ti.com/ww/en/wireless_connectivity/sensortag/
[lnk-gateway-concepts]: https://docs.microsoft.com/azure/iot-hub/iot-hub-linux-iot-edge-get-started