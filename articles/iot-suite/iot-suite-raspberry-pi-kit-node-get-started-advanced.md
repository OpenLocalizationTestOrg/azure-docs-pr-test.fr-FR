---
title: "Connexion d’un Raspberry Pi à Azure IoT Suite à l’aide de Node.js pour prendre en charge les mises à jour du microprogramme | Microsoft Docs"
description: "Utilisez le Kit de démarrage Microsoft Azure IoT pour le Raspberry Pi 3 et IoT Azure Suite. Utilisez Node.js pour connecter votre Raspberry Pi à la solution de surveillance à distance, envoyer la télémétrie des capteurs dans le cloud et effectuer une mise à jour du microprogramme à distance."
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
ms.openlocfilehash: 54503d5d6a636239d240509d7d09cf334234bac7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="connect-your-raspberry-pi-3-to-the-remote-monitoring-solution-and-enable-remote-firmware-updates-using-nodejs"></a><span data-ttu-id="4d905-104">Connexion de votre Raspberry Pi 3 à la solution de surveillance à distance et activation des mises à jour de microprogramme à distance à l’aide de Node.js</span><span class="sxs-lookup"><span data-stu-id="4d905-104">Connect your Raspberry Pi 3 to the remote monitoring solution and enable remote firmware updates using Node.js</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

<span data-ttu-id="4d905-105">Ce didacticiel vous montre comment utiliser le Kit de démarrage Microsoft Azure IoT pour Raspberry Pi 3 pour :</span><span class="sxs-lookup"><span data-stu-id="4d905-105">This tutorial shows you how to use the Microsoft Azure IoT Starter Kit for Raspberry Pi 3 to:</span></span>

* <span data-ttu-id="4d905-106">développer un lecteur de température et d’humidité capable de communiquer avec le cloud ;</span><span class="sxs-lookup"><span data-stu-id="4d905-106">Develop a temperature and humidity reader that can communicate with the cloud.</span></span>
* <span data-ttu-id="4d905-107">activer et effectuer une mise à jour à distance du microprogramme pour mettre à jour l’application cliente sur le Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="4d905-107">Enable and perform a remote firmware update to update the client application on the Raspberry Pi.</span></span>

<span data-ttu-id="4d905-108">Le didacticiel utilise :</span><span class="sxs-lookup"><span data-stu-id="4d905-108">The tutorial uses:</span></span>

- <span data-ttu-id="4d905-109">Le système d’exploitation Raspbian, le langage de programmation Node.js et le Kit SDK Microsoft Azure IoT pour Node.js en vue d’implémenter un exemple d’appareil.</span><span class="sxs-lookup"><span data-stu-id="4d905-109">Raspbian OS, the Node.js programming language, and the Microsoft Azure IoT SDK for Node.js to implement a sample device.</span></span>
- <span data-ttu-id="4d905-110">La solution préconfigurée de surveillance à distance Azure IoT Suite comme backend basé sur le cloud.</span><span class="sxs-lookup"><span data-stu-id="4d905-110">The IoT Suite remote monitoring preconfigured solution as the cloud-based back end.</span></span>

## <a name="overview"></a><span data-ttu-id="4d905-111">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="4d905-111">Overview</span></span>

<span data-ttu-id="4d905-112">Dans ce didacticiel, vous allez effectuer les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="4d905-112">In this tutorial, you complete the following steps:</span></span>

- <span data-ttu-id="4d905-113">Déployer une instance de la solution préconfigurée de surveillance à distance dans votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="4d905-113">Deploy an instance of the remote monitoring preconfigured solution to your Azure subscription.</span></span> <span data-ttu-id="4d905-114">Cette étape déploie et configure automatiquement plusieurs services Azure.</span><span class="sxs-lookup"><span data-stu-id="4d905-114">This step automatically deploys and configures multiple Azure services.</span></span>
- <span data-ttu-id="4d905-115">Configurer votre appareil pour qu’il communique avec votre ordinateur et avec la solution de surveillance à distance.</span><span class="sxs-lookup"><span data-stu-id="4d905-115">Set up your device and sensors to communicate with your computer and the remote monitoring solution.</span></span>
- <span data-ttu-id="4d905-116">Mettre à jour l’exemple de code d’appareil pour se connecter à la solution de surveillance à distance et envoyer les données de télémétrie que vous pouvez afficher sur le tableau de bord de la solution.</span><span class="sxs-lookup"><span data-stu-id="4d905-116">Update the sample device code to connect to the remote monitoring solution, and send telemetry that you can view on the solution dashboard.</span></span>
- <span data-ttu-id="4d905-117">Utiliser l’exemple de code d’appareil pour mettre à jour l’application cliente.</span><span class="sxs-lookup"><span data-stu-id="4d905-117">Use the sample device code to update the client application.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-prerequisites](../../includes/iot-suite-raspberry-pi-kit-prerequisites.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="4d905-118">La solution de surveillance à distance configure un ensemble de services Azure dans votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="4d905-118">The remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="4d905-119">Le déploiement reflète une architecture d’entreprise réelle.</span><span class="sxs-lookup"><span data-stu-id="4d905-119">The deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="4d905-120">Pour éviter des frais de consommation Azure inutiles, supprimez votre instance de la solution préconfigurée dans azureiotsuite.com quand vous ne l’utilisez plus.</span><span class="sxs-lookup"><span data-stu-id="4d905-120">To avoid unnecessary Azure consumption charges, delete your instance of the preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="4d905-121">Si vous avez à nouveau besoin de la solution préconfigurée, vous pouvez la recréer facilement.</span><span class="sxs-lookup"><span data-stu-id="4d905-121">If you need the preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="4d905-122">Pour plus d’informations sur la manière de réduire votre consommation pendant l’exécution de la solution de surveillance à distance, consultez [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config] (Configuration des solutions préconfigurées Azure IoT Suite à des fins de démonstration).</span><span class="sxs-lookup"><span data-stu-id="4d905-122">For more information about reducing consumption while the remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi](../../includes/iot-suite-raspberry-pi-kit-prepare-pi.md)]

## <a name="download-and-configure-the-sample"></a><span data-ttu-id="4d905-123">Télécharger et configurer l’exemple</span><span class="sxs-lookup"><span data-stu-id="4d905-123">Download and configure the sample</span></span>

<span data-ttu-id="4d905-124">Vous pouvez à présent télécharger et configurer l’application cliente de surveillance à distance sur votre Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="4d905-124">You can now download and configure the remote monitoring client application on your Raspberry Pi.</span></span>

### <a name="install-nodejs"></a><span data-ttu-id="4d905-125">Installer Node.js</span><span class="sxs-lookup"><span data-stu-id="4d905-125">Install Node.js</span></span>

<span data-ttu-id="4d905-126">Si vous ne l’avez pas déjà fait, installez Node.js sur votre Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="4d905-126">If you haven't done so already, install Node.js on your Raspberry Pi.</span></span> <span data-ttu-id="4d905-127">Le kit de développement logiciel (SDK) IoT pour Node.js requiert la version 0.11.5 de Node.js ou une version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="4d905-127">The IoT SDK for Node.js requires version 0.11.5 of Node.js or later.</span></span> <span data-ttu-id="4d905-128">Les étapes suivantes vous montrent comment installer Node.js v6.10.2 sur votre Raspberry Pi :</span><span class="sxs-lookup"><span data-stu-id="4d905-128">The following steps show you how to install Node.js v6.10.2 on your Raspberry Pi:</span></span>

1. <span data-ttu-id="4d905-129">Pour mettre à jour votre Raspberry Pi, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="4d905-129">Use the following command to update your Raspberry Pi:</span></span>

    ```sh
    sudo apt-get update
    ```

1. <span data-ttu-id="4d905-130">Pour télécharger les fichiers binaires Node.js sur votre Raspberry Pi, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="4d905-130">Use the following command to download the Node.js binaries to your Raspberry Pi:</span></span>

    ```sh
    wget https://nodejs.org/dist/v6.10.2/node-v6.10.2-linux-armv7l.tar.gz
    ```

1. <span data-ttu-id="4d905-131">Pour installer les binaires, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="4d905-131">Use the following command to install the binaries:</span></span>

    ```sh
    sudo tar -C /usr/local --strip-components 1 -xzf node-v6.10.2-linux-armv7l.tar.gz
    ```

1. <span data-ttu-id="4d905-132">Pour vérifier que Node.js v6.10.2 a été installé avec succès, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="4d905-132">Use the following command to verify you have installed Node.js v6.10.2 successfully:</span></span>

    ```sh
    node --version
    ```

### <a name="clone-the-repositories"></a><span data-ttu-id="4d905-133">Cloner les dépôts</span><span class="sxs-lookup"><span data-stu-id="4d905-133">Clone the repositories</span></span>

<span data-ttu-id="4d905-134">Si vous ne l’avez pas déjà fait, clonez les dépôts requis en exécutant les commandes suivantes sur votre Pi :</span><span class="sxs-lookup"><span data-stu-id="4d905-134">If you haven't done so already, clone the required repositories by running the following commands on your Pi:</span></span>

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-node-raspberrypi-getstartedkit.git
```

### <a name="update-the-device-connection-string"></a><span data-ttu-id="4d905-135">Mettre à jour la chaîne de connexion d’appareil</span><span class="sxs-lookup"><span data-stu-id="4d905-135">Update the device connection string</span></span>

<span data-ttu-id="4d905-136">Ouvrez l’exemple de fichier de configuration dans l’éditeur **nano** à l’aide de la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="4d905-136">Open the sample configuration file in the **nano** editor using the following command:</span></span>

```sh
nano ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/advanced/config/deviceinfo
```

<span data-ttu-id="4d905-137">Remplacez les valeurs dans l’espace réservé par les informations sur l’appareil et l’IoT Hub que vous avez créées et enregistrées au début de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="4d905-137">Replace the placeholder values with the device id and IoT Hub information you created and saved at the start of this tutorial.</span></span>

<span data-ttu-id="4d905-138">Lorsque vous avez terminé, le contenu du fichier deviceinfo doit ressembler à l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="4d905-138">When you are done, the contents of the deviceinfo file should look like the following example:</span></span>

```conf
yourdeviceid
HostName=youriothubname.azure-devices.net;DeviceId=yourdeviceid;SharedAccessKey=yourdevicekey
```

<span data-ttu-id="4d905-139">Enregistrez vos modifications (**Ctrl-O**, **Entrée**) et quittez l’éditeur (**Ctrl-X**).</span><span class="sxs-lookup"><span data-stu-id="4d905-139">Save your changes (**Ctrl-O**, **Enter**) and exit the editor (**Ctrl-X**).</span></span>

## <a name="run-the-sample"></a><span data-ttu-id="4d905-140">Exécution de l'exemple</span><span class="sxs-lookup"><span data-stu-id="4d905-140">Run the sample</span></span>

<span data-ttu-id="4d905-141">Exécutez les commandes suivantes pour installer les packages requis pour l’exemple :</span><span class="sxs-lookup"><span data-stu-id="4d905-141">Run the following commands to install the prerequisite packages for the sample:</span></span>

```sh
cd ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/advance/1.0
npm install
```

<span data-ttu-id="4d905-142">Vous pouvez maintenant exécuter l’exemple de programme sur le Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="4d905-142">You can now run the sample program on the Raspberry Pi.</span></span> <span data-ttu-id="4d905-143">Entrez la commande :</span><span class="sxs-lookup"><span data-stu-id="4d905-143">Enter the command:</span></span>

```sh
sudo node ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/advanced/1.0/remote_monitoring.js
```

<span data-ttu-id="4d905-144">La sortie suivante est un exemple de sortie qui peut s’afficher à l’invite de commandes sur le Raspberry Pi :</span><span class="sxs-lookup"><span data-stu-id="4d905-144">The following sample output is an example of the output you see at the command prompt on the Raspberry Pi:</span></span>

![Sortie de l’application de Raspberry Pi][img-raspberry-output]

<span data-ttu-id="4d905-146">Appuyez sur **Ctrl-C** pour quitter le programme à tout moment.</span><span class="sxs-lookup"><span data-stu-id="4d905-146">Press **Ctrl-C** to exit the program at any time.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry-advanced](../../includes/iot-suite-raspberry-pi-kit-view-telemetry-advanced.md)]

1. <span data-ttu-id="4d905-147">Dans le tableau de bord de la solution, cliquez sur **Appareils** pour accéder à la page **Appareils**.</span><span class="sxs-lookup"><span data-stu-id="4d905-147">In the solution dashboard, click **Devices** to visit the **Devices** page.</span></span> <span data-ttu-id="4d905-148">Sélectionnez votre Raspberry Pi dans la **Liste des appareils**.</span><span class="sxs-lookup"><span data-stu-id="4d905-148">Select your Raspberry Pi in the **Device List**.</span></span> <span data-ttu-id="4d905-149">Ensuite, choisissez **Méthodes** :</span><span class="sxs-lookup"><span data-stu-id="4d905-149">Then choose **Methods**:</span></span>

    ![Liste des appareils dans le tableau de bord][img-list-devices]

1. <span data-ttu-id="4d905-151">Sur la page **Appeler une méthode**, choisissez **InitiateFirmwareUpdate** dans la liste déroulante **Méthode**.</span><span class="sxs-lookup"><span data-stu-id="4d905-151">On the **Invoke Method** page, choose **InitiateFirmwareUpdate** in the **Method** dropdown.</span></span>

1. <span data-ttu-id="4d905-152">Dans le champ **FWPackageURI**, entrez **https://raw.githubusercontent.com/Azure-Samples/iot-remote-monitoring-node-raspberrypi-getstartedkit/master/advanced/2.0/raspberry.js**.</span><span class="sxs-lookup"><span data-stu-id="4d905-152">In the **FWPackageURI** field, enter **https://raw.githubusercontent.com/Azure-Samples/iot-remote-monitoring-node-raspberrypi-getstartedkit/master/advanced/2.0/raspberry.js**.</span></span> <span data-ttu-id="4d905-153">Ce fichier contient l’implémentation de la version 2.0 du microprogramme.</span><span class="sxs-lookup"><span data-stu-id="4d905-153">This file contains the implementation of version 2.0 of the firmware.</span></span>

1. <span data-ttu-id="4d905-154">Choisissez **InvokeMethod**.</span><span class="sxs-lookup"><span data-stu-id="4d905-154">Choose **InvokeMethod**.</span></span> <span data-ttu-id="4d905-155">L’application sur le Raspberry Pi envoie un accusé de réception au tableau de bord de la solution.</span><span class="sxs-lookup"><span data-stu-id="4d905-155">The app on the Raspberry Pi sends an acknowledgment back to the solution dashboard.</span></span> <span data-ttu-id="4d905-156">Elle démarre ensuite le processus de mise à jour du microprogramme en téléchargeant la nouvelle version de ce dernier :</span><span class="sxs-lookup"><span data-stu-id="4d905-156">It then starts the firmware update process by downloading the new version of the firmware:</span></span>

    ![Afficher l’historique de la méthode][img-method-history]

## <a name="observe-the-firmware-update-process"></a><span data-ttu-id="4d905-158">Observer le microprogramme des mises à jour</span><span class="sxs-lookup"><span data-stu-id="4d905-158">Observe the firmware update process</span></span>

<span data-ttu-id="4d905-159">Vous pouvez observer le processus de mise à jour du microprogramme en cours d’exécution sur l’appareil et en affichant les propriétés déclarées dans le tableau de bord de solution :</span><span class="sxs-lookup"><span data-stu-id="4d905-159">You can observe the firmware update process as it runs on the device and by viewing the reported properties in the solution dashboard:</span></span>

1. <span data-ttu-id="4d905-160">Vous pouvez afficher la progression du processus de mise à jour sur le Raspberry Pi :</span><span class="sxs-lookup"><span data-stu-id="4d905-160">You can view the progress in of the update process on the Raspberry Pi:</span></span>

    ![Afficher la progression de la mise à jour][img-update-progress]

    > [!NOTE]
    > <span data-ttu-id="4d905-162">L’application de surveillance à distance redémarre en mode silencieux à l’issue de la mise à jour.</span><span class="sxs-lookup"><span data-stu-id="4d905-162">The remote monitoring app restarts silently when the update completes.</span></span> <span data-ttu-id="4d905-163">Utilisez la commande `ps -ef` pour vérifier qu’elle est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="4d905-163">Use the command `ps -ef` to verify it is running.</span></span> <span data-ttu-id="4d905-164">Si vous souhaitez mettre fin au processus, utilisez la commande `kill` avec l’ID de processus.</span><span class="sxs-lookup"><span data-stu-id="4d905-164">If you want to terminate the process, use the `kill` command with the process id.</span></span>

1. <span data-ttu-id="4d905-165">Vous pouvez afficher l’état de la mise à jour du microprogramme, comme indiqué par l’appareil, dans le portail de la solution.</span><span class="sxs-lookup"><span data-stu-id="4d905-165">You can view the status of the firmware update, as reported by the device, in the solution portal.</span></span> <span data-ttu-id="4d905-166">La capture d’écran suivante montre l’état et la durée de chaque étape du processus de mise à jour, ainsi que la nouvelle version du microprogramme :</span><span class="sxs-lookup"><span data-stu-id="4d905-166">The following screenshot shows the status and duration of each stage of the update process, and the new firmware version:</span></span>

    ![Afficher l’état du travail][img-job-status]

    <span data-ttu-id="4d905-168">Si vous accédez de nouveau au tableau de bord, vous pouvez vérifier que l’appareil continue d’envoyer la télémétrie après la mise à jour du microprogramme.</span><span class="sxs-lookup"><span data-stu-id="4d905-168">If you navigate back to the dashboard, you can verify the device is still sending telemetry following the firmware update.</span></span>

> [!WARNING]
> <span data-ttu-id="4d905-169">Si vous quittez la solution de surveillance à distance en cours d’exécution dans votre compte Azure, vous êtes facturé en fonction du temps d’exécution.</span><span class="sxs-lookup"><span data-stu-id="4d905-169">If you leave the remote monitoring solution running in your Azure account, you are billed for the time it runs.</span></span> <span data-ttu-id="4d905-170">Pour plus d’informations sur la manière de réduire votre consommation pendant l’exécution de la solution de surveillance à distance, consultez [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config] (Configuration des solutions préconfigurées Azure IoT Suite à des fins de démonstration).</span><span class="sxs-lookup"><span data-stu-id="4d905-170">For more information about reducing consumption while the remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span> <span data-ttu-id="4d905-171">Supprimez la solution préconfigurée de votre compte Azure lorsque vous avez fini de l’utiliser.</span><span class="sxs-lookup"><span data-stu-id="4d905-171">Delete the preconfigured solution from your Azure account when you have finished using it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4d905-172">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4d905-172">Next steps</span></span>

<span data-ttu-id="4d905-173">Visitez le [Centre de développement Azure IoT](https://azure.microsoft.com/develop/iot/) pour d’autres exemples et de la documentation complémentaire sur Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="4d905-173">Visit the [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>


[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-node-get-started-advanced/app-output.png
[img-update-progress]: ./media/iot-suite-raspberry-pi-kit-node-get-started-advanced/updateprogress.png
[img-job-status]: ./media/iot-suite-raspberry-pi-kit-node-get-started-advanced/jobstatus.png
[img-list-devices]: ./media/iot-suite-raspberry-pi-kit-node-get-started-advanced/listdevices.png
[img-method-history]: ./media/iot-suite-raspberry-pi-kit-node-get-started-advanced/methodhistory.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
