---
title: "aaaConnect un tooAzure framboises Pi IoT Suite à l’aide de Node.js avec capteurs réels | Documents Microsoft"
description: "Utilisez hello Microsoft Azure IoT Starter Kit pour hello framboises Pi 3 et Azure IoT Suite. Utiliser Node.js tooconnect votre solution de surveillance à distance de toohello framboises Pi, envoyer la télémétrie de capteurs toohello cloud et répondre toomethods appelée à partir du tableau de bord de solution hello."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-suite
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: 7ffb4a7a8c04b424a1f29170f4739d89f39a2429
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-raspberry-pi-3-toohello-remote-monitoring-solution-and-send-telemetry-from-a-real-sensor-using-nodejs"></a><span data-ttu-id="88db5-104">Se connecter à votre solution de surveillance à distance de toohello framboises Pi 3 et envoyer la télémétrie à partir d’un capteur réels à l’aide de Node.js</span><span class="sxs-lookup"><span data-stu-id="88db5-104">Connect your Raspberry Pi 3 toohello remote monitoring solution and send telemetry from a real sensor using Node.js</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

<span data-ttu-id="88db5-105">Ce didacticiel vous montre comment toouse hello Microsoft Azure IoT Starter Kit pour framboises Pi 3 toodevelop, un lecteur de température et humidité pouvant communiquer avec le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="88db5-105">This tutorial shows you how toouse hello Microsoft Azure IoT Starter Kit for Raspberry Pi 3 toodevelop a temperature and humidity reader that can communicate with hello cloud.</span></span> <span data-ttu-id="88db5-106">didacticiel de Hello utilise :</span><span class="sxs-lookup"><span data-stu-id="88db5-106">hello tutorial uses:</span></span>

- <span data-ttu-id="88db5-107">Raspbian OS, hello Node.js langage de programmation et hello Microsoft Azure IoT SDK pour Node.js tooimplement un appareil de l’exemple.</span><span class="sxs-lookup"><span data-stu-id="88db5-107">Raspbian OS, hello Node.js programming language, and hello Microsoft Azure IoT SDK for Node.js tooimplement a sample device.</span></span>
- <span data-ttu-id="88db5-108">la surveillance à distance Hello IoT Suite, solution préconfigurée comme hello nuage back-end.</span><span class="sxs-lookup"><span data-stu-id="88db5-108">hello IoT Suite remote monitoring preconfigured solution as hello cloud-based back end.</span></span>

## <a name="overview"></a><span data-ttu-id="88db5-109">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="88db5-109">Overview</span></span>

<span data-ttu-id="88db5-110">Dans ce didacticiel, vous effectuez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="88db5-110">In this tutorial, you complete hello following steps:</span></span>

- <span data-ttu-id="88db5-111">Déployer une instance de hello distant tooyour solution préconfigurée analyse abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="88db5-111">Deploy an instance of hello remote monitoring preconfigured solution tooyour Azure subscription.</span></span> <span data-ttu-id="88db5-112">Cette étape déploie et configure automatiquement plusieurs services Azure.</span><span class="sxs-lookup"><span data-stu-id="88db5-112">This step automatically deploys and configures multiple Azure services.</span></span>
- <span data-ttu-id="88db5-113">Configurer votre toocommunicate capteurs et de périphérique avec votre ordinateur et le hello solution de surveillance à distance.</span><span class="sxs-lookup"><span data-stu-id="88db5-113">Set up your device and sensors toocommunicate with your computer and hello remote monitoring solution.</span></span>
- <span data-ttu-id="88db5-114">Hello exemple périphérique code tooconnect toohello distant solution d’analyse de mise à jour et envoyer la télémétrie que vous pouvez afficher sur le tableau de bord de solution hello.</span><span class="sxs-lookup"><span data-stu-id="88db5-114">Update hello sample device code tooconnect toohello remote monitoring solution, and send telemetry that you can view on hello solution dashboard.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-prerequisites](../../includes/iot-suite-raspberry-pi-kit-prerequisites.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="88db5-115">Bonjour dispositions de solution de surveillance à distance à un ensemble de services Azure dans votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="88db5-115">hello remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="88db5-116">déploiement de Hello reflète une architecture d’entreprise réel.</span><span class="sxs-lookup"><span data-stu-id="88db5-116">hello deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="88db5-117">frais de la consommation Azure inutile tooavoid, supprimer votre instance de la solution de hello préconfiguré dans azureiotsuite.com lorsque vous avez terminé avec lui.</span><span class="sxs-lookup"><span data-stu-id="88db5-117">tooavoid unnecessary Azure consumption charges, delete your instance of hello preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="88db5-118">Si vous avez besoin de hello solution préconfigurée à nouveau, vous pouvez le recréer facilement.</span><span class="sxs-lookup"><span data-stu-id="88db5-118">If you need hello preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="88db5-119">Pour plus d’informations sur la réduction de la consommation lors hello s’exécute la solution de surveillance à distance, consultez [configuration Azure IoT Suite préconfiguré des solutions à des fins de démonstration][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="88db5-119">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi](../../includes/iot-suite-raspberry-pi-kit-prepare-pi.md)]

## <a name="download-and-configure-hello-sample"></a><span data-ttu-id="88db5-120">Télécharger et configurer l’exemple hello</span><span class="sxs-lookup"><span data-stu-id="88db5-120">Download and configure hello sample</span></span>

<span data-ttu-id="88db5-121">Vous pouvez maintenant télécharger et configurer l’application du client de contrôle à distance hello sur votre Pi framboises.</span><span class="sxs-lookup"><span data-stu-id="88db5-121">You can now download and configure hello remote monitoring client application on your Raspberry Pi.</span></span>

### <a name="install-nodejs"></a><span data-ttu-id="88db5-122">Installer Node.js</span><span class="sxs-lookup"><span data-stu-id="88db5-122">Install Node.js</span></span>

<span data-ttu-id="88db5-123">Installez Node.js sur votre Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="88db5-123">Install Node.js on your Raspberry Pi.</span></span> <span data-ttu-id="88db5-124">Hello IoT SDK pour Node.js nécessite 0.11.5 Node.js ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="88db5-124">hello IoT SDK for Node.js requires version 0.11.5 of Node.js or later.</span></span> <span data-ttu-id="88db5-125">Hello étapes suivantes vous montrent comment tooinstall les v6.10.2 de Node.js sur votre Pi framboises :</span><span class="sxs-lookup"><span data-stu-id="88db5-125">hello following steps show you how tooinstall Node.js v6.10.2 on your Raspberry Pi:</span></span>

1. <span data-ttu-id="88db5-126">Utilisez hello suivant commande tooupdate votre Pi framboises :</span><span class="sxs-lookup"><span data-stu-id="88db5-126">Use hello following command tooupdate your Raspberry Pi:</span></span>

    ```sh
    sudo apt-get update
    ```

1. <span data-ttu-id="88db5-127">Utilisez hello suivant commande toodownload hello Node.js binaires tooyour framboises Pi :</span><span class="sxs-lookup"><span data-stu-id="88db5-127">Use hello following command toodownload hello Node.js binaries tooyour Raspberry Pi:</span></span>

    ```sh
    wget https://nodejs.org/dist/v6.10.2/node-v6.10.2-linux-armv7l.tar.gz
    ```

1. <span data-ttu-id="88db5-128">Utilisez hello suivant des fichiers binaires de commande tooinstall hello :</span><span class="sxs-lookup"><span data-stu-id="88db5-128">Use hello following command tooinstall hello binaries:</span></span>

    ```sh
    sudo tar -C /usr/local --strip-components 1 -xzf node-v6.10.2-linux-armv7l.tar.gz
    ```

1. <span data-ttu-id="88db5-129">Utilisez hello suivant tooverify commande avoir installé Node.js v6.10.2 correctement :</span><span class="sxs-lookup"><span data-stu-id="88db5-129">Use hello following command tooverify you have installed Node.js v6.10.2 successfully:</span></span>

    ```sh
    node --version
    ```

### <a name="clone-hello-repositories"></a><span data-ttu-id="88db5-130">Clone hello référentiels</span><span class="sxs-lookup"><span data-stu-id="88db5-130">Clone hello repositories</span></span>

<span data-ttu-id="88db5-131">Si vous n’avez pas déjà fait, hello du clone requis référentiels en exécutant hello suivant de commandes sur votre Pi :</span><span class="sxs-lookup"><span data-stu-id="88db5-131">If you haven't already done so, clone hello required repositories by running hello following commands on your Pi:</span></span>

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-node-raspberrypi-getstartedkit.git`
```

### <a name="update-hello-device-connection-string"></a><span data-ttu-id="88db5-132">Mettre à jour la chaîne de connexion de périphérique hello</span><span class="sxs-lookup"><span data-stu-id="88db5-132">Update hello device connection string</span></span>

<span data-ttu-id="88db5-133">Fichier source d’exemple hello ouvrir Bonjour **nano** éditeur à l’aide de hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="88db5-133">Open hello sample source file in hello **nano** editor using hello following command:</span></span>

```sh
nano ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/basic/remote_monitoring.js
```

<span data-ttu-id="88db5-134">Recherchez hello ligne :</span><span class="sxs-lookup"><span data-stu-id="88db5-134">Find hello line:</span></span>

```javascript
var connectionString = 'HostName=[Your IoT hub name].azure-devices.net;DeviceId=[Your device id];SharedAccessKey=[Your device key]';
```

<span data-ttu-id="88db5-135">Remplacez les valeurs d’espace réservé hello par périphérique de hello et informations IoT Hub vous avez créé et enregistré au démarrage hello de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="88db5-135">Replace hello placeholder values with hello device and IoT Hub information you created and saved at hello start of this tutorial.</span></span> <span data-ttu-id="88db5-136">Enregistrez vos modifications (**Ctrl-O**, **entrée**) et quittez l’éditeur hello (**Ctrl-X**).</span><span class="sxs-lookup"><span data-stu-id="88db5-136">Save your changes (**Ctrl-O**, **Enter**) and exit hello editor (**Ctrl-X**).</span></span>

## <a name="run-hello-sample"></a><span data-ttu-id="88db5-137">Exécuter l’exemple hello</span><span class="sxs-lookup"><span data-stu-id="88db5-137">Run hello sample</span></span>

<span data-ttu-id="88db5-138">Les commandes de suivantes de hello exécution tooinstall packages de composants requis hello pour exemple hello :</span><span class="sxs-lookup"><span data-stu-id="88db5-138">Run hello following commands tooinstall hello prerequisite packages for hello sample:</span></span>

```sh
cd ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/basic
npm install
```

<span data-ttu-id="88db5-139">Vous pouvez maintenant exécuter l’exemple de programme hello sur hello framboises Pi.</span><span class="sxs-lookup"><span data-stu-id="88db5-139">You can now run hello sample program on hello Raspberry Pi.</span></span> <span data-ttu-id="88db5-140">Entrez la commande hello :</span><span class="sxs-lookup"><span data-stu-id="88db5-140">Enter hello command:</span></span>

```sh
sudo node ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/basic/remote_monitoring.js
```

<span data-ttu-id="88db5-141">Hello exemple de sortie suivant est un exemple de sortie hello, que reportez-vous à l’invite de commande hello sur hello framboises Pi :</span><span class="sxs-lookup"><span data-stu-id="88db5-141">hello following sample output is an example of hello output you see at hello command prompt on hello Raspberry Pi:</span></span>

![Sortie de l’application de Raspberry Pi][img-raspberry-output]

<span data-ttu-id="88db5-143">Appuyez sur **Ctrl-C** programme de hello tooexit à tout moment.</span><span class="sxs-lookup"><span data-stu-id="88db5-143">Press **Ctrl-C** tooexit hello program at any time.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry](../../includes/iot-suite-raspberry-pi-kit-view-telemetry.md)]

## <a name="next-steps"></a><span data-ttu-id="88db5-144">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="88db5-144">Next steps</span></span>

<span data-ttu-id="88db5-145">Visitez hello [centre de développement Azure IoT](https://azure.microsoft.com/develop/iot/) pour plus d’exemples et documentation sur Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="88db5-145">Visit hello [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>

[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-node-get-started-basic/app-output.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md