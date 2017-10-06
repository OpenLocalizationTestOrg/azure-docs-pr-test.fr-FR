---
title: "aaaConnect un appareil à l’aide de C sur Windows | Documents Microsoft"
description: "Décrit comment tooconnect un toohello appareil Azure IoT Suite préconfiguré solution d’analyse à distance à l’aide d’une application écrite en C s’exécutant sous Windows."
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
ms.openlocfilehash: 51041e0cec113a5cfa006ab2276096baf928eef5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-device-toohello-remote-monitoring-preconfigured-solution-windows"></a><span data-ttu-id="a2dd0-103">Se connecter à votre solution préconfigurée (Windows) de surveillance à distance de toohello périphérique</span><span class="sxs-lookup"><span data-stu-id="a2dd0-103">Connect your device toohello remote monitoring preconfigured solution (Windows)</span></span>
[!INCLUDE [iot-suite-selector-connecting](../../includes/iot-suite-selector-connecting.md)]

## <a name="create-a-c-sample-solution-on-windows"></a><span data-ttu-id="a2dd0-104">Création d’un exemple de solution C sur Windows</span><span class="sxs-lookup"><span data-stu-id="a2dd0-104">Create a C sample solution on Windows</span></span>
<span data-ttu-id="a2dd0-105">Hello suit vous montre comment toocreate une application cliente qui communique avec le contrôle à distance hello solution préconfigurée.</span><span class="sxs-lookup"><span data-stu-id="a2dd0-105">hello following steps show you how toocreate a client application that communicates with hello remote monitoring preconfigured solution.</span></span> <span data-ttu-id="a2dd0-106">Cette application est écrite en C, générée et exécutée sur Windows.</span><span class="sxs-lookup"><span data-stu-id="a2dd0-106">This application is written in C and built and run on Windows.</span></span>

<span data-ttu-id="a2dd0-107">Créer un projet de démarrage dans Visual Studio 2015 ou Visual Studio 2017 et ajouter les packages NuGet hello IoT Hub périphérique client :</span><span class="sxs-lookup"><span data-stu-id="a2dd0-107">Create a starter project in Visual Studio 2015 or Visual Studio 2017 and add hello IoT Hub device client NuGet packages:</span></span>

1. <span data-ttu-id="a2dd0-108">Dans Visual Studio, créez une application de console C à l’aide de Visual C++ de hello **Application Console Win32** modèle.</span><span class="sxs-lookup"><span data-stu-id="a2dd0-108">In Visual Studio, create a C console application using hello Visual C++ **Win32 Console Application** template.</span></span> <span data-ttu-id="a2dd0-109">Projet de hello nom **RMDevice**.</span><span class="sxs-lookup"><span data-stu-id="a2dd0-109">Name hello project **RMDevice**.</span></span>
2. <span data-ttu-id="a2dd0-110">Sur hello **paramètres de l’Application** page Bonjour **Assistant Application Win32**, vérifiez que **application Console** est sélectionné, puis décochez la case **précompilé en-tête** et **du cycle de vie de développement de sécurité (SDL) vérifie**.</span><span class="sxs-lookup"><span data-stu-id="a2dd0-110">On hello **Application Settings** page in hello **Win32 Application Wizard**, ensure that **Console application** is selected, and uncheck **Precompiled header** and **Security Development Lifecycle (SDL) checks**.</span></span>
3. <span data-ttu-id="a2dd0-111">Dans **l’Explorateur de solutions**, supprimer hello fichiers stdafx.h, targetver.h et stdafx.cpp.</span><span class="sxs-lookup"><span data-stu-id="a2dd0-111">In **Solution Explorer**, delete hello files stdafx.h, targetver.h, and stdafx.cpp.</span></span>
4. <span data-ttu-id="a2dd0-112">Dans **l’Explorateur de solutions**, renommez hello fichier RMDevice.cpp tooRMDevice.c.</span><span class="sxs-lookup"><span data-stu-id="a2dd0-112">In **Solution Explorer**, rename hello file RMDevice.cpp tooRMDevice.c.</span></span>
5. <span data-ttu-id="a2dd0-113">Dans **l’Explorateur de solutions**, avec le bouton droit sur hello **RMDevice** de projet, puis cliquez sur **gérer les packages NuGet**.</span><span class="sxs-lookup"><span data-stu-id="a2dd0-113">In **Solution Explorer**, right-click on hello **RMDevice** project and then click **Manage NuGet packages**.</span></span> <span data-ttu-id="a2dd0-114">Cliquez sur **Parcourir**, puis recherchez et installez hello suivant les packages NuGet :</span><span class="sxs-lookup"><span data-stu-id="a2dd0-114">Click **Browse**, then search for and install hello following NuGet packages:</span></span>
   
   * <span data-ttu-id="a2dd0-115">Microsoft.Azure.IoTHub.Serializer</span><span class="sxs-lookup"><span data-stu-id="a2dd0-115">Microsoft.Azure.IoTHub.Serializer</span></span>
   * <span data-ttu-id="a2dd0-116">Microsoft.Azure.IoTHub.IoTHubClient</span><span class="sxs-lookup"><span data-stu-id="a2dd0-116">Microsoft.Azure.IoTHub.IoTHubClient</span></span>
   * <span data-ttu-id="a2dd0-117">Microsoft.Azure.IoTHub.MqttTransport</span><span class="sxs-lookup"><span data-stu-id="a2dd0-117">Microsoft.Azure.IoTHub.MqttTransport</span></span>
6. <span data-ttu-id="a2dd0-118">Dans **l’Explorateur de solutions**, avec le bouton droit sur hello **RMDevice** de projet, puis cliquez sur **propriétés** du projet tooopen hello **Pages de propriétés**boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="a2dd0-118">In **Solution Explorer**, right-click on hello **RMDevice** project and then click **Properties** tooopen hello project's **Property Pages** dialog box.</span></span> <span data-ttu-id="a2dd0-119">Pour plus d’informations, consultez [Setting Visual C++ Project Properties (Définition des propriétés de projet Visual C++)][lnk-c-project-properties].</span><span class="sxs-lookup"><span data-stu-id="a2dd0-119">For details, see [Setting Visual C++ Project Properties][lnk-c-project-properties].</span></span> 
7. <span data-ttu-id="a2dd0-120">Cliquez sur hello **l’éditeur de liens** dossier, puis cliquez sur hello **entrée** page de propriétés.</span><span class="sxs-lookup"><span data-stu-id="a2dd0-120">Click hello **Linker** folder, then click hello **Input** property page.</span></span>
8. <span data-ttu-id="a2dd0-121">Ajouter **crypt32.lib** toohello **dépendances supplémentaires** propriété.</span><span class="sxs-lookup"><span data-stu-id="a2dd0-121">Add **crypt32.lib** toohello **Additional Dependencies** property.</span></span> <span data-ttu-id="a2dd0-122">Cliquez sur **OK** , puis **OK** à nouveau les valeurs de propriété du projet toosave hello.</span><span class="sxs-lookup"><span data-stu-id="a2dd0-122">Click **OK** and then **OK** again toosave hello project property values.</span></span>

<span data-ttu-id="a2dd0-123">Ajouter hello Parson JSON bibliothèque toohello **RMDevice** de projet et ajouter hello requis `#include` instructions :</span><span class="sxs-lookup"><span data-stu-id="a2dd0-123">Add hello Parson JSON library toohello **RMDevice** project and add hello required `#include` statements:</span></span>

1. <span data-ttu-id="a2dd0-124">Dans un dossier approprié sur votre ordinateur, cloner le référentiel de Parson GitHub hello à l’aide de hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="a2dd0-124">In a suitable folder on your computer, clone hello Parson GitHub repository using hello following command:</span></span>

    ```
    git clone https://github.com/kgabis/parson.git
    ```

1. <span data-ttu-id="a2dd0-125">Copiez les fichiers parson.h et parson.c hello copie locale hello hello Parson référentiel tooyour **RMDevice** dossier du projet.</span><span class="sxs-lookup"><span data-stu-id="a2dd0-125">Copy hello parson.h and parson.c files from hello local copy of hello Parson repository tooyour **RMDevice** project folder.</span></span>

1. <span data-ttu-id="a2dd0-126">Dans Visual Studio, avec le bouton droit hello **RMDevice** de projet, cliquez sur **ajouter**, puis cliquez sur **élément existant**.</span><span class="sxs-lookup"><span data-stu-id="a2dd0-126">In Visual Studio, right-click hello **RMDevice** project, click **Add**, and then click **Existing Item**.</span></span>

1. <span data-ttu-id="a2dd0-127">Bonjour **ajouter un élément existant** boîte de dialogue, sélectionnez hello parson.h et parson.c les fichiers de hello **RMDevice** dossier du projet.</span><span class="sxs-lookup"><span data-stu-id="a2dd0-127">In hello **Add Existing Item** dialog, select hello parson.h and parson.c files in hello **RMDevice** project folder.</span></span> <span data-ttu-id="a2dd0-128">Puis cliquez sur **ajouter** tooadd ces projets tooyour de deux fichiers.</span><span class="sxs-lookup"><span data-stu-id="a2dd0-128">Then click **Add** tooadd these two files tooyour project.</span></span>

1. <span data-ttu-id="a2dd0-129">Dans Visual Studio, ouvrez le fichier de RMDevice.c hello.</span><span class="sxs-lookup"><span data-stu-id="a2dd0-129">In Visual Studio, open hello RMDevice.c file.</span></span> <span data-ttu-id="a2dd0-130">Remplacer hello `#include` instructions avec hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="a2dd0-130">Replace hello existing `#include` statements with hello following code:</span></span>
   
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
    > <span data-ttu-id="a2dd0-131">Vous pouvez maintenant vérifier que votre projet comporte les dépendances appropriées hello en créer.</span><span class="sxs-lookup"><span data-stu-id="a2dd0-131">Now you can verify that your project has hello correct dependencies set up by building it.</span></span>

[!INCLUDE [iot-suite-connecting-code](../../includes/iot-suite-connecting-code.md)]

## <a name="build-and-run-hello-sample"></a><span data-ttu-id="a2dd0-132">Générer et exécuter l’exemple hello</span><span class="sxs-lookup"><span data-stu-id="a2dd0-132">Build and run hello sample</span></span>

<span data-ttu-id="a2dd0-133">Ajouter hello tooinvoke de code **distant\_analyse\_exécuter** fonction puis générer et exécuter l’application d’appareil hello.</span><span class="sxs-lookup"><span data-stu-id="a2dd0-133">Add code tooinvoke hello **remote\_monitoring\_run** function and then build and run hello device application.</span></span>

1. <span data-ttu-id="a2dd0-134">Remplacez hello **principal** fonction avec hello de tooinvoke de code suivant **distant\_analyse\_exécuter** fonction :</span><span class="sxs-lookup"><span data-stu-id="a2dd0-134">Replace hello **main** function with following code tooinvoke hello **remote\_monitoring\_run** function:</span></span>
   
    ```c
    int main()
    {
      remote_monitoring_run();
      return 0;
    }
    ```

1. <span data-ttu-id="a2dd0-135">Cliquez sur **générer** , puis **générer la Solution** application d’appareil toobuild hello.</span><span class="sxs-lookup"><span data-stu-id="a2dd0-135">Click **Build** and then **Build Solution** toobuild hello device application.</span></span>

1. <span data-ttu-id="a2dd0-136">Dans **l’Explorateur de solutions**, avec le bouton hello **RMDevice** de projet, cliquez sur **déboguer**, puis cliquez sur **démarrer une nouvelle instance** toorun hello exemple.</span><span class="sxs-lookup"><span data-stu-id="a2dd0-136">In **Solution Explorer**, right-click hello **RMDevice** project, click **Debug**, and then click **Start new instance** toorun hello sample.</span></span> <span data-ttu-id="a2dd0-137">console de Hello affiche les messages hello application envoie exemple télémétrie toohello solution préconfigurée, reçoit les valeurs de propriétés souhaitées définies dans le tableau de bord de solution hello et répond toomethods appelée à partir du tableau de bord de solution hello.</span><span class="sxs-lookup"><span data-stu-id="a2dd0-137">hello console displays messages as hello application sends sample telemetry toohello preconfigured solution, receives desired property values set in hello solution dashboard, and responds toomethods invoked from hello solution dashboard.</span></span>

[!INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]

[lnk-c-project-properties]: https://msdn.microsoft.com/library/669zx6zc.aspx
