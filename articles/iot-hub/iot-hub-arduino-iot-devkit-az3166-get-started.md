---
title: "aaaIoT DevKit toocloud - tooAzure de se connecter AZ3166 de kit de développement IoT IoT Hub | Documents Microsoft"
description: "Découvrez comment toosetup et connectez-vous tooAzure AZ3166 du Kit de développement IoT IoT Hub pour qu’il plateforme de cloud computing Azure toosend données toohello dans ce didacticiel."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: 
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/11/2017
ms.author: xshi
ms.openlocfilehash: fd36abaed1fd9f73028b84312bca9e900fb9c004
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-iot-devkit-az3166-tooazure-iot-hub-in-hello-cloud"></a><span data-ttu-id="d1810-103">Se connecter AZ3166 du Kit de développement IoT tooAzure IoT Hub dans le cloud de hello</span><span class="sxs-lookup"><span data-stu-id="d1810-103">Connect IoT DevKit AZ3166 tooAzure IoT Hub in hello cloud</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="d1810-104">Hello [MXChip IoT DevKit](https://microsoft.github.io/azure-iot-developer-kit/) peuvent être utilisé toodevelop et prototype solutions Internet of Things (IoT) en exploitant les services Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="d1810-104">hello [MXChip IoT DevKit](https://microsoft.github.io/azure-iot-developer-kit/) can be used toodevelop and prototype Internet of Things (IoT) solutions leveraging Microsoft Azure services.</span></span> <span data-ttu-id="d1810-105">Il comprend une carte compatible avec Arduino et équipée d’un large éventail de périphériques et de capteurs, un package de carte open source et un [catalogue de projets](https://microsoft.github.io/azure-iot-developer-kit/docs/projects/) grandissant.</span><span class="sxs-lookup"><span data-stu-id="d1810-105">It includes an Arduino compatible board with rich peripherals and sensors, an open-source board package and a growing [projects catalog](https://microsoft.github.io/azure-iot-developer-kit/docs/projects/).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="d1810-106">Procédure</span><span class="sxs-lookup"><span data-stu-id="d1810-106">What you do</span></span>
<span data-ttu-id="d1810-107">Se connecter [DevKit](https://microsoft.github.io/azure-iot-developer-kit/) tooan Azure IoT hub que vous créez, données de température et humidité hello collecter à partir des capteurs et envoyez le concentrateur de tooIoT données hello.</span><span class="sxs-lookup"><span data-stu-id="d1810-107">Connect [DevKit](https://microsoft.github.io/azure-iot-developer-kit/) tooan Azure IoT hub that you create, collect hello temperature and humidity data from sensors and send hello data tooIoT hub.</span></span>

<span data-ttu-id="d1810-108">Vous n’avez pas encore de DevKit ?</span><span class="sxs-lookup"><span data-stu-id="d1810-108">Don't have a DevKit yet?</span></span> <span data-ttu-id="d1810-109">Cliquez [ici](https://aka.ms/iot-devkit-purchase) pour en obtenir un.</span><span class="sxs-lookup"><span data-stu-id="d1810-109">Get a new one [here](https://aka.ms/iot-devkit-purchase).</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="d1810-110">Contenu</span><span class="sxs-lookup"><span data-stu-id="d1810-110">What you learn</span></span>

* <span data-ttu-id="d1810-111">Comment tooconnect IoT DevKit tooWireless accès point et préparer votre environnement de développement.</span><span class="sxs-lookup"><span data-stu-id="d1810-111">How tooconnect IoT DevKit tooWireless access point and prepare your development environment.</span></span>
* <span data-ttu-id="d1810-112">Comment toocreate un IoT hub et inscrire un appareil pour le Kit de développement MXChip IoT.</span><span class="sxs-lookup"><span data-stu-id="d1810-112">How toocreate an IoT hub and register a device for MXChip IoT DevKit.</span></span>
* <span data-ttu-id="d1810-113">Comment les données de capteur toocollect par un exemple d’application en cours d’exécution sur le Kit de développement MXChip IoT.</span><span class="sxs-lookup"><span data-stu-id="d1810-113">How toocollect sensor data by running a sample application on MXChip IoT DevKit.</span></span>
* <span data-ttu-id="d1810-114">Comment toosend hello tooyour IoT hub capteur données.</span><span class="sxs-lookup"><span data-stu-id="d1810-114">How toosend hello sensor data tooyour IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="d1810-115">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="d1810-115">What you need</span></span>

* <span data-ttu-id="d1810-116">Une carte MXChip IoT DevKit avec câble micro USB.</span><span class="sxs-lookup"><span data-stu-id="d1810-116">An MXChip IoT DevKit board with a micro USB cable.</span></span> <span data-ttu-id="d1810-117">[Cliquez ici pour l’obtenir](https://aka.ms/iot-devkit-purchase).</span><span class="sxs-lookup"><span data-stu-id="d1810-117">[Get it now](https://aka.ms/iot-devkit-purchase)</span></span>
* <span data-ttu-id="d1810-118">Un ordinateur sous Windows 10 ou macOS 10.10 ou une version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="d1810-118">A computer running Windows 10 or macOS 10.10+</span></span>
* <span data-ttu-id="d1810-119">Un abonnement Azure actif</span><span class="sxs-lookup"><span data-stu-id="d1810-119">An active Azure subscription</span></span>
  * <span data-ttu-id="d1810-120">Activez un [compte d’évaluation Microsoft Azure gratuit pendant 30 jours](https://azureinfo.microsoft.com/us-freetrial.html).</span><span class="sxs-lookup"><span data-stu-id="d1810-120">Activate a [free 30-day trial Microsoft Azure account](https://azureinfo.microsoft.com/us-freetrial.html)</span></span>

## <a name="prepare-your-hardware"></a><span data-ttu-id="d1810-121">Préparation du matériel</span><span class="sxs-lookup"><span data-stu-id="d1810-121">Prepare your hardware</span></span>

<span data-ttu-id="d1810-122">Raccorder hello matériel tooyour ordinateur.</span><span class="sxs-lookup"><span data-stu-id="d1810-122">Hook up hello hardware tooyour computer.</span></span>

### <a name="hardware-you-need"></a><span data-ttu-id="d1810-123">Matériel nécessaire</span><span class="sxs-lookup"><span data-stu-id="d1810-123">Hardware you need</span></span>

* <span data-ttu-id="d1810-124">Carte DevKit</span><span class="sxs-lookup"><span data-stu-id="d1810-124">DevKit board</span></span>
* <span data-ttu-id="d1810-125">Câble micro USB</span><span class="sxs-lookup"><span data-stu-id="d1810-125">Micro USB cable</span></span>

![bien-démarrer-matériel](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/hardware.jpg)

### <a name="connect-devkit-tooyour-computer"></a><span data-ttu-id="d1810-127">Kit de développement tooyour ordinateur connecté</span><span class="sxs-lookup"><span data-stu-id="d1810-127">Connect DevKit tooyour computer</span></span>

1. <span data-ttu-id="d1810-128">Connexion USB fin tooyour PC</span><span class="sxs-lookup"><span data-stu-id="d1810-128">Connect USB end tooyour PC</span></span>
2. <span data-ttu-id="d1810-129">Se connecter Micro USB fin toohello Kit de développement</span><span class="sxs-lookup"><span data-stu-id="d1810-129">Connect Micro USB end toohello DevKit</span></span>
3. <span data-ttu-id="d1810-130">toopower suivant de LED Hello verte confirme la connexion</span><span class="sxs-lookup"><span data-stu-id="d1810-130">hello green LED next toopower confirms connection</span></span>

![bien-démarrer-connexion](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/connect.jpg)

## <a name="configure-wifi"></a><span data-ttu-id="d1810-132">Configurer le WiFi</span><span class="sxs-lookup"><span data-stu-id="d1810-132">Configure WiFi</span></span>

<span data-ttu-id="d1810-133">Les projets IoT dépendent de la connectivité à Internet.</span><span class="sxs-lookup"><span data-stu-id="d1810-133">IoT projects rely on Internet connectivity.</span></span> <span data-ttu-id="d1810-134">Utilisez hello suivant les instructions tooconfigure hello DevKit tooconnect tooWiFi.</span><span class="sxs-lookup"><span data-stu-id="d1810-134">Use hello following instructions tooconfigure hello DevKit tooconnect tooWiFi.</span></span>

### <a name="enter-ap-mode"></a><span data-ttu-id="d1810-135">Activer le mode « point d’accès »</span><span class="sxs-lookup"><span data-stu-id="d1810-135">Enter AP Mode</span></span>

<span data-ttu-id="d1810-136">Maintenez le bouton B, puis push et relâchez le bouton Réinitialiser de hello, puis le bouton de mise en production B. Votre Kit de développement passe en Mode de point d’accès de configuration Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="d1810-136">Hold down button B, then push and release hello reset button, then release button B. Your DevKit will enter AP Mode for configuring WiFi.</span></span> <span data-ttu-id="d1810-137">écran Hello affiche hello Service définir Identifier(SSID) Hello Kit de développement ainsi que d’adresse IP du portail configuration hello :</span><span class="sxs-lookup"><span data-stu-id="d1810-137">hello screen will display hello Service Set Identifier(SSID) of hello DevKit as well as hello configuration portal IP address:</span></span>

![bien-démarrer-point-d-accès-wifi](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/wifi-ap.jpg)

### <a name="connect-toodevkit-ap"></a><span data-ttu-id="d1810-139">Se connecter tooDevKit l’Asie-Pacifique</span><span class="sxs-lookup"><span data-stu-id="d1810-139">Connect tooDevKit AP</span></span>

<span data-ttu-id="d1810-140">À présent, utiliser un autre Wi-Fi activée périphériques (PC ou un téléphone mobile) tooconnect toohello SSID DevKit (mis en surbrillance dans la capture d’écran hello ci-dessus), laissez le mot de passe hello vide.</span><span class="sxs-lookup"><span data-stu-id="d1810-140">Now, use another WiFi enabled device (PC or mobile phone) tooconnect toohello DevKit SSID (highlighted in hello screenshot above), leave hello password empty.</span></span>

![bien-démarrer-ssid](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/connect-ssid.png)

### <a name="configure-wifi-for-devkit"></a><span data-ttu-id="d1810-142">Configurer le WiFi pour DevKit</span><span class="sxs-lookup"><span data-stu-id="d1810-142">Configure WiFi for DevKit</span></span>

<span data-ttu-id="d1810-143">Adresse IP de hello ouverte à l’écran du Kit de développement hello sur votre PC ou d’un navigateur de téléphone mobile, sélectionnez hello Wi-Fi réseau tooconnect du Kit de développement hello à, puis tapez le mot de passe hello.</span><span class="sxs-lookup"><span data-stu-id="d1810-143">Open hello IP address shown on hello DevKit screen on your PC or mobile phone browser, select hello WiFi network you want hello DevKit tooconnect to, then type hello password.</span></span> <span data-ttu-id="d1810-144">Cliquez sur **Connect** toocomplete :</span><span class="sxs-lookup"><span data-stu-id="d1810-144">Click **Connect** toocomplete:</span></span>

![bien-démarrer-portail-wifi](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/wifi-portal.png)

<span data-ttu-id="d1810-146">Une fois la connexion de hello réussit, hello Kit de développement redémarrera dans quelques secondes.</span><span class="sxs-lookup"><span data-stu-id="d1810-146">Once hello connection succeeds, hello DevKit will reboot in a few seconds.</span></span> <span data-ttu-id="d1810-147">Si a réussi, vous verrez hello Wi-Fi nom et adresse IP sur l’écran hello :</span><span class="sxs-lookup"><span data-stu-id="d1810-147">If succeeded, you will see hello WiFi name and IP address on hello screen:</span></span>

![bien-démarrer-ip-wifi](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/wifi-ip.jpg)

> [!NOTE] 
<span data-ttu-id="d1810-149">adresse IP de Hello dans photo de hello ne correspondent ne peut-être pas hello réel affecté et IP affichées sur l’écran du Kit de développement hello.</span><span class="sxs-lookup"><span data-stu-id="d1810-149">hello IP address displayed in hello photo may not match hello actual IP assigned and displayed on hello DevKit screen.</span></span> <span data-ttu-id="d1810-150">Ce comportement est normal de Wi-Fi qui utilise DHCP toodynamically affecter des adresses IP.</span><span class="sxs-lookup"><span data-stu-id="d1810-150">This is normal as WiFi uses DHCP toodynamically assign IPs.</span></span>

<span data-ttu-id="d1810-151">Après la configuration Wi-Fi, vos informations d’identification sont rendues persistantes sur l’appareil hello pour cette connexion, même si déconnecté.</span><span class="sxs-lookup"><span data-stu-id="d1810-151">After WiFi is configured, your credentials will be persisted on hello device for that connection, even if unplugged.</span></span> <span data-ttu-id="d1810-152">Par exemple, si vous configuré hello Kit de développement pour Wi-Fi à votre domicile et a ensuite pris office de toohello hello Kit de développement, vous devez tooreconfigure PA mode (commençant à l’étape **passer en Mode de l’Asie-Pacifique**) tooconnect hello DevKit tooyour office Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="d1810-152">For example, if you configured hello DevKit for WiFi in your home and then took hello DevKit toohello office, you will need tooreconfigure AP mode (starting at step **Enter AP Mode**) tooconnect hello DevKit tooyour office WiFi.</span></span> 

## <a name="start-using-devkit"></a><span data-ttu-id="d1810-153">Commencer à utiliser DevKit</span><span class="sxs-lookup"><span data-stu-id="d1810-153">Start using DevKit</span></span>

<span data-ttu-id="d1810-154">application par défaut de Hello en cours d’exécution sur le Kit de développement vérifie hello dernière version du microprogramme de hello et afficher des données de diagnostic de capteur pour vous.</span><span class="sxs-lookup"><span data-stu-id="d1810-154">hello default app running on DevKit will check hello latest version of hello firmware and display some sensor diagnosis data for you.</span></span>

### <a name="upgrade-toohello-latest-firmware"></a><span data-ttu-id="d1810-155">Mettre à niveau le microprogramme toohello</span><span class="sxs-lookup"><span data-stu-id="d1810-155">Upgrade toohello latest firmware</span></span>

<span data-ttu-id="d1810-156">Vous êtes invité à l’écran hello que deux hello version du microprogramme actuel et la plus récente s’il existe une mise à niveau si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="d1810-156">You will be prompted on hello screen both hello current and latest firmware version if there is an upgrade needed.</span></span> <span data-ttu-id="d1810-157">Suivez [mise à niveau du microprogramme](https://microsoft.github.io/azure-iot-developer-kit/docs/upgrading/) guide tooupgrade il.</span><span class="sxs-lookup"><span data-stu-id="d1810-157">Follow [Upgrade firmware](https://microsoft.github.io/azure-iot-developer-kit/docs/upgrading/) guide tooupgrade it.</span></span>

![bien-démarrer-microprogramme](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/firmware.jpg)

> [!NOTE] 
<span data-ttu-id="d1810-159">Il s’agit d’un effort à usage unique, une fois que vous démarrez le développement sur le Kit de développement de hello et télécharger votre application, vous devez le dernier microprogramme de hello sont fournis avec votre application.</span><span class="sxs-lookup"><span data-stu-id="d1810-159">This is a one-time effort, once you start developing on hello DevKit and upload your app, you will have hello latest firmware come with your app.</span></span>

### <a name="test-various-sensors"></a><span data-ttu-id="d1810-160">Tester divers capteurs</span><span class="sxs-lookup"><span data-stu-id="d1810-160">Test various sensors</span></span>

<span data-ttu-id="d1810-161">Appuyez sur les capteurs tootest bouton B, continuer en appuyant sur et en libérant hello B bouton toocycle via chaque capteur.</span><span class="sxs-lookup"><span data-stu-id="d1810-161">Press button B tootest sensors, continue pressing and releasing hello B button toocycle through each sensor.</span></span>

![bien-démarrer-capteurs](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/sensors.jpg)

## <a name="prepare-development-environment"></a><span data-ttu-id="d1810-163">Préparer l’environnement de développement</span><span class="sxs-lookup"><span data-stu-id="d1810-163">Prepare development environment</span></span>

<span data-ttu-id="d1810-164">À présent, il tooset temps d’environnement de développement hello : outils et les packages pour toobuild IoT applications surprenantes.</span><span class="sxs-lookup"><span data-stu-id="d1810-164">Now it's time tooset up hello development environment: tools and packages for you toobuild stunning IoT applications.</span></span> <span data-ttu-id="d1810-165">Vous pouvez choisir la version Windows ou macOS selon le système d’exploitation de tooyour.</span><span class="sxs-lookup"><span data-stu-id="d1810-165">You can choose Windows or macOS version according tooyour operating system.</span></span>


### <a name="windows"></a><span data-ttu-id="d1810-166">Windows</span><span class="sxs-lookup"><span data-stu-id="d1810-166">Windows</span></span>

<span data-ttu-id="d1810-167">Nous vous invitons à vous toouse hello installation package tooprepare hello environnement de développement.</span><span class="sxs-lookup"><span data-stu-id="d1810-167">We encourage you toouse hello installation package tooprepare hello development environment.</span></span> <span data-ttu-id="d1810-168">Si vous rencontrez des problèmes, vous pouvez suivre hello [étapes manuelles](https://microsoft.github.io/azure-iot-developer-kit/docs/installation/) tooget il fait.</span><span class="sxs-lookup"><span data-stu-id="d1810-168">If you encounter any issues, you can follow hello [manual steps](https://microsoft.github.io/azure-iot-developer-kit/docs/installation/) tooget it done.</span></span>

#### <a name="download-latest-package"></a><span data-ttu-id="d1810-169">Télécharger la dernière version du package</span><span class="sxs-lookup"><span data-stu-id="d1810-169">Download latest package</span></span>

<span data-ttu-id="d1810-170">Hello `.zip` fichier que vous téléchargez contient tous les outils nécessaires et les packages requis pour le développement du Kit de développement.</span><span class="sxs-lookup"><span data-stu-id="d1810-170">hello `.zip` file you download contains all necessary tools and packages required for DevKit development.</span></span>

> [!div class="button"]
[<span data-ttu-id="d1810-171">Télécharger</span><span class="sxs-lookup"><span data-stu-id="d1810-171">Download</span></span>](https://azureboard.azureedge.net/prod/installpackage/devkit_install_1.0.2.zip)


> [!NOTE] 
> <span data-ttu-id="d1810-172">Hello `.zip` fichier contient des éléments suivants de hello outils et les packages.</span><span class="sxs-lookup"><span data-stu-id="d1810-172">hello `.zip` file contains hello following tools and packages.</span></span> <span data-ttu-id="d1810-173">Si vous avez déjà des composants installés, le script de hello détectera et les ignorer.</span><span class="sxs-lookup"><span data-stu-id="d1810-173">If you already have some components installed, hello script will detect and skip them.</span></span>
> * <span data-ttu-id="d1810-174">Node.js et fils : exécution de script de configuration hello et les tâches automatisées</span><span class="sxs-lookup"><span data-stu-id="d1810-174">Node.js and Yarn: Runtime for hello setup script and automated tasks</span></span>
> * <span data-ttu-id="d1810-175">[Fichier MSI de Azure CLI 2.0](https://docs.microsoft.com//cli/azure/install-azure-cli#windows) -expérience en ligne de commande d’inter-plateformes de gestion de ressources Azure hello MSI contient les Python et pip dépendante.</span><span class="sxs-lookup"><span data-stu-id="d1810-175">[Azure CLI 2.0 MSI](https://docs.microsoft.com//cli/azure/install-azure-cli#windows) - Cross-platform command-line experience for managing Azure resources, hello MSI contains dependent Python and pip.</span></span>
> * <span data-ttu-id="d1810-176">[Visual Studio Code](https://code.visualstudio.com/) : éditeur de code léger pour le développement DevKit</span><span class="sxs-lookup"><span data-stu-id="d1810-176">[Visual Studio Code](https://code.visualstudio.com/): Lightweight code editor for DevKit development</span></span>
> * <span data-ttu-id="d1810-177">[Extension Visual Studio Code pour Arduino](https://marketplace.visualstudio.com/items?itemName=vsciot-vscode.vscode-arduino) : permet le développement Arduino dans VS Code</span><span class="sxs-lookup"><span data-stu-id="d1810-177">[Visual Studio Code extension for Arduino](https://marketplace.visualstudio.com/items?itemName=vsciot-vscode.vscode-arduino): Enables Arduino development in VS Code</span></span>
> * <span data-ttu-id="d1810-178">[Arduino IDE](https://www.arduino.cc/en/Main/Software): extension hello pour Arduino s’appuie sur cet outil</span><span class="sxs-lookup"><span data-stu-id="d1810-178">[Arduino IDE](https://www.arduino.cc/en/Main/Software): hello extension for Arduino relies on this tool</span></span>
> * <span data-ttu-id="d1810-179">Package de la carte du Kit de développement : Outil de chaînes, les bibliothèques et les projets pour hello Kit de développement</span><span class="sxs-lookup"><span data-stu-id="d1810-179">DevKit Board Package: Tool chains, libraries and projects for hello DevKit</span></span>
> * <span data-ttu-id="d1810-180">Utilitaire ST-Link : pilotes et utilitaires essentiels</span><span class="sxs-lookup"><span data-stu-id="d1810-180">ST-Link Utility: Essential utilities and drivers</span></span>

#### <a name="run-installation-script"></a><span data-ttu-id="d1810-181">Exécuter le script d’installation</span><span class="sxs-lookup"><span data-stu-id="d1810-181">Run installation script</span></span>

<span data-ttu-id="d1810-182">Dans l’Explorateur de fichiers Windows, localisez hello `.zip` et extrayez-le, recherchez `install.cmd`, avec le bouton droit et sélectionnez **« Exécuter en tant qu’administrateur »** toostart.</span><span class="sxs-lookup"><span data-stu-id="d1810-182">In Windows File Explorer, locate hello `.zip` and extract it, find `install.cmd`, right-click and select **"Run as administrator"** toostart.</span></span>

![bien-démarrer-exécution-administrateur](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/run-admin.png)

<span data-ttu-id="d1810-184">Pendant l’installation, vous verrez progression hello de chaque outil ou d’un package.</span><span class="sxs-lookup"><span data-stu-id="d1810-184">During installation, you will see hello progress of each tool or package.</span></span>

![bien-démarrer-installation](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/install.png)

#### <a name="confirm-tooinstall-drivers"></a><span data-ttu-id="d1810-186">Vérifiez les pilotes tooinstall</span><span class="sxs-lookup"><span data-stu-id="d1810-186">Confirm tooinstall drivers</span></span>

<span data-ttu-id="d1810-187">Hello VS Code pour l’extension de Arduino s’appuie sur hello Arduino IDE.</span><span class="sxs-lookup"><span data-stu-id="d1810-187">hello VS Code for Arduino extension relies on hello Arduino IDE.</span></span> <span data-ttu-id="d1810-188">S’il s’agit hello première fois que vous installez hello Arduino IDE, vous serez tooinstall demandées les pilotes appropriés :</span><span class="sxs-lookup"><span data-stu-id="d1810-188">If this is hello first time you are installing hello Arduino IDE, you will be prompted tooinstall relevant drivers:</span></span>

![bien-démarrer-pilote](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/driver.png)

<span data-ttu-id="d1810-190">Il doit prendre l’installation de toofinish environ 10 minutes en fonction de votre vitesse d’Internet.</span><span class="sxs-lookup"><span data-stu-id="d1810-190">It should take around 10 minutes toofinish installation depending on your Internet speed.</span></span> <span data-ttu-id="d1810-191">Une fois l’installation de hello est terminée, vous devez voir les raccourcis de Code Visual Studio et Arduino IDE sur votre bureau.</span><span class="sxs-lookup"><span data-stu-id="d1810-191">Once hello installation is complete, you should see Visual Studio Code and Arduino IDE shortcuts on your desktop.</span></span>

> [!NOTE] 
<span data-ttu-id="d1810-192">Au lancement de VS Code, il peut arriver qu’une erreur s’affiche, indiquant que l’IDE Arduino ou un package de carte associé est introuvable.</span><span class="sxs-lookup"><span data-stu-id="d1810-192">Occasionally, when you launch VS Code, you will be prompted with an error that cannot find Arduino IDE or related board package.</span></span> <span data-ttu-id="d1810-193">toosolve il, fermez Visual Studio Code, lancer Arduino IDE qu’une seule fois et VS Code doivent localiser les chemin d’accès Arduino IDE correctement.</span><span class="sxs-lookup"><span data-stu-id="d1810-193">toosolve it, close VS Code, launch Arduino IDE once and VS Code should locate Arduino IDE path correctly.</span></span>


### <a name="macos-preview"></a><span data-ttu-id="d1810-194">macOS (préversion)</span><span class="sxs-lookup"><span data-stu-id="d1810-194">macOS (Preview)</span></span>

<span data-ttu-id="d1810-195">Suivez ces environnement de développement tooprepare étapes macOS.</span><span class="sxs-lookup"><span data-stu-id="d1810-195">Follow these steps tooprepare development environment on macOS.</span></span>

#### <a name="install-azure-cli-20"></a><span data-ttu-id="d1810-196">Installer Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="d1810-196">Install Azure CLI 2.0</span></span>

<span data-ttu-id="d1810-197">Suivez hello [guide officiel](https://docs.microsoft.com//cli/azure/install-azure-cli) tooinstall Azure CLI 2.0 :</span><span class="sxs-lookup"><span data-stu-id="d1810-197">Follow hello [official guide](https://docs.microsoft.com//cli/azure/install-azure-cli) tooinstall Azure CLI 2.0:</span></span>

<span data-ttu-id="d1810-198">Installez Azure CLI 2.0 avec une commande `curl` :</span><span class="sxs-lookup"><span data-stu-id="d1810-198">Install Azure CLI 2.0 with one `curl` command:</span></span>

```bash
curl -L https://aka.ms/InstallAzureCli | bash
```

<span data-ttu-id="d1810-199">Et redémarrez votre interface de commande pour effet de tootake de modifications :</span><span class="sxs-lookup"><span data-stu-id="d1810-199">And restart your command shell for changes tootake effect:</span></span>

```bash
exec -l $SHELL
```

#### <a name="install-arduino-ide"></a><span data-ttu-id="d1810-200">Installer l’IDE Arduino</span><span class="sxs-lookup"><span data-stu-id="d1810-200">Install Arduino IDE</span></span>

<span data-ttu-id="d1810-201">Hello Arduino de Code Visual Studio extension s’appuie sur hello Arduino IDE.</span><span class="sxs-lookup"><span data-stu-id="d1810-201">hello Visual Studio Code Arduino extension relies on hello Arduino IDE.</span></span> <span data-ttu-id="d1810-202">Téléchargez et installez hello [Arduino IDE pour macOS](https://www.arduino.cc/en/Main/Software).</span><span class="sxs-lookup"><span data-stu-id="d1810-202">Download and install hello [Arduino IDE for macOS](https://www.arduino.cc/en/Main/Software).</span></span>

#### <a name="install-visual-studio-code"></a><span data-ttu-id="d1810-203">Installation de Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="d1810-203">Install Visual Studio Code</span></span>

<span data-ttu-id="d1810-204">Téléchargez et installez [Visual Studio Code pour macOS](https://code.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="d1810-204">Download and install [Visual Studio Code for macOS](https://code.visualstudio.com/).</span></span> <span data-ttu-id="d1810-205">Il s’agit de hello principal outil de développement pour la création d’applications DevKit IoT.</span><span class="sxs-lookup"><span data-stu-id="d1810-205">This will be hello primary development tool for building DevKit IoT applications.</span></span>

####  <a name="download-latest-package"></a><span data-ttu-id="d1810-206">Télécharger la dernière version du package</span><span class="sxs-lookup"><span data-stu-id="d1810-206">Download latest package</span></span>

1. <span data-ttu-id="d1810-207">Installez Node.js.</span><span class="sxs-lookup"><span data-stu-id="d1810-207">Install Node.js.</span></span> <span data-ttu-id="d1810-208">Vous pouvez utiliser le Gestionnaire de package macOS populaires [Homebrew](https://brew.sh/) ou [intégrées dans le programme d’installation](https://nodejs.org/en/download/) tooinstall il.</span><span class="sxs-lookup"><span data-stu-id="d1810-208">You can use popular macOS package manager [Homebrew](https://brew.sh/) or [pre-built installer](https://nodejs.org/en/download/) tooinstall it.</span></span>

2. <span data-ttu-id="d1810-209">Téléchargez le fichier `.zip` contenant les scripts de tâches requis pour le développement DevKit dans VS Code.</span><span class="sxs-lookup"><span data-stu-id="d1810-209">Download `.zip` file containing task scripts required for DevKit development in VS Code.</span></span>

   > [!div class="button"]
   [<span data-ttu-id="d1810-210">Télécharger</span><span class="sxs-lookup"><span data-stu-id="d1810-210">Download</span></span>](https://azureboard.azureedge.net/installpackage/devkit_tasks_1.0.2.zip)

   <span data-ttu-id="d1810-211">Recherchez hello `.zip` et extrayez-le.</span><span class="sxs-lookup"><span data-stu-id="d1810-211">Locate hello `.zip` and extract it.</span></span> <span data-ttu-id="d1810-212">Puis lancez **Terminal** application et exécution hello suivant tooconfigure de commandes :</span><span class="sxs-lookup"><span data-stu-id="d1810-212">Then launch **Terminal** app and run hello following commands tooconfigure:</span></span>

   <span data-ttu-id="d1810-213">Déplacez les extraits tooyour macOS utilisateur dossier :</span><span class="sxs-lookup"><span data-stu-id="d1810-213">Move extracted folder tooyour macOS user folder:</span></span>
   ```bash
   mv [.zip extracted folder]/azure-board-cli ~/. ; cd ~/azure-board-cli
   ```
  
   <span data-ttu-id="d1810-214">Installez les packages `npm` :</span><span class="sxs-lookup"><span data-stu-id="d1810-214">Install `npm` packages:</span></span>
   ```
   npm install
   ```

#### <a name="install-vs-code-extension-for-arduino"></a><span data-ttu-id="d1810-215">Installer l’extension VS Code pour Arduino</span><span class="sxs-lookup"><span data-stu-id="d1810-215">Install VS Code extension for Arduino</span></span>

<span data-ttu-id="d1810-216">Code Visual Studio permet aux extensions de Marketplace tooinstall directement dans l’outil de hello, cliquez simplement sur icône des extensions dans le volet de menu de gauche hello hello, puis recherchez `Arduino` tooinstall :</span><span class="sxs-lookup"><span data-stu-id="d1810-216">Visual Studio Code allows you tooinstall Marketplace extensions directly in hello tool, simply click hello extensions icon in hello left menu pane and then search `Arduino` tooinstall:</span></span>

![installation-extensions](media/iot-hub-arduino-devkit-az3166-get-started/installation-extensions-mac.png)

#### <a name="install-devkit-board-package"></a><span data-ttu-id="d1810-218">Installer le package de carte DevKit</span><span class="sxs-lookup"><span data-stu-id="d1810-218">Install DevKit board package</span></span>

<span data-ttu-id="d1810-219">Vous aurez besoin à l’aide de hello Gestionnaire de tableau dans Visual Studio Code le Kit de développement tableau tooadd hello.</span><span class="sxs-lookup"><span data-stu-id="d1810-219">You will need tooadd hello DevKit board using hello Board Manager in Visual Studio Code.</span></span>

1. <span data-ttu-id="d1810-220">Utilisez `Cmd+Shift+P` palette et le type de commande tooinvoke **Arduino** puis recherchez et sélectionnez **Arduino : Gestionnaire de tableau**.</span><span class="sxs-lookup"><span data-stu-id="d1810-220">Use `Cmd+Shift+P` tooinvoke command palette and type **Arduino** then find and select **Arduino: Board Manager**.</span></span>

2. <span data-ttu-id="d1810-221">Cliquez sur **'URL supplémentaires'** en bas de hello à droite.</span><span class="sxs-lookup"><span data-stu-id="d1810-221">Click **'Additional URLs'** at hello bottom right.</span></span>
   <span data-ttu-id="d1810-222">![installation-url-supplémentaires](media/iot-hub-arduino-devkit-az3166-get-started/installation-additional-urls-mac.png)</span><span class="sxs-lookup"><span data-stu-id="d1810-222">![installation-additional-urls](media/iot-hub-arduino-devkit-az3166-get-started/installation-additional-urls-mac.png)</span></span>

3. <span data-ttu-id="d1810-223">Bonjour `settings.json` , ajoutez une ligne au bas de hello de `USER SETTINGS` volet et l’enregistrer.</span><span class="sxs-lookup"><span data-stu-id="d1810-223">In hello `settings.json` file, add a line at hello bottom of `USER SETTINGS` pane and save.</span></span>
   ```json
   "arduino.additionalUrls": "https://raw.githubusercontent.com/VSChina/azureiotdevkit_tools/master/package_azureboard_index.json"
   ```
   ![installation-paramètres-json](media/iot-hub-arduino-devkit-az3166-get-started/installation-settings-json-mac.png)

4. <span data-ttu-id="d1810-225">Maintenant Bonjour Gestionnaire de tableau de rechercher « az3166 » et installer la version la plus récente hello.</span><span class="sxs-lookup"><span data-stu-id="d1810-225">Now in hello Board Manager search for 'az3166' and install hello latest version.</span></span>
   <span data-ttu-id="d1810-226">![installation-az3166](media/iot-hub-arduino-devkit-az3166-get-started/installation-az3166-mac.png)</span><span class="sxs-lookup"><span data-stu-id="d1810-226">![installation-az3166](media/iot-hub-arduino-devkit-az3166-get-started/installation-az3166-mac.png)</span></span>

<span data-ttu-id="d1810-227">Vous avez maintenant tous les outils nécessaires de hello et les packages installés pour macOS.</span><span class="sxs-lookup"><span data-stu-id="d1810-227">You now have all hello necessary tools and packages installed for macOS.</span></span>


## <a name="open-project-folder"></a><span data-ttu-id="d1810-228">Ouvrir un dossier de projet</span><span class="sxs-lookup"><span data-stu-id="d1810-228">Open project folder</span></span>

### <a name="launch-vs-code"></a><span data-ttu-id="d1810-229">Lancer VS Code</span><span class="sxs-lookup"><span data-stu-id="d1810-229">Launch VS Code</span></span>

<span data-ttu-id="d1810-230">Assurez-vous que votre DevKit n’est pas connecté.</span><span class="sxs-lookup"><span data-stu-id="d1810-230">Make sure your DevKit is not connected.</span></span> <span data-ttu-id="d1810-231">Lancez VS Code tout d’abord, puis connectez hello DevKit tooyour ordinateur.</span><span class="sxs-lookup"><span data-stu-id="d1810-231">Launch VS Code first and connect hello DevKit tooyour computer.</span></span> <span data-ttu-id="d1810-232">VS Code le détecte automatiquement et ouvre une page d’introduction :</span><span class="sxs-lookup"><span data-stu-id="d1810-232">VS Code will automatically find it and pop up an introduction page:</span></span>

![mini-solution-vscode](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution-vscode.png)

> [!NOTE] 
<span data-ttu-id="d1810-234">Au lancement de VS Code, il peut arriver qu’une erreur s’affiche, indiquant que l’IDE Arduino ou un package de carte associé est introuvable.</span><span class="sxs-lookup"><span data-stu-id="d1810-234">Occasionally, when you launch VS Code, you will be prompted with error that cannot find Arduino IDE or related board package.</span></span> <span data-ttu-id="d1810-235">toosolve il, fermez Visual Studio Code, relancez Arduino IDE qu’une seule fois et VS Code doivent localiser les chemin d’accès Arduino IDE correctement.</span><span class="sxs-lookup"><span data-stu-id="d1810-235">toosolve it, close VS Code, launch Arduino IDE once again and VS Code should locate Arduino IDE path correctly.</span></span>

### <a name="open-arduino-examples-folder"></a><span data-ttu-id="d1810-236">Ouvrir le dossier des exemples Arduino</span><span class="sxs-lookup"><span data-stu-id="d1810-236">Open Arduino Examples folder</span></span>

<span data-ttu-id="d1810-237">Basculer trop**'Exemples Arduino'** onglet, accédez trop`Examples for MXCHIP AZ3166 > AzureIoT` , puis cliquez sur `GetStarted`.</span><span class="sxs-lookup"><span data-stu-id="d1810-237">Switch too**'Arduino Examples'** tab, navigate too`Examples for MXCHIP AZ3166 > AzureIoT` and click on `GetStarted`.</span></span>

![mini-solution-exemples](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution-examples.png)

<span data-ttu-id="d1810-239">Si vous vous trouvez le volet de hello tooclose, tooreload il, utilisez `Ctrl+Shift+P` (macOS : `Cmd+Shift+P`) la palette et le type de commande tooinvoke **Arduino** toofind et sélectionnez **Arduino : exemples**.</span><span class="sxs-lookup"><span data-stu-id="d1810-239">If you happen tooclose hello pane, tooreload it, use `Ctrl+Shift+P` (macOS: `Cmd+Shift+P`) tooinvoke command palette and type **Arduino** toofind and select **Arduino: Examples**.</span></span>

## <a name="provision-azure-services"></a><span data-ttu-id="d1810-240">Approvisionner les services Azure</span><span class="sxs-lookup"><span data-stu-id="d1810-240">Provision Azure services</span></span>

<span data-ttu-id="d1810-241">Dans la fenêtre de solution hello, exécuter la tâche `Ctrl+P` (macOS : `Cmd+P`) en tapant la configuration cloud de la tâche :</span><span class="sxs-lookup"><span data-stu-id="d1810-241">In hello solution window, run your task through `Ctrl+P` (macOS: `Cmd+P`) by typing 'task cloud-provision':</span></span>

<span data-ttu-id="d1810-242">Bonjour VS Code Terminal Server, qu'une ligne de commande interactive vous guide dans la configuration hello requis des services Azure :</span><span class="sxs-lookup"><span data-stu-id="d1810-242">In hello VS Code terminal, an interactive command line will guide you through provisioning hello required Azure services:</span></span>

![mini-solution-approvisionnement-cloud](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution/connect-iothub/cloud-provision.png)

## <a name="build-and-upload-arduino-sketch"></a><span data-ttu-id="d1810-244">Générer et charger un croquis Arduino</span><span class="sxs-lookup"><span data-stu-id="d1810-244">Build and upload Arduino sketch</span></span>

### <a name="install-required-library"></a><span data-ttu-id="d1810-245">Installer la bibliothèque requise</span><span class="sxs-lookup"><span data-stu-id="d1810-245">Install required library</span></span>

1. <span data-ttu-id="d1810-246">Appuyez sur `F1` ou `Ctrl+Shift+P` (macOS : `Cmd+Shift+P`) la palette et le type de commande tooinvoke **Arduino** puis recherchez et sélectionnez **Arduino : le Gestionnaire de bibliothèque**.</span><span class="sxs-lookup"><span data-stu-id="d1810-246">Press `F1` or `Ctrl+Shift+P` (macOS: `Cmd+Shift+P`) tooinvoke command palette and type **Arduino** then find and select **Arduino: Library Manager**.</span></span>

2. <span data-ttu-id="d1810-247">Recherchez la bibliothèque `ArduinoJson` et cliquez sur **Installer**.</span><span class="sxs-lookup"><span data-stu-id="d1810-247">Search for `ArduinoJson` library and click **Install**</span></span>

### <a name="build-and-upload-hello-device-code"></a><span data-ttu-id="d1810-248">Générer et télécharger le code de périphérique hello</span><span class="sxs-lookup"><span data-stu-id="d1810-248">Build and upload hello device code</span></span>

<span data-ttu-id="d1810-249">Utilisez `Ctrl+P` (macOS : `Cmd+P`) toorun 'appareil tâche-téléchargement'.</span><span class="sxs-lookup"><span data-stu-id="d1810-249">Use `Ctrl+P` (macOS: `Cmd+P`) toorun 'task device-upload'.</span></span> <span data-ttu-id="d1810-250">Hello Terminal Server vous invite à vous tooenter en mode de configuration.</span><span class="sxs-lookup"><span data-stu-id="d1810-250">hello terminal will prompt you tooenter configuration mode.</span></span> <span data-ttu-id="d1810-251">toodo, maintenez enfoncée la touche bouton A, puis hello par émission de données et de mise en production de bouton Réinitialiser.</span><span class="sxs-lookup"><span data-stu-id="d1810-251">toodo so, hold down button A, then push and release hello reset button.</span></span> <span data-ttu-id="d1810-252">écran Hello affiche « Configuration ».</span><span class="sxs-lookup"><span data-stu-id="d1810-252">hello screen will display 'Configuration'.</span></span> <span data-ttu-id="d1810-253">Il s’agit de chaîne de connexion de hello tooset récupère à partir de l’étape de « cloud-configuration de tâche ».</span><span class="sxs-lookup"><span data-stu-id="d1810-253">This is tooset hello connection string that retrieves from 'task cloud-provision' step.</span></span>

<span data-ttu-id="d1810-254">Ensuite, il démarre vérification et téléchargement esquisse de Arduino hello :</span><span class="sxs-lookup"><span data-stu-id="d1810-254">Then it will start verifying and uploading hello Arduino sketch:</span></span>

![mini-solution-chargement-appareil](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution/connect-iothub/device-upload.png)

<span data-ttu-id="d1810-256">Kit de développement de Hello redémarre et démarrer l’exécution du code de hello.</span><span class="sxs-lookup"><span data-stu-id="d1810-256">hello DevKit will reboot and start running hello code.</span></span>

## <a name="test-hello-project"></a><span data-ttu-id="d1810-257">Projet de test hello</span><span class="sxs-lookup"><span data-stu-id="d1810-257">Test hello project</span></span>

<span data-ttu-id="d1810-258">Dans le Code de Visual Studio, cliquez sur icône plug hello sur la barre tooopen hello série moniteur d’état hello.</span><span class="sxs-lookup"><span data-stu-id="d1810-258">In VS Code, click hello power plug icon on hello status bar tooopen hello Serial Monitor.</span></span>

<span data-ttu-id="d1810-259">exemple d’application Hello est en cours d’exécution avec succès lorsque vous consultez hello suivant des résultats :</span><span class="sxs-lookup"><span data-stu-id="d1810-259">hello sample application is running successfully when you see hello following results:</span></span>

* <span data-ttu-id="d1810-260">Hello moniteurs série hello mêmes informations en tant que contenu hello dans hello capture d’écran ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="d1810-260">hello Serial Monitor displays hello same information as hello content in hello screenshot below.</span></span>
* <span data-ttu-id="d1810-261">Hello LED sur le Kit de développement MXChip IoT clignote.</span><span class="sxs-lookup"><span data-stu-id="d1810-261">hello LED on MXChip IoT DevKit is blinking.</span></span>

![Sortie finale dans VS Code](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution/connect-iothub/result-serial-output.png)

## <a name="problems-and-feedback"></a><span data-ttu-id="d1810-263">Problèmes et commentaires</span><span class="sxs-lookup"><span data-stu-id="d1810-263">Problems and feedback</span></span>

<span data-ttu-id="d1810-264">Vous pouvez trouver [FAQ](https://microsoft.github.io/azure-iot-developer-kit/docs/faq/) si vous rencontrez des problèmes ou contacter toous à partir de canaux hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="d1810-264">You can find [FAQs](https://microsoft.github.io/azure-iot-developer-kit/docs/faq/) if you encounter problems or reach out toous from hello channels below.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d1810-265">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d1810-265">Next steps</span></span>

<span data-ttu-id="d1810-266">Vous êtes connecté avec succès un tooyour du Kit de développement MXChip IoT IoT Hub et envoyé hello capturé tooyour IoT hub capteur données.</span><span class="sxs-lookup"><span data-stu-id="d1810-266">You have successfully connected an MXChip IoT DevKit tooyour IoT Hub, and sent hello captured sensor data tooyour IoT hub.</span></span>

<span data-ttu-id="d1810-267">toocontinue mise en route avec IoT Hub et tooexplore autres scénarios IoT, consultez :</span><span class="sxs-lookup"><span data-stu-id="d1810-267">toocontinue getting started with IoT Hub and tooexplore other IoT scenarios, see:</span></span>

- [<span data-ttu-id="d1810-268">Gérer la messagerie de périphérique cloud avec iothub-explorer</span><span class="sxs-lookup"><span data-stu-id="d1810-268">Manage cloud device messaging with iothub-explorer</span></span>](https://docs.microsoft.com/azure/iot-hub/iot-hub-explorer-cloud-device-messaging)
- [<span data-ttu-id="d1810-269">Enregistrer les messages IoT Hub tooAzure le stockage de données</span><span class="sxs-lookup"><span data-stu-id="d1810-269">Save IoT Hub messages tooAzure data storage</span></span>](https://docs.microsoft.com//azure/iot-hub/iot-hub-store-data-in-azure-table-storage)
- [<span data-ttu-id="d1810-270">Utiliser des données de capteur en temps réel toovisualize Power BI à partir d’Azure IoT Hub</span><span class="sxs-lookup"><span data-stu-id="d1810-270">Use Power BI toovisualize real-time sensor data from Azure IoT Hub</span></span>](https://docs.microsoft.com//azure/iot-hub/iot-hub-live-data-visualization-in-power-bi)
- [<span data-ttu-id="d1810-271">Utiliser des données de capteur en temps réel toovisualize Azure Web Apps dans Azure IoT Hub</span><span class="sxs-lookup"><span data-stu-id="d1810-271">Use Azure Web Apps toovisualize real-time sensor data from Azure IoT Hub</span></span>](https://docs.microsoft.com//azure/iot-hub/iot-hub-live-data-visualization-in-web-apps)
- [<span data-ttu-id="d1810-272">Prévisions météorologiques à l’aide des données de capteur hello à partir de votre hub IoT dans Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="d1810-272">Weather forecast using hello sensor data from your IoT hub in Azure Machine Learning</span></span>](https://docs.microsoft.com/azure/iot-hub/iot-hub-weather-forecast-machine-learning)
- [<span data-ttu-id="d1810-273">Gestion des appareils avec iothub-explorer</span><span class="sxs-lookup"><span data-stu-id="d1810-273">Device management with iothub-explorer</span></span>](https://docs.microsoft.com/azure/iot-hub/iot-hub-device-management-iothub-explorer)
- [<span data-ttu-id="d1810-274">Surveillance à distance et notifications avec Logic Apps</span><span class="sxs-lookup"><span data-stu-id="d1810-274">Remote monitoring and notifications with Logic Apps</span></span>](https://docs.microsoft.com/azure/iot-hub/iot-hub-monitoring-notifications-with-azure-logic-apps)