---
title: "aaaGet a démarré avec la gestion des appareils Azure IoT Hub (nœud/.NET) | Documents Microsoft"
description: "Comment toouse Azure IoT Hub device management tooinitiate un appareil distant redémarrer. Vous utilisez du SDK de périphérique Azure IoT hello pour Node.js tooimplement une application d’appareil simulé qui inclut une méthode directe et la hello Azure IoT service SDK pour .NET tooimplement une application de service qui appelle la méthode directe hello."
services: iot-hub
documentationcenter: .net
author: juanjperez
manager: timlt
editor: 
ms.assetid: e044006d-ffd6-469b-bc63-c182ad066e31
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/17/2016
ms.author: juanpere
ms.openlocfilehash: ea6d50dfac1c222d7836e3bf5503c6c9b8c89dfa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-device-management-netnode"></a><span data-ttu-id="32913-104">Prise en main de la gestion d’appareils (.NET/Node)</span><span class="sxs-lookup"><span data-stu-id="32913-104">Get started with device management (.NET/Node)</span></span>

[!INCLUDE [iot-hub-selector-dm-getstarted](../../includes/iot-hub-selector-dm-getstarted.md)]

<span data-ttu-id="32913-105">Ce didacticiel vous explique les procédures suivantes :</span><span class="sxs-lookup"><span data-stu-id="32913-105">This tutorial shows you how to:</span></span>

* <span data-ttu-id="32913-106">Utilisez hello toocreate portail Azure un IoT Hub et créer une identité d’appareil dans votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="32913-106">Use hello Azure portal toocreate an IoT Hub and create a device identity in your IoT hub.</span></span>
* <span data-ttu-id="32913-107">Créer une application d’appareil simulé disposant d’une méthode directe permettant le redémarrage de cet appareil.</span><span class="sxs-lookup"><span data-stu-id="32913-107">Create a simulated device app that contains a direct method that reboots that device.</span></span> <span data-ttu-id="32913-108">Méthodes directes sont appelés à partir du cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="32913-108">Direct methods are invoked from hello cloud.</span></span>
* <span data-ttu-id="32913-109">Créer une application console .NET qui appelle la méthode directe de redémarrage hello dans l’application d’appareil simulé hello via votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="32913-109">Create a .NET console app that calls hello reboot direct method in hello simulated device app through your IoT hub.</span></span>

<span data-ttu-id="32913-110">À la fin de hello de ce didacticiel, vous avez une application console Node.js et une principal d’application console .NET (c#) :</span><span class="sxs-lookup"><span data-stu-id="32913-110">At hello end of this tutorial, you have a Node.js console device app and a .NET (C#) console back-end app:</span></span>

<span data-ttu-id="32913-111">**dmpatterns_getstarted_device.js**, qui connecte tooyour IoT hub avec l’identité de l’appareil hello créée précédemment, reçoit une méthode directe de redémarrage, simule un redémarrage physique et indique le temps de hello pour le dernier redémarrage de hello.</span><span class="sxs-lookup"><span data-stu-id="32913-111">**dmpatterns_getstarted_device.js**, which connects tooyour IoT hub with hello device identity created earlier, receives a reboot direct method, simulates a physical reboot, and reports hello time for hello last reboot.</span></span>

<span data-ttu-id="32913-112">**TriggerReboot**, qui appelle une méthode directe dans l’application d’appareil simulé hello, affiche les réponse hello et hello affiche mis à jour a signalé des propriétés.</span><span class="sxs-lookup"><span data-stu-id="32913-112">**TriggerReboot**, which calls a direct method in hello simulated device app, displays hello response, and displays hello updated reported properties.</span></span>

<span data-ttu-id="32913-113">toocomplete ce didacticiel, vous devez hello suivant :</span><span class="sxs-lookup"><span data-stu-id="32913-113">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="32913-114">Visual Studio 2015 ou Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="32913-114">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="32913-115">Node.js version 0.12.x ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="32913-115">Node.js version 0.12.x or later,</span></span> <br/>  <span data-ttu-id="32913-116">[Préparer votre environnement de développement] [ lnk-dev-setup] décrit comment tooinstall Node.js pour ce didacticiel sur Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="32913-116">[Prepare your development environment][lnk-dev-setup] describes how tooinstall Node.js for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="32913-117">Un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="32913-117">An active Azure account.</span></span> <span data-ttu-id="32913-118">(Si vous ne possédez pas de compte, vous pouvez créer un [compte gratuit][lnk-free-trial] en quelques minutes.)</span><span class="sxs-lookup"><span data-stu-id="32913-118">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-reboot-on-hello-device-using-a-direct-method"></a><span data-ttu-id="32913-119">Déclencher un arrêt à distance sur l’appareil hello à l’aide d’une méthode directe</span><span class="sxs-lookup"><span data-stu-id="32913-119">Trigger a remote reboot on hello device using a direct method</span></span>
<span data-ttu-id="32913-120">Dans cette section, vous créez une application console .NET (à l’aide de C#) qui lance un redémarrage à distance sur un appareil avec une méthode directe.</span><span class="sxs-lookup"><span data-stu-id="32913-120">In this section, you create a .NET console app (using C#) that initiates a remote reboot on a device using a direct method.</span></span> <span data-ttu-id="32913-121">application Hello utilise hello de toodiscover requêtes appareil double dernier redémarrage de cet appareil.</span><span class="sxs-lookup"><span data-stu-id="32913-121">hello app uses device twin queries toodiscover hello last reboot time for that device.</span></span>

1. <span data-ttu-id="32913-122">Dans Visual Studio, ajoutez une solution de nouveau tooa de projet Visual c# bureau classique de Windows à l’aide de hello **l’application Console (.NET Framework)** modèle de projet.</span><span class="sxs-lookup"><span data-stu-id="32913-122">In Visual Studio, add a Visual C# Windows Classic Desktop project tooa new solution by using hello **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="32913-123">Assurez-vous que la version du .NET Framework hello est 4.5.1 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="32913-123">Make sure hello .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="32913-124">Projet de hello nom **TriggerReboot**.</span><span class="sxs-lookup"><span data-stu-id="32913-124">Name hello project **TriggerReboot**.</span></span>

    ![Nouveau projet Visual C# Bureau classique Windows][img-createapp]

2. <span data-ttu-id="32913-126">Dans l’Explorateur de solutions, cliquez sur hello **TriggerReboot** de projet, puis cliquez sur **gérer les Packages NuGet**.</span><span class="sxs-lookup"><span data-stu-id="32913-126">In Solution Explorer, right-click hello **TriggerReboot** project, and then click **Manage NuGet Packages**.</span></span>
3. <span data-ttu-id="32913-127">Bonjour **Gestionnaire de Package NuGet** fenêtre, sélectionnez **Parcourir**, recherchez **microsoft.azure.devices**, sélectionnez **installer** tooinstall Hello **Microsoft.Azure.Devices** empaqueter et accepter les conditions d’utilisation de hello.</span><span class="sxs-lookup"><span data-stu-id="32913-127">In hello **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** tooinstall hello **Microsoft.Azure.Devices** package, and accept hello terms of use.</span></span> <span data-ttu-id="32913-128">Cette procédure télécharge, installe et ajoute une référence toohello [Azure IoT service SDK] [ lnk-nuget-service-sdk] NuGet package et ses dépendances.</span><span class="sxs-lookup"><span data-stu-id="32913-128">This procedure downloads, installs, and adds a reference toohello [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>

    ![Fenêtre du gestionnaire de package NuGet][img-servicenuget]
4. <span data-ttu-id="32913-130">Ajoutez hello suivant `using` instructions haut hello hello **Program.cs** fichier :</span><span class="sxs-lookup"><span data-stu-id="32913-130">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
        using Microsoft.Azure.Devices.Shared;
        
5. <span data-ttu-id="32913-131">Ajouter hello suivant champs toohello **programme** classe.</span><span class="sxs-lookup"><span data-stu-id="32913-131">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="32913-132">Remplacer la valeur d’espace réservé hello avec hello chaîne de connexion de IoT Hub hub hello que vous avez créé dans la section précédente de hello et hello cible de.</span><span class="sxs-lookup"><span data-stu-id="32913-132">Replace hello placeholder value with hello IoT Hub connection string for hello hub that you created in hello previous section and hello target device.</span></span>
   
        static RegistryManager registryManager;
        static string connString = "{iot hub connection string}";
        static ServiceClient client;
        static JobClient jobClient;
        static string targetDevice = "{deviceIdForTargetDevice}";
        
6. <span data-ttu-id="32913-133">Ajouter hello suivant de méthode toohello **programme** classe.</span><span class="sxs-lookup"><span data-stu-id="32913-133">Add hello following method toohello **Program** class.</span></span>  <span data-ttu-id="32913-134">Cette double de périphérique code obtient hello pour hello hello de périphérique et les sorties de redémarrage a signalé des propriétés.</span><span class="sxs-lookup"><span data-stu-id="32913-134">This code gets hello device twin for hello rebooting device and outputs hello reported properties.</span></span>
   
        public static async Task QueryTwinRebootReported()
        {
            Twin twin = await registryManager.GetTwinAsync(targetDevice);
            Console.WriteLine(twin.Properties.Reported.ToJson());
        }
        
7. <span data-ttu-id="32913-135">Ajouter hello suivant de méthode toohello **programme** classe.</span><span class="sxs-lookup"><span data-stu-id="32913-135">Add hello following method toohello **Program** class.</span></span>  <span data-ttu-id="32913-136">Ce code initialise redémarrage hello sur périphérique hello à l’aide d’une méthode directe.</span><span class="sxs-lookup"><span data-stu-id="32913-136">This code initiates hello reboot on hello device using a direct method.</span></span>

        public static async Task StartReboot()
        {
            client = ServiceClient.CreateFromConnectionString(connString);
            CloudToDeviceMethod method = new CloudToDeviceMethod("reboot");
            method.ResponseTimeout = TimeSpan.FromSeconds(30);

            CloudToDeviceMethodResult result = await client.InvokeDeviceMethodAsync(targetDevice, method);

            Console.WriteLine("Invoked firmware update on device.");
        }

7. <span data-ttu-id="32913-137">Enfin, ajoutez hello suivant lignes toohello **Main** méthode :</span><span class="sxs-lookup"><span data-stu-id="32913-137">Finally, add hello following lines toohello **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connString);
        StartReboot().Wait();
        QueryTwinRebootReported().Wait();
        Console.WriteLine("Press ENTER tooexit.");
        Console.ReadLine();
        
8. <span data-ttu-id="32913-138">Générez la solution de hello.</span><span class="sxs-lookup"><span data-stu-id="32913-138">Build hello solution.</span></span>

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="32913-139">Création d’une application de périphérique simulé</span><span class="sxs-lookup"><span data-stu-id="32913-139">Create a simulated device app</span></span>
<span data-ttu-id="32913-140">Dans cette section, vous allez :</span><span class="sxs-lookup"><span data-stu-id="32913-140">In this section, you will</span></span>

* <span data-ttu-id="32913-141">Créer une application de console Node.js qui répond tooa de méthode directe appelé par le cloud de hello</span><span class="sxs-lookup"><span data-stu-id="32913-141">Create a Node.js console app that responds tooa direct method called by hello cloud</span></span>
* <span data-ttu-id="32913-142">Déclencher un redémarrage d’appareil simulé</span><span class="sxs-lookup"><span data-stu-id="32913-142">Trigger a simulated device reboot</span></span>
* <span data-ttu-id="32913-143">Hello d’utilisation signalées propriétés tooenable double requêtes tooidentify périphériques et quand ils dernier redémarrage</span><span class="sxs-lookup"><span data-stu-id="32913-143">Use hello reported properties tooenable device twin queries tooidentify devices and when they last rebooted</span></span>

1. <span data-ttu-id="32913-144">Créez un dossier vide nommé **simulateddevice**.</span><span class="sxs-lookup"><span data-stu-id="32913-144">Create a new empty folder called **manageddevice**.</span></span>  <span data-ttu-id="32913-145">Bonjour **manageddevice** dossier, créez un fichier package.json à l’aide de hello, la commande suivante à l’invite suivante.</span><span class="sxs-lookup"><span data-stu-id="32913-145">In hello **manageddevice** folder, create a package.json file using hello following command at your command prompt.</span></span>  <span data-ttu-id="32913-146">Acceptez les valeurs par défaut hello :</span><span class="sxs-lookup"><span data-stu-id="32913-146">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="32913-147">Votre invite de commandes Bonjour **manageddevice** dossier, exécutez hello suivant commande tooinstall hello **azure iot-appareil** package SDK de l’appareil et **azure-iot-périphérique-mqtt**package :</span><span class="sxs-lookup"><span data-stu-id="32913-147">At your command prompt in hello **manageddevice** folder, run hello following command tooinstall hello **azure-iot-device** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="32913-148">À l’aide d’un éditeur de texte, créez un nouveau **dmpatterns_getstarted_device.js** fichier Bonjour **manageddevice** dossier.</span><span class="sxs-lookup"><span data-stu-id="32913-148">Using a text editor, create a new **dmpatterns_getstarted_device.js** file in hello **manageddevice** folder.</span></span>
4. <span data-ttu-id="32913-149">Ajouter des instructions au début de hello Hello suivant de hello « exiger » **dmpatterns_getstarted_device.js** fichier :</span><span class="sxs-lookup"><span data-stu-id="32913-149">Add hello following 'require' statements at hello start of hello **dmpatterns_getstarted_device.js** file:</span></span>
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
5. <span data-ttu-id="32913-150">Ajouter un **connectionString** variable et l’utiliser toocreate un **Client** instance.</span><span class="sxs-lookup"><span data-stu-id="32913-150">Add a **connectionString** variable and use it toocreate a **Client** instance.</span></span>  <span data-ttu-id="32913-151">Remplacez la chaîne de connexion hello avec la chaîne de connexion de votre périphérique.</span><span class="sxs-lookup"><span data-stu-id="32913-151">Replace hello connection string with your device connection string.</span></span>  
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId=myDeviceId;SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```
6. <span data-ttu-id="32913-152">Ajouter hello suivant de méthode directe de fonction tooimplement hello de périphérique de hello</span><span class="sxs-lookup"><span data-stu-id="32913-152">Add hello following function tooimplement hello direct method on hello device</span></span>
   
    ```
    var onReboot = function(request, response) {
   
        // Respond hello cloud app for hello direct method
        response.send(200, 'Reboot started', function(err) {
            if (!err) {
                console.error('An error occured when sending a method response:\n' + err.toString());
            } else {
                console.log('Response toomethod \'' + request.methodName + '\' sent successfully.');
            }
        });
   
        // Report hello reboot before hello physical restart
        var date = new Date();
        var patch = {
            iothubDM : {
                reboot : {
                    lastReboot : date.toISOString(),
                }
            }
        };
   
        // Get device Twin
        client.getTwin(function(err, twin) {
            if (err) {
                console.error('could not get twin');
            } else {
                console.log('twin acquired');
                twin.properties.reported.update(patch, function(err) {
                    if (err) throw err;
                    console.log('Device reboot twin state reported')
                });  
            }
        });
   
        // Add your device's reboot API for physical restart.
        console.log('Rebooting!');
    };
    ```
7. <span data-ttu-id="32913-153">Ajoutez suivant de hello code le hub IoT tooyour tooopen hello connexion et démarrer l’écouteur de méthode directe hello :</span><span class="sxs-lookup"><span data-stu-id="32913-153">Add hello following code tooopen hello connection tooyour IoT hub and start hello direct method listener:</span></span>
   
    ```
    client.open(function(err) {
        if (err) {
            console.error('Could not open IotHub client');
        }  else {
            console.log('Client opened.  Waiting for reboot method.');
            client.onDeviceMethod('reboot', onReboot);
        }
    });
    ```
8. <span data-ttu-id="32913-154">Enregistrez et fermez hello **dmpatterns_getstarted_device.js** fichier.</span><span class="sxs-lookup"><span data-stu-id="32913-154">Save and close hello **dmpatterns_getstarted_device.js** file.</span></span>
   
> [!NOTE]
> <span data-ttu-id="32913-155">tookeep les choses simples, ce didacticiel n’implémente pas de toute stratégie de nouvelle tentative.</span><span class="sxs-lookup"><span data-stu-id="32913-155">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="32913-156">Dans le code de production, vous devez implémenter des stratégies de nouvelle tentative (par exemple, une interruption exponentielle), comme indiqué dans l’article hello [gestion des pannes temporaires][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="32913-156">In production code, you should implement retry policies (such as an exponential backoff), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>


## <a name="run-hello-apps"></a><span data-ttu-id="32913-157">Exécuter des applications de hello</span><span class="sxs-lookup"><span data-stu-id="32913-157">Run hello apps</span></span>
<span data-ttu-id="32913-158">Vous êtes maintenant prêt toorun hello applications.</span><span class="sxs-lookup"><span data-stu-id="32913-158">You are now ready toorun hello apps.</span></span>

1. <span data-ttu-id="32913-159">Invite de commandes hello Bonjour **manageddevice** dossier, exécutez hello suivant toobegin de commande à l’écoute de méthode directe de redémarrage hello.</span><span class="sxs-lookup"><span data-stu-id="32913-159">At hello command prompt in hello **manageddevice** folder, run hello following command toobegin listening for hello reboot direct method.</span></span>
   
    ```
    node dmpatterns_getstarted_device.js
    ```
2. <span data-ttu-id="32913-160">Application de console hello exécution c# **TriggerReboot**.</span><span class="sxs-lookup"><span data-stu-id="32913-160">Run hello C# console app **TriggerReboot**.</span></span> <span data-ttu-id="32913-161">Avec le bouton hello **TriggerReboot** projet, sélectionnez **déboguer**, puis sélectionnez **démarrer une nouvelle instance**.</span><span class="sxs-lookup"><span data-stu-id="32913-161">Right-click hello **TriggerReboot** project, select **Debug**, and then select **Start new instance**.</span></span>

3. <span data-ttu-id="32913-162">Vous consultez hello appareil réponse toohello méthode directe dans la console hello.</span><span class="sxs-lookup"><span data-stu-id="32913-162">You see hello device response toohello direct method in hello console.</span></span>

[!INCLUDE [iot-hub-dm-followup](../../includes/iot-hub-dm-followup.md)]

<!-- images and links -->
[img-output]: media/iot-hub-get-started-with-dm/image6.png
[img-dm-ui]: media/iot-hub-get-started-with-dm/dmui.png
[img-servicenuget]: media/iot-hub-csharp-node-device-management-get-started/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-node-device-management-get-started/createnetapp.png

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md

[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[Azure portal]: https://portal.azure.com/
[Using resource groups toomanage your Azure resources]: ../azure-portal/resource-group-portal.md
[lnk-dm-github]: https://github.com/Azure/azure-iot-device-management

[lnk-devtwin]: iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: iot-hub-devguide-direct-methods.md
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/