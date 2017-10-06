---
title: "aaaUse Azure IoT Hub direct de méthodes (nœud/.NET) | Documents Microsoft"
description: "Comment toouse Azure IoT Hub direct de méthodes. Vous utilisez du SDK de périphérique Azure IoT hello pour Node.js tooimplement une application d’appareil simulé qui inclut une méthode directe et la hello Azure IoT service SDK pour .NET tooimplement une application de service qui appelle la méthode directe hello."
services: iot-hub
documentationcenter: 
author: nberdy
manager: timlt
editor: 
ms.assetid: ab035b8e-bff8-4e12-9536-f31d6b6fe425
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/10/2017
ms.author: nberdy
ms.openlocfilehash: f566f939be840eb308b00ffa4e05c4e5b3fefb39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-direct-methods-netnode"></a>Utilisation des méthodes directes (NET/Node)
[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

Dans ce didacticiel, nous allons toodevelop .NET et une application de console Node.js :

* **CallMethodOnDevice.sln**, une application de serveur principal .NET, qui appelle une méthode dans l’application d’appareil simulé hello et affiche la réponse de hello.
* **SimulatedDevice.js**, une application Node.js, ce qui simule un appareil de connexion tooyour IoT hub avec l’identité de l’appareil hello créée précédemment et répond méthode toohello appelée par le cloud de hello.

> [!NOTE]
> article de Hello [kits de développement logiciel Azure IoT] [ lnk-hub-sdks] fournit des informations sur hello kits de développement logiciel Azure IoT que vous pouvez utiliser toobuild toorun de deux applications sur les périphériques et votre principal de la solution.
> 
> 

toocomplete ce didacticiel, vous devez :

* Visual Studio 2015 ou Visual Studio 2017.
* Node.js version 0.10.x ou ultérieure.
* Un compte Azure actif. (Si vous ne possédez pas de compte, vous pouvez créer un [compte gratuit][lnk-free-trial] en quelques minutes.)

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a>Création d’une application de périphérique simulé
Dans cette section, vous créer une application de console Node.js qui répond méthode tooa appelée par solution hello retour de fin.

1. Créez un dossier vide appelé **simulateddevice**. Bonjour **simulateddevice** dossier, créez un fichier package.json à l’aide de hello, la commande suivante à l’invite suivante. Acceptez les valeurs par défaut hello :
   
    ```
    npm init
    ```
2. Votre invite de commandes Bonjour **simulateddevice** dossier, exécutez hello suivant commande tooinstall hello **azure iot-appareil** et **azure-iot-périphérique-mqtt** packages :
   
    ```
        npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. À l’aide d’un éditeur de texte, créez un fichier Bonjour **simulateddevice** dossier et nommez-le **SimulatedDevice.js**.
4. Ajoutez hello suivant `require` instructions au hello démarrent Hello **SimulatedDevice.js** fichier :
   
    ```
    'use strict';
   
    var Mqtt = require('azure-iot-device-mqtt').Mqtt;
    var DeviceClient = require('azure-iot-device').Client;
    ```
5. Ajouter un **connectionString** variable et l’utiliser toocreate un **DeviceClient** instance. Remplacez **{chaîne de connexion de périphérique}** avec chaîne de connexion de périphérique hello générées dans hello *créer une identité d’appareil* section :
   
    ```
    var connectionString = '{device connection string}';
    var client = DeviceClient.fromConnectionString(connectionString, Mqtt);
    ```
6. Ajoutez hello suivant de méthode directe de fonction tooimplement hello de périphérique de hello :
   
    ```
    function onWriteLine(request, response) {
        console.log(request.payload);
   
        response.send(200, 'Input was written toolog.', function(err) {
            if(err) {
                console.error('An error occurred when sending a method response:\n' + err.toString());
            } else {
                console.log('Response toomethod \'' + request.methodName + '\' sent successfully.' );
            }
        });
    }
    ```
7. Ouvrez tooyour IoT hub hello connexion et initialiser l’écouteur de méthode hello :
   
    ```
    client.open(function(err) {
        if (err) {
            console.error('could not open IotHub client');
        }  else {
            console.log('client opened');
            client.onDeviceMethod('writeLine', onWriteLine);
        }
    });
    ```
8. Enregistrez et fermez hello **SimulatedDevice.js** fichier.

> [!NOTE]
> tookeep les choses simples, ce didacticiel n’implémente pas de toute stratégie de nouvelle tentative. Dans le code de production, vous devez implémenter des stratégies de nouvelle tentative (par exemple, les tentatives de connexion), comme indiqué dans l’article hello [gestion des pannes temporaires][lnk-transient-faults].
> 
> 

## <a name="call-a-direct-method-on-a-device"></a>Appeler une méthode directe sur un appareil
Dans cette section, vous créez une application de console .NET qui appelle une méthode dans l’application d’appareil simulé hello et affiche ensuite la réponse de hello.

1. Dans Visual Studio, ajoutez une solution d’actuel toohello de projet Visual c# bureau classique de Windows à l’aide de hello **Application Console** modèle de projet. Assurez-vous que la version du .NET Framework hello est 4.5.1 ou version ultérieure. Projet de hello nom **CallMethodOnDevice**.
   
    ![Nouveau projet Visual C# Bureau classique Windows][10]
2. Dans l’Explorateur de solutions, cliquez sur hello **CallMethodOnDevice** de projet, puis cliquez sur **gérer les Packages NuGet...** .
3. Bonjour **Gestionnaire de Package NuGet** fenêtre, sélectionnez **Parcourir**, recherchez **microsoft.azure.devices**, sélectionnez **installer** tooinstall Hello **Microsoft.Azure.Devices** empaqueter et accepter les conditions d’utilisation de hello. Cette procédure télécharge, installe et ajoute une référence toohello [Azure IoT service SDK] [ lnk-nuget-service-sdk] NuGet package et ses dépendances.
   
    ![Fenêtre du gestionnaire de package NuGet][11]

4. Ajoutez hello suivant `using` instructions haut hello hello **Program.cs** fichier :
   
        using System.Threading.Tasks;
        using Microsoft.Azure.Devices;
5. Ajouter hello suivant champs toohello **programme** classe. Remplacer la valeur d’espace réservé hello avec hello chaîne de connexion de IoT Hub hub hello que vous avez créé dans la section précédente de hello de.
   
        static ServiceClient serviceClient;
        static string connectionString = "{iot hub connection string}";
6. Ajouter hello suivant de méthode toohello **programme** classe :
   
        private static async Task InvokeMethod()
        {
            var methodInvocation = new CloudToDeviceMethod("writeLine") { ResponseTimeout = TimeSpan.FromSeconds(30) };
            methodInvocation.SetPayloadJson("'a line toobe written'");

            var response = await serviceClient.InvokeDeviceMethodAsync("myDeviceId", methodInvocation);

            Console.WriteLine("Response status: {0}, payload:", response.Status);
            Console.WriteLine(response.GetPayloadAsJson());
        }
   
    Cette méthode appelle une méthode directe avec le nom `writeLine` sur hello `myDeviceId` appareil. Ensuite, il écrit la réponse hello fournie par périphérique hello sur la console de hello. Notez qu’il est possible toospecify une valeur de délai d’attente pour hello périphérique toorespond.
7. Enfin, ajoutez hello suivant lignes toohello **Main** méthode :
   
        serviceClient = ServiceClient.CreateFromConnectionString(connectionString);
        InvokeMethod().Wait();
        Console.WriteLine("Press Enter tooexit.");
        Console.ReadLine();

## <a name="run-hello-applications"></a>Exécuter des applications de hello
Vous êtes maintenant prêt toorun les applications hello.

1. Dans l’Explorateur de solutions Visual Studio de hello, avec le bouton droit de votre solution, puis cliquez sur **définir les projets de démarrage...** . Sélectionnez **projet de démarrage unique**, puis sélectionnez hello **CallMethodOnDevice** projet dans le menu déroulant de hello.

2. À l’invite de commande Bonjour **simulateddevice** dossier, exécutez hello suivant toostart commande écoute les appels de méthode à partir de votre IoT Hub :
   
    ```
    node SimulatedDevice.js
    ```
   Attendez hello simulée périphérique tooopen :![][7]
3. Maintenant que hello est connectée et en attente d’appels de méthode, exécutez hello .NET **CallMethodOnDevice** méthode hello de tooinvoke d’application dans l’application d’appareil simulé hello. Vous devez voir la réponse du périphérique hello écrite dans la console hello.
   
    ![][8]
4. Appareil de Hello réagit puis toohello méthode par à l’impression de ce message :
   
    ![][9]

## <a name="next-steps"></a>Étapes suivantes
Dans ce didacticiel, vous configuré un IoT hub Bonjour portail Azure et ensuite créé une identité d’appareil dans le Registre des identités de hello IoT hub. Vous avez utilisé ce périphérique identité tooenable hello simulée appareil application tooreact toomethods appelée par le cloud de hello. Vous avez créé également une application qui appelle des méthodes sur l’appareil de hello et affiche la réponse hello périphérique de hello. 

toocontinue mise en route avec IoT Hub et tooexplore autres scénarios IoT, consultez :

* [Prise en main d’IoT Hub]
* [Planifier des travaux sur plusieurs appareils][lnk-devguide-jobs]

toolearn tooextend votre méthode de planification et de solution IoT des appels sur plusieurs appareils, consultez hello [planification et les tâches de diffusion] [ lnk-tutorial-jobs] didacticiel.

<!-- Images. -->
[7]: ./media/iot-hub-csharp-node-direct-methods/run-simulated-device.png
[8]: ./media/iot-hub-csharp-node-direct-methods/netserviceapp.png
[9]: ./media/iot-hub-csharp-node-direct-methods/methods-output.png

[10]: ./media/iot-hub-csharp-node-direct-methods/direct-methods-csharp1.png
[11]: ./media/iot-hub-csharp-node-direct-methods/direct-methods-csharp2.png

<!-- Links -->
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-portal]: https://portal.azure.com/
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md
[lnk-devguide-methods]: iot-hub-devguide-direct-methods.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md

[Send Cloud-to-Device messages with IoT Hub]: iot-hub-csharp-csharp-c2d.md
[Process Device-to-Cloud messages]: iot-hub-csharp-csharp-process-d2c.md
[Prise en main d’IoT Hub]: iot-hub-node-node-getstarted.md
