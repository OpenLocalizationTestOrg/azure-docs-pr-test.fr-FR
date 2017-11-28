---
title: "Connecter Raspberry Pi (C) à Azure IoT - Résolution des problèmes | Microsoft Docs"
description: "Page Dépannage pour l’expérience Node.js Raspberry Pi"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "problèmes iot, problèmes liés à l’internet des objets"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: 3653c79b-8a0c-41d4-b0bf-f6b4edb4d233
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 828669db23fa8d608029134fbe364033456d935a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting"></a><span data-ttu-id="0e600-104">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="0e600-104">Troubleshooting</span></span>
## <a name="hardware-issues"></a><span data-ttu-id="0e600-105">Problèmes matériels</span><span class="sxs-lookup"><span data-stu-id="0e600-105">Hardware issues</span></span>
### <a name="the-application-runs-well-but-the-led-is-not-blinking"></a><span data-ttu-id="0e600-106">L’application s’exécute correctement, mais la LED ne clignote pas</span><span class="sxs-lookup"><span data-stu-id="0e600-106">The application runs well but the LED is not blinking</span></span>
<span data-ttu-id="0e600-107">Ce problème est toujours lié à la connectivité du circuit matériel.</span><span class="sxs-lookup"><span data-stu-id="0e600-107">This issue is always related to the hardware circuit connectivity.</span></span> <span data-ttu-id="0e600-108">Pour identifier les problèmes, procédez comme suit.</span><span class="sxs-lookup"><span data-stu-id="0e600-108">Use the following steps to identify problems.</span></span>

1. <span data-ttu-id="0e600-109">Assurez-vous d’avoir choisi le port **GPIO** correct sur votre carte.</span><span class="sxs-lookup"><span data-stu-id="0e600-109">Check that you chose the correct **GPIO** on your board.</span></span> <span data-ttu-id="0e600-110">Les deux ports utilisés doivent être **GPIO GND (broche 6)** et **GPIO 04 (broche 7)**.</span><span class="sxs-lookup"><span data-stu-id="0e600-110">The two ports should be **GPIO GND (Pin 6)** and **GPIO 04 (Pin 7)**.</span></span>
2. <span data-ttu-id="0e600-111">Vérifiez que la polarité de votre LED est correcte.</span><span class="sxs-lookup"><span data-stu-id="0e600-111">Check that the polarity of your LED is correct.</span></span> <span data-ttu-id="0e600-112">Le segment le plus long doit indiquer la broche de l’anode, **positif**.</span><span class="sxs-lookup"><span data-stu-id="0e600-112">The longer leg should indicate the **positive**, anode pin.</span></span>
3. <span data-ttu-id="0e600-113">Utilisez la **broche 3.3V** et la **broche GND** sur Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="0e600-113">Use the **3.3V Pin** and **GND Pin** on Raspberry Pi 3.</span></span> <span data-ttu-id="0e600-114">Utilisez Pi comme alimentation en courant continu.</span><span class="sxs-lookup"><span data-stu-id="0e600-114">Treat Pi as the DC power.</span></span> <span data-ttu-id="0e600-115">Vérifiez que la LED fonctionne correctement.</span><span class="sxs-lookup"><span data-stu-id="0e600-115">Check that the LED works fine.</span></span>

![Spécification de la LED](media/iot-hub-raspberry-pi-lessons/troubleshooting/led_spec.png)

### <a name="other-hardware-issues"></a><span data-ttu-id="0e600-117">Autres problèmes matériels</span><span class="sxs-lookup"><span data-stu-id="0e600-117">Other hardware issues</span></span>
<span data-ttu-id="0e600-118">Pour plus d’informations sur la résolution de problèmes courants sur Raspberry Pi 3, consultez la [page officielle de résolution des problèmes](http://elinux.org/R-Pi_Troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="0e600-118">For information about solving common problems on Raspberry Pi 3, see the [official troubleshooting page](http://elinux.org/R-Pi_Troubleshooting).</span></span>

## <a name="nodejs-package-issues"></a><span data-ttu-id="0e600-119">Problèmes de package Node.js</span><span class="sxs-lookup"><span data-stu-id="0e600-119">Node.js package issues</span></span>
### <a name="no-response-during-gulp-tasks"></a><span data-ttu-id="0e600-120">Aucune réponse lors des tâches gulp</span><span class="sxs-lookup"><span data-stu-id="0e600-120">No response during gulp tasks</span></span>
<span data-ttu-id="0e600-121">Si vous rencontrez des problèmes d’exécution des tâches gulp, vous pouvez ajouter l’option `--verbose` pour le débogage.</span><span class="sxs-lookup"><span data-stu-id="0e600-121">If you encounter problems running gulp tasks, you can add the `--verbose` option for debugging.</span></span> <span data-ttu-id="0e600-122">Essayez d’arrêter les tâches gulp en cours en appuyant sur `Ctrl + C`, puis exécutez la commande suivante dans la fenêtre de la console pour afficher les messages de débogage.</span><span class="sxs-lookup"><span data-stu-id="0e600-122">Try to terminate current gulp tasks by using `Ctrl + C`, and then run the following command in your console window to see debug messages.</span></span> <span data-ttu-id="0e600-123">Des messages d’erreur détaillés peuvent s’afficher dans la sortie de la console.</span><span class="sxs-lookup"><span data-stu-id="0e600-123">You might see detailed error messages in your console output.</span></span> 

```bash
gulp --verbose
```

### <a name="device-discovery-issues"></a><span data-ttu-id="0e600-124">Problèmes de détection d’appareil</span><span class="sxs-lookup"><span data-stu-id="0e600-124">Device discovery issues</span></span>
<span data-ttu-id="0e600-125">Pour obtenir de l’aide sur la résolution de problèmes courants liés à la commande `devdisco`, consultez la rubrique [Lisez-moi](https://github.com/Azure/device-discovery-cli/blob/develop/readme.md).</span><span class="sxs-lookup"><span data-stu-id="0e600-125">For help in troubleshooting common problems with the `devdisco` command, check the [readme](https://github.com/Azure/device-discovery-cli/blob/develop/readme.md).</span></span>

### <a name="npm-issues"></a><span data-ttu-id="0e600-126">Problèmes liés à NPM</span><span class="sxs-lookup"><span data-stu-id="0e600-126">NPM issues</span></span>
<span data-ttu-id="0e600-127">Essayez de mettre à jour votre package NPM avec la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="0e600-127">Try to update your NPM package with the following command:</span></span>

```bash
npm install -g npm
```

<span data-ttu-id="0e600-128">Si le problème persiste, entrez vos commentaires à la fin de cet article ou créez un problème GitHub dans notre [exemple de référentiel](https://github.com/Azure-Samples/iot-hub-c-raspberrypi-getting-started)</span><span class="sxs-lookup"><span data-stu-id="0e600-128">If the problem still exists, leave your comments at the end of this article or create a GitHub issue in our [sample repository](https://github.com/Azure-Samples/iot-hub-c-raspberrypi-getting-started)</span></span>

## <a name="remote-debugging"></a><span data-ttu-id="0e600-129">Débogage à distance</span><span class="sxs-lookup"><span data-stu-id="0e600-129">Remote debugging</span></span>

<span data-ttu-id="0e600-130">La prise en charge du débogage à distance sera disponible prochainement dans l’extension C/C++ de Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="0e600-130">Remote debugging support will be available soon in Visual Studio Code C/C++ Extension.</span></span>

<span data-ttu-id="0e600-131">En attendant, vous pouvez utiliser GDB via votre terminal SSH favori :</span><span class="sxs-lookup"><span data-stu-id="0e600-131">In a meanwhile you can use GDB via your favourite SSH terminal:</span></span>

```bash
cd c-pi-lesson-x
sudo gdb app
```

## <a name="azure-cli-issues"></a><span data-ttu-id="0e600-132">Problèmes liés à l'interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="0e600-132">Azure-CLI issues</span></span>
<span data-ttu-id="0e600-133">L’interface de ligne de commande Azure est une version d’évaluation.</span><span class="sxs-lookup"><span data-stu-id="0e600-133">The Azure command-line interface (Azure CLI) is a preview build.</span></span> <span data-ttu-id="0e600-134">Pour rechercher des solutions, voir le [Guide d’installation de la version d’évaluation](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md).</span><span class="sxs-lookup"><span data-stu-id="0e600-134">Look for solution in the [Preview Install Guide](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md) to seek solutions.</span></span> <span data-ttu-id="0e600-135">Essayez de mettre à niveau Azure-cli à la version la plus récente lorsque les commandes ne fonctionnent pas comme prévu.</span><span class="sxs-lookup"><span data-stu-id="0e600-135">Try to upgrade Azure-cli to latest version when commands don’t work as expected.</span></span>

<span data-ttu-id="0e600-136">Si vous rencontrez des bogues avec l’outil, documentez un [problème](https://github.com/Azure/azure-cli/issues) dans la section **Issues** du dépôt GitHub.</span><span class="sxs-lookup"><span data-stu-id="0e600-136">If you encounter any bugs with the tool, file an [issue](https://github.com/Azure/azure-cli/issues) in the **Issues** section of the GitHub repo.</span></span>

<span data-ttu-id="0e600-137">Pour obtenir de l’aide sur la résolution de problèmes courants, voir la rubrique [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span><span class="sxs-lookup"><span data-stu-id="0e600-137">For help troubleshooting common problems, check the [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span></span>

<span data-ttu-id="0e600-138">Si l’erreur « Impossible de trouver une version conforme à la configuration requise » s’affiche, exécutez la commande suivante pour mettre à niveau pip vers la dernière version.</span><span class="sxs-lookup"><span data-stu-id="0e600-138">If you meet "Could not find a version that satisfies the requirement", please run the following command to upgrade pip to lastest version.</span></span>

```bash
python -m pip install --upgrade pip
```

## <a name="python-installation-issues"></a><span data-ttu-id="0e600-139">Problèmes d’installation de Python</span><span class="sxs-lookup"><span data-stu-id="0e600-139">Python installation issues</span></span>
### <a name="legacy-installation-issues-macos"></a><span data-ttu-id="0e600-140">Problèmes d’installation héritée (macOS)</span><span class="sxs-lookup"><span data-stu-id="0e600-140">Legacy installation issues (macOS)</span></span>
<span data-ttu-id="0e600-141">Lors de l’installation de **pip**, une erreur d’autorisation est levée s’il existe des packages antérieurs qui sont installés avec des autorisations **su**.</span><span class="sxs-lookup"><span data-stu-id="0e600-141">When you're installing **pip**, a permission error is thrown when older packages that are installed with **su** permissions.</span></span> <span data-ttu-id="0e600-142">Cette situation se produit parce qu’une installation précédente de Python utilisant brew (macOS) n’est pas complètement désinstallée.</span><span class="sxs-lookup"><span data-stu-id="0e600-142">This situation occurs because a previous installation of Python using brew (macOS) is not uninstalled completely.</span></span> <span data-ttu-id="0e600-143">Certains packages **pip** d’une installation précédente ont été créés par root, ce qui génère l’erreur d’autorisation.</span><span class="sxs-lookup"><span data-stu-id="0e600-143">Some **pip** packages from a previous installation were created by root, which causes the permission error.</span></span> <span data-ttu-id="0e600-144">La solution consiste à supprimer les packages installés par root.</span><span class="sxs-lookup"><span data-stu-id="0e600-144">The solution is to remove those packages installed by root.</span></span> <span data-ttu-id="0e600-145">Pour effectuer cette tâche, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="0e600-145">Use the following steps to complete this task:</span></span>

1. <span data-ttu-id="0e600-146">Accédez à : /usr/local/lib/python2.7/site-packages</span><span class="sxs-lookup"><span data-stu-id="0e600-146">Go to: /usr/local/lib/python2.7/site-packages</span></span>
2. <span data-ttu-id="0e600-147">Affichez la liste des packages créés par root : `ls -l | grep root`.</span><span class="sxs-lookup"><span data-stu-id="0e600-147">List packages create by root: `ls -l | grep root`</span></span>
3. <span data-ttu-id="0e600-148">Désinstallez les packages identifiés à l’étape 2 : `sudo rm -rf {package name}`</span><span class="sxs-lookup"><span data-stu-id="0e600-148">Uninstall packages from step 2: `sudo rm -rf {package name}`</span></span>
4. <span data-ttu-id="0e600-149">Réinstallez Python.</span><span class="sxs-lookup"><span data-stu-id="0e600-149">Reinstall Python.</span></span>

## <a name="azure-iot-hub-issues"></a><span data-ttu-id="0e600-150">Problèmes liés à Azure IoT Hub</span><span class="sxs-lookup"><span data-stu-id="0e600-150">Azure IoT Hub issues</span></span>
<span data-ttu-id="0e600-151">Si vous avez correctement configuré votre Azure IoT Hub avec `azure-cli`, et avez besoin d’un outil pour gérer les appareils se connectant à votre IoT Hub, essayez les outils suivants :</span><span class="sxs-lookup"><span data-stu-id="0e600-151">If you've successfully provisioned your Azure IoT hub with `azure-cli`, and you need a tool to manage the devices that are connecting to your IoT hub, try the following tools:</span></span>

### <a name="device-explorer"></a><span data-ttu-id="0e600-152">Explorateur d’appareils</span><span class="sxs-lookup"><span data-stu-id="0e600-152">Device Explorer</span></span>
<span data-ttu-id="0e600-153">L’[Explorateur d’appareils](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) s’exécute sur votre ordinateur Windows local et se connecte à votre IoT Hub dans Azure.</span><span class="sxs-lookup"><span data-stu-id="0e600-153">[Device Explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) runs on your Windows local machine and connects to your IoT hub in Azure.</span></span> <span data-ttu-id="0e600-154">Il communique avec les [points de terminaison IoT Hub](iot-hub-devguide.md) suivants :</span><span class="sxs-lookup"><span data-stu-id="0e600-154">It communicates with the following [IoT Hub endpoints](iot-hub-devguide.md):</span></span>

* <span data-ttu-id="0e600-155">*Device identity management* (Gestion d’identité d’appareil) pour configurer et gérer les appareils inscrits auprès de votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="0e600-155">*Device identity management* to provision and manage devices registered with your IoT hub.</span></span>
* <span data-ttu-id="0e600-156">*Receive device-to-cloud* (Réception appareil-à-cloud) pour pouvoir surveiller les messages envoyés par votre appareil à votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="0e600-156">*Receive device-to-cloud* so you can monitor messages sent from your device to your IoT hub.</span></span>
* <span data-ttu-id="0e600-157">*Send cloud-to-device* (Envoi cloud-à-appareil) pour pouvoir envoyer des messages à vos appareils à partir de votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="0e600-157">*Send cloud-to-device* so you can send messages to your devices from your IoT hub.</span></span>

<span data-ttu-id="0e600-158">Configurez votre `IoT hub connection string` dans cet outil pour utiliser toutes ses fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="0e600-158">Configure your `IoT hub connection string` within this tool to use all its capabilities.</span></span>

### <a name="iot-hub-explorer"></a><span data-ttu-id="0e600-159">IoT Hub Explorer</span><span class="sxs-lookup"><span data-stu-id="0e600-159">IoT hub Explorer</span></span>
<span data-ttu-id="0e600-160">[IoT Hub Explorer](https://github.com/Azure/iothub-explorer) est un exemple d’outil d’interface de ligne de commande multiplateforme destiné à la gestion d’appareils clients.</span><span class="sxs-lookup"><span data-stu-id="0e600-160">[IoT hub Explorer](https://github.com/Azure/iothub-explorer) is a sample multiplatform CLI tool to manage device clients.</span></span> <span data-ttu-id="0e600-161">Cet outil permet de gérer les appareils dans le registre des identités, de surveiller les messages appareil-à-cloud et d’envoyer des commandes cloud-à-appareil.</span><span class="sxs-lookup"><span data-stu-id="0e600-161">You can use the tool to manage the devices in the identity registry, monitor device-to-cloud messages, and send cloud-to-device commands.</span></span>

<span data-ttu-id="0e600-162">Pour installer la dernière version (préliminaire) de l’outil iothub-explorer, dans votre environnement de ligne de commande, exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="0e600-162">To install the latest (prerelease) version of the iothub-explorer tool, run the following command in your command-line environment:</span></span>

```
npm install -g iothub-explorer@latest
```

<span data-ttu-id="0e600-163">Pour obtenir une aide supplémentaire sur toutes les commandes d’iothub-explorer et leurs paramètres, vous pouvez utiliser la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="0e600-163">You can use the following command to get additional help about all the iothub-explorer commands and their parameters:</span></span>

```bash
iothub-explorer help
```

### <a name="azure-portal"></a><span data-ttu-id="0e600-164">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="0e600-164">Azure portal</span></span>
<span data-ttu-id="0e600-165">Une expérience complète de l’interface de ligne de commande vous permet de créer et de gérer toutes vos ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="0e600-165">A full CLI experience helps you create and manage all your Azure resources.</span></span> <span data-ttu-id="0e600-166">Vous pouvez également être amené à utiliser le [portail Azure](../azure-portal-overview.md) pour configurer, gérer et déboguer vos ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="0e600-166">You might also want to use the [Azure portal](../azure-portal-overview.md) to help provision, manage, and debug your Azure resources.</span></span>

## <a name="azure-storage-issues"></a><span data-ttu-id="0e600-167">Problèmes liés au Stockage Azure</span><span class="sxs-lookup"><span data-stu-id="0e600-167">Azure storage issues</span></span>
<span data-ttu-id="0e600-168">[L’Explorateur de stockage Microsoft Azure (en version préliminaire)](http://storageexplorer.com) est une application autonome de Microsoft qui vous permet d’utiliser des données du Stockage Azure sur Windows, macOS et Linux.</span><span class="sxs-lookup"><span data-stu-id="0e600-168">[Microsoft Azure Storage Explorer (preview)](http://storageexplorer.com) is a standalone app from Microsoft that you can use to work with Azure Storage data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="0e600-169">Cet outil vous permet de vous connecter à votre table et d’en consulter les données.</span><span class="sxs-lookup"><span data-stu-id="0e600-169">By using this tool, you can connect to your table and see the data in it.</span></span> <span data-ttu-id="0e600-170">Vous pouvez l’utiliser cet outil pour résoudre des problèmes liés au Stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="0e600-170">You can use this tool to troubleshoot your Azure Storage issues.</span></span>
