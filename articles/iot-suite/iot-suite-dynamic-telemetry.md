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
# <a name="use-dynamic-telemetry-with-hello-remote-monitoring-preconfigured-solution"></a>Utiliser la télémétrie dynamique avec hello solution préconfigurée de surveillance à distance

Télémétrie dynamique permet de vous toovisualize tout toohello de télémétrie envoyé solution préconfigurée de surveillance à distance. périphériques Hello simulée déploiement avec hello préconfiguré solution envoient la télémétrie des température et humidité, ce qui vous permet de visualiser dans le tableau de bord hello. Si vous personnalisez les simulations de périphériques existants, créer de nouveaux périphériques simulés ou connecter solution toohello préconfiguré de périphériques physiques vous pouvez envoyer d’autres valeurs de données de télémétrie telles que la température externe de hello, RPM ou vitesse du vent. Vous pouvez ensuite visualiser ces données de télémétrie supplémentaires sur le tableau de bord hello.

Ce didacticiel utilise un appareil simulé Node.js simple que vous pouvez facilement modifier tooexperiment avec les données de télémétrie dynamique.

toocomplete ce didacticiel, vous devez :

* Un abonnement Azure actif. Si vous ne possédez pas de compte, vous pouvez créer un compte d’évaluation gratuit en quelques minutes. Pour plus d’informations, consultez la rubrique [Version d’évaluation gratuite d’Azure][lnk_free_trial].
* [Node.js][lnk-node] version 0.12.x ou ultérieure.

Vous pouvez suivre ce didacticiel sur n’importe quel système d’exploitation (par exemple, Windows ou Linux) où vous pouvez installer Node.js.

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

[!INCLUDE [iot-suite-send-external-temperature](../../includes/iot-suite-send-external-temperature.md)]

## <a name="add-a-telemetry-type"></a>Ajouter un type de télémétrie

étape suivante de Hello est télémétrie de hello tooreplace généré par appareil simulé de hello Node.js avec un nouveau jeu de valeurs :

1. APPAREIL simulé Node.js hello STOP en tapant **Ctrl + C** dans votre invite de commandes ou d’un interpréteur de commandes.
2. Dans le fichier de remote_monitoring.js hello, vous pouvez voir hello des valeurs de base de données de température existant de hello, humidité et télémétrie de température externe. Ajoutez une valeur de données de base pour **rpm** comme suit :

    ```nodejs
    // Sensors data
    var temperature = 50;
    var humidity = 50;
    var externalTemperature = 55;
    var rpm = 200;
    ```

3. APPAREIL simulé de Node.js Hello utilise hello **generateRandomIncrement** de fonction dans hello remote_monitoring.js fichier tooadd un toohello incrément aléatoire des valeurs de base de données. Rendre aléatoire hello **rpm** valeur en ajoutant une ligne de code après randomisations existant de hello comme suit :

    ```nodejs
    temperature += generateRandomIncrement();
    externalTemperature += generateRandomIncrement();
    humidity += generateRandomIncrement();
    rpm += generateRandomIncrement();
    ```

4. Ajoutez hello nouvelle rpm valeur toohello JSON charge utile hello appareil envoie tooIoT Hub :

    ```nodejs
    var data = JSON.stringify({
      'DeviceID': deviceId,
      'Temperature': temperature,
      'Humidity': humidity,
      'ExternalTemperature': externalTemperature,
      'RPM': rpm
    });
    ```

5. Exécutez les appareil simulé Node.js hello à l’aide de hello de commande suivante :

    `node remote_monitoring.js`

6. Observez hello nouveau RPM télémétrie type qui s’affiche sur le graphique de hello dans le tableau de bord hello :

![Ajouter le tableau de bord toohello tr/min][image3]

> [!NOTE]
> Vous pouvez peut-être toodisable, puis activer le dispositif de Node.js hello hello **périphériques** page hello du tableau de bord toosee hello modification immédiatement.

## <a name="customize-hello-dashboard-display"></a>Personnaliser l’affichage du tableau de bord hello

Hello **informations de périphérique** message peut inclure des métadonnées sur les données de télémétrie hello appareil de hello peut envoyer des tooIoT Hub. Ces métadonnées peuvent spécifier les types de données de télémétrie hello hello appareil envoie. Modifier hello **deviceMetaData** valeur hello remote_monitoring.js fichier tooinclude un **télémétrie** définition suivant hello **commandes** définition. Hello extrait de code suivant montre hello **commandes** définition (être tooadd vraiment une `,` après hello **commandes** définition) :

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
> solution de surveillance à distance Hello utilise une définition de métadonnées de la casse toocompare hello avec des données dans le flux de données de télémétrie hello.


Ajout d’un **télémétrie** définition, comme indiqué dans hello précédente extrait de code ne modifie pas le comportement de hello du tableau de bord hello. Toutefois, les métadonnées de hello peuvent également inclure un **DisplayName** affichage de hello toocustomize dans le tableau de bord hello d’attribut. Hello de mise à jour **télémétrie** définition de métadonnées comme indiqué dans hello suivant extrait de code :

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

Hello capture d’écran suivante montre comment cette modification modifie la légende du graphique sur le tableau de bord hello hello :

![Personnaliser la légende du graphique hello][image4]

> [!NOTE]
> Vous pouvez peut-être toodisable, puis activer le dispositif de Node.js hello hello **périphériques** page hello du tableau de bord toosee hello modification immédiatement.

## <a name="filter-hello-telemetry-types"></a>Filtrer les types de données de télémétrie hello

Par défaut, le graphique hello sur le tableau de bord hello affiche chaque série de données dans le flux de données de télémétrie hello. Vous pouvez utiliser hello **informations de périphérique** toosuppress de métadonnées hello l’affichage des types de données de télémétrie spécifique sur le graphique de hello. 

graphique de hello toomake afficher uniquement les télémétrie température et humidité, omettez **ExternalTemperature** de hello **informations de périphérique** **télémétrie** métadonnées comme suit :

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

Hello **température extérieur** ne s’affiche plus dans le graphique de hello :

![Filtrer la télémétrie hello sur tableau de bord hello][image5]

Cette modification affecte uniquement l’affichage du graphique hello. Hello **ExternalTemperature** des valeurs de données sont toujours stockés et disponibles pour tout traitement principal.

> [!NOTE]
> Vous pouvez peut-être toodisable, puis activer le dispositif de Node.js hello hello **périphériques** page hello du tableau de bord toosee hello modification immédiatement.

## <a name="handle-errors"></a>des erreurs

Pour un toodisplay de flux de données sur le graphique de hello, son **Type** Bonjour **informations de périphérique** métadonnées doivent correspondre au type de données hello des valeurs de données de télémétrie hello. Par exemple, si hello métadonnées spécifient que hello **Type** de l’humidité, les données sont **int** et un **double** se trouve dans le flux de données de télémétrie hello ne de télémétrie de humidité hello pas d’affichage sur le graphique de hello. Toutefois, hello **humidité** les valeurs sont toujours stockées et mises à disposition pour tout traitement principal.

## <a name="next-steps"></a>Étapes suivantes

Maintenant que vous avez vu comment toouse de télémétrie dynamique, vous pouvez en savoir plus sur comment hello préconfiguré solutions utilisent les informations de périphérique : [solution préconfigurée de métadonnées informations de périphérique dans le contrôle à distance hello] [ lnk-devinfo].

[lnk-devinfo]: iot-suite-remote-monitoring-device-info.md

[image3]: media/iot-suite-dynamic-telemetry/image3.png
[image4]: media/iot-suite-dynamic-telemetry/image4.png
[image5]: media/iot-suite-dynamic-telemetry/image5.png

[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-node]: http://nodejs.org
