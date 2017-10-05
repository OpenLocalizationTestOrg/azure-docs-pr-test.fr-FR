---
title: "Connexion d’un périphérique à l’aide de C sur Windows | Microsoft Docs"
description: "Explique comment connecter un appareil à la solution de surveillance à distance Azure IoT Suite préconfigurée à l’aide d’une application écrite en C et exécutée sous Windows."
services: 
suite: iot-suite
documentationcenter: na
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 34e39a58-2434-482c-b3fa-29438a0c05e8
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: d222bcbd64f288d4091acb0ecd2922b9ceee57e5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="connect-your-device-to-the-remote-monitoring-preconfigured-solution-windows"></a><span data-ttu-id="ffd0a-103">Connexion de votre appareil à la solution préconfigurée de surveillance à distance (Windows)</span><span class="sxs-lookup"><span data-stu-id="ffd0a-103">Connect your device to the remote monitoring preconfigured solution (Windows)</span></span>
[!INCLUDE [iot-suite-selector-connecting](../../includes/iot-suite-selector-connecting.md)]

## <a name="create-a-c-sample-solution-on-windows"></a><span data-ttu-id="ffd0a-104">Création d’un exemple de solution C sur Windows</span><span class="sxs-lookup"><span data-stu-id="ffd0a-104">Create a C sample solution on Windows</span></span>
<span data-ttu-id="ffd0a-105">Les étapes suivantes vous montrent comment créer une application cliente qui communique avec la solution préconfigurée de surveillance à distance.</span><span class="sxs-lookup"><span data-stu-id="ffd0a-105">The following steps show you how to create a client application that communicates with the remote monitoring preconfigured solution.</span></span> <span data-ttu-id="ffd0a-106">Cette application est écrite en C, générée et exécutée sur Windows.</span><span class="sxs-lookup"><span data-stu-id="ffd0a-106">This application is written in C and built and run on Windows.</span></span>

<span data-ttu-id="ffd0a-107">Créez un projet de démarrage dans Visual Studio 2015 ou Visual Studio 2017 et ajoutez les packages NuGet clients de l’appareil IoT Hub :</span><span class="sxs-lookup"><span data-stu-id="ffd0a-107">Create a starter project in Visual Studio 2015 or Visual Studio 2017 and add the IoT Hub device client NuGet packages:</span></span>

1. <span data-ttu-id="ffd0a-108">Dans Visual Studio, créez une application console C à l’aide du modèle **Application console Win32** de Visual C++.</span><span class="sxs-lookup"><span data-stu-id="ffd0a-108">In Visual Studio, create a C console application using the Visual C++ **Win32 Console Application** template.</span></span> <span data-ttu-id="ffd0a-109">Nommez le projet **RMDevice**.</span><span class="sxs-lookup"><span data-stu-id="ffd0a-109">Name the project **RMDevice**.</span></span>
2. <span data-ttu-id="ffd0a-110">Sur la page **Paramètres de l’application** dans **l’Assistant Application Win32**, assurez-vous que l’option **Application console** est sélectionnée et décochez les cases **En-tête précompilé** et **Vérifications SDL (Security Development Lifecycle)**.</span><span class="sxs-lookup"><span data-stu-id="ffd0a-110">On the **Application Settings** page in the **Win32 Application Wizard**, ensure that **Console application** is selected, and uncheck **Precompiled header** and **Security Development Lifecycle (SDL) checks**.</span></span>
3. <span data-ttu-id="ffd0a-111">Dans l’ **Explorateur de solutions**, supprimez les fichiers stdafx.h, targetver.h et stdafx.cpp.</span><span class="sxs-lookup"><span data-stu-id="ffd0a-111">In **Solution Explorer**, delete the files stdafx.h, targetver.h, and stdafx.cpp.</span></span>
4. <span data-ttu-id="ffd0a-112">Dans l’ **Explorateur de solutions**, renommez le fichier RMDevice.cpp en RMDevice.c.</span><span class="sxs-lookup"><span data-stu-id="ffd0a-112">In **Solution Explorer**, rename the file RMDevice.cpp to RMDevice.c.</span></span>
5. <span data-ttu-id="ffd0a-113">Dans **l’Explorateur de solutions**, cliquez avec le bouton droit sur le projet **RMDevice**, puis cliquez sur **Gérer les packages NuGet**.</span><span class="sxs-lookup"><span data-stu-id="ffd0a-113">In **Solution Explorer**, right-click on the **RMDevice** project and then click **Manage NuGet packages**.</span></span> <span data-ttu-id="ffd0a-114">Cliquez sur **Parcourir**, puis recherchez et installez les packages NuGet suivants :</span><span class="sxs-lookup"><span data-stu-id="ffd0a-114">Click **Browse**, then search for and install the following NuGet packages:</span></span>
   
   * <span data-ttu-id="ffd0a-115">Microsoft.Azure.IoTHub.Serializer</span><span class="sxs-lookup"><span data-stu-id="ffd0a-115">Microsoft.Azure.IoTHub.Serializer</span></span>
   * <span data-ttu-id="ffd0a-116">Microsoft.Azure.IoTHub.IoTHubClient</span><span class="sxs-lookup"><span data-stu-id="ffd0a-116">Microsoft.Azure.IoTHub.IoTHubClient</span></span>
   * <span data-ttu-id="ffd0a-117">Microsoft.Azure.IoTHub.MqttTransport</span><span class="sxs-lookup"><span data-stu-id="ffd0a-117">Microsoft.Azure.IoTHub.MqttTransport</span></span>
6. <span data-ttu-id="ffd0a-118">Dans **l’Explorateur de solutions**, cliquez avec le bouton droit sur le projet **RMDevice**, puis cliquez sur **Propriétés** pour ouvrir la boîte de dialogue **Pages de propriétés** du projet.</span><span class="sxs-lookup"><span data-stu-id="ffd0a-118">In **Solution Explorer**, right-click on the **RMDevice** project and then click **Properties** to open the project's **Property Pages** dialog box.</span></span> <span data-ttu-id="ffd0a-119">Pour plus d’informations, consultez [Setting Visual C++ Project Properties (Définition des propriétés de projet Visual C++)][lnk-c-project-properties].</span><span class="sxs-lookup"><span data-stu-id="ffd0a-119">For details, see [Setting Visual C++ Project Properties][lnk-c-project-properties].</span></span> 
7. <span data-ttu-id="ffd0a-120">Cliquez sur le dossier **Linker**, puis cliquez sur la page de propriétés **d’entrée**.</span><span class="sxs-lookup"><span data-stu-id="ffd0a-120">Click the **Linker** folder, then click the **Input** property page.</span></span>
8. <span data-ttu-id="ffd0a-121">Ajoutez **crypt32.lib** à la propriété **Dépendances supplémentaires**.</span><span class="sxs-lookup"><span data-stu-id="ffd0a-121">Add **crypt32.lib** to the **Additional Dependencies** property.</span></span> <span data-ttu-id="ffd0a-122">Cliquez sur **OK**, puis de nouveau sur **OK** pour enregistrer les valeurs des propriétés du projet.</span><span class="sxs-lookup"><span data-stu-id="ffd0a-122">Click **OK** and then **OK** again to save the project property values.</span></span>

<span data-ttu-id="ffd0a-123">Ajoutez la bibliothèque JSON Parson au projet **RMDevice** ainsi que les instructions `#include` requises :</span><span class="sxs-lookup"><span data-stu-id="ffd0a-123">Add the Parson JSON library to the **RMDevice** project and add the required `#include` statements:</span></span>

1. <span data-ttu-id="ffd0a-124">Dans un dossier approprié sur votre ordinateur, clonez le référentiel GitHub Parson à l’aide de la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="ffd0a-124">In a suitable folder on your computer, clone the Parson GitHub repository using the following command:</span></span>

    ```
    git clone https://github.com/kgabis/parson.git
    ```

1. <span data-ttu-id="ffd0a-125">Copiez les fichiers parson.h et parson.c de la copie locale du référentiel Parson dans le dossier de votre projet **RMDevice**.</span><span class="sxs-lookup"><span data-stu-id="ffd0a-125">Copy the parson.h and parson.c files from the local copy of the Parson repository to your **RMDevice** project folder.</span></span>

1. <span data-ttu-id="ffd0a-126">Dans Visual Studio, cliquez avec le bouton droit sur le projet **RMDevice**, cliquez sur **Ajouter**, puis sur **Élément existant**.</span><span class="sxs-lookup"><span data-stu-id="ffd0a-126">In Visual Studio, right-click the **RMDevice** project, click **Add**, and then click **Existing Item**.</span></span>

1. <span data-ttu-id="ffd0a-127">Dans la boîte de dialogue **Ajouter un élément existant**, sélectionnez les fichiers parson.h et parson.c dans le dossier du projet **RMDevice**.</span><span class="sxs-lookup"><span data-stu-id="ffd0a-127">In the **Add Existing Item** dialog, select the parson.h and parson.c files in the **RMDevice** project folder.</span></span> <span data-ttu-id="ffd0a-128">Cliquez ensuite sur **Ajouter** pour ajouter ces deux fichiers à votre projet.</span><span class="sxs-lookup"><span data-stu-id="ffd0a-128">Then click **Add** to add these two files to your project.</span></span>

1. <span data-ttu-id="ffd0a-129">Dans Visual Studio, ouvrez le fichier RMDevice.c.</span><span class="sxs-lookup"><span data-stu-id="ffd0a-129">In Visual Studio, open the RMDevice.c file.</span></span> <span data-ttu-id="ffd0a-130">Remplacez les instructions existantes `#include` par ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="ffd0a-130">Replace the existing `#include` statements with the following code:</span></span>
   
    ```c
    #include "iothubtransportmqtt.h"
    #include "schemalib.h"
    #include "iothub_client.h"
    #include "serializer_devicetwin.h"
    #include "schemaserializer.h"
    #include "azure_c_shared_utility/threadapi.h"
    #include "azure_c_shared_utility/platform.h"
    #include "parson.h"
    ```

    > [!NOTE]
    > <span data-ttu-id="ffd0a-131">À présent, vous pouvez vérifier que votre projet contient les dépendances appropriées définies en le générant.</span><span class="sxs-lookup"><span data-stu-id="ffd0a-131">Now you can verify that your project has the correct dependencies set up by building it.</span></span>

[!INCLUDE [iot-suite-connecting-code](../../includes/iot-suite-connecting-code.md)]

## <a name="build-and-run-the-sample"></a><span data-ttu-id="ffd0a-132">Créer et exécuter l’exemple.</span><span class="sxs-lookup"><span data-stu-id="ffd0a-132">Build and run the sample</span></span>

<span data-ttu-id="ffd0a-133">Ajoutez du code pour appeler la fonction **remote\_monitoring\_run**, puis générez et exécutez l’application de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="ffd0a-133">Add code to invoke the **remote\_monitoring\_run** function and then build and run the device application.</span></span>

1. <span data-ttu-id="ffd0a-134">Remplacez la fonction **main** par le code suivant pour appeler la fonction **remote\_monitoring\_run** :</span><span class="sxs-lookup"><span data-stu-id="ffd0a-134">Replace the **main** function with following code to invoke the **remote\_monitoring\_run** function:</span></span>
   
    ```c
    int main()
    {
      remote_monitoring_run();
      return 0;
    }
    ```

1. <span data-ttu-id="ffd0a-135">Cliquez sur **Générer**, puis sur **Générer la solution** pour générer l’application de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="ffd0a-135">Click **Build** and then **Build Solution** to build the device application.</span></span>

1. <span data-ttu-id="ffd0a-136">Dans **l’Explorateur de solutions**, cliquez avec le bouton droit sur le projet **RMDevice**, cliquez sur **Déboguer**, puis cliquez sur **Démarrer une nouvelle instance** pour exécuter l’exemple.</span><span class="sxs-lookup"><span data-stu-id="ffd0a-136">In **Solution Explorer**, right-click the **RMDevice** project, click **Debug**, and then click **Start new instance** to run the sample.</span></span> <span data-ttu-id="ffd0a-137">La console affiche des messages, car l’application envoie un échantillon de données de télémétrie à la solution préconfigurée, reçoit les valeurs de propriété souhaitées définies dans le tableau de bord de la solution et répond aux méthodes appelées à partir du tableau de bord de la solution.</span><span class="sxs-lookup"><span data-stu-id="ffd0a-137">The console displays messages as the application sends sample telemetry to the preconfigured solution, receives desired property values set in the solution dashboard, and responds to methods invoked from the solution dashboard.</span></span>

[!INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]

[lnk-c-project-properties]: https://msdn.microsoft.com/library/669zx6zc.aspx
