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
# <a name="upload-files-from-your-device-toohello-cloud-with-iot-hub-using-net"></a><span data-ttu-id="b3b59-104">Télécharger des fichiers à partir de votre appareil toohello cloud avec IoT Hub à l’aide de .NET</span><span class="sxs-lookup"><span data-stu-id="b3b59-104">Upload files from your device toohello cloud with IoT Hub using .NET</span></span>

[!INCLUDE [iot-hub-file-upload-language-selector](../../includes/iot-hub-file-upload-language-selector.md)]

<span data-ttu-id="b3b59-105">Ce didacticiel s’appuie sur le code hello Bonjour [envoyer des messages Cloud-à-appareil avec IoT Hub](iot-hub-csharp-csharp-c2d.md) tooshow didacticiel vous comment toouse hello les fonctionnalités de téléchargement de fichier du IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="b3b59-105">This tutorial builds on hello code in hello [Send Cloud-to-Device messages with IoT Hub](iot-hub-csharp-csharp-c2d.md) tutorial tooshow you how toouse hello file upload capabilities of IoT Hub.</span></span> <span data-ttu-id="b3b59-106">Cette rubrique vous explique les procédures suivantes :</span><span class="sxs-lookup"><span data-stu-id="b3b59-106">It shows you how to:</span></span>

- <span data-ttu-id="b3b59-107">Fournissez en toute sécurité à un appareil un URI d’objet blob Azure pour le chargement d’un fichier.</span><span class="sxs-lookup"><span data-stu-id="b3b59-107">Securely provide a device with an Azure blob URI for uploading a file.</span></span>
- <span data-ttu-id="b3b59-108">Utilisez hello IoT Hub fichier téléchargement notifications tootrigger traitement du fichier hello dans votre principal de l’application.</span><span class="sxs-lookup"><span data-stu-id="b3b59-108">Use hello IoT Hub file upload notifications tootrigger processing hello file in your app back end.</span></span>

<span data-ttu-id="b3b59-109">Hello [prise en main IoT Hub](iot-hub-csharp-csharp-getstarted.md) et [envoyer des messages Cloud-à-appareil avec IoT Hub](iot-hub-csharp-csharp-c2d.md) didacticiels montrent hello appareil-à-cloud et cloud-à-appareil messagerie fonctionnalités de base d’IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="b3b59-109">hello [Get started with IoT Hub](iot-hub-csharp-csharp-getstarted.md) and [Send Cloud-to-Device messages with IoT Hub](iot-hub-csharp-csharp-c2d.md) tutorials show hello basic device-to-cloud and cloud-to-device messaging functionality of IoT Hub.</span></span> <span data-ttu-id="b3b59-110">Hello [messages processus appareil-à-Cloud](iot-hub-csharp-csharp-process-d2c.md) didacticiel décrit une façon tooreliably stocker appareil-à-cloud les messages dans le stockage blob Azure.</span><span class="sxs-lookup"><span data-stu-id="b3b59-110">hello [Process Device-to-Cloud messages](iot-hub-csharp-csharp-process-d2c.md) tutorial describes a way tooreliably store device-to-cloud messages in Azure blob storage.</span></span> <span data-ttu-id="b3b59-111">Toutefois, dans certains scénarios vous ne peut pas mapper facilement les données de hello que vos appareils envoient en messages appareil-à-cloud relativement faible hello qui accepte une IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="b3b59-111">However, in some scenarios you cannot easily map hello data your devices send into hello relatively small device-to-cloud messages that IoT Hub accepts.</span></span> <span data-ttu-id="b3b59-112">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="b3b59-112">For example:</span></span>

* <span data-ttu-id="b3b59-113">Fichiers volumineux qui contiennent des images</span><span class="sxs-lookup"><span data-stu-id="b3b59-113">Large files that contain images</span></span>
* <span data-ttu-id="b3b59-114">Vidéos</span><span class="sxs-lookup"><span data-stu-id="b3b59-114">Videos</span></span>
* <span data-ttu-id="b3b59-115">Données de vibration échantillonnées à une fréquence élevée</span><span class="sxs-lookup"><span data-stu-id="b3b59-115">Vibration data sampled at high frequency</span></span>
* <span data-ttu-id="b3b59-116">Un certain type de données prétraitées</span><span class="sxs-lookup"><span data-stu-id="b3b59-116">Some form of preprocessed data</span></span>

<span data-ttu-id="b3b59-117">Ces fichiers sont généralement traitées dans le cloud hello à l’aide des outils tels que par lots [Azure Data Factory](../data-factory/index.md) ou hello [Hadoop](../hdinsight/index.md) pile.</span><span class="sxs-lookup"><span data-stu-id="b3b59-117">These files are typically batch processed in hello cloud using tools such as [Azure Data Factory](../data-factory/index.md) or hello [Hadoop](../hdinsight/index.md) stack.</span></span> <span data-ttu-id="b3b59-118">Lorsque vous avez besoin des fichiers tooupload à partir d’un appareil, vous pouvez toujours utiliser sécurité de hello et la fiabilité de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="b3b59-118">When you need tooupload files from a device, you can still use hello security and reliability of IoT Hub.</span></span>

<span data-ttu-id="b3b59-119">À la fin de hello de ce didacticiel, vous exécutez deux applications de console .NET :</span><span class="sxs-lookup"><span data-stu-id="b3b59-119">At hello end of this tutorial you run two .NET console apps:</span></span>

* <span data-ttu-id="b3b59-120">**SimulatedDevice**, une version modifiée de l’application hello créée Bonjour [envoyer des messages Cloud-à-appareil avec IoT Hub](iot-hub-csharp-csharp-c2d.md) didacticiel.</span><span class="sxs-lookup"><span data-stu-id="b3b59-120">**SimulatedDevice**, a modified version of hello app created in hello [Send Cloud-to-Device messages with IoT Hub](iot-hub-csharp-csharp-c2d.md) tutorial.</span></span> <span data-ttu-id="b3b59-121">Cette application télécharge une toostorage de fichier à l’aide d’un URI SAS fournie par votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="b3b59-121">This app uploads a file toostorage using a SAS URI provided by your IoT hub.</span></span>
* <span data-ttu-id="b3b59-122">**ReadFileUploadNotification**, qui reçoit les notifications de téléchargement de fichier à partir de votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="b3b59-122">**ReadFileUploadNotification**, which receives file upload notifications from your IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="b3b59-123">IoT Hub offre la prise en charge de plusieurs plateformes d’appareils et plusieurs langages (notamment C, Java et Javascript) par le biais des Kits de développement logiciel (SDK) d’appareils Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="b3b59-123">IoT Hub supports many device platforms and languages (including C, Java, and Javascript) through Azure IoT device SDKs.</span></span> <span data-ttu-id="b3b59-124">Consultez toohello [centre de développement Azure IoT] pour obtenir des instructions sur la façon de tooconnect votre tooAzure appareil IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="b3b59-124">Refer toohello [Azure IoT Developer Center] for step-by-step instructions on how tooconnect your device tooAzure IoT Hub.</span></span>

<span data-ttu-id="b3b59-125">toocomplete ce didacticiel, vous devez hello suivant :</span><span class="sxs-lookup"><span data-stu-id="b3b59-125">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="b3b59-126">Visual Studio 2015 ou Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="b3b59-126">Visual Studio 2015 or Visual Studio 2017</span></span>
* <span data-ttu-id="b3b59-127">Un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="b3b59-127">An active Azure account.</span></span> <span data-ttu-id="b3b59-128">(Si vous ne possédez pas de compte, vous pouvez créer un [compte gratuit][lnk-free-trial] en quelques minutes.)</span><span class="sxs-lookup"><span data-stu-id="b3b59-128">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-associate-storage](../../includes/iot-hub-associate-storage.md)]

## <a name="upload-a-file-from-a-device-app"></a><span data-ttu-id="b3b59-129">Charger un fichier à partir d’une application d’appareil</span><span class="sxs-lookup"><span data-stu-id="b3b59-129">Upload a file from a device app</span></span>

<span data-ttu-id="b3b59-130">Dans cette section, vous modifiez l’application d’appareil hello vous avez créé dans [envoyer des messages Cloud-à-appareil avec IoT Hub](iot-hub-csharp-csharp-c2d.md) tooreceive les messages cloud-à-appareil à partir du hub IoT de hello.</span><span class="sxs-lookup"><span data-stu-id="b3b59-130">In this section, you modify hello device app you created in [Send Cloud-to-Device messages with IoT Hub](iot-hub-csharp-csharp-c2d.md) tooreceive cloud-to-device messages from hello IoT hub.</span></span>

1. <span data-ttu-id="b3b59-131">Dans Visual Studio, avec le bouton droit hello **SimulatedDevice** de projet, cliquez sur **ajouter**, puis cliquez sur **élément existant**.</span><span class="sxs-lookup"><span data-stu-id="b3b59-131">In Visual Studio, right-click hello **SimulatedDevice** project, click **Add**, and then click **Existing Item**.</span></span> <span data-ttu-id="b3b59-132">Accédez de fichier d’image tooan et l’inclure dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="b3b59-132">Navigate tooan image file and include it in your project.</span></span> <span data-ttu-id="b3b59-133">Ce didacticiel suppose que l’image de hello est nommée `image.jpg`.</span><span class="sxs-lookup"><span data-stu-id="b3b59-133">This tutorial assumes hello image is named `image.jpg`.</span></span>

1. <span data-ttu-id="b3b59-134">Avec le bouton droit sur l’image de hello, puis cliquez sur **propriétés**.</span><span class="sxs-lookup"><span data-stu-id="b3b59-134">Right-click on hello image, and then click **Properties**.</span></span> <span data-ttu-id="b3b59-135">Assurez-vous que **copier tooOutput active** est défini trop**toujours copier**.</span><span class="sxs-lookup"><span data-stu-id="b3b59-135">Make sure that **Copy tooOutput Directory** is set too**Copy always**.</span></span>

    ![][1]

1. <span data-ttu-id="b3b59-136">Bonjour **Program.cs** , ajoutez hello suivant les instructions haut hello du fichier de hello :</span><span class="sxs-lookup"><span data-stu-id="b3b59-136">In hello **Program.cs** file, add hello following statements at hello top of hello file:</span></span>

    ```csharp
    using System.IO;
    ```

1. <span data-ttu-id="b3b59-137">Ajouter hello suivant de méthode toohello **programme** classe :</span><span class="sxs-lookup"><span data-stu-id="b3b59-137">Add hello following method toohello **Program** class:</span></span>

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

    <span data-ttu-id="b3b59-138">Hello `UploadToBlobAsync` méthode accepte dans le nom de fichier hello et source de flux de hello fichier toobe téléchargé gère hello téléchargement toostorage.</span><span class="sxs-lookup"><span data-stu-id="b3b59-138">hello `UploadToBlobAsync` method takes in hello file name and stream source of hello file toobe uploaded and handles hello upload toostorage.</span></span> <span data-ttu-id="b3b59-139">application de console Hello affiche hello temps fichier hello de tooupload.</span><span class="sxs-lookup"><span data-stu-id="b3b59-139">hello console app displays hello time it takes tooupload hello file.</span></span>

1. <span data-ttu-id="b3b59-140">Ajouter hello méthode Bonjour **principal** méthode, juste avant hello `Console.ReadLine()` ligne :</span><span class="sxs-lookup"><span data-stu-id="b3b59-140">Add hello following method in hello **Main** method, right before hello `Console.ReadLine()` line:</span></span>

    ```csharp
    SendToBlobAsync();
    ```

> [!NOTE]
> <span data-ttu-id="b3b59-141">Par souci de simplicité, ce didacticiel n’implémente aucune stratégie de nouvelle tentative.</span><span class="sxs-lookup"><span data-stu-id="b3b59-141">For simplicity's sake, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="b3b59-142">Dans le code de production, vous devez implémenter des stratégies de nouvelle tentative (par exemple, d’interruption exponentielle), comme indiqué dans l’article hello [gestion des pannes temporaires].</span><span class="sxs-lookup"><span data-stu-id="b3b59-142">In production code, you should implement retry policies (such as exponential backoff), as suggested in hello MSDN article [Transient Fault Handling].</span></span>

## <a name="receive-a-file-upload-notification"></a><span data-ttu-id="b3b59-143">Recevoir une notification de téléchargement de fichier</span><span class="sxs-lookup"><span data-stu-id="b3b59-143">Receive a file upload notification</span></span>

<span data-ttu-id="b3b59-144">Dans cette section, vous allez écrire une application console .NET qui reçoit des messages de notification de téléchargement de fichier à partir d’IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="b3b59-144">In this section, you write a .NET console app that receives file upload notification messages from IoT Hub.</span></span>

1. <span data-ttu-id="b3b59-145">Dans la solution de Visual Studio en cours de hello, créer un projet Windows Visual c# à l’aide de hello **Application Console** modèle de projet.</span><span class="sxs-lookup"><span data-stu-id="b3b59-145">In hello current Visual Studio solution, create a Visual C# Windows project by using hello **Console Application** project template.</span></span> <span data-ttu-id="b3b59-146">Projet de hello nom **ReadFileUploadNotification**.</span><span class="sxs-lookup"><span data-stu-id="b3b59-146">Name hello project **ReadFileUploadNotification**.</span></span>

    ![Nouveau projet dans Visual Studio][2]

1. <span data-ttu-id="b3b59-148">Dans l’Explorateur de solutions, cliquez sur hello **ReadFileUploadNotification** de projet, puis cliquez sur **gérer les Packages NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="b3b59-148">In Solution Explorer, right-click hello **ReadFileUploadNotification** project, and then click **Manage NuGet Packages...**.</span></span>

1. <span data-ttu-id="b3b59-149">Bonjour **Gestionnaire de Package NuGet** fenêtre, recherchez **Microsoft.Azure.Devices**, cliquez sur **installer**et acceptez les conditions d’utilisation de hello.</span><span class="sxs-lookup"><span data-stu-id="b3b59-149">In hello **NuGet Package Manager** window, search for **Microsoft.Azure.Devices**, click **Install**, and accept hello terms of use.</span></span>

    <span data-ttu-id="b3b59-150">Cette action télécharge, installe et ajoute une référence toohello [package NuGet du SDK du service Azure IoT] Bonjour **ReadFileUploadNotification** projet.</span><span class="sxs-lookup"><span data-stu-id="b3b59-150">This action downloads, installs, and adds a reference toohello [Azure IoT service SDK NuGet package] in hello **ReadFileUploadNotification** project.</span></span>

1. <span data-ttu-id="b3b59-151">Bonjour **Program.cs** , ajoutez hello suivant les instructions haut hello du fichier de hello :</span><span class="sxs-lookup"><span data-stu-id="b3b59-151">In hello **Program.cs** file, add hello following statements at hello top of hello file:</span></span>

    ```csharp
    using Microsoft.Azure.Devices;
    ```

1. <span data-ttu-id="b3b59-152">Ajouter hello suivant champs toohello **programme** classe.</span><span class="sxs-lookup"><span data-stu-id="b3b59-152">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="b3b59-153">Valeur d’espace réservé hello avec hello IoT hub chaîne de connexion de remplacement [prise en main IoT Hub] :</span><span class="sxs-lookup"><span data-stu-id="b3b59-153">Substitute hello placeholder value with hello IoT hub connection string from [Get started with IoT Hub]:</span></span>

    ```csharp
    static ServiceClient serviceClient;
    static string connectionString = "{iot hub connection string}";
    ```

1. <span data-ttu-id="b3b59-154">Ajouter hello suivant de méthode toohello **programme** classe :</span><span class="sxs-lookup"><span data-stu-id="b3b59-154">Add hello following method toohello **Program** class:</span></span>

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

    <span data-ttu-id="b3b59-155">Remarque : ce modèle de réception est hello les mêmes messages cloud-à-appareil tooreceive utilisé un à partir de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="b3b59-155">Note this receive pattern is hello same one used tooreceive cloud-to-device messages from hello device app.</span></span>

1. <span data-ttu-id="b3b59-156">Enfin, ajoutez hello suivant lignes toohello **Main** méthode :</span><span class="sxs-lookup"><span data-stu-id="b3b59-156">Finally, add hello following lines toohello **Main** method:</span></span>

    ```csharp
    Console.WriteLine("Receive file upload notifications\n");
    serviceClient = ServiceClient.CreateFromConnectionString(connectionString);
    ReceiveFileUploadNotificationAsync();
    Console.WriteLine("Press Enter tooexit\n");
    Console.ReadLine();
    ```

## <a name="run-hello-applications"></a><span data-ttu-id="b3b59-157">Exécuter des applications de hello</span><span class="sxs-lookup"><span data-stu-id="b3b59-157">Run hello applications</span></span>

<span data-ttu-id="b3b59-158">Vous êtes maintenant prêt toorun les applications hello.</span><span class="sxs-lookup"><span data-stu-id="b3b59-158">Now you are ready toorun hello applications.</span></span>

1. <span data-ttu-id="b3b59-159">Dans Visual Studio, cliquez avec le bouton droit sur votre solution et sélectionnez **Définir les projets de démarrage**.</span><span class="sxs-lookup"><span data-stu-id="b3b59-159">In Visual Studio, right-click your solution, and select **Set StartUp projects**.</span></span> <span data-ttu-id="b3b59-160">Sélectionnez **plusieurs projets de démarrage**, puis sélectionnez hello **Démarrer** action pour **ReadFileUploadNotification** et **SimulatedDevice**.</span><span class="sxs-lookup"><span data-stu-id="b3b59-160">Select **Multiple startup projects**, then select hello **Start** action for **ReadFileUploadNotification** and **SimulatedDevice**.</span></span>

1. <span data-ttu-id="b3b59-161">Appuyez sur **F5**.</span><span class="sxs-lookup"><span data-stu-id="b3b59-161">Press **F5**.</span></span> <span data-ttu-id="b3b59-162">Les deux applications doivent démarrer.</span><span class="sxs-lookup"><span data-stu-id="b3b59-162">Both applications should start.</span></span> <span data-ttu-id="b3b59-163">Vous devez voir le téléchargement de hello terminé dans l’application d’une même console et de message de notification de téléchargement hello reçu par hello autre application de console.</span><span class="sxs-lookup"><span data-stu-id="b3b59-163">You should see hello upload completed in one console app and hello upload notification message received by hello other console app.</span></span> <span data-ttu-id="b3b59-164">Vous pouvez utiliser hello [portail Azure] ou toocheck Explorateur de serveurs Visual Studio présence hello Hello téléchargé le fichier dans votre compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="b3b59-164">You can use hello [Azure portal] or Visual Studio Server Explorer toocheck for hello presence of hello uploaded file in your Azure Storage account.</span></span>

    ![][50]

## <a name="next-steps"></a><span data-ttu-id="b3b59-165">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b3b59-165">Next steps</span></span>

<span data-ttu-id="b3b59-166">Dans ce didacticiel, vous avez appris comment toouse hello téléchargement fonctionnalités du IoT Hub toosimplify fichier télécharge à partir d’appareils.</span><span class="sxs-lookup"><span data-stu-id="b3b59-166">In this tutorial, you learned how toouse hello file upload capabilities of IoT Hub toosimplify file uploads from devices.</span></span> <span data-ttu-id="b3b59-167">Vous pouvez poursuivre scénarios et fonctionnalités de hub IoT tooexplore hello suivant des articles :</span><span class="sxs-lookup"><span data-stu-id="b3b59-167">You can continue tooexplore IoT hub features and scenarios with hello following articles:</span></span>

* <span data-ttu-id="b3b59-168">[Créer un IoT Hub par programme][lnk-create-hub]</span><span class="sxs-lookup"><span data-stu-id="b3b59-168">[Create an IoT hub programmatically][lnk-create-hub]</span></span>
* <span data-ttu-id="b3b59-169">[Introduction tooC SDK][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="b3b59-169">[Introduction tooC SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="b3b59-170">[Kits de développement logiciel (SDK) Azure IoT][lnk-sdks]</span><span class="sxs-lookup"><span data-stu-id="b3b59-170">[Azure IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="b3b59-171">toofurther Explorez les fonctionnalités de hello d’IoT Hub, consultez :</span><span class="sxs-lookup"><span data-stu-id="b3b59-171">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="b3b59-172">[Simulation d’un appareil avec IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="b3b59-172">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>

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
