> [!div class="op_single_selector"]
> * [<span data-ttu-id="50d1d-101">C sur Windows</span><span class="sxs-lookup"><span data-stu-id="50d1d-101">C on Windows</span></span>](../articles/iot-suite/iot-suite-connecting-devices.md)
> * [<span data-ttu-id="50d1d-102">C sur Linux</span><span class="sxs-lookup"><span data-stu-id="50d1d-102">C on Linux</span></span>](../articles/iot-suite/iot-suite-connecting-devices-linux.md)
> * [<span data-ttu-id="50d1d-103">Node.JS</span><span class="sxs-lookup"><span data-stu-id="50d1d-103">Node.js</span></span>](../articles/iot-suite/iot-suite-connecting-devices-node.md)
> 
> 

## <a name="scenario-overview"></a><span data-ttu-id="50d1d-104">Présentation du scénario</span><span class="sxs-lookup"><span data-stu-id="50d1d-104">Scenario overview</span></span>
<span data-ttu-id="50d1d-105">Dans ce scénario, vous créez un périphérique qui envoie hello suivant la surveillance à distance de télémétrie toohello [solution préconfigurée][lnk-what-are-preconfig-solutions]:</span><span class="sxs-lookup"><span data-stu-id="50d1d-105">In this scenario, you create a device that sends hello following telemetry toohello remote monitoring [preconfigured solution][lnk-what-are-preconfig-solutions]:</span></span>

* <span data-ttu-id="50d1d-106">Température externe</span><span class="sxs-lookup"><span data-stu-id="50d1d-106">External temperature</span></span>
* <span data-ttu-id="50d1d-107">Température interne</span><span class="sxs-lookup"><span data-stu-id="50d1d-107">Internal temperature</span></span>
* <span data-ttu-id="50d1d-108">Humidité</span><span class="sxs-lookup"><span data-stu-id="50d1d-108">Humidity</span></span>

<span data-ttu-id="50d1d-109">Par souci de simplicité, code hello sur l’appareil de hello génère des exemples de valeurs, mais nous encourageons exemple hello tooextend par connexion réelle capteurs tooyour appareil et l’envoi de télémétrie réel.</span><span class="sxs-lookup"><span data-stu-id="50d1d-109">For simplicity, hello code on hello device generates sample values, but we encourage you tooextend hello sample by connecting real sensors tooyour device and sending real telemetry.</span></span>

<span data-ttu-id="50d1d-110">Hello appareil est également en mesure de toorespond toomethods appelée à partir du tableau de bord de solution hello et souhaitée des valeurs de propriété définies dans le tableau de bord de solution hello.</span><span class="sxs-lookup"><span data-stu-id="50d1d-110">hello device is also able toorespond toomethods invoked from hello solution dashboard and desired property values set in hello solution dashboard.</span></span>

<span data-ttu-id="50d1d-111">toocomplete ce didacticiel, vous avez besoin d’un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="50d1d-111">toocomplete this tutorial, you need an active Azure account.</span></span> <span data-ttu-id="50d1d-112">Si vous ne possédez pas de compte, vous pouvez créer un compte d'évaluation gratuit en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="50d1d-112">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="50d1d-113">Pour plus d’informations, consultez la rubrique [Version d’évaluation gratuite d’Azure][lnk-free-trial].</span><span class="sxs-lookup"><span data-stu-id="50d1d-113">For details, see [Azure Free Trial][lnk-free-trial].</span></span>

## <a name="before-you-start"></a><span data-ttu-id="50d1d-114">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="50d1d-114">Before you start</span></span>
<span data-ttu-id="50d1d-115">Avant d’écrire du code pour votre appareil, vous devez approvisionner votre solution préconfigurée de surveillance à distance et approvisionner un nouvel appareil personnalisé dans cette solution.</span><span class="sxs-lookup"><span data-stu-id="50d1d-115">Before you write any code for your device, you must provision your remote monitoring preconfigured solution and provision a new custom device in that solution.</span></span>

### <a name="provision-your-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="50d1d-116">Approvisionner la solution préconfigurée de surveillance à distance</span><span class="sxs-lookup"><span data-stu-id="50d1d-116">Provision your remote monitoring preconfigured solution</span></span>
<span data-ttu-id="50d1d-117">APPAREIL Hello vous créez dans ce didacticiel envoie instance tooan de données de hello [surveillance à distance] [ lnk-remote-monitoring] solution préconfigurée.</span><span class="sxs-lookup"><span data-stu-id="50d1d-117">hello device you create in this tutorial sends data tooan instance of hello [remote monitoring][lnk-remote-monitoring] preconfigured solution.</span></span> <span data-ttu-id="50d1d-118">Si vous n’avez pas déjà configuré hello solution préconfigurée dans votre compte Azure de surveillance à distance, utilisez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="50d1d-118">If you haven't already provisioned hello remote monitoring preconfigured solution in your Azure account, use hello following steps:</span></span>

1. <span data-ttu-id="50d1d-119">Sur hello <https://www.azureiotsuite.com/> , cliquez sur  **+**  toocreate une solution.</span><span class="sxs-lookup"><span data-stu-id="50d1d-119">On hello <https://www.azureiotsuite.com/> page, click **+** toocreate a solution.</span></span>
2. <span data-ttu-id="50d1d-120">Cliquez sur **sélectionnez** sur hello **surveillance à distance** panneau toocreate votre solution.</span><span class="sxs-lookup"><span data-stu-id="50d1d-120">Click **Select** on hello **Remote monitoring** panel toocreate your solution.</span></span>
3. <span data-ttu-id="50d1d-121">Sur hello **créer distant solutions d’analyse** , entrez un **nom de la Solution** de votre choix, sélectionnez hello **région** vous le souhaitez toodeploy à et sélectionnez hello Azure abonnement toowant toouse.</span><span class="sxs-lookup"><span data-stu-id="50d1d-121">On hello **Create Remote monitoring solution** page, enter a **Solution name** of your choice, select hello **Region** you want toodeploy to, and select hello Azure subscription toowant toouse.</span></span> <span data-ttu-id="50d1d-122">Cliquez ensuite sur **Créer la solution**.</span><span class="sxs-lookup"><span data-stu-id="50d1d-122">Then click **Create solution**.</span></span>
4. <span data-ttu-id="50d1d-123">Attendez que hello processus de configuration est terminée.</span><span class="sxs-lookup"><span data-stu-id="50d1d-123">Wait until hello provisioning process completes.</span></span>

> [!WARNING]
> <span data-ttu-id="50d1d-124">les solutions de Hello préconfiguré utilisent les services Azure facturables.</span><span class="sxs-lookup"><span data-stu-id="50d1d-124">hello preconfigured solutions use billable Azure services.</span></span> <span data-ttu-id="50d1d-125">Veillez tooremove hello solution préconfigurée à partir de votre abonnement lorsque vous avez terminé avec lui tooavoid tous les frais inutiles.</span><span class="sxs-lookup"><span data-stu-id="50d1d-125">Be sure tooremove hello preconfigured solution from your subscription when you are done with it tooavoid any unnecessary charges.</span></span> <span data-ttu-id="50d1d-126">Vous pouvez supprimer complètement une solution préconfigurée de votre abonnement en visitant hello <https://www.azureiotsuite.com/> page.</span><span class="sxs-lookup"><span data-stu-id="50d1d-126">You can completely remove a preconfigured solution from your subscription by visiting hello <https://www.azureiotsuite.com/> page.</span></span>
> 
> 

<span data-ttu-id="50d1d-127">Lorsque hello processus pour hello solution de surveillance à distance de configuration est terminée, cliquez sur **lancer** tooopen hello solution tableau de bord dans votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="50d1d-127">When hello provisioning process for hello remote monitoring solution finishes, click **Launch** tooopen hello solution dashboard in your browser.</span></span>

![Tableau de bord de solution][img-dashboard]

### <a name="provision-your-device-in-hello-remote-monitoring-solution"></a><span data-ttu-id="50d1d-129">Configurer votre appareil dans la solution de surveillance à distance de hello</span><span class="sxs-lookup"><span data-stu-id="50d1d-129">Provision your device in hello remote monitoring solution</span></span>
> [!NOTE]
> <span data-ttu-id="50d1d-130">Si vous avez déjà approvisionné un appareil dans votre solution, vous pouvez ignorer cette étape.</span><span class="sxs-lookup"><span data-stu-id="50d1d-130">If you have already provisioned a device in your solution, you can skip this step.</span></span> <span data-ttu-id="50d1d-131">Vous avez besoin d’informations d’identification de périphérique tooknow hello lorsque vous créez l’application cliente de hello.</span><span class="sxs-lookup"><span data-stu-id="50d1d-131">You need tooknow hello device credentials when you create hello client application.</span></span>
> 
> 

<span data-ttu-id="50d1d-132">Pour une solution toohello préconfiguré tooconnect des appareils, il doit s’identifier tooIoT concentrateur à l’aide des informations d’identification valides.</span><span class="sxs-lookup"><span data-stu-id="50d1d-132">For a device tooconnect toohello preconfigured solution, it must identify itself tooIoT Hub using valid credentials.</span></span> <span data-ttu-id="50d1d-133">Vous pouvez récupérer les informations d’identification de périphérique hello à partir du tableau de bord de solution hello.</span><span class="sxs-lookup"><span data-stu-id="50d1d-133">You can retrieve hello device credentials from hello solution dashboard.</span></span> <span data-ttu-id="50d1d-134">Pour inclure des informations d’identification de périphérique hello dans votre application cliente, plus loin dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="50d1d-134">You include hello device credentials in your client application later in this tutorial.</span></span>

<span data-ttu-id="50d1d-135">tooadd une solution d’analyse à distance tooyour périphérique, hello complet suivant les étapes dans le tableau de bord de solution hello :</span><span class="sxs-lookup"><span data-stu-id="50d1d-135">tooadd a device tooyour remote monitoring solution, complete hello following steps in hello solution dashboard:</span></span>

1. <span data-ttu-id="50d1d-136">Dans hello coin inférieur gauche du tableau de bord hello, cliquez sur **ajouter un périphérique**.</span><span class="sxs-lookup"><span data-stu-id="50d1d-136">In hello lower left-hand corner of hello dashboard, click **Add a device**.</span></span>
   
   ![Ajout d’un appareil][1]
2. <span data-ttu-id="50d1d-138">Bonjour **personnalisé appareil** du panneau, cliquez sur **ajouter un nouveau**.</span><span class="sxs-lookup"><span data-stu-id="50d1d-138">In hello **Custom Device** panel, click **Add new**.</span></span>
   
   ![Ajout d’un appareil personnalisé][2]
3. <span data-ttu-id="50d1d-140">Choisissez **Me laisser définir mon propre ID d'appareil**.</span><span class="sxs-lookup"><span data-stu-id="50d1d-140">Choose **Let me define my own Device ID**.</span></span> <span data-ttu-id="50d1d-141">Entrez un ID de périphérique tel **mydevice**, cliquez sur **vérifier l’ID** tooverify ce nom n’est pas déjà en cours d’utilisation, puis cliquez sur **créer** appareil de hello tooprovision.</span><span class="sxs-lookup"><span data-stu-id="50d1d-141">Enter a Device ID such as **mydevice**, click **Check ID** tooverify that name isn't already in use, and then click **Create** tooprovision hello device.</span></span>
   
   ![Ajouter ID d’appareil][3]
4. <span data-ttu-id="50d1d-143">Rendre un périphérique de hello de note les informations d’identification (ID de périphérique, nom d’hôte du Hub IoT et clé de périphérique).</span><span class="sxs-lookup"><span data-stu-id="50d1d-143">Make a note hello device credentials (Device ID, IoT Hub Hostname, and Device Key).</span></span> <span data-ttu-id="50d1d-144">Votre application cliente doit ces toohello tooconnect de valeurs solution de surveillance à distance.</span><span class="sxs-lookup"><span data-stu-id="50d1d-144">Your client application needs these values tooconnect toohello remote monitoring solution.</span></span> <span data-ttu-id="50d1d-145">Cliquez ensuite sur **Terminé**.</span><span class="sxs-lookup"><span data-stu-id="50d1d-145">Then click **Done**.</span></span>
   
    ![Afficher les informations d’identification d’un appareil][4]
5. <span data-ttu-id="50d1d-147">Sélectionnez votre appareil dans la liste des appareils hello dans le tableau de bord de solution hello.</span><span class="sxs-lookup"><span data-stu-id="50d1d-147">Select your device in hello device list in hello solution dashboard.</span></span> <span data-ttu-id="50d1d-148">Ensuite, dans hello **détails de l’appareil** du panneau, cliquez sur **activer le périphérique**.</span><span class="sxs-lookup"><span data-stu-id="50d1d-148">Then, in hello **Device Details** panel, click **Enable Device**.</span></span> <span data-ttu-id="50d1d-149">Hello de votre appareil est maintenant **en cours d’exécution**.</span><span class="sxs-lookup"><span data-stu-id="50d1d-149">hello status of your device is now **Running**.</span></span> <span data-ttu-id="50d1d-150">solution de surveillance à distance Hello peut maintenant recevoir les données de télémétrie à partir de votre appareil et d’appeler des méthodes sur l’appareil de hello.</span><span class="sxs-lookup"><span data-stu-id="50d1d-150">hello remote monitoring solution can now receive telemetry from your device and invoke methods on hello device.</span></span>

[img-dashboard]: ./media/iot-suite-selector-connecting/dashboard.png
[1]: ./media/iot-suite-selector-connecting/suite0.png
[2]: ./media/iot-suite-selector-connecting/suite1.png
[3]: ./media/iot-suite-selector-connecting/suite2.png
[4]: ./media/iot-suite-selector-connecting/suite3.png

[lnk-what-are-preconfig-solutions]: ../articles/iot-suite/iot-suite-what-are-preconfigured-solutions.md
[lnk-remote-monitoring]: ../articles/iot-suite/iot-suite-remote-monitoring-sample-walkthrough.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/