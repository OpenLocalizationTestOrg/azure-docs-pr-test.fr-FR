## <a name="view-the-solution-dashboard"></a><span data-ttu-id="634b2-101">Afficher le tableau de bord de solution</span><span class="sxs-lookup"><span data-stu-id="634b2-101">View the solution dashboard</span></span>

<span data-ttu-id="634b2-102">Grâce au tableau de bord de solution, vous pouvez gérer la solution déployée.</span><span class="sxs-lookup"><span data-stu-id="634b2-102">The solution dashboard enables you to manage the deployed solution.</span></span> <span data-ttu-id="634b2-103">Par exemple, vous pouvez afficher les données de télémétrie, ajouter des appareils et appeler des méthodes.</span><span class="sxs-lookup"><span data-stu-id="634b2-103">For example, you can view telemetry, add devices, and invoke methods.</span></span>

1. <span data-ttu-id="634b2-104">Une fois que l’approvisionnement est terminé et que la vignette de votre solution préconfigurée indique **Prêt**, choisissez **Lancer** pour ouvrir le portail de votre solution de surveillance à distance dans un nouvel onglet.</span><span class="sxs-lookup"><span data-stu-id="634b2-104">When the provisioning is complete and the tile for your preconfigured solution indicates **Ready**, choose **Launch** to open your remote monitoring solution portal in a new tab.</span></span>

    ![Lancer la solution préconfigurée][img-launch-solution]

1. <span data-ttu-id="634b2-106">Par défaut, le portail de solution affiche le *tableau de bord*.</span><span class="sxs-lookup"><span data-stu-id="634b2-106">By default, the solution portal shows the *dashboard*.</span></span> <span data-ttu-id="634b2-107">Accédez à d’autres zones du portail de solution à l’aide du menu sur le côté gauche de la page.</span><span class="sxs-lookup"><span data-stu-id="634b2-107">Navigate to other areas of the solution portal using the menu on the left-hand side of the page.</span></span>

    ![Tableau de bord de solution préconfigurée de surveillance à distance][img-menu]

## <a name="add-a-device"></a><span data-ttu-id="634b2-109">Ajout d’un appareil</span><span class="sxs-lookup"><span data-stu-id="634b2-109">Add a device</span></span>

<span data-ttu-id="634b2-110">Pour qu’un appareil puisse se connecter à la solution préconfigurée, il doit s’identifier auprès d’IoT Hub à l’aide d’informations d’identification valides.</span><span class="sxs-lookup"><span data-stu-id="634b2-110">For a device to connect to the preconfigured solution, it must identify itself to IoT Hub using valid credentials.</span></span> <span data-ttu-id="634b2-111">Vous pouvez récupérer les informations d’identification de l’appareil à partir du tableau de bord de la solution.</span><span class="sxs-lookup"><span data-stu-id="634b2-111">You can retrieve the device credentials from the solution dashboard.</span></span> <span data-ttu-id="634b2-112">Les informations d’identification de l’appareil seront ajoutées dans votre application cliente dans la suite de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="634b2-112">You include the device credentials in your client application later in this tutorial.</span></span>

<span data-ttu-id="634b2-113">Pour ajouter un appareil à votre solution de surveillance à distance, procédez comme suit dans le tableau de bord de la solution :</span><span class="sxs-lookup"><span data-stu-id="634b2-113">To add a device to your remote monitoring solution, complete the following steps in the solution dashboard:</span></span>

1. <span data-ttu-id="634b2-114">Dans le coin inférieur gauche du tableau de bord, cliquez sur **Ajouter un périphérique**.</span><span class="sxs-lookup"><span data-stu-id="634b2-114">In the lower left-hand corner of the dashboard, click **Add a device**.</span></span>

   ![Ajout d’un appareil][1]

1. <span data-ttu-id="634b2-116">Dans le panneau **Appareil personnalisé**, cliquez sur **Ajouter nouveau**.</span><span class="sxs-lookup"><span data-stu-id="634b2-116">In the **Custom Device** panel, click **Add new**.</span></span>

   ![Ajout d’un appareil personnalisé][2]

1. <span data-ttu-id="634b2-118">Choisissez **Me laisser définir mon propre ID d'appareil**.</span><span class="sxs-lookup"><span data-stu-id="634b2-118">Choose **Let me define my own Device ID**.</span></span> <span data-ttu-id="634b2-119">Entrez un ID d’appareil comme **device01**, cliquez sur **Vérifier l’ID** pour vous assurer que ce nom n’est pas déjà utilisé dans votre solution, puis cliquez sur **Créer** pour approvisionner l’appareil.</span><span class="sxs-lookup"><span data-stu-id="634b2-119">Enter a Device ID such as **device01**, click **Check ID** to verify you haven't already used the name in your solution, and then click **Create** to provision the device.</span></span>

   ![Ajouter ID d’appareil][3]

1. <span data-ttu-id="634b2-121">Prenez note des informations d’identification de l’appareil (**ID d’appareil**, **nom d’hôte IoT Hub** et **clé d’appareil**).</span><span class="sxs-lookup"><span data-stu-id="634b2-121">Make a note the device credentials (**Device ID**, **IoT Hub Hostname**, and **Device Key**).</span></span> <span data-ttu-id="634b2-122">Votre application cliente sur Intel NUC a besoin de ces valeurs pour se connecter à la solution de surveillance à distance.</span><span class="sxs-lookup"><span data-stu-id="634b2-122">Your client application on the Intel NUC needs these values to connect to the remote monitoring solution.</span></span> <span data-ttu-id="634b2-123">Cliquez ensuite sur **Terminé**.</span><span class="sxs-lookup"><span data-stu-id="634b2-123">Then click **Done**.</span></span>

    ![Afficher les informations d’identification d’un appareil][4]

1. <span data-ttu-id="634b2-125">Sélectionnez votre appareil dans la liste d’appareils du tableau de bord de la solution.</span><span class="sxs-lookup"><span data-stu-id="634b2-125">Select your device in the device list in the solution dashboard.</span></span> <span data-ttu-id="634b2-126">Ensuite, dans le panneau **Détails de l’appareil**, cliquez sur **Activer l’appareil**.</span><span class="sxs-lookup"><span data-stu-id="634b2-126">Then, in the **Device Details** panel, click **Enable Device**.</span></span> <span data-ttu-id="634b2-127">L’état de votre appareil est maintenant **En cours d’exécution**.</span><span class="sxs-lookup"><span data-stu-id="634b2-127">The status of your device is now **Running**.</span></span> <span data-ttu-id="634b2-128">La solution de surveillance à distance peut désormais recevoir des données de télémétrie à partir de votre appareil et appeler des méthodes sur l’appareil.</span><span class="sxs-lookup"><span data-stu-id="634b2-128">The remote monitoring solution can now receive telemetry from your device and invoke methods on the device.</span></span>

[img-launch-solution]: media/iot-suite-gateway-kit-view-solution/launch.png
[img-menu]: media/iot-suite-gateway-kit-view-solution/menu.png
[1]: media/iot-suite-gateway-kit-view-solution/suite0.png
[2]: media/iot-suite-gateway-kit-view-solution/suite1.png
[3]: media/iot-suite-gateway-kit-view-solution/suite2.png
[4]: media/iot-suite-gateway-kit-view-solution/suite3.png