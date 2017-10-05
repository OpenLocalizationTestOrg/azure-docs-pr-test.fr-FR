## <a name="create-an-iot-hub"></a><span data-ttu-id="34723-101">Créer un hub IoT</span><span class="sxs-lookup"><span data-stu-id="34723-101">Create an IoT hub</span></span>
<span data-ttu-id="34723-102">Créez un IoT Hub pour que votre application de périphérique simulé puisse se connecter.</span><span class="sxs-lookup"><span data-stu-id="34723-102">Create an IoT hub for your simulated device app to connect to.</span></span> <span data-ttu-id="34723-103">Les étapes suivantes vous montrent comment exécuter cette tâche à l’aide du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="34723-103">The following steps show you how to complete this task by using the Azure portal.</span></span>

1. <span data-ttu-id="34723-104">Connectez-vous au [portail Azure][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="34723-104">Sign in to the [Azure portal][lnk-portal].</span></span>
1. <span data-ttu-id="34723-105">Dans la barre de lancement, cliquez sur **Nouveau** > **Internet des objets** > **Azure IoT Hub**.</span><span class="sxs-lookup"><span data-stu-id="34723-105">In the Jumpbar, click **New** > **Internet of Things** > **IoT Hub**.</span></span>
   
    ![Barre de lancement du portail Azure][1]
1. <span data-ttu-id="34723-107">Dans le panneau **IoT hub** , choisissez la configuration de votre concentrateur IoT.</span><span class="sxs-lookup"><span data-stu-id="34723-107">In the **IoT hub** blade, choose the configuration for your IoT hub.</span></span>
   
    ![Panneau IoT Hub][2]
   
   1. <span data-ttu-id="34723-109">Dans la zone **Nom** , saisissez un nom pour identifier votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="34723-109">In the **Name** box, enter a name for your IoT hub.</span></span> <span data-ttu-id="34723-110">Une fois le **Nom** validé et disponible, une coche verte apparaît dans la case **Nom**.</span><span class="sxs-lookup"><span data-stu-id="34723-110">If the **Name** is valid and available, a green check mark appears in the **Name** box.</span></span>
    [!INCLUDE [iot-hub-pii-note-naming-hub](iot-hub-pii-note-naming-hub.md)]
   
   1. <span data-ttu-id="34723-111">Sélectionnez une [tarification et un niveau de mise à l’échelle][lnk-pricing].</span><span class="sxs-lookup"><span data-stu-id="34723-111">Select a [pricing and scale tier][lnk-pricing].</span></span> <span data-ttu-id="34723-112">Ce didacticiel ne nécessite pas un niveau spécifique.</span><span class="sxs-lookup"><span data-stu-id="34723-112">This tutorial does not require a specific tier.</span></span> <span data-ttu-id="34723-113">Pour ce didacticiel, utilisez le niveau F1 gratuit.</span><span class="sxs-lookup"><span data-stu-id="34723-113">For this tutorial, use the free F1 tier.</span></span>
   1. <span data-ttu-id="34723-114">Dans **Groupe de ressources**, créez un groupe de ressources ou sélectionnez un groupe existant.</span><span class="sxs-lookup"><span data-stu-id="34723-114">In **Resource group**, either create a resource group, or select an existing one.</span></span> <span data-ttu-id="34723-115">Pour plus d’informations, consultez [Utilisation des groupes de ressources pour gérer vos ressources Azure][lnk-resource-groups].</span><span class="sxs-lookup"><span data-stu-id="34723-115">For more information, see [Using resource groups to manage your Azure resources][lnk-resource-groups].</span></span>
   1. <span data-ttu-id="34723-116">Dans **Emplacement**, sélectionnez l’emplacement destiné à héberger votre concentrateur IoT.</span><span class="sxs-lookup"><span data-stu-id="34723-116">In **Location**, select the location to host your IoT hub.</span></span> <span data-ttu-id="34723-117">Pour ce didacticiel, choisissez l’emplacement le plus proche.</span><span class="sxs-lookup"><span data-stu-id="34723-117">For this tutorial, choose your nearest location.</span></span>
1. <span data-ttu-id="34723-118">Une fois que vous avez choisi les options de configuration de votre hub IoT, cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="34723-118">When you have chosen your IoT hub configuration options, click **Create**.</span></span>  <span data-ttu-id="34723-119">La création du hub IoT par Azure peut prendre plusieurs minutes.</span><span class="sxs-lookup"><span data-stu-id="34723-119">It can take a few minutes for Azure to create your IoT hub.</span></span> <span data-ttu-id="34723-120">Pour vérifier l’état d’avancement de l’opération, vous pouvez consulter le tableau d’accueil ou le panneau Notifications.</span><span class="sxs-lookup"><span data-stu-id="34723-120">To check the status, you can monitor the progress on the Startboard or in the Notifications panel.</span></span>
   
    ![Nouveau statut IoT Hub][3]
1. <span data-ttu-id="34723-122">Lorsque l’IoT hub a été créé avec succès, cliquez sur la nouvelle vignette représentant votre IoT hub dans le portail Azure pour ouvrir le panneau du nouveau IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="34723-122">When the IoT hub has been created successfully, click the new tile for your IoT hub in the Azure portal to open the blade for the new IoT hub.</span></span> <span data-ttu-id="34723-123">Notez la valeur **Hostname**, puis cliquez sur **Stratégies d’accès partagé**.</span><span class="sxs-lookup"><span data-stu-id="34723-123">Make a note of the **Hostname**, and then click **Shared access policies**.</span></span>
   
    ![Nouveau panneau IoT Hub][4]
1. <span data-ttu-id="34723-125">Dans le panneau **Stratégies d’accès partagé**, cliquez sur la stratégie **iothubowner**, puis copiez et notez la chaîne de connexion IoT Hub dans le panneau **iothubowner**.</span><span class="sxs-lookup"><span data-stu-id="34723-125">In the **Shared access policies** blade, click the **iothubowner** policy, and then copy and make note of the IoT Hub connection string in the **iothubowner** blade.</span></span> <span data-ttu-id="34723-126">Consultez la rubrique [Access Control][lnk-access-control] du « Guide du développeur IoT Hub » pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="34723-126">For more information, see [Access control][lnk-access-control] in the "IoT Hub developer guide."</span></span>
   
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
