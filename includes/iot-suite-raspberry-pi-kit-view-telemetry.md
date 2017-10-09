## <a name="view-hello-telemetry"></a><span data-ttu-id="283b9-101">Télémétrie des consultations de hello</span><span class="sxs-lookup"><span data-stu-id="283b9-101">View hello telemetry</span></span>

<span data-ttu-id="283b9-102">Hello framboises Pi envoie désormais une solution d’analyse à distance toohello télémétrie.</span><span class="sxs-lookup"><span data-stu-id="283b9-102">hello Raspberry Pi is now sending telemetry toohello remote monitoring solution.</span></span> <span data-ttu-id="283b9-103">Vous pouvez afficher les données de télémétrie hello sur le tableau de bord de solution hello.</span><span class="sxs-lookup"><span data-stu-id="283b9-103">You can view hello telemetry on hello solution dashboard.</span></span> <span data-ttu-id="283b9-104">Vous pouvez également envoyer des messages tooyour framboises Pi à partir du tableau de bord de solution hello.</span><span class="sxs-lookup"><span data-stu-id="283b9-104">You can also send messages tooyour Raspberry Pi from hello solution dashboard.</span></span>

- <span data-ttu-id="283b9-105">Accédez à tableau de bord toohello solution.</span><span class="sxs-lookup"><span data-stu-id="283b9-105">Navigate toohello solution dashboard.</span></span>
- <span data-ttu-id="283b9-106">Sélectionnez votre appareil dans hello **tooView de périphérique** liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="283b9-106">Select your device in hello **Device tooView** dropdown.</span></span>
- <span data-ttu-id="283b9-107">télémétrie Hello hello framboises Pi affiche sur le tableau de bord hello.</span><span class="sxs-lookup"><span data-stu-id="283b9-107">hello telemetry from hello Raspberry Pi displays on hello dashboard.</span></span>

![Afficher les données de télémétrie de hello framboises Pi][img-telemetry-display]

## <a name="act-on-hello-device"></a><span data-ttu-id="283b9-109">Agir sur les appareils hello</span><span class="sxs-lookup"><span data-stu-id="283b9-109">Act on hello device</span></span>

<span data-ttu-id="283b9-110">À partir du tableau de bord hello solution, vous pouvez appeler des méthodes sur votre Pi framboises.</span><span class="sxs-lookup"><span data-stu-id="283b9-110">From hello solution dashboard, you can invoke methods on your Raspberry Pi.</span></span> <span data-ttu-id="283b9-111">Lorsque hello framboises Pi connecte à une solution d’analyse à distance toohello, il envoie des informations sur les méthodes hello qu'il prend en charge.</span><span class="sxs-lookup"><span data-stu-id="283b9-111">When hello Raspberry Pi connects toohello remote monitoring solution, it sends information about hello methods it supports.</span></span>

- <span data-ttu-id="283b9-112">Dans le tableau de bord hello solution, cliquez sur **périphériques** toovisit hello **périphériques** page.</span><span class="sxs-lookup"><span data-stu-id="283b9-112">In hello solution dashboard, click **Devices** toovisit hello **Devices** page.</span></span> <span data-ttu-id="283b9-113">Sélectionnez votre Pi framboises Bonjour **liste des appareils**.</span><span class="sxs-lookup"><span data-stu-id="283b9-113">Select your Raspberry Pi in hello **Device List**.</span></span> <span data-ttu-id="283b9-114">Ensuite, choisissez **Méthodes** :</span><span class="sxs-lookup"><span data-stu-id="283b9-114">Then choose **Methods**:</span></span>

    ![Liste des appareils dans le tableau de bord][img-list-devices]

- <span data-ttu-id="283b9-116">Sur hello **appeler une méthode** choisissez **LightBlink** Bonjour **méthode** liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="283b9-116">On hello **Invoke Method** page, choose **LightBlink** in hello **Method** dropdown.</span></span>

- <span data-ttu-id="283b9-117">Choisissez **InvokeMethod**.</span><span class="sxs-lookup"><span data-stu-id="283b9-117">Choose **InvokeMethod**.</span></span> <span data-ttu-id="283b9-118">Hello DEL connecté toohello que framboises Pi clignote à plusieurs reprises.</span><span class="sxs-lookup"><span data-stu-id="283b9-118">hello LED connected toohello Raspberry Pi flashes several times.</span></span> <span data-ttu-id="283b9-119">application Hello sur hello framboises Pi envoie un tableau de bord d’accusé de réception différé toohello solution :</span><span class="sxs-lookup"><span data-stu-id="283b9-119">hello app on hello Raspberry Pi sends an acknowledgment back toohello solution dashboard:</span></span>

    ![Afficher l’historique de la méthode][img-method-history]

- <span data-ttu-id="283b9-121">Vous pouvez basculer les DEL hello et désactiver à l’aide de hello **ChangeLightStatus** méthode avec un **LightStatusValue** défini trop**1** pour sur ou **0** pour désactiver.</span><span class="sxs-lookup"><span data-stu-id="283b9-121">You can switch hello LED on and off using hello **ChangeLightStatus** method with a **LightStatusValue** set too**1** for on or **0** for off.</span></span>

> [!WARNING]
> <span data-ttu-id="283b9-122">Si vous laissez hello solution en cours d’exécution dans votre compte Azure de surveillance à distance, vous êtes facturé pour hello exécution.</span><span class="sxs-lookup"><span data-stu-id="283b9-122">If you leave hello remote monitoring solution running in your Azure account, you are billed for hello time it runs.</span></span> <span data-ttu-id="283b9-123">Pour plus d’informations sur la réduction de la consommation lors hello s’exécute la solution de surveillance à distance, consultez [configuration Azure IoT Suite préconfiguré des solutions à des fins de démonstration][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="283b9-123">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span> <span data-ttu-id="283b9-124">Supprimer la solution de hello préconfiguré à partir de votre compte Azure lorsque vous avez terminé.</span><span class="sxs-lookup"><span data-stu-id="283b9-124">Delete hello preconfigured solution from your Azure account when you have finished using it.</span></span>


[img-telemetry-display]: media/iot-suite-raspberry-pi-kit-view-telemetry/telemetry.png
[img-list-devices]: media/iot-suite-raspberry-pi-kit-view-telemetry/listdevices.png
[img-method-history]: media/iot-suite-raspberry-pi-kit-view-telemetry/methodhistory.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md