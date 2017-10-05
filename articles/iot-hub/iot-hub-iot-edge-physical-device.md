---
title: Utiliser un appareil physique avec Azure IoT Edge | Microsoft Docs
description: "Guide pratique d’utilisation d’un appareil SensorTag de Texas Instruments pour envoyer des données à un IoT Hub via une passerelle IoT Edge s’exécutant sur un Raspberry Pi 3. La passerelle est créée à l’aide d’Azure IoT Edge."
services: iot-hub
documentationcenter: 
author: chipalost
manager: timlt
editor: 
ms.assetid: 212dacbf-e5e9-48b2-9c8a-1c14d9e7b913
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/12/2017
ms.author: andbuc
ms.openlocfilehash: 02962a91c739a53dfcf947bcc736e5c293b9384f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-iot-edge-on-a-raspberry-pi-to-forward-device-to-cloud-messages-to-iot-hub"></a><span data-ttu-id="202a1-104">Utiliser Azure IoT Edge sur un Raspberry Pi pour transférer les messages Appareil vers cloud à IoT Hub</span><span class="sxs-lookup"><span data-stu-id="202a1-104">Use Azure IoT Edge on a Raspberry Pi to forward device-to-cloud messages to IoT Hub</span></span>

<span data-ttu-id="202a1-105">Cette procédure pas à pas de [l’exemple à faible consommation d’énergie Bluetooth][lnk-ble-samplecode] vous montre comment utiliser [la passerelle Azure IoT Edge][lnk-sdk] pour :</span><span class="sxs-lookup"><span data-stu-id="202a1-105">This walkthrough of the [Bluetooth low energy sample][lnk-ble-samplecode] shows you how to use [Azure IoT Edge][lnk-sdk] to:</span></span>

* <span data-ttu-id="202a1-106">Transférer la télémétrie appareil-vers-cloud vers IoT Hub à partir d’un appareil physique.</span><span class="sxs-lookup"><span data-stu-id="202a1-106">Forward device-to-cloud telemetry to IoT Hub from a physical device.</span></span>
* <span data-ttu-id="202a1-107">Achemine les commandes vers un appareil physique à partir d’IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="202a1-107">Route commands from IoT Hub to a physical device.</span></span>

<span data-ttu-id="202a1-108">Cette procédure pas à pas inclut les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="202a1-108">This walkthrough covers:</span></span>

* <span data-ttu-id="202a1-109">**Architecture**: informations architecturales importantes concernant l'exemple à faible consommation d’énergie Bluetooth.</span><span class="sxs-lookup"><span data-stu-id="202a1-109">**Architecture**: important architectural information about the Bluetooth low energy sample.</span></span>
* <span data-ttu-id="202a1-110">**Créer et exécuter**: les étapes requises pour créer et exécuter l’exemple.</span><span class="sxs-lookup"><span data-stu-id="202a1-110">**Build and run**: the steps required to build and run the sample.</span></span>

## <a name="architecture"></a><span data-ttu-id="202a1-111">Architecture</span><span class="sxs-lookup"><span data-stu-id="202a1-111">Architecture</span></span>

<span data-ttu-id="202a1-112">La procédure pas à pas vous montre comment générer et exécuter une passerelle IoT Edge sur un Raspberry Pi 3 exécutant Raspbian Linux.</span><span class="sxs-lookup"><span data-stu-id="202a1-112">The walkthrough shows you how to build and run an IoT Edge gateway on a Raspberry Pi 3 that runs Raspbian Linux.</span></span> <span data-ttu-id="202a1-113">La passerelle est créée à l’aide d’IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="202a1-113">The gateway is built using IoT Edge.</span></span> <span data-ttu-id="202a1-114">L’exemple utilise un appareil Texas Instruments SensorTag Bluetooth Low Energy (BLE) pour collecter des données de température.</span><span class="sxs-lookup"><span data-stu-id="202a1-114">The sample uses a Texas Instruments SensorTag Bluetooth Low Energy (BLE) device to collect temperature data.</span></span>

<span data-ttu-id="202a1-115">Lorsque vous exécutez la passerelle IoT Edge, celle-ci :</span><span class="sxs-lookup"><span data-stu-id="202a1-115">When you run the IoT Edge gateway it:</span></span>

* <span data-ttu-id="202a1-116">Se connecte à un appareil SensorTag à l’aide du protocole Bluetooth Low Energy (BLE).</span><span class="sxs-lookup"><span data-stu-id="202a1-116">Connects to a SensorTag device using the Bluetooth Low Energy (BLE) protocol.</span></span>
* <span data-ttu-id="202a1-117">Se connecte à IoT Hub à l’aide du protocole HTTP.</span><span class="sxs-lookup"><span data-stu-id="202a1-117">Connects to IoT Hub using the HTTP protocol.</span></span>
* <span data-ttu-id="202a1-118">Transfère les données de télémétrie à partir de l’appareil SensorTag vers IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="202a1-118">Forwards telemetry from the SensorTag device to IoT Hub.</span></span>
* <span data-ttu-id="202a1-119">Achemine les commandes vers l’appareil SensorTag à partir d’IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="202a1-119">Routes commands from IoT Hub to the SensorTag device.</span></span>

<span data-ttu-id="202a1-120">La passerelle contient les modules IoT Edge suivants :</span><span class="sxs-lookup"><span data-stu-id="202a1-120">The gateway contains the following IoT Edge modules:</span></span>

* <span data-ttu-id="202a1-121">Un *module BLE* qui interagit avec un appareil BLE pour recevoir les données de température à partir de l’appareil et envoyer des commandes à l’appareil.</span><span class="sxs-lookup"><span data-stu-id="202a1-121">A *BLE module* that interfaces with a BLE device to receive temperature data from the device and send commands to the device.</span></span>
* <span data-ttu-id="202a1-122">Un *module cloud-à-appareil BLE* qui traduit les messages JSON provenant d’IoT Hub en instructions BLE pour le *module BLE*.</span><span class="sxs-lookup"><span data-stu-id="202a1-122">A *BLE cloud to device module* that translates JSON messages sent from IoT Hub into BLE instructions for the *BLE module*.</span></span>
* <span data-ttu-id="202a1-123">Un *module enregistreur* qui journalise tous les messages de la passerelle dans un fichier local.</span><span class="sxs-lookup"><span data-stu-id="202a1-123">A *logger module* that logs all gateway messages to a local file.</span></span>
* <span data-ttu-id="202a1-124">Un *module de mappage d’identité* qui effectue la traduction entre les adresses MAC de l’appareil BLE et les identités des appareils Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="202a1-124">An *identity mapping module* that translates between BLE device MAC addresses and Azure IoT Hub device identities.</span></span>
* <span data-ttu-id="202a1-125">Un *module IoT Hub* qui transfère les données de télémétrie sur un hub IoT et reçoit les commandes de l’appareil à partir d’un hub IoT.</span><span class="sxs-lookup"><span data-stu-id="202a1-125">An *IoT Hub module* that uploads telemetry data to an IoT hub and receives device commands from an IoT hub.</span></span>
* <span data-ttu-id="202a1-126">Un *module d’imprimante BLE* qui interprète les données de télémétrie fournies par l’appareil BLE et imprime des données mises en forme sur la console pour permettre la résolution des problèmes et le débogage.</span><span class="sxs-lookup"><span data-stu-id="202a1-126">A *BLE printer module* that interprets telemetry from the BLE device and prints formatted data to the console to enable troubleshooting and debugging.</span></span>

### <a name="how-data-flows-through-the-gateway"></a><span data-ttu-id="202a1-127">Flux des données sur la passerelle</span><span class="sxs-lookup"><span data-stu-id="202a1-127">How data flows through the gateway</span></span>

<span data-ttu-id="202a1-128">Le diagramme de blocs suivant illustre le pipeline du flux de téléchargement des données de télémétrie :</span><span class="sxs-lookup"><span data-stu-id="202a1-128">The following block diagram illustrates the telemetry upload data flow pipeline:</span></span>

![Pipeline de passerelle de téléchargement de télémétrie](media/iot-hub-iot-edge-physical-device/gateway_ble_upload_data_flow.png)

<span data-ttu-id="202a1-130">Les étapes qu’un élément de télémétrie suit lors de son transfert entre un appareil BLE et IoT Hub sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="202a1-130">The steps that an item of telemetry takes traveling from a BLE device to IoT Hub are:</span></span>

1. <span data-ttu-id="202a1-131">L’appareil BLE génère un exemple de température et l’envoie au module BLE de la passerelle via Bluetooth.</span><span class="sxs-lookup"><span data-stu-id="202a1-131">The BLE device generates a temperature sample and sends it over Bluetooth to the BLE module in the gateway.</span></span>
1. <span data-ttu-id="202a1-132">Le module BLE reçoit l’exemple et le publie dans le répartiteur avec l’adresse MAC de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="202a1-132">The BLE module receives the sample and publishes it to the broker along with the MAC address of the device.</span></span>
1. <span data-ttu-id="202a1-133">Le module de mappage d’identité récupère ce message et utilise une table interne pour convertir l’adresse MAC de l’appareil en une identité d’appareil IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="202a1-133">The identity mapping module picks up this message and uses an internal table to translate the MAC address of the device into an IoT Hub device identity.</span></span> <span data-ttu-id="202a1-134">Une identité d’appareil IoT Hub se compose d’un ID d’appareil et d’une clé d’appareil.</span><span class="sxs-lookup"><span data-stu-id="202a1-134">An IoT Hub device identity consists of a device ID and device key.</span></span>
1. <span data-ttu-id="202a1-135">Le module de mappage d’identité publie un nouveau message contenant les exemples de données de température, l’adresse MAC de l’appareil, l’ID de l’appareil et la clé de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="202a1-135">The identity mapping module publishes a new message that contains the temperature sample data, the MAC address of the device, the device ID, and the device key.</span></span>
1. <span data-ttu-id="202a1-136">Le module IoT Hub reçoit ce nouveau message (généré par le module de mappage d’identité) et le publie dans IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="202a1-136">The IoT Hub module receives this new message (generated by the identity mapping module) and publishes it to IoT Hub.</span></span>
1. <span data-ttu-id="202a1-137">Le module enregistreur journalise tous les messages reçus du répartiteur dans un fichier local.</span><span class="sxs-lookup"><span data-stu-id="202a1-137">The logger module logs all messages from the broker to a local file.</span></span>

<span data-ttu-id="202a1-138">Le diagramme de blocs suivant illustre le pipeline du flux des données de commandes de l’appareil :</span><span class="sxs-lookup"><span data-stu-id="202a1-138">The following block diagram illustrates the device command data flow pipeline:</span></span>

![Pipeline de passerelle de commande d’appareil](media/iot-hub-iot-edge-physical-device/gateway_ble_command_data_flow.png)

1. <span data-ttu-id="202a1-140">Le module IoT Hub interroge régulièrement IoT Hub pour savoir s’il existe de nouveaux messages de commande.</span><span class="sxs-lookup"><span data-stu-id="202a1-140">The IoT Hub module periodically polls the IoT hub for new command messages.</span></span>
1. <span data-ttu-id="202a1-141">Lorsque le module IoT Hub reçoit un nouveau message de commande, il le publie sur le répartiteur.</span><span class="sxs-lookup"><span data-stu-id="202a1-141">When the IoT Hub module receives a new command message, it publishes it to the broker.</span></span>
1. <span data-ttu-id="202a1-142">Le module de mappage d’identité récupère le message de commande et utilise une table interne pour convertir l’ID d’appareil IoT Hub en adresse MAC d’appareil.</span><span class="sxs-lookup"><span data-stu-id="202a1-142">The identity mapping module picks up the command message and uses an internal table to translate the IoT Hub device ID to a device MAC address.</span></span> <span data-ttu-id="202a1-143">Il publie ensuite un nouveau message contenant l’adresse MAC de l’appareil cible dans le mappage des propriétés du message.</span><span class="sxs-lookup"><span data-stu-id="202a1-143">It then publishes a new message that includes the MAC address of the target device in the properties map of the message.</span></span>
1. <span data-ttu-id="202a1-144">Le module cloud-à-appareil BLE récupère ce message et le traduit dans l’instruction BLE appropriée pour le module BLE.</span><span class="sxs-lookup"><span data-stu-id="202a1-144">The BLE Cloud-to-Device module picks up this message and translates it into the proper BLE instruction for the BLE module.</span></span> <span data-ttu-id="202a1-145">Il publie ensuite un nouveau message.</span><span class="sxs-lookup"><span data-stu-id="202a1-145">It then publishes a new message.</span></span>
1. <span data-ttu-id="202a1-146">Le module BLE récupère ce message et exécute l’instruction d’E/S en communiquant avec l’appareil BLE.</span><span class="sxs-lookup"><span data-stu-id="202a1-146">The BLE module picks up this message and executes the I/O instruction by communicating with the BLE device.</span></span>
1. <span data-ttu-id="202a1-147">Le module enregistreur consigne tous les messages reçus du répartiteur dans un fichier sur le disque.</span><span class="sxs-lookup"><span data-stu-id="202a1-147">The logger module logs all messages from the broker to a disk file.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="202a1-148">Composants requis</span><span class="sxs-lookup"><span data-stu-id="202a1-148">Prerequisites</span></span>

<span data-ttu-id="202a1-149">Pour suivre ce didacticiel, vous avez besoin d’un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="202a1-149">To complete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="202a1-150">Si vous ne possédez pas de compte, vous pouvez créer un compte d’évaluation gratuit en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="202a1-150">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="202a1-151">Pour plus d’informations, consultez la rubrique [Version d’évaluation gratuite d’Azure][lnk-free-trial].</span><span class="sxs-lookup"><span data-stu-id="202a1-151">For details, see [Azure Free Trial][lnk-free-trial].</span></span>

<span data-ttu-id="202a1-152">Vous devez installer le client SSH sur votre ordinateur de bureau afin de pouvoir accéder à distance à la ligne de commande sur le Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="202a1-152">You need SSH client on your desktop machine to enable you to remotely access the command line on the Raspberry Pi.</span></span>

- <span data-ttu-id="202a1-153">Windows n’inclut pas de client SSH.</span><span class="sxs-lookup"><span data-stu-id="202a1-153">Windows does not include an SSH client.</span></span> <span data-ttu-id="202a1-154">Nous vous recommandons d’utiliser [PuTTY](http://www.putty.org/).</span><span class="sxs-lookup"><span data-stu-id="202a1-154">We recommend using [PuTTY](http://www.putty.org/).</span></span>
- <span data-ttu-id="202a1-155">La plupart des distributions Linux et Mac OS incluent l’utilitaire de ligne de commande SSH.</span><span class="sxs-lookup"><span data-stu-id="202a1-155">Most Linux distributions and Mac OS include the command-line SSH utility.</span></span> <span data-ttu-id="202a1-156">Pour plus d’informations, consultez [SSH Using Linux or Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md) (Utilisation de SSH avec Linux ou Mac OS).</span><span class="sxs-lookup"><span data-stu-id="202a1-156">For more information, see [SSH Using Linux or Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md).</span></span>

## <a name="prepare-your-hardware"></a><span data-ttu-id="202a1-157">Préparation du matériel</span><span class="sxs-lookup"><span data-stu-id="202a1-157">Prepare your hardware</span></span>

<span data-ttu-id="202a1-158">Ce didacticiel suppose que vous utilisez un appareil [SensorTag de Texas Instruments](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/index.html) connecté à un Raspberry Pi 3 exécutant Raspbian.</span><span class="sxs-lookup"><span data-stu-id="202a1-158">This tutorial assumes you are using a [Texas Instruments SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/index.html) device connected to a Raspberry Pi 3 running Raspbian.</span></span>

### <a name="install-raspbian"></a><span data-ttu-id="202a1-159">Installer Raspbian</span><span class="sxs-lookup"><span data-stu-id="202a1-159">Install Raspbian</span></span>

<span data-ttu-id="202a1-160">Vous pouvez utiliser l’une des options suivantes pour installer Raspbian sur votre appareil Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="202a1-160">You can use either of the following options to install Raspbian on your Raspberry Pi 3 device.</span></span>

* <span data-ttu-id="202a1-161">Utilisez l’interface utilisateur graphique [NOOBS][lnk-noobs] pour installer la dernière version de Raspbian.</span><span class="sxs-lookup"><span data-stu-id="202a1-161">To install the latest version of Raspbian, use the [NOOBS][lnk-noobs] graphical user interface.</span></span>
* <span data-ttu-id="202a1-162">[Téléchargez][lnk-raspbian] Manuellement et écrivez la dernière image du système d’exploitation Raspbian sur une carte SD.</span><span class="sxs-lookup"><span data-stu-id="202a1-162">Manually [download][lnk-raspbian] and write the latest image of the Raspbian operating system to an SD card.</span></span>

### <a name="sign-in-and-access-the-terminal"></a><span data-ttu-id="202a1-163">Se connecter et accéder au terminal</span><span class="sxs-lookup"><span data-stu-id="202a1-163">Sign in and access the terminal</span></span>

<span data-ttu-id="202a1-164">Deux méthodes vous permettent d’accéder à un environnement de type terminal sur votre Raspberry Pi :</span><span class="sxs-lookup"><span data-stu-id="202a1-164">You have two options to access a terminal environment on your Raspberry Pi:</span></span>

* <span data-ttu-id="202a1-165">Si vous disposez d’un clavier et d’un moniteur connectés à votre Raspberry Pi, vous pouvez utiliser l’interface utilisateur graphique Raspbian pour accéder à une fenêtre de terminal.</span><span class="sxs-lookup"><span data-stu-id="202a1-165">If you have a keyboard and monitor connected to your Raspberry Pi, you can use the Raspbian GUI to access a terminal window.</span></span>

* <span data-ttu-id="202a1-166">Accédez à la ligne de commande sur votre Raspberry Pi à l’aide de SSH à partir de votre ordinateur de bureau.</span><span class="sxs-lookup"><span data-stu-id="202a1-166">Access the command line on your Raspberry Pi using SSH from your desktop machine.</span></span>

#### <a name="use-a-terminal-window-in-the-gui"></a><span data-ttu-id="202a1-167">Utiliser une fenêtre de terminal dans l’interface utilisateur graphique</span><span class="sxs-lookup"><span data-stu-id="202a1-167">Use a terminal Window in the GUI</span></span>

<span data-ttu-id="202a1-168">Les informations d’identification par défaut pour Raspbian sont le nom d’utilisateur **pi** et le mot de passe **raspberry**.</span><span class="sxs-lookup"><span data-stu-id="202a1-168">The default credentials for Raspbian are username **pi** and password **raspberry**.</span></span> <span data-ttu-id="202a1-169">Dans la barre des tâches dans l’interface utilisateur graphique, vous pouvez lancer l’utilitaire **Terminal** à l’aide de l’icône qui ressemble à un moniteur.</span><span class="sxs-lookup"><span data-stu-id="202a1-169">In the task bar in the GUI, you can launch the **Terminal** utility using the icon that looks like a monitor.</span></span>

#### <a name="sign-in-with-ssh"></a><span data-ttu-id="202a1-170">Se connecter avec SSH</span><span class="sxs-lookup"><span data-stu-id="202a1-170">Sign in with SSH</span></span>

<span data-ttu-id="202a1-171">Vous pouvez utiliser SSH pour accéder à l’aide de la ligne de commande à votre Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="202a1-171">You can use SSH for command-line access to your Raspberry Pi.</span></span> <span data-ttu-id="202a1-172">L’article [SSH (Secure Shell)][lnk-pi-ssh] décrit la configuration de SSH sur votre Raspberry Pi et la connexion à partir des systèmes d’exploitation [Windows][lnk-ssh-windows] ou [Linux et Mac][lnk-ssh-linux].</span><span class="sxs-lookup"><span data-stu-id="202a1-172">The article [SSH (Secure Shell)][lnk-pi-ssh] describes how to configure SSH on your Raspberry Pi, and how to connect from [Windows][lnk-ssh-windows] or [Linux & Mac OS][lnk-ssh-linux].</span></span>

<span data-ttu-id="202a1-173">Connectez-vous avec le nom d’utilisateur **pi** et le mot de passe **raspberry**.</span><span class="sxs-lookup"><span data-stu-id="202a1-173">Sign in with username **pi** and password **raspberry**.</span></span>

### <a name="install-bluez-537"></a><span data-ttu-id="202a1-174">Installer BlueZ 5.37</span><span class="sxs-lookup"><span data-stu-id="202a1-174">Install BlueZ 5.37</span></span>

<span data-ttu-id="202a1-175">Les modules BLE communiquent avec le matériel Bluetooth via la pile BlueZ.</span><span class="sxs-lookup"><span data-stu-id="202a1-175">The BLE modules talk to the Bluetooth hardware via the BlueZ stack.</span></span> <span data-ttu-id="202a1-176">Pour que les modules fonctionnent correctement, vous avez besoin de la version 5.37 de BlueZ.</span><span class="sxs-lookup"><span data-stu-id="202a1-176">You need version 5.37 of BlueZ for the modules to work correctly.</span></span> <span data-ttu-id="202a1-177">En suivant ces instructions, vous êtes assuré que la version installée de BlueZ est correcte.</span><span class="sxs-lookup"><span data-stu-id="202a1-177">These instructions make sure the correct version of BlueZ is installed.</span></span>

1. <span data-ttu-id="202a1-178">Arrêtez le démon Bluetooth actuel :</span><span class="sxs-lookup"><span data-stu-id="202a1-178">Stop the current bluetooth daemon:</span></span>

    ```sh
    sudo systemctl stop bluetooth
    ```

1. <span data-ttu-id="202a1-179">Installez les dépendances BlueZ :</span><span class="sxs-lookup"><span data-stu-id="202a1-179">Install the BlueZ dependencies:</span></span>

    ```sh
    sudo apt-get update
    sudo apt-get install bluetooth bluez-tools build-essential autoconf glib2.0 libglib2.0-dev libdbus-1-dev libudev-dev libical-dev libreadline-dev
    ```

1. <span data-ttu-id="202a1-180">Téléchargez le code source de BlueZ à partir de bluez.org :</span><span class="sxs-lookup"><span data-stu-id="202a1-180">Download the BlueZ source code from bluez.org:</span></span>

    ```sh
    wget http://www.kernel.org/pub/linux/bluetooth/bluez-5.37.tar.xz
    ```

1. <span data-ttu-id="202a1-181">Décompressez le code source :</span><span class="sxs-lookup"><span data-stu-id="202a1-181">Unzip the source code:</span></span>

    ```sh
    tar -xvf bluez-5.37.tar.xz
    ```

1. <span data-ttu-id="202a1-182">Déplacer les répertoires vers le dossier nouvellement créé :</span><span class="sxs-lookup"><span data-stu-id="202a1-182">Change directories to the newly created folder:</span></span>

    ```sh
    cd bluez-5.37
    ```

1. <span data-ttu-id="202a1-183">Configurez le code BlueZ à générer :</span><span class="sxs-lookup"><span data-stu-id="202a1-183">Configure the BlueZ code to be built:</span></span>

    ```sh
    ./configure --disable-udev --disable-systemd --enable-experimental
    ```

1. <span data-ttu-id="202a1-184">Générez BlueZ :</span><span class="sxs-lookup"><span data-stu-id="202a1-184">Build BlueZ:</span></span>

    ```sh
    make
    ```

1. <span data-ttu-id="202a1-185">Installez BlueZ une fois la génération terminée :</span><span class="sxs-lookup"><span data-stu-id="202a1-185">Install BlueZ once it is done building:</span></span>

    ```sh
    sudo make install
    ```

1. <span data-ttu-id="202a1-186">Modifiez la configuration du service systemd pour Bluetooth afin qu’il pointe vers le nouveau démon Bluetooth dans le fichier `/lib/systemd/system/bluetooth.service`.</span><span class="sxs-lookup"><span data-stu-id="202a1-186">Change systemd service configuration for bluetooth so it points to the new bluetooth daemon in the file `/lib/systemd/system/bluetooth.service`.</span></span> <span data-ttu-id="202a1-187">Remplacez la ligne « ExecStart » par le texte suivant :</span><span class="sxs-lookup"><span data-stu-id="202a1-187">Replace the 'ExecStart' line with the following text:</span></span>

    ```conf
    ExecStart=/usr/local/libexec/bluetooth/bluetoothd -E
    ```

### <a name="enable-connectivity-to-the-sensortag-device-from-your-raspberry-pi-3-device"></a><span data-ttu-id="202a1-188">Activer la connectivité à l’appareil SensorTag à partir de votre appareil Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="202a1-188">Enable connectivity to the SensorTag device from your Raspberry Pi 3 device</span></span>

<span data-ttu-id="202a1-189">Avant d’exécuter l’exemple, vous devez vérifier que votre Raspberry Pi 3 peut se connecter à l’appareil SensorTag.</span><span class="sxs-lookup"><span data-stu-id="202a1-189">Before running the sample, you need to verify that your Raspberry Pi 3 can connect to the SensorTag device.</span></span>

1. <span data-ttu-id="202a1-190">Vérifiez que l’utilitaire `rfkill` est installé :</span><span class="sxs-lookup"><span data-stu-id="202a1-190">Ensure the `rfkill` utility is installed:</span></span>

    ```sh
    sudo apt-get install rfkill
    ```

1. <span data-ttu-id="202a1-191">Débloquez Bluetooth sur l’appareil Raspberry Pi 3, et vérifiez que le numéro de version est **5.37** :</span><span class="sxs-lookup"><span data-stu-id="202a1-191">Unblock bluetooth on the Raspberry Pi 3 and check that the version number is **5.37**:</span></span>

    ```sh
    sudo rfkill unblock bluetooth
    bluetoothctl --version
    ```

1. <span data-ttu-id="202a1-192">Pour entrer l’interpréteur de commandes Bluetooth interactif, démarrez le service Bluetooth et exécutez la commande **bluetoothctl** :</span><span class="sxs-lookup"><span data-stu-id="202a1-192">To enter the interactive bluetooth shell, start the bluetooth service and execute the **bluetoothctl** command :</span></span>

    ```sh
    sudo systemctl start bluetooth
    bluetoothctl
    ```

1. <span data-ttu-id="202a1-193">Entrez la commande **power on** pour mettre le contrôleur bluetooth sous tension.</span><span class="sxs-lookup"><span data-stu-id="202a1-193">Enter the command **power on** to power up the bluetooth controller.</span></span> <span data-ttu-id="202a1-194">La commande retourne un résultat semblable à l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="202a1-194">The command returns output similar to the following:</span></span>

    ```sh
    [NEW] Controller 98:4F:EE:04:1F:DF C3 raspberrypi [default]
    ```

1. <span data-ttu-id="202a1-195">Dans le shell interactif bluetooth, entrez la commande **scan on** pour rechercher des appareils bluetooth.</span><span class="sxs-lookup"><span data-stu-id="202a1-195">In the interactive bluetooth shell, enter the command **scan on** to scan for bluetooth devices.</span></span> <span data-ttu-id="202a1-196">La commande retourne un résultat semblable à l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="202a1-196">The command returns output similar to the following:</span></span>

    ```sh
    Discovery started
    [CHG] Controller 98:4F:EE:04:1F:DF Discovering: yes
    ```

1. <span data-ttu-id="202a1-197">Appuyez sur le petit bouton de l’appareil SensorTag pour le rendre détectable (le voyant vert doit clignoter).</span><span class="sxs-lookup"><span data-stu-id="202a1-197">Make the SensorTag device discoverable by pressing the small button (the green LED should flash).</span></span> <span data-ttu-id="202a1-198">Le Raspberry Pi 3 doit détecter l’appareil SensorTag :</span><span class="sxs-lookup"><span data-stu-id="202a1-198">The Raspberry Pi 3 should discover the SensorTag device:</span></span>

    ```sh
    [NEW] Device A0:E6:F8:B5:F6:00 CC2650 SensorTag
    [CHG] Device A0:E6:F8:B5:F6:00 TxPower: 0
    [CHG] Device A0:E6:F8:B5:F6:00 RSSI: -43
    ```

    <span data-ttu-id="202a1-199">Dans cet exemple, vous pouvez voir que l’adresse MAC de l’appareil SensorTag est **A0:E6:F8:B5:F6:00**.</span><span class="sxs-lookup"><span data-stu-id="202a1-199">In this example, you can see that the MAC address of the SensorTag device is **A0:E6:F8:B5:F6:00**.</span></span>

1. <span data-ttu-id="202a1-200">Désactivez l’analyse en entrant la commande **scan off** :</span><span class="sxs-lookup"><span data-stu-id="202a1-200">Turn off scanning by entering the **scan off** command:</span></span>

    ```sh
    [CHG] Controller 98:4F:EE:04:1F:DF Discovering: no
    Discovery stopped
    ```

1. <span data-ttu-id="202a1-201">Connectez-vous à votre appareil SensorTag à l’aide de son adresse MAC en entrant **connect \<adresse MAC>\>**.</span><span class="sxs-lookup"><span data-stu-id="202a1-201">Connect to your SensorTag device using its MAC address by entering **connect \<MAC address\>**.</span></span> <span data-ttu-id="202a1-202">L’exemple de sortie suivant est abrégé pour plus de clarté :</span><span class="sxs-lookup"><span data-stu-id="202a1-202">The following sample output is abbreviated for clarity:</span></span>

    ```sh
    Attempting to connect to A0:E6:F8:B5:F6:00
    [CHG] Device A0:E6:F8:B5:F6:00 Connected: yes
    Connection successful
    [CHG] Device A0:E6:F8:B5:F6:00 UUIDs: 00001800-0000-1000-8000-00805f9b34fb
    ...
    [NEW] Primary Service
            /org/bluez/hci0/dev_A0_E6_F8_B5_F6_00/service000c
            Device Information
    ...
    [CHG] Device A0:E6:F8:B5:F6:00 GattServices: /org/bluez/hci0/dev_A0_E6_F8_B5_F6_00/service000c
    ...
    [CHG] Device A0:E6:F8:B5:F6:00 Name: SensorTag 2.0
    [CHG] Device A0:E6:F8:B5:F6:00 Alias: SensorTag 2.0
    [CHG] Device A0:E6:F8:B5:F6:00 Modalias: bluetooth:v000Dp0000d0110
    ```

    > <span data-ttu-id="202a1-203">Vous pouvez de nouveau répertorier les caractéristiques GATT de l’appareil à l’aide de la commande **list-attributes** .</span><span class="sxs-lookup"><span data-stu-id="202a1-203">You can list the GATT characteristics of the device again using the **list-attributes** command.</span></span>

1. <span data-ttu-id="202a1-204">Vous pouvez maintenant vous déconnecter de l’appareil à l’aide de la commande **disconnect**, puis utilisez la commande **quit** pour quitter le shell Bluetooth :</span><span class="sxs-lookup"><span data-stu-id="202a1-204">You can now disconnect from the device using the **disconnect** command and then exit from the bluetooth shell using the **quit** command:</span></span>

    ```sh
    Attempting to disconnect from A0:E6:F8:B5:F6:00
    Successful disconnected
    [CHG] Device A0:E6:F8:B5:F6:00 Connected: no
    ```

<span data-ttu-id="202a1-205">Vous êtes maintenant prêt à exécuter l’exemple de passerelle IoT Edge BLE sur votre appareil Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="202a1-205">You're now ready to run the BLE IoT Edge sample on your Raspberry Pi 3.</span></span>

## <a name="run-the-iot-edge-ble-sample"></a><span data-ttu-id="202a1-206">Exécuter l’exemple BLE IoT Edge</span><span class="sxs-lookup"><span data-stu-id="202a1-206">Run the IoT Edge BLE sample</span></span>

<span data-ttu-id="202a1-207">Pour exécuter l’exemple BLE IoT Edge, vous devez effectuer trois tâches :</span><span class="sxs-lookup"><span data-stu-id="202a1-207">To run the IoT Edge BLE sample, you need to complete three tasks:</span></span>

* <span data-ttu-id="202a1-208">Configurer deux exemples d’appareils dans votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="202a1-208">Configure two sample devices in your IoT Hub.</span></span>
* <span data-ttu-id="202a1-209">Générer IoT Edge sur votre appareil Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="202a1-209">Build IoT Edge on your Raspberry Pi 3 device.</span></span>
* <span data-ttu-id="202a1-210">Configurer et exécuter l’exemple de BLE sur votre appareil Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="202a1-210">Configure and run the BLE sample on your Raspberry Pi 3 device.</span></span>

<span data-ttu-id="202a1-211">Lors de la rédaction du présent article, IoT Edge prenait uniquement en charge les modules BLE sur des passerelles sur Linux.</span><span class="sxs-lookup"><span data-stu-id="202a1-211">At the time of writing, IoT Edge only supports BLE modules in gateways running on Linux.</span></span>

### <a name="configure-two-sample-devices-in-your-iot-hub"></a><span data-ttu-id="202a1-212">Configuration de deux exemples d’appareils dans votre IoT Hub</span><span class="sxs-lookup"><span data-stu-id="202a1-212">Configure two sample devices in your IoT Hub</span></span>

* <span data-ttu-id="202a1-213">[Créer un IoT Hub][lnk-create-hub] dans votre abonnement Azure (vous aurez besoin du nom de votre concentrateur pour effectuer cette procédure pas à pas).</span><span class="sxs-lookup"><span data-stu-id="202a1-213">[Create an IoT hub][lnk-create-hub] in your Azure subscription, you need the name of your hub to complete this walkthrough.</span></span> <span data-ttu-id="202a1-214">Si vous ne possédez pas de compte, vous pouvez créer un [compte gratuit][lnk-free-trial] en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="202a1-214">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="202a1-215">Ajoutez un appareil nommé **SensorTag_01** à votre IoT Hub et notez son ID et sa clé d’appareil.</span><span class="sxs-lookup"><span data-stu-id="202a1-215">Add one device called **SensorTag_01** to your IoT hub and make a note of its id and device key.</span></span> <span data-ttu-id="202a1-216">Vous pouvez vous servir des outils de [l’Explorateur d’appareils ou iothub-explorer][lnk-explorer-tools] pour ajouter cet appareil à l’IoT Hub que vous avez créé à l’étape précédente, et récupérer sa clé.</span><span class="sxs-lookup"><span data-stu-id="202a1-216">You can use the [device explorer or iothub-explorer][lnk-explorer-tools] tools to add this device to the IoT hub you created in the previous step and to retrieve its key.</span></span> <span data-ttu-id="202a1-217">Vous allez mapper cet appareil à l’appareil SensorTag lors de la configuration de la passerelle.</span><span class="sxs-lookup"><span data-stu-id="202a1-217">You map this device to the SensorTag device when you configure the gateway.</span></span>

### <a name="build-azure-iot-edge-on-your-raspberry-pi-3"></a><span data-ttu-id="202a1-218">Générer Azure IoT Edge sur votre appareil Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="202a1-218">Build Azure IoT Edge on your Raspberry Pi 3</span></span>

<span data-ttu-id="202a1-219">Installer les dépendances pour Azure IoT Edge :</span><span class="sxs-lookup"><span data-stu-id="202a1-219">Install dependencies for Azure IoT Edge:</span></span>

```sh
sudo apt-get install cmake uuid-dev curl libcurl4-openssl-dev libssl-dev
```

<span data-ttu-id="202a1-220">Utilisez les commandes suivantes pour cloner IoT Edge et tous ses sous-modules dans votre répertoire de base :</span><span class="sxs-lookup"><span data-stu-id="202a1-220">Use the following commands to clone IoT Edge and all its submodules to your home directory:</span></span>

```sh
cd ~
git clone https://github.com/Azure/iot-edge.git
```

<span data-ttu-id="202a1-221">Si vous disposez d’une copie complète du dépôt IoT Edge sur votre Raspberry Pi 3, vous pouvez générer la passerelle en utilisant la commande suivante à partir du dossier contenant le Kit de développement logiciel (SDK) :</span><span class="sxs-lookup"><span data-stu-id="202a1-221">When you have a complete copy of the IoT Edge repository on your Raspberry Pi 3, you can build it using the following command from the folder that contains the SDK:</span></span>

```sh
cd ~/iot-edge
./tools/build.sh  --disable-native-remote-modules
```

### <a name="configure-and-run-the-ble-sample-on-your-raspberry-pi-3"></a><span data-ttu-id="202a1-222">Configurer et exécuter l’exemple de BLE sur votre appareil Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="202a1-222">Configure and run the BLE sample on your Raspberry Pi 3</span></span>

<span data-ttu-id="202a1-223">Pour démarrer et exécuter l’exemple, vous devez configurer chaque module IoT Edge qui fait partie de la passerelle.</span><span class="sxs-lookup"><span data-stu-id="202a1-223">To bootstrap and run the sample, you must configure each IoT Edge module that participates in the gateway.</span></span> <span data-ttu-id="202a1-224">Cette configuration est fournie dans un fichier JSON et vous devez configurer les cinq modules IoT Edge participants.</span><span class="sxs-lookup"><span data-stu-id="202a1-224">This configuration is provided in a JSON file and you must configure all five participating IoT Edge modules.</span></span> <span data-ttu-id="202a1-225">Le référentiel contient un exemple de fichier JSON nommé **gateway\_sample.json** que vous pouvez utiliser comme point de départ pour créer votre propre fichier de configuration.</span><span class="sxs-lookup"><span data-stu-id="202a1-225">There is a sample JSON file in the repository called **gateway\_sample.json** that you can use as the starting point for building your own configuration file.</span></span> <span data-ttu-id="202a1-226">Ce fichier se trouve dans le dossier **samples/ble_gateway_hl/src**, dans la copie locale du dépôt IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="202a1-226">This file is in the **samples/ble_gateway/src** folder in local copy of the IoT Edge repository.</span></span>

<span data-ttu-id="202a1-227">Les sections suivantes décrivent comment modifier ce fichier de configuration pour l’exemple BLE et supposent que le dépôt IoT Edge se trouve dans le dossier **/home/pi/iot-edge/** sur votre Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="202a1-227">The following sections describe how to edit this configuration file for the BLE sample and assume that the IoT Edge repository is in the **/home/pi/iot-edge/** folder on your Raspberry Pi 3.</span></span> <span data-ttu-id="202a1-228">Si le référentiel se trouve ailleurs, vous devez ajuster les chemins d’accès en conséquence.</span><span class="sxs-lookup"><span data-stu-id="202a1-228">If the repository is elsewhere, adjust the paths accordingly.</span></span>

#### <a name="logger-configuration"></a><span data-ttu-id="202a1-229">Configuration de l’enregistreur</span><span class="sxs-lookup"><span data-stu-id="202a1-229">Logger configuration</span></span>

<span data-ttu-id="202a1-230">En supposant que le dépôt de la passerelle se trouve dans le dossier **/home/pi/iot-edge/**, configurez le module enregistreur comme suit :</span><span class="sxs-lookup"><span data-stu-id="202a1-230">Assuming the gateway repository is located in the **/home/pi/iot-edge/** folder, configure the logger module as follows:</span></span>

```json
{
  "name": "Logger",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path" : "build/modules/logger/liblogger.so"
    }
  },
  "args":
  {
    "filename": "<</path/to/log-file.log>>"
  }
}
```

#### <a name="ble-module-configuration"></a><span data-ttu-id="202a1-231">Configuration du module BLE</span><span class="sxs-lookup"><span data-stu-id="202a1-231">BLE module configuration</span></span>

<span data-ttu-id="202a1-232">L’exemple de configuration de l’appareil BLE suppose qu’il s’agit d’un appareil Texas Instruments SensorTag.</span><span class="sxs-lookup"><span data-stu-id="202a1-232">The sample configuration for the BLE device assumes a Texas Instruments SensorTag device.</span></span> <span data-ttu-id="202a1-233">Tout appareil BLE standard qui peut fonctionner comme un périphérique GATT devrait fonctionner, mais vous devrez peut-être mettre à jour les ID et les données des caractéristiques GATT.</span><span class="sxs-lookup"><span data-stu-id="202a1-233">Any standard BLE device that can operate as a GATT peripheral should work but you may need to update the GATT characteristic IDs and data.</span></span> <span data-ttu-id="202a1-234">Ajoutez l’adresse MAC de votre appareil SensorTag :</span><span class="sxs-lookup"><span data-stu-id="202a1-234">Add the MAC address of your SensorTag device:</span></span>

```json
{
  "name": "SensorTag",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/modules/ble/libble.so"
    }
  },
  "args": {
    "controller_index": 0,
    "device_mac_address": "<<AA:BB:CC:DD:EE:FF>>",
    "instructions": [
      {
        "type": "read_once",
        "characteristic_uuid": "00002A24-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A25-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A26-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A27-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A28-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A29-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "write_at_init",
        "characteristic_uuid": "F000AA02-0451-4000-B000-000000000000",
        "data": "AQ=="
      },
      {
        "type": "read_periodic",
        "characteristic_uuid": "F000AA01-0451-4000-B000-000000000000",
        "interval_in_ms": 1000
      },
      {
        "type": "write_at_exit",
        "characteristic_uuid": "F000AA02-0451-4000-B000-000000000000",
        "data": "AA=="
      }
    ]
  }
}
```

<span data-ttu-id="202a1-235">Si vous n’utilisez pas d’appareil SensorTag, consultez la documentation de votre appareil BLE afin de déterminer si vous devez mettre à jour les ID et les données des caractéristiques GATT.</span><span class="sxs-lookup"><span data-stu-id="202a1-235">If you are not using a SensorTag device, review the documentation for your BLE device to determine whether you need to update the GATT characteristic IDs and data values.</span></span>

#### <a name="iot-hub-module"></a><span data-ttu-id="202a1-236">module IoT Hub</span><span class="sxs-lookup"><span data-stu-id="202a1-236">IoT Hub module</span></span>

<span data-ttu-id="202a1-237">Ajoutez le nom de votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="202a1-237">Add the name of your IoT Hub.</span></span> <span data-ttu-id="202a1-238">La valeur de suffixe est généralement **azure-devices.net**:</span><span class="sxs-lookup"><span data-stu-id="202a1-238">The suffix value is typically **azure-devices.net**:</span></span>

```json
{
  "name": "IoTHub",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/modules/iothub/libiothub.so"
    }
  },
  "args": {
    "IoTHubName": "<<Azure IoT Hub Name>>",
    "IoTHubSuffix": "<<Azure IoT Hub Suffix>>",
    "Transport" : "amqp"
  }
}
```

#### <a name="identity-mapping-module-configuration"></a><span data-ttu-id="202a1-239">Configuration du mappage d’identité</span><span class="sxs-lookup"><span data-stu-id="202a1-239">Identity mapping module configuration</span></span>

<span data-ttu-id="202a1-240">Ajoutez l’adresse MAC de votre appareil SensorTag, ainsi que l’ID et la clé de l’appareil **SensorTag_01** que vous avez ajoutés à votre IoT Hub :</span><span class="sxs-lookup"><span data-stu-id="202a1-240">Add the MAC address of your SensorTag device and the device ID and key of the **SensorTag_01** device you added to your IoT Hub:</span></span>

```json
{
  "name": "mapping",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/modules/identitymap/libidentity_map.so"
    }
  },
  "args": [
    {
      "macAddress": "<<AA:BB:CC:DD:EE:FF>>",
      "deviceId": "<<Azure IoT Hub Device ID>>",
      "deviceKey": "<<Azure IoT Hub Device Key>>"
    }
  ]
}
```

#### <a name="ble-printer-module-configuration"></a><span data-ttu-id="202a1-241">Configuration du module d’imprimante BLE</span><span class="sxs-lookup"><span data-stu-id="202a1-241">BLE Printer module configuration</span></span>

```json
{
  "name": "BLE Printer",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/samples/ble_gateway/ble_printer/libble_printer.so"
    }
  },
  "args": null
}
```

#### <a name="blec2d-module-configuration"></a><span data-ttu-id="202a1-242">Configuration du module BLEC2D</span><span class="sxs-lookup"><span data-stu-id="202a1-242">BLEC2D Module Configuration</span></span>

```json
{
  "name": "BLEC2D",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/modules/ble/libble_c2d.so"
    }
  },
  "args": null
}
```

#### <a name="routing-configuration"></a><span data-ttu-id="202a1-243">Configuration du routage</span><span class="sxs-lookup"><span data-stu-id="202a1-243">Routing Configuration</span></span>

<span data-ttu-id="202a1-244">La configuration suivante permet d’assurer l’acheminement suivant entre les modules IoT Edge :</span><span class="sxs-lookup"><span data-stu-id="202a1-244">The following configuration ensures the following routing between IoT Edge modules:</span></span>

* <span data-ttu-id="202a1-245">Le module **Enregistreur** reçoit et journalise tous les messages.</span><span class="sxs-lookup"><span data-stu-id="202a1-245">The **Logger** module receives and logs all messages.</span></span>
* <span data-ttu-id="202a1-246">Le module **SensorTag** envoie les messages aux modules **mapping** et **BLE Printer**.</span><span class="sxs-lookup"><span data-stu-id="202a1-246">The **SensorTag** module sends messages to both the **mapping** and **BLE Printer** modules.</span></span>
* <span data-ttu-id="202a1-247">Le module **mapping** envoie les messages à envoyer à votre IoT Hub au module **IoTHub**.</span><span class="sxs-lookup"><span data-stu-id="202a1-247">The **mapping** module sends messages to the **IoTHub** module to be sent up to your IoT Hub.</span></span>
* <span data-ttu-id="202a1-248">Le module **IoTHub** renvoie les messages au module **mapping**.</span><span class="sxs-lookup"><span data-stu-id="202a1-248">The **IoTHub** module sends messages back to the **mapping** module.</span></span>
* <span data-ttu-id="202a1-249">Le module **mapping** envoie les messages au module **BLEC2D**.</span><span class="sxs-lookup"><span data-stu-id="202a1-249">The **mapping** module sends messages to the **BLEC2D** module.</span></span>
* <span data-ttu-id="202a1-250">Le module **BLEC2D** renvoie les messages au module **SensorTag**.</span><span class="sxs-lookup"><span data-stu-id="202a1-250">The **BLEC2D** module sends messages back to the **Sensor Tag** module.</span></span>

```json
"links" : [
    {"source" : "*", "sink" : "Logger" },
    {"source" : "SensorTag", "sink" : "mapping" },
    {"source" : "SensorTag", "sink" : "BLE Printer" },
    {"source" : "mapping", "sink" : "IoTHub" },
    {"source" : "IoTHub", "sink" : "mapping" },
    {"source" : "mapping", "sink" : "BLEC2D" },
    {"source" : "BLEC2D", "sink" : "SensorTag"}
 ]
```

<span data-ttu-id="202a1-251">Pour exécuter l’exemple, transmettez le chemin d’accès du fichier de configuration JSON en tant que paramètre au fichier binaire **ble\_gateway**.</span><span class="sxs-lookup"><span data-stu-id="202a1-251">To run the sample, pass the path to the JSON configuration file as a parameter to the **ble\_gateway** binary.</span></span> <span data-ttu-id="202a1-252">La commande suivante considère que vous utilisez le fichier de configuration **gateway_sample.json**.</span><span class="sxs-lookup"><span data-stu-id="202a1-252">The following command assumes you are using the **gateway_sample.json** configuration file.</span></span> <span data-ttu-id="202a1-253">Exécutez-la à partir du dossier **iot-edge** sur le Raspberry Pi :</span><span class="sxs-lookup"><span data-stu-id="202a1-253">Execute this command from the **iot-edge** folder on the Raspberry Pi:</span></span>

```sh
./build/samples/ble_gateway/ble_gateway ./samples/ble_gateway/src/gateway_sample.json
```

<span data-ttu-id="202a1-254">Vous devrez peut-être appuyer sur le petit bouton situé sur l’appareil SensorTag pour le rendre détectable avant d’exécuter l’exemple.</span><span class="sxs-lookup"><span data-stu-id="202a1-254">You may need to press the small button on the SensorTag device to make it discoverable before you run the sample.</span></span>

<span data-ttu-id="202a1-255">Lorsque vous exécutez l’exemple, vous pouvez vous servir de [Device Explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) ou de l’outil [iothub-explorer](https://github.com/Azure/iothub-explorer) pour surveiller les messages que la passerelle IoT Edge transfère à partir de l’appareil SensorTag.</span><span class="sxs-lookup"><span data-stu-id="202a1-255">When you run the sample, you can use the [device explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) or the [iothub-explorer](https://github.com/Azure/iothub-explorer) tool to monitor the messages the IoT Edge gateway forwards from the SensorTag device.</span></span> <span data-ttu-id="202a1-256">Par exemple, à l’aide d’iothub-explorer, vous pouvez surveiller les messages appareil-à-cloud à l’aide de la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="202a1-256">For example, using iothub-explorer you can monitor device-to-cloud messages using the following command:</span></span>

```sh
iothub-explorer monitor-events --login "HostName={Your iot hub name}.azure-devices.net;SharedAccessKeyName=iothubowner;SharedAccessKey={Your IoT Hub key}"
```

## <a name="send-cloud-to-device-messages"></a><span data-ttu-id="202a1-257">Envoi de messages cloud vers appareil</span><span class="sxs-lookup"><span data-stu-id="202a1-257">Send cloud-to-device messages</span></span>

<span data-ttu-id="202a1-258">Le module BLE prend également en charge l’envoi de commandes à partir d’IoT Hub à l’appareil.</span><span class="sxs-lookup"><span data-stu-id="202a1-258">The BLE module also supports sending commands from IoT Hub to the device.</span></span> <span data-ttu-id="202a1-259">Vous pouvez utiliser [l’Explorateur d’appareils](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) ou l’outil [iothub-explorer](https://github.com/Azure/iothub-explorer) pour envoyer des messages JSON que le module de passerelle BLE transmet à l’appareil BLE.</span><span class="sxs-lookup"><span data-stu-id="202a1-259">You can use the [device explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) or the [iothub-explorer](https://github.com/Azure/iothub-explorer) tool to send JSON messages that the BLE gateway module forwards on to the BLE device.</span></span>

<span data-ttu-id="202a1-260">Si vous utilisez l’appareil SensorTag de Texas Instruments, vous pouvez activer la DEL rouge, la DEL verte, ou le vibreur sonore en envoyant des commandes à partir de l’IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="202a1-260">If you are using the Texas Instruments SensorTag device, you can turn on the red LED, green LED, or buzzer by sending commands from IoT Hub.</span></span> <span data-ttu-id="202a1-261">Avant d’envoyer des commandes depuis IoT Hub, commencez par envoyer les deux messages JSON suivants dans l’ordre.</span><span class="sxs-lookup"><span data-stu-id="202a1-261">Before you send commands from IoT Hub, first send the following two JSON messages in order.</span></span> <span data-ttu-id="202a1-262">Ensuite, vous pouvez envoyer n’importe laquelle des commandes pour activer les témoins ou le vibreur sonore.</span><span class="sxs-lookup"><span data-stu-id="202a1-262">Then you can send any of the commands to turn on the lights or buzzer.</span></span>

1. <span data-ttu-id="202a1-263">Réinitialiser (éteindre) les LED et le vibreur sonore (en les mettant hors tension) :</span><span class="sxs-lookup"><span data-stu-id="202a1-263">Reset all LEDs and the buzzer (turn them off):</span></span>

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "AA=="
    }
    ```

1. <span data-ttu-id="202a1-264">Configurer les E/S en tant que « à distance » :</span><span class="sxs-lookup"><span data-stu-id="202a1-264">Configure I/O as 'remote':</span></span>

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA66-0451-4000-B000-000000000000",
      "data": "AQ=="
    }
    ```

<span data-ttu-id="202a1-265">Maintenant, vous pouvez envoyer l’une des commandes suivantes pour allumer les voyants ou le vibreur sonore sur l’appareil SensorTag :</span><span class="sxs-lookup"><span data-stu-id="202a1-265">Now you can send any of the following commands to turn on the lights or buzzer on the SensorTag device:</span></span>

* <span data-ttu-id="202a1-266">Allumer la LED rouge :</span><span class="sxs-lookup"><span data-stu-id="202a1-266">Turn on the red LED:</span></span>

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "AQ=="
    }
    ```

* <span data-ttu-id="202a1-267">Allumer la LED verte :</span><span class="sxs-lookup"><span data-stu-id="202a1-267">Turn on the green LED:</span></span>

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "Ag=="
    }
    ```

* <span data-ttu-id="202a1-268">Allumer le vibreur sonore :</span><span class="sxs-lookup"><span data-stu-id="202a1-268">Turn on the buzzer:</span></span>

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "BA=="
    }
    ```

## <a name="next-steps"></a><span data-ttu-id="202a1-269">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="202a1-269">Next Steps</span></span>

<span data-ttu-id="202a1-270">Si vous souhaitez approfondir vos connaissances sur Azure IoT Edge et découvrir certains exemples de code, consultez les tutoriels de développement et les ressources suivants :</span><span class="sxs-lookup"><span data-stu-id="202a1-270">If you want to gain a more advanced understanding of IoT Edge and experiment with some code examples, visit the following developer tutorials and resources:</span></span>

* <span data-ttu-id="202a1-271">[Azure IoT Edge][lnk-sdk]</span><span class="sxs-lookup"><span data-stu-id="202a1-271">[Azure IoT Edge][lnk-sdk]</span></span>

<span data-ttu-id="202a1-272">Pour explorer davantage les capacités de IoT Hub, consultez :</span><span class="sxs-lookup"><span data-stu-id="202a1-272">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="202a1-273">[Guide du développeur IoT Hub][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="202a1-273">[IoT Hub developer guide][lnk-devguide]</span></span>

<!-- Links -->
[lnk-ble-samplecode]: https://github.com/Azure/iot-edge/tree/master/samples/ble_gateway
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-explorer-tools]: https://github.com/Azure/azure-iot-sdks/blob/master/doc/manage_iot_hub.md
[lnk-sdk]: https://github.com/Azure/iot-edge/
[lnk-noobs]: https://www.raspberrypi.org/documentation/installation/noobs.md
[lnk-raspbian]: https://www.raspberrypi.org/downloads/raspbian/
[lnk-devguide]: iot-hub-devguide.md
[lnk-create-hub]: iot-hub-create-through-portal.md 
[lnk-pi-ssh]: https://www.raspberrypi.org/documentation/remote-access/ssh/README.md
[lnk-ssh-windows]: https://www.raspberrypi.org/documentation/remote-access/ssh/windows.md
[lnk-ssh-linux]: https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md
