#### <a name="to-stop-and-start-a-virtual-device"></a><span data-ttu-id="f7124-101">Arrêt et démarrage d’un appareil virtuel</span><span class="sxs-lookup"><span data-stu-id="f7124-101">To stop and start a virtual device</span></span>
<span data-ttu-id="f7124-102">Pour arrêter un appareil virtuel, cliquez sur son nom, puis sur **Arrêter**.</span><span class="sxs-lookup"><span data-stu-id="f7124-102">To stop a virtual device, click its name, and then click **Shutdown**.</span></span> <span data-ttu-id="f7124-103">Lorsque l’appareil virtuel est en train de s’arrêter, son état est **Arrêt en cours**.</span><span class="sxs-lookup"><span data-stu-id="f7124-103">While the virtual device is shutting down, its status is **Stopping**.</span></span> <span data-ttu-id="f7124-104">Une fois l’appareil virtuel arrêté, son état est **Arrêté**.</span><span class="sxs-lookup"><span data-stu-id="f7124-104">After the virtual device is stopped, its status is **Stopped**.</span></span>

<span data-ttu-id="f7124-105">Utilisez les applets de commande suivantes pour arrêter et démarrer un appareil virtuel.</span><span class="sxs-lookup"><span data-stu-id="f7124-105">Use the following cmdlets to stop and start a virtual device.</span></span>

`Stop-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

`Start-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

#### <a name="to-restart-a-virtual-device"></a><span data-ttu-id="f7124-106">Redémarrage d’un appareil virtuel</span><span class="sxs-lookup"><span data-stu-id="f7124-106">To restart a virtual device</span></span>
<span data-ttu-id="f7124-107">Lorsqu’un appareil virtuel est en cours d’exécution et que vous souhaitez le redémarrer, cliquez sur son nom, puis sur **Redémarrer**.</span><span class="sxs-lookup"><span data-stu-id="f7124-107">When a virtual device is running and you want to restart it, click its name, and then click **Restart**.</span></span> <span data-ttu-id="f7124-108">Lorsque l’appareil virtuel est en cours de redémarrage, son état est **Redémarrage en cours**.</span><span class="sxs-lookup"><span data-stu-id="f7124-108">While the virtual device is restarting, its status is **Restarting**.</span></span> <span data-ttu-id="f7124-109">Lorsque l’appareil virtuel est prêt à être utilisé, son état est **En cours d’exécution**.</span><span class="sxs-lookup"><span data-stu-id="f7124-109">When the virtual device is ready for you to use, its status is **Running**.</span></span>

<span data-ttu-id="f7124-110">Utilisez les applets de commande suivantes pour redémarrer un appareil virtuel.</span><span class="sxs-lookup"><span data-stu-id="f7124-110">Use the following cmdlet to restart a virtual device.</span></span>

`Restart-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

