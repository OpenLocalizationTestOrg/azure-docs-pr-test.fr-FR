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
# <a name="get-started-with-device-management-netnode"></a>Prise en main de la gestion d’appareils (.NET/Node)

[!INCLUDE [iot-hub-selector-dm-getstarted](../../includes/iot-hub-selector-dm-getstarted.md)]

Ce didacticiel vous explique les procédures suivantes :

* Utilisez hello toocreate portail Azure un IoT Hub et créer une identité d’appareil dans votre hub IoT.
* Créer une application d’appareil simulé disposant d’une méthode directe permettant le redémarrage de cet appareil. Méthodes directes sont appelés à partir du cloud de hello.
* Créer une application console .NET qui appelle la méthode directe de redémarrage hello dans l’application d’appareil simulé hello via votre hub IoT.

À la fin de hello de ce didacticiel, vous avez une application console Node.js et une principal d’application console .NET (c#) :

**dmpatterns_getstarted_device.js**, qui connecte tooyour IoT hub avec l’identité de l’appareil hello créée précédemment, reçoit une méthode directe de redémarrage, simule un redémarrage physique et indique le temps de hello pour le dernier redémarrage de hello.

**TriggerReboot**, qui appelle une méthode directe dans l’application d’appareil simulé hello, affiche les réponse hello et hello affiche mis à jour a signalé des propriétés.

toocomplete ce didacticiel, vous devez hello suivant :

* Visual Studio 2015 ou Visual Studio 2017.
* Node.js version 0.12.x ou version ultérieure. <br/>  [Préparer votre environnement de développement] [ lnk-dev-setup] décrit comment tooinstall Node.js pour ce didacticiel sur Windows ou Linux.
* Un compte Azure actif. (Si vous ne possédez pas de compte, vous pouvez créer un [compte gratuit][lnk-free-trial] en quelques minutes.)

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-reboot-on-hello-device-using-a-direct-method"></a>Déclencher un arrêt à distance sur l’appareil hello à l’aide d’une méthode directe
Dans cette section, vous créez une application console .NET (à l’aide de C#) qui lance un redémarrage à distance sur un appareil avec une méthode directe. application Hello utilise hello de toodiscover requêtes appareil double dernier redémarrage de cet appareil.

1. Dans Visual Studio, ajoutez une solution de nouveau tooa de projet Visual c# bureau classique de Windows à l’aide de hello **l’application Console (.NET Framework)** modèle de projet. Assurez-vous que la version du .NET Framework hello est 4.5.1 ou version ultérieure. Projet de hello nom **TriggerReboot**.

    ![Nouveau projet Visual C# Bureau classique Windows][img-createapp]

2. Dans l’Explorateur de solutions, cliquez sur hello **TriggerReboot** de projet, puis cliquez sur **gérer les Packages NuGet**.
3. Bonjour **Gestionnaire de Package NuGet** fenêtre, sélectionnez **Parcourir**, recherchez **microsoft.azure.devices**, sélectionnez **installer** tooinstall Hello **Microsoft.Azure.Devices** empaqueter et accepter les conditions d’utilisation de hello. Cette procédure télécharge, installe et ajoute une référence toohello [Azure IoT service SDK] [ lnk-nuget-service-sdk] NuGet package et ses dépendances.

    ![Fenêtre du gestionnaire de package NuGet][img-servicenuget]
4. Ajoutez hello suivant `using` instructions haut hello hello **Program.cs** fichier :
   
        using Microsoft.Azure.Devices;
        using Microsoft.Azure.Devices.Shared;
        
5. Ajouter hello suivant champs toohello **programme** classe. Remplacer la valeur d’espace réservé hello avec hello chaîne de connexion de IoT Hub hub hello que vous avez créé dans la section précédente de hello et hello cible de.
   
        static RegistryManager registryManager;
        static string connString = "{iot hub connection string}";
        static ServiceClient client;
        static JobClient jobClient;
        static string targetDevice = "{deviceIdForTargetDevice}";
        
6. Ajouter hello suivant de méthode toohello **programme** classe.  Cette double de périphérique code obtient hello pour hello hello de périphérique et les sorties de redémarrage a signalé des propriétés.
   
        public static async Task QueryTwinRebootReported()
        {
            Twin twin = await registryManager.GetTwinAsync(targetDevice);
            Console.WriteLine(twin.Properties.Reported.ToJson());
        }
        
7. Ajouter hello suivant de méthode toohello **programme** classe.  Ce code initialise redémarrage hello sur périphérique hello à l’aide d’une méthode directe.

        public static async Task StartReboot()
        {
            client = ServiceClient.CreateFromConnectionString(connString);
            CloudToDeviceMethod method = new CloudToDeviceMethod("reboot");
            method.ResponseTimeout = TimeSpan.FromSeconds(30);

            CloudToDeviceMethodResult result = await client.InvokeDeviceMethodAsync(targetDevice, method);

            Console.WriteLine("Invoked firmware update on device.");
        }

7. Enfin, ajoutez hello suivant lignes toohello **Main** méthode :
   
        registryManager = RegistryManager.CreateFromConnectionString(connString);
        StartReboot().Wait();
        QueryTwinRebootReported().Wait();
        Console.WriteLine("Press ENTER tooexit.");
        Console.ReadLine();
        
8. Générez la solution de hello.

## <a name="create-a-simulated-device-app"></a>Création d’une application de périphérique simulé
Dans cette section, vous allez :

* Créer une application de console Node.js qui répond tooa de méthode directe appelé par le cloud de hello
* Déclencher un redémarrage d’appareil simulé
* Hello d’utilisation signalées propriétés tooenable double requêtes tooidentify périphériques et quand ils dernier redémarrage

1. Créez un dossier vide nommé **simulateddevice**.  Bonjour **manageddevice** dossier, créez un fichier package.json à l’aide de hello, la commande suivante à l’invite suivante.  Acceptez les valeurs par défaut hello :
   
    ```
    npm init
    ```
2. Votre invite de commandes Bonjour **manageddevice** dossier, exécutez hello suivant commande tooinstall hello **azure iot-appareil** package SDK de l’appareil et **azure-iot-périphérique-mqtt**package :
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. À l’aide d’un éditeur de texte, créez un nouveau **dmpatterns_getstarted_device.js** fichier Bonjour **manageddevice** dossier.
4. Ajouter des instructions au début de hello Hello suivant de hello « exiger » **dmpatterns_getstarted_device.js** fichier :
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
5. Ajouter un **connectionString** variable et l’utiliser toocreate un **Client** instance.  Remplacez la chaîne de connexion hello avec la chaîne de connexion de votre périphérique.  
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId=myDeviceId;SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```
6. Ajouter hello suivant de méthode directe de fonction tooimplement hello de périphérique de hello
   
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
7. Ajoutez suivant de hello code le hub IoT tooyour tooopen hello connexion et démarrer l’écouteur de méthode directe hello :
   
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
8. Enregistrez et fermez hello **dmpatterns_getstarted_device.js** fichier.
   
> [!NOTE]
> tookeep les choses simples, ce didacticiel n’implémente pas de toute stratégie de nouvelle tentative. Dans le code de production, vous devez implémenter des stratégies de nouvelle tentative (par exemple, une interruption exponentielle), comme indiqué dans l’article hello [gestion des pannes temporaires][lnk-transient-faults].


## <a name="run-hello-apps"></a>Exécuter des applications de hello
Vous êtes maintenant prêt toorun hello applications.

1. Invite de commandes hello Bonjour **manageddevice** dossier, exécutez hello suivant toobegin de commande à l’écoute de méthode directe de redémarrage hello.
   
    ```
    node dmpatterns_getstarted_device.js
    ```
2. Application de console hello exécution c# **TriggerReboot**. Avec le bouton hello **TriggerReboot** projet, sélectionnez **déboguer**, puis sélectionnez **démarrer une nouvelle instance**.

3. Vous consultez hello appareil réponse toohello méthode directe dans la console hello.

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