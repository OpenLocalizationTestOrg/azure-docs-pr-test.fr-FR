---
title: "Appareil simulé et passerelle Azure IoT - Leçon 1 : Configurer NUC | Microsoft Docs"
description: Configurer Intel NUC toowork comme passerelle entre un capteur et les informations de capteur toocollect Azure IoT Hub IoT et envoyez-le tooIoT Hub.
services: iot-hub
documentationcenter: 
author: shizn
manager: yjianfeng
tags: 
keywords: passerelle iot, intel nuc, ordinateur nuc, DE3815TYKE
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: f41d6b2e-9b00-40df-90eb-17d824bea883
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: c2146c7cd8ca54adbd0af279364ec8484be1b45b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-intel-nuc-as-an-iot-gateway"></a><span data-ttu-id="60cc4-104">Configurer l’Intel NUC comme passerelle IoT</span><span class="sxs-lookup"><span data-stu-id="60cc4-104">Set up Intel NUC as an IoT gateway</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="60cc4-105">Procédure à suivre</span><span class="sxs-lookup"><span data-stu-id="60cc4-105">What you will do</span></span>

- <span data-ttu-id="60cc4-106">Configurez l’Intel NUC comme passerelle IoT.</span><span class="sxs-lookup"><span data-stu-id="60cc4-106">Set up Intel NUC as an IoT gateway.</span></span>
- <span data-ttu-id="60cc4-107">Installez le package de Azure IoT Edge de hello sur NUC d’Intel.</span><span class="sxs-lookup"><span data-stu-id="60cc4-107">Install hello Azure IoT Edge package on Intel NUC.</span></span>
- <span data-ttu-id="60cc4-108">Exécuter un exemple d’application « Bonjour_monde » sur la fonctionnalité de passerelle Intel NUC tooverify hello.</span><span class="sxs-lookup"><span data-stu-id="60cc4-108">Run a "hello_world" sample application on Intel NUC tooverify hello gateway functionality.</span></span>
<span data-ttu-id="60cc4-109">Si vous rencontrez des problèmes, recherchez des solutions sur hello [page Résolution des problèmes](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="60cc4-109">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="60cc4-110">Contenu</span><span class="sxs-lookup"><span data-stu-id="60cc4-110">What you will learn</span></span>

<span data-ttu-id="60cc4-111">Dans cette leçon, vous allez apprendre :</span><span class="sxs-lookup"><span data-stu-id="60cc4-111">In this lesson, you will learn:</span></span>

- <span data-ttu-id="60cc4-112">Comment tooconnect Intel NUC avec les périphériques.</span><span class="sxs-lookup"><span data-stu-id="60cc4-112">How tooconnect Intel NUC with peripherals.</span></span>
- <span data-ttu-id="60cc4-113">Comment tooinstall et mise à jour des packages hello requis sur l’utilisation de Intel NUC hello actives Gestionnaire de Package.</span><span class="sxs-lookup"><span data-stu-id="60cc4-113">How tooinstall and update hello required packages on Intel NUC using hello Smart Package Manager.</span></span>
- <span data-ttu-id="60cc4-114">Comment toorun hello » Bonjour_monde » exemple de fonctionnalité de passerelle d’application tooverify hello.</span><span class="sxs-lookup"><span data-stu-id="60cc4-114">How toorun hello "hello_world" sample application tooverify hello gateway functionality.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="60cc4-115">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="60cc4-115">What you need</span></span>

- <span data-ttu-id="60cc4-116">Un Intel NUC Kit DE3815TYKE avec hello Intel IoT passerelle logiciel Suite (district de vent Linux * 7.0.0.13) préinstallé.</span><span class="sxs-lookup"><span data-stu-id="60cc4-116">An Intel NUC Kit DE3815TYKE with hello Intel IoT Gateway Software Suite (Wind River Linux *7.0.0.13) preinstalled.</span></span>
- <span data-ttu-id="60cc4-117">Un câble Ethernet.</span><span class="sxs-lookup"><span data-stu-id="60cc4-117">An Ethernet cable.</span></span>
- <span data-ttu-id="60cc4-118">Un clavier.</span><span class="sxs-lookup"><span data-stu-id="60cc4-118">A keyboard.</span></span>
- <span data-ttu-id="60cc4-119">Un câble VGA ou HDMI.</span><span class="sxs-lookup"><span data-stu-id="60cc4-119">An HDMI or VGA cable.</span></span>
- <span data-ttu-id="60cc4-120">Un écran équipé d’un port VGA ou HDMI.</span><span class="sxs-lookup"><span data-stu-id="60cc4-120">A monitor with an HDMI or VGA port.</span></span>

![Un kit de passerelle](media/iot-hub-gateway-kit-lessons/lesson1/kit_without_sensortag.png)

## <a name="connect-intel-nuc-with-hello-peripherals"></a><span data-ttu-id="60cc4-122">Se connecter Intel NUC avec les périphériques de hello</span><span class="sxs-lookup"><span data-stu-id="60cc4-122">Connect Intel NUC with hello peripherals</span></span>

<span data-ttu-id="60cc4-123">image Hello ci-dessous est un exemple de NUC Intel qui est connecté avec des périphériques différents :</span><span class="sxs-lookup"><span data-stu-id="60cc4-123">hello image below is an example of Intel NUC that is connected with various peripherals:</span></span>

1. <span data-ttu-id="60cc4-124">Tooa connecté clavier.</span><span class="sxs-lookup"><span data-stu-id="60cc4-124">Connected tooa keyboard.</span></span>
2. <span data-ttu-id="60cc4-125">Connecté analyse toohello par un câble VGA ou un câble HDMI.</span><span class="sxs-lookup"><span data-stu-id="60cc4-125">Connected toohello monitor by a VGA cable or HDMI cable.</span></span>
3. <span data-ttu-id="60cc4-126">Tooa connecté réseau câblé via un câble Ethernet.</span><span class="sxs-lookup"><span data-stu-id="60cc4-126">Connected tooa wired network by an Ethernet cable.</span></span>
4. <span data-ttu-id="60cc4-127">Alimentation toohello connecté avec un câble d’alimentation.</span><span class="sxs-lookup"><span data-stu-id="60cc4-127">Connected toohello power supply with a power cable.</span></span>

![Intel NUC connecté tooperipherals](media/iot-hub-gateway-kit-lessons/lesson1/nuc.png)

## <a name="connect-toohello-intel-nuc-system-from-host-computer-via-secure-shell-ssh"></a><span data-ttu-id="60cc4-129">Connecter le système d’Intel NUC toohello à partir de l’ordinateur hôte via Secure Shell (SSH)</span><span class="sxs-lookup"><span data-stu-id="60cc4-129">Connect toohello Intel NUC system from host computer via Secure Shell (SSH)</span></span>

<span data-ttu-id="60cc4-130">Ici, vous devez clavier et écran tooget hello adresse IP de votre périphérique NUC.</span><span class="sxs-lookup"><span data-stu-id="60cc4-130">Here you need keyboard and monitor tooget hello IP address of your NUC device.</span></span> <span data-ttu-id="60cc4-131">Si vous connaissez déjà hello IP adresse, vous pouvez ignorer toostep 3 de cette section.</span><span class="sxs-lookup"><span data-stu-id="60cc4-131">If you already know hello IP address, you can skip toostep 3 in this section.</span></span>

1. <span data-ttu-id="60cc4-132">Intel NUC sous tension en appuyant sur le bouton d’alimentation hello et de journal dans le système de hello.</span><span class="sxs-lookup"><span data-stu-id="60cc4-132">Turn on Intel NUC by pressing hello Power button and log in hello system.</span></span>

   <span data-ttu-id="60cc4-133">nom d’utilisateur par défaut Hello et un mot de passe sont tous deux `root`.</span><span class="sxs-lookup"><span data-stu-id="60cc4-133">hello default user name and password are both `root`.</span></span>

2. <span data-ttu-id="60cc4-134">Obtenir l’adresse IP hello NUC en exécutant hello `ifconfig` commande.</span><span class="sxs-lookup"><span data-stu-id="60cc4-134">Get hello IP address of NUC by running hello `ifconfig` command.</span></span> <span data-ttu-id="60cc4-135">Cette étape est effectuée sur l’appareil NUC hello.</span><span class="sxs-lookup"><span data-stu-id="60cc4-135">This step is done on hello NUC device.</span></span>

   <span data-ttu-id="60cc4-136">Voici un exemple de sortie de la commande hello.</span><span class="sxs-lookup"><span data-stu-id="60cc4-136">Here is an example of hello command output.</span></span>

   ![sortie ifconfig indiquant l’IP NUC](media/iot-hub-gateway-kit-lessons/lesson1/ifconfig.png)

   <span data-ttu-id="60cc4-138">Dans cet exemple, hello valeur suit `inet addr:` est l’adresse IP hello dont vous avez besoin lorsque vous planifiez tooconnect à distance à partir d’un tooIntel d’ordinateur hôte NUC.</span><span class="sxs-lookup"><span data-stu-id="60cc4-138">In this example, hello value that follows `inet addr:` is hello IP address that you need when you plan tooconnect remotely from a host computer tooIntel NUC.</span></span>

3. <span data-ttu-id="60cc4-139">Utilisez une des hello suivant clients SSH à partir de votre ordinateur hôte ordinateur tooconnect tooIntel NUC.</span><span class="sxs-lookup"><span data-stu-id="60cc4-139">Use one of hello following SSH clients from your host machine tooconnect tooIntel NUC.</span></span>

   - <span data-ttu-id="60cc4-140">[PuTTY](http://www.putty.org/) pour Windows.</span><span class="sxs-lookup"><span data-stu-id="60cc4-140">[PuTTY](http://www.putty.org/) for Windows.</span></span>
   - <span data-ttu-id="60cc4-141">Hello dans build client SSH sur Ubuntu ou macOS.</span><span class="sxs-lookup"><span data-stu-id="60cc4-141">hello build-in SSH client on Ubuntu or macOS.</span></span>

   <span data-ttu-id="60cc4-142">Il est plus efficace et plus productif toooperate sur Intel NUC à partir d’un ordinateur hôte.</span><span class="sxs-lookup"><span data-stu-id="60cc4-142">It is more efficient and productive toooperate on Intel NUC from a host computer.</span></span> <span data-ttu-id="60cc4-143">Vous avez besoin d’adresse IP de hello hello, nom d’utilisateur et mot de passe tooconnect hello NUC via un client SSH.</span><span class="sxs-lookup"><span data-stu-id="60cc4-143">You need hello hello IP address, user name and password tooconnect hello NUC via SSH client.</span></span> <span data-ttu-id="60cc4-144">Voici le client SSH de hello exemple utilisation sur macOS.</span><span class="sxs-lookup"><span data-stu-id="60cc4-144">Here is hello example use SSH client on macOS.</span></span>
   <span data-ttu-id="60cc4-145">![Client SSH exécuté sur macOS](media/iot-hub-gateway-kit-lessons/lesson1/ssh.png)</span><span class="sxs-lookup"><span data-stu-id="60cc4-145">![SSH client running on macOS](media/iot-hub-gateway-kit-lessons/lesson1/ssh.png)</span></span>

## <a name="install-hello-azure-iot-edge-package"></a><span data-ttu-id="60cc4-146">Installer le package de Azure IoT bord hello</span><span class="sxs-lookup"><span data-stu-id="60cc4-146">Install hello Azure IoT Edge package</span></span>

<span data-ttu-id="60cc4-147">Bonjour Azure IoT bord contient hello des binaires précompilés Hello SDK et ses dépendances.</span><span class="sxs-lookup"><span data-stu-id="60cc4-147">hello Azure IoT Edge package contains hello pre-compiled binaries of hello SDK and its dependencies.</span></span> <span data-ttu-id="60cc4-148">Ces fichiers binaires sont Azure IoT Edge, hello Azure IoT SDK et les outils correspondants hello.</span><span class="sxs-lookup"><span data-stu-id="60cc4-148">These binaries are Azure IoT Edge, hello Azure IoT SDK and hello corresponding tools.</span></span> <span data-ttu-id="60cc4-149">Hello contient également un exemple d’application « Bonjour_monde » qui est une fonctionnalité de passerelle hello toovalidate utilisé.</span><span class="sxs-lookup"><span data-stu-id="60cc4-149">hello package also contains a "hello_world" sample application that is used toovalidate hello gateway functionality.</span></span> <span data-ttu-id="60cc4-150">IoT bord fait partie de noyaux de hello de passerelle de hello.</span><span class="sxs-lookup"><span data-stu-id="60cc4-150">IoT Edge is hello core part of hello gateway.</span></span> <span data-ttu-id="60cc4-151">tooinstall hello du package, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="60cc4-151">tooinstall hello package, follow these steps:</span></span>

1. <span data-ttu-id="60cc4-152">Ajoutez référentiel de cloud IoT hello en exécutant hello suivant les commandes dans une fenêtre de terminal :</span><span class="sxs-lookup"><span data-stu-id="60cc4-152">Add hello IoT cloud repository by running hello following commands in a terminal window:</span></span>

   ```bash
   rpm --import http://iotdk.intel.com/misc/iot_pub.key
   smart channel --add IoT_Cloud type=rpm-md name="IoT_Cloud" baseurl=http://iotdk.intel.com/repos/iot-cloud/wrlinux7/rcpl13/ -y
   ```

   <span data-ttu-id="60cc4-153">Hello `rpm` commande importations hello clé du TPM.</span><span class="sxs-lookup"><span data-stu-id="60cc4-153">hello `rpm` command imports hello rpm key.</span></span> <span data-ttu-id="60cc4-154">Hello `smart channel` commande ajoute tr/min hello toohello actives Gestionnaire de Package de canal.</span><span class="sxs-lookup"><span data-stu-id="60cc4-154">hello `smart channel` command adds hello rpm channel toohello Smart Package Manager.</span></span> <span data-ttu-id="60cc4-155">Avant d’exécuter hello `smart update` commande, vous voyez une sortie similaire à ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="60cc4-155">Before you run hello `smart update` command, you see an output like below.</span></span>

   ![Sortie des commandes rpm et canal intelligent](media/iot-hub-gateway-kit-lessons/lesson1/rpm_smart_channel.png)

   ```bash
   smart update
   ```

2. <span data-ttu-id="60cc4-157">Installer hello en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="60cc4-157">Install hello package by running hello following command:</span></span>

   ```bash
   smart install packagegroup-cloud-azure -y
   ```

   <span data-ttu-id="60cc4-158">`packagegroup-cloud-azure`est le nom hello du package de hello.</span><span class="sxs-lookup"><span data-stu-id="60cc4-158">`packagegroup-cloud-azure` is hello name of hello package.</span></span> <span data-ttu-id="60cc4-159">Hello `smart install` commande est utilisée tooinstall hello du package.</span><span class="sxs-lookup"><span data-stu-id="60cc4-159">hello `smart install` command is used tooinstall hello package.</span></span>

   <span data-ttu-id="60cc4-160">Après installation du package hello, Intel NUC est toowork attendu en tant que passerelle.</span><span class="sxs-lookup"><span data-stu-id="60cc4-160">After hello package is installed, Intel NUC is expected toowork as a gateway.</span></span>

## <a name="run-hello-azure-iot-edge-helloworld-sample-application"></a><span data-ttu-id="60cc4-161">Exécuter hello Azure IoT bord « Bonjour_monde » exemple d’application</span><span class="sxs-lookup"><span data-stu-id="60cc4-161">Run hello Azure IoT Edge "hello_world" sample application</span></span>

<span data-ttu-id="60cc4-162">Accédez trop`azureiotgatewaysdk/samples` et exécuter l’exemple d’application hello exemple « Bonjour_monde ».</span><span class="sxs-lookup"><span data-stu-id="60cc4-162">Go too`azureiotgatewaysdk/samples` and run hello sample "hello_world" sample application.</span></span> <span data-ttu-id="60cc4-163">Cet exemple d’application crée une passerelle de hello `hello_world.json` de fichier et utilise les composants fondamentaux de hello de hello Azure IoT bord architecture toolog un fichier de tooa hello world message toutes les 5 secondes.</span><span class="sxs-lookup"><span data-stu-id="60cc4-163">This sample application creates a gateway from hello `hello_world.json` file and uses hello fundamental components of hello Azure IoT Edge architecture toolog a hello world message tooa file every 5 seconds.</span></span>

<span data-ttu-id="60cc4-164">Vous pouvez exécuter hello exemple « Bonjour_monde » exemple d’application en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="60cc4-164">You can run hello sample "hello_world" sample application by running hello following command:</span></span>

```bash
cd /usr/share/azureiotgatewaysdk/samples/hello_world/
./hello_world hello_world.json
```

<span data-ttu-id="60cc4-165">exemple d’application Hello génère suivant hello de sortie si la fonctionnalité de passerelle hello fonctionne correctement :</span><span class="sxs-lookup"><span data-stu-id="60cc4-165">hello sample application produces hello following output if hello gateway functionality is working correctly:</span></span>

![sortie d’application](media/iot-hub-gateway-kit-lessons/lesson1/hello_world.png)

<span data-ttu-id="60cc4-167">Si vous rencontrez des problèmes, recherchez des solutions sur hello [page Résolution des problèmes](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="60cc4-167">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="summary"></a><span data-ttu-id="60cc4-168">Résumé</span><span class="sxs-lookup"><span data-stu-id="60cc4-168">Summary</span></span>

<span data-ttu-id="60cc4-169">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="60cc4-169">Congratulations!</span></span> <span data-ttu-id="60cc4-170">Vous avez terminé la configuration d’Intel NUC comme passerelle.</span><span class="sxs-lookup"><span data-stu-id="60cc4-170">You've finished setting up Intel NUC as a gateway.</span></span> <span data-ttu-id="60cc4-171">Maintenant, vous êtes prêt toomove sur toohello prochaine leçon tooset votre ordinateur hôte, créez un Azure IoT hub et inscrire votre unité logique de Azure IoT hub.</span><span class="sxs-lookup"><span data-stu-id="60cc4-171">Now you're ready toomove on toohello next lesson tooset up your host computer, create an Azure IoT hub and register your Azure IoT hub logical device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="60cc4-172">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="60cc4-172">Next steps</span></span>
[<span data-ttu-id="60cc4-173">Préparer votre ordinateur hôte et Azure IoT Hub</span><span class="sxs-lookup"><span data-stu-id="60cc4-173">Get your host computer and Azure IoT hub ready</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)
