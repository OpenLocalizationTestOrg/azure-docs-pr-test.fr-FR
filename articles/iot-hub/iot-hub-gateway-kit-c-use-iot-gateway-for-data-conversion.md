---
title: "conversion d’aaaData sur la passerelle IoT avec Azure IoT bord | Documents Microsoft"
description: "Utiliser IoT passerelle tooconvert hello le format de données de capteur via un module personnalisé à partir d’Azure IoT Edge."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "conversion de données de passerelle iot, transformation des données de passerelle iot"
ms.assetid: 75f2573d-500b-4405-bff7-61021c4c3500
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/25/2017
ms.author: xshi
ms.openlocfilehash: ae94b1f96f36dfcb4f77fadc0ece3cff3d0bba91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-iot-gateway-for-sensor-data-transformation-with-azure-iot-edge"></a>Utiliser une passerelle IoT pour la transformation des données de capteur avec Azure IoT Edge

> [!NOTE]
> Avant de commencer ce didacticiel, assurez-vous que vous avez terminé hello suivant les leçons dans l’ordre :
> * [Configurer Intel NUC comme passerelle IoT](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)
> * [Utilisez IoT passerelle tooconnect choses toohello cloud - SensorTag tooAzure IoT Hub](iot-hub-gateway-kit-c-iot-gateway-connect-device-to-cloud.md)

L’un des objectifs d’une passerelle Iot est tooprocess collectées données avant de les envoyer toohello cloud. Azure IoT bord présente les modules qui peuvent être créés et assemblés tooform hello le traitement des données de workflow. Un module reçoit un message, effectue une action sur celui-ci, puis déplacez-le d’autres tooprocess modules.

## <a name="what-you-learn"></a>Contenu

Vous allez apprendre comment les messages toocreate un tooconvert de module à partir de hello SensorTag dans un autre format.

## <a name="what-you-do"></a>Procédure

* Créer un module tooconvert un message reçu dans le format de .json hello.
* Compilez le module de hello.
* Ajoutez hello module toohello BLE exemple d’application à partir d’Azure IoT Edge.
* Exécutez l’exemple d’application hello.

## <a name="what-you-need"></a>Ce dont vous avez besoin

* Hello suivant didacticiels effectuées dans l’ordre :
  * [Configurer Intel NUC comme passerelle IoT](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)
  * [Utilisez IoT passerelle tooconnect choses toohello cloud - SensorTag tooAzure IoT Hub](iot-hub-gateway-kit-c-iot-gateway-connect-device-to-cloud.md)
* Un client SSH qui s’exécute sur votre ordinateur hôte. PuTTY est recommandé sur Windows. Linux et macOS sont déjà accompagnés d’un client SSH.
* adresse IP de Hello et hello nom d’utilisateur et mot de passe tooaccess hello passerelle à partir du client SSH hello.
* Une connexion Internet.

## <a name="create-a-module"></a>Création d’un module

1. Sur l’ordinateur hôte hello, exécutez hello SSH client et toohello IoT passerelle de connexion.
1. Cloner des fichiers de source de hello du module de conversion hello à partir de GitHub toohello répertoire de la passerelle de IoT hello en hello suivant les commandes en cours d’exécution :

   ```bash
   cd ~
   git clone https://github.com/Azure-Samples/iot-hub-c-intel-nuc-gateway-customized-module.git
   ```

   Il s’agit d’un module Azure bord natif écrit en langage de programmation C de hello. module de Hello convertit hello suivant un format hello de messages reçus :

   ```json
   {"deviceId": "Intel NUC Gateway", "messageId": 0, "temperature": 0.0}
   ```

## <a name="compile-hello-module"></a>Compilez le module de hello

module de hello toocompile, exécutez hello suivant de commandes :

```bash
cd iot-hub-c-intel-nuc-gateway-customized-module/my_module
# change hello build script runnable
chmod 777 build.sh
# remove hello invalid windows character
sed -i -e "s/\r$//" build.sh
# run hello build shell script
./build.sh
```

Vous obtenez un `libmy_module.so` fichier après la compilation de hello est terminée. Prenez note du chemin d’accès absolu de hello de ce fichier.

## <a name="add-hello-module-toohello-ble-sample-application"></a>Ajouter l’application d’exemple hello module toohello BLE

1. Dossier d’exemples toohello accédez en exécutant hello de commande suivante :

   ```bash
   cd /usr/share/azureiotgatewaysdk/samples
   ```

1. Ouvrez le fichier de configuration de hello en exécutant hello de commande suivante :

   ```bash
   vi ble_gateway.json
   ```

1. Ajouter un module en insérant hello suivant code toohello `modules` section.

   ```json
   {
       "name": "MyModule",
       "loader": {
           "name": "native",
           "entrypoint":{
               "module.path": "[Your libmy_module.so path]"
               }
            },
        "args": null
    },
    ```

1. Remplacez `[Your libmy_module.so path]` dans le code hello avec hello chemin d’accès absolu hello libmy_module.so' fichier.
1. Remplacez le code hello Bonjour `links` section avec hello suivant un :

   ```json
   {
       "source": "SensorTag",
       "sink": "MyModule"
   },
   {
       "source": "MyModule",
       "sink": "mapping"
   }
   ```

1. Appuyez sur `ESC`, puis tapez `:wq` fichier hello de toosave.

## <a name="run-hello-sample-application"></a>Exécutez l’exemple d’application hello

1. Mise sous tension hello SensorTag.
1. Définir la variable d’environnement SSL_CERT_FILE hello en exécutant hello de commande suivante :

   ```bash
   export SSL_CERT_FILE=/etc/ssl/certs/ca-certificates.crt
   ```

1. Exécuter l’exemple d’application hello avec le module ajouté hello en exécutant hello commande suivante :

   ```bash
   ./ble_gateway ble_gateway.json
   ```

## <a name="next-steps"></a>Étapes suivantes

Vous avez correctement utilisation hello IoT passerelle tooconvert message d’appel de SensorTag au format de .json hello.

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
