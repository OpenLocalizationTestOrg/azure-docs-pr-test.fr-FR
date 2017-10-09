## <a name="configure-hello-nodejs-simulated-device"></a><span data-ttu-id="1f48c-101">Configurer l’appareil simulé de hello Node.js</span><span class="sxs-lookup"><span data-stu-id="1f48c-101">Configure hello Node.js simulated device</span></span>
1. <span data-ttu-id="1f48c-102">Tableau de bord de surveillance à distance hello, cliquez sur **+ ajouter un périphérique** , puis ajoutez un *périphérique personnalisé*.</span><span class="sxs-lookup"><span data-stu-id="1f48c-102">On hello remote monitoring dashboard, click **+ Add a device** and then add a *custom device*.</span></span> <span data-ttu-id="1f48c-103">Prenez note de hello IoT Hub nom d’hôte, l’id et clé de périphérique.</span><span class="sxs-lookup"><span data-stu-id="1f48c-103">Make a note of hello IoT Hub hostname, device id, and device key.</span></span> <span data-ttu-id="1f48c-104">Vous avez besoin plus loin dans ce didacticiel lorsque vous préparez l’application de client de périphérique de remote_monitoring.js hello.</span><span class="sxs-lookup"><span data-stu-id="1f48c-104">You need them later in this tutorial when you prepare hello remote_monitoring.js device client application.</span></span>
2. <span data-ttu-id="1f48c-105">Assurez-vous que Node.js version 0.12.x ou ultérieure est installé sur votre ordinateur de développement.</span><span class="sxs-lookup"><span data-stu-id="1f48c-105">Ensure that Node.js version 0.12.x or later is installed on your development machine.</span></span> <span data-ttu-id="1f48c-106">Exécutez `node --version` à une invite de commandes ou dans une version de hello toocheck shell.</span><span class="sxs-lookup"><span data-stu-id="1f48c-106">Run `node --version` at a command prompt or in a shell toocheck hello version.</span></span> <span data-ttu-id="1f48c-107">Pour plus d’informations sur l’utilisation d’un tooinstall de gestionnaire de package Node.js sur Linux, consultez [l’installation de Node.js via le Gestionnaire de package][node-linux].</span><span class="sxs-lookup"><span data-stu-id="1f48c-107">For information about using a package manager tooinstall Node.js on Linux, see [Installing Node.js via package manager][node-linux].</span></span>
3. <span data-ttu-id="1f48c-108">Lorsque vous avez installé Node.js, cloner la version la plus récente de hello hello [azure iot-sdk-nœud] [ lnk-github-repo] ordinateur de développement tooyour de référentiel.</span><span class="sxs-lookup"><span data-stu-id="1f48c-108">When you have installed Node.js, clone hello latest version of hello [azure-iot-sdk-node][lnk-github-repo] repository tooyour development machine.</span></span> <span data-ttu-id="1f48c-109">Utilisez toujours hello **master** branche pour la version la plus récente des bibliothèques de hello et des exemples hello.</span><span class="sxs-lookup"><span data-stu-id="1f48c-109">Always use hello **master** branch for hello latest version of hello libraries and samples.</span></span>
4. <span data-ttu-id="1f48c-110">À partir de votre copie locale de hello [azure iot-sdk-nœud] [ lnk-github-repo] référentiel, hello copie suivant de deux fichiers à partir du dossier vide hello dossier nœud/périphérique/samples tooan sur votre ordinateur de développement :</span><span class="sxs-lookup"><span data-stu-id="1f48c-110">From your local copy of hello [azure-iot-sdk-node][lnk-github-repo] repository, copy hello following two files from hello node/device/samples folder tooan empty folder on your development machine:</span></span>
   
   * <span data-ttu-id="1f48c-111">packages.json</span><span class="sxs-lookup"><span data-stu-id="1f48c-111">packages.json</span></span>
   * <span data-ttu-id="1f48c-112">remote_monitoring.js</span><span class="sxs-lookup"><span data-stu-id="1f48c-112">remote_monitoring.js</span></span>
5. <span data-ttu-id="1f48c-113">Ouvrir le fichier de remote_monitoring.js hello et recherchez hello après la définition de la variable :</span><span class="sxs-lookup"><span data-stu-id="1f48c-113">Open hello remote_monitoring.js file and look for hello following variable definition:</span></span>
   
    ```
    var connectionString = "[IoT Hub device connection string]";
    ```
6. <span data-ttu-id="1f48c-114">Remplacez **[chaîne de connexion d’un périphérique de IoT Hub]** par votre chaîne de connexion de périphérique.</span><span class="sxs-lookup"><span data-stu-id="1f48c-114">Replace **[IoT Hub device connection string]** with your device connection string.</span></span> <span data-ttu-id="1f48c-115">Utilisez les valeurs hello pour votre nom d’hôte IoT Hub, id de périphérique et la clé de périphérique que vous avez notée à l’étape 1.</span><span class="sxs-lookup"><span data-stu-id="1f48c-115">Use hello values for your IoT Hub hostname, device id, and device key that you made a note of in step 1.</span></span> <span data-ttu-id="1f48c-116">Une chaîne de connexion de périphérique a hello suivant le format :</span><span class="sxs-lookup"><span data-stu-id="1f48c-116">A device connection string has hello following format:</span></span>
   
    ```
    HostName={your IoT Hub hostname};DeviceId={your device id};SharedAccessKey={your device key}
    ```
   
    <span data-ttu-id="1f48c-117">Si votre nom d’hôte du IoT Hub est **contoso** et id de votre appareil est **mydevice**, votre chaîne de connexion ressemble à hello suivant extrait de code :</span><span class="sxs-lookup"><span data-stu-id="1f48c-117">If your IoT Hub hostname is **contoso** and your device id is **mydevice**, your connection string looks like hello following snippet:</span></span>
   
    ```
    var connectionString = "HostName=contoso.azure-devices.net;DeviceId=mydevice;SharedAccessKey=2s ... =="
    ```
7. Enregistrez le fichier de hello. <span data-ttu-id="1f48c-119">Exécutez hello suivant les commandes dans un interpréteur de commandes ou d’une invite de commandes dans le dossier hello contenant ces fichiers tooinstall hello les packages, puis exécutez exemple d’application hello :</span><span class="sxs-lookup"><span data-stu-id="1f48c-119">Run hello following commands in a shell or command prompt in hello folder that contains these files tooinstall hello necessary packages and then run hello sample application:</span></span>
   
    ```
    npm install
    node remote_monitoring.js
    ```

## <a name="observe-dynamic-telemetry-in-action"></a><span data-ttu-id="1f48c-120">Observer la télémétrie dynamique en action</span><span class="sxs-lookup"><span data-stu-id="1f48c-120">Observe dynamic telemetry in action</span></span>
<span data-ttu-id="1f48c-121">tableau de bord de Hello affiche la télémétrie de température et humidité hello à partir d’appareils simulée de hello existant :</span><span class="sxs-lookup"><span data-stu-id="1f48c-121">hello dashboard shows hello temperature and humidity telemetry from hello existing simulated devices:</span></span>

![tableau de bord par défaut Hello][image1]

<span data-ttu-id="1f48c-123">Si vous sélectionnez les appareil simulé Node.js hello que vous avez exécuté dans la section précédente de hello, vous consultez température et humidité télémétrie de température externe :</span><span class="sxs-lookup"><span data-stu-id="1f48c-123">If you select hello Node.js simulated device you ran in hello previous section, you see temperature, humidity, and external temperature telemetry:</span></span>

![Ajouter le tableau de bord toohello température externe][image2]

<span data-ttu-id="1f48c-125">solution de surveillance à distance Hello détecte le type de données de télémétrie de température externe supplémentaire hello automatiquement et l’ajoute toohello graphique sur le tableau de bord hello.</span><span class="sxs-lookup"><span data-stu-id="1f48c-125">hello remote monitoring solution automatically detects hello additional external temperature telemetry type and adds it toohello chart on hello dashboard.</span></span>

[node-linux]: https://github.com/nodejs/node-v0.x-archive/wiki/Installing-Node.js-via-package-manager
[lnk-github-repo]: https://github.com/Azure/azure-iot-sdk-node
[image1]: media/iot-suite-send-external-temperature/image1.png
[image2]: media/iot-suite-send-external-temperature/image2.png