---
title: "Azure IoT device SDK pour C - Serializer | Microsoft Docs"
description: "Guide d’utilisation de la bibliothèque Serializer dans Azure IoT device SDK pour C pour créer des applications d’appareil qui communiquent avec un IoT Hub."
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
ms.openlocfilehash: aa03c29c54d75538b1fdf987cac5f09d5d344f73
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-iot-device-sdk-for-c--more-about-serializer"></a><span data-ttu-id="b71e5-103">Kit de développement logiciel (SDK) Azure IoT device pour C : en savoir plus sur serializer</span><span class="sxs-lookup"><span data-stu-id="b71e5-103">Azure IoT device SDK for C – more about serializer</span></span>
<span data-ttu-id="b71e5-104">Le [premier article](iot-hub-device-sdk-c-intro.md) de cette série a présenté le **Kit de développement logiciel (SDK) d’appareil Azure IoT (Azure IoT device SDK) pour C**. L’article suivant donne une description plus détaillée [**d’IoTHubClient**](iot-hub-device-sdk-c-iothubclient.md).</span><span class="sxs-lookup"><span data-stu-id="b71e5-104">The [first article](iot-hub-device-sdk-c-intro.md) in this series introduced the **Azure IoT device SDK for C**. The next article provided a more detailed description of the [**IoTHubClient**](iot-hub-device-sdk-c-iothubclient.md).</span></span> <span data-ttu-id="b71e5-105">Dans cet article, nous terminerons sur le sujet du Kit de développement logiciel (SDK) avec une description plus détaillée du composant restant : la bibliothèque **sérialiseur** .</span><span class="sxs-lookup"><span data-stu-id="b71e5-105">This article completes coverage of the SDK by providing a more detailed description of the remaining component: the **serializer** library.</span></span>

<span data-ttu-id="b71e5-106">L’article d’introduction décrit comment utiliser la bibliothèque **sérialiseur** pour envoyer des événements et recevoir des messages vers et depuis IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="b71e5-106">The introductory article described how to use the **serializer** library to send events to and receive messages from IoT Hub.</span></span> <span data-ttu-id="b71e5-107">Dans cet article, nous allons approfondir en fournissant une explication plus complète de la façon de modéliser vos données avec le langage de macro **sérialiseur** .</span><span class="sxs-lookup"><span data-stu-id="b71e5-107">In this article, we extend that discussion by providing a more complete explanation of how to model your data with the **serializer** macro language.</span></span> <span data-ttu-id="b71e5-108">L’article inclut également plus de détails sur la façon dont la bibliothèque sérialise les messages (et dans certains cas comment vous pouvez contrôler le comportement de sérialisation).</span><span class="sxs-lookup"><span data-stu-id="b71e5-108">The article also includes more detail about how the library serializes messages (and in some cases how you can control the serialization behavior).</span></span> <span data-ttu-id="b71e5-109">Nous décrirons également certains paramètres que vous pouvez modifier déterminant la taille des modèles que vous créez.</span><span class="sxs-lookup"><span data-stu-id="b71e5-109">We'll also describe some parameters you can modify that determine the size of the models you create.</span></span>

<span data-ttu-id="b71e5-110">En conclusion, nous reverrons certains des sujets abordés dans les articles précédents, notamment la gestion des messages et des propriétés.</span><span class="sxs-lookup"><span data-stu-id="b71e5-110">Finally, the article revisits some topics covered in previous articles such as message and property handling.</span></span> <span data-ttu-id="b71e5-111">Mais comme vous allez le voir, ces fonctionnalités fonctionnent de la même manière que celles de la bibliothèque **serializer** ou la bibliothèque **IoTHubClient**.</span><span class="sxs-lookup"><span data-stu-id="b71e5-111">As we'll find out, those features work in the same way using the **serializer** library as they do with the **IoTHubClient** library.</span></span>

<span data-ttu-id="b71e5-112">Toutes les procédures décrites dans cet article sont basées sur des exemples du Kit de développement logiciel (SDK) du **sérialiseur** .</span><span class="sxs-lookup"><span data-stu-id="b71e5-112">Everything described in this article is based on the **serializer** SDK samples.</span></span> <span data-ttu-id="b71e5-113">Si vous souhaitez approfondir, consultez les applications **simplesample\_amqp** et **simplesample\_http** incluses dans le Kit de développement logiciel (SDK) d’appareil Azure IoT (Azure IoT device SDK) pour C.</span><span class="sxs-lookup"><span data-stu-id="b71e5-113">If you want to follow along, see the **simplesample\_amqp** and **simplesample\_http** applications included in the Azure IoT device SDK for C.</span></span>

<span data-ttu-id="b71e5-114">Vous trouverez [**Azure IoT device SDK pour C**](https://github.com/Azure/azure-iot-sdk-c) dans le référentiel GitHub. Vous pouvez consulter les détails de l’[API dans Référence de l’API C](https://azure.github.io/azure-iot-sdk-c/index.html).</span><span class="sxs-lookup"><span data-stu-id="b71e5-114">You can find the [**Azure IoT device SDK for C**](https://github.com/Azure/azure-iot-sdk-c) GitHub repository and view details of the API in the [C API reference](https://azure.github.io/azure-iot-sdk-c/index.html).</span></span>

## <a name="the-modeling-language"></a><span data-ttu-id="b71e5-115">Le langage de modélisation</span><span class="sxs-lookup"><span data-stu-id="b71e5-115">The modeling language</span></span>
<span data-ttu-id="b71e5-116">[L’article d’introduction](iot-hub-device-sdk-c-intro.md) de cette série a présenté le langage de modélisation du **Kit de développement logiciel (SDK) d’appareil Azure IoT (Azure IoT device SDK) pour C** via l’exemple fourni dans l’application **simplesample\_amqp** :</span><span class="sxs-lookup"><span data-stu-id="b71e5-116">The [introductory article](iot-hub-device-sdk-c-intro.md) in this series introduced the **Azure IoT device SDK for C** modeling language through the example provided in the **simplesample\_amqp** application:</span></span>

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

<span data-ttu-id="b71e5-117">Comme vous pouvez le voir, le langage de modélisation est basé sur les macros C.</span><span class="sxs-lookup"><span data-stu-id="b71e5-117">As you can see, the modeling language is based on C macros.</span></span> <span data-ttu-id="b71e5-118">La définition commence toujours par **BEGIN\_NAMESPACE** et se termine toujours par **END\_NAMESPACE**.</span><span class="sxs-lookup"><span data-stu-id="b71e5-118">You always begin your definition with **BEGIN\_NAMESPACE** and always end with **END\_NAMESPACE**.</span></span> <span data-ttu-id="b71e5-119">Il est courant d’affecter à l’espace de noms le nom de votre entreprise ou le nom du projet sur lequel vous travaillez, comme c’est le cas dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="b71e5-119">It's common to name the namespace for your company or, as in this example, the project that you're working on.</span></span>

<span data-ttu-id="b71e5-120">À l’intérieur de l’espace de noms figurent les définitions de modèles.</span><span class="sxs-lookup"><span data-stu-id="b71e5-120">What goes inside the namespace are model definitions.</span></span> <span data-ttu-id="b71e5-121">Dans ce cas, il s’agit d’un modèle unique pour un anémomètre.</span><span class="sxs-lookup"><span data-stu-id="b71e5-121">In this case, there is a single model for an anemometer.</span></span> <span data-ttu-id="b71e5-122">Là encore, n’importe quel nom peut être affecté au modèle, mais en règle générale, on lui affecte le nom de l’appareil ou le type de données que vous souhaitez échanger avec IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="b71e5-122">Once again, the model can be named anything, but typically this is named for the device or type of data you want to exchange with IoT Hub.</span></span>  

<span data-ttu-id="b71e5-123">Les modèles contiennent une définition des événements que vous pouvez entrer dans IoT Hub (les *données*), ainsi que les messages que vous pouvez recevoir depuis IoT Hub (les *actions*).</span><span class="sxs-lookup"><span data-stu-id="b71e5-123">Models contain a definition of the events you can ingress to IoT Hub (the *data*) as well as the messages you can receive from IoT Hub (the *actions*).</span></span> <span data-ttu-id="b71e5-124">Comme vous pouvez le constater dans cet exemple, les événements ont un type et un nom ; les actions ont un nom et des paramètres facultatifs (chacun avec un type).</span><span class="sxs-lookup"><span data-stu-id="b71e5-124">As you can see from the example, events have a type and a name; actions have a name and optional parameters (each with a type).</span></span>

<span data-ttu-id="b71e5-125">Cet exemple n’illustre pas les types de données supplémentaires pris en charge par le Kit de développement logiciel (SDK).</span><span class="sxs-lookup"><span data-stu-id="b71e5-125">What’s not demonstrated in this sample are additional data types that are supported by the SDK.</span></span> <span data-ttu-id="b71e5-126">Nous allons aborder ce point par la suite.</span><span class="sxs-lookup"><span data-stu-id="b71e5-126">We'll cover that next.</span></span>

> [!NOTE]
> <span data-ttu-id="b71e5-127">IoT Hub désigne les données qu’il reçoit d’un appareil par le terme *événements*, tandis que le langage de modélisation les désigne par le terme *données* (définies à l’aide de l’instruction **WITH_DATA**).</span><span class="sxs-lookup"><span data-stu-id="b71e5-127">IoT Hub refers to the data a device sends to it as *events*, while the modeling language refers to it as *data* (defined using **WITH_DATA**).</span></span> <span data-ttu-id="b71e5-128">De la même façon, IoT Hub désigne les données envoyées à un appareil par le terme *messages*, tandis que le langage de modélisation les désigne par le terme *actions* (définies à l’aide de l’instruction **WITH_ACTION**).</span><span class="sxs-lookup"><span data-stu-id="b71e5-128">Likewise, IoT Hub refers to the data you send to devices as *messages*, while the modeling language refers to it as *actions* (defined using **WITH_ACTION**).</span></span> <span data-ttu-id="b71e5-129">Sachez que ces termes peuvent être utilisés de manière interchangeable dans cet article.</span><span class="sxs-lookup"><span data-stu-id="b71e5-129">Be aware that these terms may be used interchangeably in this article.</span></span>
> 
> 

### <a name="supported-data-types"></a><span data-ttu-id="b71e5-130">Types de données pris en charge</span><span class="sxs-lookup"><span data-stu-id="b71e5-130">Supported data types</span></span>
<span data-ttu-id="b71e5-131">Les types de données suivants sont pris en charge dans les modèles créés avec la bibliothèque **serializer** :</span><span class="sxs-lookup"><span data-stu-id="b71e5-131">The following data types are supported in models created with the **serializer** library:</span></span>

| <span data-ttu-id="b71e5-132">Type</span><span class="sxs-lookup"><span data-stu-id="b71e5-132">Type</span></span> | <span data-ttu-id="b71e5-133">Description</span><span class="sxs-lookup"><span data-stu-id="b71e5-133">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b71e5-134">double</span><span class="sxs-lookup"><span data-stu-id="b71e5-134">double</span></span> |<span data-ttu-id="b71e5-135">nombre à virgule flottante double précision</span><span class="sxs-lookup"><span data-stu-id="b71e5-135">double precision floating point number</span></span> |
| <span data-ttu-id="b71e5-136">int</span><span class="sxs-lookup"><span data-stu-id="b71e5-136">int</span></span> |<span data-ttu-id="b71e5-137">entier 32 bits</span><span class="sxs-lookup"><span data-stu-id="b71e5-137">32 bit integer</span></span> |
| <span data-ttu-id="b71e5-138">float</span><span class="sxs-lookup"><span data-stu-id="b71e5-138">float</span></span> |<span data-ttu-id="b71e5-139">nombre à virgule flottante simple précision</span><span class="sxs-lookup"><span data-stu-id="b71e5-139">single precision floating point number</span></span> |
| <span data-ttu-id="b71e5-140">long</span><span class="sxs-lookup"><span data-stu-id="b71e5-140">long</span></span> |<span data-ttu-id="b71e5-141">entier long</span><span class="sxs-lookup"><span data-stu-id="b71e5-141">long integer</span></span> |
| <span data-ttu-id="b71e5-142">int8\_t</span><span class="sxs-lookup"><span data-stu-id="b71e5-142">int8\_t</span></span> |<span data-ttu-id="b71e5-143">entier 8 bits</span><span class="sxs-lookup"><span data-stu-id="b71e5-143">8 bit integer</span></span> |
| <span data-ttu-id="b71e5-144">int16\_t</span><span class="sxs-lookup"><span data-stu-id="b71e5-144">int16\_t</span></span> |<span data-ttu-id="b71e5-145">entier 16 bits</span><span class="sxs-lookup"><span data-stu-id="b71e5-145">16 bit integer</span></span> |
| <span data-ttu-id="b71e5-146">int32\_t</span><span class="sxs-lookup"><span data-stu-id="b71e5-146">int32\_t</span></span> |<span data-ttu-id="b71e5-147">entier 32 bits</span><span class="sxs-lookup"><span data-stu-id="b71e5-147">32 bit integer</span></span> |
| <span data-ttu-id="b71e5-148">int64\_t</span><span class="sxs-lookup"><span data-stu-id="b71e5-148">int64\_t</span></span> |<span data-ttu-id="b71e5-149">entier 64 bits</span><span class="sxs-lookup"><span data-stu-id="b71e5-149">64 bit integer</span></span> |
| <span data-ttu-id="b71e5-150">valeur booléenne</span><span class="sxs-lookup"><span data-stu-id="b71e5-150">bool</span></span> |<span data-ttu-id="b71e5-151">booléenne</span><span class="sxs-lookup"><span data-stu-id="b71e5-151">boolean</span></span> |
| <span data-ttu-id="b71e5-152">ascii\_char\_ptr</span><span class="sxs-lookup"><span data-stu-id="b71e5-152">ascii\_char\_ptr</span></span> |<span data-ttu-id="b71e5-153">Chaîne ASCII</span><span class="sxs-lookup"><span data-stu-id="b71e5-153">ASCII string</span></span> |
| <span data-ttu-id="b71e5-154">EDM\_DATE\_TIME\_OFFSET</span><span class="sxs-lookup"><span data-stu-id="b71e5-154">EDM\_DATE\_TIME\_OFFSET</span></span> |<span data-ttu-id="b71e5-155">décalage de date et d’heure</span><span class="sxs-lookup"><span data-stu-id="b71e5-155">date time offset</span></span> |
| <span data-ttu-id="b71e5-156">EDM\_GUID</span><span class="sxs-lookup"><span data-stu-id="b71e5-156">EDM\_GUID</span></span> |<span data-ttu-id="b71e5-157">GUID</span><span class="sxs-lookup"><span data-stu-id="b71e5-157">GUID</span></span> |
| <span data-ttu-id="b71e5-158">EDM\_BINARY</span><span class="sxs-lookup"><span data-stu-id="b71e5-158">EDM\_BINARY</span></span> |<span data-ttu-id="b71e5-159">binaire</span><span class="sxs-lookup"><span data-stu-id="b71e5-159">binary</span></span> |
| <span data-ttu-id="b71e5-160">DECLARE\_STRUCT</span><span class="sxs-lookup"><span data-stu-id="b71e5-160">DECLARE\_STRUCT</span></span> |<span data-ttu-id="b71e5-161">type de données complexe</span><span class="sxs-lookup"><span data-stu-id="b71e5-161">complex data type</span></span> |

<span data-ttu-id="b71e5-162">Commençons par ce dernier type de données.</span><span class="sxs-lookup"><span data-stu-id="b71e5-162">Let’s start with the last data type.</span></span> <span data-ttu-id="b71e5-163">L’argument **DECLARE\_STRUCT** vous permet de définir des types de données complexes, qui sont des regroupements des autres types primitifs.</span><span class="sxs-lookup"><span data-stu-id="b71e5-163">The **DECLARE\_STRUCT** allows you to define complex data types, which are groupings of the other primitive types.</span></span> <span data-ttu-id="b71e5-164">Ces regroupements permettent de définir un modèle qui ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="b71e5-164">These groupings allow us to define a model that looks like this:</span></span>

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

<span data-ttu-id="b71e5-165">Notre modèle contient un événement de données unique de type **TestType**.</span><span class="sxs-lookup"><span data-stu-id="b71e5-165">Our model contains a single data event of type **TestType**.</span></span> <span data-ttu-id="b71e5-166">**TestType** est un type complexe qui inclut plusieurs membres montrant collectivement les types primitifs pris en charge par le langage de modélisation de la bibliothèque **serializer**.</span><span class="sxs-lookup"><span data-stu-id="b71e5-166">**TestType** is a complex type that includes several members, which collectively demonstrate the primitive types supported by the **serializer** modeling language.</span></span>

<span data-ttu-id="b71e5-167">Pour envoyer des données à IoT Hub avec un modèle comme celui-là, nous pouvons écrire du code se présentant comme suit :</span><span class="sxs-lookup"><span data-stu-id="b71e5-167">With a model like this, we can write code to send data to IoT Hub that appears as follows:</span></span>

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

<span data-ttu-id="b71e5-168">En fait, nous attribuons une valeur à chaque membre de la structure **Test**, puis nous appelons **SendAsync** pour envoyer l’événement de données **Test** dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="b71e5-168">Basically, we’re assigning a value to every member of the **Test** structure and then calling **SendAsync** to send the **Test** data event to the cloud.</span></span> <span data-ttu-id="b71e5-169">**SendAsync** est une fonction d’assistance qui envoie un événement unique de données à IoT Hub :</span><span class="sxs-lookup"><span data-stu-id="b71e5-169">**SendAsync** is a helper function that sends a single data event to IoT Hub:</span></span>

```
void SendAsync(IOTHUB_CLIENT_LL_HANDLE iotHubClientHandle, const void *dataEvent)
{
    unsigned char* destination;
    size_t destinationSize;
    if (SERIALIZE(&destination, &destinationSize, *(const unsigned char*)dataEvent) ==
    {
        // null terminate the string
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

<span data-ttu-id="b71e5-170">Cette fonction sérialise l’événement de données et l’envoie à IoT Hub à l’aide de la commande **IoTHubClient\_SendEventAsync**.</span><span class="sxs-lookup"><span data-stu-id="b71e5-170">This function serializes the given data event and sends it to IoT Hub using **IoTHubClient\_SendEventAsync**.</span></span> <span data-ttu-id="b71e5-171">Il s’agit du même code que le code traité dans les articles précédents (**SendAsync** encapsule la logique dans une fonction pratique).</span><span class="sxs-lookup"><span data-stu-id="b71e5-171">This is the same code discussed in previous articles (**SendAsync** encapsulates the logic into a convenient function).</span></span>

<span data-ttu-id="b71e5-172">**GetDateTimeOffset**est une autre fonction d’assistance utilisée dans le code précédent.</span><span class="sxs-lookup"><span data-stu-id="b71e5-172">One other helper function used in the previous code is **GetDateTimeOffset**.</span></span> <span data-ttu-id="b71e5-173">Cette fonction transforme l’heure donnée en une valeur de type **EDM\_DATE\_TIME\_OFFSET** :</span><span class="sxs-lookup"><span data-stu-id="b71e5-173">This function transforms the given time into a value of type **EDM\_DATE\_TIME\_OFFSET**:</span></span>

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

<span data-ttu-id="b71e5-174">Si nous exécutons ce code, le message suivant est envoyé à IoT Hub :</span><span class="sxs-lookup"><span data-stu-id="b71e5-174">If you run this code, the following message is sent to IoT Hub:</span></span>

```
{"aDouble":1.100000000000000, "aInt":2, "aFloat":3.000000, "aLong":4, "aInt8":5, "auInt8":6, "aInt16":7, "aInt32":8, "aInt64":9, "aBool":true, "aAsciiCharPtr":"ascii string 1", "aDateTimeOffset":"2015-09-14T21:18:21Z", "aGuid":"00010203-0405-0607-0809-0A0B0C0D0E0F", "aBinary":"AQID"}
```

<span data-ttu-id="b71e5-175">Notez que la sérialisation se fait en JSON, le format généré par la bibliothèque **serializer** .</span><span class="sxs-lookup"><span data-stu-id="b71e5-175">Note that the serialization is JSON, which is the format generated by the **serializer** library.</span></span> <span data-ttu-id="b71e5-176">Notez également que chaque membre de l’objet JSON sérialisé correspond aux membres de la structure **TestType** définie dans notre modèle.</span><span class="sxs-lookup"><span data-stu-id="b71e5-176">Also note that each member of the serialized JSON object matches the members of the **TestType** that we defined in our model.</span></span> <span data-ttu-id="b71e5-177">Les valeurs correspondent également exactement à celles que nous avons utilisées dans le code.</span><span class="sxs-lookup"><span data-stu-id="b71e5-177">The values also exactly match those used in the code.</span></span> <span data-ttu-id="b71e5-178">Toutefois, notez que les données binaires sont codées en base 64 : « AQID » est l’encodage en base 64 de {0x01, 0x02, 0x03}.</span><span class="sxs-lookup"><span data-stu-id="b71e5-178">However, note that the binary data is base64-encoded: "AQID" is the base64 encoding of {0x01, 0x02, 0x03}.</span></span>

<span data-ttu-id="b71e5-179">Cet exemple montre l’avantage que procure l’utilisation de la bibliothèque **serializer** : elle permet d’envoyer le code JSON dans le cloud, sans avoir à gérer explicitement la sérialisation dans notre application.</span><span class="sxs-lookup"><span data-stu-id="b71e5-179">This example demonstrates the advantage of using the **serializer** library -- it enables us to send JSON to the cloud, without having to explicitly deal with serialization in our application.</span></span> <span data-ttu-id="b71e5-180">Il vous suffit de définir les valeurs des événements de données dans notre modèle, puis d’appeler des API simples pour envoyer ces événements dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="b71e5-180">All we have to worry about is setting the values of the data events in our model and then calling simple APIs to send those events to the cloud.</span></span>

<span data-ttu-id="b71e5-181">Avec les informations ci-dessus, nous pouvons définir des modèles qui incluent la plage des types de données pris en charge, notamment des types complexes (et le cas échéant, nous pouvons même inclure des types complexes au sein d’autres types complexes).</span><span class="sxs-lookup"><span data-stu-id="b71e5-181">With this information, we can define models that include the range of supported data types, including complex types (we could even include complex types within other complex types).</span></span> <span data-ttu-id="b71e5-182">Cependant, le code JSON sérialisé généré par l’exemple ci-dessus soulève un point important.</span><span class="sxs-lookup"><span data-stu-id="b71e5-182">However, he serialized JSON generated by the example above brings up an important point.</span></span> <span data-ttu-id="b71e5-183">*façon* dont nous envoyons des données avec la bibliothèque **sérialiseur** détermine exactement comment le code JSON est formé.</span><span class="sxs-lookup"><span data-stu-id="b71e5-183">*How* we send data with the **serializer** library determines exactly how the JSON is formed.</span></span> <span data-ttu-id="b71e5-184">C’est ce point particulier que nous allons ensuite aborder.</span><span class="sxs-lookup"><span data-stu-id="b71e5-184">That particular point is what we'll cover next.</span></span>

## <a name="more-about-serialization"></a><span data-ttu-id="b71e5-185">En savoir plus sur la sérialisation</span><span class="sxs-lookup"><span data-stu-id="b71e5-185">More about serialization</span></span>
<span data-ttu-id="b71e5-186">La section précédente présente un exemple de la sortie générée par la bibliothèque **serializer** .</span><span class="sxs-lookup"><span data-stu-id="b71e5-186">The previous section highlights an example of the output generated by the **serializer** library.</span></span> <span data-ttu-id="b71e5-187">Dans cette section, nous allons expliquer comment la bibliothèque sérialise les données et la façon dont vous pouvez contrôler ce comportement à l’aide des API de sérialisation.</span><span class="sxs-lookup"><span data-stu-id="b71e5-187">In this section, we'll explain how the library serializes data and how you can control that behavior using the serialization APIs.</span></span>

<span data-ttu-id="b71e5-188">Pour faire progresser la discussion sur la sérialisation, nous allons utiliser un nouveau modèle basé sur un thermostat.</span><span class="sxs-lookup"><span data-stu-id="b71e5-188">In order to advance the discussion on serialization, we'll work with a new model based on a thermostat.</span></span> <span data-ttu-id="b71e5-189">Tout d’abord, définissons le contexte du scénario que nous tentons de traiter.</span><span class="sxs-lookup"><span data-stu-id="b71e5-189">First, let's provide some background on the scenario we're trying to address.</span></span>

<span data-ttu-id="b71e5-190">Nous souhaitons modéliser un thermostat qui mesure la température et l’humidité.</span><span class="sxs-lookup"><span data-stu-id="b71e5-190">We want to model a thermostat that measures temperature and humidity.</span></span> <span data-ttu-id="b71e5-191">Chaque élément de données va être envoyé à IoT Hub de façon différente.</span><span class="sxs-lookup"><span data-stu-id="b71e5-191">Each piece of data is going to be sent to IoT Hub differently.</span></span> <span data-ttu-id="b71e5-192">Par défaut, le thermostat saisit un événement de température toutes les 2 minutes ; un événement d’humidité est entré toutes les 15 minutes.</span><span class="sxs-lookup"><span data-stu-id="b71e5-192">By default, the thermostat ingresses a temperature event once every 2 minutes; a humidity event is ingressed once every 15 minutes.</span></span> <span data-ttu-id="b71e5-193">Quand l’un de ces événements est entré, il doit inclure un horodatage, c’est-à-dire l’heure à laquelle la température ou l’humidité correspondante a été mesurée.</span><span class="sxs-lookup"><span data-stu-id="b71e5-193">When either event is ingressed, it must include a timestamp that shows the time that the corresponding temperature or humidity was measured.</span></span>

<span data-ttu-id="b71e5-194">Sur la base de ce scénario, nous allons montrer deux façons différentes de modéliser les données et nous allons expliquer l’effet de la modélisation sur la sortie sérialisée.</span><span class="sxs-lookup"><span data-stu-id="b71e5-194">Given this scenario, we'll demonstrate two different ways to model the data, and we'll explain the effect that modeling has on the serialized output.</span></span>

### <a name="model-1"></a><span data-ttu-id="b71e5-195">Modèle n° 1</span><span class="sxs-lookup"><span data-stu-id="b71e5-195">Model 1</span></span>
<span data-ttu-id="b71e5-196">Voici la première version d’un modèle prenant en charge le scénario précédent :</span><span class="sxs-lookup"><span data-stu-id="b71e5-196">Here's the first version of a model that supports the previous scenario:</span></span>

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

<span data-ttu-id="b71e5-197">Notez que le modèle inclut deux événements de données : **Temperature** et **Humidity**.</span><span class="sxs-lookup"><span data-stu-id="b71e5-197">Note that the model includes two data events: **Temperature** and **Humidity**.</span></span> <span data-ttu-id="b71e5-198">Contrairement aux exemples précédents, le type de chaque événement est une structure définie à l’aide de l’instruction **DECLARE\_STRUCT**.</span><span class="sxs-lookup"><span data-stu-id="b71e5-198">Unlike previous examples, the type of each event is a structure defined using **DECLARE\_STRUCT**.</span></span> <span data-ttu-id="b71e5-199">**TemperatureEvent** comprend une mesure de température et un horodatage ; **HumidityEvent** contient une mesure d’humidité et un horodatage.</span><span class="sxs-lookup"><span data-stu-id="b71e5-199">**TemperatureEvent** includes a temperature measurement and a timestamp; **HumidityEvent** contains a humidity measurement and a timestamp.</span></span> <span data-ttu-id="b71e5-200">Ce modèle propose une façon naturelle de modéliser les données du scénario décrit ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="b71e5-200">This model gives us a natural way to model the data for the scenario described above.</span></span> <span data-ttu-id="b71e5-201">Quand nous envoyons un événement dans le cloud, il s’agit soit d’une paire température/horodatage, soit d’une paire humidité/horodatage.</span><span class="sxs-lookup"><span data-stu-id="b71e5-201">When we send an event to the cloud, we'll either send a temperature/timestamp or a humidity/timestamp pair.</span></span>

<span data-ttu-id="b71e5-202">Nous pouvons envoyer un événement de température dans le cloud à l’aide d’un code similaire tel que celui qui suit :</span><span class="sxs-lookup"><span data-stu-id="b71e5-202">We can send a temperature event to the cloud using code such as the following:</span></span>

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

<span data-ttu-id="b71e5-203">Nous allons utiliser des valeurs codées en dur pour la température et l’humidité dans l’exemple de code, mais imaginez que nous récupérions en fait ces valeurs par échantillonnage des capteurs correspondants sur le thermostat.</span><span class="sxs-lookup"><span data-stu-id="b71e5-203">We'll use hard-coded values for temperature and humidity in the sample code, but imagine that we’re actually retrieving these values by sampling the corresponding sensors on the thermostat.</span></span>

<span data-ttu-id="b71e5-204">Le code ci-dessus utilise l’outil d’assistance **GetDateTimeOffset** présenté précédemment.</span><span class="sxs-lookup"><span data-stu-id="b71e5-204">The code above uses the **GetDateTimeOffset** helper that was introduced previously.</span></span> <span data-ttu-id="b71e5-205">Et, pour des raisons qui s’éclairciront plus loin, ce code sépare la tâche de sérialisation et d’envoi de l’événement.</span><span class="sxs-lookup"><span data-stu-id="b71e5-205">For reasons that will become clear later, this code explicitly separates the task of serializing and sending the event.</span></span> <span data-ttu-id="b71e5-206">Le code précédent sérialise l’événement de température dans une mémoire tampon.</span><span class="sxs-lookup"><span data-stu-id="b71e5-206">The previous code serializes the temperature event into a buffer.</span></span> <span data-ttu-id="b71e5-207">La fonction d’assistance **sendMessage** (incluse dans **simplesample\_amqp**) envoie alors l’événement à IoT Hub :</span><span class="sxs-lookup"><span data-stu-id="b71e5-207">Then, **sendMessage** is a helper function (included in **simplesample\_amqp**) that sends the event to IoT Hub:</span></span>

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

<span data-ttu-id="b71e5-208">Ce code est un sous-ensemble de l’outil d’assistance **SendAsync** décrit dans la section précédente. Nous n’allons donc pas revenir dessus.</span><span class="sxs-lookup"><span data-stu-id="b71e5-208">This code is a subset of the **SendAsync** helper described in the previous section, so we won’t go over it again here.</span></span>

<span data-ttu-id="b71e5-209">Lorsque nous exécutons le code précédent pour envoyer l’événement de température, ce format sérialisé de l’événement est envoyé à IoT Hub :</span><span class="sxs-lookup"><span data-stu-id="b71e5-209">When we run the previous code to send the Temperature event, this serialized form of the event is sent to IoT Hub:</span></span>

```
{"Temperature":75, "Time":"2015-09-17T18:45:56Z"}
```

<span data-ttu-id="b71e5-210">Nous allons envoyer une température de type **TemperatureEvent** et cette structure contient un membre **Temperature** et **Time**.</span><span class="sxs-lookup"><span data-stu-id="b71e5-210">We're sending a temperature which is of type **TemperatureEvent** and that struct contains a **Temperature** and **Time** member.</span></span> <span data-ttu-id="b71e5-211">Ceci est reflété directement dans les données sérialisées.</span><span class="sxs-lookup"><span data-stu-id="b71e5-211">This is directly reflected in the serialized data.</span></span>

<span data-ttu-id="b71e5-212">De même, nous pouvons envoyer un événement d’humidité avec ce code :</span><span class="sxs-lookup"><span data-stu-id="b71e5-212">Similarly, we can send a humidity event with this code:</span></span>

```
thermostat->Humidity.Humidity = 45;
thermostat->Humidity.Time = GetDateTimeOffset(now);
if (SERIALIZE(&destination, &destinationSize, thermostat->Humidity) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

<span data-ttu-id="b71e5-213">Le format sérialisé envoyé à IoT Hub se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="b71e5-213">The serialized form that’s sent to IoT Hub appears as follows:</span></span>

```
{"Humidity":45, "Time":"2015-09-17T18:45:56Z"}
```

<span data-ttu-id="b71e5-214">Comme attendu, là encore.</span><span class="sxs-lookup"><span data-stu-id="b71e5-214">Again, this is as expected.</span></span>

<span data-ttu-id="b71e5-215">Avec ce modèle, vous pouvez voir comment d’autres événements peuvent facilement être ajoutés.</span><span class="sxs-lookup"><span data-stu-id="b71e5-215">With this model, you can imagine how additional events can easily be added.</span></span> <span data-ttu-id="b71e5-216">Vous définissez d’autres structures à l’aide de **DECLARE\_STRUCT**, et incluez l’événement correspondant dans le modèle à l’aide de **WITH\_DATA**.</span><span class="sxs-lookup"><span data-stu-id="b71e5-216">You define more structures using **DECLARE\_STRUCT**, and include the corresponding event in the model using **WITH\_DATA**.</span></span>

<span data-ttu-id="b71e5-217">À présent, nous allons modifier le modèle afin qu’il inclue les mêmes données, mais avec une structure différente.</span><span class="sxs-lookup"><span data-stu-id="b71e5-217">Now, let’s modify the model so that it includes the same data but with a different structure.</span></span>

### <a name="model-2"></a><span data-ttu-id="b71e5-218">Modèle n° 2</span><span class="sxs-lookup"><span data-stu-id="b71e5-218">Model 2</span></span>
<span data-ttu-id="b71e5-219">Voici un modèle alternatif à celui proposé ci-dessus :</span><span class="sxs-lookup"><span data-stu-id="b71e5-219">Consider this alternative model to the one above:</span></span>

```
DECLARE_MODEL(Thermostat,
WITH_DATA(int, Temperature),
WITH_DATA(int, Humidity),
WITH_DATA(EDM_DATE_TIME_OFFSET, Time)
);
```

<span data-ttu-id="b71e5-220">Dans ce cas, nous avons éliminé les macros **DECLARE\_STRUCT** et nous définissons simplement les éléments de données à partir de notre scénario à l’aide de types simples du langage de modélisation.</span><span class="sxs-lookup"><span data-stu-id="b71e5-220">In this case we've eliminated the **DECLARE\_STRUCT** macros and are simply defining the data items from our scenario using simple types from the modeling language.</span></span>

<span data-ttu-id="b71e5-221">Pour le moment, nous allons ignorer l’événement **Time** .</span><span class="sxs-lookup"><span data-stu-id="b71e5-221">Just for the moment let’s ignore the **Time** event.</span></span> <span data-ttu-id="b71e5-222">Ceci mis à part, voici le code pour entrer l’événement **Temperature**:</span><span class="sxs-lookup"><span data-stu-id="b71e5-222">With that aside, here’s the code to ingress **Temperature**:</span></span>

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

<span data-ttu-id="b71e5-223">Ce code envoie l’événement suivant sérialisé à IoT Hub :</span><span class="sxs-lookup"><span data-stu-id="b71e5-223">This code sends the following serialized event to IoT Hub:</span></span>

```
{"Temperature":75}
```

<span data-ttu-id="b71e5-224">Et le code pour l’envoi de l’événement Humidity ressemble à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="b71e5-224">And the code for sending the Humidity event appears as follows:</span></span>

```
thermostat->Humidity = 45;
if (SERIALIZE(&destination, &destinationSize, thermostat->Humidity) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

<span data-ttu-id="b71e5-225">Ce code envoie ceci à IoT Hub :</span><span class="sxs-lookup"><span data-stu-id="b71e5-225">This code sends this to IoT Hub:</span></span>

```
{"Humidity":45}
```

<span data-ttu-id="b71e5-226">Jusqu’à présent, toujours pas de surprise.</span><span class="sxs-lookup"><span data-stu-id="b71e5-226">So far there are still no surprises.</span></span> <span data-ttu-id="b71e5-227">Mais nous allons modifier notre façon d’utiliser la macro SERIALIZE.</span><span class="sxs-lookup"><span data-stu-id="b71e5-227">Now let's change how we use the SERIALIZE macro.</span></span>

<span data-ttu-id="b71e5-228">La macro **SERIALIZE** peut utiliser plusieurs événements de données comme arguments.</span><span class="sxs-lookup"><span data-stu-id="b71e5-228">The **SERIALIZE** macro can take multiple data events as arguments.</span></span> <span data-ttu-id="b71e5-229">Cela nous permet de sérialiser les événements **Temperature** et **Humidity** ensemble et de les envoyer à IoT Hub par le biais d’un appel unique :</span><span class="sxs-lookup"><span data-stu-id="b71e5-229">This enables us to serialize the **Temperature** and **Humidity** event together and send them to IoT Hub in one call:</span></span>

```
if (SERIALIZE(&destination, &destinationSize, thermostat->Temperature, thermostat->Humidity) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

<span data-ttu-id="b71e5-230">L’on peut supposer que le résultat de ce code est l’envoi de deux événements de données à IoT Hub :</span><span class="sxs-lookup"><span data-stu-id="b71e5-230">You might guess that the result of this code is that two data events are sent to IoT Hub:</span></span>

<span data-ttu-id="b71e5-231">[</span><span class="sxs-lookup"><span data-stu-id="b71e5-231">[</span></span>

<span data-ttu-id="b71e5-232">{"Temperature":75},</span><span class="sxs-lookup"><span data-stu-id="b71e5-232">{"Temperature":75},</span></span>

<span data-ttu-id="b71e5-233">{"Humidity":45}</span><span class="sxs-lookup"><span data-stu-id="b71e5-233">{"Humidity":45}</span></span>

<span data-ttu-id="b71e5-234">]</span><span class="sxs-lookup"><span data-stu-id="b71e5-234">]</span></span>

<span data-ttu-id="b71e5-235">En d’autres termes, vous pouvez vous attendre à ce que ce code soit identique à l’envoi de **Temperature** et de **Humidity** séparément.</span><span class="sxs-lookup"><span data-stu-id="b71e5-235">In other words, you might expect that this code is the same as sending **Temperature** and **Humidity** separately.</span></span> <span data-ttu-id="b71e5-236">C’est pour des raisons de commodité que nous transmettons les événements à **SERIALISER** dans le même appel.</span><span class="sxs-lookup"><span data-stu-id="b71e5-236">It’s just a convenience to pass both events to **SERIALIZE** in the same call.</span></span> <span data-ttu-id="b71e5-237">Toutefois, ce n’est pas le cas.</span><span class="sxs-lookup"><span data-stu-id="b71e5-237">However, that’s not the case.</span></span> <span data-ttu-id="b71e5-238">Au lieu de cela, le code ci-dessus envoie cet événement de données unique à IoT Hub :</span><span class="sxs-lookup"><span data-stu-id="b71e5-238">Instead, the code above sends this single data event to IoT Hub:</span></span>

<span data-ttu-id="b71e5-239">{"Temperature":75, "Humidity":45}</span><span class="sxs-lookup"><span data-stu-id="b71e5-239">{"Temperature":75, "Humidity":45}</span></span>

<span data-ttu-id="b71e5-240">Cela peut sembler étrange, étant donné que notre modèle définit **Temperature** et **Humidity** comme deux événements *distincts* :</span><span class="sxs-lookup"><span data-stu-id="b71e5-240">This may seem strange because our model defines **Temperature** and **Humidity** as two *separate* events:</span></span>

```
DECLARE_MODEL(Thermostat,
WITH_DATA(int, Temperature),
WITH_DATA(int, Humidity),
WITH_DATA(EDM_DATE_TIME_OFFSET, Time)
);
```

<span data-ttu-id="b71e5-241">Plus précisément, nous n’avons pas modélisé ces événements où **Temperature** et **Humidity** se trouvent dans la même structure :</span><span class="sxs-lookup"><span data-stu-id="b71e5-241">More to the point, we didn’t model these events where **Temperature** and **Humidity** are in the same structure:</span></span>

```
DECLARE_STRUCT(TemperatureAndHumidityEvent,
int, Temperature,
int, Humidity,
);

DECLARE_MODEL(Thermostat,
WITH_DATA(TemperatureAndHumidityEvent, TemperatureAndHumidity),
);
```

<span data-ttu-id="b71e5-242">Si nous avions utilisé ce modèle, il serait plus facile de comprendre l’envoi de **Temperature** et **Humidity** dans le même message sérialisé.</span><span class="sxs-lookup"><span data-stu-id="b71e5-242">If we used this model, it would be easier to understand how **Temperature** and **Humidity** would be sent in the same serialized message.</span></span> <span data-ttu-id="b71e5-243">Cependant, il peut être difficile de comprendre ce fonctionnement quand vous transmettez les deux événements de données dans la macro **SERIALIZE** à l’aide du modèle n° 2.</span><span class="sxs-lookup"><span data-stu-id="b71e5-243">However it may not be clear why it works that way when you pass both data events to **SERIALIZE** using model 2.</span></span>

<span data-ttu-id="b71e5-244">Ce comportement est plus facile à comprendre si vous connaissez les hypothèses envisagées par la bibliothèque **serializer** .</span><span class="sxs-lookup"><span data-stu-id="b71e5-244">This behavior is easier to understand if you know the assumptions that the **serializer** library is making.</span></span> <span data-ttu-id="b71e5-245">Pour que ce soit plus clair, revenons à notre modèle :</span><span class="sxs-lookup"><span data-stu-id="b71e5-245">To make sense of this let’s go back to our model:</span></span>

```
DECLARE_MODEL(Thermostat,
WITH_DATA(int, Temperature),
WITH_DATA(int, Humidity),
WITH_DATA(EDM_DATE_TIME_OFFSET, Time)
);
```

<span data-ttu-id="b71e5-246">Pensez à ce modèle en tant que modèle orienté objets.</span><span class="sxs-lookup"><span data-stu-id="b71e5-246">Think of this model in object-oriented terms.</span></span> <span data-ttu-id="b71e5-247">Dans ce cas, nous allons modéliser un appareil physique (un thermostat) et cet appareil comprend des attributs tels que **Temperature** et **Humidity**.</span><span class="sxs-lookup"><span data-stu-id="b71e5-247">In this case we’re modeling a physical device (a thermostat) and that device includes attributes like **Temperature** and **Humidity**.</span></span>

<span data-ttu-id="b71e5-248">Nous pouvons envoyer l’état complet de notre modèle avec un code ressemblant à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="b71e5-248">We can send the entire state of our model with code such as the following:</span></span>

```
if (SERIALIZE(&destination, &destinationSize, thermostat->Temperature, thermostat->Humidity, thermostat->Time) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

<span data-ttu-id="b71e5-249">En supposant que les valeurs de température, d’humidité et d’heure sont définies, nous verrions un événement envoyé à IoT Hub, comme ceci :</span><span class="sxs-lookup"><span data-stu-id="b71e5-249">Assuming the values of Temperature, Humidity and Time are set, we would see an event like this sent to IoT Hub:</span></span>

```
{"Temperature":75, "Humidity":45, "Time":"2015-09-17T18:45:56Z"}
```

<span data-ttu-id="b71e5-250">Il peut arriver que vous souhaitiez envoyer uniquement *certaines* propriétés du modèle vers le cloud (cela est particulièrement vrai si votre modèle contient un grand nombre d’événements de données).</span><span class="sxs-lookup"><span data-stu-id="b71e5-250">Sometimes you may only want to send *some* properties of the model to the cloud (this is especially true if your model contains a large number of data events).</span></span> <span data-ttu-id="b71e5-251">Il est utile d’envoyer uniquement un sous-ensemble des événements de données, comme dans notre exemple précédent :</span><span class="sxs-lookup"><span data-stu-id="b71e5-251">It’s useful to send only a subset of data events, such as in our earlier example:</span></span>

```
{"Temperature":75, "Time":"2015-09-17T18:45:56Z"}
```

<span data-ttu-id="b71e5-252">Cela génère exactement le même événement sérialisé que si nous avions défini un **TemperatureEvent** avec un membre **Temperature** et **Time**, comme nous l’avons fait avec le modèle 1.</span><span class="sxs-lookup"><span data-stu-id="b71e5-252">This generates exactly the same serialized event as if we had defined a **TemperatureEvent** with a **Temperature** and **Time** member, just as we did with model 1.</span></span> <span data-ttu-id="b71e5-253">Dans ce cas, nous avons pu générer exactement le même événement sérialisé à l’aide d’un modèle différent (modèle n° 2), car nous avons appelé **SERIALIZE** différemment.</span><span class="sxs-lookup"><span data-stu-id="b71e5-253">In this case we were able to generate exactly the same serialized event by using a different model (model 2) because we called **SERIALIZE** in a different way.</span></span>

<span data-ttu-id="b71e5-254">Ici, le point important est que si vous transmettez plusieurs événements de données à **SERIALIZE** , cela suppose que chaque événement est une propriété dans un objet JSON unique.</span><span class="sxs-lookup"><span data-stu-id="b71e5-254">The important point is that if you pass multiple data events to **SERIALIZE,** then it assumes each event is a property in a single JSON object.</span></span>

<span data-ttu-id="b71e5-255">La meilleure façon de faire dépend de vous et de la façon dont vous pensez votre modèle.</span><span class="sxs-lookup"><span data-stu-id="b71e5-255">The best approach depends on you and how you think about your model.</span></span> <span data-ttu-id="b71e5-256">Si vous envoyez des « événements » dans le cloud et que chaque événement contient un ensemble défini de propriétés, la première approche est judicieuse.</span><span class="sxs-lookup"><span data-stu-id="b71e5-256">If you’re sending "events" to the cloud and each event contains a defined set of properties, then the first approach makes a lot of sense.</span></span> <span data-ttu-id="b71e5-257">Dans ce cas, vous utiliseriez **DECLARE\_STRUCT** pour définir la structure de chaque événement et l’inclure dans votre modèle avec la macro **WITH\_DATA**.</span><span class="sxs-lookup"><span data-stu-id="b71e5-257">In that case you would use **DECLARE\_STRUCT** to define the structure of each event and then include them in your model with the **WITH\_DATA** macro.</span></span> <span data-ttu-id="b71e5-258">Vous envoyez ensuite chaque événement, comme nous l’avons fait dans le premier exemple ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="b71e5-258">Then you send each event as we did in the first example above.</span></span> <span data-ttu-id="b71e5-259">Dans cette approche, vous transmettez uniquement un événement de données à **SERIALIZER**.</span><span class="sxs-lookup"><span data-stu-id="b71e5-259">In this approach you would only pass a single data event to **SERIALIZER**.</span></span>

<span data-ttu-id="b71e5-260">Si vous envisagez votre modèle comme un modèle orienté objet, la seconde approche peut vous correspondre.</span><span class="sxs-lookup"><span data-stu-id="b71e5-260">If you think about your model in an object-oriented fashion, then the second approach may suit you.</span></span> <span data-ttu-id="b71e5-261">Dans ce cas, les éléments définis à l’aide de **WITH\_DATA** sont les « propriétés » de votre objet.</span><span class="sxs-lookup"><span data-stu-id="b71e5-261">In this case, the elements defined using **WITH\_DATA** are the "properties" of your object.</span></span> <span data-ttu-id="b71e5-262">Vous transmettez à **SERIALIZE** n’importe quel sous-ensemble d’événements de votre choix, selon la quantité de votre « objet » à envoyer dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="b71e5-262">You pass whatever subset of events to **SERIALIZE** that you like, depending on how much of your "object’s" state you want to send to the cloud.</span></span>

<span data-ttu-id="b71e5-263">Aucune approche n’est meilleure que l’autre.</span><span class="sxs-lookup"><span data-stu-id="b71e5-263">Nether approach is right or wrong.</span></span> <span data-ttu-id="b71e5-264">Sachez que la bibliothèque **serializer** fonctionne ainsi et sélectionnez l’approche de modélisation qui correspond le mieux à vos besoins.</span><span class="sxs-lookup"><span data-stu-id="b71e5-264">Just be aware of how the **serializer** library works, and pick the modeling approach that best fits your needs.</span></span>

## <a name="message-handling"></a><span data-ttu-id="b71e5-265">Gestion des messages</span><span class="sxs-lookup"><span data-stu-id="b71e5-265">Message handling</span></span>
<span data-ttu-id="b71e5-266">Jusqu’à présent, cet article a étudié uniquement l’envoi d’événements vers IoT Hub et n’a pas abordé la réception de messages.</span><span class="sxs-lookup"><span data-stu-id="b71e5-266">So far this article has only discussed sending events to IoT Hub, and hasn't addressed receiving messages.</span></span> <span data-ttu-id="b71e5-267">La raison est la suivante : ce que vous devez savoir concernant la réception de messages a été largement couvert dans un [article précédent](iot-hub-device-sdk-c-intro.md).</span><span class="sxs-lookup"><span data-stu-id="b71e5-267">The reason for this is that what we need to know about receiving messages has largely been covered in an [earlier article](iot-hub-device-sdk-c-intro.md).</span></span> <span data-ttu-id="b71e5-268">Rappel de cet article : vous traitez les messages en enregistrant une fonction de rappel de message :</span><span class="sxs-lookup"><span data-stu-id="b71e5-268">Recall from that article that you process messages by registering a message callback function:</span></span>

```
IoTHubClient_SetMessageCallback(iotHubClientHandle, IoTHubMessage, myWeather)
```

<span data-ttu-id="b71e5-269">Vous écrivez ensuite la fonction de rappel invoquée à la réception d’un message :</span><span class="sxs-lookup"><span data-stu-id="b71e5-269">You then write the callback function that’s invoked when a message is received:</span></span>

```
static IOTHUBMESSAGE_DISPOSITION_RESULT IoTHubMessage(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    IOTHUBMESSAGE_DISPOSITION_RESULT result;
    const unsigned char* buffer;
    size_t size;
    if (IoTHubMessage_GetByteArray(message, &buffer, &size) != IOTHUB_MESSAGE_OK)
    {
        printf("unable to IoTHubMessage_GetByteArray\r\n");
        result = EXECUTE_COMMAND_ERROR;
    }
    else
    {
        /*buffer is not zero terminated*/
        char* temp = malloc(size + 1);
        if (temp == NULL)
        {
            printf("failed to malloc\r\n");
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

<span data-ttu-id="b71e5-270">Cette implémentation **d’IoTHubMessage** appelle la fonction spécifique pour chaque action de votre modèle.</span><span class="sxs-lookup"><span data-stu-id="b71e5-270">This implementation of **IoTHubMessage** calls the specific function for each action in your model.</span></span> <span data-ttu-id="b71e5-271">Par exemple, si votre modèle définit cette action :</span><span class="sxs-lookup"><span data-stu-id="b71e5-271">For example, if your model defines this action:</span></span>

```
WITH_ACTION(SetAirResistance, int, Position)
```

<span data-ttu-id="b71e5-272">Vous devez définir une fonction avec cette signature :</span><span class="sxs-lookup"><span data-stu-id="b71e5-272">You must define a function with this signature:</span></span>

```
EXECUTE_COMMAND_RESULT SetAirResistance(ContosoAnemometer* device, int Position)
{
    (void)device;
    (void)printf("Setting Air Resistance Position to %d.\r\n", Position);
    return EXECUTE_COMMAND_SUCCESS;
}
```

<span data-ttu-id="b71e5-273">**SetAirResistance** est appelé quand ce message est envoyé sur votre appareil.</span><span class="sxs-lookup"><span data-stu-id="b71e5-273">**SetAirResistance** is then called when that message is sent to your device.</span></span>

<span data-ttu-id="b71e5-274">Nous n’avons pas encore expliqué à quoi ressemble la version sérialisée du message.</span><span class="sxs-lookup"><span data-stu-id="b71e5-274">What we haven't explained yet is what the serialized version of message looks like.</span></span> <span data-ttu-id="b71e5-275">En d’autres termes, si vous souhaitez envoyer un message **SetAirResistance** sur votre appareil, comment cela se présente-t-il ?</span><span class="sxs-lookup"><span data-stu-id="b71e5-275">In other words, if you want to send a **SetAirResistance** message to your device, what does that look like?</span></span>

<span data-ttu-id="b71e5-276">Si vous envoyez un message sur un appareil, cela se fait via le Kit de développement logiciel (SDK) de services Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="b71e5-276">If you're sending a message to a device, you would do so through the Azure IoT service SDK.</span></span> <span data-ttu-id="b71e5-277">Il vous reste à savoir quelle chaîne envoyer pour invoquer une action particulière.</span><span class="sxs-lookup"><span data-stu-id="b71e5-277">You still need to know what string to send to invoke a particular action.</span></span> <span data-ttu-id="b71e5-278">Le format général pour envoyer un message s’affiche comme suit :</span><span class="sxs-lookup"><span data-stu-id="b71e5-278">The general format for sending a message appears as follows:</span></span>

```
{"Name" : "", "Parameters" : "" }
```

<span data-ttu-id="b71e5-279">Vous envoyez un objet JSON sérialisé avec deux propriétés : **Name** est le nom de l’action (message) et **Parameters** contient les paramètres de cette action.</span><span class="sxs-lookup"><span data-stu-id="b71e5-279">You're sending a serialized JSON object with two properties: **Name** is the name of the action (message) and **Parameters** contains the parameters of that action.</span></span>

<span data-ttu-id="b71e5-280">Par exemple, pour invoquer **SetAirResistance** , vous pouvez envoyer ce message sur un appareil :</span><span class="sxs-lookup"><span data-stu-id="b71e5-280">For example, to invoke **SetAirResistance** you can send this message to a device:</span></span>

```
{"Name" : "SetAirResistance", "Parameters" : { "Position" : 5 }}
```

<span data-ttu-id="b71e5-281">Le nom de l’action doit correspondre exactement à une action définie dans votre modèle.</span><span class="sxs-lookup"><span data-stu-id="b71e5-281">The action name must exactly match an action defined in your model.</span></span> <span data-ttu-id="b71e5-282">Les noms de paramètre doivent correspondre également.</span><span class="sxs-lookup"><span data-stu-id="b71e5-282">The parameter names must match as well.</span></span> <span data-ttu-id="b71e5-283">Notez également que la casse est respectée.</span><span class="sxs-lookup"><span data-stu-id="b71e5-283">Also note case sensitivity.</span></span> <span data-ttu-id="b71e5-284">**Name** et **Parameters** sont toujours en majuscules.</span><span class="sxs-lookup"><span data-stu-id="b71e5-284">**Name** and **Parameters** are always uppercase.</span></span> <span data-ttu-id="b71e5-285">Respectez la casse pour le nom d’action et les paramètres dans votre modèle.</span><span class="sxs-lookup"><span data-stu-id="b71e5-285">Make sure to match the case of your action name and parameters in your model.</span></span> <span data-ttu-id="b71e5-286">Dans cet exemple le nom d’action est « SetAirResistance » et non « setairresistance ».</span><span class="sxs-lookup"><span data-stu-id="b71e5-286">In this example, the action name is "SetAirResistance" and not "setairresistance".</span></span>

<span data-ttu-id="b71e5-287">Les deux autres actions **TurnFanOn** et **TurnFanOff** peuvent être appelées en envoyant ces messages à un appareil :</span><span class="sxs-lookup"><span data-stu-id="b71e5-287">The two other actions **TurnFanOn** and **TurnFanOff** can be invoked by sending these messages to a device:</span></span>

```
{"Name" : "TurnFanOn", "Parameters" : {}}
{"Name" : "TurnFanOff", "Parameters" : {}}
```

<span data-ttu-id="b71e5-288">Cette section décrit tout ce que vous devez savoir au moment de l’envoi d’événements et de la réception de messages avec la bibliothèque **serializer** .</span><span class="sxs-lookup"><span data-stu-id="b71e5-288">This section described everything you need to know when sending events and receiving messages with the **serializer** library.</span></span> <span data-ttu-id="b71e5-289">Mais avant de poursuivre, intéressons-nous à certains paramètres que vous pouvez configurer pour contrôler la taille de votre modèle.</span><span class="sxs-lookup"><span data-stu-id="b71e5-289">Before moving on, let's cover some parameters you can configure that control how large your model is.</span></span>

## <a name="macro-configuration"></a><span data-ttu-id="b71e5-290">Configuration des macros</span><span class="sxs-lookup"><span data-stu-id="b71e5-290">Macro configuration</span></span>
<span data-ttu-id="b71e5-291">Si vous utilisez la bibliothèque **Serializer** , il convient de connaître une partie importante du Kit de développement logiciel (SDK), accessible dans la bibliothèque azure-c-shared-utility.</span><span class="sxs-lookup"><span data-stu-id="b71e5-291">If you’re using the **Serializer** library an important part of the SDK to be aware of is found in the azure-c-shared-utility library.</span></span>
<span data-ttu-id="b71e5-292">Si vous avez cloné le référentiel Azure-iot-sdk-c à partir de GitHub à l’aide de l’option récursive, vous trouverez cette bibliothèque d’utilitaire partagé ici :</span><span class="sxs-lookup"><span data-stu-id="b71e5-292">If you have cloned the Azure-iot-sdk-c repository from GitHub using the --recursive option, then you will find this shared utility library here:</span></span>

```
.\\c-utility
```

<span data-ttu-id="b71e5-293">Si vous n’avez pas cloné la bibliothèque, vous pouvez la trouver [ici](https://github.com/Azure/azure-c-shared-utility).</span><span class="sxs-lookup"><span data-stu-id="b71e5-293">If you have not cloned the library, you can find it [here](https://github.com/Azure/azure-c-shared-utility).</span></span>

<span data-ttu-id="b71e5-294">Dans la bibliothèque de l’utilitaire partagé, vous trouverez le dossier suivant :</span><span class="sxs-lookup"><span data-stu-id="b71e5-294">Within the shared utility library, you will find the following folder:</span></span>

```
azure-c-shared-utility\\macro\_utils\_h\_generator.
```

<span data-ttu-id="b71e5-295">Ce dossier contient une solution Visual Studio appelée **macro\_utils\_h\_generator.sln** :</span><span class="sxs-lookup"><span data-stu-id="b71e5-295">This folder contains a Visual Studio solution called **macro\_utils\_h\_generator.sln**:</span></span>

  ![](media/iot-hub-device-sdk-c-serializer/01-macro_utils_h_generator.PNG)

<span data-ttu-id="b71e5-296">Le programme de cette solution génère le fichier **macro\_utils.h**.</span><span class="sxs-lookup"><span data-stu-id="b71e5-296">The program in this solution generates the **macro\_utils.h** file.</span></span> <span data-ttu-id="b71e5-297">Un fichier macro\_utils.h par défaut est inclus avec le Kit de développement logiciel (SDK).</span><span class="sxs-lookup"><span data-stu-id="b71e5-297">There’s a default macro\_utils.h file included with the SDK.</span></span> <span data-ttu-id="b71e5-298">Cette solution vous permet de modifier certains paramètres, puis de recréer le fichier d’en-tête en fonction de ces paramètres.</span><span class="sxs-lookup"><span data-stu-id="b71e5-298">This solution allows you to modify some parameters and then recreate the header file based on these parameters.</span></span>

<span data-ttu-id="b71e5-299">Les deux paramètres essentiels dont vous devez vous préoccuper sont **nArithmetic** et **nMacroParameters** qui sont définis dans ces deux lignes du fichier macro\_utils.tt :</span><span class="sxs-lookup"><span data-stu-id="b71e5-299">The two key parameters to be concerned with are **nArithmetic** and **nMacroParameters** which are defined in these two lines found in macro\_utils.tt:</span></span>

```
<#int nArithmetic=1024;#>
<#int nMacroParameters=124;/*127 parameters in one macro deﬁnition in C99 in chapter 5.2.4.1 Translation limits*/#>

```

<span data-ttu-id="b71e5-300">Les valeurs ci-dessus sont les paramètres par défaut inclus avec le Kit de développement logiciel (SDK).</span><span class="sxs-lookup"><span data-stu-id="b71e5-300">These values are the default parameters included with the SDK.</span></span> <span data-ttu-id="b71e5-301">Chaque paramètre a la signification suivante :</span><span class="sxs-lookup"><span data-stu-id="b71e5-301">Each parameter has the following meaning:</span></span>

* <span data-ttu-id="b71e5-302">nMacroParameters : contrôle le nombre de paramètres que vous pouvez avoir dans une définition de macro DECLARE\_MODEL.</span><span class="sxs-lookup"><span data-stu-id="b71e5-302">nMacroParameters – Controls how many parameters you can have in one DECLARE\_MODEL macro definition.</span></span>
* <span data-ttu-id="b71e5-303">nArithmetic : contrôle le nombre total de membres autorisés dans un modèle.</span><span class="sxs-lookup"><span data-stu-id="b71e5-303">nArithmetic – Controls the total number of members allowed in a model.</span></span>

<span data-ttu-id="b71e5-304">Ces paramètres sont importants, car ils déterminent la taille éventuelle de votre modèle.</span><span class="sxs-lookup"><span data-stu-id="b71e5-304">The reason these parameters are important is because they control how large your model can be.</span></span> <span data-ttu-id="b71e5-305">Par exemple, prenez cette définition de modèle :</span><span class="sxs-lookup"><span data-stu-id="b71e5-305">For example, consider this model definition:</span></span>

```
DECLARE_MODEL(MyModel,
WITH_DATA(int, MyData)
);
```

<span data-ttu-id="b71e5-306">Comme mentionné précédemment, **DECLARE\_MODEL** est une simple macro C.</span><span class="sxs-lookup"><span data-stu-id="b71e5-306">As mentioned previously, **DECLARE\_MODEL** is just a C macro.</span></span> <span data-ttu-id="b71e5-307">Les noms du modèle et l’instruction **WITH\_DATA** (une autre macro) sont des paramètres de **DECLARE\_MODEL**.</span><span class="sxs-lookup"><span data-stu-id="b71e5-307">The names of the model and the **WITH\_DATA** statement (yet another macro) are parameters of **DECLARE\_MODEL**.</span></span> <span data-ttu-id="b71e5-308">**nMacroParameters** définit le nombre de paramètres qui peuvent être inclus dans **DECLARE\_MODEL**.</span><span class="sxs-lookup"><span data-stu-id="b71e5-308">**nMacroParameters** defines how many parameters can be included in **DECLARE\_MODEL**.</span></span> <span data-ttu-id="b71e5-309">Ces éléments définissent effectivement le nombre possible de déclarations d’événements de données et d’actions.</span><span class="sxs-lookup"><span data-stu-id="b71e5-309">Effectively, this defines how many data event and action declarations you can have.</span></span> <span data-ttu-id="b71e5-310">Ainsi, avec la limite de 124 par défaut, vous êtes en mesure de définir un modèle avec une combinaison d’environ 60 actions et événements de données.</span><span class="sxs-lookup"><span data-stu-id="b71e5-310">As such, with the default limit of 124 this means that you can define a model with a combination of about 60 actions and data events.</span></span> <span data-ttu-id="b71e5-311">Si vous tentez de dépasser cette limite, vous obtenez des erreurs du compilateur similaires à celles-ci :</span><span class="sxs-lookup"><span data-stu-id="b71e5-311">If you try to exceed this limit, you'll receive compiler errors that look similar to this:</span></span>

  ![](media/iot-hub-device-sdk-c-serializer/02-nMacroParametersCompilerErrors.PNG)

<span data-ttu-id="b71e5-312">Le paramètre **nArithmetic** concerne davantage le fonctionnement interne du langage de la macro que votre application.</span><span class="sxs-lookup"><span data-stu-id="b71e5-312">The **nArithmetic** parameter is more about the internal workings of the macro language than your application.</span></span>  <span data-ttu-id="b71e5-313">Il contrôle le nombre total de membres que vous pouvez avoir dans votre modèle, notamment les macros **DECLARE_STRUCT**.</span><span class="sxs-lookup"><span data-stu-id="b71e5-313">It controls the total number of members you can have in your model, including **DECLARE_STRUCT** macros.</span></span> <span data-ttu-id="b71e5-314">Donc si vous commencez à voir des erreurs du compilateur comme celles-ci, essayez d’augmenter **nArithmetic**:</span><span class="sxs-lookup"><span data-stu-id="b71e5-314">If you start seeing compiler errors such as this, then you should try increasing **nArithmetic**:</span></span>

   ![](media/iot-hub-device-sdk-c-serializer/03-nArithmeticCompilerErrors.PNG)

<span data-ttu-id="b71e5-315">Si vous souhaitez modifier ces paramètres, modifiez les valeurs dans le fichier macro\_utils.tt, recompilez la solution macro\_utils\_h\_generator.sln, puis exécutez le programme compilé.</span><span class="sxs-lookup"><span data-stu-id="b71e5-315">If you want to change these parameters, modify the values in the macro\_utils.tt file, recompile the macro\_utils\_h\_generator.sln solution, and run the compiled program.</span></span> <span data-ttu-id="b71e5-316">Lorsque vous procédez ainsi, un nouveau fichier macro\_utils.h est généré et placé dans le répertoire .\\common\\inc.</span><span class="sxs-lookup"><span data-stu-id="b71e5-316">When you do so, a new macro\_utils.h file is generated and placed in the .\\common\\inc directory.</span></span>

<span data-ttu-id="b71e5-317">Pour utiliser la nouvelle version de macro\_utils.h, vous devez supprimer le package NuGet **serializer** de votre solution et le remplacer par le projet Visual Studio **serializer**.</span><span class="sxs-lookup"><span data-stu-id="b71e5-317">In order to use the new version of macro\_utils.h, remove the **serializer** NuGet package from your solution and in its place include the **serializer** Visual Studio project.</span></span> <span data-ttu-id="b71e5-318">Cela permet à votre code de se compiler par rapport au code source de la bibliothèque sérialiseur.</span><span class="sxs-lookup"><span data-stu-id="b71e5-318">This enables your code to compile against the source code of the serializer library.</span></span> <span data-ttu-id="b71e5-319">Cela inclut la macro\_utils.h mise à jour.</span><span class="sxs-lookup"><span data-stu-id="b71e5-319">This includes the updated macro\_utils.h.</span></span> <span data-ttu-id="b71e5-320">Pour effectuer l’opération sur **simplesample\_amqp**, commencez par supprimer de la solution le package NuGet de la bibliothèque serializer :</span><span class="sxs-lookup"><span data-stu-id="b71e5-320">If you want to do this for **simplesample\_amqp**, start by removing the NuGet package for the serializer library from the solution:</span></span>

   ![](media/iot-hub-device-sdk-c-serializer/04-serializer-github-package.PNG)

<span data-ttu-id="b71e5-321">Ajoutez ensuite ce projet à votre solution Visual Studio :</span><span class="sxs-lookup"><span data-stu-id="b71e5-321">Then add this project to your Visual Studio solution:</span></span>

> <span data-ttu-id="b71e5-322">.\\c\\serializer\\build\\windows\\serializer.vcxproj</span><span class="sxs-lookup"><span data-stu-id="b71e5-322">.\\c\\serializer\\build\\windows\\serializer.vcxproj</span></span>
> 
> 

<span data-ttu-id="b71e5-323">Lorsque vous avez terminé, votre solution doit ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="b71e5-323">When you're done, your solution should look like this:</span></span>

   ![](media/iot-hub-device-sdk-c-serializer/05-serializer-project.PNG)

<span data-ttu-id="b71e5-324">Désormais, quand vous compilez votre solution, la version macro\_utils.h mise à jour est incluse dans votre fichier binaire.</span><span class="sxs-lookup"><span data-stu-id="b71e5-324">Now when you compile your solution, the updated macro\_utils.h is included in your binary.</span></span>

<span data-ttu-id="b71e5-325">Notez qu’en augmentant ces valeurs à un niveau assez élevé, elles peuvent dépasser les limites du compilateur.</span><span class="sxs-lookup"><span data-stu-id="b71e5-325">Note that increasing these values high enough can exceed compiler limits.</span></span> <span data-ttu-id="b71e5-326">À ce stade, le paramètre **nMacroParameters** est le principal paramètre à prendre en compte.</span><span class="sxs-lookup"><span data-stu-id="b71e5-326">To this point, the **nMacroParameters** is the main parameter with which to be concerned.</span></span> <span data-ttu-id="b71e5-327">La norme C99 indique qu’un minimum de 127 paramètres sont autorisés dans une définition de macro.</span><span class="sxs-lookup"><span data-stu-id="b71e5-327">The C99 spec specifies that a minimum of 127 parameters are allowed in a macro definition.</span></span> <span data-ttu-id="b71e5-328">Le compilateur Microsoft respecte exactement cette spécification (avec une limite de 127) ; vous ne pouvez donc pas augmenter **nMacroParameters** au-delà de la valeur par défaut.</span><span class="sxs-lookup"><span data-stu-id="b71e5-328">The Microsoft compiler follows the spec exactly (and has a limit of 127), so you won't be able to increase **nMacroParameters** beyond the default.</span></span> <span data-ttu-id="b71e5-329">Mais d’autres compilateurs peuvent vous permettre de le faire (par exemple, le compilateur GNU prend en charge une limite plus élevée).</span><span class="sxs-lookup"><span data-stu-id="b71e5-329">Other compilers might allow you to do so (for example, the GNU compiler supports a higher limit).</span></span>

<span data-ttu-id="b71e5-330">Jusqu’à présent, nous avons abordé pratiquement tout ce que vous devez savoir sur l’écriture de code avec la bibliothèque **serializer** .</span><span class="sxs-lookup"><span data-stu-id="b71e5-330">So far we've covered just about everything you need to know about how to write code with the **serializer** library.</span></span> <span data-ttu-id="b71e5-331">Avant de conclure, nous allons revoir certaines rubriques d’articles précédents qui amènent peut-être des questions.</span><span class="sxs-lookup"><span data-stu-id="b71e5-331">Before concluding, let's revisit some topics from previous articles that you may be wondering about.</span></span>

## <a name="the-lower-level-apis"></a><span data-ttu-id="b71e5-332">API de niveau inférieur</span><span class="sxs-lookup"><span data-stu-id="b71e5-332">The lower-level APIs</span></span>
<span data-ttu-id="b71e5-333">L’exemple d’application traité dans cet article est **simplesample\_amqp**.</span><span class="sxs-lookup"><span data-stu-id="b71e5-333">The sample application on which this article focused is **simplesample\_amqp**.</span></span> <span data-ttu-id="b71e5-334">Cet exemple utilise les API de niveau supérieur (non « LL ») pour envoyer des événements et recevoir des messages.</span><span class="sxs-lookup"><span data-stu-id="b71e5-334">This sample uses the higher-level (the non-"LL") APIs to send events and receive messages.</span></span> <span data-ttu-id="b71e5-335">Si vous utilisez ces API, un thread d’arrière-plan s’exécute, prenant en charge l’envoi d’événements et la réception de messages.</span><span class="sxs-lookup"><span data-stu-id="b71e5-335">If you use these APIs, a background thread runs which takes care of both sending events and receiving messages.</span></span> <span data-ttu-id="b71e5-336">Toutefois, vous pouvez utiliser les API de niveau inférieur (LL) pour éliminer ce thread d’arrière-plan et prendre le contrôle explicite quand vous envoyez des événements ou recevez des messages du cloud.</span><span class="sxs-lookup"><span data-stu-id="b71e5-336">However, you can use the lower-level (LL) APIs to eliminate this background thread and take explicit control over when you send events or receive messages from the cloud.</span></span>

<span data-ttu-id="b71e5-337">Comme décrit dans un [article précédent](iot-hub-device-sdk-c-iothubclient.md), il existe un ensemble de fonctions composé des API de niveau supérieur :</span><span class="sxs-lookup"><span data-stu-id="b71e5-337">As described in a [previous article](iot-hub-device-sdk-c-iothubclient.md), there is a set of functions that consists of the higher-level APIs:</span></span>

* <span data-ttu-id="b71e5-338">IoTHubClient\_CreateFromConnectionString</span><span class="sxs-lookup"><span data-stu-id="b71e5-338">IoTHubClient\_CreateFromConnectionString</span></span>
* <span data-ttu-id="b71e5-339">IoTHubClient\_SendEventAsync</span><span class="sxs-lookup"><span data-stu-id="b71e5-339">IoTHubClient\_SendEventAsync</span></span>
* <span data-ttu-id="b71e5-340">IoTHubClient\_SetMessageCallback</span><span class="sxs-lookup"><span data-stu-id="b71e5-340">IoTHubClient\_SetMessageCallback</span></span>
* <span data-ttu-id="b71e5-341">IoTHubClient\_Destroy</span><span class="sxs-lookup"><span data-stu-id="b71e5-341">IoTHubClient\_Destroy</span></span>

<span data-ttu-id="b71e5-342">Ces API sont décrites dans **simplesample\_amqp**.</span><span class="sxs-lookup"><span data-stu-id="b71e5-342">These APIs are demonstrated in **simplesample\_amqp**.</span></span>

<span data-ttu-id="b71e5-343">Il existe également un ensemble d’API de niveau inférieur analogue.</span><span class="sxs-lookup"><span data-stu-id="b71e5-343">There is also an analogous set of lower-level APIs.</span></span>

* <span data-ttu-id="b71e5-344">IoTHubClient\_LL\_CreateFromConnectionString</span><span class="sxs-lookup"><span data-stu-id="b71e5-344">IoTHubClient\_LL\_CreateFromConnectionString</span></span>
* <span data-ttu-id="b71e5-345">IoTHubClient\_LL\_SendEventAsync</span><span class="sxs-lookup"><span data-stu-id="b71e5-345">IoTHubClient\_LL\_SendEventAsync</span></span>
* <span data-ttu-id="b71e5-346">IoTHubClient\_LL\_SetMessageCallback</span><span class="sxs-lookup"><span data-stu-id="b71e5-346">IoTHubClient\_LL\_SetMessageCallback</span></span>
* <span data-ttu-id="b71e5-347">IoTHubClient\_LL\_Destroy</span><span class="sxs-lookup"><span data-stu-id="b71e5-347">IoTHubClient\_LL\_Destroy</span></span>

<span data-ttu-id="b71e5-348">Notez que les API de niveau inférieur fonctionnent exactement comme le décrivent les articles qui précèdent.</span><span class="sxs-lookup"><span data-stu-id="b71e5-348">Note that the lower-level APIs work exactly the same way as described in the previous articles.</span></span> <span data-ttu-id="b71e5-349">Vous pouvez utiliser le premier ensemble d’API si vous souhaitez un thread d’arrière-plan pour gérer les événements d’envoi et réception de messages.</span><span class="sxs-lookup"><span data-stu-id="b71e5-349">You can use the first set of APIs if you want a background thread to handle sending events and receiving messages.</span></span> <span data-ttu-id="b71e5-350">Vous utilisez le deuxième ensemble d’API si vous souhaitez contrôler explicitement vos envois et réceptions de données depuis IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="b71e5-350">You use the second set of APIs if you want explicit control over when you send and receive data from IoT Hub.</span></span> <span data-ttu-id="b71e5-351">Les deux ensembles d’API fonctionnent aussi bien l’un que l’autre avec la bibliothèque **serializer** .</span><span class="sxs-lookup"><span data-stu-id="b71e5-351">Either set of APIs work equally well with the **serializer** library.</span></span>

<span data-ttu-id="b71e5-352">Pour obtenir un exemple d’utilisation des API de niveau inférieur avec la bibliothèque **serializer**, consultez l’application **simplesample\_http**.</span><span class="sxs-lookup"><span data-stu-id="b71e5-352">For an example of how the lower-level APIs are used with the **serializer** library, see the **simplesample\_http** application.</span></span>

## <a name="additional-topics"></a><span data-ttu-id="b71e5-353">Rubriques supplémentaires</span><span class="sxs-lookup"><span data-stu-id="b71e5-353">Additional topics</span></span>
<span data-ttu-id="b71e5-354">Voici quelques autres sujets qu’il est intéressant de mentionner à nouveau : gestion des propriétés, utilisation d’autres informations d’identification sur l’appareil et options de configuration.</span><span class="sxs-lookup"><span data-stu-id="b71e5-354">A few other topics worth mentioning again are property handling, using alternate device credentials, and configuration options.</span></span> <span data-ttu-id="b71e5-355">Toutes ces rubriques sont traitées dans un [article précédent](iot-hub-device-sdk-c-iothubclient.md).</span><span class="sxs-lookup"><span data-stu-id="b71e5-355">These are all topics covered in a [previous article](iot-hub-device-sdk-c-iothubclient.md).</span></span> <span data-ttu-id="b71e5-356">Le point essentiel à retenir, c’est que toutes ces fonctionnalités fonctionnent de la même manière avec la bibliothèque **serializer** ou avec la bibliothèque **IoTHubClient**.</span><span class="sxs-lookup"><span data-stu-id="b71e5-356">The main point is that all of these features work in the same way with the **serializer** library as they do with the **IoTHubClient** library.</span></span> <span data-ttu-id="b71e5-357">Par exemple, si vous souhaitez joindre des propriétés à un événement à partir de votre modèle, vous devez utiliser **IoTHubMessage\_Properties** et **Map**\_**AddorUpdate** de la même manière que décrit précédemment :</span><span class="sxs-lookup"><span data-stu-id="b71e5-357">For example, if you want to attach properties to an event from your model, you use **IoTHubMessage\_Properties** and **Map**\_**AddorUpdate**, the same way as described previously:</span></span>

```
MAP_HANDLE propMap = IoTHubMessage_Properties(message.messageHandle);
sprintf_s(propText, sizeof(propText), "%d", i);
Map_AddOrUpdate(propMap, "SequenceNumber", propText);
```

<span data-ttu-id="b71e5-358">Peu importe que l’événement ait été généré à partir de la bibliothèque **serializer** ou manuellement par le biais de la bibliothèque **IoTHubClient**.</span><span class="sxs-lookup"><span data-stu-id="b71e5-358">Whether the event was generated from the **serializer** library or created manually using the **IoTHubClient** library does not matter.</span></span>

<span data-ttu-id="b71e5-359">En ce qui concerne les autres informations d’identification sur l’appareil, vous pouvez indifféremment utiliser **IoTHubClient\_LL\_Create** ou **IoTHubClient\_CreateFromConnectionString** pour allouer un élément **IOTHUB\_CLIENT\_HANDLE**.</span><span class="sxs-lookup"><span data-stu-id="b71e5-359">For the alternate device credentials, using **IoTHubClient\_LL\_Create** works just as well as **IoTHubClient\_CreateFromConnectionString** for allocating an **IOTHUB\_CLIENT\_HANDLE**.</span></span>

<span data-ttu-id="b71e5-360">Enfin, si vous utilisez la bibliothèque **serializer**, vous pouvez définir des options de configuration avec **IoTHubClient\_LL\_SetOption** tout comme vous l’avez fait pendant l’utilisation de la bibliothèque **IoTHubClient**.</span><span class="sxs-lookup"><span data-stu-id="b71e5-360">Finally, if you're using the **serializer** library, you can set configuration options with **IoTHubClient\_LL\_SetOption** just as you did when using the **IoTHubClient** library.</span></span>

<span data-ttu-id="b71e5-361">Les API d’initialisation sont des fonctionnalités secondaires uniques de la bibliothèque **serializer** .</span><span class="sxs-lookup"><span data-stu-id="b71e5-361">A feature that is unique to the **serializer** library are the initialization APIs.</span></span> <span data-ttu-id="b71e5-362">Avant de pouvoir commencer à travailler avec la bibliothèque, vous devez appeler **serializer\_init** :</span><span class="sxs-lookup"><span data-stu-id="b71e5-362">Before you can start working with the library, you must call **serializer\_init**:</span></span>

```
serializer_init(NULL);
```

<span data-ttu-id="b71e5-363">Cet appel doit être effectué juste avant l’appel de **IoTHubClient\_CreateFromConnectionString**.</span><span class="sxs-lookup"><span data-stu-id="b71e5-363">This is done just before you call **IoTHubClient\_CreateFromConnectionString**.</span></span>

<span data-ttu-id="b71e5-364">De même, quand vous avez fini d’utiliser la bibliothèque, le dernier appel effectué est normalement l’appel de **serializer\_deinit** :</span><span class="sxs-lookup"><span data-stu-id="b71e5-364">Similarly, when you're done working with the library, the last call you’ll make is to **serializer\_deinit**:</span></span>

```
serializer_deinit();
```

<span data-ttu-id="b71e5-365">Sinon, toutes les autres fonctionnalités répertoriées ci-dessus fonctionnent de la même manière dans la bibliothèque **serializer** ou dans la bibliothèque **IoTHubClient**.</span><span class="sxs-lookup"><span data-stu-id="b71e5-365">Otherwise, all of the other features listed above work the same in the **serializer** library as they do in the **IoTHubClient** library.</span></span> <span data-ttu-id="b71e5-366">Pour plus d’informations sur ces rubriques, consultez [l’article précédent](iot-hub-device-sdk-c-iothubclient.md) de cette série.</span><span class="sxs-lookup"><span data-stu-id="b71e5-366">For more information about any of these topics, see the [previous article](iot-hub-device-sdk-c-iothubclient.md) in this series.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b71e5-367">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b71e5-367">Next steps</span></span>
<span data-ttu-id="b71e5-368">Cet article décrit en détail les aspects uniques de la bibliothèque **serializer** contenue dans le **Kit de développement logiciel (SDK) d’appareil Azure IoT pour C**. Ces informations devraient vous aider à bien comprendre comment utiliser des modèles pour envoyer des événements et recevoir des messages vers et depuis IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="b71e5-368">This article describes in detail the unique aspects of the **serializer** library contained in the **Azure IoT device SDK for C**. With the information provided you should have a good understanding of how to use models to send events and receive messages from IoT Hub.</span></span>

<span data-ttu-id="b71e5-369">Ceci conclut également la série en trois parties sur le développement d’applications avec le **Kit de développement logiciel (SDK) d’appareil Azure IoT (Azure IoT device SDK) pour C**. Ces informations devraient suffire pour vous aider à commencer et à bien comprendre le fonctionnement des API.</span><span class="sxs-lookup"><span data-stu-id="b71e5-369">This also concludes the three-part series on how to develop applications with the **Azure IoT device SDK for C**. This should be enough information to not only get you started but give you a thorough understanding of how the APIs work.</span></span> <span data-ttu-id="b71e5-370">Pour plus d’informations, il existe quelques exemples du kit de développement logiciel non couverts ici.</span><span class="sxs-lookup"><span data-stu-id="b71e5-370">For additional information, there are a few samples in the SDK not covered here.</span></span> <span data-ttu-id="b71e5-371">Sinon, la [documentation du Kit de développement logiciel (SDK)](https://github.com/Azure/azure-iot-sdk-c) est une ressource précieuse pour obtenir des informations complémentaires.</span><span class="sxs-lookup"><span data-stu-id="b71e5-371">Otherwise, the [SDK documentation](https://github.com/Azure/azure-iot-sdk-c) is a good resource for additional information.</span></span>

<span data-ttu-id="b71e5-372">Pour en savoir plus sur le développement pour IoT Hub, consultez les [SDK Azure IoT][lnk-sdks].</span><span class="sxs-lookup"><span data-stu-id="b71e5-372">To learn more about developing for IoT Hub, see the [Azure IoT SDKs][lnk-sdks].</span></span>

<span data-ttu-id="b71e5-373">Pour explorer davantage les capacités de IoT Hub, consultez :</span><span class="sxs-lookup"><span data-stu-id="b71e5-373">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="b71e5-374">[Simulation d’un appareil avec Azure IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="b71e5-374">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
