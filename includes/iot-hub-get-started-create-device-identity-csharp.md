## <a name="create-a-device-identity"></a>Création d’une identité d’appareil
Dans cette section, vous créez une application console .NET qui crée une identité d’appareil dans le Registre des identités hello dans votre hub IoT. Un appareil ne peut pas se connecter à tooIoT concentrateur sauf si elle possède une entrée dans le Registre des identités hello. Pour plus d’informations, voir section « Registre des identités » hello hello [guide du développeur IoT Hub][lnk-devguide-identity]. Lorsque vous exécutez cette application console, il génère un ID d’appareil unique et clé que votre appareil peut utiliser tooidentify lui-même lorsqu’il envoie l’appareil-à-cloud messages tooIoT Hub. Les ID d’appareil respectent la casse.

1. Dans Visual Studio, ajoutez une solution de nouveau tooa de projet Visual c# bureau classique de Windows à l’aide de hello **l’application Console (.NET Framework)** modèle de projet. Assurez-vous que la version du .NET Framework hello est 4.5.1 ou version ultérieure. Projet de hello nom **CreateDeviceIdentity** et nom hello solution **IoTHubGetStarted**.
   
    ![Nouveau projet Visual C# Bureau classique Windows][10]
2. Dans l’Explorateur de solutions, cliquez sur hello **CreateDeviceIdentity** de projet, puis cliquez sur **gérer les Packages NuGet**.
3. Bonjour **Gestionnaire de Package NuGet** fenêtre, sélectionnez **Parcourir**, recherchez **microsoft.azure.devices**, sélectionnez **installer** tooinstall Hello **Microsoft.Azure.Devices** empaqueter et accepter les conditions d’utilisation de hello. Cette procédure télécharge, installe et ajoute une référence toohello [Azure IoT service SDK] [ lnk-nuget-service-sdk] NuGet package et ses dépendances.
   
    ![Fenêtre du gestionnaire de package NuGet][11]
4. Ajoutez hello suivant `using` instructions haut hello hello **Program.cs** fichier :
   
        using Microsoft.Azure.Devices;
        using Microsoft.Azure.Devices.Common.Exceptions;
5. Ajouter hello suivant champs toohello **programme** classe. Remplacer la valeur d’espace réservé hello avec hello chaîne de connexion de IoT Hub hub hello que vous avez créé dans la section précédente de hello de.
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
6. Ajouter hello suivant de méthode toohello **programme** classe :
   
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
   
    Cette méthode crée une identité d’appareil avec l’ID **myFirstDevice**. (Si cet ID d’appareil existe déjà dans le Registre des identités hello, hello code récupère simplement les informations de périphérique existantes hello.) application Hello affiche ensuite la clé primaire de hello pour cette identité. Vous utilisez cette clé dans hello simulée appareil application tooconnect tooyour IoT hub.
[!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

7. Enfin, ajoutez hello suivant lignes toohello **Main** méthode :
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        AddDeviceAsync().Wait();
        Console.ReadLine();
8. Exécution de cette application et prenez note de la clé de périphérique hello.
   
    ![Clé de périphérique généré par l’application hello][12]

> [!NOTE]
> Hello Registre des identités IoT Hub stocke uniquement toohello IoT hub de périphérique identités tooenable un accès sécurisé. Il stocke toouse ID et les clés de périphérique en tant qu’informations d’identification de sécurité et un indicateur activée/désactivée que vous pouvez utiliser l’accès toodisable pour un périphérique. Si votre application doit toostore autres métadonnées spécifiques au périphérique, elle doit utiliser un magasin spécifique à l’application. Pour plus d’informations, reportez-vous au [Guide du développeur IoT Hub][lnk-devguide-identity].
> 
> 

<!-- Images. -->
[10]: ./media/iot-hub-get-started-create-device-identity-csharp/create-identity-csharp1.png
[11]: ./media/iot-hub-get-started-create-device-identity-csharp/create-identity-csharp2.png
[12]: ./media/iot-hub-get-started-create-device-identity-csharp/create-identity-csharp3.png


<!-- Links -->
[lnk-devguide-identity]: ../articles/iot-hub/iot-hub-devguide-identity-registry.md
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
