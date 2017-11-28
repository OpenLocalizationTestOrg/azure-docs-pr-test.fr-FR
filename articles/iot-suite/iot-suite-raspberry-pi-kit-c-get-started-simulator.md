---
title: "Connexion d’un Raspberry Pi à Azure IoT Suite à l’aide du langage de programmation C avec la télémétrie simulée | Microsoft Docs"
description: "Utilisez le Kit de démarrage Microsoft Azure IoT pour le Raspberry Pi 3 et IoT Azure Suite. Utilisez C pour connecter votre Raspberry Pi à la solution de surveillance à distance, envoyer la télémétrie simulée dans le cloud et répondre aux méthodes appelées à partir du tableau de bord de la solution."
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
ms.openlocfilehash: 43b82e5fb6a309283979f23d8c87af600595bc55
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="connect-your-raspberry-pi-3-to-the-remote-monitoring-solution-and-send-simulated-telemetry-using-c"></a><span data-ttu-id="52d95-104">Connecter votre Raspberry Pi 3 à la solution de surveillance à distance et envoyer la télémétrie simulée à l’aide de C</span><span class="sxs-lookup"><span data-stu-id="52d95-104">Connect your Raspberry Pi 3 to the remote monitoring solution and send simulated telemetry using C</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

<span data-ttu-id="52d95-105">Ce tutoriel vous montre comment utiliser le Raspberry Pi 3 pour simuler des données de température et d’humidité à envoyer dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="52d95-105">This tutorial shows you how to use the Raspberry Pi 3 to simulate temperature and humidity data to send to the cloud.</span></span> <span data-ttu-id="52d95-106">Le tutoriel utilise :</span><span class="sxs-lookup"><span data-stu-id="52d95-106">The tutorial uses:</span></span>

- <span data-ttu-id="52d95-107">le système d’exploitation Raspbian, le langage de programmation C et le kit de développement logiciel (SDK) Microsoft Azure IoT pour C pour implémenter un exemple d’appareil ;</span><span class="sxs-lookup"><span data-stu-id="52d95-107">Raspbian OS, the C programming language, and the Microsoft Azure IoT SDK for C to implement a sample device.</span></span>
- <span data-ttu-id="52d95-108">la solution préconfigurée de surveillance à distance Azure IoT Suite comme serveur principal basé sur le cloud.</span><span class="sxs-lookup"><span data-stu-id="52d95-108">The IoT Suite remote monitoring preconfigured solution as the cloud-based back end.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-overview-simulator](../../includes/iot-suite-raspberry-pi-kit-overview-simulator.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="52d95-109">La solution de surveillance à distance configure un ensemble de services Azure dans votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="52d95-109">The remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="52d95-110">Le déploiement reflète une architecture d’entreprise réelle.</span><span class="sxs-lookup"><span data-stu-id="52d95-110">The deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="52d95-111">Pour éviter des frais de consommation Azure inutiles, supprimez votre instance de la solution préconfigurée dans azureiotsuite.com quand vous ne l’utilisez plus.</span><span class="sxs-lookup"><span data-stu-id="52d95-111">To avoid unnecessary Azure consumption charges, delete your instance of the preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="52d95-112">Si vous avez à nouveau besoin de la solution préconfigurée, vous pouvez la recréer facilement.</span><span class="sxs-lookup"><span data-stu-id="52d95-112">If you need the preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="52d95-113">Pour plus d’informations sur la manière de réduire votre consommation pendant l’exécution de la solution de surveillance à distance, consultez [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config] (Configuration des solutions préconfigurées Azure IoT Suite à des fins de démonstration).</span><span class="sxs-lookup"><span data-stu-id="52d95-113">For more information about reducing consumption while the remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi-simulator](../../includes/iot-suite-raspberry-pi-kit-prepare-pi-simulator.md)]

## <a name="download-and-configure-the-sample"></a><span data-ttu-id="52d95-114">Télécharger et configurer l’exemple</span><span class="sxs-lookup"><span data-stu-id="52d95-114">Download and configure the sample</span></span>

<span data-ttu-id="52d95-115">Vous pouvez à présent télécharger et configurer l’application cliente de surveillance à distance sur votre Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="52d95-115">You can now download and configure the remote monitoring client application on your Raspberry Pi.</span></span>

### <a name="clone-the-repositories"></a><span data-ttu-id="52d95-116">Cloner les dépôts</span><span class="sxs-lookup"><span data-stu-id="52d95-116">Clone the repositories</span></span>

<span data-ttu-id="52d95-117">Si vous ne l’avez pas déjà fait, clonez les dépôts requis en exécutant les commandes suivantes dans un terminal sur votre Pi :</span><span class="sxs-lookup"><span data-stu-id="52d95-117">If you haven't already done so, clone the required repositories by running the following commands in a terminal on your Pi:</span></span>

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-c-raspberrypi-getstartedkit.git
```

### <a name="update-the-device-connection-string"></a><span data-ttu-id="52d95-118">Mettre à jour la chaîne de connexion d’appareil</span><span class="sxs-lookup"><span data-stu-id="52d95-118">Update the device connection string</span></span>

<span data-ttu-id="52d95-119">Ouvrez l’exemple de fichier source dans l’éditeur **nano** à l’aide de la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="52d95-119">Open the sample source file in the **nano** editor using the following command:</span></span>

```sh
nano ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/simulator/remote_monitoring/remote_monitoring.c
```

<span data-ttu-id="52d95-120">Recherchez les lignes suivantes :</span><span class="sxs-lookup"><span data-stu-id="52d95-120">Locate the following lines:</span></span>

```c
static const char* deviceId = "[Device Id]";
static const char* connectionString = "HostName=[IoTHub Name].azure-devices.net;DeviceId=[Device Id];SharedAccessKey=[Device Key]";
```

<span data-ttu-id="52d95-121">Remplacez les valeurs dans l’espace réservé par les informations sur l’appareil et l’IoT Hub que vous avez créées et enregistrées au début de ce tutoriel.</span><span class="sxs-lookup"><span data-stu-id="52d95-121">Replace the placeholder values with the device and IoT Hub information you created and saved at the start of this tutorial.</span></span> <span data-ttu-id="52d95-122">Enregistrez vos modifications (**Ctrl-O**, **Entrée**) et quittez l’éditeur (**Ctrl-X**).</span><span class="sxs-lookup"><span data-stu-id="52d95-122">Save your changes (**Ctrl-O**, **Enter**) and exit the editor (**Ctrl-X**).</span></span>

## <a name="build-the-sample"></a><span data-ttu-id="52d95-123">Générer l’exemple</span><span class="sxs-lookup"><span data-stu-id="52d95-123">Build the sample</span></span>

<span data-ttu-id="52d95-124">Installez les packages requis pour le Kit de développement logiciel (SDK) d’appareil Microsoft Azure IoT pour C en exécutant les commandes suivantes dans un terminal sur le Raspberry Pi :</span><span class="sxs-lookup"><span data-stu-id="52d95-124">Install the prerequisite packages for the Microsoft Azure IoT Device SDK for C by running the following commands in a terminal on the Raspberry Pi:</span></span>

```sh
sudo apt-get update
sudo apt-get install g++ make cmake git libcurl4-openssl-dev libssl-dev uuid-dev
```

<span data-ttu-id="52d95-125">Vous pouvez maintenant créer l’exemple de solution mis à jour sur le Raspberry Pi :</span><span class="sxs-lookup"><span data-stu-id="52d95-125">You can now build the updated sample solution on the Raspberry Pi:</span></span>

```sh
chmod +x ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/simulator/build.sh
~/iot-remote-monitoring-c-raspberrypi-getstartedkit/simulator/build.sh
```

<span data-ttu-id="52d95-126">Vous pouvez maintenant exécuter l’exemple de programme sur le Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="52d95-126">You can now run the sample program on the Raspberry Pi.</span></span> <span data-ttu-id="52d95-127">Entrez la commande :</span><span class="sxs-lookup"><span data-stu-id="52d95-127">Enter the command:</span></span>

```sh
sudo ~/cmake/remote_monitoring/remote_monitoring
```

<span data-ttu-id="52d95-128">La sortie suivante est un exemple de sortie qui peut s’afficher à l’invite de commandes sur le Raspberry Pi :</span><span class="sxs-lookup"><span data-stu-id="52d95-128">The following sample output is an example of the output you see at the command prompt on the Raspberry Pi:</span></span>

![Sortie de l’application de Raspberry Pi][img-raspberry-output]

<span data-ttu-id="52d95-130">Appuyez sur **Ctrl-C** pour quitter le programme à tout moment.</span><span class="sxs-lookup"><span data-stu-id="52d95-130">Press **Ctrl-C** to exit the program at any time.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry-simulator](../../includes/iot-suite-raspberry-pi-kit-view-telemetry-simulator.md)]

## <a name="next-steps"></a><span data-ttu-id="52d95-131">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="52d95-131">Next steps</span></span>

<span data-ttu-id="52d95-132">Visitez le [Centre de développement Azure IoT](https://azure.microsoft.com/develop/iot/) pour d’autres exemples et de la documentation complémentaire sur Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="52d95-132">Visit the [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>

[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-c-get-started-simulator/appoutput.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
