---
title: "Appareil SensorTag et passerelle Azure Io - Leçon 1 : Configurer l’Intel NUC | Microsoft Docs"
description: "Configurez Intel NUC comme passerelle IoT entre un capteur et Azure IoT Hub, afin de collecter des informations de capteurs et de les envoyer à IoT Hub."
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
ms.openlocfilehash: 1a3a92ab8d08c6ed6f047208217c46022027157e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="set-up-intel-nuc-as-an-iot-gateway"></a><span data-ttu-id="987ca-104">Configurer l’Intel NUC comme passerelle IoT</span><span class="sxs-lookup"><span data-stu-id="987ca-104">Set up Intel NUC as an IoT gateway</span></span>
[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

## <a name="what-you-will-do"></a><span data-ttu-id="987ca-105">Procédure à suivre</span><span class="sxs-lookup"><span data-stu-id="987ca-105">What you will do</span></span>

- <span data-ttu-id="987ca-106">Configurez l’Intel NUC comme passerelle IoT.</span><span class="sxs-lookup"><span data-stu-id="987ca-106">Set up Intel NUC as an IoT gateway.</span></span>
- <span data-ttu-id="987ca-107">Installez le package Azure IoT Edge sur l’Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="987ca-107">Install the Azure IoT Edge package on the Intel NUC.</span></span>
- <span data-ttu-id="987ca-108">Exécutez un exemple d’application « hello_world » sur l’Intel NUC pour vérifier le bon fonctionnement de la passerelle.</span><span class="sxs-lookup"><span data-stu-id="987ca-108">Run a "hello_world" sample application on the Intel NUC to verify the gateway functionality.</span></span>

  > <span data-ttu-id="987ca-109">Si vous rencontrez des problèmes, recherchez des solutions dans la [page de résolution des problèmes](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="987ca-109">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="987ca-110">Contenu</span><span class="sxs-lookup"><span data-stu-id="987ca-110">What you will learn</span></span>

<span data-ttu-id="987ca-111">Dans cette leçon, vous allez apprendre :</span><span class="sxs-lookup"><span data-stu-id="987ca-111">In this lesson, you will learn:</span></span>

- <span data-ttu-id="987ca-112">la connexion d’Intel NUC à des périphériques ;</span><span class="sxs-lookup"><span data-stu-id="987ca-112">How to connect Intel NUC with peripherals.</span></span>
- <span data-ttu-id="987ca-113">l’installation et la mise à jour des packages nécessaires sur Intel NUC à l’aide du gestionnaire de package intelligent ;</span><span class="sxs-lookup"><span data-stu-id="987ca-113">How to install and update the required packages on Intel NUC using the Smart Package Manager.</span></span>
- <span data-ttu-id="987ca-114">l’exécution de l’exemple d’application « hello_world » pour vérifier le bon fonctionnement de la passerelle.</span><span class="sxs-lookup"><span data-stu-id="987ca-114">How to run the "hello_world" sample application to verify the gateway functionality.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="987ca-115">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="987ca-115">What you need</span></span>

- <span data-ttu-id="987ca-116">Un Kit Intel NUC DE3815TYKE avec la suite logicielle de passerelle Intel IoT (Wind River Linux *7.0.0.13) préinstallée.</span><span class="sxs-lookup"><span data-stu-id="987ca-116">An Intel NUC Kit DE3815TYKE with the Intel IoT Gateway Software Suite (Wind River Linux *7.0.0.13) preinstalled.</span></span> <span data-ttu-id="987ca-117">[Cliquez ici pour acheter le kit de passerelle commerciale Grove IoT](https://www.seeedstudio.com/Grove-IoT-Commercial-Gateway-Kit-p-2724.html).</span><span class="sxs-lookup"><span data-stu-id="987ca-117">[Click here to purchase Grove IoT Commercial Gateway Kit](https://www.seeedstudio.com/Grove-IoT-Commercial-Gateway-Kit-p-2724.html).</span></span>
- <span data-ttu-id="987ca-118">Un câble Ethernet.</span><span class="sxs-lookup"><span data-stu-id="987ca-118">An Ethernet cable.</span></span>
- <span data-ttu-id="987ca-119">Un clavier.</span><span class="sxs-lookup"><span data-stu-id="987ca-119">A keyboard.</span></span>
- <span data-ttu-id="987ca-120">Un câble VGA ou HDMI.</span><span class="sxs-lookup"><span data-stu-id="987ca-120">An HDMI or VGA cable.</span></span>
- <span data-ttu-id="987ca-121">Un écran équipé d’un port VGA ou HDMI.</span><span class="sxs-lookup"><span data-stu-id="987ca-121">A monitor with an HDMI or VGA port.</span></span>
- <span data-ttu-id="987ca-122">Facultatif : [SensorTag Texas Instruments (CC2650STK)](http://www.ti.com/tool/cc2650stk)</span><span class="sxs-lookup"><span data-stu-id="987ca-122">Optional: [Texas Instruments Sensor Tag (CC2650STK)](http://www.ti.com/tool/cc2650stk)</span></span>

![Un kit de passerelle](media/iot-hub-gateway-kit-lessons/lesson1/kit.png)

## <a name="connect-intel-nuc-with-the-peripherals"></a><span data-ttu-id="987ca-124">Connexion d’Intel NUC aux périphériques</span><span class="sxs-lookup"><span data-stu-id="987ca-124">Connect Intel NUC with the peripherals</span></span>

<span data-ttu-id="987ca-125">L’image ci-dessous est un exemple d’Intel NUC connecté à plusieurs périphériques :</span><span class="sxs-lookup"><span data-stu-id="987ca-125">The image below is an example of Intel NUC that is connected with various peripherals:</span></span>

1. <span data-ttu-id="987ca-126">Connecté à un clavier.</span><span class="sxs-lookup"><span data-stu-id="987ca-126">Connected to a keyboard.</span></span>
2. <span data-ttu-id="987ca-127">Connecté à un écran à l’aide d’un câble VGA ou d’un câble HDMI.</span><span class="sxs-lookup"><span data-stu-id="987ca-127">Connected to a monitor with a VGA cable or HDMI cable.</span></span>
3. <span data-ttu-id="987ca-128">Connecté à un réseau filaire à l’aide d’un câble Ethernet.</span><span class="sxs-lookup"><span data-stu-id="987ca-128">Connected to a wired network with an Ethernet cable.</span></span>
4. <span data-ttu-id="987ca-129">Connecté à l’alimentation à l’aide d’un câble d’alimentation.</span><span class="sxs-lookup"><span data-stu-id="987ca-129">Connected to a power supply with a power cable.</span></span>

![Intel NUC connecté à des périphériques](media/iot-hub-gateway-kit-lessons/lesson1/nuc.png)

## <a name="connect-to-the-intel-nuc-system-from-host-computer-via-secure-shell-ssh"></a><span data-ttu-id="987ca-131">Connexion au système Intel NUC à partir de l’ordinateur hôte par le biais de Secure Shell (SSH)</span><span class="sxs-lookup"><span data-stu-id="987ca-131">Connect to the Intel NUC system from host computer via Secure Shell (SSH)</span></span>

<span data-ttu-id="987ca-132">Vous aurez besoin d’un clavier et d’un écran pour obtenir l’adresse IP de votre appareil Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="987ca-132">You will need a keyboard and a monitor to get the IP address of your Intel NUC device.</span></span> <span data-ttu-id="987ca-133">Si vous connaissez déjà l’adresse IP, vous pouvez passer directement à l’étape 3 de cette section.</span><span class="sxs-lookup"><span data-stu-id="987ca-133">If you already know the IP address, you can skip ahead to step 3 in this section.</span></span>

1. <span data-ttu-id="987ca-134">Activez l’Intel NUC en appuyant sur le bouton d’alimentation, puis connectez-vous.</span><span class="sxs-lookup"><span data-stu-id="987ca-134">Turn on the Intel NUC by pressing the power button and then log in.</span></span>

   <span data-ttu-id="987ca-135">Le nom d’utilisateur et le mot de passe par défaut sont tous les deux `root`.</span><span class="sxs-lookup"><span data-stu-id="987ca-135">The default user name and password are both `root`.</span></span>

       > Hit the enter key on your keyboard if you see either of the following errors when you boot: 'A TPM error (7) occurred attempting to read a pcr value.' or 'Timeout, No TPM chip found, activating TPM-bypass!'

2. <span data-ttu-id="987ca-136">Obtenez l’adresse IP de l’Intel NUC en exécutant la commande `ifconfig` sur l’appareil Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="987ca-136">Get the IP address of the Intel NUC by running the `ifconfig` command on the Intel NUC device.</span></span>

   <span data-ttu-id="987ca-137">Voici un exemple de la sortie de cette commande.</span><span class="sxs-lookup"><span data-stu-id="987ca-137">Here is an example of the command output.</span></span>

   ![Sortie de la commande ifconfig indiquant l’adresse IP de l’Intel NUC](media/iot-hub-gateway-kit-lessons/lesson1/ifconfig.png)

   <span data-ttu-id="987ca-139">Dans cet exemple, la valeur qui suit `inet addr:` correspond à l’adresse IP dont vous avez besoin lorsque vous vous connectez à l’Intel NUC à partir d’un ordinateur hôte.</span><span class="sxs-lookup"><span data-stu-id="987ca-139">In this example, the value that follows `inet addr:` is the IP address that you need when connect to the Intel NUC from a host computer.</span></span>

3. <span data-ttu-id="987ca-140">Utilisez l’un des clients SSH suivants à partir de votre ordinateur hôte pour vous connecter à l’Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="987ca-140">Use one of the following SSH clients from your host computer to connect to Intel NUC.</span></span>

    - <span data-ttu-id="987ca-141">[PuTTY](http://www.putty.org/) pour Windows.</span><span class="sxs-lookup"><span data-stu-id="987ca-141">[PuTTY](http://www.putty.org/) for Windows.</span></span>
    - <span data-ttu-id="987ca-142">Le client SSH intégré sur Ubuntu ou macOS.</span><span class="sxs-lookup"><span data-stu-id="987ca-142">The built-in SSH client on Ubuntu or macOS.</span></span>

   <span data-ttu-id="987ca-143">Il est plus efficace et productif d’utiliser un Intel NUC à partir d’un ordinateur hôte.</span><span class="sxs-lookup"><span data-stu-id="987ca-143">It is more efficient and productive to operate an Intel NUC from a host computer.</span></span> <span data-ttu-id="987ca-144">Vous aurez besoin de l’adresse IP, du nom d’utilisateur et du mot de passe de l’Intel NUC pour vous y connecter par le biais d’un client SSH.</span><span class="sxs-lookup"><span data-stu-id="987ca-144">You'll need the Intel NUC's IP address, user name and password to connect to it via an SSH client.</span></span> <span data-ttu-id="987ca-145">Voici un exemple qui fait appel à un client SSH sur Mac OS.</span><span class="sxs-lookup"><span data-stu-id="987ca-145">Here is an example that uses an SSH client on macOS.</span></span>
   <span data-ttu-id="987ca-146">![Client SSH exécuté sur macOS](media/iot-hub-gateway-kit-lessons/lesson1/ssh.png)</span><span class="sxs-lookup"><span data-stu-id="987ca-146">![SSH client running on macOS](media/iot-hub-gateway-kit-lessons/lesson1/ssh.png)</span></span>

## <a name="install-the-azure-iot-edge-package"></a><span data-ttu-id="987ca-147">Installer le package Azure IoT Edge</span><span class="sxs-lookup"><span data-stu-id="987ca-147">Install the Azure IoT Edge package</span></span>

<span data-ttu-id="987ca-148">Le package Azure IoT Edge contient les fichiers binaires précompilés d’Azure IoT Edge et de ses dépendances.</span><span class="sxs-lookup"><span data-stu-id="987ca-148">The Azure IoT Edge package contains the pre-compiled binaries of IoT Edge and its dependencies.</span></span> <span data-ttu-id="987ca-149">Ces fichiers binaires sont Azure IoT Edge, le kit de développement logiciel (SDK) Azure IoT et les outils correspondants.</span><span class="sxs-lookup"><span data-stu-id="987ca-149">These binaries are Azure IoT Edge, the Azure IoT SDK and the corresponding tools.</span></span> <span data-ttu-id="987ca-150">Le package contient également un exemple d’application « hello_world » qui est utilisé pour vérifier le bon fonctionnement de la passerelle.</span><span class="sxs-lookup"><span data-stu-id="987ca-150">The package also contains a "hello_world" sample application is used to validate the gateway functionality.</span></span> <span data-ttu-id="987ca-151">IoT Edge constitue la partie principale de la passerelle.</span><span class="sxs-lookup"><span data-stu-id="987ca-151">IoT Edge is the core part of the gateway.</span></span> 

<span data-ttu-id="987ca-152">Pour installer le package, procédez comme suit.</span><span class="sxs-lookup"><span data-stu-id="987ca-152">Follow these steps to install the package.</span></span>

1. <span data-ttu-id="987ca-153">Ajoutez le référentiel cloud IoT en exécutant les commandes suivantes dans une fenêtre de terminal :</span><span class="sxs-lookup"><span data-stu-id="987ca-153">Add the IoT Cloud repository by running the following commands in a terminal window:</span></span>

   ```bash
   rpm --import https://iotdk.intel.com/misc/iot_pub2.key
   smart channel --add IoT_Cloud type=rpm-md name="IoT_Cloud" baseurl=http://iotdk.intel.com/repos/iot-cloud/wrlinux7/rcpl13/ -y
   smart channel --add WR_Repo type=rpm-md baseurl=https://distro.windriver.com/release/idp-3-xt/public_feeds/WR-IDP-3-XT-Intel-Baytrail-public-repo/RCPL13/corei7_64/
   ```

   > <span data-ttu-id="987ca-154">Entrez « o » quand il vous est demandé si vous voulez « inclure ce canal ? »</span><span class="sxs-lookup"><span data-stu-id="987ca-154">Enter 'y', when it prompts you to 'Include this channel?'</span></span>
   
   <span data-ttu-id="987ca-155">Si vous recevez une erreur `import read failed(-1)`, utilisez les commandes suivantes pour résoudre le problème :</span><span class="sxs-lookup"><span data-stu-id="987ca-155">If you receive an `import read failed(-1)` error, use the following commands to resolve the issue:</span></span>
   ```bash
   wget http://iotdk.intel.com/misc/iot_pub2.key 
   rpm --import iot_pub2.key  
   ```

   <span data-ttu-id="987ca-156">La commande `rpm` importe la clé rpm.</span><span class="sxs-lookup"><span data-stu-id="987ca-156">The `rpm` command imports the rpm key.</span></span> <span data-ttu-id="987ca-157">La commande `smart channel` ajoute le canal rpm au gestionnaire de package intelligent (Smart Package Manager).</span><span class="sxs-lookup"><span data-stu-id="987ca-157">The `smart channel` command adds the rpm channel to the Smart Package Manager.</span></span> <span data-ttu-id="987ca-158">Avant d’exécuter la commande `smart update`, vous verrez une sortie similaire à celle ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="987ca-158">Before you run the `smart update` command, you will see an output like below.</span></span>

   ![Sortie des commandes rpm et canal intelligent](media/iot-hub-gateway-kit-lessons/lesson1/rpm_smart_channel.png)

2. <span data-ttu-id="987ca-160">Exécutez la commande smart update :</span><span class="sxs-lookup"><span data-stu-id="987ca-160">Execute the smart update command:</span></span>

   ```bash
   smart update
   ```

3. <span data-ttu-id="987ca-161">Installez le package Gateway Azure IoT en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="987ca-161">Install the Azure IoT Gateway package by running the following command:</span></span>

   ```bash
   smart install packagegroup-cloud-azure -y
   ```

   <span data-ttu-id="987ca-162">`packagegroup-cloud-azure` est le nom du package.</span><span class="sxs-lookup"><span data-stu-id="987ca-162">`packagegroup-cloud-azure` is the name of the package.</span></span> <span data-ttu-id="987ca-163">La commande `smart install` permet d’installer le package.</span><span class="sxs-lookup"><span data-stu-id="987ca-163">The `smart install` command is used to install the package.</span></span>

    > <span data-ttu-id="987ca-164">Exécutez la commande suivante si vous recevez l’erreur « public key not available » (Clé publique non disponible).</span><span class="sxs-lookup"><span data-stu-id="987ca-164">Run the following command if you see this error: 'public key not available'</span></span>

    ```bash
    smart config --set rpm-check-signatures=false
    smart install packagegroup-cloud-azure -y
    ```
    > <span data-ttu-id="987ca-165">Redémarrez l’ordinateur Intel NUC si vous voyez cette erreur : « aucun package ne fournit util-linux-dev »</span><span class="sxs-lookup"><span data-stu-id="987ca-165">Reboot the Intel NUC if you see this error: 'no package provides util-linux-dev'</span></span>

   <span data-ttu-id="987ca-166">Une fois le package installé, l’Intel NUC est prêt à fonctionner en tant que passerelle.</span><span class="sxs-lookup"><span data-stu-id="987ca-166">After the package is installed, Intel NUC is ready to function as a gateway.</span></span>

## <a name="run-the-azure-iot-edge-helloworld-sample-application"></a><span data-ttu-id="987ca-167">Exécution de l’exemple d’application « hello_world » d’Azure IoT Edge</span><span class="sxs-lookup"><span data-stu-id="987ca-167">Run the Azure IoT Edge "hello_world" sample application</span></span>

<span data-ttu-id="987ca-168">L’exemple d’application suivant crée une passerelle à partir d’un fichier `hello_world.json` et utilise les composants fondamentaux de l’architecture Azure IoT Edge pour consigner le message « Hello World » dans un fichier (log.txt) toutes les 5 secondes.</span><span class="sxs-lookup"><span data-stu-id="987ca-168">The following sample application creates a gateway from a `hello_world.json` file and uses the fundamental components of Azure IoT Edge architecture to log a hello world message to a file (log.txt) every 5 seconds.</span></span>

<span data-ttu-id="987ca-169">Vous pouvez exécuter l’exemple Hello World en utilisant les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="987ca-169">You can run the Hello World sample by executing the following commands:</span></span>

```bash
cd /usr/share/azureiotgatewaysdk/samples/hello_world/
./hello_world hello_world.json
```

<span data-ttu-id="987ca-170">Laissez l’application Hello World s’exécuter pendant quelques minutes, puis appuyez sur la touche Entrée pour l’arrêter.</span><span class="sxs-lookup"><span data-stu-id="987ca-170">Let the Hello World application run for a few minutes and then hit the Enter key to stop it.</span></span>
<span data-ttu-id="987ca-171">![Sortie de l’application](media/iot-hub-gateway-kit-lessons/lesson1/hello_world.png)</span><span class="sxs-lookup"><span data-stu-id="987ca-171">![application output](media/iot-hub-gateway-kit-lessons/lesson1/hello_world.png)</span></span>

> <span data-ttu-id="987ca-172">Vous pouvez ignorer les erreurs « invalid argument handle(NULL) » (Descripteur d’argument non valide (NULL)) qui s’affichent après que vous avez appuyé sur Entrée.</span><span class="sxs-lookup"><span data-stu-id="987ca-172">You can ignore any 'invalid argument handle(NULL)' errors that appear after you hit Enter.</span></span>

<span data-ttu-id="987ca-173">Vous pouvez vérifier que la passerelle a été correctement exécutée en ouvrant le fichier log.txt qui se trouve maintenant dans votre dossier hello_world : ![Vue du répertoire de log.txt](media/iot-hub-gateway-kit-lessons/lesson1/logtxtdir.png)</span><span class="sxs-lookup"><span data-stu-id="987ca-173">You can verify that the gateway ran successfully by opening the log.txt file that is now in your hello_world folder ![log.txt directory view](media/iot-hub-gateway-kit-lessons/lesson1/logtxtdir.png)</span></span>

<span data-ttu-id="987ca-174">Ouvrez le fichier log.txt en utilisant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="987ca-174">Open log.txt using the following command:</span></span>

```bash
vim log.txt
```

<span data-ttu-id="987ca-175">Vous verrez alors le contenu du fichier log.txt, qui est une sortie mise en forme des messages de journalisation qui ont été consignés toutes les 5 secondes par le module de passerelle Hello World.</span><span class="sxs-lookup"><span data-stu-id="987ca-175">You will then see the contents of log.txt, which will be a JSON formatted output of the logging messages that were written every 5 seconds by the gateway Hello World module.</span></span>
<span data-ttu-id="987ca-176">![Vue du répertoire de log.txt](media/iot-hub-gateway-kit-lessons/lesson1/logtxtview.png)</span><span class="sxs-lookup"><span data-stu-id="987ca-176">![log.txt directory view](media/iot-hub-gateway-kit-lessons/lesson1/logtxtview.png)</span></span>

<span data-ttu-id="987ca-177">Si vous rencontrez des problèmes, recherchez des solutions dans la [page de résolution des problèmes](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="987ca-177">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="summary"></a><span data-ttu-id="987ca-178">Résumé</span><span class="sxs-lookup"><span data-stu-id="987ca-178">Summary</span></span>

<span data-ttu-id="987ca-179">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="987ca-179">Congratulations!</span></span> <span data-ttu-id="987ca-180">Vous avez terminé la configuration d’Intel NUC comme passerelle.</span><span class="sxs-lookup"><span data-stu-id="987ca-180">You've finished setting up Intel NUC as a gateway.</span></span> <span data-ttu-id="987ca-181">Vous pouvez maintenant passer à la leçon suivante afin de configurer un ordinateur hôte, de créer un Azure IoT Hub et d’inscrire votre unité logique Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="987ca-181">Now you're ready to move on to the next lesson to set up your host computer, create an Azure IoT Hub and register your Azure IoT Hub logical device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="987ca-182">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="987ca-182">Next steps</span></span>
[<span data-ttu-id="987ca-183">Utiliser une passerelle IoT pour connecter un appareil à Azure IoT Hub</span><span class="sxs-lookup"><span data-stu-id="987ca-183">Use an IoT gateway to connect a device to Azure IoT Hub</span></span>](iot-hub-gateway-kit-c-iot-gateway-connect-device-to-cloud.md)

