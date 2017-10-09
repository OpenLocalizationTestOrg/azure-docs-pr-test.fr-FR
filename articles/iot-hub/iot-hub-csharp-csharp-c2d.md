---
title: "les messages aaaCloud sur l’appareil avec Azure IoT Hub (.NET) | Documents Microsoft"
description: "Comment toosend cloud-à-appareil messages appareil tooa à partir d’un hub IoT d’Azure à l’aide de kits de développement IoT hello Azure pour .NET. Modifier une application appareil tooreceive les messages cloud-à-appareil et de modifier une application de serveur principal toosend hello cloud-à-appareil les messages."
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: a31c05ed-6ec0-40f3-99ab-8fdd28b1a89a
ms.service: iot-hub
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: elioda
ms.openlocfilehash: f6a7618b164d95c8ddaf28943f244aeeb568217f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="send-messages-from-hello-cloud-tooyour-device-with-iot-hub-net"></a>Envoyer des messages à partir de l’appareil de tooyour hello cloud avec IoT Hub (.NET)
[!INCLUDE [iot-hub-selector-c2d](../../includes/iot-hub-selector-c2d.md)]

## <a name="introduction"></a>Introduction
Azure IoT Hub est un service entièrement géré qui permet d’autoriser des communications bidirectionnelles fiables et sécurisées entre des millions d’appareils et un serveur principal de solution. Hello [prise en main IoT Hub] didacticiel montre comment toocreate un IoT hub, configurer une identité d’appareil qu’il contient et code d’une application de périphérique qui envoie des messages de l’appareil-à-cloud.

Ce didacticiel s’appuie sur l’article [prise en main IoT Hub]. Cette rubrique vous explique les procédures suivantes :

* À partir de votre solution back-end, envoyer des messages cloud-à-appareil tooa seule unité via IoT Hub.
* Recevez des messages cloud-à-appareil sur un appareil.
* À partir de votre solution back-end demande l’accusé de réception (*commentaires*) pour tooa appareil les messages envoyés à partir de IoT Hub.

Vous trouverez plus d’informations sur les messages cloud-à-appareil Bonjour [guide du développeur IoT Hub][IoT Hub developer guide - C2D].

À la fin de hello de ce didacticiel, vous exécutez deux applications de console .NET :

* **SimulatedDevice**, une version modifiée de l’application hello créée dans [prise en main IoT Hub], qui se connecte tooyour IoT hub et reçoit des messages cloud-à-appareil.
* **SendCloudToDevice**, qui envoie une application de périphérique toohello cloud-à-appareil message via IoT Hub et reçoit ensuite son accusé de réception.

> [!NOTE]
> IoT Hub offre la prise en charge de Kits de développement logiciel (SDK) pour plusieurs plateformes d’appareils et plusieurs langages (notamment C, Java et Javascript) par le biais des [Kits Azure IoT device SDK]. Pour obtenir des instructions sur tooconnect du votre appareil toothis didacticiel code et généralement tooAzure IoT Hub, voir hello [guide du développeur IoT Hub].
> 
> 

toocomplete ce didacticiel, vous devez hello suivant :

* Visual Studio 2015 ou Visual Studio 2017
* Un compte Azure actif. (Si vous ne possédez pas de compte, vous pouvez créer un [compte gratuit][lnk-free-trial] en quelques minutes.)

## <a name="receive-messages-in-hello-device-app"></a>Recevoir des messages dans une application de périphérique hello
Dans cette section, vous allez modifier créé à l’application pour appareil hello [prise en main IoT Hub] tooreceive les messages cloud-à-appareil à partir du hub IoT de hello.

1. Dans Visual Studio, Bonjour **SimulatedDevice** de projet, ajoutez hello suivant de méthode toohello **programme** classe.
   
        private static async void ReceiveC2dAsync()
        {
            Console.WriteLine("\nReceiving cloud toodevice messages from service");
            while (true)
            {
                Message receivedMessage = await deviceClient.ReceiveAsync();
                if (receivedMessage == null) continue;
   
                Console.ForegroundColor = ConsoleColor.Yellow;
                Console.WriteLine("Received message: {0}", Encoding.ASCII.GetString(receivedMessage.GetBytes()));
                Console.ResetColor();
   
                await deviceClient.CompleteAsync(receivedMessage);
            }
        }
   
    Hello `ReceiveAsync` méthode renvoie de manière asynchrone message de salutation reçu au moment de hello est reçue par le périphérique de hello. Elle retourne *null* après une période de délai d’attente pouvant être précisés (dans ce cas, est utilisé par défaut de hello d’une minute). Lorsque application hello reçoit un *null*, il doit continuer toowait pour les nouveaux messages. Cette exigence est la raison de hello hello `if (receivedMessage == null) continue` ligne.
   
    Hello appel trop`CompleteAsync()` notifie IoT Hub ce message de salutation n’a pas été correctement traité. message de type Hello peut être supprimé à partir de la file d’attente de hello. Si un problème est survenu cette application de périphérique a empêché hello à partir de la fin du traitement de hello de message de type hello, IoT Hub le remet à nouveau. Il est important de cette logique dans l’application hello de traitement des messages sont puis *idempotent*, de sorte que la réception hello même message plusieurs fois produit hello même résultat. Une application peut abandonner également temporairement un message, ce qui entraîne l’IoT hub en conservant le message de type hello dans la file d’attente hello de sa consommation ultérieure. Ou bien, application hello capable de rejeter un message, ce qui supprime définitivement le message de type hello à partir de la file d’attente hello. Pour plus d’informations sur le cycle de vie des cloud-à-appareil message hello, consultez hello [guide du développeur IoT Hub][IoT Hub developer guide - C2D].
   
   > [!NOTE]
   > Lorsque vous utilisez HTTP au lieu de MQTT ou AMQP comme transport, hello `ReceiveAsync` méthode est retournée immédiatement. modèle Hello pris en charge pour les messages cloud-à-appareil avec HTTP est connectés en permanence pour les appareils qui vérifient pour les messages rarement (inférieur à 25 minutes). Émission plus HTTP reçoit les résultats dans les demandes de hello limitation IoT Hub. Pour plus d’informations sur les différences de hello entre la prise en charge MQTT, AMQP et HTTP et de limitation IoT Hub, consultez hello [guide du développeur IoT Hub][IoT Hub developer guide - C2D].
   > 
   > 
2. Ajouter hello méthode Bonjour **principal** méthode, juste avant hello `Console.ReadLine()` ligne :
   
        ReceiveC2dAsync();

> [!NOTE]
> Par souci de simplicité, ce didacticiel n’implémente aucune stratégie de nouvelle tentative. Dans le code de production, vous devez implémenter des stratégies de nouvelle tentative (par exemple, d’interruption exponentielle), comme indiqué dans l’article hello [gestion des pannes temporaires].
> 
> 

## <a name="send-a-cloud-to-device-message"></a>Envoi d’un message cloud vers appareil
Dans cette section, vous écrivez une application console .NET qui envoie des messages cloud-à-appareil toohello appareil application.

1. Dans la solution de Visual Studio en cours de hello, créer un projet d’application de bureau Visual c# à l’aide de hello **Application Console** modèle de projet. Projet de hello nom **SendCloudToDevice**.
   
    ![Nouveau projet dans Visual Studio][20]
2. Dans l’Explorateur de solutions, cliquez sur la solution de hello, puis cliquez sur **gérer les Packages NuGet pour la Solution...** . 
   
    Cette action ouvre hello **gérer les Packages NuGet** fenêtre.
3. Recherchez **Microsoft.Azure.Devices**, cliquez sur **installer**et acceptez les conditions d’utilisation de hello. 
   
    Il télécharge, installe et ajoute une référence toohello [package NuGet du SDK du service Azure IoT].

4. Ajoutez hello suivant `using` instruction début hello Hello **Program.cs** fichier :
   
        using Microsoft.Azure.Devices;
5. Ajouter hello suivant champs toohello **programme** classe. Valeur d’espace réservé hello avec hello IoT hub chaîne de connexion de remplacement [prise en main IoT Hub]:
   
        static ServiceClient serviceClient;
        static string connectionString = "{iot hub connection string}";
6. Ajouter hello suivant de méthode toohello **programme** classe :
   
        private async static Task SendCloudToDeviceMessageAsync()
        {
            var commandMessage = new Message(Encoding.ASCII.GetBytes("Cloud toodevice message."));
            await serviceClient.SendAsync("myFirstDevice", commandMessage);
        }
   
    Cette méthode envoie un nouveau périphérique de toohello cloud-à-appareil message avec l’ID de hello, `myFirstDevice`. Modifiez ce paramètre uniquement si vous l’avez modifié à partir de hello celui utilisé dans [prise en main IoT Hub].
7. Enfin, ajoutez hello suivant lignes toohello **Main** méthode :
   
        Console.WriteLine("Send Cloud-to-Device message\n");
        serviceClient = ServiceClient.CreateFromConnectionString(connectionString);
   
        Console.WriteLine("Press any key toosend a C2D message.");
        Console.ReadLine();
        SendCloudToDeviceMessageAsync().Wait();
        Console.ReadLine();
8. Dans Visual Studio, cliquez avec le bouton droit sur votre solution et sélectionnez **Définir les projets de démarrage...**. Sélectionnez **plusieurs projets de démarrage**, puis sélectionnez hello **Démarrer** action pour **ReadDeviceToCloudMessages**, **SimulatedDevice**, et **SendCloudToDevice**.
9. Appuyez sur **F5**. Les trois applications doivent démarrer. Sélectionnez hello **SendCloudToDevice** windows, puis appuyez sur **entrée**. Vous devez voir le message de salutation reçu par l’application d’appareil hello.
   
   ![Application recevant le message][21]

## <a name="receive-delivery-feedback"></a>Réception des commentaires de remise
Il est possible de toorequest remise (ou expiration) des accusés de réception IoT Hub pour chaque message cloud-à-appareil. Cette tooeasily back-end de solution option active hello informe la logique de nouvelle tentative ou de compensation. Pour plus d’informations sur les évaluations du cloud sur l’appareil, consultez hello [guide du développeur IoT Hub][IoT Hub developer guide - C2D].

Dans cette section, vous modifiez hello **SendCloudToDevice** commentaires concernant l’application toorequest et recevoir d’IoT Hub.

1. Dans Visual Studio, Bonjour **SendCloudToDevice** de projet, ajoutez hello suivant de méthode toohello **programme** classe.
   
        private async static void ReceiveFeedbackAsync()
        {
            var feedbackReceiver = serviceClient.GetFeedbackReceiver();
   
            Console.WriteLine("\nReceiving c2d feedback from service");
            while (true)
            {
                var feedbackBatch = await feedbackReceiver.ReceiveAsync();
                if (feedbackBatch == null) continue;
   
                Console.ForegroundColor = ConsoleColor.Yellow;
                Console.WriteLine("Received feedback: {0}", string.Join(", ", feedbackBatch.Records.Select(f => f.StatusCode)));
                Console.ResetColor();
   
                await feedbackReceiver.CompleteAsync(feedbackBatch);
            }
        }
   
    Remarque : ce modèle de réception est hello les mêmes messages cloud-à-appareil tooreceive utilisé un à partir de l’application hello.
2. Ajouter hello méthode Bonjour **principal** méthode, juste après hello `serviceClient = ServiceClient.CreateFromConnectionString(connectionString)` ligne :
   
        ReceiveFeedbackAsync();
3. commentaires toorequest pour la remise de hello de votre message cloud-à-appareil, vous avez toospecify une propriété Bonjour **SendCloudToDeviceMessageAsync** (méthode). Ajouter hello suivant de ligne, juste après hello `var commandMessage = new Message(...);` ligne :
   
        commandMessage.Ack = DeliveryAcknowledgement.Full;
4. Exécuter des applications de hello en appuyant sur **F5**. Les trois applications doivent démarrer. Sélectionnez hello **SendCloudToDevice** windows, puis appuyez sur **entrée**. Vous devez voir hello de message reçus par l’application hello et après quelques secondes, hello message des commentaires reçu par votre **SendCloudToDevice** application.
   
   ![Application recevant le message][22]

> [!NOTE]
> Par souci de simplicité, ce didacticiel n’implémente aucune stratégie de nouvelle tentative. Dans le code de production, vous devez implémenter des stratégies de nouvelle tentative (par exemple, d’interruption exponentielle), comme indiqué dans l’article hello [gestion des pannes temporaires].
> 
> 

## <a name="next-steps"></a>Étapes suivantes
Dans ce didacticiel, vous avez appris comment toosend et recevoir des messages cloud-à-appareil. 

exemples de toosee des solutions de bout en bout complets qui utilisent l’IoT Hub, consultez [Azure IoT Suite].

toolearn savoir plus sur le développement de solutions avec IoT Hub, consultez hello [guide du développeur IoT Hub].

<!-- Images -->
[20]: ./media/iot-hub-csharp-csharp-c2d/create-identity-csharp1.png
[21]: ./media/iot-hub-csharp-csharp-c2d/sendc2d1.png
[22]: ./media/iot-hub-csharp-csharp-c2d/sendc2d2.png

<!-- Links -->

[package NuGet du SDK du service Azure IoT]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
[gestion des pannes temporaires]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[IoT Hub developer guide - C2D]: iot-hub-devguide-messaging.md

[guide du développeur IoT Hub]: iot-hub-devguide.md
[prise en main IoT Hub]: iot-hub-csharp-csharp-getstarted.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[Azure IoT Suite]: https://docs.microsoft.com/en-us/azure/iot-suite/
[Kits Azure IoT device SDK]: iot-hub-devguide-sdks.md