---
title: "Prise en main des représentations physiques Azure IoT Hub (Node) | Microsoft Docs"
description: "Guide d’utilisation des représentations d’appareils Azure IoT Hub pour ajouter des balises, puis utiliser une requête IoT Hub. Vous utilisez les SDK Azure IoT pour Node.js afin d’implémenter l’application d’appareil simulé et une application de service qui ajoute les balises et exécute la requête IoT Hub."
services: iot-hub
documentationcenter: node
author: fsautomata
manager: timlt
editor: 
ms.assetid: 314c88e4-cce1-441c-b75a-d2e08e39ae7d
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: elioda
ms.openlocfilehash: 633c9fd4f8a1d017d93148f8c2e860ccba14238c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-device-twins-node"></a><span data-ttu-id="0b359-104">Prise en main des représentations d’appareils (Node)</span><span class="sxs-lookup"><span data-stu-id="0b359-104">Get started with device twins (Node)</span></span>
[!INCLUDE [iot-hub-selector-twin-get-started](../../includes/iot-hub-selector-twin-get-started.md)]

<span data-ttu-id="0b359-105">À la fin de ce didacticiel, vous disposerez de deux applications console Node.js :</span><span class="sxs-lookup"><span data-stu-id="0b359-105">At the end of this tutorial, you will have two Node.js console apps:</span></span>

* <span data-ttu-id="0b359-106">**AddTagsAndQuery.js**, application Node.js qui ajoute des balises et interroge des représentations d’appareil.</span><span class="sxs-lookup"><span data-stu-id="0b359-106">**AddTagsAndQuery.js**, a Node.js back-end app, which adds tags and queries device twins.</span></span>
* <span data-ttu-id="0b359-107">**TwinSimulatedDevice.js**, application Node.js qui simule un appareil se connectant à votre IoT Hub avec l’identité d’appareil créée précédemment, et signale son état de connectivité.</span><span class="sxs-lookup"><span data-stu-id="0b359-107">**TwinSimulatedDevice.js**, a Node.js app which simulates a device that connects to your IoT hub with the device identity created earlier, and reports its connectivity condition.</span></span>

> [!NOTE]
> <span data-ttu-id="0b359-108">L’article [Kits de développement logiciel (SDK) Azure IoT][lnk-hub-sdks] fournit des informations sur les Kits de développement logiciel (SDK) IoT que vous pouvez utiliser pour générer des applications pour appareil et des applications principales.</span><span class="sxs-lookup"><span data-stu-id="0b359-108">The article [Azure IoT SDKs][lnk-hub-sdks] provides information about the Azure IoT SDKs that you can use to build both device and back-end apps.</span></span>
> 
> 

<span data-ttu-id="0b359-109">Pour réaliser ce didacticiel, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="0b359-109">To complete this tutorial you need the following:</span></span>

* <span data-ttu-id="0b359-110">Node.js version 0.10.x ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="0b359-110">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="0b359-111">Un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="0b359-111">An active Azure account.</span></span> <span data-ttu-id="0b359-112">(Si vous ne possédez pas de compte, vous pouvez créer un [compte gratuit][lnk-free-trial] en quelques minutes.)</span><span class="sxs-lookup"><span data-stu-id="0b359-112">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-the-service-app"></a><span data-ttu-id="0b359-113">Créer l’application de service</span><span class="sxs-lookup"><span data-stu-id="0b359-113">Create the service app</span></span>
<span data-ttu-id="0b359-114">Dans cette section, vous créez une application console Node.js qui ajoute des métadonnées d’emplacement à la représentation d’appareil associée à **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="0b359-114">In this section, you create a Node.js console app that adds location metadata to the device twin associated with **myDeviceId**.</span></span> <span data-ttu-id="0b359-115">Elle interroge ensuite les jumeaux d’appareil stockés dans le hub IoT en sélectionnant les appareils situés aux États-Unis, puis ceux qui signalent une connexion mobile.</span><span class="sxs-lookup"><span data-stu-id="0b359-115">It then queries the device twins stored in the IoT hub selecting the devices located in the US, and then the ones that are reporting a cellular connection.</span></span>

1. <span data-ttu-id="0b359-116">Créez un dossier vide nommé **addtagsandqueryapp**.</span><span class="sxs-lookup"><span data-stu-id="0b359-116">Create a new empty folder called **addtagsandqueryapp**.</span></span> <span data-ttu-id="0b359-117">Dans le dossier **addtagsandqueryapp**, créez un fichier package.json en utilisant la commande suivante à l’invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="0b359-117">In the **addtagsandqueryapp** folder, create a new package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="0b359-118">Acceptez toutes les valeurs par défaut :</span><span class="sxs-lookup"><span data-stu-id="0b359-118">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="0b359-119">À l’invite de commandes, dans le dossier **addtagsandqueryapp**, exécutez la commande suivante pour installer le package **azure-iothub** :</span><span class="sxs-lookup"><span data-stu-id="0b359-119">At your command prompt in the **addtagsandqueryapp** folder, run the following command to install the **azure-iothub** package:</span></span>
   
    ```
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="0b359-120">À l’aide d’un éditeur de texte, créez un fichier **AddTagsAndQuery.js** dans le dossier **addtagsandqueryapp**.</span><span class="sxs-lookup"><span data-stu-id="0b359-120">Using a text editor, create a new **AddTagsAndQuery.js** file in the **addtagsandqueryapp** folder.</span></span>
4. <span data-ttu-id="0b359-121">Ajoutez le code suivant au fichier **AddTagsAndQuery.js**, puis remplacez l’espace réservé **{iot hub connection string}** par la chaîne de connexion que vous avez copiée lors de la création de votre IoT Hub :</span><span class="sxs-lookup"><span data-stu-id="0b359-121">Add the following code to the **AddTagsAndQuery.js** file, and substitute the **{iot hub connection string}** placeholder with the IoT Hub connection string you copied when you created your hub:</span></span>
   
        'use strict';
        var iothub = require('azure-iothub');
        var connectionString = '{iot hub connection string}';
        var registry = iothub.Registry.fromConnectionString(connectionString);
   
        registry.getTwin('myDeviceId', function(err, twin){
            if (err) {
                console.error(err.constructor.name + ': ' + err.message);
            } else {
                var patch = {
                    tags: {
                        location: {
                            region: 'US',
                            plant: 'Redmond43'
                      }
                    }
                };
   
                twin.update(patch, function(err) {
                  if (err) {
                    console.error('Could not update twin: ' + err.constructor.name + ': ' + err.message);
                  } else {
                    console.log(twin.deviceId + ' twin updated successfully');
                    queryTwins();
                  }
                });
            }
        });
   
    <span data-ttu-id="0b359-122">L’objet **Registry** expose toutes les méthodes requises pour interagir avec des représentations d’appareil à partir du service.</span><span class="sxs-lookup"><span data-stu-id="0b359-122">The **Registry** object exposes all the methods required to interact with device twins from the service.</span></span> <span data-ttu-id="0b359-123">Le code précédent initialise l’objet **Registry**, récupère la représentation d’appareil de **myDeviceId**, puis met à jour ses balises avec les informations d’emplacement souhaitées.</span><span class="sxs-lookup"><span data-stu-id="0b359-123">The previous code first initializes the **Registry** object, then retrieves the device twin for **myDeviceId**, and finally updates its tags with the desired location information.</span></span>
   
    <span data-ttu-id="0b359-124">Une fois les balises mises à jour, il appelle la fonction **queryTwins**.</span><span class="sxs-lookup"><span data-stu-id="0b359-124">After the updating the tags it calls the **queryTwins** function.</span></span>
5. <span data-ttu-id="0b359-125">Ajoutez le code suivant à la fin de  **AddTagsAndQuery.js** pour implémenter la fonction **queryTwins**:</span><span class="sxs-lookup"><span data-stu-id="0b359-125">Add the following code at the end of  **AddTagsAndQuery.js** to implement the **queryTwins** function:</span></span>
   
        var queryTwins = function() {
            var query = registry.createQuery("SELECT * FROM devices WHERE tags.location.plant = 'Redmond43'", 100);
            query.nextAsTwin(function(err, results) {
                if (err) {
                    console.error('Failed to fetch the results: ' + err.message);
                } else {
                    console.log("Devices in Redmond43: " + results.map(function(twin) {return twin.deviceId}).join(','));
                }
            });
   
            query = registry.createQuery("SELECT * FROM devices WHERE tags.location.plant = 'Redmond43' AND properties.reported.connectivity.type = 'cellular'", 100);
            query.nextAsTwin(function(err, results) {
                if (err) {
                    console.error('Failed to fetch the results: ' + err.message);
                } else {
                    console.log("Devices in Redmond43 using cellular network: " + results.map(function(twin) {return twin.deviceId}).join(','));
                }
            });
        };
   
    <span data-ttu-id="0b359-126">Le code précédent exécute deux requêtes : la première sélectionne uniquement les représentations des appareils situés dans l’usine **Redmond43**et la seconde affine la requête pour sélectionner uniquement les appareils qui sont également connectés via un réseau cellulaire.</span><span class="sxs-lookup"><span data-stu-id="0b359-126">The previous code executes two queries: the first selects only the device twins of devices located in the **Redmond43** plant, and the second refines the query to select only the devices that are also connected through cellular network.</span></span>
   
    <span data-ttu-id="0b359-127">Notez que le code précédent, quand il crée l’objet **query**, spécifie un nombre maximal de documents retournés.</span><span class="sxs-lookup"><span data-stu-id="0b359-127">Note that the previous code, when it creates the **query** object, specifies a maximum number of returned documents.</span></span> <span data-ttu-id="0b359-128">L’objet **query** contient une propriété booléenne **hasMoreResults** permettant d’appeler les méthodes **nextAsTwin** plusieurs fois afin de récupérer tous les résultats.</span><span class="sxs-lookup"><span data-stu-id="0b359-128">The **query** object contains a **hasMoreResults** boolean property that you can use to invoke the **nextAsTwin** methods multiple times to retrieve all results.</span></span> <span data-ttu-id="0b359-129">Une méthode appelée **next** est disponible pour les résultats qui ne sont pas des représentations d’appareil, par exemple, les résultats de requêtes d’agrégation.</span><span class="sxs-lookup"><span data-stu-id="0b359-129">A method called **next** is available for results that are not device twins for example, results of aggregation queries.</span></span>
6. <span data-ttu-id="0b359-130">Exécutez l’application avec :</span><span class="sxs-lookup"><span data-stu-id="0b359-130">Run the application with:</span></span>
   
        node AddTagsAndQuery.js
   
    <span data-ttu-id="0b359-131">Vous devriez voir un appareil dans les résultats de la requête demandant tous les appareils situés à **Redmond43**, et aucun pour la requête limitant les résultats aux appareils utilisant un réseau cellulaire.</span><span class="sxs-lookup"><span data-stu-id="0b359-131">You should see one device in the results for the query asking for all devices located in **Redmond43** and none for the query that restricts the results to devices that use a cellular network.</span></span>
   
    ![][1]

<span data-ttu-id="0b359-132">Dans la section suivante, vous allez créer une application d’appareil qui signale les informations de connectivité et modifie le résultat de la requête de la section précédente.</span><span class="sxs-lookup"><span data-stu-id="0b359-132">In the next section you create a device app that reports the connectivity information and changes the result of the query in the previous section.</span></span>

## <a name="create-the-device-app"></a><span data-ttu-id="0b359-133">Créer l’application d’appareil</span><span class="sxs-lookup"><span data-stu-id="0b359-133">Create the device app</span></span>
<span data-ttu-id="0b359-134">Dans cette section, vous allez créer une application console Node.js qui se connecte à votre hub en tant que **myDeviceId**, puis met à jour les propriétés signalées de sa représentation d’appareil afin qu’elles contiennent les informations indiquant qu’elle est connectée par le biais d’un réseau cellulaire.</span><span class="sxs-lookup"><span data-stu-id="0b359-134">In this section, you create a Node.js console app that connects to your hub as **myDeviceId**, and then updates its device twin's reported properties to contain the information that it is connected using a cellular network.</span></span>

> [!NOTE]
> <span data-ttu-id="0b359-135">Actuellement, des représentations d’appareil sont accessibles uniquement à partir d’appareils qui se connectent à IoT Hub à l’aide du protocole MQTT.</span><span class="sxs-lookup"><span data-stu-id="0b359-135">At this time, device twins are accessible only from devices that connect to IoT Hub using the MQTT protocol.</span></span> <span data-ttu-id="0b359-136">Pour obtenir des instructions sur la conversion d’une application de périphérique existante pour utiliser MQTT, voir [Support MQTT][lnk-devguide-mqtt].</span><span class="sxs-lookup"><span data-stu-id="0b359-136">Please refer to the [MQTT support][lnk-devguide-mqtt] article for instructions on how to convert existing device app to use MQTT.</span></span>
> 
> 

1. <span data-ttu-id="0b359-137">Créez un dossier vide nommé **reportconnectivity**.</span><span class="sxs-lookup"><span data-stu-id="0b359-137">Create a new empty folder called **reportconnectivity**.</span></span> <span data-ttu-id="0b359-138">Dans le dossier **reportconnectivity**, créez un fichier package.json en utilisant la commande suivante à l’invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="0b359-138">In the **reportconnectivity** folder, create a new package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="0b359-139">Acceptez toutes les valeurs par défaut :</span><span class="sxs-lookup"><span data-stu-id="0b359-139">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="0b359-140">À l’invite de commandes, dans le dossier **reportconnectivity**, exécutez la commande suivante pour installer les packages **azure-iot-device** et **azure-iot-device-mqtt** :</span><span class="sxs-lookup"><span data-stu-id="0b359-140">At your command prompt in the **reportconnectivity** folder, run the following command to install the **azure-iot-device**, and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="0b359-141">À l’aide d’un éditeur de texte, créez un fichier **ReportConnectivity.js** dans le dossier **reportconnectivity**.</span><span class="sxs-lookup"><span data-stu-id="0b359-141">Using a text editor, create a new **ReportConnectivity.js** file in the **reportconnectivity** folder.</span></span>
4. <span data-ttu-id="0b359-142">Ajoutez le code suivant au fichier **ReportConnectivity.js**, puis remplacez l’espace réservé **{device connection string}** par la chaîne de connexion à l’appareil que vous avez copiée lors de la création de l’identité d’appareil **myDeviceId** :</span><span class="sxs-lookup"><span data-stu-id="0b359-142">Add the following code to the **ReportConnectivity.js** file, and substitute the **{device connection string}** placeholder with the device connection string you copied when you created the **myDeviceId** device identity:</span></span>
   
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
   
    <span data-ttu-id="0b359-143">L’objet **Client** expose toutes les méthodes requises pour interagir avec des représentations d’appareil à partir de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="0b359-143">The **Client** object exposes all the methods you require to interact with device twins from the device.</span></span> <span data-ttu-id="0b359-144">Le code précédent, après avoir initialisé l’objet **Client**, récupère la représentation d’appareil de **myDeviceId**, puis met à jour sa propriété signalée avec les informations de connectivité.</span><span class="sxs-lookup"><span data-stu-id="0b359-144">The previous code, after it initializes the **Client** object, retrieves the device twin for **myDeviceId** and updates its reported property with the connectivity information.</span></span>
5. <span data-ttu-id="0b359-145">Exécuter l’application d’appareil</span><span class="sxs-lookup"><span data-stu-id="0b359-145">Run the device app</span></span>
   
        node ReportConnectivity.js
   
    <span data-ttu-id="0b359-146">Vous devriez voir le message `twin state reported`.</span><span class="sxs-lookup"><span data-stu-id="0b359-146">You should see the message `twin state reported`.</span></span>
6. <span data-ttu-id="0b359-147">À présent que l’appareil a signalé ses informations de connectivité, il doit apparaître dans les deux requêtes.</span><span class="sxs-lookup"><span data-stu-id="0b359-147">Now that the device reported its connectivity information, it should appear in both queries.</span></span> <span data-ttu-id="0b359-148">Accédez au dossier **addtagsandqueryapp**, puis réexécutez les requêtes :</span><span class="sxs-lookup"><span data-stu-id="0b359-148">Go back in the **addtagsandqueryapp** folder and run the queries again:</span></span>
   
        node AddTagsAndQuery.js
   
    <span data-ttu-id="0b359-149">Cette fois, **myDeviceId** doit apparaître dans les résultats des deux requêtes.</span><span class="sxs-lookup"><span data-stu-id="0b359-149">This time **myDeviceId** should appear in both query results.</span></span>
   
    ![][3]

## <a name="next-steps"></a><span data-ttu-id="0b359-150">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0b359-150">Next steps</span></span>
<span data-ttu-id="0b359-151">Dans ce didacticiel, vous avez configuré un nouveau hub IoT dans le portail Azure, puis créé une identité d’appareil dans le registre des identités du hub IoT.</span><span class="sxs-lookup"><span data-stu-id="0b359-151">In this tutorial, you configured a new IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span></span> <span data-ttu-id="0b359-152">Vous avez ajouté des métadonnées d’appareil en tant que balises à partir d’une application principale et écrit une application pour appareil simulée pour signaler des informations de connectivité d’appareil dans le jumeau d’appareil.</span><span class="sxs-lookup"><span data-stu-id="0b359-152">You added device metadata as tags from a back-end app, and wrote a simulated device app to report device connectivity information in the device twin.</span></span> <span data-ttu-id="0b359-153">Vous avez également appris à interroger ces informations à l’aide du langage de requête IoT Hub de type SQL.</span><span class="sxs-lookup"><span data-stu-id="0b359-153">You also learned how to query this information using the SQL-like IoT Hub query language.</span></span>

<span data-ttu-id="0b359-154">Utilisez les ressources suivantes :</span><span class="sxs-lookup"><span data-stu-id="0b359-154">Use the following resources to learn how to:</span></span>

* <span data-ttu-id="0b359-155">Pour savoir comment envoyer les données de télémétrie à partir d’appareils, consultez le didacticiel [Prise en main d’IoT Hub][lnk-iothub-getstarted].</span><span class="sxs-lookup"><span data-stu-id="0b359-155">send telemetry from devices with the [Get started with IoT Hub][lnk-iothub-getstarted] tutorial,</span></span>
* <span data-ttu-id="0b359-156">Pour savoir comment configurer des appareils à l’aide des propriétés de représentation d’appareil souhaitées, consultez le didacticiel [Utiliser des propriétés souhaitées pour configurer des appareils][lnk-twin-how-to-configure].</span><span class="sxs-lookup"><span data-stu-id="0b359-156">configure devices using device twin's desired properties with the [Use desired properties to configure devices][lnk-twin-how-to-configure] tutorial,</span></span>
* <span data-ttu-id="0b359-157">Pour savoir comment contrôler des appareils de façon interactive (par exemple en mettant en marche un ventilateur à partir d’une application contrôlée par l’utilisateur), consultez le didacticiel [Utiliser des méthodes directes][lnk-methods-tutorial].</span><span class="sxs-lookup"><span data-stu-id="0b359-157">control devices interactively (such as turning on a fan from a user-controlled app), with the [Use direct methods][lnk-methods-tutorial] tutorial.</span></span>

<!-- images -->
[1]: media/iot-hub-node-node-twin-getstarted/service1.png
[3]: media/iot-hub-node-node-twin-getstarted/service2.png

<!-- links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[lnk-d2c]: iot-hub-devguide-messaging.md#device-to-cloud-messages
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-identity]: iot-hub-devguide-identity-registry.md

[lnk-iothub-getstarted]: iot-hub-node-node-getstarted.md
[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/

[lnk-twin-how-to-configure]: iot-hub-node-node-twin-how-to-configure.md
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md

[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
