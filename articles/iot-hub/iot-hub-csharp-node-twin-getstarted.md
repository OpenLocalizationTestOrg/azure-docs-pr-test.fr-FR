---
title: "Prise en main des représentations physiques Azure IoT Hub (.NET/Node) | Microsoft Docs"
description: "Guide d’utilisation des représentations d’appareils Azure IoT Hub pour ajouter des balises, puis utiliser une requête IoT Hub. Vous utilisez Azure IoT device SDK pour Node.js afin d’implémenter l’application d’appareil simulé et Azure IoT service SDK pour .NET afin d’implémenter une application de service qui ajoute les balises et exécute la requête IoT Hub."
services: iot-hub
documentationcenter: node
author: fsautomata
manager: timlt
editor: 
ms.assetid: f7e23b6e-bfde-4fba-a6ec-dbb0f0e005f4
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/29/2017
ms.author: elioda
ms.openlocfilehash: 07797b9159c9b926e9eb47d8864c63048951931a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-device-twins-netnode"></a><span data-ttu-id="cfeae-104">Prise en main des représentations d’appareils (.NET/Node)</span><span class="sxs-lookup"><span data-stu-id="cfeae-104">Get started with device twins (.NET/Node)</span></span>
[!INCLUDE [iot-hub-selector-twin-get-started](../../includes/iot-hub-selector-twin-get-started.md)]

<span data-ttu-id="cfeae-105">À la fin de ce didacticiel, vous disposerez d’applications console Node.js et .NET :</span><span class="sxs-lookup"><span data-stu-id="cfeae-105">At the end of this tutorial, you will have a .NET and a Node.js console app:</span></span>

* <span data-ttu-id="cfeae-106">**AddTagsAndQuery.sln**, application .NET qui ajoute des balises et interroge des représentations d’appareil.</span><span class="sxs-lookup"><span data-stu-id="cfeae-106">**AddTagsAndQuery.sln**, a .NET back-end app, which adds tags and queries device twins.</span></span>
* <span data-ttu-id="cfeae-107">**TwinSimulatedDevice.js**, application Node.js qui simule un appareil se connectant à votre IoT Hub avec l’identité d’appareil créée précédemment, et signale son état de connectivité.</span><span class="sxs-lookup"><span data-stu-id="cfeae-107">**TwinSimulatedDevice.js**, a Node.js app which simulates a device that connects to your IoT hub with the device identity created earlier, and reports its connectivity condition.</span></span>

> [!NOTE]
> <span data-ttu-id="cfeae-108">L’article [Kits de développement logiciel (SDK) Azure IoT][lnk-hub-sdks] fournit des informations sur les Kits de développement logiciel (SDK) IoT que vous pouvez utiliser pour générer des applications pour appareil et des applications principales.</span><span class="sxs-lookup"><span data-stu-id="cfeae-108">The article [Azure IoT SDKs][lnk-hub-sdks] provides information about the Azure IoT SDKs that you can use to build both device and back-end apps.</span></span>
> 
> 

<span data-ttu-id="cfeae-109">Pour réaliser ce didacticiel, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="cfeae-109">To complete this tutorial you need the following:</span></span>

* <span data-ttu-id="cfeae-110">Visual Studio 2015 ou Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="cfeae-110">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="cfeae-111">Node.js version 0.10.x ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="cfeae-111">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="cfeae-112">Un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="cfeae-112">An active Azure account.</span></span> <span data-ttu-id="cfeae-113">(Si vous ne possédez pas de compte, vous pouvez créer un [compte gratuit][lnk-free-trial] en quelques minutes.)</span><span class="sxs-lookup"><span data-stu-id="cfeae-113">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-the-service-app"></a><span data-ttu-id="cfeae-114">Créer l’application de service</span><span class="sxs-lookup"><span data-stu-id="cfeae-114">Create the service app</span></span>
<span data-ttu-id="cfeae-115">Dans cette section, vous créez une application console (utilisant C#) qui ajoute des métadonnées d’emplacement au jumeau d’appareil associé à **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="cfeae-115">In this section, you create a .NET console app (using C#) that adds location metadata to the device twin associated with **myDeviceId**.</span></span> <span data-ttu-id="cfeae-116">L’application console interroge ensuite les jumeaux d’appareil stockés dans le hub IoT en sélectionnant les appareils situés aux États-Unis, puis ceux qui signalent une connexion mobile.</span><span class="sxs-lookup"><span data-stu-id="cfeae-116">It then queries the device twins stored in the IoT hub selecting the devices located in the US, and then the ones that reported a cellular connection.</span></span>

1. <span data-ttu-id="cfeae-117">Dans Visual Studio, ajoutez un projet Visual C# Bureau classique Windows à la solution actuelle en utilisant le modèle de projet **Application Console** .</span><span class="sxs-lookup"><span data-stu-id="cfeae-117">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution by using the **Console Application** project template.</span></span> <span data-ttu-id="cfeae-118">Nommez le projet **AddTagsAndQuery**.</span><span class="sxs-lookup"><span data-stu-id="cfeae-118">Name the project **AddTagsAndQuery**.</span></span>
   
    ![Nouveau projet Visual C# Bureau classique Windows][img-createapp]
1. <span data-ttu-id="cfeae-120">Dans l’Explorateur de solutions, cliquez avec le bouton droit sur le projet **AddTagsAndQuery**, puis cliquez sur **Gérer les packages NuGet...**.</span><span class="sxs-lookup"><span data-stu-id="cfeae-120">In Solution Explorer, right-click the **AddTagsAndQuery** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="cfeae-121">Dans la fenêtre **Gestionnaire de Package NuGet**, sélectionnez **Parcourir**, puis recherchez **microsoft.azure.devices**.</span><span class="sxs-lookup"><span data-stu-id="cfeae-121">In the **NuGet Package Manager** window, select **Browse** and search for **microsoft.azure.devices**.</span></span> <span data-ttu-id="cfeae-122">Sélectionnez **Installer** pour installer le package **Microsoft.Azure.Devices**, puis acceptez les conditions d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="cfeae-122">Select **Install** to install the **Microsoft.Azure.Devices** package, and accept the terms of use.</span></span> <span data-ttu-id="cfeae-123">Cette procédure lance le téléchargement et l’installation et ajoute une référence au [package Azure IoT Service SDK NuGet][lnk-nuget-service-sdk] et ses dépendances.</span><span class="sxs-lookup"><span data-stu-id="cfeae-123">This procedure downloads, installs, and adds a reference to the [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![Fenêtre du gestionnaire de package NuGet][img-servicenuget]
1. <span data-ttu-id="cfeae-125">Ajoutez les instructions `using` suivantes en haut du fichier **Program.cs** :</span><span class="sxs-lookup"><span data-stu-id="cfeae-125">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
1. <span data-ttu-id="cfeae-126">Ajoutez les champs suivants à la classe **Program** .</span><span class="sxs-lookup"><span data-stu-id="cfeae-126">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="cfeae-127">Remplacez la valeur d’espace réservé par la chaîne de connexion IoT Hub pour le hub créé dans la section précédente.</span><span class="sxs-lookup"><span data-stu-id="cfeae-127">Replace the placeholder value with the IoT Hub connection string for the hub that you created in the previous section.</span></span>
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
1. <span data-ttu-id="cfeae-128">Ajoutez la méthode suivante à la classe **Program** :</span><span class="sxs-lookup"><span data-stu-id="cfeae-128">Add the following method to the **Program** class:</span></span>
   
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
   
    <span data-ttu-id="cfeae-129">La classe **RegistryManager** expose toutes les méthodes requises pour interagir avec des jumeaux d’appareil à partir du service.</span><span class="sxs-lookup"><span data-stu-id="cfeae-129">The **RegistryManager** class exposes all the methods required to interact with device twins from the service.</span></span> <span data-ttu-id="cfeae-130">Le code précédent initialise l’objet **registryManager**, récupère le jumeau d’appareil de **myDeviceId**, puis met à jour ses balises avec les informations d’emplacement souhaitées.</span><span class="sxs-lookup"><span data-stu-id="cfeae-130">The previous code first initializes the **registryManager** object, then retrieves the device twin for **myDeviceId**, and finally updates its tags with the desired location information.</span></span>
   
    <span data-ttu-id="cfeae-131">Après la mise à jour, il exécute deux requêtes : la première sélectionne uniquement les jumeaux d’appareils situés dans l’usine **Redmond43** et la seconde affine la requête pour sélectionner uniquement les appareils qui sont également connectés via un réseau cellulaire.</span><span class="sxs-lookup"><span data-stu-id="cfeae-131">After updating, it executes two queries: the first selects only the device twins of devices located in the **Redmond43** plant, and the second refines the query to select only the devices that are also connected through cellular network.</span></span>
   
    <span data-ttu-id="cfeae-132">Notez que le code précédent, quand il crée l’objet **query**, spécifie un nombre maximal de documents retournés.</span><span class="sxs-lookup"><span data-stu-id="cfeae-132">Note that the previous code, when it creates the **query** object, specifies a maximum number of returned documents.</span></span> <span data-ttu-id="cfeae-133">L’objet **query** contient une propriété booléenne **HasMoreResults** permettant d’appeler les méthodes **GetNextAsTwinAsync** plusieurs fois afin de récupérer tous les résultats.</span><span class="sxs-lookup"><span data-stu-id="cfeae-133">The **query** object contains a **HasMoreResults** boolean property that you can use to invoke the **GetNextAsTwinAsync** methods multiple times to retrieve all results.</span></span> <span data-ttu-id="cfeae-134">Une méthode appelée **GetNextAsJson** est disponible pour les résultats qui ne sont pas des jumeaux d’appareil, par exemple, les résultats de requêtes d’agrégation.</span><span class="sxs-lookup"><span data-stu-id="cfeae-134">A method called **GetNextAsJson** is available for results that are not device twins, for example, results of aggregation queries.</span></span>
1. <span data-ttu-id="cfeae-135">Enfin, ajoutez les lignes suivantes à la méthode **Main** :</span><span class="sxs-lookup"><span data-stu-id="cfeae-135">Finally, add the following lines to the **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        AddTagsAndQuery().Wait();
        Console.WriteLine("Press Enter to exit.");
        Console.ReadLine();

1. <span data-ttu-id="cfeae-136">Dans l’Explorateur de solutions, sélectionnez **Définir les projets de démarrage...** et vérifiez que l’**Action** définie pour le projet **AddTagsAndQuery** est **Démarrer**.</span><span class="sxs-lookup"><span data-stu-id="cfeae-136">In the Solution Explorer, open the **Set StartUp projects...** and make sure the **Action** for **AddTagsAndQuery** project is **Start**.</span></span> <span data-ttu-id="cfeae-137">Générez la solution.</span><span class="sxs-lookup"><span data-stu-id="cfeae-137">Build the solution.</span></span>
1. <span data-ttu-id="cfeae-138">Exécutez cette application en cliquant avec le bouton droit sur le projet **AddTagsAndQuery** et en sélectionnant **Déboguer**, puis **Démarrer une nouvelle instance**.</span><span class="sxs-lookup"><span data-stu-id="cfeae-138">Run this application by right-clicking on the **AddTagsAndQuery** project and selecting **Debug**, followed by **Start new instance**.</span></span> <span data-ttu-id="cfeae-139">Vous devriez voir un appareil dans les résultats de la requête demandant tous les appareils situés à **Redmond43**, et aucun pour la requête limitant les résultats aux appareils utilisant un réseau cellulaire.</span><span class="sxs-lookup"><span data-stu-id="cfeae-139">You should see one device in the results for the query asking for all devices located in **Redmond43** and none for the query that restricts the results to devices that use a cellular network.</span></span>
   
    ![Résultats de requête dans la fenêtre][img-addtagapp]

<span data-ttu-id="cfeae-141">Dans la section suivante, vous allez créer une application d’appareil qui transmet les informations de connectivité et modifie le résultat de la requête de la section précédente.</span><span class="sxs-lookup"><span data-stu-id="cfeae-141">In the next section, you create a device app that reports the connectivity information and changes the result of the query in the previous section.</span></span>

## <a name="create-the-device-app"></a><span data-ttu-id="cfeae-142">Créer l’application d’appareil</span><span class="sxs-lookup"><span data-stu-id="cfeae-142">Create the device app</span></span>
<span data-ttu-id="cfeae-143">Dans cette section, vous créez une application console Node.js qui se connecte à votre hub en tant que **myDeviceId**, puis met à jour ses propriétés signalées afin qu’elles contiennent les informations indiquant qu’elle est connectée par le biais d’un réseau cellulaire.</span><span class="sxs-lookup"><span data-stu-id="cfeae-143">In this section, you create a Node.js console app that connects to your hub as **myDeviceId**, and then updates its reported properties to contain the information that it is connected using a cellular network.</span></span>

1. <span data-ttu-id="cfeae-144">Créez un dossier vide nommé **reportconnectivity**.</span><span class="sxs-lookup"><span data-stu-id="cfeae-144">Create a new empty folder called **reportconnectivity**.</span></span> <span data-ttu-id="cfeae-145">Dans le dossier **reportconnectivity**, créez un fichier package.json en utilisant la commande suivante à l’invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="cfeae-145">In the **reportconnectivity** folder, create a new package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="cfeae-146">Acceptez toutes les valeurs par défaut.</span><span class="sxs-lookup"><span data-stu-id="cfeae-146">Accept all the defaults.</span></span>
   
    ```
    npm init
    ```
1. <span data-ttu-id="cfeae-147">À l’invite de commandes, dans le dossier **reportconnectivity**, exécutez la commande suivante pour installer les packages **azure-iot-device** et **azure-iot-device-mqtt** :</span><span class="sxs-lookup"><span data-stu-id="cfeae-147">At your command prompt in the **reportconnectivity** folder, run the following command to install the **azure-iot-device**, and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
1. <span data-ttu-id="cfeae-148">À l’aide d’un éditeur de texte, créez un fichier **ReportConnectivity.js** dans le dossier **reportconnectivity**.</span><span class="sxs-lookup"><span data-stu-id="cfeae-148">Using a text editor, create a new **ReportConnectivity.js** file in the **reportconnectivity** folder.</span></span>
1. <span data-ttu-id="cfeae-149">Ajoutez le code suivant au fichier **ReportConnectivity.js**, puis remplacez l’espace réservé pour la chaîne de connexion d’appareil par la chaîne de connexion que vous avez copiée lors de la création de l’identité d’appareil **myDeviceId** :</span><span class="sxs-lookup"><span data-stu-id="cfeae-149">Add the following code to the **ReportConnectivity.js** file, and substitute the placeholder for device connection string with the one you copied when you created the **myDeviceId** device identity:</span></span>
   
        'use strict';
        var Client = require('azure-iot-device').Client;
        var Protocol = require('azure-iot-device-mqtt').Mqtt;
   
        var connectionString = '{device connection string}';
        var client = Client.fromConnectionString(connectionString, Protocol);
   
        client.open(function(err) {
        if (err) {
            console.error('could not open IotHub client');
        }  else {
            console.log('client opened');
   
            client.getTwin(function(err, twin) {
            if (err) {
                console.error('could not get twin');
            } else {
                var patch = {
                    connectivity: {
                        type: 'cellular'
                    }
                };
   
                twin.properties.reported.update(patch, function(err) {
                    if (err) {
                        console.error('could not update twin');
                    } else {
                        console.log('twin state reported');
                        process.exit();
                    }
                });
            }
            });
        }
        });
   
    <span data-ttu-id="cfeae-150">L’objet **Client** expose toutes les méthodes requises pour interagir avec des représentations d’appareil à partir de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="cfeae-150">The **Client** object exposes all the methods you require to interact with device twins from the device.</span></span> <span data-ttu-id="cfeae-151">Le code précédent, après avoir initialisé l’objet **Client**, récupère la représentation d’appareil de **myDeviceId**, puis met à jour sa propriété signalée avec les informations de connectivité.</span><span class="sxs-lookup"><span data-stu-id="cfeae-151">The previous code, after it initializes the **Client** object, retrieves the device twin for **myDeviceId** and updates its reported property with the connectivity information.</span></span>
1. <span data-ttu-id="cfeae-152">Exécuter l’application d’appareil</span><span class="sxs-lookup"><span data-stu-id="cfeae-152">Run the device app</span></span>
   
        node ReportConnectivity.js
   
    <span data-ttu-id="cfeae-153">Vous devriez voir le message `twin state reported`.</span><span class="sxs-lookup"><span data-stu-id="cfeae-153">You should see the message `twin state reported`.</span></span>
1. <span data-ttu-id="cfeae-154">À présent que l’appareil a signalé ses informations de connectivité, il doit apparaître dans les deux requêtes.</span><span class="sxs-lookup"><span data-stu-id="cfeae-154">Now that the device reported its connectivity information, it should appear in both queries.</span></span> <span data-ttu-id="cfeae-155">Exécutez l’application .NET **AddTagsAndQuery** pour exécuter des requêtes à nouveau.</span><span class="sxs-lookup"><span data-stu-id="cfeae-155">Run the .NET **AddTagsAndQuery** app to run the queries again.</span></span> <span data-ttu-id="cfeae-156">Cette fois, **myDeviceId** doit apparaître dans les résultats des deux requêtes.</span><span class="sxs-lookup"><span data-stu-id="cfeae-156">This time **myDeviceId** should appear in both query results.</span></span>
   
    ![][img-addtagapp2]

## <a name="next-steps"></a><span data-ttu-id="cfeae-157">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="cfeae-157">Next steps</span></span>
<span data-ttu-id="cfeae-158">Dans ce didacticiel, vous avez configuré un nouveau hub IoT dans le portail Azure, puis créé une identité d’appareil dans le registre des identités du hub IoT.</span><span class="sxs-lookup"><span data-stu-id="cfeae-158">In this tutorial, you configured a new IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span></span> <span data-ttu-id="cfeae-159">Vous avez ajouté des métadonnées d’appareil en tant que balises à partir d’une application principale et écrit une application pour appareil simulée pour signaler des informations de connectivité d’appareil dans le jumeau d’appareil.</span><span class="sxs-lookup"><span data-stu-id="cfeae-159">You added device metadata as tags from a back-end app, and wrote a simulated device app to report device connectivity information in the device twin.</span></span> <span data-ttu-id="cfeae-160">Vous avez également appris à interroger ces informations à l’aide du langage de requête IoT Hub de type SQL.</span><span class="sxs-lookup"><span data-stu-id="cfeae-160">You also learned how to query this information using the SQL-like IoT Hub query language.</span></span>

<span data-ttu-id="cfeae-161">Utilisez les ressources suivantes :</span><span class="sxs-lookup"><span data-stu-id="cfeae-161">Use the following resources to learn how to:</span></span>

* <span data-ttu-id="cfeae-162">Pour savoir comment envoyer les données de télémétrie à partir d’appareils, consultez le didacticiel [Prise en main d’IoT Hub][lnk-iothub-getstarted].</span><span class="sxs-lookup"><span data-stu-id="cfeae-162">send telemetry from devices with the [Get started with IoT Hub][lnk-iothub-getstarted] tutorial,</span></span>
* <span data-ttu-id="cfeae-163">Pour savoir comment configurer des appareils à l’aide des propriétés de jumeau d’appareil souhaitées, voir le didacticiel [Utiliser des propriétés souhaitées pour configurer des appareils][lnk-twin-how-to-configure].</span><span class="sxs-lookup"><span data-stu-id="cfeae-163">configure devices using device twin's desired properties with the [Use desired properties to configure devices][lnk-twin-how-to-configure] tutorial,</span></span>
* <span data-ttu-id="cfeae-164">Pour savoir comment contrôler des appareils de façon interactive (par exemple en mettant en marche un ventilateur à partir d’une application contrôlée par l’utilisateur), voir le didacticiel [Utiliser des méthodes directes][lnk-methods-tutorial].</span><span class="sxs-lookup"><span data-stu-id="cfeae-164">control devices interactively (such as turning on a fan from a user-controlled app) with the [Use direct methods][lnk-methods-tutorial] tutorial.</span></span>

<!-- images -->
[img-servicenuget]: media/iot-hub-csharp-node-twin-getstarted/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-node-twin-getstarted/createnetapp.png
[img-addtagapp]: media/iot-hub-csharp-node-twin-getstarted/addtagapp.png
[img-addtagapp2]: media/iot-hub-csharp-node-twin-getstarted/addtagapp2.png

<!-- links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/

[lnk-d2c]: iot-hub-devguide-messaging.md#device-to-cloud-messages
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-identity]: iot-hub-devguide-identity-registry.md

[lnk-iothub-getstarted]: iot-hub-node-node-getstarted.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md
[lnk-twin-how-to-configure]: iot-hub-csharp-node-twin-how-to-configure.md

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md

