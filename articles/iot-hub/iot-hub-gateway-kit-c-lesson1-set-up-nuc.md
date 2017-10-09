---
title: "Appareil SensorTag et passerelle Azure Io - Leçon 1 : Configurer l’Intel NUC | Microsoft Docs"
description: Configurer Intel NUC toowork comme passerelle entre un capteur et les informations de capteur toocollect Azure IoT Hub IoT et envoyez-le tooIoT Hub.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: passerelle iot, intel nuc, ordinateur nuc, DE3815TYKE
ms.assetid: 917090d6-35c2-495b-a620-ca6f9c02b317
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 7c3ab3b014713c7facb86b8e8622d70e60a960e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-intel-nuc-as-an-iot-gateway"></a><span data-ttu-id="bd4e1-104">Configurer l’Intel NUC comme passerelle IoT</span><span class="sxs-lookup"><span data-stu-id="bd4e1-104">Set up Intel NUC as an IoT gateway</span></span>
[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

## <a name="what-you-will-do"></a><span data-ttu-id="bd4e1-105">Procédure à suivre</span><span class="sxs-lookup"><span data-stu-id="bd4e1-105">What you will do</span></span>

- <span data-ttu-id="bd4e1-106">Configurez l’Intel NUC comme passerelle IoT.</span><span class="sxs-lookup"><span data-stu-id="bd4e1-106">Set up Intel NUC as an IoT gateway.</span></span>
- <span data-ttu-id="bd4e1-107">Installez le package de Azure IoT Edge de hello sur hello NUC d’Intel.</span><span class="sxs-lookup"><span data-stu-id="bd4e1-107">Install hello Azure IoT Edge package on hello Intel NUC.</span></span>
- <span data-ttu-id="bd4e1-108">Exécuter un exemple d’application « Bonjour_monde » sur hello fonctionnalité de passerelle Intel NUC tooverify hello.</span><span class="sxs-lookup"><span data-stu-id="bd4e1-108">Run a "hello_world" sample application on hello Intel NUC tooverify hello gateway functionality.</span></span>

  > <span data-ttu-id="bd4e1-109">Si vous rencontrez des problèmes, recherchez des solutions sur hello [page Résolution des problèmes](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="bd4e1-109">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="bd4e1-110">Contenu</span><span class="sxs-lookup"><span data-stu-id="bd4e1-110">What you will learn</span></span>

<span data-ttu-id="bd4e1-111">Dans cette leçon, vous allez apprendre :</span><span class="sxs-lookup"><span data-stu-id="bd4e1-111">In this lesson, you will learn:</span></span>

- <span data-ttu-id="bd4e1-112">Comment tooconnect Intel NUC avec les périphériques.</span><span class="sxs-lookup"><span data-stu-id="bd4e1-112">How tooconnect Intel NUC with peripherals.</span></span>
- <span data-ttu-id="bd4e1-113">Comment tooinstall et mise à jour des packages hello requis sur l’utilisation de Intel NUC hello actives Gestionnaire de Package.</span><span class="sxs-lookup"><span data-stu-id="bd4e1-113">How tooinstall and update hello required packages on Intel NUC using hello Smart Package Manager.</span></span>
- <span data-ttu-id="bd4e1-114">Comment toorun hello » Bonjour_monde » exemple de fonctionnalité de passerelle d’application tooverify hello.</span><span class="sxs-lookup"><span data-stu-id="bd4e1-114">How toorun hello "hello_world" sample application tooverify hello gateway functionality.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="bd4e1-115">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="bd4e1-115">What you need</span></span>

- <span data-ttu-id="bd4e1-116">Un Intel NUC Kit DE3815TYKE avec hello Intel IoT passerelle logiciel Suite (district de vent Linux * 7.0.0.13) préinstallé.</span><span class="sxs-lookup"><span data-stu-id="bd4e1-116">An Intel NUC Kit DE3815TYKE with hello Intel IoT Gateway Software Suite (Wind River Linux *7.0.0.13) preinstalled.</span></span> <span data-ttu-id="bd4e1-117">[Cliquez ici toopurchase Grove IoT Commercial passerelle Kit](https://www.seeedstudio.com/Grove-IoT-Commercial-Gateway-Kit-p-2724.html).</span><span class="sxs-lookup"><span data-stu-id="bd4e1-117">[Click here toopurchase Grove IoT Commercial Gateway Kit](https://www.seeedstudio.com/Grove-IoT-Commercial-Gateway-Kit-p-2724.html).</span></span>
- <span data-ttu-id="bd4e1-118">Un câble Ethernet.</span><span class="sxs-lookup"><span data-stu-id="bd4e1-118">An Ethernet cable.</span></span>
- <span data-ttu-id="bd4e1-119">Un clavier.</span><span class="sxs-lookup"><span data-stu-id="bd4e1-119">A keyboard.</span></span>
- <span data-ttu-id="bd4e1-120">Un câble VGA ou HDMI.</span><span class="sxs-lookup"><span data-stu-id="bd4e1-120">An HDMI or VGA cable.</span></span>
- <span data-ttu-id="bd4e1-121">Un écran équipé d’un port VGA ou HDMI.</span><span class="sxs-lookup"><span data-stu-id="bd4e1-121">A monitor with an HDMI or VGA port.</span></span>
- <span data-ttu-id="bd4e1-122">Facultatif : [SensorTag Texas Instruments (CC2650STK)](http://www.ti.com/tool/cc2650stk)</span><span class="sxs-lookup"><span data-stu-id="bd4e1-122">Optional: [Texas Instruments Sensor Tag (CC2650STK)](http://www.ti.com/tool/cc2650stk)</span></span>

![Un kit de passerelle](media/iot-hub-gateway-kit-lessons/lesson1/kit.png)

## <a name="connect-intel-nuc-with-hello-peripherals"></a><span data-ttu-id="bd4e1-124">Se connecter Intel NUC avec les périphériques de hello</span><span class="sxs-lookup"><span data-stu-id="bd4e1-124">Connect Intel NUC with hello peripherals</span></span>

<span data-ttu-id="bd4e1-125">image Hello ci-dessous est un exemple de NUC Intel qui est connecté avec des périphériques différents :</span><span class="sxs-lookup"><span data-stu-id="bd4e1-125">hello image below is an example of Intel NUC that is connected with various peripherals:</span></span>

1. <span data-ttu-id="bd4e1-126">Tooa connecté clavier.</span><span class="sxs-lookup"><span data-stu-id="bd4e1-126">Connected tooa keyboard.</span></span>
2. <span data-ttu-id="bd4e1-127">Connecté tooa moniteur avec un câble VGA ou un câble HDMI.</span><span class="sxs-lookup"><span data-stu-id="bd4e1-127">Connected tooa monitor with a VGA cable or HDMI cable.</span></span>
3. <span data-ttu-id="bd4e1-128">Tooa connecté réseau via un câble Ethernet câblé.</span><span class="sxs-lookup"><span data-stu-id="bd4e1-128">Connected tooa wired network with an Ethernet cable.</span></span>
4. <span data-ttu-id="bd4e1-129">Alimentation tooa connecté avec un câble d’alimentation.</span><span class="sxs-lookup"><span data-stu-id="bd4e1-129">Connected tooa power supply with a power cable.</span></span>

![Intel NUC connecté tooperipherals](media/iot-hub-gateway-kit-lessons/lesson1/nuc.png)

## <a name="connect-toohello-intel-nuc-system-from-host-computer-via-secure-shell-ssh"></a><span data-ttu-id="bd4e1-131">Connecter le système d’Intel NUC toohello à partir de l’ordinateur hôte via Secure Shell (SSH)</span><span class="sxs-lookup"><span data-stu-id="bd4e1-131">Connect toohello Intel NUC system from host computer via Secure Shell (SSH)</span></span>

<span data-ttu-id="bd4e1-132">Vous devez un clavier et une adresse IP de moniteur tooget hello de votre appareil NUC d’Intel.</span><span class="sxs-lookup"><span data-stu-id="bd4e1-132">You will need a keyboard and a monitor tooget hello IP address of your Intel NUC device.</span></span> <span data-ttu-id="bd4e1-133">Si vous connaissez déjà hello IP adresse, vous pouvez ignorer le transfert toostep 3 de cette section.</span><span class="sxs-lookup"><span data-stu-id="bd4e1-133">If you already know hello IP address, you can skip ahead toostep 3 in this section.</span></span>

1. <span data-ttu-id="bd4e1-134">Activez hello Intel NUC en appuyant sur le bouton d’alimentation hello et puis connectez-vous.</span><span class="sxs-lookup"><span data-stu-id="bd4e1-134">Turn on hello Intel NUC by pressing hello power button and then log in.</span></span>

   <span data-ttu-id="bd4e1-135">nom d’utilisateur par défaut Hello et un mot de passe sont tous deux `root`.</span><span class="sxs-lookup"><span data-stu-id="bd4e1-135">hello default user name and password are both `root`.</span></span>

       > Hit hello enter key on your keyboard if you see either of hello following errors when you boot: 'A TPM error (7) occurred attempting tooread a pcr value.' or 'Timeout, No TPM chip found, activating TPM-bypass!'

2. <span data-ttu-id="bd4e1-136">Adresse IP hello hello Intel NUC d’obtenir en exécutant hello `ifconfig` commande sur l’appareil de Intel NUC hello.</span><span class="sxs-lookup"><span data-stu-id="bd4e1-136">Get hello IP address of hello Intel NUC by running hello `ifconfig` command on hello Intel NUC device.</span></span>

   <span data-ttu-id="bd4e1-137">Voici un exemple de sortie de la commande hello.</span><span class="sxs-lookup"><span data-stu-id="bd4e1-137">Here is an example of hello command output.</span></span>

   ![Sortie de la commande ifconfig indiquant l’adresse IP de l’Intel NUC](media/iot-hub-gateway-kit-lessons/lesson1/ifconfig.png)

   <span data-ttu-id="bd4e1-139">Dans cet exemple, hello valeur suit `inet addr:` est l’adresse IP hello dont vous avez besoin lorsque vous connecter toohello Intel NUC à partir d’un ordinateur hôte.</span><span class="sxs-lookup"><span data-stu-id="bd4e1-139">In this example, hello value that follows `inet addr:` is hello IP address that you need when connect toohello Intel NUC from a host computer.</span></span>

3. <span data-ttu-id="bd4e1-140">Utilisez une des hello suivant clients SSH à partir de votre ordinateur hôte ordinateur tooconnect tooIntel NUC.</span><span class="sxs-lookup"><span data-stu-id="bd4e1-140">Use one of hello following SSH clients from your host computer tooconnect tooIntel NUC.</span></span>

    - <span data-ttu-id="bd4e1-141">[PuTTY](http://www.putty.org/) pour Windows.</span><span class="sxs-lookup"><span data-stu-id="bd4e1-141">[PuTTY](http://www.putty.org/) for Windows.</span></span>
    - <span data-ttu-id="bd4e1-142">client Hello intégré SSH sur Ubuntu ou macOS.</span><span class="sxs-lookup"><span data-stu-id="bd4e1-142">hello built-in SSH client on Ubuntu or macOS.</span></span>

   <span data-ttu-id="bd4e1-143">Il est plus efficace et plus productif toooperate un NUC Intel à partir d’un ordinateur hôte.</span><span class="sxs-lookup"><span data-stu-id="bd4e1-143">It is more efficient and productive toooperate an Intel NUC from a host computer.</span></span> <span data-ttu-id="bd4e1-144">Vous aurez besoin hello adresse IP de NUC Intel tooit de tooconnect des nom et mot de passe utilisateur via un client SSH.</span><span class="sxs-lookup"><span data-stu-id="bd4e1-144">You'll need hello Intel NUC's IP address, user name and password tooconnect tooit via an SSH client.</span></span> <span data-ttu-id="bd4e1-145">Voici un exemple qui fait appel à un client SSH sur Mac OS.</span><span class="sxs-lookup"><span data-stu-id="bd4e1-145">Here is an example that uses an SSH client on macOS.</span></span>
   <span data-ttu-id="bd4e1-146">![Client SSH exécuté sur macOS](media/iot-hub-gateway-kit-lessons/lesson1/ssh.png)</span><span class="sxs-lookup"><span data-stu-id="bd4e1-146">![SSH client running on macOS](media/iot-hub-gateway-kit-lessons/lesson1/ssh.png)</span></span>

## <a name="install-hello-azure-iot-edge-package"></a><span data-ttu-id="bd4e1-147">Installer le package de Azure IoT bord hello</span><span class="sxs-lookup"><span data-stu-id="bd4e1-147">Install hello Azure IoT Edge package</span></span>

<span data-ttu-id="bd4e1-148">Azure IoT bord Hello contient hello des binaires précompilés de IoT Edge et ses dépendances.</span><span class="sxs-lookup"><span data-stu-id="bd4e1-148">hello Azure IoT Edge package contains hello pre-compiled binaries of IoT Edge and its dependencies.</span></span> <span data-ttu-id="bd4e1-149">Ces fichiers binaires sont Azure IoT Edge, hello Azure IoT SDK et les outils correspondants hello.</span><span class="sxs-lookup"><span data-stu-id="bd4e1-149">These binaries are Azure IoT Edge, hello Azure IoT SDK and hello corresponding tools.</span></span> <span data-ttu-id="bd4e1-150">Hello package contient également une « Bonjour_monde » exemple d’application est une fonctionnalité de passerelle hello toovalidate utilisé.</span><span class="sxs-lookup"><span data-stu-id="bd4e1-150">hello package also contains a "hello_world" sample application is used toovalidate hello gateway functionality.</span></span> <span data-ttu-id="bd4e1-151">IoT bord fait partie de noyaux de hello de passerelle de hello.</span><span class="sxs-lookup"><span data-stu-id="bd4e1-151">IoT Edge is hello core part of hello gateway.</span></span> 

<span data-ttu-id="bd4e1-152">Suivez ces packages de hello tooinstall étapes.</span><span class="sxs-lookup"><span data-stu-id="bd4e1-152">Follow these steps tooinstall hello package.</span></span>

1. <span data-ttu-id="bd4e1-153">Ajoutez hello référentiel de IoT Cloud en exécutant hello suivant les commandes dans une fenêtre de terminal :</span><span class="sxs-lookup"><span data-stu-id="bd4e1-153">Add hello IoT Cloud repository by running hello following commands in a terminal window:</span></span>

   ```bash
   rpm --import https://iotdk.intel.com/misc/iot_pub2.key
   smart channel --add IoT_Cloud type=rpm-md name="IoT_Cloud" baseurl=http://iotdk.intel.com/repos/iot-cloud/wrlinux7/rcpl13/ -y
   smart channel --add WR_Repo type=rpm-md baseurl=https://distro.windriver.com/release/idp-3-xt/public_feeds/WR-IDP-3-XT-Intel-Baytrail-public-repo/RCPL13/corei7_64/
   ```

   > <span data-ttu-id="bd4e1-154">Entrez 'y', lorsque vous invite too'Include ce canal ? »</span><span class="sxs-lookup"><span data-stu-id="bd4e1-154">Enter 'y', when it prompts you too'Include this channel?'</span></span>
   
   <span data-ttu-id="bd4e1-155">Si vous recevez un `import read failed(-1)` erreur, hello utilisation suivant le problème de hello tooresolve de commandes :</span><span class="sxs-lookup"><span data-stu-id="bd4e1-155">If you receive an `import read failed(-1)` error, use hello following commands tooresolve hello issue:</span></span>
   ```bash
   wget http://iotdk.intel.com/misc/iot_pub2.key 
   rpm --import iot_pub2.key  
   ```

   <span data-ttu-id="bd4e1-156">Hello `rpm` commande importations hello clé du TPM.</span><span class="sxs-lookup"><span data-stu-id="bd4e1-156">hello `rpm` command imports hello rpm key.</span></span> <span data-ttu-id="bd4e1-157">Hello `smart channel` commande ajoute tr/min hello toohello actives Gestionnaire de Package de canal.</span><span class="sxs-lookup"><span data-stu-id="bd4e1-157">hello `smart channel` command adds hello rpm channel toohello Smart Package Manager.</span></span> <span data-ttu-id="bd4e1-158">Avant d’exécuter hello `smart update` de commande, vous pouvez voir une sortie comme ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="bd4e1-158">Before you run hello `smart update` command, you will see an output like below.</span></span>

   ![Sortie des commandes rpm et canal intelligent](media/iot-hub-gateway-kit-lessons/lesson1/rpm_smart_channel.png)

2. <span data-ttu-id="bd4e1-160">Exécuter la commande de mise à jour actives hello :</span><span class="sxs-lookup"><span data-stu-id="bd4e1-160">Execute hello smart update command:</span></span>

   ```bash
   smart update
   ```

3. <span data-ttu-id="bd4e1-161">Installer le package de passerelle de Azure IoT de hello en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="bd4e1-161">Install hello Azure IoT Gateway package by running hello following command:</span></span>

   ```bash
   smart install packagegroup-cloud-azure -y
   ```

   <span data-ttu-id="bd4e1-162">`packagegroup-cloud-azure`est le nom hello du package de hello.</span><span class="sxs-lookup"><span data-stu-id="bd4e1-162">`packagegroup-cloud-azure` is hello name of hello package.</span></span> <span data-ttu-id="bd4e1-163">Hello `smart install` commande est utilisée tooinstall hello du package.</span><span class="sxs-lookup"><span data-stu-id="bd4e1-163">hello `smart install` command is used tooinstall hello package.</span></span>

    > <span data-ttu-id="bd4e1-164">Suivante d’exécution hello commande si vous voyez cette erreur : « clé publique non disponible »</span><span class="sxs-lookup"><span data-stu-id="bd4e1-164">Run hello following command if you see this error: 'public key not available'</span></span>

    ```bash
    smart config --set rpm-check-signatures=false
    smart install packagegroup-cloud-azure -y
    ```
    > <span data-ttu-id="bd4e1-165">Redémarrez hello Intel NUC si vous voyez cette erreur : « aucun package ne fournit util-linux-dev »</span><span class="sxs-lookup"><span data-stu-id="bd4e1-165">Reboot hello Intel NUC if you see this error: 'no package provides util-linux-dev'</span></span>

   <span data-ttu-id="bd4e1-166">Après installation du package hello, Intel NUC est toofunction prêt en tant que passerelle.</span><span class="sxs-lookup"><span data-stu-id="bd4e1-166">After hello package is installed, Intel NUC is ready toofunction as a gateway.</span></span>

## <a name="run-hello-azure-iot-edge-helloworld-sample-application"></a><span data-ttu-id="bd4e1-167">Exécuter hello Azure IoT bord « Bonjour_monde » exemple d’application</span><span class="sxs-lookup"><span data-stu-id="bd4e1-167">Run hello Azure IoT Edge "hello_world" sample application</span></span>

<span data-ttu-id="bd4e1-168">Hello suivant l’exemple d’application crée une passerelle d’un `hello_world.json` de fichier et utilise les composants fondamentaux de hello de Azure IoT bord architecture toolog un fichier de tooa message hello world (log.txt) toutes les 5 secondes.</span><span class="sxs-lookup"><span data-stu-id="bd4e1-168">hello following sample application creates a gateway from a `hello_world.json` file and uses hello fundamental components of Azure IoT Edge architecture toolog a hello world message tooa file (log.txt) every 5 seconds.</span></span>

<span data-ttu-id="bd4e1-169">Vous pouvez exécuter l’exemple hello Hello World en exécutant hello suivant les commandes :</span><span class="sxs-lookup"><span data-stu-id="bd4e1-169">You can run hello Hello World sample by executing hello following commands:</span></span>

```bash
cd /usr/share/azureiotgatewaysdk/samples/hello_world/
./hello_world hello_world.json
```

<span data-ttu-id="bd4e1-170">Permettent l’application hello Hello World s’exécuter pendant quelques minutes, puis appuyez sur toostop de clé entrée hello il.</span><span class="sxs-lookup"><span data-stu-id="bd4e1-170">Let hello Hello World application run for a few minutes and then hit hello Enter key toostop it.</span></span>
<span data-ttu-id="bd4e1-171">![Sortie de l’application](media/iot-hub-gateway-kit-lessons/lesson1/hello_world.png)</span><span class="sxs-lookup"><span data-stu-id="bd4e1-171">![application output](media/iot-hub-gateway-kit-lessons/lesson1/hello_world.png)</span></span>

> <span data-ttu-id="bd4e1-172">Vous pouvez ignorer les erreurs « invalid argument handle(NULL) » (Descripteur d’argument non valide (NULL)) qui s’affichent après que vous avez appuyé sur Entrée.</span><span class="sxs-lookup"><span data-stu-id="bd4e1-172">You can ignore any 'invalid argument handle(NULL)' errors that appear after you hit Enter.</span></span>

<span data-ttu-id="bd4e1-173">Vous pouvez vérifier cette passerelle hello a été effectuée correctement en ouvrant le fichier log.txt hello qui est désormais dans votre dossier Bonjour_monde ![log.txt vue d’annuaire](media/iot-hub-gateway-kit-lessons/lesson1/logtxtdir.png)</span><span class="sxs-lookup"><span data-stu-id="bd4e1-173">You can verify that hello gateway ran successfully by opening hello log.txt file that is now in your hello_world folder ![log.txt directory view](media/iot-hub-gateway-kit-lessons/lesson1/logtxtdir.png)</span></span>

<span data-ttu-id="bd4e1-174">Ouvrez log.txt à l’aide de hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="bd4e1-174">Open log.txt using hello following command:</span></span>

```bash
vim log.txt
```

<span data-ttu-id="bd4e1-175">Vous verrez ensuite contenu hello de log.txt, qui sera une sortie au format JSON de messages de journalisation hello qui ont été écrits de toutes les 5 secondes par le module de Hello World hello passerelle.</span><span class="sxs-lookup"><span data-stu-id="bd4e1-175">You will then see hello contents of log.txt, which will be a JSON formatted output of hello logging messages that were written every 5 seconds by hello gateway Hello World module.</span></span>
<span data-ttu-id="bd4e1-176">![Vue du répertoire de log.txt](media/iot-hub-gateway-kit-lessons/lesson1/logtxtview.png)</span><span class="sxs-lookup"><span data-stu-id="bd4e1-176">![log.txt directory view](media/iot-hub-gateway-kit-lessons/lesson1/logtxtview.png)</span></span>

<span data-ttu-id="bd4e1-177">Si vous rencontrez des problèmes, recherchez des solutions sur hello [page Résolution des problèmes](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="bd4e1-177">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="summary"></a><span data-ttu-id="bd4e1-178">Résumé</span><span class="sxs-lookup"><span data-stu-id="bd4e1-178">Summary</span></span>

<span data-ttu-id="bd4e1-179">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="bd4e1-179">Congratulations!</span></span> <span data-ttu-id="bd4e1-180">Vous avez terminé la configuration d’Intel NUC comme passerelle.</span><span class="sxs-lookup"><span data-stu-id="bd4e1-180">You've finished setting up Intel NUC as a gateway.</span></span> <span data-ttu-id="bd4e1-181">Maintenant, vous êtes prêt toomove sur toohello prochaine leçon tooset votre ordinateur hôte, créez un Azure IoT Hub et inscrire votre appareil logique Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="bd4e1-181">Now you're ready toomove on toohello next lesson tooset up your host computer, create an Azure IoT Hub and register your Azure IoT Hub logical device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bd4e1-182">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="bd4e1-182">Next steps</span></span>
[<span data-ttu-id="bd4e1-183">Utilisez un tooconnect de passerelle un tooAzure appareil IoT Hub IoT</span><span class="sxs-lookup"><span data-stu-id="bd4e1-183">Use an IoT gateway tooconnect a device tooAzure IoT Hub</span></span>](iot-hub-gateway-kit-c-iot-gateway-connect-device-to-cloud.md)

