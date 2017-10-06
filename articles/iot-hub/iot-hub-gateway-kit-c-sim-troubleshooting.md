---
title: "Appareil simulé et passerelle Azure IoT - Résolution de problèmes | Microsoft Docs"
description: "Page de résolution des problèmes pour la passerelle Intel NUC"
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "problèmes iot, problèmes liés à l’internet des objets"
ROBOTS: NOINDEX
ms.assetid: 3ee8f4b0-5799-40a3-8cf0-8d5aa44dbc2b
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: cc7add6273e66aadeca9a4915a44f5edf61a0a59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting"></a><span data-ttu-id="355dd-104">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="355dd-104">Troubleshooting</span></span>

## <a name="hardware-issues"></a><span data-ttu-id="355dd-105">Problèmes matériels</span><span class="sxs-lookup"><span data-stu-id="355dd-105">Hardware issues</span></span>

### <a name="ti-sensortag-cannot-be-connected"></a><span data-ttu-id="355dd-106">TI SensorTag ne peut pas être connecté</span><span class="sxs-lookup"><span data-stu-id="355dd-106">TI SensorTag cannot be connected</span></span>

<span data-ttu-id="355dd-107">des problèmes de connectivité tootroubleshoot SensorTag utiliser hello [SensorTag application](http://processors.wiki.ti.com/index.php/SensorTag_User_Guide#SensorTag_App_user_guide).</span><span class="sxs-lookup"><span data-stu-id="355dd-107">tootroubleshoot SensorTag connectivity issues, use hello [SensorTag app](http://processors.wiki.ti.com/index.php/SensorTag_User_Guide#SensorTag_App_user_guide).</span></span>

### <a name="have-an-issue-with-intel-nuc"></a><span data-ttu-id="355dd-108">Problème avec Intel NUC</span><span class="sxs-lookup"><span data-stu-id="355dd-108">Have an issue with Intel NUC</span></span>

<span data-ttu-id="355dd-109">tootroubleshoot démarrage, consultez trop[résolution des problèmes de démarrage non sur Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/000005845.html).</span><span class="sxs-lookup"><span data-stu-id="355dd-109">tootroubleshoot boot issues, refer too[troubleshooting No Boot Issues on Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/000005845.html).</span></span>

<span data-ttu-id="355dd-110">tootroubleshoot système d’exploitation, consultez trop[résolution des problèmes du système d’exploitation sur Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/000006018.html).</span><span class="sxs-lookup"><span data-stu-id="355dd-110">tootroubleshoot operating system issues, refer too[troubleshooting Operating System Issues on Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/000006018.html).</span></span>

<span data-ttu-id="355dd-111">tootroubleshoot autres, consultez trop[Blink de Codes et émettre un signal sonore pour Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/intel-nuc-boards/000005854.html).</span><span class="sxs-lookup"><span data-stu-id="355dd-111">tootroubleshoot other issues, refer too[Blink Codes and Beep Codes for Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/intel-nuc-boards/000005854.html).</span></span>

## <a name="nodejs-package-issues"></a><span data-ttu-id="355dd-112">Problèmes de package Node.js</span><span class="sxs-lookup"><span data-stu-id="355dd-112">Node.js package issues</span></span>

### <a name="no-response-during-gulp-tasks"></a><span data-ttu-id="355dd-113">Aucune réponse lors des tâches gulp</span><span class="sxs-lookup"><span data-stu-id="355dd-113">No response during gulp tasks</span></span>

<span data-ttu-id="355dd-114">Si vous rencontrez des problèmes dans gulp tâches en cours d’exécution, vous pouvez ajouter hello `--verbose` option pour le débogage.</span><span class="sxs-lookup"><span data-stu-id="355dd-114">If you encounter problems in running gulp tasks, you can add hello `--verbose` option for debugging.</span></span> <span data-ttu-id="355dd-115">Essayez tooterminate actuel gulp tâches à l’aide de `Ctrl + C`, puis en exécution hello suivant commande dans les messages de débogage de toosee fenêtre console.</span><span class="sxs-lookup"><span data-stu-id="355dd-115">Try tooterminate current gulp tasks by using `Ctrl + C`, and then run hello following command in your console window toosee debug messages.</span></span> <span data-ttu-id="355dd-116">Des messages d’erreur détaillés peuvent s’afficher dans la sortie de la console.</span><span class="sxs-lookup"><span data-stu-id="355dd-116">You might see detailed error messages in your console output.</span></span>

```bash
gulp --verbose
```

### <a name="device-discovery-issues"></a><span data-ttu-id="355dd-117">Problèmes de détection d’appareil</span><span class="sxs-lookup"><span data-stu-id="355dd-117">Device discovery issues</span></span>

<span data-ttu-id="355dd-118">Pour vous aider à résoudre les problèmes courants avec hello `discover-sensortag` de commande, vérifiez hello [page wiki](https://wiki.archlinux.org/index.php/bluetooth#Bluetoothctl).</span><span class="sxs-lookup"><span data-stu-id="355dd-118">For help in troubleshooting common problems with hello `discover-sensortag` command, check hello [wiki page](https://wiki.archlinux.org/index.php/bluetooth#Bluetoothctl).</span></span>

### <a name="npm-issues"></a><span data-ttu-id="355dd-119">problèmes liés à npm</span><span class="sxs-lookup"><span data-stu-id="355dd-119">npm issues</span></span>

<span data-ttu-id="355dd-120">Essayez tooupdate votre package npm en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="355dd-120">Try tooupdate your npm package by running hello following command:</span></span>

```bash
npm install -g npm
```

<span data-ttu-id="355dd-121">Si le problème de hello existe toujours, laisser vos commentaires à la fin de hello de cet article ou créer un problème de GitHub dans notre [dépôt d’exemples](https://github.com/azure-samples/iot-hub-c-intel-nuc-gateway-getting-started).</span><span class="sxs-lookup"><span data-stu-id="355dd-121">If hello problem still exists, leave your comments at hello end of this article or create a GitHub issue in our [sample repository](https://github.com/azure-samples/iot-hub-c-intel-nuc-gateway-getting-started).</span></span>

## <a name="remote-debugging"></a><span data-ttu-id="355dd-122">Débogage à distance</span><span class="sxs-lookup"><span data-stu-id="355dd-122">Remote Debugging</span></span>
> <span data-ttu-id="355dd-123">Les instructions ci-dessous s’appliquent au débogage des scripts node.js utilisés dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="355dd-123">Below instructions are meant for debugging node.js scripts used in this tutorial.</span></span>
### <a name="run-hello-sample-application-in-debug-mode"></a><span data-ttu-id="355dd-124">Exécuter l’exemple d’application hello en mode débogage</span><span class="sxs-lookup"><span data-stu-id="355dd-124">Run hello sample application in debug mode</span></span>

<span data-ttu-id="355dd-125">Exécuter l’exemple d’application hello en mode débogage en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="355dd-125">Run hello sample application in debug mode by running hello following command:</span></span>

```bash
gulp run --debug
```

<span data-ttu-id="355dd-126">Lorsque le moteur de débogage hello est prêt, vous devez voir `Debugger listening on port 5858` dans la sortie de console hello.</span><span class="sxs-lookup"><span data-stu-id="355dd-126">When hello debug engine is ready, you should see `Debugger listening on port 5858` in hello console output.</span></span>

### <a name="configure-visual-studio-code-tooconnect-toohello-remote-device"></a><span data-ttu-id="355dd-127">Configurez le périphérique distant de Visual Studio Code tooconnect toohello</span><span class="sxs-lookup"><span data-stu-id="355dd-127">Configure Visual Studio Code tooconnect toohello remote device</span></span>

1. <span data-ttu-id="355dd-128">Ouvrez hello **déboguer** Panneau de configuration sur le côté gauche de hello.</span><span class="sxs-lookup"><span data-stu-id="355dd-128">Open hello **Debug** panel on hello left side.</span></span>
2. <span data-ttu-id="355dd-129">Cliquez sur hello verte **démarrer le débogage** bouton (F5).</span><span class="sxs-lookup"><span data-stu-id="355dd-129">Click hello green **Start Debugging** (F5) button.</span></span> <span data-ttu-id="355dd-130">Visual Studio Code ouvre un fichier `launch.json`.</span><span class="sxs-lookup"><span data-stu-id="355dd-130">Visual Studio Code opens a `launch.json` file.</span></span>
3. <span data-ttu-id="355dd-131">Hello de mise à jour `launch.json` fichier avec hello suivant le contenu.</span><span class="sxs-lookup"><span data-stu-id="355dd-131">Update hello `launch.json` file with hello following content.</span></span> <span data-ttu-id="355dd-132">Remplacez `[device hostname or IP address]` avec hello périphérique réel IP adresse ou nom d’hôte.</span><span class="sxs-lookup"><span data-stu-id="355dd-132">Replace `[device hostname or IP address]` with hello actual device IP address or host name.</span></span>

   ``` json
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
            "remoteRoot": "~/ble_sample"
        }
     ]
   }
   ```

![Configuration du débogage à distance](./media/iot-hub-gateway-kit-lessons/troubleshooting/remote_debugging_configuration.png)

### <a name="attach-toohello-remote-application"></a><span data-ttu-id="355dd-134">Attacher toohello des applications à distance</span><span class="sxs-lookup"><span data-stu-id="355dd-134">Attach toohello remote application</span></span>

<span data-ttu-id="355dd-135">Cliquez sur hello verte **démarrer le débogage** toostart de débogage de bouton (F5).</span><span class="sxs-lookup"><span data-stu-id="355dd-135">Click hello green **Start Debugging** (F5) button toostart debugging.</span></span>

<span data-ttu-id="355dd-136">Lecture [JavaScript dans Visual Studio Code](https://code.visualstudio.com/docs/languages/javascript#_debugging) toolearn plus à propos du débogueur de hello.</span><span class="sxs-lookup"><span data-stu-id="355dd-136">Read [JavaScript in VS Code](https://code.visualstudio.com/docs/languages/javascript#_debugging) toolearn more about hello debugger.</span></span>

![Exemple de débogage BLE](./media/iot-hub-gateway-kit-lessons/troubleshooting/debugging_ble_sample.png)

## <a name="azure-cli-issues"></a><span data-ttu-id="355dd-138">Problèmes d’interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="355dd-138">Azure CLI issues</span></span>

<span data-ttu-id="355dd-139">Bonjour Azure interface de ligne de commande (CLI d’Azure) est une version préliminaire.</span><span class="sxs-lookup"><span data-stu-id="355dd-139">hello Azure command-line interface (Azure CLI) is a preview build.</span></span> <span data-ttu-id="355dd-140">les solutions tooseek, vous pouvez utiliser hello [Guide d’installation de version préliminaire](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md).</span><span class="sxs-lookup"><span data-stu-id="355dd-140">tooseek solutions, you can use hello [Preview Install Guide](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md).</span></span>

<span data-ttu-id="355dd-141">Si vous rencontrez des bogues avec l’outil de hello, fichier un [problème](https://github.com/Azure/azure-cli/issues) Bonjour **problèmes** section du référentiel GitHub de hello.</span><span class="sxs-lookup"><span data-stu-id="355dd-141">If you encounter any bugs with hello tool, file an [issue](https://github.com/Azure/azure-cli/issues) in hello **Issues** section of hello GitHub repo.</span></span>

<span data-ttu-id="355dd-142">Pour vous aider à résoudre les problèmes courants, consultez hello [Lisez-moi](https://github.com/Azure/azure-cli/blob/master/README.rst).</span><span class="sxs-lookup"><span data-stu-id="355dd-142">For help in troubleshooting common problems, check hello [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span></span>

<span data-ttu-id="355dd-143">Si vous répondez à « Impossible de trouver une version qui satisfait aux exigences de hello, » veuillez suivante d’exécution hello commande version de toolastest tooupgrade pip.</span><span class="sxs-lookup"><span data-stu-id="355dd-143">If you meet "Could not find a version that satisfies hello requirement", please run hello following command tooupgrade pip toolastest version.</span></span>

```bash
python -m pip install --upgrade pip
```

## <a name="python-installation-issues"></a><span data-ttu-id="355dd-144">Problèmes d’installation de Python</span><span class="sxs-lookup"><span data-stu-id="355dd-144">Python installation issues</span></span>

### <a name="legacy-installation-issues-macos"></a><span data-ttu-id="355dd-145">Problèmes d’installation héritée (macOS)</span><span class="sxs-lookup"><span data-stu-id="355dd-145">Legacy installation issues (macOS)</span></span>

<span data-ttu-id="355dd-146">Lors de l’installation de pip, une erreur d’autorisation est levée s’il existe des packages antérieurs qui sont installés avec des autorisations **su**.</span><span class="sxs-lookup"><span data-stu-id="355dd-146">When you're installing pip, a permission error is thrown when older packages are installed with **su** permissions.</span></span> <span data-ttu-id="355dd-147">Cette situation se produit parce qu’une installation précédente de Python utilisant brew (macOS) n’est pas complètement désinstallée.</span><span class="sxs-lookup"><span data-stu-id="355dd-147">This situation occurs because a previous installation of Python using brew (macOS) is not uninstalled completely.</span></span> <span data-ttu-id="355dd-148">Certains packages pip d’une installation précédente ont été créées par la racine, ce qui provoque l’erreur d’autorisation hello.</span><span class="sxs-lookup"><span data-stu-id="355dd-148">Some pip packages from a previous installation were created by root, which causes hello permission error.</span></span> <span data-ttu-id="355dd-149">solution de Hello est tooremove ces packages installés par la racine.</span><span class="sxs-lookup"><span data-stu-id="355dd-149">hello solution is tooremove those packages installed by root.</span></span> <span data-ttu-id="355dd-150">Utilisez hello suivant les étapes toocomplete cette tâche :</span><span class="sxs-lookup"><span data-stu-id="355dd-150">Use hello following steps toocomplete this task:</span></span>

1. <span data-ttu-id="355dd-151">Accédez trop`/usr/local/lib/python2.7/site-packages`</span><span class="sxs-lookup"><span data-stu-id="355dd-151">Go too`/usr/local/lib/python2.7/site-packages`</span></span>
2. <span data-ttu-id="355dd-152">Affichez la liste des packages créés par root : `ls -l | grep root`</span><span class="sxs-lookup"><span data-stu-id="355dd-152">List packages created by root: `ls -l | grep root`</span></span>
3. <span data-ttu-id="355dd-153">Désinstallez les packages identifiés à l’étape 2 : `sudo rm -rf {package name}`</span><span class="sxs-lookup"><span data-stu-id="355dd-153">Uninstall packages from step 2: `sudo rm -rf {package name}`</span></span>
4. <span data-ttu-id="355dd-154">Réinstallez Python.</span><span class="sxs-lookup"><span data-stu-id="355dd-154">Reinstall Python.</span></span>

## <a name="azure-iot-hub-issues"></a><span data-ttu-id="355dd-155">Problèmes liés à Azure IoT Hub</span><span class="sxs-lookup"><span data-stu-id="355dd-155">Azure IoT Hub issues</span></span>

<span data-ttu-id="355dd-156">Si vous avez déployé votre concentrateur Azure IoT avec hello CLI d’Azure et que vous avez besoin d’un outil toomanage hello les appareils qui sont connectent tooyour IoT hub, essayez de hello suite d’outils.</span><span class="sxs-lookup"><span data-stu-id="355dd-156">If you've successfully provisioned your Azure IoT hub with hello Azure CLI, and you need a tool toomanage hello devices that are connecting tooyour IoT hub, try hello following tools.</span></span>

### <a name="device-explorer"></a><span data-ttu-id="355dd-157">Explorateur d’appareils</span><span class="sxs-lookup"><span data-stu-id="355dd-157">Device Explorer</span></span>

<span data-ttu-id="355dd-158">[Explorateur de périphérique](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) s’exécute sur votre ordinateur local de Windows et se connecte tooyour IoT hub dans Azure.</span><span class="sxs-lookup"><span data-stu-id="355dd-158">[Device Explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) runs on your Windows local machine and connects tooyour IoT hub in Azure.</span></span> <span data-ttu-id="355dd-159">Il communique avec les éléments suivants de hello [points de terminaison IoT Hub](https://azure.microsoft.com/en-us/documentation/articles/iot-hub-devguide/):</span><span class="sxs-lookup"><span data-stu-id="355dd-159">It communicates with hello following [IoT Hub endpoints](https://azure.microsoft.com/en-us/documentation/articles/iot-hub-devguide/):</span></span>

- <span data-ttu-id="355dd-160">Tooprovision de gestion de périphérique identité et de gérer les appareils inscrits avec votre IoT hub.</span><span class="sxs-lookup"><span data-stu-id="355dd-160">Device identity management tooprovision and manage devices registered with your IoT hub.</span></span>
- <span data-ttu-id="355dd-161">Vous pouvez surveiller les messages envoyés à partir de votre appareil tooyour IoT de supervision reçoivent appareil-à-cloud.</span><span class="sxs-lookup"><span data-stu-id="355dd-161">Receive device-to-cloud so you can monitor messages sent from your device tooyour IoT hub.</span></span>
- <span data-ttu-id="355dd-162">Envoyer le cloud sur l’appareil afin de pouvoir envoyer des messages tooyour périphériques à partir de votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="355dd-162">Send cloud-to-device so you can send messages tooyour devices from your IoT hub.</span></span>

<span data-ttu-id="355dd-163">Configurer votre chaîne de connexion de hub IoT dans cette toouse outil toutes ses fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="355dd-163">Configure your IoT hub connection string within this tool toouse all its capabilities.</span></span>

### <a name="iothub-explorer"></a><span data-ttu-id="355dd-164">iothub-explorer</span><span class="sxs-lookup"><span data-stu-id="355dd-164">iothub-explorer</span></span>

<span data-ttu-id="355dd-165">[Explorateur d’iothub](https://github.com/Azure/iothub-explorer) est un exemple d’outil CLI multiplateforme toomanage appareils clients.</span><span class="sxs-lookup"><span data-stu-id="355dd-165">[iothub-explorer](https://github.com/Azure/iothub-explorer) is a sample multiplatform CLI tool toomanage device clients.</span></span> <span data-ttu-id="355dd-166">Vous pouvez utiliser des périphériques de hello hello outil toomanage dans le Registre des identités hello, surveiller les messages appareil-à-cloud et envoyer des commandes de cloud sur l’appareil.</span><span class="sxs-lookup"><span data-stu-id="355dd-166">You can use hello tool toomanage hello devices in hello identity registry, monitor device-to-cloud messages, and send cloud-to-device commands.</span></span>

<span data-ttu-id="355dd-167">tooinstall hello dernière (version préliminaire) version de hello iothub-explorer outil, exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="355dd-167">tooinstall hello latest (prerelease) version of hello iothub-explorer tool, run hello following command:</span></span>

```bash
npm install -g iothub-explorer@latest
```

<span data-ttu-id="355dd-168">tooget une aide supplémentaire sur tous les hello iothub-Explorateur commandes et leurs paramètres, exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="355dd-168">tooget additional help about all hello iothub-explorer commands and their parameters, run hello following command:</span></span>

```bash
iothub-explorer help
```

### <a name="hello-azure-portal"></a><span data-ttu-id="355dd-169">Hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="355dd-169">hello Azure portal</span></span>

<span data-ttu-id="355dd-170">Une expérience complète de l’interface de ligne de commande vous permet de créer et de gérer toutes vos ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="355dd-170">A full CLI experience helps you create and manage all your Azure resources.</span></span> <span data-ttu-id="355dd-171">Vous pouvez également vous toouse hello [portail Azure](https://azure.microsoft.com/en-us/documentation/articles/azure-portal-overview/) toohelp configurer, gérer et déboguer vos ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="355dd-171">You might also want toouse hello [Azure portal](https://azure.microsoft.com/en-us/documentation/articles/azure-portal-overview/) toohelp provision, manage, and debug your Azure resources.</span></span>

## <a name="azure-storage-issues"></a><span data-ttu-id="355dd-172">Problèmes liés au Stockage Azure</span><span class="sxs-lookup"><span data-stu-id="355dd-172">Azure Storage issues</span></span>

<span data-ttu-id="355dd-173">[Explorateur de stockage Microsoft Azure (aperçu)](http://storageexplorer.com/) est une application autonome de Microsoft que vous pouvez utiliser toowork avec des données de stockage Azure sur Windows, Mac OS et Linux.</span><span class="sxs-lookup"><span data-stu-id="355dd-173">[Microsoft Azure Storage Explorer (preview)](http://storageexplorer.com/) is a standalone app from Microsoft that you can use toowork with Azure Storage data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="355dd-174">À l’aide de cet outil, vous pouvez connecter tooyour table et voir les données hello.</span><span class="sxs-lookup"><span data-stu-id="355dd-174">By using this tool, you can connect tooyour table and see hello data in it.</span></span> <span data-ttu-id="355dd-175">Vous pouvez utiliser cet outil tootroubleshoot vos problèmes de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="355dd-175">You can use this tool tootroubleshoot your Azure Storage issues.</span></span>
