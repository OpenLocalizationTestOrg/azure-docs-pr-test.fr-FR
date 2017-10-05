---
title: "Connecter une passerelle à Azure IoT Suite à l’aide d’un Intel NUC | Documents Microsoft"
description: "Utilisez le kit de passerelle commerciale Microsoft IoT et la solution préconfigurée de surveillance à distance. Utilisez la passerelle Azure IoT Edge pour vous connecter à la solution de surveillance à distance, envoyer la télémétrie simulée dans le cloud et répondre aux méthodes appelées à partir du tableau de bord de la solution."
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
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: 9ed57d3c23e2adbd42c054f33c8ed46e3d6c9792
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="connect-your-azure-iot-edge-gateway-to-the-remote-monitoring-preconfigured-solution-and-send-simulated-telemetry"></a><span data-ttu-id="4169e-104">Connecter votre passerelle Azure IoT Edge à la solution préconfigurée de surveillance à distance et envoyer la télémétrie simulée</span><span class="sxs-lookup"><span data-stu-id="4169e-104">Connect your Azure IoT Edge gateway to the remote monitoring preconfigured solution and send simulated telemetry</span></span>

[!INCLUDE [iot-suite-gateway-kit-selector](../../includes/iot-suite-gateway-kit-selector.md)]

<span data-ttu-id="4169e-105">Ce didacticiel montre comment utiliser Azure IoT Edge pour simuler des données de température et d’humidité à envoyer à la solution préconfigurée de surveillance à distance.</span><span class="sxs-lookup"><span data-stu-id="4169e-105">This tutorial shows you how to use Azure IoT Edge to simulate temperature and humidity data to send to the remote monitoring preconfigured solution.</span></span> <span data-ttu-id="4169e-106">Le tutoriel utilise :</span><span class="sxs-lookup"><span data-stu-id="4169e-106">The tutorial uses:</span></span>

- <span data-ttu-id="4169e-107">Azure IoT Edge pour implémenter un exemple de passerelle.</span><span class="sxs-lookup"><span data-stu-id="4169e-107">Azure IoT Edge to implement a sample gateway.</span></span>
- <span data-ttu-id="4169e-108">la solution préconfigurée de surveillance à distance Azure IoT Suite comme serveur principal basé sur le cloud.</span><span class="sxs-lookup"><span data-stu-id="4169e-108">The IoT Suite remote monitoring preconfigured solution as the cloud-based back end.</span></span>

## <a name="overview"></a><span data-ttu-id="4169e-109">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="4169e-109">Overview</span></span>

<span data-ttu-id="4169e-110">Dans ce didacticiel, vous allez effectuer les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="4169e-110">In this tutorial, you complete the following steps:</span></span>

- <span data-ttu-id="4169e-111">Déployer une instance de la solution préconfigurée de surveillance à distance dans votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="4169e-111">Deploy an instance of the remote monitoring preconfigured solution to your Azure subscription.</span></span> <span data-ttu-id="4169e-112">Cette étape déploie et configure automatiquement plusieurs services Azure.</span><span class="sxs-lookup"><span data-stu-id="4169e-112">This step automatically deploys and configures multiple Azure services.</span></span>
- <span data-ttu-id="4169e-113">Configurez votre appareil de passerelle Intel NUC pour qu’il communique avec votre ordinateur et avec la solution de surveillance à distance.</span><span class="sxs-lookup"><span data-stu-id="4169e-113">Set up your Intel NUC gateway device to communicate with your computer and the remote monitoring solution.</span></span>
- <span data-ttu-id="4169e-114">Configurez la passerelle IoT Edge pour qu’elle envoie la télémétrie simulée que vous pouvez afficher sur le tableau de bord de la solution.</span><span class="sxs-lookup"><span data-stu-id="4169e-114">Configure the IoT Edge gateway to send simulated telemetry that you can view on the solution dashboard.</span></span>

[!INCLUDE [iot-suite-gateway-kit-prerequisites](../../includes/iot-suite-gateway-kit-prerequisites.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="4169e-115">La solution de surveillance à distance configure un ensemble de services Azure dans votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="4169e-115">The remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="4169e-116">Le déploiement reflète une architecture d’entreprise réelle.</span><span class="sxs-lookup"><span data-stu-id="4169e-116">The deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="4169e-117">Pour éviter des frais de consommation Azure inutiles, supprimez votre instance de la solution préconfigurée dans azureiotsuite.com quand vous ne l’utilisez plus.</span><span class="sxs-lookup"><span data-stu-id="4169e-117">To avoid unnecessary Azure consumption charges, delete your instance of the preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="4169e-118">Si vous avez à nouveau besoin de la solution préconfigurée, vous pouvez la recréer facilement.</span><span class="sxs-lookup"><span data-stu-id="4169e-118">If you need the preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="4169e-119">Pour plus d’informations sur la manière de réduire votre consommation pendant l’exécution de la solution de surveillance à distance, consultez [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config] (Configuration des solutions préconfigurées Azure IoT Suite à des fins de démonstration).</span><span class="sxs-lookup"><span data-stu-id="4169e-119">For more information about reducing consumption while the remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-gateway-kit-view-solution](../../includes/iot-suite-gateway-kit-view-solution.md)]

<span data-ttu-id="4169e-120">Répétez les étapes précédentes pour ajouter un deuxième appareil à l’aide d’un ID d’appareil tel que **device02**.</span><span class="sxs-lookup"><span data-stu-id="4169e-120">Repeat the previous steps to add a second device using a Device ID such as **device02**.</span></span> <span data-ttu-id="4169e-121">L’exemple envoie des données à partir de deux appareils simulés dans la passerelle à la solution de surveillance à distance.</span><span class="sxs-lookup"><span data-stu-id="4169e-121">The sample sends data from two simulated devices in the gateway to the remote monitoring solution.</span></span>

[!INCLUDE [iot-suite-gateway-kit-prepare-nuc-connectivity](../../includes/iot-suite-gateway-kit-prepare-nuc-connectivity.md)]

[!INCLUDE [iot-suite-gateway-kit-prepare-nuc-software](../../includes/iot-suite-gateway-kit-prepare-nuc-software.md)]

## <a name="build-the-custom-iot-edge-module"></a><span data-ttu-id="4169e-122">Créer le module IoT Edge personnalisé</span><span class="sxs-lookup"><span data-stu-id="4169e-122">Build the custom IoT Edge module</span></span>

<span data-ttu-id="4169e-123">Vous pouvez maintenant générer le module IoT personnalisé qui permet à la passerelle d’envoyer des messages à la solution de surveillance à distance.</span><span class="sxs-lookup"><span data-stu-id="4169e-123">You can now build the custom IoT Edge module that enables the gateway to send messages to the remote monitoring solution.</span></span> <span data-ttu-id="4169e-124">Pour plus d’informations sur la configuration d’une passerelle et des modules IoT Edge, voir [Concepts relatifs à Azure IoT Edge][lnk-gateway-concepts].</span><span class="sxs-lookup"><span data-stu-id="4169e-124">For more information about configuring a gateway and IoT Edge modules, see [Azure IoT Edge concepts][lnk-gateway-concepts].</span></span>

<span data-ttu-id="4169e-125">Téléchargez le code source pour les modules IoT Edge personnalisés à partir de GitHub à l’aide des commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="4169e-125">Download the source code for the custom IoT Edge modules from GitHub using the following commands:</span></span>

```bash
cd ~
git clone https://github.com/Azure-Samples/iot-remote-monitoring-c-intel-nuc-gateway-getting-started.git
```

<span data-ttu-id="4169e-126">Créez le module IoT Edge personnalisé à l’aide des commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="4169e-126">Build the custom IoT Edge module using the following commands:</span></span>

```bash
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/simulator
chmod u+x build.sh
sed -i -e 's/\r$//' build.sh
./build.sh
```

<span data-ttu-id="4169e-127">Le script de génération place le module IoT Edge personnalisé libsimulator.so dans le dossier de génération.</span><span class="sxs-lookup"><span data-stu-id="4169e-127">The build script places the libsimulator.so custom IoT Edge module in the build folder.</span></span>

## <a name="configure-and-run-the-iot-edge-gateway"></a><span data-ttu-id="4169e-128">Configurer et exécuter la passerelle IoT Edge</span><span class="sxs-lookup"><span data-stu-id="4169e-128">Configure and run the IoT Edge gateway</span></span>

<span data-ttu-id="4169e-129">Vous pouvez maintenant configurer la passerelle IoT Edge pour qu’elle envoie la télémétrie simulée au tableau de bord de la solution de surveillance à distance.</span><span class="sxs-lookup"><span data-stu-id="4169e-129">You can now configure the IoT Edge gateway to send simulated telemetry to your remote monitoring dashboard.</span></span> <span data-ttu-id="4169e-130">Pour plus d’informations sur la configuration d’une passerelle et des modules IoT Edge, consultez [Concepts Azure IoT Edge][lnk-gateway-concepts].</span><span class="sxs-lookup"><span data-stu-id="4169e-130">For more information about configuring a gateway and IoT Edge modules, see [Azure IoT Edge concepts][lnk-gateway-concepts].</span></span>

> [!TIP]
> <span data-ttu-id="4169e-131">Dans ce didacticiel, vous utilisez l’éditeur de texte `vi` standard sur l’Intel Nuc.</span><span class="sxs-lookup"><span data-stu-id="4169e-131">In this tutorial, you use the standard `vi` text editor on the Intel NUC.</span></span> <span data-ttu-id="4169e-132">Si vous n’avez pas utilisé `vi` précédemment, vous devez suivre un didacticiel d’introduction, tel que [Unix - Didacticiel de l’éditeur vi][lnk-vi-tutorial], pour vous familiariser avec cet éditeur.</span><span class="sxs-lookup"><span data-stu-id="4169e-132">If you have not used `vi` before, you should complete an introductory tutorial, such as [Unix - The vi Editor Tutorial][lnk-vi-tutorial] to familiarize yourself with this editor.</span></span> <span data-ttu-id="4169e-133">Vous pouvez également installer l’éditeur [nano](https://www.nano-editor.org/), plus convivial, à l’aide de la commande `smart install nano -y`.</span><span class="sxs-lookup"><span data-stu-id="4169e-133">Alternatively, you can install the more user-friendly [nano](https://www.nano-editor.org/) editor using the command `smart install nano -y`.</span></span>

<span data-ttu-id="4169e-134">Ouvrez l’exemple de fichier de configuration dans l’éditeur **vi** à l’aide de la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="4169e-134">Open the sample configuration file in the **vi** editor using the following command:</span></span>

```bash
vi ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/simulator/remote_monitoring.json
```

<span data-ttu-id="4169e-135">Recherchez les lignes suivantes dans la configuration pour le module IoTHub :</span><span class="sxs-lookup"><span data-stu-id="4169e-135">Locate the following lines in the configuration for the IoTHub module:</span></span>

```json
"args": {
  "IoTHubName": "<<Azure IoT Hub Name>>",
  "IoTHubSuffix": "<<Azure IoT Hub Suffix>>",
  "Transport": "http"
}
```

<span data-ttu-id="4169e-136">Remplacez les valeurs de l’espace réservé par les informations sur l’IoT Hub que vous avez créées et enregistrées au début de ce tutoriel.</span><span class="sxs-lookup"><span data-stu-id="4169e-136">Replace the placeholder values with the IoT Hub information you created and saved at the start of this tutorial.</span></span> <span data-ttu-id="4169e-137">La valeur de IoTHubName ressemble à **yourrmsolution37e08** et la valeur de IoTSuffix est généralement **azure-devices.net**.</span><span class="sxs-lookup"><span data-stu-id="4169e-137">The value for IoTHubName looks like **yourrmsolution37e08**, and the value for IoTSuffix is typically **azure-devices.net**.</span></span>

<span data-ttu-id="4169e-138">Recherchez les lignes suivantes dans la configuration du module de mappage :</span><span class="sxs-lookup"><span data-stu-id="4169e-138">Locate the following lines in the configuration for the mapping module:</span></span>

```json
args": [
  {
    "macAddress": "AA:BB:CC:DD:EE:FF",
    "deviceId": "<<Azure IoT Hub Device ID>>",
    "deviceKey": "<<Azure IoT Hub Device Key>>"
  },
  {
    "macAddress": "AA:BB:CC:DD:EE:FF",
    "deviceId": "<<Azure IoT Hub Device ID>>",
    "deviceKey": "<<Azure IoT Hub Device Key>>"
  }
]
```

<span data-ttu-id="4169e-139">Remplacez les espaces réservés **deviceID** et **deviceKey** par les ID et les clés des deux appareils que vous avez créés précédemment dans la solution de surveillance à distance.</span><span class="sxs-lookup"><span data-stu-id="4169e-139">Replace the **deviceID** and **deviceKey** placeholders with the IDs and keys for the two devices you created in the remote monitoring solution previously.</span></span>

<span data-ttu-id="4169e-140">Enregistrez vos modifications.</span><span class="sxs-lookup"><span data-stu-id="4169e-140">Save your changes.</span></span>

<span data-ttu-id="4169e-141">Vous pouvez maintenant exécuter la passerelle IoT Edge en utilisant les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="4169e-141">You can now run the IoT Edge gateway using the following commands:</span></span>

```bash
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/simulator
/usr/share/azureiotgatewaysdk/samples/simulated_device_cloud_upload/simulated_device_cloud_upload remote_monitoring.json
```

<span data-ttu-id="4169e-142">La passerelle démarre sur l’appareil Intel NUC et envoie la télémétrie simulée à la solution de surveillance à distance :</span><span class="sxs-lookup"><span data-stu-id="4169e-142">The gateway starts on the Intel NUC and sends simulated telemetry to the remote monitoring solution:</span></span>

![La passerelle IoT Edge génère la télémétrie simulée][img-simulated telemetry]

<span data-ttu-id="4169e-144">Appuyez sur **Ctrl-C** pour quitter le programme à tout moment.</span><span class="sxs-lookup"><span data-stu-id="4169e-144">Press **Ctrl-C** to exit the program at any time.</span></span>

## <a name="view-the-telemetry"></a><span data-ttu-id="4169e-145">Afficher les données de télémétrie</span><span class="sxs-lookup"><span data-stu-id="4169e-145">View the telemetry</span></span>

<span data-ttu-id="4169e-146">La passerelle IoT Edge envoie à présent la télémétrie simulée à la solution de surveillance à distance.</span><span class="sxs-lookup"><span data-stu-id="4169e-146">The IoT Edge gateway is now sending simulated telemetry to the remote monitoring solution.</span></span> <span data-ttu-id="4169e-147">Vous pouvez afficher les données de télémétrie sur le tableau de bord de la solution.</span><span class="sxs-lookup"><span data-stu-id="4169e-147">You can view the telemetry on the solution dashboard.</span></span>

- <span data-ttu-id="4169e-148">Accédez au tableau de bord de la solution.</span><span class="sxs-lookup"><span data-stu-id="4169e-148">Navigate to the solution dashboard.</span></span>
- <span data-ttu-id="4169e-149">Sélectionnez un des deux appareils que vous avez configurés dans la passerelle dans la liste déroulante **Appareil à afficher**.</span><span class="sxs-lookup"><span data-stu-id="4169e-149">Select one of the two devices you configured in the gateway in the **Device to View** dropdown.</span></span>
- <span data-ttu-id="4169e-150">Les données de télémétrie des appareils de passerelle s’affichent sur le tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="4169e-150">The telemetry from the gateway devices displays on the dashboard.</span></span>

![Afficher les données de télémétrie depuis les appareils de passerelle][img-telemetry-display]

> [!WARNING]
> <span data-ttu-id="4169e-152">Si vous quittez la solution de surveillance à distance en cours d’exécution dans votre compte Azure, vous êtes facturé en fonction du temps d’exécution.</span><span class="sxs-lookup"><span data-stu-id="4169e-152">If you leave the remote monitoring solution running in your Azure account, you are billed for the time it runs.</span></span> <span data-ttu-id="4169e-153">Pour plus d’informations sur la manière de réduire votre consommation pendant l’exécution de la solution de surveillance à distance, consultez [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config] (Configuration des solutions préconfigurées Azure IoT Suite à des fins de démonstration).</span><span class="sxs-lookup"><span data-stu-id="4169e-153">For more information about reducing consumption while the remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span> <span data-ttu-id="4169e-154">Supprimez la solution préconfigurée de votre compte Azure lorsque vous avez fini de l’utiliser.</span><span class="sxs-lookup"><span data-stu-id="4169e-154">Delete the preconfigured solution from your Azure account when you have finished using it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4169e-155">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4169e-155">Next steps</span></span>

<span data-ttu-id="4169e-156">Visitez le [Centre de développement Azure IoT](https://azure.microsoft.com/develop/iot/) pour d’autres exemples et de la documentation complémentaire sur Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="4169e-156">Visit the [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>

[img-simulated telemetry]: ./media/iot-suite-gateway-kit-get-started-simulator/appoutput.png

[img-telemetry-display]: ./media/iot-suite-gateway-kit-get-started-simulator/telemetry.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md

[lnk-vi-tutorial]: http://www.tutorialspoint.com/unix/unix-vi-editor.htm
[lnk-gateway-concepts]: https://docs.microsoft.com/azure/iot-hub/iot-hub-linux-iot-edge-get-started