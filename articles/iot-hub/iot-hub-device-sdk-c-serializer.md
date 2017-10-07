---
title: "aaaAzure, appareils IoT SDK pour C - sérialiseur | Documents Microsoft"
description: "La bibliothèque de sérialiseur toouse hello dans le dispositif hello Azure IoT SDK des applications d’appareil toocreate C qui communiquent avec un hub IoT."
services: iot-hub
documentationcenter: 
author: olivierbloch
manager: timlt
editor: 
ms.assetid: defbed34-de73-429c-8592-cd863a38e4dd
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/06/2016
ms.author: obloch
ms.openlocfilehash: c5776e9b50ffea71df96cb2d342ea2fc045f5a0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-device-sdk-for-c--more-about-serializer"></a>Kit de développement logiciel (SDK) Azure IoT device pour C : en savoir plus sur serializer
Hello [tout d’abord l’article](iot-hub-device-sdk-c-intro.md) cette Bonjour série introduites **appareil Azure IoT SDK pour C**. l’article suivant de hello fourni une description plus détaillée de hello [ **IoTHubClient** ](iot-hub-device-sdk-c-iothubclient.md). Cet article termine la couverture de hello SDK en fournissant une description plus détaillée de hello restante du composant : hello **sérialiseur** bibliothèque.

article de présentation Hello décrit comment toouse hello **sérialiseur** bibliothèque toosend événements tooand recevoir des messages à partir de IoT Hub. Dans cet article, nous étendre cette discussion, en fournissant une explication plus complète de la toomodel vos données avec hello **sérialiseur** langage de macro. Hello inclut également des détails supplémentaires à propos de la bibliothèque de hello sérialise des messages (et dans certains cas comment vous pouvez contrôler un comportement de sérialisation hello). Nous allons également décrire certains que vous pouvez modifier les paramètres qui déterminent la taille de hello de modèles hello que vous créez.

Enfin, l’article de hello revisite certaines rubriques abordées dans les articles précédents, tels que le message et la gestion de propriétés. Comme nous allons découvrir, ces fonctionnalités travail hello même à l’aide hello **sérialiseur** bibliothèque comme ils le font avec hello **IoTHubClient** bibliothèque.

Tous les éléments décrits dans cet article sont basé sur hello **sérialiseur** exemples SDK. Si vous souhaitez toofollow le long, consultez hello **simplesample\_amqp** et **simplesample\_http** applications incluses dans le dispositif de Azure IoT hello SDK pour C.

Vous pouvez trouver hello [ **appareil Azure IoT SDK pour C** ](https://github.com/Azure/azure-iot-sdk-c) GitHub référentiel et consulter les détails de hello API Bonjour [référence d’API C](https://azure.github.io/azure-iot-sdk-c/index.html).

## <a name="hello-modeling-language"></a>langage de modélisation Hello
Hello [article de présentation](iot-hub-device-sdk-c-intro.md) cette Bonjour série introduites **appareil Azure IoT SDK pour C** modélisation au moyen de l’exemple hello prévue hello **simplesample\_amqp**  application :

```
BEGIN_NAMESPACE(WeatherStation);

DECLARE_MODEL(ContosoAnemometer,
WITH_DATA(ascii_char_ptr, DeviceId),
WITH_DATA(double, WindSpeed),
WITH_ACTION(TurnFanOn),
WITH_ACTION(TurnFanOff),
WITH_ACTION(SetAirResistance, int, Position)
);

END_NAMESPACE(WeatherStation);
```

Comme vous pouvez le voir, hello langage de modélisation est basée sur les macros C. La définition commence toujours par **BEGIN\_NAMESPACE** et se termine toujours par **END\_NAMESPACE**. Il est commun tooname hello espace de noms pour votre société ou, comme dans cet exemple, le projet de hello sur lequel vous travaillez.

Ce qui se passe dans l’espace de noms hello sont des définitions de modèle. Dans ce cas, il s’agit d’un modèle unique pour un anémomètre. Une fois encore, modèle de hello peut être n’importe quel nom, mais en général, cela est nommé pour hello périphérique ou un type de données que vous souhaitez tooexchange IoT Hub.  

Les modèles contiennent une définition d’événements de hello, vous pouvez en entrée tooIoT concentrateur (hello *données*), ainsi que les messages hello vous pouvez recevoir de IoT Hub (hello *actions*). Comme vous pouvez le voir à partir de l’exemple de hello, les événements ont un type et un nom. actions ont un nom et des paramètres facultatifs (chacun avec un type).

N’est pas illustrée dans cet exemple sont des types de données supplémentaires qui sont prises en charge par le Kit de développement logiciel de hello. Nous allons aborder ce point par la suite.

> [!NOTE]
> IoT Hub fait référence à des données toohello un appareil envoie tooit comme *événements*, tandis que le langage de modélisation de hello fait référence tooit en tant que *données* (défini à l’aide **WITH_DATA**). De même, IoT Hub fait référence à des données toohello vous envoyez toodevices comme *messages*, tandis que le langage de modélisation de hello fait référence tooit en tant que *actions* (défini à l’aide **WITH_ACTION**). Sachez que ces termes peuvent être utilisés de manière interchangeable dans cet article.
> 
> 

### <a name="supported-data-types"></a>Types de données pris en charge
Hello, les types de données suivants est pris en charge dans les modèles créés avec hello **sérialiseur** bibliothèque :

| Type | Description |
| --- | --- |
| double |nombre à virgule flottante double précision |
| int |entier 32 bits |
| float |nombre à virgule flottante simple précision |
| long |entier long |
| int8\_t |entier 8 bits |
| int16\_t |entier 16 bits |
| int32\_t |entier 32 bits |
| int64\_t |entier 64 bits |
| valeur booléenne |booléenne |
| ascii\_char\_ptr |Chaîne ASCII |
| EDM\_DATE\_TIME\_OFFSET |décalage de date et d’heure |
| EDM\_GUID |GUID |
| EDM\_BINARY |binaire |
| DECLARE\_STRUCT |type de données complexe |

Commençons par type de données de dernière hello. Hello **DECLARE\_STRUCT** vous permet de types de données complexes toodefine, qui sont des groupements de hello autres types primitifs. Ces regroupements permettent nous toodefine un modèle qui ressemble à ceci :

```
DECLARE_STRUCT(TestType,
double, aDouble,
int, aInt,
float, aFloat,
long, aLong,
int8_t, aInt8,
uint8_t, auInt8,
int16_t, aInt16,
int32_t, aInt32,
int64_t, aInt64,
bool, aBool,
ascii_char_ptr, aAsciiCharPtr,
EDM_DATE_TIME_OFFSET, aDateTimeOffset,
EDM_GUID, aGuid,
EDM_BINARY, aBinary
);

DECLARE_MODEL(TestModel,
WITH_DATA(TestType, Test)
);
```

Notre modèle contient un événement de données unique de type **TestType**. **TestType** est un type complexe qui inclut plusieurs membres, qui illustrent la prise en charge par hello des types primitifs hello collectivement **sérialiseur** langage de modélisation.

Avec un modèle de ce type, nous pouvons écrire le code toosend données tooIoT Hub qui s’affiche comme suit :

```
TestModel* testModel = CREATE_MODEL_INSTANCE(MyThermostat, TestModel);

testModel->Test.aDouble = 1.1;
testModel->Test.aInt = 2;
testModel->Test.aFloat = 3.0f;
testModel->Test.aLong = 4;
testModel->Test.aInt8 = 5;
testModel->Test.auInt8 = 6;
testModel->Test.aInt16 = 7;
testModel->Test.aInt32 = 8;
testModel->Test.aInt64 = 9;
testModel->Test.aBool = true;
testModel->Test.aAsciiCharPtr = "ascii string 1";

time_t now;
time(&now);
testModel->Test.aDateTimeOffset = GetDateTimeOffset(now);

EDM_GUID guid = { { 0x00, 0x01, 0x02, 0x03, 0x04, 0x05, 0x06, 0x07, 0x08, 0x09, 0x0A, 0x0B, 0x0C, 0x0D, 0x0E, 0x0F } };
testModel->Test.aGuid = guid;

unsigned char binaryArray[3] = { 0x01, 0x02, 0x03 };
EDM_BINARY binaryData = { sizeof(binaryArray), &binaryArray };
testModel->Test.aBinary = binaryData;

SendAsync(iotHubClientHandle, (const void*)&(testModel->Test));
```

En fait, nous allons affectation membre tooevery valeur hello **Test** structure, puis en appelant **SendAsync** toosend hello **Test** données dans le cloud toohello événement. **SendAsync** est une fonction d’assistance qui envoie un tooIoT d’événement de données Hub :

```
void SendAsync(IOTHUB_CLIENT_LL_HANDLE iotHubClientHandle, const void *dataEvent)
{
    unsigned char* destination;
    size_t destinationSize;
    if (SERIALIZE(&destination, &destinationSize, *(const unsigned char*)dataEvent) ==
    {
        // null terminate hello string
        char* destinationAsString = (char*)malloc(destinationSize + 1);
        if (destinationAsString != NULL)
        {
            memcpy(destinationAsString, destination, destinationSize);
            destinationAsString[destinationSize] = '\0';
            IOTHUB_MESSAGE_HANDLE messageHandle = IoTHubMessage_CreateFromString(destinationAsString);
            if (messageHandle != NULL)
            {
                IoTHubClient_SendEventAsync(iotHubClientHandle, messageHandle, sendCallback, (void*)0);

                IoTHubMessage_Destroy(messageHandle);
            }
            free(destinationAsString);
        }
        free(destination);
    }
}
```

Cette fonction sérialise hello données événement donné et envoie tooIoT concentrateur à l’aide de **IoTHubClient\_SendEventAsync**. Il s’agit de hello même code présenté dans les articles précédents (**SendAsync** encapsule la logique de hello dans une fonction pratique).

Une autre fonction d’assistance utilisée dans le code précédent hello est **GetDateTimeOffset**. Cette fonction transforme hello moment donné en une valeur de type **EDM\_DATE\_temps\_décalage**:

```
EDM_DATE_TIME_OFFSET GetDateTimeOffset(time_t time)
{
    struct tm newTime;
    gmtime_s(&newTime, &time);
    EDM_DATE_TIME_OFFSET dateTimeOffset;
    dateTimeOffset.dateTime = newTime;
    dateTimeOffset.fractionalSecond = 0;
    dateTimeOffset.hasFractionalSecond = 0;
    dateTimeOffset.hasTimeZone = 0;
    dateTimeOffset.timeZoneHour = 0;
    dateTimeOffset.timeZoneMinute = 0;
    return dateTimeOffset;
}
```

Si vous exécutez ce code, hello suivant message est envoyé à tooIoT Hub :

```
{"aDouble":1.100000000000000, "aInt":2, "aFloat":3.000000, "aLong":4, "aInt8":5, "auInt8":6, "aInt16":7, "aInt32":8, "aInt64":9, "aBool":true, "aAsciiCharPtr":"ascii string 1", "aDateTimeOffset":"2015-09-14T21:18:21Z", "aGuid":"00010203-0405-0607-0809-0A0B0C0D0E0F", "aBinary":"AQID"}
```

Notez que la sérialisation de hello est JSON, qui est le format hello généré par hello **sérialiseur** bibliothèque. Notez que chaque membre de hello sérialisé objet JSON correspond également à des membres de hello Hello **TestType** que nous avons défini dans notre modèle. les valeurs Hello également correspondre exactement à celles utilisées dans le code hello. Toutefois, notez que les données binaires hello sont codée en base64 : « AQID » est hello encodage base64 de {0 x 01, 0 x 02, 0 x 03}.

Cet exemple montre comment présente l’avantage de hello hello **sérialiseur** bibliothèque--il nous permet de toosend JSON toohello cloud, sans avoir à tooexplicitly de gérer la sérialisation dans notre application. Il nous tooworry sur est valeurs de paramètre hello de hello événements de données dans notre modèle, puis à appeler simple API toosend ces cloud de toohello d’événements.

Avec ces informations, nous pouvons définir des modèles qui incluent la plage hello pris en charge des types de données, y compris les types complexes (nous avons même inclure des types complexes dans d’autres types complexes). Cependant, il a sérialisée JSON généré par hello exemple ci-dessus affiche un point important. *Comment* nous envoyer des données avec hello **sérialiseur** bibliothèque détermine exactement comment hello JSON est formé. C’est ce point particulier que nous allons ensuite aborder.

## <a name="more-about-serialization"></a>En savoir plus sur la sérialisation
section précédente de Hello met en évidence un exemple de sortie hello généré par hello **sérialiseur** bibliothèque. Dans cette section, nous expliquerons comment les bibliothèque hello sérialise les données et comment vous pouvez contrôler ce comportement à l’aide des API de sérialisation hello.

Dans la discussion hello du tooadvance ordre lors de la sérialisation, nous travaillons en collaboration avec un nouveau modèle basé sur un thermostat. Tout d’abord, nous allons fournir des informations générales sur le scénario de hello nous essayons de tooaddress.

Nous souhaitons toomodel un thermostat qui mesure la température et humidité. Chaque élément de données est en cours toobe envoyé tooIoT Hub différemment. Par défaut, hello ingresses de thermostat un événement de température toutes les 2 minutes ; un événement de l’humidité est ingressed toutes les 15 minutes. Lorsque l’événement est ingressed, elle doit inclure un horodatage qui indique les temps de hello que la température correspondante hello ou humidité a été mesurée.

Étant donné ce scénario, nous vous montrer les données de salutation toomodel deux façons différentes, et nous expliquerons effet hello que modélisation a hello sérialisée pour la sortie.

### <a name="model-1"></a>Modèle n° 1
Voici hello première version d’un modèle que prend en charge hello scénario précédent :

```
BEGIN_NAMESPACE(Contoso);

DECLARE_STRUCT(TemperatureEvent,
int, Temperature,
EDM_DATE_TIME_OFFSET, Time);

DECLARE_STRUCT(HumidityEvent,
int, Humidity,
EDM_DATE_TIME_OFFSET, Time);

DECLARE_MODEL(Thermostat,
WITH_DATA(TemperatureEvent, Temperature),
WITH_DATA(HumidityEvent, Humidity)
);

END_NAMESPACE(Contoso);
```

Notez que ce modèle hello inclut deux événements de données : **température** et **humidité**. Contrairement aux exemples précédents, type hello de chaque événement est une structure définie à l’aide de **DECLARE\_STRUCT**. **TemperatureEvent** comprend une mesure de température et un horodatage ; **HumidityEvent** contient une mesure d’humidité et un horodatage. Ce modèle nous offre un moyen naturel toomodel hello de données pour le scénario hello décrit ci-dessus. Lorsque nous envoyer un nuage de toohello d’événement, nous vous enverrons soit un température/horodatage ou une paire humidité/horodatage.

Nous pouvons envoyer un nuage de toohello température événement à l’aide de code tel que hello suivant :

```
time_t now;
time(&now);
thermostat->Temperature.Temperature = 75;
thermostat->Temperature.Time = GetDateTimeOffset(now);

unsigned char* destination;
size_t destinationSize;
if (SERIALIZE(&destination, &destinationSize, thermostat->Temperature) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

Nous verrons utiliser des valeurs codées en dur pour la température et humidité dans l’exemple de code hello, mais supposons que nous récupérons réellement ces valeurs en échantillonnant les capteurs de hello correspondant sur thermostat de hello.

code Hello ci-dessus utilise hello **GetDateTimeOffset** assistance qui a été introduit précédemment. Pour des raisons qui deviendront désactivez ultérieures, ce code sépare explicitement tâche hello de sérialisation et l’envoi d’événements de hello. code précédent de Hello sérialise les événements de température hello dans une mémoire tampon. Ensuite, **sendMessage** est une fonction d’assistance (inclus dans **simplesample\_amqp**) qu’envoie hello événement tooIoT Hub :

```
static void sendMessage(IOTHUB_CLIENT_HANDLE iotHubClientHandle, const unsigned char* buffer, size_t size)
{
    static unsigned int messageTrackingId;
    IOTHUB_MESSAGE_HANDLE messageHandle = IoTHubMessage_CreateFromByteArray(buffer, size);
    if (messageHandle != NULL)
    {
        IoTHubClient_SendEventAsync(iotHubClientHandle, messageHandle, sendCallback, (void*)(uintptr_t)messageTrackingId);

        IoTHubMessage_Destroy(messageHandle);
    }
    free((void*)buffer);
}
```

Ce code est un sous-ensemble de hello **SendAsync** helper décrite dans la section précédente de hello, donc nous n’allons pas dessus à nouveau ici.

Si nous exécutons hello code toosend hello température l’événement précédent, cette forme sérialisée de l’événement de hello est envoyée tooIoT Hub :

```
{"Temperature":75, "Time":"2015-09-17T18:45:56Z"}
```

Nous allons envoyer une température de type **TemperatureEvent** et cette structure contient un membre **Temperature** et **Time**. Cela se reflète directement dans les données de salutation sérialisée.

De même, nous pouvons envoyer un événement d’humidité avec ce code :

```
thermostat->Humidity.Humidity = 45;
thermostat->Humidity.Time = GetDateTimeOffset(now);
if (SERIALIZE(&destination, &destinationSize, thermostat->Humidity) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

écran Hello sérialisée qui a envoyé tooIoT Hub apparaît comme suit :

```
{"Humidity":45, "Time":"2015-09-17T18:45:56Z"}
```

Comme attendu, là encore.

Avec ce modèle, vous pouvez voir comment d’autres événements peuvent facilement être ajoutés. Vous définissez plusieurs structures à l’aide **DECLARE\_STRUCT**et inclure les événements correspondants hello dans à l’aide du modèle hello **WITH\_données**.

Maintenant, nous allons modifier le modèle de hello afin qu’il inclue hello mêmes données, mais avec une structure différente.

### <a name="model-2"></a>Modèle n° 2
Prenez en compte cette toohello autre modèle une ci-dessus :

```
DECLARE_MODEL(Thermostat,
WITH_DATA(int, Temperature),
WITH_DATA(int, Humidity),
WITH_DATA(EDM_DATE_TIME_OFFSET, Time)
);
```

Dans ce cas, nous avons éliminé hello **DECLARE\_STRUCT** macros et définissez simplement les éléments de données hello dans notre scénario à l’aide de types simples à partir du langage de modélisation de hello.

Juste pour le moment de hello, nous allons ignorer hello **temps** événement. Avec ce aside, voici hello code tooingress **température**:

```
time_t now;
time(&now);
thermostat->Temperature = 75;

unsigned char* destination;
size_t destinationSize;
if (SERIALIZE(&destination, &destinationSize, thermostat->Temperature) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

Ce code envoie suivant de hello sérialisé événement tooIoT Hub :

```
{"Temperature":75}
```

Et code hello pour envoyer des événements de humidité hello apparaît comme suit :

```
thermostat->Humidity = 45;
if (SERIALIZE(&destination, &destinationSize, thermostat->Humidity) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

Ce code envoie cette tooIoT Hub :

```
{"Humidity":45}
```

Jusqu’à présent, toujours pas de surprise. Maintenant nous allons modifier comment nous utilisons la macro SERIALIZE hello.

Hello **SERIALIZE** macro peut prendre plusieurs événements de données en tant qu’arguments. Cela nous permet de tooserialize hello **température** et **humidité** ensemble d’événements et les envoyer tooIoT concentrateur dans un seul appel :

```
if (SERIALIZE(&destination, &destinationSize, thermostat->Temperature, thermostat->Humidity) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

Vous pouvez le deviner que le résultat hello de ce code est que les événements de deux fichiers de données sont envoyés tooIoT Hub :

[

{"Temperature":75},

{"Humidity":45}

]

En d’autres termes, vous pouvez attendre que ce code est hello même que l’envoi de **température** et **humidité** séparément. Il est simplement un toopass commodité les deux événements trop**SERIALIZE** Bonjour même appeler. Toutefois, qui n’est pas le cas de hello. Au lieu de cela, le code hello ci-dessus envoie cette tooIoT d’événement de données concentrateur :

{"Temperature":75, "Humidity":45}

Cela peut sembler étrange, étant donné que notre modèle définit **Temperature** et **Humidity** comme deux événements *distincts* :

```
DECLARE_MODEL(Thermostat,
WITH_DATA(int, Temperature),
WITH_DATA(int, Humidity),
WITH_DATA(EDM_DATE_TIME_OFFSET, Time)
);
```

Point toohello, nous n’a pas de modèle ces événements où **température** et **humidité** sont Bonjour même structure :

```
DECLARE_STRUCT(TemperatureAndHumidityEvent,
int, Temperature,
int, Humidity,
);

DECLARE_MODEL(Thermostat,
WITH_DATA(TemperatureAndHumidityEvent, TemperatureAndHumidity),
);
```

Si nous utilisons ce modèle, il serait plus facile toounderstand comment **température** et **humidité** seraient envoyées Bonjour même message sérialisé. Toutefois peut-être pas clairement pourquoi il fonctionne de cette façon, lorsque vous transmettez les deux événements de données trop**SERIALIZE** à l’aide du modèle de 2.

Ce comportement est toounderstand plus facile si vous connaissez les hypothèses hello que hello **sérialiseur** apporte de la bibliothèque. toomake décryptage passons tooour précédent modèle :

```
DECLARE_MODEL(Thermostat,
WITH_DATA(int, Temperature),
WITH_DATA(int, Humidity),
WITH_DATA(EDM_DATE_TIME_OFFSET, Time)
);
```

Pensez à ce modèle en tant que modèle orienté objets. Dans ce cas, nous allons modéliser un appareil physique (un thermostat) et cet appareil comprend des attributs tels que **Temperature** et **Humidity**.

Nous pouvons envoyer un état d’entier hello de notre modèle avec le code suivant de hello :

```
if (SERIALIZE(&destination, &destinationSize, thermostat->Temperature, thermostat->Humidity, thermostat->Time) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

En supposant que les valeurs hello de température, humidité et l’heure sont définies, nous verriez un événement comme cette tooIoT envoyé Hub :

```
{"Temperature":75, "Humidity":45, "Time":"2015-09-17T18:45:56Z"}
```

Parfois, vous pouvez souhaiter que toosend *certains* propriétés du cloud de toohello modèle hello (cela est particulièrement vrai si votre modèle contient un grand nombre d’événements de données). Il est utile toosend uniquement un sous-ensemble d’événements de données, comme dans notre précédent exemple :

```
{"Temperature":75, "Time":"2015-09-17T18:45:56Z"}
```

Cette opération génère exactement hello même sérialisée des événements comme si nous avions défini un **TemperatureEvent** avec un **température** et **temps** membre, comme nous avec modèle 1. Dans ce cas, nous avons pu toogenerate exactement hello même sérialisé événement à l’aide d’un autre modèle (2), car nous avons appelé **SERIALIZE** d’une manière différente.

Hello point important est que si vous passez plusieurs événements de données trop**SERIALIZE,** puis il suppose que chaque événement est une propriété dans un seul objet JSON.

Hello meilleure approche dépend de vous et comment vous réfléchissez à votre modèle. Si vous l’envoyez « événements » toohello cloud et chaque événement contient un ensemble défini de propriétés, première approche de hello rend très utile. Dans ce cas, vous utiliseriez **DECLARE\_STRUCT** toodefine hello la structure de chaque événement et les inclure dans votre modèle avec hello **WITH\_données** (macro). Puis vous envoyez chaque événement comme dans le premier exemple hello ci-dessus. Dans cette approche vous pouvez uniquement passer un événement de données trop**sérialiseur**.

Si vous pensez que sur votre modèle de manière orientée objet, puis deuxième approche de hello peut-être répondre à vous. Hello dans ce cas, les éléments définis à l’aide de **WITH\_données** hello « propriétés » de votre objet. Vous passez le sous-ensemble d’événements trop**SERIALIZE** que vous le souhaitez, en fonction de la part de vos état de l’objet « » vous toosend toohello cloud.

Aucune approche n’est meilleure que l’autre. Soyez conscient de façon hello **sérialiseur** fonctionne de la bibliothèque et une nouvelle approche de modélisation hello choix qui répond le mieux à vos besoins.

## <a name="message-handling"></a>Gestion des messages
Jusqu'à présent cet article a traité uniquement envoi événements tooIoT Hub et n’a pas traité la réception des messages. Hello raison pour ce qui est ce que nous devons tooknow sur la réception des messages a principalement été traité dans un [précédemment article](iot-hub-device-sdk-c-intro.md). Rappel de cet article : vous traitez les messages en enregistrant une fonction de rappel de message :

```
IoTHubClient_SetMessageCallback(iotHubClientHandle, IoTHubMessage, myWeather)
```

Vous écrivez ensuite la fonction de rappel hello est appelée lorsqu’un message est reçu :

```
static IOTHUBMESSAGE_DISPOSITION_RESULT IoTHubMessage(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    IOTHUBMESSAGE_DISPOSITION_RESULT result;
    const unsigned char* buffer;
    size_t size;
    if (IoTHubMessage_GetByteArray(message, &buffer, &size) != IOTHUB_MESSAGE_OK)
    {
        printf("unable tooIoTHubMessage_GetByteArray\r\n");
        result = EXECUTE_COMMAND_ERROR;
    }
    else
    {
        /*buffer is not zero terminated*/
        char* temp = malloc(size + 1);
        if (temp == NULL)
        {
            printf("failed toomalloc\r\n");
            result = EXECUTE_COMMAND_ERROR;
        }
        else
        {
            memcpy(temp, buffer, size);
            temp[size] = '\0';
            EXECUTE_COMMAND_RESULT executeCommandResult = EXECUTE_COMMAND(userContextCallback, temp);
            result =
                (executeCommandResult == EXECUTE_COMMAND_ERROR) ? IOTHUBMESSAGE_ABANDONED :
                (executeCommandResult == EXECUTE_COMMAND_SUCCESS) ? IOTHUBMESSAGE_ACCEPTED :
                IOTHUBMESSAGE_REJECTED;
            free(temp);
        }
    }
    return result;
}
```

Cette implémentation de **IoTHubMessage** appels hello fonction spécifique pour chaque action dans votre modèle. Par exemple, si votre modèle définit cette action :

```
WITH_ACTION(SetAirResistance, int, Position)
```

Vous devez définir une fonction avec cette signature :

```
EXECUTE_COMMAND_RESULT SetAirResistance(ContosoAnemometer* device, int Position)
{
    (void)device;
    (void)printf("Setting Air Resistance Position too%d.\r\n", Position);
    return EXECUTE_COMMAND_SUCCESS;
}
```

**SetAirResistance** est ensuite appelé lorsque ce message est envoyé à tooyour appareil.

Nous n’avons pas expliqué est encore version hello sérialisé de message ressemble. En d’autres termes, si vous voulez toosend un **SetAirResistance** périphérique tooyour de message, ce qui, qui recherchent ?

Si vous envoyez un périphérique tooa de message, vous le faites via le SDK du service de Azure IoT hello. Vous devez toujours tooknow quelle chaîne toosend tooinvoke une action particulière. format général de Hello pour envoyer un message s’affiche comme suit :

```
{"Name" : "", "Parameters" : "" }
```

Vous envoyez un objet JSON sérialisé avec deux propriétés : **nom** hello désigne l’action hello (message) et **paramètres** contient des paramètres hello de cette action.

Par exemple, tooinvoke **SetAirResistance** vous pouvez envoyer cet appareil tooa de message :

```
{"Name" : "SetAirResistance", "Parameters" : { "Position" : 5 }}
```

nom de l’action Hello doit correspondre exactement à une action définie dans votre modèle. les noms de paramètre Hello doivent correspondre également. Notez également que la casse est respectée. **Name** et **Parameters** sont toujours en majuscules. Assurez-vous que cas de hello toomatch de votre nom d’action et les paramètres dans votre modèle. Dans cet exemple, le nom de l’action hello est « SetAirResistance » et non « setairresistance ».

Hello deux autres actions **TurnFanOn** et **TurnFanOff** peut être appelée en envoyant ces appareils tooa de messages :

```
{"Name" : "TurnFanOn", "Parameters" : {}}
{"Name" : "TurnFanOff", "Parameters" : {}}
```

Cette section décrit tous les éléments nécessaires tooknow lors de l’envoi d’événements et de recevoir des messages avec hello **sérialiseur** bibliothèque. Mais avant de poursuivre, intéressons-nous à certains paramètres que vous pouvez configurer pour contrôler la taille de votre modèle.

## <a name="macro-configuration"></a>Configuration des macros
Si vous utilisez hello **sérialiseur** bibliothèque une partie importante de toobe du Kit de développement logiciel hello prenant en charge de se trouve dans la bibliothèque d’azure-c-partagé-utilitaire hello.
Si vous avez cloné référentiel hello Azure iot-sdk--c à partir de GitHub à l’aide hello--récursive option, vous trouverez cette bibliothèque d’utilitaires partagées ici :

```
.\\c-utility
```

Si vous n’avez pas cloné bibliothèque de hello, vous pouvez le trouver [ici](https://github.com/Azure/azure-c-shared-utility).

Dans la bibliothèque d’utilitaires partagées hello, vous trouverez hello suivant du dossier :

```
azure-c-shared-utility\\macro\_utils\_h\_generator.
```

Ce dossier contient une solution Visual Studio appelée **macro\_utils\_h\_generator.sln** :

  ![](media/iot-hub-device-sdk-c-serializer/01-macro_utils_h_generator.PNG)

programme Hello dans cette solution génère hello **macro\_utils.h** fichier. Il existe une macro par défaut\_fichier utils.h inclus avec le Kit de développement logiciel de hello. Cette solution vous permet de toomodify quelques paramètres et le recréer puis hello fichier d’en-tête en fonction de ces paramètres.

les paramètres de clé Hello deux toobe concerné avec sont **nArithmetic** et **nMacroParameters** qui sont définies dans ces deux lignes trouvées dans la macro\_utils.tt :

```
<#int nArithmetic=1024;#>
<#int nMacroParameters=124;/*127 parameters in one macro deﬁnition in C99 in chapter 5.2.4.1 Translation limits*/#>

```

Ces valeurs sont les paramètres par défaut hello inclus avec le Kit de développement logiciel de hello. Chaque paramètre a hello suivant signification :

* nMacroParameters : contrôle le nombre de paramètres que vous pouvez avoir dans une définition de macro DECLARE\_MODEL.
* nArithmetic – nombre total de contrôles hello de membres autorisé dans un modèle.

Hello que ces paramètres sont importants est car elles contrôlent la taille votre modèle. Par exemple, prenez cette définition de modèle :

```
DECLARE_MODEL(MyModel,
WITH_DATA(int, MyData)
);
```

Comme mentionné précédemment, **DECLARE\_MODEL** est une simple macro C. Hello des noms de modèle de hello et hello **WITH\_données** instruction (encore une autre macro) est des paramètres de **DECLARE\_modèle**. **nMacroParameters** définit le nombre de paramètres qui peuvent être inclus dans **DECLARE\_MODEL**. Ces éléments définissent effectivement le nombre possible de déclarations d’événements de données et d’actions. Par conséquent, la limite par défaut hello 124 cela signifie que vous pouvez définir un modèle avec une combinaison d’environ 60 actions et les événements de données. Si vous essayez tooexceed cette limite, vous recevrez les erreurs du compilateur rechercher toothis similaire :

  ![](media/iot-hub-device-sdk-c-serializer/02-nMacroParametersCompilerErrors.PNG)

Hello **nArithmetic** paramètre est plus sur le fonctionnement interne de hello du langage de macro hello de votre application.  Elle contrôle le nombre total de hello de membres que vous avez dans votre modèle, y compris **DECLARE_STRUCT** macros. Donc si vous commencez à voir des erreurs du compilateur comme celles-ci, essayez d’augmenter **nArithmetic**:

   ![](media/iot-hub-device-sdk-c-serializer/03-nArithmeticCompilerErrors.PNG)

Si vous souhaitez toochange ces paramètres, modifiez les valeurs hello macro hello\_utils.tt fichier, recompile hello macro\_utils\_h\_generator.sln solution et un programme compilé d’exécution hello. Quand vous procédez ainsi, une nouvelle macro\_utils.h fichier est généré et placé dans hello.\\ Common\\active de inc.

Dans la nouvelle version de hello de toouse d’ordre de la macro\_utils.h, remove hello **sérialiseur** package NuGet à partir de votre solution et à la place inclure hello **sérialiseur** projet Visual Studio. Cela permet à votre toocompile code contre le code source de hello de bibliothèque de sérialiseur hello. Cela inclut la macro hello mis à jour\_utils.h. Si vous le souhaitez toodo pour **simplesample\_amqp**, commencez par supprimer le package NuGet de hello pour la bibliothèque de sérialiseur hello à partir de la solution de hello :

   ![](media/iot-hub-device-sdk-c-serializer/04-serializer-github-package.PNG)

Ajoutez ensuite ce tooyour projet solution Visual Studio :

> .\\c\\serializer\\build\\windows\\serializer.vcxproj
> 
> 

Lorsque vous avez terminé, votre solution doit ressembler à ceci :

   ![](media/iot-hub-device-sdk-c-serializer/05-serializer-project.PNG)

Maintenant lorsque vous compilez votre solution, hello de mise à jour la macro\_utils.h est inclus dans votre fichier binaire.

Notez qu’en augmentant ces valeurs à un niveau assez élevé, elles peuvent dépasser les limites du compilateur. toothis point, hello **nMacroParameters** est hello paramètre principal qui toobe concerné. norme C99 Hello Spécifie qu’un minimum de 127 paramètres sont autorisés dans une définition de macro. Hello compilateur Microsoft suit exactement les spécifications de hello (et est limité à 127), donc vous ne serez pas en mesure de tooincrease **nMacroParameters** au-delà de la valeur par défaut hello. Autres compilateurs peuvent vous permettre de toodo donc (par exemple, hello GNU compilateur prend en charge une limite plus élevée).

Jusqu'à présent, nous avons couvert quasiment tous les éléments nécessaires tooknow sur la façon dont toowrite code avec hello **sérialiseur** bibliothèque. Avant de conclure, nous allons revoir certaines rubriques d’articles précédents qui amènent peut-être des questions.

## <a name="hello-lower-level-apis"></a>Hello API de niveau inférieur
exemple d’application Hello sur lequel cet article actif est **simplesample\_amqp**. Cet exemple utilise hello (hello non-« LL ») API toosend événements de niveau supérieur et recevoir des messages. Si vous utilisez ces API, un thread d’arrière-plan s’exécute, prenant en charge l’envoi d’événements et la réception de messages. Toutefois, vous pouvez utiliser hello niveau inférieur (II) API tooeliminate ce thread d’arrière-plan et prendre le contrôle explicit lorsque vous envoyez des événements ou recevez des messages à partir du cloud de hello.

Comme décrit dans un [article précédent](iot-hub-device-sdk-c-iothubclient.md), il existe un ensemble de fonctions qui se compose de hello API de niveau supérieur :

* IoTHubClient\_CreateFromConnectionString
* IoTHubClient\_SendEventAsync
* IoTHubClient\_SetMessageCallback
* IoTHubClient\_Destroy

Ces API sont décrites dans **simplesample\_amqp**.

Il existe également un ensemble d’API de niveau inférieur analogue.

* IoTHubClient\_LL\_CreateFromConnectionString
* IoTHubClient\_LL\_SendEventAsync
* IoTHubClient\_LL\_SetMessageCallback
* IoTHubClient\_LL\_Destroy

Notez que travail d’API de niveau inférieur hello hello exactement comme décrit dans les articles précédents hello. Vous pouvez utiliser le premier jeu d’API de hello si vous souhaitez un toohandle de thread d’arrière-plan, l’envoi d’événements et de recevoir des messages. Vous utilisez hello deuxième ensemble d’API si vous souhaitez contrôler explicitement lorsque vous envoyez et recevez des données d’IoT Hub. L’ensemble du travail de l’API indifféremment avec hello **sérialiseur** bibliothèque.

Pour obtenir un exemple de hello API de niveau inférieur est utilisés avec hello **sérialiseur** bibliothèque, consultez hello **simplesample\_http** application.

## <a name="additional-topics"></a>Rubriques supplémentaires
Voici quelques autres sujets qu’il est intéressant de mentionner à nouveau : gestion des propriétés, utilisation d’autres informations d’identification sur l’appareil et options de configuration. Toutes ces rubriques sont traitées dans un [article précédent](iot-hub-device-sdk-c-iothubclient.md). Hello essentiel est que toutes ces fonctionnalités fonctionnent Bonjour même façon avec hello **sérialiseur** bibliothèque comme ils le font avec hello **IoTHubClient** bibliothèque. Par exemple, si vous souhaitez que les événements de tooan tooattach propriétés à partir de votre modèle, vous utilisez **IoTHubMessage\_propriétés** et **carte**\_**AddorUpdate**, comme décrit précédemment hello :

```
MAP_HANDLE propMap = IoTHubMessage_Properties(message.messageHandle);
sprintf_s(propText, sizeof(propText), "%d", i);
Map_AddOrUpdate(propMap, "SequenceNumber", propText);
```

Si les événements hello a été générée à partir de hello **sérialiseur** bibliothèque ou créées manuellement à l’aide de hello **IoTHubClient** bibliothèque n’a pas d’importance.

Hello pour les autres informations d’identification de l’appareil, à l’aide de **IoTHubClient\_LL\_créer** fonctionne aussi bien en tant que **IoTHubClient\_CreateFromConnectionString** pour allouer un **IOTHUB\_CLIENT\_gérer**.

Enfin, si vous utilisez hello **sérialiseur** bibliothèque, vous pouvez définir des options de configuration avec **IoTHubClient\_LL\_SetOption** tout comme vous l’avez fait lors de l’utilisation de hello **IoTHubClient** bibliothèque.

Une fonctionnalité unique toohello **sérialiseur** bibliothèque sont l’initialisation de hello API. Avant de commencer à travailler avec la bibliothèque de hello, vous devez appeler **sérialiseur\_init**:

```
serializer_init(NULL);
```

Cet appel doit être effectué juste avant l’appel de **IoTHubClient\_CreateFromConnectionString**.

De même, lorsque vous avez terminé hello dernier appel vous apporterez utilisez hello bibliothèque, est trop**sérialiseur\_deinit**:

```
serializer_deinit();
```

Dans le cas contraire, tous les hello autres fonctionnalités répertoriées ci-dessus travail hello même Bonjour **sérialiseur** bibliothèque comme Bonjour **IoTHubClient** bibliothèque. Pour plus d’informations sur ces rubriques, consultez hello [article précédent](iot-hub-device-sdk-c-iothubclient.md) dans cette série.

## <a name="next-steps"></a>Étapes suivantes
Cet article décrit en détail hello particularités de hello **sérialiseur** bibliothèque contenue dans hello **appareil Azure IoT SDK pour C**. Avec les informations de hello fournies, vous devez avoir une bonne compréhension de la toouse modélise les événements toosend et recevoir des messages de IoT Hub.

Ceci conclut également série en trois parties hello sur la façon dont les applications toodevelop avec hello **appareil Azure IoT SDK pour C**. Cela doit être suffisamment d’informations toonot obtenez que vous avez démarré mais vous donner une bonne compréhension du fonctionnement de l’API de hello. Pour plus d’informations, il existe quelques exemples Bonjour que SDK pas couverts ici. Dans le cas contraire, hello [documentation du Kit de développement logiciel](https://github.com/Azure/azure-iot-sdk-c) constitue une bonne ressource pour plus d’informations.

toolearn plus sur le développement pour IoT Hub, consultez hello [kits de développement logiciel Azure IoT][lnk-sdks].

toofurther Explorez les fonctionnalités de hello d’IoT Hub, consultez :

* [Simulation d’un appareil avec Azure IoT Edge][lnk-iotedge]

[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
