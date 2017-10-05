---
title: "Connecter Arduino (C) à Azure IoT - Résolution des problèmes | Microsoft Docs"
description: "Page de résolution des problèmes pour l'expérience Adafruit Feather M0 WiFi Arduino"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "résolution des problèmes arduino"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: fdcc56ff-4420-463c-8a0e-5a1d215a874f
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 3bb369da9148300a80e7d351522a4d908e926996
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting"></a><span data-ttu-id="f3d59-104">Résolution de problèmes</span><span class="sxs-lookup"><span data-stu-id="f3d59-104">Troubleshooting</span></span>
## <a name="hardware-issues"></a><span data-ttu-id="f3d59-105">Problèmes matériels</span><span class="sxs-lookup"><span data-stu-id="f3d59-105">Hardware issues</span></span>
<span data-ttu-id="f3d59-106">Pour plus d’informations sur la résolution de problèmes courants sur votre carte Adafruit Feather M0 WiFi Arduino, consultez la [page officielle de résolution des problèmes](https://learn.adafruit.com/adafruit-feather-m0-wifi-atwinc1500?view=all#faq).</span><span class="sxs-lookup"><span data-stu-id="f3d59-106">For information about solving common problems on your Adafruit Feather M0 WiFi Arduino board, see the [official troubleshooting page](https://learn.adafruit.com/adafruit-feather-m0-wifi-atwinc1500?view=all#faq).</span></span>

## <a name="nodejs-package-issues"></a><span data-ttu-id="f3d59-107">Problèmes de package Node.js</span><span class="sxs-lookup"><span data-stu-id="f3d59-107">Node.js package issues</span></span>
### <a name="no-response-during-gulp-tasks"></a><span data-ttu-id="f3d59-108">Aucune réponse lors des tâches gulp</span><span class="sxs-lookup"><span data-stu-id="f3d59-108">No response during gulp tasks</span></span>
<span data-ttu-id="f3d59-109">Si vous rencontrez des problèmes d’exécution des tâches gulp, vous pouvez ajouter l’option `--verbose` pour le débogage.</span><span class="sxs-lookup"><span data-stu-id="f3d59-109">If you encounter problems running gulp tasks, you can add the `--verbose` option for debugging.</span></span> <span data-ttu-id="f3d59-110">Essayez d’arrêter les tâches gulp en cours en appuyant sur `Ctrl + C`, puis exécutez la commande suivante dans la fenêtre de la console pour afficher les messages de débogage.</span><span class="sxs-lookup"><span data-stu-id="f3d59-110">Try to terminate current gulp tasks by using `Ctrl + C`, and then run the following command in your console window to see debug messages.</span></span> <span data-ttu-id="f3d59-111">Des messages d’erreur détaillés peuvent s’afficher dans la sortie de la console.</span><span class="sxs-lookup"><span data-stu-id="f3d59-111">You might see detailed error messages in your console output.</span></span>

```bash
gulp --verbose
```

<span data-ttu-id="f3d59-112">Vous pouvez également ajouter `--listen` pour ouvrir le port série afin d'obtenir la sortie du journal de l'appareil.</span><span class="sxs-lookup"><span data-stu-id="f3d59-112">Or you can add `--listen` to open serial port to output device log information.</span></span>

```bash
gulp --listen
``` 

### <a name="npm-issues"></a><span data-ttu-id="f3d59-113">problèmes liés à NPM</span><span class="sxs-lookup"><span data-stu-id="f3d59-113">NPM issues</span></span>
<span data-ttu-id="f3d59-114">Essayez de mettre à jour votre package NPM avec la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="f3d59-114">Try to update your NPM package with the following command:</span></span>

```bash
npm install -g npm
```

<span data-ttu-id="f3d59-115">Si le problème persiste, entrez vos commentaires à la fin de cet article ou créez un problème GitHub dans notre [exemple de référentiel][sample-repository].</span><span class="sxs-lookup"><span data-stu-id="f3d59-115">If the problem still exists, leave your comments at the end of this article or create a GitHub issue in our [sample repository][sample-repository].</span></span>

## <a name="azure-cli-issues"></a><span data-ttu-id="f3d59-116">Problèmes liés à l'interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="f3d59-116">Azure-CLI issues</span></span>
<span data-ttu-id="f3d59-117">L’interface de ligne de commande Azure est une version d’évaluation.</span><span class="sxs-lookup"><span data-stu-id="f3d59-117">The Azure command-line interface (Azure CLI) is a preview build.</span></span> <span data-ttu-id="f3d59-118">Pour rechercher des solutions, voir le [Guide d’installation de la version d’évaluation](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md).</span><span class="sxs-lookup"><span data-stu-id="f3d59-118">Look for solution in the [Preview Install Guide](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md) to seek solutions.</span></span> <span data-ttu-id="f3d59-119">Essayez de mettre à niveau Azure-cli à la version la plus récente lorsque les commandes ne fonctionnent pas comme prévu.</span><span class="sxs-lookup"><span data-stu-id="f3d59-119">Try to upgrade Azure-cli to latest version when commands don’t work as expected.</span></span>

<span data-ttu-id="f3d59-120">Si vous rencontrez des bogues avec l’outil, documentez un [problème](https://github.com/Azure/azure-cli/issues) dans la section **Issues** du dépôt GitHub.</span><span class="sxs-lookup"><span data-stu-id="f3d59-120">If you encounter any bugs with the tool, file an [issue](https://github.com/Azure/azure-cli/issues) in the **Issues** section of the GitHub repo.</span></span>

<span data-ttu-id="f3d59-121">Pour obtenir de l’aide sur la résolution de problèmes courants, voir la rubrique [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span><span class="sxs-lookup"><span data-stu-id="f3d59-121">For help troubleshooting common problems, check the [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span></span>

<span data-ttu-id="f3d59-122">Si l’erreur « Impossible de trouver une version conforme à la configuration requise » s’affiche, exécutez la commande suivante pour mettre à niveau pip vers la dernière version.</span><span class="sxs-lookup"><span data-stu-id="f3d59-122">If you meet "Could not find a version that satisfies the requirement", please run the following command to upgrade pip to lastest version.</span></span>

```bash
python -m pip install --upgrade pip
```

## <a name="python-installation-issues"></a><span data-ttu-id="f3d59-123">Problèmes d’installation de Python</span><span class="sxs-lookup"><span data-stu-id="f3d59-123">Python installation issues</span></span>
### <a name="legacy-installation-issues-macos"></a><span data-ttu-id="f3d59-124">Problèmes d’installation héritée (macOS)</span><span class="sxs-lookup"><span data-stu-id="f3d59-124">Legacy installation issues (macOS)</span></span>
<span data-ttu-id="f3d59-125">Lors de l’installation de **pip**, une erreur d’autorisation est levée s’il existe des packages antérieurs qui sont installés avec des autorisations **su**.</span><span class="sxs-lookup"><span data-stu-id="f3d59-125">When you're installing **pip**, a permission error is thrown when older packages that are installed with **su** permissions.</span></span> <span data-ttu-id="f3d59-126">Cette situation se produit parce qu’une installation précédente de Python utilisant brew (macOS) n’est pas complètement désinstallée.</span><span class="sxs-lookup"><span data-stu-id="f3d59-126">This situation occurs because a previous installation of Python using brew (macOS) is not uninstalled completely.</span></span> <span data-ttu-id="f3d59-127">Certains packages **pip** d’une installation précédente ont été créés par root, ce qui génère l’erreur d’autorisation.</span><span class="sxs-lookup"><span data-stu-id="f3d59-127">Some **pip** packages from a previous installation were created by root, which causes the permission error.</span></span> <span data-ttu-id="f3d59-128">La solution consiste à supprimer les packages installés par root.</span><span class="sxs-lookup"><span data-stu-id="f3d59-128">The solution is to remove those packages installed by root.</span></span> <span data-ttu-id="f3d59-129">Pour effectuer cette tâche, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="f3d59-129">Use the following steps to complete this task:</span></span>

1. <span data-ttu-id="f3d59-130">Accédez à : /usr/local/lib/python2.7/site-packages</span><span class="sxs-lookup"><span data-stu-id="f3d59-130">Go to: /usr/local/lib/python2.7/site-packages</span></span>
2. <span data-ttu-id="f3d59-131">Affichez la liste des packages créés par root : `ls -l | grep root`.</span><span class="sxs-lookup"><span data-stu-id="f3d59-131">List packages create by root: `ls -l | grep root`</span></span>
3. <span data-ttu-id="f3d59-132">Désinstallez les packages identifiés à l’étape 2 : `sudo rm -rf {package name}`</span><span class="sxs-lookup"><span data-stu-id="f3d59-132">Uninstall packages from step 2: `sudo rm -rf {package name}`</span></span>
4. <span data-ttu-id="f3d59-133">Réinstallez Python.</span><span class="sxs-lookup"><span data-stu-id="f3d59-133">Reinstall Python.</span></span>

## <a name="azure-iot-hub-issues"></a><span data-ttu-id="f3d59-134">Problèmes liés à Azure IoT Hub</span><span class="sxs-lookup"><span data-stu-id="f3d59-134">Azure IoT Hub issues</span></span>
<span data-ttu-id="f3d59-135">Si vous avez correctement configuré votre Azure IoT Hub avec `azure-cli`, et avez besoin d’un outil pour gérer les appareils se connectant à votre IoT Hub, essayez les outils suivants :</span><span class="sxs-lookup"><span data-stu-id="f3d59-135">If you've successfully provisioned your Azure IoT hub with `azure-cli`, and you need a tool to manage the devices that are connecting to your IoT hub, try the following tools:</span></span>

### <a name="device-explorer"></a><span data-ttu-id="f3d59-136">Explorateur d’appareils</span><span class="sxs-lookup"><span data-stu-id="f3d59-136">Device Explorer</span></span>
<span data-ttu-id="f3d59-137">L’[Explorateur d’appareils](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) s’exécute sur votre ordinateur Windows local et se connecte à votre IoT Hub dans Azure.</span><span class="sxs-lookup"><span data-stu-id="f3d59-137">[Device Explorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) runs on your Windows local machine and connects to your IoT hub in Azure.</span></span> <span data-ttu-id="f3d59-138">Il communique avec les [points de terminaison IoT Hub](iot-hub-devguide.md) suivants :</span><span class="sxs-lookup"><span data-stu-id="f3d59-138">It communicates with the following [IoT Hub endpoints](iot-hub-devguide.md):</span></span>

* <span data-ttu-id="f3d59-139">*Device identity management* (Gestion d’identité d’appareil) pour configurer et gérer les appareils inscrits auprès de votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="f3d59-139">*Device identity management* to provision and manage devices registered with your IoT hub.</span></span>
* <span data-ttu-id="f3d59-140">*Receive device-to-cloud* (Réception appareil-à-cloud) pour pouvoir surveiller les messages envoyés par votre appareil à votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="f3d59-140">*Receive device-to-cloud* so you can monitor messages sent from your device to your IoT hub.</span></span>
* <span data-ttu-id="f3d59-141">*Send cloud-to-device* (Envoi cloud-à-appareil) pour pouvoir envoyer des messages à vos appareils à partir de votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="f3d59-141">*Send cloud-to-device* so you can send messages to your devices from your IoT hub.</span></span>

<span data-ttu-id="f3d59-142">Configurez votre `IoT hub connection string` dans cet outil pour utiliser toutes ses fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="f3d59-142">Configure your `IoT hub connection string` within this tool to use all its capabilities.</span></span>

### <a name="iot-hub-explorer"></a><span data-ttu-id="f3d59-143">IoT Hub Explorer</span><span class="sxs-lookup"><span data-stu-id="f3d59-143">IoT hub Explorer</span></span>
<span data-ttu-id="f3d59-144">[IoT Hub Explorer](https://github.com/Azure/iothub-explorer) est un exemple d’outil d’interface de ligne de commande multiplateforme destiné à la gestion d’appareils clients.</span><span class="sxs-lookup"><span data-stu-id="f3d59-144">[IoT hub Explorer](https://github.com/Azure/iothub-explorer) is a sample multiplatform CLI tool to manage device clients.</span></span> <span data-ttu-id="f3d59-145">Cet outil permet de gérer les appareils dans le registre des identités, de surveiller les messages appareil-à-cloud et d’envoyer des commandes cloud-à-appareil.</span><span class="sxs-lookup"><span data-stu-id="f3d59-145">You can use the tool to manage the devices in the identity registry, monitor device-to-cloud messages, and send cloud-to-device commands.</span></span>


<span data-ttu-id="f3d59-146">Pour installer la dernière version (préliminaire) de l’outil iothub-explorer, dans votre environnement de ligne de commande, exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="f3d59-146">To install the latest (prerelease) version of the iothub-explorer tool, run the following command in your command-line environment:</span></span>

```bash
npm install -g iothub-explorer@latest
```

<span data-ttu-id="f3d59-147">Pour obtenir une aide supplémentaire sur toutes les commandes d’iothub-explorer et leurs paramètres, vous pouvez utiliser la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="f3d59-147">You can use the following command to get additional help about all the iothub-explorer commands and their parameters:</span></span>

```bash
iothub-explorer help
```

### <a name="azure-portal"></a><span data-ttu-id="f3d59-148">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="f3d59-148">Azure portal</span></span>
<span data-ttu-id="f3d59-149">Une expérience complète de l’interface de ligne de commande vous permet de créer et de gérer toutes vos ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="f3d59-149">A full CLI experience helps you create and manage all your Azure resources.</span></span> <span data-ttu-id="f3d59-150">Vous pouvez également être amené à utiliser le [portail Azure](../azure-portal-overview.md) pour configurer, gérer et déboguer vos ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="f3d59-150">You might also want to use the [Azure portal](../azure-portal-overview.md) to help provision, manage, and debug your Azure resources.</span></span>

## <a name="azure-storage-issues"></a><span data-ttu-id="f3d59-151">Problèmes liés au Stockage Azure</span><span class="sxs-lookup"><span data-stu-id="f3d59-151">Azure storage issues</span></span>
<span data-ttu-id="f3d59-152">[L’Explorateur de stockage Microsoft Azure (en version préliminaire)](http://storageexplorer.com) est une application autonome de Microsoft qui vous permet d’utiliser des données du Stockage Azure sur Windows, macOS et Linux.</span><span class="sxs-lookup"><span data-stu-id="f3d59-152">[Microsoft Azure Storage Explorer (preview)](http://storageexplorer.com) is a standalone app from Microsoft that you can use to work with Azure Storage data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="f3d59-153">Cet outil vous permet de vous connecter à votre table et d’en consulter les données.</span><span class="sxs-lookup"><span data-stu-id="f3d59-153">By using this tool, you can connect to your table and see the data in it.</span></span> <span data-ttu-id="f3d59-154">Vous pouvez l’utiliser cet outil pour résoudre des problèmes liés au Stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="f3d59-154">You can use this tool to troubleshoot your Azure Storage issues.</span></span>

<!-- Images and links -->

[sample-repository]: https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md