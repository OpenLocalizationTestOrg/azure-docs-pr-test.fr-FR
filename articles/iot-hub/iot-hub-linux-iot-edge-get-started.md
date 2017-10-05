---
title: "Prise en main d’Azure IoT Edge (Linux) | Microsoft Docs"
description: "Comment créer une passerelle sur une machine Linux et en savoir plus sur les concepts clés dans Azure IoT Edge, comme les modules et les fichiers de configuration JSON."
services: iot-hub
documentationcenter: 
author: chipalost
manager: timlt
editor: 
ms.assetid: cf537bdd-2352-4bb1-96cd-a283fcd3d6cf
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/07/2017
ms.author: andbuc
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b02d79fcd9cd2a2ef0041aac4e85528263c8d58a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="explore-azure-iot-edge-architecture-on-linux"></a><span data-ttu-id="d71b9-103">Explorer l’architecture de Azure IoT Edge sur Linux</span><span class="sxs-lookup"><span data-stu-id="d71b9-103">Explore Azure IoT Edge architecture on Linux</span></span>

[!INCLUDE [iot-hub-iot-edge-getstarted-selector](../../includes/iot-hub-iot-edge-getstarted-selector.md)]

[!INCLUDE [iot-hub-iot-edge-install-build-linux](../../includes/iot-hub-iot-edge-install-build-linux.md)]

## <a name="how-to-run-the-sample"></a><span data-ttu-id="d71b9-104">Comment exécuter l’exemple</span><span class="sxs-lookup"><span data-stu-id="d71b9-104">How to run the sample</span></span>

<span data-ttu-id="d71b9-105">Le script **build.sh** génère sa sortie dans le dossier **build** de votre copie locale du référentiel **iot-edge**.</span><span class="sxs-lookup"><span data-stu-id="d71b9-105">The **build.sh** script generates its output in the **build** folder in your local copy of the **iot-edge** repository.</span></span> <span data-ttu-id="d71b9-106">Cette sortie inclut les deux modules IoT Edge utilisés dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="d71b9-106">This output includes the two IoT Edge modules used in this sample.</span></span>

<span data-ttu-id="d71b9-107">Le script place **liblogger.so** dans le dossier **build/modules/logger/** et **libhello\_world.so** dans le dossier **build/modules/hello_world/**.</span><span class="sxs-lookup"><span data-stu-id="d71b9-107">The build script places **liblogger.so** in the **build/modules/logger/** folder and **libhello\_world.so** in the **build/modules/hello_world/** folder.</span></span> <span data-ttu-id="d71b9-108">Utilisez ces chemins d’accès pour les valeurs **module path** comme indiqué dans le fichier d’exemple de paramètres JSON suivant.</span><span class="sxs-lookup"><span data-stu-id="d71b9-108">Use these paths for the **module path** values as shown in the following example JSON settings file.</span></span>

<span data-ttu-id="d71b9-109">Le processus hello\_world\_sample utilise le chemin d’accès à un fichier de configuration JSON en tant qu’argument de ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="d71b9-109">The hello\_world\_sample process takes the path to a JSON configuration file a command-line argument.</span></span> <span data-ttu-id="d71b9-110">Le fichier d’exemple JSON suivant est fourni dans le référentiel du Kit de développement logiciel (SDK) à **samples/hello\_world/src/hello\_world\_lin.json**.</span><span class="sxs-lookup"><span data-stu-id="d71b9-110">The following example JSON file is provided in the SDK repository at **samples/hello\_world/src/hello\_world\_lin.json**.</span></span> <span data-ttu-id="d71b9-111">Ce fichier de configuration fonctionne comme tel, sauf si vous modifiez le script build pour placer des modules IoT Edge ou des exécutables de l’exemple dans des emplacements autres que ceux par défaut.</span><span class="sxs-lookup"><span data-stu-id="d71b9-111">This configuration file works as is unless you modify the build script to place the IoT Edge modules or sample executables in non-default locations.</span></span>

> [!NOTE]
> <span data-ttu-id="d71b9-112">Les chemins d’accès du module sont relatifs au répertoire de travail actuel à partir duquel l’exécutable hello\_world\_sample est lancé, et non au répertoire où se trouve l’exécutable.</span><span class="sxs-lookup"><span data-stu-id="d71b9-112">The module paths are relative to the current working directory from where the hello\_world\_sample executable is launched, not the directory where the executable is located.</span></span> <span data-ttu-id="d71b9-113">L’exemple de fichier de configuration JSON écrit par défaut « log.txt » dans votre répertoire de travail actuel.</span><span class="sxs-lookup"><span data-stu-id="d71b9-113">The sample JSON configuration file defaults to writing 'log.txt' in your current working directory.</span></span>

```json
{
    "modules" :
    [
        {
            "name" : "logger",
            "loader": {
            "name": "native",
            "entrypoint": {
                "module.path": "./modules/logger/liblogger.so"
            }
            },
            "args" : {"filename":"log.txt"}
        },
        {
            "name" : "hello_world",
            "loader": {
            "name": "native",
            "entrypoint": {
                "module.path": "./modules/hello_world/libhello_world.so"
            }
            },
            "args" : null
        }
    ],
    "links":
    [
        {
            "source": "hello_world",
            "sink": "logger"
        }
    ]
}
```

1. <span data-ttu-id="d71b9-114">Accédez au dossier **build** à la racine de votre copie locale du référentiel **iot-edge**.</span><span class="sxs-lookup"><span data-stu-id="d71b9-114">Navigate to the **build** folder in the root of your local copy of the **iot-edge** repository.</span></span>

1. <span data-ttu-id="d71b9-115">Exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="d71b9-115">Run the following command:</span></span>

    ```sh
    ./samples/hello_world/hello_world_sample ../samples/hello_world/src/hello_world_lin.json`
    ```

[!INCLUDE [iot-hub-iot-edge-getstarted-code](../../includes/iot-hub-iot-edge-getstarted-code.md)]

