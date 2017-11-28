> [!div class="op_single_selector"]
> * [<span data-ttu-id="923e3-101">Linux</span><span class="sxs-lookup"><span data-stu-id="923e3-101">Linux</span></span>](../articles/iot-hub/iot-hub-linux-iot-edge-get-started.md)
> * [<span data-ttu-id="923e3-102">Windows</span><span class="sxs-lookup"><span data-stu-id="923e3-102">Windows</span></span>](../articles/iot-hub/iot-hub-windows-iot-edge-get-started.md)
> 
> 

<span data-ttu-id="923e3-103">Cet article fournit une description détaillée de [l’exemple de code Hello World][lnk-helloworld-sample] pour illustrer les composants fondamentaux de l’architecture [Azure IoT Edge][lnk-iot-edge].</span><span class="sxs-lookup"><span data-stu-id="923e3-103">This article provides a detailed walkthrough of the [Hello World sample code][lnk-helloworld-sample] to illustrate the fundamental components of the [Azure IoT Edge][lnk-iot-edge] architecture.</span></span> <span data-ttu-id="923e3-104">L’exemple utilise Azure IoT Edge pour générer une passerelle simple qui enregistre un message « hello world » dans un fichier toutes les cinq secondes.</span><span class="sxs-lookup"><span data-stu-id="923e3-104">The sample uses the Azure IoT Edge to build a simple gateway that logs a "hello world" message to a file every five seconds.</span></span>

<span data-ttu-id="923e3-105">Cette procédure pas à pas inclut les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="923e3-105">This walkthrough covers:</span></span>

* <span data-ttu-id="923e3-106">**Architecture de l’exemple Hello World** : décrit la façon dont les [concepts architecturaux d’Azure IoT Edge][lnk-edge-concepts] s’appliquent à l’exemple Hello World, ainsi que la façon dont les composants s’imbriquent.</span><span class="sxs-lookup"><span data-stu-id="923e3-106">**Hello World sample architecture**: Describes how [Azure IoT Edge architectural concepts][lnk-edge-concepts] apply to the Hello World sample and how the components fit together.</span></span>
* <span data-ttu-id="923e3-107">**Comment créer l'exemple**: les étapes requises pour créer l'exemple.</span><span class="sxs-lookup"><span data-stu-id="923e3-107">**How to build the sample**: The steps required to build the sample.</span></span>
* <span data-ttu-id="923e3-108">**Comment exécuter l'exemple**: les étapes requises pour exécuter l'exemple.</span><span class="sxs-lookup"><span data-stu-id="923e3-108">**How to run the sample**: The steps required to run the sample.</span></span> 
* <span data-ttu-id="923e3-109">**Exemple de résultat**: un exemple du résultat attendu lorsque vous exécutez l'exemple.</span><span class="sxs-lookup"><span data-stu-id="923e3-109">**Typical output**: An example of the output to expect when you run the sample.</span></span>
* <span data-ttu-id="923e3-110">**Extraits de code** : collection d’extraits de code montrant comment l’exemple Hello World implémente les composants clés de la passerelle IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="923e3-110">**Code snippets**: A collection of code snippets to show how the Hello World sample implements key IoT Edge gateway components.</span></span>


## <a name="hello-world-sample-architecture"></a><span data-ttu-id="923e3-111">Exemple d'architecture Hello World</span><span class="sxs-lookup"><span data-stu-id="923e3-111">Hello World sample architecture</span></span>
<span data-ttu-id="923e3-112">L'exemple Hello World illustre les concepts décrits dans la section précédente.</span><span class="sxs-lookup"><span data-stu-id="923e3-112">The Hello World sample illustrates the concepts described in the previous section.</span></span> <span data-ttu-id="923e3-113">L’exemple Hello World implémente une passerelle IoT Edge avec un pipeline composé de deux modules IoT Edge :</span><span class="sxs-lookup"><span data-stu-id="923e3-113">The Hello World sample implements a IoT Edge gateway that has a pipeline made up of two IoT Edge modules:</span></span>

* <span data-ttu-id="923e3-114">Le module *Hello Wolrd* crée un message toutes les cinq secondes et le transmet au module enregistreur.</span><span class="sxs-lookup"><span data-stu-id="923e3-114">The *hello world* module creates a message every five seconds and passes it to the logger module.</span></span>
* <span data-ttu-id="923e3-115">Le module *enregistreur* inscrit les messages qu’il reçoit dans un fichier.</span><span class="sxs-lookup"><span data-stu-id="923e3-115">The *logger* module writes the messages it receives to a file.</span></span>

![Architecture de l’exemple Hello World conçu avec Azure IoT Edge][4]

<span data-ttu-id="923e3-117">Comme décrit dans la section précédente, le module Hello World ne transmet pas les messages directement vers le module enregistreur toutes les cinq secondes.</span><span class="sxs-lookup"><span data-stu-id="923e3-117">As described in the previous section, the Hello World module does not pass messages directly to the logger module every five seconds.</span></span> <span data-ttu-id="923e3-118">Au lieu de cela, il publie un message sur le répartiteur toutes les cinq secondes.</span><span class="sxs-lookup"><span data-stu-id="923e3-118">Instead, it publishes a message to the broker every five seconds.</span></span>

<span data-ttu-id="923e3-119">Le module enregistreur reçoit le message du répartiteur et intervient en écrivant le contenu du message dans un fichier.</span><span class="sxs-lookup"><span data-stu-id="923e3-119">The logger module receives the message from the broker and acts upon it, writing the contents of the message to a file.</span></span>

<span data-ttu-id="923e3-120">Le module enregistreur utilise uniquement les messages provenant du répartiteur et ne publie jamais de nouveaux messages sur le répartiteur.</span><span class="sxs-lookup"><span data-stu-id="923e3-120">The logger module only consumes messages from the broker, it never publishes new messages to the broker.</span></span>

![Comment le répartiteur achemine les messages entre les modules dans Azure IoT Edge][5]

<span data-ttu-id="923e3-122">La figure ci-dessus montre l’architecture de l’exemple Hello World et les chemins d’accès relatifs aux fichiers sources qui implémentent différentes parties de l’exemple dans le [référentiel][lnk-iot-edge].</span><span class="sxs-lookup"><span data-stu-id="923e3-122">The figure above shows the architecture of the Hello World sample and the relative paths to the source files that implement different portions of the sample in the [repository][lnk-iot-edge].</span></span> <span data-ttu-id="923e3-123">Explorez vous-même le code, ou utilisez les extraits de code ci-dessous comme guide.</span><span class="sxs-lookup"><span data-stu-id="923e3-123">Explore the code on your own, or use the code snippets below as a guide.</span></span>

<!-- Images -->
[4]: media/iot-hub-iot-edge-getstarted-selector/high_level_architecture.png
[5]: media/iot-hub-iot-edge-getstarted-selector/detailed_architecture.png

<!-- Links -->
[lnk-helloworld-sample]: https://github.com/Azure/iot-edge/tree/master/samples/hello_world
[lnk-iot-edge]: https://github.com/Azure/iot-edge
[lnk-edge-concepts]: ../articles/iot-hub/iot-hub-iot-edge-overview.md