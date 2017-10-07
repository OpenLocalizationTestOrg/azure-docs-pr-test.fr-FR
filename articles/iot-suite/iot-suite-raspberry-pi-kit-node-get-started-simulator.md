---
title: "aaaConnect un tooAzure framboises Pi IoT Suite à une télémétrie simulée à l’aide de Node.js | Documents Microsoft"
description: "Utilisez hello Microsoft Azure IoT Starter Kit pour hello framboises Pi 3 et Azure IoT Suite. Utiliser Node.js tooconnect votre solution de surveillance à distance de toohello framboises Pi, envoyer la télémétrie simulé toohello cloud et répondre toomethods appelée à partir du tableau de bord de solution hello."
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
ms.openlocfilehash: f65eeaa6e83fd89cdedae8fa8386a3e9ef8417d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-raspberry-pi-3-toohello-remote-monitoring-solution-and-send-simulated-telemetry-using-nodejs"></a><span data-ttu-id="d6bd2-104">Se connecter à votre solution de surveillance à distance de toohello framboises Pi 3 et envoyer la télémétrie simulé à l’aide de Node.js</span><span class="sxs-lookup"><span data-stu-id="d6bd2-104">Connect your Raspberry Pi 3 toohello remote monitoring solution and send simulated telemetry using Node.js</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

<span data-ttu-id="d6bd2-105">Ce didacticiel vous montre comment toouse hello framboises Pi 3 toosimulate température et humidité données toosend toohello cloud.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-105">This tutorial shows you how toouse hello Raspberry Pi 3 toosimulate temperature and humidity data toosend toohello cloud.</span></span> <span data-ttu-id="d6bd2-106">didacticiel de Hello utilise :</span><span class="sxs-lookup"><span data-stu-id="d6bd2-106">hello tutorial uses:</span></span>

- <span data-ttu-id="d6bd2-107">Raspbian OS, hello Node.js langage de programmation et hello Microsoft Azure IoT SDK pour Node.js tooimplement un appareil de l’exemple.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-107">Raspbian OS, hello Node.js programming language, and hello Microsoft Azure IoT SDK for Node.js tooimplement a sample device.</span></span>
- <span data-ttu-id="d6bd2-108">la surveillance à distance Hello IoT Suite, solution préconfigurée comme hello nuage back-end.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-108">hello IoT Suite remote monitoring preconfigured solution as hello cloud-based back end.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-overview-simulator](../../includes/iot-suite-raspberry-pi-kit-overview-simulator.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="d6bd2-109">Bonjour dispositions de solution de surveillance à distance à un ensemble de services Azure dans votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-109">hello remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="d6bd2-110">déploiement de Hello reflète une architecture d’entreprise réel.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-110">hello deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="d6bd2-111">frais de la consommation Azure inutile tooavoid, supprimer votre instance de la solution de hello préconfiguré dans azureiotsuite.com lorsque vous avez terminé avec lui.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-111">tooavoid unnecessary Azure consumption charges, delete your instance of hello preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="d6bd2-112">Si vous avez besoin de hello solution préconfigurée à nouveau, vous pouvez le recréer facilement.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-112">If you need hello preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="d6bd2-113">Pour plus d’informations sur la réduction de la consommation lors hello s’exécute la solution de surveillance à distance, consultez [configuration Azure IoT Suite préconfiguré des solutions à des fins de démonstration][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="d6bd2-113">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi-simulator](../../includes/iot-suite-raspberry-pi-kit-prepare-pi-simulator.md)]

## <a name="download-and-configure-hello-sample"></a><span data-ttu-id="d6bd2-114">Télécharger et configurer l’exemple hello</span><span class="sxs-lookup"><span data-stu-id="d6bd2-114">Download and configure hello sample</span></span>

<span data-ttu-id="d6bd2-115">Vous pouvez maintenant télécharger et configurer l’application du client de contrôle à distance hello sur votre Pi framboises.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-115">You can now download and configure hello remote monitoring client application on your Raspberry Pi.</span></span>

### <a name="install-nodejs"></a><span data-ttu-id="d6bd2-116">Installer Node.js</span><span class="sxs-lookup"><span data-stu-id="d6bd2-116">Install Node.js</span></span>

<span data-ttu-id="d6bd2-117">Si vous ne l’avez pas déjà fait, installez Node.js sur votre Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-117">If you haven't done so already, install Node.js on your Raspberry Pi.</span></span> <span data-ttu-id="d6bd2-118">Hello IoT SDK pour Node.js nécessite 0.11.5 Node.js ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-118">hello IoT SDK for Node.js requires version 0.11.5 of Node.js or later.</span></span> <span data-ttu-id="d6bd2-119">Hello étapes suivantes vous montrent comment tooinstall les v6.10.2 de Node.js sur votre Pi framboises :</span><span class="sxs-lookup"><span data-stu-id="d6bd2-119">hello following steps show you how tooinstall Node.js v6.10.2 on your Raspberry Pi:</span></span>

1. <span data-ttu-id="d6bd2-120">Utilisez hello suivant commande tooupdate votre Pi framboises :</span><span class="sxs-lookup"><span data-stu-id="d6bd2-120">Use hello following command tooupdate your Raspberry Pi:</span></span>

    ```sh
    sudo apt-get update
    ```

1. <span data-ttu-id="d6bd2-121">Utilisez hello suivant commande toodownload hello Node.js binaires tooyour framboises Pi :</span><span class="sxs-lookup"><span data-stu-id="d6bd2-121">Use hello following command toodownload hello Node.js binaries tooyour Raspberry Pi:</span></span>

    ```sh
    wget https://nodejs.org/dist/v6.10.2/node-v6.10.2-linux-armv7l.tar.gz
    ```

1. <span data-ttu-id="d6bd2-122">Utilisez hello suivant des fichiers binaires de commande tooinstall hello :</span><span class="sxs-lookup"><span data-stu-id="d6bd2-122">Use hello following command tooinstall hello binaries:</span></span>

    ```sh
    sudo tar -C /usr/local --strip-components 1 -xzf node-v6.10.2-linux-armv7l.tar.gz
    ```

1. <span data-ttu-id="d6bd2-123">Utilisez hello suivant tooverify commande avoir installé Node.js v6.10.2 correctement :</span><span class="sxs-lookup"><span data-stu-id="d6bd2-123">Use hello following command tooverify you have installed Node.js v6.10.2 successfully:</span></span>

    ```sh
    node --version
    ```

### <a name="clone-hello-repositories"></a><span data-ttu-id="d6bd2-124">Clone hello référentiels</span><span class="sxs-lookup"><span data-stu-id="d6bd2-124">Clone hello repositories</span></span>

<span data-ttu-id="d6bd2-125">Si vous n’avez pas déjà fait, hello du clone requis référentiels en exécutant hello suivant de commandes dans un terminal de votre Pi :</span><span class="sxs-lookup"><span data-stu-id="d6bd2-125">If you haven't already done so, clone hello required repositories by running hello following commands in a terminal on your Pi:</span></span>

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-node-raspberrypi-getstartedkit.git
```

### <a name="update-hello-device-connection-string"></a><span data-ttu-id="d6bd2-126">Mettre à jour la chaîne de connexion de périphérique hello</span><span class="sxs-lookup"><span data-stu-id="d6bd2-126">Update hello device connection string</span></span>

<span data-ttu-id="d6bd2-127">Fichier source d’exemple hello ouvrir Bonjour **nano** éditeur à l’aide de hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="d6bd2-127">Open hello sample source file in hello **nano** editor using hello following command:</span></span>

```sh
nano ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/simulator/remote_monitoring.js
```

<span data-ttu-id="d6bd2-128">Recherchez hello ligne :</span><span class="sxs-lookup"><span data-stu-id="d6bd2-128">Find hello line:</span></span>

```javascript
var connectionString = 'HostName=[Your IoT hub name].azure-devices.net;DeviceId=[Your device id];SharedAccessKey=[Your device key]';
```

<span data-ttu-id="d6bd2-129">Remplacez les valeurs d’espace réservé hello par périphérique de hello et informations IoT Hub vous avez créé et enregistré au démarrage hello de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-129">Replace hello placeholder values with hello device and IoT Hub information you created and saved at hello start of this tutorial.</span></span> <span data-ttu-id="d6bd2-130">Enregistrez vos modifications (**Ctrl-O**, **entrée**) et quittez l’éditeur hello (**Ctrl-X**).</span><span class="sxs-lookup"><span data-stu-id="d6bd2-130">Save your changes (**Ctrl-O**, **Enter**) and exit hello editor (**Ctrl-X**).</span></span>

## <a name="run-hello-sample"></a><span data-ttu-id="d6bd2-131">Exécuter l’exemple hello</span><span class="sxs-lookup"><span data-stu-id="d6bd2-131">Run hello sample</span></span>

<span data-ttu-id="d6bd2-132">Les commandes de suivantes de hello exécution tooinstall packages de composants requis hello pour exemple hello :</span><span class="sxs-lookup"><span data-stu-id="d6bd2-132">Run hello following commands tooinstall hello prerequisite packages for hello sample:</span></span>

```sh
cd ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/simulator
npm install
```

<span data-ttu-id="d6bd2-133">Vous pouvez maintenant exécuter l’exemple de programme hello sur hello framboises Pi.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-133">You can now run hello sample program on hello Raspberry Pi.</span></span> <span data-ttu-id="d6bd2-134">Entrez la commande hello :</span><span class="sxs-lookup"><span data-stu-id="d6bd2-134">Enter hello command:</span></span>

```sh
sudo node ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/simulator/remote_monitoring.js
```

<span data-ttu-id="d6bd2-135">Hello exemple de sortie suivant est un exemple de sortie hello, que reportez-vous à l’invite de commande hello sur hello framboises Pi :</span><span class="sxs-lookup"><span data-stu-id="d6bd2-135">hello following sample output is an example of hello output you see at hello command prompt on hello Raspberry Pi:</span></span>

![Sortie de l’application de Raspberry Pi][img-raspberry-output]

<span data-ttu-id="d6bd2-137">Appuyez sur **Ctrl-C** programme de hello tooexit à tout moment.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-137">Press **Ctrl-C** tooexit hello program at any time.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry-simulator](../../includes/iot-suite-raspberry-pi-kit-view-telemetry-simulator.md)]

## <a name="next-steps"></a><span data-ttu-id="d6bd2-138">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d6bd2-138">Next steps</span></span>

<span data-ttu-id="d6bd2-139">Visitez hello [centre de développement Azure IoT](https://azure.microsoft.com/develop/iot/) pour plus d’exemples et documentation sur Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-139">Visit hello [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>

[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-node-get-started-simulator/app-output.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
