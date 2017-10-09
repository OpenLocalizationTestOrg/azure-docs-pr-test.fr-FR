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
# <a name="connect-your-device-toohello-remote-monitoring-preconfigured-solution-linux"></a><span data-ttu-id="9cd2f-103">Se connecter à votre solution préconfigurée (Linux) de surveillance à distance de toohello périphérique</span><span class="sxs-lookup"><span data-stu-id="9cd2f-103">Connect your device toohello remote monitoring preconfigured solution (Linux)</span></span>
[!INCLUDE [iot-suite-selector-connecting](../../includes/iot-suite-selector-connecting.md)]

## <a name="build-and-run-a-sample-c-client-linux"></a><span data-ttu-id="9cd2f-104">Création et exécution d’un exemple de client Linux C</span><span class="sxs-lookup"><span data-stu-id="9cd2f-104">Build and run a sample C client Linux</span></span>
<span data-ttu-id="9cd2f-105">Hello suit vous montre comment toocreate une application cliente qui communique avec le contrôle à distance hello solution préconfigurée.</span><span class="sxs-lookup"><span data-stu-id="9cd2f-105">hello following steps show you how toocreate a client application that communicates with hello remote monitoring preconfigured solution.</span></span> <span data-ttu-id="9cd2f-106">Cette application est écrite en C, générée et exécutée sur Ubuntu Linux.</span><span class="sxs-lookup"><span data-stu-id="9cd2f-106">This application is written in C and built and run on Ubuntu Linux.</span></span>

<span data-ttu-id="9cd2f-107">toocomplete ces étapes, vous devez un périphérique qui exécute la version 15.04 ou 15.10 d’Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="9cd2f-107">toocomplete these steps, you need a device running Ubuntu version 15.04 or 15.10.</span></span> <span data-ttu-id="9cd2f-108">Avant de continuer, installez les packages de composants requis hello sur votre appareil Ubuntu à l’aide de hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="9cd2f-108">Before proceeding, install hello prerequisite packages on your Ubuntu device using hello following command:</span></span>

```
sudo apt-get install cmake gcc g++
```

## <a name="install-hello-client-libraries-on-your-device"></a><span data-ttu-id="9cd2f-109">Installer les bibliothèques clientes hello sur votre appareil</span><span class="sxs-lookup"><span data-stu-id="9cd2f-109">Install hello client libraries on your device</span></span>
<span data-ttu-id="9cd2f-110">Bonjour Azure IoT Hub bibliothèques clientes sont disponibles sous forme de package que vous pouvez installer sur votre appareil Ubuntu à l’aide de hello **apt-get** commande.</span><span class="sxs-lookup"><span data-stu-id="9cd2f-110">hello Azure IoT Hub client libraries are available as a package you can install on your Ubuntu device using hello **apt-get** command.</span></span> <span data-ttu-id="9cd2f-111">Hello complet suivant les étapes tooinstall hello package contenant hello bibliothèque cliente de IoT Hub et les fichiers d’en-tête sur votre ordinateur Ubuntu :</span><span class="sxs-lookup"><span data-stu-id="9cd2f-111">Complete hello following steps tooinstall hello package that contains hello IoT Hub client library and header files on your Ubuntu computer:</span></span>

1. <span data-ttu-id="9cd2f-112">Dans un interpréteur de commandes, ajouter de hello AzureIoT référentiel tooyour :</span><span class="sxs-lookup"><span data-stu-id="9cd2f-112">In a shell, add hello AzureIoT repository tooyour computer:</span></span>
   
    ```
    sudo add-apt-repository ppa:aziotsdklinux/ppa-azureiot
    sudo apt-get update
    ```
2. <span data-ttu-id="9cd2f-113">Installer le package d’azure-iot-sdk-c-dev hello</span><span class="sxs-lookup"><span data-stu-id="9cd2f-113">Install hello azure-iot-sdk-c-dev package</span></span>
   
    ```
    sudo apt-get install -y azure-iot-sdk-c-dev
    ```

## <a name="install-hello-parson-json-parser"></a><span data-ttu-id="9cd2f-114">Installer hello Analyseur de Parson JSON</span><span class="sxs-lookup"><span data-stu-id="9cd2f-114">Install hello Parson JSON parser</span></span>
<span data-ttu-id="9cd2f-115">Hello client IoT Hub bibliothèques utilisent hello charges de message tooparse Parson JSON analyseur.</span><span class="sxs-lookup"><span data-stu-id="9cd2f-115">hello IoT Hub client libraries use hello Parson JSON parser tooparse message payloads.</span></span> <span data-ttu-id="9cd2f-116">Dans un dossier approprié sur votre ordinateur, cloner le référentiel de Parson GitHub hello à l’aide de hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="9cd2f-116">In a suitable folder on your computer, clone hello Parson GitHub repository using hello following command:</span></span>

```
git clone https://github.com/kgabis/parson.git
```

## <a name="prepare-your-project"></a><span data-ttu-id="9cd2f-117">Préparation du projet</span><span class="sxs-lookup"><span data-stu-id="9cd2f-117">Prepare your project</span></span>
<span data-ttu-id="9cd2f-118">Sur votre ordinateur Ubuntu, créez un dossier nommé **remote\_monitoring**.</span><span class="sxs-lookup"><span data-stu-id="9cd2f-118">On your Ubuntu machine, create a folder called **remote\_monitoring**.</span></span> <span data-ttu-id="9cd2f-119">Bonjour **distant\_analyse** dossier :</span><span class="sxs-lookup"><span data-stu-id="9cd2f-119">In hello **remote\_monitoring** folder:</span></span>

- <span data-ttu-id="9cd2f-120">Créer des quatre fichiers hello **main.c**, **distant\_monitoring.c**, **distant\_monitoring.h**, et **CMakeLists.txt**.</span><span class="sxs-lookup"><span data-stu-id="9cd2f-120">Create hello four files **main.c**, **remote\_monitoring.c**, **remote\_monitoring.h**, and **CMakeLists.txt**.</span></span>
- <span data-ttu-id="9cd2f-121">Créez un dossier nommé **parson**.</span><span class="sxs-lookup"><span data-stu-id="9cd2f-121">Create folder called **parson**.</span></span>

<span data-ttu-id="9cd2f-122">Copiez les fichiers hello **parson.c** et **parson.h** à partir de votre copie locale du référentiel de Parson hello en hello **distant\_analyse/parson** dossier.</span><span class="sxs-lookup"><span data-stu-id="9cd2f-122">Copy hello files **parson.c** and **parson.h** from your local copy of hello Parson repository into hello **remote\_monitoring/parson** folder.</span></span>

<span data-ttu-id="9cd2f-123">Dans un éditeur de texte, ouvrez hello **distant\_monitoring.c** fichier.</span><span class="sxs-lookup"><span data-stu-id="9cd2f-123">In a text editor, open hello **remote\_monitoring.c** file.</span></span> <span data-ttu-id="9cd2f-124">Ajoutez hello suit `#include` instructions :</span><span class="sxs-lookup"><span data-stu-id="9cd2f-124">Add hello following `#include` statements:</span></span>
   
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

## <a name="call-hello-remotemonitoringrun-function"></a><span data-ttu-id="9cd2f-125">Appelez hello distant\_analyse\_exécuter (fonction)</span><span class="sxs-lookup"><span data-stu-id="9cd2f-125">Call hello remote\_monitoring\_run function</span></span>
<span data-ttu-id="9cd2f-126">Dans un éditeur de texte, ouvrez hello **remote_monitoring.h** fichier.</span><span class="sxs-lookup"><span data-stu-id="9cd2f-126">In a text editor, open hello **remote_monitoring.h** file.</span></span> <span data-ttu-id="9cd2f-127">Ajoutez hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="9cd2f-127">Add hello following code:</span></span>

```
void remote_monitoring_run(void);
```

<span data-ttu-id="9cd2f-128">Dans un éditeur de texte, ouvrez hello **main.c** fichier.</span><span class="sxs-lookup"><span data-stu-id="9cd2f-128">In a text editor, open hello **main.c** file.</span></span> <span data-ttu-id="9cd2f-129">Ajoutez hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="9cd2f-129">Add hello following code:</span></span>

```
#include "remote_monitoring.h"

int main(void)
{
    remote_monitoring_run();

    return 0;
}
```

## <a name="build-and-run-hello-application"></a><span data-ttu-id="9cd2f-130">Générer et exécuter l’application hello</span><span class="sxs-lookup"><span data-stu-id="9cd2f-130">Build and run hello application</span></span>
<span data-ttu-id="9cd2f-131">Hello étapes suivantes décrivent comment toouse *CMake* toobuild votre application cliente.</span><span class="sxs-lookup"><span data-stu-id="9cd2f-131">hello following steps describe how toouse *CMake* toobuild your client application.</span></span>

1. <span data-ttu-id="9cd2f-132">Dans un éditeur de texte, ouvrez hello **CMakeLists.txt** fichier Bonjour **remote_monitoring** dossier.</span><span class="sxs-lookup"><span data-stu-id="9cd2f-132">In a text editor, open hello **CMakeLists.txt** file in hello **remote_monitoring** folder.</span></span>

1. <span data-ttu-id="9cd2f-133">Ajouter hello suivant les instructions toodefine comment toobuild votre application cliente :</span><span class="sxs-lookup"><span data-stu-id="9cd2f-133">Add hello following instructions toodefine how toobuild your client application:</span></span>
   
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
1. <span data-ttu-id="9cd2f-134">Bonjour **remote_monitoring** dossier, créez un Bonjour toostore de dossier *rendre* fichiers que CMake génère et puis exécutez hello **cmake** et **rendre** commandes comme suit :</span><span class="sxs-lookup"><span data-stu-id="9cd2f-134">In hello **remote_monitoring** folder, create a folder toostore hello *make* files that CMake generates and then run hello **cmake** and **make** commands as follows:</span></span>
   
    ```
    mkdir cmake
    cd cmake
    cmake ../
    make
    ```

1. <span data-ttu-id="9cd2f-135">Exécuter l’application cliente de hello et envoyer des données de télémétrie tooIoT Hub :</span><span class="sxs-lookup"><span data-stu-id="9cd2f-135">Run hello client application and send telemetry tooIoT Hub:</span></span>
   
    ```
    ./sample_app
    ```

[!INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]

