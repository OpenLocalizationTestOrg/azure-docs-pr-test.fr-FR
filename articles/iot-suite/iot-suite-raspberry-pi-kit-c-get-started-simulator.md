---
title: "aaaConnect un tooAzure framboises Pi IoT Suite à l’aide de C avec les données de télémétrie simulée | Documents Microsoft"
description: "Utilisez hello Microsoft Azure IoT Starter Kit pour hello framboises Pi 3 et Azure IoT Suite. Utilisez C tooconnect votre solution de surveillance à distance de toohello framboises Pi, envoyer la télémétrie simulé toohello cloud et répondre toomethods appelée à partir du tableau de bord de solution hello."
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
ms.openlocfilehash: 3c4fa43b381385d1a7896cada34aa3aa0b8e5fb4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-raspberry-pi-3-toohello-remote-monitoring-solution-and-send-simulated-telemetry-using-c"></a><span data-ttu-id="f5496-104">Se connecter à votre solution de surveillance à distance de toohello framboises Pi 3 et envoyer la télémétrie simulé à l’aide de C</span><span class="sxs-lookup"><span data-stu-id="f5496-104">Connect your Raspberry Pi 3 toohello remote monitoring solution and send simulated telemetry using C</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

<span data-ttu-id="f5496-105">Ce didacticiel vous montre comment toouse hello framboises Pi 3 toosimulate température et humidité données toosend toohello cloud.</span><span class="sxs-lookup"><span data-stu-id="f5496-105">This tutorial shows you how toouse hello Raspberry Pi 3 toosimulate temperature and humidity data toosend toohello cloud.</span></span> <span data-ttu-id="f5496-106">didacticiel de Hello utilise :</span><span class="sxs-lookup"><span data-stu-id="f5496-106">hello tutorial uses:</span></span>

- <span data-ttu-id="f5496-107">Raspbian du système d’exploitation, langage de programmation hello C et hello Microsoft Azure IoT SDK pour C tooimplement un appareil de l’exemple.</span><span class="sxs-lookup"><span data-stu-id="f5496-107">Raspbian OS, hello C programming language, and hello Microsoft Azure IoT SDK for C tooimplement a sample device.</span></span>
- <span data-ttu-id="f5496-108">la surveillance à distance Hello IoT Suite, solution préconfigurée comme hello nuage back-end.</span><span class="sxs-lookup"><span data-stu-id="f5496-108">hello IoT Suite remote monitoring preconfigured solution as hello cloud-based back end.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-overview-simulator](../../includes/iot-suite-raspberry-pi-kit-overview-simulator.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="f5496-109">Bonjour dispositions de solution de surveillance à distance à un ensemble de services Azure dans votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="f5496-109">hello remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="f5496-110">déploiement de Hello reflète une architecture d’entreprise réel.</span><span class="sxs-lookup"><span data-stu-id="f5496-110">hello deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="f5496-111">frais de la consommation Azure inutile tooavoid, supprimer votre instance de la solution de hello préconfiguré dans azureiotsuite.com lorsque vous avez terminé avec lui.</span><span class="sxs-lookup"><span data-stu-id="f5496-111">tooavoid unnecessary Azure consumption charges, delete your instance of hello preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="f5496-112">Si vous avez besoin de hello solution préconfigurée à nouveau, vous pouvez le recréer facilement.</span><span class="sxs-lookup"><span data-stu-id="f5496-112">If you need hello preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="f5496-113">Pour plus d’informations sur la réduction de la consommation lors hello s’exécute la solution de surveillance à distance, consultez [configuration Azure IoT Suite préconfiguré des solutions à des fins de démonstration][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="f5496-113">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi-simulator](../../includes/iot-suite-raspberry-pi-kit-prepare-pi-simulator.md)]

## <a name="download-and-configure-hello-sample"></a><span data-ttu-id="f5496-114">Télécharger et configurer l’exemple hello</span><span class="sxs-lookup"><span data-stu-id="f5496-114">Download and configure hello sample</span></span>

<span data-ttu-id="f5496-115">Vous pouvez maintenant télécharger et configurer l’application du client de contrôle à distance hello sur votre Pi framboises.</span><span class="sxs-lookup"><span data-stu-id="f5496-115">You can now download and configure hello remote monitoring client application on your Raspberry Pi.</span></span>

### <a name="clone-hello-repositories"></a><span data-ttu-id="f5496-116">Clone hello référentiels</span><span class="sxs-lookup"><span data-stu-id="f5496-116">Clone hello repositories</span></span>

<span data-ttu-id="f5496-117">Si vous n’avez pas déjà fait, hello du clone requis référentiels en exécutant hello suivant de commandes dans un terminal de votre Pi :</span><span class="sxs-lookup"><span data-stu-id="f5496-117">If you haven't already done so, clone hello required repositories by running hello following commands in a terminal on your Pi:</span></span>

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-c-raspberrypi-getstartedkit.git
```

### <a name="update-hello-device-connection-string"></a><span data-ttu-id="f5496-118">Mettre à jour la chaîne de connexion de périphérique hello</span><span class="sxs-lookup"><span data-stu-id="f5496-118">Update hello device connection string</span></span>

<span data-ttu-id="f5496-119">Fichier source d’exemple hello ouvrir Bonjour **nano** éditeur à l’aide de hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="f5496-119">Open hello sample source file in hello **nano** editor using hello following command:</span></span>

```sh
nano ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/simulator/remote_monitoring/remote_monitoring.c
```

<span data-ttu-id="f5496-120">Recherchez hello lignes suivantes :</span><span class="sxs-lookup"><span data-stu-id="f5496-120">Locate hello following lines:</span></span>

```c
static const char* deviceId = "[Device Id]";
static const char* connectionString = "HostName=[IoTHub Name].azure-devices.net;DeviceId=[Device Id];SharedAccessKey=[Device Key]";
```

<span data-ttu-id="f5496-121">Remplacez les valeurs d’espace réservé hello par périphérique de hello et informations IoT Hub vous avez créé et enregistré au démarrage hello de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="f5496-121">Replace hello placeholder values with hello device and IoT Hub information you created and saved at hello start of this tutorial.</span></span> <span data-ttu-id="f5496-122">Enregistrez vos modifications (**Ctrl-O**, **entrée**) et quittez l’éditeur hello (**Ctrl-X**).</span><span class="sxs-lookup"><span data-stu-id="f5496-122">Save your changes (**Ctrl-O**, **Enter**) and exit hello editor (**Ctrl-X**).</span></span>

## <a name="build-hello-sample"></a><span data-ttu-id="f5496-123">Générez l’exemple hello</span><span class="sxs-lookup"><span data-stu-id="f5496-123">Build hello sample</span></span>

<span data-ttu-id="f5496-124">Installer les packages de composants requis hello pour hello Kit de développement logiciel de Microsoft Azure IoT appareil pour C en exécutant hello suivant de commandes dans un terminal de hello framboises Pi :</span><span class="sxs-lookup"><span data-stu-id="f5496-124">Install hello prerequisite packages for hello Microsoft Azure IoT Device SDK for C by running hello following commands in a terminal on hello Raspberry Pi:</span></span>

```sh
sudo apt-get update
sudo apt-get install g++ make cmake git libcurl4-openssl-dev libssl-dev uuid-dev
```

<span data-ttu-id="f5496-125">Vous pouvez ensuite générer la solution de l’exemple hello mis à jour sur hello framboises Pi :</span><span class="sxs-lookup"><span data-stu-id="f5496-125">You can now build hello updated sample solution on hello Raspberry Pi:</span></span>

```sh
chmod +x ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/simulator/build.sh
~/iot-remote-monitoring-c-raspberrypi-getstartedkit/simulator/build.sh
```

<span data-ttu-id="f5496-126">Vous pouvez maintenant exécuter l’exemple de programme hello sur hello framboises Pi.</span><span class="sxs-lookup"><span data-stu-id="f5496-126">You can now run hello sample program on hello Raspberry Pi.</span></span> <span data-ttu-id="f5496-127">Entrez la commande hello :</span><span class="sxs-lookup"><span data-stu-id="f5496-127">Enter hello command:</span></span>

```sh
sudo ~/cmake/remote_monitoring/remote_monitoring
```

<span data-ttu-id="f5496-128">Hello exemple de sortie suivant est un exemple de sortie hello, que reportez-vous à l’invite de commande hello sur hello framboises Pi :</span><span class="sxs-lookup"><span data-stu-id="f5496-128">hello following sample output is an example of hello output you see at hello command prompt on hello Raspberry Pi:</span></span>

![Sortie de l’application de Raspberry Pi][img-raspberry-output]

<span data-ttu-id="f5496-130">Appuyez sur **Ctrl-C** programme de hello tooexit à tout moment.</span><span class="sxs-lookup"><span data-stu-id="f5496-130">Press **Ctrl-C** tooexit hello program at any time.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry-simulator](../../includes/iot-suite-raspberry-pi-kit-view-telemetry-simulator.md)]

## <a name="next-steps"></a><span data-ttu-id="f5496-131">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f5496-131">Next steps</span></span>

<span data-ttu-id="f5496-132">Visitez hello [centre de développement Azure IoT](https://azure.microsoft.com/develop/iot/) pour plus d’exemples et documentation sur Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="f5496-132">Visit hello [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>

[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-c-get-started-simulator/appoutput.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
