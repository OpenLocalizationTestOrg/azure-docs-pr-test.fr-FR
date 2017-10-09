---
title: "aaaGet main jumeaux d’appareil Azure IoT Hub (nœud/.NET) | Documents Microsoft"
description: "Comment toouse Azure IoT Hub appareil jumeaux tooadd balises, puis utilisez une requête IoT Hub. Vous utilisez du SDK de périphérique Azure IoT hello pour l’application d’appareil simulé Node.js tooimplement hello et hello Azure IoT service SDK pour .NET tooimplement une application de service qui ajoute des balises de hello et s’exécute hello requête de IoT Hub."
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
ms.openlocfilehash: 1cec082ebddc19c9b87998a5fd0159d32b07acd8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-device-twins-netnode"></a><span data-ttu-id="79a5e-104">Prise en main des représentations d’appareils (.NET/Node)</span><span class="sxs-lookup"><span data-stu-id="79a5e-104">Get started with device twins (.NET/Node)</span></span>
[!INCLUDE [iot-hub-selector-twin-get-started](../../includes/iot-hub-selector-twin-get-started.md)]

<span data-ttu-id="79a5e-105">À la fin hello de ce didacticiel, vous disposez .NET et une application de console Node.js :</span><span class="sxs-lookup"><span data-stu-id="79a5e-105">At hello end of this tutorial, you will have a .NET and a Node.js console app:</span></span>

* <span data-ttu-id="79a5e-106">**AddTagsAndQuery.sln**, application .NET qui ajoute des balises et interroge des représentations d’appareil.</span><span class="sxs-lookup"><span data-stu-id="79a5e-106">**AddTagsAndQuery.sln**, a .NET back-end app, which adds tags and queries device twins.</span></span>
* <span data-ttu-id="79a5e-107">**TwinSimulatedDevice.js**, une application Node.js qui simule un appareil qui se connecte tooyour IoT hub avec l’identité de l’appareil hello créée précédemment et signale l’état de connectivité.</span><span class="sxs-lookup"><span data-stu-id="79a5e-107">**TwinSimulatedDevice.js**, a Node.js app which simulates a device that connects tooyour IoT hub with hello device identity created earlier, and reports its connectivity condition.</span></span>

> [!NOTE]
> <span data-ttu-id="79a5e-108">article de Hello [kits de développement logiciel Azure IoT] [ lnk-hub-sdks] fournit des informations sur hello kits de développement logiciel Azure IoT que vous pouvez utiliser toobuild applications de périphérique et back-end.</span><span class="sxs-lookup"><span data-stu-id="79a5e-108">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both device and back-end apps.</span></span>
> 
> 

<span data-ttu-id="79a5e-109">toocomplete ce didacticiel, vous devez suivant de hello :</span><span class="sxs-lookup"><span data-stu-id="79a5e-109">toocomplete this tutorial you need hello following:</span></span>

* <span data-ttu-id="79a5e-110">Visual Studio 2015 ou Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="79a5e-110">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="79a5e-111">Node.js version 0.10.x ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="79a5e-111">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="79a5e-112">Un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="79a5e-112">An active Azure account.</span></span> <span data-ttu-id="79a5e-113">(Si vous ne possédez pas de compte, vous pouvez créer un [compte gratuit][lnk-free-trial] en quelques minutes.)</span><span class="sxs-lookup"><span data-stu-id="79a5e-113">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-hello-service-app"></a><span data-ttu-id="79a5e-114">Créer l’application de service hello</span><span class="sxs-lookup"><span data-stu-id="79a5e-114">Create hello service app</span></span>
<span data-ttu-id="79a5e-115">Dans cette section, vous créez .NET application console (à l’aide de c#) ajoute double d’appareil emplacement métadonnées toohello associé **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="79a5e-115">In this section, you create a .NET console app (using C#) that adds location metadata toohello device twin associated with **myDeviceId**.</span></span> <span data-ttu-id="79a5e-116">Il interroge ensuite jumeaux de périphérique hello stockées dans hello IoT hub en sélectionnant les appareils hello situés dans hello nous et puis hello ceux qui a signalé une connexion cellulaire.</span><span class="sxs-lookup"><span data-stu-id="79a5e-116">It then queries hello device twins stored in hello IoT hub selecting hello devices located in hello US, and then hello ones that reported a cellular connection.</span></span>

1. <span data-ttu-id="79a5e-117">Dans Visual Studio, ajoutez une solution d’actuel toohello de projet Visual c# bureau classique de Windows à l’aide de hello **Application Console** modèle de projet.</span><span class="sxs-lookup"><span data-stu-id="79a5e-117">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution by using hello **Console Application** project template.</span></span> <span data-ttu-id="79a5e-118">Projet de hello nom **AddTagsAndQuery**.</span><span class="sxs-lookup"><span data-stu-id="79a5e-118">Name hello project **AddTagsAndQuery**.</span></span>
   
    ![Nouveau projet Visual C# Bureau classique Windows][img-createapp]
1. <span data-ttu-id="79a5e-120">Dans l’Explorateur de solutions, cliquez sur hello **AddTagsAndQuery** de projet, puis cliquez sur **gérer les Packages NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="79a5e-120">In Solution Explorer, right-click hello **AddTagsAndQuery** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="79a5e-121">Bonjour **Gestionnaire de Package NuGet** fenêtre, sélectionnez **Parcourir** et recherchez **microsoft.azure.devices**.</span><span class="sxs-lookup"><span data-stu-id="79a5e-121">In hello **NuGet Package Manager** window, select **Browse** and search for **microsoft.azure.devices**.</span></span> <span data-ttu-id="79a5e-122">Sélectionnez **installer** tooinstall hello **Microsoft.Azure.Devices** empaqueter et accepter les conditions d’utilisation de hello.</span><span class="sxs-lookup"><span data-stu-id="79a5e-122">Select **Install** tooinstall hello **Microsoft.Azure.Devices** package, and accept hello terms of use.</span></span> <span data-ttu-id="79a5e-123">Cette procédure télécharge, installe et ajoute une référence toohello [Azure IoT service SDK] [ lnk-nuget-service-sdk] NuGet package et ses dépendances.</span><span class="sxs-lookup"><span data-stu-id="79a5e-123">This procedure downloads, installs, and adds a reference toohello [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![Fenêtre du gestionnaire de package NuGet][img-servicenuget]
1. <span data-ttu-id="79a5e-125">Ajoutez hello suivant `using` instructions haut hello hello **Program.cs** fichier :</span><span class="sxs-lookup"><span data-stu-id="79a5e-125">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
1. <span data-ttu-id="79a5e-126">Ajouter hello suivant champs toohello **programme** classe.</span><span class="sxs-lookup"><span data-stu-id="79a5e-126">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="79a5e-127">Remplacer la valeur d’espace réservé hello avec hello chaîne de connexion de IoT Hub hub hello que vous avez créé dans la section précédente de hello de.</span><span class="sxs-lookup"><span data-stu-id="79a5e-127">Replace hello placeholder value with hello IoT Hub connection string for hello hub that you created in hello previous section.</span></span>
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
1. <span data-ttu-id="79a5e-128">Ajouter hello suivant de méthode toohello **programme** classe :</span><span class="sxs-lookup"><span data-stu-id="79a5e-128">Add hello following method toohello **Program** class:</span></span>
   
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
   
    <span data-ttu-id="79a5e-129">Hello **RegistryManager** classe expose tous les hello méthodes requis toointeract avec jumeaux de périphérique à partir du service de hello.</span><span class="sxs-lookup"><span data-stu-id="79a5e-129">hello **RegistryManager** class exposes all hello methods required toointeract with device twins from hello service.</span></span> <span data-ttu-id="79a5e-130">code précédent de Hello initialise tout d’abord hello **registryManager** de l’objet, puis récupère hello double de périphérique pour **myDeviceId**et enfin met à jour ses balises avec les informations d’emplacement hello souhaité.</span><span class="sxs-lookup"><span data-stu-id="79a5e-130">hello previous code first initializes hello **registryManager** object, then retrieves hello device twin for **myDeviceId**, and finally updates its tags with hello desired location information.</span></span>
   
    <span data-ttu-id="79a5e-131">Après la mise à jour, il exécute deux requêtes : hello sélectionne tout d’abord uniquement les jumeaux appareil hello des périphériques situés dans hello **Redmond43** usine et hello deuxième affine hello requête tooselect uniquement hello pour les appareils qui sont également connectés via réseau cellulaire.</span><span class="sxs-lookup"><span data-stu-id="79a5e-131">After updating, it executes two queries: hello first selects only hello device twins of devices located in hello **Redmond43** plant, and hello second refines hello query tooselect only hello devices that are also connected through cellular network.</span></span>
   
    <span data-ttu-id="79a5e-132">Notez que hello le code précédent, lorsqu’il crée hello **requête** d’objet, spécifie un nombre maximal de documents renvoyés.</span><span class="sxs-lookup"><span data-stu-id="79a5e-132">Note that hello previous code, when it creates hello **query** object, specifies a maximum number of returned documents.</span></span> <span data-ttu-id="79a5e-133">Hello **requête** objet contient un **HasMoreResults** propriété booléenne que vous pouvez utiliser tooinvoke hello **GetNextAsTwinAsync** méthodes tooretrieve plusieurs fois tous les résultats.</span><span class="sxs-lookup"><span data-stu-id="79a5e-133">hello **query** object contains a **HasMoreResults** boolean property that you can use tooinvoke hello **GetNextAsTwinAsync** methods multiple times tooretrieve all results.</span></span> <span data-ttu-id="79a5e-134">Une méthode appelée **GetNextAsJson** est disponible pour les résultats qui ne sont pas des jumeaux d’appareil, par exemple, les résultats de requêtes d’agrégation.</span><span class="sxs-lookup"><span data-stu-id="79a5e-134">A method called **GetNextAsJson** is available for results that are not device twins, for example, results of aggregation queries.</span></span>
1. <span data-ttu-id="79a5e-135">Enfin, ajoutez hello suivant lignes toohello **Main** méthode :</span><span class="sxs-lookup"><span data-stu-id="79a5e-135">Finally, add hello following lines toohello **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        AddTagsAndQuery().Wait();
        Console.WriteLine("Press Enter tooexit.");
        Console.ReadLine();

1. <span data-ttu-id="79a5e-136">Dans l’Explorateur de solutions de hello, ouvrez hello **projets de définir le démarrage...**  et assurez-vous que hello **Action** pour **AddTagsAndQuery** projet est **Démarrer**.</span><span class="sxs-lookup"><span data-stu-id="79a5e-136">In hello Solution Explorer, open hello **Set StartUp projects...** and make sure hello **Action** for **AddTagsAndQuery** project is **Start**.</span></span> <span data-ttu-id="79a5e-137">Générez la solution de hello.</span><span class="sxs-lookup"><span data-stu-id="79a5e-137">Build hello solution.</span></span>
1. <span data-ttu-id="79a5e-138">Exécution de cette application en cliquant sur hello **AddTagsAndQuery** projet et en sélectionnant **déboguer**, suivi par **démarrer une nouvelle instance**.</span><span class="sxs-lookup"><span data-stu-id="79a5e-138">Run this application by right-clicking on hello **AddTagsAndQuery** project and selecting **Debug**, followed by **Start new instance**.</span></span> <span data-ttu-id="79a5e-139">Vous devez voir un périphérique dans les résultats de hello pour poser des requêtes hello pour tous les appareils qui se trouve dans **Redmond43** et none pour les requêtes hello qui restreint hello toodevices qui utilisent un réseau cellulaire.</span><span class="sxs-lookup"><span data-stu-id="79a5e-139">You should see one device in hello results for hello query asking for all devices located in **Redmond43** and none for hello query that restricts hello results toodevices that use a cellular network.</span></span>
   
    ![Résultats de requête dans la fenêtre][img-addtagapp]

<span data-ttu-id="79a5e-141">Dans la section suivante de hello, vous créez une application de périphérique qui fournit des informations de connectivité hello et modifications hello résultat de requête hello dans la section précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="79a5e-141">In hello next section, you create a device app that reports hello connectivity information and changes hello result of hello query in hello previous section.</span></span>

## <a name="create-hello-device-app"></a><span data-ttu-id="79a5e-142">Créer l’application hello</span><span class="sxs-lookup"><span data-stu-id="79a5e-142">Create hello device app</span></span>
<span data-ttu-id="79a5e-143">Dans cette section, vous créez une application de console Node.js qui connecte le concentrateur tooyour **myDeviceId**, puis met à jour ses informations de hello toocontain propriétés signalé qu’il est connecté à l’aide d’un réseau cellulaire.</span><span class="sxs-lookup"><span data-stu-id="79a5e-143">In this section, you create a Node.js console app that connects tooyour hub as **myDeviceId**, and then updates its reported properties toocontain hello information that it is connected using a cellular network.</span></span>

1. <span data-ttu-id="79a5e-144">Créez un dossier vide nommé **reportconnectivity**.</span><span class="sxs-lookup"><span data-stu-id="79a5e-144">Create a new empty folder called **reportconnectivity**.</span></span> <span data-ttu-id="79a5e-145">Bonjour **reportconnectivity** dossier, créez un nouveau fichier package.json à l’aide de hello, la commande suivante à l’invite suivante.</span><span class="sxs-lookup"><span data-stu-id="79a5e-145">In hello **reportconnectivity** folder, create a new package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="79a5e-146">Acceptez les valeurs par défaut hello.</span><span class="sxs-lookup"><span data-stu-id="79a5e-146">Accept all hello defaults.</span></span>
   
    ```
    npm init
    ```
1. <span data-ttu-id="79a5e-147">Votre invite de commandes Bonjour **reportconnectivity** dossier, exécutez hello suivant commande tooinstall hello **azure iot-appareil**, et **azure-iot-périphérique-mqtt** package :</span><span class="sxs-lookup"><span data-stu-id="79a5e-147">At your command prompt in hello **reportconnectivity** folder, run hello following command tooinstall hello **azure-iot-device**, and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
1. <span data-ttu-id="79a5e-148">À l’aide d’un éditeur de texte, créez un nouveau **ReportConnectivity.js** fichier Bonjour **reportconnectivity** dossier.</span><span class="sxs-lookup"><span data-stu-id="79a5e-148">Using a text editor, create a new **ReportConnectivity.js** file in hello **reportconnectivity** folder.</span></span>
1. <span data-ttu-id="79a5e-149">Ajouter hello suivant code toohello **ReportConnectivity.js** de fichier et remplacez l’espace réservé de hello pour la chaîne de connexion de périphérique avec hello vous copié lors de la création de hello **myDeviceId** périphérique identité :</span><span class="sxs-lookup"><span data-stu-id="79a5e-149">Add hello following code toohello **ReportConnectivity.js** file, and substitute hello placeholder for device connection string with hello one you copied when you created hello **myDeviceId** device identity:</span></span>
   
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
   
    <span data-ttu-id="79a5e-150">Hello **Client** objet expose toutes les méthodes hello nécessitent de toointeract avec jumeaux de périphérique à partir de l’appareil de hello.</span><span class="sxs-lookup"><span data-stu-id="79a5e-150">hello **Client** object exposes all hello methods you require toointeract with device twins from hello device.</span></span> <span data-ttu-id="79a5e-151">Hello le code précédent, une fois qu’il initialise hello **Client** de l’objet, récupère hello double de périphérique pour **myDeviceId** et met à jour sa propriété signalée avec les informations de connectivité hello.</span><span class="sxs-lookup"><span data-stu-id="79a5e-151">hello previous code, after it initializes hello **Client** object, retrieves hello device twin for **myDeviceId** and updates its reported property with hello connectivity information.</span></span>
1. <span data-ttu-id="79a5e-152">Exécutez l’application hello</span><span class="sxs-lookup"><span data-stu-id="79a5e-152">Run hello device app</span></span>
   
        node ReportConnectivity.js
   
    <span data-ttu-id="79a5e-153">Vous devez voir le message de type hello `twin state reported`.</span><span class="sxs-lookup"><span data-stu-id="79a5e-153">You should see hello message `twin state reported`.</span></span>
1. <span data-ttu-id="79a5e-154">Maintenant que hello appareil signalé ses informations de connectivité, il doit s’afficher dans les deux requêtes.</span><span class="sxs-lookup"><span data-stu-id="79a5e-154">Now that hello device reported its connectivity information, it should appear in both queries.</span></span> <span data-ttu-id="79a5e-155">Exécutez hello .NET **AddTagsAndQuery** hello de toorun application interroge à nouveau.</span><span class="sxs-lookup"><span data-stu-id="79a5e-155">Run hello .NET **AddTagsAndQuery** app toorun hello queries again.</span></span> <span data-ttu-id="79a5e-156">Cette fois, **myDeviceId** doit apparaître dans les résultats des deux requêtes.</span><span class="sxs-lookup"><span data-stu-id="79a5e-156">This time **myDeviceId** should appear in both query results.</span></span>
   
    ![][img-addtagapp2]

## <a name="next-steps"></a><span data-ttu-id="79a5e-157">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="79a5e-157">Next steps</span></span>
<span data-ttu-id="79a5e-158">Dans ce didacticiel, vous configuré un IoT hub Bonjour portail Azure et ensuite créé une identité d’appareil dans le Registre des identités de hello IoT hub.</span><span class="sxs-lookup"><span data-stu-id="79a5e-158">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="79a5e-159">Vous ajouté des métadonnées de l’appareil sous forme de balises à partir d’une application back-end et a écrit un appareil simulé application tooreport appareil connectivité des informations en double du périphérique hello.</span><span class="sxs-lookup"><span data-stu-id="79a5e-159">You added device metadata as tags from a back-end app, and wrote a simulated device app tooreport device connectivity information in hello device twin.</span></span> <span data-ttu-id="79a5e-160">Vous avez également appris tooquery ces informations à l’aide du langage de requête de type SQL IoT Hub hello.</span><span class="sxs-lookup"><span data-stu-id="79a5e-160">You also learned how tooquery this information using hello SQL-like IoT Hub query language.</span></span>

<span data-ttu-id="79a5e-161">Hello utilisation suivant comment les ressources toolearn à :</span><span class="sxs-lookup"><span data-stu-id="79a5e-161">Use hello following resources toolearn how to:</span></span>

* <span data-ttu-id="79a5e-162">envoyer la télémétrie des appareils avec hello [prise en main IoT Hub] [ lnk-iothub-getstarted] (didacticiel),</span><span class="sxs-lookup"><span data-stu-id="79a5e-162">send telemetry from devices with hello [Get started with IoT Hub][lnk-iothub-getstarted] tutorial,</span></span>
* <span data-ttu-id="79a5e-163">configurer des appareils à l’aide des propriétés de votre choix du double de l’appareil avec hello [utilisation souhaitée propriétés tooconfigure dispositifs] [ lnk-twin-how-to-configure] (didacticiel),</span><span class="sxs-lookup"><span data-stu-id="79a5e-163">configure devices using device twin's desired properties with hello [Use desired properties tooconfigure devices][lnk-twin-how-to-configure] tutorial,</span></span>
* <span data-ttu-id="79a5e-164">contrôler les périphériques de manière interactive (telles que l’activation sur un ventilateur à partir d’une application contrôlée par l’utilisateur) avec hello [utiliser les méthodes directes] [ lnk-methods-tutorial] didacticiel.</span><span class="sxs-lookup"><span data-stu-id="79a5e-164">control devices interactively (such as turning on a fan from a user-controlled app) with hello [Use direct methods][lnk-methods-tutorial] tutorial.</span></span>

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

