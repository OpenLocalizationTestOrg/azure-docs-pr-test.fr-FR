---
title: aaaGet en main Azure IoT Edge (Windows) | Documents Microsoft
description: "Comment toobuild une passerelle Azure IoT sur un Windows de l’ordinateur et en savoir plus sur les concepts clés dans Azure IoT Edge tels que les modules et les fichiers de configuration JSON."
services: iot-hub
documentationcenter: 
author: chipalost
manager: timlt
editor: 
ms.assetid: 9aff3724-5e4e-40ec-b95a-d00df4f590c5
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/07/2017
ms.author: andbuc
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 5dd13cbfc02eeb55d9f2dbffca5021f2624acf14
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="explore-azure-iot-edge-architecture-on-windows"></a><span data-ttu-id="d0ec9-103">Explorer l’architecture de Azure IoT Edge sur Windows</span><span class="sxs-lookup"><span data-stu-id="d0ec9-103">Explore Azure IoT Edge architecture on Windows</span></span>

[!INCLUDE [iot-hub-iot-edge-getstarted-selector](../../includes/iot-hub-iot-edge-getstarted-selector.md)]

[!INCLUDE [iot-hub-iot-edge-install-build-windows](../../includes/iot-hub-iot-edge-install-build-windows.md)]

## <a name="how-toorun-hello-sample"></a><span data-ttu-id="d0ec9-104">Comment toorun hello exemple</span><span class="sxs-lookup"><span data-stu-id="d0ec9-104">How toorun hello sample</span></span>

<span data-ttu-id="d0ec9-105">Hello **build.cmd** script génère sa sortie dans hello **générer** dossier dans votre copie locale de hello **iot-bord** référentiel.</span><span class="sxs-lookup"><span data-stu-id="d0ec9-105">hello **build.cmd** script generates its output in hello **build** folder in your local copy of hello **iot-edge** repository.</span></span> <span data-ttu-id="d0ec9-106">Cette sortie inclut deux modules de IoT bord hello utilisés dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="d0ec9-106">This output includes hello two IoT Edge modules used in this sample.</span></span>

<span data-ttu-id="d0ec9-107">Hello endroits du script build **logger.dll** Bonjour **générer\\modules\\journal\\déboguer** dossier et **hello\_world.dll**  Bonjour **générer\\modules\\Bonjour_monde\\déboguer** dossier.</span><span class="sxs-lookup"><span data-stu-id="d0ec9-107">hello build script places **logger.dll** in hello **build\\modules\\logger\\Debug** folder and **hello\_world.dll** in hello **build\\modules\\hello_world\\Debug** folder.</span></span> <span data-ttu-id="d0ec9-108">Utilisez ces chemins d’accès pour hello **chemin du module** valeurs comme indiqué dans hello suivant du fichier de paramètres JSON.</span><span class="sxs-lookup"><span data-stu-id="d0ec9-108">Use these paths for hello **module path** values as shown in hello following JSON settings file.</span></span>

<span data-ttu-id="d0ec9-109">Bonjour Bonjour\_world\_exemple de processus prend le fichier de configuration hello chemin d’accès tooa JSON comme un argument de ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="d0ec9-109">hello hello\_world\_sample process takes hello path tooa JSON configuration file as a command-line argument.</span></span> <span data-ttu-id="d0ec9-110">exemple de fichier JSON suivant Hello est fourni dans le référentiel du Kit de développement logiciel hello à **exemples\\hello\_world\\src\\hello\_world\_win.json**.</span><span class="sxs-lookup"><span data-stu-id="d0ec9-110">hello following example JSON file is provided in hello SDK repository at **samples\\hello\_world\\src\\hello\_world\_win.json**.</span></span> <span data-ttu-id="d0ec9-111">Ce fonctionne de fichier de configuration en l’état, sauf si vous modifiez hello construire des modules hello tooplace de script IoT bord ou un échantillon exécutables dans les emplacements par défaut.</span><span class="sxs-lookup"><span data-stu-id="d0ec9-111">This configuration file works as is unless you modify hello build script tooplace hello IoT Edge modules or sample executables in non-default locations.</span></span>

> [!NOTE]
> <span data-ttu-id="d0ec9-112">chemins d’accès du module de Hello sont toohello relatif répertoire où hello hello\_world\_sample.exe se trouve.</span><span class="sxs-lookup"><span data-stu-id="d0ec9-112">hello module paths are relative toohello directory where hello hello\_world\_sample.exe is located.</span></span> <span data-ttu-id="d0ec9-113">exemple Hello JSON configuration fichier par défaut toowriting 'log.txt » dans votre répertoire de travail actuel.</span><span class="sxs-lookup"><span data-stu-id="d0ec9-113">hello sample JSON configuration file defaults toowriting 'log.txt' in your current working directory.</span></span>

```json
{
  "modules": [
    {
      "name": "logger",
      "loader": {
        "name": "native",
        "entrypoint": {
          "module.path": "..\\..\\..\\modules\\logger\\Debug\\logger.dll"
        }
      },
      "args": { "filename": "log.txt" }
    },
    {
      "name": "hello_world",
      "loader": {
        "name": "native",
        "entrypoint": {
          "module.path": "..\\..\\..\\modules\\hello_world\\Debug\\hello_world.dll"
        }
      },
      "args": null
      }
  ],
  "links": [
    {
      "source": "hello_world",
      "sink": "logger"
    }
  ]
}
```

1. <span data-ttu-id="d0ec9-114">Accédez toohello **générer** dossier racine hello de votre copie locale de hello **iot-bord** référentiel.</span><span class="sxs-lookup"><span data-stu-id="d0ec9-114">Navigate toohello **build** folder in hello root of your local copy of hello **iot-edge** repository.</span></span>

1. <span data-ttu-id="d0ec9-115">Exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="d0ec9-115">Run hello following command:</span></span>

    ```cmd
    samples\hello_world\Debug\hello_world_sample.exe ..\samples\hello_world\src\hello_world_win.json
    ```

[!INCLUDE [iot-hub-iot-edge-getstarted-code](../../includes/iot-hub-iot-edge-getstarted-code.md)]
