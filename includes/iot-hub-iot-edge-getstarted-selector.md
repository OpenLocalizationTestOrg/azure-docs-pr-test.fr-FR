> [!div class="op_single_selector"]
> * [<span data-ttu-id="6df0d-101">Linux</span><span class="sxs-lookup"><span data-stu-id="6df0d-101">Linux</span></span>](../articles/iot-hub/iot-hub-linux-iot-edge-get-started.md)
> * [<span data-ttu-id="6df0d-102">Windows</span><span class="sxs-lookup"><span data-stu-id="6df0d-102">Windows</span></span>](../articles/iot-hub/iot-hub-windows-iot-edge-get-started.md)
> 
> 

<span data-ttu-id="6df0d-103">Cet article fournit une description détaillée de hello [exemple de code Hello World] [ lnk-helloworld-sample] composants fondamentaux de hello tooillustrate Hello [Azure IoT bord] [ lnk-iot-edge] architecture.</span><span class="sxs-lookup"><span data-stu-id="6df0d-103">This article provides a detailed walkthrough of hello [Hello World sample code][lnk-helloworld-sample] tooillustrate hello fundamental components of hello [Azure IoT Edge][lnk-iot-edge] architecture.</span></span> <span data-ttu-id="6df0d-104">Hello utilise hello Azure IoT bord toobuild une passerelle simple qui se connecte à un fichier de tooa de message « hello world » toutes les cinq secondes.</span><span class="sxs-lookup"><span data-stu-id="6df0d-104">hello sample uses hello Azure IoT Edge toobuild a simple gateway that logs a "hello world" message tooa file every five seconds.</span></span>

<span data-ttu-id="6df0d-105">Cette procédure pas à pas inclut les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="6df0d-105">This walkthrough covers:</span></span>

* <span data-ttu-id="6df0d-106">**Hello exemple d’architecture World**: décrit comment [concepts d’architecture Azure IoT bord] [ lnk-edge-concepts] appliquer l’exemple Hello World de toohello et comment les composants de hello ensemble.</span><span class="sxs-lookup"><span data-stu-id="6df0d-106">**Hello World sample architecture**: Describes how [Azure IoT Edge architectural concepts][lnk-edge-concepts] apply toohello Hello World sample and how hello components fit together.</span></span>
* <span data-ttu-id="6df0d-107">**Comment toobuild hello exemple**: hello, exemple hello étapes toobuild requis.</span><span class="sxs-lookup"><span data-stu-id="6df0d-107">**How toobuild hello sample**: hello steps required toobuild hello sample.</span></span>
* <span data-ttu-id="6df0d-108">**Comment toorun hello exemple**: hello, exemple hello étapes toorun requis.</span><span class="sxs-lookup"><span data-stu-id="6df0d-108">**How toorun hello sample**: hello steps required toorun hello sample.</span></span> 
* <span data-ttu-id="6df0d-109">**Exemple de résultat**: un exemple Hello tooexpect de sortie lorsque vous exécutez l’exemple hello.</span><span class="sxs-lookup"><span data-stu-id="6df0d-109">**Typical output**: An example of hello output tooexpect when you run hello sample.</span></span>
* <span data-ttu-id="6df0d-110">**Extraits de code**: une collection de tooshow d’extraits de code comment hello Hello World (exemple) implémente les composants de passerelle de IoT bord clés.</span><span class="sxs-lookup"><span data-stu-id="6df0d-110">**Code snippets**: A collection of code snippets tooshow how hello Hello World sample implements key IoT Edge gateway components.</span></span>


## <a name="hello-world-sample-architecture"></a><span data-ttu-id="6df0d-111">Exemple d'architecture Hello World</span><span class="sxs-lookup"><span data-stu-id="6df0d-111">Hello World sample architecture</span></span>
<span data-ttu-id="6df0d-112">exemple Hello Hello World illustre les concepts de hello décrites dans la section précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="6df0d-112">hello Hello World sample illustrates hello concepts described in hello previous section.</span></span> <span data-ttu-id="6df0d-113">exemple Hello Hello World implémente une passerelle IoT dispose d’un pipeline composé de deux modules de IoT bord :</span><span class="sxs-lookup"><span data-stu-id="6df0d-113">hello Hello World sample implements a IoT Edge gateway that has a pipeline made up of two IoT Edge modules:</span></span>

* <span data-ttu-id="6df0d-114">Hello *Bonjour* module crée un message toutes les cinq secondes et le passe module du journal toohello.</span><span class="sxs-lookup"><span data-stu-id="6df0d-114">hello *hello world* module creates a message every five seconds and passes it toohello logger module.</span></span>
* <span data-ttu-id="6df0d-115">Hello *journal* module écrit les messages hello réception tooa fichier.</span><span class="sxs-lookup"><span data-stu-id="6df0d-115">hello *logger* module writes hello messages it receives tooa file.</span></span>

![Architecture de l’exemple Hello World conçu avec Azure IoT Edge][4]

<span data-ttu-id="6df0d-117">Comme décrit dans la section précédente de hello, hello World Hello module ne passe pas directement toohello journal module messages toutes les cinq secondes.</span><span class="sxs-lookup"><span data-stu-id="6df0d-117">As described in hello previous section, hello Hello World module does not pass messages directly toohello logger module every five seconds.</span></span> <span data-ttu-id="6df0d-118">Au lieu de cela, elle publie le message broker toohello toutes les cinq secondes.</span><span class="sxs-lookup"><span data-stu-id="6df0d-118">Instead, it publishes a message toohello broker every five seconds.</span></span>

<span data-ttu-id="6df0d-119">module d’enregistreur d’événements Hello reçoit un message de type hello à partir du service broker de hello et agit sur, écriture du contenu hello du fichier de tooa message hello.</span><span class="sxs-lookup"><span data-stu-id="6df0d-119">hello logger module receives hello message from hello broker and acts upon it, writing hello contents of hello message tooa file.</span></span>

<span data-ttu-id="6df0d-120">module d’enregistreur d’événements Hello utilise uniquement les messages de service broker de hello, il publie jamais service Broker pour les nouveaux messages toohello.</span><span class="sxs-lookup"><span data-stu-id="6df0d-120">hello logger module only consumes messages from hello broker, it never publishes new messages toohello broker.</span></span>

![Comment hello broker route les messages entre les modules dans Azure IoT Edge][5]

<span data-ttu-id="6df0d-122">Hello figure ci-dessus illustre hello architecture de hello Hello World (exemple) et les chemins d’accès relatifs hello fichiers toohello sources qui implémentent différentes parties de l’exemple hello Bonjour [référentiel][lnk-iot-edge].</span><span class="sxs-lookup"><span data-stu-id="6df0d-122">hello figure above shows hello architecture of hello Hello World sample and hello relative paths toohello source files that implement different portions of hello sample in hello [repository][lnk-iot-edge].</span></span> <span data-ttu-id="6df0d-123">Explorer le code de hello vous-même, ou utiliser des extraits de code hello ci-dessous comme guide.</span><span class="sxs-lookup"><span data-stu-id="6df0d-123">Explore hello code on your own, or use hello code snippets below as a guide.</span></span>

<!-- Images -->
[4]: media/iot-hub-iot-edge-getstarted-selector/high_level_architecture.png
[5]: media/iot-hub-iot-edge-getstarted-selector/detailed_architecture.png

<!-- Links -->
[lnk-helloworld-sample]: https://github.com/Azure/iot-edge/tree/master/samples/hello_world
[lnk-iot-edge]: https://github.com/Azure/iot-edge
[lnk-edge-concepts]: ../articles/iot-hub/iot-hub-iot-edge-overview.md