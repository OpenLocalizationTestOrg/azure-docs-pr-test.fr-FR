## <a name="create-a-device-identity"></a><span data-ttu-id="a1e4d-101">Création d’une identité d’appareil</span><span class="sxs-lookup"><span data-stu-id="a1e4d-101">Create a device identity</span></span>
<span data-ttu-id="a1e4d-102">Dans cette section, vous allez créer une application console .NET qui crée une identité d’appareil dans le registre d’identités de votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="a1e4d-102">In this section, you create a .NET console app that creates a device identity in the identity registry in your IoT hub.</span></span> <span data-ttu-id="a1e4d-103">Un appareil ne peut pas se connecter à IoT Hub, à moins de posséder une entrée dans le registre des identités.</span><span class="sxs-lookup"><span data-stu-id="a1e4d-103">A device cannot connect to IoT hub unless it has an entry in the identity registry.</span></span> <span data-ttu-id="a1e4d-104">Reportez-vous à la section Registre d’identité du [Guide du développeur IoT Hub][lnk-devguide-identity] pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="a1e4d-104">For more information, see the "Identity registry" section of the [IoT Hub developer guide][lnk-devguide-identity].</span></span> <span data-ttu-id="a1e4d-105">Lorsque vous exécutez cette application de console, elle génère un ID d’appareil et une clé uniques que votre appareil peut utiliser pour s’identifier pour lorsqu’il envoie des messages appareil-à-cloud à IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="a1e4d-105">When you run this console app, it generates a unique device ID and key that your device can use to identify itself when it sends device-to-cloud messages to IoT Hub.</span></span> <span data-ttu-id="a1e4d-106">Les ID d’appareil respectent la casse.</span><span class="sxs-lookup"><span data-stu-id="a1e4d-106">Device IDs are case sensitive.</span></span>

1. <span data-ttu-id="a1e4d-107">Dans Visual Studio, ajoutez un projet Visual C# Bureau classique Windows à une nouvelle solution en utilisant le modèle de projet **Application console (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="a1e4d-107">In Visual Studio, add a Visual C# Windows Classic Desktop project to a new solution by using the **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="a1e4d-108">Assurez-vous que la version du .NET Framework est définie sur 4.5.1 ou supérieur.</span><span class="sxs-lookup"><span data-stu-id="a1e4d-108">Make sure the .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="a1e4d-109">Nommez le projet **CreateDeviceIdentity** et nommez la solution **IoTHubGetStarted**.</span><span class="sxs-lookup"><span data-stu-id="a1e4d-109">Name the project **CreateDeviceIdentity** and name the solution **IoTHubGetStarted**.</span></span>
   
    ![Nouveau projet Visual C# Bureau classique Windows][10]
2. <span data-ttu-id="a1e4d-111">Dans l’Explorateur de solutions, cliquez avec le bouton droit sur le projet **CreateDeviceIdentity**, puis cliquez sur **Gérer les packages Nuget**.</span><span class="sxs-lookup"><span data-stu-id="a1e4d-111">In Solution Explorer, right-click the **CreateDeviceIdentity** project, and then click **Manage NuGet Packages**.</span></span>
3. <span data-ttu-id="a1e4d-112">Dans la fenêtre **Gestionnaire de package NuGet**, cliquez sur **Parcourir**, puis recherchez **microsoft.azure.devices**. Cliquez ensuite sur **Installer** pour installer le package **Microsoft.Azure.Devices**, puis acceptez les conditions d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="a1e4d-112">In the **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** to install the **Microsoft.Azure.Devices** package, and accept the terms of use.</span></span> <span data-ttu-id="a1e4d-113">Cette procédure lance le téléchargement et l’installation et ajoute une référence au [package Azure IoT Service SDK NuGet][lnk-nuget-service-sdk] et ses dépendances.</span><span class="sxs-lookup"><span data-stu-id="a1e4d-113">This procedure downloads, installs, and adds a reference to the [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![Fenêtre du gestionnaire de package NuGet][11]
4. <span data-ttu-id="a1e4d-115">Ajoutez les instructions `using` suivantes en haut du fichier **Program.cs** :</span><span class="sxs-lookup"><span data-stu-id="a1e4d-115">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
        using Microsoft.Azure.Devices.Common.Exceptions;
5. <span data-ttu-id="a1e4d-116">Ajoutez les champs suivants à la classe **Program** .</span><span class="sxs-lookup"><span data-stu-id="a1e4d-116">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="a1e4d-117">Remplacez la valeur d’espace réservé par la chaîne de connexion IoT Hub pour le hub créé dans la section précédente.</span><span class="sxs-lookup"><span data-stu-id="a1e4d-117">Replace the placeholder value with the IoT Hub connection string for the hub that you created in the previous section.</span></span>
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
6. <span data-ttu-id="a1e4d-118">Ajoutez la méthode suivante à la classe **Program** :</span><span class="sxs-lookup"><span data-stu-id="a1e4d-118">Add the following method to the **Program** class:</span></span>
   
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
   
    <span data-ttu-id="a1e4d-119">Cette méthode crée une identité d’appareil avec l’ID **myFirstDevice**.</span><span class="sxs-lookup"><span data-stu-id="a1e4d-119">This method creates a device identity with ID **myFirstDevice**.</span></span> <span data-ttu-id="a1e4d-120">(si cet ID d’appareil existe déjà dans le registre d’identité, le code récupère simplement les informations d’appareil existantes.) L’application affiche ensuite la clé primaire pour cette identité.</span><span class="sxs-lookup"><span data-stu-id="a1e4d-120">(If that device ID already exists in the identity registry, the code simply retrieves the existing device information.) The app then displays the primary key for that identity.</span></span> <span data-ttu-id="a1e4d-121">Vous utilisez cette clé dans l’application de périphérique simulé pour vous connecter à votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="a1e4d-121">You use this key in the simulated device app to connect to your IoT hub.</span></span>
[!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

7. <span data-ttu-id="a1e4d-122">Enfin, ajoutez les lignes suivantes à la méthode **Main** :</span><span class="sxs-lookup"><span data-stu-id="a1e4d-122">Finally, add the following lines to the **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        AddDeviceAsync().Wait();
        Console.ReadLine();
8. <span data-ttu-id="a1e4d-123">Exécutez cette application et notez la clé de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="a1e4d-123">Run this application, and make a note of the device key.</span></span>
   
    ![Clé d’appareil générée par l’application][12]

> [!NOTE]
> <span data-ttu-id="a1e4d-125">Le registre des identités IoT Hub stocke uniquement les identités des appareils pour permettre un accès sécurisé à IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="a1e4d-125">The IoT Hub identity registry only stores device identities to enable secure access to the IoT hub.</span></span> <span data-ttu-id="a1e4d-126">Il stocke les ID des appareils et les clés à utiliser comme informations d’identification de sécurité et un indicateur activé/désactivé que vous pouvez utiliser pour désactiver l’accès pour un appareil individuel.</span><span class="sxs-lookup"><span data-stu-id="a1e4d-126">It stores device IDs and keys to use as security credentials, and an enabled/disabled flag that you can use to disable access for an individual device.</span></span> <span data-ttu-id="a1e4d-127">Si votre application a besoin de stocker d’autres métadonnées spécifiques aux appareils, elle doit utiliser un magasin spécifique aux applications.</span><span class="sxs-lookup"><span data-stu-id="a1e4d-127">If your application needs to store other device-specific metadata, it should use an application-specific store.</span></span> <span data-ttu-id="a1e4d-128">Pour plus d’informations, reportez-vous au [Guide du développeur IoT Hub][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="a1e4d-128">For more information, see [IoT Hub developer guide][lnk-devguide-identity].</span></span>
> 
> 

<!-- Images. -->
[10]: ./media/iot-hub-get-started-create-device-identity-csharp/create-identity-csharp1.png
[11]: ./media/iot-hub-get-started-create-device-identity-csharp/create-identity-csharp2.png
[12]: ./media/iot-hub-get-started-create-device-identity-csharp/create-identity-csharp3.png


<!-- Links -->
[lnk-devguide-identity]: ../articles/iot-hub/iot-hub-devguide-identity-registry.md
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
