## <a name="create-a-device-identity"></a><span data-ttu-id="813e1-101">Création d’une identité d’appareil</span><span class="sxs-lookup"><span data-stu-id="813e1-101">Create a device identity</span></span>
<span data-ttu-id="813e1-102">Dans cette section, vous créez une application console .NET qui crée une identité d’appareil dans le Registre des identités hello dans votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="813e1-102">In this section, you create a .NET console app that creates a device identity in hello identity registry in your IoT hub.</span></span> <span data-ttu-id="813e1-103">Un appareil ne peut pas se connecter à tooIoT concentrateur sauf si elle possède une entrée dans le Registre des identités hello.</span><span class="sxs-lookup"><span data-stu-id="813e1-103">A device cannot connect tooIoT hub unless it has an entry in hello identity registry.</span></span> <span data-ttu-id="813e1-104">Pour plus d’informations, voir section « Registre des identités » hello hello [guide du développeur IoT Hub][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="813e1-104">For more information, see hello "Identity registry" section of hello [IoT Hub developer guide][lnk-devguide-identity].</span></span> <span data-ttu-id="813e1-105">Lorsque vous exécutez cette application console, il génère un ID d’appareil unique et clé que votre appareil peut utiliser tooidentify lui-même lorsqu’il envoie l’appareil-à-cloud messages tooIoT Hub.</span><span class="sxs-lookup"><span data-stu-id="813e1-105">When you run this console app, it generates a unique device ID and key that your device can use tooidentify itself when it sends device-to-cloud messages tooIoT Hub.</span></span> <span data-ttu-id="813e1-106">Les ID d’appareil respectent la casse.</span><span class="sxs-lookup"><span data-stu-id="813e1-106">Device IDs are case sensitive.</span></span>

1. <span data-ttu-id="813e1-107">Dans Visual Studio, ajoutez une solution de nouveau tooa de projet Visual c# bureau classique de Windows à l’aide de hello **l’application Console (.NET Framework)** modèle de projet.</span><span class="sxs-lookup"><span data-stu-id="813e1-107">In Visual Studio, add a Visual C# Windows Classic Desktop project tooa new solution by using hello **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="813e1-108">Assurez-vous que la version du .NET Framework hello est 4.5.1 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="813e1-108">Make sure hello .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="813e1-109">Projet de hello nom **CreateDeviceIdentity** et nom hello solution **IoTHubGetStarted**.</span><span class="sxs-lookup"><span data-stu-id="813e1-109">Name hello project **CreateDeviceIdentity** and name hello solution **IoTHubGetStarted**.</span></span>
   
    ![Nouveau projet Visual C# Bureau classique Windows][10]
2. <span data-ttu-id="813e1-111">Dans l’Explorateur de solutions, cliquez sur hello **CreateDeviceIdentity** de projet, puis cliquez sur **gérer les Packages NuGet**.</span><span class="sxs-lookup"><span data-stu-id="813e1-111">In Solution Explorer, right-click hello **CreateDeviceIdentity** project, and then click **Manage NuGet Packages**.</span></span>
3. <span data-ttu-id="813e1-112">Bonjour **Gestionnaire de Package NuGet** fenêtre, sélectionnez **Parcourir**, recherchez **microsoft.azure.devices**, sélectionnez **installer** tooinstall Hello **Microsoft.Azure.Devices** empaqueter et accepter les conditions d’utilisation de hello.</span><span class="sxs-lookup"><span data-stu-id="813e1-112">In hello **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** tooinstall hello **Microsoft.Azure.Devices** package, and accept hello terms of use.</span></span> <span data-ttu-id="813e1-113">Cette procédure télécharge, installe et ajoute une référence toohello [Azure IoT service SDK] [ lnk-nuget-service-sdk] NuGet package et ses dépendances.</span><span class="sxs-lookup"><span data-stu-id="813e1-113">This procedure downloads, installs, and adds a reference toohello [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![Fenêtre du gestionnaire de package NuGet][11]
4. <span data-ttu-id="813e1-115">Ajoutez hello suivant `using` instructions haut hello hello **Program.cs** fichier :</span><span class="sxs-lookup"><span data-stu-id="813e1-115">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
        using Microsoft.Azure.Devices.Common.Exceptions;
5. <span data-ttu-id="813e1-116">Ajouter hello suivant champs toohello **programme** classe.</span><span class="sxs-lookup"><span data-stu-id="813e1-116">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="813e1-117">Remplacer la valeur d’espace réservé hello avec hello chaîne de connexion de IoT Hub hub hello que vous avez créé dans la section précédente de hello de.</span><span class="sxs-lookup"><span data-stu-id="813e1-117">Replace hello placeholder value with hello IoT Hub connection string for hello hub that you created in hello previous section.</span></span>
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
6. <span data-ttu-id="813e1-118">Ajouter hello suivant de méthode toohello **programme** classe :</span><span class="sxs-lookup"><span data-stu-id="813e1-118">Add hello following method toohello **Program** class:</span></span>
   
        private static async Task AddDeviceAsync()
        {
            string deviceId = "myFirstDevice";
            Device device;
            try
            {
                device = await registryManager.AddDeviceAsync(new Device(deviceId));
            }
            catch (DeviceAlreadyExistsException)
            {
                device = await registryManager.GetDeviceAsync(deviceId);
            }
            Console.WriteLine("Generated device key: {0}", device.Authentication.SymmetricKey.PrimaryKey);
        }
   
    <span data-ttu-id="813e1-119">Cette méthode crée une identité d’appareil avec l’ID **myFirstDevice**.</span><span class="sxs-lookup"><span data-stu-id="813e1-119">This method creates a device identity with ID **myFirstDevice**.</span></span> <span data-ttu-id="813e1-120">(Si cet ID d’appareil existe déjà dans le Registre des identités hello, hello code récupère simplement les informations de périphérique existantes hello.) application Hello affiche ensuite la clé primaire de hello pour cette identité.</span><span class="sxs-lookup"><span data-stu-id="813e1-120">(If that device ID already exists in hello identity registry, hello code simply retrieves hello existing device information.) hello app then displays hello primary key for that identity.</span></span> <span data-ttu-id="813e1-121">Vous utilisez cette clé dans hello simulée appareil application tooconnect tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="813e1-121">You use this key in hello simulated device app tooconnect tooyour IoT hub.</span></span>
[!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

7. <span data-ttu-id="813e1-122">Enfin, ajoutez hello suivant lignes toohello **Main** méthode :</span><span class="sxs-lookup"><span data-stu-id="813e1-122">Finally, add hello following lines toohello **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        AddDeviceAsync().Wait();
        Console.ReadLine();
8. <span data-ttu-id="813e1-123">Exécution de cette application et prenez note de la clé de périphérique hello.</span><span class="sxs-lookup"><span data-stu-id="813e1-123">Run this application, and make a note of hello device key.</span></span>
   
    ![Clé de périphérique généré par l’application hello][12]

> [!NOTE]
> <span data-ttu-id="813e1-125">Hello Registre des identités IoT Hub stocke uniquement toohello IoT hub de périphérique identités tooenable un accès sécurisé.</span><span class="sxs-lookup"><span data-stu-id="813e1-125">hello IoT Hub identity registry only stores device identities tooenable secure access toohello IoT hub.</span></span> <span data-ttu-id="813e1-126">Il stocke toouse ID et les clés de périphérique en tant qu’informations d’identification de sécurité et un indicateur activée/désactivée que vous pouvez utiliser l’accès toodisable pour un périphérique.</span><span class="sxs-lookup"><span data-stu-id="813e1-126">It stores device IDs and keys toouse as security credentials, and an enabled/disabled flag that you can use toodisable access for an individual device.</span></span> <span data-ttu-id="813e1-127">Si votre application doit toostore autres métadonnées spécifiques au périphérique, elle doit utiliser un magasin spécifique à l’application.</span><span class="sxs-lookup"><span data-stu-id="813e1-127">If your application needs toostore other device-specific metadata, it should use an application-specific store.</span></span> <span data-ttu-id="813e1-128">Pour plus d’informations, reportez-vous au [Guide du développeur IoT Hub][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="813e1-128">For more information, see [IoT Hub developer guide][lnk-devguide-identity].</span></span>
> 
> 

<!-- Images. -->
[10]: ./media/iot-hub-get-started-create-device-identity-csharp/create-identity-csharp1.png
[11]: ./media/iot-hub-get-started-create-device-identity-csharp/create-identity-csharp2.png
[12]: ./media/iot-hub-get-started-create-device-identity-csharp/create-identity-csharp3.png


<!-- Links -->
[lnk-devguide-identity]: ../articles/iot-hub/iot-hub-devguide-identity-registry.md
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
