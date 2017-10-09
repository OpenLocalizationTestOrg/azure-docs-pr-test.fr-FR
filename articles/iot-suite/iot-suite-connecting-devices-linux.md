---
title: "aaaConnect un appareil à l’aide de C sur Linux | Documents Microsoft"
description: "Décrit comment tooconnect un toohello appareil Azure IoT Suite préconfiguré solution d’analyse à distance à l’aide d’une application écrite en C en cours d’exécution sur Linux."
services: 
suite: iot-suite
documentationcenter: na
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 0c7c8039-0bbf-4bb5-9e79-ed8cff433629
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: 57393817d40d3555177956a01fa71058bc256988
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-device-toohello-remote-monitoring-preconfigured-solution-linux"></a>Se connecter à votre solution préconfigurée (Linux) de surveillance à distance de toohello périphérique
[!INCLUDE [iot-suite-selector-connecting](../../includes/iot-suite-selector-connecting.md)]

## <a name="build-and-run-a-sample-c-client-linux"></a>Création et exécution d’un exemple de client Linux C
Hello suit vous montre comment toocreate une application cliente qui communique avec le contrôle à distance hello solution préconfigurée. Cette application est écrite en C, générée et exécutée sur Ubuntu Linux.

toocomplete ces étapes, vous devez un périphérique qui exécute la version 15.04 ou 15.10 d’Ubuntu. Avant de continuer, installez les packages de composants requis hello sur votre appareil Ubuntu à l’aide de hello de commande suivante :

```
sudo apt-get install cmake gcc g++
```

## <a name="install-hello-client-libraries-on-your-device"></a>Installer les bibliothèques clientes hello sur votre appareil
Bonjour Azure IoT Hub bibliothèques clientes sont disponibles sous forme de package que vous pouvez installer sur votre appareil Ubuntu à l’aide de hello **apt-get** commande. Hello complet suivant les étapes tooinstall hello package contenant hello bibliothèque cliente de IoT Hub et les fichiers d’en-tête sur votre ordinateur Ubuntu :

1. Dans un interpréteur de commandes, ajouter de hello AzureIoT référentiel tooyour :
   
    ```
    sudo add-apt-repository ppa:aziotsdklinux/ppa-azureiot
    sudo apt-get update
    ```
2. Installer le package d’azure-iot-sdk-c-dev hello
   
    ```
    sudo apt-get install -y azure-iot-sdk-c-dev
    ```

## <a name="install-hello-parson-json-parser"></a>Installer hello Analyseur de Parson JSON
Hello client IoT Hub bibliothèques utilisent hello charges de message tooparse Parson JSON analyseur. Dans un dossier approprié sur votre ordinateur, cloner le référentiel de Parson GitHub hello à l’aide de hello de commande suivante :

```
git clone https://github.com/kgabis/parson.git
```

## <a name="prepare-your-project"></a>Préparation du projet
Sur votre ordinateur Ubuntu, créez un dossier nommé **remote\_monitoring**. Bonjour **distant\_analyse** dossier :

- Créer des quatre fichiers hello **main.c**, **distant\_monitoring.c**, **distant\_monitoring.h**, et **CMakeLists.txt**.
- Créez un dossier nommé **parson**.

Copiez les fichiers hello **parson.c** et **parson.h** à partir de votre copie locale du référentiel de Parson hello en hello **distant\_analyse/parson** dossier.

Dans un éditeur de texte, ouvrez hello **distant\_monitoring.c** fichier. Ajoutez hello suit `#include` instructions :
   
```
#include "iothubtransportmqtt.h"
#include "schemalib.h"
#include "iothub_client.h"
#include "serializer_devicetwin.h"
#include "schemaserializer.h"
#include "azure_c_shared_utility/threadapi.h"
#include "azure_c_shared_utility/platform.h"
#include "parson.h"
```

[!INCLUDE [iot-suite-connecting-code](../../includes/iot-suite-connecting-code.md)]

## <a name="call-hello-remotemonitoringrun-function"></a>Appelez hello distant\_analyse\_exécuter (fonction)
Dans un éditeur de texte, ouvrez hello **remote_monitoring.h** fichier. Ajoutez hello suivant de code :

```
void remote_monitoring_run(void);
```

Dans un éditeur de texte, ouvrez hello **main.c** fichier. Ajoutez hello suivant de code :

```
#include "remote_monitoring.h"

int main(void)
{
    remote_monitoring_run();

    return 0;
}
```

## <a name="build-and-run-hello-application"></a>Générer et exécuter l’application hello
Hello étapes suivantes décrivent comment toouse *CMake* toobuild votre application cliente.

1. Dans un éditeur de texte, ouvrez hello **CMakeLists.txt** fichier Bonjour **remote_monitoring** dossier.

1. Ajouter hello suivant les instructions toodefine comment toobuild votre application cliente :
   
    ```
    macro(compileAsC99)
      if (CMAKE_VERSION VERSION_LESS "3.1")
        if (CMAKE_C_COMPILER_ID STREQUAL "GNU")
          set (CMAKE_C_FLAGS "--std=c99 ${CMAKE_C_FLAGS}")
          set (CMAKE_CXX_FLAGS "--std=c++11 ${CMAKE_CXX_FLAGS}")
        endif()
      else()
        set (CMAKE_C_STANDARD 99)
        set (CMAKE_CXX_STANDARD 11)
      endif()
    endmacro(compileAsC99)

    cmake_minimum_required(VERSION 2.8.11)
    compileAsC99()

    set(AZUREIOT_INC_FOLDER "${CMAKE_SOURCE_DIR}" "${CMAKE_SOURCE_DIR}/parson" "/usr/include/azureiot" "/usr/include/azureiot/inc")

    include_directories(${AZUREIOT_INC_FOLDER})

    set(sample_application_c_files
        ./parson/parson.c
        ./remote_monitoring.c
        ./main.c
    )

    set(sample_application_h_files
        ./parson/parson.h
        ./remote_monitoring.h
    )

    add_executable(sample_app ${sample_application_c_files} ${sample_application_h_files})

    target_link_libraries(sample_app
        serializer
        iothub_client
        iothub_client_mqtt_transport
        aziotsharedutil
        umqtt
        pthread
        curl
        ssl
        crypto
        m
    )
    ```
1. Bonjour **remote_monitoring** dossier, créez un Bonjour toostore de dossier *rendre* fichiers que CMake génère et puis exécutez hello **cmake** et **rendre** commandes comme suit :
   
    ```
    mkdir cmake
    cd cmake
    cmake ../
    make
    ```

1. Exécuter l’application cliente de hello et envoyer des données de télémétrie tooIoT Hub :
   
    ```
    ./sample_app
    ```

[!INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]

