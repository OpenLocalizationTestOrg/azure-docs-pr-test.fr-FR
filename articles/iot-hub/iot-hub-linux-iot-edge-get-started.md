---
title: aaaGet en main Azure IoT Edge (Linux) | Documents Microsoft
description: "Comment toobuild une passerelle sur une Linux de l’ordinateur et en savoir plus sur les concepts clés dans Azure IoT Edge tels que les modules et les fichiers de configuration JSON."
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
ms.openlocfilehash: 40aa9c8ddca6a974c361cbb0b453c7d0ddc71b8d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="explore-azure-iot-edge-architecture-on-linux"></a><span data-ttu-id="dfc4d-103">Explorer l’architecture de Azure IoT Edge sur Linux</span><span class="sxs-lookup"><span data-stu-id="dfc4d-103">Explore Azure IoT Edge architecture on Linux</span></span>

[!INCLUDE [iot-hub-iot-edge-getstarted-selector](../../includes/iot-hub-iot-edge-getstarted-selector.md)]

[!INCLUDE [iot-hub-iot-edge-install-build-linux](../../includes/iot-hub-iot-edge-install-build-linux.md)]

## <a name="how-toorun-hello-sample"></a><span data-ttu-id="dfc4d-104">Comment toorun hello exemple</span><span class="sxs-lookup"><span data-stu-id="dfc4d-104">How toorun hello sample</span></span>

<span data-ttu-id="dfc4d-105">Hello **build.sh** script génère sa sortie dans hello **générer** dossier dans votre copie locale de hello **iot-bord** référentiel.</span><span class="sxs-lookup"><span data-stu-id="dfc4d-105">hello **build.sh** script generates its output in hello **build** folder in your local copy of hello **iot-edge** repository.</span></span> <span data-ttu-id="dfc4d-106">Cette sortie inclut deux modules de IoT bord hello utilisés dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="dfc4d-106">This output includes hello two IoT Edge modules used in this sample.</span></span>

<span data-ttu-id="dfc4d-107">Hello endroits du script build **liblogger.so** Bonjour **/modules/journal de build/** dossier et **libhello\_world.so** Bonjour **générer / modules/Bonjour_monde/** dossier.</span><span class="sxs-lookup"><span data-stu-id="dfc4d-107">hello build script places **liblogger.so** in hello **build/modules/logger/** folder and **libhello\_world.so** in hello **build/modules/hello_world/** folder.</span></span> <span data-ttu-id="dfc4d-108">Utilisez ces chemins d’accès pour hello **chemin du module** valeurs comme indiqué dans hello suivant l’exemple de fichier de paramètres JSON.</span><span class="sxs-lookup"><span data-stu-id="dfc4d-108">Use these paths for hello **module path** values as shown in hello following example JSON settings file.</span></span>

<span data-ttu-id="dfc4d-109">Bonjour Bonjour\_world\_exemple dure fichier de configuration JSON hello chemin tooa un argument de ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="dfc4d-109">hello hello\_world\_sample process takes hello path tooa JSON configuration file a command-line argument.</span></span> <span data-ttu-id="dfc4d-110">exemple de fichier JSON suivant Hello est fourni dans le référentiel du Kit de développement logiciel hello à **exemples/hello\_world/src/hello\_world\_lin.json**.</span><span class="sxs-lookup"><span data-stu-id="dfc4d-110">hello following example JSON file is provided in hello SDK repository at **samples/hello\_world/src/hello\_world\_lin.json**.</span></span> <span data-ttu-id="dfc4d-111">Ce fonctionne de fichier de configuration en l’état, sauf si vous modifiez hello construire des modules hello tooplace de script IoT bord ou un échantillon exécutables dans les emplacements par défaut.</span><span class="sxs-lookup"><span data-stu-id="dfc4d-111">This configuration file works as is unless you modify hello build script tooplace hello IoT Edge modules or sample executables in non-default locations.</span></span>

> [!NOTE]
> <span data-ttu-id="dfc4d-112">répertoire de travail actuel relatif toohello à partir de laquelle sont Hello chemins d’accès du module Bonjour Bonjour\_world\_exécutable de l’exemple est lancé, pas hello répertoire où se trouve hello exécutable.</span><span class="sxs-lookup"><span data-stu-id="dfc4d-112">hello module paths are relative toohello current working directory from where hello hello\_world\_sample executable is launched, not hello directory where hello executable is located.</span></span> <span data-ttu-id="dfc4d-113">exemple Hello JSON configuration fichier par défaut toowriting 'log.txt » dans votre répertoire de travail actuel.</span><span class="sxs-lookup"><span data-stu-id="dfc4d-113">hello sample JSON configuration file defaults toowriting 'log.txt' in your current working directory.</span></span>

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

1. <span data-ttu-id="dfc4d-114">Accédez toohello **générer** dossier racine hello de votre copie locale de hello **iot-bord** référentiel.</span><span class="sxs-lookup"><span data-stu-id="dfc4d-114">Navigate toohello **build** folder in hello root of your local copy of hello **iot-edge** repository.</span></span>

1. <span data-ttu-id="dfc4d-115">Exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="dfc4d-115">Run hello following command:</span></span>

    ```sh
    ./samples/hello_world/hello_world_sample ../samples/hello_world/src/hello_world_lin.json`
    ```

[!INCLUDE [iot-hub-iot-edge-getstarted-code](../../includes/iot-hub-iot-edge-getstarted-code.md)]

