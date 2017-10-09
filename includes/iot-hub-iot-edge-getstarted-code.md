## <a name="typical-output"></a>Exemple de résultat

Hello suivant montre sortie hello écrit le fichier de journal de toohello par hello Hello World (exemple). sortie de Hello est mise en forme pour une meilleure lisibilité :

```json
[{
    "time": "Mon Apr 11 13:48:07 2016",
    "content": "Log started"
}, {
    "time": "Mon Apr 11 13:48:48 2016",
    "properties": {
        "helloWorld": "from Azure IoT Gateway SDK simple sample!"
    },
    "content": "aGVsbG8gd29ybGQ="
}, {
    "time": "Mon Apr 11 13:48:55 2016",
    "properties": {
        "helloWorld": "from Azure IoT Gateway SDK simple sample!"
    },
    "content": "aGVsbG8gd29ybGQ="
}, {
    "time": "Mon Apr 11 13:49:01 2016",
    "properties": {
        "helloWorld": "from Azure IoT Gateway SDK simple sample!"
    },
    "content": "aGVsbG8gd29ybGQ="
}, {
    "time": "Mon Apr 11 13:49:04 2016",
    "content": "Log stopped"
}]
```

## <a name="code-snippets"></a>Extraits de code

Cette section présente certaines des sections spécifiques de code hello dans Bonjour Bonjour\_world (exemple).

### <a name="iot-edge-gateway-creation"></a>Création de la passerelle IoT Edge

Vous devez implémenter un *processus de passerelle*. Ce programme crée l’infrastructure interne de hello (broker hello), charge les modules de IoT bord hello et configure le processus de passerelle hello. IoT Edge fournit hello **passerelle\_créer\_de\_JSON** fonction tooenable toobootstrap une passerelle à partir d’un fichier JSON. toouse hello **passerelle\_créer\_de\_JSON** fonctionner, passez-le hello chemin d’accès tooa fichier JSON qui spécifie hello tooload de modules IoT Edge.

Vous pouvez trouver le code de hello pour le processus de passerelle hello Bonjour *Hello World* exemple Bonjour [main.c] [ lnk-main-c] fichier. Pour une meilleure lisibilité, hello extrait de code suivant montre une version abrégée de code hello du processus de passerelle. Cet exemple de programme crée une passerelle, puis attend pour hello de hello utilisateur toopress **entrée** avant qu’il met fin à la passerelle de hello de clé.

```c
int main(int argc, char** argv)
{
    GATEWAY_HANDLE gateway;
    if ((gateway = Gateway_Create_From_JSON(argv[1])) == NULL)
    {
        printf("failed toocreate hello gateway from JSON\n");
    }
    else
    {
        printf("gateway successfully created from JSON\n");
        printf("gateway shall run until ENTER is pressed\n");
        (void)getchar();
        Gateway_LL_Destroy(gateway);
    }
    return 0;
}
```

fichier de paramètres JSON Hello contient une liste de tooload de modules IoT Edge et liens hello entre modules de hello. Chaque module IoT Edge doit spécifier les éléments suivants :

* **nom**: un nom unique pour le module de hello.
* **chargeur**: un chargeur qui sait comment hello de tooload souhaité module. Les chargeurs correspondent à un point d’extension pour le chargement des différents types de modules. IoT Edge fournit des chargeurs compatibles avec des modules écrits nativement en C, en Node.js, en Java et en .NET. Hello, exemple Hello World utilise uniquement le chargeur de C natif hello, car tous les modules de hello dans cet exemple sont des bibliothèques dynamiques écrites en C. Pour plus d’informations sur les modules de IoT bord toouse écrits dans différents langages, consultez hello [Node.js](https://github.com/Azure/iot-edge/blob/master/samples/nodejs_simple_sample/), [Java](https://github.com/Azure/iot-edge/tree/master/samples/java_sample), ou [.NET](https://github.com/Azure/iot-edge/tree/master/samples/dotnet_binding_sample) exemples.
    * **nom**: nom hello du chargeur de hello utilisé le module de hello tooload.
    * **point d’entrée**: bibliothèque de toohello hello chemin d’accès contenant le module de hello. Il s’agit d’un fichier .so sous Linux, et d’un fichier .dll sous Windows. point d’entrée Hello est de type toohello spécifique du chargeur utilisé. Hello point d’entrée du chargeur Node.js est un fichier .js. Hello point d’entrée du chargeur Java est un chemin de classe et un nom de classe. Hello point d’entrée du chargeur .NET est un nom d’assembly et un nom de classe.

* **args**: a besoin de n’importe quel module de hello d’informations de configuration.

Hello suivant de code montre hello JSON utilisé toodeclare tous les hello modules IoT Edge pour hello, exemple Hello World sur Linux. Si un module requiert des arguments dépend de la conception hello du module de hello. Dans cet exemple, le module de journalisation hello prend un argument qui est le fichier de sortie toohello hello chemin d’accès et Bonjour Bonjour\_module du monde dispose d’aucun argument.

```json
"modules" :
[
    {
        "name" : "logger",
        "loader": {
          "name": "native",
          "entrypoint": {
            "module.path": "./modules/logger/liblogger.so"
        }
        },
        "args" : {"filename":"log.txt"}
    },
    {
        "name" : "hello_world",
        "loader": {
          "name": "native",
          "entrypoint": {
            "module.path": "./modules/hello_world/libhello_world.so"
        }
        },
        "args" : null
    }
]
```

fichier JSON de Hello contient également des liens hello entre modules hello passés toohello broker. Une liaison possède deux propriétés :

* **source**: un nom de module à partir de hello `modules` section, ou `\*`.
* **récepteur**: un nom de module à partir de hello `modules` section.

Chaque liaison définit un itinéraire de message et une direction. Messages de hello **source** module sont remis toohello **récepteur** module. Vous pouvez définir hello **source** module trop`\*`, ce qui signifie que hello **récepteur** module reçoit des messages à partir de n’importe quel module.

Hello de code suivant montre hello JSON utilisé tooconfigure les liens entre les modules hello utilisés dans Bonjour Bonjour\_world (exemple) sur Linux. Tous les messages produits par hello `hello_world` module est consommé par hello `logger` module.

```json
"links":
[
    {
        "source": "hello_world",
        "sink": "logger"
    }
]
```

### <a name="helloworld-module-message-publishing"></a>Publication des messages du module hello\_world

Vous pouvez trouver le code hello utilisé par Bonjour Bonjour\_messages toopublish du module du monde Bonjour ['hello_world.c'] [ lnk-helloworld-c] fichier. Hello extrait de code suivant montre une version modifiée du code de hello avec commentaires ajoutés et une erreur de la gestion du code supprimé pour une meilleure lisibilité :

```c
int helloWorldThread(void *param)
{
    // create data structures used in function.
    HELLOWORLD_HANDLE_DATA* handleData = param;
    MESSAGE_CONFIG msgConfig;
    MAP_HANDLE propertiesMap = Map_Create(NULL);

    // add a property named "helloWorld" with a value of "from Azure IoT
    // Gateway SDK simple sample!" tooa set of message properties that
    // will be appended toohello message before publishing it. 
    Map_AddOrUpdate(propertiesMap, "helloWorld", "from Azure IoT Gateway SDK simple sample!")

    // set hello content for hello message
    msgConfig.size = strlen(HELLOWORLD_MESSAGE);
    msgConfig.source = HELLOWORLD_MESSAGE;

    // set hello properties for hello message
    msgConfig.sourceProperties = propertiesMap;

    // create a message based on hello msgConfig structure
    MESSAGE_HANDLE helloWorldMessage = Message_Create(&msgConfig);

    while (1)
    {
        if (handleData->stopThread)
        {
            (void)Unlock(handleData->lockHandle);
            break; /*gets out of hello thread*/
        }
        else
        {
            // publish hello message toohello broker
            (void)Broker_Publish(handleData->brokerHandle, helloWorldMessage);
            (void)Unlock(handleData->lockHandle);
        }

        (void)ThreadAPI_Sleep(5000); /*every 5 seconds*/
    }

    Message_Destroy(helloWorldMessage);

    return 0;
}
```

### <a name="helloworld-module-message-processing"></a>Traitement des messages du module hello\_world

Bonjour Bonjour\_module du monde jamais traite les messages que les autres modules IoT bord publient toohello broker. Par conséquent, hello implémentation du rappel de message hello dans Bonjour Bonjour\_world du module est une fonction de l’absence d’opération.

```c
static void HelloWorld_Receive(MODULE_HANDLE moduleHandle, MESSAGE_HANDLE messageHandle)
{
    /* No action, HelloWorld is not interested in any messages. */
}
```

### <a name="logger-module-message-publishing-and-processing"></a>Publication et traitement des messages du module enregistreur

module d’enregistreur d’événements Hello reçoit des messages du service Broker pour hello et les écrit tooa fichier. Il ne publie jamais les messages. Par conséquent, code hello du module du journal hello appelle jamais hello **Broker_Publish** (fonction).

Hello **Logger_Receive** fonction Bonjour [logger.c] [ lnk-logger-c] fichier est le service broker de hello hello rappel appelle le module de journalisation toohello toodeliver messages. Hello extrait de code suivant montre une version modifiée avec commentaires ajoutés et une erreur de la gestion du code supprimé pour une meilleure lisibilité :

```c
static void Logger_Receive(MODULE_HANDLE moduleHandle, MESSAGE_HANDLE messageHandle)
{

    time_t temp = time(NULL);
    struct tm* t = localtime(&temp);
    char timetemp[80] = { 0 };

    // Get hello message properties from hello message
    CONSTMAP_HANDLE originalProperties = Message_GetProperties(messageHandle); 
    MAP_HANDLE propertiesAsMap = ConstMap_CloneWriteable(originalProperties);

    // Convert hello collection of properties into a JSON string
    STRING_HANDLE jsonProperties = Map_ToJSON(propertiesAsMap);

    //  base64 encode hello message content
    const CONSTBUFFER * content = Message_GetContent(messageHandle);
    STRING_HANDLE contentAsJSON = Base64_Encode_Bytes(content->buffer, content->size);

    // Start hello construction of hello final string toobe logged by adding
    // hello timestamp
    STRING_HANDLE jsonToBeAppended = STRING_construct(",{\"time\":\"");
    STRING_concat(jsonToBeAppended, timetemp);

    // Add hello message properties
    STRING_concat(jsonToBeAppended, "\",\"properties\":"); 
    STRING_concat_with_STRING(jsonToBeAppended, jsonProperties);

    // Add hello content
    STRING_concat(jsonToBeAppended, ",\"content\":\"");
    STRING_concat_with_STRING(jsonToBeAppended, contentAsJSON);
    STRING_concat(jsonToBeAppended, "\"}]");

    // Write hello formatted string
    LOGGER_HANDLE_DATA *handleData = (LOGGER_HANDLE_DATA *)moduleHandle;
    addJSONString(handleData->fout, STRING_c_str(jsonToBeAppended);
}
```

## <a name="next-steps"></a>Étapes suivantes

Dans cet article, vous avez exécuté une passerelle IoT bord simple qui écrit le fichier journal des messages tooa. toorun un exemple qui envoie des messages tooIoT Hub, consultez [IoT Edge – envoyer des messages de l’appareil-à-cloud avec un appareil simulé à l’aide de Linux] [ lnk-gateway-simulated-linux] ou [IoT Edge – envoyer les messages appareil-à-cloud avec un APPAREIL simulé à l’aide de Windows][lnk-gateway-simulated-windows].


<!-- Links -->
[lnk-main-c]: https://github.com/Azure/iot-edge/blob/master/samples/hello_world/src/main.c
[lnk-helloworld-c]: https://github.com/Azure/iot-edge/blob/master/modules/hello_world/src/hello_world.c
[lnk-logger-c]: https://github.com/Azure/iot-edge/blob/master/modules/logger/src/logger.c
[lnk-iot-edge]: https://github.com/Azure/iot-edge/
[lnk-gateway-simulated-linux]: ../articles/iot-hub/iot-hub-linux-iot-edge-simulated-device.md
[lnk-gateway-simulated-windows]: ../articles/iot-hub/iot-hub-windows-iot-edge-simulated-device.md