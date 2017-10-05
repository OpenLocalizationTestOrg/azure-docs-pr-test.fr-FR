---
title: "Bien démarrer avec les jumeaux d’appareil Azure IoT Hub (.NET/.NET) | Microsoft Docs"
description: "Guide d’utilisation des jumeaux d’appareils Azure IoT Hub pour ajouter des balises, puis utiliser une requête IoT Hub. Vous utilisez le kit Azure IoT device SDK pour .NET pour implémenter l’application d’appareil simulé et le kit Azure IoT service SDK pour .NET pour implémenter une application de service qui ajoute des balises et exécute la requête IoT Hub."
services: iot-hub
documentationcenter: node
author: dsk-2015
manager: timlt
editor: 
ms.assetid: f7e23b6e-bfde-4fba-a6ec-dbb0f0e005f4
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: dkshir
ms.openlocfilehash: 6073d594117e69676b753a1e3af25fffa3583a2b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-device-twins-netnet"></a><span data-ttu-id="1b75a-104">Bien démarrer avec les jumeaux d’appareils (.NET/.NET)</span><span class="sxs-lookup"><span data-stu-id="1b75a-104">Get started with device twins (.NET/.NET)</span></span>
[!INCLUDE [iot-hub-selector-twin-get-started](../../includes/iot-hub-selector-twin-get-started.md)]

<span data-ttu-id="1b75a-105">À la fin de ce didacticiel, vous disposerez des deux applications console .NET suivantes :</span><span class="sxs-lookup"><span data-stu-id="1b75a-105">At the end of this tutorial, you will have these .NET console apps:</span></span>

* <span data-ttu-id="1b75a-106">**CreateDeviceIdentity**, application .NET qui crée une identité d’appareil et une clé de sécurité associée pour connecter votre application d’appareil simulé.</span><span class="sxs-lookup"><span data-stu-id="1b75a-106">**CreateDeviceIdentity**, a .NET app which creates a device identity and associated security key to connect your simulated device app.</span></span>
* <span data-ttu-id="1b75a-107">**AddTagsAndQuery**, application principale .NET qui ajoute des balises et interroge des jumeaux d’appareil.</span><span class="sxs-lookup"><span data-stu-id="1b75a-107">**AddTagsAndQuery**, a .NET back-end app which adds tags and queries device twins.</span></span>
* <span data-ttu-id="1b75a-108">**ReportConnectivity**, application pour appareil .NET qui simule un appareil se connectant à votre hub IoT avec l’identité d’appareil créée précédemment, et signale son état de connectivité.</span><span class="sxs-lookup"><span data-stu-id="1b75a-108">**ReportConnectivity**, a .NET device app which simulates a device that connects to your IoT hub with the device identity created earlier, and reports its connectivity condition.</span></span>

> [!NOTE]
> <span data-ttu-id="1b75a-109">L’article [Kits Azure IoT SDK][lnk-hub-sdks] fournit des informations sur les kits Azure IoT SDK que vous pouvez utiliser pour générer des applications pour appareil et des applications principales.</span><span class="sxs-lookup"><span data-stu-id="1b75a-109">The article [Azure IoT SDKs][lnk-hub-sdks] provides information about the Azure IoT SDKs that you can use to build both device and back-end apps.</span></span>
> 
> 

<span data-ttu-id="1b75a-110">Pour réaliser ce didacticiel, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="1b75a-110">To complete this tutorial you need the following:</span></span>

* <span data-ttu-id="1b75a-111">Visual Studio 2015 ou Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="1b75a-111">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="1b75a-112">Un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="1b75a-112">An active Azure account.</span></span> <span data-ttu-id="1b75a-113">(Si vous ne possédez pas de compte, vous pouvez créer un [compte gratuit][lnk-free-trial] en quelques minutes.)</span><span class="sxs-lookup"><span data-stu-id="1b75a-113">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

<span data-ttu-id="1b75a-114">Si vous voulez plutôt créer l’identité de l’appareil par programmation, lisez la section correspondante dans l’article [Connexion de l’appareil simulé à votre hub IoT à l’aide de .NET] [lnk-device-identity-csharp].</span><span class="sxs-lookup"><span data-stu-id="1b75a-114">If you want to create the device identity programmatically instead, read the corresponding section in the [Connect your simulated device to your IoT hub using .NET][lnk-device-identity-csharp] article.</span></span>

## <a name="create-the-service-app"></a><span data-ttu-id="1b75a-115">Créer l’application de service</span><span class="sxs-lookup"><span data-stu-id="1b75a-115">Create the service app</span></span>
<span data-ttu-id="1b75a-116">Dans cette section, vous créez une application console (utilisant C#) qui ajoute des métadonnées d’emplacement au jumeau d’appareil associé à **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="1b75a-116">In this section, you create a .NET console app (using C#) that adds location metadata to the device twin associated with **myDeviceId**.</span></span> <span data-ttu-id="1b75a-117">L’application console interroge ensuite les jumeaux d’appareil stockés dans le hub IoT en sélectionnant les appareils situés aux États-Unis, puis ceux qui signalent une connexion mobile.</span><span class="sxs-lookup"><span data-stu-id="1b75a-117">It then queries the device twins stored in the IoT hub selecting the devices located in the US, and then the ones that reported a cellular connection.</span></span>

1. <span data-ttu-id="1b75a-118">Dans Visual Studio, ajoutez un projet Visual C# Bureau classique Windows à la solution actuelle en utilisant le modèle de projet **Application Console** .</span><span class="sxs-lookup"><span data-stu-id="1b75a-118">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution by using the **Console Application** project template.</span></span> <span data-ttu-id="1b75a-119">Nommez le projet **AddTagsAndQuery**.</span><span class="sxs-lookup"><span data-stu-id="1b75a-119">Name the project **AddTagsAndQuery**.</span></span>
   
    ![Nouveau projet Visual C# Bureau classique Windows][img-createapp]
1. <span data-ttu-id="1b75a-121">Dans l’Explorateur de solutions, cliquez avec le bouton droit sur le projet **AddTagsAndQuery**, puis cliquez sur **Gérer les packages NuGet...**.</span><span class="sxs-lookup"><span data-stu-id="1b75a-121">In Solution Explorer, right-click the **AddTagsAndQuery** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="1b75a-122">Dans la fenêtre **Gestionnaire de Package NuGet**, sélectionnez **Parcourir**, puis recherchez **microsoft.azure.devices**.</span><span class="sxs-lookup"><span data-stu-id="1b75a-122">In the **NuGet Package Manager** window, select **Browse** and search for **microsoft.azure.devices**.</span></span> <span data-ttu-id="1b75a-123">Sélectionnez **Installer** pour installer le package **Microsoft.Azure.Devices**, puis acceptez les conditions d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="1b75a-123">Select **Install** to install the **Microsoft.Azure.Devices** package, and accept the terms of use.</span></span> <span data-ttu-id="1b75a-124">Cette procédure lance le téléchargement et l’installation et ajoute une référence au [package Azure IoT Service SDK NuGet][lnk-nuget-service-sdk] et ses dépendances.</span><span class="sxs-lookup"><span data-stu-id="1b75a-124">This procedure downloads, installs, and adds a reference to the [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![Fenêtre du gestionnaire de package NuGet][img-servicenuget]
1. <span data-ttu-id="1b75a-126">Ajoutez les instructions `using` suivantes en haut du fichier **Program.cs** :</span><span class="sxs-lookup"><span data-stu-id="1b75a-126">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
1. <span data-ttu-id="1b75a-127">Ajoutez les champs suivants à la classe **Program** .</span><span class="sxs-lookup"><span data-stu-id="1b75a-127">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="1b75a-128">Remplacez la valeur d’espace réservé par la chaîne de connexion IoT Hub pour le hub créé dans la section précédente.</span><span class="sxs-lookup"><span data-stu-id="1b75a-128">Replace the placeholder value with the IoT Hub connection string for the hub that you created in the previous section.</span></span>
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
1. <span data-ttu-id="1b75a-129">Ajoutez la méthode suivante à la classe **Program** :</span><span class="sxs-lookup"><span data-stu-id="1b75a-129">Add the following method to the **Program** class:</span></span>
   
        public static async Task AddTagsAndQuery()
        {
            var twin = await registryManager.GetTwinAsync("myDeviceId");
            var patch =
                @"{
                    tags: {
                        location: {
                            region: 'US',
                            plant: 'Redmond43'
                        }
                    }
                }";
            await registryManager.UpdateTwinAsync(twin.DeviceId, patch, twin.ETag);
   
            var query = registryManager.CreateQuery("SELECT * FROM devices WHERE tags.location.plant = 'Redmond43'", 100);
            var twinsInRedmond43 = await query.GetNextAsTwinAsync();
            Console.WriteLine("Devices in Redmond43: {0}", string.Join(", ", twinsInRedmond43.Select(t => t.DeviceId)));
   
            query = registryManager.CreateQuery("SELECT * FROM devices WHERE tags.location.plant = 'Redmond43' AND properties.reported.connectivity.type = 'cellular'", 100);
            var twinsInRedmond43UsingCellular = await query.GetNextAsTwinAsync();
            Console.WriteLine("Devices in Redmond43 using cellular network: {0}", string.Join(", ", twinsInRedmond43UsingCellular.Select(t => t.DeviceId)));
        }
   
    <span data-ttu-id="1b75a-130">La classe **RegistryManager** expose toutes les méthodes requises pour interagir avec des jumeaux d’appareil à partir du service.</span><span class="sxs-lookup"><span data-stu-id="1b75a-130">The **RegistryManager** class exposes all the methods required to interact with device twins from the service.</span></span> <span data-ttu-id="1b75a-131">Le code précédent initialise l’objet **registryManager**, récupère le jumeau d’appareil de **myDeviceId**, puis met à jour ses balises avec les informations d’emplacement souhaitées.</span><span class="sxs-lookup"><span data-stu-id="1b75a-131">The previous code first initializes the **registryManager** object, then retrieves the device twin for **myDeviceId**, and finally updates its tags with the desired location information.</span></span>
   
    <span data-ttu-id="1b75a-132">Après la mise à jour, il exécute deux requêtes : la première sélectionne uniquement les jumeaux d’appareils situés dans l’usine **Redmond43** et la seconde affine la requête pour sélectionner uniquement les appareils qui sont également connectés via un réseau cellulaire.</span><span class="sxs-lookup"><span data-stu-id="1b75a-132">After updating, it executes two queries: the first selects only the device twins of devices located in the **Redmond43** plant, and the second refines the query to select only the devices that are also connected through cellular network.</span></span>
   
    <span data-ttu-id="1b75a-133">Notez que le code précédent, quand il crée l’objet **query**, spécifie un nombre maximal de documents retournés.</span><span class="sxs-lookup"><span data-stu-id="1b75a-133">Note that the previous code, when it creates the **query** object, specifies a maximum number of returned documents.</span></span> <span data-ttu-id="1b75a-134">L’objet **query** contient une propriété booléenne **HasMoreResults** permettant d’appeler les méthodes **GetNextAsTwinAsync** plusieurs fois afin de récupérer tous les résultats.</span><span class="sxs-lookup"><span data-stu-id="1b75a-134">The **query** object contains a **HasMoreResults** boolean property that you can use to invoke the **GetNextAsTwinAsync** methods multiple times to retrieve all results.</span></span> <span data-ttu-id="1b75a-135">Une méthode appelée **GetNextAsJson** est disponible pour les résultats qui ne sont pas des jumeaux d’appareil, par exemple, les résultats de requêtes d’agrégation.</span><span class="sxs-lookup"><span data-stu-id="1b75a-135">A method called **GetNextAsJson** is available for results that are not device twins, for example, results of aggregation queries.</span></span>
1. <span data-ttu-id="1b75a-136">Enfin, ajoutez les lignes suivantes à la méthode **Main** :</span><span class="sxs-lookup"><span data-stu-id="1b75a-136">Finally, add the following lines to the **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        AddTagsAndQuery().Wait();
        Console.WriteLine("Press Enter to exit.");
        Console.ReadLine();

1. <span data-ttu-id="1b75a-137">Dans l’Explorateur de solutions, sélectionnez **Définir les projets de démarrage...** et vérifiez que l’**Action** définie pour le projet **AddTagsAndQuery** est **Démarrer**.</span><span class="sxs-lookup"><span data-stu-id="1b75a-137">In the Solution Explorer, open the **Set StartUp projects...** and make sure the **Action** for **AddTagsAndQuery** project is **Start**.</span></span> <span data-ttu-id="1b75a-138">Générez la solution.</span><span class="sxs-lookup"><span data-stu-id="1b75a-138">Build the solution.</span></span>
1. <span data-ttu-id="1b75a-139">Exécutez cette application en cliquant avec le bouton droit sur le projet **AddTagsAndQuery** et en sélectionnant **Déboguer**, puis **Démarrer une nouvelle instance**.</span><span class="sxs-lookup"><span data-stu-id="1b75a-139">Run this application by right-clicking on the **AddTagsAndQuery** project and selecting **Debug**, followed by **Start new instance**.</span></span> <span data-ttu-id="1b75a-140">Vous devriez voir un appareil dans les résultats de la requête demandant tous les appareils situés à **Redmond43**, et aucun pour la requête limitant les résultats aux appareils utilisant un réseau cellulaire.</span><span class="sxs-lookup"><span data-stu-id="1b75a-140">You should see one device in the results for the query asking for all devices located in **Redmond43** and none for the query that restricts the results to devices that use a cellular network.</span></span>
   
    ![Résultats de requête dans la fenêtre][img-addtagapp]

<span data-ttu-id="1b75a-142">Dans la section suivante, vous allez créer une application d’appareil qui transmet les informations de connectivité et modifie le résultat de la requête de la section précédente.</span><span class="sxs-lookup"><span data-stu-id="1b75a-142">In the next section, you create a device app that reports the connectivity information and changes the result of the query in the previous section.</span></span>

## <a name="create-the-device-app"></a><span data-ttu-id="1b75a-143">Créer l’application pour appareil</span><span class="sxs-lookup"><span data-stu-id="1b75a-143">Create the device app</span></span>
<span data-ttu-id="1b75a-144">Dans cette section, vous allez créer une application console .NET qui se connecte à votre hub en tant que **myDeviceId**, puis met à jour ses propriétés signalées afin qu’elles contiennent les informations indiquant qu’elle est connectée par le biais d’un réseau mobile.</span><span class="sxs-lookup"><span data-stu-id="1b75a-144">In this section, you create a .NET console app that connects to your hub as **myDeviceId**, and then updates its reported properties to contain the information that it is connected using a cellular network.</span></span>

1. <span data-ttu-id="1b75a-145">Dans Visual Studio, ajoutez un projet Visual C# Bureau classique Windows à la solution actuelle en utilisant le modèle de projet **Application Console** .</span><span class="sxs-lookup"><span data-stu-id="1b75a-145">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution by using the **Console Application** project template.</span></span> <span data-ttu-id="1b75a-146">Nommez le projet **ReportConnectivity**.</span><span class="sxs-lookup"><span data-stu-id="1b75a-146">Name the project **ReportConnectivity**.</span></span>
   
    ![Nouvelle application pour appareil Windows classique Visual C#][img-createdeviceapp]
    
1. <span data-ttu-id="1b75a-148">Dans l’Explorateur de solutions, cliquez avec le bouton droit sur le projet **ReportConnectivity**, puis cliquez sur **Gérer les packages NuGet...**</span><span class="sxs-lookup"><span data-stu-id="1b75a-148">In Solution Explorer, right-click the **ReportConnectivity** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="1b75a-149">Dans la fenêtre **Gestionnaire de package NuGet**, sélectionnez **Parcourir**, puis recherchez **microsoft.azure.devices.client**.</span><span class="sxs-lookup"><span data-stu-id="1b75a-149">In the **NuGet Package Manager** window, select **Browse** and search for **microsoft.azure.devices.client**.</span></span> <span data-ttu-id="1b75a-150">Sélectionnez **Installer** pour installer le package **Microsoft.Azure.Devices.Client**, puis acceptez les conditions d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="1b75a-150">Select **Install** to install the **Microsoft.Azure.Devices.Client** package, and accept the terms of use.</span></span> <span data-ttu-id="1b75a-151">Cette procédure télécharge, installe et ajoute une référence au package NuGet [ Azure IoT device SDK][lnk-nuget-client-sdk] et à ses dépendances.</span><span class="sxs-lookup"><span data-stu-id="1b75a-151">This procedure downloads, installs, and adds a reference to the [Azure IoT device SDK][lnk-nuget-client-sdk] NuGet package and its dependencies.</span></span>
   
    ![Application cliente dans la fenêtre du gestionnaire de package NuGet][img-clientnuget]
1. <span data-ttu-id="1b75a-153">Ajoutez les instructions `using` suivantes en haut du fichier **Program.cs** :</span><span class="sxs-lookup"><span data-stu-id="1b75a-153">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices.Client;
        using Microsoft.Azure.Devices.Shared;
        using Newtonsoft.Json;

1. <span data-ttu-id="1b75a-154">Ajoutez les champs suivants à la classe **Program** .</span><span class="sxs-lookup"><span data-stu-id="1b75a-154">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="1b75a-155">Remplacez la valeur d’espace réservé par la chaîne de connexion de l’appareil notée dans la section précédente.</span><span class="sxs-lookup"><span data-stu-id="1b75a-155">Replace the placeholder value with the device connection string that you noted in the previous section.</span></span>
   
        static string DeviceConnectionString = "HostName=<yourIotHubName>.azure-devices.net;DeviceId=<yourIotDeviceName>;SharedAccessKey=<yourIotDeviceAccessKey>";
        static DeviceClient Client = null;

1. <span data-ttu-id="1b75a-156">Ajoutez la méthode suivante à la classe **Program** :</span><span class="sxs-lookup"><span data-stu-id="1b75a-156">Add the following method to the **Program** class:</span></span>

       public static async void InitClient()
        {
            try
            {
                Console.WriteLine("Connecting to hub");
                Client = DeviceClient.CreateFromConnectionString(DeviceConnectionString, TransportType.Mqtt);
                Console.WriteLine("Retrieving twin");
                await Client.GetTwinAsync();
            }
            catch (Exception ex)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", ex.Message);
            }
        }

    <span data-ttu-id="1b75a-157">L’objet **Client** expose toutes les méthodes requises pour interagir avec des jumeaux d’appareil à partir de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="1b75a-157">The **Client** object exposes all the methods you require to interact with device twins from the device.</span></span> <span data-ttu-id="1b75a-158">Le code présenté ci-dessus initialise l’objet **Client**, puis récupère le jumeau d’appareil pour **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="1b75a-158">The code shown above, initializes the **Client** object, and then retrieves the device twin for **myDeviceId**.</span></span>

1. <span data-ttu-id="1b75a-159">Ajoutez la méthode suivante à la classe **Program** :</span><span class="sxs-lookup"><span data-stu-id="1b75a-159">Add the following method to the **Program** class:</span></span>
   
        public static async void ReportConnectivity()
        {
            try
            {
                Console.WriteLine("Sending connectivity data as reported property");
                
                TwinCollection reportedProperties, connectivity;
                reportedProperties = new TwinCollection();
                connectivity = new TwinCollection();
                connectivity["type"] = "cellular";
                reportedProperties["connectivity"] = connectivity;
                await Client.UpdateReportedPropertiesAsync(reportedProperties);
            }
            catch (Exception ex)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", ex.Message);
            }
        }

   <span data-ttu-id="1b75a-160">Le code ci-dessus met à jour la propriété signalée de **myDeviceId** avec les informations de connectivité.</span><span class="sxs-lookup"><span data-stu-id="1b75a-160">The code above updates **myDeviceId**'s reported property with the connectivity information.</span></span>

1. <span data-ttu-id="1b75a-161">Enfin, ajoutez les lignes suivantes à la méthode **Main** :</span><span class="sxs-lookup"><span data-stu-id="1b75a-161">Finally, add the following lines to the **Main** method:</span></span>
   
       try
       {
            InitClient();
            ReportConnectivity();
       }
       catch (Exception ex)
       {
            Console.WriteLine();
            Console.WriteLine("Error in sample: {0}", ex.Message);
       }
       Console.WriteLine("Press Enter to exit.");
       Console.ReadLine();

1. <span data-ttu-id="1b75a-162">Dans l’Explorateur de solutions, ouvrez **Définir les projets de démarrage...** et vérifiez que la valeur **Action** définie pour le projet **ReportConnectivity** est **Démarrer**.</span><span class="sxs-lookup"><span data-stu-id="1b75a-162">In the Solution Explorer, open the **Set StartUp projects...** and make sure the **Action** for **ReportConnectivity** project is **Start**.</span></span> <span data-ttu-id="1b75a-163">Générez la solution.</span><span class="sxs-lookup"><span data-stu-id="1b75a-163">Build the solution.</span></span>
1. <span data-ttu-id="1b75a-164">Exécutez cette application en cliquant avec le bouton droit sur le projet **ReportConnectivity** et en sélectionnant **Déboguer**, puis **Démarrer une nouvelle instance**.</span><span class="sxs-lookup"><span data-stu-id="1b75a-164">Run this application by right-clicking on the **ReportConnectivity** project and selecting **Debug**, followed by **Start new instance**.</span></span> <span data-ttu-id="1b75a-165">Vous devez la voir obtenir les informations relatives au jumeau et envoyer la connectivité sous la forme d’une *propriété signalée*.</span><span class="sxs-lookup"><span data-stu-id="1b75a-165">You should see it getting the twin information, and then sending connectivity as a *reported property*.</span></span>
   
    ![Exécuter l’application pour appareil pour signaler la connectivité][img-rundeviceapp]
    
    
1. <span data-ttu-id="1b75a-167">À présent que l’appareil a signalé ses informations de connectivité, il doit apparaître dans les deux requêtes.</span><span class="sxs-lookup"><span data-stu-id="1b75a-167">Now that the device reported its connectivity information, it should appear in both queries.</span></span> <span data-ttu-id="1b75a-168">Exécutez l’application .NET **AddTagsAndQuery** pour exécuter des requêtes à nouveau.</span><span class="sxs-lookup"><span data-stu-id="1b75a-168">Run the .NET **AddTagsAndQuery** app to run the queries again.</span></span> <span data-ttu-id="1b75a-169">Cette fois, **myDeviceId** doit apparaître dans les résultats des deux requêtes.</span><span class="sxs-lookup"><span data-stu-id="1b75a-169">This time **myDeviceId** should appear in both query results.</span></span>
   
    ![Connectivité des appareils signalée avec succès][img-tagappsuccess]

## <a name="next-steps"></a><span data-ttu-id="1b75a-171">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1b75a-171">Next steps</span></span>
<span data-ttu-id="1b75a-172">Dans ce didacticiel, vous avez configuré un nouveau hub IoT dans le portail Azure, puis créé une identité d’appareil dans le registre des identités du hub IoT.</span><span class="sxs-lookup"><span data-stu-id="1b75a-172">In this tutorial, you configured a new IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span></span> <span data-ttu-id="1b75a-173">Vous avez ajouté des métadonnées d’appareil en tant que balises à partir d’une application principale et écrit une application pour appareil simulée pour signaler des informations de connectivité d’appareil dans le jumeau d’appareil.</span><span class="sxs-lookup"><span data-stu-id="1b75a-173">You added device metadata as tags from a back-end app, and wrote a simulated device app to report device connectivity information in the device twin.</span></span> <span data-ttu-id="1b75a-174">Vous avez également appris à interroger ces informations à l’aide du langage de requête IoT Hub de type SQL.</span><span class="sxs-lookup"><span data-stu-id="1b75a-174">You also learned how to query this information using the SQL-like IoT Hub query language.</span></span>

<span data-ttu-id="1b75a-175">Utilisez les ressources suivantes :</span><span class="sxs-lookup"><span data-stu-id="1b75a-175">Use the following resources to learn how to:</span></span>

* <span data-ttu-id="1b75a-176">Pour savoir comment envoyer les données de télémétrie à partir d’appareils, consultez le didacticiel [Prise en main d’IoT Hub][lnk-iothub-getstarted].</span><span class="sxs-lookup"><span data-stu-id="1b75a-176">send telemetry from devices with the [Get started with IoT Hub][lnk-iothub-getstarted] tutorial,</span></span>
* <span data-ttu-id="1b75a-177">Pour savoir comment configurer des appareils à l’aide des propriétés de jumeau d’appareil souhaitées, voir le didacticiel [Utiliser des propriétés souhaitées pour configurer des appareils][lnk-twin-how-to-configure].</span><span class="sxs-lookup"><span data-stu-id="1b75a-177">configure devices using device twin's desired properties with the [Use desired properties to configure devices][lnk-twin-how-to-configure] tutorial,</span></span>
* <span data-ttu-id="1b75a-178">Pour savoir comment contrôler des appareils de façon interactive (par exemple en mettant en marche un ventilateur à partir d’une application contrôlée par l’utilisateur), voir le didacticiel [Utiliser des méthodes directes][lnk-methods-tutorial].</span><span class="sxs-lookup"><span data-stu-id="1b75a-178">control devices interactively (such as turning on a fan from a user-controlled app) with the [Use direct methods][lnk-methods-tutorial] tutorial.</span></span>

<!-- images -->
[img-servicenuget]: media/iot-hub-csharp-csharp-twin-getstarted/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-csharp-twin-getstarted/createnetapp.png
[img-addtagapp]: media/iot-hub-csharp-csharp-twin-getstarted/addtagapp.png
[img-createdeviceapp]: media/iot-hub-csharp-csharp-twin-getstarted/createdeviceapp.png
[img-clientnuget]: media/iot-hub-csharp-csharp-twin-getstarted/clientsdknuget.png
[img-rundeviceapp]: media/iot-hub-csharp-csharp-twin-getstarted/rundeviceapp.png
[img-tagappsuccess]: media/iot-hub-csharp-csharp-twin-getstarted/tagappsuccess.png

<!-- links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
[lnk-nuget-client-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices.Client/

[lnk-device-identity-csharp]: iot-hub-csharp-csharp-getstarted.md#DeviceIdentity_csharp
[lnk-d2c]: iot-hub-devguide-messaging.md#device-to-cloud-messages
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-identity]: iot-hub-devguide-identity-registry.md

[lnk-iothub-getstarted]: iot-hub-csharp-csharp-getstarted.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md
[lnk-twin-how-to-configure]: iot-hub-csharp-node-twin-how-to-configure.md

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md

