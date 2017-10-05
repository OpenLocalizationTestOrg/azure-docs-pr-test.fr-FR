---
title: "Personnalisation des solutions préconfigurées | Microsoft Docs"
description: "Fournit des conseils sur la personnalisation des solutions préconfigurées Azure IoT Suite."
services: 
suite: iot-suite
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 4653ae53-4110-4a10-bd6c-7dc034c293a8
ms.service: iot-suite
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: corywink
ms.openlocfilehash: bdf4cd89d5ad0392337dfe761108608d506adf18
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="customize-a-preconfigured-solution"></a><span data-ttu-id="0ce74-103">Personnaliser une solution préconfigurée</span><span class="sxs-lookup"><span data-stu-id="0ce74-103">Customize a preconfigured solution</span></span>

<span data-ttu-id="0ce74-104">Les solutions préconfigurées fournies avec Azure IoT Suite présentent les services de la suite qui collaborent pour fournir une solution de bout en bout.</span><span class="sxs-lookup"><span data-stu-id="0ce74-104">The preconfigured solutions provided with the Azure IoT Suite demonstrate the services within the suite working together to deliver an end-to-end solution.</span></span> <span data-ttu-id="0ce74-105">À partir de ce point de départ, il existe différents endroits où vous pouvez étendre et personnaliser la solution pour des scénarios spécifiques.</span><span class="sxs-lookup"><span data-stu-id="0ce74-105">From this starting point, there are various places in which you can extend and customize the solution for specific scenarios.</span></span> <span data-ttu-id="0ce74-106">Les sections suivantes décrivent ces points de personnalisation courants.</span><span class="sxs-lookup"><span data-stu-id="0ce74-106">The following sections describe these common customization points.</span></span>

## <a name="find-the-source-code"></a><span data-ttu-id="0ce74-107">Recherche du code source</span><span class="sxs-lookup"><span data-stu-id="0ce74-107">Find the source code</span></span>

<span data-ttu-id="0ce74-108">Le code source pour les solutions préconfigurées est disponible sur GitHub dans les dépôts suivants :</span><span class="sxs-lookup"><span data-stu-id="0ce74-108">The source code for the preconfigured solutions is available on GitHub in the following repositories:</span></span>

* <span data-ttu-id="0ce74-109">Surveillance à distance : [https://www.github.com/Azure/azure-iot-remote-monitoring](https://github.com/Azure/azure-iot-remote-monitoring)</span><span class="sxs-lookup"><span data-stu-id="0ce74-109">Remote Monitoring: [https://www.github.com/Azure/azure-iot-remote-monitoring](https://github.com/Azure/azure-iot-remote-monitoring)</span></span>
* <span data-ttu-id="0ce74-110">Maintenance prédictive : [https://github.com/Azure/azure-iot-predictive-maintenance](https://github.com/Azure/azure-iot-predictive-maintenance)</span><span class="sxs-lookup"><span data-stu-id="0ce74-110">Predictive Maintenance: [https://github.com/Azure/azure-iot-predictive-maintenance](https://github.com/Azure/azure-iot-predictive-maintenance)</span></span>
* <span data-ttu-id="0ce74-111">Usine connectée : [https://github.com/Azure/azure-iot-connected-factory](https://github.com/Azure/azure-iot-connected-factory)</span><span class="sxs-lookup"><span data-stu-id="0ce74-111">Connected factory: [https://github.com/Azure/azure-iot-connected-factory](https://github.com/Azure/azure-iot-connected-factory)</span></span>

<span data-ttu-id="0ce74-112">Le code source pour les solutions préconfigurées est fourni dans le but d’illustrer les modèles et pratiques utilisés pour implémenter la fonctionnalité de bout en bout d’une solution IoT utilisant Azure IoT Suite.</span><span class="sxs-lookup"><span data-stu-id="0ce74-112">The source code for the preconfigured solutions is provided to demonstrate the patterns and practices used to implement the end-to-end functionality of an IoT solution using Azure IoT Suite.</span></span> <span data-ttu-id="0ce74-113">Pour plus d’informations sur la création et le déploiement des solutions, consultez les dépôts GitHub.</span><span class="sxs-lookup"><span data-stu-id="0ce74-113">You can find more information about how to build and deploy the solutions in the GitHub repositories.</span></span>

## <a name="change-the-preconfigured-rules"></a><span data-ttu-id="0ce74-114">Modification des règles préconfigurées</span><span class="sxs-lookup"><span data-stu-id="0ce74-114">Change the preconfigured rules</span></span>

<span data-ttu-id="0ce74-115">La solution de surveillance à distance inclut trois travaux [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/) destinés à gérer la logique d’informations, de règles et de télémétrie dans la solution.</span><span class="sxs-lookup"><span data-stu-id="0ce74-115">The remote monitoring solution includes three [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/) jobs to handle device information, telemetry, and rules logic in the solution.</span></span>

<span data-ttu-id="0ce74-116">Les trois travaux Stream Analytics et leur syntaxe sont décrits en détail dans [Présentation de la solution préconfigurée de surveillance à distance](iot-suite-remote-monitoring-sample-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="0ce74-116">The three stream analytics jobs and their syntax are described in depth in the [Remote monitoring preconfigured solution walkthrough](iot-suite-remote-monitoring-sample-walkthrough.md).</span></span> 

<span data-ttu-id="0ce74-117">Vous pouvez modifier ces tâches directement pour en modifier la logique, ou ajouter une logique spécifique à votre scénario.</span><span class="sxs-lookup"><span data-stu-id="0ce74-117">You can edit these jobs directly to alter the logic, or add logic specific to your scenario.</span></span> <span data-ttu-id="0ce74-118">Pour rechercher les tâches Stream Analytics, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="0ce74-118">You can find the Stream Analytics jobs as follows:</span></span>

1. <span data-ttu-id="0ce74-119">Accédez au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0ce74-119">Go to [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="0ce74-120">Accédez au groupe de ressources portant le même nom que votre solution IoT.</span><span class="sxs-lookup"><span data-stu-id="0ce74-120">Navigate to the resource group with the same name as your IoT solution.</span></span> 
3. <span data-ttu-id="0ce74-121">Sélectionnez la tâche Azure Stream Analytics à modifier.</span><span class="sxs-lookup"><span data-stu-id="0ce74-121">Select the Azure Stream Analytics job you'd like to modify.</span></span> 
4. <span data-ttu-id="0ce74-122">Arrêtez le travail en sélectionnant **Arrêter**dans l’ensemble de commandes.</span><span class="sxs-lookup"><span data-stu-id="0ce74-122">Stop the job by selecting **Stop** in the set of commands.</span></span> 
5. <span data-ttu-id="0ce74-123">Modifiez les entrées, la requête et les sorties.</span><span class="sxs-lookup"><span data-stu-id="0ce74-123">Edit the inputs, query, and outputs.</span></span>
   
    <span data-ttu-id="0ce74-124">Une simple modification consiste à changer la requête pour la tâche **Règles** afin d’utiliser le signe **« < »** au lieu du signe **« > »**.</span><span class="sxs-lookup"><span data-stu-id="0ce74-124">A simple modification is to change the query for the **Rules** job to use a **"<"** instead of a **">"**.</span></span> <span data-ttu-id="0ce74-125">Le portail de solution affiche toujours **« > »** quand vous modifiez une règle, mais le comportement est inversé en raison de la modification du travail sous-jacent.</span><span class="sxs-lookup"><span data-stu-id="0ce74-125">The solution portal still shows **">"** when you edit a rule, but notice how the behavior is flipped due to the change in the underlying job.</span></span>
6. <span data-ttu-id="0ce74-126">Démarrage du travail</span><span class="sxs-lookup"><span data-stu-id="0ce74-126">Start the job</span></span>

> [!NOTE]
> <span data-ttu-id="0ce74-127">Le tableau de bord de surveillance à distance dépend de données spécifiques. Ainsi, modifier les tâches peut provoquer l’échec du tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="0ce74-127">The remote monitoring dashboard depends on specific data, so altering the jobs can cause the dashboard to fail.</span></span>

## <a name="add-your-own-rules"></a><span data-ttu-id="0ce74-128">Ajout de vos propres règles</span><span class="sxs-lookup"><span data-stu-id="0ce74-128">Add your own rules</span></span>

<span data-ttu-id="0ce74-129">En plus de modifier les tâches Azure Stream Analytics préconfigurées, vous pouvez utiliser le portail Azure pour ajouter de nouvelles tâches ou ajouter de nouvelles requêtes aux tâches existantes.</span><span class="sxs-lookup"><span data-stu-id="0ce74-129">In addition to changing the preconfigured Azure Stream Analytics jobs, you can use the Azure portal to add new jobs or add new queries to existing jobs.</span></span>

## <a name="customize-devices"></a><span data-ttu-id="0ce74-130">Personnalisation des appareils</span><span class="sxs-lookup"><span data-stu-id="0ce74-130">Customize devices</span></span>

<span data-ttu-id="0ce74-131">L’une des activités d’extension les plus courantes consiste à utiliser des appareils spécifiques à votre scénario.</span><span class="sxs-lookup"><span data-stu-id="0ce74-131">One of the most common extension activities is working with devices specific to your scenario.</span></span> <span data-ttu-id="0ce74-132">Il existe plusieurs méthodes pour travailler avec des appareils,</span><span class="sxs-lookup"><span data-stu-id="0ce74-132">There are several methods for working with devices.</span></span> <span data-ttu-id="0ce74-133">Notamment, la modification d’un appareil simulé pour qu’il corresponde à votre scénario ou l’utilisation du [Kit SDK d’appareils IoT][IoT Device SDK] pour connecter votre appareil physique à la solution.</span><span class="sxs-lookup"><span data-stu-id="0ce74-133">These methods include altering a simulated device to match your scenario, or using the [IoT Device SDK][IoT Device SDK] to connect your physical device to the solution.</span></span>

<span data-ttu-id="0ce74-134">Pour obtenir un guide étape par étape sur l’ajout d’appareils, consultez les articles sur la [connexion des appareils dans IoT Suite](iot-suite-connecting-devices.md) et [l’exemple de Kit de développement logiciel (SDK) C de surveillance à distance](https://github.com/Azure/azure-iot-sdk-c/tree/master/serializer/samples/remote_monitoring).</span><span class="sxs-lookup"><span data-stu-id="0ce74-134">For a step-by-step guide to adding devices, see the [Iot Suite Connecting Devices](iot-suite-connecting-devices.md) article and the [remote monitoring C SDK Sample](https://github.com/Azure/azure-iot-sdk-c/tree/master/serializer/samples/remote_monitoring).</span></span> <span data-ttu-id="0ce74-135">Ces appareils sont conçus pour fonctionner avec la solution préconfigurée de surveillance à distance.</span><span class="sxs-lookup"><span data-stu-id="0ce74-135">This sample is designed to work with the remote monitoring preconfigured solution.</span></span>

### <a name="create-your-own-simulated-device"></a><span data-ttu-id="0ce74-136">Création de votre propre appareil simulé</span><span class="sxs-lookup"><span data-stu-id="0ce74-136">Create your own simulated device</span></span>

<span data-ttu-id="0ce74-137">Le [code source de la solution de surveillance à distance](https://github.com/Azure/azure-iot-remote-monitoring) contient un simulateur .NET.</span><span class="sxs-lookup"><span data-stu-id="0ce74-137">Included in the [remote monitoring solution source code](https://github.com/Azure/azure-iot-remote-monitoring), is a .NET simulator.</span></span> <span data-ttu-id="0ce74-138">C’est lui qui est configuré dans le cadre de la solution et qui peut être modifié pour envoyer des données de télémétrie ou des métadonnées différentes, ou pour répondre à des commandes et méthodes différentes.</span><span class="sxs-lookup"><span data-stu-id="0ce74-138">This simulator is the one provisioned as part of the solution and you can alter it to send different metadata, telemetry, and respond to different commands and methods.</span></span>

<span data-ttu-id="0ce74-139">Le simulateur préconfiguré dans la solution préconfigurée de surveillance à distance simule un appareil de refroidissement qui émet des données de télémétrie de température et d’humidité.</span><span class="sxs-lookup"><span data-stu-id="0ce74-139">The preconfigured simulator in the remote monitoring preconfigured solution simulates a cooler device that emits temperature and humidity telemetry.</span></span> <span data-ttu-id="0ce74-140">Vous pouvez modifier le simulateur dans le projet [Simulator.WebJob](https://github.com/Azure/azure-iot-remote-monitoring/tree/master/Simulator/Simulator.WebJob) une fois le référentiel GitHub dupliqué.</span><span class="sxs-lookup"><span data-stu-id="0ce74-140">You can modify the simulator in the [Simulator.WebJob](https://github.com/Azure/azure-iot-remote-monitoring/tree/master/Simulator/Simulator.WebJob) project when you've forked the GitHub repository.</span></span>

### <a name="available-locations-for-simulated-devices"></a><span data-ttu-id="0ce74-141">Emplacements disponibles pour les appareils simulés</span><span class="sxs-lookup"><span data-stu-id="0ce74-141">Available locations for simulated devices</span></span>

<span data-ttu-id="0ce74-142">L’ensemble des emplacements par défaut se trouve à Seattle/Redmond, Washington, États-Unis.</span><span class="sxs-lookup"><span data-stu-id="0ce74-142">The default set of locations is in Seattle/Redmond, Washington, United States of America.</span></span> <span data-ttu-id="0ce74-143">Vous pouvez modifier ces emplacements dans [SampleDeviceFactory.cs][lnk-sample-device-factory].</span><span class="sxs-lookup"><span data-stu-id="0ce74-143">You can change these locations in [SampleDeviceFactory.cs][lnk-sample-device-factory].</span></span>

### <a name="add-a-desired-property-update-handler-to-the-simulator"></a><span data-ttu-id="0ce74-144">Ajout du gestionnaire de mise à jour des propriétés souhaitées au simulateur</span><span class="sxs-lookup"><span data-stu-id="0ce74-144">Add a desired property update handler to the simulator</span></span>

<span data-ttu-id="0ce74-145">Vous pouvez définir la valeur d’une propriété souhaitée pour un appareil dans le portail de solution.</span><span class="sxs-lookup"><span data-stu-id="0ce74-145">You can set a value for a desired property for a device in the solution portal.</span></span> <span data-ttu-id="0ce74-146">C’est l’appareil qui gère la demande de modification de propriété lorsqu’il récupère la valeur de propriété souhaitée.</span><span class="sxs-lookup"><span data-stu-id="0ce74-146">It is the responsibility of the device to handle the property change request when the device retrieves the desired property value.</span></span> <span data-ttu-id="0ce74-147">Pour ajouter la prise en charge d’une modification de valeur de propriété par une propriété souhaitée, vous devez ajouter un gestionnaire au simulateur.</span><span class="sxs-lookup"><span data-stu-id="0ce74-147">To add support for a property value change through a desired property, you need to add a handler to the simulator.</span></span>

<span data-ttu-id="0ce74-148">Le simulateur contient des gestionnaires pour les propriétés **SetPointTemp** et **TelemetryInterval** que vous pouvez mettre à jour en définissant les valeurs souhaitées dans le portail de solution.</span><span class="sxs-lookup"><span data-stu-id="0ce74-148">The simulator contains handlers for the **SetPointTemp** and **TelemetryInterval** properties that you can update by setting desired values in the solution portal.</span></span>

<span data-ttu-id="0ce74-149">L’exemple suivant montre le gestionnaire pour la propriété souhaitée **SetPointTemp** dans la classe **CoolerDevice** :</span><span class="sxs-lookup"><span data-stu-id="0ce74-149">The following example shows the handler for the **SetPointTemp** desired property in the **CoolerDevice** class:</span></span>

```csharp
protected async Task OnSetPointTempUpdate(object value)
{
    var telemetry = _telemetryController as ITelemetryWithSetPointTemperature;
    telemetry.SetPointTemperature = Convert.ToDouble(value);

    await SetReportedPropertyAsync(SetPointTempPropertyName, telemetry.SetPointTemperature);
}
```

<span data-ttu-id="0ce74-150">Cette méthode met à jour la température du point de télémétrie, puis signale la modification à IoT Hub en définissant une propriété signalée.</span><span class="sxs-lookup"><span data-stu-id="0ce74-150">This method updates the telemetry point temperature and then reports the change back to IoT Hub by setting a reported property.</span></span>

<span data-ttu-id="0ce74-151">Vous pouvez ajouter vos propres gestionnaires pour vos propres propriétés en suivant le modèle de l’exemple précédent.</span><span class="sxs-lookup"><span data-stu-id="0ce74-151">You can add your own handlers for your own properties by following the pattern in the preceding example.</span></span>

<span data-ttu-id="0ce74-152">Vous devez également lier la propriété souhaitée au gestionnaire comme indiqué dans l’exemple suivant issu du constructeur **CoolerDevice** :</span><span class="sxs-lookup"><span data-stu-id="0ce74-152">You must also bind the desired property to the handler as shown in the following example from the **CoolerDevice** constructor:</span></span>

```csharp
_desiredPropertyUpdateHandlers.Add(SetPointTempPropertyName, OnSetPointTempUpdate);
```

<span data-ttu-id="0ce74-153">Notez que **SetPointTempPropertyName** est une constante définie en tant que « Config.SetPointTemp ».</span><span class="sxs-lookup"><span data-stu-id="0ce74-153">Note that **SetPointTempPropertyName** is a constant defined as "Config.SetPointTemp".</span></span>

### <a name="add-support-for-a-new-method-to-the-simulator"></a><span data-ttu-id="0ce74-154">Ajout de la prise en charge d’une nouvelle méthode au simulateur</span><span class="sxs-lookup"><span data-stu-id="0ce74-154">Add support for a new method to the simulator</span></span>

<span data-ttu-id="0ce74-155">Vous pouvez personnaliser le simulateur pour ajouter la prise en charge d’une nouvelle [méthode (méthode directe)][lnk-direct-methods].</span><span class="sxs-lookup"><span data-stu-id="0ce74-155">You can customize the simulator to add support for a new [method (direct method)][lnk-direct-methods].</span></span> <span data-ttu-id="0ce74-156">Les deux principales étapes requises sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="0ce74-156">There are two key steps required:</span></span>

- <span data-ttu-id="0ce74-157">Le simulateur doit fournir à IoT hub des informations sur la méthode dans la solution préconfigurée.</span><span class="sxs-lookup"><span data-stu-id="0ce74-157">The simulator must notify the IoT hub in the preconfigured solution with details of the method.</span></span>
- <span data-ttu-id="0ce74-158">Le simulateur doit inclure le code pour gérer l’appel de méthode lorsque vous l’appelez à partir du volet **Informations sur l’appareil** dans l’Explorateur de solutions ou via un travail.</span><span class="sxs-lookup"><span data-stu-id="0ce74-158">The simulator must include code to handle the method call when you invoke it from the **Device details** panel in the solution explorer or through a job.</span></span>

<span data-ttu-id="0ce74-159">La solution préconfigurée de surveillance à distance utilise les *propriétés signalées* pour envoyer des informations sur les méthodes prises en charge à IoT hub.</span><span class="sxs-lookup"><span data-stu-id="0ce74-159">The remote monitoring preconfigured solution uses *reported properties* to send details of supported methods to IoT hub.</span></span> <span data-ttu-id="0ce74-160">Le serveur principal de solution gère une liste de toutes les méthodes prises en charge par chaque appareil, ainsi que l’historique des appels de méthode.</span><span class="sxs-lookup"><span data-stu-id="0ce74-160">The solution back end maintains a list of all the methods supported by each device along with a history of method invocations.</span></span> <span data-ttu-id="0ce74-161">Vous pouvez afficher ces informations sur les appareils et appeler des méthodes dans le portail de solution.</span><span class="sxs-lookup"><span data-stu-id="0ce74-161">You can view this information about devices and invoke methods in the solution portal.</span></span>

<span data-ttu-id="0ce74-162">Pour informer IoT Hub qu’un appareil prend en charge une méthode, l’appareil doit ajouter des informations sur la méthode au nœud **SupportedMethods** dans les propriétés signalées :</span><span class="sxs-lookup"><span data-stu-id="0ce74-162">To notify the IoT hub that a device supports a method, the device must add details of the method to the **SupportedMethods** node in the reported properties:</span></span>

```json
"SupportedMethods": {
  "<method signature>": "<method description>",
  "<method signature>": "<method description>"
}
```

<span data-ttu-id="0ce74-163">La signature de méthode a le format suivant : `<method name>--<parameter #0 name>-<parameter #1 type>-...-<parameter #n name>-<parameter #n type>`.</span><span class="sxs-lookup"><span data-stu-id="0ce74-163">The method signature has the following format: `<method name>--<parameter #0 name>-<parameter #1 type>-...-<parameter #n name>-<parameter #n type>`.</span></span> <span data-ttu-id="0ce74-164">Par exemple, pour spécifier que la méthode **InitiateFirmwareUpdate** attend un paramètre de chaîne nommé **FwPackageURI**, utilisez la signature de méthode suivante :</span><span class="sxs-lookup"><span data-stu-id="0ce74-164">For example, to specify the **InitiateFirmwareUpdate** method expects a string parameter named **FwPackageURI**, use the following method signature:</span></span>

```json
InitiateFirmwareUpate--FwPackageURI-string: "description of method"
```

<span data-ttu-id="0ce74-165">Pour obtenir la liste des types de paramètres pris en charge, consultez la classe **CommandTypes** dans le projet Infrastructure.</span><span class="sxs-lookup"><span data-stu-id="0ce74-165">For a list of supported parameter types, see the **CommandTypes** class in the Infrastructure project.</span></span>

<span data-ttu-id="0ce74-166">Pour supprimer une méthode, définissez la signature de méthode `null` dans les propriétés signalées.</span><span class="sxs-lookup"><span data-stu-id="0ce74-166">To delete a method, set the method signature to `null` in the reported properties.</span></span>

> [!NOTE]
> <span data-ttu-id="0ce74-167">Le serveur principal de solution met uniquement à jour les informations sur les méthodes prises en charge lorsqu’il reçoit un message *d’informations sur l’appareil* de la part de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="0ce74-167">The solution back end only updates information about supported methods when it receives a *device information* message from the device.</span></span>

<span data-ttu-id="0ce74-168">L’exemple de code suivant issu de la classe **SampleDeviceFactory** du projet Common montre comment ajouter une méthode à la liste des **SupportedMethods** dans les propriétés signalées envoyées par l’appareil :</span><span class="sxs-lookup"><span data-stu-id="0ce74-168">The following code sample from the **SampleDeviceFactory** class in the Common project shows how to add a method to the list of **SupportedMethods** in the reported properties sent by the device:</span></span>

```csharp
device.Commands.Add(new Command(
    "InitiateFirmwareUpdate",
    DeliveryType.Method,
    "Updates device Firmware. Use parameter 'FwPackageUri' to specifiy the URI of the firmware file, e.g. https://iotrmassets.blob.core.windows.net/firmwares/FW20.bin",
    new[] { new Parameter("FwPackageUri", "string") }
));
```

<span data-ttu-id="0ce74-169">Cet extrait de code ajoute les informations sur la méthode **InitiateFirmwareUpdate**, y compris le texte à afficher dans le portail de solution et les informations sur les paramètres de méthode requis.</span><span class="sxs-lookup"><span data-stu-id="0ce74-169">This code snippet adds details of the **InitiateFirmwareUpdate** method including text to display in the solution portal and details of the required method parameters.</span></span>

<span data-ttu-id="0ce74-170">Le simulateur envoie les propriétés signalées, y compris la liste des méthodes prises en charge, à IoT Hub au démarrage du simulateur.</span><span class="sxs-lookup"><span data-stu-id="0ce74-170">The simulator sends reported properties, including the list of supported methods, to IoT Hub when the simulator starts.</span></span>

<span data-ttu-id="0ce74-171">Ajoutez un gestionnaire au code du simulateur pour chaque méthode qu'il prend en charge.</span><span class="sxs-lookup"><span data-stu-id="0ce74-171">Add a handler to the simulator code for each method it supports.</span></span> <span data-ttu-id="0ce74-172">Vous pouvez voir les gestionnaires existants dans la classe **CoolerDevice** du projet Simulator.WebJob.</span><span class="sxs-lookup"><span data-stu-id="0ce74-172">You can see the existing handlers in the **CoolerDevice** class in the Simulator.WebJob project.</span></span> <span data-ttu-id="0ce74-173">L’exemple suivant montre le gestionnaire de la méthode **InitiateFirmwareUpdate** :</span><span class="sxs-lookup"><span data-stu-id="0ce74-173">The following example shows the handler for **InitiateFirmwareUpdate** method:</span></span>

```csharp
public async Task<MethodResponse> OnInitiateFirmwareUpdate(MethodRequest methodRequest, object userContext)
{
    if (_deviceManagementTask != null && !_deviceManagementTask.IsCompleted)
    {
        return await Task.FromResult(BuildMethodRespose(new
        {
            Message = "Device is busy"
        }, 409));
    }

    try
    {
        var operation = new FirmwareUpdate(methodRequest);
        _deviceManagementTask = operation.Run(Transport).ContinueWith(async task =>
        {
            // after firmware completed, we reset telemetry
            var telemetry = _telemetryController as ITelemetryWithTemperatureMeanValue;
            if (telemetry != null)
            {
                telemetry.TemperatureMeanValue = 34.5;
            }

            await UpdateReportedTemperatureMeanValue();
        });

        return await Task.FromResult(BuildMethodRespose(new
        {
            Message = "FirmwareUpdate accepted",
            Uri = operation.Uri
        }));
    }
    catch (Exception ex)
    {
        return await Task.FromResult(BuildMethodRespose(new
        {
            Message = ex.Message
        }, 400));
    }
}
```

<span data-ttu-id="0ce74-174">Les noms de gestionnaires de méthode doivent commencer par `On` suivi du nom de la méthode.</span><span class="sxs-lookup"><span data-stu-id="0ce74-174">Method handler names must start with `On` followed by the name of the method.</span></span> <span data-ttu-id="0ce74-175">Le paramètre **methodRequest** contient tous les paramètres transmis avec l’appel de méthode à partir du serveur principal de solution.</span><span class="sxs-lookup"><span data-stu-id="0ce74-175">The **methodRequest** parameter contains any parameters passed with the method invocation from the solution back end.</span></span> <span data-ttu-id="0ce74-176">La valeur de retour doit être de type **Task&lt;MethodResponse&gt;**.</span><span class="sxs-lookup"><span data-stu-id="0ce74-176">The return value must be of type **Task&lt;MethodResponse&gt;**.</span></span> <span data-ttu-id="0ce74-177">La méthode d’utilitaire **BuildMethodResponse** vous permet de créer la valeur de retour.</span><span class="sxs-lookup"><span data-stu-id="0ce74-177">The **BuildMethodResponse** utility method helps you create the return value.</span></span>

<span data-ttu-id="0ce74-178">Dans le gestionnaire de méthode, vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="0ce74-178">Inside the method handler, you could:</span></span>

- <span data-ttu-id="0ce74-179">Démarrer une tâche asynchrone.</span><span class="sxs-lookup"><span data-stu-id="0ce74-179">Start an asynchronous task.</span></span>
- <span data-ttu-id="0ce74-180">Récupérer les propriétés souhaitées depuis le *jumeau d’appareil* dans IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="0ce74-180">Retrieve desired properties from the *device twin* in IoT Hub.</span></span>
- <span data-ttu-id="0ce74-181">Mettre à jour une seule propriété signalée à l’aide de la méthode **SetReportedPropertyAsync** dans la classe **CoolerDevice**.</span><span class="sxs-lookup"><span data-stu-id="0ce74-181">Update a single reported property using the **SetReportedPropertyAsync** method in the **CoolerDevice** class.</span></span>
- <span data-ttu-id="0ce74-182">Mettre à jour plusieurs propriétés signalées en créant une instance **TwinCollection** et en appelant la méthode **Transport.UpdateReportedPropertiesAsync**.</span><span class="sxs-lookup"><span data-stu-id="0ce74-182">Update multiple reported properties by creating a **TwinCollection** instance and calling the **Transport.UpdateReportedPropertiesAsync** method.</span></span>

<span data-ttu-id="0ce74-183">L’exemple précédent de mise à jour du microprogramme effectue les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="0ce74-183">The preceding firmware update example performs the following steps:</span></span>

- <span data-ttu-id="0ce74-184">Vérifie que l’appareil est en mesure d’accepter la demande de mise à jour du microprogramme.</span><span class="sxs-lookup"><span data-stu-id="0ce74-184">Checks the device is able to accept the firmware update request.</span></span>
- <span data-ttu-id="0ce74-185">Lance l’opération de mise à jour du microprogramme de façon asynchrone et réinitialise les données de télémétrie lorsque l’opération est terminée.</span><span class="sxs-lookup"><span data-stu-id="0ce74-185">Asynchronously initiates the firmware update operation and resets the telemetry when the operation is complete.</span></span>
- <span data-ttu-id="0ce74-186">Retourne immédiatement le message « FirmwareUpdate accepted » (Mise à jour du microprogramme acceptée) pour indiquer que la demande a été acceptée par l’appareil.</span><span class="sxs-lookup"><span data-stu-id="0ce74-186">Immediately returns the "FirmwareUpdate accepted" message to indicate the request was accepted by the device.</span></span>

### <a name="build-and-use-your-own-physical-device"></a><span data-ttu-id="0ce74-187">Création et utilisation de votre propre appareil (physique)</span><span class="sxs-lookup"><span data-stu-id="0ce74-187">Build and use your own (physical) device</span></span>

<span data-ttu-id="0ce74-188">Les [Kits de développement logiciel (SDK) Azure IoT](https://github.com/Azure/azure-iot-sdks) fournissent des bibliothèques pour la connexion de nombreux types d’appareils (langages et systèmes d’exploitation) à des solutions IoT.</span><span class="sxs-lookup"><span data-stu-id="0ce74-188">The [Azure IoT SDKs](https://github.com/Azure/azure-iot-sdks) provide libraries for connecting numerous device types (languages and operating systems) into IoT solutions.</span></span>

## <a name="modify-dashboard-limits"></a><span data-ttu-id="0ce74-189">Modification des limites de tableau de bord</span><span class="sxs-lookup"><span data-stu-id="0ce74-189">Modify dashboard limits</span></span>

### <a name="number-of-devices-displayed-in-dashboard-dropdown"></a><span data-ttu-id="0ce74-190">Nombre d’appareils affichés dans la liste déroulante du tableau de bord</span><span class="sxs-lookup"><span data-stu-id="0ce74-190">Number of devices displayed in dashboard dropdown</span></span>

<span data-ttu-id="0ce74-191">Par défaut, la valeur est 200.</span><span class="sxs-lookup"><span data-stu-id="0ce74-191">The default is 200.</span></span> <span data-ttu-id="0ce74-192">Vous pouvez modifier cette valeur dans [DashboardController.cs][lnk-dashboard-controller].</span><span class="sxs-lookup"><span data-stu-id="0ce74-192">You can change this number in [DashboardController.cs][lnk-dashboard-controller].</span></span>

### <a name="number-of-pins-to-display-in-bing-map-control"></a><span data-ttu-id="0ce74-193">Nombre d’épingles à afficher dans le contrôle de carte Bing</span><span class="sxs-lookup"><span data-stu-id="0ce74-193">Number of pins to display in Bing Map control</span></span>

<span data-ttu-id="0ce74-194">Par défaut, la valeur est 200.</span><span class="sxs-lookup"><span data-stu-id="0ce74-194">The default is 200.</span></span> <span data-ttu-id="0ce74-195">Vous pouvez modifier cette valeur dans [TelemetryApiController.cs][lnk-telemetry-api-controller-01].</span><span class="sxs-lookup"><span data-stu-id="0ce74-195">You can change this number in [TelemetryApiController.cs][lnk-telemetry-api-controller-01].</span></span>

### <a name="time-period-of-telemetry-graph"></a><span data-ttu-id="0ce74-196">Période de temps du graphique de télémétrie</span><span class="sxs-lookup"><span data-stu-id="0ce74-196">Time period of telemetry graph</span></span>

<span data-ttu-id="0ce74-197">La valeur par défaut est 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="0ce74-197">The default is 10 minutes.</span></span> <span data-ttu-id="0ce74-198">Vous pouvez modifier cette valeur dans [TelemetryApiController.cs][lnk-telemetry-api-controller-02].</span><span class="sxs-lookup"><span data-stu-id="0ce74-198">You can change this value in [TelmetryApiController.cs][lnk-telemetry-api-controller-02].</span></span>

## <a name="manually-set-up-application-roles"></a><span data-ttu-id="0ce74-199">Configuration manuelle des rôles d’application</span><span class="sxs-lookup"><span data-stu-id="0ce74-199">Manually set up application roles</span></span>

<span data-ttu-id="0ce74-200">La procédure suivante décrit comment ajouter les rôles d’application **Admin** et **ReadOnly** à une solution préconfigurée.</span><span class="sxs-lookup"><span data-stu-id="0ce74-200">The following procedure describes how to add **Admin** and **ReadOnly** application roles to a preconfigured solution.</span></span> <span data-ttu-id="0ce74-201">Les solutions préconfigurées provisionnées à partir du site azureiotsuite.com incluent les rôles **Admin** et **ReadOnly**.</span><span class="sxs-lookup"><span data-stu-id="0ce74-201">Note that preconfigured solutions provisioned from the azureiotsuite.com site already include the **Admin** and **ReadOnly** roles.</span></span>

<span data-ttu-id="0ce74-202">Les membres du rôle **ReadOnly** peuvent afficher le tableau de bord et la liste des appareils, mais ils ne sont pas autorisés à ajouter des appareils, modifier les attributs de l’appareil ou envoyer des commandes.</span><span class="sxs-lookup"><span data-stu-id="0ce74-202">Members of the **ReadOnly** role can see the dashboard and the device list, but are not allowed to add devices, change device attributes, or send commands.</span></span>  <span data-ttu-id="0ce74-203">Les membres du rôle **Admin** ont un accès complet à toutes les fonctionnalités de la solution.</span><span class="sxs-lookup"><span data-stu-id="0ce74-203">Members of the **Admin** role have full access to all the functionality in the solution.</span></span>

1. <span data-ttu-id="0ce74-204">Connectez-vous au [Portail Azure Classic][lnk-classic-portal].</span><span class="sxs-lookup"><span data-stu-id="0ce74-204">Go to the [Azure classic portal][lnk-classic-portal].</span></span>
2. <span data-ttu-id="0ce74-205">Sélectionnez **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0ce74-205">Select **Active Directory**.</span></span>
3. <span data-ttu-id="0ce74-206">Cliquez sur le nom du client AAD que vous avez utilisé lorsque vous avez provisionné votre solution.</span><span class="sxs-lookup"><span data-stu-id="0ce74-206">Click the name of the AAD tenant you used when you provisioned your solution.</span></span>
4. <span data-ttu-id="0ce74-207">Cliquez sur **Applications**.</span><span class="sxs-lookup"><span data-stu-id="0ce74-207">Click **Applications**.</span></span>
5. <span data-ttu-id="0ce74-208">Cliquez sur le nom de l’application qui correspond au nom de votre solution préconfigurée.</span><span class="sxs-lookup"><span data-stu-id="0ce74-208">Click the name of the application that matches your preconfigured solution name.</span></span> <span data-ttu-id="0ce74-209">Si vous ne voyez pas votre application dans la liste, sélectionnez **Applications que ma société possède** dans le menu déroulant **Afficher** et cliquez sur la coche.</span><span class="sxs-lookup"><span data-stu-id="0ce74-209">If you don't see your application in the list, select **Applications my company owns** in the **Show** dropdown and click the check mark.</span></span>
6. <span data-ttu-id="0ce74-210">En bas de la page, cliquez sur **Gérer le manifeste** et **Télécharger le manifeste**.</span><span class="sxs-lookup"><span data-stu-id="0ce74-210">At the bottom of the page, click **Manage Manifest** and then **Download Manifest**.</span></span>
7. <span data-ttu-id="0ce74-211">Cette procédure télécharge un fichier .json sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="0ce74-211">This procedure downloads a .json file to your local machine.</span></span> <span data-ttu-id="0ce74-212">Ouvrez ce fichier pour le modifier dans un éditeur de texte de votre choix.</span><span class="sxs-lookup"><span data-stu-id="0ce74-212">Open this file for editing in a text editor of your choice.</span></span>
8. <span data-ttu-id="0ce74-213">Sur la troisième ligne du fichier .json, vous trouverez :</span><span class="sxs-lookup"><span data-stu-id="0ce74-213">On the third line of the .json file, you can see:</span></span>

   ```json
   "appRoles" : [],
   ```
   <span data-ttu-id="0ce74-214">Remplacez cette ligne par le code suivant :</span><span class="sxs-lookup"><span data-stu-id="0ce74-214">Replace this line with the following code:</span></span>

   ```json
   "appRoles": [
   {
   "allowedMemberTypes": [
   "User"
   ],
   "description": "Administrator access to the application",
   "displayName": "Admin",
   "id": "a400a00b-f67c-42b7-ba9a-f73d8c67e433",
   "isEnabled": true,
   "value": "Admin"
   },
   {
   "allowedMemberTypes": [
   "User"
   ],
   "description": "Read only access to device information",
   "displayName": "Read Only",
   "id": "e5bbd0f5-128e-4362-9dd1-8f253c6082d7",
   "isEnabled": true,
   "value": "ReadOnly"
   } ],
   ```

9. <span data-ttu-id="0ce74-215">Enregistrez le fichier .json mis à jour (vous pouvez remplacer le fichier existant).</span><span class="sxs-lookup"><span data-stu-id="0ce74-215">Save the updated .json file (you can overwrite the existing file).</span></span>
10. <span data-ttu-id="0ce74-216">Au bas de la page du portail Azure Classic, sélectionnez **Gérer le manifeste**, puis **Télécharger le manifeste** pour télécharger le fichier .json que vous avez enregistré à l’étape précédente.</span><span class="sxs-lookup"><span data-stu-id="0ce74-216">In the Azure classic portal, at the bottom of the page, select **Manage Manifest** then **Upload Manifest** to upload the .json file you saved in the previous step.</span></span>
11. <span data-ttu-id="0ce74-217">Vous avez maintenant ajouté les rôles **Admin** et **ReadOnly** à votre application.</span><span class="sxs-lookup"><span data-stu-id="0ce74-217">You have now added the **Admin** and **ReadOnly** roles to your application.</span></span>
12. <span data-ttu-id="0ce74-218">Pour affecter un de ces rôles à un utilisateur de votre répertoire, consultez [Autorisations sur le site azureiotsuite.com][lnk-permissions].</span><span class="sxs-lookup"><span data-stu-id="0ce74-218">To assign one of these roles to a user in your directory, see [Permissions on the azureiotsuite.com site][lnk-permissions].</span></span>

## <a name="feedback"></a><span data-ttu-id="0ce74-219">Commentaires</span><span class="sxs-lookup"><span data-stu-id="0ce74-219">Feedback</span></span>

<span data-ttu-id="0ce74-220">Vous avez une personnalisation que vous aimeriez voir couverte dans ce document ?</span><span class="sxs-lookup"><span data-stu-id="0ce74-220">Do you have a customization you'd like to see covered in this document?</span></span> <span data-ttu-id="0ce74-221">Ajoutez des suggestions de fonctionnalités à [User Voice](https://feedback.azure.com/forums/321918-azure-iot) ou commentez cet article.</span><span class="sxs-lookup"><span data-stu-id="0ce74-221">Add feature suggestions to [User Voice](https://feedback.azure.com/forums/321918-azure-iot), or comment on this article.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="0ce74-222">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0ce74-222">Next steps</span></span>

<span data-ttu-id="0ce74-223">Pour en savoir plus sur les options permettant de personnaliser les solutions préconfigurées, consultez :</span><span class="sxs-lookup"><span data-stu-id="0ce74-223">To learn more about the options for customizing the preconfigured solutions, see:</span></span>

* <span data-ttu-id="0ce74-224">[Connecter Logic App à la solution préconfigurée de surveillance à distance Azure IoT Suite][lnk-logicapp]</span><span class="sxs-lookup"><span data-stu-id="0ce74-224">[Connect Logic App to your Azure IoT Suite Remote Monitoring preconfigured solution][lnk-logicapp]</span></span>
* <span data-ttu-id="0ce74-225">[Utilisation de la télémétrie dynamique avec la solution préconfigurée de surveillance à distance][lnk-dynamic]</span><span class="sxs-lookup"><span data-stu-id="0ce74-225">[Use dynamic telemetry with the remote monitoring preconfigured solution][lnk-dynamic]</span></span>
* <span data-ttu-id="0ce74-226">[Métadonnées relatives aux informations d’appareil dans la solution préconfigurée de surveillance à distance][lnk-devinfo]</span><span class="sxs-lookup"><span data-stu-id="0ce74-226">[Device information metadata in the remote monitoring preconfigured solution][lnk-devinfo]</span></span>
* <span data-ttu-id="0ce74-227">[Personnaliser comment la solution à usine connectée présente les données à partir de vos serveurs OPC UA][lnk-cf-customize]</span><span class="sxs-lookup"><span data-stu-id="0ce74-227">[Customize how the connected factory solution displays data from your OPC UA servers][lnk-cf-customize]</span></span>

[lnk-logicapp]: iot-suite-logic-apps-tutorial.md
[lnk-dynamic]: iot-suite-dynamic-telemetry.md
[lnk-devinfo]: iot-suite-remote-monitoring-device-info.md

[IoT Device SDK]: https://azure.microsoft.com/documentation/articles/iot-hub-sdks-summary/
[lnk-permissions]: iot-suite-permissions.md
[lnk-dashboard-controller]: https://github.com/Azure/azure-iot-remote-monitoring/blob/3fd43b8a9f7e0f2774d73f3569439063705cebe4/DeviceAdministration/Web/Controllers/DashboardController.cs#L27
[lnk-telemetry-api-controller-01]: https://github.com/Azure/azure-iot-remote-monitoring/blob/3fd43b8a9f7e0f2774d73f3569439063705cebe4/DeviceAdministration/Web/WebApiControllers/TelemetryApiController.cs#L27
[lnk-telemetry-api-controller-02]: https://github.com/Azure/azure-iot-remote-monitoring/blob/e7003339f73e21d3930f71ceba1e74fb5c0d9ea0/DeviceAdministration/Web/WebApiControllers/TelemetryApiController.cs#L25 
[lnk-sample-device-factory]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Common/Factory/SampleDeviceFactory.cs#L40
[lnk-classic-portal]: https://manage.windowsazure.com
[lnk-direct-methods]: ../iot-hub/iot-hub-devguide-direct-methods.md
[lnk-cf-customize]: iot-suite-connected-factory-customize.md