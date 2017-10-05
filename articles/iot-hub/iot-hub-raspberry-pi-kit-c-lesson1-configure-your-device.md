---
title: "Connecter Raspberry Pi (C) à Azure IoT - Leçon 1 : Configurer l’appareil | Microsoft Docs"
description: "Configurez Raspberry Pi 3 pour une première utilisation et installez le système d’exploitation Raspbian, un système d’exploitation gratuit optimisé pour le matériel Raspberry Pi."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "installer raspbian, téléchargement de raspbian, installation de raspbian, configuration de raspbian, raspberry pi installer raspbian, raspberry pi installer le système d’exploitation, raspberry pi installer la carte sd, connexion de raspberry pi, connexion à raspberry pi, connectivité de raspberry pi"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: 8ee9b23c-93f7-43ff-8ea1-e7761eb87a6f
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 2a380f78d67db47a0dcab5b90843404921510528
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-your-device"></a><span data-ttu-id="13a6b-104">Configurer votre appareil</span><span class="sxs-lookup"><span data-stu-id="13a6b-104">Configure your device</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="13a6b-105">Procédure à suivre</span><span class="sxs-lookup"><span data-stu-id="13a6b-105">What you will do</span></span>
<span data-ttu-id="13a6b-106">Configurez Pi pour une première utilisation et installez le système d’exploitation Raspbian.</span><span class="sxs-lookup"><span data-stu-id="13a6b-106">Configure Pi for first-time use and install the Raspbian operating system.</span></span> <span data-ttu-id="13a6b-107">Raspbian est un système d’exploitation gratuit optimisé pour le matériel Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="13a6b-107">Raspbian is a free operating system that is optimized for the Raspberry Pi hardware.</span></span> <span data-ttu-id="13a6b-108">Si vous rencontrez des problèmes, recherchez des solutions dans la [page de résolution des problèmes](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="13a6b-108">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="13a6b-109">Contenu</span><span class="sxs-lookup"><span data-stu-id="13a6b-109">What you will learn</span></span>
<span data-ttu-id="13a6b-110">Cet article portera sur les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="13a6b-110">In this article, you will learn:</span></span>

* <span data-ttu-id="13a6b-111">Installation de Raspbian sur Pi.</span><span class="sxs-lookup"><span data-stu-id="13a6b-111">How to install Raspbian on Pi.</span></span>
* <span data-ttu-id="13a6b-112">Mise sous tension de Pi à l’aide d’un câble USB.</span><span class="sxs-lookup"><span data-stu-id="13a6b-112">How to power up Pi by using a USB cable.</span></span>
* <span data-ttu-id="13a6b-113">Connexion de Pi au réseau à l’aide d’un câble Ethernet ou d’un réseau sans fil.</span><span class="sxs-lookup"><span data-stu-id="13a6b-113">How to connect Pi to the network by using an Ethernet cable or wireless network.</span></span>
* <span data-ttu-id="13a6b-114">Ajout d’une LED sur la platine d’expérimentation et connexion à Pi.</span><span class="sxs-lookup"><span data-stu-id="13a6b-114">How to add an LED to the breadboard and connect it to Pi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="13a6b-115">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="13a6b-115">What you need</span></span>
<span data-ttu-id="13a6b-116">Pour cette opération, vous aurez besoin des composants suivants de votre Starter Kit Raspberry Pi 3 :</span><span class="sxs-lookup"><span data-stu-id="13a6b-116">To complete this operation, you need the following parts from your Raspberry Pi 3 Starter Kit:</span></span>

* <span data-ttu-id="13a6b-117">Carte Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="13a6b-117">The Raspberry Pi 3 board</span></span>
* <span data-ttu-id="13a6b-118">Carte microSD de 16 Go</span><span class="sxs-lookup"><span data-stu-id="13a6b-118">The 16-GB microSD card</span></span>
* <span data-ttu-id="13a6b-119">Alimentation 5V 2A avec le câble micro USB de 6 pieds (~183 cm)</span><span class="sxs-lookup"><span data-stu-id="13a6b-119">The 5-volt 2-amp power supply with the 6-foot micro USB cable</span></span>
* <span data-ttu-id="13a6b-120">Platine d’expérimentation</span><span class="sxs-lookup"><span data-stu-id="13a6b-120">The breadboard</span></span>
* <span data-ttu-id="13a6b-121">Câbles de connexion</span><span class="sxs-lookup"><span data-stu-id="13a6b-121">Connector wires</span></span>
* <span data-ttu-id="13a6b-122">Résistance de 560 Ohm</span><span class="sxs-lookup"><span data-stu-id="13a6b-122">A 560-ohm resistor</span></span>
* <span data-ttu-id="13a6b-123">LED de 10 mm diffuse</span><span class="sxs-lookup"><span data-stu-id="13a6b-123">A diffused 10-mm LED</span></span>
* <span data-ttu-id="13a6b-124">Câble Ethernet</span><span class="sxs-lookup"><span data-stu-id="13a6b-124">The Ethernet cable</span></span>

![Éléments de votre Starter Kit](media/iot-hub-raspberry-pi-lessons/lesson1/starter_kit.jpg)

<span data-ttu-id="13a6b-126">Vous aurez également besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="13a6b-126">You also need:</span></span>

* <span data-ttu-id="13a6b-127">Une connexion câblée ou sans fil pour la connexion de Pi.</span><span class="sxs-lookup"><span data-stu-id="13a6b-127">A wired or wireless connection for Pi to connect to.</span></span>
* <span data-ttu-id="13a6b-128">Un adaptateur USB-SD ou carte mini-SD pour graver l’image du système d’exploitation sur la carte microSD.</span><span class="sxs-lookup"><span data-stu-id="13a6b-128">A USB-SD adapter or mini-SD card to burn the OS image onto the microSD card.</span></span>
* <span data-ttu-id="13a6b-129">Un ordinateur exécutant Windows, Mac ou Linux.</span><span class="sxs-lookup"><span data-stu-id="13a6b-129">A computer running Windows, Mac, or Linux.</span></span> <span data-ttu-id="13a6b-130">L’ordinateur est utilisé pour installer Raspbian sur la carte microSD.</span><span class="sxs-lookup"><span data-stu-id="13a6b-130">The computer is used to install Raspbian on the microSD card.</span></span>
* <span data-ttu-id="13a6b-131">Une connexion Internet pour télécharger les outils et le logiciel nécessaires.</span><span class="sxs-lookup"><span data-stu-id="13a6b-131">An Internet connection to download the necessary tools and software.</span></span>

## <a name="install-raspbian-on-the-microsd-card"></a><span data-ttu-id="13a6b-132">Installation de Raspbian sur la carte microSD</span><span class="sxs-lookup"><span data-stu-id="13a6b-132">Install Raspbian on the MicroSD card</span></span>
<span data-ttu-id="13a6b-133">Préparez la carte microSD pour l’installation de l’image Raspbian.</span><span class="sxs-lookup"><span data-stu-id="13a6b-133">Prepare the microSD card for installation of the Raspbian image.</span></span>

1. <span data-ttu-id="13a6b-134">Téléchargez Raspbian.</span><span class="sxs-lookup"><span data-stu-id="13a6b-134">Download Raspbian.</span></span>
   1. <span data-ttu-id="13a6b-135">[Téléchargez](https://www.raspberrypi.org/downloads/raspbian/) le fichier .zip pour Raspbian Jessie avec Pixel.</span><span class="sxs-lookup"><span data-stu-id="13a6b-135">[Download](https://www.raspberrypi.org/downloads/raspbian/) the .zip file for Raspbian Jessie with Pixel.</span></span>
   2. <span data-ttu-id="13a6b-136">Extrayez l’image Raspbian dans un dossier sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="13a6b-136">Extract the Raspbian image to a folder on your computer.</span></span>
2. <span data-ttu-id="13a6b-137">Installez Raspbian sur la carte microSD.</span><span class="sxs-lookup"><span data-stu-id="13a6b-137">Install Raspbian to the microSD card.</span></span>
   1. <span data-ttu-id="13a6b-138">[Téléchargez](https://www.etcher.io) et installez l’utilitaire de graveur de carte SD Etcher.</span><span class="sxs-lookup"><span data-stu-id="13a6b-138">[Download](https://www.etcher.io) and install the Etcher SD card burner utility.</span></span>
   2. <span data-ttu-id="13a6b-139">Exécutez Etcher et sélectionnez l’image Raspbian extraite à l’étape 1.</span><span class="sxs-lookup"><span data-stu-id="13a6b-139">Run Etcher and select the Raspbian image that you extracted in step 1.</span></span>
   3. <span data-ttu-id="13a6b-140">Sélectionnez le lecteur de carte microSD.</span><span class="sxs-lookup"><span data-stu-id="13a6b-140">Select the microSD card drive.</span></span>
      <span data-ttu-id="13a6b-141">Remarque : Etcher a peut-être déjà sélectionné le lecteur approprié.</span><span class="sxs-lookup"><span data-stu-id="13a6b-141">Note that Etcher may have already selected the correct drive.</span></span>
   4. <span data-ttu-id="13a6b-142">Cliquez sur **Flash** pour installer Raspbian sur la carte microSD.</span><span class="sxs-lookup"><span data-stu-id="13a6b-142">Click **Flash** to install Raspbian to the microSD card.</span></span>
   5. <span data-ttu-id="13a6b-143">Retirez la carte microSD de votre ordinateur une fois l’installation terminée.</span><span class="sxs-lookup"><span data-stu-id="13a6b-143">Remove the microSD card from your computer when installation is complete.</span></span>
      <span data-ttu-id="13a6b-144">Vous pouvez retirer directement la carte microSD en toute sécurité, car Etcher éjecte ou démonte automatiquement la carte microSD une fois le processus terminé.</span><span class="sxs-lookup"><span data-stu-id="13a6b-144">It is safe to remove the microSD card directly because Etcher automatically ejects or unmounts the microSD card upon completion.</span></span>
   6. <span data-ttu-id="13a6b-145">Insérez la carte MicroSD dans votre Pi.</span><span class="sxs-lookup"><span data-stu-id="13a6b-145">Insert the microSD card into your Pi.</span></span>

![Insertion de la carte SD](media/iot-hub-raspberry-pi-lessons/lesson1/insert_sdcard.jpg)

## <a name="turn-on-pi"></a><span data-ttu-id="13a6b-147">Mise sous tension de Pi</span><span class="sxs-lookup"><span data-stu-id="13a6b-147">Turn on Pi</span></span>
<span data-ttu-id="13a6b-148">Mettez Pi sous tension à l’aide du câble micro USB et de l’alimentation.</span><span class="sxs-lookup"><span data-stu-id="13a6b-148">Turn on Pi by using the micro USB cable and the power supply.</span></span>

![Mise sous tension](media/iot-hub-raspberry-pi-lessons/lesson1/micro_usb_power_on.jpg)

> [!NOTE]
> <span data-ttu-id="13a6b-150">Il est important d’utiliser l’alimentation fournie dans le kit qui dispose d’une puissance d’au moins 2A pour vous assurer que votre Raspberry dispose d’une puissance suffisante pour fonctionner correctement.</span><span class="sxs-lookup"><span data-stu-id="13a6b-150">It is important to use the power supply in the kit that is at least 2A to make sure that your Raspberry has enough power to work correctly.</span></span>

## <a name="enable-ssh"></a><span data-ttu-id="13a6b-151">Activation de SSH</span><span class="sxs-lookup"><span data-stu-id="13a6b-151">Enable SSH</span></span>
<span data-ttu-id="13a6b-152">En date de la version de novembre 2016, Raspbian a le serveur SSH désactivé par défaut.</span><span class="sxs-lookup"><span data-stu-id="13a6b-152">As of the November 2016 release, Raspbian has the SSH server disabled by default.</span></span> <span data-ttu-id="13a6b-153">Vous devez l’activer manuellement.</span><span class="sxs-lookup"><span data-stu-id="13a6b-153">You need to enable it manually.</span></span> <span data-ttu-id="13a6b-154">Vous pouvez faire référence aux [instructions officielles](https://www.raspberrypi.org/documentation/remote-access/ssh/) ou connecter un écran et accéder à **Préférences-> Configuration de Raspberry Pi** pour activer SSH.</span><span class="sxs-lookup"><span data-stu-id="13a6b-154">You can refer to the [official instructions](https://www.raspberrypi.org/documentation/remote-access/ssh/) or connect a monitor and go to **Preferences -> Raspberry Pi Configuration** to enable SSH.</span></span>

## <a name="connect-raspberry-pi-3-to-the-network"></a><span data-ttu-id="13a6b-155">Connexion de Raspberry Pi 3 au réseau</span><span class="sxs-lookup"><span data-stu-id="13a6b-155">Connect Raspberry Pi 3 to the network</span></span>
<span data-ttu-id="13a6b-156">Vous pouvez connecter Pi à un réseau câblé ou à un réseau sans fil.</span><span class="sxs-lookup"><span data-stu-id="13a6b-156">You can connect Pi to a wired network or to a wireless network.</span></span> <span data-ttu-id="13a6b-157">Assurez-vous que Pi est connecté au même réseau que votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="13a6b-157">Make sure that Pi is connected to the same network as your computer.</span></span> <span data-ttu-id="13a6b-158">Par exemple, vous pouvez connecter Pi au même commutateur que celui utilisé par votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="13a6b-158">For example, you can connect Pi to the same switch that your computer is connected to.</span></span>

### <a name="connect-to-a-wired-network"></a><span data-ttu-id="13a6b-159">Connexion à un réseau câblé</span><span class="sxs-lookup"><span data-stu-id="13a6b-159">Connect to a wired network</span></span>
<span data-ttu-id="13a6b-160">Utilisez le câble Ethernet pour connecter Pi à votre réseau câblé.</span><span class="sxs-lookup"><span data-stu-id="13a6b-160">Use the Ethernet cable to connect Pi to your wired network.</span></span> <span data-ttu-id="13a6b-161">Si la connexion est établie, les deux LED sur Pi s’allument.</span><span class="sxs-lookup"><span data-stu-id="13a6b-161">The two LEDs on Pi turn on if the connection is established.</span></span>

![Connexion à l’aide d’un câble Ethernet](media/iot-hub-raspberry-pi-lessons/lesson1/connect_ethernet.jpg)

### <a name="connect-to-a-wireless-network"></a><span data-ttu-id="13a6b-163">Connexion à un réseau sans fil</span><span class="sxs-lookup"><span data-stu-id="13a6b-163">Connect to a wireless network</span></span>
<span data-ttu-id="13a6b-164">Suivez les [instructions](https://www.raspberrypi.org/learning/software-guide/wifi/) de Raspberry Pi Foundation pour connecter Pi à votre réseau sans fil.</span><span class="sxs-lookup"><span data-stu-id="13a6b-164">Follow the [instructions](https://www.raspberrypi.org/learning/software-guide/wifi/) from the Raspberry Pi Foundation to connect Pi to your wireless network.</span></span> <span data-ttu-id="13a6b-165">Ces instructions nécessitent tout d’abord de connecter un moniteur et un clavier à Pi.</span><span class="sxs-lookup"><span data-stu-id="13a6b-165">These instructions require you to first connect a monitor and a keyboard to Pi.</span></span>

## <a name="connect-the-led-to-pi"></a><span data-ttu-id="13a6b-166">Connexion de la LED à Pi</span><span class="sxs-lookup"><span data-stu-id="13a6b-166">Connect the LED to Pi</span></span>
<span data-ttu-id="13a6b-167">Pour effectuer cette tâche, utilisez la [platine d’expérimentation](https://learn.sparkfun.com/tutorials/how-to-use-a-breadboard), les câbles de connexion, la LED et la résistance.</span><span class="sxs-lookup"><span data-stu-id="13a6b-167">To complete this task, use the [breadboard](https://learn.sparkfun.com/tutorials/how-to-use-a-breadboard), the connector wires, the LED, and the resistor.</span></span> <span data-ttu-id="13a6b-168">Connectez-les aux ports [d’entrée/sortie à usage général](https://www.raspberrypi.org/documentation/usage/gpio/) (GPIO) de Pi.</span><span class="sxs-lookup"><span data-stu-id="13a6b-168">Connect them to the [general-purpose input/output](https://www.raspberrypi.org/documentation/usage/gpio/) (GPIO) ports of Pi.</span></span>

![Platine d’expérimentation, LED et résistance](media/iot-hub-raspberry-pi-lessons/lesson1/breadboard_led_resistor.jpg)

1. <span data-ttu-id="13a6b-170">Connectez la broche la plus courte de la LED à **GPIO GND (broche 6)**.</span><span class="sxs-lookup"><span data-stu-id="13a6b-170">Connect the shorter leg of the LED to **GPIO GND (Pin 6)**.</span></span>
2. <span data-ttu-id="13a6b-171">Connectez la broche la plus longue de la LED à une broche de la résistance.</span><span class="sxs-lookup"><span data-stu-id="13a6b-171">Connect the longer leg of the LED to one leg of the resistor.</span></span>
3. <span data-ttu-id="13a6b-172">Connectez l’autre broche de la résistance à **GPIO 4 (broche 7)**.</span><span class="sxs-lookup"><span data-stu-id="13a6b-172">Connect the other leg of the resistor to **GPIO 4 (Pin 7)**.</span></span>

<span data-ttu-id="13a6b-173">Notez que la polarité de la LED est importante.</span><span class="sxs-lookup"><span data-stu-id="13a6b-173">Note that the LED polarity is important.</span></span> <span data-ttu-id="13a6b-174">Ce paramètre de polarité est communément appelé Faible actif.</span><span class="sxs-lookup"><span data-stu-id="13a6b-174">This polarity setting is commonly known as Active Low.</span></span>

![Brochage](media/iot-hub-raspberry-pi-lessons/lesson1/pinout_breadboard.png)

<span data-ttu-id="13a6b-176">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="13a6b-176">Congratulations!</span></span> <span data-ttu-id="13a6b-177">Vous avez réussi à configurer Pi.</span><span class="sxs-lookup"><span data-stu-id="13a6b-177">You've successfully configured Pi.</span></span>

## <a name="summary"></a><span data-ttu-id="13a6b-178">Résumé</span><span class="sxs-lookup"><span data-stu-id="13a6b-178">Summary</span></span>
<span data-ttu-id="13a6b-179">Dans cet article, vous avez appris à configurer Pi en installant Raspbian, en connectant Pi à un réseau et en connectant une LED à Pi.</span><span class="sxs-lookup"><span data-stu-id="13a6b-179">In this article, you’ve learned how to configure Pi by installing Raspbian, connecting Pi to a network, and connecting an LED to Pi.</span></span> <span data-ttu-id="13a6b-180">Notez que la LED n’est pas encore allumée.</span><span class="sxs-lookup"><span data-stu-id="13a6b-180">Note that the LED doesn't yet light up.</span></span> <span data-ttu-id="13a6b-181">La tâche suivante consiste à installer les outils et le logiciel nécessaires en vue d’exécuter un exemple d’application sur Pi.</span><span class="sxs-lookup"><span data-stu-id="13a6b-181">The next task is to install the necessary tools and software in preparation for running a sample application on Pi.</span></span>

![Le matériel est prêt.](media/iot-hub-raspberry-pi-lessons/lesson1/hardware_ready.jpg)

## <a name="next-steps"></a><span data-ttu-id="13a6b-183">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="13a6b-183">Next steps</span></span>
[<span data-ttu-id="13a6b-184">Obtention des outils</span><span class="sxs-lookup"><span data-stu-id="13a6b-184">Get the tools</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-win32.md)

