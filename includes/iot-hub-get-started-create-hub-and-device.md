## <a name="create-an-iot-hub"></a><span data-ttu-id="b2c53-101">Créer un hub IoT</span><span class="sxs-lookup"><span data-stu-id="b2c53-101">Create an IoT hub</span></span>

1. <span data-ttu-id="b2c53-102">Bonjour [portail Azure](https://portal.azure.com/), cliquez sur **nouveau** > **Internet of Things** > **IoT Hub**.</span><span class="sxs-lookup"><span data-stu-id="b2c53-102">In hello [Azure portal](https://portal.azure.com/), click **New** > **Internet of Things** > **IoT Hub**.</span></span>

   ![Créez un hub IoT Bonjour portail Azure](../articles/iot-hub/media/iot-hub-create-hub-and-device/1_create-azure-iot-hub-portal.png)
2. <span data-ttu-id="b2c53-104">Bonjour **IoT hub** volet, entrez hello informations pour votre hub IoT suivantes :</span><span class="sxs-lookup"><span data-stu-id="b2c53-104">In hello **IoT hub** pane, enter hello following information for your IoT hub:</span></span>

     <span data-ttu-id="b2c53-105">**Nom**: entrez le nom hello de votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="b2c53-105">**Name**: Enter hello name of your IoT hub.</span></span> <span data-ttu-id="b2c53-106">Si le nom hello que vous entrez est valide, une coche verte s’affiche.</span><span class="sxs-lookup"><span data-stu-id="b2c53-106">If hello name you enter is valid, a green check mark appears.</span></span>

     <span data-ttu-id="b2c53-107">**Niveau de tarification et de mise à l’échelle**: hello sélectionnez **F1 - libre** couche.</span><span class="sxs-lookup"><span data-stu-id="b2c53-107">**Pricing and scale tier**: Select hello **F1 - Free** tier.</span></span> <span data-ttu-id="b2c53-108">Cette option suffit pour cette démonstration.</span><span class="sxs-lookup"><span data-stu-id="b2c53-108">This option is sufficient for this demo.</span></span> <span data-ttu-id="b2c53-109">Pour plus d’informations, consultez hello [niveau de tarification et de mise à l’échelle](https://azure.microsoft.com/pricing/details/iot-hub/).</span><span class="sxs-lookup"><span data-stu-id="b2c53-109">For more information, see hello [Pricing and scale tier](https://azure.microsoft.com/pricing/details/iot-hub/).</span></span>

     <span data-ttu-id="b2c53-110">**Groupe de ressources**: création d’un ressource groupe toohost hello IoT hub ou utilisez-en un existant.</span><span class="sxs-lookup"><span data-stu-id="b2c53-110">**Resource group**: Create a resource group toohost hello IoT hub or use an existing one.</span></span> <span data-ttu-id="b2c53-111">Pour plus d’informations, consultez [groupes de ressources de l’utilisation toomanage vos ressources Azure](../articles/azure-resource-manager/resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="b2c53-111">For more information, see [Use resource groups toomanage your Azure resources](../articles/azure-resource-manager/resource-group-portal.md).</span></span>

     <span data-ttu-id="b2c53-112">**Emplacement**: sélectionnez hello plus proche tooyou emplacement où hub IoT de hello est créé.</span><span class="sxs-lookup"><span data-stu-id="b2c53-112">**Location**: Select hello closest location tooyou where hello IoT hub is created.</span></span>

     <span data-ttu-id="b2c53-113">**Code confidentiel toodashboard**: sélectionnez cette option pour le hub de IoT tooyour accéder facilement à partir du tableau de bord hello.</span><span class="sxs-lookup"><span data-stu-id="b2c53-113">**Pin toodashboard**: Select this option for easy access tooyour IoT hub from hello dashboard.</span></span>

   ![Entrez les informations toocreate votre IoT hub](../articles/iot-hub/media/iot-hub-create-hub-and-device/2_fill-in-fields-for-azure-iot-hub-portal.png)

   [!INCLUDE [iot-hub-pii-note-naming-hub](iot-hub-pii-note-naming-hub.md)]

3. <span data-ttu-id="b2c53-115">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="b2c53-115">Click **Create**.</span></span> <span data-ttu-id="b2c53-116">Votre IoT hub peut prendre quelques minutes toocreate.</span><span class="sxs-lookup"><span data-stu-id="b2c53-116">Your IoT hub might take a few minutes toocreate.</span></span> <span data-ttu-id="b2c53-117">Vous pouvez consulter la progression dans hello **Notifications** volet.</span><span class="sxs-lookup"><span data-stu-id="b2c53-117">You can see progress in hello **Notifications** pane.</span></span>

   ![Voir les notifications de progression de votre IoT Hub](../articles/iot-hub/media/iot-hub-create-hub-and-device/3_notification-azure-iot-hub-creation-progress-portal.png)

4. <span data-ttu-id="b2c53-119">Une fois votre hub IoT est créé, cliquez dessus dans le tableau de bord hello.</span><span class="sxs-lookup"><span data-stu-id="b2c53-119">After your IoT hub is created, click it on hello dashboard.</span></span> <span data-ttu-id="b2c53-120">Prenez note de hello **nom d’hôte**, puis cliquez sur **les stratégies d’accès partagé**.</span><span class="sxs-lookup"><span data-stu-id="b2c53-120">Make a note of hello **Hostname**, and then click **Shared access policies**.</span></span>

   ![Obtenir le nom d’hôte hello de votre hub IoT](../articles/iot-hub/media/iot-hub-create-hub-and-device/4_get-azure-iot-hub-hostname-portal.png)

5. <span data-ttu-id="b2c53-122">Bonjour **les stratégies d’accès partagé** volet, cliquez sur hello **iothubowner** stratégie, puis copie et noté de hello **chaîne de connexion** de votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="b2c53-122">In hello **Shared access policies** pane, click hello **iothubowner** policy, and then copy and make a note of hello **Connection string** of your IoT hub.</span></span> <span data-ttu-id="b2c53-123">Pour plus d’informations, consultez [tooIoT d’accès contrôle Hub](../articles/iot-hub/iot-hub-devguide-security.md).</span><span class="sxs-lookup"><span data-stu-id="b2c53-123">For more information, see [Control access tooIoT Hub](../articles/iot-hub/iot-hub-devguide-security.md).</span></span>

> [!NOTE] 
<span data-ttu-id="b2c53-124">Vous n’aurez pas besoin de cette chaîne de connexion iothubowner pour ce didacticiel d’installation.</span><span class="sxs-lookup"><span data-stu-id="b2c53-124">You will not need this iothubowner connection string for this set-up tutorial.</span></span> <span data-ttu-id="b2c53-125">Toutefois, vous devrez il pour certaines des didacticiels hello sur différents scénarios IoT après avoir terminé cette installation.</span><span class="sxs-lookup"><span data-stu-id="b2c53-125">However, you may need it for some of hello tutorials on different IoT scenarios after you complete this set-up.</span></span>

   ![Obtention de la chaîne de connexion de votre IoT Hub](../articles/iot-hub/media/iot-hub-create-hub-and-device/5_get-azure-iot-hub-connection-string-portal.png)

## <a name="register-a-device-in-hello-iot-hub-for-your-device"></a><span data-ttu-id="b2c53-127">Inscrire un appareil dans hello IoT hub pour votre appareil</span><span class="sxs-lookup"><span data-stu-id="b2c53-127">Register a device in hello IoT hub for your device</span></span>

1. <span data-ttu-id="b2c53-128">Bonjour [portail Azure](https://portal.azure.com/), ouvrez votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="b2c53-128">In hello [Azure portal](https://portal.azure.com/), open your IoT hub.</span></span>

2. <span data-ttu-id="b2c53-129">Cliquez sur **Explorateur d’appareils**.</span><span class="sxs-lookup"><span data-stu-id="b2c53-129">Click **Device Explorer**.</span></span>
3. <span data-ttu-id="b2c53-130">Dans le volet de l’Explorateur de l’appareil hello, cliquez sur **ajouter** tooadd un IoT hub de périphérique tooyour.</span><span class="sxs-lookup"><span data-stu-id="b2c53-130">In hello Device Explorer pane, click **Add** tooadd a device tooyour IoT hub.</span></span> <span data-ttu-id="b2c53-131">Puis la hello suivant :</span><span class="sxs-lookup"><span data-stu-id="b2c53-131">Then do hello following:</span></span>

   <span data-ttu-id="b2c53-132">**ID de périphérique**: hello de saisir de nouveau périphérique de hello.</span><span class="sxs-lookup"><span data-stu-id="b2c53-132">**Device ID**: Enter hello ID of hello new device.</span></span> <span data-ttu-id="b2c53-133">Les ID d’appareil respectent la casse.</span><span class="sxs-lookup"><span data-stu-id="b2c53-133">Device IDs are case sensitive.</span></span>

   <span data-ttu-id="b2c53-134">**Type d’authentification** : sélectionnez **Clé symétrique**.</span><span class="sxs-lookup"><span data-stu-id="b2c53-134">**Authentication Type**: Select **Symmetric Key**.</span></span>

   <span data-ttu-id="b2c53-135">**Générer automatiquement les clés** : cochez cette case.</span><span class="sxs-lookup"><span data-stu-id="b2c53-135">**Auto Generate Keys**: Select this check box.</span></span>

   <span data-ttu-id="b2c53-136">**Connecter l’appareil tooIoT Hub**: cliquez sur **activer**.</span><span class="sxs-lookup"><span data-stu-id="b2c53-136">**Connect device tooIoT Hub**: Click **Enable**.</span></span>

   ![Ajouter un périphérique dans hello Explorateur de l’appareil de votre hub IoT](../articles/iot-hub/media/iot-hub-create-hub-and-device/6_add-device-in-azure-iot-hub-device-explorer-portal.png)

   [!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

4. <span data-ttu-id="b2c53-138">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="b2c53-138">Click **Save**.</span></span>
5. <span data-ttu-id="b2c53-139">Après la création de l’appareil de hello, d’ouvrir l’unité de hello Bonjour **appareil Explorer** volet.</span><span class="sxs-lookup"><span data-stu-id="b2c53-139">After hello device is created, open hello device in hello **Device Explorer** pane.</span></span>
6. <span data-ttu-id="b2c53-140">Prenez note de clé primaire de hello hello de chaîne de connexion.</span><span class="sxs-lookup"><span data-stu-id="b2c53-140">Make a note of hello primary key of hello connection string.</span></span>

   ![Obtenir la chaîne de connexion de périphérique hello](../articles/iot-hub/media/iot-hub-create-hub-and-device/7_get-device-connection-string-in-device-explorer-portal.png)
