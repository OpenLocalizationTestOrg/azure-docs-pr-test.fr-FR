---
title: "Prise en main d’Azure IoT Edge (Windows) | Microsoft Docs"
description: "Comment créer une passerelle Azure IoT Edge sur une machine Windows et en savoir plus sur les concepts clés dans Azure IoT Edge, comme les modules et les fichiers de configuration JSON."
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
ms.openlocfilehash: 5db39bab8e31a8e7026b34e72b4614b0f6f57772
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="explore-azure-iot-edge-architecture-on-windows"></a><span data-ttu-id="c72cc-103">Explorer l’architecture de Azure IoT Edge sur Windows</span><span class="sxs-lookup"><span data-stu-id="c72cc-103">Explore Azure IoT Edge architecture on Windows</span></span>

[!INCLUDE [iot-hub-iot-edge-getstarted-selector](../../includes/iot-hub-iot-edge-getstarted-selector.md)]

[!INCLUDE [iot-hub-iot-edge-install-build-windows](../../includes/iot-hub-iot-edge-install-build-windows.md)]

## <a name="how-to-run-the-sample"></a><span data-ttu-id="c72cc-104">Comment exécuter l’exemple</span><span class="sxs-lookup"><span data-stu-id="c72cc-104">How to run the sample</span></span>

<span data-ttu-id="c72cc-105">Le script **build.cmd** génère sa sortie dans le dossier **build** de votre copie locale du référentiel **iot-edge**.</span><span class="sxs-lookup"><span data-stu-id="c72cc-105">The **build.cmd** script generates its output in the **build** folder in your local copy of the **iot-edge** repository.</span></span> <span data-ttu-id="c72cc-106">Cette sortie inclut les deux modules IoT Edge utilisés dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="c72cc-106">This output includes the two IoT Edge modules used in this sample.</span></span>

<span data-ttu-id="c72cc-107">Le script de génération place **logger.dll** dans le dossier **build\\modules\\logger\\Debug**, et **hello\_world.dll** dans le dossier **build\\modules\\hello_world\\Debug**.</span><span class="sxs-lookup"><span data-stu-id="c72cc-107">The build script places **logger.dll** in the **build\\modules\\logger\\Debug** folder and **hello\_world.dll** in the **build\\modules\\hello_world\\Debug** folder.</span></span> <span data-ttu-id="c72cc-108">Utilisez ces chemins pour les valeurs de **module path** comme indiqué dans le fichier de paramètres JSON suivant.</span><span class="sxs-lookup"><span data-stu-id="c72cc-108">Use these paths for the **module path** values as shown in the following JSON settings file.</span></span>

<span data-ttu-id="c72cc-109">Le processus hello\_world\_sample utilise le chemin vers un fichier de configuration JSON comme argument de ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="c72cc-109">The hello\_world\_sample process takes the path to a JSON configuration file as a command-line argument.</span></span> <span data-ttu-id="c72cc-110">L’exemple de fichier JSON suivant est fourni dans le référentiel du SDK dans **samples\\hello\_world\\src\\hello\_world\_wlin.json**.</span><span class="sxs-lookup"><span data-stu-id="c72cc-110">The following example JSON file is provided in the SDK repository at **samples\\hello\_world\\src\\hello\_world\_win.json**.</span></span> <span data-ttu-id="c72cc-111">Ce fichier config fonctionne comme tel, sauf si vous modifiez le script de build pour placer les modules IoT Edge ou des exemples d’exécutables dans des emplacements autres que ceux par défaut.</span><span class="sxs-lookup"><span data-stu-id="c72cc-111">This configuration file works as is unless you modify the build script to place the IoT Edge modules or sample executables in non-default locations.</span></span>

> [!NOTE]
> <span data-ttu-id="c72cc-112">Les chemins de module sont relatif au répertoire où se trouve le fichier hello\_world\_sample.exe.</span><span class="sxs-lookup"><span data-stu-id="c72cc-112">The module paths are relative to the directory where the hello\_world\_sample.exe is located.</span></span> <span data-ttu-id="c72cc-113">L’exemple de fichier de configuration JSON écrit par défaut « log.txt » dans votre répertoire de travail actuel.</span><span class="sxs-lookup"><span data-stu-id="c72cc-113">The sample JSON configuration file defaults to writing 'log.txt' in your current working directory.</span></span>

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

1. <span data-ttu-id="c72cc-114">Accédez au dossier **build** à la racine de votre copie locale du référentiel **iot-edge**.</span><span class="sxs-lookup"><span data-stu-id="c72cc-114">Navigate to the **build** folder in the root of your local copy of the **iot-edge** repository.</span></span>

1. <span data-ttu-id="c72cc-115">Exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="c72cc-115">Run the following command:</span></span>

    ```cmd
    samples\hello_world\Debug\hello_world_sample.exe ..\samples\hello_world\src\hello_world_win.json
    ```

[!INCLUDE [iot-hub-iot-edge-getstarted-code](../../includes/iot-hub-iot-edge-getstarted-code.md)]
