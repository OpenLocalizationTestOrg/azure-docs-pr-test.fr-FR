---
title: "Connecter un périphérique à l’aide de C sous Linux | Microsoft Docs"
description: "Explique comment connecter un appareil à la solution de surveillance à distance Azure IoT Suite préconfigurée à l’aide d’une application écrite en C et exécutée sous Linux."
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
ms.openlocfilehash: 9adbc9cc13f0b4cafa3a3a7703c46f8085b15232
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="connect-your-device-to-the-remote-monitoring-preconfigured-solution-linux"></a><span data-ttu-id="b9ab0-103">Connexion de votre appareil à la solution préconfigurée de surveillance à distance (Linux)</span><span class="sxs-lookup"><span data-stu-id="b9ab0-103">Connect your device to the remote monitoring preconfigured solution (Linux)</span></span>
[!INCLUDE [iot-suite-selector-connecting](../../includes/iot-suite-selector-connecting.md)]

## <a name="build-and-run-a-sample-c-client-linux"></a><span data-ttu-id="b9ab0-104">Création et exécution d’un exemple de client Linux C</span><span class="sxs-lookup"><span data-stu-id="b9ab0-104">Build and run a sample C client Linux</span></span>
<span data-ttu-id="b9ab0-105">Les étapes suivantes vous montrent comment créer une application cliente qui communique avec la solution préconfigurée de surveillance à distance.</span><span class="sxs-lookup"><span data-stu-id="b9ab0-105">The following steps show you how to create a client application that communicates with the remote monitoring preconfigured solution.</span></span> <span data-ttu-id="b9ab0-106">Cette application est écrite en C, générée et exécutée sur Ubuntu Linux.</span><span class="sxs-lookup"><span data-stu-id="b9ab0-106">This application is written in C and built and run on Ubuntu Linux.</span></span>

<span data-ttu-id="b9ab0-107">Pour effectuer ces étapes, vous avez besoin d’un appareil exécutant Ubuntu version 15.04 ou 15.10.</span><span class="sxs-lookup"><span data-stu-id="b9ab0-107">To complete these steps, you need a device running Ubuntu version 15.04 or 15.10.</span></span> <span data-ttu-id="b9ab0-108">Avant de continuer, installez les packages requis sur votre appareil Ubuntu à l’aide de la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="b9ab0-108">Before proceeding, install the prerequisite packages on your Ubuntu device using the following command:</span></span>

```
sudo apt-get install cmake gcc g++
```

## <a name="install-the-client-libraries-on-your-device"></a><span data-ttu-id="b9ab0-109">Installation des bibliothèques clientes sur votre appareil</span><span class="sxs-lookup"><span data-stu-id="b9ab0-109">Install the client libraries on your device</span></span>
<span data-ttu-id="b9ab0-110">Les bibliothèques clientes Azure IoT Hub sont disponibles sous la forme d’un package que vous pouvez installer sur votre appareil Ubuntu à l’aide de la commande **apt-get** .</span><span class="sxs-lookup"><span data-stu-id="b9ab0-110">The Azure IoT Hub client libraries are available as a package you can install on your Ubuntu device using the **apt-get** command.</span></span> <span data-ttu-id="b9ab0-111">Procédez comme suit pour installer le package contenant les fichiers d’en-tête et de bibliothèque du client IoT Hub sur votre ordinateur Ubuntu :</span><span class="sxs-lookup"><span data-stu-id="b9ab0-111">Complete the following steps to install the package that contains the IoT Hub client library and header files on your Ubuntu computer:</span></span>

1. <span data-ttu-id="b9ab0-112">Dans un interpréteur de commandes, ajoutez le référentiel AzureIoT sur votre ordinateur :</span><span class="sxs-lookup"><span data-stu-id="b9ab0-112">In a shell, add the AzureIoT repository to your computer:</span></span>
   
    ```
    sudo add-apt-repository ppa:aziotsdklinux/ppa-azureiot
    sudo apt-get update
    ```
2. <span data-ttu-id="b9ab0-113">Installation du package azure-iot-sdk-c-dev</span><span class="sxs-lookup"><span data-stu-id="b9ab0-113">Install the azure-iot-sdk-c-dev package</span></span>
   
    ```
    sudo apt-get install -y azure-iot-sdk-c-dev
    ```

## <a name="install-the-parson-json-parser"></a><span data-ttu-id="b9ab0-114">Installation de l’analyseur JSON Parson JSON</span><span class="sxs-lookup"><span data-stu-id="b9ab0-114">Install the Parson JSON parser</span></span>
<span data-ttu-id="b9ab0-115">Les bibliothèques clientes IoT Hub utilisent l’analyseur JSON Parson pour analyser les charges utiles des messages.</span><span class="sxs-lookup"><span data-stu-id="b9ab0-115">The IoT Hub client libraries use the Parson JSON parser to parse message payloads.</span></span> <span data-ttu-id="b9ab0-116">Dans un dossier approprié sur votre ordinateur, clonez le référentiel GitHub Parson à l’aide de la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="b9ab0-116">In a suitable folder on your computer, clone the Parson GitHub repository using the following command:</span></span>

```
git clone https://github.com/kgabis/parson.git
```

## <a name="prepare-your-project"></a><span data-ttu-id="b9ab0-117">Préparation du projet</span><span class="sxs-lookup"><span data-stu-id="b9ab0-117">Prepare your project</span></span>
<span data-ttu-id="b9ab0-118">Sur votre ordinateur Ubuntu, créez un dossier nommé **remote\_monitoring**.</span><span class="sxs-lookup"><span data-stu-id="b9ab0-118">On your Ubuntu machine, create a folder called **remote\_monitoring**.</span></span> <span data-ttu-id="b9ab0-119">Dans le dossier **remote\_monitoring** :</span><span class="sxs-lookup"><span data-stu-id="b9ab0-119">In the **remote\_monitoring** folder:</span></span>

- <span data-ttu-id="b9ab0-120">Créez quatre fichiers : **main.c**, **remote\_monitoring.c**, **remote\_monitoring.h** et **CMakeLists.txt**.</span><span class="sxs-lookup"><span data-stu-id="b9ab0-120">Create the four files **main.c**, **remote\_monitoring.c**, **remote\_monitoring.h**, and **CMakeLists.txt**.</span></span>
- <span data-ttu-id="b9ab0-121">Créez un dossier nommé **parson**.</span><span class="sxs-lookup"><span data-stu-id="b9ab0-121">Create folder called **parson**.</span></span>

<span data-ttu-id="b9ab0-122">Copiez les fichiers **parson.c** et **parson.h** à partir de votre copie locale du référentiel Parson dans le dossier **remote\_monitoring/parson**.</span><span class="sxs-lookup"><span data-stu-id="b9ab0-122">Copy the files **parson.c** and **parson.h** from your local copy of the Parson repository into the **remote\_monitoring/parson** folder.</span></span>

<span data-ttu-id="b9ab0-123">Dans un éditeur de texte, ouvrez le fichier **remote\_monitoring.c**.</span><span class="sxs-lookup"><span data-stu-id="b9ab0-123">In a text editor, open the **remote\_monitoring.c** file.</span></span> <span data-ttu-id="b9ab0-124">Ajoutez les instructions `#include` suivantes :</span><span class="sxs-lookup"><span data-stu-id="b9ab0-124">Add the following `#include` statements:</span></span>
   
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

## <a name="call-the-remotemonitoringrun-function"></a><span data-ttu-id="b9ab0-125">Appel de la fonction remote\_monitoring\_run</span><span class="sxs-lookup"><span data-stu-id="b9ab0-125">Call the remote\_monitoring\_run function</span></span>
<span data-ttu-id="b9ab0-126">Dans un éditeur de texte, ouvrez le fichier **remote_monitoring.h**.</span><span class="sxs-lookup"><span data-stu-id="b9ab0-126">In a text editor, open the **remote_monitoring.h** file.</span></span> <span data-ttu-id="b9ab0-127">Ajoutez le code suivant :</span><span class="sxs-lookup"><span data-stu-id="b9ab0-127">Add the following code:</span></span>

```
void remote_monitoring_run(void);
```

<span data-ttu-id="b9ab0-128">Dans un éditeur de texte, ouvrez le fichier **main.c** .</span><span class="sxs-lookup"><span data-stu-id="b9ab0-128">In a text editor, open the **main.c** file.</span></span> <span data-ttu-id="b9ab0-129">Ajoutez le code suivant :</span><span class="sxs-lookup"><span data-stu-id="b9ab0-129">Add the following code:</span></span>

```
#include "remote_monitoring.h"

int main(void)
{
    remote_monitoring_run();

    return 0;
}
```

## <a name="build-and-run-the-application"></a><span data-ttu-id="b9ab0-130">Génération et exécution de l’application</span><span class="sxs-lookup"><span data-stu-id="b9ab0-130">Build and run the application</span></span>
<span data-ttu-id="b9ab0-131">Les étapes suivantes décrivent comment utiliser *CMake* pour créer votre application cliente.</span><span class="sxs-lookup"><span data-stu-id="b9ab0-131">The following steps describe how to use *CMake* to build your client application.</span></span>

1. <span data-ttu-id="b9ab0-132">Dans un éditeur de texte, ouvrez le fichier **CMakeLists.txt** dans le dossier **remote_monitoring**.</span><span class="sxs-lookup"><span data-stu-id="b9ab0-132">In a text editor, open the **CMakeLists.txt** file in the **remote_monitoring** folder.</span></span>

1. <span data-ttu-id="b9ab0-133">Ajoutez les instructions suivantes pour définir comment créer votre application cliente :</span><span class="sxs-lookup"><span data-stu-id="b9ab0-133">Add the following instructions to define how to build your client application:</span></span>
   
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
1. <span data-ttu-id="b9ab0-134">Dans le dossier **remote_monitoring**, créez un dossier pour stocker les fichiers *make* générés par CMake, puis exécutez les commandes **cmake** et **make** comme suit :</span><span class="sxs-lookup"><span data-stu-id="b9ab0-134">In the **remote_monitoring** folder, create a folder to store the *make* files that CMake generates and then run the **cmake** and **make** commands as follows:</span></span>
   
    ```
    mkdir cmake
    cd cmake
    cmake ../
    make
    ```

1. <span data-ttu-id="b9ab0-135">Exécutez l’application cliente et envoyez les données de télémétrie à IoT Hub :</span><span class="sxs-lookup"><span data-stu-id="b9ab0-135">Run the client application and send telemetry to IoT Hub:</span></span>
   
    ```
    ./sample_app
    ```

[!INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]

