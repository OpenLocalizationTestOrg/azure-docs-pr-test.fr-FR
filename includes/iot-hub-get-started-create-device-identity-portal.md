## <a name="create-a-device-identity"></a><span data-ttu-id="c4c8a-101">Création d’une identité d’appareil</span><span class="sxs-lookup"><span data-stu-id="c4c8a-101">Create a device identity</span></span>

<span data-ttu-id="c4c8a-102">Dans cette section, vous utilisez hello [portail Azure] [ lnk-azure-portal] toocreate une identité d’appareil dans le Registre des identités hello dans votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="c4c8a-102">In this section, you use hello [Azure portal][lnk-azure-portal] toocreate a device identity in hello identity registry in your IoT hub.</span></span> <span data-ttu-id="c4c8a-103">Un appareil ne peut pas se connecter à tooIoT concentrateur sauf si elle possède une entrée dans le Registre des identités hello.</span><span class="sxs-lookup"><span data-stu-id="c4c8a-103">A device cannot connect tooIoT hub unless it has an entry in hello identity registry.</span></span> <span data-ttu-id="c4c8a-104">Pour plus d’informations, voir section « Registre des identités » hello hello [guide du développeur IoT Hub][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="c4c8a-104">For more information, see hello "Identity registry" section of hello [IoT Hub developer guide][lnk-devguide-identity].</span></span> <span data-ttu-id="c4c8a-105">Hello **appareil Explorer** Bonjour portail vous permet de générer un ID d’appareil unique et une clé que votre appareil peut utiliser tooidentify lui-même quand il connecte tooIoT Hub.</span><span class="sxs-lookup"><span data-stu-id="c4c8a-105">hello **Device Explorer** in hello portal helps you generate a unique device ID and key that your device can use tooidentify itself when it connects tooIoT Hub.</span></span> <span data-ttu-id="c4c8a-106">Les ID d’appareil respectent la casse.</span><span class="sxs-lookup"><span data-stu-id="c4c8a-106">Device IDs are case sensitive.</span></span>

1. <span data-ttu-id="c4c8a-107">Assurez-vous que vous êtes connecté dans toohello [portail Azure][lnk-azure-portal].</span><span class="sxs-lookup"><span data-stu-id="c4c8a-107">Make sure you are signed in toohello [Azure portal][lnk-azure-portal].</span></span>

1. <span data-ttu-id="c4c8a-108">Bonjour Jumpbar, cliquez sur **toutes les ressources** et recherchez votre ressource de hub IoT.</span><span class="sxs-lookup"><span data-stu-id="c4c8a-108">In hello Jumpbar, click **All resources** and find your IoT hub resource.</span></span>

    ![Accédez tooyour Iot hub][img-find-iothub]

1. <span data-ttu-id="c4c8a-110">Lorsque votre ressource de hub IoT est ouverte, cliquez sur hello **appareil Explorer** d’outils, puis cliquez sur **ajouter** haut hello.</span><span class="sxs-lookup"><span data-stu-id="c4c8a-110">When your IoT hub resource is opened, click hello **Device Explorer** tool, and then click **Add** at hello top.</span></span> <span data-ttu-id="c4c8a-111">Fournir le nom hello pour votre nouveau périphérique, tel que **myDeviceId**, puis cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="c4c8a-111">Provide hello name for your new device, such as **myDeviceId**, and click **Save**.</span></span>

    ![Créer une identité d’appareil sur le portail][img-create-device]

   <span data-ttu-id="c4c8a-113">Cela permet de créer une identité d’appareil pour votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="c4c8a-113">This creates a new device identity for your IoT hub.</span></span>

   [!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

1. <span data-ttu-id="c4c8a-114">Bonjour **appareil Explorer**de liste de périphériques, cliquez sur le périphérique de hello qui vient d’être créé et prenez note de hello **chaîne de connexion---clé primaire**.</span><span class="sxs-lookup"><span data-stu-id="c4c8a-114">In hello **Device Explorer**'s device list, click hello newly created device and make note of hello **Connection string---primary key**.</span></span> 

    ![Chaîne de connexion de l’appareil][img-connection-string]

> [!NOTE]
> <span data-ttu-id="c4c8a-116">Hello Registre des identités IoT Hub stocke uniquement toohello IoT hub de périphérique identités tooenable un accès sécurisé.</span><span class="sxs-lookup"><span data-stu-id="c4c8a-116">hello IoT Hub identity registry only stores device identities tooenable secure access toohello IoT hub.</span></span> <span data-ttu-id="c4c8a-117">Il stocke toouse ID et les clés de périphérique en tant qu’informations d’identification de sécurité et un indicateur activée/désactivée que vous pouvez utiliser l’accès toodisable pour un périphérique.</span><span class="sxs-lookup"><span data-stu-id="c4c8a-117">It stores device IDs and keys toouse as security credentials, and an enabled/disabled flag that you can use toodisable access for an individual device.</span></span> <span data-ttu-id="c4c8a-118">Si votre application doit toostore autres métadonnées spécifiques au périphérique, elle doit utiliser un magasin spécifique à l’application.</span><span class="sxs-lookup"><span data-stu-id="c4c8a-118">If your application needs toostore other device-specific metadata, it should use an application-specific store.</span></span> <span data-ttu-id="c4c8a-119">Pour plus d’informations, reportez-vous au [Guide du développeur IoT Hub][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="c4c8a-119">For more information, see [IoT Hub developer guide][lnk-devguide-identity].</span></span>

<!-- Images. -->
[img-find-iothub]: ./media/iot-hub-get-started-create-device-identity-portal/find-iothub.png
[img-create-device]: ./media/iot-hub-get-started-create-device-identity-portal/create-identity-portal.png
[img-connection-string]: ./media/iot-hub-get-started-create-device-identity-portal/device-connection-string.png


<!-- Links -->
[lnk-azure-portal]: https://portal.azure.com
[lnk-devguide-identity]: ../articles/iot-hub/iot-hub-devguide-identity-registry.md

