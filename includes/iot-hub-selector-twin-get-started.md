> [!div class="op_single_selector"]
> * [<span data-ttu-id="5b02c-101">Node.JS</span><span class="sxs-lookup"><span data-stu-id="5b02c-101">Node.js</span></span>](../articles/iot-hub/iot-hub-node-node-twin-getstarted.md)
> * [<span data-ttu-id="5b02c-102">C#/Node.js</span><span class="sxs-lookup"><span data-stu-id="5b02c-102">C#/Node.js</span></span>](../articles/iot-hub/iot-hub-csharp-node-twin-getstarted.md)
> * [<span data-ttu-id="5b02c-103">C#</span><span class="sxs-lookup"><span data-stu-id="5b02c-103">C#</span></span>](../articles/iot-hub/iot-hub-csharp-csharp-twin-getstarted.md)
> * [<span data-ttu-id="5b02c-104">Java</span><span class="sxs-lookup"><span data-stu-id="5b02c-104">Java</span></span>](../articles/iot-hub/iot-hub-java-java-twin-getstarted.md)

<span data-ttu-id="5b02c-105">Les représentations d’appareil sont des documents JSON qui stockent des informations sur l’état des appareils (métadonnées, configurations et conditions).</span><span class="sxs-lookup"><span data-stu-id="5b02c-105">Device twins are JSON documents that store device state information (metadata, configurations, and conditions).</span></span> <span data-ttu-id="5b02c-106">IoT Hub conserve un double du périphérique pour chaque périphérique qui se connecte tooit.</span><span class="sxs-lookup"><span data-stu-id="5b02c-106">IoT Hub persists a device twin for each device that connects tooit.</span></span>

<span data-ttu-id="5b02c-107">Vous pouvez utiliser des représentations d’appareil pour répondre aux besoins suivants :</span><span class="sxs-lookup"><span data-stu-id="5b02c-107">Use device twins to:</span></span>

* <span data-ttu-id="5b02c-108">Stockez les métadonnées d’appareil à partir de votre serveur principal de solution.</span><span class="sxs-lookup"><span data-stu-id="5b02c-108">Store device metadata from your solution back end.</span></span>
* <span data-ttu-id="5b02c-109">Rapports des informations d’état actuelles tels que conditions (par exemple, les méthode de connectivité de hello sont utilisée) et les fonctionnalités disponibles à partir de votre application.</span><span class="sxs-lookup"><span data-stu-id="5b02c-109">Report current state information such as available capabilities and conditions (for example, hello connectivity method used) from your device app.</span></span>
* <span data-ttu-id="5b02c-110">Synchroniser l’état hello de flux de travail longue (par exemple, les mises à jour de microprogramme et configuration) entre une application de périphérique et une application back-end.</span><span class="sxs-lookup"><span data-stu-id="5b02c-110">Synchronize hello state of long-running workflows (such as firmware and configuration updates) between a device app and a back-end app.</span></span>
* <span data-ttu-id="5b02c-111">Interroger les métadonnées, la configuration ou l’état de vos appareils</span><span class="sxs-lookup"><span data-stu-id="5b02c-111">Query your device metadata, configuration, or state.</span></span>

> [!NOTE]
> <span data-ttu-id="5b02c-112">Les représentations d’appareil sont conçues pour les synchronisations et pour l’interrogation des configurations et des conditions d’appareil.</span><span class="sxs-lookup"><span data-stu-id="5b02c-112">Device twins are designed for synchronization and for querying device configurations and conditions.</span></span> <span data-ttu-id="5b02c-113">Plus d’informations sur quand jumeaux de périphérique toouse se trouvent dans [comprendre jumeaux de périphérique][lnk-twins].</span><span class="sxs-lookup"><span data-stu-id="5b02c-113">More informations on when toouse device twins can be found in [Understand device twins][lnk-twins].</span></span>

<span data-ttu-id="5b02c-114">Les représentations d’appareil sont stockées dans un IoT Hub et contiennent les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="5b02c-114">Device twins are stored in an IoT hub and contain:</span></span>

* <span data-ttu-id="5b02c-115">*balises*, les métadonnées de périphérique uniquement accessible hello solution back-end ;</span><span class="sxs-lookup"><span data-stu-id="5b02c-115">*tags*, device metadata accessible only by hello solution back end;</span></span>
* <span data-ttu-id="5b02c-116">*propriétés souhaitée*, objets JSON modifiables par les solutions hello back-end et observable par application d’appareil hello ; et</span><span class="sxs-lookup"><span data-stu-id="5b02c-116">*desired properties*, JSON objects modifiable by hello solution back end and observable by hello device app; and</span></span>
* <span data-ttu-id="5b02c-117">*signalé propriétés*, les objets JSON modifiables par l’application d’appareil hello et lisibles par hello solution back-end.</span><span class="sxs-lookup"><span data-stu-id="5b02c-117">*reported properties*, JSON objects modifiable by hello device app and readable by hello solution back end.</span></span> <span data-ttu-id="5b02c-118">Les étiquettes et les propriétés ne peuvent pas contenir de tableaux, mais les objets peuvent être imbriqués.</span><span class="sxs-lookup"><span data-stu-id="5b02c-118">Tags and properties cannot contain arrays, but objects can be nested.</span></span>

![][img-twin]

<span data-ttu-id="5b02c-119">En outre, hello solution back-end peut interroger jumeaux appareil selon hello toutes les données.</span><span class="sxs-lookup"><span data-stu-id="5b02c-119">Additionally, hello solution back end can query device twins based on all hello above data.</span></span>
<span data-ttu-id="5b02c-120">Consultez trop[comprendre jumeaux de périphérique] [ lnk-twins] pour plus d’informations sur jumeaux de périphérique et toohello [langage de requête IoT Hub] [ lnk-query] référence pour l’interrogation.</span><span class="sxs-lookup"><span data-stu-id="5b02c-120">Refer too[Understand device twins][lnk-twins] for more information about device twins, and toohello [IoT Hub query language][lnk-query] reference for querying.</span></span>

> [!NOTE]
> <span data-ttu-id="5b02c-121">À ce stade, jumeaux de périphérique est accessibles uniquement à partir d’appareils qui se connectent tooIoT concentrateur à l’aide du protocole MQTT hello.</span><span class="sxs-lookup"><span data-stu-id="5b02c-121">At this time, device twins are accessible only from devices that connect tooIoT Hub using hello MQTT protocol.</span></span> <span data-ttu-id="5b02c-122">Reportez-vous toohello [prise en charge MQTT] [ lnk-devguide-mqtt] article pour obtenir des instructions sur la façon de tooconvert existant appareil application toouse MQTT.</span><span class="sxs-lookup"><span data-stu-id="5b02c-122">Please refer toohello [MQTT support][lnk-devguide-mqtt] article for instructions on how tooconvert existing device app toouse MQTT.</span></span>

<span data-ttu-id="5b02c-123">Ce didacticiel vous explique les procédures suivantes :</span><span class="sxs-lookup"><span data-stu-id="5b02c-123">This tutorial shows you how to:</span></span>

* <span data-ttu-id="5b02c-124">Créer une application back-end qui ajoute *balises* double de périphérique tooa et une application d’appareil simulé qui indique sa connectivité de canal en tant qu’un *signalé propriété* sur le double de périphérique hello.</span><span class="sxs-lookup"><span data-stu-id="5b02c-124">Create a back-end app that adds *tags* tooa device twin, and a simulated device app that reports its connectivity channel as a *reported property* on hello device twin.</span></span>
* <span data-ttu-id="5b02c-125">Interroger les périphériques à partir de votre application back-end à l’aide de filtres sur les balises de hello et de propriétés créées précédemment.</span><span class="sxs-lookup"><span data-stu-id="5b02c-125">Query devices from your back-end app using filters on hello tags and properties previously created.</span></span>

<!-- images -->
[img-twin]: media/iot-hub-selector-twin-get-started/twin.png

<!-- links -->
[lnk-query]: ../articles/iot-hub/iot-hub-devguide-query-language.md
[lnk-twins]: ../articles/iot-hub/iot-hub-devguide-device-twins.md
[lnk-d2c]: ../articles/iot-hub/iot-hub-devguide-messaging.md#device-to-cloud-messages
[lnk-methods]: ../articles/iot-hub/iot-hub-devguide-direct-methods.md
[lnk-devguide-mqtt]: ../articles/iot-hub/iot-hub-mqtt-support.md