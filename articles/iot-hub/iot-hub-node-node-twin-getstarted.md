---
title: "aaaGet main jumeaux d’appareil Azure IoT Hub (nœud) | Documents Microsoft"
description: "Comment toouse Azure IoT Hub appareil jumeaux tooadd balises, puis utilisez une requête IoT Hub. Vous utilisez hello kits de développement logiciel Azure IoT pour l’application d’appareil simulé Node.js tooimplement hello et une application de service qui ajoute des balises de hello et s’exécute hello requête de IoT Hub."
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
ms.openlocfilehash: d60b8c3de85e9285e496b86e27d4ee31a0554a1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-device-twins-node"></a><span data-ttu-id="d4bae-104">Prise en main des représentations d’appareils (Node)</span><span class="sxs-lookup"><span data-stu-id="d4bae-104">Get started with device twins (Node)</span></span>
[!INCLUDE [iot-hub-selector-twin-get-started](../../includes/iot-hub-selector-twin-get-started.md)]

<span data-ttu-id="d4bae-105">À la fin de hello de ce didacticiel, vous aurez deux applications de console Node.js :</span><span class="sxs-lookup"><span data-stu-id="d4bae-105">At hello end of this tutorial, you will have two Node.js console apps:</span></span>

* <span data-ttu-id="d4bae-106">**AddTagsAndQuery.js**, application Node.js qui ajoute des balises et interroge des représentations d’appareil.</span><span class="sxs-lookup"><span data-stu-id="d4bae-106">**AddTagsAndQuery.js**, a Node.js back-end app, which adds tags and queries device twins.</span></span>
* <span data-ttu-id="d4bae-107">**TwinSimulatedDevice.js**, une application Node.js qui simule un appareil qui se connecte tooyour IoT hub avec l’identité de l’appareil hello créée précédemment et signale l’état de connectivité.</span><span class="sxs-lookup"><span data-stu-id="d4bae-107">**TwinSimulatedDevice.js**, a Node.js app which simulates a device that connects tooyour IoT hub with hello device identity created earlier, and reports its connectivity condition.</span></span>

> [!NOTE]
> <span data-ttu-id="d4bae-108">article de Hello [kits de développement logiciel Azure IoT] [ lnk-hub-sdks] fournit des informations sur hello kits de développement logiciel Azure IoT que vous pouvez utiliser toobuild applications de périphérique et back-end.</span><span class="sxs-lookup"><span data-stu-id="d4bae-108">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both device and back-end apps.</span></span>
> 
> 

<span data-ttu-id="d4bae-109">toocomplete ce didacticiel, vous devez suivant de hello :</span><span class="sxs-lookup"><span data-stu-id="d4bae-109">toocomplete this tutorial you need hello following:</span></span>

* <span data-ttu-id="d4bae-110">Node.js version 0.10.x ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="d4bae-110">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="d4bae-111">Un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="d4bae-111">An active Azure account.</span></span> <span data-ttu-id="d4bae-112">(Si vous ne possédez pas de compte, vous pouvez créer un [compte gratuit][lnk-free-trial] en quelques minutes.)</span><span class="sxs-lookup"><span data-stu-id="d4bae-112">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-hello-service-app"></a><span data-ttu-id="d4bae-113">Créer l’application de service hello</span><span class="sxs-lookup"><span data-stu-id="d4bae-113">Create hello service app</span></span>
<span data-ttu-id="d4bae-114">Dans cette section, vous créez une application de console Node.js qui ajoute le double d’appareil emplacement métadonnées toohello associé **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="d4bae-114">In this section, you create a Node.js console app that adds location metadata toohello device twin associated with **myDeviceId**.</span></span> <span data-ttu-id="d4bae-115">Il interroge ensuite jumeaux de périphérique hello stockées dans hello IoT hub en sélectionnant les appareils hello situés dans hello nous et puis hello ceux qui signalent une connexion cellulaire.</span><span class="sxs-lookup"><span data-stu-id="d4bae-115">It then queries hello device twins stored in hello IoT hub selecting hello devices located in hello US, and then hello ones that are reporting a cellular connection.</span></span>

1. <span data-ttu-id="d4bae-116">Créez un dossier vide nommé **addtagsandqueryapp**.</span><span class="sxs-lookup"><span data-stu-id="d4bae-116">Create a new empty folder called **addtagsandqueryapp**.</span></span> <span data-ttu-id="d4bae-117">Bonjour **addtagsandqueryapp** dossier, créez un nouveau fichier package.json à l’aide de hello, la commande suivante à l’invite suivante.</span><span class="sxs-lookup"><span data-stu-id="d4bae-117">In hello **addtagsandqueryapp** folder, create a new package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="d4bae-118">Acceptez les valeurs par défaut hello :</span><span class="sxs-lookup"><span data-stu-id="d4bae-118">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="d4bae-119">Votre invite de commandes Bonjour **addtagsandqueryapp** dossier, exécutez hello suivant commande tooinstall hello **azure-iothub** package :</span><span class="sxs-lookup"><span data-stu-id="d4bae-119">At your command prompt in hello **addtagsandqueryapp** folder, run hello following command tooinstall hello **azure-iothub** package:</span></span>
   
    ```
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="d4bae-120">À l’aide d’un éditeur de texte, créez un nouveau **AddTagsAndQuery.js** fichier Bonjour **addtagsandqueryapp** dossier.</span><span class="sxs-lookup"><span data-stu-id="d4bae-120">Using a text editor, create a new **AddTagsAndQuery.js** file in hello **addtagsandqueryapp** folder.</span></span>
4. <span data-ttu-id="d4bae-121">Ajouter hello suivant code toohello **AddTagsAndQuery.js** de fichiers et remplacez-le par hello **{chaîne de connexion de hub iot}** espace réservé par hello chaîne de connexion de IoT Hub vous avez copié lorsque vous avez créé votre hub :</span><span class="sxs-lookup"><span data-stu-id="d4bae-121">Add hello following code toohello **AddTagsAndQuery.js** file, and substitute hello **{iot hub connection string}** placeholder with hello IoT Hub connection string you copied when you created your hub:</span></span>
   
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
   
    <span data-ttu-id="d4bae-122">Hello **Registre** objet expose tous les hello méthodes requis toointeract avec jumeaux de périphérique à partir du service de hello.</span><span class="sxs-lookup"><span data-stu-id="d4bae-122">hello **Registry** object exposes all hello methods required toointeract with device twins from hello service.</span></span> <span data-ttu-id="d4bae-123">code précédent de Hello initialise tout d’abord hello **Registre** de l’objet, puis récupère hello double de périphérique pour **myDeviceId**et enfin met à jour ses balises avec les informations d’emplacement hello souhaité.</span><span class="sxs-lookup"><span data-stu-id="d4bae-123">hello previous code first initializes hello **Registry** object, then retrieves hello device twin for **myDeviceId**, and finally updates its tags with hello desired location information.</span></span>
   
    <span data-ttu-id="d4bae-124">Après avoir hello hello de mise à jour des balises il hello d’appels **queryTwins** (fonction).</span><span class="sxs-lookup"><span data-stu-id="d4bae-124">After hello updating hello tags it calls hello **queryTwins** function.</span></span>
5. <span data-ttu-id="d4bae-125">Ajouter hello suivant du code à la fin de hello de **AddTagsAndQuery.js** tooimplement hello **queryTwins** (fonction) :</span><span class="sxs-lookup"><span data-stu-id="d4bae-125">Add hello following code at hello end of  **AddTagsAndQuery.js** tooimplement hello **queryTwins** function:</span></span>
   
        var queryTwins = function() {
            var query = registry.createQuery("SELECT * FROM devices WHERE tags.location.plant = 'Redmond43'", 100);
            query.nextAsTwin(function(err, results) {
                if (err) {
                    console.error('Failed toofetch hello results: ' + err.message);
                } else {
                    console.log("Devices in Redmond43: " + results.map(function(twin) {return twin.deviceId}).join(','));
                }
            });
   
            query = registry.createQuery("SELECT * FROM devices WHERE tags.location.plant = 'Redmond43' AND properties.reported.connectivity.type = 'cellular'", 100);
            query.nextAsTwin(function(err, results) {
                if (err) {
                    console.error('Failed toofetch hello results: ' + err.message);
                } else {
                    console.log("Devices in Redmond43 using cellular network: " + results.map(function(twin) {return twin.deviceId}).join(','));
                }
            });
        };
   
    <span data-ttu-id="d4bae-126">code de précédent Hello exécute deux requêtes : hello sélectionne tout d’abord uniquement les jumeaux appareil hello des périphériques situés dans hello **Redmond43** usine et hello deuxième affine hello requête tooselect uniquement hello pour les appareils qui sont également connectés via réseau cellulaire.</span><span class="sxs-lookup"><span data-stu-id="d4bae-126">hello previous code executes two queries: hello first selects only hello device twins of devices located in hello **Redmond43** plant, and hello second refines hello query tooselect only hello devices that are also connected through cellular network.</span></span>
   
    <span data-ttu-id="d4bae-127">Notez que hello le code précédent, lorsqu’il crée hello **requête** d’objet, spécifie un nombre maximal de documents renvoyés.</span><span class="sxs-lookup"><span data-stu-id="d4bae-127">Note that hello previous code, when it creates hello **query** object, specifies a maximum number of returned documents.</span></span> <span data-ttu-id="d4bae-128">Hello **requête** objet contient un **hasMoreResults** propriété booléenne que vous pouvez utiliser tooinvoke hello **nextAsTwin** méthodes tooretrieve tous les résultats de plusieurs fois.</span><span class="sxs-lookup"><span data-stu-id="d4bae-128">hello **query** object contains a **hasMoreResults** boolean property that you can use tooinvoke hello **nextAsTwin** methods multiple times tooretrieve all results.</span></span> <span data-ttu-id="d4bae-129">Une méthode appelée **next** est disponible pour les résultats qui ne sont pas des représentations d’appareil, par exemple, les résultats de requêtes d’agrégation.</span><span class="sxs-lookup"><span data-stu-id="d4bae-129">A method called **next** is available for results that are not device twins for example, results of aggregation queries.</span></span>
6. <span data-ttu-id="d4bae-130">Exécutez l’application hello avec :</span><span class="sxs-lookup"><span data-stu-id="d4bae-130">Run hello application with:</span></span>
   
        node AddTagsAndQuery.js
   
    <span data-ttu-id="d4bae-131">Vous devez voir un périphérique dans les résultats de hello pour poser des requêtes hello pour tous les appareils qui se trouve dans **Redmond43** et none pour les requêtes hello qui restreint hello toodevices qui utilisent un réseau cellulaire.</span><span class="sxs-lookup"><span data-stu-id="d4bae-131">You should see one device in hello results for hello query asking for all devices located in **Redmond43** and none for hello query that restricts hello results toodevices that use a cellular network.</span></span>
   
    ![][1]

<span data-ttu-id="d4bae-132">Dans la section suivante de hello vous créez une application de périphérique qui fournit des informations de connectivité hello et modifications hello résultat de requête hello dans la section précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="d4bae-132">In hello next section you create a device app that reports hello connectivity information and changes hello result of hello query in hello previous section.</span></span>

## <a name="create-hello-device-app"></a><span data-ttu-id="d4bae-133">Créer l’application hello</span><span class="sxs-lookup"><span data-stu-id="d4bae-133">Create hello device app</span></span>
<span data-ttu-id="d4bae-134">Dans cette section, vous créez une application de console Node.js qui connecte le concentrateur tooyour **myDeviceId**et ensuite les mises à jour son double de l’appareil de signalé toocontain hello informations sur les propriétés qu’il est connecté à l’aide d’un réseau cellulaire.</span><span class="sxs-lookup"><span data-stu-id="d4bae-134">In this section, you create a Node.js console app that connects tooyour hub as **myDeviceId**, and then updates its device twin's reported properties toocontain hello information that it is connected using a cellular network.</span></span>

> [!NOTE]
> <span data-ttu-id="d4bae-135">À ce stade, jumeaux de périphérique est accessibles uniquement à partir d’appareils qui se connectent tooIoT concentrateur à l’aide du protocole MQTT hello.</span><span class="sxs-lookup"><span data-stu-id="d4bae-135">At this time, device twins are accessible only from devices that connect tooIoT Hub using hello MQTT protocol.</span></span> <span data-ttu-id="d4bae-136">Reportez-vous toohello [prise en charge MQTT] [ lnk-devguide-mqtt] article pour obtenir des instructions sur la façon de tooconvert existant appareil application toouse MQTT.</span><span class="sxs-lookup"><span data-stu-id="d4bae-136">Please refer toohello [MQTT support][lnk-devguide-mqtt] article for instructions on how tooconvert existing device app toouse MQTT.</span></span>
> 
> 

1. <span data-ttu-id="d4bae-137">Créez un dossier vide nommé **reportconnectivity**.</span><span class="sxs-lookup"><span data-stu-id="d4bae-137">Create a new empty folder called **reportconnectivity**.</span></span> <span data-ttu-id="d4bae-138">Bonjour **reportconnectivity** dossier, créez un nouveau fichier package.json à l’aide de hello, la commande suivante à l’invite suivante.</span><span class="sxs-lookup"><span data-stu-id="d4bae-138">In hello **reportconnectivity** folder, create a new package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="d4bae-139">Acceptez les valeurs par défaut hello :</span><span class="sxs-lookup"><span data-stu-id="d4bae-139">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="d4bae-140">Votre invite de commandes Bonjour **reportconnectivity** dossier, exécutez hello suivant commande tooinstall hello **azure iot-appareil**, et **azure-iot-périphérique-mqtt** package :</span><span class="sxs-lookup"><span data-stu-id="d4bae-140">At your command prompt in hello **reportconnectivity** folder, run hello following command tooinstall hello **azure-iot-device**, and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="d4bae-141">À l’aide d’un éditeur de texte, créez un nouveau **ReportConnectivity.js** fichier Bonjour **reportconnectivity** dossier.</span><span class="sxs-lookup"><span data-stu-id="d4bae-141">Using a text editor, create a new **ReportConnectivity.js** file in hello **reportconnectivity** folder.</span></span>
4. <span data-ttu-id="d4bae-142">Ajouter hello suivant code toohello **ReportConnectivity.js** de fichiers et remplacez-le par hello **{chaîne de connexion de périphérique}** espace réservé avec la chaîne de connexion de périphérique hello vous avez copié lors de la création de hello **myDeviceId** identité d’appareil :</span><span class="sxs-lookup"><span data-stu-id="d4bae-142">Add hello following code toohello **ReportConnectivity.js** file, and substitute hello **{device connection string}** placeholder with hello device connection string you copied when you created hello **myDeviceId** device identity:</span></span>
   
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
   
    <span data-ttu-id="d4bae-143">Hello **Client** objet expose toutes les méthodes hello nécessitent de toointeract avec jumeaux de périphérique à partir de l’appareil de hello.</span><span class="sxs-lookup"><span data-stu-id="d4bae-143">hello **Client** object exposes all hello methods you require toointeract with device twins from hello device.</span></span> <span data-ttu-id="d4bae-144">Hello le code précédent, une fois qu’il initialise hello **Client** de l’objet, récupère hello double de périphérique pour **myDeviceId** et met à jour sa propriété signalée avec les informations de connectivité hello.</span><span class="sxs-lookup"><span data-stu-id="d4bae-144">hello previous code, after it initializes hello **Client** object, retrieves hello device twin for **myDeviceId** and updates its reported property with hello connectivity information.</span></span>
5. <span data-ttu-id="d4bae-145">Exécutez l’application hello</span><span class="sxs-lookup"><span data-stu-id="d4bae-145">Run hello device app</span></span>
   
        node ReportConnectivity.js
   
    <span data-ttu-id="d4bae-146">Vous devez voir le message de type hello `twin state reported`.</span><span class="sxs-lookup"><span data-stu-id="d4bae-146">You should see hello message `twin state reported`.</span></span>
6. <span data-ttu-id="d4bae-147">Maintenant que hello appareil signalé ses informations de connectivité, il doit s’afficher dans les deux requêtes.</span><span class="sxs-lookup"><span data-stu-id="d4bae-147">Now that hello device reported its connectivity information, it should appear in both queries.</span></span> <span data-ttu-id="d4bae-148">Accédez à hello **addtagsandqueryapp** hello et exécutez à nouveau des requêtes :</span><span class="sxs-lookup"><span data-stu-id="d4bae-148">Go back in hello **addtagsandqueryapp** folder and run hello queries again:</span></span>
   
        node AddTagsAndQuery.js
   
    <span data-ttu-id="d4bae-149">Cette fois, **myDeviceId** doit apparaître dans les résultats des deux requêtes.</span><span class="sxs-lookup"><span data-stu-id="d4bae-149">This time **myDeviceId** should appear in both query results.</span></span>
   
    ![][3]

## <a name="next-steps"></a><span data-ttu-id="d4bae-150">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d4bae-150">Next steps</span></span>
<span data-ttu-id="d4bae-151">Dans ce didacticiel, vous configuré un IoT hub Bonjour portail Azure et ensuite créé une identité d’appareil dans le Registre des identités de hello IoT hub.</span><span class="sxs-lookup"><span data-stu-id="d4bae-151">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="d4bae-152">Vous ajouté des métadonnées de l’appareil sous forme de balises à partir d’une application back-end et a écrit un appareil simulé application tooreport appareil connectivité des informations en double du périphérique hello.</span><span class="sxs-lookup"><span data-stu-id="d4bae-152">You added device metadata as tags from a back-end app, and wrote a simulated device app tooreport device connectivity information in hello device twin.</span></span> <span data-ttu-id="d4bae-153">Vous avez également appris tooquery ces informations à l’aide du langage de requête de type SQL IoT Hub hello.</span><span class="sxs-lookup"><span data-stu-id="d4bae-153">You also learned how tooquery this information using hello SQL-like IoT Hub query language.</span></span>

<span data-ttu-id="d4bae-154">Hello utilisation suivant comment les ressources toolearn à :</span><span class="sxs-lookup"><span data-stu-id="d4bae-154">Use hello following resources toolearn how to:</span></span>

* <span data-ttu-id="d4bae-155">envoyer la télémétrie des appareils avec hello [prise en main IoT Hub] [ lnk-iothub-getstarted] (didacticiel),</span><span class="sxs-lookup"><span data-stu-id="d4bae-155">send telemetry from devices with hello [Get started with IoT Hub][lnk-iothub-getstarted] tutorial,</span></span>
* <span data-ttu-id="d4bae-156">configurer des appareils à l’aide des propriétés de votre choix du double de l’appareil avec hello [utilisation souhaitée propriétés tooconfigure dispositifs] [ lnk-twin-how-to-configure] (didacticiel),</span><span class="sxs-lookup"><span data-stu-id="d4bae-156">configure devices using device twin's desired properties with hello [Use desired properties tooconfigure devices][lnk-twin-how-to-configure] tutorial,</span></span>
* <span data-ttu-id="d4bae-157">contrôler les périphériques de manière interactive (telles que l’activation sur un ventilateur à partir d’une application contrôlée par l’utilisateur), avec hello [utiliser les méthodes directes] [ lnk-methods-tutorial] didacticiel.</span><span class="sxs-lookup"><span data-stu-id="d4bae-157">control devices interactively (such as turning on a fan from a user-controlled app), with hello [Use direct methods][lnk-methods-tutorial] tutorial.</span></span>

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
