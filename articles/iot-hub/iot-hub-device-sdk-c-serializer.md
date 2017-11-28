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
# <a name="azure-iot-device-sdk-for-c--more-about-serializer"></a><span data-ttu-id="54491-103">Kit de développement logiciel (SDK) Azure IoT device pour C : en savoir plus sur serializer</span><span class="sxs-lookup"><span data-stu-id="54491-103">Azure IoT device SDK for C – more about serializer</span></span>
<span data-ttu-id="54491-104">Hello [tout d’abord l’article](iot-hub-device-sdk-c-intro.md) cette Bonjour série introduites **appareil Azure IoT SDK pour C**. l’article suivant de hello fourni une description plus détaillée de hello [ **IoTHubClient** ](iot-hub-device-sdk-c-iothubclient.md).</span><span class="sxs-lookup"><span data-stu-id="54491-104">hello [first article](iot-hub-device-sdk-c-intro.md) in this series introduced hello **Azure IoT device SDK for C**. hello next article provided a more detailed description of hello [**IoTHubClient**](iot-hub-device-sdk-c-iothubclient.md).</span></span> <span data-ttu-id="54491-105">Cet article termine la couverture de hello SDK en fournissant une description plus détaillée de hello restante du composant : hello **sérialiseur** bibliothèque.</span><span class="sxs-lookup"><span data-stu-id="54491-105">This article completes coverage of hello SDK by providing a more detailed description of hello remaining component: hello **serializer** library.</span></span>

<span data-ttu-id="54491-106">article de présentation Hello décrit comment toouse hello **sérialiseur** bibliothèque toosend événements tooand recevoir des messages à partir de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="54491-106">hello introductory article described how toouse hello **serializer** library toosend events tooand receive messages from IoT Hub.</span></span> <span data-ttu-id="54491-107">Dans cet article, nous étendre cette discussion, en fournissant une explication plus complète de la toomodel vos données avec hello **sérialiseur** langage de macro.</span><span class="sxs-lookup"><span data-stu-id="54491-107">In this article, we extend that discussion by providing a more complete explanation of how toomodel your data with hello **serializer** macro language.</span></span> <span data-ttu-id="54491-108">Hello inclut également des détails supplémentaires à propos de la bibliothèque de hello sérialise des messages (et dans certains cas comment vous pouvez contrôler un comportement de sérialisation hello).</span><span class="sxs-lookup"><span data-stu-id="54491-108">hello article also includes more detail about how hello library serializes messages (and in some cases how you can control hello serialization behavior).</span></span> <span data-ttu-id="54491-109">Nous allons également décrire certains que vous pouvez modifier les paramètres qui déterminent la taille de hello de modèles hello que vous créez.</span><span class="sxs-lookup"><span data-stu-id="54491-109">We'll also describe some parameters you can modify that determine hello size of hello models you create.</span></span>

<span data-ttu-id="54491-110">Enfin, l’article de hello revisite certaines rubriques abordées dans les articles précédents, tels que le message et la gestion de propriétés.</span><span class="sxs-lookup"><span data-stu-id="54491-110">Finally, hello article revisits some topics covered in previous articles such as message and property handling.</span></span> <span data-ttu-id="54491-111">Comme nous allons découvrir, ces fonctionnalités travail hello même à l’aide hello **sérialiseur** bibliothèque comme ils le font avec hello **IoTHubClient** bibliothèque.</span><span class="sxs-lookup"><span data-stu-id="54491-111">As we'll find out, those features work in hello same way using hello **serializer** library as they do with hello **IoTHubClient** library.</span></span>

<span data-ttu-id="54491-112">Tous les éléments décrits dans cet article sont basé sur hello **sérialiseur** exemples SDK.</span><span class="sxs-lookup"><span data-stu-id="54491-112">Everything described in this article is based on hello **serializer** SDK samples.</span></span> <span data-ttu-id="54491-113">Si vous souhaitez toofollow le long, consultez hello **simplesample\_amqp** et **simplesample\_http** applications incluses dans le dispositif de Azure IoT hello SDK pour C.</span><span class="sxs-lookup"><span data-stu-id="54491-113">If you want toofollow along, see hello **simplesample\_amqp** and **simplesample\_http** applications included in hello Azure IoT device SDK for C.</span></span>

<span data-ttu-id="54491-114">Vous pouvez trouver hello [ **appareil Azure IoT SDK pour C** ](https://github.com/Azure/azure-iot-sdk-c) GitHub référentiel et consulter les détails de hello API Bonjour [référence d’API C](https://azure.github.io/azure-iot-sdk-c/index.html).</span><span class="sxs-lookup"><span data-stu-id="54491-114">You can find hello [**Azure IoT device SDK for C**](https://github.com/Azure/azure-iot-sdk-c) GitHub repository and view details of hello API in hello [C API reference](https://azure.github.io/azure-iot-sdk-c/index.html).</span></span>

## <a name="hello-modeling-language"></a><span data-ttu-id="54491-115">langage de modélisation Hello</span><span class="sxs-lookup"><span data-stu-id="54491-115">hello modeling language</span></span>
<span data-ttu-id="54491-116">Hello [article de présentation](iot-hub-device-sdk-c-intro.md) cette Bonjour série introduites **appareil Azure IoT SDK pour C** modélisation au moyen de l’exemple hello prévue hello **simplesample\_amqp**  application :</span><span class="sxs-lookup"><span data-stu-id="54491-116">hello [introductory article](iot-hub-device-sdk-c-intro.md) in this series introduced hello **Azure IoT device SDK for C** modeling language through hello example provided in hello **simplesample\_amqp** application:</span></span>

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

<span data-ttu-id="54491-117">Comme vous pouvez le voir, hello langage de modélisation est basée sur les macros C.</span><span class="sxs-lookup"><span data-stu-id="54491-117">As you can see, hello modeling language is based on C macros.</span></span> <span data-ttu-id="54491-118">La définition commence toujours par **BEGIN\_NAMESPACE** et se termine toujours par **END\_NAMESPACE**.</span><span class="sxs-lookup"><span data-stu-id="54491-118">You always begin your definition with **BEGIN\_NAMESPACE** and always end with **END\_NAMESPACE**.</span></span> <span data-ttu-id="54491-119">Il est commun tooname hello espace de noms pour votre société ou, comme dans cet exemple, le projet de hello sur lequel vous travaillez.</span><span class="sxs-lookup"><span data-stu-id="54491-119">It's common tooname hello namespace for your company or, as in this example, hello project that you're working on.</span></span>

<span data-ttu-id="54491-120">Ce qui se passe dans l’espace de noms hello sont des définitions de modèle.</span><span class="sxs-lookup"><span data-stu-id="54491-120">What goes inside hello namespace are model definitions.</span></span> <span data-ttu-id="54491-121">Dans ce cas, il s’agit d’un modèle unique pour un anémomètre.</span><span class="sxs-lookup"><span data-stu-id="54491-121">In this case, there is a single model for an anemometer.</span></span> <span data-ttu-id="54491-122">Une fois encore, modèle de hello peut être n’importe quel nom, mais en général, cela est nommé pour hello périphérique ou un type de données que vous souhaitez tooexchange IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="54491-122">Once again, hello model can be named anything, but typically this is named for hello device or type of data you want tooexchange with IoT Hub.</span></span>  

<span data-ttu-id="54491-123">Les modèles contiennent une définition d’événements de hello, vous pouvez en entrée tooIoT concentrateur (hello *données*), ainsi que les messages hello vous pouvez recevoir de IoT Hub (hello *actions*).</span><span class="sxs-lookup"><span data-stu-id="54491-123">Models contain a definition of hello events you can ingress tooIoT Hub (hello *data*) as well as hello messages you can receive from IoT Hub (hello *actions*).</span></span> <span data-ttu-id="54491-124">Comme vous pouvez le voir à partir de l’exemple de hello, les événements ont un type et un nom. actions ont un nom et des paramètres facultatifs (chacun avec un type).</span><span class="sxs-lookup"><span data-stu-id="54491-124">As you can see from hello example, events have a type and a name; actions have a name and optional parameters (each with a type).</span></span>

<span data-ttu-id="54491-125">N’est pas illustrée dans cet exemple sont des types de données supplémentaires qui sont prises en charge par le Kit de développement logiciel de hello.</span><span class="sxs-lookup"><span data-stu-id="54491-125">What’s not demonstrated in this sample are additional data types that are supported by hello SDK.</span></span> <span data-ttu-id="54491-126">Nous allons aborder ce point par la suite.</span><span class="sxs-lookup"><span data-stu-id="54491-126">We'll cover that next.</span></span>

> [!NOTE]
> <span data-ttu-id="54491-127">IoT Hub fait référence à des données toohello un appareil envoie tooit comme *événements*, tandis que le langage de modélisation de hello fait référence tooit en tant que *données* (défini à l’aide **WITH_DATA**).</span><span class="sxs-lookup"><span data-stu-id="54491-127">IoT Hub refers toohello data a device sends tooit as *events*, while hello modeling language refers tooit as *data* (defined using **WITH_DATA**).</span></span> <span data-ttu-id="54491-128">De même, IoT Hub fait référence à des données toohello vous envoyez toodevices comme *messages*, tandis que le langage de modélisation de hello fait référence tooit en tant que *actions* (défini à l’aide **WITH_ACTION**).</span><span class="sxs-lookup"><span data-stu-id="54491-128">Likewise, IoT Hub refers toohello data you send toodevices as *messages*, while hello modeling language refers tooit as *actions* (defined using **WITH_ACTION**).</span></span> <span data-ttu-id="54491-129">Sachez que ces termes peuvent être utilisés de manière interchangeable dans cet article.</span><span class="sxs-lookup"><span data-stu-id="54491-129">Be aware that these terms may be used interchangeably in this article.</span></span>
> 
> 

### <a name="supported-data-types"></a><span data-ttu-id="54491-130">Types de données pris en charge</span><span class="sxs-lookup"><span data-stu-id="54491-130">Supported data types</span></span>
<span data-ttu-id="54491-131">Hello, les types de données suivants est pris en charge dans les modèles créés avec hello **sérialiseur** bibliothèque :</span><span class="sxs-lookup"><span data-stu-id="54491-131">hello following data types are supported in models created with hello **serializer** library:</span></span>

| <span data-ttu-id="54491-132">Type</span><span class="sxs-lookup"><span data-stu-id="54491-132">Type</span></span> | <span data-ttu-id="54491-133">Description</span><span class="sxs-lookup"><span data-stu-id="54491-133">Description</span></span> |
| --- | --- |
| <span data-ttu-id="54491-134">double</span><span class="sxs-lookup"><span data-stu-id="54491-134">double</span></span> |<span data-ttu-id="54491-135">nombre à virgule flottante double précision</span><span class="sxs-lookup"><span data-stu-id="54491-135">double precision floating point number</span></span> |
| <span data-ttu-id="54491-136">int</span><span class="sxs-lookup"><span data-stu-id="54491-136">int</span></span> |<span data-ttu-id="54491-137">entier 32 bits</span><span class="sxs-lookup"><span data-stu-id="54491-137">32 bit integer</span></span> |
| <span data-ttu-id="54491-138">float</span><span class="sxs-lookup"><span data-stu-id="54491-138">float</span></span> |<span data-ttu-id="54491-139">nombre à virgule flottante simple précision</span><span class="sxs-lookup"><span data-stu-id="54491-139">single precision floating point number</span></span> |
| <span data-ttu-id="54491-140">long</span><span class="sxs-lookup"><span data-stu-id="54491-140">long</span></span> |<span data-ttu-id="54491-141">entier long</span><span class="sxs-lookup"><span data-stu-id="54491-141">long integer</span></span> |
| <span data-ttu-id="54491-142">int8\_t</span><span class="sxs-lookup"><span data-stu-id="54491-142">int8\_t</span></span> |<span data-ttu-id="54491-143">entier 8 bits</span><span class="sxs-lookup"><span data-stu-id="54491-143">8 bit integer</span></span> |
| <span data-ttu-id="54491-144">int16\_t</span><span class="sxs-lookup"><span data-stu-id="54491-144">int16\_t</span></span> |<span data-ttu-id="54491-145">entier 16 bits</span><span class="sxs-lookup"><span data-stu-id="54491-145">16 bit integer</span></span> |
| <span data-ttu-id="54491-146">int32\_t</span><span class="sxs-lookup"><span data-stu-id="54491-146">int32\_t</span></span> |<span data-ttu-id="54491-147">entier 32 bits</span><span class="sxs-lookup"><span data-stu-id="54491-147">32 bit integer</span></span> |
| <span data-ttu-id="54491-148">int64\_t</span><span class="sxs-lookup"><span data-stu-id="54491-148">int64\_t</span></span> |<span data-ttu-id="54491-149">entier 64 bits</span><span class="sxs-lookup"><span data-stu-id="54491-149">64 bit integer</span></span> |
| <span data-ttu-id="54491-150">valeur booléenne</span><span class="sxs-lookup"><span data-stu-id="54491-150">bool</span></span> |<span data-ttu-id="54491-151">booléenne</span><span class="sxs-lookup"><span data-stu-id="54491-151">boolean</span></span> |
| <span data-ttu-id="54491-152">ascii\_char\_ptr</span><span class="sxs-lookup"><span data-stu-id="54491-152">ascii\_char\_ptr</span></span> |<span data-ttu-id="54491-153">Chaîne ASCII</span><span class="sxs-lookup"><span data-stu-id="54491-153">ASCII string</span></span> |
| <span data-ttu-id="54491-154">EDM\_DATE\_TIME\_OFFSET</span><span class="sxs-lookup"><span data-stu-id="54491-154">EDM\_DATE\_TIME\_OFFSET</span></span> |<span data-ttu-id="54491-155">décalage de date et d’heure</span><span class="sxs-lookup"><span data-stu-id="54491-155">date time offset</span></span> |
| <span data-ttu-id="54491-156">EDM\_GUID</span><span class="sxs-lookup"><span data-stu-id="54491-156">EDM\_GUID</span></span> |<span data-ttu-id="54491-157">GUID</span><span class="sxs-lookup"><span data-stu-id="54491-157">GUID</span></span> |
| <span data-ttu-id="54491-158">EDM\_BINARY</span><span class="sxs-lookup"><span data-stu-id="54491-158">EDM\_BINARY</span></span> |<span data-ttu-id="54491-159">binaire</span><span class="sxs-lookup"><span data-stu-id="54491-159">binary</span></span> |
| <span data-ttu-id="54491-160">DECLARE\_STRUCT</span><span class="sxs-lookup"><span data-stu-id="54491-160">DECLARE\_STRUCT</span></span> |<span data-ttu-id="54491-161">type de données complexe</span><span class="sxs-lookup"><span data-stu-id="54491-161">complex data type</span></span> |

<span data-ttu-id="54491-162">Commençons par type de données de dernière hello.</span><span class="sxs-lookup"><span data-stu-id="54491-162">Let’s start with hello last data type.</span></span> <span data-ttu-id="54491-163">Hello **DECLARE\_STRUCT** vous permet de types de données complexes toodefine, qui sont des groupements de hello autres types primitifs.</span><span class="sxs-lookup"><span data-stu-id="54491-163">hello **DECLARE\_STRUCT** allows you toodefine complex data types, which are groupings of hello other primitive types.</span></span> <span data-ttu-id="54491-164">Ces regroupements permettent nous toodefine un modèle qui ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="54491-164">These groupings allow us toodefine a model that looks like this:</span></span>

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

<span data-ttu-id="54491-165">Notre modèle contient un événement de données unique de type **TestType**.</span><span class="sxs-lookup"><span data-stu-id="54491-165">Our model contains a single data event of type **TestType**.</span></span> <span data-ttu-id="54491-166">**TestType** est un type complexe qui inclut plusieurs membres, qui illustrent la prise en charge par hello des types primitifs hello collectivement **sérialiseur** langage de modélisation.</span><span class="sxs-lookup"><span data-stu-id="54491-166">**TestType** is a complex type that includes several members, which collectively demonstrate hello primitive types supported by hello **serializer** modeling language.</span></span>

<span data-ttu-id="54491-167">Avec un modèle de ce type, nous pouvons écrire le code toosend données tooIoT Hub qui s’affiche comme suit :</span><span class="sxs-lookup"><span data-stu-id="54491-167">With a model like this, we can write code toosend data tooIoT Hub that appears as follows:</span></span>

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

<span data-ttu-id="54491-168">En fait, nous allons affectation membre tooevery valeur hello **Test** structure, puis en appelant **SendAsync** toosend hello **Test** données dans le cloud toohello événement.</span><span class="sxs-lookup"><span data-stu-id="54491-168">Basically, we’re assigning a value tooevery member of hello **Test** structure and then calling **SendAsync** toosend hello **Test** data event toohello cloud.</span></span> <span data-ttu-id="54491-169">**SendAsync** est une fonction d’assistance qui envoie un tooIoT d’événement de données Hub :</span><span class="sxs-lookup"><span data-stu-id="54491-169">**SendAsync** is a helper function that sends a single data event tooIoT Hub:</span></span>

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

<span data-ttu-id="54491-170">Cette fonction sérialise hello données événement donné et envoie tooIoT concentrateur à l’aide de **IoTHubClient\_SendEventAsync**.</span><span class="sxs-lookup"><span data-stu-id="54491-170">This function serializes hello given data event and sends it tooIoT Hub using **IoTHubClient\_SendEventAsync**.</span></span> <span data-ttu-id="54491-171">Il s’agit de hello même code présenté dans les articles précédents (**SendAsync** encapsule la logique de hello dans une fonction pratique).</span><span class="sxs-lookup"><span data-stu-id="54491-171">This is hello same code discussed in previous articles (**SendAsync** encapsulates hello logic into a convenient function).</span></span>

<span data-ttu-id="54491-172">Une autre fonction d’assistance utilisée dans le code précédent hello est **GetDateTimeOffset**.</span><span class="sxs-lookup"><span data-stu-id="54491-172">One other helper function used in hello previous code is **GetDateTimeOffset**.</span></span> <span data-ttu-id="54491-173">Cette fonction transforme hello moment donné en une valeur de type **EDM\_DATE\_temps\_décalage**:</span><span class="sxs-lookup"><span data-stu-id="54491-173">This function transforms hello given time into a value of type **EDM\_DATE\_TIME\_OFFSET**:</span></span>

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

<span data-ttu-id="54491-174">Si vous exécutez ce code, hello suivant message est envoyé à tooIoT Hub :</span><span class="sxs-lookup"><span data-stu-id="54491-174">If you run this code, hello following message is sent tooIoT Hub:</span></span>

```
{"aDouble":1.100000000000000, "aInt":2, "aFloat":3.000000, "aLong":4, "aInt8":5, "auInt8":6, "aInt16":7, "aInt32":8, "aInt64":9, "aBool":true, "aAsciiCharPtr":"ascii string 1", "aDateTimeOffset":"2015-09-14T21:18:21Z", "aGuid":"00010203-0405-0607-0809-0A0B0C0D0E0F", "aBinary":"AQID"}
```

<span data-ttu-id="54491-175">Notez que la sérialisation de hello est JSON, qui est le format hello généré par hello **sérialiseur** bibliothèque.</span><span class="sxs-lookup"><span data-stu-id="54491-175">Note that hello serialization is JSON, which is hello format generated by hello **serializer** library.</span></span> <span data-ttu-id="54491-176">Notez que chaque membre de hello sérialisé objet JSON correspond également à des membres de hello Hello **TestType** que nous avons défini dans notre modèle.</span><span class="sxs-lookup"><span data-stu-id="54491-176">Also note that each member of hello serialized JSON object matches hello members of hello **TestType** that we defined in our model.</span></span> <span data-ttu-id="54491-177">les valeurs Hello également correspondre exactement à celles utilisées dans le code hello.</span><span class="sxs-lookup"><span data-stu-id="54491-177">hello values also exactly match those used in hello code.</span></span> <span data-ttu-id="54491-178">Toutefois, notez que les données binaires hello sont codée en base64 : « AQID » est hello encodage base64 de {0 x 01, 0 x 02, 0 x 03}.</span><span class="sxs-lookup"><span data-stu-id="54491-178">However, note that hello binary data is base64-encoded: "AQID" is hello base64 encoding of {0x01, 0x02, 0x03}.</span></span>

<span data-ttu-id="54491-179">Cet exemple montre comment présente l’avantage de hello hello **sérialiseur** bibliothèque--il nous permet de toosend JSON toohello cloud, sans avoir à tooexplicitly de gérer la sérialisation dans notre application.</span><span class="sxs-lookup"><span data-stu-id="54491-179">This example demonstrates hello advantage of using hello **serializer** library -- it enables us toosend JSON toohello cloud, without having tooexplicitly deal with serialization in our application.</span></span> <span data-ttu-id="54491-180">Il nous tooworry sur est valeurs de paramètre hello de hello événements de données dans notre modèle, puis à appeler simple API toosend ces cloud de toohello d’événements.</span><span class="sxs-lookup"><span data-stu-id="54491-180">All we have tooworry about is setting hello values of hello data events in our model and then calling simple APIs toosend those events toohello cloud.</span></span>

<span data-ttu-id="54491-181">Avec ces informations, nous pouvons définir des modèles qui incluent la plage hello pris en charge des types de données, y compris les types complexes (nous avons même inclure des types complexes dans d’autres types complexes).</span><span class="sxs-lookup"><span data-stu-id="54491-181">With this information, we can define models that include hello range of supported data types, including complex types (we could even include complex types within other complex types).</span></span> <span data-ttu-id="54491-182">Cependant, il a sérialisée JSON généré par hello exemple ci-dessus affiche un point important.</span><span class="sxs-lookup"><span data-stu-id="54491-182">However, he serialized JSON generated by hello example above brings up an important point.</span></span> <span data-ttu-id="54491-183">*Comment* nous envoyer des données avec hello **sérialiseur** bibliothèque détermine exactement comment hello JSON est formé.</span><span class="sxs-lookup"><span data-stu-id="54491-183">*How* we send data with hello **serializer** library determines exactly how hello JSON is formed.</span></span> <span data-ttu-id="54491-184">C’est ce point particulier que nous allons ensuite aborder.</span><span class="sxs-lookup"><span data-stu-id="54491-184">That particular point is what we'll cover next.</span></span>

## <a name="more-about-serialization"></a><span data-ttu-id="54491-185">En savoir plus sur la sérialisation</span><span class="sxs-lookup"><span data-stu-id="54491-185">More about serialization</span></span>
<span data-ttu-id="54491-186">section précédente de Hello met en évidence un exemple de sortie hello généré par hello **sérialiseur** bibliothèque.</span><span class="sxs-lookup"><span data-stu-id="54491-186">hello previous section highlights an example of hello output generated by hello **serializer** library.</span></span> <span data-ttu-id="54491-187">Dans cette section, nous expliquerons comment les bibliothèque hello sérialise les données et comment vous pouvez contrôler ce comportement à l’aide des API de sérialisation hello.</span><span class="sxs-lookup"><span data-stu-id="54491-187">In this section, we'll explain how hello library serializes data and how you can control that behavior using hello serialization APIs.</span></span>

<span data-ttu-id="54491-188">Dans la discussion hello du tooadvance ordre lors de la sérialisation, nous travaillons en collaboration avec un nouveau modèle basé sur un thermostat.</span><span class="sxs-lookup"><span data-stu-id="54491-188">In order tooadvance hello discussion on serialization, we'll work with a new model based on a thermostat.</span></span> <span data-ttu-id="54491-189">Tout d’abord, nous allons fournir des informations générales sur le scénario de hello nous essayons de tooaddress.</span><span class="sxs-lookup"><span data-stu-id="54491-189">First, let's provide some background on hello scenario we're trying tooaddress.</span></span>

<span data-ttu-id="54491-190">Nous souhaitons toomodel un thermostat qui mesure la température et humidité.</span><span class="sxs-lookup"><span data-stu-id="54491-190">We want toomodel a thermostat that measures temperature and humidity.</span></span> <span data-ttu-id="54491-191">Chaque élément de données est en cours toobe envoyé tooIoT Hub différemment.</span><span class="sxs-lookup"><span data-stu-id="54491-191">Each piece of data is going toobe sent tooIoT Hub differently.</span></span> <span data-ttu-id="54491-192">Par défaut, hello ingresses de thermostat un événement de température toutes les 2 minutes ; un événement de l’humidité est ingressed toutes les 15 minutes.</span><span class="sxs-lookup"><span data-stu-id="54491-192">By default, hello thermostat ingresses a temperature event once every 2 minutes; a humidity event is ingressed once every 15 minutes.</span></span> <span data-ttu-id="54491-193">Lorsque l’événement est ingressed, elle doit inclure un horodatage qui indique les temps de hello que la température correspondante hello ou humidité a été mesurée.</span><span class="sxs-lookup"><span data-stu-id="54491-193">When either event is ingressed, it must include a timestamp that shows hello time that hello corresponding temperature or humidity was measured.</span></span>

<span data-ttu-id="54491-194">Étant donné ce scénario, nous vous montrer les données de salutation toomodel deux façons différentes, et nous expliquerons effet hello que modélisation a hello sérialisée pour la sortie.</span><span class="sxs-lookup"><span data-stu-id="54491-194">Given this scenario, we'll demonstrate two different ways toomodel hello data, and we'll explain hello effect that modeling has on hello serialized output.</span></span>

### <a name="model-1"></a><span data-ttu-id="54491-195">Modèle n° 1</span><span class="sxs-lookup"><span data-stu-id="54491-195">Model 1</span></span>
<span data-ttu-id="54491-196">Voici hello première version d’un modèle que prend en charge hello scénario précédent :</span><span class="sxs-lookup"><span data-stu-id="54491-196">Here's hello first version of a model that supports hello previous scenario:</span></span>

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

<span data-ttu-id="54491-197">Notez que ce modèle hello inclut deux événements de données : **température** et **humidité**.</span><span class="sxs-lookup"><span data-stu-id="54491-197">Note that hello model includes two data events: **Temperature** and **Humidity**.</span></span> <span data-ttu-id="54491-198">Contrairement aux exemples précédents, type hello de chaque événement est une structure définie à l’aide de **DECLARE\_STRUCT**.</span><span class="sxs-lookup"><span data-stu-id="54491-198">Unlike previous examples, hello type of each event is a structure defined using **DECLARE\_STRUCT**.</span></span> <span data-ttu-id="54491-199">**TemperatureEvent** comprend une mesure de température et un horodatage ; **HumidityEvent** contient une mesure d’humidité et un horodatage.</span><span class="sxs-lookup"><span data-stu-id="54491-199">**TemperatureEvent** includes a temperature measurement and a timestamp; **HumidityEvent** contains a humidity measurement and a timestamp.</span></span> <span data-ttu-id="54491-200">Ce modèle nous offre un moyen naturel toomodel hello de données pour le scénario hello décrit ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="54491-200">This model gives us a natural way toomodel hello data for hello scenario described above.</span></span> <span data-ttu-id="54491-201">Lorsque nous envoyer un nuage de toohello d’événement, nous vous enverrons soit un température/horodatage ou une paire humidité/horodatage.</span><span class="sxs-lookup"><span data-stu-id="54491-201">When we send an event toohello cloud, we'll either send a temperature/timestamp or a humidity/timestamp pair.</span></span>

<span data-ttu-id="54491-202">Nous pouvons envoyer un nuage de toohello température événement à l’aide de code tel que hello suivant :</span><span class="sxs-lookup"><span data-stu-id="54491-202">We can send a temperature event toohello cloud using code such as hello following:</span></span>

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

<span data-ttu-id="54491-203">Nous verrons utiliser des valeurs codées en dur pour la température et humidité dans l’exemple de code hello, mais supposons que nous récupérons réellement ces valeurs en échantillonnant les capteurs de hello correspondant sur thermostat de hello.</span><span class="sxs-lookup"><span data-stu-id="54491-203">We'll use hard-coded values for temperature and humidity in hello sample code, but imagine that we’re actually retrieving these values by sampling hello corresponding sensors on hello thermostat.</span></span>

<span data-ttu-id="54491-204">code Hello ci-dessus utilise hello **GetDateTimeOffset** assistance qui a été introduit précédemment.</span><span class="sxs-lookup"><span data-stu-id="54491-204">hello code above uses hello **GetDateTimeOffset** helper that was introduced previously.</span></span> <span data-ttu-id="54491-205">Pour des raisons qui deviendront désactivez ultérieures, ce code sépare explicitement tâche hello de sérialisation et l’envoi d’événements de hello.</span><span class="sxs-lookup"><span data-stu-id="54491-205">For reasons that will become clear later, this code explicitly separates hello task of serializing and sending hello event.</span></span> <span data-ttu-id="54491-206">code précédent de Hello sérialise les événements de température hello dans une mémoire tampon.</span><span class="sxs-lookup"><span data-stu-id="54491-206">hello previous code serializes hello temperature event into a buffer.</span></span> <span data-ttu-id="54491-207">Ensuite, **sendMessage** est une fonction d’assistance (inclus dans **simplesample\_amqp**) qu’envoie hello événement tooIoT Hub :</span><span class="sxs-lookup"><span data-stu-id="54491-207">Then, **sendMessage** is a helper function (included in **simplesample\_amqp**) that sends hello event tooIoT Hub:</span></span>

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

<span data-ttu-id="54491-208">Ce code est un sous-ensemble de hello **SendAsync** helper décrite dans la section précédente de hello, donc nous n’allons pas dessus à nouveau ici.</span><span class="sxs-lookup"><span data-stu-id="54491-208">This code is a subset of hello **SendAsync** helper described in hello previous section, so we won’t go over it again here.</span></span>

<span data-ttu-id="54491-209">Si nous exécutons hello code toosend hello température l’événement précédent, cette forme sérialisée de l’événement de hello est envoyée tooIoT Hub :</span><span class="sxs-lookup"><span data-stu-id="54491-209">When we run hello previous code toosend hello Temperature event, this serialized form of hello event is sent tooIoT Hub:</span></span>

```
{"Temperature":75, "Time":"2015-09-17T18:45:56Z"}
```

<span data-ttu-id="54491-210">Nous allons envoyer une température de type **TemperatureEvent** et cette structure contient un membre **Temperature** et **Time**.</span><span class="sxs-lookup"><span data-stu-id="54491-210">We're sending a temperature which is of type **TemperatureEvent** and that struct contains a **Temperature** and **Time** member.</span></span> <span data-ttu-id="54491-211">Cela se reflète directement dans les données de salutation sérialisée.</span><span class="sxs-lookup"><span data-stu-id="54491-211">This is directly reflected in hello serialized data.</span></span>

<span data-ttu-id="54491-212">De même, nous pouvons envoyer un événement d’humidité avec ce code :</span><span class="sxs-lookup"><span data-stu-id="54491-212">Similarly, we can send a humidity event with this code:</span></span>

```
thermostat->Humidity.Humidity = 45;
thermostat->Humidity.Time = GetDateTimeOffset(now);
if (SERIALIZE(&destination, &destinationSize, thermostat->Humidity) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

<span data-ttu-id="54491-213">écran Hello sérialisée qui a envoyé tooIoT Hub apparaît comme suit :</span><span class="sxs-lookup"><span data-stu-id="54491-213">hello serialized form that’s sent tooIoT Hub appears as follows:</span></span>

```
{"Humidity":45, "Time":"2015-09-17T18:45:56Z"}
```

<span data-ttu-id="54491-214">Comme attendu, là encore.</span><span class="sxs-lookup"><span data-stu-id="54491-214">Again, this is as expected.</span></span>

<span data-ttu-id="54491-215">Avec ce modèle, vous pouvez voir comment d’autres événements peuvent facilement être ajoutés.</span><span class="sxs-lookup"><span data-stu-id="54491-215">With this model, you can imagine how additional events can easily be added.</span></span> <span data-ttu-id="54491-216">Vous définissez plusieurs structures à l’aide **DECLARE\_STRUCT**et inclure les événements correspondants hello dans à l’aide du modèle hello **WITH\_données**.</span><span class="sxs-lookup"><span data-stu-id="54491-216">You define more structures using **DECLARE\_STRUCT**, and include hello corresponding event in hello model using **WITH\_DATA**.</span></span>

<span data-ttu-id="54491-217">Maintenant, nous allons modifier le modèle de hello afin qu’il inclue hello mêmes données, mais avec une structure différente.</span><span class="sxs-lookup"><span data-stu-id="54491-217">Now, let’s modify hello model so that it includes hello same data but with a different structure.</span></span>

### <a name="model-2"></a><span data-ttu-id="54491-218">Modèle n° 2</span><span class="sxs-lookup"><span data-stu-id="54491-218">Model 2</span></span>
<span data-ttu-id="54491-219">Prenez en compte cette toohello autre modèle une ci-dessus :</span><span class="sxs-lookup"><span data-stu-id="54491-219">Consider this alternative model toohello one above:</span></span>

```
DECLARE_MODEL(Thermostat,
WITH_DATA(int, Temperature),
WITH_DATA(int, Humidity),
WITH_DATA(EDM_DATE_TIME_OFFSET, Time)
);
```

<span data-ttu-id="54491-220">Dans ce cas, nous avons éliminé hello **DECLARE\_STRUCT** macros et définissez simplement les éléments de données hello dans notre scénario à l’aide de types simples à partir du langage de modélisation de hello.</span><span class="sxs-lookup"><span data-stu-id="54491-220">In this case we've eliminated hello **DECLARE\_STRUCT** macros and are simply defining hello data items from our scenario using simple types from hello modeling language.</span></span>

<span data-ttu-id="54491-221">Juste pour le moment de hello, nous allons ignorer hello **temps** événement.</span><span class="sxs-lookup"><span data-stu-id="54491-221">Just for hello moment let’s ignore hello **Time** event.</span></span> <span data-ttu-id="54491-222">Avec ce aside, voici hello code tooingress **température**:</span><span class="sxs-lookup"><span data-stu-id="54491-222">With that aside, here’s hello code tooingress **Temperature**:</span></span>

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

<span data-ttu-id="54491-223">Ce code envoie suivant de hello sérialisé événement tooIoT Hub :</span><span class="sxs-lookup"><span data-stu-id="54491-223">This code sends hello following serialized event tooIoT Hub:</span></span>

```
{"Temperature":75}
```

<span data-ttu-id="54491-224">Et code hello pour envoyer des événements de humidité hello apparaît comme suit :</span><span class="sxs-lookup"><span data-stu-id="54491-224">And hello code for sending hello Humidity event appears as follows:</span></span>

```
thermostat->Humidity = 45;
if (SERIALIZE(&destination, &destinationSize, thermostat->Humidity) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

<span data-ttu-id="54491-225">Ce code envoie cette tooIoT Hub :</span><span class="sxs-lookup"><span data-stu-id="54491-225">This code sends this tooIoT Hub:</span></span>

```
{"Humidity":45}
```

<span data-ttu-id="54491-226">Jusqu’à présent, toujours pas de surprise.</span><span class="sxs-lookup"><span data-stu-id="54491-226">So far there are still no surprises.</span></span> <span data-ttu-id="54491-227">Maintenant nous allons modifier comment nous utilisons la macro SERIALIZE hello.</span><span class="sxs-lookup"><span data-stu-id="54491-227">Now let's change how we use hello SERIALIZE macro.</span></span>

<span data-ttu-id="54491-228">Hello **SERIALIZE** macro peut prendre plusieurs événements de données en tant qu’arguments.</span><span class="sxs-lookup"><span data-stu-id="54491-228">hello **SERIALIZE** macro can take multiple data events as arguments.</span></span> <span data-ttu-id="54491-229">Cela nous permet de tooserialize hello **température** et **humidité** ensemble d’événements et les envoyer tooIoT concentrateur dans un seul appel :</span><span class="sxs-lookup"><span data-stu-id="54491-229">This enables us tooserialize hello **Temperature** and **Humidity** event together and send them tooIoT Hub in one call:</span></span>

```
if (SERIALIZE(&destination, &destinationSize, thermostat->Temperature, thermostat->Humidity) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

<span data-ttu-id="54491-230">Vous pouvez le deviner que le résultat hello de ce code est que les événements de deux fichiers de données sont envoyés tooIoT Hub :</span><span class="sxs-lookup"><span data-stu-id="54491-230">You might guess that hello result of this code is that two data events are sent tooIoT Hub:</span></span>

<span data-ttu-id="54491-231">[</span><span class="sxs-lookup"><span data-stu-id="54491-231">[</span></span>

<span data-ttu-id="54491-232">{"Temperature":75},</span><span class="sxs-lookup"><span data-stu-id="54491-232">{"Temperature":75},</span></span>

<span data-ttu-id="54491-233">{"Humidity":45}</span><span class="sxs-lookup"><span data-stu-id="54491-233">{"Humidity":45}</span></span>

<span data-ttu-id="54491-234">]</span><span class="sxs-lookup"><span data-stu-id="54491-234">]</span></span>

<span data-ttu-id="54491-235">En d’autres termes, vous pouvez attendre que ce code est hello même que l’envoi de **température** et **humidité** séparément.</span><span class="sxs-lookup"><span data-stu-id="54491-235">In other words, you might expect that this code is hello same as sending **Temperature** and **Humidity** separately.</span></span> <span data-ttu-id="54491-236">Il est simplement un toopass commodité les deux événements trop**SERIALIZE** Bonjour même appeler.</span><span class="sxs-lookup"><span data-stu-id="54491-236">It’s just a convenience toopass both events too**SERIALIZE** in hello same call.</span></span> <span data-ttu-id="54491-237">Toutefois, qui n’est pas le cas de hello.</span><span class="sxs-lookup"><span data-stu-id="54491-237">However, that’s not hello case.</span></span> <span data-ttu-id="54491-238">Au lieu de cela, le code hello ci-dessus envoie cette tooIoT d’événement de données concentrateur :</span><span class="sxs-lookup"><span data-stu-id="54491-238">Instead, hello code above sends this single data event tooIoT Hub:</span></span>

<span data-ttu-id="54491-239">{"Temperature":75, "Humidity":45}</span><span class="sxs-lookup"><span data-stu-id="54491-239">{"Temperature":75, "Humidity":45}</span></span>

<span data-ttu-id="54491-240">Cela peut sembler étrange, étant donné que notre modèle définit **Temperature** et **Humidity** comme deux événements *distincts* :</span><span class="sxs-lookup"><span data-stu-id="54491-240">This may seem strange because our model defines **Temperature** and **Humidity** as two *separate* events:</span></span>

```
DECLARE_MODEL(Thermostat,
WITH_DATA(int, Temperature),
WITH_DATA(int, Humidity),
WITH_DATA(EDM_DATE_TIME_OFFSET, Time)
);
```

<span data-ttu-id="54491-241">Point toohello, nous n’a pas de modèle ces événements où **température** et **humidité** sont Bonjour même structure :</span><span class="sxs-lookup"><span data-stu-id="54491-241">More toohello point, we didn’t model these events where **Temperature** and **Humidity** are in hello same structure:</span></span>

```
DECLARE_STRUCT(TemperatureAndHumidityEvent,
int, Temperature,
int, Humidity,
);

DECLARE_MODEL(Thermostat,
WITH_DATA(TemperatureAndHumidityEvent, TemperatureAndHumidity),
);
```

<span data-ttu-id="54491-242">Si nous utilisons ce modèle, il serait plus facile toounderstand comment **température** et **humidité** seraient envoyées Bonjour même message sérialisé.</span><span class="sxs-lookup"><span data-stu-id="54491-242">If we used this model, it would be easier toounderstand how **Temperature** and **Humidity** would be sent in hello same serialized message.</span></span> <span data-ttu-id="54491-243">Toutefois peut-être pas clairement pourquoi il fonctionne de cette façon, lorsque vous transmettez les deux événements de données trop**SERIALIZE** à l’aide du modèle de 2.</span><span class="sxs-lookup"><span data-stu-id="54491-243">However it may not be clear why it works that way when you pass both data events too**SERIALIZE** using model 2.</span></span>

<span data-ttu-id="54491-244">Ce comportement est toounderstand plus facile si vous connaissez les hypothèses hello que hello **sérialiseur** apporte de la bibliothèque.</span><span class="sxs-lookup"><span data-stu-id="54491-244">This behavior is easier toounderstand if you know hello assumptions that hello **serializer** library is making.</span></span> <span data-ttu-id="54491-245">toomake décryptage passons tooour précédent modèle :</span><span class="sxs-lookup"><span data-stu-id="54491-245">toomake sense of this let’s go back tooour model:</span></span>

```
DECLARE_MODEL(Thermostat,
WITH_DATA(int, Temperature),
WITH_DATA(int, Humidity),
WITH_DATA(EDM_DATE_TIME_OFFSET, Time)
);
```

<span data-ttu-id="54491-246">Pensez à ce modèle en tant que modèle orienté objets.</span><span class="sxs-lookup"><span data-stu-id="54491-246">Think of this model in object-oriented terms.</span></span> <span data-ttu-id="54491-247">Dans ce cas, nous allons modéliser un appareil physique (un thermostat) et cet appareil comprend des attributs tels que **Temperature** et **Humidity**.</span><span class="sxs-lookup"><span data-stu-id="54491-247">In this case we’re modeling a physical device (a thermostat) and that device includes attributes like **Temperature** and **Humidity**.</span></span>

<span data-ttu-id="54491-248">Nous pouvons envoyer un état d’entier hello de notre modèle avec le code suivant de hello :</span><span class="sxs-lookup"><span data-stu-id="54491-248">We can send hello entire state of our model with code such as hello following:</span></span>

```
if (SERIALIZE(&destination, &destinationSize, thermostat->Temperature, thermostat->Humidity, thermostat->Time) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

<span data-ttu-id="54491-249">En supposant que les valeurs hello de température, humidité et l’heure sont définies, nous verriez un événement comme cette tooIoT envoyé Hub :</span><span class="sxs-lookup"><span data-stu-id="54491-249">Assuming hello values of Temperature, Humidity and Time are set, we would see an event like this sent tooIoT Hub:</span></span>

```
{"Temperature":75, "Humidity":45, "Time":"2015-09-17T18:45:56Z"}
```

<span data-ttu-id="54491-250">Parfois, vous pouvez souhaiter que toosend *certains* propriétés du cloud de toohello modèle hello (cela est particulièrement vrai si votre modèle contient un grand nombre d’événements de données).</span><span class="sxs-lookup"><span data-stu-id="54491-250">Sometimes you may only want toosend *some* properties of hello model toohello cloud (this is especially true if your model contains a large number of data events).</span></span> <span data-ttu-id="54491-251">Il est utile toosend uniquement un sous-ensemble d’événements de données, comme dans notre précédent exemple :</span><span class="sxs-lookup"><span data-stu-id="54491-251">It’s useful toosend only a subset of data events, such as in our earlier example:</span></span>

```
{"Temperature":75, "Time":"2015-09-17T18:45:56Z"}
```

<span data-ttu-id="54491-252">Cette opération génère exactement hello même sérialisée des événements comme si nous avions défini un **TemperatureEvent** avec un **température** et **temps** membre, comme nous avec modèle 1.</span><span class="sxs-lookup"><span data-stu-id="54491-252">This generates exactly hello same serialized event as if we had defined a **TemperatureEvent** with a **Temperature** and **Time** member, just as we did with model 1.</span></span> <span data-ttu-id="54491-253">Dans ce cas, nous avons pu toogenerate exactement hello même sérialisé événement à l’aide d’un autre modèle (2), car nous avons appelé **SERIALIZE** d’une manière différente.</span><span class="sxs-lookup"><span data-stu-id="54491-253">In this case we were able toogenerate exactly hello same serialized event by using a different model (model 2) because we called **SERIALIZE** in a different way.</span></span>

<span data-ttu-id="54491-254">Hello point important est que si vous passez plusieurs événements de données trop**SERIALIZE,** puis il suppose que chaque événement est une propriété dans un seul objet JSON.</span><span class="sxs-lookup"><span data-stu-id="54491-254">hello important point is that if you pass multiple data events too**SERIALIZE,** then it assumes each event is a property in a single JSON object.</span></span>

<span data-ttu-id="54491-255">Hello meilleure approche dépend de vous et comment vous réfléchissez à votre modèle.</span><span class="sxs-lookup"><span data-stu-id="54491-255">hello best approach depends on you and how you think about your model.</span></span> <span data-ttu-id="54491-256">Si vous l’envoyez « événements » toohello cloud et chaque événement contient un ensemble défini de propriétés, première approche de hello rend très utile.</span><span class="sxs-lookup"><span data-stu-id="54491-256">If you’re sending "events" toohello cloud and each event contains a defined set of properties, then hello first approach makes a lot of sense.</span></span> <span data-ttu-id="54491-257">Dans ce cas, vous utiliseriez **DECLARE\_STRUCT** toodefine hello la structure de chaque événement et les inclure dans votre modèle avec hello **WITH\_données** (macro).</span><span class="sxs-lookup"><span data-stu-id="54491-257">In that case you would use **DECLARE\_STRUCT** toodefine hello structure of each event and then include them in your model with hello **WITH\_DATA** macro.</span></span> <span data-ttu-id="54491-258">Puis vous envoyez chaque événement comme dans le premier exemple hello ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="54491-258">Then you send each event as we did in hello first example above.</span></span> <span data-ttu-id="54491-259">Dans cette approche vous pouvez uniquement passer un événement de données trop**sérialiseur**.</span><span class="sxs-lookup"><span data-stu-id="54491-259">In this approach you would only pass a single data event too**SERIALIZER**.</span></span>

<span data-ttu-id="54491-260">Si vous pensez que sur votre modèle de manière orientée objet, puis deuxième approche de hello peut-être répondre à vous.</span><span class="sxs-lookup"><span data-stu-id="54491-260">If you think about your model in an object-oriented fashion, then hello second approach may suit you.</span></span> <span data-ttu-id="54491-261">Hello dans ce cas, les éléments définis à l’aide de **WITH\_données** hello « propriétés » de votre objet.</span><span class="sxs-lookup"><span data-stu-id="54491-261">In this case, hello elements defined using **WITH\_DATA** are hello "properties" of your object.</span></span> <span data-ttu-id="54491-262">Vous passez le sous-ensemble d’événements trop**SERIALIZE** que vous le souhaitez, en fonction de la part de vos état de l’objet « » vous toosend toohello cloud.</span><span class="sxs-lookup"><span data-stu-id="54491-262">You pass whatever subset of events too**SERIALIZE** that you like, depending on how much of your "object’s" state you want toosend toohello cloud.</span></span>

<span data-ttu-id="54491-263">Aucune approche n’est meilleure que l’autre.</span><span class="sxs-lookup"><span data-stu-id="54491-263">Nether approach is right or wrong.</span></span> <span data-ttu-id="54491-264">Soyez conscient de façon hello **sérialiseur** fonctionne de la bibliothèque et une nouvelle approche de modélisation hello choix qui répond le mieux à vos besoins.</span><span class="sxs-lookup"><span data-stu-id="54491-264">Just be aware of how hello **serializer** library works, and pick hello modeling approach that best fits your needs.</span></span>

## <a name="message-handling"></a><span data-ttu-id="54491-265">Gestion des messages</span><span class="sxs-lookup"><span data-stu-id="54491-265">Message handling</span></span>
<span data-ttu-id="54491-266">Jusqu'à présent cet article a traité uniquement envoi événements tooIoT Hub et n’a pas traité la réception des messages.</span><span class="sxs-lookup"><span data-stu-id="54491-266">So far this article has only discussed sending events tooIoT Hub, and hasn't addressed receiving messages.</span></span> <span data-ttu-id="54491-267">Hello raison pour ce qui est ce que nous devons tooknow sur la réception des messages a principalement été traité dans un [précédemment article](iot-hub-device-sdk-c-intro.md).</span><span class="sxs-lookup"><span data-stu-id="54491-267">hello reason for this is that what we need tooknow about receiving messages has largely been covered in an [earlier article](iot-hub-device-sdk-c-intro.md).</span></span> <span data-ttu-id="54491-268">Rappel de cet article : vous traitez les messages en enregistrant une fonction de rappel de message :</span><span class="sxs-lookup"><span data-stu-id="54491-268">Recall from that article that you process messages by registering a message callback function:</span></span>

```
IoTHubClient_SetMessageCallback(iotHubClientHandle, IoTHubMessage, myWeather)
```

<span data-ttu-id="54491-269">Vous écrivez ensuite la fonction de rappel hello est appelée lorsqu’un message est reçu :</span><span class="sxs-lookup"><span data-stu-id="54491-269">You then write hello callback function that’s invoked when a message is received:</span></span>

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

<span data-ttu-id="54491-270">Cette implémentation de **IoTHubMessage** appels hello fonction spécifique pour chaque action dans votre modèle.</span><span class="sxs-lookup"><span data-stu-id="54491-270">This implementation of **IoTHubMessage** calls hello specific function for each action in your model.</span></span> <span data-ttu-id="54491-271">Par exemple, si votre modèle définit cette action :</span><span class="sxs-lookup"><span data-stu-id="54491-271">For example, if your model defines this action:</span></span>

```
WITH_ACTION(SetAirResistance, int, Position)
```

<span data-ttu-id="54491-272">Vous devez définir une fonction avec cette signature :</span><span class="sxs-lookup"><span data-stu-id="54491-272">You must define a function with this signature:</span></span>

```
EXECUTE_COMMAND_RESULT SetAirResistance(ContosoAnemometer* device, int Position)
{
    (void)device;
    (void)printf("Setting Air Resistance Position too%d.\r\n", Position);
    return EXECUTE_COMMAND_SUCCESS;
}
```

<span data-ttu-id="54491-273">**SetAirResistance** est ensuite appelé lorsque ce message est envoyé à tooyour appareil.</span><span class="sxs-lookup"><span data-stu-id="54491-273">**SetAirResistance** is then called when that message is sent tooyour device.</span></span>

<span data-ttu-id="54491-274">Nous n’avons pas expliqué est encore version hello sérialisé de message ressemble.</span><span class="sxs-lookup"><span data-stu-id="54491-274">What we haven't explained yet is what hello serialized version of message looks like.</span></span> <span data-ttu-id="54491-275">En d’autres termes, si vous voulez toosend un **SetAirResistance** périphérique tooyour de message, ce qui, qui recherchent ?</span><span class="sxs-lookup"><span data-stu-id="54491-275">In other words, if you want toosend a **SetAirResistance** message tooyour device, what does that look like?</span></span>

<span data-ttu-id="54491-276">Si vous envoyez un périphérique tooa de message, vous le faites via le SDK du service de Azure IoT hello.</span><span class="sxs-lookup"><span data-stu-id="54491-276">If you're sending a message tooa device, you would do so through hello Azure IoT service SDK.</span></span> <span data-ttu-id="54491-277">Vous devez toujours tooknow quelle chaîne toosend tooinvoke une action particulière.</span><span class="sxs-lookup"><span data-stu-id="54491-277">You still need tooknow what string toosend tooinvoke a particular action.</span></span> <span data-ttu-id="54491-278">format général de Hello pour envoyer un message s’affiche comme suit :</span><span class="sxs-lookup"><span data-stu-id="54491-278">hello general format for sending a message appears as follows:</span></span>

```
{"Name" : "", "Parameters" : "" }
```

<span data-ttu-id="54491-279">Vous envoyez un objet JSON sérialisé avec deux propriétés : **nom** hello désigne l’action hello (message) et **paramètres** contient des paramètres hello de cette action.</span><span class="sxs-lookup"><span data-stu-id="54491-279">You're sending a serialized JSON object with two properties: **Name** is hello name of hello action (message) and **Parameters** contains hello parameters of that action.</span></span>

<span data-ttu-id="54491-280">Par exemple, tooinvoke **SetAirResistance** vous pouvez envoyer cet appareil tooa de message :</span><span class="sxs-lookup"><span data-stu-id="54491-280">For example, tooinvoke **SetAirResistance** you can send this message tooa device:</span></span>

```
{"Name" : "SetAirResistance", "Parameters" : { "Position" : 5 }}
```

<span data-ttu-id="54491-281">nom de l’action Hello doit correspondre exactement à une action définie dans votre modèle.</span><span class="sxs-lookup"><span data-stu-id="54491-281">hello action name must exactly match an action defined in your model.</span></span> <span data-ttu-id="54491-282">les noms de paramètre Hello doivent correspondre également.</span><span class="sxs-lookup"><span data-stu-id="54491-282">hello parameter names must match as well.</span></span> <span data-ttu-id="54491-283">Notez également que la casse est respectée.</span><span class="sxs-lookup"><span data-stu-id="54491-283">Also note case sensitivity.</span></span> <span data-ttu-id="54491-284">**Name** et **Parameters** sont toujours en majuscules.</span><span class="sxs-lookup"><span data-stu-id="54491-284">**Name** and **Parameters** are always uppercase.</span></span> <span data-ttu-id="54491-285">Assurez-vous que cas de hello toomatch de votre nom d’action et les paramètres dans votre modèle.</span><span class="sxs-lookup"><span data-stu-id="54491-285">Make sure toomatch hello case of your action name and parameters in your model.</span></span> <span data-ttu-id="54491-286">Dans cet exemple, le nom de l’action hello est « SetAirResistance » et non « setairresistance ».</span><span class="sxs-lookup"><span data-stu-id="54491-286">In this example, hello action name is "SetAirResistance" and not "setairresistance".</span></span>

<span data-ttu-id="54491-287">Hello deux autres actions **TurnFanOn** et **TurnFanOff** peut être appelée en envoyant ces appareils tooa de messages :</span><span class="sxs-lookup"><span data-stu-id="54491-287">hello two other actions **TurnFanOn** and **TurnFanOff** can be invoked by sending these messages tooa device:</span></span>

```
{"Name" : "TurnFanOn", "Parameters" : {}}
{"Name" : "TurnFanOff", "Parameters" : {}}
```

<span data-ttu-id="54491-288">Cette section décrit tous les éléments nécessaires tooknow lors de l’envoi d’événements et de recevoir des messages avec hello **sérialiseur** bibliothèque.</span><span class="sxs-lookup"><span data-stu-id="54491-288">This section described everything you need tooknow when sending events and receiving messages with hello **serializer** library.</span></span> <span data-ttu-id="54491-289">Mais avant de poursuivre, intéressons-nous à certains paramètres que vous pouvez configurer pour contrôler la taille de votre modèle.</span><span class="sxs-lookup"><span data-stu-id="54491-289">Before moving on, let's cover some parameters you can configure that control how large your model is.</span></span>

## <a name="macro-configuration"></a><span data-ttu-id="54491-290">Configuration des macros</span><span class="sxs-lookup"><span data-stu-id="54491-290">Macro configuration</span></span>
<span data-ttu-id="54491-291">Si vous utilisez hello **sérialiseur** bibliothèque une partie importante de toobe du Kit de développement logiciel hello prenant en charge de se trouve dans la bibliothèque d’azure-c-partagé-utilitaire hello.</span><span class="sxs-lookup"><span data-stu-id="54491-291">If you’re using hello **Serializer** library an important part of hello SDK toobe aware of is found in hello azure-c-shared-utility library.</span></span>
<span data-ttu-id="54491-292">Si vous avez cloné référentiel hello Azure iot-sdk--c à partir de GitHub à l’aide hello--récursive option, vous trouverez cette bibliothèque d’utilitaires partagées ici :</span><span class="sxs-lookup"><span data-stu-id="54491-292">If you have cloned hello Azure-iot-sdk-c repository from GitHub using hello --recursive option, then you will find this shared utility library here:</span></span>

```
.\\c-utility
```

<span data-ttu-id="54491-293">Si vous n’avez pas cloné bibliothèque de hello, vous pouvez le trouver [ici](https://github.com/Azure/azure-c-shared-utility).</span><span class="sxs-lookup"><span data-stu-id="54491-293">If you have not cloned hello library, you can find it [here](https://github.com/Azure/azure-c-shared-utility).</span></span>

<span data-ttu-id="54491-294">Dans la bibliothèque d’utilitaires partagées hello, vous trouverez hello suivant du dossier :</span><span class="sxs-lookup"><span data-stu-id="54491-294">Within hello shared utility library, you will find hello following folder:</span></span>

```
azure-c-shared-utility\\macro\_utils\_h\_generator.
```

<span data-ttu-id="54491-295">Ce dossier contient une solution Visual Studio appelée **macro\_utils\_h\_generator.sln** :</span><span class="sxs-lookup"><span data-stu-id="54491-295">This folder contains a Visual Studio solution called **macro\_utils\_h\_generator.sln**:</span></span>

  ![](media/iot-hub-device-sdk-c-serializer/01-macro_utils_h_generator.PNG)

<span data-ttu-id="54491-296">programme Hello dans cette solution génère hello **macro\_utils.h** fichier.</span><span class="sxs-lookup"><span data-stu-id="54491-296">hello program in this solution generates hello **macro\_utils.h** file.</span></span> <span data-ttu-id="54491-297">Il existe une macro par défaut\_fichier utils.h inclus avec le Kit de développement logiciel de hello.</span><span class="sxs-lookup"><span data-stu-id="54491-297">There’s a default macro\_utils.h file included with hello SDK.</span></span> <span data-ttu-id="54491-298">Cette solution vous permet de toomodify quelques paramètres et le recréer puis hello fichier d’en-tête en fonction de ces paramètres.</span><span class="sxs-lookup"><span data-stu-id="54491-298">This solution allows you toomodify some parameters and then recreate hello header file based on these parameters.</span></span>

<span data-ttu-id="54491-299">les paramètres de clé Hello deux toobe concerné avec sont **nArithmetic** et **nMacroParameters** qui sont définies dans ces deux lignes trouvées dans la macro\_utils.tt :</span><span class="sxs-lookup"><span data-stu-id="54491-299">hello two key parameters toobe concerned with are **nArithmetic** and **nMacroParameters** which are defined in these two lines found in macro\_utils.tt:</span></span>

```
<#int nArithmetic=1024;#>
<#int nMacroParameters=124;/*127 parameters in one macro deﬁnition in C99 in chapter 5.2.4.1 Translation limits*/#>

```

<span data-ttu-id="54491-300">Ces valeurs sont les paramètres par défaut hello inclus avec le Kit de développement logiciel de hello.</span><span class="sxs-lookup"><span data-stu-id="54491-300">These values are hello default parameters included with hello SDK.</span></span> <span data-ttu-id="54491-301">Chaque paramètre a hello suivant signification :</span><span class="sxs-lookup"><span data-stu-id="54491-301">Each parameter has hello following meaning:</span></span>

* <span data-ttu-id="54491-302">nMacroParameters : contrôle le nombre de paramètres que vous pouvez avoir dans une définition de macro DECLARE\_MODEL.</span><span class="sxs-lookup"><span data-stu-id="54491-302">nMacroParameters – Controls how many parameters you can have in one DECLARE\_MODEL macro definition.</span></span>
* <span data-ttu-id="54491-303">nArithmetic – nombre total de contrôles hello de membres autorisé dans un modèle.</span><span class="sxs-lookup"><span data-stu-id="54491-303">nArithmetic – Controls hello total number of members allowed in a model.</span></span>

<span data-ttu-id="54491-304">Hello que ces paramètres sont importants est car elles contrôlent la taille votre modèle.</span><span class="sxs-lookup"><span data-stu-id="54491-304">hello reason these parameters are important is because they control how large your model can be.</span></span> <span data-ttu-id="54491-305">Par exemple, prenez cette définition de modèle :</span><span class="sxs-lookup"><span data-stu-id="54491-305">For example, consider this model definition:</span></span>

```
DECLARE_MODEL(MyModel,
WITH_DATA(int, MyData)
);
```

<span data-ttu-id="54491-306">Comme mentionné précédemment, **DECLARE\_MODEL** est une simple macro C.</span><span class="sxs-lookup"><span data-stu-id="54491-306">As mentioned previously, **DECLARE\_MODEL** is just a C macro.</span></span> <span data-ttu-id="54491-307">Hello des noms de modèle de hello et hello **WITH\_données** instruction (encore une autre macro) est des paramètres de **DECLARE\_modèle**.</span><span class="sxs-lookup"><span data-stu-id="54491-307">hello names of hello model and hello **WITH\_DATA** statement (yet another macro) are parameters of **DECLARE\_MODEL**.</span></span> <span data-ttu-id="54491-308">**nMacroParameters** définit le nombre de paramètres qui peuvent être inclus dans **DECLARE\_MODEL**.</span><span class="sxs-lookup"><span data-stu-id="54491-308">**nMacroParameters** defines how many parameters can be included in **DECLARE\_MODEL**.</span></span> <span data-ttu-id="54491-309">Ces éléments définissent effectivement le nombre possible de déclarations d’événements de données et d’actions.</span><span class="sxs-lookup"><span data-stu-id="54491-309">Effectively, this defines how many data event and action declarations you can have.</span></span> <span data-ttu-id="54491-310">Par conséquent, la limite par défaut hello 124 cela signifie que vous pouvez définir un modèle avec une combinaison d’environ 60 actions et les événements de données.</span><span class="sxs-lookup"><span data-stu-id="54491-310">As such, with hello default limit of 124 this means that you can define a model with a combination of about 60 actions and data events.</span></span> <span data-ttu-id="54491-311">Si vous essayez tooexceed cette limite, vous recevrez les erreurs du compilateur rechercher toothis similaire :</span><span class="sxs-lookup"><span data-stu-id="54491-311">If you try tooexceed this limit, you'll receive compiler errors that look similar toothis:</span></span>

  ![](media/iot-hub-device-sdk-c-serializer/02-nMacroParametersCompilerErrors.PNG)

<span data-ttu-id="54491-312">Hello **nArithmetic** paramètre est plus sur le fonctionnement interne de hello du langage de macro hello de votre application.</span><span class="sxs-lookup"><span data-stu-id="54491-312">hello **nArithmetic** parameter is more about hello internal workings of hello macro language than your application.</span></span>  <span data-ttu-id="54491-313">Elle contrôle le nombre total de hello de membres que vous avez dans votre modèle, y compris **DECLARE_STRUCT** macros.</span><span class="sxs-lookup"><span data-stu-id="54491-313">It controls hello total number of members you can have in your model, including **DECLARE_STRUCT** macros.</span></span> <span data-ttu-id="54491-314">Donc si vous commencez à voir des erreurs du compilateur comme celles-ci, essayez d’augmenter **nArithmetic**:</span><span class="sxs-lookup"><span data-stu-id="54491-314">If you start seeing compiler errors such as this, then you should try increasing **nArithmetic**:</span></span>

   ![](media/iot-hub-device-sdk-c-serializer/03-nArithmeticCompilerErrors.PNG)

<span data-ttu-id="54491-315">Si vous souhaitez toochange ces paramètres, modifiez les valeurs hello macro hello\_utils.tt fichier, recompile hello macro\_utils\_h\_generator.sln solution et un programme compilé d’exécution hello.</span><span class="sxs-lookup"><span data-stu-id="54491-315">If you want toochange these parameters, modify hello values in hello macro\_utils.tt file, recompile hello macro\_utils\_h\_generator.sln solution, and run hello compiled program.</span></span> <span data-ttu-id="54491-316">Quand vous procédez ainsi, une nouvelle macro\_utils.h fichier est généré et placé dans hello.\\ Common\\active de inc.</span><span class="sxs-lookup"><span data-stu-id="54491-316">When you do so, a new macro\_utils.h file is generated and placed in hello .\\common\\inc directory.</span></span>

<span data-ttu-id="54491-317">Dans la nouvelle version de hello de toouse d’ordre de la macro\_utils.h, remove hello **sérialiseur** package NuGet à partir de votre solution et à la place inclure hello **sérialiseur** projet Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="54491-317">In order toouse hello new version of macro\_utils.h, remove hello **serializer** NuGet package from your solution and in its place include hello **serializer** Visual Studio project.</span></span> <span data-ttu-id="54491-318">Cela permet à votre toocompile code contre le code source de hello de bibliothèque de sérialiseur hello.</span><span class="sxs-lookup"><span data-stu-id="54491-318">This enables your code toocompile against hello source code of hello serializer library.</span></span> <span data-ttu-id="54491-319">Cela inclut la macro hello mis à jour\_utils.h.</span><span class="sxs-lookup"><span data-stu-id="54491-319">This includes hello updated macro\_utils.h.</span></span> <span data-ttu-id="54491-320">Si vous le souhaitez toodo pour **simplesample\_amqp**, commencez par supprimer le package NuGet de hello pour la bibliothèque de sérialiseur hello à partir de la solution de hello :</span><span class="sxs-lookup"><span data-stu-id="54491-320">If you want toodo this for **simplesample\_amqp**, start by removing hello NuGet package for hello serializer library from hello solution:</span></span>

   ![](media/iot-hub-device-sdk-c-serializer/04-serializer-github-package.PNG)

<span data-ttu-id="54491-321">Ajoutez ensuite ce tooyour projet solution Visual Studio :</span><span class="sxs-lookup"><span data-stu-id="54491-321">Then add this project tooyour Visual Studio solution:</span></span>

> <span data-ttu-id="54491-322">.\\c\\serializer\\build\\windows\\serializer.vcxproj</span><span class="sxs-lookup"><span data-stu-id="54491-322">.\\c\\serializer\\build\\windows\\serializer.vcxproj</span></span>
> 
> 

<span data-ttu-id="54491-323">Lorsque vous avez terminé, votre solution doit ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="54491-323">When you're done, your solution should look like this:</span></span>

   ![](media/iot-hub-device-sdk-c-serializer/05-serializer-project.PNG)

<span data-ttu-id="54491-324">Maintenant lorsque vous compilez votre solution, hello de mise à jour la macro\_utils.h est inclus dans votre fichier binaire.</span><span class="sxs-lookup"><span data-stu-id="54491-324">Now when you compile your solution, hello updated macro\_utils.h is included in your binary.</span></span>

<span data-ttu-id="54491-325">Notez qu’en augmentant ces valeurs à un niveau assez élevé, elles peuvent dépasser les limites du compilateur.</span><span class="sxs-lookup"><span data-stu-id="54491-325">Note that increasing these values high enough can exceed compiler limits.</span></span> <span data-ttu-id="54491-326">toothis point, hello **nMacroParameters** est hello paramètre principal qui toobe concerné.</span><span class="sxs-lookup"><span data-stu-id="54491-326">toothis point, hello **nMacroParameters** is hello main parameter with which toobe concerned.</span></span> <span data-ttu-id="54491-327">norme C99 Hello Spécifie qu’un minimum de 127 paramètres sont autorisés dans une définition de macro.</span><span class="sxs-lookup"><span data-stu-id="54491-327">hello C99 spec specifies that a minimum of 127 parameters are allowed in a macro definition.</span></span> <span data-ttu-id="54491-328">Hello compilateur Microsoft suit exactement les spécifications de hello (et est limité à 127), donc vous ne serez pas en mesure de tooincrease **nMacroParameters** au-delà de la valeur par défaut hello.</span><span class="sxs-lookup"><span data-stu-id="54491-328">hello Microsoft compiler follows hello spec exactly (and has a limit of 127), so you won't be able tooincrease **nMacroParameters** beyond hello default.</span></span> <span data-ttu-id="54491-329">Autres compilateurs peuvent vous permettre de toodo donc (par exemple, hello GNU compilateur prend en charge une limite plus élevée).</span><span class="sxs-lookup"><span data-stu-id="54491-329">Other compilers might allow you toodo so (for example, hello GNU compiler supports a higher limit).</span></span>

<span data-ttu-id="54491-330">Jusqu'à présent, nous avons couvert quasiment tous les éléments nécessaires tooknow sur la façon dont toowrite code avec hello **sérialiseur** bibliothèque.</span><span class="sxs-lookup"><span data-stu-id="54491-330">So far we've covered just about everything you need tooknow about how toowrite code with hello **serializer** library.</span></span> <span data-ttu-id="54491-331">Avant de conclure, nous allons revoir certaines rubriques d’articles précédents qui amènent peut-être des questions.</span><span class="sxs-lookup"><span data-stu-id="54491-331">Before concluding, let's revisit some topics from previous articles that you may be wondering about.</span></span>

## <a name="hello-lower-level-apis"></a><span data-ttu-id="54491-332">Hello API de niveau inférieur</span><span class="sxs-lookup"><span data-stu-id="54491-332">hello lower-level APIs</span></span>
<span data-ttu-id="54491-333">exemple d’application Hello sur lequel cet article actif est **simplesample\_amqp**.</span><span class="sxs-lookup"><span data-stu-id="54491-333">hello sample application on which this article focused is **simplesample\_amqp**.</span></span> <span data-ttu-id="54491-334">Cet exemple utilise hello (hello non-« LL ») API toosend événements de niveau supérieur et recevoir des messages.</span><span class="sxs-lookup"><span data-stu-id="54491-334">This sample uses hello higher-level (hello non-"LL") APIs toosend events and receive messages.</span></span> <span data-ttu-id="54491-335">Si vous utilisez ces API, un thread d’arrière-plan s’exécute, prenant en charge l’envoi d’événements et la réception de messages.</span><span class="sxs-lookup"><span data-stu-id="54491-335">If you use these APIs, a background thread runs which takes care of both sending events and receiving messages.</span></span> <span data-ttu-id="54491-336">Toutefois, vous pouvez utiliser hello niveau inférieur (II) API tooeliminate ce thread d’arrière-plan et prendre le contrôle explicit lorsque vous envoyez des événements ou recevez des messages à partir du cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="54491-336">However, you can use hello lower-level (LL) APIs tooeliminate this background thread and take explicit control over when you send events or receive messages from hello cloud.</span></span>

<span data-ttu-id="54491-337">Comme décrit dans un [article précédent](iot-hub-device-sdk-c-iothubclient.md), il existe un ensemble de fonctions qui se compose de hello API de niveau supérieur :</span><span class="sxs-lookup"><span data-stu-id="54491-337">As described in a [previous article](iot-hub-device-sdk-c-iothubclient.md), there is a set of functions that consists of hello higher-level APIs:</span></span>

* <span data-ttu-id="54491-338">IoTHubClient\_CreateFromConnectionString</span><span class="sxs-lookup"><span data-stu-id="54491-338">IoTHubClient\_CreateFromConnectionString</span></span>
* <span data-ttu-id="54491-339">IoTHubClient\_SendEventAsync</span><span class="sxs-lookup"><span data-stu-id="54491-339">IoTHubClient\_SendEventAsync</span></span>
* <span data-ttu-id="54491-340">IoTHubClient\_SetMessageCallback</span><span class="sxs-lookup"><span data-stu-id="54491-340">IoTHubClient\_SetMessageCallback</span></span>
* <span data-ttu-id="54491-341">IoTHubClient\_Destroy</span><span class="sxs-lookup"><span data-stu-id="54491-341">IoTHubClient\_Destroy</span></span>

<span data-ttu-id="54491-342">Ces API sont décrites dans **simplesample\_amqp**.</span><span class="sxs-lookup"><span data-stu-id="54491-342">These APIs are demonstrated in **simplesample\_amqp**.</span></span>

<span data-ttu-id="54491-343">Il existe également un ensemble d’API de niveau inférieur analogue.</span><span class="sxs-lookup"><span data-stu-id="54491-343">There is also an analogous set of lower-level APIs.</span></span>

* <span data-ttu-id="54491-344">IoTHubClient\_LL\_CreateFromConnectionString</span><span class="sxs-lookup"><span data-stu-id="54491-344">IoTHubClient\_LL\_CreateFromConnectionString</span></span>
* <span data-ttu-id="54491-345">IoTHubClient\_LL\_SendEventAsync</span><span class="sxs-lookup"><span data-stu-id="54491-345">IoTHubClient\_LL\_SendEventAsync</span></span>
* <span data-ttu-id="54491-346">IoTHubClient\_LL\_SetMessageCallback</span><span class="sxs-lookup"><span data-stu-id="54491-346">IoTHubClient\_LL\_SetMessageCallback</span></span>
* <span data-ttu-id="54491-347">IoTHubClient\_LL\_Destroy</span><span class="sxs-lookup"><span data-stu-id="54491-347">IoTHubClient\_LL\_Destroy</span></span>

<span data-ttu-id="54491-348">Notez que travail d’API de niveau inférieur hello hello exactement comme décrit dans les articles précédents hello.</span><span class="sxs-lookup"><span data-stu-id="54491-348">Note that hello lower-level APIs work exactly hello same way as described in hello previous articles.</span></span> <span data-ttu-id="54491-349">Vous pouvez utiliser le premier jeu d’API de hello si vous souhaitez un toohandle de thread d’arrière-plan, l’envoi d’événements et de recevoir des messages.</span><span class="sxs-lookup"><span data-stu-id="54491-349">You can use hello first set of APIs if you want a background thread toohandle sending events and receiving messages.</span></span> <span data-ttu-id="54491-350">Vous utilisez hello deuxième ensemble d’API si vous souhaitez contrôler explicitement lorsque vous envoyez et recevez des données d’IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="54491-350">You use hello second set of APIs if you want explicit control over when you send and receive data from IoT Hub.</span></span> <span data-ttu-id="54491-351">L’ensemble du travail de l’API indifféremment avec hello **sérialiseur** bibliothèque.</span><span class="sxs-lookup"><span data-stu-id="54491-351">Either set of APIs work equally well with hello **serializer** library.</span></span>

<span data-ttu-id="54491-352">Pour obtenir un exemple de hello API de niveau inférieur est utilisés avec hello **sérialiseur** bibliothèque, consultez hello **simplesample\_http** application.</span><span class="sxs-lookup"><span data-stu-id="54491-352">For an example of how hello lower-level APIs are used with hello **serializer** library, see hello **simplesample\_http** application.</span></span>

## <a name="additional-topics"></a><span data-ttu-id="54491-353">Rubriques supplémentaires</span><span class="sxs-lookup"><span data-stu-id="54491-353">Additional topics</span></span>
<span data-ttu-id="54491-354">Voici quelques autres sujets qu’il est intéressant de mentionner à nouveau : gestion des propriétés, utilisation d’autres informations d’identification sur l’appareil et options de configuration.</span><span class="sxs-lookup"><span data-stu-id="54491-354">A few other topics worth mentioning again are property handling, using alternate device credentials, and configuration options.</span></span> <span data-ttu-id="54491-355">Toutes ces rubriques sont traitées dans un [article précédent](iot-hub-device-sdk-c-iothubclient.md).</span><span class="sxs-lookup"><span data-stu-id="54491-355">These are all topics covered in a [previous article](iot-hub-device-sdk-c-iothubclient.md).</span></span> <span data-ttu-id="54491-356">Hello essentiel est que toutes ces fonctionnalités fonctionnent Bonjour même façon avec hello **sérialiseur** bibliothèque comme ils le font avec hello **IoTHubClient** bibliothèque.</span><span class="sxs-lookup"><span data-stu-id="54491-356">hello main point is that all of these features work in hello same way with hello **serializer** library as they do with hello **IoTHubClient** library.</span></span> <span data-ttu-id="54491-357">Par exemple, si vous souhaitez que les événements de tooan tooattach propriétés à partir de votre modèle, vous utilisez **IoTHubMessage\_propriétés** et **carte**\_**AddorUpdate**, comme décrit précédemment hello :</span><span class="sxs-lookup"><span data-stu-id="54491-357">For example, if you want tooattach properties tooan event from your model, you use **IoTHubMessage\_Properties** and **Map**\_**AddorUpdate**, hello same way as described previously:</span></span>

```
MAP_HANDLE propMap = IoTHubMessage_Properties(message.messageHandle);
sprintf_s(propText, sizeof(propText), "%d", i);
Map_AddOrUpdate(propMap, "SequenceNumber", propText);
```

<span data-ttu-id="54491-358">Si les événements hello a été générée à partir de hello **sérialiseur** bibliothèque ou créées manuellement à l’aide de hello **IoTHubClient** bibliothèque n’a pas d’importance.</span><span class="sxs-lookup"><span data-stu-id="54491-358">Whether hello event was generated from hello **serializer** library or created manually using hello **IoTHubClient** library does not matter.</span></span>

<span data-ttu-id="54491-359">Hello pour les autres informations d’identification de l’appareil, à l’aide de **IoTHubClient\_LL\_créer** fonctionne aussi bien en tant que **IoTHubClient\_CreateFromConnectionString** pour allouer un **IOTHUB\_CLIENT\_gérer**.</span><span class="sxs-lookup"><span data-stu-id="54491-359">For hello alternate device credentials, using **IoTHubClient\_LL\_Create** works just as well as **IoTHubClient\_CreateFromConnectionString** for allocating an **IOTHUB\_CLIENT\_HANDLE**.</span></span>

<span data-ttu-id="54491-360">Enfin, si vous utilisez hello **sérialiseur** bibliothèque, vous pouvez définir des options de configuration avec **IoTHubClient\_LL\_SetOption** tout comme vous l’avez fait lors de l’utilisation de hello **IoTHubClient** bibliothèque.</span><span class="sxs-lookup"><span data-stu-id="54491-360">Finally, if you're using hello **serializer** library, you can set configuration options with **IoTHubClient\_LL\_SetOption** just as you did when using hello **IoTHubClient** library.</span></span>

<span data-ttu-id="54491-361">Une fonctionnalité unique toohello **sérialiseur** bibliothèque sont l’initialisation de hello API.</span><span class="sxs-lookup"><span data-stu-id="54491-361">A feature that is unique toohello **serializer** library are hello initialization APIs.</span></span> <span data-ttu-id="54491-362">Avant de commencer à travailler avec la bibliothèque de hello, vous devez appeler **sérialiseur\_init**:</span><span class="sxs-lookup"><span data-stu-id="54491-362">Before you can start working with hello library, you must call **serializer\_init**:</span></span>

```
serializer_init(NULL);
```

<span data-ttu-id="54491-363">Cet appel doit être effectué juste avant l’appel de **IoTHubClient\_CreateFromConnectionString**.</span><span class="sxs-lookup"><span data-stu-id="54491-363">This is done just before you call **IoTHubClient\_CreateFromConnectionString**.</span></span>

<span data-ttu-id="54491-364">De même, lorsque vous avez terminé hello dernier appel vous apporterez utilisez hello bibliothèque, est trop**sérialiseur\_deinit**:</span><span class="sxs-lookup"><span data-stu-id="54491-364">Similarly, when you're done working with hello library, hello last call you’ll make is too**serializer\_deinit**:</span></span>

```
serializer_deinit();
```

<span data-ttu-id="54491-365">Dans le cas contraire, tous les hello autres fonctionnalités répertoriées ci-dessus travail hello même Bonjour **sérialiseur** bibliothèque comme Bonjour **IoTHubClient** bibliothèque.</span><span class="sxs-lookup"><span data-stu-id="54491-365">Otherwise, all of hello other features listed above work hello same in hello **serializer** library as they do in hello **IoTHubClient** library.</span></span> <span data-ttu-id="54491-366">Pour plus d’informations sur ces rubriques, consultez hello [article précédent](iot-hub-device-sdk-c-iothubclient.md) dans cette série.</span><span class="sxs-lookup"><span data-stu-id="54491-366">For more information about any of these topics, see hello [previous article](iot-hub-device-sdk-c-iothubclient.md) in this series.</span></span>

## <a name="next-steps"></a><span data-ttu-id="54491-367">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="54491-367">Next steps</span></span>
<span data-ttu-id="54491-368">Cet article décrit en détail hello particularités de hello **sérialiseur** bibliothèque contenue dans hello **appareil Azure IoT SDK pour C**. Avec les informations de hello fournies, vous devez avoir une bonne compréhension de la toouse modélise les événements toosend et recevoir des messages de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="54491-368">This article describes in detail hello unique aspects of hello **serializer** library contained in hello **Azure IoT device SDK for C**. With hello information provided you should have a good understanding of how toouse models toosend events and receive messages from IoT Hub.</span></span>

<span data-ttu-id="54491-369">Ceci conclut également série en trois parties hello sur la façon dont les applications toodevelop avec hello **appareil Azure IoT SDK pour C**. Cela doit être suffisamment d’informations toonot obtenez que vous avez démarré mais vous donner une bonne compréhension du fonctionnement de l’API de hello.</span><span class="sxs-lookup"><span data-stu-id="54491-369">This also concludes hello three-part series on how toodevelop applications with hello **Azure IoT device SDK for C**. This should be enough information toonot only get you started but give you a thorough understanding of how hello APIs work.</span></span> <span data-ttu-id="54491-370">Pour plus d’informations, il existe quelques exemples Bonjour que SDK pas couverts ici.</span><span class="sxs-lookup"><span data-stu-id="54491-370">For additional information, there are a few samples in hello SDK not covered here.</span></span> <span data-ttu-id="54491-371">Dans le cas contraire, hello [documentation du Kit de développement logiciel](https://github.com/Azure/azure-iot-sdk-c) constitue une bonne ressource pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="54491-371">Otherwise, hello [SDK documentation](https://github.com/Azure/azure-iot-sdk-c) is a good resource for additional information.</span></span>

<span data-ttu-id="54491-372">toolearn plus sur le développement pour IoT Hub, consultez hello [kits de développement logiciel Azure IoT][lnk-sdks].</span><span class="sxs-lookup"><span data-stu-id="54491-372">toolearn more about developing for IoT Hub, see hello [Azure IoT SDKs][lnk-sdks].</span></span>

<span data-ttu-id="54491-373">toofurther Explorez les fonctionnalités de hello d’IoT Hub, consultez :</span><span class="sxs-lookup"><span data-stu-id="54491-373">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="54491-374">[Simulation d’un appareil avec Azure IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="54491-374">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
