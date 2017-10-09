---
title: "Connect Raspberry PI (C) tooAzure IoT - dépanner | Documents Microsoft"
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
ms.openlocfilehash: 4f1ea81dd25d10a39c2939f5ee5f19f6d2ba2b2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting"></a><span data-ttu-id="ea090-104">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="ea090-104">Troubleshooting</span></span>
## <a name="hardware-issues"></a><span data-ttu-id="ea090-105">Problèmes matériels</span><span class="sxs-lookup"><span data-stu-id="ea090-105">Hardware issues</span></span>
### <a name="hello-application-runs-well-but-hello-led-is-not-blinking"></a><span data-ttu-id="ea090-106">application Hello s’exécute correctement mais hello LED clignote pas</span><span class="sxs-lookup"><span data-stu-id="ea090-106">hello application runs well but hello LED is not blinking</span></span>
<span data-ttu-id="ea090-107">Ce problème est toujours une connectivité de circuits matériel toohello connexes.</span><span class="sxs-lookup"><span data-stu-id="ea090-107">This issue is always related toohello hardware circuit connectivity.</span></span> <span data-ttu-id="ea090-108">Utilisez hello étapes tooidentify problèmes suivants.</span><span class="sxs-lookup"><span data-stu-id="ea090-108">Use hello following steps tooidentify problems.</span></span>

1. <span data-ttu-id="ea090-109">Vérifiez que vous avez choisi hello correct **GPIO** sur votre carte mère.</span><span class="sxs-lookup"><span data-stu-id="ea090-109">Check that you chose hello correct **GPIO** on your board.</span></span> <span data-ttu-id="ea090-110">Hello deux ports doivent être **GPIO GND (code confidentiel 6)** et **GPIO 04 (code confidentiel 7)**.</span><span class="sxs-lookup"><span data-stu-id="ea090-110">hello two ports should be **GPIO GND (Pin 6)** and **GPIO 04 (Pin 7)**.</span></span>
2. <span data-ttu-id="ea090-111">Vérifiez que la polarité hello de votre DEL est correcte.</span><span class="sxs-lookup"><span data-stu-id="ea090-111">Check that hello polarity of your LED is correct.</span></span> <span data-ttu-id="ea090-112">branche de plus de temps Hello doit indiquer hello **positif**, code confidentiel d’anode.</span><span class="sxs-lookup"><span data-stu-id="ea090-112">hello longer leg should indicate hello **positive**, anode pin.</span></span>
3. <span data-ttu-id="ea090-113">Hello d’utilisation **3,3 v épingler** et **code confidentiel de terre** sur framboises Pi 3.</span><span class="sxs-lookup"><span data-stu-id="ea090-113">Use hello **3.3V Pin** and **GND Pin** on Raspberry Pi 3.</span></span> <span data-ttu-id="ea090-114">Traiter Pi comme hello alimentation électrique.</span><span class="sxs-lookup"><span data-stu-id="ea090-114">Treat Pi as hello DC power.</span></span> <span data-ttu-id="ea090-115">Vérifiez que hello DEL fonctionne correctement.</span><span class="sxs-lookup"><span data-stu-id="ea090-115">Check that hello LED works fine.</span></span>

![Spécification de la LED](media/iot-hub-raspberry-pi-lessons/troubleshooting/led_spec.png)

### <a name="other-hardware-issues"></a><span data-ttu-id="ea090-117">Autres problèmes matériels</span><span class="sxs-lookup"><span data-stu-id="ea090-117">Other hardware issues</span></span>
<span data-ttu-id="ea090-118">Pour plus d’informations sur la résolution des problèmes courants sur framboises Pi 3, consultez hello [page officielle de dépannage](http://elinux.org/R-Pi_Troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="ea090-118">For information about solving common problems on Raspberry Pi 3, see hello [official troubleshooting page](http://elinux.org/R-Pi_Troubleshooting).</span></span>

## <a name="nodejs-package-issues"></a><span data-ttu-id="ea090-119">Problèmes de package Node.js</span><span class="sxs-lookup"><span data-stu-id="ea090-119">Node.js package issues</span></span>
### <a name="no-response-during-gulp-tasks"></a><span data-ttu-id="ea090-120">Aucune réponse lors des tâches gulp</span><span class="sxs-lookup"><span data-stu-id="ea090-120">No response during gulp tasks</span></span>
<span data-ttu-id="ea090-121">Si vous rencontrez des problèmes d’exécution des tâches de choses, vous pouvez ajouter hello `--verbose` option pour le débogage.</span><span class="sxs-lookup"><span data-stu-id="ea090-121">If you encounter problems running gulp tasks, you can add hello `--verbose` option for debugging.</span></span> <span data-ttu-id="ea090-122">Essayez tooterminate actuel gulp tâches à l’aide de `Ctrl + C`, puis en exécution hello suivant commande dans les messages de débogage de toosee fenêtre console.</span><span class="sxs-lookup"><span data-stu-id="ea090-122">Try tooterminate current gulp tasks by using `Ctrl + C`, and then run hello following command in your console window toosee debug messages.</span></span> <span data-ttu-id="ea090-123">Des messages d’erreur détaillés peuvent s’afficher dans la sortie de la console.</span><span class="sxs-lookup"><span data-stu-id="ea090-123">You might see detailed error messages in your console output.</span></span> 

```bash
gulp --verbose
```

### <a name="device-discovery-issues"></a><span data-ttu-id="ea090-124">Problèmes de détection d’appareil</span><span class="sxs-lookup"><span data-stu-id="ea090-124">Device discovery issues</span></span>
<span data-ttu-id="ea090-125">Pour vous aider à résoudre les problèmes courants avec hello `devdisco` de commande, vérifiez hello [Lisez-moi](https://github.com/Azure/device-discovery-cli/blob/develop/readme.md).</span><span class="sxs-lookup"><span data-stu-id="ea090-125">For help in troubleshooting common problems with hello `devdisco` command, check hello [readme](https://github.com/Azure/device-discovery-cli/blob/develop/readme.md).</span></span>

### <a name="npm-issues"></a><span data-ttu-id="ea090-126">problèmes liés à NPM</span><span class="sxs-lookup"><span data-stu-id="ea090-126">NPM issues</span></span>
<span data-ttu-id="ea090-127">Essayez de votre package NPM tooupdate avec hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="ea090-127">Try tooupdate your NPM package with hello following command:</span></span>

```bash
npm install -g npm
```

<span data-ttu-id="ea090-128">Si le problème de hello existe toujours, laisser vos commentaires à la fin de hello de cet article ou créer un problème de GitHub dans notre [dépôt d’exemples](https://github.com/Azure-Samples/iot-hub-c-raspberrypi-getting-started)</span><span class="sxs-lookup"><span data-stu-id="ea090-128">If hello problem still exists, leave your comments at hello end of this article or create a GitHub issue in our [sample repository](https://github.com/Azure-Samples/iot-hub-c-raspberrypi-getting-started)</span></span>

## <a name="remote-debugging"></a><span data-ttu-id="ea090-129">Débogage à distance</span><span class="sxs-lookup"><span data-stu-id="ea090-129">Remote debugging</span></span>

<span data-ttu-id="ea090-130">La prise en charge du débogage à distance sera disponible prochainement dans l’extension C/C++ de Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="ea090-130">Remote debugging support will be available soon in Visual Studio Code C/C++ Extension.</span></span>

<span data-ttu-id="ea090-131">En attendant, vous pouvez utiliser GDB via votre terminal SSH favori :</span><span class="sxs-lookup"><span data-stu-id="ea090-131">In a meanwhile you can use GDB via your favourite SSH terminal:</span></span>

```bash
cd c-pi-lesson-x
sudo gdb app
```

## <a name="azure-cli-issues"></a><span data-ttu-id="ea090-132">Problèmes liés à l'interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="ea090-132">Azure-CLI issues</span></span>
<span data-ttu-id="ea090-133">Bonjour Azure interface de ligne de commande (CLI d’Azure) est une version préliminaire.</span><span class="sxs-lookup"><span data-stu-id="ea090-133">hello Azure command-line interface (Azure CLI) is a preview build.</span></span> <span data-ttu-id="ea090-134">Recherchez la solution Bonjour [Guide d’installation de version préliminaire](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md) tooseek solutions.</span><span class="sxs-lookup"><span data-stu-id="ea090-134">Look for solution in hello [Preview Install Guide](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md) tooseek solutions.</span></span> <span data-ttu-id="ea090-135">Essayez tooupgrade cli d’Azure toolatest version lorsque les commandes ne fonctionnent pas comme prévu.</span><span class="sxs-lookup"><span data-stu-id="ea090-135">Try tooupgrade Azure-cli toolatest version when commands don’t work as expected.</span></span>

<span data-ttu-id="ea090-136">Si vous rencontrez des bogues avec l’outil de hello, fichier un [problème](https://github.com/Azure/azure-cli/issues) Bonjour **problèmes** section du référentiel GitHub de hello.</span><span class="sxs-lookup"><span data-stu-id="ea090-136">If you encounter any bugs with hello tool, file an [issue](https://github.com/Azure/azure-cli/issues) in hello **Issues** section of hello GitHub repo.</span></span>

<span data-ttu-id="ea090-137">Pour résoudre les problèmes courants de l’aide, consultez hello [Lisez-moi](https://github.com/Azure/azure-cli/blob/master/README.rst).</span><span class="sxs-lookup"><span data-stu-id="ea090-137">For help troubleshooting common problems, check hello [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span></span>

<span data-ttu-id="ea090-138">Si vous répondez à « Impossible de trouver une version qui satisfait aux exigences de hello, » veuillez suivante d’exécution hello commande version de toolastest tooupgrade pip.</span><span class="sxs-lookup"><span data-stu-id="ea090-138">If you meet "Could not find a version that satisfies hello requirement", please run hello following command tooupgrade pip toolastest version.</span></span>

```bash
python -m pip install --upgrade pip
```

## <a name="python-installation-issues"></a><span data-ttu-id="ea090-139">Problèmes d’installation de Python</span><span class="sxs-lookup"><span data-stu-id="ea090-139">Python installation issues</span></span>
### <a name="legacy-installation-issues-macos"></a><span data-ttu-id="ea090-140">Problèmes d’installation héritée (macOS)</span><span class="sxs-lookup"><span data-stu-id="ea090-140">Legacy installation issues (macOS)</span></span>
<span data-ttu-id="ea090-141">Lors de l’installation de **pip**, une erreur d’autorisation est levée s’il existe des packages antérieurs qui sont installés avec des autorisations **su**.</span><span class="sxs-lookup"><span data-stu-id="ea090-141">When you're installing **pip**, a permission error is thrown when older packages that are installed with **su** permissions.</span></span> <span data-ttu-id="ea090-142">Cette situation se produit parce qu’une installation précédente de Python utilisant brew (macOS) n’est pas complètement désinstallée.</span><span class="sxs-lookup"><span data-stu-id="ea090-142">This situation occurs because a previous installation of Python using brew (macOS) is not uninstalled completely.</span></span> <span data-ttu-id="ea090-143">Certains **pip** packages à partir d’une installation précédente ont été créés à la racine, ce qui provoque l’erreur d’autorisation hello.</span><span class="sxs-lookup"><span data-stu-id="ea090-143">Some **pip** packages from a previous installation were created by root, which causes hello permission error.</span></span> <span data-ttu-id="ea090-144">solution de Hello est tooremove ces packages installés par la racine.</span><span class="sxs-lookup"><span data-stu-id="ea090-144">hello solution is tooremove those packages installed by root.</span></span> <span data-ttu-id="ea090-145">Utilisez hello suivant les étapes toocomplete cette tâche :</span><span class="sxs-lookup"><span data-stu-id="ea090-145">Use hello following steps toocomplete this task:</span></span>

1. <span data-ttu-id="ea090-146">Accédez à : /usr/local/lib/python2.7/site-packages</span><span class="sxs-lookup"><span data-stu-id="ea090-146">Go to: /usr/local/lib/python2.7/site-packages</span></span>
2. <span data-ttu-id="ea090-147">Affichez la liste des packages créés par root : `ls -l | grep root`.</span><span class="sxs-lookup"><span data-stu-id="ea090-147">List packages create by root: `ls -l | grep root`</span></span>
3. <span data-ttu-id="ea090-148">Désinstallez les packages identifiés à l’étape 2 : `sudo rm -rf {package name}`</span><span class="sxs-lookup"><span data-stu-id="ea090-148">Uninstall packages from step 2: `sudo rm -rf {package name}`</span></span>
4. <span data-ttu-id="ea090-149">Réinstallez Python.</span><span class="sxs-lookup"><span data-stu-id="ea090-149">Reinstall Python.</span></span>

## <a name="azure-iot-hub-issues"></a><span data-ttu-id="ea090-150">Problèmes liés à Azure IoT Hub</span><span class="sxs-lookup"><span data-stu-id="ea090-150">Azure IoT Hub issues</span></span>
<span data-ttu-id="ea090-151">Si vous avez déployé votre concentrateur Azure IoT avec `azure-cli`, et vous avez besoin d’un outil toomanage hello les appareils qui sont connectent tooyour IoT hub, hello try suivant outils :</span><span class="sxs-lookup"><span data-stu-id="ea090-151">If you've successfully provisioned your Azure IoT hub with `azure-cli`, and you need a tool toomanage hello devices that are connecting tooyour IoT hub, try hello following tools:</span></span>

### <a name="device-explorer"></a><span data-ttu-id="ea090-152">Explorateur d’appareils</span><span class="sxs-lookup"><span data-stu-id="ea090-152">Device Explorer</span></span>
<span data-ttu-id="ea090-153">[Explorateur de périphérique](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) s’exécute sur votre ordinateur local de Windows et se connecte tooyour IoT hub dans Azure.</span><span class="sxs-lookup"><span data-stu-id="ea090-153">[Device Explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) runs on your Windows local machine and connects tooyour IoT hub in Azure.</span></span> <span data-ttu-id="ea090-154">Il communique avec les éléments suivants de hello [points de terminaison IoT Hub](iot-hub-devguide.md):</span><span class="sxs-lookup"><span data-stu-id="ea090-154">It communicates with hello following [IoT Hub endpoints](iot-hub-devguide.md):</span></span>

* <span data-ttu-id="ea090-155">*Gestion des identités* tooprovision et gérer les appareils inscrits avec votre IoT hub.</span><span class="sxs-lookup"><span data-stu-id="ea090-155">*Device identity management* tooprovision and manage devices registered with your IoT hub.</span></span>
* <span data-ttu-id="ea090-156">*Réception d’appareil-à-cloud* afin de surveiller les messages envoyés à partir de votre appareil tooyour IoT de supervision.</span><span class="sxs-lookup"><span data-stu-id="ea090-156">*Receive device-to-cloud* so you can monitor messages sent from your device tooyour IoT hub.</span></span>
* <span data-ttu-id="ea090-157">*Envoyer le cloud-à-appareil* afin de pouvoir envoyer des messages tooyour périphériques à partir de votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="ea090-157">*Send cloud-to-device* so you can send messages tooyour devices from your IoT hub.</span></span>

<span data-ttu-id="ea090-158">Configurer votre `IoT hub connection string` dans cette toouse outil toutes ses fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="ea090-158">Configure your `IoT hub connection string` within this tool toouse all its capabilities.</span></span>

### <a name="iot-hub-explorer"></a><span data-ttu-id="ea090-159">IoT Hub Explorer</span><span class="sxs-lookup"><span data-stu-id="ea090-159">IoT hub Explorer</span></span>
<span data-ttu-id="ea090-160">[IoT hub Explorer](https://github.com/Azure/iothub-explorer) est un exemple d’outil CLI multiplateforme toomanage appareils clients.</span><span class="sxs-lookup"><span data-stu-id="ea090-160">[IoT hub Explorer](https://github.com/Azure/iothub-explorer) is a sample multiplatform CLI tool toomanage device clients.</span></span> <span data-ttu-id="ea090-161">Vous pouvez utiliser des périphériques de hello hello outil toomanage dans le Registre des identités hello, surveiller les messages appareil-à-cloud et envoyer des commandes de cloud sur l’appareil.</span><span class="sxs-lookup"><span data-stu-id="ea090-161">You can use hello tool toomanage hello devices in hello identity registry, monitor device-to-cloud messages, and send cloud-to-device commands.</span></span>

<span data-ttu-id="ea090-162">tooinstall hello la dernière version (version préliminaire) de hello iothub-Explorateur, exécutez hello commande dans votre environnement de ligne de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="ea090-162">tooinstall hello latest (prerelease) version of hello iothub-explorer tool, run hello following command in your command-line environment:</span></span>

```
npm install -g iothub-explorer@latest
```

<span data-ttu-id="ea090-163">Vous pouvez utiliser hello tooget une aide supplémentaire sur l’ensemble hello iothub-Explorateur commandes et leurs paramètres de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="ea090-163">You can use hello following command tooget additional help about all hello iothub-explorer commands and their parameters:</span></span>

```bash
iothub-explorer help
```

### <a name="azure-portal"></a><span data-ttu-id="ea090-164">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="ea090-164">Azure portal</span></span>
<span data-ttu-id="ea090-165">Une expérience complète de l’interface de ligne de commande vous permet de créer et de gérer toutes vos ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="ea090-165">A full CLI experience helps you create and manage all your Azure resources.</span></span> <span data-ttu-id="ea090-166">Vous pouvez également vous toouse hello [portail Azure](../azure-portal-overview.md) toohelp configurer, gérer et déboguer vos ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="ea090-166">You might also want toouse hello [Azure portal](../azure-portal-overview.md) toohelp provision, manage, and debug your Azure resources.</span></span>

## <a name="azure-storage-issues"></a><span data-ttu-id="ea090-167">Problèmes liés au Stockage Azure</span><span class="sxs-lookup"><span data-stu-id="ea090-167">Azure storage issues</span></span>
<span data-ttu-id="ea090-168">[Explorateur de stockage Microsoft Azure (aperçu)](http://storageexplorer.com) est une application autonome de Microsoft que vous pouvez utiliser toowork avec des données de stockage Azure sur Windows, Mac OS et Linux.</span><span class="sxs-lookup"><span data-stu-id="ea090-168">[Microsoft Azure Storage Explorer (preview)](http://storageexplorer.com) is a standalone app from Microsoft that you can use toowork with Azure Storage data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="ea090-169">À l’aide de cet outil, vous pouvez connecter tooyour table et voir les données hello.</span><span class="sxs-lookup"><span data-stu-id="ea090-169">By using this tool, you can connect tooyour table and see hello data in it.</span></span> <span data-ttu-id="ea090-170">Vous pouvez utiliser cet outil tootroubleshoot vos problèmes de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="ea090-170">You can use this tool tootroubleshoot your Azure Storage issues.</span></span>
