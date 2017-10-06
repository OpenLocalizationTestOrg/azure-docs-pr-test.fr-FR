---
title: "le périphérique aaaThe Azure IoT SDK pour C | Documents Microsoft"
description: "Prise en main du SDK de périphérique Azure IoT hello pour C et découvrez comment les applications pour appareil toocreate qui communiquent avec un hub IoT."
services: iot-hub
documentationcenter: 
author: olivierbloch
manager: timlt
editor: 
ms.assetid: e448b061-6bdd-470a-a527-15ec03cca7b9
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: obloch
ms.openlocfilehash: 9e20742e6ea513c124bfaf28f02f6fba86170daf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-device-sdk-for-c"></a>Azure IoT device SDK pour C

Hello **Azure IoT appareil SDK** est un ensemble de bibliothèques conçu le processus de hello toosimplify d’envoi de messages tooand réception de messages hello **Azure IoT Hub** service. Il existe différentes variantes de hello SDK, ciblant chacun une plateforme spécifique, mais cet article décrit hello **appareil Azure IoT SDK pour C**.

Dispositif de Azure IoT Hello SDK pour C est écrite en ANSI C (C99) toomaximize portabilité. Cette fonctionnalité rend toooperate convient parfaitement de bibliothèques hello sur plusieurs plateformes et des périphériques, surtout lorsque la réduction du disque et l’encombrement mémoire est une priorité.

Il existe un large éventail de plateformes sur quel hello SDK a été testé (voir hello [Azure certifié pour le catalogue de périphérique IoT](https://catalog.azureiotsuite.com/) pour plus d’informations). Bien que cet article contient des procédures pas à pas de l’exemple de code en cours d’exécution sur la plate-forme de Windows hello, code hello décrit dans cet article est identique sur gamme hello des plateformes prises en charge.

Cet article vous présente d’architecture toohello du périphérique de Azure IoT hello SDK pour C. Il montre comment les bibliothèque de périphériques tooinitialize hello, envoyer des données tooIoT Hub et recevoir des messages à partir de celui-ci. informations Hello dans cet article doivent être suffisamment tooget démarré à l’aide du Kit de développement logiciel de hello, mais il fournit également des informations de tooadditional des pointeurs sur les bibliothèques de hello.

## <a name="sdk-architecture"></a>Architecture du kit de développement logiciel (SDK)

Vous pouvez trouver hello [ **appareil Azure IoT SDK pour C** ](https://github.com/Azure/azure-iot-sdk-c) GitHub référentiel et consulter les détails de hello API Bonjour [référence d’API C](https://azure.github.io/azure-iot-sdk-c/index.html).

Vous trouverez la version la plus récente des bibliothèques de hello Hello Bonjour **master** branche du référentiel de hello :

  ![](media/iot-hub-device-sdk-c-intro/01-MasterBranch.PNG)

* Bonjour implémentation de base de hello SDK est Bonjour **iothub\_client** dossier qui contient l’implémentation de hello de couche API la plus basse hello Bonjour SDK : hello **IoTHubClient** bibliothèque. Hello **IoTHubClient** bibliothèque contient des API implémentation brutes de messagerie pour envoyer des messages tooIoT concentrateur et de réception de messages à partir de IoT Hub. Lorsque vous utilisez cette bibliothèque, vous êtes responsable de la mise en œuvre de la sérialisation du message, mais d’autres détails concernant la communication avec IoT Hub sont gérés pour vous.
* Hello **sérialiseur** dossier contient des fonctions d’assistance et des exemples qui montrent comment les données de tooserialize avant leur envoi à l’aide de Hub IoT tooAzure hello bibliothèque cliente. utilisation de Hello de sérialiseur de hello n’est pas obligatoire et est fournie à titre informatif. toouse hello **sérialiseur** bibliothèque, vous définissez un modèle qui spécifie les données toosend tooIoT Hub et hello messages hello souhaitées tooreceive à partir de celui-ci. Une fois le modèle de hello est défini, hello Kit de développement logiciel vous apporte une surface API qui vous permet de tooeasily travail avec l’appareil-à-cloud et messages cloud-à-appareil sans se préoccuper hello détails de la sérialisation. bibliothèque de Hello dépend d’autres bibliothèques open source qui implémentent le transport à l’aide des protocoles tels que MQTT et AMQP.
* Hello **IoTHubClient** bibliothèque vis-à-vis d’autres bibliothèques open source :
  * Hello [Azure C partagé utilitaire](https://github.com/Azure/azure-c-shared-utility) bibliothèque, qui fournit des fonctionnalités communes pour les tâches de base (par exemple, les chaînes, la manipulation de la liste et e/s) nécessaire à travers plusieurs liées à Azure C kits de développement logiciel.
  * Hello [uAMQP Azure](https://github.com/Azure/azure-uamqp-c) bibliothèque, ce qui est une implémentation côté client de AMQP optimisée pour les appareils limité en ressources.
  * Hello [uMQTT Azure](https://github.com/Azure/azure-umqtt-c) bibliothèque, qui est une implémentation hello MQTT protocole de bibliothèque à usage général et optimisées pour les appareils limité en ressources.

Utilisation de ces bibliothèques est toounderstand plus facilement en examinant les exemples de code. Hello les sections suivantes vous guide plusieurs exemples d’applications hello qui sont inclus dans le Kit de développement logiciel de hello. Cette procédure pas à pas doit vous donner une bonne sentir pour hello différentes fonctionnalités de couches de l’architecture hello de hello Kit de développement logiciel et une hello toohow de présentation des API de travail.

## <a name="before-you-run-hello-samples"></a>Avant d’exécuter les exemples hello

Avant de pouvoir exécuter les exemples hello dans SDK de périphérique Azure IoT hello pour C, vous devez [créer une instance de hello IoT Hub service](iot-hub-create-through-portal.md) dans votre abonnement Azure. Puis terminez hello tâches suivantes :

* Préparer votre environnement de développement
* Obtenir les informations d’identification de l’appareil.

### <a name="prepare-your-development-environment"></a>Préparer votre environnement de développement

Les packages sont fournis pour les plates-formes courantes (telles que NuGet pour Windows ou apt_get pour Debian et Ubuntu) et les exemples hello utilisent ces packages lorsqu’il est disponible. Dans certains cas, vous devez toocompile hello SDK pour ou sur votre appareil. Si vous devez toocompile hello SDK, consultez [préparer votre environnement de développement](https://github.com/Azure/azure-iot-sdk-c/blob/master/doc/devbox_setup.md) dans le référentiel GitHub de hello.

code d’application exemple hello dans tooobtain, télécharger une copie de hello SDK à partir de GitHub. Obtenir une copie de la source de hello de hello **master** branche Hello [référentiel GitHub](https://github.com/Azure/azure-iot-sdk-c).


### <a name="obtain-hello-device-credentials"></a>Obtenir des informations d’identification de périphérique hello

Maintenant que vous avez les exemples de code source hello, hello suivant chose toodo est tooget un ensemble d’informations d’identification de l’appareil. Pour un tooaccess périphérique le toobe en mesure d’un hub IoT, vous devez d’abord ajouter hello appareil toohello Registre des identités IoT Hub. Lorsque vous ajoutez votre appareil, vous obtenez un ensemble d’informations d’identification de périphérique dont vous avez besoin pour le hub IoT de hello appareil toobe tooconnect en mesure de toohello. exemples d’applications Hello présentés dans la section suivante de hello attendent ces informations d’identification sous forme de hello d’un **chaîne de connexion de périphérique**.

Il existe plusieurs toohelp d’outils open source vous gérez votre hub IoT.

* Une application Windows appelée [Explorateur d’appareils](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer).
* Un outil d’interface de ligne de commande (CLI) multiplateforme node.js appelé [iothub-explorer](https://github.com/azure/iothub-explorer).

Ce didacticiel utilise hello graphique *Explorateur de périphérique* outil. Vous pouvez également utiliser hello *iothub-explorer* outil si vous préférez toouse un outil CLI.

outil Explorateur de périphérique Hello utilise hello Azure IoT service bibliothèques tooperform diverses fonctions sur IoT Hub, y compris l’ajout de périphériques. Si vous utilisez hello appareil explorer outil tooadd un appareil, vous obtenez une chaîne de connexion pour votre appareil. Vous avez besoin de cette connexion chaîne toorun hello exemples d’applications.

Si vous n’êtes pas familiarisé avec l’outil Explorateur de périphérique hello, hello procédure décrit comment toouse il tooadd un appareil et d’obtenir une chaîne de connexion de périphérique.

outil d’explorer des appareils tooinstall hello, consultez [comment toouse hello Explorateur de périphérique pour les appareils IoT Hub](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer).

Lorsque vous exécutez le programme de hello, vous voyez cette interface :

  ![](media/iot-hub-device-sdk-c-intro/03-DeviceExplorer.PNG)

Entrez votre **chaîne de connexion de Hub IoT** Bonjour premier champ, puis cliquez sur **mise à jour**. Cette étape configure l’outil de hello afin qu’il puisse communiquer avec IoT Hub.

Lorsque hello chaîne de connexion de IoT Hub est configuré, cliquez sur hello **gestion** onglet :

  ![](media/iot-hub-device-sdk-c-intro/04-ManagementTab.PNG)

Cet onglet est la gestion des appareils hello inscrits dans votre IoT hub.

Vous créez un périphérique en cliquant sur hello **créer** bouton. Une boîte de dialogue avec un jeu de clés (primaire et secondaire) préalablement remplies s’affiche. Entrez un **ID d’appareil**, puis cliquez sur **Créer**.

  ![](media/iot-hub-device-sdk-c-intro/05-CreateDevice.PNG)

Lors de la création de l’appareil de hello, hello périphériques liste des mises à jour avec tous les périphériques hello enregistré, y compris hello que celui que vous venez de créer. Si vous cliquez avec le bouton droit sur le nouvel appareil, le menu qui suit s’affiche :

  ![](media/iot-hub-device-sdk-c-intro/06-RightClickDevice.PNG)

Si vous choisissez **copier la chaîne de connexion pour le périphérique sélectionné**, chaîne de connexion de périphérique hello est copié toohello Presse-papiers. Conservez une copie de la chaîne de connexion de périphérique hello. Vous avez besoin lors de l’exécution des exemples d’applications hello décrites dans les sections suivantes de hello.

Lorsque vous avez terminé les étapes de hello ci-dessus, vous êtes prêt toostart en cours d’exécution du code. Les deux exemples, il est une constante haut hello hello principal fichier source qui permet de vous tooenter une chaîne de connexion. Par exemple, hello ligne correspondante à partir de hello **iothub\_client\_exemple\_mqtt** application s’affiche comme suit.

```c
static const char* connectionString = "[device connection string]";
```

## <a name="use-hello-iothubclient-library"></a>Utiliser la bibliothèque IoTHubClient hello

Au sein de hello **iothub\_client** dossier Bonjour [azure iot-sdk--c](https://github.com/azure/azure-iot-sdk-c) référentiel, il existe un **exemples** dossier qui contient une application appelée **iothub\_client\_exemple\_mqtt**.

version de Windows Hello de hello **iothub\_client\_exemple\_mqtt** application inclut hello suivant la solution Visual Studio :

  ![](media/iot-hub-device-sdk-c-intro/12-iothub-client-sample-mqtt.PNG)

> [!NOTE]
> Si vous ouvrez ce projet dans Visual Studio 2017, accepter hello invites tooretarget hello projet toohello dernière version.

Cette solution inclut un seul projet : Cette solution installe quatre packages NuGet :

* Microsoft.Azure.C.SharedUtility
* Microsoft.Azure.IoTHub.MqttTransport
* Microsoft.Azure.IoTHub.IoTHubClient
* Microsoft.Azure.umqtt

Vous devez toujours hello **Microsoft.Azure.C.SharedUtility** lorsque vous travaillez avec le Kit de développement logiciel de hello du package. Cet exemple utilise le protocole MQTT hello, par conséquent, vous devez inclure hello **Microsoft.Azure.umqtt** et **Microsoft.Azure.IoTHub.MqttTransport** packages (il existe des packages équivalentes pour HTTP et AMQP ). Étant donné que l’exemple hello utilise hello **IoTHubClient** bibliothèque, vous devez également inclure hello **Microsoft.Azure.IoTHub.IoTHubClient** package dans votre solution.

Vous pouvez trouver l’implémentation hello pour exemple d’application hello Bonjour **iothub\_client\_exemple\_mqtt.c** fichier source.

Hello étapes suivantes utilisent ce toowalk d’application exemple vous guide dans les étapes nécessaires toouse hello **IoTHubClient** bibliothèque.

### <a name="initialize-hello-library"></a>Initialisation de la bibliothèque de hello

> [!NOTE]
> Avant de commencer à utiliser avec les bibliothèques hello, vous devrez peut-être tooperform une initialisation spécifique à la plateforme. Par exemple, si vous envisagez de toouse AMQP sur Linux, vous devez initialiser bibliothèque OpenSSL de hello. Hello exemples Bonjour [référentiel GitHub](https://github.com/Azure/azure-iot-sdk-c) appeler la fonction de l’utilitaire hello **plateforme\_init** lorsque hello client démarre et appeler hello **plateforme\_deinit**  (fonction) avant de quitter. Ces fonctions sont déclarées dans le fichier d’en-tête platform.h hello. Examiner les définitions de ces fonctions pour votre plateforme cible Bonjour hello [référentiel](https://github.com/Azure/azure-iot-sdk-c) toodetermine si vous avez besoin tooinclude tout code d’initialisation propre à la plateforme dans votre client.

tout d’abord, toostart dans les bibliothèques de hello, allouer un handle de client IoT Hub :

```c
if ((iotHubClientHandle = IoTHubClient_LL_CreateFromConnectionString(connectionString, MQTT_Protocol)) == NULL)
{
    (void)printf("ERROR: iotHubClientHandle is NULL!\r\n");
}
else
{
    ...
```

Vous passez d’une copie de la chaîne de connexion de périphérique hello que vous obtenu à partir de la fonction de toothis l’outil Explorateur hello appareil. Vous désignez également toouse de protocole de communication hello. Cet exemple utilise MQTT, mais AMQP et HTTP sont également possibles.

Lorsque vous avez valide **IOTHUB\_CLIENT\_gérer**, vous pouvez commencer à appeler hello API toosend et recevoir des messages tooand de IoT Hub.

### <a name="send-messages"></a>Envoyer des messages

exemple d’application Hello définit un hub IoT de boucle toosend messages tooyour. Hello suivant extrait de code :

- Crée un message.
- Ajoute une propriété message toohello.
- Envoie un message.

Tout d’abord, créez un message :

```c
size_t iterator = 0;
do
{
    if (iterator < MESSAGE_COUNT)
    {
        sprintf_s(msgText, sizeof(msgText), "{\"deviceId\":\"myFirstDevice\",\"windSpeed\":%.2f}", avgWindSpeed + (rand() % 4 + 2));
        if ((messages[iterator].messageHandle = IoTHubMessage_CreateFromByteArray((const unsigned char*)msgText, strlen(msgText))) == NULL)
        {
            (void)printf("ERROR: iotHubMessageHandle is NULL!\r\n");
        }
        else
        {
            messages[iterator].messageTrackingId = iterator;
            MAP_HANDLE propMap = IoTHubMessage_Properties(messages[iterator].messageHandle);
            (void)sprintf_s(propText, sizeof(propText), "PropMsg_%zu", iterator);
            if (Map_AddOrUpdate(propMap, "PropName", propText) != MAP_OK)
            {
                (void)printf("ERROR: Map_AddOrUpdate Failed!\r\n");
            }

            if (IoTHubClient_LL_SendEventAsync(iotHubClientHandle, messages[iterator].messageHandle, SendConfirmationCallback, &messages[iterator]) != IOTHUB_CLIENT_OK)
            {
                (void)printf("ERROR: IoTHubClient_LL_SendEventAsync..........FAILED!\r\n");
            }
            else
            {
                (void)printf("IoTHubClient_LL_SendEventAsync accepted message [%d] for transmission tooIoT Hub.\r\n", (int)iterator);
            }
        }
    }
    IoTHubClient_LL_DoWork(iotHubClientHandle);
    ThreadAPI_Sleep(1);

    iterator++;
} while (g_continueRunning);
```

Chaque fois que vous envoyez un message, vous spécifiez une fonction de rappel tooa référence qui est appelée lorsque les données hello sont envoyées. Dans cet exemple, la fonction de rappel hello est appelée **SendConfirmationCallback**. Hello suivant extrait de code montre cette fonction de rappel :

```c
static void SendConfirmationCallback(IOTHUB_CLIENT_CONFIRMATION_RESULT result, void* userContextCallback)
{
    EVENT_INSTANCE* eventInstance = (EVENT_INSTANCE*)userContextCallback;
    (void)printf("Confirmation[%d] received for message tracking id = %zu with result = %s\r\n", callbackCounter, eventInstance->messageTrackingId, ENUM_TO_STRING(IOTHUB_CLIENT_CONFIRMATION_RESULT, result));
    /* Some device specific action code goes here... */
    callbackCounter++;
    IoTHubMessage_Destroy(eventInstance->messageHandle);
}
```

Notez hello appel toohello **IoTHubMessage\_détruire** lorsque vous avez terminé avec le message d’appel de fonction. Cette fonction libère les ressources de hello alloués lors de la création du message de type hello.

### <a name="receive-messages"></a>Recevoir des messages

La réception d’un message est une opération asynchrone. Tout d’abord, vous inscrivez hello rappel tooinvoke lors de l’appareil de hello reçoit un message :

```c
if (IoTHubClient_LL_SetMessageCallback(iotHubClientHandle, ReceiveMessageCallback, &receiveContext) != IOTHUB_CLIENT_OK)
{
    (void)printf("ERROR: IoTHubClient_LL_SetMessageCallback..........FAILED!\r\n");
}
else
{
    (void)printf("IoTHubClient_LL_SetMessageCallback...successful.\r\n");
...
```

Hello dernier paramètre est un toowhatever pointeur void souhaité. Dans l’exemple hello, il s’agit d’un entier de tooan de pointeur, mais elle peut être un pointeur tooa structure de données plus complexe. Ce paramètre permet de toooperate de fonction de rappel hello sur l’état partagé avec un appelant de hello de cette fonction.

Lors de l’appareil de hello reçoit un message, hello inscrits fonction de rappel est appelée. Cette fonction de rappel récupère :

* id de message Hello et id de corrélation de message de type hello.
* contenu du message Hello.
* Toutes les propriétés personnalisées à partir du message de type hello.

```c
static IOTHUBMESSAGE_DISPOSITION_RESULT ReceiveMessageCallback(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    int* counter = (int*)userContextCallback;
    const char* buffer;
    size_t size;
    MAP_HANDLE mapProperties;
    const char* messageId;
    const char* correlationId;

    // Message properties
    if ((messageId = IoTHubMessage_GetMessageId(message)) == NULL)
    {
        messageId = "<null>";
    }

    if ((correlationId = IoTHubMessage_GetCorrelationId(message)) == NULL)
    {
        correlationId = "<null>";
    }

    // Message content
    if (IoTHubMessage_GetByteArray(message, (const unsigned char**)&buffer, &size) != IOTHUB_MESSAGE_OK)
    {
        (void)printf("unable tooretrieve hello message data\r\n");
    }
    else
    {
        (void)printf("Received Message [%d]\r\n Message ID: %s\r\n Correlation ID: %s\r\n Data: <<<%.*s>>> & Size=%d\r\n", *counter, messageId, correlationId, (int)size, buffer, (int)size);
        // If we receive hello work 'quit' then we stop running
        if (size == (strlen("quit") * sizeof(char)) && memcmp(buffer, "quit", size) == 0)
        {
            g_continueRunning = false;
        }
    }

    // Retrieve properties from hello message
    mapProperties = IoTHubMessage_Properties(message);
    if (mapProperties != NULL)
    {
        const char*const* keys;
        const char*const* values;
        size_t propertyCount = 0;
        if (Map_GetInternals(mapProperties, &keys, &values, &propertyCount) == MAP_OK)
        {
            if (propertyCount > 0)
            {
                size_t index;

                printf(" Message Properties:\r\n");
                for (index = 0; index < propertyCount; index++)
                {
                    (void)printf("\tKey: %s Value: %s\r\n", keys[index], values[index]);
                }
                (void)printf("\r\n");
            }
        }
    }

    /* Some device specific action code goes here... */
    (*counter)++;
    return IOTHUBMESSAGE_ACCEPTED;
}
```

Hello d’utilisation **IoTHubMessage\_GetByteArray** fonction tooretrieve message de type hello, qui dans cet exemple est une chaîne.

### <a name="uninitialize-hello-library"></a>Annuler l’initialisation de la bibliothèque de hello

Lorsque vous avez terminé d’envoi d’événements et réception de messages, vous pouvez annuler l’initialisation de bibliothèque de IoT hello. toodo émettre donc hello après l’appel de fonction :

```
IoTHubClient_LL_Destroy(iotHubClientHandle);
```

Cet appel permet de libérer les ressources hello précédemment alloués par hello **IoTHubClient\_CreateFromConnectionString** (fonction).

Comme vous pouvez le voir, il est facile toosend et recevoir des messages avec hello **IoTHubClient** bibliothèque. bibliothèque Hello gère les détails de hello de communiquer avec IoT Hub, y compris le toouse protocol (du point de vue hello du développeur de hello, c’est une option de configuration simple).

Hello **IoTHubClient** bibliothèque fournit également un contrôle précis sur comment les données de salutation tooserialize votre appareil envoie tooIoT Hub. Dans certains cas, ce niveau de contrôle est un avantage, mais dans d’autres, il est un détail d’implémentation que vous ne souhaitez pas toobe concerné avec. Si tel est le cas de hello, vous pouvez envisager d’utiliser hello **sérialiseur** bibliothèque, ce qui est décrit dans la section suivante de hello.

## <a name="use-hello-serializer-library"></a>Utiliser la bibliothèque sérialiseur hello

Point de vue conceptuel hello **sérialiseur** bibliothèque se situe au-dessus hello **IoTHubClient** bibliothèque Bonjour SDK. Il utilise hello **IoTHubClient** bibliothèque pour hello sous-jacent de la communication avec IoT Hub, mais il ajoute des fonctionnalités de modélisation qui suppriment les charge hello de traitement de sérialisation de messages de développeur de hello. Le fonctionnement de la bibliothèque est mieux illustré par un exemple.

À l’intérieur hello **sérialiseur** dossier Bonjour [azure iot-sdk--c référentiel](https://github.com/Azure/azure-iot-sdk-c), est un **exemples** dossier qui contient une application appelée **simplesample \_mqtt**. version de Windows Hello de cet exemple inclut hello suivant la solution Visual Studio :

  ![](media/iot-hub-device-sdk-c-intro/14-simplesample_mqtt.PNG)

> [!NOTE]
> Si vous ouvrez ce projet dans Visual Studio 2017, accepter hello invites tooretarget hello projet toohello dernière version.

Comme avec l’exemple précédent de hello, celle-ci comprend plusieurs packages NuGet :

* Microsoft.Azure.C.SharedUtility
* Microsoft.Azure.IoTHub.MqttTransport
* Microsoft.Azure.IoTHub.IoTHubClient
* Microsoft.Azure.IoTHub.Serializer
* Microsoft.Azure.umqtt

Vous avez vu la plupart de ces packages dans l’exemple précédent de hello, mais **Microsoft.Azure.IoTHub.Serializer** est nouveau. Ce package est requis lorsque vous utilisez hello **sérialiseur** bibliothèque.

Vous trouverez une implémentation hello de l’exemple d’application hello Bonjour **simplesample\_mqtt.c** fichier.

Hello sections suivantes vous guident dans les parties de clé hello de cet exemple.

### <a name="initialize-hello-library"></a>Initialisation de la bibliothèque de hello

toostart utilisation de hello **sérialiseur** bibliothèque, les appels API de l’initialisation hello :

```c
if (serializer_init(NULL) != SERIALIZER_OK)
{
    (void)printf("Failed on serializer_init\r\n");
}
else
{
    IOTHUB_CLIENT_LL_HANDLE iotHubClientHandle = IoTHubClient_LL_CreateFromConnectionString(connectionString, MQTT_Protocol);
    srand((unsigned int)time(NULL));
    int avgWindSpeed = 10;

    if (iotHubClientHandle == NULL)
    {
        (void)printf("Failed on IoTHubClient_LL_Create\r\n");
    }
    else
    {
        ContosoAnemometer* myWeather = CREATE_MODEL_INSTANCE(WeatherStation, ContosoAnemometer);
        if (myWeather == NULL)
        {
            (void)printf("Failed on CREATE_MODEL_INSTANCE\r\n");
        }
        else
        {
...
```

Hello appel toohello **sérialiseur\_init** fonction est un appel à usage unique et l’initialise hello bibliothèque sous-jacente. Ensuite, vous appelez hello **IoTHubClient\_LL\_CreateFromConnectionString** fonction, qui est hello même API que dans hello **IoTHubClient** exemple. Cet appel définit la chaîne de connexion de votre périphérique (cet appel est également où vous choisissez le protocole de hello souhaité toouse). Cet exemple utilise MQTT comme couche de transport hello, mais il peut utiliser AMQP ou HTTP.

Enfin, appelez hello **créer\_modèle\_INSTANCE** (fonction). **WeatherStation** est l’espace de noms hello du modèle de hello et **ContosoAnemometer** est le nom hello du modèle de hello. Une fois que l’instance de modèle hello est créé, vous pouvez l’utiliser toostart envoyer et recevoir des messages. Toutefois, il est important toounderstand un quel modèle est.

### <a name="define-hello-model"></a>Définir le modèle de hello

Un modèle Bonjour **sérialiseur** bibliothèque définit les messages de salutation votre appareil peut envoyer tooIoT messages Hub et hello, appelé *actions* Bonjour langage de modélisation, qui peut recevoir. Vous définissez un modèle à l’aide d’un ensemble de macros C comme hello **simplesample\_mqtt** exemple d’application :

```c
BEGIN_NAMESPACE(WeatherStation);

DECLARE_MODEL(ContosoAnemometer,
WITH_DATA(ascii_char_ptr, DeviceId),
WITH_DATA(int, WindSpeed),
WITH_ACTION(TurnFanOn),
WITH_ACTION(TurnFanOff),
WITH_ACTION(SetAirResistance, int, Position)
);

END_NAMESPACE(WeatherStation);
```

Hello **commencer\_espace de noms** et **fin\_espace de noms** macros les deux prennent hello espace de noms du modèle hello en tant qu’argument. Il est probable que quoi que ce soit entre ces macros est définition hello de votre modèle ou de modèles et structures de données hello qui utilisent des modèles de hello.

Dans cet exemple, il existe un seul modèle appelé **ContosoAnemometer**. Ce modèle définit deux éléments de données que votre appareil peut envoyer tooIoT Hub : **DeviceId** et **WindSpeed**. Il définit également trois actions (messages) que votre appareil peut recevoir : **TurnFanOn**, **TurnFanOff** et **SetAirResistance**. Chaque élément de données possède un type et chaque action a un nom (et éventuellement, un ensemble de paramètres).

les données de salutation et les actions définies dans le modèle de hello définissent une surface API que vous pouvez utiliser toosend messages tooIoT Hub et répondre toomessages envoyés toohello appareil. Un exemple permet de mieux comprendre l’utilisation de ce modèle.

### <a name="send-messages"></a>Envoyer des messages

modèle de Hello définit des données hello vous pouvez envoyer tooIoT Hub. Dans cet exemple, cela signifie qu’un des hello deux éléments de données définis à l’aide de hello **WITH_DATA** (macro). Il existe plusieurs toosend requis d’étapes **DeviceId** et **WindSpeed** IoT hub tooan de valeurs. Hello est tout d’abord tooset hello données toosend :

```c
myWeather->DeviceId = "myFirstDevice";
myWeather->WindSpeed = avgWindSpeed + (rand() % 4 + 2);
```

Hello modèle défini précédemment vous permet des valeurs hello tooset en définissant les membres d’un **struct**. Ensuite, sérialiser le message de salutation souhaité toosend :

```c
unsigned char* destination;
size_t destinationSize;
if (SERIALIZE(&destination, &destinationSize, myWeather->DeviceId, myWeather->WindSpeed) != CODEFIRST_OK)
{
    (void)printf("Failed tooserialize\r\n");
}
else
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
    free(destination);
}
```

Ce code sérialise la mémoire tampon de périphérique dans le cloud tooa hello (référencé par **destination**). code de Hello puis appelle hello **sendMessage** fonction toosend hello message tooIoT Hub :

```c
static void sendMessage(IOTHUB_CLIENT_LL_HANDLE iotHubClientHandle, const unsigned char* buffer, size_t size)
{
    static unsigned int messageTrackingId;
    IOTHUB_MESSAGE_HANDLE messageHandle = IoTHubMessage_CreateFromByteArray(buffer, size);
    if (messageHandle == NULL)
    {
        printf("unable toocreate a new IoTHubMessage\r\n");
    }
    else
    {
        if (IoTHubClient_LL_SendEventAsync(iotHubClientHandle, messageHandle, sendCallback, (void*)(uintptr_t)messageTrackingId) != IOTHUB_CLIENT_OK)
        {
            printf("failed toohand over hello message tooIoTHubClient");
        }
        else
        {
            printf("IoTHubClient accepted hello message for delivery\r\n");
        }
        IoTHubMessage_Destroy(messageHandle);
    }
    messageTrackingId++;
}
```


Hello du deuxième paramètre toolast de **IoTHubClient\_LL\_SendEventAsync** est une fonction de rappel de tooa de référence qui est appelée quand les données hello sont envoyées avec succès. Voici la fonction de rappel hello dans l’exemple hello :

```c
void sendCallback(IOTHUB_CLIENT_CONFIRMATION_RESULT result, void* userContextCallback)
{
    unsigned int messageTrackingId = (unsigned int)(uintptr_t)userContextCallback;

    (void)printf("Message Id: %u Received.\r\n", messageTrackingId);

    (void)printf("Result Call Back Called! Result is: %s \r\n", ENUM_TO_STRING(IOTHUB_CLIENT_CONFIRMATION_RESULT, result));
}
```

Hello deuxième paramètre est un contexte de toouser pointeur ; Hello même pointeur passé trop**IoTHubClient\_LL\_SendEventAsync**. Dans ce cas, le contexte de hello est un compteur simple, mais il peut s’agir comme vous le souhaitez.

C’est tout est toosending les messages appareil-à-cloud. Hello uniquement gauche toocover consiste comment tooreceive messages.

### <a name="receive-messages"></a>Recevoir des messages

Réception d’un message fonctionne de façon similaire toohello fonctionnement de messages de hello **IoTHubClient** bibliothèque. Tout d’abord, vous enregistrez une fonction de rappel de message :

```c
if (IoTHubClient_LL_SetMessageCallback(iotHubClientHandle, IoTHubMessage, myWeather) != IOTHUB_CLIENT_OK)
{
    printf("unable tooIoTHubClient_SetMessageCallback\r\n");
}
else
{
...
```

Ensuite, vous écrivez la fonction de rappel hello est appelée lorsqu’un message est reçu :

```c
static IOTHUBMESSAGE_DISPOSITION_RESULT IoTHubMessage(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    IOTHUBMESSAGE_DISPOSITION_RESULT result;
    const unsigned char* buffer;
    size_t size;
    if (IoTHubMessage_GetByteArray(message, &buffer, &size) != IOTHUB_MESSAGE_OK)
    {
        printf("unable tooIoTHubMessage_GetByteArray\r\n");
        result = IOTHUBMESSAGE_ABANDONED;
    }
    else
    {
        /*buffer is not zero terminated*/
        char* temp = malloc(size + 1);
        if (temp == NULL)
        {
            printf("failed toomalloc\r\n");
            result = IOTHUBMESSAGE_ABANDONED;
        }
        else
        {
            (void)memcpy(temp, buffer, size);
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

Ce code est réutilisable--il a hello même pour une solution. Cette fonction reçoit le message de type hello et prend en charge le routage il toohello la fonction appropriée via l’appel de hello trop**EXECUTE\_commande**. fonction Hello appelée dépend à ce stade de la définition de hello d’actions hello dans votre modèle.

Lorsque vous définissez une action dans votre modèle, que vous devez tooimplement une fonction qui est appelée lorsque votre appareil reçoit le message de type hello correspondant. Par exemple, si votre modèle définit cette action :

```c
WITH_ACTION(SetAirResistance, int, Position)
```

Définissez une fonction avec cette signature :

```c
EXECUTE_COMMAND_RESULT SetAirResistance(ContosoAnemometer* device, int Position)
{
    (void)device;
    (void)printf("Setting Air Resistance Position too%d.\r\n", Position);
    return EXECUTE_COMMAND_SUCCESS;
}
```

Notez comment hello nom de fonction hello correspond au nom hello d’action hello dans le modèle de hello et que les paramètres de fonction hello hello correspondent aux paramètres de hello spécifiés pour l’action de hello. Hello premier paramètre est toujours requis et contient une instance de toohello de pointeur de votre modèle.

Lors de l’appareil de hello reçoit un message qui correspond à cette signature, la fonction correspondante de hello est appelée. Par conséquent, à l’exception d’ayant un code réutilisable hello tooinclude de **IoTHubMessage**, recevoir des messages est simplement de la définition d’une fonction simple pour chaque action définie dans votre modèle.

### <a name="uninitialize-hello-library"></a>Annuler l’initialisation de la bibliothèque de hello

Lorsque vous avez terminé d’envoi de données et recevoir des messages, vous pouvez annuler l’initialisation de bibliothèque de IoT hello :

```c
...
        DESTROY_MODEL_INSTANCE(myWeather);
    }
    IoTHubClient_LL_Destroy(iotHubClientHandle);
}
serializer_deinit();
```

Chacune de ces trois fonctions s’aligne avec trois fonctions d’initialisation hello décrites précédemment. L’appel de ces API vous permet de libérer les ressources affectées au préalable.

## <a name="next-steps"></a>Étapes suivantes

Cet article couvert les principes fondamentaux de hello de l’utilisation de bibliothèques hello Bonjour **appareil Azure IoT SDK pour C**. Il vous fourni suffisamment toounderstand informations ce qui est inclus dans hello SDK, son architecture, et comment tooget commencer à utiliser les exemples Windows hello. l’article suivant de Hello continue description hello Hello SDK en expliquant [plus sur la bibliothèque de IoTHubClient hello](iot-hub-device-sdk-c-iothubclient.md).

toolearn plus sur le développement pour IoT Hub, consultez hello [kits de développement logiciel Azure IoT][lnk-sdks].

toofurther Explorez les fonctionnalités de hello d’IoT Hub, consultez :

* [Simulation d’un appareil avec Azure IoT Edge][lnk-iotedge]

[lnk-file upload]: iot-hub-csharp-csharp-file-upload.md
[lnk-create-hub]: iot-hub-rm-template-powershell.md
[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
