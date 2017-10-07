---
title: "Connect Arduino (C) tooAzure IoT - dépanner | Documents Microsoft"
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
ms.openlocfilehash: ed793041ffa1887dbe73067f7c48d2417e982866
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting"></a><span data-ttu-id="65f03-104">Résolution de problèmes</span><span class="sxs-lookup"><span data-stu-id="65f03-104">Troubleshooting</span></span>
## <a name="hardware-issues"></a><span data-ttu-id="65f03-105">Problèmes matériels</span><span class="sxs-lookup"><span data-stu-id="65f03-105">Hardware issues</span></span>
<span data-ttu-id="65f03-106">Pour plus d’informations sur la résolution des problèmes courants sur votre carte mère Adafruit estompe M0 Wi-Fi Arduino, consultez hello [page officielle de dépannage](https://learn.adafruit.com/adafruit-feather-m0-wifi-atwinc1500?view=all#faq).</span><span class="sxs-lookup"><span data-stu-id="65f03-106">For information about solving common problems on your Adafruit Feather M0 WiFi Arduino board, see hello [official troubleshooting page](https://learn.adafruit.com/adafruit-feather-m0-wifi-atwinc1500?view=all#faq).</span></span>

## <a name="nodejs-package-issues"></a><span data-ttu-id="65f03-107">Problèmes de package Node.js</span><span class="sxs-lookup"><span data-stu-id="65f03-107">Node.js package issues</span></span>
### <a name="no-response-during-gulp-tasks"></a><span data-ttu-id="65f03-108">Aucune réponse lors des tâches gulp</span><span class="sxs-lookup"><span data-stu-id="65f03-108">No response during gulp tasks</span></span>
<span data-ttu-id="65f03-109">Si vous rencontrez des problèmes d’exécution des tâches de choses, vous pouvez ajouter hello `--verbose` option pour le débogage.</span><span class="sxs-lookup"><span data-stu-id="65f03-109">If you encounter problems running gulp tasks, you can add hello `--verbose` option for debugging.</span></span> <span data-ttu-id="65f03-110">Essayez tooterminate actuel gulp tâches à l’aide de `Ctrl + C`, puis en exécution hello suivant commande dans les messages de débogage de toosee fenêtre console.</span><span class="sxs-lookup"><span data-stu-id="65f03-110">Try tooterminate current gulp tasks by using `Ctrl + C`, and then run hello following command in your console window toosee debug messages.</span></span> <span data-ttu-id="65f03-111">Des messages d’erreur détaillés peuvent s’afficher dans la sortie de la console.</span><span class="sxs-lookup"><span data-stu-id="65f03-111">You might see detailed error messages in your console output.</span></span>

```bash
gulp --verbose
```

<span data-ttu-id="65f03-112">Vous pouvez aussi ajouter `--listen` informations du journal tooopen port série toooutput appareil.</span><span class="sxs-lookup"><span data-stu-id="65f03-112">Or you can add `--listen` tooopen serial port toooutput device log information.</span></span>

```bash
gulp --listen
``` 

### <a name="npm-issues"></a><span data-ttu-id="65f03-113">problèmes liés à NPM</span><span class="sxs-lookup"><span data-stu-id="65f03-113">NPM issues</span></span>
<span data-ttu-id="65f03-114">Essayez de votre package NPM tooupdate avec hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="65f03-114">Try tooupdate your NPM package with hello following command:</span></span>

```bash
npm install -g npm
```

<span data-ttu-id="65f03-115">Si le problème de hello existe toujours, laisser vos commentaires à la fin de hello de cet article ou créer un problème de GitHub dans notre [dépôt d’exemples][sample-repository].</span><span class="sxs-lookup"><span data-stu-id="65f03-115">If hello problem still exists, leave your comments at hello end of this article or create a GitHub issue in our [sample repository][sample-repository].</span></span>

## <a name="azure-cli-issues"></a><span data-ttu-id="65f03-116">Problèmes liés à l'interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="65f03-116">Azure-CLI issues</span></span>
<span data-ttu-id="65f03-117">Bonjour Azure interface de ligne de commande (CLI d’Azure) est une version préliminaire.</span><span class="sxs-lookup"><span data-stu-id="65f03-117">hello Azure command-line interface (Azure CLI) is a preview build.</span></span> <span data-ttu-id="65f03-118">Recherchez la solution Bonjour [Guide d’installation de version préliminaire](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md) tooseek solutions.</span><span class="sxs-lookup"><span data-stu-id="65f03-118">Look for solution in hello [Preview Install Guide](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md) tooseek solutions.</span></span> <span data-ttu-id="65f03-119">Essayez tooupgrade cli d’Azure toolatest version lorsque les commandes ne fonctionnent pas comme prévu.</span><span class="sxs-lookup"><span data-stu-id="65f03-119">Try tooupgrade Azure-cli toolatest version when commands don’t work as expected.</span></span>

<span data-ttu-id="65f03-120">Si vous rencontrez des bogues avec l’outil de hello, fichier un [problème](https://github.com/Azure/azure-cli/issues) Bonjour **problèmes** section du référentiel GitHub de hello.</span><span class="sxs-lookup"><span data-stu-id="65f03-120">If you encounter any bugs with hello tool, file an [issue](https://github.com/Azure/azure-cli/issues) in hello **Issues** section of hello GitHub repo.</span></span>

<span data-ttu-id="65f03-121">Pour résoudre les problèmes courants de l’aide, consultez hello [Lisez-moi](https://github.com/Azure/azure-cli/blob/master/README.rst).</span><span class="sxs-lookup"><span data-stu-id="65f03-121">For help troubleshooting common problems, check hello [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span></span>

<span data-ttu-id="65f03-122">Si vous répondez à « Impossible de trouver une version qui satisfait aux exigences de hello, » veuillez suivante d’exécution hello commande version de toolastest tooupgrade pip.</span><span class="sxs-lookup"><span data-stu-id="65f03-122">If you meet "Could not find a version that satisfies hello requirement", please run hello following command tooupgrade pip toolastest version.</span></span>

```bash
python -m pip install --upgrade pip
```

## <a name="python-installation-issues"></a><span data-ttu-id="65f03-123">Problèmes d’installation de Python</span><span class="sxs-lookup"><span data-stu-id="65f03-123">Python installation issues</span></span>
### <a name="legacy-installation-issues-macos"></a><span data-ttu-id="65f03-124">Problèmes d’installation héritée (macOS)</span><span class="sxs-lookup"><span data-stu-id="65f03-124">Legacy installation issues (macOS)</span></span>
<span data-ttu-id="65f03-125">Lors de l’installation de **pip**, une erreur d’autorisation est levée s’il existe des packages antérieurs qui sont installés avec des autorisations **su**.</span><span class="sxs-lookup"><span data-stu-id="65f03-125">When you're installing **pip**, a permission error is thrown when older packages that are installed with **su** permissions.</span></span> <span data-ttu-id="65f03-126">Cette situation se produit parce qu’une installation précédente de Python utilisant brew (macOS) n’est pas complètement désinstallée.</span><span class="sxs-lookup"><span data-stu-id="65f03-126">This situation occurs because a previous installation of Python using brew (macOS) is not uninstalled completely.</span></span> <span data-ttu-id="65f03-127">Certains **pip** packages à partir d’une installation précédente ont été créés à la racine, ce qui provoque l’erreur d’autorisation hello.</span><span class="sxs-lookup"><span data-stu-id="65f03-127">Some **pip** packages from a previous installation were created by root, which causes hello permission error.</span></span> <span data-ttu-id="65f03-128">solution de Hello est tooremove ces packages installés par la racine.</span><span class="sxs-lookup"><span data-stu-id="65f03-128">hello solution is tooremove those packages installed by root.</span></span> <span data-ttu-id="65f03-129">Utilisez hello suivant les étapes toocomplete cette tâche :</span><span class="sxs-lookup"><span data-stu-id="65f03-129">Use hello following steps toocomplete this task:</span></span>

1. <span data-ttu-id="65f03-130">Accédez à : /usr/local/lib/python2.7/site-packages</span><span class="sxs-lookup"><span data-stu-id="65f03-130">Go to: /usr/local/lib/python2.7/site-packages</span></span>
2. <span data-ttu-id="65f03-131">Affichez la liste des packages créés par root : `ls -l | grep root`.</span><span class="sxs-lookup"><span data-stu-id="65f03-131">List packages create by root: `ls -l | grep root`</span></span>
3. <span data-ttu-id="65f03-132">Désinstallez les packages identifiés à l’étape 2 : `sudo rm -rf {package name}`</span><span class="sxs-lookup"><span data-stu-id="65f03-132">Uninstall packages from step 2: `sudo rm -rf {package name}`</span></span>
4. <span data-ttu-id="65f03-133">Réinstallez Python.</span><span class="sxs-lookup"><span data-stu-id="65f03-133">Reinstall Python.</span></span>

## <a name="azure-iot-hub-issues"></a><span data-ttu-id="65f03-134">Problèmes liés à Azure IoT Hub</span><span class="sxs-lookup"><span data-stu-id="65f03-134">Azure IoT Hub issues</span></span>
<span data-ttu-id="65f03-135">Si vous avez déployé votre concentrateur Azure IoT avec `azure-cli`, et vous avez besoin d’un outil toomanage hello les appareils qui sont connectent tooyour IoT hub, hello try suivant outils :</span><span class="sxs-lookup"><span data-stu-id="65f03-135">If you've successfully provisioned your Azure IoT hub with `azure-cli`, and you need a tool toomanage hello devices that are connecting tooyour IoT hub, try hello following tools:</span></span>

### <a name="device-explorer"></a><span data-ttu-id="65f03-136">Explorateur d’appareils</span><span class="sxs-lookup"><span data-stu-id="65f03-136">Device Explorer</span></span>
<span data-ttu-id="65f03-137">[Explorateur de périphérique](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) s’exécute sur votre ordinateur local de Windows et se connecte tooyour IoT hub dans Azure.</span><span class="sxs-lookup"><span data-stu-id="65f03-137">[Device Explorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) runs on your Windows local machine and connects tooyour IoT hub in Azure.</span></span> <span data-ttu-id="65f03-138">Il communique avec les éléments suivants de hello [points de terminaison IoT Hub](iot-hub-devguide.md):</span><span class="sxs-lookup"><span data-stu-id="65f03-138">It communicates with hello following [IoT Hub endpoints](iot-hub-devguide.md):</span></span>

* <span data-ttu-id="65f03-139">*Gestion des identités* tooprovision et gérer les appareils inscrits avec votre IoT hub.</span><span class="sxs-lookup"><span data-stu-id="65f03-139">*Device identity management* tooprovision and manage devices registered with your IoT hub.</span></span>
* <span data-ttu-id="65f03-140">*Réception d’appareil-à-cloud* afin de surveiller les messages envoyés à partir de votre appareil tooyour IoT de supervision.</span><span class="sxs-lookup"><span data-stu-id="65f03-140">*Receive device-to-cloud* so you can monitor messages sent from your device tooyour IoT hub.</span></span>
* <span data-ttu-id="65f03-141">*Envoyer le cloud-à-appareil* afin de pouvoir envoyer des messages tooyour périphériques à partir de votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="65f03-141">*Send cloud-to-device* so you can send messages tooyour devices from your IoT hub.</span></span>

<span data-ttu-id="65f03-142">Configurer votre `IoT hub connection string` dans cette toouse outil toutes ses fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="65f03-142">Configure your `IoT hub connection string` within this tool toouse all its capabilities.</span></span>

### <a name="iot-hub-explorer"></a><span data-ttu-id="65f03-143">IoT Hub Explorer</span><span class="sxs-lookup"><span data-stu-id="65f03-143">IoT hub Explorer</span></span>
<span data-ttu-id="65f03-144">[IoT hub Explorer](https://github.com/Azure/iothub-explorer) est un exemple d’outil CLI multiplateforme toomanage appareils clients.</span><span class="sxs-lookup"><span data-stu-id="65f03-144">[IoT hub Explorer](https://github.com/Azure/iothub-explorer) is a sample multiplatform CLI tool toomanage device clients.</span></span> <span data-ttu-id="65f03-145">Vous pouvez utiliser des périphériques de hello hello outil toomanage dans le Registre des identités hello, surveiller les messages appareil-à-cloud et envoyer des commandes de cloud sur l’appareil.</span><span class="sxs-lookup"><span data-stu-id="65f03-145">You can use hello tool toomanage hello devices in hello identity registry, monitor device-to-cloud messages, and send cloud-to-device commands.</span></span>


<span data-ttu-id="65f03-146">tooinstall hello la dernière version (version préliminaire) de hello iothub-Explorateur, exécutez hello commande dans votre environnement de ligne de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="65f03-146">tooinstall hello latest (prerelease) version of hello iothub-explorer tool, run hello following command in your command-line environment:</span></span>

```bash
npm install -g iothub-explorer@latest
```

<span data-ttu-id="65f03-147">Vous pouvez utiliser hello tooget une aide supplémentaire sur l’ensemble hello iothub-Explorateur commandes et leurs paramètres de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="65f03-147">You can use hello following command tooget additional help about all hello iothub-explorer commands and their parameters:</span></span>

```bash
iothub-explorer help
```

### <a name="azure-portal"></a><span data-ttu-id="65f03-148">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="65f03-148">Azure portal</span></span>
<span data-ttu-id="65f03-149">Une expérience complète de l’interface de ligne de commande vous permet de créer et de gérer toutes vos ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="65f03-149">A full CLI experience helps you create and manage all your Azure resources.</span></span> <span data-ttu-id="65f03-150">Vous pouvez également vous toouse hello [portail Azure](../azure-portal-overview.md) toohelp configurer, gérer et déboguer vos ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="65f03-150">You might also want toouse hello [Azure portal](../azure-portal-overview.md) toohelp provision, manage, and debug your Azure resources.</span></span>

## <a name="azure-storage-issues"></a><span data-ttu-id="65f03-151">Problèmes liés au Stockage Azure</span><span class="sxs-lookup"><span data-stu-id="65f03-151">Azure storage issues</span></span>
<span data-ttu-id="65f03-152">[Explorateur de stockage Microsoft Azure (aperçu)](http://storageexplorer.com) est une application autonome de Microsoft que vous pouvez utiliser toowork avec des données de stockage Azure sur Windows, Mac OS et Linux.</span><span class="sxs-lookup"><span data-stu-id="65f03-152">[Microsoft Azure Storage Explorer (preview)](http://storageexplorer.com) is a standalone app from Microsoft that you can use toowork with Azure Storage data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="65f03-153">À l’aide de cet outil, vous pouvez connecter tooyour table et voir les données hello.</span><span class="sxs-lookup"><span data-stu-id="65f03-153">By using this tool, you can connect tooyour table and see hello data in it.</span></span> <span data-ttu-id="65f03-154">Vous pouvez utiliser cet outil tootroubleshoot vos problèmes de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="65f03-154">You can use this tool tootroubleshoot your Azure Storage issues.</span></span>

<!-- Images and links -->

[sample-repository]: https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md