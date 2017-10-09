#### <a name="toostop-and-start-a-virtual-device"></a><span data-ttu-id="9d6b4-101">toostop et démarrer un appareil virtuel</span><span class="sxs-lookup"><span data-stu-id="9d6b4-101">toostop and start a virtual device</span></span>
<span data-ttu-id="9d6b4-102">toostop un appareil virtuel, cliquez sur son nom, puis cliquez sur **arrêt**.</span><span class="sxs-lookup"><span data-stu-id="9d6b4-102">toostop a virtual device, click its name, and then click **Shutdown**.</span></span> <span data-ttu-id="9d6b4-103">Pendant l’arrêt de l’appareil virtuel de hello, son état est **arrêt**.</span><span class="sxs-lookup"><span data-stu-id="9d6b4-103">While hello virtual device is shutting down, its status is **Stopping**.</span></span> <span data-ttu-id="9d6b4-104">Une fois un appareil virtuel hello est arrêté, son état est **arrêté**.</span><span class="sxs-lookup"><span data-stu-id="9d6b4-104">After hello virtual device is stopped, its status is **Stopped**.</span></span>

<span data-ttu-id="9d6b4-105">Utilisez hello suivant toostop d’applets de commande et démarrez un appareil virtuel.</span><span class="sxs-lookup"><span data-stu-id="9d6b4-105">Use hello following cmdlets toostop and start a virtual device.</span></span>

`Stop-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

`Start-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

#### <a name="toorestart-a-virtual-device"></a><span data-ttu-id="9d6b4-106">toorestart un appareil virtuel</span><span class="sxs-lookup"><span data-stu-id="9d6b4-106">toorestart a virtual device</span></span>
<span data-ttu-id="9d6b4-107">Lorsqu’un périphérique virtuel est en cours d’exécution et que vous souhaitez toorestart, cliquez sur son nom, puis cliquez sur **redémarrer**.</span><span class="sxs-lookup"><span data-stu-id="9d6b4-107">When a virtual device is running and you want toorestart it, click its name, and then click **Restart**.</span></span> <span data-ttu-id="9d6b4-108">Pendant le redémarrage de périphérique virtuel de hello, son état est **redémarrage**.</span><span class="sxs-lookup"><span data-stu-id="9d6b4-108">While hello virtual device is restarting, its status is **Restarting**.</span></span> <span data-ttu-id="9d6b4-109">Quand un appareil virtuel hello est prêt à vous toouse, son état est **en cours d’exécution**.</span><span class="sxs-lookup"><span data-stu-id="9d6b4-109">When hello virtual device is ready for you toouse, its status is **Running**.</span></span>

<span data-ttu-id="9d6b4-110">Utilisez hello suivant l’applet de commande toorestart un appareil virtuel.</span><span class="sxs-lookup"><span data-stu-id="9d6b4-110">Use hello following cmdlet toorestart a virtual device.</span></span>

`Restart-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

