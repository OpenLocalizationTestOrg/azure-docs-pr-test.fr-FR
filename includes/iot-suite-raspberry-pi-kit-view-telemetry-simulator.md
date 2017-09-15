## <a name="view-the-telemetry"></a><span data-ttu-id="d54aa-101">Afficher les données de télémétrie</span><span class="sxs-lookup"><span data-stu-id="d54aa-101">View the telemetry</span></span>

<span data-ttu-id="d54aa-102">Le Raspberry Pi prend désormais en charge l’envoi de données de télémétrie à la solution de surveillance à distance.</span><span class="sxs-lookup"><span data-stu-id="d54aa-102">The Raspberry Pi is now sending telemetry to the remote monitoring solution.</span></span> <span data-ttu-id="d54aa-103">Vous pouvez afficher les données de télémétrie sur le tableau de bord de la solution.</span><span class="sxs-lookup"><span data-stu-id="d54aa-103">You can view the telemetry on the solution dashboard.</span></span> <span data-ttu-id="d54aa-104">Vous pouvez également envoyer des messages à votre Raspberry Pi à partir du tableau de bord de la solution.</span><span class="sxs-lookup"><span data-stu-id="d54aa-104">You can also send messages to your Raspberry Pi from the solution dashboard.</span></span>

- <span data-ttu-id="d54aa-105">Accédez au tableau de bord de la solution.</span><span class="sxs-lookup"><span data-stu-id="d54aa-105">Navigate to the solution dashboard.</span></span>
- <span data-ttu-id="d54aa-106">Sélectionnez votre appareil dans la liste déroulante **Appareil à afficher**.</span><span class="sxs-lookup"><span data-stu-id="d54aa-106">Select your device in the **Device to View** dropdown.</span></span>
- <span data-ttu-id="d54aa-107">Les données de télémétrie du Raspberry Pi s’affichent sur le tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="d54aa-107">The telemetry from the Raspberry Pi displays on the dashboard.</span></span>

![Afficher les données de télémétrie depuis le Raspberry Pi][img-telemetry-display]

## <a name="act-on-the-device"></a><span data-ttu-id="d54aa-109">Action sur l’appareil</span><span class="sxs-lookup"><span data-stu-id="d54aa-109">Act on the device</span></span>

<span data-ttu-id="d54aa-110">À partir du tableau de bord de la solution, vous pouvez appeler des méthodes sur votre Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="d54aa-110">From the solution dashboard, you can invoke methods on your Raspberry Pi.</span></span> <span data-ttu-id="d54aa-111">Lorsque le Raspberry Pi se connecte à la solution de surveillance à distance, il envoie des informations sur les méthodes qu’il prend en charge.</span><span class="sxs-lookup"><span data-stu-id="d54aa-111">When the Raspberry Pi connects to the remote monitoring solution, it sends information about the methods it supports.</span></span>

- <span data-ttu-id="d54aa-112">Dans le tableau de bord de la solution, cliquez sur **Appareils** pour accéder à la page **Appareils**.</span><span class="sxs-lookup"><span data-stu-id="d54aa-112">In the solution dashboard, click **Devices** to visit the **Devices** page.</span></span> <span data-ttu-id="d54aa-113">Sélectionnez votre Raspberry Pi dans la **Liste des appareils**.</span><span class="sxs-lookup"><span data-stu-id="d54aa-113">Select your Raspberry Pi in the **Device List**.</span></span> <span data-ttu-id="d54aa-114">Ensuite, choisissez **Méthodes** :</span><span class="sxs-lookup"><span data-stu-id="d54aa-114">Then choose **Methods**:</span></span>

    ![Répertorier les appareils dans le tableau de bord][img-list-devices]

- <span data-ttu-id="d54aa-116">Dans la page **Appeler une méthode**, choisissez **LightBlink** dans la liste déroulante **Méthode**.</span><span class="sxs-lookup"><span data-stu-id="d54aa-116">On the **Invoke Method** page, choose **LightBlink** in the **Method** dropdown.</span></span>

- <span data-ttu-id="d54aa-117">Choisissez **InvokeMethod**.</span><span class="sxs-lookup"><span data-stu-id="d54aa-117">Choose **InvokeMethod**.</span></span> <span data-ttu-id="d54aa-118">Le simulateur imprime un message dans la console sur le Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="d54aa-118">The simulator prints a message in the console on the Raspberry Pi.</span></span> <span data-ttu-id="d54aa-119">L’application sur le Raspberry Pi renvoie un accusé de réception sur le tableau de bord de la solution :</span><span class="sxs-lookup"><span data-stu-id="d54aa-119">The app on the Raspberry Pi sends an acknowledgment back to the solution dashboard:</span></span>

    ![Afficher l’historique des méthodes][img-method-history]

- <span data-ttu-id="d54aa-121">Vous pouvez allumer et éteindre le voyant en utilisant la méthode **ChangeLightStatus** et en définissant le paramètre **LightStatusValue** sur la valeur **1** pour l’allumer, ou sur la valeur **0** pour l’éteindre.</span><span class="sxs-lookup"><span data-stu-id="d54aa-121">You can switch the LED on and off using the **ChangeLightStatus** method with a **LightStatusValue** set to **1** for on or **0** for off.</span></span>

> [!WARNING]
> <span data-ttu-id="d54aa-122">Si vous laissez la solution de surveillance à distance s’exécuter dans votre compte Azure, vous serez facturé pour son temps d’exécution.</span><span class="sxs-lookup"><span data-stu-id="d54aa-122">If you leave the remote monitoring solution running in your Azure account, you are billed for the time it runs.</span></span> <span data-ttu-id="d54aa-123">Pour plus d’informations sur la manière de réduire votre consommation pendant l’exécution de la solution de surveillance à distance, consultez [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config] (Configuration des solutions préconfigurées Azure IoT Suite à des fins de démonstration).</span><span class="sxs-lookup"><span data-stu-id="d54aa-123">For more information about reducing consumption while the remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span> <span data-ttu-id="d54aa-124">Supprimez la solution préconfigurée de votre compte Azure lorsque vous avez fini de l’utiliser.</span><span class="sxs-lookup"><span data-stu-id="d54aa-124">Delete the preconfigured solution from your Azure account when you have finished using it.</span></span>


[img-telemetry-display]: media/iot-suite-raspberry-pi-kit-view-telemetry-simulator/telemetry.png
[img-list-devices]: media/iot-suite-raspberry-pi-kit-view-telemetry-simulator/listdevices.png
[img-method-history]: media/iot-suite-raspberry-pi-kit-view-telemetry-simulator/methodhistory.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md