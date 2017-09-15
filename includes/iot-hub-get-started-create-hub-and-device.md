## <a name="create-an-iot-hub"></a><span data-ttu-id="2822a-101">Créer un hub IoT</span><span class="sxs-lookup"><span data-stu-id="2822a-101">Create an IoT hub</span></span>

1. <span data-ttu-id="2822a-102">Dans le [portail Azure](https://portal.azure.com/), cliquez sur **Nouveau** > **Internet des objets** > **IoT Hub**.</span><span class="sxs-lookup"><span data-stu-id="2822a-102">In the [Azure portal](https://portal.azure.com/), click **New** > **Internet of Things** > **IoT Hub**.</span></span>

   ![Créer un IoT Hub dans le portail Azure](../articles/iot-hub/media/iot-hub-create-hub-and-device/1_create-azure-iot-hub-portal.png)
2. <span data-ttu-id="2822a-104">Dans le volet **IoT Hub**, entrez les informations suivantes pour votre IoT Hub :</span><span class="sxs-lookup"><span data-stu-id="2822a-104">In the **IoT hub** pane, enter the following information for your IoT hub:</span></span>

     <span data-ttu-id="2822a-105">**Nom** : entrez le nom de votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="2822a-105">**Name**: Enter the name of your IoT hub.</span></span> <span data-ttu-id="2822a-106">Si le nom saisi est valide, une coche verte s’affiche.</span><span class="sxs-lookup"><span data-stu-id="2822a-106">If the name you enter is valid, a green check mark appears.</span></span>

     <span data-ttu-id="2822a-107">**Niveau de tarification et de mise à l’échelle** : sélectionnez le niveau **F1 gratuit**.</span><span class="sxs-lookup"><span data-stu-id="2822a-107">**Pricing and scale tier**: Select the **F1 - Free** tier.</span></span> <span data-ttu-id="2822a-108">Cette option suffit pour cette démonstration.</span><span class="sxs-lookup"><span data-stu-id="2822a-108">This option is sufficient for this demo.</span></span> <span data-ttu-id="2822a-109">Pour plus d’informations, consultez [Niveau de tarification et de mise à l’échelle](https://azure.microsoft.com/pricing/details/iot-hub/).</span><span class="sxs-lookup"><span data-stu-id="2822a-109">For more information, see the [Pricing and scale tier](https://azure.microsoft.com/pricing/details/iot-hub/).</span></span>

     <span data-ttu-id="2822a-110">**Groupe de ressources** : créez un groupe de ressources pour héberger l’IoT Hub ou utilisez-en un existant.</span><span class="sxs-lookup"><span data-stu-id="2822a-110">**Resource group**: Create a resource group to host the IoT hub or use an existing one.</span></span> <span data-ttu-id="2822a-111">Pour plus d’informations, consultez [Utilisation des groupes de ressources pour gérer vos ressources Azure](../articles/azure-resource-manager/resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="2822a-111">For more information, see [Use resource groups to manage your Azure resources](../articles/azure-resource-manager/resource-group-portal.md).</span></span>

     <span data-ttu-id="2822a-112">**Emplacement** : sélectionnez l’emplacement le plus proche de l’endroit où vous créez l’IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="2822a-112">**Location**: Select the closest location to you where the IoT hub is created.</span></span>

     <span data-ttu-id="2822a-113">**Épingler au tableau de bord** : Sélectionnez cette option pour pouvoir accéder facilement à votre instance IoT Hub à partir du tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="2822a-113">**Pin to dashboard**: Select this option for easy access to your IoT hub from the dashboard.</span></span>

   ![Entrer des informations pour créer votre IoT hub](../articles/iot-hub/media/iot-hub-create-hub-and-device/2_fill-in-fields-for-azure-iot-hub-portal.png)

   [!INCLUDE [iot-hub-pii-note-naming-hub](iot-hub-pii-note-naming-hub.md)]

3. <span data-ttu-id="2822a-115">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="2822a-115">Click **Create**.</span></span> <span data-ttu-id="2822a-116">La création de votre IoT Hub peut prendre plusieurs minutes.</span><span class="sxs-lookup"><span data-stu-id="2822a-116">Your IoT hub might take a few minutes to create.</span></span> <span data-ttu-id="2822a-117">Vous pouvez suivre la progression dans le volet **Notifications**.</span><span class="sxs-lookup"><span data-stu-id="2822a-117">You can see progress in the **Notifications** pane.</span></span>

   ![Voir les notifications de progression de votre IoT Hub](../articles/iot-hub/media/iot-hub-create-hub-and-device/3_notification-azure-iot-hub-creation-progress-portal.png)

4. <span data-ttu-id="2822a-119">Une fois votre IoT Hub créé, cliquez dessus dans le tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="2822a-119">After your IoT hub is created, click it on the dashboard.</span></span> <span data-ttu-id="2822a-120">Notez la valeur **Hostname**, puis cliquez sur **Stratégies d’accès partagé**.</span><span class="sxs-lookup"><span data-stu-id="2822a-120">Make a note of the **Hostname**, and then click **Shared access policies**.</span></span>

   ![Obtention du nom d’hôte de votre IoT Hub](../articles/iot-hub/media/iot-hub-create-hub-and-device/4_get-azure-iot-hub-hostname-portal.png)

5. <span data-ttu-id="2822a-122">Dans le volet **Stratégies d’accès partagé**, cliquez sur la stratégie **iothubowner**, puis copiez et notez la **chaîne de connexion** de votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="2822a-122">In the **Shared access policies** pane, click the **iothubowner** policy, and then copy and make a note of the **Connection string** of your IoT hub.</span></span> <span data-ttu-id="2822a-123">Pour plus d’informations, consultez [Contrôler l’accès à IoT Hub](../articles/iot-hub/iot-hub-devguide-security.md).</span><span class="sxs-lookup"><span data-stu-id="2822a-123">For more information, see [Control access to IoT Hub](../articles/iot-hub/iot-hub-devguide-security.md).</span></span>

> [!NOTE] 
<span data-ttu-id="2822a-124">Vous n’aurez pas besoin de cette chaîne de connexion iothubowner pour ce didacticiel d’installation.</span><span class="sxs-lookup"><span data-stu-id="2822a-124">You will not need this iothubowner connection string for this set-up tutorial.</span></span> <span data-ttu-id="2822a-125">Toutefois, elle vous sera peut-être nécessaire pour certains didacticiels présentant différents scénarios IoT une fois cette installation terminée.</span><span class="sxs-lookup"><span data-stu-id="2822a-125">However, you may need it for some of the tutorials on different IoT scenarios after you complete this set-up.</span></span>

   ![Obtention de la chaîne de connexion de votre IoT Hub](../articles/iot-hub/media/iot-hub-create-hub-and-device/5_get-azure-iot-hub-connection-string-portal.png)

## <a name="register-a-device-in-the-iot-hub-for-your-device"></a><span data-ttu-id="2822a-127">Inscrire un appareil dans l’IoT Hub pour votre appareil</span><span class="sxs-lookup"><span data-stu-id="2822a-127">Register a device in the IoT hub for your device</span></span>

1. <span data-ttu-id="2822a-128">Dans le [portail Azure](https://portal.azure.com/), ouvrez votre instance IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="2822a-128">In the [Azure portal](https://portal.azure.com/), open your IoT hub.</span></span>

2. <span data-ttu-id="2822a-129">Cliquez sur **Explorateur d’appareils**.</span><span class="sxs-lookup"><span data-stu-id="2822a-129">Click **Device Explorer**.</span></span>
3. <span data-ttu-id="2822a-130">Dans le volet Explorateur d’appareils, cliquez sur **Ajouter** pour ajouter un appareil à votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="2822a-130">In the Device Explorer pane, click **Add** to add a device to your IoT hub.</span></span> <span data-ttu-id="2822a-131">Faites ensuite ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="2822a-131">Then do the following:</span></span>

   <span data-ttu-id="2822a-132">**ID d’appareil** : entrez l’ID du nouvel appareil.</span><span class="sxs-lookup"><span data-stu-id="2822a-132">**Device ID**: Enter the ID of the new device.</span></span> <span data-ttu-id="2822a-133">Les ID d’appareil respectent la casse.</span><span class="sxs-lookup"><span data-stu-id="2822a-133">Device IDs are case sensitive.</span></span>

   <span data-ttu-id="2822a-134">**Type d’authentification** : sélectionnez **Clé symétrique**.</span><span class="sxs-lookup"><span data-stu-id="2822a-134">**Authentication Type**: Select **Symmetric Key**.</span></span>

   <span data-ttu-id="2822a-135">**Générer automatiquement les clés** : cochez cette case.</span><span class="sxs-lookup"><span data-stu-id="2822a-135">**Auto Generate Keys**: Select this check box.</span></span>

   <span data-ttu-id="2822a-136">**Connecter l’appareil à IoT Hub** : cliquez sur **Activer**.</span><span class="sxs-lookup"><span data-stu-id="2822a-136">**Connect device to IoT Hub**: Click **Enable**.</span></span>

   ![Ajouter un appareil dans l’outil Device Explorer de votre IoT Hub](../articles/iot-hub/media/iot-hub-create-hub-and-device/6_add-device-in-azure-iot-hub-device-explorer-portal.png)

   [!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

4. <span data-ttu-id="2822a-138">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="2822a-138">Click **Save**.</span></span>
5. <span data-ttu-id="2822a-139">Une fois que l’appareil est créé, ouvrez-le dans le volet **Explorateur d’appareils**.</span><span class="sxs-lookup"><span data-stu-id="2822a-139">After the device is created, open the device in the **Device Explorer** pane.</span></span>
6. <span data-ttu-id="2822a-140">Notez la clé primaire de la chaîne de connexion.</span><span class="sxs-lookup"><span data-stu-id="2822a-140">Make a note of the primary key of the connection string.</span></span>

   ![Obtention de la chaîne de connexion de l’appareil](../articles/iot-hub/media/iot-hub-create-hub-and-device/7_get-device-connection-string-in-device-explorer-portal.png)
