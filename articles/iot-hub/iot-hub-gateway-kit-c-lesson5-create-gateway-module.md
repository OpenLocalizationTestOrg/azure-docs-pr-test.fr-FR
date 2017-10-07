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
# <a name="lesson-5-create-your-first-azure-iot-gateway-module"></a>Leçon 5 : Créer votre premier module de passerelle Azure IoT
Azure IoT bord vous permet de modules toobuild écrits en Java, .NET ou Node.js, ce didacticiel vous guide à travers les étapes de hello pour la création d’un module en C.

## <a name="what-you-will-do"></a>Procédure à suivre

- Compilez et exécutez l’application d’exemple hello Bonjour_monde sur Intel NUC.
- Créez un module et compilez-le sur l’Intel NUC.
- Ajouter hello nouveau module toohello Bonjour_monde exemple d’application, puis exécutez exemple hello sur NUC d’Intel. nouveau module de Hello imprime les messages « Bonjour_monde » avec un horodatage.

## <a name="what-you-will-learn"></a>Contenu

- Comment toocompile et exécuter un exemple d’application sur NUC d’Intel.
- Comment toocreate un module.
- Comment tooadd module tooa exemple d’application.

## <a name="what-you-need"></a>Ce dont vous avez besoin

Azure IoT Edge installé sur votre ordinateur hôte.

## <a name="folder-structure"></a>Structure de dossiers

Dans le sous-dossier hello leçon 5 de l’exemple de code hello que vous avez cloné dans la leçon 1, il existe un `module` dossier et un `sample` dossier.

![my_module](media/iot-hub-gateway-kit-lessons/lesson5/my_module.png)

- Hello `module/my_module` dossier contient hello code et le script toobuild hello module de source.
- Hello `sample` dossier contient hello source code et le script toobuild hello exemple d’application.

## <a name="compile-and-run-hello-helloworld-sample-app-on-intel-nuc"></a>Compiler et exécuter l’application d’exemple hello Bonjour_monde sur Intel NUC

Hello `hello_world` exemple crée une passerelle selon hello `hello_world.json` fichier qui spécifie les modules prédéfinis deux hello associés application hello. passerelle de Hello enregistre toutes les 5 secondes à un fichier de tooa de message « hello world ». Dans cette section, vous compilez et exécutez hello `hello_world` application avec son module par défaut.

hello toocompile et exécutez `hello_world` application, procédez comme suit sur votre ordinateur hôte :

1. Initialiser les fichiers de configuration hello en hello suivant les commandes en cours d’exécution :

   ```bash
   cd iot-hub-c-intel-nuc-gateway-getting-started
   cd Lesson5
   npm install
   gulp init
   ```

1. Mettre à jour le fichier de configuration de passerelle hello avec hello adresse MAC d’Intel NUC. Ignorez cette étape si vous avez parcouru leçon de hello trop[configurer et exécuter un exemple d’application BLE][config_ble].

   1. Ouvrez le fichier de configuration de passerelle de hello en exécutant hello de commande suivante :

      ```bash
      # For Windows command prompt
      code %USERPROFILE%\.iot-hub-getting-started\config-gateway.json

      # For MacOS or Ubuntu
      code ~/.iot-hub-getting-started/config-gateway.json
      ```

   1. D’adresses MAC de la passerelle de mise à jour hello lorsque vous [configurer NUC Intel comme passerelle IoT][setup_nuc], puis enregistrez le fichier de hello.

1. Compilez les exemples de code source hello en exécutant hello de commande suivante :

   ```bash
   gulp compile
   ```

   transfère la source d’exemple hello tooIntel code NUC Hello commande et exécute `build.sh` toocompile il.

1. Exécutez hello `hello_world` application sur Intel NUC en exécutant hello de commande suivante :

   ```bash
   gulp run
   ```

   Hello s’exécute la commande `../Tools/run-hello-world.js` qui est spécifié dans `config.json` toostart hello exemple d’application sur NUC d’Intel.

   ![run_sample](media/iot-hub-gateway-kit-lessons/lesson5/run_sample.png)

## <a name="create-a-new-module-and-compile-it-on-intel-nuc"></a>Créer un module et le compiler sur l’Intel NUC

étapes Hello ci-dessous vous guident dans la création d’un nouveau module et le compiler sur NUC d’Intel. module de Hello imprime les messages avec un horodatage lors de leur réception. Vous allez créer votre premier module de passerelle personnalisé dans cette section.

N’importe quel module Azure IoT Edge doit implémenter hello suivant des interfaces :

   ```C
   pfModule_ParseConfigurationFromJson Module_ParseConfigurationFromJson
   pfModule_FreeConfiguration Module_FreeConfiguration
   pfModule_Create Module_Create
   pfModule_Destroy Module_Destroy
   pfModule_Receive Module_Receive
   ```

Vous pouvez implémenter hello suivant interface :

   ```C
   pfModule_Start Module_Start
   ```

Hello diagramme suivant montre chemins d’accès de hello état importants d’un module. les rectangles carré Hello représentent des méthodes que vous implémentez les opérations tooperform lorsque le module de hello se déplace entre les États. ovales de Hello sont les principaux États module de hello.

![state_path](media/iot-hub-gateway-kit-lessons/lesson5/state_path.png)

Maintenant nous allons créer un module basé sur le modèle de hello :

1. Ouvrez le dossier de modèle de hello en exécutant hello de commande suivante :

   ```bash
   code module/my_module
   ```

   ![code_module](media/iot-hub-gateway-kit-lessons/lesson5/code_module.png)

   - `src/my_module.c`sert de modèle qui facilite la création d’un module hello. modèle de Hello déclare les interfaces hello. Il vous suffit de toodo est tooadd logique toohello `MyModule_Receive` (fonction).
   - `build.sh`est hello build script toocompile hello module NUC d’Intel.
1. Ouvrez hello `src/my_module.c` de fichiers et d’inclure les deux fichiers d’en-tête :

   ```C
   #include <stdio.h>
   #include "azure_c_shared_utility/xlogging.h"
   ```

1. Ajouter hello suivant code toohello `MyModule_Receive` fonction :

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

1. Hello de mise à jour `config.json` hello toospecify de fichier `workspace` dossier sur votre ordinateur et hello déploiement chemin vers l’hôte sur NUC d’Intel. Pendant la compilation, hello fichiers Bonjour `workspace` dossier seront transférées toohello le chemin de déploiement.

   1. Ouvrez hello `config.json` fichier en exécutant hello de commande suivante :

      ```bash
      code config.json
      ```

   1. Mise à jour `config.json` avec hello configuration suivante :

      ```json
      "workspace": "./module/my_module",
      "deploy_path": "module/my_module"
      ```

      ![config_json](media/iot-hub-gateway-kit-lessons/lesson5/config_json.png)

1. Compilez le module de hello en exécutant hello de commande suivante :

   ```bash
   gulp compile
   ```

   transfère hello source code tooIntel NUC Hello commande et exécute `build.sh` module de hello toocompile.

## <a name="add-hello-module-toohello-helloworld-sample-app-and-run-hello-app-on-intel-nuc"></a>Ajouter hello module toohello Bonjour_monde exemple d’application et exécutez l’application hello sur Intel NUC

tooperform cette tâche, procédez comme suit :

1. Répertorier tous les binaires de module disponible hello (fichiers .so) sur Intel NUC en exécutant hello de commande suivante :

   ```bash
   gulp modules --list
   ```

   Hello chemin d’accès binaire `my_module` que vous avez compilé doit être répertorié comme ci-dessous :

   ```path
   /root/gateway_sample/module/my_module/build/libmy_module.so
   ```

   Si vous modifiez le nom d’utilisateur du compte de connexion par défaut hello dans `config-gateway.json`, chemin d’accès binaire de hello démarrera avec `home/<your username>` au lieu de `root`.

1. Ajouter `my_module` toohello `hello_world` exemple d’application :

   1. Ouvrez hello `hello_world.json` fichier en exécutant hello de commande suivante :

      ```bash
      code sample/hello_world/src/hello_world.json
      ```

   1. Ajouter hello suivant code toohello `modules` section :

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

      Hello valeur `module.path` doit être `/root/gateway_sample/module/my_module/build/libmy_module.so`. code de Hello déclare `my_module` toobe associée passerelle de hello ainsi que d’emplacement hello du fichier binaire du module hello spécifié dans `module.path`.
   1. Ajouter hello suivant code toohello `links` section :

      ```json
      {
        "source": "hello_world",
        "sink": "my_module"
      }
      ```

      Ce code spécifie que les messages sont transférés de hello `hello_world` module trop`my_module`.

      ![hello_world_json](media/iot-hub-gateway-kit-lessons/lesson5/hello_world_json.png)

1. Exécutez hello `hello_world` exemple d’application en exécutant hello de commande suivante :

   ```bash
   gulp run --config sample/hello_world/src/hello_world.json
   ```

   Hello `--config` paramètre force hello `run-hello-world.js` toorun de script à l’aide de hello `hello_world.json` fichier.

   ![hello_world_new](media/iot-hub-gateway-kit-lessons/lesson5/hello_world_new.png)

Félicitations ! Vous pouvez maintenant voir le comportement de hello ce nouveau module, il imprime simplement les messages « hello world » avec un horodatage, un résultat différent d’un module hello d’origine « Bonjour_monde ».

## <a name="next-steps"></a>Étapes suivantes

Vous avez créé un nouveau module, ajouté toohello Bonjour_monde exemple et get hello exemple application toorun avec le nouveau module de hello sur votre passerelle. Si vous souhaitez toolearn plus d’informations sur les modules de passerelle Azure IoT, vous trouverez d’autres exemples de module ici : [https://github.com/Azure/azure-iot-gateway-sdk/tree/master/modules](https://github.com/Azure/azure-iot-gateway-sdk/tree/master/modules).

<!-- Images and links -->

[config_ble]: iot-hub-gateway-kit-c-lesson3-configure-ble-app.md
[setup_nuc]: iot-hub-gateway-kit-c-lesson1-set-up-nuc.md
