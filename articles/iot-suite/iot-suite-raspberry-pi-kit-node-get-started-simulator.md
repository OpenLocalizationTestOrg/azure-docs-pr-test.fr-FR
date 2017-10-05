---
title: "Connexion d’un Raspberry Pi à Azure IoT Suite à l’aide de Node.js avec la télémétrie simulée | Microsoft Docs"
description: "Utilisez le Kit de démarrage Microsoft Azure IoT pour le Raspberry Pi 3 et IoT Azure Suite. Utiliser C pour connecter votre Raspberry Pi à la solution de surveillance à distance, envoyer la télémétrie simulée dans le cloud et répondre aux méthodes appelées à partir du tableau de bord de la solution."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-suite
ms.devlang: node.js
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/26/2017
ms.author: dobett
ms.openlocfilehash: 43fbfe2f2c5fb86e496c4419f9565365cf89830a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="connect-your-raspberry-pi-3-to-the-remote-monitoring-solution-and-send-simulated-telemetry-using-nodejs"></a><span data-ttu-id="6e1ed-104">Connecter votre Raspberry Pi 3 à la solution de surveillance à distance et envoyer la télémétrie simulée à l’aide de Node.js</span><span class="sxs-lookup"><span data-stu-id="6e1ed-104">Connect your Raspberry Pi 3 to the remote monitoring solution and send simulated telemetry using Node.js</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

<span data-ttu-id="6e1ed-105">Ce tutoriel vous montre comment utiliser le Raspberry Pi 3 pour simuler des données de température et d’humidité à envoyer dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="6e1ed-105">This tutorial shows you how to use the Raspberry Pi 3 to simulate temperature and humidity data to send to the cloud.</span></span> <span data-ttu-id="6e1ed-106">Le tutoriel utilise :</span><span class="sxs-lookup"><span data-stu-id="6e1ed-106">The tutorial uses:</span></span>

- <span data-ttu-id="6e1ed-107">Le système d’exploitation Raspbian, le langage de programmation Node.js et le Kit SDK Microsoft Azure IoT pour Node.js en vue d’implémenter un exemple d’appareil.</span><span class="sxs-lookup"><span data-stu-id="6e1ed-107">Raspbian OS, the Node.js programming language, and the Microsoft Azure IoT SDK for Node.js to implement a sample device.</span></span>
- <span data-ttu-id="6e1ed-108">la solution préconfigurée de surveillance à distance Azure IoT Suite comme serveur principal basé sur le cloud.</span><span class="sxs-lookup"><span data-stu-id="6e1ed-108">The IoT Suite remote monitoring preconfigured solution as the cloud-based back end.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-overview-simulator](../../includes/iot-suite-raspberry-pi-kit-overview-simulator.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="6e1ed-109">La solution de surveillance à distance configure un ensemble de services Azure dans votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="6e1ed-109">The remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="6e1ed-110">Le déploiement reflète une architecture d’entreprise réelle.</span><span class="sxs-lookup"><span data-stu-id="6e1ed-110">The deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="6e1ed-111">Pour éviter des frais de consommation Azure inutiles, supprimez votre instance de la solution préconfigurée dans azureiotsuite.com quand vous ne l’utilisez plus.</span><span class="sxs-lookup"><span data-stu-id="6e1ed-111">To avoid unnecessary Azure consumption charges, delete your instance of the preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="6e1ed-112">Si vous avez à nouveau besoin de la solution préconfigurée, vous pouvez la recréer facilement.</span><span class="sxs-lookup"><span data-stu-id="6e1ed-112">If you need the preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="6e1ed-113">Pour plus d’informations sur la manière de réduire votre consommation pendant l’exécution de la solution de surveillance à distance, consultez [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config] (Configuration des solutions préconfigurées Azure IoT Suite à des fins de démonstration).</span><span class="sxs-lookup"><span data-stu-id="6e1ed-113">For more information about reducing consumption while the remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi-simulator](../../includes/iot-suite-raspberry-pi-kit-prepare-pi-simulator.md)]

## <a name="download-and-configure-the-sample"></a><span data-ttu-id="6e1ed-114">Télécharger et configurer l’exemple</span><span class="sxs-lookup"><span data-stu-id="6e1ed-114">Download and configure the sample</span></span>

<span data-ttu-id="6e1ed-115">Vous pouvez à présent télécharger et configurer l’application cliente de surveillance à distance sur votre Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="6e1ed-115">You can now download and configure the remote monitoring client application on your Raspberry Pi.</span></span>

### <a name="install-nodejs"></a><span data-ttu-id="6e1ed-116">Installer Node.js</span><span class="sxs-lookup"><span data-stu-id="6e1ed-116">Install Node.js</span></span>

<span data-ttu-id="6e1ed-117">Si vous ne l’avez pas déjà fait, installez Node.js sur votre Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="6e1ed-117">If you haven't done so already, install Node.js on your Raspberry Pi.</span></span> <span data-ttu-id="6e1ed-118">Le kit de développement logiciel (SDK) IoT pour Node.js requiert la version 0.11.5 de Node.js ou une version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="6e1ed-118">The IoT SDK for Node.js requires version 0.11.5 of Node.js or later.</span></span> <span data-ttu-id="6e1ed-119">Les étapes suivantes vous montrent comment installer Node.js v6.10.2 sur votre Raspberry Pi :</span><span class="sxs-lookup"><span data-stu-id="6e1ed-119">The following steps show you how to install Node.js v6.10.2 on your Raspberry Pi:</span></span>

1. <span data-ttu-id="6e1ed-120">Pour mettre à jour votre Raspberry Pi, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="6e1ed-120">Use the following command to update your Raspberry Pi:</span></span>

    ```sh
    sudo apt-get update
    ```

1. <span data-ttu-id="6e1ed-121">Pour télécharger les fichiers binaires Node.js sur votre Raspberry Pi, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="6e1ed-121">Use the following command to download the Node.js binaries to your Raspberry Pi:</span></span>

    ```sh
    wget https://nodejs.org/dist/v6.10.2/node-v6.10.2-linux-armv7l.tar.gz
    ```

1. <span data-ttu-id="6e1ed-122">Pour installer les binaires, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="6e1ed-122">Use the following command to install the binaries:</span></span>

    ```sh
    sudo tar -C /usr/local --strip-components 1 -xzf node-v6.10.2-linux-armv7l.tar.gz
    ```

1. <span data-ttu-id="6e1ed-123">Pour vérifier que Node.js v6.10.2 a été installé avec succès, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="6e1ed-123">Use the following command to verify you have installed Node.js v6.10.2 successfully:</span></span>

    ```sh
    node --version
    ```

### <a name="clone-the-repositories"></a><span data-ttu-id="6e1ed-124">Cloner les dépôts</span><span class="sxs-lookup"><span data-stu-id="6e1ed-124">Clone the repositories</span></span>

<span data-ttu-id="6e1ed-125">Si vous ne l’avez pas déjà fait, clonez les dépôts requis en exécutant les commandes suivantes dans un terminal sur votre Pi :</span><span class="sxs-lookup"><span data-stu-id="6e1ed-125">If you haven't already done so, clone the required repositories by running the following commands in a terminal on your Pi:</span></span>

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-node-raspberrypi-getstartedkit.git
```

### <a name="update-the-device-connection-string"></a><span data-ttu-id="6e1ed-126">Mettre à jour la chaîne de connexion d’appareil</span><span class="sxs-lookup"><span data-stu-id="6e1ed-126">Update the device connection string</span></span>

<span data-ttu-id="6e1ed-127">Ouvrez l’exemple de fichier source dans l’éditeur **nano** à l’aide de la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="6e1ed-127">Open the sample source file in the **nano** editor using the following command:</span></span>

```sh
nano ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/simulator/remote_monitoring.js
```

<span data-ttu-id="6e1ed-128">Recherchez la ligne :</span><span class="sxs-lookup"><span data-stu-id="6e1ed-128">Find the line:</span></span>

```javascript
var connectionString = 'HostName=[Your IoT hub name].azure-devices.net;DeviceId=[Your device id];SharedAccessKey=[Your device key]';
```

<span data-ttu-id="6e1ed-129">Remplacez les valeurs dans l’espace réservé par les informations sur l’appareil et l’IoT Hub que vous avez créées et enregistrées au début de ce tutoriel.</span><span class="sxs-lookup"><span data-stu-id="6e1ed-129">Replace the placeholder values with the device and IoT Hub information you created and saved at the start of this tutorial.</span></span> <span data-ttu-id="6e1ed-130">Enregistrez vos modifications (**Ctrl-O**, **Entrée**) et quittez l’éditeur (**Ctrl-X**).</span><span class="sxs-lookup"><span data-stu-id="6e1ed-130">Save your changes (**Ctrl-O**, **Enter**) and exit the editor (**Ctrl-X**).</span></span>

## <a name="run-the-sample"></a><span data-ttu-id="6e1ed-131">Exécution de l'exemple</span><span class="sxs-lookup"><span data-stu-id="6e1ed-131">Run the sample</span></span>

<span data-ttu-id="6e1ed-132">Exécutez les commandes suivantes pour installer les packages requis pour l’exemple :</span><span class="sxs-lookup"><span data-stu-id="6e1ed-132">Run the following commands to install the prerequisite packages for the sample:</span></span>

```sh
cd ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/simulator
npm install
```

<span data-ttu-id="6e1ed-133">Vous pouvez maintenant exécuter l’exemple de programme sur le Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="6e1ed-133">You can now run the sample program on the Raspberry Pi.</span></span> <span data-ttu-id="6e1ed-134">Entrez la commande :</span><span class="sxs-lookup"><span data-stu-id="6e1ed-134">Enter the command:</span></span>

```sh
sudo node ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/simulator/remote_monitoring.js
```

<span data-ttu-id="6e1ed-135">La sortie suivante est un exemple de sortie qui peut s’afficher à l’invite de commandes sur le Raspberry Pi :</span><span class="sxs-lookup"><span data-stu-id="6e1ed-135">The following sample output is an example of the output you see at the command prompt on the Raspberry Pi:</span></span>

![Sortie de l’application de Raspberry Pi][img-raspberry-output]

<span data-ttu-id="6e1ed-137">Appuyez sur **Ctrl-C** pour quitter le programme à tout moment.</span><span class="sxs-lookup"><span data-stu-id="6e1ed-137">Press **Ctrl-C** to exit the program at any time.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry-simulator](../../includes/iot-suite-raspberry-pi-kit-view-telemetry-simulator.md)]

## <a name="next-steps"></a><span data-ttu-id="6e1ed-138">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6e1ed-138">Next steps</span></span>

<span data-ttu-id="6e1ed-139">Visitez le [Centre de développement Azure IoT](https://azure.microsoft.com/develop/iot/) pour d’autres exemples et de la documentation complémentaire sur Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="6e1ed-139">Visit the [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>

[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-node-get-started-simulator/app-output.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
