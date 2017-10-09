## <a name="create-an-iot-hub"></a><span data-ttu-id="fee83-101">Créer un hub IoT</span><span class="sxs-lookup"><span data-stu-id="fee83-101">Create an IoT hub</span></span>
<span data-ttu-id="fee83-102">Créez un hub IoT pour votre tooconnect d’application appareil simulé à.</span><span class="sxs-lookup"><span data-stu-id="fee83-102">Create an IoT hub for your simulated device app tooconnect to.</span></span> <span data-ttu-id="fee83-103">Hello étapes suivantes vous montrent comment toocomplete cette tâche à l’aide de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="fee83-103">hello following steps show you how toocomplete this task by using hello Azure portal.</span></span>

1. <span data-ttu-id="fee83-104">Connectez-vous à toohello [portail Azure][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="fee83-104">Sign in toohello [Azure portal][lnk-portal].</span></span>
1. <span data-ttu-id="fee83-105">Bonjour Jumpbar, cliquez sur **nouveau** > **Internet of Things** > **IoT Hub**.</span><span class="sxs-lookup"><span data-stu-id="fee83-105">In hello Jumpbar, click **New** > **Internet of Things** > **IoT Hub**.</span></span>
   
    ![Barre de lancement du portail Azure][1]
1. <span data-ttu-id="fee83-107">Bonjour **IoT hub** panneau, choisissez configuration hello pour votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="fee83-107">In hello **IoT hub** blade, choose hello configuration for your IoT hub.</span></span>
   
    ![Panneau IoT Hub][2]
   
   1. <span data-ttu-id="fee83-109">Bonjour **nom** , entrez un nom pour votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="fee83-109">In hello **Name** box, enter a name for your IoT hub.</span></span> <span data-ttu-id="fee83-110">Si hello **nom** n’est valide et disponible, une coche verte s’affiche dans hello **nom** boîte.</span><span class="sxs-lookup"><span data-stu-id="fee83-110">If hello **Name** is valid and available, a green check mark appears in hello **Name** box.</span></span>
    [!INCLUDE [iot-hub-pii-note-naming-hub](iot-hub-pii-note-naming-hub.md)]
   
   1. <span data-ttu-id="fee83-111">Sélectionnez une [tarification et un niveau de mise à l’échelle][lnk-pricing].</span><span class="sxs-lookup"><span data-stu-id="fee83-111">Select a [pricing and scale tier][lnk-pricing].</span></span> <span data-ttu-id="fee83-112">Ce didacticiel ne nécessite pas un niveau spécifique.</span><span class="sxs-lookup"><span data-stu-id="fee83-112">This tutorial does not require a specific tier.</span></span> <span data-ttu-id="fee83-113">Pour ce didacticiel, utilisez le gratuit F1 hello.</span><span class="sxs-lookup"><span data-stu-id="fee83-113">For this tutorial, use hello free F1 tier.</span></span>
   1. <span data-ttu-id="fee83-114">Dans **Groupe de ressources**, créez un groupe de ressources ou sélectionnez un groupe existant.</span><span class="sxs-lookup"><span data-stu-id="fee83-114">In **Resource group**, either create a resource group, or select an existing one.</span></span> <span data-ttu-id="fee83-115">Pour plus d’informations, consultez [à l’aide de la ressource groupes toomanage vos ressources Azure][lnk-resource-groups].</span><span class="sxs-lookup"><span data-stu-id="fee83-115">For more information, see [Using resource groups toomanage your Azure resources][lnk-resource-groups].</span></span>
   1. <span data-ttu-id="fee83-116">Dans **emplacement**, sélectionnez hello emplacement toohost votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="fee83-116">In **Location**, select hello location toohost your IoT hub.</span></span> <span data-ttu-id="fee83-117">Pour ce didacticiel, choisissez l’emplacement le plus proche.</span><span class="sxs-lookup"><span data-stu-id="fee83-117">For this tutorial, choose your nearest location.</span></span>
1. <span data-ttu-id="fee83-118">Une fois que vous avez choisi les options de configuration de votre hub IoT, cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="fee83-118">When you have chosen your IoT hub configuration options, click **Create**.</span></span>  <span data-ttu-id="fee83-119">Il peut prendre quelques minutes pour Azure toocreate votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="fee83-119">It can take a few minutes for Azure toocreate your IoT hub.</span></span> <span data-ttu-id="fee83-120">état de hello toocheck, vous pouvez surveiller progression hello sur hello tableau d’accueil ou dans le panneau de configuration de Notifications hello.</span><span class="sxs-lookup"><span data-stu-id="fee83-120">toocheck hello status, you can monitor hello progress on hello Startboard or in hello Notifications panel.</span></span>
   
    ![Nouveau statut IoT Hub][3]
1. <span data-ttu-id="fee83-122">Lorsque le hub IoT de hello a été créé avec succès, cliquez sur hello nouvelle vignette représentant votre hub IoT dans Panneau de hello hello tooopen portail Azure pour le nouveau concentrateur de IoT hello.</span><span class="sxs-lookup"><span data-stu-id="fee83-122">When hello IoT hub has been created successfully, click hello new tile for your IoT hub in hello Azure portal tooopen hello blade for hello new IoT hub.</span></span> <span data-ttu-id="fee83-123">Prenez note de hello **nom d’hôte**, puis cliquez sur **les stratégies d’accès partagé**.</span><span class="sxs-lookup"><span data-stu-id="fee83-123">Make a note of hello **Hostname**, and then click **Shared access policies**.</span></span>
   
    ![Nouveau panneau IoT Hub][4]
1. <span data-ttu-id="fee83-125">Bonjour **les stratégies d’accès partagé** panneau, cliquez sur hello **iothubowner** stratégie, puis copiez et prenez note de hello chaîne de connexion de IoT Hub Bonjour **iothubowner** panneau.</span><span class="sxs-lookup"><span data-stu-id="fee83-125">In hello **Shared access policies** blade, click hello **iothubowner** policy, and then copy and make note of hello IoT Hub connection string in hello **iothubowner** blade.</span></span> <span data-ttu-id="fee83-126">Pour plus d’informations, consultez [le contrôle d’accès] [ lnk-access-control] Bonjour « Guide du développeur IoT Hub ».</span><span class="sxs-lookup"><span data-stu-id="fee83-126">For more information, see [Access control][lnk-access-control] in hello "IoT Hub developer guide."</span></span>
   
    ![Panneau des stratégies d’accès partagées][5]

<!-- Images. -->
[1]: ./media/iot-hub-get-started-create-hub/create-iot-hub1.png
[2]: ./media/iot-hub-get-started-create-hub/create-iot-hub2.png
[3]: ./media/iot-hub-get-started-create-hub/create-iot-hub3.png
[4]: ./media/iot-hub-get-started-create-hub/create-iot-hub4.png
[5]: ./media/iot-hub-get-started-create-hub/create-iot-hub5.png

<!-- Links -->
[lnk-resource-groups]: ../articles/azure-resource-manager/resource-group-portal.md
[lnk-portal]: https://portal.azure.com/
[lnk-pricing]: https://azure.microsoft.com/pricing/details/iot-hub/
[lnk-access-control]: ../articles/iot-hub/iot-hub-devguide-security.md
