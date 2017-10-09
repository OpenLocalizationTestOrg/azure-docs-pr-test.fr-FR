---
title: aaaUse un appareil physique avec Azure IoT bord | Documents Microsoft
description: "Comment toouse un hub IoT Texas Instruments SensorTag périphérique toosend données tooan via une passerelle IoT en cours d’exécution sur un périphérique framboises Pi 3. passerelle de Hello est générée à l’aide de Azure IoT Edge."
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
ms.openlocfilehash: a2385accdbd99012ad094232653ee47d4e5c7839
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-iot-edge-on-a-raspberry-pi-tooforward-device-to-cloud-messages-tooiot-hub"></a><span data-ttu-id="a784b-104">Utilisez Azure IoT bord sur un ordinateur framboises Pi tooforward messages appareil-à-cloud tooIoT Hub</span><span class="sxs-lookup"><span data-stu-id="a784b-104">Use Azure IoT Edge on a Raspberry Pi tooforward device-to-cloud messages tooIoT Hub</span></span>

<span data-ttu-id="a784b-105">Cette procédure pas à pas de hello [exemple de faible consommation d’énergie Bluetooth] [ lnk-ble-samplecode] vous montre comment toouse [Azure IoT bord] [ lnk-sdk] à :</span><span class="sxs-lookup"><span data-stu-id="a784b-105">This walkthrough of hello [Bluetooth low energy sample][lnk-ble-samplecode] shows you how toouse [Azure IoT Edge][lnk-sdk] to:</span></span>

* <span data-ttu-id="a784b-106">Transférer la télémétrie de l’appareil-à-cloud tooIoT Hub à partir d’un périphérique physique.</span><span class="sxs-lookup"><span data-stu-id="a784b-106">Forward device-to-cloud telemetry tooIoT Hub from a physical device.</span></span>
* <span data-ttu-id="a784b-107">Router les commandes à partir de l’unité physique de tooa IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="a784b-107">Route commands from IoT Hub tooa physical device.</span></span>

<span data-ttu-id="a784b-108">Cette procédure pas à pas inclut les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="a784b-108">This walkthrough covers:</span></span>

* <span data-ttu-id="a784b-109">**Architecture**: architecture des informations importantes Bluetooth hello, exemple de faible consommation d’énergie.</span><span class="sxs-lookup"><span data-stu-id="a784b-109">**Architecture**: important architectural information about hello Bluetooth low energy sample.</span></span>
* <span data-ttu-id="a784b-110">**Générez et exécutez**: toobuild de hello étapes requis et exemple hello d’exécution.</span><span class="sxs-lookup"><span data-stu-id="a784b-110">**Build and run**: hello steps required toobuild and run hello sample.</span></span>

## <a name="architecture"></a><span data-ttu-id="a784b-111">Architecture</span><span class="sxs-lookup"><span data-stu-id="a784b-111">Architecture</span></span>

<span data-ttu-id="a784b-112">procédure pas à pas Hello vous montre comment toobuild et exécuter une passerelle IoT sur un Pi framboises 3 qui exécute Raspbian Linux.</span><span class="sxs-lookup"><span data-stu-id="a784b-112">hello walkthrough shows you how toobuild and run an IoT Edge gateway on a Raspberry Pi 3 that runs Raspbian Linux.</span></span> <span data-ttu-id="a784b-113">passerelle de Hello est générée à l’aide de IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="a784b-113">hello gateway is built using IoT Edge.</span></span> <span data-ttu-id="a784b-114">exemple Hello utilise un Texas Instruments SensorTag Bluetooth faible énergie (BLE) périphérique toocollect température de données.</span><span class="sxs-lookup"><span data-stu-id="a784b-114">hello sample uses a Texas Instruments SensorTag Bluetooth Low Energy (BLE) device toocollect temperature data.</span></span>

<span data-ttu-id="a784b-115">Lorsque vous exécutez hello IoT passerelle il :</span><span class="sxs-lookup"><span data-stu-id="a784b-115">When you run hello IoT Edge gateway it:</span></span>

* <span data-ttu-id="a784b-116">Connecte l’appareil de SensorTag de tooa à l’aide de protocole d’énergie de faible Bluetooth (BLE) hello.</span><span class="sxs-lookup"><span data-stu-id="a784b-116">Connects tooa SensorTag device using hello Bluetooth Low Energy (BLE) protocol.</span></span>
* <span data-ttu-id="a784b-117">Se connecte tooIoT concentrateur à l’aide du protocole de hello HTTP.</span><span class="sxs-lookup"><span data-stu-id="a784b-117">Connects tooIoT Hub using hello HTTP protocol.</span></span>
* <span data-ttu-id="a784b-118">Transfère les données de télémétrie depuis hello SensorTag périphérique tooIoT Hub.</span><span class="sxs-lookup"><span data-stu-id="a784b-118">Forwards telemetry from hello SensorTag device tooIoT Hub.</span></span>
* <span data-ttu-id="a784b-119">Achemine les commandes à partir de l’appareil de SensorTag toohello IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="a784b-119">Routes commands from IoT Hub toohello SensorTag device.</span></span>

<span data-ttu-id="a784b-120">passerelle de Hello contient hello suivant les modules IoT bord :</span><span class="sxs-lookup"><span data-stu-id="a784b-120">hello gateway contains hello following IoT Edge modules:</span></span>

* <span data-ttu-id="a784b-121">A *module BLE* qui interagit avec un ver appareil tooreceive température de données à partir de hello et envoi commandes toohello périphérique.</span><span class="sxs-lookup"><span data-stu-id="a784b-121">A *BLE module* that interfaces with a BLE device tooreceive temperature data from hello device and send commands toohello device.</span></span>
* <span data-ttu-id="a784b-122">A *module BLE cloud toodevice* qui traduit les messages JSON envoyés à partir de IoT Hub en instructions BLE pour hello *module BLE*.</span><span class="sxs-lookup"><span data-stu-id="a784b-122">A *BLE cloud toodevice module* that translates JSON messages sent from IoT Hub into BLE instructions for hello *BLE module*.</span></span>
* <span data-ttu-id="a784b-123">A *module de l’enregistreur d’événements* enregistre tous les fichiers local passerelle messages tooa.</span><span class="sxs-lookup"><span data-stu-id="a784b-123">A *logger module* that logs all gateway messages tooa local file.</span></span>
* <span data-ttu-id="a784b-124">Un *module de mappage d’identité* qui effectue la traduction entre les adresses MAC de l’appareil BLE et les identités des appareils Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="a784b-124">An *identity mapping module* that translates between BLE device MAC addresses and Azure IoT Hub device identities.</span></span>
* <span data-ttu-id="a784b-125">Un *module de IoT Hub* qui télécharge tooan IoT hub de télémétrie des données et reçoit les commandes de l’appareil à partir d’un hub IoT.</span><span class="sxs-lookup"><span data-stu-id="a784b-125">An *IoT Hub module* that uploads telemetry data tooan IoT hub and receives device commands from an IoT hub.</span></span>
* <span data-ttu-id="a784b-126">A *module d’imprimante BLE* qui interprète les données de télémétrie à partir de l’appareil BLE hello et imprime la résolution des problèmes de données mises en forme toohello console tooenable et de débogage.</span><span class="sxs-lookup"><span data-stu-id="a784b-126">A *BLE printer module* that interprets telemetry from hello BLE device and prints formatted data toohello console tooenable troubleshooting and debugging.</span></span>

### <a name="how-data-flows-through-hello-gateway"></a><span data-ttu-id="a784b-127">Le flux des données via la passerelle de hello</span><span class="sxs-lookup"><span data-stu-id="a784b-127">How data flows through hello gateway</span></span>

<span data-ttu-id="a784b-128">Hello suivant le schéma illustre pipeline de flux de données hello télémétrie téléchargement :</span><span class="sxs-lookup"><span data-stu-id="a784b-128">hello following block diagram illustrates hello telemetry upload data flow pipeline:</span></span>

![Pipeline de passerelle de téléchargement de télémétrie](media/iot-hub-iot-edge-physical-device/gateway_ble_upload_data_flow.png)

<span data-ttu-id="a784b-130">étapes Hello qui un élément de données de télémétrie prend en déplacement à partir d’un tooIoT de périphérique BLE Hub sont :</span><span class="sxs-lookup"><span data-stu-id="a784b-130">hello steps that an item of telemetry takes traveling from a BLE device tooIoT Hub are:</span></span>

1. <span data-ttu-id="a784b-131">APPAREIL BLE Hello génère un exemple de la température et l’envoie sur le module BLE toohello Bluetooth dans la passerelle de hello.</span><span class="sxs-lookup"><span data-stu-id="a784b-131">hello BLE device generates a temperature sample and sends it over Bluetooth toohello BLE module in hello gateway.</span></span>
1. <span data-ttu-id="a784b-132">module BLE Hello reçoit l’exemple hello et le publie broker toohello, ainsi que l’adresse MAC de hello du périphérique de hello.</span><span class="sxs-lookup"><span data-stu-id="a784b-132">hello BLE module receives hello sample and publishes it toohello broker along with hello MAC address of hello device.</span></span>
1. <span data-ttu-id="a784b-133">module de mappage d’identité Hello récupère ce message et utilise un hello tootranslate de table interne adresse MAC du périphérique de hello en une identité d’appareil IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="a784b-133">hello identity mapping module picks up this message and uses an internal table tootranslate hello MAC address of hello device into an IoT Hub device identity.</span></span> <span data-ttu-id="a784b-134">Une identité d’appareil IoT Hub se compose d’un ID d’appareil et d’une clé d’appareil.</span><span class="sxs-lookup"><span data-stu-id="a784b-134">An IoT Hub device identity consists of a device ID and device key.</span></span>
1. <span data-ttu-id="a784b-135">module de mappage d’identité Hello publie un nouveau message qui contient les données d’exemple hello température, adresse MAC de hello du dispositif de hello, ID de périphérique hello et clé de périphérique hello.</span><span class="sxs-lookup"><span data-stu-id="a784b-135">hello identity mapping module publishes a new message that contains hello temperature sample data, hello MAC address of hello device, hello device ID, and hello device key.</span></span>
1. <span data-ttu-id="a784b-136">Hello module de IoT Hub reçoit ce nouveau message (généré par le module de mappage d’identité hello) et le publie tooIoT Hub.</span><span class="sxs-lookup"><span data-stu-id="a784b-136">hello IoT Hub module receives this new message (generated by hello identity mapping module) and publishes it tooIoT Hub.</span></span>
1. <span data-ttu-id="a784b-137">module d’enregistreur d’événements Hello enregistre tous les messages à partir de fichiers local de hello broker tooa.</span><span class="sxs-lookup"><span data-stu-id="a784b-137">hello logger module logs all messages from hello broker tooa local file.</span></span>

<span data-ttu-id="a784b-138">Hello suivant le schéma illustre pipeline de flux de données hello appareil commande :</span><span class="sxs-lookup"><span data-stu-id="a784b-138">hello following block diagram illustrates hello device command data flow pipeline:</span></span>

![Pipeline de passerelle de commande d’appareil](media/iot-hub-iot-edge-physical-device/gateway_ble_command_data_flow.png)

1. <span data-ttu-id="a784b-140">Hello IoT Hub module interroge régulièrement hello IoT hub pour les nouveaux messages de commande.</span><span class="sxs-lookup"><span data-stu-id="a784b-140">hello IoT Hub module periodically polls hello IoT hub for new command messages.</span></span>
1. <span data-ttu-id="a784b-141">Lorsque hello module de IoT Hub reçoit un nouveau message de commande, il publie toohello broker.</span><span class="sxs-lookup"><span data-stu-id="a784b-141">When hello IoT Hub module receives a new command message, it publishes it toohello broker.</span></span>
1. <span data-ttu-id="a784b-142">module de mappage d’identité Hello récupère le message de commande hello et utilise un hello tootranslate de table interne IoT Hub ID tooa périphérique adresse MAC.</span><span class="sxs-lookup"><span data-stu-id="a784b-142">hello identity mapping module picks up hello command message and uses an internal table tootranslate hello IoT Hub device ID tooa device MAC address.</span></span> <span data-ttu-id="a784b-143">Il publie ensuite un nouveau message qui comprend des hello l’adresse MAC du périphérique cible de hello dans le mappage de propriétés hello de message de type hello.</span><span class="sxs-lookup"><span data-stu-id="a784b-143">It then publishes a new message that includes hello MAC address of hello target device in hello properties map of hello message.</span></span>
1. <span data-ttu-id="a784b-144">module BLE Cloud-à-appareil Hello récupère ce message et le traduit en instruction BLE appropriée de hello pour le module BLE hello.</span><span class="sxs-lookup"><span data-stu-id="a784b-144">hello BLE Cloud-to-Device module picks up this message and translates it into hello proper BLE instruction for hello BLE module.</span></span> <span data-ttu-id="a784b-145">Il publie ensuite un nouveau message.</span><span class="sxs-lookup"><span data-stu-id="a784b-145">It then publishes a new message.</span></span>
1. <span data-ttu-id="a784b-146">module BLE Hello récupère ce message et exécute l’instruction d’e/s de hello en communiquant avec un périphérique BLE hello.</span><span class="sxs-lookup"><span data-stu-id="a784b-146">hello BLE module picks up this message and executes hello I/O instruction by communicating with hello BLE device.</span></span>
1. <span data-ttu-id="a784b-147">module d’enregistreur d’événements Hello enregistre tous les messages à partir du fichier de disque tooa hello broker.</span><span class="sxs-lookup"><span data-stu-id="a784b-147">hello logger module logs all messages from hello broker tooa disk file.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a784b-148">Composants requis</span><span class="sxs-lookup"><span data-stu-id="a784b-148">Prerequisites</span></span>

<span data-ttu-id="a784b-149">toocomplete ce didacticiel, vous avez besoin d’un abonnement Azure actif.</span><span class="sxs-lookup"><span data-stu-id="a784b-149">toocomplete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="a784b-150">Si vous ne possédez pas de compte, vous pouvez créer un compte d’évaluation gratuit en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="a784b-150">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="a784b-151">Pour plus d’informations, consultez la rubrique [Version d’évaluation gratuite d’Azure][lnk-free-trial].</span><span class="sxs-lookup"><span data-stu-id="a784b-151">For details, see [Azure Free Trial][lnk-free-trial].</span></span>

<span data-ttu-id="a784b-152">Vous devez client SSH sur votre tooenable d’ordinateur de bureau vous tooremotely accès hello de ligne de commande sur hello framboises Pi.</span><span class="sxs-lookup"><span data-stu-id="a784b-152">You need SSH client on your desktop machine tooenable you tooremotely access hello command line on hello Raspberry Pi.</span></span>

- <span data-ttu-id="a784b-153">Windows n’inclut pas de client SSH.</span><span class="sxs-lookup"><span data-stu-id="a784b-153">Windows does not include an SSH client.</span></span> <span data-ttu-id="a784b-154">Nous vous recommandons d’utiliser [PuTTY](http://www.putty.org/).</span><span class="sxs-lookup"><span data-stu-id="a784b-154">We recommend using [PuTTY](http://www.putty.org/).</span></span>
- <span data-ttu-id="a784b-155">La plupart des distributions Linux et Mac OS incluent l’utilitaire SSH hello.</span><span class="sxs-lookup"><span data-stu-id="a784b-155">Most Linux distributions and Mac OS include hello command-line SSH utility.</span></span> <span data-ttu-id="a784b-156">Pour plus d’informations, consultez [SSH Using Linux or Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md) (Utilisation de SSH avec Linux ou Mac OS).</span><span class="sxs-lookup"><span data-stu-id="a784b-156">For more information, see [SSH Using Linux or Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md).</span></span>

## <a name="prepare-your-hardware"></a><span data-ttu-id="a784b-157">Préparation du matériel</span><span class="sxs-lookup"><span data-stu-id="a784b-157">Prepare your hardware</span></span>

<span data-ttu-id="a784b-158">Ce didacticiel suppose que vous utilisez un [Texas Instruments SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/index.html) appareil connecté tooa framboises Pi 3 Raspbian en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="a784b-158">This tutorial assumes you are using a [Texas Instruments SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/index.html) device connected tooa Raspberry Pi 3 running Raspbian.</span></span>

### <a name="install-raspbian"></a><span data-ttu-id="a784b-159">Installer Raspbian</span><span class="sxs-lookup"><span data-stu-id="a784b-159">Install Raspbian</span></span>

<span data-ttu-id="a784b-160">Vous pouvez utiliser une des hello suivant les options tooinstall Raspbian sur votre appareil framboises Pi 3.</span><span class="sxs-lookup"><span data-stu-id="a784b-160">You can use either of hello following options tooinstall Raspbian on your Raspberry Pi 3 device.</span></span>

* <span data-ttu-id="a784b-161">version la plus récente hello tooinstall de Raspbian, utilisez hello [NOOBS] [ lnk-noobs] interface utilisateur graphique.</span><span class="sxs-lookup"><span data-stu-id="a784b-161">tooinstall hello latest version of Raspbian, use hello [NOOBS][lnk-noobs] graphical user interface.</span></span>
* <span data-ttu-id="a784b-162">Manuellement [télécharger] [ lnk-raspbian] et écrire la dernière image de hello de carte de hello Raspbian système d’exploitation tooan SD.</span><span class="sxs-lookup"><span data-stu-id="a784b-162">Manually [download][lnk-raspbian] and write hello latest image of hello Raspbian operating system tooan SD card.</span></span>

### <a name="sign-in-and-access-hello-terminal"></a><span data-ttu-id="a784b-163">Se connecter et accéder à Terminal Server de hello</span><span class="sxs-lookup"><span data-stu-id="a784b-163">Sign in and access hello terminal</span></span>

<span data-ttu-id="a784b-164">Vous avez deux options tooaccess d’un environnement de Terminal Server sur votre Pi framboises :</span><span class="sxs-lookup"><span data-stu-id="a784b-164">You have two options tooaccess a terminal environment on your Raspberry Pi:</span></span>

* <span data-ttu-id="a784b-165">Si vous possédez un clavier et surveillez tooyour connecté framboises Pi, vous pouvez utiliser hello Raspbian GUI tooaccess une fenêtre de terminal.</span><span class="sxs-lookup"><span data-stu-id="a784b-165">If you have a keyboard and monitor connected tooyour Raspberry Pi, you can use hello Raspbian GUI tooaccess a terminal window.</span></span>

* <span data-ttu-id="a784b-166">Ligne de commande accès hello sur votre Pi framboises à l’aide de SSH à partir de votre ordinateur de bureau.</span><span class="sxs-lookup"><span data-stu-id="a784b-166">Access hello command line on your Raspberry Pi using SSH from your desktop machine.</span></span>

#### <a name="use-a-terminal-window-in-hello-gui"></a><span data-ttu-id="a784b-167">Utiliser une fenêtre de terminal dans l’interface graphique utilisateur de hello</span><span class="sxs-lookup"><span data-stu-id="a784b-167">Use a terminal Window in hello GUI</span></span>

<span data-ttu-id="a784b-168">informations d’identification par défaut de Hello pour Raspbian sont le nom d’utilisateur **pi** et le mot de passe **framboises**.</span><span class="sxs-lookup"><span data-stu-id="a784b-168">hello default credentials for Raspbian are username **pi** and password **raspberry**.</span></span> <span data-ttu-id="a784b-169">Dans la barre des tâches hello Bonjour l’interface graphique utilisateur, vous pouvez lancer hello **Terminal** utility à l’aide d’icône hello qui ressemble à une analyse.</span><span class="sxs-lookup"><span data-stu-id="a784b-169">In hello task bar in hello GUI, you can launch hello **Terminal** utility using hello icon that looks like a monitor.</span></span>

#### <a name="sign-in-with-ssh"></a><span data-ttu-id="a784b-170">Se connecter avec SSH</span><span class="sxs-lookup"><span data-stu-id="a784b-170">Sign in with SSH</span></span>

<span data-ttu-id="a784b-171">Vous pouvez utiliser SSH pour l’accès en ligne de commande tooyour framboises Pi.</span><span class="sxs-lookup"><span data-stu-id="a784b-171">You can use SSH for command-line access tooyour Raspberry Pi.</span></span> <span data-ttu-id="a784b-172">article de Hello [SSH (Secure Shell)] [ lnk-pi-ssh] décrit comment tooconfigure SSH sur votre Pi framboises et comment tooconnect de [Windows] [ lnk-ssh-windows] ou [Linux et Mac OS][lnk-ssh-linux].</span><span class="sxs-lookup"><span data-stu-id="a784b-172">hello article [SSH (Secure Shell)][lnk-pi-ssh] describes how tooconfigure SSH on your Raspberry Pi, and how tooconnect from [Windows][lnk-ssh-windows] or [Linux & Mac OS][lnk-ssh-linux].</span></span>

<span data-ttu-id="a784b-173">Connectez-vous avec le nom d’utilisateur **pi** et le mot de passe **raspberry**.</span><span class="sxs-lookup"><span data-stu-id="a784b-173">Sign in with username **pi** and password **raspberry**.</span></span>

### <a name="install-bluez-537"></a><span data-ttu-id="a784b-174">Installer BlueZ 5.37</span><span class="sxs-lookup"><span data-stu-id="a784b-174">Install BlueZ 5.37</span></span>

<span data-ttu-id="a784b-175">matériel de Bluetooth toohello via la pile de BlueZ hello communiquer avec les modules BLE Hello.</span><span class="sxs-lookup"><span data-stu-id="a784b-175">hello BLE modules talk toohello Bluetooth hardware via hello BlueZ stack.</span></span> <span data-ttu-id="a784b-176">Vous devez correctement version 5.37 de BlueZ pour toowork de modules hello.</span><span class="sxs-lookup"><span data-stu-id="a784b-176">You need version 5.37 of BlueZ for hello modules toowork correctly.</span></span> <span data-ttu-id="a784b-177">Ces instructions Assurez-vous hello la version correcte de BlueZ est installée.</span><span class="sxs-lookup"><span data-stu-id="a784b-177">These instructions make sure hello correct version of BlueZ is installed.</span></span>

1. <span data-ttu-id="a784b-178">Arrêter le démon de bluetooth hello actuel :</span><span class="sxs-lookup"><span data-stu-id="a784b-178">Stop hello current bluetooth daemon:</span></span>

    ```sh
    sudo systemctl stop bluetooth
    ```

1. <span data-ttu-id="a784b-179">Installer les dépendances de BlueZ hello :</span><span class="sxs-lookup"><span data-stu-id="a784b-179">Install hello BlueZ dependencies:</span></span>

    ```sh
    sudo apt-get update
    sudo apt-get install bluetooth bluez-tools build-essential autoconf glib2.0 libglib2.0-dev libdbus-1-dev libudev-dev libical-dev libreadline-dev
    ```

1. <span data-ttu-id="a784b-180">Télécharger le code de source de hello BlueZ de bluez.org :</span><span class="sxs-lookup"><span data-stu-id="a784b-180">Download hello BlueZ source code from bluez.org:</span></span>

    ```sh
    wget http://www.kernel.org/pub/linux/bluetooth/bluez-5.37.tar.xz
    ```

1. <span data-ttu-id="a784b-181">Décompressez le code source de hello :</span><span class="sxs-lookup"><span data-stu-id="a784b-181">Unzip hello source code:</span></span>

    ```sh
    tar -xvf bluez-5.37.tar.xz
    ```

1. <span data-ttu-id="a784b-182">Changer le dossier répertoires toohello nouvellement créé :</span><span class="sxs-lookup"><span data-stu-id="a784b-182">Change directories toohello newly created folder:</span></span>

    ```sh
    cd bluez-5.37
    ```

1. <span data-ttu-id="a784b-183">Configurer hello BlueZ code toobe généré :</span><span class="sxs-lookup"><span data-stu-id="a784b-183">Configure hello BlueZ code toobe built:</span></span>

    ```sh
    ./configure --disable-udev --disable-systemd --enable-experimental
    ```

1. <span data-ttu-id="a784b-184">Générez BlueZ :</span><span class="sxs-lookup"><span data-stu-id="a784b-184">Build BlueZ:</span></span>

    ```sh
    make
    ```

1. <span data-ttu-id="a784b-185">Installez BlueZ une fois la génération terminée :</span><span class="sxs-lookup"><span data-stu-id="a784b-185">Install BlueZ once it is done building:</span></span>

    ```sh
    sudo make install
    ```

1. <span data-ttu-id="a784b-186">Modifier la configuration service systemd pour bluetooth afin qu’il pointe toohello nouveau bluetooth démon dans le fichier de hello `/lib/systemd/system/bluetooth.service`.</span><span class="sxs-lookup"><span data-stu-id="a784b-186">Change systemd service configuration for bluetooth so it points toohello new bluetooth daemon in hello file `/lib/systemd/system/bluetooth.service`.</span></span> <span data-ttu-id="a784b-187">Remplacez ligne de 'ExecStart' hello hello suivant du texte :</span><span class="sxs-lookup"><span data-stu-id="a784b-187">Replace hello 'ExecStart' line with hello following text:</span></span>

    ```conf
    ExecStart=/usr/local/libexec/bluetooth/bluetoothd -E
    ```

### <a name="enable-connectivity-toohello-sensortag-device-from-your-raspberry-pi-3-device"></a><span data-ttu-id="a784b-188">Activer la connectivité toohello SensorTag périphérique à partir de votre appareil framboises Pi 3</span><span class="sxs-lookup"><span data-stu-id="a784b-188">Enable connectivity toohello SensorTag device from your Raspberry Pi 3 device</span></span>

<span data-ttu-id="a784b-189">Avant d’en cours d’exécution exemple hello, vous devez tooverify que votre framboises Pi 3 peut se connecter toohello SensorTag appareil.</span><span class="sxs-lookup"><span data-stu-id="a784b-189">Before running hello sample, you need tooverify that your Raspberry Pi 3 can connect toohello SensorTag device.</span></span>

1. <span data-ttu-id="a784b-190">Assurez-vous de hello `rfkill` utilitaire est installé :</span><span class="sxs-lookup"><span data-stu-id="a784b-190">Ensure hello `rfkill` utility is installed:</span></span>

    ```sh
    sudo apt-get install rfkill
    ```

1. <span data-ttu-id="a784b-191">Débloquer bluetooth sur hello framboises Pi 3 et vérifier que le numéro de version de hello est **5.37**:</span><span class="sxs-lookup"><span data-stu-id="a784b-191">Unblock bluetooth on hello Raspberry Pi 3 and check that hello version number is **5.37**:</span></span>

    ```sh
    sudo rfkill unblock bluetooth
    bluetoothctl --version
    ```

1. <span data-ttu-id="a784b-192">interpréteur de commandes tooenter hello bluetooth interactif, démarrer le service bluetooth hello et exécutez hello **bluetoothctl** commande :</span><span class="sxs-lookup"><span data-stu-id="a784b-192">tooenter hello interactive bluetooth shell, start hello bluetooth service and execute hello **bluetoothctl** command :</span></span>

    ```sh
    sudo systemctl start bluetooth
    bluetoothctl
    ```

1. <span data-ttu-id="a784b-193">Entrez la commande hello **mise sous tension** toopower contrôleur bluetooth de hello.</span><span class="sxs-lookup"><span data-stu-id="a784b-193">Enter hello command **power on** toopower up hello bluetooth controller.</span></span> <span data-ttu-id="a784b-194">commande Hello retourne suivant toohello similaire de sortie :</span><span class="sxs-lookup"><span data-stu-id="a784b-194">hello command returns output similar toohello following:</span></span>

    ```sh
    [NEW] Controller 98:4F:EE:04:1F:DF C3 raspberrypi [default]
    ```

1. <span data-ttu-id="a784b-195">Dans l’interpréteur de commandes interactive bluetooth hello, entrez la commande hello **analyse sur** tooscan pour les appareils bluetooth.</span><span class="sxs-lookup"><span data-stu-id="a784b-195">In hello interactive bluetooth shell, enter hello command **scan on** tooscan for bluetooth devices.</span></span> <span data-ttu-id="a784b-196">commande Hello retourne suivant toohello similaire de sortie :</span><span class="sxs-lookup"><span data-stu-id="a784b-196">hello command returns output similar toohello following:</span></span>

    ```sh
    Discovery started
    [CHG] Controller 98:4F:EE:04:1F:DF Discovering: yes
    ```

1. <span data-ttu-id="a784b-197">Rendre les périphériques de SensorTag hello détectable en appuyant sur le bouton de petit hello (hello LED verte doit clignoter).</span><span class="sxs-lookup"><span data-stu-id="a784b-197">Make hello SensorTag device discoverable by pressing hello small button (hello green LED should flash).</span></span> <span data-ttu-id="a784b-198">Hello framboises Pi 3 doit découvrir un périphérique SensorTag hello :</span><span class="sxs-lookup"><span data-stu-id="a784b-198">hello Raspberry Pi 3 should discover hello SensorTag device:</span></span>

    ```sh
    [NEW] Device A0:E6:F8:B5:F6:00 CC2650 SensorTag
    [CHG] Device A0:E6:F8:B5:F6:00 TxPower: 0
    [CHG] Device A0:E6:F8:B5:F6:00 RSSI: -43
    ```

    <span data-ttu-id="a784b-199">Dans cet exemple, vous pouvez voir cette adresse MAC de hello SensorTag périphérique est hello **A0:E6:F8:B5:F6:00**.</span><span class="sxs-lookup"><span data-stu-id="a784b-199">In this example, you can see that hello MAC address of hello SensorTag device is **A0:E6:F8:B5:F6:00**.</span></span>

1. <span data-ttu-id="a784b-200">Désactiver l’analyse en entrant hello **analyse désactivée** commande :</span><span class="sxs-lookup"><span data-stu-id="a784b-200">Turn off scanning by entering hello **scan off** command:</span></span>

    ```sh
    [CHG] Controller 98:4F:EE:04:1F:DF Discovering: no
    Discovery stopped
    ```

1. <span data-ttu-id="a784b-201">Connecter l’appareil de SensorTag tooyour à l’aide de son adresse MAC en entrant **connecter \<adresse MAC\>**.</span><span class="sxs-lookup"><span data-stu-id="a784b-201">Connect tooyour SensorTag device using its MAC address by entering **connect \<MAC address\>**.</span></span> <span data-ttu-id="a784b-202">Pour plus de clarté, Hello suivant l’exemple de sortie est abrégé :</span><span class="sxs-lookup"><span data-stu-id="a784b-202">hello following sample output is abbreviated for clarity:</span></span>

    ```sh
    Attempting tooconnect tooA0:E6:F8:B5:F6:00
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

    > <span data-ttu-id="a784b-203">Vous pouvez répertorier les caractéristiques de GATT hello du périphérique hello à nouveau à l’aide de hello **-liste d’attributs** commande.</span><span class="sxs-lookup"><span data-stu-id="a784b-203">You can list hello GATT characteristics of hello device again using hello **list-attributes** command.</span></span>

1. <span data-ttu-id="a784b-204">Vous pouvez désormais vous déconnecter d’appareil hello à l’aide de hello **déconnecter** de commandes, puis quittez à partir de l’interpréteur de commandes bluetooth hello à l’aide de hello **quitter** commande :</span><span class="sxs-lookup"><span data-stu-id="a784b-204">You can now disconnect from hello device using hello **disconnect** command and then exit from hello bluetooth shell using hello **quit** command:</span></span>

    ```sh
    Attempting toodisconnect from A0:E6:F8:B5:F6:00
    Successful disconnected
    [CHG] Device A0:E6:F8:B5:F6:00 Connected: no
    ```

<span data-ttu-id="a784b-205">Vous êtes maintenant prêt toorun hello, exemple BLE IoT bord sur votre framboises Pi 3.</span><span class="sxs-lookup"><span data-stu-id="a784b-205">You're now ready toorun hello BLE IoT Edge sample on your Raspberry Pi 3.</span></span>

## <a name="run-hello-iot-edge-ble-sample"></a><span data-ttu-id="a784b-206">Exécutez l’exemple de tableau de bord IoT hello</span><span class="sxs-lookup"><span data-stu-id="a784b-206">Run hello IoT Edge BLE sample</span></span>

<span data-ttu-id="a784b-207">exemple de tableau de bord IoT toorun hello, vous devez toocomplete trois tâches :</span><span class="sxs-lookup"><span data-stu-id="a784b-207">toorun hello IoT Edge BLE sample, you need toocomplete three tasks:</span></span>

* <span data-ttu-id="a784b-208">Configurer deux exemples d’appareils dans votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="a784b-208">Configure two sample devices in your IoT Hub.</span></span>
* <span data-ttu-id="a784b-209">Générer IoT Edge sur votre appareil Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="a784b-209">Build IoT Edge on your Raspberry Pi 3 device.</span></span>
* <span data-ttu-id="a784b-210">Configurer et exécuter l’exemple de tableau hello sur votre appareil framboises Pi 3.</span><span class="sxs-lookup"><span data-stu-id="a784b-210">Configure and run hello BLE sample on your Raspberry Pi 3 device.</span></span>

<span data-ttu-id="a784b-211">Au moment de l’écriture de hello, IoT Edge prend uniquement en charge les modules de l’activer dans les passerelles en cours d’exécution sur Linux.</span><span class="sxs-lookup"><span data-stu-id="a784b-211">At hello time of writing, IoT Edge only supports BLE modules in gateways running on Linux.</span></span>

### <a name="configure-two-sample-devices-in-your-iot-hub"></a><span data-ttu-id="a784b-212">Configuration de deux exemples d’appareils dans votre IoT Hub</span><span class="sxs-lookup"><span data-stu-id="a784b-212">Configure two sample devices in your IoT Hub</span></span>

* <span data-ttu-id="a784b-213">[Créez un hub IoT] [ lnk-create-hub] dans votre abonnement Azure, vous devez fournir hello nom de votre concentrateur de toocomplete cette procédure pas à pas.</span><span class="sxs-lookup"><span data-stu-id="a784b-213">[Create an IoT hub][lnk-create-hub] in your Azure subscription, you need hello name of your hub toocomplete this walkthrough.</span></span> <span data-ttu-id="a784b-214">Si vous ne possédez pas de compte, vous pouvez créer un [compte gratuit][lnk-free-trial] en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="a784b-214">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="a784b-215">Ajouter un périphérique appelé **SensorTag_01** tooyour IoT hub et prenez note de sa clé d’id et de périphérique.</span><span class="sxs-lookup"><span data-stu-id="a784b-215">Add one device called **SensorTag_01** tooyour IoT hub and make a note of its id and device key.</span></span> <span data-ttu-id="a784b-216">Vous pouvez utiliser hello [Explorateur de l’appareil ou l’Explorateur de l’iothub] [ lnk-explorer-tools] outils tooadd ce hub IoT de toohello périphérique vous avez créé dans l’étape précédente de hello et tooretrieve sa clé.</span><span class="sxs-lookup"><span data-stu-id="a784b-216">You can use hello [device explorer or iothub-explorer][lnk-explorer-tools] tools tooadd this device toohello IoT hub you created in hello previous step and tooretrieve its key.</span></span> <span data-ttu-id="a784b-217">Vous mappez ce périphérique toohello SensorTag périphérique lorsque vous configurez la passerelle de hello.</span><span class="sxs-lookup"><span data-stu-id="a784b-217">You map this device toohello SensorTag device when you configure hello gateway.</span></span>

### <a name="build-azure-iot-edge-on-your-raspberry-pi-3"></a><span data-ttu-id="a784b-218">Générer Azure IoT Edge sur votre appareil Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="a784b-218">Build Azure IoT Edge on your Raspberry Pi 3</span></span>

<span data-ttu-id="a784b-219">Installer les dépendances pour Azure IoT Edge :</span><span class="sxs-lookup"><span data-stu-id="a784b-219">Install dependencies for Azure IoT Edge:</span></span>

```sh
sudo apt-get install cmake uuid-dev curl libcurl4-openssl-dev libssl-dev
```

<span data-ttu-id="a784b-220">Des commandes suivantes de hello utilisation tooclone IoT Edge et tous les sous-modules tooyour répertoire de base :</span><span class="sxs-lookup"><span data-stu-id="a784b-220">Use hello following commands tooclone IoT Edge and all its submodules tooyour home directory:</span></span>

```sh
cd ~
git clone https://github.com/Azure/iot-edge.git
```

<span data-ttu-id="a784b-221">Quand vous avez une copie complète de hello référentiel de IoT bord sur votre framboises Pi 3, vous pouvez créer à l’aide de hello de commande suivante à partir du dossier hello contenant hello SDK :</span><span class="sxs-lookup"><span data-stu-id="a784b-221">When you have a complete copy of hello IoT Edge repository on your Raspberry Pi 3, you can build it using hello following command from hello folder that contains hello SDK:</span></span>

```sh
cd ~/iot-edge
./tools/build.sh  --disable-native-remote-modules
```

### <a name="configure-and-run-hello-ble-sample-on-your-raspberry-pi-3"></a><span data-ttu-id="a784b-222">Configurer et exécuter l’exemple BLE de hello sur votre framboises Pi 3</span><span class="sxs-lookup"><span data-stu-id="a784b-222">Configure and run hello BLE sample on your Raspberry Pi 3</span></span>

<span data-ttu-id="a784b-223">toobootstrap et exemple hello exécution, vous devez configurer chaque module IoT Edge qui participe dans la passerelle de hello.</span><span class="sxs-lookup"><span data-stu-id="a784b-223">toobootstrap and run hello sample, you must configure each IoT Edge module that participates in hello gateway.</span></span> <span data-ttu-id="a784b-224">Cette configuration est fournie dans un fichier JSON et vous devez configurer les cinq modules IoT Edge participants.</span><span class="sxs-lookup"><span data-stu-id="a784b-224">This configuration is provided in a JSON file and you must configure all five participating IoT Edge modules.</span></span> <span data-ttu-id="a784b-225">Il est un exemple de fichier JSON dans le référentiel hello appelé **passerelle\_sample.json** que vous pouvez utiliser comme point de départ pour créer votre propre fichier de configuration de hello.</span><span class="sxs-lookup"><span data-stu-id="a784b-225">There is a sample JSON file in hello repository called **gateway\_sample.json** that you can use as hello starting point for building your own configuration file.</span></span> <span data-ttu-id="a784b-226">Ce fichier est hello **ble_gateway/samples/src** dossier dans une copie locale de hello référentiel de IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="a784b-226">This file is in hello **samples/ble_gateway/src** folder in local copy of hello IoT Edge repository.</span></span>

<span data-ttu-id="a784b-227">Hello sections suivantes décrivent comment tooedit cette configuration du fichier pour l’exemple de tableau hello et supposent que référentiel de IoT bord hello est Bonjour **/home/pi/iot-edge /** dossier sur votre framboises Pi 3.</span><span class="sxs-lookup"><span data-stu-id="a784b-227">hello following sections describe how tooedit this configuration file for hello BLE sample and assume that hello IoT Edge repository is in hello **/home/pi/iot-edge/** folder on your Raspberry Pi 3.</span></span> <span data-ttu-id="a784b-228">Si le référentiel de hello se trouve ailleurs, ajuster en conséquence les chemins d’accès hello.</span><span class="sxs-lookup"><span data-stu-id="a784b-228">If hello repository is elsewhere, adjust hello paths accordingly.</span></span>

#### <a name="logger-configuration"></a><span data-ttu-id="a784b-229">Configuration de l’enregistreur</span><span class="sxs-lookup"><span data-stu-id="a784b-229">Logger configuration</span></span>

<span data-ttu-id="a784b-230">En supposant que le référentiel de passerelle hello se trouve dans hello **/home/pi/iot-edge /** dossier, configurez le module d’enregistreur d’événements hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="a784b-230">Assuming hello gateway repository is located in hello **/home/pi/iot-edge/** folder, configure hello logger module as follows:</span></span>

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

#### <a name="ble-module-configuration"></a><span data-ttu-id="a784b-231">Configuration du module BLE</span><span class="sxs-lookup"><span data-stu-id="a784b-231">BLE module configuration</span></span>

<span data-ttu-id="a784b-232">configuration d’exemple Hello pour appareil BLE hello suppose un appareil Texas Instruments SensorTag.</span><span class="sxs-lookup"><span data-stu-id="a784b-232">hello sample configuration for hello BLE device assumes a Texas Instruments SensorTag device.</span></span> <span data-ttu-id="a784b-233">N’importe quel appareil BLE standard qui peut fonctionner comme un périphérique de GATT doit fonctionner, mais vous devrez peut-être caractéristique de GATT hello tooupdate ID et les données.</span><span class="sxs-lookup"><span data-stu-id="a784b-233">Any standard BLE device that can operate as a GATT peripheral should work but you may need tooupdate hello GATT characteristic IDs and data.</span></span> <span data-ttu-id="a784b-234">Ajouter une adresse MAC de hello de votre périphérique SensorTag :</span><span class="sxs-lookup"><span data-stu-id="a784b-234">Add hello MAC address of your SensorTag device:</span></span>

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

<span data-ttu-id="a784b-235">Si vous n’utilisez pas un appareil SensorTag, passez en revue documentation hello pour votre toodetermine de périphérique BLE si vous avez besoin de caractéristique de GATT hello tooupdate ID et les valeurs de données.</span><span class="sxs-lookup"><span data-stu-id="a784b-235">If you are not using a SensorTag device, review hello documentation for your BLE device toodetermine whether you need tooupdate hello GATT characteristic IDs and data values.</span></span>

#### <a name="iot-hub-module"></a><span data-ttu-id="a784b-236">module IoT Hub</span><span class="sxs-lookup"><span data-stu-id="a784b-236">IoT Hub module</span></span>

<span data-ttu-id="a784b-237">Ajouter le nom hello de votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="a784b-237">Add hello name of your IoT Hub.</span></span> <span data-ttu-id="a784b-238">valeur de suffixe Hello est généralement **azure-devices.net**:</span><span class="sxs-lookup"><span data-stu-id="a784b-238">hello suffix value is typically **azure-devices.net**:</span></span>

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

#### <a name="identity-mapping-module-configuration"></a><span data-ttu-id="a784b-239">Configuration du mappage d’identité</span><span class="sxs-lookup"><span data-stu-id="a784b-239">Identity mapping module configuration</span></span>

<span data-ttu-id="a784b-240">Ajouter une adresse MAC de hello de SensorTag appareil et hello périphérique ID et votre clé de hello **SensorTag_01** appareil que vous avez ajouté tooyour IoT Hub :</span><span class="sxs-lookup"><span data-stu-id="a784b-240">Add hello MAC address of your SensorTag device and hello device ID and key of hello **SensorTag_01** device you added tooyour IoT Hub:</span></span>

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

#### <a name="ble-printer-module-configuration"></a><span data-ttu-id="a784b-241">Configuration du module d’imprimante BLE</span><span class="sxs-lookup"><span data-stu-id="a784b-241">BLE Printer module configuration</span></span>

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

#### <a name="blec2d-module-configuration"></a><span data-ttu-id="a784b-242">Configuration du module BLEC2D</span><span class="sxs-lookup"><span data-stu-id="a784b-242">BLEC2D Module Configuration</span></span>

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

#### <a name="routing-configuration"></a><span data-ttu-id="a784b-243">Configuration du routage</span><span class="sxs-lookup"><span data-stu-id="a784b-243">Routing Configuration</span></span>

<span data-ttu-id="a784b-244">Hello configuration suivante garantit suivant de hello routage entre les modules IoT bord :</span><span class="sxs-lookup"><span data-stu-id="a784b-244">hello following configuration ensures hello following routing between IoT Edge modules:</span></span>

* <span data-ttu-id="a784b-245">Hello **journal** module reçoit et enregistre tous les messages.</span><span class="sxs-lookup"><span data-stu-id="a784b-245">hello **Logger** module receives and logs all messages.</span></span>
* <span data-ttu-id="a784b-246">Hello **SensorTag** module envoie hello tooboth de messages **mappage** et **BLE imprimante** modules.</span><span class="sxs-lookup"><span data-stu-id="a784b-246">hello **SensorTag** module sends messages tooboth hello **mapping** and **BLE Printer** modules.</span></span>
* <span data-ttu-id="a784b-247">Hello **mappage** module envoie des messages toohello **IoTHub** toobe module envoyé tooyour IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="a784b-247">hello **mapping** module sends messages toohello **IoTHub** module toobe sent up tooyour IoT Hub.</span></span>
* <span data-ttu-id="a784b-248">Hello **IoTHub** module envoie des messages au toohello **mappage** module.</span><span class="sxs-lookup"><span data-stu-id="a784b-248">hello **IoTHub** module sends messages back toohello **mapping** module.</span></span>
* <span data-ttu-id="a784b-249">Hello **mappage** module envoie des messages toohello **BLEC2D** module.</span><span class="sxs-lookup"><span data-stu-id="a784b-249">hello **mapping** module sends messages toohello **BLEC2D** module.</span></span>
* <span data-ttu-id="a784b-250">Hello **BLEC2D** module envoie des messages au toohello **capteur balise** module.</span><span class="sxs-lookup"><span data-stu-id="a784b-250">hello **BLEC2D** module sends messages back toohello **Sensor Tag** module.</span></span>

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

<span data-ttu-id="a784b-251">exemple hello de toorun, fichier configuration passe hello chemin d’accès toohello JSON comme un paramètre de toohello **ble\_passerelle** binaire.</span><span class="sxs-lookup"><span data-stu-id="a784b-251">toorun hello sample, pass hello path toohello JSON configuration file as a parameter toohello **ble\_gateway** binary.</span></span> <span data-ttu-id="a784b-252">Hello commande suivante suppose que vous utilisez hello **gateway_sample.json** fichier de configuration.</span><span class="sxs-lookup"><span data-stu-id="a784b-252">hello following command assumes you are using hello **gateway_sample.json** configuration file.</span></span> <span data-ttu-id="a784b-253">Exécutez la commande suivante à partir de hello **iot-bord** dossier hello framboises Pi :</span><span class="sxs-lookup"><span data-stu-id="a784b-253">Execute this command from hello **iot-edge** folder on hello Raspberry Pi:</span></span>

```sh
./build/samples/ble_gateway/ble_gateway ./samples/ble_gateway/src/gateway_sample.json
```

<span data-ttu-id="a784b-254">Vous devrez peut-être toopress hello petit bouton hello SensorTag périphérique toomake il détectables avant d’exécuter les exemples hello.</span><span class="sxs-lookup"><span data-stu-id="a784b-254">You may need toopress hello small button on hello SensorTag device toomake it discoverable before you run hello sample.</span></span>

<span data-ttu-id="a784b-255">Lorsque vous exécutez hello, exemple, vous pouvez utiliser hello [Explorateur de périphérique](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) ou hello [iothub-explorer](https://github.com/Azure/iothub-explorer) outil toomonitor Bonjour messages Bonjour IoT passerelle transfère à partir de l’appareil de SensorTag hello.</span><span class="sxs-lookup"><span data-stu-id="a784b-255">When you run hello sample, you can use hello [device explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) or hello [iothub-explorer](https://github.com/Azure/iothub-explorer) tool toomonitor hello messages hello IoT Edge gateway forwards from hello SensorTag device.</span></span> <span data-ttu-id="a784b-256">Par exemple, à l’aide de l’Explorateur du iothub vous pouvez surveiller les messages de périphérique dans le cloud à l’aide de hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="a784b-256">For example, using iothub-explorer you can monitor device-to-cloud messages using hello following command:</span></span>

```sh
iothub-explorer monitor-events --login "HostName={Your iot hub name}.azure-devices.net;SharedAccessKeyName=iothubowner;SharedAccessKey={Your IoT Hub key}"
```

## <a name="send-cloud-to-device-messages"></a><span data-ttu-id="a784b-257">Envoi de messages cloud vers appareil</span><span class="sxs-lookup"><span data-stu-id="a784b-257">Send cloud-to-device messages</span></span>

<span data-ttu-id="a784b-258">module BLE Hello prend également en charge l’envoi de commandes à partir de l’appareil de toohello IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="a784b-258">hello BLE module also supports sending commands from IoT Hub toohello device.</span></span> <span data-ttu-id="a784b-259">Vous pouvez utiliser hello [Explorateur de périphérique](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) ou hello [iothub-explorer](https://github.com/Azure/iothub-explorer) transfère les messages de l’outil toosend JSON ce module de passerelle BLE hello sur l’appareil BLE toohello.</span><span class="sxs-lookup"><span data-stu-id="a784b-259">You can use hello [device explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) or hello [iothub-explorer](https://github.com/Azure/iothub-explorer) tool toosend JSON messages that hello BLE gateway module forwards on toohello BLE device.</span></span>

<span data-ttu-id="a784b-260">Si vous utilisez un périphérique de Texas Instruments SensorTag hello, vous pouvez activer les DEL hello rouge, vert ou alarme sonore en envoyant des commandes à partir de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="a784b-260">If you are using hello Texas Instruments SensorTag device, you can turn on hello red LED, green LED, or buzzer by sending commands from IoT Hub.</span></span> <span data-ttu-id="a784b-261">Avant d’envoyer des commandes à partir de IoT Hub, d’abord envoyer hello suivant deux messages JSON dans l’ordre.</span><span class="sxs-lookup"><span data-stu-id="a784b-261">Before you send commands from IoT Hub, first send hello following two JSON messages in order.</span></span> <span data-ttu-id="a784b-262">Ensuite, vous pouvez envoyer des tooturn de commandes hello sur les témoins lumineux de hello ou alarme sonore.</span><span class="sxs-lookup"><span data-stu-id="a784b-262">Then you can send any of hello commands tooturn on hello lights or buzzer.</span></span>

1. <span data-ttu-id="a784b-263">Réinitialiser tous les voyants et alarme sonore de hello (les mettre hors tension) :</span><span class="sxs-lookup"><span data-stu-id="a784b-263">Reset all LEDs and hello buzzer (turn them off):</span></span>

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "AA=="
    }
    ```

1. <span data-ttu-id="a784b-264">Configurer les E/S en tant que « à distance » :</span><span class="sxs-lookup"><span data-stu-id="a784b-264">Configure I/O as 'remote':</span></span>

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA66-0451-4000-B000-000000000000",
      "data": "AQ=="
    }
    ```

<span data-ttu-id="a784b-265">Vous pouvez maintenant envoyer des hello suivant de commandes tooturn sur les témoins lumineux de hello ou alarme sonore sur le périphérique de SensorTag hello :</span><span class="sxs-lookup"><span data-stu-id="a784b-265">Now you can send any of hello following commands tooturn on hello lights or buzzer on hello SensorTag device:</span></span>

* <span data-ttu-id="a784b-266">Activer les DEL hello rouge :</span><span class="sxs-lookup"><span data-stu-id="a784b-266">Turn on hello red LED:</span></span>

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "AQ=="
    }
    ```

* <span data-ttu-id="a784b-267">Activer les DEL hello vert :</span><span class="sxs-lookup"><span data-stu-id="a784b-267">Turn on hello green LED:</span></span>

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "Ag=="
    }
    ```

* <span data-ttu-id="a784b-268">Activer l’alarme sonore de hello :</span><span class="sxs-lookup"><span data-stu-id="a784b-268">Turn on hello buzzer:</span></span>

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "BA=="
    }
    ```

## <a name="next-steps"></a><span data-ttu-id="a784b-269">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a784b-269">Next Steps</span></span>

<span data-ttu-id="a784b-270">Si vous souhaitez toogain une plus grande maîtrise du bord de IoT et faire des essais avec quelques exemples de code, visitez hello développeur didacticiels et ressources :</span><span class="sxs-lookup"><span data-stu-id="a784b-270">If you want toogain a more advanced understanding of IoT Edge and experiment with some code examples, visit hello following developer tutorials and resources:</span></span>

* <span data-ttu-id="a784b-271">[Azure IoT Edge][lnk-sdk]</span><span class="sxs-lookup"><span data-stu-id="a784b-271">[Azure IoT Edge][lnk-sdk]</span></span>

<span data-ttu-id="a784b-272">toofurther Explorez les fonctionnalités de hello d’IoT Hub, consultez :</span><span class="sxs-lookup"><span data-stu-id="a784b-272">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="a784b-273">[Guide du développeur IoT Hub][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="a784b-273">[IoT Hub developer guide][lnk-devguide]</span></span>

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
