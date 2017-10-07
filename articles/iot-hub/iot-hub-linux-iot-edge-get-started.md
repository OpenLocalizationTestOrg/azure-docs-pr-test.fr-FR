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
# <a name="explore-azure-iot-edge-architecture-on-linux"></a>Explorer l’architecture de Azure IoT Edge sur Linux

[!INCLUDE [iot-hub-iot-edge-getstarted-selector](../../includes/iot-hub-iot-edge-getstarted-selector.md)]

[!INCLUDE [iot-hub-iot-edge-install-build-linux](../../includes/iot-hub-iot-edge-install-build-linux.md)]

## <a name="how-toorun-hello-sample"></a>Comment toorun hello exemple

Hello **build.sh** script génère sa sortie dans hello **générer** dossier dans votre copie locale de hello **iot-bord** référentiel. Cette sortie inclut deux modules de IoT bord hello utilisés dans cet exemple.

Hello endroits du script build **liblogger.so** Bonjour **/modules/journal de build/** dossier et **libhello\_world.so** Bonjour **générer / modules/Bonjour_monde/** dossier. Utilisez ces chemins d’accès pour hello **chemin du module** valeurs comme indiqué dans hello suivant l’exemple de fichier de paramètres JSON.

Bonjour Bonjour\_world\_exemple dure fichier de configuration JSON hello chemin tooa un argument de ligne de commande. exemple de fichier JSON suivant Hello est fourni dans le référentiel du Kit de développement logiciel hello à **exemples/hello\_world/src/hello\_world\_lin.json**. Ce fonctionne de fichier de configuration en l’état, sauf si vous modifiez hello construire des modules hello tooplace de script IoT bord ou un échantillon exécutables dans les emplacements par défaut.

> [!NOTE]
> répertoire de travail actuel relatif toohello à partir de laquelle sont Hello chemins d’accès du module Bonjour Bonjour\_world\_exécutable de l’exemple est lancé, pas hello répertoire où se trouve hello exécutable. exemple Hello JSON configuration fichier par défaut toowriting 'log.txt » dans votre répertoire de travail actuel.

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

1. Accédez toohello **générer** dossier racine hello de votre copie locale de hello **iot-bord** référentiel.

1. Exécutez hello de commande suivante :

    ```sh
    ./samples/hello_world/hello_world_sample ../samples/hello_world/src/hello_world_lin.json`
    ```

[!INCLUDE [iot-hub-iot-edge-getstarted-code](../../includes/iot-hub-iot-edge-getstarted-code.md)]

