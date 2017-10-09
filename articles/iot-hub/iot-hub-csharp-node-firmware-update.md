---
title: "mise à jour de microprogramme aaaDevice avec Azure IoT Hub (nœud/.NET) | Documents Microsoft"
description: "Comment mettre à jour toouse la gestion des appareils sur Azure IoT Hub tooinitiate un microprogramme de l’appareil. Vous utilisez hello Azure IoT SDK pour Node.js tooimplement une application d’appareil simulé et hello Azure IoT service SDK pour .NET tooimplement une application de service qui déclenche la mise à jour du microprogramme hello."
services: iot-hub
documentationcenter: .net
author: juanjperez
manager: timlt
editor: 
ms.assetid: 70b84258-bc9f-43b1-b7cf-de1bb715f2cf
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/17/2017
ms.author: juanpere
ms.openlocfilehash: d48899651bcd5d67e577c971be0f9453c8f21592
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-device-management-tooinitiate-a-device-firmware-update-netnode"></a>Utiliser la gestion de périphérique tooinitiate une mise à jour du microprogramme de périphérique (nœud/.NET)
[!INCLUDE [iot-hub-selector-firmware-update](../../includes/iot-hub-selector-firmware-update.md)]

## <a name="introduction"></a>Introduction
Bonjour [prise en main la gestion des appareils] [ lnk-dm-getstarted] didacticiel, vous avez vu comment toouse hello [double de l’appareil] [ lnk-devtwin] et [directe méthodes] [ lnk-c2dmethod] tooremotely de primitives redémarrer un appareil. Ce didacticiel utilise hello mêmes primitives IoT Hub et vous montre comment toodo un bout en bout simulée mise à jour du microprogramme.  Ce modèle est utilisé dans l’implémentation de mise à jour du microprogramme hello pour hello [exemple d’implémentation framboises Pi appareil][lnk-rpi-implementation].

Ce didacticiel vous explique les procédures suivantes :

* Créer une application console .NET qui appelle la méthode directe de hello firmwareUpdate dans l’application d’appareil simulé hello via votre hub IoT.
* Créez un appareil simulé qui implémente une méthode directe **firmwareUpdate**. Cette méthode lance un processus en plusieurs étapes qui attend l’image de microprogramme toodownload hello, télécharge l’image de microprogramme hello et enfin applique image de microprogramme hello. Lors de chaque étape de mise à jour hello, hello périphérique utilise hello signalée tooreport de propriétés sur la progression.

À la fin de hello de ce didacticiel, vous avez une application console Node.js et une principal d’application console .NET (c#) :

**dmpatterns_fwupdate_service.js**, qui appelle une méthode directe dans l’application d’appareil simulé hello, réponse de hello s’affiche et périodiquement (chaque 500 ms) hello affiche mis à jour signalés propriétés.

**TriggerFWUpdate**, qui connecte tooyour IoT hub avec l’identité de l’appareil hello créée précédemment, reçoit une méthode directe firmwareUpdate, s’exécute via un toosimulate plusieurs États de processus pour une mise à jour de microprogramme, y compris : en attente de téléchargement de l’image hello, Télécharger la nouvelle image de hello et enfin application hello image.

toocomplete ce didacticiel, vous devez hello suivant :

* Visual Studio 2015 ou Visual Studio 2017.
* Node.js version 0.12.x ou version ultérieure. <br/>  [Préparer votre environnement de développement] [ lnk-dev-setup] décrit comment tooinstall Node.js pour ce didacticiel sur Windows ou Linux.
* Un compte Azure actif. (Si vous ne possédez pas de compte, vous pouvez créer un [compte gratuit][lnk-free-trial] en quelques minutes.)

Suivez hello [prise en main la gestion des appareils](iot-hub-csharp-node-device-management-get-started.md) article toocreate votre IoT hub et obtenir votre chaîne de connexion de IoT Hub.

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-firmware-update-on-hello-device-using-a-direct-method"></a>Déclencher une mise à jour de microprogramme à distance sur l’appareil hello à l’aide d’une méthode directe
Dans cette section, vous créez une application de console .NET (à l’aide de C#) qui lance une mise à jour de microprogramme à distance sur un appareil. application Hello utilise une mise à jour de méthode directe tooinitiate hello et utilise appareil double requêtes tooperiodically obtenir l’état de hello de mise à jour du microprogramme active hello.

1. Dans Visual Studio, ajoutez une solution d’actuel toohello de projet Visual c# bureau classique de Windows à l’aide de hello **Application Console** modèle de projet. Projet de hello nom **TriggerFWUpdate**.

    ![Nouveau projet Visual C# Bureau classique Windows][img-createapp]

1. Dans l’Explorateur de solutions, cliquez sur hello **TriggerFWUpdate** de projet, puis cliquez sur **gérer les Packages NuGet...** .
1. Bonjour **Gestionnaire de Package NuGet** fenêtre, sélectionnez **Parcourir**, recherchez **microsoft.azure.devices**, sélectionnez **installer** tooinstall Hello **Microsoft.Azure.Devices** empaqueter et accepter les conditions d’utilisation de hello. Cette procédure télécharge, installe et ajoute une référence toohello [Azure IoT service SDK] [ lnk-nuget-service-sdk] NuGet package et ses dépendances.

    ![Fenêtre du gestionnaire de package NuGet][img-servicenuget]
1. Ajoutez hello suivant `using` instructions haut hello hello **Program.cs** fichier :
   
        using Microsoft.Azure.Devices;
        using Microsoft.Azure.Devices.Shared;
        
1. Ajouter hello suivant champs toohello **programme** classe. Remplacez hello plusieurs valeurs d’espace réservé avec hello la chaîne de connexion de IoT Hub pour le hub hello que vous avez créé dans la section précédente de hello et hello Id de votre appareil.
   
        static RegistryManager registryManager;
        static string connString = "{iot hub connection string}";
        static ServiceClient client;
        static JobClient jobClient;
        static string targetDevice = "{deviceIdForTargetDevice}";
        
1. Ajouter hello suivant de méthode toohello **programme** classe :
   
        public static async Task QueryTwinFWUpdateReported()
        {
            Twin twin = await registryManager.GetTwinAsync(targetDevice);
            Console.WriteLine(twin.Properties.Reported.ToJson());
        }
        
1. Ajouter hello suivant de méthode toohello **programme** classe :

        public static async Task StartFirmwareUpdate()
        {
            client = ServiceClient.CreateFromConnectionString(connString);
            CloudToDeviceMethod method = new CloudToDeviceMethod("firmwareUpdate");
            method.ResponseTimeout = TimeSpan.FromSeconds(30);
            method.SetPayloadJson(
                @"{
                    fwPackageUri : 'https://someurl'
                }");

            CloudToDeviceMethodResult result = await client.InvokeDeviceMethodAsync(targetDevice, method);

            Console.WriteLine("Invoked firmware update on device.");
        }

1. Enfin, ajoutez hello suivant lignes toohello **Main** méthode :
   
        registryManager = RegistryManager.CreateFromConnectionString(connString);
        StartFirmwareUpdate().Wait();
        QueryTwinFWUpdateReported().Wait();
        Console.WriteLine("Press ENTER tooexit.");
        Console.ReadLine();
        
1. Dans l’Explorateur de solutions de hello, ouvrez hello **projets de définir le démarrage...**  et assurez-vous que hello **Action** pour **TriggerFWUpdate** projet est **Démarrer**.

1. Générez la solution de hello.

[!INCLUDE [iot-hub-device-firmware-update](../../includes/iot-hub-device-firmware-update.md)]

## <a name="run-hello-apps"></a>Exécuter des applications de hello
Vous êtes maintenant prêt toorun hello applications.

1. Invite de commandes hello Bonjour **manageddevice** dossier, exécutez hello suivant toobegin de commande à l’écoute de méthode directe de redémarrage hello.
   
    ```
    node dmpatterns_fwupdate_device.js
    ```
2. Dans Visual Studio, cliquez sur hello **TriggerFWUpdate** projectRun toohello c# application console, sélectionnez **déboguer** et **démarrer une nouvelle instance**.

3. Vous consultez hello appareil réponse toohello méthode directe dans la console hello.

    ![Le microprogramme a été mis à jour][img-fwupdate]

## <a name="next-steps"></a>Étapes suivantes
Dans ce didacticiel, vous avez utilisé un tootrigger méthode directe à une distance mise à jour de microprogramme sur un appareil et un hello utilisé signalé progression de hello toofollow propriétés de mise à jour du microprogramme hello.

toolearn tooextend votre méthode de planification et de solution IoT des appels sur plusieurs appareils, consultez hello [planification et les tâches de diffusion] [ lnk-tutorial-jobs] didacticiel.

<!-- images -->
[img-servicenuget]: media/iot-hub-csharp-node-firmware-update/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-node-firmware-update/createnetapp.png
[img-fwupdate]: media/iot-hub-csharp-node-firmware-update/fwupdated.png

[lnk-devtwin]: iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: iot-hub-devguide-direct-methods.md
[lnk-dm-getstarted]: iot-hub-node-node-device-management-get-started.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[lnk-rpi-implementation]: https://github.com/Azure/azure-iot-sdk-c/tree/master/iothub_client/samples/iothub_client_sample_mqtt_dm/pi_device
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/