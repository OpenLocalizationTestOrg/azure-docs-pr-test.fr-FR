---
title: "Connect Raspberry PI (C) tooAzure IoT - dépanner | Documents Microsoft"
description: "Résolution des problèmes de page pour une expérience hello framboises Pi Node.js"
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "problèmes iot, problèmes liés à l’internet des objets"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 22cf50dc-8206-42a2-a1fc-f75fa85135fa
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 8f0807104550e8e53a132f7741564b33f1db17ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting"></a><span data-ttu-id="d27f9-104">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="d27f9-104">Troubleshooting</span></span>
## <a name="hardware-issues"></a><span data-ttu-id="d27f9-105">Problèmes matériels</span><span class="sxs-lookup"><span data-stu-id="d27f9-105">Hardware issues</span></span>
### <a name="hello-application-runs-well-but-hello-led-is-not-blinking"></a><span data-ttu-id="d27f9-106">application Hello s’exécute correctement mais hello LED clignote pas</span><span class="sxs-lookup"><span data-stu-id="d27f9-106">hello application runs well but hello LED is not blinking</span></span>
<span data-ttu-id="d27f9-107">Ce problème est toujours une connectivité de circuits toohardware connexes.</span><span class="sxs-lookup"><span data-stu-id="d27f9-107">This issue is always related toohardware circuit connectivity.</span></span> <span data-ttu-id="d27f9-108">Utilisez hello étapes tooidentify problèmes suivants :</span><span class="sxs-lookup"><span data-stu-id="d27f9-108">Use hello following steps tooidentify problems:</span></span>

1. <span data-ttu-id="d27f9-109">Vérifiez que vous avez choisi hello correct **GPIO** sur votre carte mère.</span><span class="sxs-lookup"><span data-stu-id="d27f9-109">Check that you chose hello correct **GPIO** on your board.</span></span> <span data-ttu-id="d27f9-110">Hello deux ports doivent être **GPIO GND (code confidentiel 6)** et **GPIO 04 (code confidentiel 7)**.</span><span class="sxs-lookup"><span data-stu-id="d27f9-110">hello two ports should be **GPIO GND (Pin 6)** and **GPIO 04 (Pin 7)**.</span></span>
2. <span data-ttu-id="d27f9-111">Vérifiez que la polarité hello de votre DEL est correcte.</span><span class="sxs-lookup"><span data-stu-id="d27f9-111">Check that hello polarity of your LED is correct.</span></span> <span data-ttu-id="d27f9-112">branche de plus de temps Hello doit indiquer hello **positif**, code confidentiel d’anode.</span><span class="sxs-lookup"><span data-stu-id="d27f9-112">hello longer leg should indicate hello **positive**, anode pin.</span></span>
3. <span data-ttu-id="d27f9-113">Hello d’utilisation **3,3 v épingler** et **code confidentiel de terre** sur framboises Pi 3.</span><span class="sxs-lookup"><span data-stu-id="d27f9-113">Use hello **3.3V Pin** and **GND Pin** on Raspberry Pi 3.</span></span> <span data-ttu-id="d27f9-114">Traiter Pi comme hello alimentation électrique.</span><span class="sxs-lookup"><span data-stu-id="d27f9-114">Treat Pi as hello DC power.</span></span> <span data-ttu-id="d27f9-115">Vérifiez que hello DEL fonctionne correctement.</span><span class="sxs-lookup"><span data-stu-id="d27f9-115">Check that hello LED works fine.</span></span>

![Spécification de la LED](media/iot-hub-raspberry-pi-lessons/troubleshooting/led_spec.png)

### <a name="other-hardware-issues"></a><span data-ttu-id="d27f9-117">Autres problèmes matériels</span><span class="sxs-lookup"><span data-stu-id="d27f9-117">Other hardware issues</span></span>
<span data-ttu-id="d27f9-118">Pour plus d’informations sur la résolution des problèmes courants sur framboises Pi 3, consultez hello [page officielle de dépannage](http://elinux.org/R-Pi_Troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="d27f9-118">For information about solving common problems on Raspberry Pi 3, see hello [official troubleshooting page](http://elinux.org/R-Pi_Troubleshooting).</span></span>

## <a name="nodejs-package-issues"></a><span data-ttu-id="d27f9-119">Problèmes de package Node.js</span><span class="sxs-lookup"><span data-stu-id="d27f9-119">Node.js package issues</span></span>
### <a name="no-response-during-gulp-tasks"></a><span data-ttu-id="d27f9-120">Aucune réponse lors des tâches gulp</span><span class="sxs-lookup"><span data-stu-id="d27f9-120">No response during gulp tasks</span></span>
<span data-ttu-id="d27f9-121">Si vous rencontrez des problèmes dans gulp tâches en cours d’exécution, vous pouvez ajouter hello `--verbose` option pour le débogage.</span><span class="sxs-lookup"><span data-stu-id="d27f9-121">If you encounter problems in running gulp tasks, you can add hello `--verbose` option for debugging.</span></span> <span data-ttu-id="d27f9-122">Essayez de tooterminate actuel gulp tâches à l’aide de Ctrl + C et puis exécutez hello commande dans les messages de débogage de toosee fenêtre console suivante.</span><span class="sxs-lookup"><span data-stu-id="d27f9-122">Try tooterminate current gulp tasks by using Ctrl + C, and then run hello following command in your console window toosee debug messages.</span></span> <span data-ttu-id="d27f9-123">Des messages d’erreur détaillés peuvent s’afficher dans la sortie de la console.</span><span class="sxs-lookup"><span data-stu-id="d27f9-123">You might see detailed error messages in your console output.</span></span>

```bash
gulp --verbose
```

### <a name="device-discovery-issues"></a><span data-ttu-id="d27f9-124">Problèmes de détection d’appareil</span><span class="sxs-lookup"><span data-stu-id="d27f9-124">Device discovery issues</span></span>
<span data-ttu-id="d27f9-125">Pour vous aider à résoudre les problèmes courants avec hello `devdisco` de commande, vérifiez hello [Lisez-moi](https://github.com/Azure/device-discovery-cli/blob/develop/readme.md).</span><span class="sxs-lookup"><span data-stu-id="d27f9-125">For help in troubleshooting common problems with hello `devdisco` command, check hello [readme](https://github.com/Azure/device-discovery-cli/blob/develop/readme.md).</span></span>

### <a name="npm-issues"></a><span data-ttu-id="d27f9-126">problèmes liés à npm</span><span class="sxs-lookup"><span data-stu-id="d27f9-126">npm issues</span></span>
<span data-ttu-id="d27f9-127">Essayez de votre package npm tooupdate à l’aide de hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="d27f9-127">Try tooupdate your npm package by using hello following command:</span></span>

```bash
npm install -g npm
```

<span data-ttu-id="d27f9-128">Si le problème de hello existe toujours, laisser vos commentaires à la fin de hello de cet article ou créer un problème de GitHub dans notre [dépôt d’exemples](https://github.com/Azure-Samples/iot-hub-node-raspberrypi-getting-started).</span><span class="sxs-lookup"><span data-stu-id="d27f9-128">If hello problem still exists, leave your comments at hello end of this article or create a GitHub issue in our [sample repository](https://github.com/Azure-Samples/iot-hub-node-raspberrypi-getting-started).</span></span>

## <a name="remote-debugging"></a><span data-ttu-id="d27f9-129">Débogage à distance</span><span class="sxs-lookup"><span data-stu-id="d27f9-129">Remote debugging</span></span>
### <a name="run-hello-sample-application-in-debug-mode"></a><span data-ttu-id="d27f9-130">Exécuter l’exemple d’application hello en mode débogage</span><span class="sxs-lookup"><span data-stu-id="d27f9-130">Run hello sample application in debug mode</span></span>
```bash
gulp run --debug
```

<span data-ttu-id="d27f9-131">Lorsque le moteur de débogage hello est prêt, vous devez voir ```Debugger listening on port 5858``` dans la sortie de console hello.</span><span class="sxs-lookup"><span data-stu-id="d27f9-131">When hello debug engine is ready, you should see ```Debugger listening on port 5858``` in hello console output.</span></span>

### <a name="configure-visual-studio-code-tooconnect-toohello-remote-device"></a><span data-ttu-id="d27f9-132">Configurez le périphérique distant de Visual Studio Code tooconnect toohello</span><span class="sxs-lookup"><span data-stu-id="d27f9-132">Configure Visual Studio Code tooconnect toohello remote device</span></span>
1. <span data-ttu-id="d27f9-133">Ouvrez hello **déboguer** Panneau de configuration sur le côté gauche de hello.</span><span class="sxs-lookup"><span data-stu-id="d27f9-133">Open hello **Debug** panel on hello left side.</span></span>
2. <span data-ttu-id="d27f9-134">Cliquez sur hello verte **démarrer le débogage** bouton (F5).</span><span class="sxs-lookup"><span data-stu-id="d27f9-134">Click hello green **Start Debugging** (F5) button.</span></span> <span data-ttu-id="d27f9-135">Visual Studio Code ouvre un fichier launch.json.</span><span class="sxs-lookup"><span data-stu-id="d27f9-135">Visual Studio Code opens a launch.json file.</span></span>
3. <span data-ttu-id="d27f9-136">Mettre à jour les fichiers de launch.json hello avec hello suivant le contenu.</span><span class="sxs-lookup"><span data-stu-id="d27f9-136">Update hello launch.json file with hello following content.</span></span> <span data-ttu-id="d27f9-137">Remplacez `[device hostname or IP address]` avec hello périphérique réel IP adresse ou nom d’hôte.</span><span class="sxs-lookup"><span data-stu-id="d27f9-137">Replace `[device hostname or IP address]` with hello actual device IP address or host name.</span></span>

> [!NOTE]
> <span data-ttu-id="d27f9-138">toolearn en savoir plus sur hello débogage Visual Studio, consultez trop[débogage dans Visual Studio Code](https://code.visualstudio.com/Docs/editor/debugging#_launchjson-attributes).</span><span class="sxs-lookup"><span data-stu-id="d27f9-138">toolearn more about hello Visual Studio Debugging, please refer too[Debugging in Visual Studio Code](https://code.visualstudio.com/Docs/editor/debugging#_launchjson-attributes).</span></span>


```json
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Attach",
            "type": "node",
            "request": "attach",
            "port": 5858,
            "address": "[device hostname or IP address]",
            "restart": false,
            "sourceMaps": false,
            "outDir": null,
            "localRoot": "${workspaceRoot}",
            "remoteRoot": null
        }
    ]
}
```

![Configuration du débogage à distance](media/iot-hub-raspberry-pi-lessons/troubleshooting/remote_debugging_configuration.png)

### <a name="attach-toohello-remote-application"></a><span data-ttu-id="d27f9-140">Attacher toohello des applications à distance</span><span class="sxs-lookup"><span data-stu-id="d27f9-140">Attach toohello remote application</span></span>
<span data-ttu-id="d27f9-141">Cliquez sur hello verte **démarrer le débogage** toostart de débogage de bouton (F5).</span><span class="sxs-lookup"><span data-stu-id="d27f9-141">Click hello green **Start Debugging** (F5) button toostart debugging.</span></span>

<span data-ttu-id="d27f9-142">Lecture [JavaScript dans Visual Studio Code](https://code.visualstudio.com/docs/languages/javascript#_debugging) toolearn plus à propos du débogueur de hello.</span><span class="sxs-lookup"><span data-stu-id="d27f9-142">Read [JavaScript in VS Code](https://code.visualstudio.com/docs/languages/javascript#_debugging) toolearn more about hello debugger.</span></span>

![Débogage interactif à distance](media/iot-hub-raspberry-pi-lessons/troubleshooting/remote_debugging_interactive.png)

## <a name="azure-cli-issues"></a><span data-ttu-id="d27f9-144">Problèmes d’interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="d27f9-144">Azure CLI issues</span></span>
<span data-ttu-id="d27f9-145">Bonjour Azure interface de ligne de commande (CLI d’Azure) est une version préliminaire.</span><span class="sxs-lookup"><span data-stu-id="d27f9-145">hello Azure command-line interface (Azure CLI) is a preview build.</span></span> <span data-ttu-id="d27f9-146">les solutions tooseek, vous pouvez utiliser hello [Guide d’installation de version préliminaire](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md).</span><span class="sxs-lookup"><span data-stu-id="d27f9-146">tooseek solutions, you can use hello [Preview Install Guide](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md).</span></span>

<span data-ttu-id="d27f9-147">Si vous rencontrez des bogues avec l’outil de hello, fichier un [problème](https://github.com/Azure/azure-cli/issues) Bonjour **problèmes** section du référentiel GitHub de hello.</span><span class="sxs-lookup"><span data-stu-id="d27f9-147">If you encounter any bugs with hello tool, file an [issue](https://github.com/Azure/azure-cli/issues) in hello **Issues** section of hello GitHub repo.</span></span>

<span data-ttu-id="d27f9-148">Pour vous aider à résoudre les problèmes courants, consultez hello [Lisez-moi](https://github.com/Azure/azure-cli/blob/master/README.rst).</span><span class="sxs-lookup"><span data-stu-id="d27f9-148">For help in troubleshooting common problems, check hello [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span></span>

## <a name="python-installation-issues"></a><span data-ttu-id="d27f9-149">Problèmes d’installation de Python</span><span class="sxs-lookup"><span data-stu-id="d27f9-149">Python installation issues</span></span>
### <a name="legacy-installation-issues-macos"></a><span data-ttu-id="d27f9-150">Problèmes d’installation héritée (macOS)</span><span class="sxs-lookup"><span data-stu-id="d27f9-150">Legacy installation issues (macOS)</span></span>
<span data-ttu-id="d27f9-151">Lors de l’installation de pip, une erreur d’autorisation est levée s’il existe des packages antérieurs qui sont installés avec des autorisations **su**.</span><span class="sxs-lookup"><span data-stu-id="d27f9-151">When you're installing pip, a permission error is thrown when older packages are installed with **su** permissions.</span></span> <span data-ttu-id="d27f9-152">Cette situation se produit parce qu’une installation précédente de Python utilisant brew (macOS) n’est pas complètement désinstallée.</span><span class="sxs-lookup"><span data-stu-id="d27f9-152">This situation occurs because a previous installation of Python using brew (macOS) is not uninstalled completely.</span></span> <span data-ttu-id="d27f9-153">Certains packages pip d’une installation précédente ont été créées par la racine, ce qui provoque l’erreur d’autorisation hello.</span><span class="sxs-lookup"><span data-stu-id="d27f9-153">Some pip packages from a previous installation were created by root, which causes hello permission error.</span></span> <span data-ttu-id="d27f9-154">solution de Hello est tooremove ces packages installés par la racine.</span><span class="sxs-lookup"><span data-stu-id="d27f9-154">hello solution is tooremove those packages installed by root.</span></span> <span data-ttu-id="d27f9-155">Utilisez hello suivant les étapes toocomplete cette tâche :</span><span class="sxs-lookup"><span data-stu-id="d27f9-155">Use hello following steps toocomplete this task:</span></span>

1. <span data-ttu-id="d27f9-156">Accédez à : /usr/local/lib/python2.7/site-packages</span><span class="sxs-lookup"><span data-stu-id="d27f9-156">Go to: /usr/local/lib/python2.7/site-packages</span></span>
2. <span data-ttu-id="d27f9-157">Affichez la liste des packages créés par root : `ls -l | grep root`</span><span class="sxs-lookup"><span data-stu-id="d27f9-157">List packages created by root: `ls -l | grep root`</span></span>
3. <span data-ttu-id="d27f9-158">Désinstallez les packages identifiés à l’étape 2 : `sudo rm -rf {package name}`</span><span class="sxs-lookup"><span data-stu-id="d27f9-158">Uninstall packages from step 2: `sudo rm -rf {package name}`</span></span>
4. <span data-ttu-id="d27f9-159">Réinstallez Python.</span><span class="sxs-lookup"><span data-stu-id="d27f9-159">Reinstall Python.</span></span>

## <a name="azure-iot-hub-issues"></a><span data-ttu-id="d27f9-160">Problèmes liés à Azure IoT Hub</span><span class="sxs-lookup"><span data-stu-id="d27f9-160">Azure IoT Hub issues</span></span>
<span data-ttu-id="d27f9-161">Si vous avez déployé votre concentrateur Azure IoT avec CLI d’Azure et que vous avez besoin d’un outil toomanage hello les appareils qui sont connectent tooyour IoT hub, essayez de hello suite d’outils.</span><span class="sxs-lookup"><span data-stu-id="d27f9-161">If you've successfully provisioned your Azure IoT hub with Azure CLI, and you need a tool toomanage hello devices that are connecting tooyour IoT hub, try hello following tools.</span></span>

### <a name="device-explorer"></a><span data-ttu-id="d27f9-162">Explorateur d’appareils</span><span class="sxs-lookup"><span data-stu-id="d27f9-162">Device explorer</span></span>
<span data-ttu-id="d27f9-163">Hello [Explorateur de périphérique](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) s’exécute sur votre ordinateur local de Windows et se connecte tooyour IoT hub dans Azure.</span><span class="sxs-lookup"><span data-stu-id="d27f9-163">hello [Device explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) tool runs on your Windows local machine and connects tooyour IoT hub in Azure.</span></span> <span data-ttu-id="d27f9-164">Il communique avec les éléments suivants de hello [points de terminaison IoT Hub](iot-hub-devguide.md):</span><span class="sxs-lookup"><span data-stu-id="d27f9-164">It communicates with hello following [IoT Hub endpoints](iot-hub-devguide.md):</span></span>


* <span data-ttu-id="d27f9-165">*Gestion des identités* tooprovision et gérer les appareils inscrits avec votre IoT hub.</span><span class="sxs-lookup"><span data-stu-id="d27f9-165">*Device identity management* tooprovision and manage devices registered with your IoT hub.</span></span>
* <span data-ttu-id="d27f9-166">*Réception d’appareil-à-cloud* afin de surveiller les messages envoyés à partir de votre appareil tooyour IoT de supervision.</span><span class="sxs-lookup"><span data-stu-id="d27f9-166">*Receive device-to-cloud* so you can monitor messages sent from your device tooyour IoT hub.</span></span>
* <span data-ttu-id="d27f9-167">*Envoyer le cloud-à-appareil* afin de pouvoir envoyer des messages tooyour périphériques à partir de votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="d27f9-167">*Send cloud-to-device* so you can send messages tooyour devices from your IoT hub.</span></span>

<span data-ttu-id="d27f9-168">Configurer votre chaîne de connexion de hub IoT dans cette toouse outil toutes ses fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="d27f9-168">Configure your IoT hub connection string within this tool toouse all its capabilities.</span></span>

### <a name="iothub-explorer"></a><span data-ttu-id="d27f9-169">iothub-explorer</span><span class="sxs-lookup"><span data-stu-id="d27f9-169">iothub-explorer</span></span>
<span data-ttu-id="d27f9-170">[Explorateur d’iothub](https://github.com/Azure/iothub-explorer) est un exemple d’outil CLI multiplateforme toomanage pour les appareils.</span><span class="sxs-lookup"><span data-stu-id="d27f9-170">[iothub-explorer](https://github.com/Azure/iothub-explorer) is a sample multiplatform CLI tool toomanage devices.</span></span> <span data-ttu-id="d27f9-171">Vous pouvez utiliser des périphériques de hello hello outil toomanage dans le Registre des identités hello, surveiller les messages appareil-à-cloud et envoyer des messages cloud-à-appareil.</span><span class="sxs-lookup"><span data-stu-id="d27f9-171">You can use hello tool toomanage hello devices in hello identity registry, monitor device-to-cloud messages, and send cloud-to-device messages.</span></span>

<span data-ttu-id="d27f9-172">tooinstall hello la dernière version (version préliminaire) de hello iothub-Explorateur, exécutez hello commande dans votre environnement de ligne de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="d27f9-172">tooinstall hello latest (prerelease) version of hello iothub-explorer tool, run hello following command in your command-line environment:</span></span>

```bash
npm install -g iothub-explorer@latest
```

<span data-ttu-id="d27f9-173">Vous pouvez utiliser hello tooget une aide supplémentaire sur l’ensemble hello iothub-Explorateur commandes et leurs paramètres de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="d27f9-173">You can use hello following command tooget additional help about all hello iothub-explorer commands and their parameters:</span></span>

```bash
iothub-explorer help
```

### <a name="azure-portal"></a><span data-ttu-id="d27f9-174">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="d27f9-174">Azure portal</span></span>
<span data-ttu-id="d27f9-175">Une expérience complète de l’interface de ligne de commande vous permet de créer et de gérer toutes vos ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="d27f9-175">A full CLI experience helps you create and manage all your Azure resources.</span></span> <span data-ttu-id="d27f9-176">Vous pouvez également vous toouse hello [portail Azure](../azure-portal-overview.md) toohelp configurer, gérer et déboguer vos ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="d27f9-176">You might also want toouse hello [Azure portal](../azure-portal-overview.md) toohelp provision, manage, and debug your Azure resources.</span></span>

## <a name="azure-storage-issues"></a><span data-ttu-id="d27f9-177">Problèmes liés au Stockage Azure</span><span class="sxs-lookup"><span data-stu-id="d27f9-177">Azure Storage issues</span></span>
<span data-ttu-id="d27f9-178">[Explorateur de stockage Microsoft Azure (aperçu)](http://storageexplorer.com) est une application autonome de Microsoft que vous pouvez utiliser toowork avec des données de stockage Azure sur Windows, Mac OS et Linux.</span><span class="sxs-lookup"><span data-stu-id="d27f9-178">[Microsoft Azure Storage Explorer (preview)](http://storageexplorer.com) is a standalone app from Microsoft that you can use toowork with Azure Storage data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="d27f9-179">À l’aide de cet outil, vous pouvez connecter tooyour table et voir les données hello.</span><span class="sxs-lookup"><span data-stu-id="d27f9-179">By using this tool, you can connect tooyour table and see hello data in it.</span></span> <span data-ttu-id="d27f9-180">Vous pouvez utiliser cet outil tootroubleshoot vos problèmes de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="d27f9-180">You can use this tool tootroubleshoot your Azure Storage issues.</span></span>

