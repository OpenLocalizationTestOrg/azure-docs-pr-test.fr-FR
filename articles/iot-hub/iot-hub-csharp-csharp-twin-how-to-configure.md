---
title: "propriétés de double de l’appareil Azure IoT Hub aaaUse (.NET/.NET) | Documents Microsoft"
description: "Comment jumeaux dispositif de Azure IoT Hub toouse tooconfigure périphériques. Vous utilisez hello Azure IoT SDK pour .NET tooimplement une application d’appareil simulé et hello Azure IoT service SDK pour .NET tooimplement une application de service qui modifie une configuration de l’appareil à l’aide d’un double de l’appareil."
services: iot-hub
documentationcenter: .net
author: dsk-2015
manager: timlt
editor: 
ms.assetid: 3c627476-f982-43c9-bd17-e0698c5d236d
ms.service: iot-hub
ms.devlang: csharp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/10/2017
ms.author: dkshir
ms.openlocfilehash: 486436d29abfd5158c253adc5abf5935e0e1fdba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-desired-properties-tooconfigure-devices"></a><span data-ttu-id="3394e-104">Utiliser les propriétés souhaitées tooconfigure périphériques</span><span class="sxs-lookup"><span data-stu-id="3394e-104">Use desired properties tooconfigure devices</span></span>
[!INCLUDE [iot-hub-selector-twin-how-to-configure](../../includes/iot-hub-selector-twin-how-to-configure.md)]

<span data-ttu-id="3394e-105">À la fin de hello de ce didacticiel, vous aurez deux applications de console .NET :</span><span class="sxs-lookup"><span data-stu-id="3394e-105">At hello end of this tutorial, you will have two .NET console apps:</span></span>

* <span data-ttu-id="3394e-106">**SimulateDeviceConfiguration**, une application d’appareil simulé qui attend une mise à jour de la configuration souhaitée et signale l’état hello d’un processus de mise à jour de configuration simulé.</span><span class="sxs-lookup"><span data-stu-id="3394e-106">**SimulateDeviceConfiguration**, a simulated device app that waits for a desired configuration update and reports hello status of a simulated configuration update process.</span></span>
* <span data-ttu-id="3394e-107">**SetDesiredConfigurationAndQuery**, une application back-end, qui définit hello souhaitée de configuration sur un appareil et requêtes hello le processus de mise à jour de configuration.</span><span class="sxs-lookup"><span data-stu-id="3394e-107">**SetDesiredConfigurationAndQuery**, a back-end app, which sets hello desired configuration on a device and queries hello configuration update process.</span></span>

> [!NOTE]
> <span data-ttu-id="3394e-108">article de Hello [kits de développement logiciel Azure IoT] [ lnk-hub-sdks] fournit des informations sur hello kits de développement logiciel Azure IoT que vous pouvez utiliser toobuild applications de périphérique et back-end.</span><span class="sxs-lookup"><span data-stu-id="3394e-108">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both device and back-end apps.</span></span>
> 
> 

<span data-ttu-id="3394e-109">toocomplete ce didacticiel, vous devez suivant de hello :</span><span class="sxs-lookup"><span data-stu-id="3394e-109">toocomplete this tutorial you need hello following:</span></span>

* <span data-ttu-id="3394e-110">Visual Studio 2015 ou Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="3394e-110">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="3394e-111">Un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="3394e-111">An active Azure account.</span></span> <span data-ttu-id="3394e-112">Si vous ne possédez pas de compte, vous pouvez créer un [compte gratuit][lnk-free-trial] en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="3394e-112">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>

<span data-ttu-id="3394e-113">Si vous avez suivi hello [prise en main jumeaux de périphérique] [ lnk-twin-tutorial] didacticiel, vous disposez déjà d’un IoT hub et une identité d’appareil appelé **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="3394e-113">If you followed hello [Get started with device twins][lnk-twin-tutorial] tutorial, you already have an IoT hub and a device identity called **myDeviceId**.</span></span> <span data-ttu-id="3394e-114">Dans ce cas, vous pouvez ignorer toohello [Create hello appareil simulé app] [ lnk-how-to-configure-createapp] section.</span><span class="sxs-lookup"><span data-stu-id="3394e-114">In that case, you can skip toohello [Create hello simulated device app][lnk-how-to-configure-createapp] section.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

<a id="#create-the-simulated-device-app"></a>
## <a name="create-hello-simulated-device-app"></a><span data-ttu-id="3394e-115">Créer l’application d’appareil simulé hello</span><span class="sxs-lookup"><span data-stu-id="3394e-115">Create hello simulated device app</span></span>
<span data-ttu-id="3394e-116">Dans cette section, vous créez une application console .NET qui se connecte concentrateur tooyour **myDeviceId**et attend une mise à jour de la configuration souhaitée et signale ensuite les mises à jour sur le processus de mise à jour de configuration hello simulé.</span><span class="sxs-lookup"><span data-stu-id="3394e-116">In this section, you create a .NET console app that connects tooyour hub as **myDeviceId**, waits for a desired configuration update and then reports updates on hello simulated configuration update process.</span></span>

1. <span data-ttu-id="3394e-117">Dans Visual Studio, créez un nouveau projet Visual c# bureau classique de Windows à l’aide de hello **Application Console** modèle de projet.</span><span class="sxs-lookup"><span data-stu-id="3394e-117">In Visual Studio, create a new Visual C# Windows Classic Desktop project by using hello **Console Application** project template.</span></span> <span data-ttu-id="3394e-118">Projet de hello nom **SimulateDeviceConfiguration**.</span><span class="sxs-lookup"><span data-stu-id="3394e-118">Name hello project **SimulateDeviceConfiguration**.</span></span>
   
    ![Nouvelle application pour appareil Windows classique Visual C#][img-createdeviceapp]

1. <span data-ttu-id="3394e-120">Dans l’Explorateur de solutions, cliquez sur hello **SimulateDeviceConfiguration** de projet, puis cliquez sur **gérer les Packages NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="3394e-120">In Solution Explorer, right-click hello **SimulateDeviceConfiguration** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="3394e-121">Bonjour **Gestionnaire de Package NuGet** fenêtre, sélectionnez **Parcourir** et recherchez **microsoft.azure.devices.client**.</span><span class="sxs-lookup"><span data-stu-id="3394e-121">In hello **NuGet Package Manager** window, select **Browse** and search for **microsoft.azure.devices.client**.</span></span> <span data-ttu-id="3394e-122">Sélectionnez **installer** tooinstall hello **Microsoft.Azure.Devices.Client** empaqueter et accepter les conditions d’utilisation de hello.</span><span class="sxs-lookup"><span data-stu-id="3394e-122">Select **Install** tooinstall hello **Microsoft.Azure.Devices.Client** package, and accept hello terms of use.</span></span> <span data-ttu-id="3394e-123">Cette procédure télécharge, installe et ajoute une référence toohello [Azure IoT appareil SDK] [ lnk-nuget-client-sdk] NuGet package et ses dépendances.</span><span class="sxs-lookup"><span data-stu-id="3394e-123">This procedure downloads, installs, and adds a reference toohello [Azure IoT device SDK][lnk-nuget-client-sdk] NuGet package and its dependencies.</span></span>
   
    ![Application cliente dans la fenêtre du gestionnaire de package NuGet][img-clientnuget]
1. <span data-ttu-id="3394e-125">Ajoutez hello suivant `using` instructions haut hello hello **Program.cs** fichier :</span><span class="sxs-lookup"><span data-stu-id="3394e-125">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices.Client;
        using Microsoft.Azure.Devices.Shared;
        using Newtonsoft.Json;

1. <span data-ttu-id="3394e-126">Ajouter hello suivant champs toohello **programme** classe.</span><span class="sxs-lookup"><span data-stu-id="3394e-126">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="3394e-127">Remplacez la valeur d’espace réservé hello avec la chaîne de connexion de périphérique hello que vous avez noté dans la section précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="3394e-127">Replace hello placeholder value with hello device connection string that you noted in hello previous section.</span></span>
   
        static string DeviceConnectionString = "HostName=<yourIotHubName>.azure-devices.net;DeviceId=<yourIotDeviceName>;SharedAccessKey=<yourIotDeviceAccessKey>";
        static DeviceClient Client = null;
        static TwinCollection reportedProperties = new TwinCollection();

1. <span data-ttu-id="3394e-128">Ajouter hello suivant de méthode toohello **programme** classe :</span><span class="sxs-lookup"><span data-stu-id="3394e-128">Add hello following method toohello **Program** class:</span></span>
 
        public static void InitClient()
        {
            try
            {
                Console.WriteLine("Connecting toohub");
                Client = DeviceClient.CreateFromConnectionString(DeviceConnectionString, TransportType.Mqtt);
            }
            catch (Exception ex)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", ex.Message);
            }
        }
    <span data-ttu-id="3394e-129">Hello **Client** objet expose toutes les méthodes hello nécessitent de toointeract avec jumeaux de périphérique à partir de l’appareil de hello.</span><span class="sxs-lookup"><span data-stu-id="3394e-129">hello **Client** object exposes all hello methods you require toointeract with device twins from hello device.</span></span> <span data-ttu-id="3394e-130">Hello code ci-dessus, initialise hello **Client** objet, puis récupère hello appareil double pour **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="3394e-130">hello code shown above, initializes hello **Client** object, and then retrieves hello device twin for **myDeviceId**.</span></span>

1. <span data-ttu-id="3394e-131">Ajouter hello suivant de méthode toohello **programme** classe.</span><span class="sxs-lookup"><span data-stu-id="3394e-131">Add hello following method toohello **Program** class.</span></span> <span data-ttu-id="3394e-132">Cette méthode définit les valeurs d’initiale de hello de télémétrie sur l’appareil local de hello, puis les mises à jour hello double de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="3394e-132">This method sets hello initial values of telemetry on hello local device and then updates hello device twin.</span></span>

        public static async void InitTelemetry()
        {
            try
            {
                Console.WriteLine("Report initial telemetry config:");
                TwinCollection telemetryConfig = new TwinCollection();
                
                telemetryConfig["configId"] = "0";
                telemetryConfig["sendFrequency"] = "24h";
                reportedProperties["telemetryConfig"] = telemetryConfig;
                Console.WriteLine(JsonConvert.SerializeObject(reportedProperties));

                await Client.UpdateReportedPropertiesAsync(reportedProperties);
            }
            catch (AggregateException ex)
            {
                foreach (Exception exception in ex.InnerExceptions)
                {
                    Console.WriteLine();
                    Console.WriteLine("Error in sample: {0}", exception);
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", ex.Message);
            }
        }

1. <span data-ttu-id="3394e-133">Ajouter hello suivant de méthode toohello **programme** classe.</span><span class="sxs-lookup"><span data-stu-id="3394e-133">Add hello following method toohello **Program** class.</span></span> <span data-ttu-id="3394e-134">Il s’agit d’un rappel qui détecte une modification de *propriétés souhaitée* deux conteneurs de périphérique hello.</span><span class="sxs-lookup"><span data-stu-id="3394e-134">This is a callback which will detect a change in *desired properties* in hello device twin.</span></span>

        private static async Task OnDesiredPropertyChanged(TwinCollection desiredProperties, object userContext)
        {
            try
            {
                Console.WriteLine("Desired property change:");
                Console.WriteLine(JsonConvert.SerializeObject(desiredProperties));

                var currentTelemetryConfig = reportedProperties["telemetryConfig"];
                var desiredTelemetryConfig = desiredProperties["telemetryConfig"];

                if ((desiredTelemetryConfig != null) && (desiredTelemetryConfig["configId"] != currentTelemetryConfig["configId"]))
                {
                    Console.WriteLine("\nInitiating config change");
                    currentTelemetryConfig["status"] = "Pending";
                    currentTelemetryConfig["pendingConfig"] = desiredTelemetryConfig;

                    await Client.UpdateReportedPropertiesAsync(reportedProperties);

                    CompleteConfigChange();
                }
            }
            catch (AggregateException ex)
            {
                foreach (Exception exception in ex.InnerExceptions)
                {
                    Console.WriteLine();
                    Console.WriteLine("Error in sample: {0}", exception);
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", ex.Message);
            }
        }

    <span data-ttu-id="3394e-135">Cette hello de mises à jour de méthode signalé propriétés sur l’objet de double hello périphérique local avec une configuration hello mises à jour demande et définit l’état de hello trop**en attente**, puis les mises à jour hello double du périphérique sur le service de hello.</span><span class="sxs-lookup"><span data-stu-id="3394e-135">This method updates hello reported properties on hello local device twin object with hello configuration update request and sets hello status too**Pending**, then updates hello device twin on hello service.</span></span> <span data-ttu-id="3394e-136">Après la mise à jour de double de périphérique hello, il termine hello modification de la configuration en appelant la méthode hello `CompleteConfigChange` décrite au point suivant de hello.</span><span class="sxs-lookup"><span data-stu-id="3394e-136">After successfully updating hello device twin, it completes hello config change by calling hello method `CompleteConfigChange` described in hello next point.</span></span>

1. <span data-ttu-id="3394e-137">Ajouter hello suivant de méthode toohello **programme** classe.</span><span class="sxs-lookup"><span data-stu-id="3394e-137">Add hello following method toohello **Program** class.</span></span> <span data-ttu-id="3394e-138">Cette méthode simule une réinitialisation du périphérique, puis les mises à jour hello propriétés signalées local définir le statut de hello trop**réussite** et supprime hello **pendingConfig** élément.</span><span class="sxs-lookup"><span data-stu-id="3394e-138">This method simulates a device reset, then updates hello local reported properties setting hello status too**Success** and removes hello **pendingConfig** element.</span></span> <span data-ttu-id="3394e-139">Il met ensuite à jour le double de périphérique hello sur le service de hello.</span><span class="sxs-lookup"><span data-stu-id="3394e-139">It then updates hello device twin on hello service.</span></span> 

        public static async void CompleteConfigChange()
        {
            try
            {
                var currentTelemetryConfig = reportedProperties["telemetryConfig"];

                Console.WriteLine("\nSimulating device reset");
                await Task.Delay(30000); 

                Console.WriteLine("\nCompleting config change");
                currentTelemetryConfig["configId"] = currentTelemetryConfig["pendingConfig"]["configId"];
                currentTelemetryConfig["sendFrequency"] = currentTelemetryConfig["pendingConfig"]["sendFrequency"];
                currentTelemetryConfig["status"] = "Success";
                currentTelemetryConfig["pendingConfig"] = null;

                await Client.UpdateReportedPropertiesAsync(reportedProperties);
                Console.WriteLine("Config change complete \nPress any key tooexit.");
            }
            catch (AggregateException ex)
            {
                foreach (Exception exception in ex.InnerExceptions)
                {
                    Console.WriteLine();
                    Console.WriteLine("Error in sample: {0}", exception);
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", ex.Message);
            }
        }

1. <span data-ttu-id="3394e-140">Ajoutez enfin hello suivant lignes toohello **Main** méthode :</span><span class="sxs-lookup"><span data-stu-id="3394e-140">Finally add hello following lines toohello **Main** method:</span></span>

        try
        {
            InitClient();
            InitTelemetry();

            Console.WriteLine("Wait for desired telemetry...");
            Client.SetDesiredPropertyUpdateCallback(OnDesiredPropertyChanged, null).Wait();
            Console.ReadKey();
        }
        catch (AggregateException ex)
        {
            foreach (Exception exception in ex.InnerExceptions)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", exception);
            }
        }
        catch (Exception ex)
        {
            Console.WriteLine();
            Console.WriteLine("Error in sample: {0}", ex.Message);
        }

   > [!NOTE]
   > <span data-ttu-id="3394e-141">Ce didacticiel ne simule pas de comportement pour des mises à jour de configuration simultanées.</span><span class="sxs-lookup"><span data-stu-id="3394e-141">This tutorial does not simulate any behavior for concurrent configuration updates.</span></span> <span data-ttu-id="3394e-142">Certains processus de mise à jour de configuration peuvent être en mesure de tooaccommodate des modifications de configuration de la cible pendant l’exécution de mise à jour hello, certaines peuvent comporter des tooqueue et certains peuvent rejeter les avec une condition d’erreur.</span><span class="sxs-lookup"><span data-stu-id="3394e-142">Some configuration update processes might be able tooaccommodate changes of target configuration while hello update is running, some might have tooqueue them, and some could reject them with an error condition.</span></span> <span data-ttu-id="3394e-143">Assurez-vous que tooconsider hello le comportement souhaité pour votre processus de configuration spécifique et ajouter une logique approprié de hello avant le lancement de la modification de configuration hello.</span><span class="sxs-lookup"><span data-stu-id="3394e-143">Make sure tooconsider hello desired behavior for your specific configuration process, and add hello appropriate logic before initiating hello configuration change.</span></span>
   > 
   > 
1. <span data-ttu-id="3394e-144">Générez la solution de hello et puis exécutez l’application hello à partir de Visual Studio en cliquant sur **F5**.</span><span class="sxs-lookup"><span data-stu-id="3394e-144">Build hello solution and then run hello device app from Visual Studio by clicking **F5**.</span></span> <span data-ttu-id="3394e-145">Dans la console de sortie hello, vous devez voir des messages hello indiquant que votre appareil simulé est la récupération de double de périphérique hello, la définition des données de télémétrie hello et en attente de la modification de la propriété souhaitée.</span><span class="sxs-lookup"><span data-stu-id="3394e-145">On hello output console, you should see hello messages indicating that your simulated device is retrieving hello device twin, setting up hello telemetry, and waiting for desired property change.</span></span> <span data-ttu-id="3394e-146">Gardez à l’application hello en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="3394e-146">Keep hello app running.</span></span>

## <a name="create-hello-service-app"></a><span data-ttu-id="3394e-147">Créer l’application de service hello</span><span class="sxs-lookup"><span data-stu-id="3394e-147">Create hello service app</span></span>
<span data-ttu-id="3394e-148">Dans cette section, vous allez créer une application de console .NET qui hello mises à jour *propriétés souhaitée* sur hello double de périphérique associé **myDeviceId** avec un nouvel objet de configuration de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="3394e-148">In this section, you will create a .NET console app that updates hello *desired properties* on hello device twin associated with **myDeviceId** with a new telemetry configuration object.</span></span> <span data-ttu-id="3394e-149">Il interroge jumeaux de périphérique hello stockées dans le hub IoT de hello et montre la différence hello entre hello souhaitée et a signalé des configurations de périphérique de hello.</span><span class="sxs-lookup"><span data-stu-id="3394e-149">It then queries hello device twins stored in hello IoT hub and shows hello difference between hello desired and reported configurations of hello device.</span></span>

1. <span data-ttu-id="3394e-150">Dans Visual Studio, ajoutez une solution d’actuel toohello de projet Visual c# bureau classique de Windows à l’aide de hello **Application Console** modèle de projet.</span><span class="sxs-lookup"><span data-stu-id="3394e-150">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution by using hello **Console Application** project template.</span></span> <span data-ttu-id="3394e-151">Projet de hello nom **SetDesiredConfigurationAndQuery**.</span><span class="sxs-lookup"><span data-stu-id="3394e-151">Name hello project **SetDesiredConfigurationAndQuery**.</span></span>
   
    ![Nouveau projet Visual C# Bureau classique Windows][img-createapp]
1. <span data-ttu-id="3394e-153">Dans l’Explorateur de solutions, cliquez sur hello **SetDesiredConfigurationAndQuery** de projet, puis cliquez sur **gérer les Packages NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="3394e-153">In Solution Explorer, right-click hello **SetDesiredConfigurationAndQuery** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="3394e-154">Bonjour **Gestionnaire de Package NuGet** fenêtre, sélectionnez **Parcourir**, recherchez **microsoft.azure.devices**, sélectionnez **installer** tooinstall Hello **Microsoft.Azure.Devices** empaqueter et accepter les conditions d’utilisation de hello.</span><span class="sxs-lookup"><span data-stu-id="3394e-154">In hello **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** tooinstall hello **Microsoft.Azure.Devices** package, and accept hello terms of use.</span></span> <span data-ttu-id="3394e-155">Cette procédure télécharge, installe et ajoute une référence toohello [Azure IoT service SDK] [ lnk-nuget-service-sdk] NuGet package et ses dépendances.</span><span class="sxs-lookup"><span data-stu-id="3394e-155">This procedure downloads, installs, and adds a reference toohello [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![Fenêtre du gestionnaire de package NuGet][img-servicenuget]
1. <span data-ttu-id="3394e-157">Ajoutez hello suivant `using` instructions haut hello hello **Program.cs** fichier :</span><span class="sxs-lookup"><span data-stu-id="3394e-157">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
        using System.Threading;
        using Newtonsoft.Json;
1. <span data-ttu-id="3394e-158">Ajouter hello suivant champs toohello **programme** classe.</span><span class="sxs-lookup"><span data-stu-id="3394e-158">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="3394e-159">Remplacer la valeur d’espace réservé hello avec hello chaîne de connexion de IoT Hub hub hello que vous avez créé dans la section précédente de hello de.</span><span class="sxs-lookup"><span data-stu-id="3394e-159">Replace hello placeholder value with hello IoT Hub connection string for hello hub that you created in hello previous section.</span></span>
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
1. <span data-ttu-id="3394e-160">Ajouter hello suivant de méthode toohello **programme** classe :</span><span class="sxs-lookup"><span data-stu-id="3394e-160">Add hello following method toohello **Program** class:</span></span>
   
        static private async Task SetDesiredConfigurationAndQuery()
        {
            var twin = await registryManager.GetTwinAsync("myDeviceId");
            var patch = new {
                    properties = new {
                        desired = new {
                            telemetryConfig = new {
                                configId = Guid.NewGuid().ToString(),
                                sendFrequency = "5m"
                            }
                        }
                    }
                };
   
            await registryManager.UpdateTwinAsync(twin.DeviceId, JsonConvert.SerializeObject(patch), twin.ETag);
            Console.WriteLine("Updated desired configuration");
   
            while (true)
            {
                var query = registryManager.CreateQuery("SELECT * FROM devices WHERE deviceId = 'myDeviceId'");
                var results = await query.GetNextAsTwinAsync();
                foreach (var result in results)
                {
                    Console.WriteLine("Config report for: {0}", result.DeviceId);
                    Console.WriteLine("Desired telemetryConfig: {0}", JsonConvert.SerializeObject(result.Properties.Desired["telemetryConfig"], Formatting.Indented));
                    Console.WriteLine("Reported telemetryConfig: {0}", JsonConvert.SerializeObject(result.Properties.Reported["telemetryConfig"], Formatting.Indented));
                    Console.WriteLine();
                }
                Thread.Sleep(10000);
            }
        }
   
    <span data-ttu-id="3394e-161">Hello **Registre** objet expose tous les hello méthodes requis toointeract avec jumeaux de périphérique à partir du service de hello.</span><span class="sxs-lookup"><span data-stu-id="3394e-161">hello **Registry** object exposes all hello methods required toointeract with device twins from hello service.</span></span> <span data-ttu-id="3394e-162">Ce code initialise hello **Registre** de l’objet, récupère hello double de périphérique pour **myDeviceId**, puis met à jour ses propriétés souhaitées par un nouvel objet de configuration de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="3394e-162">This code initializes hello **Registry** object, retrieves hello device twin for **myDeviceId**, and then updates its desired properties with a new telemetry configuration object.</span></span>
    <span data-ttu-id="3394e-163">Après cela, elle interroge jumeaux de périphérique hello stockées dans le hub IoT de hello toutes les 10 secondes et commander des photos hello souhaité et a signalé des configurations de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="3394e-163">After that, it queries hello device twins stored in hello IoT hub every 10 seconds, and prints hello desired and reported telemetry configurations.</span></span> <span data-ttu-id="3394e-164">Consultez toohello [langage de requête IoT Hub] [ lnk-query] toolearn comment toogenerate enrichi les rapports sur tous vos appareils.</span><span class="sxs-lookup"><span data-stu-id="3394e-164">Refer toohello [IoT Hub query language][lnk-query] toolearn how toogenerate rich reports across all your devices.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="3394e-165">Cette application interroge IoT Hub toutes les 10 secondes à titre d’exemple.</span><span class="sxs-lookup"><span data-stu-id="3394e-165">This application queries IoT Hub every 10 seconds for illustrative purposes.</span></span> <span data-ttu-id="3394e-166">Utilisez des requêtes toogenerate orientés utilisateur rapports entre plusieurs appareils et pas les modifications toodetect.</span><span class="sxs-lookup"><span data-stu-id="3394e-166">Use queries toogenerate user-facing reports across many devices, and not toodetect changes.</span></span> <span data-ttu-id="3394e-167">Si votre solution nécessite des notifications d’événements d’appareil en temps réel, utilisez des [notifications jumelles][lnk-twin-notifications].</span><span class="sxs-lookup"><span data-stu-id="3394e-167">If your solution requires real-time notifications of device events, use [twin notifications][lnk-twin-notifications].</span></span>
   > 
   > 
1. <span data-ttu-id="3394e-168">Enfin, ajoutez hello suivant lignes toohello **Main** méthode :</span><span class="sxs-lookup"><span data-stu-id="3394e-168">Finally, add hello following lines toohello **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        SetDesiredConfigurationAndQuery();
        Console.WriteLine("Press any key tooquit.");
        Console.ReadLine();
1. <span data-ttu-id="3394e-169">Dans l’Explorateur de solutions de hello, ouvrez hello **projets de définir le démarrage...**  et assurez-vous que hello **Action** pour **SetDesiredConfigurationAndQuery** projet est **Démarrer**.</span><span class="sxs-lookup"><span data-stu-id="3394e-169">In hello Solution Explorer, open hello **Set StartUp projects...** and make sure hello **Action** for **SetDesiredConfigurationAndQuery** project is **Start**.</span></span> <span data-ttu-id="3394e-170">Générez la solution de hello.</span><span class="sxs-lookup"><span data-stu-id="3394e-170">Build hello solution.</span></span>
1. <span data-ttu-id="3394e-171">Avec **SimulateDeviceConfiguration** en cours d’exécution application appareil, application de service de hello exécution à partir de Visual Studio à l’aide **F5**.</span><span class="sxs-lookup"><span data-stu-id="3394e-171">With **SimulateDeviceConfiguration** device app running, run hello service app from Visual Studio using **F5**.</span></span> <span data-ttu-id="3394e-172">Vous devez voir configuration signalé de hello modifier à partir de **en attente** trop**réussite** avec active de nouveau hello fréquence d’envoi des cinq minutes au lieu de 24 heures.</span><span class="sxs-lookup"><span data-stu-id="3394e-172">You should see hello reported configuration change from **Pending** too**Success** with hello new active send frequency of five minutes instead of 24 hours.</span></span>

 ![Appareil configuré correctement][img-deviceconfigured]
   
   > [!IMPORTANT]
   > <span data-ttu-id="3394e-174">Il existe un délai d’une minute tooa entre l’opération de rapport d’appareil hello et le résultat de la requête hello.</span><span class="sxs-lookup"><span data-stu-id="3394e-174">There is a delay of up tooa minute between hello device report operation and hello query result.</span></span> <span data-ttu-id="3394e-175">Il s’agit de tooenable hello requête infrastructure toowork à très grande échelle.</span><span class="sxs-lookup"><span data-stu-id="3394e-175">This is tooenable hello query infrastructure toowork at very high scale.</span></span> <span data-ttu-id="3394e-176">tooretrieve des vues cohérentes d’un double d’appareil unique utilisent hello **getDeviceTwin** méthode Bonjour **Registre** classe.</span><span class="sxs-lookup"><span data-stu-id="3394e-176">tooretrieve consistent views of a single device twin use hello **getDeviceTwin** method in hello **Registry** class.</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="3394e-177">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3394e-177">Next steps</span></span>
<span data-ttu-id="3394e-178">Dans ce didacticiel, vous définissez la configuration souhaitée en tant que *propriétés souhaitée* à partir de la solution de hello back-end et a écrit un toodetect application de périphérique qui changent et simuler un processus de mise à jour de plusieurs étapes son état hello signalé par le biais de création de rapports Propriétés.</span><span class="sxs-lookup"><span data-stu-id="3394e-178">In this tutorial, you set a desired configuration as *desired properties* from hello solution back end, and wrote a device app toodetect that change and simulate a multi-step update process reporting its status through hello reported properties.</span></span>

<span data-ttu-id="3394e-179">Hello utilisation suivant comment les ressources toolearn à :</span><span class="sxs-lookup"><span data-stu-id="3394e-179">Use hello following resources toolearn how to:</span></span>

* <span data-ttu-id="3394e-180">envoyer la télémétrie des appareils avec hello [prise en main IoT Hub] [ lnk-iothub-getstarted] (didacticiel),</span><span class="sxs-lookup"><span data-stu-id="3394e-180">send telemetry from devices with hello [Get started with IoT Hub][lnk-iothub-getstarted] tutorial,</span></span>
* <span data-ttu-id="3394e-181">planifier ou exécuter des opérations sur les grands ensembles de périphériques Voir hello [planification et les tâches de diffusion] [ lnk-schedule-jobs] didacticiel.</span><span class="sxs-lookup"><span data-stu-id="3394e-181">schedule or perform operations on large sets of devices see hello [Schedule and broadcast jobs][lnk-schedule-jobs] tutorial.</span></span>
* <span data-ttu-id="3394e-182">contrôler les périphériques de manière interactive (telles que l’activation sur un ventilateur à partir d’une application contrôlée par l’utilisateur), avec hello [utiliser les méthodes directes] [ lnk-methods-tutorial] didacticiel.</span><span class="sxs-lookup"><span data-stu-id="3394e-182">control devices interactively (such as turning on a fan from a user-controlled app), with hello [Use direct methods][lnk-methods-tutorial] tutorial.</span></span>

<!-- images -->
[img-servicenuget]: media/iot-hub-csharp-csharp-twin-how-to-configure/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-csharp-twin-how-to-configure/createnetapp.png
[img-deviceconfigured]: media/iot-hub-csharp-csharp-twin-how-to-configure/deviceconfigured.png
[img-createdeviceapp]: media/iot-hub-csharp-csharp-twin-how-to-configure/createdeviceapp.png
[img-clientnuget]: media/iot-hub-csharp-csharp-twin-how-to-configure/devicesdknuget.png
[img-deviceconfigured]: media/iot-hub-csharp-csharp-twin-how-to-configure/deviceconfigured.png


<!-- links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-nuget-client-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices.Client/
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/1.1.0/

[lnk-query]: iot-hub-devguide-query-language.md
[lnk-twin-notifications]: iot-hub-devguide-device-twins.md#back-end-operations
[lnk-twin-tutorial]: iot-hub-csharp-csharp-twin-getstarted.md
[lnk-schedule-jobs]: iot-hub-node-node-schedule-jobs.md
[lnk-iothub-getstarted]: iot-hub-csharp-csharp-getstarted.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md
[lnk-how-to-configure-createapp]: iot-hub-csharp-csharp-twin-how-to-configure.md#create-the-simulated-device-app
