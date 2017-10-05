---
title: "Appareil simulé et passerelle Azure IoT - Leçon 1 : Configurer NUC | Microsoft Docs"
description: "Configurez Intel NUC comme passerelle IoT entre un capteur et Azure IoT Hub, afin de collecter des informations de capteurs et de les envoyer à IoT Hub."
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
ms.openlocfilehash: b87974be9570f7d03fe84ae0a1d1fa7e346ff189
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="set-up-intel-nuc-as-an-iot-gateway"></a><span data-ttu-id="48f99-104">Configurer l’Intel NUC comme passerelle IoT</span><span class="sxs-lookup"><span data-stu-id="48f99-104">Set up Intel NUC as an IoT gateway</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="48f99-105">Procédure à suivre</span><span class="sxs-lookup"><span data-stu-id="48f99-105">What you will do</span></span>

- <span data-ttu-id="48f99-106">Configurez l’Intel NUC comme passerelle IoT.</span><span class="sxs-lookup"><span data-stu-id="48f99-106">Set up Intel NUC as an IoT gateway.</span></span>
- <span data-ttu-id="48f99-107">Installez le package Azure IoT Edge sur Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="48f99-107">Install the Azure IoT Edge package on Intel NUC.</span></span>
- <span data-ttu-id="48f99-108">Exécutez un exemple d’application « hello_world » sur Intel NUC pour vérifier le bon fonctionnement de la passerelle.</span><span class="sxs-lookup"><span data-stu-id="48f99-108">Run a "hello_world" sample application on Intel NUC to verify the gateway functionality.</span></span>
<span data-ttu-id="48f99-109">Si vous rencontrez des problèmes, recherchez des solutions dans la [page de résolution des problèmes](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="48f99-109">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="48f99-110">Contenu</span><span class="sxs-lookup"><span data-stu-id="48f99-110">What you will learn</span></span>

<span data-ttu-id="48f99-111">Dans cette leçon, vous allez apprendre :</span><span class="sxs-lookup"><span data-stu-id="48f99-111">In this lesson, you will learn:</span></span>

- <span data-ttu-id="48f99-112">la connexion d’Intel NUC à des périphériques ;</span><span class="sxs-lookup"><span data-stu-id="48f99-112">How to connect Intel NUC with peripherals.</span></span>
- <span data-ttu-id="48f99-113">l’installation et la mise à jour des packages nécessaires sur Intel NUC à l’aide du gestionnaire de package intelligent ;</span><span class="sxs-lookup"><span data-stu-id="48f99-113">How to install and update the required packages on Intel NUC using the Smart Package Manager.</span></span>
- <span data-ttu-id="48f99-114">l’exécution de l’exemple d’application « hello_world » pour vérifier le bon fonctionnement de la passerelle.</span><span class="sxs-lookup"><span data-stu-id="48f99-114">How to run the "hello_world" sample application to verify the gateway functionality.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="48f99-115">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="48f99-115">What you need</span></span>

- <span data-ttu-id="48f99-116">Un Kit Intel NUC DE3815TYKE avec la suite logicielle de passerelle Intel IoT (Wind River Linux *7.0.0.13) préinstallée.</span><span class="sxs-lookup"><span data-stu-id="48f99-116">An Intel NUC Kit DE3815TYKE with the Intel IoT Gateway Software Suite (Wind River Linux *7.0.0.13) preinstalled.</span></span>
- <span data-ttu-id="48f99-117">Un câble Ethernet.</span><span class="sxs-lookup"><span data-stu-id="48f99-117">An Ethernet cable.</span></span>
- <span data-ttu-id="48f99-118">Un clavier.</span><span class="sxs-lookup"><span data-stu-id="48f99-118">A keyboard.</span></span>
- <span data-ttu-id="48f99-119">Un câble VGA ou HDMI.</span><span class="sxs-lookup"><span data-stu-id="48f99-119">An HDMI or VGA cable.</span></span>
- <span data-ttu-id="48f99-120">Un écran équipé d’un port VGA ou HDMI.</span><span class="sxs-lookup"><span data-stu-id="48f99-120">A monitor with an HDMI or VGA port.</span></span>

![Un kit de passerelle](media/iot-hub-gateway-kit-lessons/lesson1/kit_without_sensortag.png)

## <a name="connect-intel-nuc-with-the-peripherals"></a><span data-ttu-id="48f99-122">Connexion d’Intel NUC aux périphériques</span><span class="sxs-lookup"><span data-stu-id="48f99-122">Connect Intel NUC with the peripherals</span></span>

<span data-ttu-id="48f99-123">L’image ci-dessous est un exemple d’Intel NUC connecté à plusieurs périphériques :</span><span class="sxs-lookup"><span data-stu-id="48f99-123">The image below is an example of Intel NUC that is connected with various peripherals:</span></span>

1. <span data-ttu-id="48f99-124">Connecté à un clavier.</span><span class="sxs-lookup"><span data-stu-id="48f99-124">Connected to a keyboard.</span></span>
2. <span data-ttu-id="48f99-125">Connecté à l’écran par le biais d’un câble VGA ou d’un câble HDMI.</span><span class="sxs-lookup"><span data-stu-id="48f99-125">Connected to the monitor by a VGA cable or HDMI cable.</span></span>
3. <span data-ttu-id="48f99-126">Connecté à un réseau filaire par le biais d’un câble Ethernet.</span><span class="sxs-lookup"><span data-stu-id="48f99-126">Connected to a wired network by an Ethernet cable.</span></span>
4. <span data-ttu-id="48f99-127">Connecté à l’alimentation par le biais d’un câble d’alimentation.</span><span class="sxs-lookup"><span data-stu-id="48f99-127">Connected to the power supply with a power cable.</span></span>

![Intel NUC connecté à des périphériques](media/iot-hub-gateway-kit-lessons/lesson1/nuc.png)

## <a name="connect-to-the-intel-nuc-system-from-host-computer-via-secure-shell-ssh"></a><span data-ttu-id="48f99-129">Connexion au système Intel NUC à partir de l’ordinateur hôte par le biais de Secure Shell (SSH)</span><span class="sxs-lookup"><span data-stu-id="48f99-129">Connect to the Intel NUC system from host computer via Secure Shell (SSH)</span></span>

<span data-ttu-id="48f99-130">Vous devez disposer d’un clavier et d’un écran pour obtenir l’adresse IP de votre appareil NUC.</span><span class="sxs-lookup"><span data-stu-id="48f99-130">Here you need keyboard and monitor to get the IP address of your NUC device.</span></span> <span data-ttu-id="48f99-131">Si vous connaissez déjà l’adresse IP, vous pouvez passer à l’étape 3 de cette section.</span><span class="sxs-lookup"><span data-stu-id="48f99-131">If you already know the IP address, you can skip to step 3 in this section.</span></span>

1. <span data-ttu-id="48f99-132">Activez Intel NUC en appuyant sur le bouton d’alimentation et connectez-vous au système.</span><span class="sxs-lookup"><span data-stu-id="48f99-132">Turn on Intel NUC by pressing the Power button and log in the system.</span></span>

   <span data-ttu-id="48f99-133">Le nom d’utilisateur et le mot de passe par défaut sont tous les deux `root`.</span><span class="sxs-lookup"><span data-stu-id="48f99-133">The default user name and password are both `root`.</span></span>

2. <span data-ttu-id="48f99-134">Obtenez l’adresse IP de NUC en exécutant la commande `ifconfig`.</span><span class="sxs-lookup"><span data-stu-id="48f99-134">Get the IP address of NUC by running the `ifconfig` command.</span></span> <span data-ttu-id="48f99-135">Cette étape s’effectue sur l’appareil NUC.</span><span class="sxs-lookup"><span data-stu-id="48f99-135">This step is done on the NUC device.</span></span>

   <span data-ttu-id="48f99-136">Voici un exemple de la sortie de cette commande.</span><span class="sxs-lookup"><span data-stu-id="48f99-136">Here is an example of the command output.</span></span>

   ![sortie ifconfig indiquant l’IP NUC](media/iot-hub-gateway-kit-lessons/lesson1/ifconfig.png)

   <span data-ttu-id="48f99-138">Dans cet exemple, la valeur qui suit `inet addr:` correspond à l’adresse IP dont vous avez besoin lorsque vous prévoyez de vous connecter à distance à partir d’un ordinateur hôte à Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="48f99-138">In this example, the value that follows `inet addr:` is the IP address that you need when you plan to connect remotely from a host computer to Intel NUC.</span></span>

3. <span data-ttu-id="48f99-139">Utilisez l’un des clients SSH suivants à partir de votre ordinateur hôte pour vous connecter à Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="48f99-139">Use one of the following SSH clients from your host machine to connect to Intel NUC.</span></span>

   - <span data-ttu-id="48f99-140">[PuTTY](http://www.putty.org/) pour Windows.</span><span class="sxs-lookup"><span data-stu-id="48f99-140">[PuTTY](http://www.putty.org/) for Windows.</span></span>
   - <span data-ttu-id="48f99-141">Le client SSH intégré sur Ubuntu ou macOS.</span><span class="sxs-lookup"><span data-stu-id="48f99-141">The build-in SSH client on Ubuntu or macOS.</span></span>

   <span data-ttu-id="48f99-142">Il est plus efficace et plus productif d’utiliser Intel NUC à partir d’un ordinateur hôte.</span><span class="sxs-lookup"><span data-stu-id="48f99-142">It is more efficient and productive to operate on Intel NUC from a host computer.</span></span> <span data-ttu-id="48f99-143">Vous avez besoin de l’adresse IP, du nom d’utilisateur et du mot de passe pour vous connecter à NUC par le biais d’un client SSH.</span><span class="sxs-lookup"><span data-stu-id="48f99-143">You need the the IP address, user name and password to connect the NUC via SSH client.</span></span> <span data-ttu-id="48f99-144">Voici un exemple d’utilisation d’un client SSH sur macOS.</span><span class="sxs-lookup"><span data-stu-id="48f99-144">Here is the example use SSH client on macOS.</span></span>
   <span data-ttu-id="48f99-145">![Client SSH exécuté sur macOS](media/iot-hub-gateway-kit-lessons/lesson1/ssh.png)</span><span class="sxs-lookup"><span data-stu-id="48f99-145">![SSH client running on macOS](media/iot-hub-gateway-kit-lessons/lesson1/ssh.png)</span></span>

## <a name="install-the-azure-iot-edge-package"></a><span data-ttu-id="48f99-146">Installer le package Azure IoT Edge</span><span class="sxs-lookup"><span data-stu-id="48f99-146">Install the Azure IoT Edge package</span></span>

<span data-ttu-id="48f99-147">Le package Azure IoT Edge contient les fichiers binaires précompilés du kit de développement logiciel (SDK) et de ses dépendances.</span><span class="sxs-lookup"><span data-stu-id="48f99-147">The Azure IoT Edge package contains the pre-compiled binaries of the SDK and its dependencies.</span></span> <span data-ttu-id="48f99-148">Ces fichiers binaires sont Azure IoT Edge, le kit de développement logiciel (SDK) Azure IoT et les outils correspondants.</span><span class="sxs-lookup"><span data-stu-id="48f99-148">These binaries are Azure IoT Edge, the Azure IoT SDK and the corresponding tools.</span></span> <span data-ttu-id="48f99-149">Le package contient également un exemple d’application « hello_world » qui est utilisé pour vérifier le bon fonctionnement de la passerelle.</span><span class="sxs-lookup"><span data-stu-id="48f99-149">The package also contains a "hello_world" sample application that is used to validate the gateway functionality.</span></span> <span data-ttu-id="48f99-150">IoT Edge constitue la partie principale de la passerelle.</span><span class="sxs-lookup"><span data-stu-id="48f99-150">IoT Edge is the core part of the gateway.</span></span> <span data-ttu-id="48f99-151">Pour installer le package, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="48f99-151">To install the package, follow these steps:</span></span>

1. <span data-ttu-id="48f99-152">Ajoutez le référentiel cloud IoT en exécutant les commandes suivantes dans une fenêtre de terminal :</span><span class="sxs-lookup"><span data-stu-id="48f99-152">Add the IoT cloud repository by running the following commands in a terminal window:</span></span>

   ```bash
   rpm --import http://iotdk.intel.com/misc/iot_pub.key
   smart channel --add IoT_Cloud type=rpm-md name="IoT_Cloud" baseurl=http://iotdk.intel.com/repos/iot-cloud/wrlinux7/rcpl13/ -y
   ```

   <span data-ttu-id="48f99-153">La commande `rpm` importe la clé rpm.</span><span class="sxs-lookup"><span data-stu-id="48f99-153">The `rpm` command imports the rpm key.</span></span> <span data-ttu-id="48f99-154">La commande `smart channel` ajoute le canal rpm au gestionnaire de package intelligent (Smart Package Manager).</span><span class="sxs-lookup"><span data-stu-id="48f99-154">The `smart channel` command adds the rpm channel to the Smart Package Manager.</span></span> <span data-ttu-id="48f99-155">Avant d’exécuter la commande `smart update`, vous voyez un résultat similaire à celui ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="48f99-155">Before you run the `smart update` command, you see an output like below.</span></span>

   ![Sortie des commandes rpm et canal intelligent](media/iot-hub-gateway-kit-lessons/lesson1/rpm_smart_channel.png)

   ```bash
   smart update
   ```

2. <span data-ttu-id="48f99-157">Exécutez la commande suivante pour installer le package :</span><span class="sxs-lookup"><span data-stu-id="48f99-157">Install the package by running the following command:</span></span>

   ```bash
   smart install packagegroup-cloud-azure -y
   ```

   <span data-ttu-id="48f99-158">`packagegroup-cloud-azure` est le nom du package.</span><span class="sxs-lookup"><span data-stu-id="48f99-158">`packagegroup-cloud-azure` is the name of the package.</span></span> <span data-ttu-id="48f99-159">La commande `smart install` permet d’installer le package.</span><span class="sxs-lookup"><span data-stu-id="48f99-159">The `smart install` command is used to install the package.</span></span>

   <span data-ttu-id="48f99-160">Une fois le package installé, Intel NUC doit fonctionner en tant que passerelle.</span><span class="sxs-lookup"><span data-stu-id="48f99-160">After the package is installed, Intel NUC is expected to work as a gateway.</span></span>

## <a name="run-the-azure-iot-edge-helloworld-sample-application"></a><span data-ttu-id="48f99-161">Exécution de l’exemple d’application « hello_world » d’Azure IoT Edge</span><span class="sxs-lookup"><span data-stu-id="48f99-161">Run the Azure IoT Edge "hello_world" sample application</span></span>

<span data-ttu-id="48f99-162">Accédez à `azureiotgatewaysdk/samples` et exécutez l’exemple d’application « hello_world ».</span><span class="sxs-lookup"><span data-stu-id="48f99-162">Go to `azureiotgatewaysdk/samples` and run the sample "hello_world" sample application.</span></span> <span data-ttu-id="48f99-163">Cet exemple d’application crée une passerelle à partir du fichier `hello_world.json` et utilise les composants fondamentaux de l’architecture Azure IoT Edge pour consigner le message « Hello World » dans un fichier toutes les 5 secondes.</span><span class="sxs-lookup"><span data-stu-id="48f99-163">This sample application creates a gateway from the `hello_world.json` file and uses the fundamental components of the Azure IoT Edge architecture to log a hello world message to a file every 5 seconds.</span></span>

<span data-ttu-id="48f99-164">Vous pouvez exécuter l’exemple d’application « hello_world » en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="48f99-164">You can run the sample "hello_world" sample application by running the following command:</span></span>

```bash
cd /usr/share/azureiotgatewaysdk/samples/hello_world/
./hello_world hello_world.json
```

<span data-ttu-id="48f99-165">L’exemple d’application génère la sortie suivante si la passerelle fonctionne correctement :</span><span class="sxs-lookup"><span data-stu-id="48f99-165">The sample application produces the following output if the gateway functionality is working correctly:</span></span>

![sortie d’application](media/iot-hub-gateway-kit-lessons/lesson1/hello_world.png)

<span data-ttu-id="48f99-167">Si vous rencontrez des problèmes, recherchez des solutions dans la [page de résolution des problèmes](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="48f99-167">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="summary"></a><span data-ttu-id="48f99-168">Résumé</span><span class="sxs-lookup"><span data-stu-id="48f99-168">Summary</span></span>

<span data-ttu-id="48f99-169">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="48f99-169">Congratulations!</span></span> <span data-ttu-id="48f99-170">Vous avez terminé la configuration d’Intel NUC comme passerelle.</span><span class="sxs-lookup"><span data-stu-id="48f99-170">You've finished setting up Intel NUC as a gateway.</span></span> <span data-ttu-id="48f99-171">Vous pouvez maintenant passer à la leçon suivante afin de configurer un ordinateur hôte, de créer un Azure IoT Hub et d’inscrire votre unité logique Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="48f99-171">Now you're ready to move on to the next lesson to set up your host computer, create an Azure IoT hub and register your Azure IoT hub logical device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="48f99-172">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="48f99-172">Next steps</span></span>
[<span data-ttu-id="48f99-173">Préparer votre ordinateur hôte et Azure IoT Hub</span><span class="sxs-lookup"><span data-stu-id="48f99-173">Get your host computer and Azure IoT hub ready</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)
