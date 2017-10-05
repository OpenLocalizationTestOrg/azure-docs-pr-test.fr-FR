---
title: "Utiliser la télémétrie dynamique | Microsoft Docs"
description: "Suivez ce didacticiel pour savoir comment utiliser la télémétrie dynamique avec la solution préconfigurée de surveillance à distance Azure IoT Suite."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 562799dc-06ea-4cdd-b822-80d1f70d2f09
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: 0114f27f9b8ae76e1170d04ddf66e2c4bf20686a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="use-dynamic-telemetry-with-the-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="c253a-103">Utilisation de la télémétrie dynamique avec la solution préconfigurée de surveillance à distance</span><span class="sxs-lookup"><span data-stu-id="c253a-103">Use dynamic telemetry with the remote monitoring preconfigured solution</span></span>

<span data-ttu-id="c253a-104">La télémétrie dynamique vous permet de visualiser toutes les données de télémétrie envoyées vers la solution préconfigurée de surveillance à distance.</span><span class="sxs-lookup"><span data-stu-id="c253a-104">Dynamic telemetry enables you to visualize any telemetry sent to the remote monitoring preconfigured solution.</span></span> <span data-ttu-id="c253a-105">Les appareils simulés déployés avec la solution préconfigurée envoient les données de télémétrie de température et d’humidité, que vous pouvez afficher sur le tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="c253a-105">The simulated devices that deploy with the preconfigured solution send temperature and humidity telemetry, which you can visualize on the dashboard.</span></span> <span data-ttu-id="c253a-106">Si vous personnalisez les appareils simulés existants, créez des appareils simulés ou connectez des appareils physiques sur la solution préconfigurée vers laquelle vous pouvez envoyer d’autres valeurs de télémétrie comme la température externe, les données RPM ou la vitesse du vent.</span><span class="sxs-lookup"><span data-stu-id="c253a-106">If you customize existing simulated devices, create new simulated devices, or connect physical devices to the preconfigured solution you can send other telemetry values such as the external temperature, RPM, or windspeed.</span></span> <span data-ttu-id="c253a-107">Vous pouvez ensuite visualiser ces données de télémétrie supplémentaires sur le tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="c253a-107">You can then visualize this additional telemetry on the dashboard.</span></span>

<span data-ttu-id="c253a-108">Ce didacticiel utilise un appareil simulé Node.js simple que vous pouvez facilement modifier pour faire des essais avec les données de télémétrie dynamique.</span><span class="sxs-lookup"><span data-stu-id="c253a-108">This tutorial uses a simple Node.js simulated device that you can easily modify to experiment with dynamic telemetry.</span></span>

<span data-ttu-id="c253a-109">Pour suivre ce didacticiel, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="c253a-109">To complete this tutorial, you’ll need:</span></span>

* <span data-ttu-id="c253a-110">Un abonnement Azure actif.</span><span class="sxs-lookup"><span data-stu-id="c253a-110">An active Azure subscription.</span></span> <span data-ttu-id="c253a-111">Si vous ne possédez pas de compte, vous pouvez créer un compte d’évaluation gratuit en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="c253a-111">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="c253a-112">Pour plus d’informations, consultez la rubrique [Version d’évaluation gratuite d’Azure][lnk_free_trial].</span><span class="sxs-lookup"><span data-stu-id="c253a-112">For details, see [Azure Free Trial][lnk_free_trial].</span></span>
* <span data-ttu-id="c253a-113">[Node.js][lnk-node] version 0.12.x ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="c253a-113">[Node.js][lnk-node] version 0.12.x or later.</span></span>

<span data-ttu-id="c253a-114">Vous pouvez suivre ce didacticiel sur n’importe quel système d’exploitation (par exemple, Windows ou Linux) où vous pouvez installer Node.js.</span><span class="sxs-lookup"><span data-stu-id="c253a-114">You can complete this tutorial on any operating system, such as Windows or Linux, where you can install Node.js.</span></span>

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

[!INCLUDE [iot-suite-send-external-temperature](../../includes/iot-suite-send-external-temperature.md)]

## <a name="add-a-telemetry-type"></a><span data-ttu-id="c253a-115">Ajouter un type de télémétrie</span><span class="sxs-lookup"><span data-stu-id="c253a-115">Add a telemetry type</span></span>

<span data-ttu-id="c253a-116">L’étape suivante consiste à remplacer les données de télémétrie générées par l’appareil simulé Node.js par un nouveau jeu de valeurs :</span><span class="sxs-lookup"><span data-stu-id="c253a-116">The next step is to replace the telemetry generated by the Node.js simulated device with a new set of values:</span></span>

1. <span data-ttu-id="c253a-117">Arrêtez l’appareil simulé Node.js en tapant **Ctrl+C** dans l’invite de commandes ou l’interpréteur de commandes.</span><span class="sxs-lookup"><span data-stu-id="c253a-117">Stop the Node.js simulated device by typing **Ctrl+C** in your command prompt or shell.</span></span>
2. <span data-ttu-id="c253a-118">Dans le fichier remote_monitoring.js, vous pouvez voir les valeurs de données de base pour la télémétrie existante de température, d’humidité et de température externe.</span><span class="sxs-lookup"><span data-stu-id="c253a-118">In the remote_monitoring.js file, you can see the base data values for the existing temperature, humidity, and external temperature telemetry.</span></span> <span data-ttu-id="c253a-119">Ajoutez une valeur de données de base pour **rpm** comme suit :</span><span class="sxs-lookup"><span data-stu-id="c253a-119">Add a base data value for **rpm** as follows:</span></span>

    ```nodejs
    // Sensors data
    var temperature = 50;
    var humidity = 50;
    var externalTemperature = 55;
    var rpm = 200;
    ```

3. <span data-ttu-id="c253a-120">L’appareil simulé Node.js utilise la fonction **generateRandomIncrement** dans le fichier remote_monitoring.js pour ajouter un incrément aléatoire aux valeurs de données de base.</span><span class="sxs-lookup"><span data-stu-id="c253a-120">The Node.js simulated device uses the **generateRandomIncrement** function in the remote_monitoring.js file to add a random increment to the base data values.</span></span> <span data-ttu-id="c253a-121">Rendez aléatoire la valeur **rpm** en ajoutant une ligne de code après les randomisations existantes comme suit :</span><span class="sxs-lookup"><span data-stu-id="c253a-121">Randomize the **rpm** value by adding a line of code after the existing randomizations as follows:</span></span>

    ```nodejs
    temperature += generateRandomIncrement();
    externalTemperature += generateRandomIncrement();
    humidity += generateRandomIncrement();
    rpm += generateRandomIncrement();
    ```

4. <span data-ttu-id="c253a-122">Ajoutez la nouvelle valeur rpm pour la charge utile JSON que l’appareil envoie vers IoT Hub :</span><span class="sxs-lookup"><span data-stu-id="c253a-122">Add the new rpm value to the JSON payload the device sends to IoT Hub:</span></span>

    ```nodejs
    var data = JSON.stringify({
      'DeviceID': deviceId,
      'Temperature': temperature,
      'Humidity': humidity,
      'ExternalTemperature': externalTemperature,
      'RPM': rpm
    });
    ```

5. <span data-ttu-id="c253a-123">Exécutez l’appareil simulé Node.js à l’aide de la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="c253a-123">Run the Node.js simulated device using the following command:</span></span>

    `node remote_monitoring.js`

6. <span data-ttu-id="c253a-124">Observez le nouveau type de télémétrie RPM qui s’affiche sur le graphique dans le tableau de bord :</span><span class="sxs-lookup"><span data-stu-id="c253a-124">Observe the new RPM telemetry type that displays on the chart in the dashboard:</span></span>

![Ajouter les valeurs RPM au tableau de bord][image3]

> [!NOTE]
> <span data-ttu-id="c253a-126">Vous devrez peut-être désactiver, puis activer l’appareil Node.js sur la page **Appareils** du tableau de bord pour afficher immédiatement les changements.</span><span class="sxs-lookup"><span data-stu-id="c253a-126">You may need to disable and then enable the Node.js device on the **Devices** page in the dashboard to see the change immediately.</span></span>

## <a name="customize-the-dashboard-display"></a><span data-ttu-id="c253a-127">Personnaliser l’affichage du tableau de bord</span><span class="sxs-lookup"><span data-stu-id="c253a-127">Customize the dashboard display</span></span>

<span data-ttu-id="c253a-128">Le message **Device-Info** peut inclure des métadonnées sur la télémétrie pouvant être envoyée par l’appareil vers IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="c253a-128">The **Device-Info** message can include metadata about the telemetry the device can send to IoT Hub.</span></span> <span data-ttu-id="c253a-129">Ces métadonnées peuvent spécifier les types de télémétrie envoyés par l’appareil.</span><span class="sxs-lookup"><span data-stu-id="c253a-129">This metadata can specify the telemetry types the device sends.</span></span> <span data-ttu-id="c253a-130">Modifiez la valeur **deviceMetaData** dans le fichier remote_monitoring.js pour inclure une définition **Telemetry** à la suite de la définition **Commands**.</span><span class="sxs-lookup"><span data-stu-id="c253a-130">Modify the **deviceMetaData** value in the remote_monitoring.js file to include a **Telemetry** definition following the **Commands** definition.</span></span> <span data-ttu-id="c253a-131">L’extrait de code suivant illustre la définition **Commands** (veillez à ajouter un `,` après la définition **Commands**) :</span><span class="sxs-lookup"><span data-stu-id="c253a-131">The following code snippet shows the **Commands** definition (be sure to add a `,` after the **Commands** definition):</span></span>

```nodejs
'Commands': [{
  'Name': 'SetTemperature',
  'Parameters': [{
    'Name': 'Temperature',
    'Type': 'double'
  }]
},
{
  'Name': 'SetHumidity',
  'Parameters': [{
    'Name': 'Humidity',
    'Type': 'double'
  }]
}],
'Telemetry': [{
  'Name': 'Temperature',
  'Type': 'double'
},
{
  'Name': 'Humidity',
  'Type': 'double'
},
{
  'Name': 'ExternalTemperature',
  'Type': 'double'
}]
```

> [!NOTE]
> <span data-ttu-id="c253a-132">La solution de surveillance à distance utilise une correspondance non sensible à la casse pour comparer la définition des métadonnées avec les données du flux de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="c253a-132">The remote monitoring solution uses a case-insensitive match to compare the metadata definition with data in the telemetry stream.</span></span>


<span data-ttu-id="c253a-133">Le fait d’ajouter une définition **Telemetry** comme le montre l’extrait de code précédent ne modifie pas le comportement du tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="c253a-133">Adding a **Telemetry** definition as shown in the preceding code snippet does not change the behavior of the dashboard.</span></span> <span data-ttu-id="c253a-134">Cependant, les métadonnées peuvent également inclure un attribut **DisplayName** pour personnaliser l’affichage dans le tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="c253a-134">However, the metadata can also include a **DisplayName** attribute to customize the display in the dashboard.</span></span> <span data-ttu-id="c253a-135">Mettez à jour la définition des métadonnées **Telemetry** comme le montre l’extrait suivant :</span><span class="sxs-lookup"><span data-stu-id="c253a-135">Update the **Telemetry** metadata definition as shown in the following snippet:</span></span>

```nodejs
'Telemetry': [
{
  'Name': 'Temperature',
  'Type': 'double',
  'DisplayName': 'Temperature (C*)'
},
{
  'Name': 'Humidity',
  'Type': 'double',
  'DisplayName': 'Humidity (relative)'
},
{
  'Name': 'ExternalTemperature',
  'Type': 'double',
  'DisplayName': 'Outdoor Temperature (C*)'
}
]
```

<span data-ttu-id="c253a-136">La capture d’écran suivante montre de quelle manière ce changement modifie la légende du graphique dans le tableau de bord :</span><span class="sxs-lookup"><span data-stu-id="c253a-136">The following screenshot shows how this change modifies the chart legend on the dashboard:</span></span>

![Personnaliser la légende du graphique][image4]

> [!NOTE]
> <span data-ttu-id="c253a-138">Vous devrez peut-être désactiver, puis activer l’appareil Node.js sur la page **Appareils** du tableau de bord pour afficher immédiatement les changements.</span><span class="sxs-lookup"><span data-stu-id="c253a-138">You may need to disable and then enable the Node.js device on the **Devices** page in the dashboard to see the change immediately.</span></span>

## <a name="filter-the-telemetry-types"></a><span data-ttu-id="c253a-139">Filtrer les types de télémétrie</span><span class="sxs-lookup"><span data-stu-id="c253a-139">Filter the telemetry types</span></span>

<span data-ttu-id="c253a-140">Par défaut, le graphique du tableau de bord affiche toutes les séries de données dans le flux de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="c253a-140">By default, the chart on the dashboard shows every data series in the telemetry stream.</span></span> <span data-ttu-id="c253a-141">Vous pouvez utiliser les métadonnées **Device-Info** pour supprimer l’affichage des types de télémétrie spécifiques sur le graphique.</span><span class="sxs-lookup"><span data-stu-id="c253a-141">You can use the **Device-Info** metadata to suppress the display of specific telemetry types on the chart.</span></span> 

<span data-ttu-id="c253a-142">Pour que le graphique affiche uniquement la télémétrie de température et d’humidité, omettez **ExternalTemperature** dans les métadonnées **Telemetry** **Device-Info** comme suit :</span><span class="sxs-lookup"><span data-stu-id="c253a-142">To make the chart show only Temperature and Humidity telemetry, omit **ExternalTemperature** from the **Device-Info** **Telemetry** metadata as follows:</span></span>

```nodejs
'Telemetry': [
{
  'Name': 'Temperature',
  'Type': 'double',
  'DisplayName': 'Temperature (C*)'
},
{
  'Name': 'Humidity',
  'Type': 'double',
  'DisplayName': 'Humidity (relative)'
},
//{
//  'Name': 'ExternalTemperature',
//  'Type': 'double',
//  'DisplayName': 'Outdoor Temperature (C*)'
//}
]
```

<span data-ttu-id="c253a-143">**Outdoor Temperature** (Température externe) ne s’affiche plus dans le graphique :</span><span class="sxs-lookup"><span data-stu-id="c253a-143">The **Outdoor Temperature** no longer displays on the chart:</span></span>

![Filtrer la télémétrie sur le tableau de bord][image5]

<span data-ttu-id="c253a-145">Cette modification affecte uniquement l’affichage du graphique.</span><span class="sxs-lookup"><span data-stu-id="c253a-145">This change only affects the chart display.</span></span> <span data-ttu-id="c253a-146">Les données **ExternalTemperature** sont toujours stockées et mises à disposition pour le traitement principal, quel qu’il soit.</span><span class="sxs-lookup"><span data-stu-id="c253a-146">The **ExternalTemperature** data values are still stored and made available for any backend processing.</span></span>

> [!NOTE]
> <span data-ttu-id="c253a-147">Vous devrez peut-être désactiver, puis activer l’appareil Node.js sur la page **Appareils** du tableau de bord pour afficher immédiatement les changements.</span><span class="sxs-lookup"><span data-stu-id="c253a-147">You may need to disable and then enable the Node.js device on the **Devices** page in the dashboard to see the change immediately.</span></span>

## <a name="handle-errors"></a><span data-ttu-id="c253a-148">des erreurs</span><span class="sxs-lookup"><span data-stu-id="c253a-148">Handle errors</span></span>

<span data-ttu-id="c253a-149">Pour qu’un flux de données s’affiche sur le graphique, son **Type** dans les métadonnées **Device-Info** doit correspondre au type de données des valeurs de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="c253a-149">For a data stream to display on the chart, its **Type** in the **Device-Info** metadata must match the data type of the telemetry values.</span></span> <span data-ttu-id="c253a-150">Par exemple, si les métadonnées spécifient que le **Type** de données d’humidité est **int** et qu’un **double** est trouvé dans le flux de télémétrie, la télémétrie d’humidité ne s’affiche pas sur le graphique.</span><span class="sxs-lookup"><span data-stu-id="c253a-150">For example, if the metadata specifies that the **Type** of humidity data is **int** and a **double** is found in the telemetry stream then the humidity telemetry does not display on the chart.</span></span> <span data-ttu-id="c253a-151">Toutefois, les valeurs **d’humidité** sont toujours stockées et mises à disposition pour le traitement principal, quel qu’il soit.</span><span class="sxs-lookup"><span data-stu-id="c253a-151">However, the **Humidity** values are still stored and made available for any back-end processing.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c253a-152">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c253a-152">Next steps</span></span>

<span data-ttu-id="c253a-153">Maintenant que vous savez comment utiliser la télémétrie dynamique, vous pouvez en savoir plus sur la manière dont les solutions préconfigurées utilisent les informations d’appareil : [Métadonnées relatives aux informations d’appareil dans la solution préconfigurée de surveillance à distance][lnk-devinfo].</span><span class="sxs-lookup"><span data-stu-id="c253a-153">Now that you've seen how to use dynamic telemetry, you can learn more about how the preconfigured solutions use device information: [Device information metadata in the remote monitoring preconfigured solution][lnk-devinfo].</span></span>

[lnk-devinfo]: iot-suite-remote-monitoring-device-info.md

[image3]: media/iot-suite-dynamic-telemetry/image3.png
[image4]: media/iot-suite-dynamic-telemetry/image4.png
[image5]: media/iot-suite-dynamic-telemetry/image5.png

[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-node]: http://nodejs.org
