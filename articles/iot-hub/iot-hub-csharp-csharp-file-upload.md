---
title: "les fichiers à partir d’appareils tooAzure IoT Hub avec .NET aaaUpload | Documents Microsoft"
description: "Comment tooupload les fichiers à partir d’un appareil cloud toohello à l’aide de l’appareil Azure IoT SDK pour .NET. Les fichiers téléchargés sont stockés dans un conteneur d’objets blob de stockage Azure."
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: 4759d229-f856-4526-abda-414f8b00a56d
ms.service: iot-hub
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/04/2017
ms.author: elioda
ms.openlocfilehash: 07d555f6ba8b067bbd3233bc8eebaa220ad2388b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-from-your-device-toohello-cloud-with-iot-hub-using-net"></a>Télécharger des fichiers à partir de votre appareil toohello cloud avec IoT Hub à l’aide de .NET

[!INCLUDE [iot-hub-file-upload-language-selector](../../includes/iot-hub-file-upload-language-selector.md)]

Ce didacticiel s’appuie sur le code hello Bonjour [envoyer des messages Cloud-à-appareil avec IoT Hub](iot-hub-csharp-csharp-c2d.md) tooshow didacticiel vous comment toouse hello les fonctionnalités de téléchargement de fichier du IoT Hub. Cette rubrique vous explique les procédures suivantes :

- Fournissez en toute sécurité à un appareil un URI d’objet blob Azure pour le chargement d’un fichier.
- Utilisez hello IoT Hub fichier téléchargement notifications tootrigger traitement du fichier hello dans votre principal de l’application.

Hello [prise en main IoT Hub](iot-hub-csharp-csharp-getstarted.md) et [envoyer des messages Cloud-à-appareil avec IoT Hub](iot-hub-csharp-csharp-c2d.md) didacticiels montrent hello appareil-à-cloud et cloud-à-appareil messagerie fonctionnalités de base d’IoT Hub. Hello [messages processus appareil-à-Cloud](iot-hub-csharp-csharp-process-d2c.md) didacticiel décrit une façon tooreliably stocker appareil-à-cloud les messages dans le stockage blob Azure. Toutefois, dans certains scénarios vous ne peut pas mapper facilement les données de hello que vos appareils envoient en messages appareil-à-cloud relativement faible hello qui accepte une IoT Hub. Par exemple :

* Fichiers volumineux qui contiennent des images
* Vidéos
* Données de vibration échantillonnées à une fréquence élevée
* Un certain type de données prétraitées

Ces fichiers sont généralement traitées dans le cloud hello à l’aide des outils tels que par lots [Azure Data Factory](../data-factory/index.md) ou hello [Hadoop](../hdinsight/index.md) pile. Lorsque vous avez besoin des fichiers tooupload à partir d’un appareil, vous pouvez toujours utiliser sécurité de hello et la fiabilité de IoT Hub.

À la fin de hello de ce didacticiel, vous exécutez deux applications de console .NET :

* **SimulatedDevice**, une version modifiée de l’application hello créée Bonjour [envoyer des messages Cloud-à-appareil avec IoT Hub](iot-hub-csharp-csharp-c2d.md) didacticiel. Cette application télécharge une toostorage de fichier à l’aide d’un URI SAS fournie par votre hub IoT.
* **ReadFileUploadNotification**, qui reçoit les notifications de téléchargement de fichier à partir de votre IoT Hub.

> [!NOTE]
> IoT Hub offre la prise en charge de plusieurs plateformes d’appareils et plusieurs langages (notamment C, Java et Javascript) par le biais des Kits de développement logiciel (SDK) d’appareils Azure IoT. Consultez toohello [centre de développement Azure IoT] pour obtenir des instructions sur la façon de tooconnect votre tooAzure appareil IoT Hub.

toocomplete ce didacticiel, vous devez hello suivant :

* Visual Studio 2015 ou Visual Studio 2017
* Un compte Azure actif. (Si vous ne possédez pas de compte, vous pouvez créer un [compte gratuit][lnk-free-trial] en quelques minutes.)

[!INCLUDE [iot-hub-associate-storage](../../includes/iot-hub-associate-storage.md)]

## <a name="upload-a-file-from-a-device-app"></a>Charger un fichier à partir d’une application d’appareil

Dans cette section, vous modifiez l’application d’appareil hello vous avez créé dans [envoyer des messages Cloud-à-appareil avec IoT Hub](iot-hub-csharp-csharp-c2d.md) tooreceive les messages cloud-à-appareil à partir du hub IoT de hello.

1. Dans Visual Studio, avec le bouton droit hello **SimulatedDevice** de projet, cliquez sur **ajouter**, puis cliquez sur **élément existant**. Accédez de fichier d’image tooan et l’inclure dans votre projet. Ce didacticiel suppose que l’image de hello est nommée `image.jpg`.

1. Avec le bouton droit sur l’image de hello, puis cliquez sur **propriétés**. Assurez-vous que **copier tooOutput active** est défini trop**toujours copier**.

    ![][1]

1. Bonjour **Program.cs** , ajoutez hello suivant les instructions haut hello du fichier de hello :

    ```csharp
    using System.IO;
    ```

1. Ajouter hello suivant de méthode toohello **programme** classe :

    ```csharp
    private static async void SendToBlobAsync()
    {
        string fileName = "image.jpg";
        Console.WriteLine("Uploading file: {0}", fileName);
        var watch = System.Diagnostics.Stopwatch.StartNew();

        using (var sourceData = new FileStream(@"image.jpg", FileMode.Open))
        {
            await deviceClient.UploadToBlobAsync(fileName, sourceData);
        }

        watch.Stop();
        Console.WriteLine("Time tooupload file: {0}ms\n", watch.ElapsedMilliseconds);
    }
    ```

    Hello `UploadToBlobAsync` méthode accepte dans le nom de fichier hello et source de flux de hello fichier toobe téléchargé gère hello téléchargement toostorage. application de console Hello affiche hello temps fichier hello de tooupload.

1. Ajouter hello méthode Bonjour **principal** méthode, juste avant hello `Console.ReadLine()` ligne :

    ```csharp
    SendToBlobAsync();
    ```

> [!NOTE]
> Par souci de simplicité, ce didacticiel n’implémente aucune stratégie de nouvelle tentative. Dans le code de production, vous devez implémenter des stratégies de nouvelle tentative (par exemple, d’interruption exponentielle), comme indiqué dans l’article hello [gestion des pannes temporaires].

## <a name="receive-a-file-upload-notification"></a>Recevoir une notification de téléchargement de fichier

Dans cette section, vous allez écrire une application console .NET qui reçoit des messages de notification de téléchargement de fichier à partir d’IoT Hub.

1. Dans la solution de Visual Studio en cours de hello, créer un projet Windows Visual c# à l’aide de hello **Application Console** modèle de projet. Projet de hello nom **ReadFileUploadNotification**.

    ![Nouveau projet dans Visual Studio][2]

1. Dans l’Explorateur de solutions, cliquez sur hello **ReadFileUploadNotification** de projet, puis cliquez sur **gérer les Packages NuGet...** .

1. Bonjour **Gestionnaire de Package NuGet** fenêtre, recherchez **Microsoft.Azure.Devices**, cliquez sur **installer**et acceptez les conditions d’utilisation de hello.

    Cette action télécharge, installe et ajoute une référence toohello [package NuGet du SDK du service Azure IoT] Bonjour **ReadFileUploadNotification** projet.

1. Bonjour **Program.cs** , ajoutez hello suivant les instructions haut hello du fichier de hello :

    ```csharp
    using Microsoft.Azure.Devices;
    ```

1. Ajouter hello suivant champs toohello **programme** classe. Valeur d’espace réservé hello avec hello IoT hub chaîne de connexion de remplacement [prise en main IoT Hub] :

    ```csharp
    static ServiceClient serviceClient;
    static string connectionString = "{iot hub connection string}";
    ```

1. Ajouter hello suivant de méthode toohello **programme** classe :

    ```csharp
    private async static void ReceiveFileUploadNotificationAsync()
    {
        var notificationReceiver = serviceClient.GetFileNotificationReceiver();

        Console.WriteLine("\nReceiving file upload notification from service");
        while (true)
        {
            var fileUploadNotification = await notificationReceiver.ReceiveAsync();
            if (fileUploadNotification == null) continue;

            Console.ForegroundColor = ConsoleColor.Yellow;
            Console.WriteLine("Received file upload noticiation: {0}", string.Join(", ", fileUploadNotification.BlobName));
            Console.ResetColor();

            await notificationReceiver.CompleteAsync(fileUploadNotification);
        }
    }
    ```

    Remarque : ce modèle de réception est hello les mêmes messages cloud-à-appareil tooreceive utilisé un à partir de l’application hello.

1. Enfin, ajoutez hello suivant lignes toohello **Main** méthode :

    ```csharp
    Console.WriteLine("Receive file upload notifications\n");
    serviceClient = ServiceClient.CreateFromConnectionString(connectionString);
    ReceiveFileUploadNotificationAsync();
    Console.WriteLine("Press Enter tooexit\n");
    Console.ReadLine();
    ```

## <a name="run-hello-applications"></a>Exécuter des applications de hello

Vous êtes maintenant prêt toorun les applications hello.

1. Dans Visual Studio, cliquez avec le bouton droit sur votre solution et sélectionnez **Définir les projets de démarrage**. Sélectionnez **plusieurs projets de démarrage**, puis sélectionnez hello **Démarrer** action pour **ReadFileUploadNotification** et **SimulatedDevice**.

1. Appuyez sur **F5**. Les deux applications doivent démarrer. Vous devez voir le téléchargement de hello terminé dans l’application d’une même console et de message de notification de téléchargement hello reçu par hello autre application de console. Vous pouvez utiliser hello [portail Azure] ou toocheck Explorateur de serveurs Visual Studio présence hello Hello téléchargé le fichier dans votre compte de stockage Azure.

    ![][50]

## <a name="next-steps"></a>Étapes suivantes

Dans ce didacticiel, vous avez appris comment toouse hello téléchargement fonctionnalités du IoT Hub toosimplify fichier télécharge à partir d’appareils. Vous pouvez poursuivre scénarios et fonctionnalités de hub IoT tooexplore hello suivant des articles :

* [Créer un IoT Hub par programme][lnk-create-hub]
* [Introduction tooC SDK][lnk-c-sdk]
* [Kits de développement logiciel (SDK) Azure IoT][lnk-sdks]

toofurther Explorez les fonctionnalités de hello d’IoT Hub, consultez :

* [Simulation d’un appareil avec IoT Edge][lnk-iotedge]

<!-- Images. -->

[50]: ./media/iot-hub-csharp-csharp-file-upload/run-apps1.png
[1]: ./media/iot-hub-csharp-csharp-file-upload/image-properties.png
[2]: ./media/iot-hub-csharp-csharp-file-upload/file-upload-project-csharp1.png

<!-- Links -->

[portail Azure]: https://portal.azure.com/

[centre de développement Azure IoT]: http://www.azure.com/develop/iot

[gestion des pannes temporaires]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[package NuGet du SDK du service Azure IoT]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[lnk-create-hub]: iot-hub-rm-template-powershell.md
[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-windows-iot-edge-simulated-device.md
