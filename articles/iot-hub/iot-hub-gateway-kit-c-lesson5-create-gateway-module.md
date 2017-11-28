---
title: aaaCreate votre premier module Azure IoT passerelle | Documents Microsoft
description: "Créez un module et ajouter des comportements de module toocustomize tooa exemple application."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: 
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: cd7660f4-7b8b-4091-8d71-bb8723165b0b
ms.service: iot-hub
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 48996fc026c8b708e328b5629801465810e5b6a2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="lesson-5-create-your-first-azure-iot-gateway-module"></a><span data-ttu-id="c38c0-103">Leçon 5 : Créer votre premier module de passerelle Azure IoT</span><span class="sxs-lookup"><span data-stu-id="c38c0-103">Lesson 5: Create your first Azure IoT Gateway module</span></span>
<span data-ttu-id="c38c0-104">Azure IoT bord vous permet de modules toobuild écrits en Java, .NET ou Node.js, ce didacticiel vous guide à travers les étapes de hello pour la création d’un module en C.</span><span class="sxs-lookup"><span data-stu-id="c38c0-104">While Azure IoT Edge allows you toobuild modules written in Java, .NET, or Node.js, this tutorial walks you through hello steps for building a module in C.</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="c38c0-105">Procédure à suivre</span><span class="sxs-lookup"><span data-stu-id="c38c0-105">What you will do</span></span>

- <span data-ttu-id="c38c0-106">Compilez et exécutez l’application d’exemple hello Bonjour_monde sur Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="c38c0-106">Compile and run hello hello_world sample app on Intel NUC.</span></span>
- <span data-ttu-id="c38c0-107">Créez un module et compilez-le sur l’Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="c38c0-107">Create a module and compile it on Intel NUC.</span></span>
- <span data-ttu-id="c38c0-108">Ajouter hello nouveau module toohello Bonjour_monde exemple d’application, puis exécutez exemple hello sur NUC d’Intel.</span><span class="sxs-lookup"><span data-stu-id="c38c0-108">Add hello new module toohello hello_world sample app and then run hello sample on Intel NUC.</span></span> <span data-ttu-id="c38c0-109">nouveau module de Hello imprime les messages « Bonjour_monde » avec un horodatage.</span><span class="sxs-lookup"><span data-stu-id="c38c0-109">hello new module prints out "hello_world" messages with a timestamp.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="c38c0-110">Contenu</span><span class="sxs-lookup"><span data-stu-id="c38c0-110">What you will learn</span></span>

- <span data-ttu-id="c38c0-111">Comment toocompile et exécuter un exemple d’application sur NUC d’Intel.</span><span class="sxs-lookup"><span data-stu-id="c38c0-111">How toocompile and run a sample app on Intel NUC.</span></span>
- <span data-ttu-id="c38c0-112">Comment toocreate un module.</span><span class="sxs-lookup"><span data-stu-id="c38c0-112">How toocreate a module.</span></span>
- <span data-ttu-id="c38c0-113">Comment tooadd module tooa exemple d’application.</span><span class="sxs-lookup"><span data-stu-id="c38c0-113">How tooadd module tooa sample app.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="c38c0-114">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="c38c0-114">What you need</span></span>

<span data-ttu-id="c38c0-115">Azure IoT Edge installé sur votre ordinateur hôte.</span><span class="sxs-lookup"><span data-stu-id="c38c0-115">Azure IoT Edge that has been installed on your host computer.</span></span>

## <a name="folder-structure"></a><span data-ttu-id="c38c0-116">Structure de dossiers</span><span class="sxs-lookup"><span data-stu-id="c38c0-116">Folder structure</span></span>

<span data-ttu-id="c38c0-117">Dans le sous-dossier hello leçon 5 de l’exemple de code hello que vous avez cloné dans la leçon 1, il existe un `module` dossier et un `sample` dossier.</span><span class="sxs-lookup"><span data-stu-id="c38c0-117">In hello Lesson 5 subfolder of hello sample code which you cloned in lesson 1, there is a `module` folder and a `sample` folder.</span></span>

![my_module](media/iot-hub-gateway-kit-lessons/lesson5/my_module.png)

- <span data-ttu-id="c38c0-119">Hello `module/my_module` dossier contient hello code et le script toobuild hello module de source.</span><span class="sxs-lookup"><span data-stu-id="c38c0-119">hello `module/my_module` folder contains hello source code and script toobuild hello module.</span></span>
- <span data-ttu-id="c38c0-120">Hello `sample` dossier contient hello source code et le script toobuild hello exemple d’application.</span><span class="sxs-lookup"><span data-stu-id="c38c0-120">hello `sample` folder contains hello source code and script toobuild hello sample app.</span></span>

## <a name="compile-and-run-hello-helloworld-sample-app-on-intel-nuc"></a><span data-ttu-id="c38c0-121">Compiler et exécuter l’application d’exemple hello Bonjour_monde sur Intel NUC</span><span class="sxs-lookup"><span data-stu-id="c38c0-121">Compile and run hello hello_world sample app on Intel NUC</span></span>

<span data-ttu-id="c38c0-122">Hello `hello_world` exemple crée une passerelle selon hello `hello_world.json` fichier qui spécifie les modules prédéfinis deux hello associés application hello.</span><span class="sxs-lookup"><span data-stu-id="c38c0-122">hello `hello_world` sample creates a gateway based on hello `hello_world.json` file which specifies hello two predefined modules associated with hello app.</span></span> <span data-ttu-id="c38c0-123">passerelle de Hello enregistre toutes les 5 secondes à un fichier de tooa de message « hello world ».</span><span class="sxs-lookup"><span data-stu-id="c38c0-123">hello gateway logs a "hello world" message tooa file every 5 seconds.</span></span> <span data-ttu-id="c38c0-124">Dans cette section, vous compilez et exécutez hello `hello_world` application avec son module par défaut.</span><span class="sxs-lookup"><span data-stu-id="c38c0-124">In this section, you compile and run hello `hello_world` app with its default module.</span></span>

<span data-ttu-id="c38c0-125">hello toocompile et exécutez `hello_world` application, procédez comme suit sur votre ordinateur hôte :</span><span class="sxs-lookup"><span data-stu-id="c38c0-125">toocompile and run hello `hello_world` app, follow these steps on your host computer:</span></span>

1. <span data-ttu-id="c38c0-126">Initialiser les fichiers de configuration hello en hello suivant les commandes en cours d’exécution :</span><span class="sxs-lookup"><span data-stu-id="c38c0-126">Initialize hello configuration files by running hello following commands:</span></span>

   ```bash
   cd iot-hub-c-intel-nuc-gateway-getting-started
   cd Lesson5
   npm install
   gulp init
   ```

1. <span data-ttu-id="c38c0-127">Mettre à jour le fichier de configuration de passerelle hello avec hello adresse MAC d’Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="c38c0-127">Update hello gateway configuration file with hello MAC address of Intel NUC.</span></span> <span data-ttu-id="c38c0-128">Ignorez cette étape si vous avez parcouru leçon de hello trop[configurer et exécuter un exemple d’application BLE][config_ble].</span><span class="sxs-lookup"><span data-stu-id="c38c0-128">Skip this step if you have gone through hello lesson too[configure and run a BLE sample application][config_ble].</span></span>

   1. <span data-ttu-id="c38c0-129">Ouvrez le fichier de configuration de passerelle de hello en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="c38c0-129">Open hello gateway configuration file by running hello following command:</span></span>

      ```bash
      # For Windows command prompt
      code %USERPROFILE%\.iot-hub-getting-started\config-gateway.json

      # For MacOS or Ubuntu
      code ~/.iot-hub-getting-started/config-gateway.json
      ```

   1. <span data-ttu-id="c38c0-130">D’adresses MAC de la passerelle de mise à jour hello lorsque vous [configurer NUC Intel comme passerelle IoT][setup_nuc], puis enregistrez le fichier de hello.</span><span class="sxs-lookup"><span data-stu-id="c38c0-130">Update hello gateway's MAC address when you [set up Intel NUC as a IoT gateway][setup_nuc], and then save hello file.</span></span>

1. <span data-ttu-id="c38c0-131">Compilez les exemples de code source hello en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="c38c0-131">Compile hello sample source code by running hello following command:</span></span>

   ```bash
   gulp compile
   ```

   <span data-ttu-id="c38c0-132">transfère la source d’exemple hello tooIntel code NUC Hello commande et exécute `build.sh` toocompile il.</span><span class="sxs-lookup"><span data-stu-id="c38c0-132">hello command transfers hello sample source code tooIntel NUC and runs `build.sh` toocompile it.</span></span>

1. <span data-ttu-id="c38c0-133">Exécutez hello `hello_world` application sur Intel NUC en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="c38c0-133">Run hello `hello_world` app on Intel NUC by running hello following command:</span></span>

   ```bash
   gulp run
   ```

   <span data-ttu-id="c38c0-134">Hello s’exécute la commande `../Tools/run-hello-world.js` qui est spécifié dans `config.json` toostart hello exemple d’application sur NUC d’Intel.</span><span class="sxs-lookup"><span data-stu-id="c38c0-134">hello command runs `../Tools/run-hello-world.js` that is specified in `config.json` toostart hello sample app on Intel NUC.</span></span>

   ![run_sample](media/iot-hub-gateway-kit-lessons/lesson5/run_sample.png)

## <a name="create-a-new-module-and-compile-it-on-intel-nuc"></a><span data-ttu-id="c38c0-136">Créer un module et le compiler sur l’Intel NUC</span><span class="sxs-lookup"><span data-stu-id="c38c0-136">Create a new module and compile it on Intel NUC</span></span>

<span data-ttu-id="c38c0-137">étapes Hello ci-dessous vous guident dans la création d’un nouveau module et le compiler sur NUC d’Intel.</span><span class="sxs-lookup"><span data-stu-id="c38c0-137">hello steps below walk you through creating a new module and compile it on Intel NUC.</span></span> <span data-ttu-id="c38c0-138">module de Hello imprime les messages avec un horodatage lors de leur réception.</span><span class="sxs-lookup"><span data-stu-id="c38c0-138">hello module prints out messages with a timestamp upon receiving them.</span></span> <span data-ttu-id="c38c0-139">Vous allez créer votre premier module de passerelle personnalisé dans cette section.</span><span class="sxs-lookup"><span data-stu-id="c38c0-139">You will create your first customized gateway module in this section.</span></span>

<span data-ttu-id="c38c0-140">N’importe quel module Azure IoT Edge doit implémenter hello suivant des interfaces :</span><span class="sxs-lookup"><span data-stu-id="c38c0-140">Any Azure IoT Edge module must implement hello following interfaces:</span></span>

   ```C
   pfModule_ParseConfigurationFromJson Module_ParseConfigurationFromJson
   pfModule_FreeConfiguration Module_FreeConfiguration
   pfModule_Create Module_Create
   pfModule_Destroy Module_Destroy
   pfModule_Receive Module_Receive
   ```

<span data-ttu-id="c38c0-141">Vous pouvez implémenter hello suivant interface :</span><span class="sxs-lookup"><span data-stu-id="c38c0-141">You can optionally implement hello following interface:</span></span>

   ```C
   pfModule_Start Module_Start
   ```

<span data-ttu-id="c38c0-142">Hello diagramme suivant montre chemins d’accès de hello état importants d’un module.</span><span class="sxs-lookup"><span data-stu-id="c38c0-142">hello following diagram shows hello important state paths of a module.</span></span> <span data-ttu-id="c38c0-143">les rectangles carré Hello représentent des méthodes que vous implémentez les opérations tooperform lorsque le module de hello se déplace entre les États.</span><span class="sxs-lookup"><span data-stu-id="c38c0-143">hello square rectangles represent methods you implement tooperform operations when hello module moves between states.</span></span> <span data-ttu-id="c38c0-144">ovales de Hello sont les principaux États module de hello.</span><span class="sxs-lookup"><span data-stu-id="c38c0-144">hello ovals are major states hello module can be in.</span></span>

![state_path](media/iot-hub-gateway-kit-lessons/lesson5/state_path.png)

<span data-ttu-id="c38c0-146">Maintenant nous allons créer un module basé sur le modèle de hello :</span><span class="sxs-lookup"><span data-stu-id="c38c0-146">Now let’s create a module based on hello template:</span></span>

1. <span data-ttu-id="c38c0-147">Ouvrez le dossier de modèle de hello en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="c38c0-147">Open hello template folder by running hello following command:</span></span>

   ```bash
   code module/my_module
   ```

   ![code_module](media/iot-hub-gateway-kit-lessons/lesson5/code_module.png)

   - <span data-ttu-id="c38c0-149">`src/my_module.c`sert de modèle qui facilite la création d’un module hello.</span><span class="sxs-lookup"><span data-stu-id="c38c0-149">`src/my_module.c` serves as a template that facilitates hello creation of a module.</span></span> <span data-ttu-id="c38c0-150">modèle de Hello déclare les interfaces hello.</span><span class="sxs-lookup"><span data-stu-id="c38c0-150">hello template declares hello interfaces.</span></span> <span data-ttu-id="c38c0-151">Il vous suffit de toodo est tooadd logique toohello `MyModule_Receive` (fonction).</span><span class="sxs-lookup"><span data-stu-id="c38c0-151">All you need toodo is tooadd logic toohello `MyModule_Receive` function.</span></span>
   - <span data-ttu-id="c38c0-152">`build.sh`est hello build script toocompile hello module NUC d’Intel.</span><span class="sxs-lookup"><span data-stu-id="c38c0-152">`build.sh` is hello build script toocompile hello module on Intel NUC.</span></span>
1. <span data-ttu-id="c38c0-153">Ouvrez hello `src/my_module.c` de fichiers et d’inclure les deux fichiers d’en-tête :</span><span class="sxs-lookup"><span data-stu-id="c38c0-153">Open hello `src/my_module.c` file and include two header files:</span></span>

   ```C
   #include <stdio.h>
   #include "azure_c_shared_utility/xlogging.h"
   ```

1. <span data-ttu-id="c38c0-154">Ajouter hello suivant code toohello `MyModule_Receive` fonction :</span><span class="sxs-lookup"><span data-stu-id="c38c0-154">Add hello following code toohello `MyModule_Receive` function:</span></span>

   ```C
   if (message == NULL)
   {
      LogError("invalid arg message");
   }
   else
   {
      // get hello message content
      const CONSTBUFFER * content = Message_GetContent(message);
      // get hello local time and format it
      time_t temp = time(NULL);
      if (temp == (time_t)-1)
      {
          LogError("time function failed");
      }
      else
      {
          struct tm* t = localtime(&temp);
          if (t == NULL)
          {
              LogError("localtime failed");
          }
          else
          {
              char timetemp[80] = { 0 };
              if (strftime(timetemp, sizeof(timetemp) / sizeof(timetemp[0]), "%c", t) == 0)
              {
                  LogError("unable toostrftime");
              }
              else
              {
                  printf("[%s] %.*s\r\n", timetemp, (int)content->size, content->buffer);
              }
          }
      }
   }
   ```

1. <span data-ttu-id="c38c0-155">Hello de mise à jour `config.json` hello toospecify de fichier `workspace` dossier sur votre ordinateur et hello déploiement chemin vers l’hôte sur NUC d’Intel.</span><span class="sxs-lookup"><span data-stu-id="c38c0-155">Update hello `config.json` file toospecify hello `workspace` folder on your host computer and hello deployment path on Intel NUC.</span></span> <span data-ttu-id="c38c0-156">Pendant la compilation, hello fichiers Bonjour `workspace` dossier seront transférées toohello le chemin de déploiement.</span><span class="sxs-lookup"><span data-stu-id="c38c0-156">During compiling, hello files in hello `workspace` folder will be transferred toohello deployment path.</span></span>

   1. <span data-ttu-id="c38c0-157">Ouvrez hello `config.json` fichier en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="c38c0-157">Open hello `config.json` file by running hello following command:</span></span>

      ```bash
      code config.json
      ```

   1. <span data-ttu-id="c38c0-158">Mise à jour `config.json` avec hello configuration suivante :</span><span class="sxs-lookup"><span data-stu-id="c38c0-158">Update `config.json` with hello following configuration:</span></span>

      ```json
      "workspace": "./module/my_module",
      "deploy_path": "module/my_module"
      ```

      ![config_json](media/iot-hub-gateway-kit-lessons/lesson5/config_json.png)

1. <span data-ttu-id="c38c0-160">Compilez le module de hello en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="c38c0-160">Compile hello module by running hello following command:</span></span>

   ```bash
   gulp compile
   ```

   <span data-ttu-id="c38c0-161">transfère hello source code tooIntel NUC Hello commande et exécute `build.sh` module de hello toocompile.</span><span class="sxs-lookup"><span data-stu-id="c38c0-161">hello command transfers hello source code tooIntel NUC and runs `build.sh` toocompile hello module.</span></span>

## <a name="add-hello-module-toohello-helloworld-sample-app-and-run-hello-app-on-intel-nuc"></a><span data-ttu-id="c38c0-162">Ajouter hello module toohello Bonjour_monde exemple d’application et exécutez l’application hello sur Intel NUC</span><span class="sxs-lookup"><span data-stu-id="c38c0-162">Add hello module toohello hello_world sample app and run hello app on Intel NUC</span></span>

<span data-ttu-id="c38c0-163">tooperform cette tâche, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="c38c0-163">tooperform this task, follow these steps:</span></span>

1. <span data-ttu-id="c38c0-164">Répertorier tous les binaires de module disponible hello (fichiers .so) sur Intel NUC en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="c38c0-164">List all hello available module binaries (.so files) on Intel NUC by running hello following command:</span></span>

   ```bash
   gulp modules --list
   ```

   <span data-ttu-id="c38c0-165">Hello chemin d’accès binaire `my_module` que vous avez compilé doit être répertorié comme ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="c38c0-165">hello binary path of `my_module` that you compiled should be listed as below:</span></span>

   ```path
   /root/gateway_sample/module/my_module/build/libmy_module.so
   ```

   <span data-ttu-id="c38c0-166">Si vous modifiez le nom d’utilisateur du compte de connexion par défaut hello dans `config-gateway.json`, chemin d’accès binaire de hello démarrera avec `home/<your username>` au lieu de `root`.</span><span class="sxs-lookup"><span data-stu-id="c38c0-166">If you change hello default login username in `config-gateway.json`, hello binary path will start with `home/<your username>` instead of `root`.</span></span>

1. <span data-ttu-id="c38c0-167">Ajouter `my_module` toohello `hello_world` exemple d’application :</span><span class="sxs-lookup"><span data-stu-id="c38c0-167">Add `my_module` toohello `hello_world` sample app:</span></span>

   1. <span data-ttu-id="c38c0-168">Ouvrez hello `hello_world.json` fichier en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="c38c0-168">Open hello `hello_world.json` file by running hello following command:</span></span>

      ```bash
      code sample/hello_world/src/hello_world.json
      ```

   1. <span data-ttu-id="c38c0-169">Ajouter hello suivant code toohello `modules` section :</span><span class="sxs-lookup"><span data-stu-id="c38c0-169">Add hello following code toohello `modules` section:</span></span>

      ```json
      {
       "name": "my_module",
       "loader": {
       "name": "native",
       "entrypoint": {
       "module.path": "/root/gateway_sample/module/my_module/build/libmy_module.so"
         }
        },
       "args": null
      }
      ```

      <span data-ttu-id="c38c0-170">Hello valeur `module.path` doit être `/root/gateway_sample/module/my_module/build/libmy_module.so`.</span><span class="sxs-lookup"><span data-stu-id="c38c0-170">hello value of `module.path` should be `/root/gateway_sample/module/my_module/build/libmy_module.so`.</span></span> <span data-ttu-id="c38c0-171">code de Hello déclare `my_module` toobe associée passerelle de hello ainsi que d’emplacement hello du fichier binaire du module hello spécifié dans `module.path`.</span><span class="sxs-lookup"><span data-stu-id="c38c0-171">hello code declares `my_module` toobe associated with hello gateway as well as hello location of hello module binary specified in `module.path`.</span></span>
   1. <span data-ttu-id="c38c0-172">Ajouter hello suivant code toohello `links` section :</span><span class="sxs-lookup"><span data-stu-id="c38c0-172">Add hello following code toohello `links` section:</span></span>

      ```json
      {
        "source": "hello_world",
        "sink": "my_module"
      }
      ```

      <span data-ttu-id="c38c0-173">Ce code spécifie que les messages sont transférés de hello `hello_world` module trop`my_module`.</span><span class="sxs-lookup"><span data-stu-id="c38c0-173">This code specifies that messages are transferred from hello `hello_world` module too`my_module`.</span></span>

      ![hello_world_json](media/iot-hub-gateway-kit-lessons/lesson5/hello_world_json.png)

1. <span data-ttu-id="c38c0-175">Exécutez hello `hello_world` exemple d’application en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="c38c0-175">Run hello `hello_world` sample app by running hello following command:</span></span>

   ```bash
   gulp run --config sample/hello_world/src/hello_world.json
   ```

   <span data-ttu-id="c38c0-176">Hello `--config` paramètre force hello `run-hello-world.js` toorun de script à l’aide de hello `hello_world.json` fichier.</span><span class="sxs-lookup"><span data-stu-id="c38c0-176">hello `--config` parameter forces hello `run-hello-world.js` script toorun by using hello `hello_world.json` file.</span></span>

   ![hello_world_new](media/iot-hub-gateway-kit-lessons/lesson5/hello_world_new.png)

<span data-ttu-id="c38c0-178">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="c38c0-178">Congratulations.</span></span> <span data-ttu-id="c38c0-179">Vous pouvez maintenant voir le comportement de hello ce nouveau module, il imprime simplement les messages « hello world » avec un horodatage, un résultat différent d’un module hello d’origine « Bonjour_monde ».</span><span class="sxs-lookup"><span data-stu-id="c38c0-179">You can now see hello behavior of this new module, it simply prints out "hello world" messages with a timestamp, a different result from hello original "hello_world" module.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c38c0-180">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c38c0-180">Next Steps</span></span>

<span data-ttu-id="c38c0-181">Vous avez créé un nouveau module, ajouté toohello Bonjour_monde exemple et get hello exemple application toorun avec le nouveau module de hello sur votre passerelle.</span><span class="sxs-lookup"><span data-stu-id="c38c0-181">You’ve created a new module, added it toohello hello_world sample, and get hello sample app toorun with hello new module on your gateway.</span></span> <span data-ttu-id="c38c0-182">Si vous souhaitez toolearn plus d’informations sur les modules de passerelle Azure IoT, vous trouverez d’autres exemples de module ici : [https://github.com/Azure/azure-iot-gateway-sdk/tree/master/modules](https://github.com/Azure/azure-iot-gateway-sdk/tree/master/modules).</span><span class="sxs-lookup"><span data-stu-id="c38c0-182">If you want toolearn more about Azure IoT gateway modules, you can find more module samples here: [https://github.com/Azure/azure-iot-gateway-sdk/tree/master/modules](https://github.com/Azure/azure-iot-gateway-sdk/tree/master/modules).</span></span>

<!-- Images and links -->

[config_ble]: iot-hub-gateway-kit-c-lesson3-configure-ble-app.md
[setup_nuc]: iot-hub-gateway-kit-c-lesson1-set-up-nuc.md
