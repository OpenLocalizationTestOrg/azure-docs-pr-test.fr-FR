---
title: "travaux aaaSchedule avec Azure IoT Hub (nœud/.NET) | Documents Microsoft"
description: "Comment tooschedule un Azure IoT Hub travail tooinvoke une méthode directe sur plusieurs appareils. Vous utilisez du SDK de périphérique Azure IoT hello pour les applications pour appareil Node.js tooimplement hello simulée et hello Azure IoT service SDK pour .NET tooimplement un travail de service application toorun hello."
services: iot-hub
documentationcenter: .net
author: juanjperez
manager: timlt
editor: 
ms.assetid: 2233356e-b005-4765-ae41-3a4872bda943
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/10/2017
ms.author: juanpere
ms.openlocfilehash: f6148b67129dde4580bfe9ccceafd6400fbc5976
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="schedule-and-broadcast-jobs-netnodejs"></a>Planifier et diffuser des travaux (.NET/Node.js)

[!INCLUDE [iot-hub-selector-schedule-jobs](../../includes/iot-hub-selector-schedule-jobs.md)]

Utilisez les Azure IoT Hub tooschedule et suivre les travaux qui mettent à jour des millions d’appareils. Utilisez les travaux pour :

* Mettre à jour les propriétés souhaitées
* Mettre à jour les balises
* Appeler des méthodes directes

Une tâche encapsule une de ces actions et pistes hello d’exécution par rapport à un ensemble d’appareils qui est défini par une requête de double de périphérique. Par exemple, une application back-end peut utiliser un tooinvoke de travail une méthode directe sur 10 000 appareils qui redémarre les appareils hello. Vous spécifiez ensemble hello d’appareils avec une requête de double de périphérique et que vous planifiez hello travail toorun à l’avenir. progression assure le suivi des travaux Hello en tant que chacun des périphériques de hello recevoir et exécuter la méthode directe de redémarrage hello.

toolearn savoir plus sur chacune de ces fonctionnalités, consultez :

* Double de l’appareil et les propriétés : [prise en main jumeaux de périphérique] [ lnk-get-started-twin] et [didacticiel : comment toouse appareil à deux propriétés][lnk-twin-props]
* Méthodes directes : [Guide du développeur IoT Hub - Méthodes directes][lnk-dev-methods] et [Tutorial: Use direct methods][lnk-c2d-methods] (Didacticiel : utilisation des méthodes directes)

Ce didacticiel vous explique les procédures suivantes :

* Créer une application de périphérique qui implémente une méthode directe appelée **lockDoor** qui peut être appelée par l’application back-end de hello. application d’appareil Hello reçoit également les modifications de propriété de votre choix à partir de l’application back-end de hello.
* Créer une application de serveur principal qui crée un Bonjour toocall de travail **lockDoor** méthode directe sur plusieurs appareils. Une autre tâche envoie la propriété désirée toomultiple périphériques des mises à jour.

À la fin de hello de ce didacticiel, vous avez une application console Node.js et une principal d’application console .NET (c#) :

**simDevice.js** qui se connecte tooyour IoT hub, implémente hello **lockDoor** direct de méthode et les handles de modifications apportées aux propriétés souhaité.

**ScheduleJob** qui utilise hello toocall de travaux **lockDoor** direct double périphérique hello (méthode) et mise à jour des propriétés de la sur plusieurs appareils souhaitée.

toocomplete ce didacticiel, vous devez hello suivant :

* Visual Studio 2015 ou Visual Studio 2017.
* Node.js version 0.12.x ou version ultérieure. article de Hello [préparer votre environnement de développement] [ lnk-dev-setup] décrit comment tooinstall Node.js pour ce didacticiel sur Windows ou Linux.
* Un compte Azure actif. Si vous ne possédez pas de compte, vous pouvez créer un [compte gratuit][lnk-free-trial] en quelques minutes.

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="schedule-jobs-for-calling-a-direct-method-and-sending-device-twin-updates"></a>Planifier des travaux pour appeler une méthode directe et envoyer des mises à jour de jumeaux d’appareils

Dans cette section, vous créez .NET application console (à l’aide de c#) utilise hello toocall de travaux **lockDoor** méthode directe et envoyer la propriété désirée toomultiple périphériques des mises à jour.

1. Dans Visual Studio, ajoutez une solution d’actuel toohello de projet Visual c# bureau classique de Windows à l’aide de hello **Application Console** modèle de projet. Projet de hello nom **ScheduleJob**.

    ![Nouveau projet Visual C# Bureau classique Windows][img-createapp]

1. Dans l’Explorateur de solutions, cliquez sur hello **ScheduleJob** de projet, puis cliquez sur **gérer les Packages NuGet...** .
1. Bonjour **Gestionnaire de Package NuGet** fenêtre, sélectionnez **Parcourir**, recherchez **microsoft.azure.devices**, sélectionnez **installer** tooinstall Hello **Microsoft.Azure.Devices** empaqueter et accepter les conditions d’utilisation de hello. Cette étape télécharge, installe et ajoute une référence toohello [Azure IoT service SDK] [ lnk-nuget-service-sdk] NuGet package et ses dépendances.

    ![Fenêtre du gestionnaire de package NuGet][img-servicenuget]
1. Ajoutez hello suivant `using` instructions haut hello hello **Program.cs** fichier :
    
    ```csharp
    using Microsoft.Azure.Devices;
    using Microsoft.Azure.Devices.Shared;
    ```

1. Ajoutez hello suit `using` instruction si elle est déjà présent dans les instructions par défaut hello.

    ```csharp
    using System.Threading.Tasks;
    ```

1. Ajouter hello suivant champs toohello **programme** classe. Remplacer l’espace réservé de hello avec hello chaîne de connexion de IoT Hub hub hello que vous avez créé dans la section précédente de hello de.

    ```csharp
    static string connString = "{iot hub connection string}";
    static ServiceClient client;
    static JobClient jobClient;
    ```

1. Ajouter hello suivant de méthode toohello **programme** classe :

    ```csharp
    public static async Task MonitorJob(string jobId)
    {
        JobResponse result;
        do
        {
            result = await jobClient.GetJobAsync(jobId);
            Console.WriteLine("Job Status : " + result.Status.ToString());
            Thread.Sleep(2000);
        } while ((result.Status != JobStatus.Completed) && (result.Status != JobStatus.Failed));
    }
    ```

1. Ajouter hello suivant de méthode toohello **programme** classe :

    ```csharp
    public static async Task StartMethodJob(string jobId)
    {
        CloudToDeviceMethod directMethod = new CloudToDeviceMethod("lockDoor", TimeSpan.FromSeconds(5), TimeSpan.FromSeconds(5));

        JobResponse result = await jobClient.ScheduleDeviceMethodAsync(jobId,
            "deviceId='myDeviceId'",
            directMethod,
            DateTime.Now,
            10);

        Console.WriteLine("Started Method Job");
    }
    ```

1. Ajouter hello suivant de méthode toohello **programme** classe :

    ```csharp
    public static async Task StartTwinUpdateJob(string jobId)
    {
        var twin = new Twin();
        twin.Properties.Desired["Building"] = "43";
        twin.Properties.Desired["Floor"] = "3";
        twin.ETag = "*";

        JobResponse result = await jobClient.ScheduleTwinUpdateAsync(jobId,
            "deviceId='myDeviceId'",
            twin,
            DateTime.Now,
            10);

        Console.WriteLine("Started Twin Update Job");
    }
    ```

1. Enfin, ajoutez hello suivant lignes toohello **Main** méthode :

    ```csharp
    jobClient = JobClient.CreateFromConnectionString(connString);

    string methodJobId = Guid.NewGuid().ToString();

    StartMethodJob(methodJobId);
    MonitorJob(methodJobId).Wait();
    Console.WriteLine("Press ENTER toorun hello next job.");
    Console.ReadLine();

    string twinUpdateJobId = Guid.NewGuid().ToString();

    StartTwinUpdateJob(twinUpdateJobId);
    MonitorJob(twinUpdateJobId).Wait();
    Console.WriteLine("Press ENTER tooexit.");
    Console.ReadLine();
    ```

1. Dans l’Explorateur de solutions de hello, ouvrez hello **projets de définir le démarrage...**  et assurez-vous que hello **Action** pour **ScheduleJob** projet est **Démarrer**. Générez la solution de hello.

## <a name="create-a-simulated-device-app"></a>Création d’une application de périphérique simulé

Dans cette section, vous créez une application console Node.js qui répond tooa de méthode directe appelé par le cloud hello, qui déclenche un redémarrage de l’appareil simulé et utilise hello signalées propriétés tooenable double requêtes tooidentify périphériques et quand ils dernier redémarrage.

1. Créez un dossier vide appelé **simDevice**.  Bonjour **simDevice** dossier, créez un fichier package.json à l’aide de hello, la commande suivante à l’invite suivante.  Acceptez les valeurs par défaut hello :

    ```cmd/sh
    npm init
    ```

1. Votre invite de commandes Bonjour **simDevice** dossier, exécutez hello suivant commande tooinstall hello **azure iot-appareil** et **azure-iot-périphérique-mqtt** packages :

    ```cmd/sh
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```

1. À l’aide d’un éditeur de texte, créez un nouveau **simDevice.js** fichier Bonjour **simDevice** dossier.

1. Ajouter des instructions au début de hello Hello suivant de hello « exiger » **simDevice.js** fichier :

    ```nodejs
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```

1. Ajouter un **connectionString** variable et l’utiliser toocreate un **Client** instance. Rendre des espaces réservés de hello tooreplace que le programme d’installation de valeurs tooyour approprié.

    ```nodejs
    var connectionString = 'HostName={youriothostname};DeviceId={yourdeviceid};SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```

1. Ajouter hello suivant hello toohandle de fonction **lockDoor** (méthode).

    ```nodejs
    var onLockDoor = function(request, response) {
   
        // Respond hello cloud app for hello direct method
        response.send(200, function(err) {
            if (!err) {
                console.error('An error occured when sending a method response:\n' + err.toString());
            } else {
                console.log('Response toomethod \'' + request.methodName + '\' sent successfully.');
            }
        });
   
        console.log('Locking Door!');
    };
    ```

1. Ajouter hello suivant du Gestionnaire de hello code tooregister pour hello **lockDoor** (méthode).

    ```nodejs
    client.open(function(err) {
        if (err) {
            console.error('Could not connect tooIotHub client.');
        }  else {
            console.log('Client connected tooIoT Hub.  Waiting for lockDoor direct method.');
            client.onDeviceMethod('lockDoor', onLockDoor);
        }
    });
    ```

1. Enregistrez et fermez hello **simDevice.js** fichier.

> [!NOTE]
> tookeep les choses simples, ce didacticiel n’implémente pas de toute stratégie de nouvelle tentative. Dans le code de production, vous devez implémenter des stratégies de nouvelle tentative (par exemple, une interruption exponentielle), comme indiqué dans l’article hello [gestion des pannes temporaires][lnk-transient-faults].

## <a name="run-hello-apps"></a>Exécuter des applications de hello

Vous êtes maintenant prêt toorun hello applications.

1. Invite de commandes hello Bonjour **simDevice** dossier, exécutez hello suivant toobegin de commande à l’écoute de méthode directe de redémarrage hello.

    ```cmd/sh
    node simDevice.js
    ```

1. Application de console hello exécution c# **ScheduleJob** en cliquant sur hello **ScheduleJob** projet, puis en sélectionnant **déboguer** et **démarrer une nouvelle instance**.

1. Vous voyez la sortie hello à partir de périphériques et les applications de serveur principal.

    ![Exécuter des applications de hello tooschedule travaux][img-schedulejobs]

## <a name="next-steps"></a>Étapes suivantes

Dans ce didacticiel, vous avez utilisé un travail tooschedule un appareil de tooa méthode directe et la mise à jour de hello des propriétés du double hello appareil.

toocontinue mise en route avec les modèles de gestion des IoT Hub et de périphérique tel que distant sur hello air microprogramme mise à jour, consultez [didacticiel : comment toodo un microprogramme mettre à jour][lnk-fwupdate].

toocontinue mise en route avec IoT Hub, consultez [mise en route avec IoT bord][lnk-iot-edge].

<!-- images -->
[img-servicenuget]: media/iot-hub-csharp-node-schedule-jobs/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-node-schedule-jobs/createnetapp.png
[img-schedulejobs]: media/iot-hub-csharp-node-schedule-jobs/schedulejobs.png

[lnk-get-started-twin]: iot-hub-node-node-twin-getstarted.md
[lnk-twin-props]: iot-hub-node-node-twin-how-to-configure.md
[lnk-c2d-methods]: iot-hub-node-node-direct-methods.md
[lnk-dev-methods]: iot-hub-devguide-direct-methods.md
[lnk-fwupdate]: iot-hub-node-node-firmware-update.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
