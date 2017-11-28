---
title: "données de télémétrie dynamique aaaUse | Documents Microsoft"
description: "Suivez ce didacticiel toolearn comment toouse de télémétrie dynamique avec l’analyse à distance hello Azure IoT Suite solution préconfigurée."
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
ms.openlocfilehash: 06cb2a370b67b4950efdfa4c7d906ac92106f4a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-dynamic-telemetry-with-hello-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="c581f-103">Utiliser la télémétrie dynamique avec hello solution préconfigurée de surveillance à distance</span><span class="sxs-lookup"><span data-stu-id="c581f-103">Use dynamic telemetry with hello remote monitoring preconfigured solution</span></span>

<span data-ttu-id="c581f-104">Télémétrie dynamique permet de vous toovisualize tout toohello de télémétrie envoyé solution préconfigurée de surveillance à distance.</span><span class="sxs-lookup"><span data-stu-id="c581f-104">Dynamic telemetry enables you toovisualize any telemetry sent toohello remote monitoring preconfigured solution.</span></span> <span data-ttu-id="c581f-105">périphériques Hello simulée déploiement avec hello préconfiguré solution envoient la télémétrie des température et humidité, ce qui vous permet de visualiser dans le tableau de bord hello.</span><span class="sxs-lookup"><span data-stu-id="c581f-105">hello simulated devices that deploy with hello preconfigured solution send temperature and humidity telemetry, which you can visualize on hello dashboard.</span></span> <span data-ttu-id="c581f-106">Si vous personnalisez les simulations de périphériques existants, créer de nouveaux périphériques simulés ou connecter solution toohello préconfiguré de périphériques physiques vous pouvez envoyer d’autres valeurs de données de télémétrie telles que la température externe de hello, RPM ou vitesse du vent.</span><span class="sxs-lookup"><span data-stu-id="c581f-106">If you customize existing simulated devices, create new simulated devices, or connect physical devices toohello preconfigured solution you can send other telemetry values such as hello external temperature, RPM, or windspeed.</span></span> <span data-ttu-id="c581f-107">Vous pouvez ensuite visualiser ces données de télémétrie supplémentaires sur le tableau de bord hello.</span><span class="sxs-lookup"><span data-stu-id="c581f-107">You can then visualize this additional telemetry on hello dashboard.</span></span>

<span data-ttu-id="c581f-108">Ce didacticiel utilise un appareil simulé Node.js simple que vous pouvez facilement modifier tooexperiment avec les données de télémétrie dynamique.</span><span class="sxs-lookup"><span data-stu-id="c581f-108">This tutorial uses a simple Node.js simulated device that you can easily modify tooexperiment with dynamic telemetry.</span></span>

<span data-ttu-id="c581f-109">toocomplete ce didacticiel, vous devez :</span><span class="sxs-lookup"><span data-stu-id="c581f-109">toocomplete this tutorial, you’ll need:</span></span>

* <span data-ttu-id="c581f-110">Un abonnement Azure actif.</span><span class="sxs-lookup"><span data-stu-id="c581f-110">An active Azure subscription.</span></span> <span data-ttu-id="c581f-111">Si vous ne possédez pas de compte, vous pouvez créer un compte d’évaluation gratuit en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="c581f-111">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="c581f-112">Pour plus d’informations, consultez la rubrique [Version d’évaluation gratuite d’Azure][lnk_free_trial].</span><span class="sxs-lookup"><span data-stu-id="c581f-112">For details, see [Azure Free Trial][lnk_free_trial].</span></span>
* <span data-ttu-id="c581f-113">[Node.js][lnk-node] version 0.12.x ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="c581f-113">[Node.js][lnk-node] version 0.12.x or later.</span></span>

<span data-ttu-id="c581f-114">Vous pouvez suivre ce didacticiel sur n’importe quel système d’exploitation (par exemple, Windows ou Linux) où vous pouvez installer Node.js.</span><span class="sxs-lookup"><span data-stu-id="c581f-114">You can complete this tutorial on any operating system, such as Windows or Linux, where you can install Node.js.</span></span>

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

[!INCLUDE [iot-suite-send-external-temperature](../../includes/iot-suite-send-external-temperature.md)]

## <a name="add-a-telemetry-type"></a><span data-ttu-id="c581f-115">Ajouter un type de télémétrie</span><span class="sxs-lookup"><span data-stu-id="c581f-115">Add a telemetry type</span></span>

<span data-ttu-id="c581f-116">étape suivante de Hello est télémétrie de hello tooreplace généré par appareil simulé de hello Node.js avec un nouveau jeu de valeurs :</span><span class="sxs-lookup"><span data-stu-id="c581f-116">hello next step is tooreplace hello telemetry generated by hello Node.js simulated device with a new set of values:</span></span>

1. <span data-ttu-id="c581f-117">APPAREIL simulé Node.js hello STOP en tapant **Ctrl + C** dans votre invite de commandes ou d’un interpréteur de commandes.</span><span class="sxs-lookup"><span data-stu-id="c581f-117">Stop hello Node.js simulated device by typing **Ctrl+C** in your command prompt or shell.</span></span>
2. <span data-ttu-id="c581f-118">Dans le fichier de remote_monitoring.js hello, vous pouvez voir hello des valeurs de base de données de température existant de hello, humidité et télémétrie de température externe.</span><span class="sxs-lookup"><span data-stu-id="c581f-118">In hello remote_monitoring.js file, you can see hello base data values for hello existing temperature, humidity, and external temperature telemetry.</span></span> <span data-ttu-id="c581f-119">Ajoutez une valeur de données de base pour **rpm** comme suit :</span><span class="sxs-lookup"><span data-stu-id="c581f-119">Add a base data value for **rpm** as follows:</span></span>

    ```nodejs
    // Sensors data
    var temperature = 50;
    var humidity = 50;
    var externalTemperature = 55;
    var rpm = 200;
    ```

3. <span data-ttu-id="c581f-120">APPAREIL simulé de Node.js Hello utilise hello **generateRandomIncrement** de fonction dans hello remote_monitoring.js fichier tooadd un toohello incrément aléatoire des valeurs de base de données.</span><span class="sxs-lookup"><span data-stu-id="c581f-120">hello Node.js simulated device uses hello **generateRandomIncrement** function in hello remote_monitoring.js file tooadd a random increment toohello base data values.</span></span> <span data-ttu-id="c581f-121">Rendre aléatoire hello **rpm** valeur en ajoutant une ligne de code après randomisations existant de hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="c581f-121">Randomize hello **rpm** value by adding a line of code after hello existing randomizations as follows:</span></span>

    ```nodejs
    temperature += generateRandomIncrement();
    externalTemperature += generateRandomIncrement();
    humidity += generateRandomIncrement();
    rpm += generateRandomIncrement();
    ```

4. <span data-ttu-id="c581f-122">Ajoutez hello nouvelle rpm valeur toohello JSON charge utile hello appareil envoie tooIoT Hub :</span><span class="sxs-lookup"><span data-stu-id="c581f-122">Add hello new rpm value toohello JSON payload hello device sends tooIoT Hub:</span></span>

    ```nodejs
    var data = JSON.stringify({
      'DeviceID': deviceId,
      'Temperature': temperature,
      'Humidity': humidity,
      'ExternalTemperature': externalTemperature,
      'RPM': rpm
    });
    ```

5. <span data-ttu-id="c581f-123">Exécutez les appareil simulé Node.js hello à l’aide de hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="c581f-123">Run hello Node.js simulated device using hello following command:</span></span>

    `node remote_monitoring.js`

6. <span data-ttu-id="c581f-124">Observez hello nouveau RPM télémétrie type qui s’affiche sur le graphique de hello dans le tableau de bord hello :</span><span class="sxs-lookup"><span data-stu-id="c581f-124">Observe hello new RPM telemetry type that displays on hello chart in hello dashboard:</span></span>

![Ajouter le tableau de bord toohello tr/min][image3]

> [!NOTE]
> <span data-ttu-id="c581f-126">Vous pouvez peut-être toodisable, puis activer le dispositif de Node.js hello hello **périphériques** page hello du tableau de bord toosee hello modification immédiatement.</span><span class="sxs-lookup"><span data-stu-id="c581f-126">You may need toodisable and then enable hello Node.js device on hello **Devices** page in hello dashboard toosee hello change immediately.</span></span>

## <a name="customize-hello-dashboard-display"></a><span data-ttu-id="c581f-127">Personnaliser l’affichage du tableau de bord hello</span><span class="sxs-lookup"><span data-stu-id="c581f-127">Customize hello dashboard display</span></span>

<span data-ttu-id="c581f-128">Hello **informations de périphérique** message peut inclure des métadonnées sur les données de télémétrie hello appareil de hello peut envoyer des tooIoT Hub.</span><span class="sxs-lookup"><span data-stu-id="c581f-128">hello **Device-Info** message can include metadata about hello telemetry hello device can send tooIoT Hub.</span></span> <span data-ttu-id="c581f-129">Ces métadonnées peuvent spécifier les types de données de télémétrie hello hello appareil envoie.</span><span class="sxs-lookup"><span data-stu-id="c581f-129">This metadata can specify hello telemetry types hello device sends.</span></span> <span data-ttu-id="c581f-130">Modifier hello **deviceMetaData** valeur hello remote_monitoring.js fichier tooinclude un **télémétrie** définition suivant hello **commandes** définition.</span><span class="sxs-lookup"><span data-stu-id="c581f-130">Modify hello **deviceMetaData** value in hello remote_monitoring.js file tooinclude a **Telemetry** definition following hello **Commands** definition.</span></span> <span data-ttu-id="c581f-131">Hello extrait de code suivant montre hello **commandes** définition (être tooadd vraiment une `,` après hello **commandes** définition) :</span><span class="sxs-lookup"><span data-stu-id="c581f-131">hello following code snippet shows hello **Commands** definition (be sure tooadd a `,` after hello **Commands** definition):</span></span>

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
> <span data-ttu-id="c581f-132">solution de surveillance à distance Hello utilise une définition de métadonnées de la casse toocompare hello avec des données dans le flux de données de télémétrie hello.</span><span class="sxs-lookup"><span data-stu-id="c581f-132">hello remote monitoring solution uses a case-insensitive match toocompare hello metadata definition with data in hello telemetry stream.</span></span>


<span data-ttu-id="c581f-133">Ajout d’un **télémétrie** définition, comme indiqué dans hello précédente extrait de code ne modifie pas le comportement de hello du tableau de bord hello.</span><span class="sxs-lookup"><span data-stu-id="c581f-133">Adding a **Telemetry** definition as shown in hello preceding code snippet does not change hello behavior of hello dashboard.</span></span> <span data-ttu-id="c581f-134">Toutefois, les métadonnées de hello peuvent également inclure un **DisplayName** affichage de hello toocustomize dans le tableau de bord hello d’attribut.</span><span class="sxs-lookup"><span data-stu-id="c581f-134">However, hello metadata can also include a **DisplayName** attribute toocustomize hello display in hello dashboard.</span></span> <span data-ttu-id="c581f-135">Hello de mise à jour **télémétrie** définition de métadonnées comme indiqué dans hello suivant extrait de code :</span><span class="sxs-lookup"><span data-stu-id="c581f-135">Update hello **Telemetry** metadata definition as shown in hello following snippet:</span></span>

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

<span data-ttu-id="c581f-136">Hello capture d’écran suivante montre comment cette modification modifie la légende du graphique sur le tableau de bord hello hello :</span><span class="sxs-lookup"><span data-stu-id="c581f-136">hello following screenshot shows how this change modifies hello chart legend on hello dashboard:</span></span>

![Personnaliser la légende du graphique hello][image4]

> [!NOTE]
> <span data-ttu-id="c581f-138">Vous pouvez peut-être toodisable, puis activer le dispositif de Node.js hello hello **périphériques** page hello du tableau de bord toosee hello modification immédiatement.</span><span class="sxs-lookup"><span data-stu-id="c581f-138">You may need toodisable and then enable hello Node.js device on hello **Devices** page in hello dashboard toosee hello change immediately.</span></span>

## <a name="filter-hello-telemetry-types"></a><span data-ttu-id="c581f-139">Filtrer les types de données de télémétrie hello</span><span class="sxs-lookup"><span data-stu-id="c581f-139">Filter hello telemetry types</span></span>

<span data-ttu-id="c581f-140">Par défaut, le graphique hello sur le tableau de bord hello affiche chaque série de données dans le flux de données de télémétrie hello.</span><span class="sxs-lookup"><span data-stu-id="c581f-140">By default, hello chart on hello dashboard shows every data series in hello telemetry stream.</span></span> <span data-ttu-id="c581f-141">Vous pouvez utiliser hello **informations de périphérique** toosuppress de métadonnées hello l’affichage des types de données de télémétrie spécifique sur le graphique de hello.</span><span class="sxs-lookup"><span data-stu-id="c581f-141">You can use hello **Device-Info** metadata toosuppress hello display of specific telemetry types on hello chart.</span></span> 

<span data-ttu-id="c581f-142">graphique de hello toomake afficher uniquement les télémétrie température et humidité, omettez **ExternalTemperature** de hello **informations de périphérique** **télémétrie** métadonnées comme suit :</span><span class="sxs-lookup"><span data-stu-id="c581f-142">toomake hello chart show only Temperature and Humidity telemetry, omit **ExternalTemperature** from hello **Device-Info** **Telemetry** metadata as follows:</span></span>

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

<span data-ttu-id="c581f-143">Hello **température extérieur** ne s’affiche plus dans le graphique de hello :</span><span class="sxs-lookup"><span data-stu-id="c581f-143">hello **Outdoor Temperature** no longer displays on hello chart:</span></span>

![Filtrer la télémétrie hello sur tableau de bord hello][image5]

<span data-ttu-id="c581f-145">Cette modification affecte uniquement l’affichage du graphique hello.</span><span class="sxs-lookup"><span data-stu-id="c581f-145">This change only affects hello chart display.</span></span> <span data-ttu-id="c581f-146">Hello **ExternalTemperature** des valeurs de données sont toujours stockés et disponibles pour tout traitement principal.</span><span class="sxs-lookup"><span data-stu-id="c581f-146">hello **ExternalTemperature** data values are still stored and made available for any backend processing.</span></span>

> [!NOTE]
> <span data-ttu-id="c581f-147">Vous pouvez peut-être toodisable, puis activer le dispositif de Node.js hello hello **périphériques** page hello du tableau de bord toosee hello modification immédiatement.</span><span class="sxs-lookup"><span data-stu-id="c581f-147">You may need toodisable and then enable hello Node.js device on hello **Devices** page in hello dashboard toosee hello change immediately.</span></span>

## <a name="handle-errors"></a><span data-ttu-id="c581f-148">des erreurs</span><span class="sxs-lookup"><span data-stu-id="c581f-148">Handle errors</span></span>

<span data-ttu-id="c581f-149">Pour un toodisplay de flux de données sur le graphique de hello, son **Type** Bonjour **informations de périphérique** métadonnées doivent correspondre au type de données hello des valeurs de données de télémétrie hello.</span><span class="sxs-lookup"><span data-stu-id="c581f-149">For a data stream toodisplay on hello chart, its **Type** in hello **Device-Info** metadata must match hello data type of hello telemetry values.</span></span> <span data-ttu-id="c581f-150">Par exemple, si hello métadonnées spécifient que hello **Type** de l’humidité, les données sont **int** et un **double** se trouve dans le flux de données de télémétrie hello ne de télémétrie de humidité hello pas d’affichage sur le graphique de hello.</span><span class="sxs-lookup"><span data-stu-id="c581f-150">For example, if hello metadata specifies that hello **Type** of humidity data is **int** and a **double** is found in hello telemetry stream then hello humidity telemetry does not display on hello chart.</span></span> <span data-ttu-id="c581f-151">Toutefois, hello **humidité** les valeurs sont toujours stockées et mises à disposition pour tout traitement principal.</span><span class="sxs-lookup"><span data-stu-id="c581f-151">However, hello **Humidity** values are still stored and made available for any back-end processing.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c581f-152">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c581f-152">Next steps</span></span>

<span data-ttu-id="c581f-153">Maintenant que vous avez vu comment toouse de télémétrie dynamique, vous pouvez en savoir plus sur comment hello préconfiguré solutions utilisent les informations de périphérique : [solution préconfigurée de métadonnées informations de périphérique dans le contrôle à distance hello] [ lnk-devinfo].</span><span class="sxs-lookup"><span data-stu-id="c581f-153">Now that you've seen how toouse dynamic telemetry, you can learn more about how hello preconfigured solutions use device information: [Device information metadata in hello remote monitoring preconfigured solution][lnk-devinfo].</span></span>

[lnk-devinfo]: iot-suite-remote-monitoring-device-info.md

[image3]: media/iot-suite-dynamic-telemetry/image3.png
[image4]: media/iot-suite-dynamic-telemetry/image4.png
[image5]: media/iot-suite-dynamic-telemetry/image5.png

[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-node]: http://nodejs.org
