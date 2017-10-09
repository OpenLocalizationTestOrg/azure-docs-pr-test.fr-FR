## <a name="typical-output"></a><span data-ttu-id="e14d9-101">Exemple de résultat</span><span class="sxs-lookup"><span data-stu-id="e14d9-101">Typical output</span></span>

<span data-ttu-id="e14d9-102">Hello suivant montre sortie hello écrit le fichier de journal de toohello par hello Hello World (exemple).</span><span class="sxs-lookup"><span data-stu-id="e14d9-102">hello following example shows hello output written toohello log file by hello Hello World sample.</span></span> <span data-ttu-id="e14d9-103">sortie de Hello est mise en forme pour une meilleure lisibilité :</span><span class="sxs-lookup"><span data-stu-id="e14d9-103">hello output is formatted for legibility:</span></span>

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

## <a name="code-snippets"></a><span data-ttu-id="e14d9-104">Extraits de code</span><span class="sxs-lookup"><span data-stu-id="e14d9-104">Code snippets</span></span>

<span data-ttu-id="e14d9-105">Cette section présente certaines des sections spécifiques de code hello dans Bonjour Bonjour\_world (exemple).</span><span class="sxs-lookup"><span data-stu-id="e14d9-105">This section discusses some key sections of hello code in hello hello\_world sample.</span></span>

### <a name="iot-edge-gateway-creation"></a><span data-ttu-id="e14d9-106">Création de la passerelle IoT Edge</span><span class="sxs-lookup"><span data-stu-id="e14d9-106">IoT Edge gateway creation</span></span>

<span data-ttu-id="e14d9-107">Vous devez implémenter un *processus de passerelle*.</span><span class="sxs-lookup"><span data-stu-id="e14d9-107">You must implement a *gateway process*.</span></span> <span data-ttu-id="e14d9-108">Ce programme crée l’infrastructure interne de hello (broker hello), charge les modules de IoT bord hello et configure le processus de passerelle hello.</span><span class="sxs-lookup"><span data-stu-id="e14d9-108">This program creates hello internal infrastructure (hello broker), loads hello IoT Edge modules, and configures hello gateway process.</span></span> <span data-ttu-id="e14d9-109">IoT Edge fournit hello **passerelle\_créer\_de\_JSON** fonction tooenable toobootstrap une passerelle à partir d’un fichier JSON.</span><span class="sxs-lookup"><span data-stu-id="e14d9-109">IoT Edge provides hello **Gateway\_Create\_From\_JSON** function tooenable you toobootstrap a gateway from a JSON file.</span></span> <span data-ttu-id="e14d9-110">toouse hello **passerelle\_créer\_de\_JSON** fonctionner, passez-le hello chemin d’accès tooa fichier JSON qui spécifie hello tooload de modules IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="e14d9-110">toouse hello **Gateway\_Create\_From\_JSON** function, pass it hello path tooa JSON file that specifies hello IoT Edge modules tooload.</span></span>

<span data-ttu-id="e14d9-111">Vous pouvez trouver le code de hello pour le processus de passerelle hello Bonjour *Hello World* exemple Bonjour [main.c] [ lnk-main-c] fichier.</span><span class="sxs-lookup"><span data-stu-id="e14d9-111">You can find hello code for hello gateway process in hello *Hello World* sample in hello [main.c][lnk-main-c] file.</span></span> <span data-ttu-id="e14d9-112">Pour une meilleure lisibilité, hello extrait de code suivant montre une version abrégée de code hello du processus de passerelle.</span><span class="sxs-lookup"><span data-stu-id="e14d9-112">For legibility, hello following snippet shows an abbreviated version of hello gateway process code.</span></span> <span data-ttu-id="e14d9-113">Cet exemple de programme crée une passerelle, puis attend pour hello de hello utilisateur toopress **entrée** avant qu’il met fin à la passerelle de hello de clé.</span><span class="sxs-lookup"><span data-stu-id="e14d9-113">This example program creates a gateway and then waits for hello user toopress hello **ENTER** key before it tears down hello gateway.</span></span>

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

<span data-ttu-id="e14d9-114">fichier de paramètres JSON Hello contient une liste de tooload de modules IoT Edge et liens hello entre modules de hello.</span><span class="sxs-lookup"><span data-stu-id="e14d9-114">hello JSON settings file contains a list of IoT Edge modules tooload and hello links between hello modules.</span></span> <span data-ttu-id="e14d9-115">Chaque module IoT Edge doit spécifier les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="e14d9-115">Each IoT Edge module must specify a:</span></span>

* <span data-ttu-id="e14d9-116">**nom**: un nom unique pour le module de hello.</span><span class="sxs-lookup"><span data-stu-id="e14d9-116">**name**: a unique name for hello module.</span></span>
* <span data-ttu-id="e14d9-117">**chargeur**: un chargeur qui sait comment hello de tooload souhaité module.</span><span class="sxs-lookup"><span data-stu-id="e14d9-117">**loader**: a loader that knows how tooload hello desired module.</span></span> <span data-ttu-id="e14d9-118">Les chargeurs correspondent à un point d’extension pour le chargement des différents types de modules.</span><span class="sxs-lookup"><span data-stu-id="e14d9-118">Loaders are an extension point for loading different types of modules.</span></span> <span data-ttu-id="e14d9-119">IoT Edge fournit des chargeurs compatibles avec des modules écrits nativement en C, en Node.js, en Java et en .NET.</span><span class="sxs-lookup"><span data-stu-id="e14d9-119">IoT Edge provides loaders for use with modules written in native C, Node.js, Java, and .NET.</span></span> <span data-ttu-id="e14d9-120">Hello, exemple Hello World utilise uniquement le chargeur de C natif hello, car tous les modules de hello dans cet exemple sont des bibliothèques dynamiques écrites en C. Pour plus d’informations sur les modules de IoT bord toouse écrits dans différents langages, consultez hello [Node.js](https://github.com/Azure/iot-edge/blob/master/samples/nodejs_simple_sample/), [Java](https://github.com/Azure/iot-edge/tree/master/samples/java_sample), ou [.NET](https://github.com/Azure/iot-edge/tree/master/samples/dotnet_binding_sample) exemples.</span><span class="sxs-lookup"><span data-stu-id="e14d9-120">hello Hello World sample only uses hello native C loader because all hello modules in this sample are dynamic libraries written in C. For more information about how toouse IoT Edge modules written in different languages, see hello [Node.js](https://github.com/Azure/iot-edge/blob/master/samples/nodejs_simple_sample/), [Java](https://github.com/Azure/iot-edge/tree/master/samples/java_sample), or [.NET](https://github.com/Azure/iot-edge/tree/master/samples/dotnet_binding_sample) samples.</span></span>
    * <span data-ttu-id="e14d9-121">**nom**: nom hello du chargeur de hello utilisé le module de hello tooload.</span><span class="sxs-lookup"><span data-stu-id="e14d9-121">**name**: hello name of hello loader used tooload hello module.</span></span>
    * <span data-ttu-id="e14d9-122">**point d’entrée**: bibliothèque de toohello hello chemin d’accès contenant le module de hello.</span><span class="sxs-lookup"><span data-stu-id="e14d9-122">**entrypoint**: hello path toohello library containing hello module.</span></span> <span data-ttu-id="e14d9-123">Il s’agit d’un fichier .so sous Linux, et d’un fichier .dll sous Windows.</span><span class="sxs-lookup"><span data-stu-id="e14d9-123">On Linux this library is a .so file, on Windows this library is a .dll file.</span></span> <span data-ttu-id="e14d9-124">point d’entrée Hello est de type toohello spécifique du chargeur utilisé.</span><span class="sxs-lookup"><span data-stu-id="e14d9-124">hello entry point is specific toohello type of loader being used.</span></span> <span data-ttu-id="e14d9-125">Hello point d’entrée du chargeur Node.js est un fichier .js.</span><span class="sxs-lookup"><span data-stu-id="e14d9-125">hello Node.js loader entry point is a .js file.</span></span> <span data-ttu-id="e14d9-126">Hello point d’entrée du chargeur Java est un chemin de classe et un nom de classe.</span><span class="sxs-lookup"><span data-stu-id="e14d9-126">hello Java loader entry point is a classpath and a class name.</span></span> <span data-ttu-id="e14d9-127">Hello point d’entrée du chargeur .NET est un nom d’assembly et un nom de classe.</span><span class="sxs-lookup"><span data-stu-id="e14d9-127">hello .NET loader entry point is an assembly name and a class name.</span></span>

* <span data-ttu-id="e14d9-128">**args**: a besoin de n’importe quel module de hello d’informations de configuration.</span><span class="sxs-lookup"><span data-stu-id="e14d9-128">**args**: any configuration information hello module needs.</span></span>

<span data-ttu-id="e14d9-129">Hello suivant de code montre hello JSON utilisé toodeclare tous les hello modules IoT Edge pour hello, exemple Hello World sur Linux.</span><span class="sxs-lookup"><span data-stu-id="e14d9-129">hello following code shows hello JSON used toodeclare all hello IoT Edge modules for hello Hello World sample on Linux.</span></span> <span data-ttu-id="e14d9-130">Si un module requiert des arguments dépend de la conception hello du module de hello.</span><span class="sxs-lookup"><span data-stu-id="e14d9-130">Whether a module requires any arguments depends on hello design of hello module.</span></span> <span data-ttu-id="e14d9-131">Dans cet exemple, le module de journalisation hello prend un argument qui est le fichier de sortie toohello hello chemin d’accès et Bonjour Bonjour\_module du monde dispose d’aucun argument.</span><span class="sxs-lookup"><span data-stu-id="e14d9-131">In this example, hello logger module takes an argument that is hello path toohello output file and hello hello\_world module has no arguments.</span></span>

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

<span data-ttu-id="e14d9-132">fichier JSON de Hello contient également des liens hello entre modules hello passés toohello broker.</span><span class="sxs-lookup"><span data-stu-id="e14d9-132">hello JSON file also contains hello links between hello modules that are passed toohello broker.</span></span> <span data-ttu-id="e14d9-133">Une liaison possède deux propriétés :</span><span class="sxs-lookup"><span data-stu-id="e14d9-133">A link has two properties:</span></span>

* <span data-ttu-id="e14d9-134">**source**: un nom de module à partir de hello `modules` section, ou `\*`.</span><span class="sxs-lookup"><span data-stu-id="e14d9-134">**source**: a module name from hello `modules` section, or `\*`.</span></span>
* <span data-ttu-id="e14d9-135">**récepteur**: un nom de module à partir de hello `modules` section.</span><span class="sxs-lookup"><span data-stu-id="e14d9-135">**sink**: a module name from hello `modules` section.</span></span>

<span data-ttu-id="e14d9-136">Chaque liaison définit un itinéraire de message et une direction.</span><span class="sxs-lookup"><span data-stu-id="e14d9-136">Each link defines a message route and direction.</span></span> <span data-ttu-id="e14d9-137">Messages de hello **source** module sont remis toohello **récepteur** module.</span><span class="sxs-lookup"><span data-stu-id="e14d9-137">Messages from hello **source** module are delivered toohello **sink** module.</span></span> <span data-ttu-id="e14d9-138">Vous pouvez définir hello **source** module trop`\*`, ce qui signifie que hello **récepteur** module reçoit des messages à partir de n’importe quel module.</span><span class="sxs-lookup"><span data-stu-id="e14d9-138">You can set hello **source** module too`\*`, which indicates that hello **sink** module receives messages from any module.</span></span>

<span data-ttu-id="e14d9-139">Hello de code suivant montre hello JSON utilisé tooconfigure les liens entre les modules hello utilisés dans Bonjour Bonjour\_world (exemple) sur Linux.</span><span class="sxs-lookup"><span data-stu-id="e14d9-139">hello following code shows hello JSON used tooconfigure links between hello modules used in hello hello\_world sample on Linux.</span></span> <span data-ttu-id="e14d9-140">Tous les messages produits par hello `hello_world` module est consommé par hello `logger` module.</span><span class="sxs-lookup"><span data-stu-id="e14d9-140">Every message produced by hello `hello_world` module is consumed by hello `logger` module.</span></span>

```json
"links":
[
    {
        "source": "hello_world",
        "sink": "logger"
    }
]
```

### <a name="helloworld-module-message-publishing"></a><span data-ttu-id="e14d9-141">Publication des messages du module hello\_world</span><span class="sxs-lookup"><span data-stu-id="e14d9-141">Hello\_world module message publishing</span></span>

<span data-ttu-id="e14d9-142">Vous pouvez trouver le code hello utilisé par Bonjour Bonjour\_messages toopublish du module du monde Bonjour ['hello_world.c'] [ lnk-helloworld-c] fichier.</span><span class="sxs-lookup"><span data-stu-id="e14d9-142">You can find hello code used by hello hello\_world module toopublish messages in hello ['hello_world.c'][lnk-helloworld-c] file.</span></span> <span data-ttu-id="e14d9-143">Hello extrait de code suivant montre une version modifiée du code de hello avec commentaires ajoutés et une erreur de la gestion du code supprimé pour une meilleure lisibilité :</span><span class="sxs-lookup"><span data-stu-id="e14d9-143">hello following snippet shows an amended version of hello code with comments added and some error handling code removed for legibility:</span></span>

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

### <a name="helloworld-module-message-processing"></a><span data-ttu-id="e14d9-144">Traitement des messages du module hello\_world</span><span class="sxs-lookup"><span data-stu-id="e14d9-144">Hello\_world module message processing</span></span>

<span data-ttu-id="e14d9-145">Bonjour Bonjour\_module du monde jamais traite les messages que les autres modules IoT bord publient toohello broker.</span><span class="sxs-lookup"><span data-stu-id="e14d9-145">hello hello\_world module never processes messages that other IoT Edge modules publish toohello broker.</span></span> <span data-ttu-id="e14d9-146">Par conséquent, hello implémentation du rappel de message hello dans Bonjour Bonjour\_world du module est une fonction de l’absence d’opération.</span><span class="sxs-lookup"><span data-stu-id="e14d9-146">Therefore, hello implementation of hello message callback in hello hello\_world module is a no-op function.</span></span>

```c
static void HelloWorld_Receive(MODULE_HANDLE moduleHandle, MESSAGE_HANDLE messageHandle)
{
    /* No action, HelloWorld is not interested in any messages. */
}
```

### <a name="logger-module-message-publishing-and-processing"></a><span data-ttu-id="e14d9-147">Publication et traitement des messages du module enregistreur</span><span class="sxs-lookup"><span data-stu-id="e14d9-147">Logger module message publishing and processing</span></span>

<span data-ttu-id="e14d9-148">module d’enregistreur d’événements Hello reçoit des messages du service Broker pour hello et les écrit tooa fichier.</span><span class="sxs-lookup"><span data-stu-id="e14d9-148">hello logger module receives messages from hello broker and writes them tooa file.</span></span> <span data-ttu-id="e14d9-149">Il ne publie jamais les messages.</span><span class="sxs-lookup"><span data-stu-id="e14d9-149">It never publishes any messages.</span></span> <span data-ttu-id="e14d9-150">Par conséquent, code hello du module du journal hello appelle jamais hello **Broker_Publish** (fonction).</span><span class="sxs-lookup"><span data-stu-id="e14d9-150">Therefore, hello code of hello logger module never calls hello **Broker_Publish** function.</span></span>

<span data-ttu-id="e14d9-151">Hello **Logger_Receive** fonction Bonjour [logger.c] [ lnk-logger-c] fichier est le service broker de hello hello rappel appelle le module de journalisation toohello toodeliver messages.</span><span class="sxs-lookup"><span data-stu-id="e14d9-151">hello **Logger_Receive** function in hello [logger.c][lnk-logger-c] file is hello callback hello broker invokes toodeliver messages toohello logger module.</span></span> <span data-ttu-id="e14d9-152">Hello extrait de code suivant montre une version modifiée avec commentaires ajoutés et une erreur de la gestion du code supprimé pour une meilleure lisibilité :</span><span class="sxs-lookup"><span data-stu-id="e14d9-152">hello following snippet shows an amended version with comments added and some error handling code removed for legibility:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="e14d9-153">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e14d9-153">Next steps</span></span>

<span data-ttu-id="e14d9-154">Dans cet article, vous avez exécuté une passerelle IoT bord simple qui écrit le fichier journal des messages tooa.</span><span class="sxs-lookup"><span data-stu-id="e14d9-154">In this article, you ran a simple IoT Edge gateway that writes messages tooa log file.</span></span> <span data-ttu-id="e14d9-155">toorun un exemple qui envoie des messages tooIoT Hub, consultez [IoT Edge – envoyer des messages de l’appareil-à-cloud avec un appareil simulé à l’aide de Linux] [ lnk-gateway-simulated-linux] ou [IoT Edge – envoyer les messages appareil-à-cloud avec un APPAREIL simulé à l’aide de Windows][lnk-gateway-simulated-windows].</span><span class="sxs-lookup"><span data-stu-id="e14d9-155">toorun a sample that sends messages tooIoT Hub, see [IoT Edge – send device-to-cloud messages with a simulated device using Linux][lnk-gateway-simulated-linux] or [IoT Edge – send device-to-cloud messages with a simulated device using Windows][lnk-gateway-simulated-windows].</span></span>


<!-- Links -->
[lnk-main-c]: https://github.com/Azure/iot-edge/blob/master/samples/hello_world/src/main.c
[lnk-helloworld-c]: https://github.com/Azure/iot-edge/blob/master/modules/hello_world/src/hello_world.c
[lnk-logger-c]: https://github.com/Azure/iot-edge/blob/master/modules/logger/src/logger.c
[lnk-iot-edge]: https://github.com/Azure/iot-edge/
[lnk-gateway-simulated-linux]: ../articles/iot-hub/iot-hub-linux-iot-edge-simulated-device.md
[lnk-gateway-simulated-windows]: ../articles/iot-hub/iot-hub-windows-iot-edge-simulated-device.md