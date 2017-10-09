---
title: "aaaCustomizing préconfiguré solutions | Documents Microsoft"
description: "Explique comment toocustomize hello Azure IoT Suite préconfiguré solutions."
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
ms.openlocfilehash: 1a8573f5ac6ed944c44459df495446f15174d513
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="customize-a-preconfigured-solution"></a><span data-ttu-id="a3de3-103">Personnaliser une solution préconfigurée</span><span class="sxs-lookup"><span data-stu-id="a3de3-103">Customize a preconfigured solution</span></span>

<span data-ttu-id="a3de3-104">solutions de Hello préconfiguré fournies avec hello Azure IoT Suite illustrent les services de hello dans hello suite travailler ensemble toodeliver une solution de bout en bout.</span><span class="sxs-lookup"><span data-stu-id="a3de3-104">hello preconfigured solutions provided with hello Azure IoT Suite demonstrate hello services within hello suite working together toodeliver an end-to-end solution.</span></span> <span data-ttu-id="a3de3-105">À partir de ce point de départ, il existe divers emplacements dans lesquels vous pouvez étendre et personnaliser des solutions hello pour des scénarios spécifiques.</span><span class="sxs-lookup"><span data-stu-id="a3de3-105">From this starting point, there are various places in which you can extend and customize hello solution for specific scenarios.</span></span> <span data-ttu-id="a3de3-106">Hello les sections suivantes décrire ces points de personnalisation courantes.</span><span class="sxs-lookup"><span data-stu-id="a3de3-106">hello following sections describe these common customization points.</span></span>

## <a name="find-hello-source-code"></a><span data-ttu-id="a3de3-107">Rechercher du code source de hello</span><span class="sxs-lookup"><span data-stu-id="a3de3-107">Find hello source code</span></span>

<span data-ttu-id="a3de3-108">code source de Hello pour les solutions hello préconfiguré est disponible sur GitHub Bonjour suivant référentiels :</span><span class="sxs-lookup"><span data-stu-id="a3de3-108">hello source code for hello preconfigured solutions is available on GitHub in hello following repositories:</span></span>

* <span data-ttu-id="a3de3-109">Surveillance à distance : [https://www.github.com/Azure/azure-iot-remote-monitoring](https://github.com/Azure/azure-iot-remote-monitoring)</span><span class="sxs-lookup"><span data-stu-id="a3de3-109">Remote Monitoring: [https://www.github.com/Azure/azure-iot-remote-monitoring](https://github.com/Azure/azure-iot-remote-monitoring)</span></span>
* <span data-ttu-id="a3de3-110">Maintenance prédictive : [https://github.com/Azure/azure-iot-predictive-maintenance](https://github.com/Azure/azure-iot-predictive-maintenance)</span><span class="sxs-lookup"><span data-stu-id="a3de3-110">Predictive Maintenance: [https://github.com/Azure/azure-iot-predictive-maintenance](https://github.com/Azure/azure-iot-predictive-maintenance)</span></span>
* <span data-ttu-id="a3de3-111">Usine connectée : [https://github.com/Azure/azure-iot-connected-factory](https://github.com/Azure/azure-iot-connected-factory)</span><span class="sxs-lookup"><span data-stu-id="a3de3-111">Connected factory: [https://github.com/Azure/azure-iot-connected-factory](https://github.com/Azure/azure-iot-connected-factory)</span></span>

<span data-ttu-id="a3de3-112">code source de Hello pour les solutions hello préconfiguré est fournie pratiques et les modèles de hello toodemonstrate aux fonctionnalités de bout en bout hello tooimplement d’une solution IoT à l’aide d’Azure IoT Suite utilisées.</span><span class="sxs-lookup"><span data-stu-id="a3de3-112">hello source code for hello preconfigured solutions is provided toodemonstrate hello patterns and practices used tooimplement hello end-to-end functionality of an IoT solution using Azure IoT Suite.</span></span> <span data-ttu-id="a3de3-113">Vous trouverez plus d’informations sur la façon toobuild et déployer des solutions hello dans des référentiels GitHub hello.</span><span class="sxs-lookup"><span data-stu-id="a3de3-113">You can find more information about how toobuild and deploy hello solutions in hello GitHub repositories.</span></span>

## <a name="change-hello-preconfigured-rules"></a><span data-ttu-id="a3de3-114">Modifier les règles de hello préconfiguré</span><span class="sxs-lookup"><span data-stu-id="a3de3-114">Change hello preconfigured rules</span></span>

<span data-ttu-id="a3de3-115">Hello solution d’analyse à distance inclut trois [Analytique de flux de données Azure](https://azure.microsoft.com/services/stream-analytics/) travaux toohandle les informations de périphérique, la télémétrie et logique des règles dans les solutions hello.</span><span class="sxs-lookup"><span data-stu-id="a3de3-115">hello remote monitoring solution includes three [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/) jobs toohandle device information, telemetry, and rules logic in hello solution.</span></span>

<span data-ttu-id="a3de3-116">Hello trois flux de travaux de l’analytique et leur syntaxe sont décrites en détail dans hello [surveillance à distance préconfiguré procédure pas à pas de solution](iot-suite-remote-monitoring-sample-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="a3de3-116">hello three stream analytics jobs and their syntax are described in depth in hello [Remote monitoring preconfigured solution walkthrough](iot-suite-remote-monitoring-sample-walkthrough.md).</span></span> 

<span data-ttu-id="a3de3-117">Vous pouvez modifier ces travaux directement tooalter hello logique, ou ajouter une logique spécifique tooyour scénario.</span><span class="sxs-lookup"><span data-stu-id="a3de3-117">You can edit these jobs directly tooalter hello logic, or add logic specific tooyour scenario.</span></span> <span data-ttu-id="a3de3-118">Vous pouvez trouver hello les tâches de flux de données Analytique comme suit :</span><span class="sxs-lookup"><span data-stu-id="a3de3-118">You can find hello Stream Analytics jobs as follows:</span></span>

1. <span data-ttu-id="a3de3-119">Accédez trop[portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a3de3-119">Go too[Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="a3de3-120">Recherchez le groupe de ressources toohello avec le même nom que votre solution IoT de hello.</span><span class="sxs-lookup"><span data-stu-id="a3de3-120">Navigate toohello resource group with hello same name as your IoT solution.</span></span> 
3. <span data-ttu-id="a3de3-121">Sélectionnez hello Analytique de flux de données Azure tâche toomodify.</span><span class="sxs-lookup"><span data-stu-id="a3de3-121">Select hello Azure Stream Analytics job you'd like toomodify.</span></span> 
4. <span data-ttu-id="a3de3-122">Tâche d’arrêt de hello en sélectionnant **arrêter** dans l’ensemble de hello de commandes.</span><span class="sxs-lookup"><span data-stu-id="a3de3-122">Stop hello job by selecting **Stop** in hello set of commands.</span></span> 
5. <span data-ttu-id="a3de3-123">Modifier les sorties, les requêtes et les entrées de hello.</span><span class="sxs-lookup"><span data-stu-id="a3de3-123">Edit hello inputs, query, and outputs.</span></span>
   
    <span data-ttu-id="a3de3-124">Une simple modification est la requête de hello toochange pour hello **règles** travail toouse un **« < »** au lieu d’un **» > «**.</span><span class="sxs-lookup"><span data-stu-id="a3de3-124">A simple modification is toochange hello query for hello **Rules** job toouse a **"<"** instead of a **">"**.</span></span> <span data-ttu-id="a3de3-125">portail de solution Hello affiche toujours **» > «** lorsque vous modifiez une règle, mais notez comment le comportement de hello est retournée en raison de modifications toohello Bonjour sous-jacent du travail.</span><span class="sxs-lookup"><span data-stu-id="a3de3-125">hello solution portal still shows **">"** when you edit a rule, but notice how hello behavior is flipped due toohello change in hello underlying job.</span></span>
6. <span data-ttu-id="a3de3-126">Démarrer le travail de hello</span><span class="sxs-lookup"><span data-stu-id="a3de3-126">Start hello job</span></span>

> [!NOTE]
> <span data-ttu-id="a3de3-127">tableau de bord analyse Hello à distance dépend des données spécifiques, toute modification des travaux de hello peut causer toofail du tableau de bord hello.</span><span class="sxs-lookup"><span data-stu-id="a3de3-127">hello remote monitoring dashboard depends on specific data, so altering hello jobs can cause hello dashboard toofail.</span></span>

## <a name="add-your-own-rules"></a><span data-ttu-id="a3de3-128">Ajout de vos propres règles</span><span class="sxs-lookup"><span data-stu-id="a3de3-128">Add your own rules</span></span>

<span data-ttu-id="a3de3-129">En outre toochanging hello préconfiguré les travaux de l’Analytique des flux de données Azure, vous pouvez utiliser les nouveaux travaux de hello tooadd portail Azure ou ajouter de nouveaux travaux de tooexisting de requêtes.</span><span class="sxs-lookup"><span data-stu-id="a3de3-129">In addition toochanging hello preconfigured Azure Stream Analytics jobs, you can use hello Azure portal tooadd new jobs or add new queries tooexisting jobs.</span></span>

## <a name="customize-devices"></a><span data-ttu-id="a3de3-130">Personnalisation des appareils</span><span class="sxs-lookup"><span data-stu-id="a3de3-130">Customize devices</span></span>

<span data-ttu-id="a3de3-131">Une des activités extension les plus courantes hello travaille avec un scénario tooyour spécifique de périphériques.</span><span class="sxs-lookup"><span data-stu-id="a3de3-131">One of hello most common extension activities is working with devices specific tooyour scenario.</span></span> <span data-ttu-id="a3de3-132">Il existe plusieurs méthodes pour travailler avec des appareils,</span><span class="sxs-lookup"><span data-stu-id="a3de3-132">There are several methods for working with devices.</span></span> <span data-ttu-id="a3de3-133">Ces méthodes incluent la modification d’un toomatch appareil simulé votre scénario ou à l’aide de hello [IoT appareil SDK] [ IoT Device SDK] tooconnect votre solution de toohello périphérique physique.</span><span class="sxs-lookup"><span data-stu-id="a3de3-133">These methods include altering a simulated device toomatch your scenario, or using hello [IoT Device SDK][IoT Device SDK] tooconnect your physical device toohello solution.</span></span>

<span data-ttu-id="a3de3-134">Pour une unité de tooadding guide pas à pas, consultez hello [Iot Suite connexion appareils](iot-suite-connecting-devices.md) article et hello [exemple du Kit de développement logiciel C de surveillance à distance](https://github.com/Azure/azure-iot-sdk-c/tree/master/serializer/samples/remote_monitoring).</span><span class="sxs-lookup"><span data-stu-id="a3de3-134">For a step-by-step guide tooadding devices, see hello [Iot Suite Connecting Devices](iot-suite-connecting-devices.md) article and hello [remote monitoring C SDK Sample](https://github.com/Azure/azure-iot-sdk-c/tree/master/serializer/samples/remote_monitoring).</span></span> <span data-ttu-id="a3de3-135">Cet exemple est conçu toowork avec hello solution préconfigurée de surveillance à distance.</span><span class="sxs-lookup"><span data-stu-id="a3de3-135">This sample is designed toowork with hello remote monitoring preconfigured solution.</span></span>

### <a name="create-your-own-simulated-device"></a><span data-ttu-id="a3de3-136">Création de votre propre appareil simulé</span><span class="sxs-lookup"><span data-stu-id="a3de3-136">Create your own simulated device</span></span>

<span data-ttu-id="a3de3-137">Inclus dans hello [code source de la solution de surveillance à distance](https://github.com/Azure/azure-iot-remote-monitoring), est un simulateur .NET.</span><span class="sxs-lookup"><span data-stu-id="a3de3-137">Included in hello [remote monitoring solution source code](https://github.com/Azure/azure-iot-remote-monitoring), is a .NET simulator.</span></span> <span data-ttu-id="a3de3-138">Ce simulateur est hello une configuré comme partie de la solution de hello et que vous pouvez modifier toosend différentes métadonnées, données de télémétrie et répondre de méthodes et les commandes de toodifferent.</span><span class="sxs-lookup"><span data-stu-id="a3de3-138">This simulator is hello one provisioned as part of hello solution and you can alter it toosend different metadata, telemetry, and respond toodifferent commands and methods.</span></span>

<span data-ttu-id="a3de3-139">Simulateur préconfigurées de Hello Bonjour solution préconfigurée de surveillance à distance simule un périphérique de refroidissement qui émet les données de télémétrie température et humidité.</span><span class="sxs-lookup"><span data-stu-id="a3de3-139">hello preconfigured simulator in hello remote monitoring preconfigured solution simulates a cooler device that emits temperature and humidity telemetry.</span></span> <span data-ttu-id="a3de3-140">Vous pouvez modifier le simulateur hello Bonjour [Simulator.WebJob](https://github.com/Azure/azure-iot-remote-monitoring/tree/master/Simulator/Simulator.WebJob) projeter le moment où vous avez dupliquée référentiel GitHub de hello.</span><span class="sxs-lookup"><span data-stu-id="a3de3-140">You can modify hello simulator in hello [Simulator.WebJob](https://github.com/Azure/azure-iot-remote-monitoring/tree/master/Simulator/Simulator.WebJob) project when you've forked hello GitHub repository.</span></span>

### <a name="available-locations-for-simulated-devices"></a><span data-ttu-id="a3de3-141">Emplacements disponibles pour les appareils simulés</span><span class="sxs-lookup"><span data-stu-id="a3de3-141">Available locations for simulated devices</span></span>

<span data-ttu-id="a3de3-142">ensemble des emplacements par défaut de Hello est en Seattle Way, Redmond, Washington, États-Unis d’Amérique.</span><span class="sxs-lookup"><span data-stu-id="a3de3-142">hello default set of locations is in Seattle/Redmond, Washington, United States of America.</span></span> <span data-ttu-id="a3de3-143">Vous pouvez modifier ces emplacements dans [SampleDeviceFactory.cs][lnk-sample-device-factory].</span><span class="sxs-lookup"><span data-stu-id="a3de3-143">You can change these locations in [SampleDeviceFactory.cs][lnk-sample-device-factory].</span></span>

### <a name="add-a-desired-property-update-handler-toohello-simulator"></a><span data-ttu-id="a3de3-144">Ajouter un simulateur de toohello Gestionnaire de propriétés souhaitées mise à jour</span><span class="sxs-lookup"><span data-stu-id="a3de3-144">Add a desired property update handler toohello simulator</span></span>

<span data-ttu-id="a3de3-145">Vous pouvez définir une valeur pour une propriété spécifique pour un périphérique dans le portail de solution hello.</span><span class="sxs-lookup"><span data-stu-id="a3de3-145">You can set a value for a desired property for a device in hello solution portal.</span></span> <span data-ttu-id="a3de3-146">Il incombe hello de demande de modification de propriété hello appareil toohandle hello lors de l’appareil de hello récupère la valeur de propriété de hello souhaité.</span><span class="sxs-lookup"><span data-stu-id="a3de3-146">It is hello responsibility of hello device toohandle hello property change request when hello device retrieves hello desired property value.</span></span> <span data-ttu-id="a3de3-147">prise en charge de tooadd pour une modification de valeur de propriété via une propriété de votre choix, vous devez tooadd un simulateur toohello de gestionnaire.</span><span class="sxs-lookup"><span data-stu-id="a3de3-147">tooadd support for a property value change through a desired property, you need tooadd a handler toohello simulator.</span></span>

<span data-ttu-id="a3de3-148">Simulateur de Hello contient des gestionnaires pour hello **SetPointTemp** et **TelemetryInterval** propriétés que vous pouvez mettre à jour en définissant souhaitée des valeurs dans le portail de solution hello.</span><span class="sxs-lookup"><span data-stu-id="a3de3-148">hello simulator contains handlers for hello **SetPointTemp** and **TelemetryInterval** properties that you can update by setting desired values in hello solution portal.</span></span>

<span data-ttu-id="a3de3-149">exemple Hello présente Gestionnaire hello pour hello **SetPointTemp** souhaité propriété Bonjour **CoolerDevice** classe :</span><span class="sxs-lookup"><span data-stu-id="a3de3-149">hello following example shows hello handler for hello **SetPointTemp** desired property in hello **CoolerDevice** class:</span></span>

```csharp
protected async Task OnSetPointTempUpdate(object value)
{
    var telemetry = _telemetryController as ITelemetryWithSetPointTemperature;
    telemetry.SetPointTemperature = Convert.ToDouble(value);

    await SetReportedPropertyAsync(SetPointTempPropertyName, telemetry.SetPointTemperature);
}
```

<span data-ttu-id="a3de3-150">Cette méthode met à jour le point de données de télémétrie hello température hello de rapports change différé tooIoT Hub en définissant une propriété signalée.</span><span class="sxs-lookup"><span data-stu-id="a3de3-150">This method updates hello telemetry point temperature and then reports hello change back tooIoT Hub by setting a reported property.</span></span>

<span data-ttu-id="a3de3-151">Vous pouvez ajouter vos propres gestionnaires pour vos propres propriétés en suivant le modèle hello Bonjour précédent exemple.</span><span class="sxs-lookup"><span data-stu-id="a3de3-151">You can add your own handlers for your own properties by following hello pattern in hello preceding example.</span></span>

<span data-ttu-id="a3de3-152">Vous devez également lier Gestionnaire de toohello hello propriété souhaitée comme indiqué dans hello hello de l’exemple suivant **CoolerDevice** constructeur :</span><span class="sxs-lookup"><span data-stu-id="a3de3-152">You must also bind hello desired property toohello handler as shown in hello following example from hello **CoolerDevice** constructor:</span></span>

```csharp
_desiredPropertyUpdateHandlers.Add(SetPointTempPropertyName, OnSetPointTempUpdate);
```

<span data-ttu-id="a3de3-153">Notez que **SetPointTempPropertyName** est une constante définie en tant que « Config.SetPointTemp ».</span><span class="sxs-lookup"><span data-stu-id="a3de3-153">Note that **SetPointTempPropertyName** is a constant defined as "Config.SetPointTemp".</span></span>

### <a name="add-support-for-a-new-method-toohello-simulator"></a><span data-ttu-id="a3de3-154">Ajouter la prise en charge pour un nouveau simulateur de toohello (méthode)</span><span class="sxs-lookup"><span data-stu-id="a3de3-154">Add support for a new method toohello simulator</span></span>

<span data-ttu-id="a3de3-155">Vous pouvez personnaliser hello simulateur tooadd prise en charge pour un nouveau [(méthode) (méthode directe)][lnk-direct-methods].</span><span class="sxs-lookup"><span data-stu-id="a3de3-155">You can customize hello simulator tooadd support for a new [method (direct method)][lnk-direct-methods].</span></span> <span data-ttu-id="a3de3-156">Les deux principales étapes requises sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="a3de3-156">There are two key steps required:</span></span>

- <span data-ttu-id="a3de3-157">Simulateur de Hello doit le signaler hello IoT hub dans solution hello préconfiguré avec les détails de la méthode hello.</span><span class="sxs-lookup"><span data-stu-id="a3de3-157">hello simulator must notify hello IoT hub in hello preconfigured solution with details of hello method.</span></span>
- <span data-ttu-id="a3de3-158">Simulateur de Hello doit inclure l’appel de méthode de code toohandle hello lorsque vous l’appelez à partir de hello **détails de l’appareil** Panneau de configuration dans l’Explorateur de solutions hello ou via un travail.</span><span class="sxs-lookup"><span data-stu-id="a3de3-158">hello simulator must include code toohandle hello method call when you invoke it from hello **Device details** panel in hello solution explorer or through a job.</span></span>

<span data-ttu-id="a3de3-159">Hello surveillance à distance préconfiguré solution utilise *signalé propriétés* toosend les détails du concentrateur de tooIoT méthodes prises en charge.</span><span class="sxs-lookup"><span data-stu-id="a3de3-159">hello remote monitoring preconfigured solution uses *reported properties* toosend details of supported methods tooIoT hub.</span></span> <span data-ttu-id="a3de3-160">Hello solution back-end conserve une liste de toutes les méthodes hello pris en charge par chaque périphérique, ainsi que l’historique des appels de méthode.</span><span class="sxs-lookup"><span data-stu-id="a3de3-160">hello solution back end maintains a list of all hello methods supported by each device along with a history of method invocations.</span></span> <span data-ttu-id="a3de3-161">Vous pouvez afficher ces informations sur les périphériques et appeler des méthodes dans le portail de solution hello.</span><span class="sxs-lookup"><span data-stu-id="a3de3-161">You can view this information about devices and invoke methods in hello solution portal.</span></span>

<span data-ttu-id="a3de3-162">toonotify hello IoT hub qu’un périphérique prend en charge une méthode, les appareils hello doivent ajouter les détails de hello méthode toohello **SupportedMethods** nœud Bonjour signalé propriétés :</span><span class="sxs-lookup"><span data-stu-id="a3de3-162">toonotify hello IoT hub that a device supports a method, hello device must add details of hello method toohello **SupportedMethods** node in hello reported properties:</span></span>

```json
"SupportedMethods": {
  "<method signature>": "<method description>",
  "<method signature>": "<method description>"
}
```

<span data-ttu-id="a3de3-163">signature de méthode Hello a hello suivant le format : `<method name>--<parameter #0 name>-<parameter #1 type>-...-<parameter #n name>-<parameter #n type>`.</span><span class="sxs-lookup"><span data-stu-id="a3de3-163">hello method signature has hello following format: `<method name>--<parameter #0 name>-<parameter #1 type>-...-<parameter #n name>-<parameter #n type>`.</span></span> <span data-ttu-id="a3de3-164">Par exemple, toospecify hello **InitiateFirmwareUpdate** méthode attend un paramètre de chaîne nommé **FwPackageURI**, utilisez hello après la signature de méthode :</span><span class="sxs-lookup"><span data-stu-id="a3de3-164">For example, toospecify hello **InitiateFirmwareUpdate** method expects a string parameter named **FwPackageURI**, use hello following method signature:</span></span>

```json
InitiateFirmwareUpate--FwPackageURI-string: "description of method"
```

<span data-ttu-id="a3de3-165">Pour obtenir la liste des types de paramètres pris en charge, consultez hello **CommandTypes** classe dans le projet d’Infrastructure hello.</span><span class="sxs-lookup"><span data-stu-id="a3de3-165">For a list of supported parameter types, see hello **CommandTypes** class in hello Infrastructure project.</span></span>

<span data-ttu-id="a3de3-166">toodelete une méthode, définissez trop de signature de méthode hello`null` Bonjour signalé propriétés.</span><span class="sxs-lookup"><span data-stu-id="a3de3-166">toodelete a method, set hello method signature too`null` in hello reported properties.</span></span>

> [!NOTE]
> <span data-ttu-id="a3de3-167">Hello back-end solution met à jour uniquement les informations sur les méthodes prises en charge lorsqu’il reçoit un *les informations de périphérique* message à partir de l’appareil de hello.</span><span class="sxs-lookup"><span data-stu-id="a3de3-167">hello solution back end only updates information about supported methods when it receives a *device information* message from hello device.</span></span>

<span data-ttu-id="a3de3-168">Hello suivant l’exemple de code à partir de hello **SampleDeviceFactory** classe Bonjour commun projet montre comment tooadd liste méthode toohello de **SupportedMethods** Bonjour signalé propriétés envoyées par hello périphérique :</span><span class="sxs-lookup"><span data-stu-id="a3de3-168">hello following code sample from hello **SampleDeviceFactory** class in hello Common project shows how tooadd a method toohello list of **SupportedMethods** in hello reported properties sent by hello device:</span></span>

```csharp
device.Commands.Add(new Command(
    "InitiateFirmwareUpdate",
    DeliveryType.Method,
    "Updates device Firmware. Use parameter 'FwPackageUri' toospecifiy hello URI of hello firmware file, e.g. https://iotrmassets.blob.core.windows.net/firmwares/FW20.bin",
    new[] { new Parameter("FwPackageUri", "string") }
));
```

<span data-ttu-id="a3de3-169">Cet extrait de code ajoute les détails de hello **InitiateFirmwareUpdate** méthode notamment toodisplay de texte dans le portail de solution hello et les détails de hello nécessaire les paramètres de méthode.</span><span class="sxs-lookup"><span data-stu-id="a3de3-169">This code snippet adds details of hello **InitiateFirmwareUpdate** method including text toodisplay in hello solution portal and details of hello required method parameters.</span></span>

<span data-ttu-id="a3de3-170">Simulateur de Hello envoie des propriétés déclarées, y compris la liste hello des méthodes prises en charge, tooIoT Hub au démarrage du simulateur de hello.</span><span class="sxs-lookup"><span data-stu-id="a3de3-170">hello simulator sends reported properties, including hello list of supported methods, tooIoT Hub when hello simulator starts.</span></span>

<span data-ttu-id="a3de3-171">Ajouter un code de simulateur Gestionnaire toohello pour chaque méthode, qu'il prend en charge.</span><span class="sxs-lookup"><span data-stu-id="a3de3-171">Add a handler toohello simulator code for each method it supports.</span></span> <span data-ttu-id="a3de3-172">Vous pouvez voir les gestionnaires existants de hello Bonjour **CoolerDevice** classe dans le projet de Simulator.WebJob hello.</span><span class="sxs-lookup"><span data-stu-id="a3de3-172">You can see hello existing handlers in hello **CoolerDevice** class in hello Simulator.WebJob project.</span></span> <span data-ttu-id="a3de3-173">exemple Hello présente Gestionnaire hello pour **InitiateFirmwareUpdate** méthode :</span><span class="sxs-lookup"><span data-stu-id="a3de3-173">hello following example shows hello handler for **InitiateFirmwareUpdate** method:</span></span>

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

<span data-ttu-id="a3de3-174">Noms de gestionnaire de méthode doivent commencer par `On` suivi nom hello de méthode hello.</span><span class="sxs-lookup"><span data-stu-id="a3de3-174">Method handler names must start with `On` followed by hello name of hello method.</span></span> <span data-ttu-id="a3de3-175">Hello **methodRequest** paramètre contient tous les paramètres transmis avec l’appel de méthode hello de hello solution back-end.</span><span class="sxs-lookup"><span data-stu-id="a3de3-175">hello **methodRequest** parameter contains any parameters passed with hello method invocation from hello solution back end.</span></span> <span data-ttu-id="a3de3-176">valeur de retour Hello doit être de type **tâche&lt;MethodResponse&gt;**.</span><span class="sxs-lookup"><span data-stu-id="a3de3-176">hello return value must be of type **Task&lt;MethodResponse&gt;**.</span></span> <span data-ttu-id="a3de3-177">Hello **BuildMethodResponse** méthode utilitaire vous permet de créer la valeur de retour hello.</span><span class="sxs-lookup"><span data-stu-id="a3de3-177">hello **BuildMethodResponse** utility method helps you create hello return value.</span></span>

<span data-ttu-id="a3de3-178">À l’intérieur du Gestionnaire de méthode hello, vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="a3de3-178">Inside hello method handler, you could:</span></span>

- <span data-ttu-id="a3de3-179">Démarrer une tâche asynchrone.</span><span class="sxs-lookup"><span data-stu-id="a3de3-179">Start an asynchronous task.</span></span>
- <span data-ttu-id="a3de3-180">Extraire les propriétés souhaitées hello *double de l’appareil* dans IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="a3de3-180">Retrieve desired properties from hello *device twin* in IoT Hub.</span></span>
- <span data-ttu-id="a3de3-181">Mettre à jour une seule propriété signalée à l’aide de hello **SetReportedPropertyAsync** méthode Bonjour **CoolerDevice** classe.</span><span class="sxs-lookup"><span data-stu-id="a3de3-181">Update a single reported property using hello **SetReportedPropertyAsync** method in hello **CoolerDevice** class.</span></span>
- <span data-ttu-id="a3de3-182">Mettre à jour plusieurs propriétés déclarées en créant un **TwinCollection** instance et hello appelant **Transport.UpdateReportedPropertiesAsync** (méthode).</span><span class="sxs-lookup"><span data-stu-id="a3de3-182">Update multiple reported properties by creating a **TwinCollection** instance and calling hello **Transport.UpdateReportedPropertiesAsync** method.</span></span>

<span data-ttu-id="a3de3-183">Hello précédent exemple de mise à jour de microprogramme exécute hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="a3de3-183">hello preceding firmware update example performs hello following steps:</span></span>

- <span data-ttu-id="a3de3-184">Vérifications hello périphérique est la demande de mise à jour du microprogramme tooaccept en mesure de hello.</span><span class="sxs-lookup"><span data-stu-id="a3de3-184">Checks hello device is able tooaccept hello firmware update request.</span></span>
- <span data-ttu-id="a3de3-185">Lance l’opération de mise à jour de microprogramme hello de façon asynchrone et réinitialise les données de télémétrie hello lorsque hello est terminée.</span><span class="sxs-lookup"><span data-stu-id="a3de3-185">Asynchronously initiates hello firmware update operation and resets hello telemetry when hello operation is complete.</span></span>
- <span data-ttu-id="a3de3-186">Immédiatement retourne hello « FirmwareUpdate accepté » demande de message tooindicate hello a été acceptée par le périphérique de hello.</span><span class="sxs-lookup"><span data-stu-id="a3de3-186">Immediately returns hello "FirmwareUpdate accepted" message tooindicate hello request was accepted by hello device.</span></span>

### <a name="build-and-use-your-own-physical-device"></a><span data-ttu-id="a3de3-187">Création et utilisation de votre propre appareil (physique)</span><span class="sxs-lookup"><span data-stu-id="a3de3-187">Build and use your own (physical) device</span></span>

<span data-ttu-id="a3de3-188">Hello [kits de développement logiciel Azure IoT](https://github.com/Azure/azure-iot-sdks) fournissent des bibliothèques pour la connexion de nombreux types d’appareils (systèmes d’exploitation et langues) dans les solutions IoT.</span><span class="sxs-lookup"><span data-stu-id="a3de3-188">hello [Azure IoT SDKs](https://github.com/Azure/azure-iot-sdks) provide libraries for connecting numerous device types (languages and operating systems) into IoT solutions.</span></span>

## <a name="modify-dashboard-limits"></a><span data-ttu-id="a3de3-189">Modification des limites de tableau de bord</span><span class="sxs-lookup"><span data-stu-id="a3de3-189">Modify dashboard limits</span></span>

### <a name="number-of-devices-displayed-in-dashboard-dropdown"></a><span data-ttu-id="a3de3-190">Nombre d’appareils affichés dans la liste déroulante du tableau de bord</span><span class="sxs-lookup"><span data-stu-id="a3de3-190">Number of devices displayed in dashboard dropdown</span></span>

<span data-ttu-id="a3de3-191">valeur par défaut Hello est 200.</span><span class="sxs-lookup"><span data-stu-id="a3de3-191">hello default is 200.</span></span> <span data-ttu-id="a3de3-192">Vous pouvez modifier cette valeur dans [DashboardController.cs][lnk-dashboard-controller].</span><span class="sxs-lookup"><span data-stu-id="a3de3-192">You can change this number in [DashboardController.cs][lnk-dashboard-controller].</span></span>

### <a name="number-of-pins-toodisplay-in-bing-map-control"></a><span data-ttu-id="a3de3-193">Nombre de toodisplay des codes confidentiels dans un contrôle de carte Bing</span><span class="sxs-lookup"><span data-stu-id="a3de3-193">Number of pins toodisplay in Bing Map control</span></span>

<span data-ttu-id="a3de3-194">valeur par défaut Hello est 200.</span><span class="sxs-lookup"><span data-stu-id="a3de3-194">hello default is 200.</span></span> <span data-ttu-id="a3de3-195">Vous pouvez modifier cette valeur dans [TelemetryApiController.cs][lnk-telemetry-api-controller-01].</span><span class="sxs-lookup"><span data-stu-id="a3de3-195">You can change this number in [TelemetryApiController.cs][lnk-telemetry-api-controller-01].</span></span>

### <a name="time-period-of-telemetry-graph"></a><span data-ttu-id="a3de3-196">Période de temps du graphique de télémétrie</span><span class="sxs-lookup"><span data-stu-id="a3de3-196">Time period of telemetry graph</span></span>

<span data-ttu-id="a3de3-197">valeur par défaut Hello est de 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="a3de3-197">hello default is 10 minutes.</span></span> <span data-ttu-id="a3de3-198">Vous pouvez modifier cette valeur dans [TelemetryApiController.cs][lnk-telemetry-api-controller-02].</span><span class="sxs-lookup"><span data-stu-id="a3de3-198">You can change this value in [TelmetryApiController.cs][lnk-telemetry-api-controller-02].</span></span>

## <a name="manually-set-up-application-roles"></a><span data-ttu-id="a3de3-199">Configuration manuelle des rôles d’application</span><span class="sxs-lookup"><span data-stu-id="a3de3-199">Manually set up application roles</span></span>

<span data-ttu-id="a3de3-200">Hello procédure suivante décrit comment tooadd **Admin** et **ReadOnly** tooa de rôles d’application de solution préconfigurée.</span><span class="sxs-lookup"><span data-stu-id="a3de3-200">hello following procedure describes how tooadd **Admin** and **ReadOnly** application roles tooa preconfigured solution.</span></span> <span data-ttu-id="a3de3-201">Notez que les solutions préconfigurées déjà mis en service à partir du site de azureiotsuite.com hello incluent hello **Admin** et **ReadOnly** rôles.</span><span class="sxs-lookup"><span data-stu-id="a3de3-201">Note that preconfigured solutions provisioned from hello azureiotsuite.com site already include hello **Admin** and **ReadOnly** roles.</span></span>

<span data-ttu-id="a3de3-202">Membres de hello **ReadOnly** rôle peut voir hello le tableau de bord et de la liste des appareils hello, mais ne sont pas autorisées tooadd périphériques, modifier les attributs de périphérique ou les commandes de l’envoi.</span><span class="sxs-lookup"><span data-stu-id="a3de3-202">Members of hello **ReadOnly** role can see hello dashboard and hello device list, but are not allowed tooadd devices, change device attributes, or send commands.</span></span>  <span data-ttu-id="a3de3-203">Membres de hello **Admin** rôle possèdent un accès complet des fonctionnalités de hello de tooall dans la solution de hello.</span><span class="sxs-lookup"><span data-stu-id="a3de3-203">Members of hello **Admin** role have full access tooall hello functionality in hello solution.</span></span>

1. <span data-ttu-id="a3de3-204">Accédez toohello [portail Azure classic][lnk-classic-portal].</span><span class="sxs-lookup"><span data-stu-id="a3de3-204">Go toohello [Azure classic portal][lnk-classic-portal].</span></span>
2. <span data-ttu-id="a3de3-205">Sélectionnez **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a3de3-205">Select **Active Directory**.</span></span>
3. <span data-ttu-id="a3de3-206">Cliquez sur nom hello client AAD de hello que vous avez utilisé lors de la configuration de votre solution.</span><span class="sxs-lookup"><span data-stu-id="a3de3-206">Click hello name of hello AAD tenant you used when you provisioned your solution.</span></span>
4. <span data-ttu-id="a3de3-207">Cliquez sur **Applications**.</span><span class="sxs-lookup"><span data-stu-id="a3de3-207">Click **Applications**.</span></span>
5. <span data-ttu-id="a3de3-208">Cliquez sur nom hello application hello qui correspond au nom de votre solution préconfigurée.</span><span class="sxs-lookup"><span data-stu-id="a3de3-208">Click hello name of hello application that matches your preconfigured solution name.</span></span> <span data-ttu-id="a3de3-209">Si vous ne voyez pas votre application dans la liste de hello, sélectionnez **Applications que ma société possède** Bonjour **afficher** liste déroulante et cliquez sur hello case à cocher.</span><span class="sxs-lookup"><span data-stu-id="a3de3-209">If you don't see your application in hello list, select **Applications my company owns** in hello **Show** dropdown and click hello check mark.</span></span>
6. <span data-ttu-id="a3de3-210">Au bas de hello de page de hello, cliquez sur **gérer manifeste** , puis **télécharger le manifeste**.</span><span class="sxs-lookup"><span data-stu-id="a3de3-210">At hello bottom of hello page, click **Manage Manifest** and then **Download Manifest**.</span></span>
7. <span data-ttu-id="a3de3-211">Cette procédure télécharge un ordinateur local de .json fichier tooyour.</span><span class="sxs-lookup"><span data-stu-id="a3de3-211">This procedure downloads a .json file tooyour local machine.</span></span> <span data-ttu-id="a3de3-212">Ouvrez ce fichier pour le modifier dans un éditeur de texte de votre choix.</span><span class="sxs-lookup"><span data-stu-id="a3de3-212">Open this file for editing in a text editor of your choice.</span></span>
8. <span data-ttu-id="a3de3-213">Sur hello troisième ligne du fichier .json de hello, vous pouvez voir :</span><span class="sxs-lookup"><span data-stu-id="a3de3-213">On hello third line of hello .json file, you can see:</span></span>

   ```json
   "appRoles" : [],
   ```
   <span data-ttu-id="a3de3-214">Remplacez cette ligne hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="a3de3-214">Replace this line with hello following code:</span></span>

   ```json
   "appRoles": [
   {
   "allowedMemberTypes": [
   "User"
   ],
   "description": "Administrator access toohello application",
   "displayName": "Admin",
   "id": "a400a00b-f67c-42b7-ba9a-f73d8c67e433",
   "isEnabled": true,
   "value": "Admin"
   },
   {
   "allowedMemberTypes": [
   "User"
   ],
   "description": "Read only access toodevice information",
   "displayName": "Read Only",
   "id": "e5bbd0f5-128e-4362-9dd1-8f253c6082d7",
   "isEnabled": true,
   "value": "ReadOnly"
   } ],
   ```

9. <span data-ttu-id="a3de3-215">Enregistrez le fichier de mise à jour .json de hello (vous pouvez remplacer les fichiers existants hello).</span><span class="sxs-lookup"><span data-stu-id="a3de3-215">Save hello updated .json file (you can overwrite hello existing file).</span></span>
10. <span data-ttu-id="a3de3-216">Bonjour portail Azure classic, bas hello de page de hello, sélectionnez **gérer manifeste** puis **télécharger le manifeste** tooupload hello .json enregistré à l’étape précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="a3de3-216">In hello Azure classic portal, at hello bottom of hello page, select **Manage Manifest** then **Upload Manifest** tooupload hello .json file you saved in hello previous step.</span></span>
11. <span data-ttu-id="a3de3-217">Vous avez maintenant ajouté hello **Admin** et **ReadOnly** application tooyour de rôles.</span><span class="sxs-lookup"><span data-stu-id="a3de3-217">You have now added hello **Admin** and **ReadOnly** roles tooyour application.</span></span>
12. <span data-ttu-id="a3de3-218">tooassign un de ces utilisateurs tooa de rôles dans votre annuaire, consultez [autorisations sur le site de azureiotsuite.com hello][lnk-permissions].</span><span class="sxs-lookup"><span data-stu-id="a3de3-218">tooassign one of these roles tooa user in your directory, see [Permissions on hello azureiotsuite.com site][lnk-permissions].</span></span>

## <a name="feedback"></a><span data-ttu-id="a3de3-219">Commentaires</span><span class="sxs-lookup"><span data-stu-id="a3de3-219">Feedback</span></span>

<span data-ttu-id="a3de3-220">Avez-vous une personnalisation que vous aimeriez toosee traitée dans ce document ?</span><span class="sxs-lookup"><span data-stu-id="a3de3-220">Do you have a customization you'd like toosee covered in this document?</span></span> <span data-ttu-id="a3de3-221">Ajouter des suggestions de fonctionnalités trop[User Voice](https://feedback.azure.com/forums/321918-azure-iot), ou un commentaire sur cet article.</span><span class="sxs-lookup"><span data-stu-id="a3de3-221">Add feature suggestions too[User Voice](https://feedback.azure.com/forums/321918-azure-iot), or comment on this article.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="a3de3-222">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a3de3-222">Next steps</span></span>

<span data-ttu-id="a3de3-223">toolearn savoir plus sur les options hello pour la personnalisation des solutions de hello préconfiguré, consultez :</span><span class="sxs-lookup"><span data-stu-id="a3de3-223">toolearn more about hello options for customizing hello preconfigured solutions, see:</span></span>

* <span data-ttu-id="a3de3-224">[Solution de Azure IoT Suite l’analyse à distance préconfiguré tooyour application logique de connexion][lnk-logicapp]</span><span class="sxs-lookup"><span data-stu-id="a3de3-224">[Connect Logic App tooyour Azure IoT Suite Remote Monitoring preconfigured solution][lnk-logicapp]</span></span>
* <span data-ttu-id="a3de3-225">[Utiliser la télémétrie dynamique avec hello solution préconfigurée de surveillance à distance][lnk-dynamic]</span><span class="sxs-lookup"><span data-stu-id="a3de3-225">[Use dynamic telemetry with hello remote monitoring preconfigured solution][lnk-dynamic]</span></span>
* <span data-ttu-id="a3de3-226">[Métadonnées d’informations de périphérique Bonjour solution préconfigurée de surveillance à distance][lnk-devinfo]</span><span class="sxs-lookup"><span data-stu-id="a3de3-226">[Device information metadata in hello remote monitoring preconfigured solution][lnk-devinfo]</span></span>
* <span data-ttu-id="a3de3-227">[Personnaliser l’interconnexion hello fabrique solution affiche les données à partir de vos serveurs OPC UA][lnk-cf-customize]</span><span class="sxs-lookup"><span data-stu-id="a3de3-227">[Customize how hello connected factory solution displays data from your OPC UA servers][lnk-cf-customize]</span></span>

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