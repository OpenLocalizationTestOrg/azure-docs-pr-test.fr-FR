## <a name="view-device-telemetry-in-hello-dashboard"></a><span data-ttu-id="d7397-101">Télémétrie des consultations de périphérique dans le tableau de bord hello</span><span class="sxs-lookup"><span data-stu-id="d7397-101">View device telemetry in hello dashboard</span></span>
<span data-ttu-id="d7397-102">tableau de bord Hello Bonjour permet de solution télémétrie hello tooview tooIoT Hub d’envoi de vos appareils de surveillance à distance.</span><span class="sxs-lookup"><span data-stu-id="d7397-102">hello dashboard in hello remote monitoring solution enables you tooview hello telemetry your devices send tooIoT Hub.</span></span>

1. <span data-ttu-id="d7397-103">Dans votre navigateur, retour toohello distant solutions tableau de bord, cliquez sur **périphériques** dans hello panneau gauche toonavigate toohello **liste de périphériques**.</span><span class="sxs-lookup"><span data-stu-id="d7397-103">In your browser, return toohello remote monitoring solution dashboard, click **Devices** in hello left-hand panel toonavigate toohello **Devices list**.</span></span>
2. <span data-ttu-id="d7397-104">Bonjour **liste de périphériques**, vous devez voir que hello de votre appareil sont **en cours d’exécution**.</span><span class="sxs-lookup"><span data-stu-id="d7397-104">In hello **Devices list**, you should see that hello status of your device is **Running**.</span></span> <span data-ttu-id="d7397-105">Dans le cas contraire, cliquez sur **activer le périphérique** Bonjour **détails de l’appareil** Panneau de configuration.</span><span class="sxs-lookup"><span data-stu-id="d7397-105">If not, click **Enable Device** in hello **Device Details** panel.</span></span>
   
    ![Afficher l’état de l’appareil][18]
3. <span data-ttu-id="d7397-107">Cliquez sur **tableau de bord** tooreturn toohello tableau de bord, sélectionnez votre appareil dans hello **tooView de périphérique** tooview de liste déroulante ses données de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="d7397-107">Click **Dashboard** tooreturn toohello dashboard, select your device in hello **Device tooView** drop-down tooview its telemetry.</span></span> <span data-ttu-id="d7397-108">télémétrie Hello à partir de l’exemple d’application hello est 50 unités pour la température interne, 55 unités pour la température externe et 50 unités de l’humidité.</span><span class="sxs-lookup"><span data-stu-id="d7397-108">hello telemetry from hello sample application is 50 units for internal temperature, 55 units for external temperature, and 50 units for humidity.</span></span>
   
    ![Afficher la télémétrie d’appareil][img-telemetry]

## <a name="invoke-a-method-on-your-device"></a><span data-ttu-id="d7397-110">Appel d’une méthode sur votre appareil</span><span class="sxs-lookup"><span data-stu-id="d7397-110">Invoke a method on your device</span></span>
<span data-ttu-id="d7397-111">tableau de bord Hello dans la solution d’analyse à distance hello vous permet de méthodes tooinvoke sur vos appareils via IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="d7397-111">hello dashboard in hello remote monitoring solution enables you tooinvoke methods on your devices through IoT Hub.</span></span> <span data-ttu-id="d7397-112">Par exemple, Bonjour solution de surveillance à distance, vous pouvez appeler une toosimulate méthode redémarrage d’un périphérique.</span><span class="sxs-lookup"><span data-stu-id="d7397-112">For example, in hello remote monitoring solution you can invoke a method toosimulate rebooting a device.</span></span>

1. <span data-ttu-id="d7397-113">Dans hello distant solutions tableau de bord, cliquez sur **périphériques** dans hello panneau gauche toonavigate toohello **liste de périphériques**.</span><span class="sxs-lookup"><span data-stu-id="d7397-113">In hello remote monitoring solution dashboard, click **Devices** in hello left-hand panel toonavigate toohello **Devices list**.</span></span>
2. <span data-ttu-id="d7397-114">Cliquez sur **ID de périphérique** pour votre appareil dans hello **liste de périphériques**.</span><span class="sxs-lookup"><span data-stu-id="d7397-114">Click **Device ID** for your device in hello **Devices list**.</span></span>
3. <span data-ttu-id="d7397-115">Bonjour **détails de l’appareil** du panneau, cliquez sur **méthodes**.</span><span class="sxs-lookup"><span data-stu-id="d7397-115">In hello **Device details** panel, click **Methods**.</span></span>
   
    ![Méthodes d’appareil][13]
4. <span data-ttu-id="d7397-117">Bonjour **méthode** liste déroulante, sélectionnez **InitiateFirmwareUpdate**, puis dans **FWPACKAGEURI** entrer une URL factice.</span><span class="sxs-lookup"><span data-stu-id="d7397-117">In hello **Method** drop-down, select **InitiateFirmwareUpdate**, and then in **FWPACKAGEURI** enter a dummy URL.</span></span> <span data-ttu-id="d7397-118">Cliquez sur **appeler une méthode** toocall la méthode hello sur le périphérique de hello.</span><span class="sxs-lookup"><span data-stu-id="d7397-118">Click **Invoke Method** toocall hello method on hello device.</span></span>
   
    ![Appel d’une méthode d’appareil][14]
   

5. <span data-ttu-id="d7397-120">Vous voyez un message dans la console hello votre code de l’appareil en cours d’exécution lorsque le périphérique de hello gère la méthode hello.</span><span class="sxs-lookup"><span data-stu-id="d7397-120">You see a message in hello console running your device code when hello device handles hello method.</span></span> <span data-ttu-id="d7397-121">résultats Hello de méthode hello sont ajoutées toohello historique au portail de solution hello :</span><span class="sxs-lookup"><span data-stu-id="d7397-121">hello results of hello method are added toohello history in hello solution portal:</span></span>

    ![Affichage de l’historique des méthodes][img-method-history]

## <a name="next-steps"></a><span data-ttu-id="d7397-123">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d7397-123">Next steps</span></span>
<span data-ttu-id="d7397-124">article de Hello [personnalisation préconfiguré solutions] [ lnk-customize] décrit quelques méthodes que vous pouvez étendre cet exemple.</span><span class="sxs-lookup"><span data-stu-id="d7397-124">hello article [Customizing preconfigured solutions][lnk-customize] describes some ways you can extend this sample.</span></span> <span data-ttu-id="d7397-125">Les extensions incluent l'utilisation de capteurs réels et l'implémentation de commandes supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="d7397-125">Possible extensions include using real sensors and implementing additional commands.</span></span>

<span data-ttu-id="d7397-126">Vous en apprendrez davantage sur hello [autorisations sur le site de azureiotsuite.com hello][lnk-permissions].</span><span class="sxs-lookup"><span data-stu-id="d7397-126">You can learn more about hello [permissions on hello azureiotsuite.com site][lnk-permissions].</span></span>

[13]: ./media/iot-suite-visualize-connecting/suite4.png
[14]: ./media/iot-suite-visualize-connecting/suite7-1.png
[18]: ./media/iot-suite-visualize-connecting/suite10.png
[img-telemetry]: ./media/iot-suite-visualize-connecting/telemetry.png
[img-method-history]: ./media/iot-suite-visualize-connecting/history.png
[lnk-customize]: ../articles/iot-suite/iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-permissions]: ../articles/iot-suite/iot-suite-permissions.md
