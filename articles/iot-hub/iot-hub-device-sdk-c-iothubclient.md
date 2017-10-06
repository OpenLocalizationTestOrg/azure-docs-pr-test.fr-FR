---
title: aaaAzure, appareils IoT SDK pour C - IoTHubClient | Documents Microsoft
description: "La bibliothèque de IoTHubClient toouse hello dans le dispositif hello Azure IoT SDK des applications d’appareil toocreate C qui communiquent avec un hub IoT."
services: iot-hub
documentationcenter: 
author: olivierbloch
manager: timlt
editor: 
ms.assetid: 828cf2bf-999d-4b8a-8a28-c7c901629600
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/06/2016
ms.author: obloch
ms.openlocfilehash: d1ece79e9ba6d1e5fd45cabb8fca393b24052e07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-device-sdk-for-c--more-about-iothubclient"></a>Kit de développement logiciel d’appareil Azure IoT pour C : en savoir plus sur IoTHubClient
Hello [tout d’abord l’article](iot-hub-device-sdk-c-intro.md) cette Bonjour série introduites **appareil Azure IoT SDK pour C**. Cet article explique qu’il existe deux couches architecturales dans le Kit de développement logiciel (SDK). À la base de hello est hello **IoTHubClient** bibliothèque qui gère la communication avec IoT Hub directement. Il est également hello **sérialiseur** bibliothèque qui génère tooprovide de services de sérialisation. Dans cet article, nous fournissons des détails supplémentaires sur hello **IoTHubClient** bibliothèque.

Hello précédent article décrit comment toouse hello **IoTHubClient** bibliothèque toosend événements tooIoT Hub et recevoir des messages. Cet article étend cette discussion et explique comment gérer précisément toomore *lorsque* vous envoyer et recevoir des données, elle vous initiant toohello **API de niveau inférieur**. Nous allons également expliquer comment tooattach propriétés tooevents (et les récupérer à partir de messages) à l’aide de la propriété hello la gestion des fonctionnalités de hello **IoTHubClient** bibliothèque. Enfin, nous fournissons une explication supplémentaire de différentes façons toohandle messages reçus à partir de IoT Hub.

Hello article se termine en couvrant plusieurs rubriques divers, y compris les plus sur les informations d’identification de l’appareil et comment toochange hello comportement Hello **IoTHubClient** les options de configuration.

Nous allons utiliser hello **IoTHubClient** SDK exemples tooexplain ces rubriques. Si vous souhaitez toofollow le long, consultez hello **iothub\_client\_exemple\_http** et **iothub\_client\_exemple\_amqp** les applications qui sont incluses dans le dispositif de Azure IoT hello SDK pour C. tous les éléments décrits dans les sections suivantes de hello est illustré dans ces exemples.

Vous pouvez trouver hello [ **appareil Azure IoT SDK pour C** ](https://github.com/Azure/azure-iot-sdk-c) GitHub référentiel et consulter les détails de hello API Bonjour [référence d’API C](https://azure.github.io/azure-iot-sdk-c/index.html).

## <a name="hello-lower-level-apis"></a>Hello API de niveau inférieur
article précédent de Hello décrit les opérations de base hello Hello **IotHubClient** au sein du contexte hello Hello **iothub\_client\_exemple\_amqp** application. Par exemple, il explique comment tooinitialize hello bibliothèque à l’aide de ce code.

```
IOTHUB_CLIENT_HANDLE iotHubClientHandle;
iotHubClientHandle = IoTHubClient_CreateFromConnectionString(connectionString, AMQP_Protocol);
```

Il décrit également comment les événements de toosend à l’aide de cette appel de fonction.

```
IoTHubClient_SendEventAsync(iotHubClientHandle, message.messageHandle, SendConfirmationCallback, &message);
```

article de Hello décrit également comment les messages tooreceive en inscrivant une fonction de rappel.

```
int receiveContext = 0;
IoTHubClient_SetMessageCallback(iotHubClientHandle, ReceiveMessageCallback, &receiveContext);
```

article de Hello a également montré comment toofree les ressources à l’aide de code tels que les suivants hello.

```
IoTHubClient_Destroy(iotHubClientHandle);
```

Il existe toutefois des tooeach de fonctions d’accompagnement de ces API :

* IoTHubClient\_LL\_CreateFromConnectionString
* IoTHubClient\_LL\_SendEventAsync
* IoTHubClient\_LL\_SetMessageCallback
* IoTHubClient\_LL\_Destroy

Ces fonctions tous incluent « LL » dans le nom de l’API hello. Reste, paramètres hello de chacune de ces fonctions sont équivalents et de non-LL tootheir identiques. Toutefois, le comportement hello de ces fonctions est différent sur un point important.

Lorsque vous appelez **IoTHubClient\_CreateFromConnectionString**, les bibliothèques sous-jacentes hello créent un nouveau thread qui s’exécute en arrière-plan de hello. Ce thread envoie les événements vers IoT Hub et reçoit les messages émanant d’IoT Hub. Aucun thread n’est créé lorsque vous travaillez avec hello « LL » API. la création du thread d’arrière-plan hello Hello est développeur toohello plus de commodité. Vous n’avez pas tooworry sur l’envoi d’événements et la réception de messages à partir de IoT Hub--il se produit automatiquement en arrière-plan de hello explicitement. En revanche, hello « LL » API vous donner un contrôle explicite sur la communication avec IoT Hub, si vous en avez besoin.

toounderstand cette favorable, examinons un exemple :

Lorsque vous appelez **IoTHubClient\_SendEventAsync**, ce que vous faites réellement pour placer des événements de hello dans une mémoire tampon. Hello thread d’arrière-plan créé quand vous appelez **IoTHubClient\_CreateFromConnectionString** continuellement surveille cette mémoire tampon et envoie des données qu’il contient tooIoT Hub. Dans ce cas en arrière-plan hello en hello en même temps que hello thread principal exécute un autre travail.

De même, lorsque vous enregistrez une fonction de rappel pour les messages à l’aide de **IoTHubClient\_SetMessageCallback**, vous êtes demandant d’arrière-plan de hello SDK toohave hello thread appeler la fonction de rappel hello lorsqu’un message reçu, indépendamment du thread principal de hello.

Hello « LL » API ne créez pas un thread d’arrière-plan. Au lieu de cela, une nouvelle API doit être appelée tooexplicitly envoyer et recevoir des données à partir de IoT Hub. Cela est illustré dans hello l’exemple suivant.

Hello **iothub\_client\_exemple\_http** application qui est incluse dans hello SDK montre hello API de niveau inférieur. Dans cet exemple, nous envoyer des événements tooIoT concentrateur avec le code suivant de hello :

```
EVENT_INSTANCE message;
sprintf_s(msgText, sizeof(msgText), "Message_%d_From_IoTHubClient_LL_Over_HTTP", i);
message.messageHandle = IoTHubMessage_CreateFromByteArray((const unsigned char*)msgText, strlen(msgText));

IoTHubClient_LL_SendEventAsync(iotHubClientHandle, message.messageHandle, SendConfirmationCallback, &message)
```

message de type hello créent Hello trois premières lignes et dernière ligne de hello envoie les événements hello. Toutefois, comme mentionné précédemment, « envoi » les événements hello signifie que les données de salutation sont simplement placées dans une mémoire tampon. Rien n’est transmis sur le réseau de hello lorsque nous appelons **IoTHubClient\_LL\_SendEventAsync**. Dans l’ordre tooactually entrée hello données tooIoT Hub, vous devez appeler **IoTHubClient\_LL\_DoWork**, comme dans cet exemple :

```
while (1)
{
    IoTHubClient_LL_DoWork(iotHubClientHandle);
    ThreadAPI_Sleep(1000);
}
```

Ce code (à partir de hello **iothub\_client\_exemple\_http** application) appelle à plusieurs reprises **IoTHubClient\_LL\_DoWork** . Chaque fois que **IoTHubClient\_LL\_DoWork** est appelé, il envoie certains événements de tooIoT de mémoire tampon hello Hub et il récupère un message en file d’attente envoyé toohello appareil. ce dernier cas de Hello signifie que si nous inscrit une fonction de rappel pour les messages, puis hello de rappel est appelée (en supposant que tous les messages sont la file d’attente). Nous serait inscrit une telle fonction de rappel avec le code suivant de hello :

```
IoTHubClient_LL_SetMessageCallback(iotHubClientHandle, ReceiveMessageCallback, &receiveContext)
```

Hello raison pour laquelle **IoTHubClient\_LL\_DoWork** est souvent appelée dans une boucle est que chaque fois qu’elle est appelée, elle envoie *certains* mis en mémoire tampon des événements tooIoT Hub et récupère *hello ensuite* message de la file d’attente pour le périphérique de hello. Chaque appel n’est pas garanti que les toosend toutes les mises en mémoire tamponné les événements ou en file d’attente tooretrieve tous les messages. Si vous souhaitez toosend tous les événements de hello de la mémoire tampon et poursuivez avec un autre traitement, vous pouvez remplacer cette boucle avec le code suivant de hello :

```
IOTHUB_CLIENT_STATUS status;

while ((IoTHubClient_LL_GetSendStatus(iotHubClientHandle, &status) == IOTHUB_CLIENT_OK) && (status == IOTHUB_CLIENT_SEND_STATUS_BUSY))
{
    IoTHubClient_LL_DoWork(iotHubClientHandle);
    ThreadAPI_Sleep(1000);
}
```

Ce code appelle **IoTHubClient\_LL\_DoWork** jusqu'à ce que tous les événements dans la mémoire tampon de hello ont été envoyés tooIoT Hub. Notez que cela ne signifie pas non plus que tous les messages en file d’attente ont été reçus. Partie de raison hello est que la vérification des messages « tous » n’est pas déterministe comme une action. Que se passe-t-il si vous récupérez « all » de messages hello, mais ensuite un autre est envoyé toohello appareil immédiatement après ? Une meilleure toodeal de façon avec qui est un délai d’attente programmée. Par exemple, fonction de rappel de message hello pourrait réinitialiser un minuteur chaque fois qu’elle est appelée. Vous pouvez ensuite écrire le traitement de logique toocontinue si, par exemple, aucun message n’ont été reçus dans hello dernière *X* secondes.

Lorsque vous les événements de la pénétration de molécules terminé et recevoir des messages, être toocall vraiment hello correspondant fonction tooclean des ressources.

```
IoTHubClient_LL_Destroy(iotHubClientHandle);
```

En fait, il n'est qu’un ensemble d’API toosend et recevoir des données avec un thread d’arrière-plan et un autre ensemble d’API qui hello même chose sans thread d’arrière-plan hello. De nombreux développeurs préfèrent hello non - LL API, mais hello API de niveau inférieur est utiles lorsque le développeur de hello veut contrôle explicite sur les transmissions réseau. Par exemple, certains appareils recueillent des données au fil du temps et n’enregistrent que les événements à des intervalles spécifiés (par exemple, une fois par heure ou une fois par jour). Bonjour donnez aux API de niveau inférieur vous hello contrôle tooexplicitly de capacité lorsque vous envoyez et recevez des données à partir de IoT Hub. D’autres préfèreront à plus de simplicité hello simplement que hello que fournit des API de niveau inférieur. Tout se produit sur le thread principal de hello plutôt que certains se produise de travail en arrière-plan de hello.

Le modèle que vous choisissez, être vraiment toobe cohérente dans lesquelles API que vous utilisez. Si vous démarrez en appelant **IoTHubClient\_LL\_CreateFromConnectionString**, veillez à utiliser uniquement hello correspondant API de niveau inférieur pour tout travail de suivi :

* IoTHubClient\_LL\_SendEventAsync
* IoTHubClient\_LL\_SetMessageCallback
* IoTHubClient\_LL\_Destroy
* IoTHubClient\_LL\_DoWork

Hello inverse est vrai également. Si vous démarrez avec **IoTHubClient\_CreateFromConnectionString**, puis utilisez hello non - LL interfaces API pour un traitement supplémentaire.

Dans l’appareil Azure IoT hello SDK pour C, consultez hello **iothub\_client\_exemple\_http** inférieur de niveau application pour obtenir un exemple complet de hello API. Hello **iothub\_client\_exemple\_amqp** application peut être référencée pour obtenir un exemple complet de hello non - LL API.

## <a name="property-handling"></a>Gestion des propriétés
Jusqu'à présent lorsque nous avons décrit l’envoi de données, nous avons été référence toohello des corps de message de type hello. Considérez par exemple le code suivant :

```
EVENT_INSTANCE message;
sprintf_s(msgText, sizeof(msgText), "Hello World");
message.messageHandle = IoTHubMessage_CreateFromByteArray((const unsigned char*)msgText, strlen(msgText));
IoTHubClient_LL_SendEventAsync(iotHubClientHandle, message.messageHandle, SendConfirmationCallback, &message)
```

Cet exemple envoie un message de tooIoT concentrateur avec le texte hello « Hello World ». Toutefois, IoT Hub permet également de message de propriétés toobe tooeach attaché. Les propriétés sont des paires nom/valeur qui peuvent être attaché toohello message. Par exemple, nous pouvons modifier hello précédent code tooattach une propriété de message toohello :

```
MAP_HANDLE propMap = IoTHubMessage_Properties(message.messageHandle);
sprintf_s(propText, sizeof(propText), "%d", i);
Map_AddOrUpdate(propMap, "SequenceNumber", propText);
```

Nous allons commencer par appeler **IoTHubMessage\_propriétés** et en lui passant hello handle de notre message. Ce que nous obtenons est un **carte\_gérer** référence qui nous permet de toostart Ajout de propriétés. Hello ce dernier s’effectue en appelant **carte\_AddOrUpdate**, qui accepte une référence de tooa carte\_HANDLE, nom de la propriété hello et valeur de la propriété hello. Avec cette API, nous pouvons ajouter autant de propriétés que nous le souhaitons.

Lorsque les événements hello sont lu à partir de **concentrateurs d’événements**, récepteur de hello peut énumérer les propriétés hello et récupérer leurs valeurs correspondantes. Par exemple, dans .NET cela interviendrait en accédant à hello [collection de propriétés de l’objet de EventData hello](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.eventdata.properties.aspx).

Dans l’exemple précédent de hello, nous allons attacher des événements de tooan de propriétés que nous envoyer tooIoT Hub. Propriétés peuvent également être attachés toomessages provenant du IoT Hub. Si nous voulons tooretrieve des propriétés d’un message, nous pouvons utiliser le code tel que hello suivant dans votre fonction de rappel de message :

```
static IOTHUBMESSAGE_DISPOSITION_RESULT ReceiveMessageCallback(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    . . .

    // Retrieve properties from hello message
    MAP_HANDLE mapProperties = IoTHubMessage_Properties(message);
    if (mapProperties != NULL)
    {
        const char*const* keys;
        const char*const* values;
        size_t propertyCount = 0;
        if (Map_GetInternals(mapProperties, &keys, &values, &propertyCount) == MAP_OK)
        {
            if (propertyCount > 0)
            {
                printf("Message Properties:\r\n");
                for (size_t index = 0; index < propertyCount; index++)
                {
                    printf("\tKey: %s Value: %s\r\n", keys[index], values[index]);
                }
                printf("\r\n");
            }
        }
    }

    . . .
}
```

Hello appel trop**IoTHubMessage\_propriétés** renvoie hello **carte\_gérer** référence. Nous avons ensuite passer cette référence trop**carte\_GetInternals** tooobtain un tableau de tooan de référence de nom/valeur de hello paires (ainsi que le nombre de propriétés de hello). À ce stade, il est très simple de l’énumération hello propriétés tooget toohello valeurs.

Vous n’avez toouse propriétés dans votre application. Toutefois, si vous avez besoin de tooset à des événements ou en extraire les messages, hello **IoTHubClient** bibliothèque facilite la tâche.

## <a name="message-handling"></a>Gestion des messages
Comme indiqué précédemment, lorsque les messages arrivent de hello de IoT Hub **IoTHubClient** bibliothèque répond en appelant une fonction de rappel enregistré. Un des paramètres de retour de cette fonction mérite cependant quelques explications supplémentaires. Voici un extrait de la fonction de rappel hello Bonjour **iothub\_client\_exemple\_http** exemple d’application :

```
static IOTHUBMESSAGE_DISPOSITION_RESULT ReceiveMessageCallback(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    . . .
    return IOTHUBMESSAGE_ACCEPTED;
}
```

Notez que le type de retour hello est **IOTHUBMESSAGE\_DISPOSITION\_résultat** et dans ce cas particulier, nous renvoyons **IOTHUBMESSAGE\_accepté**. Il existe d’autres valeurs que nous pouvons retourner à partir de cette fonction que modification hello comment **IoTHubClient** bibliothèque réagit toohello rappel du message. Voici les options hello.

* **IOTHUBMESSAGE\_accepté** – message de salutation a été correctement traité. Hello **IoTHubClient** bibliothèque n’appelle pas la fonction de rappel hello avec hello même message.
* **IOTHUBMESSAGE\_rejeté** : message d’appel n’a pas été traité et existe dans aucun toodo désir ne hello futures. Hello **IoTHubClient** bibliothèque ne doit pas appeler de fonction de rappel hello avec hello même message.
* **IOTHUBMESSAGE\_abandonné** : message d’appel n’a pas été traité avec succès, mais hello **IoTHubClient** bibliothèque doit appeler la fonction de rappel hello avec hello même message.

Pourquoi tout d’abord deux codes de retour, hello **IoTHubClient** bibliothèque envoie un tooIoT message Hub indiquant ce message de type hello doit être supprimé de la file d’attente de hello et n’a pas remis à nouveau. effet net de Hello est hello même (message de type hello est supprimé à partir de la file d’attente de hello), mais si le message de salutation a été accepté ou rejeté est toujours enregistré.  L’enregistrement de cette distinction est utile toosenders de message de type hello qui peut écouter des commentaires et déterminer si un périphérique a accepté ou rejeté un message particulier.

Dans le dernier cas de hello, un message est envoyé également tooIoT concentrateur, mais indique que message de type hello doit être de nouveau remis. En général, vous devez abandonner un message si vous rencontrez une erreur mais tootry tooprocess hello message à nouveau. En revanche, la rejeter un message est appropriée lorsque vous rencontrez une erreur irrécupérable (ou si vous décidez simplement vous ne souhaitez pas que message de type hello tooprocess).

Dans tous les cas, tenez compte des codes de retour différents hello afin que vous pouvez provoquer le comportement de hello que vous souhaitez à partir de hello **IoTHubClient** bibliothèque.

## <a name="alternate-device-credentials"></a>Autres informations d’identification d’appareil
Comme expliqué précédemment, hello première toodo lorsque vous travaillez avec hello **IoTHubClient** bibliothèque est tooobtain un **IOTHUB\_CLIENT\_gérer** avec un appel de hello suivant :

```
IOTHUB_CLIENT_HANDLE iotHubClientHandle;
iotHubClientHandle = IoTHubClient_CreateFromConnectionString(connectionString, AMQP_Protocol);
```

Hello arguments trop**IoTHubClient\_CreateFromConnectionString** sont une chaîne de connexion de périphérique hello et un paramètre qui indique le protocole hello nous utilisons toocommunicate avec IoT Hub. chaîne de connexion de périphérique Hello a un format qui s’affiche comme suit :

```
HostName=IOTHUBNAME.IOTHUBSUFFIX;DeviceId=DEVICEID;SharedAccessKey=SHAREDACCESSKEY
```

Il existe ici quatre éléments d’information : le nom IoT Hub, le suffixe IoT Hub, l’ID d’appareil et la clé d’accès partagé. Vous obtenez le nom de domaine complet (FQDN) hello d’un hub IoT lorsque vous créez votre instance de hub IoT Bonjour portail Azure, cela vous donne nom de hub IoT hello (hello première partie du nom de domaine complet de hello) et le suffixe de hub IoT hello (hello rest nom de domaine complet de Hello). Vous obtenez les ID de périphérique hello et clé d’accès partagé hello lorsque vous inscrivez votre appareil avec IoT Hub (comme décrit dans hello [article précédent](iot-hub-device-sdk-c-intro.md)).

**IoTHubClient\_CreateFromConnectionString** vous donne la bibliothèque de hello tooinitialize unidirectionnel. Si vous préférez, vous pouvez créer un nouveau **IOTHUB\_CLIENT\_gérer** à l’aide de ces paramètres individuels plutôt que de chaîne de connexion de périphérique hello. Cela est possible avec hello suivant de code :

```
IOTHUB_CLIENT_CONFIG iotHubClientConfig;
iotHubClientConfig.iotHubName = "";
iotHubClientConfig.deviceId = "";
iotHubClientConfig.deviceKey = "";
iotHubClientConfig.iotHubSuffix = "";
iotHubClientConfig.protocol = HTTP_Protocol;
IOTHUB_CLIENT_HANDLE iotHubClientHandle = IoTHubClient_LL_Create(&iotHubClientConfig);
```

Ceci fait hello même chose que **IoTHubClient\_CreateFromConnectionString**.

Cela peut paraître évident que vous souhaitiez toouse **IoTHubClient\_CreateFromConnectionString** au lieu de cette méthode plus détaillée de l’initialisation. Cependant, gardez à l’esprit que lorsque vous enregistrez un appareil dans IoT Hub, vous obtenez un ID d’appareil et une clé d’appareil (pas une chaîne de connexion). Hello *Explorateur de périphérique* outil du Kit de développement logiciel introduite dans hello [article précédent](iot-hub-device-sdk-c-intro.md) utilise les bibliothèques Bonjour **Azure IoT service SDK** toocreate hello appareil chaîne de connexion ID de périphérique Hello, la clé de périphérique et le nom d’hôte de IoT Hub. Ainsi, l’appel **IoTHubClient\_LL\_créer** peut être préférable, car elle permet d’étape hello de la génération d’une chaîne de connexion. Utilisez la méthode adéquate.

## <a name="configuration-options"></a>Options de configuration
Jusqu'à présent tous les éléments décrits sur hello de façon hello **IoTHubClient** bibliothèque works reflète son comportement par défaut. Toutefois, il existe quelques options que vous pouvez définir toochange fonctionne de la bibliothèque de hello. Cela est effectué en tirant parti de hello **IoTHubClient\_LL\_SetOption** API. Examinez cet exemple :

```
unsigned int timeout = 30000;
IoTHubClient_LL_SetOption(iotHubClientHandle, "timeout", &timeout);
```

Quelques options sont couramment utilisées :

* **SetBatching** (bool) – si **true**, alors les données envoyées tooIoT Hub est envoyé par lots. Si elle a la valeur **false**, les messages sont envoyés individuellement. valeur par défaut Hello est **false**. Notez que hello **SetBatching** option s’applique uniquement au protocole de toohello HTTP pas aux protocoles de toohello MQTT ou AMQP.
* **Timeout** (unsigned int) : cette valeur est exprimée en millisecondes. Si vous envoyez une demande HTTP ou recevoir une réponse dure plus longtemps que cette fois, puis hello connexion expire.

option de traitement par lot de Hello est important. Par défaut, hello les événements d’une bibliothèque ingresses individuellement (un seul événement est tout ce que vous passez trop**IoTHubClient\_LL\_SendEventAsync**). Si l’option de traitement par lot de hello est **true**, bibliothèque de hello collecte les événements autant que possible à partir du tampon hello (haut toohello taille maximale du message qui accepte les IoT Hub).  Hello lot d’événements est envoyé tooIoT concentrateur dans un seul appel HTTP (les événements individuels de hello sont regroupés dans un tableau JSON). L’activation de l’option de traitement par lot permet d’obtenir des gains de performance, car vous réduisez le nombre d’allers-retours sur le réseau. Elle réduit également considérablement la bande passante, car vous envoyez un seul ensemble d’en-têtes HTTP avec un lot d’événements plutôt qu’un ensemble d’en-têtes pour chaque événement individuel. En général, sauf si vous avez une raison spécifique de toodo dans le cas contraire, vous pouvez répondre tooenable de traitement par lot.

## <a name="next-steps"></a>Étapes suivantes
Cet article décrit un comportement hello détail de hello **IoTHubClient** bibliothèque trouvé dans hello **appareil Azure IoT SDK pour C**. Avec cette information, doit avoir une bonne compréhension des fonctionnalités de hello Hello **IoTHubClient** bibliothèque. Hello [l’article suivant](iot-hub-device-sdk-c-serializer.md) fournit des détails similaires sur hello **sérialiseur** bibliothèque.

toolearn plus sur le développement pour IoT Hub, consultez hello [kits de développement logiciel Azure IoT][lnk-sdks].

toofurther Explorez les fonctionnalités de hello d’IoT Hub, consultez :

* [Simulation d’un appareil avec Azure IoT Edge][lnk-iotedge]

[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
