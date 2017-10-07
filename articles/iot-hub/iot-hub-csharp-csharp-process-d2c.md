---
title: "messages de périphérique dans le cloud Azure IoT Hub aaaProcess à l’aide d’itinéraires (.Net) | Documents Microsoft"
description: "Comment tooprocess les messages appareil-à-cloud IoT Hub à l’aide des règles de routage et les points de terminaison personnalisés toodispatch messages tooother les services principaux."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 5177bac9-722f-47ef-8a14-b201142ba4bc
ms.service: iot-hub
ms.devlang: csharp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: c1dd5be04ca30c65af2be466ba6c8c1858333154
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="process-iot-hub-device-to-cloud-messages-using-routes-net"></a>Traiter les messages appareil-à-cloud IoT Hub en utilisant les itinéraires (.NET)

[!INCLUDE [iot-hub-selector-process-d2c](../../includes/iot-hub-selector-process-d2c.md)]

Ce didacticiel s’appuie sur hello [prise en main IoT Hub] didacticiel. didacticiel de Hello :

* Montre comment toouse règles de routage toodispatch les messages appareil-à-cloud dans un moyen simple et basée sur la configuration.
* Illustre comment les messages interactif tooisolate qui nécessitent une action immédiate à partir de la solution de hello back-end pour un traitement ultérieur. Par exemple, un appareil peut envoyer un message d’alerte qui déclenche l’insertion d’un ticket dans un système CRM. Par opposition, les messages de point de données tels que la télémétrie de température sont chargés dans un moteur d’analyse.

À la fin de hello de ce didacticiel, vous exécutez trois applications de console .NET :

* **SimulatedDevice**, une version modifiée de l’application hello créée Bonjour [prise en main IoT Hub] didacticiel envoie des messages de périphérique dans le cloud de point de données par seconde et toutes les 10 des messages interactif appareil-à-cloud secondes.
* **ReadDeviceToCloudMessages** qu’affiche hello non critiques télémétrie envoyé par votre application.
* **ReadCriticalQueue** sort file d’attente de messages critiques de hello envoyées par votre application à partir d’une file d’attente Service Bus. Cette file d’attente est attaché toohello IoT hub.

> [!NOTE]
> IoT Hub offre la prise en charge de Kit de développement logiciel (SDK) de plusieurs plateformes d’appareils et de plusieurs langages (notamment C, Java et JavaScript). toolearn tooreplace hello appareil simulé dans ce didacticiel avec un périphérique physique, voir hello [centre de développement Azure IoT].

toocomplete ce didacticiel, vous devez hello suivant :

* Visual Studio 2015 ou Visual Studio 2017.
* Un compte Azure actif. <br/>Si vous ne possédez pas de compte, vous pouvez créer un [compte gratuit](https://azure.microsoft.com/free/) en quelques minutes.

Vous devez avoir une connaissance de base de [Stockage Azure] et d’[Azure Service Bus].

## <a name="send-interactive-messages"></a>Envoyer des messages interactifs

Modifier l’application d’appareil hello vous avez créé dans hello [prise en main IoT Hub] toooccasionally didacticiel envoyer des messages interactifs.

Dans Visual Studio, Bonjour **SimulatedDevice** de projet, remplacez hello `SendDeviceToCloudMessagesAsync` méthode avec hello suivant de code :

```csharp
private static async void SendDeviceToCloudMessagesAsync()
{
    double minTemperature = 20;
    double minHumidity = 60;
    Random rand = new Random();

    while (true)
    {
        double currentTemperature = minTemperature + rand.NextDouble() * 15;
        double currentHumidity = minHumidity + rand.NextDouble() * 20;

        var telemetryDataPoint = new
        {
            deviceId = "myFirstDevice",
            temperature = currentTemperature,
            humidity = currentHumidity
        };
        var messageString = JsonConvert.SerializeObject(telemetryDataPoint);
        string levelValue;

        if (rand.NextDouble() > 0.7)
        {
            messageString = "This is a critical message";
            levelValue = "critical";
        }
        else
        {
            levelValue = "normal";
        }
        
        var message = new Message(Encoding.ASCII.GetBytes(messageString));
        message.Properties.Add("level", levelValue);
        
        await deviceClient.SendEventAsync(message);
        Console.WriteLine("{0} > Sent message: {1}", DateTime.Now, messageString);

        await Task.Delay(1000);
    }
}
```

Cette méthode ajoute au hasard les propriété hello `"level": "critical"` toomessages envoyés par périphérique hello, qui simule un message qui requiert une action immédiate par hello solution back-end. application d’appareil Hello transmet ces informations dans les propriétés de message hello, au lieu de dans le corps du message hello, afin que IoT Hub peut acheminer la destination du message approprié hello message toohello.

> [!NOTE]
> Vous pouvez utiliser les messages de tooroute de propriétés de message pour différents scénarios, y compris à froid-chemin d’accès de traitement, en outre des exemple de chemin d’accès à chaud toohello ci-après.

> [!NOTE]
> Pour des raisons de hello de simplicité, ce didacticiel n’implémente pas de toute stratégie de nouvelle tentative. Dans le code de production, vous devez implémenter une stratégie de nouvelle tentative comme une interruption exponentielle, comme indiqué dans l’article hello [gestion des pannes temporaires].

## <a name="route-messages-tooa-queue-in-your-iot-hub"></a>Itinéraire messages tooa file d’attente dans votre IoT hub

Dans cette section, vous allez :

* créer une file d’attente Service Bus ;
* Connecter tooyour IoT hub.
* Configurez votre IoT hub toosend toohello file d’attente messages en fonction de la présence de hello d’une propriété de message de type hello.

Pour plus d’informations sur la tooprocess des messages des files d’attente Service Bus, consultez [prise en main les files d’attente][Service Bus queue].

1. Créez une file d’attente Service Bus, comme décrit dans [Prise en main des files d’attente][Service Bus queue]. file d’attente Hello doit être Bonjour même abonnement et région que votre hub IoT. Prenez note du nom d’espace de noms et de file d’attente hello.

    > [!NOTE]
    > Les options **Sessions** ou **Détection des doublons** ne doivent pas être activées pour les files d’attente et rubriques Service Bus utilisées comme points de terminaison IoT Hub. Si une de ces options sont activée, le point de terminaison hello s’affiche en tant que **inaccessible** Bonjour portail Azure.

2. Dans hello portail Azure, ouvrez votre IoT hub, cliquez sur **points de terminaison**.
    
    ![Points de terminaison dans IoT hub][30]

3. Bonjour **points de terminaison** panneau, cliquez sur **ajouter** à hello tooadd supérieur votre concentrateur de IoT tooyour file d’attente. Point de terminaison nom hello **CriticalQueue** et utiliser hello déroulantes tooselect **file d’attente Service Bus**hello dans lequel réside votre file d’attente de l’espace de noms de Bus de Service et hello du nom de votre file d’attente. Lorsque vous avez terminé, cliquez sur **enregistrer** bas hello.
    
    ![Ajout d’un point de terminaison][31]
    
4. À présent, cliquez sur **Itinéraires** dans votre IoT Hub. Cliquez sur **ajouter** haut hello hello panneau toocreate est une règle de routage qui achemine les messages toohello de file d’attente vous simplement ajoutée. Sélectionnez **DeviceTelemetry** comme source de hello de données. Entrez `level="critical"` en tant que condition de hello, choisissez la file d’attente hello vous venez d’ajouter en tant qu’un point de terminaison personnalisé en tant que point de terminaison de règle de routage de hello. Lorsque vous avez terminé, cliquez sur **enregistrer** bas hello.
    
    ![Ajout d’un itinéraire][32]
    
    Assurez-vous que l’itinéraire de secours hello est défini trop**ON**. Cette valeur est la configuration par défaut de hello pour un hub IoT.
    
    ![Itinéraire de secours][33]

## <a name="read-from-hello-queue-endpoint"></a>Lire à partir du point de terminaison de file d’attente hello

Dans cette section, vous lisez les messages de hello à partir du point de terminaison de file d’attente hello.

1. Dans Visual Studio, ajouter une solution d’actuel toohello de projet Visual c# bureau classique de Windows, à l’aide de hello **l’application Console (.NET Framework)** modèle de projet. Projet de hello nom **ReadCriticalQueue**.

2. Dans l’Explorateur de solutions, cliquez sur hello **ReadCriticalQueue** de projet, puis cliquez sur **gérer les Packages NuGet**. Cette opération affiche hello **Gestionnaire de Package NuGet** fenêtre.

3. Recherchez **WindowsAzure.ServiceBus**, cliquez sur **installer**et acceptez les conditions d’utilisation de hello. Cette opération télécharge, installe et ajoute une référence de toohello Azure Service Bus, avec toutes ses dépendances.

4. Ajoutez hello suivant **à l’aide de** instructions haut hello hello **Program.cs** fichier :
   
    ```csharp
    using System.IO;
    using Microsoft.ServiceBus.Messaging;
    ```

5. Enfin, ajoutez hello suivant lignes toohello **Main** (méthode). Remplacez par la chaîne de connexion hello **écouter** autorisations pour la file d’attente hello :
   
    ```csharp
    Console.WriteLine("Receive critical messages. Ctrl-C tooexit.\n");
    var connectionString = "{service bus listen string}";
    var queueName = "{queue name}";
    
    var client = QueueClient.CreateFromConnectionString(connectionString, queueName);

    client.OnMessage(message =>
        {
            Stream stream = message.GetBody<Stream>();
            StreamReader reader = new StreamReader(stream, Encoding.ASCII);
            string s = reader.ReadToEnd();
            Console.WriteLine(String.Format("Message body: {0}", s));
        });
        
    Console.ReadLine();
    ```

## <a name="run-hello-applications"></a>Exécuter des applications de hello
Vous êtes maintenant prêt toorun les applications hello.

1. Dans Visual Studio, dans l’Explorateur de solutions, cliquez avec le bouton droit sur votre solution, puis sélectionnez **Définir les projets de démarrage**. Sélectionnez **plusieurs projets de démarrage**, puis sélectionnez **Démarrer** en tant qu’action hello pour hello **ReadDeviceToCloudMessages**, **SimulatedDevice**, et **ReadCriticalQueue** projets.
2. Appuyez sur **F5** toostart hello trois applications console. Hello **ReadDeviceToCloudMessages** application a uniquement les messages non critiques sont envoyés à partir de hello **SimulatedDevice** application et hello **ReadCriticalQueue** application a uniquement messages critiques.
   
   ![Trois applications de console][50]

## <a name="next-steps"></a>Étapes suivantes
Dans ce didacticiel, vous avez appris comment tooreliably distribuer des messages de l’appareil-à-cloud en utilisant la fonctionnalité de routage de messages hello du IoT Hub.

Hello [comment les messages toosend cloud-à-appareil avec IoT Hub] [ lnk-c2d] vous montre comment les messages toosend tooyour des périphériques à partir de votre serveur principal de solution.

exemples de toosee des solutions de bout en bout complets qui utilisent l’IoT Hub, consultez [Azure IoT Suite][lnk-suite].

toolearn savoir plus sur le développement de solutions avec IoT Hub, consultez hello [guide du développeur IoT Hub].

toolearn en savoir plus sur le routage des messages dans IoT Hub, consultez [envoyer et recevoir des messages avec IoT Hub][lnk-devguide-messaging].

<!-- Images. -->
[50]: ./media/iot-hub-csharp-csharp-process-d2c/run1.png
[30]: ./media/iot-hub-csharp-csharp-process-d2c/click-endpoints.png
[31]: ./media/iot-hub-csharp-csharp-process-d2c/endpoint-creation.png
[32]: ./media/iot-hub-csharp-csharp-process-d2c/route-creation.png
[33]: ./media/iot-hub-csharp-csharp-process-d2c/fallback-route.png

<!-- Links -->
[Service Bus queue]: ../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md
[Stockage Azure]: https://azure.microsoft.com/documentation/services/storage/
[Azure Service Bus]: https://azure.microsoft.com/documentation/services/service-bus/
[guide du développeur IoT Hub]: iot-hub-devguide.md
[prise en main IoT Hub]: iot-hub-csharp-csharp-getstarted.md
[lnk-devguide-messaging]: iot-hub-devguide-messaging.md
[centre de développement Azure IoT]: https://azure.microsoft.com/develop/iot
[gestion des pannes temporaires]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[lnk-c2d]: iot-hub-csharp-csharp-process-d2c.md
[lnk-suite]: https://azure.microsoft.com/documentation/suites/iot-suite/
