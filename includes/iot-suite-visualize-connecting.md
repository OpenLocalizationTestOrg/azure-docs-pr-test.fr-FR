## <a name="view-device-telemetry-in-the-dashboard"></a><span data-ttu-id="33b35-101">Affichage de la télémétrie des appareils dans le tableau de bord</span><span class="sxs-lookup"><span data-stu-id="33b35-101">View device telemetry in the dashboard</span></span>
<span data-ttu-id="33b35-102">Le tableau de bord de la solution de surveillance à distance permet d'afficher la télémétrie que vos appareils envoient au IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="33b35-102">The dashboard in the remote monitoring solution enables you to view the telemetry your devices send to IoT Hub.</span></span>

1. <span data-ttu-id="33b35-103">Dans votre navigateur, revenez au tableau de bord de la solution de surveillance à distance, cliquez sur **Périphériques** dans le panneau de gauche pour accéder à la **Liste de périphériques**.</span><span class="sxs-lookup"><span data-stu-id="33b35-103">In your browser, return to the remote monitoring solution dashboard, click **Devices** in the left-hand panel to navigate to the **Devices list**.</span></span>
2. <span data-ttu-id="33b35-104">Dans la **Liste d’appareils**, vous devez voir que l’état de votre appareil est maintenant **En cours d’exécution**.</span><span class="sxs-lookup"><span data-stu-id="33b35-104">In the **Devices list**, you should see that the status of your device is **Running**.</span></span> <span data-ttu-id="33b35-105">Sinon, cliquez sur **Activer l’appareil** dans le panneau **Détails de l’appareil**.</span><span class="sxs-lookup"><span data-stu-id="33b35-105">If not, click **Enable Device** in the **Device Details** panel.</span></span>
   
    ![Afficher l’état de l’appareil][18]
3. <span data-ttu-id="33b35-107">Cliquez sur **Tableau de bord** pour revenir au tableau de bord, sélectionnez votre périphérique dans la liste déroulante **Périphérique à afficher** pour afficher sa télémétrie.</span><span class="sxs-lookup"><span data-stu-id="33b35-107">Click **Dashboard** to return to the dashboard, select your device in the **Device to View** drop-down to view its telemetry.</span></span> <span data-ttu-id="33b35-108">La télémétrie de l’exemple d’application est configurée pour envoyer 50 unités correspondant à la température interne, 55 unités correspondant à la température externe et 50 à l’humidité.</span><span class="sxs-lookup"><span data-stu-id="33b35-108">The telemetry from the sample application is 50 units for internal temperature, 55 units for external temperature, and 50 units for humidity.</span></span>
   
    ![Afficher la télémétrie d’appareil][img-telemetry]

## <a name="invoke-a-method-on-your-device"></a><span data-ttu-id="33b35-110">Appel d’une méthode sur votre appareil</span><span class="sxs-lookup"><span data-stu-id="33b35-110">Invoke a method on your device</span></span>
<span data-ttu-id="33b35-111">Le tableau de bord de la solution de surveillance à distance vous permet d’appeler des méthodes sur vos appareils via IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="33b35-111">The dashboard in the remote monitoring solution enables you to invoke methods on your devices through IoT Hub.</span></span> <span data-ttu-id="33b35-112">Par exemple, dans la solution de surveillance à distance, vous pouvez appeler une méthode pour simuler le redémarrage d’un appareil.</span><span class="sxs-lookup"><span data-stu-id="33b35-112">For example, in the remote monitoring solution you can invoke a method to simulate rebooting a device.</span></span>

1. <span data-ttu-id="33b35-113">Dans le tableau de bord de la solution de surveillance à distance, cliquez sur **Périphériques** dans le panneau de gauche pour accéder à la **Liste de périphériques**.</span><span class="sxs-lookup"><span data-stu-id="33b35-113">In the remote monitoring solution dashboard, click **Devices** in the left-hand panel to navigate to the **Devices list**.</span></span>
2. <span data-ttu-id="33b35-114">Cliquez sur **ID de périphérique** pour votre périphérique dans la **Liste de périphériques**.</span><span class="sxs-lookup"><span data-stu-id="33b35-114">Click **Device ID** for your device in the **Devices list**.</span></span>
3. <span data-ttu-id="33b35-115">Dans le panneau **Détails de l’appareil**, cliquez sur **Méthodes**.</span><span class="sxs-lookup"><span data-stu-id="33b35-115">In the **Device details** panel, click **Methods**.</span></span>
   
    ![Méthodes d’appareil][13]
4. <span data-ttu-id="33b35-117">Dans la liste déroulante **Méthode**, sélectionnez **InitiateFirmwareUpdate**, puis dans **FWPACKAGEURI**, saisissez une URL factice.</span><span class="sxs-lookup"><span data-stu-id="33b35-117">In the **Method** drop-down, select **InitiateFirmwareUpdate**, and then in **FWPACKAGEURI** enter a dummy URL.</span></span> <span data-ttu-id="33b35-118">Cliquez sur **Appeler une méthode** pour appeler la méthode sur l’appareil.</span><span class="sxs-lookup"><span data-stu-id="33b35-118">Click **Invoke Method** to call the method on the device.</span></span>
   
    ![Appel d’une méthode d’appareil][14]
   

5. <span data-ttu-id="33b35-120">Vous voyez un message dans la console exécutant votre code d’appareil lorsque l’appareil traite la méthode.</span><span class="sxs-lookup"><span data-stu-id="33b35-120">You see a message in the console running your device code when the device handles the method.</span></span> <span data-ttu-id="33b35-121">Les résultats de la méthode sont ajoutés à l’historique dans le portail de solution :</span><span class="sxs-lookup"><span data-stu-id="33b35-121">The results of the method are added to the history in the solution portal:</span></span>

    ![Affichage de l’historique des méthodes][img-method-history]

## <a name="next-steps"></a><span data-ttu-id="33b35-123">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="33b35-123">Next steps</span></span>
<span data-ttu-id="33b35-124">L'article [Personnalisation des solutions préconfigurées][lnk-customize] décrit quelques méthodes pour étendre cet exemple.</span><span class="sxs-lookup"><span data-stu-id="33b35-124">The article [Customizing preconfigured solutions][lnk-customize] describes some ways you can extend this sample.</span></span> <span data-ttu-id="33b35-125">Les extensions incluent l'utilisation de capteurs réels et l'implémentation de commandes supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="33b35-125">Possible extensions include using real sensors and implementing additional commands.</span></span>

<span data-ttu-id="33b35-126">Vous pouvez en savoir plus sur les [autorisations sur le site azureiotsuite.com][lnk-permissions].</span><span class="sxs-lookup"><span data-stu-id="33b35-126">You can learn more about the [permissions on the azureiotsuite.com site][lnk-permissions].</span></span>

[13]: ./media/iot-suite-visualize-connecting/suite4.png
[14]: ./media/iot-suite-visualize-connecting/suite7-1.png
[18]: ./media/iot-suite-visualize-connecting/suite10.png
[img-telemetry]: ./media/iot-suite-visualize-connecting/telemetry.png
[img-method-history]: ./media/iot-suite-visualize-connecting/history.png
[lnk-customize]: ../articles/iot-suite/iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-permissions]: ../articles/iot-suite/iot-suite-permissions.md
