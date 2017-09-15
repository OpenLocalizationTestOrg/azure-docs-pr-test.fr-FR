> [!div class="op_single_selector"]
> * [<span data-ttu-id="ed82a-101">C sur Windows</span><span class="sxs-lookup"><span data-stu-id="ed82a-101">C on Windows</span></span>](../articles/iot-suite/iot-suite-connecting-devices.md)
> * [<span data-ttu-id="ed82a-102">C sur Linux</span><span class="sxs-lookup"><span data-stu-id="ed82a-102">C on Linux</span></span>](../articles/iot-suite/iot-suite-connecting-devices-linux.md)
> * [<span data-ttu-id="ed82a-103">Node.JS</span><span class="sxs-lookup"><span data-stu-id="ed82a-103">Node.js</span></span>](../articles/iot-suite/iot-suite-connecting-devices-node.md)
> 
> 

## <a name="scenario-overview"></a><span data-ttu-id="ed82a-104">Présentation du scénario</span><span class="sxs-lookup"><span data-stu-id="ed82a-104">Scenario overview</span></span>
<span data-ttu-id="ed82a-105">Dans ce scénario, vous allez créer un appareil qui envoie la télémétrie suivante à la [solution préconfigurée][lnk-what-are-preconfig-solutions] de surveillance à distance :</span><span class="sxs-lookup"><span data-stu-id="ed82a-105">In this scenario, you create a device that sends the following telemetry to the remote monitoring [preconfigured solution][lnk-what-are-preconfig-solutions]:</span></span>

* <span data-ttu-id="ed82a-106">Température externe</span><span class="sxs-lookup"><span data-stu-id="ed82a-106">External temperature</span></span>
* <span data-ttu-id="ed82a-107">Température interne</span><span class="sxs-lookup"><span data-stu-id="ed82a-107">Internal temperature</span></span>
* <span data-ttu-id="ed82a-108">Humidité</span><span class="sxs-lookup"><span data-stu-id="ed82a-108">Humidity</span></span>

<span data-ttu-id="ed82a-109">Par souci de simplicité, le code sur l’appareil génère des valeurs d’exemple, mais nous vous encourageons à étendre l'exemple en connectant des capteurs réels à votre appareil et en envoyant une télémétrie réelle.</span><span class="sxs-lookup"><span data-stu-id="ed82a-109">For simplicity, the code on the device generates sample values, but we encourage you to extend the sample by connecting real sensors to your device and sending real telemetry.</span></span>

<span data-ttu-id="ed82a-110">L’appareil est également en mesure de répondre aux méthodes appelées à partir du tableau de bord de la solution et aux valeurs de propriétés souhaitées définies dans le tableau de bord de la solution.</span><span class="sxs-lookup"><span data-stu-id="ed82a-110">The device is also able to respond to methods invoked from the solution dashboard and desired property values set in the solution dashboard.</span></span>

<span data-ttu-id="ed82a-111">Pour effectuer ce didacticiel, vous avez besoin d’un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="ed82a-111">To complete this tutorial, you need an active Azure account.</span></span> <span data-ttu-id="ed82a-112">Si vous ne possédez pas de compte, vous pouvez créer un compte d'évaluation gratuit en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="ed82a-112">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="ed82a-113">Pour plus d’informations, consultez la rubrique [Version d’évaluation gratuite d’Azure][lnk-free-trial].</span><span class="sxs-lookup"><span data-stu-id="ed82a-113">For details, see [Azure Free Trial][lnk-free-trial].</span></span>

## <a name="before-you-start"></a><span data-ttu-id="ed82a-114">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="ed82a-114">Before you start</span></span>
<span data-ttu-id="ed82a-115">Avant d’écrire du code pour votre appareil, vous devez approvisionner votre solution préconfigurée de surveillance à distance et approvisionner un nouvel appareil personnalisé dans cette solution.</span><span class="sxs-lookup"><span data-stu-id="ed82a-115">Before you write any code for your device, you must provision your remote monitoring preconfigured solution and provision a new custom device in that solution.</span></span>

### <a name="provision-your-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="ed82a-116">Approvisionner la solution préconfigurée de surveillance à distance</span><span class="sxs-lookup"><span data-stu-id="ed82a-116">Provision your remote monitoring preconfigured solution</span></span>
<span data-ttu-id="ed82a-117">L’appareil que vous créez dans ce didacticiel envoie des données à une instance de la solution préconfigurée de [surveillance à distance][lnk-remote-monitoring].</span><span class="sxs-lookup"><span data-stu-id="ed82a-117">The device you create in this tutorial sends data to an instance of the [remote monitoring][lnk-remote-monitoring] preconfigured solution.</span></span> <span data-ttu-id="ed82a-118">Si vous n’avez pas déjà approvisionné la solution préconfigurée de surveillance à distance dans votre compte Azure, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="ed82a-118">If you haven't already provisioned the remote monitoring preconfigured solution in your Azure account, use the following steps:</span></span>

1. <span data-ttu-id="ed82a-119">Sur la page <https://www.azureiotsuite.com/>, cliquez sur **+** pour créer une solution.</span><span class="sxs-lookup"><span data-stu-id="ed82a-119">On the <https://www.azureiotsuite.com/> page, click **+** to create a solution.</span></span>
2. <span data-ttu-id="ed82a-120">Cliquez sur **Sélectionner** dans le panneau **Surveillance à distance** pour créer votre solution.</span><span class="sxs-lookup"><span data-stu-id="ed82a-120">Click **Select** on the **Remote monitoring** panel to create your solution.</span></span>
3. <span data-ttu-id="ed82a-121">Sur la page **Create Remote monitoring solution** (Créer une solution de surveillance à distance), entrez le nom de votre choix dans la zone **Nom de solution**, sélectionnez la **Région** dans laquelle vous souhaitez procéder au déploiement, puis sélectionnez l’abonnement Azure à utiliser.</span><span class="sxs-lookup"><span data-stu-id="ed82a-121">On the **Create Remote monitoring solution** page, enter a **Solution name** of your choice, select the **Region** you want to deploy to, and select the Azure subscription to want to use.</span></span> <span data-ttu-id="ed82a-122">Cliquez ensuite sur **Créer la solution**.</span><span class="sxs-lookup"><span data-stu-id="ed82a-122">Then click **Create solution**.</span></span>
4. <span data-ttu-id="ed82a-123">Attendez la fin du processus de configuration.</span><span class="sxs-lookup"><span data-stu-id="ed82a-123">Wait until the provisioning process completes.</span></span>

> [!WARNING]
> <span data-ttu-id="ed82a-124">Les solutions préconfigurées utilisent des services Azure facturables.</span><span class="sxs-lookup"><span data-stu-id="ed82a-124">The preconfigured solutions use billable Azure services.</span></span> <span data-ttu-id="ed82a-125">Veillez à supprimer la solution préconfigurée de votre abonnement lorsque vous avez terminé pour éviter toute facturation inutile.</span><span class="sxs-lookup"><span data-stu-id="ed82a-125">Be sure to remove the preconfigured solution from your subscription when you are done with it to avoid any unnecessary charges.</span></span> <span data-ttu-id="ed82a-126">Vous pouvez supprimer complètement une solution préconfigurée de votre abonnement à partir de la page <https://www.azureiotsuite.com/>.</span><span class="sxs-lookup"><span data-stu-id="ed82a-126">You can completely remove a preconfigured solution from your subscription by visiting the <https://www.azureiotsuite.com/> page.</span></span>
> 
> 

<span data-ttu-id="ed82a-127">Au terme du processus d’approvisionnement de la solution de surveillance à distance, cliquez sur **Lancer** pour ouvrir le tableau de bord de la solution dans votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="ed82a-127">When the provisioning process for the remote monitoring solution finishes, click **Launch** to open the solution dashboard in your browser.</span></span>

![Tableau de bord de solution][img-dashboard]

### <a name="provision-your-device-in-the-remote-monitoring-solution"></a><span data-ttu-id="ed82a-129">Configurer votre appareil dans la solution de surveillance à distance</span><span class="sxs-lookup"><span data-stu-id="ed82a-129">Provision your device in the remote monitoring solution</span></span>
> [!NOTE]
> <span data-ttu-id="ed82a-130">Si vous avez déjà approvisionné un appareil dans votre solution, vous pouvez ignorer cette étape.</span><span class="sxs-lookup"><span data-stu-id="ed82a-130">If you have already provisioned a device in your solution, you can skip this step.</span></span> <span data-ttu-id="ed82a-131">Vous devez connaître les informations d'identification de l’appareil lorsque vous créez l'application cliente.</span><span class="sxs-lookup"><span data-stu-id="ed82a-131">You need to know the device credentials when you create the client application.</span></span>
> 
> 

<span data-ttu-id="ed82a-132">Pour qu’un appareil puisse se connecter à la solution préconfigurée, il doit s’identifier auprès d’IoT Hub à l’aide d’informations d’identification valides.</span><span class="sxs-lookup"><span data-stu-id="ed82a-132">For a device to connect to the preconfigured solution, it must identify itself to IoT Hub using valid credentials.</span></span> <span data-ttu-id="ed82a-133">Vous pouvez récupérer les informations d’identification de l’appareil à partir du tableau de bord de la solution.</span><span class="sxs-lookup"><span data-stu-id="ed82a-133">You can retrieve the device credentials from the solution dashboard.</span></span> <span data-ttu-id="ed82a-134">Les informations d’identification de l’appareil seront ajoutées dans votre application cliente dans la suite de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="ed82a-134">You include the device credentials in your client application later in this tutorial.</span></span>

<span data-ttu-id="ed82a-135">Pour ajouter un appareil à votre solution de surveillance à distance, procédez comme suit dans le tableau de bord de la solution :</span><span class="sxs-lookup"><span data-stu-id="ed82a-135">To add a device to your remote monitoring solution, complete the following steps in the solution dashboard:</span></span>

1. <span data-ttu-id="ed82a-136">Dans le coin inférieur gauche du tableau de bord, cliquez sur **Ajouter un périphérique**.</span><span class="sxs-lookup"><span data-stu-id="ed82a-136">In the lower left-hand corner of the dashboard, click **Add a device**.</span></span>
   
   ![Ajout d’un appareil][1]
2. <span data-ttu-id="ed82a-138">Dans le panneau **Appareil personnalisé**, cliquez sur **Ajouter nouveau**.</span><span class="sxs-lookup"><span data-stu-id="ed82a-138">In the **Custom Device** panel, click **Add new**.</span></span>
   
   ![Ajout d’un appareil personnalisé][2]
3. <span data-ttu-id="ed82a-140">Choisissez **Me laisser définir mon propre ID d'appareil**.</span><span class="sxs-lookup"><span data-stu-id="ed82a-140">Choose **Let me define my own Device ID**.</span></span> <span data-ttu-id="ed82a-141">Entrez un ID d’appareil comme **monappareil**, cliquez sur **Vérifier l’ID** pour vous assurer que ce nom n’est pas déjà utilisé, puis cliquez sur **Créer** pour approvisionner l’appareil.</span><span class="sxs-lookup"><span data-stu-id="ed82a-141">Enter a Device ID such as **mydevice**, click **Check ID** to verify that name isn't already in use, and then click **Create** to provision the device.</span></span>
   
   ![Ajouter ID d’appareil][3]
4. <span data-ttu-id="ed82a-143">Prenez note des informations d’identification de l’appareil (ID d’appareil, nom d’hôte IoT Hub et clé d’appareil).</span><span class="sxs-lookup"><span data-stu-id="ed82a-143">Make a note the device credentials (Device ID, IoT Hub Hostname, and Device Key).</span></span> <span data-ttu-id="ed82a-144">Votre application cliente a besoin de ces valeurs pour se connecter à la solution de surveillance à distance.</span><span class="sxs-lookup"><span data-stu-id="ed82a-144">Your client application needs these values to connect to the remote monitoring solution.</span></span> <span data-ttu-id="ed82a-145">Cliquez ensuite sur **Terminé**.</span><span class="sxs-lookup"><span data-stu-id="ed82a-145">Then click **Done**.</span></span>
   
    ![Afficher les informations d’identification d’un appareil][4]
5. <span data-ttu-id="ed82a-147">Sélectionnez votre appareil dans la liste d’appareils du tableau de bord de la solution.</span><span class="sxs-lookup"><span data-stu-id="ed82a-147">Select your device in the device list in the solution dashboard.</span></span> <span data-ttu-id="ed82a-148">Ensuite, dans le panneau **Détails de l’appareil**, cliquez sur **Activer l’appareil**.</span><span class="sxs-lookup"><span data-stu-id="ed82a-148">Then, in the **Device Details** panel, click **Enable Device**.</span></span> <span data-ttu-id="ed82a-149">L’état de votre appareil est maintenant **En cours d’exécution**.</span><span class="sxs-lookup"><span data-stu-id="ed82a-149">The status of your device is now **Running**.</span></span> <span data-ttu-id="ed82a-150">La solution de surveillance à distance peut désormais recevoir des données de télémétrie à partir de votre appareil et appeler des méthodes sur l’appareil.</span><span class="sxs-lookup"><span data-stu-id="ed82a-150">The remote monitoring solution can now receive telemetry from your device and invoke methods on the device.</span></span>

[img-dashboard]: ./media/iot-suite-selector-connecting/dashboard.png
[1]: ./media/iot-suite-selector-connecting/suite0.png
[2]: ./media/iot-suite-selector-connecting/suite1.png
[3]: ./media/iot-suite-selector-connecting/suite2.png
[4]: ./media/iot-suite-selector-connecting/suite3.png

[lnk-what-are-preconfig-solutions]: ../articles/iot-suite/iot-suite-what-are-preconfigured-solutions.md
[lnk-remote-monitoring]: ../articles/iot-suite/iot-suite-remote-monitoring-sample-walkthrough.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/