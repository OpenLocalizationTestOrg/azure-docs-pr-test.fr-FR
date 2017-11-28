---
title: "met à jour des IoT Suite à l’aide de Node.js toosupport microprogramme aaaConnect un tooAzure framboises Pi | Documents Microsoft"
description: "Utilisez hello Microsoft Azure IoT Starter Kit pour hello framboises Pi 3 et Azure IoT Suite. Utiliser Node.js tooconnect votre solution de surveillance à distance de toohello framboises Pi, envoyer la télémétrie de capteurs toohello cloud et effectuer une mise à jour de microprogramme à distance."
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
ms.openlocfilehash: 43bd3f16ee3d292cd9cffa8bfe7d4ca721e5c39c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-raspberry-pi-3-toohello-remote-monitoring-solution-and-enable-remote-firmware-updates-using-nodejs"></a><span data-ttu-id="5e185-104">Se connecter à votre solution de surveillance à distance de toohello framboises Pi 3 et activer les mises à jour de microprogramme à distance à l’aide de Node.js</span><span class="sxs-lookup"><span data-stu-id="5e185-104">Connect your Raspberry Pi 3 toohello remote monitoring solution and enable remote firmware updates using Node.js</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

<span data-ttu-id="5e185-105">Ce didacticiel vous montre comment toouse hello Microsoft Azure IoT Starter Kit pour framboises Pi 3 à :</span><span class="sxs-lookup"><span data-stu-id="5e185-105">This tutorial shows you how toouse hello Microsoft Azure IoT Starter Kit for Raspberry Pi 3 to:</span></span>

* <span data-ttu-id="5e185-106">Développer un lecteur de température et humidité pouvant communiquer avec le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="5e185-106">Develop a temperature and humidity reader that can communicate with hello cloud.</span></span>
* <span data-ttu-id="5e185-107">Activer et exécuter une application cliente hello de tooupdate de mise à jour du microprogramme à distance sur hello framboises Pi.</span><span class="sxs-lookup"><span data-stu-id="5e185-107">Enable and perform a remote firmware update tooupdate hello client application on hello Raspberry Pi.</span></span>

<span data-ttu-id="5e185-108">didacticiel de Hello utilise :</span><span class="sxs-lookup"><span data-stu-id="5e185-108">hello tutorial uses:</span></span>

- <span data-ttu-id="5e185-109">Raspbian OS, hello Node.js langage de programmation et hello Microsoft Azure IoT SDK pour Node.js tooimplement un appareil de l’exemple.</span><span class="sxs-lookup"><span data-stu-id="5e185-109">Raspbian OS, hello Node.js programming language, and hello Microsoft Azure IoT SDK for Node.js tooimplement a sample device.</span></span>
- <span data-ttu-id="5e185-110">la surveillance à distance Hello IoT Suite, solution préconfigurée comme hello nuage back-end.</span><span class="sxs-lookup"><span data-stu-id="5e185-110">hello IoT Suite remote monitoring preconfigured solution as hello cloud-based back end.</span></span>

## <a name="overview"></a><span data-ttu-id="5e185-111">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="5e185-111">Overview</span></span>

<span data-ttu-id="5e185-112">Dans ce didacticiel, vous effectuez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="5e185-112">In this tutorial, you complete hello following steps:</span></span>

- <span data-ttu-id="5e185-113">Déployer une instance de hello distant tooyour solution préconfigurée analyse abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="5e185-113">Deploy an instance of hello remote monitoring preconfigured solution tooyour Azure subscription.</span></span> <span data-ttu-id="5e185-114">Cette étape déploie et configure automatiquement plusieurs services Azure.</span><span class="sxs-lookup"><span data-stu-id="5e185-114">This step automatically deploys and configures multiple Azure services.</span></span>
- <span data-ttu-id="5e185-115">Configurer votre toocommunicate capteurs et de périphérique avec votre ordinateur et le hello solution de surveillance à distance.</span><span class="sxs-lookup"><span data-stu-id="5e185-115">Set up your device and sensors toocommunicate with your computer and hello remote monitoring solution.</span></span>
- <span data-ttu-id="5e185-116">Hello exemple périphérique code tooconnect toohello distant solution d’analyse de mise à jour et envoyer la télémétrie que vous pouvez afficher sur le tableau de bord de solution hello.</span><span class="sxs-lookup"><span data-stu-id="5e185-116">Update hello sample device code tooconnect toohello remote monitoring solution, and send telemetry that you can view on hello solution dashboard.</span></span>
- <span data-ttu-id="5e185-117">Utilisez hello exemple périphérique code tooupdate hello d’application cliente.</span><span class="sxs-lookup"><span data-stu-id="5e185-117">Use hello sample device code tooupdate hello client application.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-prerequisites](../../includes/iot-suite-raspberry-pi-kit-prerequisites.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="5e185-118">Bonjour dispositions de solution de surveillance à distance à un ensemble de services Azure dans votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="5e185-118">hello remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="5e185-119">déploiement de Hello reflète une architecture d’entreprise réel.</span><span class="sxs-lookup"><span data-stu-id="5e185-119">hello deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="5e185-120">frais de la consommation Azure inutile tooavoid, supprimer votre instance de la solution de hello préconfiguré dans azureiotsuite.com lorsque vous avez terminé avec lui.</span><span class="sxs-lookup"><span data-stu-id="5e185-120">tooavoid unnecessary Azure consumption charges, delete your instance of hello preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="5e185-121">Si vous avez besoin de hello solution préconfigurée à nouveau, vous pouvez le recréer facilement.</span><span class="sxs-lookup"><span data-stu-id="5e185-121">If you need hello preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="5e185-122">Pour plus d’informations sur la réduction de la consommation lors hello s’exécute la solution de surveillance à distance, consultez [configuration Azure IoT Suite préconfiguré des solutions à des fins de démonstration][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="5e185-122">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi](../../includes/iot-suite-raspberry-pi-kit-prepare-pi.md)]

## <a name="download-and-configure-hello-sample"></a><span data-ttu-id="5e185-123">Télécharger et configurer l’exemple hello</span><span class="sxs-lookup"><span data-stu-id="5e185-123">Download and configure hello sample</span></span>

<span data-ttu-id="5e185-124">Vous pouvez maintenant télécharger et configurer l’application du client de contrôle à distance hello sur votre Pi framboises.</span><span class="sxs-lookup"><span data-stu-id="5e185-124">You can now download and configure hello remote monitoring client application on your Raspberry Pi.</span></span>

### <a name="install-nodejs"></a><span data-ttu-id="5e185-125">Installer Node.js</span><span class="sxs-lookup"><span data-stu-id="5e185-125">Install Node.js</span></span>

<span data-ttu-id="5e185-126">Si vous ne l’avez pas déjà fait, installez Node.js sur votre Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="5e185-126">If you haven't done so already, install Node.js on your Raspberry Pi.</span></span> <span data-ttu-id="5e185-127">Hello IoT SDK pour Node.js nécessite 0.11.5 Node.js ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="5e185-127">hello IoT SDK for Node.js requires version 0.11.5 of Node.js or later.</span></span> <span data-ttu-id="5e185-128">Hello étapes suivantes vous montrent comment tooinstall les v6.10.2 de Node.js sur votre Pi framboises :</span><span class="sxs-lookup"><span data-stu-id="5e185-128">hello following steps show you how tooinstall Node.js v6.10.2 on your Raspberry Pi:</span></span>

1. <span data-ttu-id="5e185-129">Utilisez hello suivant commande tooupdate votre Pi framboises :</span><span class="sxs-lookup"><span data-stu-id="5e185-129">Use hello following command tooupdate your Raspberry Pi:</span></span>

    ```sh
    sudo apt-get update
    ```

1. <span data-ttu-id="5e185-130">Utilisez hello suivant commande toodownload hello Node.js binaires tooyour framboises Pi :</span><span class="sxs-lookup"><span data-stu-id="5e185-130">Use hello following command toodownload hello Node.js binaries tooyour Raspberry Pi:</span></span>

    ```sh
    wget https://nodejs.org/dist/v6.10.2/node-v6.10.2-linux-armv7l.tar.gz
    ```

1. <span data-ttu-id="5e185-131">Utilisez hello suivant des fichiers binaires de commande tooinstall hello :</span><span class="sxs-lookup"><span data-stu-id="5e185-131">Use hello following command tooinstall hello binaries:</span></span>

    ```sh
    sudo tar -C /usr/local --strip-components 1 -xzf node-v6.10.2-linux-armv7l.tar.gz
    ```

1. <span data-ttu-id="5e185-132">Utilisez hello suivant tooverify commande avoir installé Node.js v6.10.2 correctement :</span><span class="sxs-lookup"><span data-stu-id="5e185-132">Use hello following command tooverify you have installed Node.js v6.10.2 successfully:</span></span>

    ```sh
    node --version
    ```

### <a name="clone-hello-repositories"></a><span data-ttu-id="5e185-133">Clone hello référentiels</span><span class="sxs-lookup"><span data-stu-id="5e185-133">Clone hello repositories</span></span>

<span data-ttu-id="5e185-134">Si vous n’avez pas déjà fait, hello du clone requis référentiels en exécutant hello suivant de commandes sur votre Pi :</span><span class="sxs-lookup"><span data-stu-id="5e185-134">If you haven't done so already, clone hello required repositories by running hello following commands on your Pi:</span></span>

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-node-raspberrypi-getstartedkit.git
```

### <a name="update-hello-device-connection-string"></a><span data-ttu-id="5e185-135">Mettre à jour la chaîne de connexion de périphérique hello</span><span class="sxs-lookup"><span data-stu-id="5e185-135">Update hello device connection string</span></span>

<span data-ttu-id="5e185-136">Fichier de configuration d’exemple hello ouvrir Bonjour **nano** éditeur à l’aide de hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="5e185-136">Open hello sample configuration file in hello **nano** editor using hello following command:</span></span>

```sh
nano ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/advanced/config/deviceinfo
```

<span data-ttu-id="5e185-137">Remplacez les valeurs d’espace réservé hello avec l’id de périphérique hello et informations IoT Hub vous avez créé et enregistré au démarrage hello de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="5e185-137">Replace hello placeholder values with hello device id and IoT Hub information you created and saved at hello start of this tutorial.</span></span>

<span data-ttu-id="5e185-138">Lorsque vous avez terminé, contenu hello du fichier deviceinfo de hello doit ressembler à hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="5e185-138">When you are done, hello contents of hello deviceinfo file should look like hello following example:</span></span>

```conf
yourdeviceid
HostName=youriothubname.azure-devices.net;DeviceId=yourdeviceid;SharedAccessKey=yourdevicekey
```

<span data-ttu-id="5e185-139">Enregistrez vos modifications (**Ctrl-O**, **entrée**) et quittez l’éditeur hello (**Ctrl-X**).</span><span class="sxs-lookup"><span data-stu-id="5e185-139">Save your changes (**Ctrl-O**, **Enter**) and exit hello editor (**Ctrl-X**).</span></span>

## <a name="run-hello-sample"></a><span data-ttu-id="5e185-140">Exécuter l’exemple hello</span><span class="sxs-lookup"><span data-stu-id="5e185-140">Run hello sample</span></span>

<span data-ttu-id="5e185-141">Les commandes de suivantes de hello exécution tooinstall packages de composants requis hello pour exemple hello :</span><span class="sxs-lookup"><span data-stu-id="5e185-141">Run hello following commands tooinstall hello prerequisite packages for hello sample:</span></span>

```sh
cd ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/advance/1.0
npm install
```

<span data-ttu-id="5e185-142">Vous pouvez maintenant exécuter l’exemple de programme hello sur hello framboises Pi.</span><span class="sxs-lookup"><span data-stu-id="5e185-142">You can now run hello sample program on hello Raspberry Pi.</span></span> <span data-ttu-id="5e185-143">Entrez la commande hello :</span><span class="sxs-lookup"><span data-stu-id="5e185-143">Enter hello command:</span></span>

```sh
sudo node ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/advanced/1.0/remote_monitoring.js
```

<span data-ttu-id="5e185-144">Hello exemple de sortie suivant est un exemple de sortie hello, que reportez-vous à l’invite de commande hello sur hello framboises Pi :</span><span class="sxs-lookup"><span data-stu-id="5e185-144">hello following sample output is an example of hello output you see at hello command prompt on hello Raspberry Pi:</span></span>

![Sortie de l’application de Raspberry Pi][img-raspberry-output]

<span data-ttu-id="5e185-146">Appuyez sur **Ctrl-C** programme de hello tooexit à tout moment.</span><span class="sxs-lookup"><span data-stu-id="5e185-146">Press **Ctrl-C** tooexit hello program at any time.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry-advanced](../../includes/iot-suite-raspberry-pi-kit-view-telemetry-advanced.md)]

1. <span data-ttu-id="5e185-147">Dans le tableau de bord hello solution, cliquez sur **périphériques** toovisit hello **périphériques** page.</span><span class="sxs-lookup"><span data-stu-id="5e185-147">In hello solution dashboard, click **Devices** toovisit hello **Devices** page.</span></span> <span data-ttu-id="5e185-148">Sélectionnez votre Pi framboises Bonjour **liste des appareils**.</span><span class="sxs-lookup"><span data-stu-id="5e185-148">Select your Raspberry Pi in hello **Device List**.</span></span> <span data-ttu-id="5e185-149">Ensuite, choisissez **Méthodes** :</span><span class="sxs-lookup"><span data-stu-id="5e185-149">Then choose **Methods**:</span></span>

    ![Liste des appareils dans le tableau de bord][img-list-devices]

1. <span data-ttu-id="5e185-151">Sur hello **appeler une méthode** choisissez **InitiateFirmwareUpdate** Bonjour **méthode** liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="5e185-151">On hello **Invoke Method** page, choose **InitiateFirmwareUpdate** in hello **Method** dropdown.</span></span>

1. <span data-ttu-id="5e185-152">Bonjour **FWPackageURI** , entrez **https://raw.githubusercontent.com/Azure-Samples/iot-remote-monitoring-node-raspberrypi-getstartedkit/master/advanced/2.0/raspberry.js**.</span><span class="sxs-lookup"><span data-stu-id="5e185-152">In hello **FWPackageURI** field, enter **https://raw.githubusercontent.com/Azure-Samples/iot-remote-monitoring-node-raspberrypi-getstartedkit/master/advanced/2.0/raspberry.js**.</span></span> <span data-ttu-id="5e185-153">Ce fichier contient l’implémentation de hello de la version 2.0 du microprogramme de hello.</span><span class="sxs-lookup"><span data-stu-id="5e185-153">This file contains hello implementation of version 2.0 of hello firmware.</span></span>

1. <span data-ttu-id="5e185-154">Choisissez **InvokeMethod**.</span><span class="sxs-lookup"><span data-stu-id="5e185-154">Choose **InvokeMethod**.</span></span> <span data-ttu-id="5e185-155">application Hello sur hello framboises Pi envoie un tableau de bord d’accusé de réception différé toohello solution.</span><span class="sxs-lookup"><span data-stu-id="5e185-155">hello app on hello Raspberry Pi sends an acknowledgment back toohello solution dashboard.</span></span> <span data-ttu-id="5e185-156">Il démarre ensuite le processus de mise à jour de microprogramme hello en téléchargeant hello nouvelle version du microprogramme de hello :</span><span class="sxs-lookup"><span data-stu-id="5e185-156">It then starts hello firmware update process by downloading hello new version of hello firmware:</span></span>

    ![Afficher l’historique de la méthode][img-method-history]

## <a name="observe-hello-firmware-update-process"></a><span data-ttu-id="5e185-158">Observez le processus de mise à jour de microprogramme hello</span><span class="sxs-lookup"><span data-stu-id="5e185-158">Observe hello firmware update process</span></span>

<span data-ttu-id="5e185-159">Vous pouvez observer les processus de mise à jour de microprogramme hello lorsqu’elle s’exécute sur l’appareil de hello et que vous affichez hello signalés propriétés dans le tableau de bord de solution hello :</span><span class="sxs-lookup"><span data-stu-id="5e185-159">You can observe hello firmware update process as it runs on hello device and by viewing hello reported properties in hello solution dashboard:</span></span>

1. <span data-ttu-id="5e185-160">Vous pouvez afficher la progression hello dans des processus de mise à jour hello sur hello framboises Pi :</span><span class="sxs-lookup"><span data-stu-id="5e185-160">You can view hello progress in of hello update process on hello Raspberry Pi:</span></span>

    ![Afficher la progression de la mise à jour][img-update-progress]

    > [!NOTE]
    > <span data-ttu-id="5e185-162">application de surveillance à distance Hello redémarre en mode silencieux lors de la mise à jour hello terminée.</span><span class="sxs-lookup"><span data-stu-id="5e185-162">hello remote monitoring app restarts silently when hello update completes.</span></span> <span data-ttu-id="5e185-163">Utilisez la commande hello `ps -ef` tooverify, il est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="5e185-163">Use hello command `ps -ef` tooverify it is running.</span></span> <span data-ttu-id="5e185-164">Si vous souhaitez que le processus de hello tooterminate, utilisez hello `kill` avec l’id de processus hello.</span><span class="sxs-lookup"><span data-stu-id="5e185-164">If you want tooterminate hello process, use hello `kill` command with hello process id.</span></span>

1. <span data-ttu-id="5e185-165">Vous pouvez afficher le statut hello de mise à jour du microprogramme hello, comme indiqué par l’appareil de hello, dans le portail de solution hello.</span><span class="sxs-lookup"><span data-stu-id="5e185-165">You can view hello status of hello firmware update, as reported by hello device, in hello solution portal.</span></span> <span data-ttu-id="5e185-166">Hello capture d’écran suivante montre les état hello et durée de chaque étape du processus de mise à jour hello et la nouvelle version de microprogramme hello :</span><span class="sxs-lookup"><span data-stu-id="5e185-166">hello following screenshot shows hello status and duration of each stage of hello update process, and hello new firmware version:</span></span>

    ![Afficher l’état du travail][img-job-status]

    <span data-ttu-id="5e185-168">Si vous accédez à tableau de bord toohello précédent, vous pouvez vérifier le périphérique de hello envoie encore télémétrie après mise à jour du microprogramme hello.</span><span class="sxs-lookup"><span data-stu-id="5e185-168">If you navigate back toohello dashboard, you can verify hello device is still sending telemetry following hello firmware update.</span></span>

> [!WARNING]
> <span data-ttu-id="5e185-169">Si vous laissez hello solution en cours d’exécution dans votre compte Azure de surveillance à distance, vous êtes facturé pour hello exécution.</span><span class="sxs-lookup"><span data-stu-id="5e185-169">If you leave hello remote monitoring solution running in your Azure account, you are billed for hello time it runs.</span></span> <span data-ttu-id="5e185-170">Pour plus d’informations sur la réduction de la consommation lors hello s’exécute la solution de surveillance à distance, consultez [configuration Azure IoT Suite préconfiguré des solutions à des fins de démonstration][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="5e185-170">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span> <span data-ttu-id="5e185-171">Supprimer la solution de hello préconfiguré à partir de votre compte Azure lorsque vous avez terminé.</span><span class="sxs-lookup"><span data-stu-id="5e185-171">Delete hello preconfigured solution from your Azure account when you have finished using it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5e185-172">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5e185-172">Next steps</span></span>

<span data-ttu-id="5e185-173">Visitez hello [centre de développement Azure IoT](https://azure.microsoft.com/develop/iot/) pour plus d’exemples et documentation sur Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="5e185-173">Visit hello [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>


[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-node-get-started-advanced/app-output.png
[img-update-progress]: ./media/iot-suite-raspberry-pi-kit-node-get-started-advanced/updateprogress.png
[img-job-status]: ./media/iot-suite-raspberry-pi-kit-node-get-started-advanced/jobstatus.png
[img-list-devices]: ./media/iot-suite-raspberry-pi-kit-node-get-started-advanced/listdevices.png
[img-method-history]: ./media/iot-suite-raspberry-pi-kit-node-get-started-advanced/methodhistory.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
