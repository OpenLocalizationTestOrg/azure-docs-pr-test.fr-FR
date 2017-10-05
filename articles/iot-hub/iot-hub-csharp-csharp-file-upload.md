---
title: "Charger des fichiers sur Azure IoT Hub à partir d’appareils avec .NET | Microsoft Docs"
description: "Comment charger des fichiers sur le cloud à partir d’un appareil avec Azure IoT device SDK pour .NET. Les fichiers téléchargés sont stockés dans un conteneur d’objets blob de stockage Azure."
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
ms.openlocfilehash: b45d85d0d77cf47f36cb793bc8c0dbe2d5c12634
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="upload-files-from-your-device-to-the-cloud-with-iot-hub-using-net"></a><span data-ttu-id="90818-104">Charger des fichiers sur le cloud à partir d’un appareil avec IoT Hub en utilisant .NET</span><span class="sxs-lookup"><span data-stu-id="90818-104">Upload files from your device to the cloud with IoT Hub using .NET</span></span>

[!INCLUDE [iot-hub-file-upload-language-selector](../../includes/iot-hub-file-upload-language-selector.md)]

<span data-ttu-id="90818-105">Ce didacticiel s’appuie sur le code du didacticiel [Envoi de messages cloud à appareil avec IoT Hub](iot-hub-csharp-csharp-c2d.md) pour vous montrer comment utiliser les fonctions de téléchargement de fichier d’IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="90818-105">This tutorial builds on the code in the [Send Cloud-to-Device messages with IoT Hub](iot-hub-csharp-csharp-c2d.md) tutorial to show you how to use the file upload capabilities of IoT Hub.</span></span> <span data-ttu-id="90818-106">Cette rubrique vous explique les procédures suivantes :</span><span class="sxs-lookup"><span data-stu-id="90818-106">It shows you how to:</span></span>

- <span data-ttu-id="90818-107">Fournissez en toute sécurité à un appareil un URI d’objet blob Azure pour le chargement d’un fichier.</span><span class="sxs-lookup"><span data-stu-id="90818-107">Securely provide a device with an Azure blob URI for uploading a file.</span></span>
- <span data-ttu-id="90818-108">Utilisez les notifications de chargement de fichier IoT Hub pour déclencher le traitement du fichier dans votre serveur principal d’application.</span><span class="sxs-lookup"><span data-stu-id="90818-108">Use the IoT Hub file upload notifications to trigger processing the file in your app back end.</span></span>

<span data-ttu-id="90818-109">Les didacticiels [Bien démarrer avec IoT Hub](iot-hub-csharp-csharp-getstarted.md) et [Envoyer des messages du cloud vers un appareil avec IoT Hub](iot-hub-csharp-csharp-c2d.md) illustrent les fonctionnalités de base de la messagerie d’un appareil vers le cloud et du cloud vers un appareil offertes par IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="90818-109">The [Get started with IoT Hub](iot-hub-csharp-csharp-getstarted.md) and [Send Cloud-to-Device messages with IoT Hub](iot-hub-csharp-csharp-c2d.md) tutorials show the basic device-to-cloud and cloud-to-device messaging functionality of IoT Hub.</span></span> <span data-ttu-id="90818-110">Le didacticiel [Traiter les messages appareil-à-cloud](iot-hub-csharp-csharp-process-d2c.md) décrit un moyen de stocker en toute fiabilité les messages appareil-à-cloud dans le stockage d’objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="90818-110">The [Process Device-to-Cloud messages](iot-hub-csharp-csharp-process-d2c.md) tutorial describes a way to reliably store device-to-cloud messages in Azure blob storage.</span></span> <span data-ttu-id="90818-111">Toutefois, dans certains scénarios, vous ne pouvez pas facilement mapper les données que vos appareils envoient dans des messages appareil-à-cloud relativement petits et acceptés par IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="90818-111">However, in some scenarios you cannot easily map the data your devices send into the relatively small device-to-cloud messages that IoT Hub accepts.</span></span> <span data-ttu-id="90818-112">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="90818-112">For example:</span></span>

* <span data-ttu-id="90818-113">Fichiers volumineux qui contiennent des images</span><span class="sxs-lookup"><span data-stu-id="90818-113">Large files that contain images</span></span>
* <span data-ttu-id="90818-114">Vidéos</span><span class="sxs-lookup"><span data-stu-id="90818-114">Videos</span></span>
* <span data-ttu-id="90818-115">Données de vibration échantillonnées à une fréquence élevée</span><span class="sxs-lookup"><span data-stu-id="90818-115">Vibration data sampled at high frequency</span></span>
* <span data-ttu-id="90818-116">Un certain type de données prétraitées</span><span class="sxs-lookup"><span data-stu-id="90818-116">Some form of preprocessed data</span></span>

<span data-ttu-id="90818-117">Ces fichiers sont généralement traités par lot dans le cloud à l’aide d’outils tels que [Azure Data Factory](../data-factory/index.md) ou de la pile [Hadoop](../hdinsight/index.md).</span><span class="sxs-lookup"><span data-stu-id="90818-117">These files are typically batch processed in the cloud using tools such as [Azure Data Factory](../data-factory/index.md) or the [Hadoop](../hdinsight/index.md) stack.</span></span> <span data-ttu-id="90818-118">Si vous avez besoin de charger des fichiers à partir d’un appareil, vous pouvez toujours exploiter la sécurité et la fiabilité d’IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="90818-118">When you need to upload files from a device, you can still use the security and reliability of IoT Hub.</span></span>

<span data-ttu-id="90818-119">À la fin de ce didacticiel, vous exécutez deux applications console .NET :</span><span class="sxs-lookup"><span data-stu-id="90818-119">At the end of this tutorial you run two .NET console apps:</span></span>

* <span data-ttu-id="90818-120">**SimulatedDevice**, version modifiée de l’application créée dans le cadre du didacticiel [Envoyer des messages cloud-à-appareil avec IoT Hub](iot-hub-csharp-csharp-c2d.md).</span><span class="sxs-lookup"><span data-stu-id="90818-120">**SimulatedDevice**, a modified version of the app created in the [Send Cloud-to-Device messages with IoT Hub](iot-hub-csharp-csharp-c2d.md) tutorial.</span></span> <span data-ttu-id="90818-121">Cette application charge un fichier de stockage à l’aide d’un URI SAP fourni par votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="90818-121">This app uploads a file to storage using a SAS URI provided by your IoT hub.</span></span>
* <span data-ttu-id="90818-122">**ReadFileUploadNotification**, qui reçoit les notifications de téléchargement de fichier à partir de votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="90818-122">**ReadFileUploadNotification**, which receives file upload notifications from your IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="90818-123">IoT Hub offre la prise en charge de plusieurs plateformes d’appareils et plusieurs langages (notamment C, Java et Javascript) par le biais des Kits de développement logiciel (SDK) d’appareils Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="90818-123">IoT Hub supports many device platforms and languages (including C, Java, and Javascript) through Azure IoT device SDKs.</span></span> <span data-ttu-id="90818-124">Pour obtenir des instructions pas à pas expliquant comment connecter votre appareil à Azure IoT Hub, voir le [Centre de développement Azure IoT].</span><span class="sxs-lookup"><span data-stu-id="90818-124">Refer to the [Azure IoT Developer Center] for step-by-step instructions on how to connect your device to Azure IoT Hub.</span></span>

<span data-ttu-id="90818-125">Pour réaliser ce didacticiel, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="90818-125">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="90818-126">Visual Studio 2015 ou Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="90818-126">Visual Studio 2015 or Visual Studio 2017</span></span>
* <span data-ttu-id="90818-127">Un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="90818-127">An active Azure account.</span></span> <span data-ttu-id="90818-128">(Si vous ne possédez pas de compte, vous pouvez créer un [compte gratuit][lnk-free-trial] en quelques minutes.)</span><span class="sxs-lookup"><span data-stu-id="90818-128">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-associate-storage](../../includes/iot-hub-associate-storage.md)]

## <a name="upload-a-file-from-a-device-app"></a><span data-ttu-id="90818-129">Charger un fichier à partir d’une application d’appareil</span><span class="sxs-lookup"><span data-stu-id="90818-129">Upload a file from a device app</span></span>

<span data-ttu-id="90818-130">Dans cette section, vous allez modifier l’application d’appareil créée dans [Envoyer des messages du cloud à votre appareil avec IoT Hub](iot-hub-csharp-csharp-c2d.md) pour recevoir des messages cloud-à-appareil en provenance de l’IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="90818-130">In this section, you modify the device app you created in [Send Cloud-to-Device messages with IoT Hub](iot-hub-csharp-csharp-c2d.md) to receive cloud-to-device messages from the IoT hub.</span></span>

1. <span data-ttu-id="90818-131">Dans Visual Studio, cliquez avec le bouton droit sur le projet **SimulatedDevice**, cliquez sur **Ajouter**, puis sur **Élément existant**.</span><span class="sxs-lookup"><span data-stu-id="90818-131">In Visual Studio, right-click the **SimulatedDevice** project, click **Add**, and then click **Existing Item**.</span></span> <span data-ttu-id="90818-132">Accédez à un fichier image et ajoutez-le à votre projet.</span><span class="sxs-lookup"><span data-stu-id="90818-132">Navigate to an image file and include it in your project.</span></span> <span data-ttu-id="90818-133">Ce didacticiel suppose que l’image a pour nom `image.jpg`.</span><span class="sxs-lookup"><span data-stu-id="90818-133">This tutorial assumes the image is named `image.jpg`.</span></span>

1. <span data-ttu-id="90818-134">Cliquez avec le bouton droit sur l’image, puis cliquez sur **Propriétés**.</span><span class="sxs-lookup"><span data-stu-id="90818-134">Right-click on the image, and then click **Properties**.</span></span> <span data-ttu-id="90818-135">Assurez-vous que l’option **Copier dans le répertoire de sortie** est définie sur **Toujours copier**.</span><span class="sxs-lookup"><span data-stu-id="90818-135">Make sure that **Copy to Output Directory** is set to **Copy always**.</span></span>

    ![][1]

1. <span data-ttu-id="90818-136">Au début du fichier **Program.cs** , ajoutez les instructions suivantes :</span><span class="sxs-lookup"><span data-stu-id="90818-136">In the **Program.cs** file, add the following statements at the top of the file:</span></span>

    ```csharp
    using System.IO;
    ```

1. <span data-ttu-id="90818-137">Ajoutez la méthode suivante à la classe **Program** :</span><span class="sxs-lookup"><span data-stu-id="90818-137">Add the following method to the **Program** class:</span></span>

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
        Console.WriteLine("Time to upload file: {0}ms\n", watch.ElapsedMilliseconds);
    }
    ```

    <span data-ttu-id="90818-138">La méthode `UploadToBlobAsync` utilise le nom de fichier et la source de flux du fichier à télécharger et gère le téléchargement vers le stockage.</span><span class="sxs-lookup"><span data-stu-id="90818-138">The `UploadToBlobAsync` method takes in the file name and stream source of the file to be uploaded and handles the upload to storage.</span></span> <span data-ttu-id="90818-139">L’application console affiche le temps nécessaire pour télécharger le fichier.</span><span class="sxs-lookup"><span data-stu-id="90818-139">The console app displays the time it takes to upload the file.</span></span>

1. <span data-ttu-id="90818-140">Ajoutez la méthode suivante à la méthode **Main** juste avant la ligne `Console.ReadLine()` :</span><span class="sxs-lookup"><span data-stu-id="90818-140">Add the following method in the **Main** method, right before the `Console.ReadLine()` line:</span></span>

    ```csharp
    SendToBlobAsync();
    ```

> [!NOTE]
> <span data-ttu-id="90818-141">Par souci de simplicité, ce didacticiel n’implémente aucune stratégie de nouvelle tentative.</span><span class="sxs-lookup"><span data-stu-id="90818-141">For simplicity's sake, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="90818-142">Dans le code de production, vous devez mettre en œuvre des stratégies de nouvelle tentative (par exemple, une interruption exponentielle), comme indiqué dans l’article MSDN [Transient Fault Handling](Gestion des erreurs temporaires).</span><span class="sxs-lookup"><span data-stu-id="90818-142">In production code, you should implement retry policies (such as exponential backoff), as suggested in the MSDN article [Transient Fault Handling].</span></span>

## <a name="receive-a-file-upload-notification"></a><span data-ttu-id="90818-143">Recevoir une notification de téléchargement de fichier</span><span class="sxs-lookup"><span data-stu-id="90818-143">Receive a file upload notification</span></span>

<span data-ttu-id="90818-144">Dans cette section, vous allez écrire une application console .NET qui reçoit des messages de notification de téléchargement de fichier à partir d’IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="90818-144">In this section, you write a .NET console app that receives file upload notification messages from IoT Hub.</span></span>

1. <span data-ttu-id="90818-145">Dans la solution Visual Studio actuelle, créez un projet Windows Visual C# à l’aide du modèle de projet **d’application de console** .</span><span class="sxs-lookup"><span data-stu-id="90818-145">In the current Visual Studio solution, create a Visual C# Windows project by using the **Console Application** project template.</span></span> <span data-ttu-id="90818-146">Nommez le projet **ReadFileUploadNotification**.</span><span class="sxs-lookup"><span data-stu-id="90818-146">Name the project **ReadFileUploadNotification**.</span></span>

    ![Nouveau projet dans Visual Studio][2]

1. <span data-ttu-id="90818-148">Dans l’Explorateur de solutions, cliquez avec le bouton droit sur le projet **ReadFileUploadNotification**, puis cliquez sur **Gérer les packages NuGet...**.</span><span class="sxs-lookup"><span data-stu-id="90818-148">In Solution Explorer, right-click the **ReadFileUploadNotification** project, and then click **Manage NuGet Packages...**.</span></span>

1. <span data-ttu-id="90818-149">Dans la fenêtre **Gestionnaire de package NuGet**, recherchez **Microsoft.Azure.Devices**, cliquez sur **Installer** et acceptez les conditions d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="90818-149">In the **NuGet Package Manager** window, search for **Microsoft.Azure.Devices**, click **Install**, and accept the terms of use.</span></span>

    <span data-ttu-id="90818-150">Cette action a pour effet de télécharger, d’installer et d’ajouter une référence au [Package NuGet du SDK service IoT Azure] dans le projet **ReadFileUploadNotification**.</span><span class="sxs-lookup"><span data-stu-id="90818-150">This action downloads, installs, and adds a reference to the [Azure IoT service SDK NuGet package] in the **ReadFileUploadNotification** project.</span></span>

1. <span data-ttu-id="90818-151">Au début du fichier **Program.cs** , ajoutez les instructions suivantes :</span><span class="sxs-lookup"><span data-stu-id="90818-151">In the **Program.cs** file, add the following statements at the top of the file:</span></span>

    ```csharp
    using Microsoft.Azure.Devices;
    ```

1. <span data-ttu-id="90818-152">Ajoutez les champs suivants à la classe **Program** .</span><span class="sxs-lookup"><span data-stu-id="90818-152">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="90818-153">Remplacez la valeur d’espace réservé par la chaîne de connexion de l’IoT Hub obtenue dans le didacticiel [Prise en main d’Azure IoT Hub] :</span><span class="sxs-lookup"><span data-stu-id="90818-153">Substitute the placeholder value with the IoT hub connection string from [Get started with IoT Hub]:</span></span>

    ```csharp
    static ServiceClient serviceClient;
    static string connectionString = "{iot hub connection string}";
    ```

1. <span data-ttu-id="90818-154">Ajoutez la méthode suivante à la classe **Program** :</span><span class="sxs-lookup"><span data-stu-id="90818-154">Add the following method to the **Program** class:</span></span>

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

    <span data-ttu-id="90818-155">Notez que ce modèle de réception est le même que celui utilisé pour recevoir des messages cloud-à-appareil à partir de l’application de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="90818-155">Note this receive pattern is the same one used to receive cloud-to-device messages from the device app.</span></span>

1. <span data-ttu-id="90818-156">Enfin, ajoutez les lignes suivantes à la méthode **Main** :</span><span class="sxs-lookup"><span data-stu-id="90818-156">Finally, add the following lines to the **Main** method:</span></span>

    ```csharp
    Console.WriteLine("Receive file upload notifications\n");
    serviceClient = ServiceClient.CreateFromConnectionString(connectionString);
    ReceiveFileUploadNotificationAsync();
    Console.WriteLine("Press Enter to exit\n");
    Console.ReadLine();
    ```

## <a name="run-the-applications"></a><span data-ttu-id="90818-157">Exécution des applications</span><span class="sxs-lookup"><span data-stu-id="90818-157">Run the applications</span></span>

<span data-ttu-id="90818-158">Vous êtes maintenant prêt à exécuter les applications.</span><span class="sxs-lookup"><span data-stu-id="90818-158">Now you are ready to run the applications.</span></span>

1. <span data-ttu-id="90818-159">Dans Visual Studio, cliquez avec le bouton droit sur votre solution et sélectionnez **Définir les projets de démarrage**.</span><span class="sxs-lookup"><span data-stu-id="90818-159">In Visual Studio, right-click your solution, and select **Set StartUp projects**.</span></span> <span data-ttu-id="90818-160">Sélectionnez **Plusieurs projets de démarrage**, puis sélectionnez l’action **Démarrer** pour **ReadFileUploadNotification** et **SimulatedDevice**.</span><span class="sxs-lookup"><span data-stu-id="90818-160">Select **Multiple startup projects**, then select the **Start** action for **ReadFileUploadNotification** and **SimulatedDevice**.</span></span>

1. <span data-ttu-id="90818-161">Appuyez sur **F5**.</span><span class="sxs-lookup"><span data-stu-id="90818-161">Press **F5**.</span></span> <span data-ttu-id="90818-162">Les deux applications doivent démarrer.</span><span class="sxs-lookup"><span data-stu-id="90818-162">Both applications should start.</span></span> <span data-ttu-id="90818-163">Vous devriez voir le téléchargement terminé dans une application console et le message de notification de téléchargement reçus par l’autre application console.</span><span class="sxs-lookup"><span data-stu-id="90818-163">You should see the upload completed in one console app and the upload notification message received by the other console app.</span></span> <span data-ttu-id="90818-164">Vous pouvez utiliser le [portail Azure] ou l’Explorateur de serveurs Visual Studio pour vérifier la présence du fichier chargé dans votre compte Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="90818-164">You can use the [Azure portal] or Visual Studio Server Explorer to check for the presence of the uploaded file in your Azure Storage account.</span></span>

    ![][50]

## <a name="next-steps"></a><span data-ttu-id="90818-165">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="90818-165">Next steps</span></span>

<span data-ttu-id="90818-166">Dans ce didacticiel, vous avez appris à utiliser les fonctionnalités de téléchargement de fichier d’IoT Hub pour simplifier les chargements de fichiers à partir d’appareils.</span><span class="sxs-lookup"><span data-stu-id="90818-166">In this tutorial, you learned how to use the file upload capabilities of IoT Hub to simplify file uploads from devices.</span></span> <span data-ttu-id="90818-167">Vous pouvez continuer à explorer les scénarios et fonctionnalités d’IoT Hub avec les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="90818-167">You can continue to explore IoT hub features and scenarios with the following articles:</span></span>

* <span data-ttu-id="90818-168">[Créer un IoT Hub par programme][lnk-create-hub]</span><span class="sxs-lookup"><span data-stu-id="90818-168">[Create an IoT hub programmatically][lnk-create-hub]</span></span>
* <span data-ttu-id="90818-169">[Présentation du Kit de développement logiciel (SDK) C][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="90818-169">[Introduction to C SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="90818-170">[Kits de développement logiciel (SDK) Azure IoT][lnk-sdks]</span><span class="sxs-lookup"><span data-stu-id="90818-170">[Azure IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="90818-171">Pour explorer davantage les capacités de IoT Hub, consultez :</span><span class="sxs-lookup"><span data-stu-id="90818-171">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="90818-172">[Simulation d’un appareil avec IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="90818-172">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>

<!-- Images. -->

[50]: ./media/iot-hub-csharp-csharp-file-upload/run-apps1.png
[1]: ./media/iot-hub-csharp-csharp-file-upload/image-properties.png
[2]: ./media/iot-hub-csharp-csharp-file-upload/file-upload-project-csharp1.png

<!-- Links -->

<span data-ttu-id="90818-173">[portail Azure]: https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="90818-173">[Azure portal]: https://portal.azure.com/</span></span>

<span data-ttu-id="90818-174">[Centre de développement Azure IoT]: http://www.azure.com/develop/iot</span><span class="sxs-lookup"><span data-stu-id="90818-174">[Azure IoT Developer Center]: http://www.azure.com/develop/iot</span></span>

<span data-ttu-id="90818-175">[Transient Fault Handling]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx</span><span class="sxs-lookup"><span data-stu-id="90818-175">[Transient Fault Handling]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx</span></span>
<span data-ttu-id="90818-176">[Package NuGet du SDK service IoT Azure]: https://www.nuget.org/packages/Microsoft.Azure.Devices/</span><span class="sxs-lookup"><span data-stu-id="90818-176">[Azure IoT service SDK NuGet package]: https://www.nuget.org/packages/Microsoft.Azure.Devices/</span></span>
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[lnk-create-hub]: iot-hub-rm-template-powershell.md
[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-windows-iot-edge-simulated-device.md
