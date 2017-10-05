---
title: "Connecter Intel Edison (C) à Azure IoT - Résolution des problèmes | Microsoft Docs"
description: "Page Dépannage pour l’expérience C Intel Edison"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "résolution des problèmes arduino"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: fe20f2fe-490c-4910-82e1-578ed504ae86
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: dd6338ad29e0bb858c33e5bb24b8f41d3c22575a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting"></a><span data-ttu-id="cf772-104">Résolution de problèmes</span><span class="sxs-lookup"><span data-stu-id="cf772-104">Troubleshooting</span></span>
## <a name="hardware-issues"></a><span data-ttu-id="cf772-105">Problèmes matériels</span><span class="sxs-lookup"><span data-stu-id="cf772-105">Hardware issues</span></span>
<span data-ttu-id="cf772-106">Pour plus d’informations sur la résolution de problèmes courants sur Intel Edison, consultez la [page de dépannage officielle](https://software.intel.com/en-us/node/637974).</span><span class="sxs-lookup"><span data-stu-id="cf772-106">For information about solving common problems on Intel Edison, see the [official troubleshooting page](https://software.intel.com/en-us/node/637974).</span></span>

## <a name="nodejs-package-issues"></a><span data-ttu-id="cf772-107">Problèmes de package Node.js</span><span class="sxs-lookup"><span data-stu-id="cf772-107">Node.js package issues</span></span>
### <a name="no-response-during-gulp-tasks"></a><span data-ttu-id="cf772-108">Aucune réponse lors des tâches gulp</span><span class="sxs-lookup"><span data-stu-id="cf772-108">No response during gulp tasks</span></span>
<span data-ttu-id="cf772-109">Si vous rencontrez des problèmes d’exécution des tâches gulp, vous pouvez ajouter l’option `--verbose` pour le débogage.</span><span class="sxs-lookup"><span data-stu-id="cf772-109">If you encounter problems running gulp tasks, you can add the `--verbose` option for debugging.</span></span> <span data-ttu-id="cf772-110">Essayez d’arrêter les tâches gulp en cours en appuyant sur `Ctrl + C`, puis exécutez la commande suivante dans la fenêtre de la console pour afficher les messages de débogage.</span><span class="sxs-lookup"><span data-stu-id="cf772-110">Try to terminate current gulp tasks by using `Ctrl + C`, and then run the following command in your console window to see debug messages.</span></span> <span data-ttu-id="cf772-111">Des messages d’erreur détaillés peuvent s’afficher dans la sortie de la console.</span><span class="sxs-lookup"><span data-stu-id="cf772-111">You might see detailed error messages in your console output.</span></span> 

```bash
gulp --verbose
```

### <a name="npm-issues"></a><span data-ttu-id="cf772-112">Problèmes liés à NPM</span><span class="sxs-lookup"><span data-stu-id="cf772-112">NPM issues</span></span>
<span data-ttu-id="cf772-113">Essayez de mettre à jour votre package NPM avec la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="cf772-113">Try to update your NPM package with the following command:</span></span>

```bash
npm install -g npm
```

<span data-ttu-id="cf772-114">Si le problème persiste, entrez vos commentaires à la fin de cet article ou créez un problème GitHub dans notre [exemple de référentiel][sample-repository].</span><span class="sxs-lookup"><span data-stu-id="cf772-114">If the problem still exists, leave your comments at the end of this article or create a GitHub issue in our [sample repository][sample-repository].</span></span>

## <a name="azure-cli-issues"></a><span data-ttu-id="cf772-115">Problèmes liés à l'interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="cf772-115">Azure-CLI issues</span></span>
<span data-ttu-id="cf772-116">L’interface de ligne de commande Azure est une version d’évaluation.</span><span class="sxs-lookup"><span data-stu-id="cf772-116">The Azure command-line interface (Azure CLI) is a preview build.</span></span> <span data-ttu-id="cf772-117">Pour rechercher des solutions, voir le [Guide d’installation de la version d’évaluation](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md).</span><span class="sxs-lookup"><span data-stu-id="cf772-117">Look for solution in the [Preview Install Guide](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md) to seek solutions.</span></span> <span data-ttu-id="cf772-118">Essayez de mettre à niveau Azure-cli à la version la plus récente lorsque les commandes ne fonctionnent pas comme prévu.</span><span class="sxs-lookup"><span data-stu-id="cf772-118">Try to upgrade Azure-cli to latest version when commands don’t work as expected.</span></span>

<span data-ttu-id="cf772-119">Si vous rencontrez des bogues avec l’outil, documentez un [problème](https://github.com/Azure/azure-cli/issues) dans la section **Issues** du dépôt GitHub.</span><span class="sxs-lookup"><span data-stu-id="cf772-119">If you encounter any bugs with the tool, file an [issue](https://github.com/Azure/azure-cli/issues) in the **Issues** section of the GitHub repo.</span></span>

<span data-ttu-id="cf772-120">Pour obtenir de l’aide sur la résolution de problèmes courants, voir la rubrique [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span><span class="sxs-lookup"><span data-stu-id="cf772-120">For help troubleshooting common problems, check the [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span></span>

<span data-ttu-id="cf772-121">Si l’erreur « Impossible de trouver une version conforme à la configuration requise » s’affiche, exécutez la commande suivante pour mettre à niveau pip vers la dernière version.</span><span class="sxs-lookup"><span data-stu-id="cf772-121">If you meet "Could not find a version that satisfies the requirement", please run the following command to upgrade pip to lastest version.</span></span>

```bash
python -m pip install --upgrade pip
```

## <a name="python-installation-issues"></a><span data-ttu-id="cf772-122">Problèmes d’installation de Python</span><span class="sxs-lookup"><span data-stu-id="cf772-122">Python installation issues</span></span>
### <a name="legacy-installation-issues-macos"></a><span data-ttu-id="cf772-123">Problèmes d’installation héritée (macOS)</span><span class="sxs-lookup"><span data-stu-id="cf772-123">Legacy installation issues (macOS)</span></span>
<span data-ttu-id="cf772-124">Lors de l’installation de **pip**, une erreur d’autorisation est levée s’il existe des packages antérieurs qui sont installés avec des autorisations **su**.</span><span class="sxs-lookup"><span data-stu-id="cf772-124">When you're installing **pip**, a permission error is thrown when older packages that are installed with **su** permissions.</span></span> <span data-ttu-id="cf772-125">Cette situation se produit parce qu’une installation précédente de Python utilisant brew (macOS) n’est pas complètement désinstallée.</span><span class="sxs-lookup"><span data-stu-id="cf772-125">This situation occurs because a previous installation of Python using brew (macOS) is not uninstalled completely.</span></span> <span data-ttu-id="cf772-126">Certains packages **pip** d’une installation précédente ont été créés par root, ce qui génère l’erreur d’autorisation.</span><span class="sxs-lookup"><span data-stu-id="cf772-126">Some **pip** packages from a previous installation were created by root, which causes the permission error.</span></span> <span data-ttu-id="cf772-127">La solution consiste à supprimer les packages installés par root.</span><span class="sxs-lookup"><span data-stu-id="cf772-127">The solution is to remove those packages installed by root.</span></span> <span data-ttu-id="cf772-128">Pour effectuer cette tâche, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="cf772-128">Use the following steps to complete this task:</span></span>

1. <span data-ttu-id="cf772-129">Accédez à : /usr/local/lib/python2.7/site-packages</span><span class="sxs-lookup"><span data-stu-id="cf772-129">Go to: /usr/local/lib/python2.7/site-packages</span></span>
2. <span data-ttu-id="cf772-130">Affichez la liste des packages créés par root : `ls -l | grep root`.</span><span class="sxs-lookup"><span data-stu-id="cf772-130">List packages create by root: `ls -l | grep root`</span></span>
3. <span data-ttu-id="cf772-131">Désinstallez les packages identifiés à l’étape 2 : `sudo rm -rf {package name}`</span><span class="sxs-lookup"><span data-stu-id="cf772-131">Uninstall packages from step 2: `sudo rm -rf {package name}`</span></span>
4. <span data-ttu-id="cf772-132">Réinstallez Python.</span><span class="sxs-lookup"><span data-stu-id="cf772-132">Reinstall Python.</span></span>

## <a name="azure-iot-hub-issues"></a><span data-ttu-id="cf772-133">Problèmes liés à Azure IoT Hub</span><span class="sxs-lookup"><span data-stu-id="cf772-133">Azure IoT Hub issues</span></span>
<span data-ttu-id="cf772-134">Si vous avez correctement configuré votre Azure IoT Hub avec `azure-cli`, et avez besoin d’un outil pour gérer les appareils se connectant à votre IoT Hub, essayez les outils suivants :</span><span class="sxs-lookup"><span data-stu-id="cf772-134">If you've successfully provisioned your Azure IoT hub with `azure-cli`, and you need a tool to manage the devices that are connecting to your IoT hub, try the following tools:</span></span>

### <a name="device-explorer"></a><span data-ttu-id="cf772-135">Explorateur d’appareils</span><span class="sxs-lookup"><span data-stu-id="cf772-135">Device Explorer</span></span>
<span data-ttu-id="cf772-136">L’[Explorateur d’appareils](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) s’exécute sur votre ordinateur Windows local et se connecte à votre IoT Hub dans Azure.</span><span class="sxs-lookup"><span data-stu-id="cf772-136">[Device Explorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) runs on your Windows local machine and connects to your IoT hub in Azure.</span></span> <span data-ttu-id="cf772-137">Il communique avec les [points de terminaison IoT Hub](iot-hub-devguide.md) suivants :</span><span class="sxs-lookup"><span data-stu-id="cf772-137">It communicates with the following [IoT Hub endpoints](iot-hub-devguide.md):</span></span>

- <span data-ttu-id="cf772-138">_Device identity management_ (Gestion d’identité d’appareil) pour configurer et gérer les appareils inscrits auprès de votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="cf772-138">_Device identity management_ to provision and manage devices registered with your IoT hub.</span></span>
- <span data-ttu-id="cf772-139">_Receive device-to-cloud_ (Réception appareil-à-cloud) pour pouvoir surveiller les messages envoyés par votre appareil à votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="cf772-139">_Receive device-to-cloud_ so you can monitor messages sent from your device to your IoT hub.</span></span>
- <span data-ttu-id="cf772-140">_Send cloud-to-device_ (Envoi cloud-à-appareil) pour pouvoir envoyer des messages à vos appareils à partir de votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="cf772-140">_Send cloud-to-device_ so you can send messages to your devices from your IoT hub.</span></span>

<span data-ttu-id="cf772-141">Configurez votre `IoT hub connection string` dans cet outil pour utiliser toutes ses fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="cf772-141">Configure your `IoT hub connection string` within this tool to use all its capabilities.</span></span>

### <a name="iot-hub-explorer"></a><span data-ttu-id="cf772-142">IoT Hub Explorer</span><span class="sxs-lookup"><span data-stu-id="cf772-142">IoT hub Explorer</span></span>
<span data-ttu-id="cf772-143">[IoT Hub Explorer](https://github.com/Azure/iothub-explorer) est un exemple d’outil d’interface de ligne de commande multiplateforme destiné à la gestion d’appareils clients.</span><span class="sxs-lookup"><span data-stu-id="cf772-143">[IoT hub Explorer](https://github.com/Azure/iothub-explorer) is a sample multiplatform CLI tool to manage device clients.</span></span> <span data-ttu-id="cf772-144">Cet outil permet de gérer les appareils dans le registre des identités, de surveiller les messages appareil-à-cloud et d’envoyer des commandes cloud-à-appareil.</span><span class="sxs-lookup"><span data-stu-id="cf772-144">You can use the tool to manage the devices in the identity registry, monitor device-to-cloud messages, and send cloud-to-device commands.</span></span>

<span data-ttu-id="cf772-145">Pour installer la dernière version (préliminaire) de l’outil iothub-explorer, dans votre environnement de ligne de commande, exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="cf772-145">To install the latest (prerelease) version of the iothub-explorer tool, run the following command in your command-line environment:</span></span>

```bash
npm install -g iothub-explorer@latest
```

<span data-ttu-id="cf772-146">Pour obtenir une aide supplémentaire sur toutes les commandes d’iothub-explorer et leurs paramètres, vous pouvez utiliser la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="cf772-146">You can use the following command to get additional help about all the iothub-explorer commands and their parameters:</span></span>

```bash
iothub-explorer help
```

### <a name="azure-portal"></a><span data-ttu-id="cf772-147">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="cf772-147">Azure portal</span></span>
<span data-ttu-id="cf772-148">Une expérience complète de l’interface de ligne de commande vous permet de créer et de gérer toutes vos ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="cf772-148">A full CLI experience helps you create and manage all your Azure resources.</span></span> <span data-ttu-id="cf772-149">Vous pouvez également être amené à utiliser le [portail Azure](../azure-portal-overview.md) pour configurer, gérer et déboguer vos ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="cf772-149">You might also want to use the [Azure portal](../azure-portal-overview.md) to help provision, manage, and debug your Azure resources.</span></span>

## <a name="azure-storage-issues"></a><span data-ttu-id="cf772-150">Problèmes liés au stockage Azure</span><span class="sxs-lookup"><span data-stu-id="cf772-150">Azure storage issues</span></span>
<span data-ttu-id="cf772-151">[L’Explorateur de stockage Microsoft Azure (en version préliminaire)](http://storageexplorer.com) est une application autonome de Microsoft qui vous permet d’utiliser des données du [Stockage Azure](https://azure.microsoft.com/en-us/services/storage/) sur Windows, macOS et Linux.</span><span class="sxs-lookup"><span data-stu-id="cf772-151">[Microsoft Azure Storage Explorer (preview)](http://storageexplorer.com) is a standalone app from Microsoft that you can use to work with [Azure Storage](https://azure.microsoft.com/en-us/services/storage/) data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="cf772-152">Cet outil vous permet de vous connecter à votre table et d’en consulter les données.</span><span class="sxs-lookup"><span data-stu-id="cf772-152">By using this tool, you can connect to your table and see the data in it.</span></span> <span data-ttu-id="cf772-153">Vous pouvez l’utiliser cet outil pour résoudre des problèmes liés au Stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="cf772-153">You can use this tool to troubleshoot your Azure Storage issues.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cf772-154">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="cf772-154">Next steps</span></span>
<span data-ttu-id="cf772-155">Cette page inclut uniquement les problèmes les plus courants du kit Intel Edison.</span><span class="sxs-lookup"><span data-stu-id="cf772-155">This page only includes the most common problems of Intel Edison kit.</span></span> <span data-ttu-id="cf772-156">Vous pouvez également laisser des commentaires en bas pour signaler des problèmes nécessitant un dépannage.</span><span class="sxs-lookup"><span data-stu-id="cf772-156">You can also leave bottom comments to report issues for further troubleshooting.</span></span>

<span data-ttu-id="cf772-157">Revenez à [Prise en main d’Intel Edison (C)](iot-hub-intel-edison-kit-c-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="cf772-157">Go back to [Get started with Intel Edison (C)](iot-hub-intel-edison-kit-c-get-started.md)</span></span>

<!-- Images and links -->

[sample-repository]: https://github.com/Azure-Samples/iot-hub-c-edison-getting-started