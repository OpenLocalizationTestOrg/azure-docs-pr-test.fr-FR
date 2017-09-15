## <a name="configure-the-nodejs-simulated-device"></a><span data-ttu-id="f7f9d-101">Configurer l’appareil simulé Node.js</span><span class="sxs-lookup"><span data-stu-id="f7f9d-101">Configure the Node.js simulated device</span></span>
1. <span data-ttu-id="f7f9d-102">Dans le tableau de bord de surveillance à distance, cliquez sur **+ Ajouter un appareil**, puis ajoutez un *appareil personnalisé*.</span><span class="sxs-lookup"><span data-stu-id="f7f9d-102">On the remote monitoring dashboard, click **+ Add a device** and then add a *custom device*.</span></span> <span data-ttu-id="f7f9d-103">Notez le nom d’hôte, l’ID de l’appareil et la clé de l’appareil IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="f7f9d-103">Make a note of the IoT Hub hostname, device id, and device key.</span></span> <span data-ttu-id="f7f9d-104">Vous en aurez besoin ultérieurement dans ce didacticiel lorsque vous préparerez l’application cliente de l’appareil remote_monitoring.js.</span><span class="sxs-lookup"><span data-stu-id="f7f9d-104">You need them later in this tutorial when you prepare the remote_monitoring.js device client application.</span></span>
2. <span data-ttu-id="f7f9d-105">Assurez-vous que Node.js version 0.12.x ou ultérieure est installé sur votre ordinateur de développement.</span><span class="sxs-lookup"><span data-stu-id="f7f9d-105">Ensure that Node.js version 0.12.x or later is installed on your development machine.</span></span> <span data-ttu-id="f7f9d-106">Exécutez `node --version` à l’invite de commande ou dans un interpréteur de commandes pour vérifier la version.</span><span class="sxs-lookup"><span data-stu-id="f7f9d-106">Run `node --version` at a command prompt or in a shell to check the version.</span></span> <span data-ttu-id="f7f9d-107">Pour plus d’informations sur l’utilisation d’un gestionnaire de package pour installer Node.js sur Linux, consultez l’article [Installing Node.js via package manager][node-linux] (Installation de Node.js par le biais d’un gestionnaire de package).</span><span class="sxs-lookup"><span data-stu-id="f7f9d-107">For information about using a package manager to install Node.js on Linux, see [Installing Node.js via package manager][node-linux].</span></span>
3. <span data-ttu-id="f7f9d-108">Une fois que vous avez installé Node.js, clonez la dernière version du référentiel [azure-iot-sdk-node][lnk-github-repo] sur votre ordinateur de développement.</span><span class="sxs-lookup"><span data-stu-id="f7f9d-108">When you have installed Node.js, clone the latest version of the [azure-iot-sdk-node][lnk-github-repo] repository to your development machine.</span></span> <span data-ttu-id="f7f9d-109">Utilisez toujours la branche **maître** pour avoir la version la plus récente des bibliothèques et des exemples.</span><span class="sxs-lookup"><span data-stu-id="f7f9d-109">Always use the **master** branch for the latest version of the libraries and samples.</span></span>
4. <span data-ttu-id="f7f9d-110">À partir de votre copie locale du référentiel [azure-iot-sdk-node][lnk-github-repo], copiez les deux fichiers ci-après du dossier node/device/samples vers un dossier vide de votre ordinateur de développement :</span><span class="sxs-lookup"><span data-stu-id="f7f9d-110">From your local copy of the [azure-iot-sdk-node][lnk-github-repo] repository, copy the following two files from the node/device/samples folder to an empty folder on your development machine:</span></span>
   
   * <span data-ttu-id="f7f9d-111">packages.json</span><span class="sxs-lookup"><span data-stu-id="f7f9d-111">packages.json</span></span>
   * <span data-ttu-id="f7f9d-112">remote_monitoring.js</span><span class="sxs-lookup"><span data-stu-id="f7f9d-112">remote_monitoring.js</span></span>
5. <span data-ttu-id="f7f9d-113">Ouvrez le fichier remote_monitoring.js et recherchez la définition de variable suivante :</span><span class="sxs-lookup"><span data-stu-id="f7f9d-113">Open the remote_monitoring.js file and look for the following variable definition:</span></span>
   
    ```
    var connectionString = "[IoT Hub device connection string]";
    ```
6. <span data-ttu-id="f7f9d-114">Remplacez **[chaîne de connexion d’un périphérique de IoT Hub]** par votre chaîne de connexion de périphérique.</span><span class="sxs-lookup"><span data-stu-id="f7f9d-114">Replace **[IoT Hub device connection string]** with your device connection string.</span></span> <span data-ttu-id="f7f9d-115">Utilisez les valeurs de nom d’hôte, ID de l’appareil et clé de l’appareil IoT Hub notées à l’étape 1.</span><span class="sxs-lookup"><span data-stu-id="f7f9d-115">Use the values for your IoT Hub hostname, device id, and device key that you made a note of in step 1.</span></span> <span data-ttu-id="f7f9d-116">La chaîne de connexion du périphérique suit ce format :</span><span class="sxs-lookup"><span data-stu-id="f7f9d-116">A device connection string has the following format:</span></span>
   
    ```
    HostName={your IoT Hub hostname};DeviceId={your device id};SharedAccessKey={your device key}
    ```
   
    <span data-ttu-id="f7f9d-117">Si votre nom d’hôte IoT Hub est **contoso** et votre ID d’appareil **mydevice**, votre chaîne de connexion ressemble à l’extrait de code suivant :</span><span class="sxs-lookup"><span data-stu-id="f7f9d-117">If your IoT Hub hostname is **contoso** and your device id is **mydevice**, your connection string looks like the following snippet:</span></span>
   
    ```
    var connectionString = "HostName=contoso.azure-devices.net;DeviceId=mydevice;SharedAccessKey=2s ... =="
    ```
7. Enregistrez le fichier . <span data-ttu-id="f7f9d-119">Exécutez les commandes suivantes dans un interpréteur de commandes ou une invite de commandes dans le dossier contenant ces fichiers pour installer les packages nécessaires, puis exécutez l’exemple d’application :</span><span class="sxs-lookup"><span data-stu-id="f7f9d-119">Run the following commands in a shell or command prompt in the folder that contains these files to install the necessary packages and then run the sample application:</span></span>
   
    ```
    npm install
    node remote_monitoring.js
    ```

## <a name="observe-dynamic-telemetry-in-action"></a><span data-ttu-id="f7f9d-120">Observer la télémétrie dynamique en action</span><span class="sxs-lookup"><span data-stu-id="f7f9d-120">Observe dynamic telemetry in action</span></span>
<span data-ttu-id="f7f9d-121">Le tableau de bord affiche la télémétrie de température et d’humidité à partir des appareils simulés existants :</span><span class="sxs-lookup"><span data-stu-id="f7f9d-121">The dashboard shows the temperature and humidity telemetry from the existing simulated devices:</span></span>

![Tableau de bord par défaut][image1]

<span data-ttu-id="f7f9d-123">Si vous sélectionnez l’appareil simulé Node.js que vous avez exécuté dans la section précédente, vous affichez la télémétrie de température, d’humidité et de température externe :</span><span class="sxs-lookup"><span data-stu-id="f7f9d-123">If you select the Node.js simulated device you ran in the previous section, you see temperature, humidity, and external temperature telemetry:</span></span>

![Ajouter une température externe au tableau de bord][image2]

<span data-ttu-id="f7f9d-125">La solution de surveillance à distance détecte automatiquement le type supplémentaire de télémétrie de température externe et l’ajoute au graphique sur le tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="f7f9d-125">The remote monitoring solution automatically detects the additional external temperature telemetry type and adds it to the chart on the dashboard.</span></span>

[node-linux]: https://github.com/nodejs/node-v0.x-archive/wiki/Installing-Node.js-via-package-manager
[lnk-github-repo]: https://github.com/Azure/azure-iot-sdk-node
[image1]: media/iot-suite-send-external-temperature/image1.png
[image2]: media/iot-suite-send-external-temperature/image2.png