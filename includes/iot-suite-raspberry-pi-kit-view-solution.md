## <a name="view-hello-solution-dashboard"></a><span data-ttu-id="ad37b-101">Tableau de bord View hello solution</span><span class="sxs-lookup"><span data-stu-id="ad37b-101">View hello solution dashboard</span></span>

<span data-ttu-id="ad37b-102">tableau de bord Hello solution vous permet de solution de hello déployé toomanage.</span><span class="sxs-lookup"><span data-stu-id="ad37b-102">hello solution dashboard enables you toomanage hello deployed solution.</span></span> <span data-ttu-id="ad37b-103">Par exemple, vous pouvez afficher les données de télémétrie, ajouter des appareils et appeler des méthodes.</span><span class="sxs-lookup"><span data-stu-id="ad37b-103">For example, you can view telemetry, add devices, and invoke methods.</span></span>

1. <span data-ttu-id="ad37b-104">Lorsque l’approvisionnement hello est terminé et vignette hello pour votre solution préconfigurée indique **prêt**, choisissez **lancer** tooopen votre portail de solution de surveillance à distance dans un nouvel onglet.</span><span class="sxs-lookup"><span data-stu-id="ad37b-104">When hello provisioning is complete and hello tile for your preconfigured solution indicates **Ready**, choose **Launch** tooopen your remote monitoring solution portal in a new tab.</span></span>

    ![Lancer la solution de hello préconfiguré][img-launch-solution]

1. <span data-ttu-id="ad37b-106">Par défaut, portail de solution hello affiche hello *tableau de bord*.</span><span class="sxs-lookup"><span data-stu-id="ad37b-106">By default, hello solution portal shows hello *dashboard*.</span></span> <span data-ttu-id="ad37b-107">Vous pouvez naviguer tooother des zones du portail de solution hello à l’aide du menu de hello sur la partie gauche de la page de hello hello.</span><span class="sxs-lookup"><span data-stu-id="ad37b-107">You can navigate tooother areas of hello solution portal using hello menu on hello left-hand side of hello page.</span></span>

    ![Tableau de bord de solution préconfigurée de surveillance à distance][img-menu]

## <a name="add-a-device"></a><span data-ttu-id="ad37b-109">Ajout d’un appareil</span><span class="sxs-lookup"><span data-stu-id="ad37b-109">Add a device</span></span>

<span data-ttu-id="ad37b-110">Pour une solution toohello préconfiguré tooconnect des appareils, il doit s’identifier tooIoT concentrateur à l’aide des informations d’identification valides.</span><span class="sxs-lookup"><span data-stu-id="ad37b-110">For a device tooconnect toohello preconfigured solution, it must identify itself tooIoT Hub using valid credentials.</span></span> <span data-ttu-id="ad37b-111">Vous pouvez récupérer les informations d’identification de périphérique hello à partir du tableau de bord de solution hello.</span><span class="sxs-lookup"><span data-stu-id="ad37b-111">You can retrieve hello device credentials from hello solution dashboard.</span></span> <span data-ttu-id="ad37b-112">Pour inclure des informations d’identification de périphérique hello dans votre application cliente, plus loin dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="ad37b-112">You include hello device credentials in your client application later in this tutorial.</span></span>

<span data-ttu-id="ad37b-113">Si vous n’avez pas déjà fait, ajoutez une solution d’analyse à distance tooyour périphérique personnalisés.</span><span class="sxs-lookup"><span data-stu-id="ad37b-113">If you haven't already done so, add a custom device tooyour remote monitoring solution.</span></span> <span data-ttu-id="ad37b-114">Hello terminée dans le tableau de bord de solution hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="ad37b-114">Complete hello following steps in hello solution dashboard:</span></span>

1. <span data-ttu-id="ad37b-115">Dans hello coin inférieur gauche du tableau de bord hello, cliquez sur **ajouter un périphérique**.</span><span class="sxs-lookup"><span data-stu-id="ad37b-115">In hello lower left-hand corner of hello dashboard, click **Add a device**.</span></span>

   ![Ajout d’un appareil][1]

1. <span data-ttu-id="ad37b-117">Bonjour **personnalisé appareil** du panneau, cliquez sur **ajouter un nouveau**.</span><span class="sxs-lookup"><span data-stu-id="ad37b-117">In hello **Custom Device** panel, click **Add new**.</span></span>

   ![Ajout d’un appareil personnalisé][2]

1. <span data-ttu-id="ad37b-119">Choisissez **Me laisser définir mon propre ID d'appareil**.</span><span class="sxs-lookup"><span data-stu-id="ad37b-119">Choose **Let me define my own Device ID**.</span></span> <span data-ttu-id="ad37b-120">Entrez un ID de périphérique tel **rasppi**, cliquez sur **vérifier l’ID** tooverify vous n’avez pas déjà utilisé le nom de hello dans votre solution, puis cliquez sur **créer** appareil de hello tooprovision.</span><span class="sxs-lookup"><span data-stu-id="ad37b-120">Enter a Device ID such as **rasppi**, click **Check ID** tooverify you haven't already used hello name in your solution, and then click **Create** tooprovision hello device.</span></span>

   ![Ajouter ID d’appareil][3]

1. <span data-ttu-id="ad37b-122">Rendre un périphérique de hello Remarque informations d’identification (**ID de périphérique**, **nom d’hôte du Hub IoT**, et **clé de périphérique**).</span><span class="sxs-lookup"><span data-stu-id="ad37b-122">Make a note hello device credentials (**Device ID**, **IoT Hub Hostname**, and **Device Key**).</span></span> <span data-ttu-id="ad37b-123">Votre application cliente sur hello framboises Pi doit ces toohello tooconnect de valeurs solution de surveillance à distance.</span><span class="sxs-lookup"><span data-stu-id="ad37b-123">Your client application on hello Raspberry Pi needs these values tooconnect toohello remote monitoring solution.</span></span> <span data-ttu-id="ad37b-124">Cliquez ensuite sur **Terminé**.</span><span class="sxs-lookup"><span data-stu-id="ad37b-124">Then click **Done**.</span></span>

    ![Afficher les informations d’identification d’un appareil][4]

1. <span data-ttu-id="ad37b-126">Sélectionnez votre appareil dans la liste des appareils hello dans le tableau de bord de solution hello.</span><span class="sxs-lookup"><span data-stu-id="ad37b-126">Select your device in hello device list in hello solution dashboard.</span></span> <span data-ttu-id="ad37b-127">Ensuite, dans hello **détails de l’appareil** du panneau, cliquez sur **activer le périphérique**.</span><span class="sxs-lookup"><span data-stu-id="ad37b-127">Then, in hello **Device Details** panel, click **Enable Device**.</span></span> <span data-ttu-id="ad37b-128">Hello de votre appareil est maintenant **en cours d’exécution**.</span><span class="sxs-lookup"><span data-stu-id="ad37b-128">hello status of your device is now **Running**.</span></span> <span data-ttu-id="ad37b-129">solution de surveillance à distance Hello peut maintenant recevoir les données de télémétrie à partir de votre appareil et d’appeler des méthodes sur l’appareil de hello.</span><span class="sxs-lookup"><span data-stu-id="ad37b-129">hello remote monitoring solution can now receive telemetry from your device and invoke methods on hello device.</span></span>

[img-launch-solution]: media/iot-suite-raspberry-pi-kit-view-solution/launch.png
[img-menu]: media/iot-suite-raspberry-pi-kit-view-solution/menu.png
[1]: media/iot-suite-raspberry-pi-kit-view-solution/suite0.png
[2]: media/iot-suite-raspberry-pi-kit-view-solution/suite1.png
[3]: media/iot-suite-raspberry-pi-kit-view-solution/suite2.png
[4]: media/iot-suite-raspberry-pi-kit-view-solution/suite3.png