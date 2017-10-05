---
title: "Créer votre premier module de passerelle Azure IoT | Microsoft Docs"
description: "Créez un module et ajoutez-le à un exemple d’application pour personnaliser les comportements du module."
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
ms.openlocfilehash: 5e28422158684c3aaf0ac3fdf5b19c80fbccfb02
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="lesson-5-create-your-first-azure-iot-gateway-module"></a><span data-ttu-id="02fef-103">Leçon 5 : Créer votre premier module de passerelle Azure IoT</span><span class="sxs-lookup"><span data-stu-id="02fef-103">Lesson 5: Create your first Azure IoT Gateway module</span></span>
<span data-ttu-id="02fef-104">Bien qu’Azure IoT Edge permette de développer des modules écrits en Java, .NET ou Node.js, ce didacticiel vous guide à travers les étapes de création d’un module en langage C.</span><span class="sxs-lookup"><span data-stu-id="02fef-104">While Azure IoT Edge allows you to build modules written in Java, .NET, or Node.js, this tutorial walks you through the steps for building a module in C.</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="02fef-105">Procédure à suivre</span><span class="sxs-lookup"><span data-stu-id="02fef-105">What you will do</span></span>

- <span data-ttu-id="02fef-106">Compilez et exécutez l’exemple d’application hello_world sur l’Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="02fef-106">Compile and run the hello_world sample app on Intel NUC.</span></span>
- <span data-ttu-id="02fef-107">Créez un module et compilez-le sur l’Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="02fef-107">Create a module and compile it on Intel NUC.</span></span>
- <span data-ttu-id="02fef-108">Ajouter le nouveau module à l’exemple d’application hello_world, puis exécutez l’exemple sur l’Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="02fef-108">Add the new module to the hello_world sample app and then run the sample on Intel NUC.</span></span> <span data-ttu-id="02fef-109">Le nouveau module affiche des messages « hello world » avec un horodatage.</span><span class="sxs-lookup"><span data-stu-id="02fef-109">The new module prints out "hello_world" messages with a timestamp.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="02fef-110">Contenu</span><span class="sxs-lookup"><span data-stu-id="02fef-110">What you will learn</span></span>

- <span data-ttu-id="02fef-111">Compilation et exécution d’un exemple d’application sur l’Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="02fef-111">How to compile and run a sample app on Intel NUC.</span></span>
- <span data-ttu-id="02fef-112">Création d’un module.</span><span class="sxs-lookup"><span data-stu-id="02fef-112">How to create a module.</span></span>
- <span data-ttu-id="02fef-113">Ajout d’un module à un exemple d’application.</span><span class="sxs-lookup"><span data-stu-id="02fef-113">How to add module to a sample app.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="02fef-114">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="02fef-114">What you need</span></span>

<span data-ttu-id="02fef-115">Azure IoT Edge installé sur votre ordinateur hôte.</span><span class="sxs-lookup"><span data-stu-id="02fef-115">Azure IoT Edge that has been installed on your host computer.</span></span>

## <a name="folder-structure"></a><span data-ttu-id="02fef-116">Structure de dossiers</span><span class="sxs-lookup"><span data-stu-id="02fef-116">Folder structure</span></span>

<span data-ttu-id="02fef-117">Dans le sous-dossier de la leçon 5 pour l’exemple de code que vous avez cloné dans la leçon 1, il y a un dossier `module` et un dossier `sample`.</span><span class="sxs-lookup"><span data-stu-id="02fef-117">In the Lesson 5 subfolder of the sample code which you cloned in lesson 1, there is a `module` folder and a `sample` folder.</span></span>

![my_module](media/iot-hub-gateway-kit-lessons/lesson5/my_module.png)

- <span data-ttu-id="02fef-119">Le dossier `module/my_module` contient le code source et le script permettant de générer le module.</span><span class="sxs-lookup"><span data-stu-id="02fef-119">The `module/my_module` folder contains the source code and script to build the module.</span></span>
- <span data-ttu-id="02fef-120">Le dossier `sample` contient le code source et le script permettant de générer l’exemple d’application.</span><span class="sxs-lookup"><span data-stu-id="02fef-120">The `sample` folder contains the source code and script to build the sample app.</span></span>

## <a name="compile-and-run-the-helloworld-sample-app-on-intel-nuc"></a><span data-ttu-id="02fef-121">Compiler et exécuter l’exemple d’application hello_world sur l’Intel NUC</span><span class="sxs-lookup"><span data-stu-id="02fef-121">Compile and run the hello_world sample app on Intel NUC</span></span>

<span data-ttu-id="02fef-122">L’exemple `hello_world` crée une passerelle en fonction du fichier `hello_world.json` qui spécifie les deux modules prédéfinis associés à l’application.</span><span class="sxs-lookup"><span data-stu-id="02fef-122">The `hello_world` sample creates a gateway based on the `hello_world.json` file which specifies the two predefined modules associated with the app.</span></span> <span data-ttu-id="02fef-123">La passerelle consigne un message « hello world » dans un fichier toutes les 5 secondes.</span><span class="sxs-lookup"><span data-stu-id="02fef-123">The gateway logs a "hello world" message to a file every 5 seconds.</span></span> <span data-ttu-id="02fef-124">Dans cette section, vous compilez et exécutez l’application `hello_world` avec son module par défaut.</span><span class="sxs-lookup"><span data-stu-id="02fef-124">In this section, you compile and run the `hello_world` app with its default module.</span></span>

<span data-ttu-id="02fef-125">Pour compiler et exécuter l’application `hello_world`, procédez comme suit sur votre ordinateur hôte :</span><span class="sxs-lookup"><span data-stu-id="02fef-125">To compile and run the `hello_world` app, follow these steps on your host computer:</span></span>

1. <span data-ttu-id="02fef-126">Initialisez les fichiers de configuration en exécutant les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="02fef-126">Initialize the configuration files by running the following commands:</span></span>

   ```bash
   cd iot-hub-c-intel-nuc-gateway-getting-started
   cd Lesson5
   npm install
   gulp init
   ```

1. <span data-ttu-id="02fef-127">Mettez à jour le fichier de configuration de la passerelle avec l’adresse MAC de l’Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="02fef-127">Update the gateway configuration file with the MAC address of Intel NUC.</span></span> <span data-ttu-id="02fef-128">Ignorez cette étape si vous avez suivi la leçon pour [configurer et exécuter un exemple d’application BLE][config_ble].</span><span class="sxs-lookup"><span data-stu-id="02fef-128">Skip this step if you have gone through the lesson to [configure and run a BLE sample application][config_ble].</span></span>

   1. <span data-ttu-id="02fef-129">Ouvrez le fichier de configuration de la passerelle en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="02fef-129">Open the gateway configuration file by running the following command:</span></span>

      ```bash
      # For Windows command prompt
      code %USERPROFILE%\.iot-hub-getting-started\config-gateway.json

      # For MacOS or Ubuntu
      code ~/.iot-hub-getting-started/config-gateway.json
      ```

   1. <span data-ttu-id="02fef-130">Mettez à jour l’adresse MAC de la passerelle lorsque vous [configurez l’Intel NUC en tant que passerelle IoT][setup_nuc], puis enregistrez le fichier.</span><span class="sxs-lookup"><span data-stu-id="02fef-130">Update the gateway's MAC address when you [set up Intel NUC as a IoT gateway][setup_nuc], and then save the file.</span></span>

1. <span data-ttu-id="02fef-131">Compilez l’exemple de code source en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="02fef-131">Compile the sample source code by running the following command:</span></span>

   ```bash
   gulp compile
   ```

   <span data-ttu-id="02fef-132">La commande transfère l’exemple de code source à l’Intel NUC et exécute `build.sh` pour le compiler.</span><span class="sxs-lookup"><span data-stu-id="02fef-132">The command transfers the sample source code to Intel NUC and runs `build.sh` to compile it.</span></span>

1. <span data-ttu-id="02fef-133">Exécutez l’application `hello_world` sur l’Intel NUC à l’aide de la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="02fef-133">Run the `hello_world` app on Intel NUC by running the following command:</span></span>

   ```bash
   gulp run
   ```

   <span data-ttu-id="02fef-134">Cette commande exécute le fichier `../Tools/run-hello-world.js` spécifié dans `config.json` pour démarrer l’exemple d’application sur l’Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="02fef-134">The command runs `../Tools/run-hello-world.js` that is specified in `config.json` to start the sample app on Intel NUC.</span></span>

   ![run_sample](media/iot-hub-gateway-kit-lessons/lesson5/run_sample.png)

## <a name="create-a-new-module-and-compile-it-on-intel-nuc"></a><span data-ttu-id="02fef-136">Créer un module et le compiler sur l’Intel NUC</span><span class="sxs-lookup"><span data-stu-id="02fef-136">Create a new module and compile it on Intel NUC</span></span>

<span data-ttu-id="02fef-137">La procédure ci-dessous vous guide dans la création d’un module et sa compilation sur l’Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="02fef-137">The steps below walk you through creating a new module and compile it on Intel NUC.</span></span> <span data-ttu-id="02fef-138">Le module affiche des messages avec un horodatage au moment de leur réception.</span><span class="sxs-lookup"><span data-stu-id="02fef-138">The module prints out messages with a timestamp upon receiving them.</span></span> <span data-ttu-id="02fef-139">Vous allez créer votre premier module de passerelle personnalisé dans cette section.</span><span class="sxs-lookup"><span data-stu-id="02fef-139">You will create your first customized gateway module in this section.</span></span>

<span data-ttu-id="02fef-140">Tout module Azure IoT Edge doit implémenter les interfaces suivantes :</span><span class="sxs-lookup"><span data-stu-id="02fef-140">Any Azure IoT Edge module must implement the following interfaces:</span></span>

   ```C
   pfModule_ParseConfigurationFromJson Module_ParseConfigurationFromJson
   pfModule_FreeConfiguration Module_FreeConfiguration
   pfModule_Create Module_Create
   pfModule_Destroy Module_Destroy
   pfModule_Receive Module_Receive
   ```

<span data-ttu-id="02fef-141">Vous avez également la possibilité d’implémenter l’interface suivante :</span><span class="sxs-lookup"><span data-stu-id="02fef-141">You can optionally implement the following interface:</span></span>

   ```C
   pfModule_Start Module_Start
   ```

<span data-ttu-id="02fef-142">Le schéma suivant illustre les chemins d’état importants d’un module.</span><span class="sxs-lookup"><span data-stu-id="02fef-142">The following diagram shows the important state paths of a module.</span></span> <span data-ttu-id="02fef-143">Les rectangles représentent les méthodes que vous implémentez pour exécuter des opérations lorsque le module passe d’un état à un autre.</span><span class="sxs-lookup"><span data-stu-id="02fef-143">The square rectangles represent methods you implement to perform operations when the module moves between states.</span></span> <span data-ttu-id="02fef-144">Les ovales correspondent aux états principaux dans lesquels le module peut se trouver.</span><span class="sxs-lookup"><span data-stu-id="02fef-144">The ovals are major states the module can be in.</span></span>

![state_path](media/iot-hub-gateway-kit-lessons/lesson5/state_path.png)

<span data-ttu-id="02fef-146">Maintenant, nous allons créer un module basé sur le modèle :</span><span class="sxs-lookup"><span data-stu-id="02fef-146">Now let’s create a module based on the template:</span></span>

1. <span data-ttu-id="02fef-147">Ouvrez le dossier du modèle en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="02fef-147">Open the template folder by running the following command:</span></span>

   ```bash
   code module/my_module
   ```

   ![code_module](media/iot-hub-gateway-kit-lessons/lesson5/code_module.png)

   - <span data-ttu-id="02fef-149">`src/my_module.c` joue un rôle de modèle qui facilite la création d’un module.</span><span class="sxs-lookup"><span data-stu-id="02fef-149">`src/my_module.c` serves as a template that facilitates the creation of a module.</span></span> <span data-ttu-id="02fef-150">Le modèle déclare les interfaces.</span><span class="sxs-lookup"><span data-stu-id="02fef-150">The template declares the interfaces.</span></span> <span data-ttu-id="02fef-151">Vous avez simplement besoin d’ajouter une logique à la fonction `MyModule_Receive`.</span><span class="sxs-lookup"><span data-stu-id="02fef-151">All you need to do is to add logic to the `MyModule_Receive` function.</span></span>
   - <span data-ttu-id="02fef-152">`build.sh` est le script permettant de compiler le module sur l’Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="02fef-152">`build.sh` is the build script to compile the module on Intel NUC.</span></span>
1. <span data-ttu-id="02fef-153">Ouvrez le fichier `src/my_module.c` et incluez deux fichiers d’en-tête :</span><span class="sxs-lookup"><span data-stu-id="02fef-153">Open the `src/my_module.c` file and include two header files:</span></span>

   ```C
   #include <stdio.h>
   #include "azure_c_shared_utility/xlogging.h"
   ```

1. <span data-ttu-id="02fef-154">Ajoutez le code suivant à la fonction `MyModule_Receive` :</span><span class="sxs-lookup"><span data-stu-id="02fef-154">Add the following code to the `MyModule_Receive` function:</span></span>

   ```C
   if (message == NULL)
   {
      LogError("invalid arg message");
   }
   else
   {
      // get the message content
      const CONSTBUFFER * content = Message_GetContent(message);
      // get the local time and format it
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
                  LogError("unable to strftime");
              }
              else
              {
                  printf("[%s] %.*s\r\n", timetemp, (int)content->size, content->buffer);
              }
          }
      }
   }
   ```

1. <span data-ttu-id="02fef-155">Mettez à jour le fichier `config.json` pour spécifier le dossier `workspace` sur votre ordinateur hôte et le chemin de déploiement sur l’Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="02fef-155">Update the `config.json` file to specify the `workspace` folder on your host computer and the deployment path on Intel NUC.</span></span> <span data-ttu-id="02fef-156">Pendant la compilation, les fichiers du dossier `workspace` sont transférés vers le chemin de déploiement.</span><span class="sxs-lookup"><span data-stu-id="02fef-156">During compiling, the files in the `workspace` folder will be transferred to the deployment path.</span></span>

   1. <span data-ttu-id="02fef-157">Ouvrez le fichier `config.json` en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="02fef-157">Open the `config.json` file by running the following command:</span></span>

      ```bash
      code config.json
      ```

   1. <span data-ttu-id="02fef-158">Mettez à jour `config.json` avec la configuration suivante :</span><span class="sxs-lookup"><span data-stu-id="02fef-158">Update `config.json` with the following configuration:</span></span>

      ```json
      "workspace": "./module/my_module",
      "deploy_path": "module/my_module"
      ```

      ![config_json](media/iot-hub-gateway-kit-lessons/lesson5/config_json.png)

1. <span data-ttu-id="02fef-160">Compilez le module en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="02fef-160">Compile the module by running the following command:</span></span>

   ```bash
   gulp compile
   ```

   <span data-ttu-id="02fef-161">La commande transfère le code source à l’Intel NUC et exécute `build.sh` pour le compiler.</span><span class="sxs-lookup"><span data-stu-id="02fef-161">The command transfers the source code to Intel NUC and runs `build.sh` to compile the module.</span></span>

## <a name="add-the-module-to-the-helloworld-sample-app-and-run-the-app-on-intel-nuc"></a><span data-ttu-id="02fef-162">Ajouter le module à l’exemple d’application hello_world et exécuter l’application sur l’Intel NUC</span><span class="sxs-lookup"><span data-stu-id="02fef-162">Add the module to the hello_world sample app and run the app on Intel NUC</span></span>

<span data-ttu-id="02fef-163">Pour accomplir cette tâche, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="02fef-163">To perform this task, follow these steps:</span></span>

1. <span data-ttu-id="02fef-164">Répertoriez tous les fichiers binaires de module disponibles (fichiers .so) sur l’Intel NUC en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="02fef-164">List all the available module binaries (.so files) on Intel NUC by running the following command:</span></span>

   ```bash
   gulp modules --list
   ```

   <span data-ttu-id="02fef-165">Le chemin binaire de `my_module` que vous avez compilé doit être répertorié comme suit :</span><span class="sxs-lookup"><span data-stu-id="02fef-165">The binary path of `my_module` that you compiled should be listed as below:</span></span>

   ```path
   /root/gateway_sample/module/my_module/build/libmy_module.so
   ```

   <span data-ttu-id="02fef-166">Si vous modifiez le nom d’utilisateur de connexion par défaut dans `config-gateway.json`, le chemin binaire commencera par `home/<your username>` au lieu de `root`.</span><span class="sxs-lookup"><span data-stu-id="02fef-166">If you change the default login username in `config-gateway.json`, the binary path will start with `home/<your username>` instead of `root`.</span></span>

1. <span data-ttu-id="02fef-167">Ajoutez `my_module` à l’exemple d’application `hello_world`:</span><span class="sxs-lookup"><span data-stu-id="02fef-167">Add `my_module` to the `hello_world` sample app:</span></span>

   1. <span data-ttu-id="02fef-168">Ouvrez le fichier `hello_world.json` en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="02fef-168">Open the `hello_world.json` file by running the following command:</span></span>

      ```bash
      code sample/hello_world/src/hello_world.json
      ```

   1. <span data-ttu-id="02fef-169">Ajoutez le code suivant à la section `modules` :</span><span class="sxs-lookup"><span data-stu-id="02fef-169">Add the following code to the `modules` section:</span></span>

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

      <span data-ttu-id="02fef-170">La valeur de `module.path` doit être `/root/gateway_sample/module/my_module/build/libmy_module.so`.</span><span class="sxs-lookup"><span data-stu-id="02fef-170">The value of `module.path` should be `/root/gateway_sample/module/my_module/build/libmy_module.so`.</span></span> <span data-ttu-id="02fef-171">Le code déclare l’association de `my_module` à la passerelle, ainsi que l’emplacement du fichier binaire de module spécifié dans `module.path`.</span><span class="sxs-lookup"><span data-stu-id="02fef-171">The code declares `my_module` to be associated with the gateway as well as the location of the module binary specified in `module.path`.</span></span>
   1. <span data-ttu-id="02fef-172">Ajoutez le code suivant à la section `links` :</span><span class="sxs-lookup"><span data-stu-id="02fef-172">Add the following code to the `links` section:</span></span>

      ```json
      {
        "source": "hello_world",
        "sink": "my_module"
      }
      ```

      <span data-ttu-id="02fef-173">Ce code spécifie le transfert des messages du module `hello_world` à `my_module`.</span><span class="sxs-lookup"><span data-stu-id="02fef-173">This code specifies that messages are transferred from the `hello_world` module to `my_module`.</span></span>

      ![hello_world_json](media/iot-hub-gateway-kit-lessons/lesson5/hello_world_json.png)

1. <span data-ttu-id="02fef-175">Exécutez l’exemple d’application `hello_world` avec la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="02fef-175">Run the `hello_world` sample app by running the following command:</span></span>

   ```bash
   gulp run --config sample/hello_world/src/hello_world.json
   ```

   <span data-ttu-id="02fef-176">Le paramètre `--config` force le script `run-hello-world.js` à s’exécuter à l’aide du fichier `hello_world.json`.</span><span class="sxs-lookup"><span data-stu-id="02fef-176">The `--config` parameter forces the `run-hello-world.js` script to run by using the `hello_world.json` file.</span></span>

   ![hello_world_new](media/iot-hub-gateway-kit-lessons/lesson5/hello_world_new.png)

<span data-ttu-id="02fef-178">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="02fef-178">Congratulations.</span></span> <span data-ttu-id="02fef-179">Vous pouvez maintenant voir le comportement de ce nouveau module, qui affiche simplement des messages « hello world » avec un horodatage, résultat qui diffère de celui du module « hello_world » d’origine.</span><span class="sxs-lookup"><span data-stu-id="02fef-179">You can now see the behavior of this new module, it simply prints out "hello world" messages with a timestamp, a different result from the original "hello_world" module.</span></span>

## <a name="next-steps"></a><span data-ttu-id="02fef-180">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="02fef-180">Next Steps</span></span>

<span data-ttu-id="02fef-181">Vous avez créé un module, l’avez ajouté à l’exemple d’application hello_world et fait s’exécuter l’exemple d’application avec le nouveau module sur votre passerelle.</span><span class="sxs-lookup"><span data-stu-id="02fef-181">You’ve created a new module, added it to the hello_world sample, and get the sample app to run with the new module on your gateway.</span></span> <span data-ttu-id="02fef-182">Si vous souhaitez en savoir plus sur les modules de passerelle Azure IoT, vous trouverez d’autres exemples de modules ici : [https://github.com/Azure/azure-iot-gateway-sdk/tree/master/modules](https://github.com/Azure/azure-iot-gateway-sdk/tree/master/modules).</span><span class="sxs-lookup"><span data-stu-id="02fef-182">If you want to learn more about Azure IoT gateway modules, you can find more module samples here: [https://github.com/Azure/azure-iot-gateway-sdk/tree/master/modules](https://github.com/Azure/azure-iot-gateway-sdk/tree/master/modules).</span></span>

<!-- Images and links -->

[config_ble]: iot-hub-gateway-kit-c-lesson3-configure-ble-app.md
[setup_nuc]: iot-hub-gateway-kit-c-lesson1-set-up-nuc.md
