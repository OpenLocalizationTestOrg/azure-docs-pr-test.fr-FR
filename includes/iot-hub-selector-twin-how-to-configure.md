> [!div class="op_single_selector"]
> * [<span data-ttu-id="099c0-101">Node.JS</span><span class="sxs-lookup"><span data-stu-id="099c0-101">Node.js</span></span>](../articles/iot-hub/iot-hub-node-node-twin-how-to-configure.md)
> * [<span data-ttu-id="099c0-102">C#/Node.js</span><span class="sxs-lookup"><span data-stu-id="099c0-102">C#/Node.js</span></span>](../articles/iot-hub/iot-hub-csharp-node-twin-how-to-configure.md)
> * [<span data-ttu-id="099c0-103">C#</span><span class="sxs-lookup"><span data-stu-id="099c0-103">C#</span></span>](../articles/iot-hub/iot-hub-csharp-csharp-twin-how-to-configure.md)
> 
> 

## <a name="introduction"></a><span data-ttu-id="099c0-104">Introduction</span><span class="sxs-lookup"><span data-stu-id="099c0-104">Introduction</span></span>

<span data-ttu-id="099c0-105">Dans [prise en main jumeaux des appareils IoT Hub][lnk-twin-tutorial], vous avez appris comment tooset les métadonnées de périphérique à partir de votre solution précédent mettre fin à l’aide de *balises*, signaler l’appareil à partir d’une application de périphérique à l’aide de *signalé propriétés*et ces informations à l’aide d’un langage de type SQL de la requête.</span><span class="sxs-lookup"><span data-stu-id="099c0-105">In [Get started with IoT Hub device twins][lnk-twin-tutorial], you learned how tooset device metadata from your solution back end using *tags*, report device conditions from a device app using *reported properties*, and query this information using a SQL-like language.</span></span>

<span data-ttu-id="099c0-106">Dans ce didacticiel, vous allez apprendre comment toouse hello du double hello appareil *propriétés souhaitée* avec *signalé propriétés*, tooremotely configurer des applications de périphérique.</span><span class="sxs-lookup"><span data-stu-id="099c0-106">In this tutorial, you will learn how toouse hello hello device twin's *desired properties* along with *reported properties*, tooremotely configure device apps.</span></span> <span data-ttu-id="099c0-107">Plus spécifiquement, ce didacticiel montre comment un double de périphérique signalé et propriétés souhaitées activer une configuration à plusieurs étapes d’une application de périphérique et fournissent des hello visibilité toohello solution back end d’état hello de cette opération sur tous les périphériques.</span><span class="sxs-lookup"><span data-stu-id="099c0-107">More specifically, this tutorial shows how a device twin's reported and desired properties enable a multi-step configuration of a device application, and provide hello visibility toohello solution back end of hello status of this operation across all devices.</span></span> <span data-ttu-id="099c0-108">Vous trouverez plus d’informations sur le rôle de hello de configurations du périphérique dans [vue d’ensemble de gestion des appareils avec IoT Hub][lnk-dm-overview].</span><span class="sxs-lookup"><span data-stu-id="099c0-108">You can find more information regarding hello role of device configurations in [Overview of device management with IoT Hub][lnk-dm-overview].</span></span>

<span data-ttu-id="099c0-109">À un niveau élevé, jumeaux de périphérique grâce à hello solution back-end toospecify hello configuration souhaitée pour les appareils hello géré, au lieu d’envoyer des commandes spécifiques.</span><span class="sxs-lookup"><span data-stu-id="099c0-109">At a high level, using device twins enables hello solution back end toospecify hello desired configuration for hello managed devices, instead of sending specific commands.</span></span> <span data-ttu-id="099c0-110">Cela met l’appareil hello responsable de la configuration hello meilleure manière tooupdate sa configuration (très important dans les scénarios IoT où les conditions de périphérique spécifique affectent hello capacité tooimmediately exécuter des commandes spécifiques), tout en permanence reporting toohello solution de retour de fin état actuel de hello et conditions d’erreur potentielle du processus de mise à jour hello.</span><span class="sxs-lookup"><span data-stu-id="099c0-110">This puts hello device in charge of setting up hello best way tooupdate its configuration (very important in IoT scenarios where specific device conditions affect hello ability tooimmediately carry out specific commands), while continually reporting toohello solution back end hello current state and potential error conditions of hello update process.</span></span> <span data-ttu-id="099c0-111">Ce modèle est gestion toohello instrumentale de grands ensembles de périphériques, car elle permet des hello solution back-end toohave une visibilité complète de l’état de hello hello du processus de configuration sur tous les périphériques.</span><span class="sxs-lookup"><span data-stu-id="099c0-111">This pattern is instrumental toohello management of large sets of devices, as it enables hello solution back end toohave full visibility of hello state of hello configuration process across all devices.</span></span>

> [!NOTE]
> <span data-ttu-id="099c0-112">Pour les scénarios impliquant un contrôle plus interactif des appareils (mise en marche d’un ventilateur à partir d’une application contrôlée par l’utilisateur), envisagez d’utiliser des [méthodes directes][lnk-methods].</span><span class="sxs-lookup"><span data-stu-id="099c0-112">In scenarios where devices are controlled in a more interactive fashion (turn on a fan from a user-controlled app), consider using [direct methods][lnk-methods].</span></span>
> 
> 

<span data-ttu-id="099c0-113">Dans ce didacticiel, modifications de back-end de solution hello hello télémétrie configuration d’un appareil cible, à la suite qui, application d’appareil hello suit un processus comportant plusieurs étapes de tooapply une configuration de mise à jour (par exemple, nécessitant un redémarrage de module logiciel, dans lequel ce didacticiel simule avec un simple délai).</span><span class="sxs-lookup"><span data-stu-id="099c0-113">In this tutorial, hello solution back end changes hello telemetry configuration of a target device and, as a result of that, hello device app follows a multi-step process tooapply a configuration update (for example, requiring a software module restart, which this tutorial simulates with a simple delay).</span></span>

<span data-ttu-id="099c0-114">Hello solution back-end stocke la configuration de hello dans les propriétés du double hello appareil Bonjour de configuration suivant :</span><span class="sxs-lookup"><span data-stu-id="099c0-114">hello solution back end stores hello configuration in hello device twin's desired properties in hello following way:</span></span>

        {
            ...
            "properties": {
                ...
                "desired": {
                    "telemetryConfig": {
                        "configId": "{id of hello configuration}",
                        "sendFrequency": "{config}"
                    }
                }
                ...
            }
            ...
        }

> [!NOTE]
> <span data-ttu-id="099c0-115">Étant donné que les configurations peuvent être des objets complexes, elles sont généralement affectés des ID uniques (hachages ou [GUID][lnk-guid]) toosimplify leurs comparaisons.</span><span class="sxs-lookup"><span data-stu-id="099c0-115">Since configurations can be complex objects, they are usually assigned unique ids (hashes or [GUIDs][lnk-guid]) toosimplify their comparisons.</span></span>
> 
> 

<span data-ttu-id="099c0-116">application Hello signale sa configuration actuelle, mise en miroir de la propriété de hello souhaité **telemetryConfig** Bonjour signalé propriétés :</span><span class="sxs-lookup"><span data-stu-id="099c0-116">hello device app reports its current configuration mirroring hello desired property **telemetryConfig** in hello reported properties:</span></span>

        {
            "properties": {
                ...
                "reported": {
                    "telemetryConfig": {
                        "changeId": "{id of hello current configuration}",
                        "sendFrequency": "{current configuration}",
                        "status": "Success",
                    }
                }
                ...
            }
        }

<span data-ttu-id="099c0-117">Notez comment hello **telemetryConfig** a une propriété supplémentaire **état**, utilisé l’état de hello tooreport hello mise à jour du processus de configuration.</span><span class="sxs-lookup"><span data-stu-id="099c0-117">Note how hello reported **telemetryConfig** has an additional property **status**, used tooreport hello state of hello configuration update process.</span></span>

<span data-ttu-id="099c0-118">Lorsqu’une nouvelle configuration souhaitée est reçue, application hello signale une configuration en attente en modifiant les informations de hello :</span><span class="sxs-lookup"><span data-stu-id="099c0-118">When a new desired configuration is received, hello device app reports a pending configuration by changing hello information:</span></span>

        {
            "properties": {
                ...
                "reported": {
                    "telemetryConfig": {
                        "changeId": "{id of hello current configuration}",
                        "sendFrequency": "{current configuration}",
                        "status": "Pending",
                        "pendingConfig": {
                            "changeId": "{id of hello pending configuration}",
                            "sendFrequency": "{pending configuration}"
                        }
                    }
                }
                ...
            }
        }

<span data-ttu-id="099c0-119">Ensuite, à un moment ultérieur, application d’appareil hello signalera réussite de hello ou l’échec de cette opération en mettant à jour hello au-dessus de propriété.</span><span class="sxs-lookup"><span data-stu-id="099c0-119">Then, at some later time, hello device app will report hello success or failure of this operation by updating hello above property.</span></span>
<span data-ttu-id="099c0-120">Notez comment hello solution back-end est capable, à tout moment, l’état de hello tooquery hello du processus de configuration sur tous les périphériques hello.</span><span class="sxs-lookup"><span data-stu-id="099c0-120">Note how hello solution back end is able, at any time, tooquery hello status of hello configuration process across all hello devices.</span></span>

<span data-ttu-id="099c0-121">Ce didacticiel vous explique les procédures suivantes :</span><span class="sxs-lookup"><span data-stu-id="099c0-121">This tutorial shows you how to:</span></span>

* <span data-ttu-id="099c0-122">Créer une application d’appareil simulé qui reçoit des mises à jour de la configuration de hello solution back-end et des rapports de plusieurs mises à jour en tant que *signalé propriétés* sur la configuration de hello des mises à jour.</span><span class="sxs-lookup"><span data-stu-id="099c0-122">Create a simulated device app that receives configuration updates from hello solution back end, and reports multiple updates as *reported properties* on hello configuration update process.</span></span>
* <span data-ttu-id="099c0-123">Créer une application back-end que les mises à jour hello souhaitée de configuration d’un périphérique, et puis requêtes hello le processus de mise à jour de configuration.</span><span class="sxs-lookup"><span data-stu-id="099c0-123">Create a back-end app that updates hello desired configuration of a device, and then queries hello configuration update process.</span></span>

<!-- links -->

[lnk-methods]: ../articles/iot-hub/iot-hub-devguide-direct-methods.md
[lnk-dm-overview]: ../articles/iot-hub/iot-hub-device-management-overview.md
[lnk-twin-tutorial]: ../articles/iot-hub/iot-hub-node-node-twin-getstarted.md
[lnk-guid]: https://en.wikipedia.org/wiki/Globally_unique_identifier
