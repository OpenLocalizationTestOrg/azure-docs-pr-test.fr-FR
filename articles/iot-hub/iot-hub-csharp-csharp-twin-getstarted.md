---
title: "aaaGet main jumeaux d’appareil Azure IoT Hub (.NET/.NET) | Documents Microsoft"
description: "Comment toouse Azure IoT Hub appareil jumeaux tooadd balises, puis utilisez une requête IoT Hub. Vous utilisez du SDK de périphérique Azure IoT hello pour application d’appareil simulé .NET tooimplement hello et hello Azure IoT service SDK pour .NET tooimplement une application de service qui ajoute des balises de hello et s’exécute hello requête de IoT Hub."
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
ms.openlocfilehash: 7fa73ac896c44e79c6522d252cd1515bd6e7bb2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-device-twins-netnet"></a><span data-ttu-id="7712e-104">Bien démarrer avec les jumeaux d’appareils (.NET/.NET)</span><span class="sxs-lookup"><span data-stu-id="7712e-104">Get started with device twins (.NET/.NET)</span></span>
[!INCLUDE [iot-hub-selector-twin-get-started](../../includes/iot-hub-selector-twin-get-started.md)]

<span data-ttu-id="7712e-105">À la fin de hello de ce didacticiel, vous disposerez ces applications de console .NET :</span><span class="sxs-lookup"><span data-stu-id="7712e-105">At hello end of this tutorial, you will have these .NET console apps:</span></span>

* <span data-ttu-id="7712e-106">**CreateDeviceIdentity**, une application .NET qui crée une identité de l’appareil et la sécurité associés clé tooconnect votre application d’appareil simulé.</span><span class="sxs-lookup"><span data-stu-id="7712e-106">**CreateDeviceIdentity**, a .NET app which creates a device identity and associated security key tooconnect your simulated device app.</span></span>
* <span data-ttu-id="7712e-107">**AddTagsAndQuery**, application principale .NET qui ajoute des balises et interroge des jumeaux d’appareil.</span><span class="sxs-lookup"><span data-stu-id="7712e-107">**AddTagsAndQuery**, a .NET back-end app which adds tags and queries device twins.</span></span>
* <span data-ttu-id="7712e-108">**ReportConnectivity**, une périphérique d’application .NET qui simule un appareil qui se connecte tooyour IoT hub avec l’identité de l’appareil hello créée précédemment et signale l’état de connectivité.</span><span class="sxs-lookup"><span data-stu-id="7712e-108">**ReportConnectivity**, a .NET device app which simulates a device that connects tooyour IoT hub with hello device identity created earlier, and reports its connectivity condition.</span></span>

> [!NOTE]
> <span data-ttu-id="7712e-109">article de Hello [kits de développement logiciel Azure IoT] [ lnk-hub-sdks] fournit des informations sur hello kits de développement logiciel Azure IoT que vous pouvez utiliser toobuild applications de périphérique et back-end.</span><span class="sxs-lookup"><span data-stu-id="7712e-109">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both device and back-end apps.</span></span>
> 
> 

<span data-ttu-id="7712e-110">toocomplete ce didacticiel, vous devez suivant de hello :</span><span class="sxs-lookup"><span data-stu-id="7712e-110">toocomplete this tutorial you need hello following:</span></span>

* <span data-ttu-id="7712e-111">Visual Studio 2015 ou Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="7712e-111">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="7712e-112">Un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="7712e-112">An active Azure account.</span></span> <span data-ttu-id="7712e-113">(Si vous ne possédez pas de compte, vous pouvez créer un [compte gratuit][lnk-free-trial] en quelques minutes.)</span><span class="sxs-lookup"><span data-stu-id="7712e-113">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

<span data-ttu-id="7712e-114">Si vous souhaitez identité d’appareil toocreate hello par programme à la place, lire la section correspondante de hello Bonjour [connectez votre concentrateur de IoT tooyour appareil simulé à l’aide de .NET] [ lnk-device-identity-csharp] l’article.</span><span class="sxs-lookup"><span data-stu-id="7712e-114">If you want toocreate hello device identity programmatically instead, read hello corresponding section in hello [Connect your simulated device tooyour IoT hub using .NET][lnk-device-identity-csharp] article.</span></span>

## <a name="create-hello-service-app"></a><span data-ttu-id="7712e-115">Créer l’application de service hello</span><span class="sxs-lookup"><span data-stu-id="7712e-115">Create hello service app</span></span>
<span data-ttu-id="7712e-116">Dans cette section, vous créez .NET application console (à l’aide de c#) ajoute double d’appareil emplacement métadonnées toohello associé **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="7712e-116">In this section, you create a .NET console app (using C#) that adds location metadata toohello device twin associated with **myDeviceId**.</span></span> <span data-ttu-id="7712e-117">Il interroge ensuite jumeaux de périphérique hello stockées dans hello IoT hub en sélectionnant les appareils hello situés dans hello nous et puis hello ceux qui a signalé une connexion cellulaire.</span><span class="sxs-lookup"><span data-stu-id="7712e-117">It then queries hello device twins stored in hello IoT hub selecting hello devices located in hello US, and then hello ones that reported a cellular connection.</span></span>

1. <span data-ttu-id="7712e-118">Dans Visual Studio, ajoutez une solution d’actuel toohello de projet Visual c# bureau classique de Windows à l’aide de hello **Application Console** modèle de projet.</span><span class="sxs-lookup"><span data-stu-id="7712e-118">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution by using hello **Console Application** project template.</span></span> <span data-ttu-id="7712e-119">Projet de hello nom **AddTagsAndQuery**.</span><span class="sxs-lookup"><span data-stu-id="7712e-119">Name hello project **AddTagsAndQuery**.</span></span>
   
    ![Nouveau projet Visual C# Bureau classique Windows][img-createapp]
1. <span data-ttu-id="7712e-121">Dans l’Explorateur de solutions, cliquez sur hello **AddTagsAndQuery** de projet, puis cliquez sur **gérer les Packages NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="7712e-121">In Solution Explorer, right-click hello **AddTagsAndQuery** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="7712e-122">Bonjour **Gestionnaire de Package NuGet** fenêtre, sélectionnez **Parcourir** et recherchez **microsoft.azure.devices**.</span><span class="sxs-lookup"><span data-stu-id="7712e-122">In hello **NuGet Package Manager** window, select **Browse** and search for **microsoft.azure.devices**.</span></span> <span data-ttu-id="7712e-123">Sélectionnez **installer** tooinstall hello **Microsoft.Azure.Devices** empaqueter et accepter les conditions d’utilisation de hello.</span><span class="sxs-lookup"><span data-stu-id="7712e-123">Select **Install** tooinstall hello **Microsoft.Azure.Devices** package, and accept hello terms of use.</span></span> <span data-ttu-id="7712e-124">Cette procédure télécharge, installe et ajoute une référence toohello [Azure IoT service SDK] [ lnk-nuget-service-sdk] NuGet package et ses dépendances.</span><span class="sxs-lookup"><span data-stu-id="7712e-124">This procedure downloads, installs, and adds a reference toohello [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![Fenêtre du gestionnaire de package NuGet][img-servicenuget]
1. <span data-ttu-id="7712e-126">Ajoutez hello suivant `using` instructions haut hello hello **Program.cs** fichier :</span><span class="sxs-lookup"><span data-stu-id="7712e-126">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
1. <span data-ttu-id="7712e-127">Ajouter hello suivant champs toohello **programme** classe.</span><span class="sxs-lookup"><span data-stu-id="7712e-127">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="7712e-128">Remplacer la valeur d’espace réservé hello avec hello chaîne de connexion de IoT Hub hub hello que vous avez créé dans la section précédente de hello de.</span><span class="sxs-lookup"><span data-stu-id="7712e-128">Replace hello placeholder value with hello IoT Hub connection string for hello hub that you created in hello previous section.</span></span>
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
1. <span data-ttu-id="7712e-129">Ajouter hello suivant de méthode toohello **programme** classe :</span><span class="sxs-lookup"><span data-stu-id="7712e-129">Add hello following method toohello **Program** class:</span></span>
   
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
   
    <span data-ttu-id="7712e-130">Hello **RegistryManager** classe expose tous les hello méthodes requis toointeract avec jumeaux de périphérique à partir du service de hello.</span><span class="sxs-lookup"><span data-stu-id="7712e-130">hello **RegistryManager** class exposes all hello methods required toointeract with device twins from hello service.</span></span> <span data-ttu-id="7712e-131">code précédent de Hello initialise tout d’abord hello **registryManager** de l’objet, puis récupère hello double de périphérique pour **myDeviceId**et enfin met à jour ses balises avec les informations d’emplacement hello souhaité.</span><span class="sxs-lookup"><span data-stu-id="7712e-131">hello previous code first initializes hello **registryManager** object, then retrieves hello device twin for **myDeviceId**, and finally updates its tags with hello desired location information.</span></span>
   
    <span data-ttu-id="7712e-132">Après la mise à jour, il exécute deux requêtes : hello sélectionne tout d’abord uniquement les jumeaux appareil hello des périphériques situés dans hello **Redmond43** usine et hello deuxième affine hello requête tooselect uniquement hello pour les appareils qui sont également connectés via réseau cellulaire.</span><span class="sxs-lookup"><span data-stu-id="7712e-132">After updating, it executes two queries: hello first selects only hello device twins of devices located in hello **Redmond43** plant, and hello second refines hello query tooselect only hello devices that are also connected through cellular network.</span></span>
   
    <span data-ttu-id="7712e-133">Notez que hello le code précédent, lorsqu’il crée hello **requête** d’objet, spécifie un nombre maximal de documents renvoyés.</span><span class="sxs-lookup"><span data-stu-id="7712e-133">Note that hello previous code, when it creates hello **query** object, specifies a maximum number of returned documents.</span></span> <span data-ttu-id="7712e-134">Hello **requête** objet contient un **HasMoreResults** propriété booléenne que vous pouvez utiliser tooinvoke hello **GetNextAsTwinAsync** méthodes tooretrieve plusieurs fois tous les résultats.</span><span class="sxs-lookup"><span data-stu-id="7712e-134">hello **query** object contains a **HasMoreResults** boolean property that you can use tooinvoke hello **GetNextAsTwinAsync** methods multiple times tooretrieve all results.</span></span> <span data-ttu-id="7712e-135">Une méthode appelée **GetNextAsJson** est disponible pour les résultats qui ne sont pas des jumeaux d’appareil, par exemple, les résultats de requêtes d’agrégation.</span><span class="sxs-lookup"><span data-stu-id="7712e-135">A method called **GetNextAsJson** is available for results that are not device twins, for example, results of aggregation queries.</span></span>
1. <span data-ttu-id="7712e-136">Enfin, ajoutez hello suivant lignes toohello **Main** méthode :</span><span class="sxs-lookup"><span data-stu-id="7712e-136">Finally, add hello following lines toohello **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        AddTagsAndQuery().Wait();
        Console.WriteLine("Press Enter tooexit.");
        Console.ReadLine();

1. <span data-ttu-id="7712e-137">Dans l’Explorateur de solutions de hello, ouvrez hello **projets de définir le démarrage...**  et assurez-vous que hello **Action** pour **AddTagsAndQuery** projet est **Démarrer**.</span><span class="sxs-lookup"><span data-stu-id="7712e-137">In hello Solution Explorer, open hello **Set StartUp projects...** and make sure hello **Action** for **AddTagsAndQuery** project is **Start**.</span></span> <span data-ttu-id="7712e-138">Générez la solution de hello.</span><span class="sxs-lookup"><span data-stu-id="7712e-138">Build hello solution.</span></span>
1. <span data-ttu-id="7712e-139">Exécution de cette application en cliquant sur hello **AddTagsAndQuery** projet et en sélectionnant **déboguer**, suivi par **démarrer une nouvelle instance**.</span><span class="sxs-lookup"><span data-stu-id="7712e-139">Run this application by right-clicking on hello **AddTagsAndQuery** project and selecting **Debug**, followed by **Start new instance**.</span></span> <span data-ttu-id="7712e-140">Vous devez voir un périphérique dans les résultats de hello pour poser des requêtes hello pour tous les appareils qui se trouve dans **Redmond43** et none pour les requêtes hello qui restreint hello toodevices qui utilisent un réseau cellulaire.</span><span class="sxs-lookup"><span data-stu-id="7712e-140">You should see one device in hello results for hello query asking for all devices located in **Redmond43** and none for hello query that restricts hello results toodevices that use a cellular network.</span></span>
   
    ![Résultats de requête dans la fenêtre][img-addtagapp]

<span data-ttu-id="7712e-142">Dans la section suivante de hello, vous créez une application de périphérique qui fournit des informations de connectivité hello et modifications hello résultat de requête hello dans la section précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="7712e-142">In hello next section, you create a device app that reports hello connectivity information and changes hello result of hello query in hello previous section.</span></span>

## <a name="create-hello-device-app"></a><span data-ttu-id="7712e-143">Créer l’application hello</span><span class="sxs-lookup"><span data-stu-id="7712e-143">Create hello device app</span></span>
<span data-ttu-id="7712e-144">Dans cette section, vous créez une application console .NET qui se connecte concentrateur tooyour **myDeviceId**, puis met à jour ses informations de hello toocontain propriétés signalé qu’il est connecté à l’aide d’un réseau cellulaire.</span><span class="sxs-lookup"><span data-stu-id="7712e-144">In this section, you create a .NET console app that connects tooyour hub as **myDeviceId**, and then updates its reported properties toocontain hello information that it is connected using a cellular network.</span></span>

1. <span data-ttu-id="7712e-145">Dans Visual Studio, ajoutez une solution d’actuel toohello de projet Visual c# bureau classique de Windows à l’aide de hello **Application Console** modèle de projet.</span><span class="sxs-lookup"><span data-stu-id="7712e-145">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution by using hello **Console Application** project template.</span></span> <span data-ttu-id="7712e-146">Projet de hello nom **ReportConnectivity**.</span><span class="sxs-lookup"><span data-stu-id="7712e-146">Name hello project **ReportConnectivity**.</span></span>
   
    ![Nouvelle application pour appareil Windows classique Visual C#][img-createdeviceapp]
    
1. <span data-ttu-id="7712e-148">Dans l’Explorateur de solutions, cliquez sur hello **ReportConnectivity** de projet, puis cliquez sur **gérer les Packages NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="7712e-148">In Solution Explorer, right-click hello **ReportConnectivity** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="7712e-149">Bonjour **Gestionnaire de Package NuGet** fenêtre, sélectionnez **Parcourir** et recherchez **microsoft.azure.devices.client**.</span><span class="sxs-lookup"><span data-stu-id="7712e-149">In hello **NuGet Package Manager** window, select **Browse** and search for **microsoft.azure.devices.client**.</span></span> <span data-ttu-id="7712e-150">Sélectionnez **installer** tooinstall hello **Microsoft.Azure.Devices.Client** empaqueter et accepter les conditions d’utilisation de hello.</span><span class="sxs-lookup"><span data-stu-id="7712e-150">Select **Install** tooinstall hello **Microsoft.Azure.Devices.Client** package, and accept hello terms of use.</span></span> <span data-ttu-id="7712e-151">Cette procédure télécharge, installe et ajoute une référence toohello [Azure IoT appareil SDK] [ lnk-nuget-client-sdk] NuGet package et ses dépendances.</span><span class="sxs-lookup"><span data-stu-id="7712e-151">This procedure downloads, installs, and adds a reference toohello [Azure IoT device SDK][lnk-nuget-client-sdk] NuGet package and its dependencies.</span></span>
   
    ![Application cliente dans la fenêtre du gestionnaire de package NuGet][img-clientnuget]
1. <span data-ttu-id="7712e-153">Ajoutez hello suivant `using` instructions haut hello hello **Program.cs** fichier :</span><span class="sxs-lookup"><span data-stu-id="7712e-153">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices.Client;
        using Microsoft.Azure.Devices.Shared;
        using Newtonsoft.Json;

1. <span data-ttu-id="7712e-154">Ajouter hello suivant champs toohello **programme** classe.</span><span class="sxs-lookup"><span data-stu-id="7712e-154">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="7712e-155">Remplacez la valeur d’espace réservé hello avec la chaîne de connexion de périphérique hello que vous avez noté dans la section précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="7712e-155">Replace hello placeholder value with hello device connection string that you noted in hello previous section.</span></span>
   
        static string DeviceConnectionString = "HostName=<yourIotHubName>.azure-devices.net;DeviceId=<yourIotDeviceName>;SharedAccessKey=<yourIotDeviceAccessKey>";
        static DeviceClient Client = null;

1. <span data-ttu-id="7712e-156">Ajouter hello suivant de méthode toohello **programme** classe :</span><span class="sxs-lookup"><span data-stu-id="7712e-156">Add hello following method toohello **Program** class:</span></span>

       public static async void InitClient()
        {
            try
            {
                Console.WriteLine("Connecting toohub");
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

    <span data-ttu-id="7712e-157">Hello **Client** objet expose toutes les méthodes hello nécessitent de toointeract avec jumeaux de périphérique à partir de l’appareil de hello.</span><span class="sxs-lookup"><span data-stu-id="7712e-157">hello **Client** object exposes all hello methods you require toointeract with device twins from hello device.</span></span> <span data-ttu-id="7712e-158">Hello code ci-dessus, initialise hello **Client** objet, puis récupère hello appareil double pour **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="7712e-158">hello code shown above, initializes hello **Client** object, and then retrieves hello device twin for **myDeviceId**.</span></span>

1. <span data-ttu-id="7712e-159">Ajouter hello suivant de méthode toohello **programme** classe :</span><span class="sxs-lookup"><span data-stu-id="7712e-159">Add hello following method toohello **Program** class:</span></span>
   
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

   <span data-ttu-id="7712e-160">Hello code au-dessus de mises à jour **myDeviceId**de signalé propriété avec les informations de connectivité hello.</span><span class="sxs-lookup"><span data-stu-id="7712e-160">hello code above updates **myDeviceId**'s reported property with hello connectivity information.</span></span>

1. <span data-ttu-id="7712e-161">Enfin, ajoutez hello suivant lignes toohello **Main** méthode :</span><span class="sxs-lookup"><span data-stu-id="7712e-161">Finally, add hello following lines toohello **Main** method:</span></span>
   
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
       Console.WriteLine("Press Enter tooexit.");
       Console.ReadLine();

1. <span data-ttu-id="7712e-162">Dans l’Explorateur de solutions de hello, ouvrez hello **projets de définir le démarrage...**  et assurez-vous que hello **Action** pour **ReportConnectivity** projet est **Démarrer**.</span><span class="sxs-lookup"><span data-stu-id="7712e-162">In hello Solution Explorer, open hello **Set StartUp projects...** and make sure hello **Action** for **ReportConnectivity** project is **Start**.</span></span> <span data-ttu-id="7712e-163">Générez la solution de hello.</span><span class="sxs-lookup"><span data-stu-id="7712e-163">Build hello solution.</span></span>
1. <span data-ttu-id="7712e-164">Exécution de cette application en cliquant sur hello **ReportConnectivity** projet et en sélectionnant **déboguer**, suivi par **démarrer une nouvelle instance**.</span><span class="sxs-lookup"><span data-stu-id="7712e-164">Run this application by right-clicking on hello **ReportConnectivity** project and selecting **Debug**, followed by **Start new instance**.</span></span> <span data-ttu-id="7712e-165">Vous devez le voir obtention des informations sur le double hello et connectivité que d’envoyer un *signalé propriété*.</span><span class="sxs-lookup"><span data-stu-id="7712e-165">You should see it getting hello twin information, and then sending connectivity as a *reported property*.</span></span>
   
    ![Exécuter une connexion de périphérique application tooreport][img-rundeviceapp]
    
    
1. <span data-ttu-id="7712e-167">Maintenant que hello appareil signalé ses informations de connectivité, il doit s’afficher dans les deux requêtes.</span><span class="sxs-lookup"><span data-stu-id="7712e-167">Now that hello device reported its connectivity information, it should appear in both queries.</span></span> <span data-ttu-id="7712e-168">Exécutez hello .NET **AddTagsAndQuery** hello de toorun application interroge à nouveau.</span><span class="sxs-lookup"><span data-stu-id="7712e-168">Run hello .NET **AddTagsAndQuery** app toorun hello queries again.</span></span> <span data-ttu-id="7712e-169">Cette fois, **myDeviceId** doit apparaître dans les résultats des deux requêtes.</span><span class="sxs-lookup"><span data-stu-id="7712e-169">This time **myDeviceId** should appear in both query results.</span></span>
   
    ![Connectivité des appareils signalée avec succès][img-tagappsuccess]

## <a name="next-steps"></a><span data-ttu-id="7712e-171">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7712e-171">Next steps</span></span>
<span data-ttu-id="7712e-172">Dans ce didacticiel, vous configuré un IoT hub Bonjour portail Azure et ensuite créé une identité d’appareil dans le Registre des identités de hello IoT hub.</span><span class="sxs-lookup"><span data-stu-id="7712e-172">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="7712e-173">Vous ajouté des métadonnées de l’appareil sous forme de balises à partir d’une application back-end et a écrit un appareil simulé application tooreport appareil connectivité des informations en double du périphérique hello.</span><span class="sxs-lookup"><span data-stu-id="7712e-173">You added device metadata as tags from a back-end app, and wrote a simulated device app tooreport device connectivity information in hello device twin.</span></span> <span data-ttu-id="7712e-174">Vous avez également appris tooquery ces informations à l’aide du langage de requête de type SQL IoT Hub hello.</span><span class="sxs-lookup"><span data-stu-id="7712e-174">You also learned how tooquery this information using hello SQL-like IoT Hub query language.</span></span>

<span data-ttu-id="7712e-175">Hello utilisation suivant comment les ressources toolearn à :</span><span class="sxs-lookup"><span data-stu-id="7712e-175">Use hello following resources toolearn how to:</span></span>

* <span data-ttu-id="7712e-176">envoyer la télémétrie des appareils avec hello [prise en main IoT Hub] [ lnk-iothub-getstarted] (didacticiel),</span><span class="sxs-lookup"><span data-stu-id="7712e-176">send telemetry from devices with hello [Get started with IoT Hub][lnk-iothub-getstarted] tutorial,</span></span>
* <span data-ttu-id="7712e-177">configurer des appareils à l’aide des propriétés de votre choix du double de l’appareil avec hello [utilisation souhaitée propriétés tooconfigure dispositifs] [ lnk-twin-how-to-configure] (didacticiel),</span><span class="sxs-lookup"><span data-stu-id="7712e-177">configure devices using device twin's desired properties with hello [Use desired properties tooconfigure devices][lnk-twin-how-to-configure] tutorial,</span></span>
* <span data-ttu-id="7712e-178">contrôler les périphériques de manière interactive (telles que l’activation sur un ventilateur à partir d’une application contrôlée par l’utilisateur) avec hello [utiliser les méthodes directes] [ lnk-methods-tutorial] didacticiel.</span><span class="sxs-lookup"><span data-stu-id="7712e-178">control devices interactively (such as turning on a fan from a user-controlled app) with hello [Use direct methods][lnk-methods-tutorial] tutorial.</span></span>

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

