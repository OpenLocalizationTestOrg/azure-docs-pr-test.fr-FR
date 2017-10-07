---
title: "Se connecter framboises Pi (nœud) tooAzure IoT - leçon 1 : configurer l’appareil | Documents Microsoft"
description: "Configurer framboises Pi 3 pour la première utilisation et installer hello Raspbian du système d’exploitation, un système d’exploitation libre qui est optimisé pour hello matériel de framboises Pi."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "raspbian de l’installation, téléchargement de raspbian, comment tooinstall raspbian, raspbian raspberry, le programme d’installation pi installation raspbian, raspberry pi installation du système d’exploitation, raspberry pi sd carte install, raspberry pi vous connecter, se connecter connectivité de pi pi, raspberry tooraspberry"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 43f7c2cf-f1a5-4dd5-93f0-7e546c6dc91e
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 504a4d2a3f29717f955530812442cce2a78a6448
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-your-device"></a><span data-ttu-id="8c2dc-104">Configurer votre appareil</span><span class="sxs-lookup"><span data-stu-id="8c2dc-104">Configure your device</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="8c2dc-105">Procédure à suivre</span><span class="sxs-lookup"><span data-stu-id="8c2dc-105">What you will do</span></span>
<span data-ttu-id="8c2dc-106">Configurer Pi pour la première utilisation et installer le système d’exploitation de Raspbian hello.</span><span class="sxs-lookup"><span data-stu-id="8c2dc-106">Configure Pi for first-time use and install hello Raspbian operating system.</span></span> <span data-ttu-id="8c2dc-107">Raspbian est un système d’exploitation libre qui est optimisé pour hello matériel de framboises Pi.</span><span class="sxs-lookup"><span data-stu-id="8c2dc-107">Raspbian is a free operating system that is optimized for hello Raspberry Pi hardware.</span></span> <span data-ttu-id="8c2dc-108">Si vous rencontrez des problèmes, vous pouvez rechercher des solutions sur hello [page Résolution des problèmes](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="8c2dc-108">If you have any problems, you can seek solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="8c2dc-109">Contenu</span><span class="sxs-lookup"><span data-stu-id="8c2dc-109">What you will learn</span></span>
<span data-ttu-id="8c2dc-110">Cet article portera sur les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="8c2dc-110">In this article, you will learn:</span></span>

* <span data-ttu-id="8c2dc-111">Comment tooinstall Raspbian sur Pi.</span><span class="sxs-lookup"><span data-stu-id="8c2dc-111">How tooinstall Raspbian on Pi.</span></span>
* <span data-ttu-id="8c2dc-112">Comment toopower des Pi à l’aide d’un câble USB.</span><span class="sxs-lookup"><span data-stu-id="8c2dc-112">How toopower up Pi by using a USB cable.</span></span>
* <span data-ttu-id="8c2dc-113">Comment tooconnect Pi toohello réseau à l’aide d’un réseau sans fil ou un câble Ethernet.</span><span class="sxs-lookup"><span data-stu-id="8c2dc-113">How tooconnect Pi toohello network by using an Ethernet cable or wireless network.</span></span>
* <span data-ttu-id="8c2dc-114">Comment tooadd un toohello LED breadboard et connectez-la tooPi.</span><span class="sxs-lookup"><span data-stu-id="8c2dc-114">How tooadd an LED toohello breadboard and connect it tooPi.</span></span>

## <a name="what-you-will-need"></a><span data-ttu-id="8c2dc-115">Éléments requis</span><span class="sxs-lookup"><span data-stu-id="8c2dc-115">What you will need</span></span>
<span data-ttu-id="8c2dc-116">toocomplete cette opération, vous devez hello pièces suivantes à partir de votre framboises Pi 3 Starter Kit :</span><span class="sxs-lookup"><span data-stu-id="8c2dc-116">toocomplete this operation, you need hello following parts from your Raspberry Pi 3 Starter Kit:</span></span>

* <span data-ttu-id="8c2dc-117">Hello framboises Pi 3 tableau</span><span class="sxs-lookup"><span data-stu-id="8c2dc-117">hello Raspberry Pi 3 board</span></span>
* <span data-ttu-id="8c2dc-118">carte microSD de 16 Go de Hello</span><span class="sxs-lookup"><span data-stu-id="8c2dc-118">hello 16-GB microSD card</span></span>
* <span data-ttu-id="8c2dc-119">Hello 5-volt 2-amp alimentation avec un câble USB micro de hello 6-pied</span><span class="sxs-lookup"><span data-stu-id="8c2dc-119">hello 5-volt 2-amp power supply with hello 6-foot micro USB cable</span></span>
* <span data-ttu-id="8c2dc-120">breadboard de Hello</span><span class="sxs-lookup"><span data-stu-id="8c2dc-120">hello breadboard</span></span>
* <span data-ttu-id="8c2dc-121">Câbles de connexion</span><span class="sxs-lookup"><span data-stu-id="8c2dc-121">Connector wires</span></span>
* <span data-ttu-id="8c2dc-122">Résistance de 560 Ohm</span><span class="sxs-lookup"><span data-stu-id="8c2dc-122">A 560-ohm resistor</span></span>
* <span data-ttu-id="8c2dc-123">LED de 10 mm diffuse</span><span class="sxs-lookup"><span data-stu-id="8c2dc-123">A diffused 10-mm LED</span></span>
* <span data-ttu-id="8c2dc-124">Hello câble Ethernet</span><span class="sxs-lookup"><span data-stu-id="8c2dc-124">hello Ethernet cable</span></span>

![Éléments de votre Starter Kit](media/iot-hub-raspberry-pi-lessons/lesson1/starter_kit.jpg)

<span data-ttu-id="8c2dc-126">Vous aurez également besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="8c2dc-126">You also need:</span></span>

* <span data-ttu-id="8c2dc-127">Une connexion câblée ou sans fil pour tooconnect Pi à.</span><span class="sxs-lookup"><span data-stu-id="8c2dc-127">A wired or wireless connection for Pi tooconnect to.</span></span>
* <span data-ttu-id="8c2dc-128">Un USB-SD adaptateur ou miniSD carte tooburn hello image système d’exploitation sur une carte microSD de hello.</span><span class="sxs-lookup"><span data-stu-id="8c2dc-128">A USB-SD adapter or miniSD card tooburn hello operating system image onto hello microSD card.</span></span>
* <span data-ttu-id="8c2dc-129">Un ordinateur exécutant Windows, Mac ou Linux.</span><span class="sxs-lookup"><span data-stu-id="8c2dc-129">A computer running Windows, Mac, or Linux.</span></span> <span data-ttu-id="8c2dc-130">l’ordinateur Hello est utilisé tooinstall Raspbian sur une carte microSD de hello.</span><span class="sxs-lookup"><span data-stu-id="8c2dc-130">hello computer is used tooinstall Raspbian on hello microSD card.</span></span>
* <span data-ttu-id="8c2dc-131">Un toodownload de connexion Internet hello outils nécessaires et logiciels.</span><span class="sxs-lookup"><span data-stu-id="8c2dc-131">An Internet connection toodownload hello necessary tools and software.</span></span>

## <a name="install-raspbian-on-hello-microsd-card"></a><span data-ttu-id="8c2dc-132">Installer Raspbian sur une carte microSD de hello</span><span class="sxs-lookup"><span data-stu-id="8c2dc-132">Install Raspbian on hello microSD card</span></span>
<span data-ttu-id="8c2dc-133">Préparer la carte microSD de hello pour l’installation de l’image de Raspbian hello.</span><span class="sxs-lookup"><span data-stu-id="8c2dc-133">Prepare hello microSD card for installation of hello Raspbian image.</span></span>

1. <span data-ttu-id="8c2dc-134">Téléchargez Raspbian.</span><span class="sxs-lookup"><span data-stu-id="8c2dc-134">Download Raspbian.</span></span>
   1. <span data-ttu-id="8c2dc-135">[Télécharger](https://www.raspberrypi.org/downloads/raspbian/) fichier .zip hello Raspbian Jessie par Pixel.</span><span class="sxs-lookup"><span data-stu-id="8c2dc-135">[Download](https://www.raspberrypi.org/downloads/raspbian/) hello .zip file for Raspbian Jessie with Pixel.</span></span>
   2. <span data-ttu-id="8c2dc-136">Extraire le dossier de tooa hello Raspbian image sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="8c2dc-136">Extract hello Raspbian image tooa folder on your computer.</span></span>
2. <span data-ttu-id="8c2dc-137">Installez Raspbian toohello microSD carte.</span><span class="sxs-lookup"><span data-stu-id="8c2dc-137">Install Raspbian toohello microSD card.</span></span>
   1. <span data-ttu-id="8c2dc-138">[Télécharger](https://www.etcher.io) et installer l’utilitaire de graveur carte hello Etcher SD.</span><span class="sxs-lookup"><span data-stu-id="8c2dc-138">[Download](https://www.etcher.io) and install hello Etcher SD card burner utility.</span></span>
   2. <span data-ttu-id="8c2dc-139">Exécutez Etcher et sélectionnez l’image Raspbian hello que vous avez extrait à l’étape 1.</span><span class="sxs-lookup"><span data-stu-id="8c2dc-139">Run Etcher and select hello Raspbian image that you extracted in step 1.</span></span>
   3. <span data-ttu-id="8c2dc-140">Sélectionnez le lecteur de carte microSD hello.</span><span class="sxs-lookup"><span data-stu-id="8c2dc-140">Select hello microSD card drive.</span></span>
      <span data-ttu-id="8c2dc-141">Notez que Etcher peut avoir déjà sélectionné lecteur hello.</span><span class="sxs-lookup"><span data-stu-id="8c2dc-141">Note that Etcher may have already selected hello correct drive.</span></span>
   4. <span data-ttu-id="8c2dc-142">Cliquez sur **Flash** tooinstall Raspbian toohello microSD carte.</span><span class="sxs-lookup"><span data-stu-id="8c2dc-142">Click **Flash** tooinstall Raspbian toohello microSD card.</span></span>
   5. <span data-ttu-id="8c2dc-143">Retirez hello microSD votre ordinateur lorsque l’installation est terminée.</span><span class="sxs-lookup"><span data-stu-id="8c2dc-143">Remove hello microSD card from your computer when installation is complete.</span></span>
      <span data-ttu-id="8c2dc-144">Carte microSD de hello tooremove safe est directement car Etcher éjecte automatiquement ou démonte carte microSD de hello à l’achèvement.</span><span class="sxs-lookup"><span data-stu-id="8c2dc-144">It's safe tooremove hello microSD card directly because Etcher automatically ejects or unmounts hello microSD card upon completion.</span></span>
   6. <span data-ttu-id="8c2dc-145">Insérer carte microSD de hello Pi.</span><span class="sxs-lookup"><span data-stu-id="8c2dc-145">Insert hello microSD card into Pi.</span></span>

![Insérez la carte de hello SD](media/iot-hub-raspberry-pi-lessons/lesson1/insert_sdcard.jpg)

## <a name="turn-on-pi"></a><span data-ttu-id="8c2dc-147">Mise sous tension de Pi</span><span class="sxs-lookup"><span data-stu-id="8c2dc-147">Turn on Pi</span></span>
<span data-ttu-id="8c2dc-148">Pi sous tension à l’aide de câble USB micro de hello et alimentation hello.</span><span class="sxs-lookup"><span data-stu-id="8c2dc-148">Turn on Pi by using hello micro USB cable and hello power supply.</span></span>

![Mise sous tension](media/iot-hub-raspberry-pi-lessons/lesson1/micro_usb_power_on.jpg)

> [!NOTE]
> <span data-ttu-id="8c2dc-150">Il s’agit d’alimentation toouse important hello kit hello est au moins de toomake 2 a que votre framboises comporte suffisamment toowork power correctement.</span><span class="sxs-lookup"><span data-stu-id="8c2dc-150">It is important toouse hello power supply in hello kit that is at least 2A toomake sure that your Raspberry has enough power toowork correctly.</span></span>

## <a name="enable-ssh"></a><span data-ttu-id="8c2dc-151">Activation de SSH</span><span class="sxs-lookup"><span data-stu-id="8c2dc-151">Enable SSH</span></span>
<span data-ttu-id="8c2dc-152">À compter de la version de novembre 2016 de hello, Raspbian de serveur SSH de hello désactivé par défaut.</span><span class="sxs-lookup"><span data-stu-id="8c2dc-152">As of hello November 2016 release, Raspbian has hello SSH server disabled by default.</span></span> <span data-ttu-id="8c2dc-153">Vous devez tooenable il manuellement.</span><span class="sxs-lookup"><span data-stu-id="8c2dc-153">You need tooenable it manually.</span></span> <span data-ttu-id="8c2dc-154">Vous pouvez faire référence toohello [instructions officielles](https://www.raspberrypi.org/documentation/remote-access/ssh/) ou connecter un moniteur et accédez trop**Préférences -> Configuration de Pi framboises** tooenable SSH.</span><span class="sxs-lookup"><span data-stu-id="8c2dc-154">You can refer toohello [official instructions](https://www.raspberrypi.org/documentation/remote-access/ssh/) or connect a monitor and go too**Preferences -> Raspberry Pi Configuration** tooenable SSH.</span></span>

## <a name="connect-raspberry-pi-3-toohello-network"></a><span data-ttu-id="8c2dc-155">Connecter framboises Pi 3 toohello réseau</span><span class="sxs-lookup"><span data-stu-id="8c2dc-155">Connect Raspberry Pi 3 toohello network</span></span>
<span data-ttu-id="8c2dc-156">Vous pouvez vous connecter tooa Pi câblé réseau tooa réseau ou sans fil.</span><span class="sxs-lookup"><span data-stu-id="8c2dc-156">You can connect Pi tooa wired network or tooa wireless network.</span></span> <span data-ttu-id="8c2dc-157">Assurez-vous que Pi est connecté toohello même réseau que votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="8c2dc-157">Make sure that Pi is connected toohello same network as your computer.</span></span> <span data-ttu-id="8c2dc-158">Par exemple, vous pouvez vous connecter toohello Pi à que même commutateur que votre ordinateur est connecté.</span><span class="sxs-lookup"><span data-stu-id="8c2dc-158">For example, you can connect Pi toohello same switch that your computer is connected to.</span></span>

### <a name="connect-tooa-wired-network"></a><span data-ttu-id="8c2dc-159">Se connecter tooa de réseau câblé</span><span class="sxs-lookup"><span data-stu-id="8c2dc-159">Connect tooa wired network</span></span>
<span data-ttu-id="8c2dc-160">Utilisez tooconnect de câble Ethernet hello tooyour Pi réseau câblé.</span><span class="sxs-lookup"><span data-stu-id="8c2dc-160">Use hello Ethernet cable tooconnect Pi tooyour wired network.</span></span> <span data-ttu-id="8c2dc-161">Hello deux voyants Pi sous tension si hello connexion est établie.</span><span class="sxs-lookup"><span data-stu-id="8c2dc-161">hello two LEDs on Pi turn on if hello connection is established.</span></span>

![Connexion à l’aide d’un câble Ethernet](media/iot-hub-raspberry-pi-lessons/lesson1/connect_ethernet.jpg)

### <a name="connect-tooa-wireless-network"></a><span data-ttu-id="8c2dc-163">Connexion réseau sans fil de tooa</span><span class="sxs-lookup"><span data-stu-id="8c2dc-163">Connect tooa wireless network</span></span>
<span data-ttu-id="8c2dc-164">Suivez hello [instructions](https://www.raspberrypi.org/learning/software-guide/wifi/) à partir du réseau sans fil tooyour du Pi tooconnect hello framboises Pi Foundation.</span><span class="sxs-lookup"><span data-stu-id="8c2dc-164">Follow hello [instructions](https://www.raspberrypi.org/learning/software-guide/wifi/) from hello Raspberry Pi Foundation tooconnect Pi tooyour wireless network.</span></span> <span data-ttu-id="8c2dc-165">Les instructions suivantes requièrent que vous toofirst connecter un moniteur et un tooPi de clavier.</span><span class="sxs-lookup"><span data-stu-id="8c2dc-165">These instructions require you toofirst connect a monitor and a keyboard tooPi.</span></span>

## <a name="connect-hello-led-toopi"></a><span data-ttu-id="8c2dc-166">Se connecter hello DEL tooPi</span><span class="sxs-lookup"><span data-stu-id="8c2dc-166">Connect hello LED tooPi</span></span>
<span data-ttu-id="8c2dc-167">toocomplete de cette tâche, utilisez hello [breadboard](https://learn.sparkfun.com/tutorials/how-to-use-a-breadboard), hello fils de connecteur, hello DEL et hello résistance.</span><span class="sxs-lookup"><span data-stu-id="8c2dc-167">toocomplete this task, use hello [breadboard](https://learn.sparkfun.com/tutorials/how-to-use-a-breadboard), hello connector wires, hello LED, and hello resistor.</span></span> <span data-ttu-id="8c2dc-168">Connectez-les toohello [à usage général d’entrée/sortie](https://www.raspberrypi.org/documentation/usage/gpio/) ports (GPIO) de Pi.</span><span class="sxs-lookup"><span data-stu-id="8c2dc-168">Connect them toohello [general-purpose input/output](https://www.raspberrypi.org/documentation/usage/gpio/) (GPIO) ports of Pi.</span></span>

![Platine d’expérimentation, LED et résistance](media/iot-hub-raspberry-pi-lessons/lesson1/breadboard_led_resistor.jpg)

1. <span data-ttu-id="8c2dc-170">Vous connecter trop de tronçon de hello plus courte de hello DEL**GPIO GND (code confidentiel 6)**.</span><span class="sxs-lookup"><span data-stu-id="8c2dc-170">Connect hello shorter leg of hello LED too**GPIO GND (Pin 6)**.</span></span>
2. <span data-ttu-id="8c2dc-171">Se connecter tronçon de plus de temps hello Hello tronçon de tooone LED de résistance de hello.</span><span class="sxs-lookup"><span data-stu-id="8c2dc-171">Connect hello longer leg of hello LED tooone leg of hello resistor.</span></span>
3. <span data-ttu-id="8c2dc-172">Se connecter hello autres tronçon de résistance de hello trop**GPIO 4 (code confidentiel 7)**.</span><span class="sxs-lookup"><span data-stu-id="8c2dc-172">Connect hello other leg of hello resistor too**GPIO 4 (Pin 7)**.</span></span>

<span data-ttu-id="8c2dc-173">Notez que la polarité hello DEL est importante.</span><span class="sxs-lookup"><span data-stu-id="8c2dc-173">Note that hello LED polarity is important.</span></span> <span data-ttu-id="8c2dc-174">Ce paramètre de polarité est communément appelé Faible actif.</span><span class="sxs-lookup"><span data-stu-id="8c2dc-174">This polarity setting is commonly known as Active Low.</span></span>

![Brochage](media/iot-hub-raspberry-pi-lessons/lesson1/pinout_breadboard.png)

<span data-ttu-id="8c2dc-176">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="8c2dc-176">Congratulations!</span></span> <span data-ttu-id="8c2dc-177">Vous avez réussi à configurer Pi.</span><span class="sxs-lookup"><span data-stu-id="8c2dc-177">You've successfully configured Pi.</span></span>

## <a name="summary"></a><span data-ttu-id="8c2dc-178">Résumé</span><span class="sxs-lookup"><span data-stu-id="8c2dc-178">Summary</span></span>
<span data-ttu-id="8c2dc-179">Dans cet article, vous avez appris comment tooconfigure Pi en installant Raspbian, connexion au réseau tooa Pi et de la connexion à un tooPi LED.</span><span class="sxs-lookup"><span data-stu-id="8c2dc-179">In this article, you’ve learned how tooconfigure Pi by installing Raspbian, connecting Pi tooa network, and connecting an LED tooPi.</span></span> <span data-ttu-id="8c2dc-180">Notez que hello que voyant ne s’allume encore.</span><span class="sxs-lookup"><span data-stu-id="8c2dc-180">Note that hello LED doesn't yet light up.</span></span> <span data-ttu-id="8c2dc-181">la tâche suivante Hello est tooinstall hello outils et nécessaires logiciel en vue d’un exemple d’application en cours d’exécution sur Pi.</span><span class="sxs-lookup"><span data-stu-id="8c2dc-181">hello next task is tooinstall hello necessary tools and software in preparation for running a sample application on Pi.</span></span>

![Le matériel est prêt.](media/iot-hub-raspberry-pi-lessons/lesson1/hardware_ready.jpg)

## <a name="next-steps"></a><span data-ttu-id="8c2dc-183">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8c2dc-183">Next steps</span></span>
[<span data-ttu-id="8c2dc-184">Obtenir les outils de hello</span><span class="sxs-lookup"><span data-stu-id="8c2dc-184">Get hello tools</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-win32.md)

