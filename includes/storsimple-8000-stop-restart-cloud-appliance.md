#### <a name="toostop-and-start-a-cloud-appliance"></a><span data-ttu-id="50970-101">toostop et démarrer une application cloud</span><span class="sxs-lookup"><span data-stu-id="50970-101">toostop and start a cloud appliance</span></span>

1. <span data-ttu-id="50970-102">toostop un dispositif de cloud, accédez toohello machine virtuelle pour votre solution de cloud.</span><span class="sxs-lookup"><span data-stu-id="50970-102">toostop a cloud appliance, go toohello VM for your cloud appliance.</span></span>
    <span data-ttu-id="50970-103">![Machine virtuelle StorSimple Cloud Appliance](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart1.png)</span><span class="sxs-lookup"><span data-stu-id="50970-103">![StorSimple Cloud Appliance Virtual Machine](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart1.png)</span></span>

2. <span data-ttu-id="50970-104">Dans la barre de commandes hello, cliquez sur **arrêter**.</span><span class="sxs-lookup"><span data-stu-id="50970-104">From hello command bar, click **Stop**.</span></span>

    ![Machine virtuelle StorSimple Cloud Appliance](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart2.png)

3. <span data-ttu-id="50970-106">Cliquez sur **Oui**lorsque vous êtes invité à confirmer l’opération.</span><span class="sxs-lookup"><span data-stu-id="50970-106">When prompted for confirmation, click **Yes**.</span></span>

    ![Machine virtuelle StorSimple Cloud Appliance](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart3.png)

4. <span data-ttu-id="50970-108">Lorsque vous arrêtez une machine virtuelle, celle-ci est désallouée.</span><span class="sxs-lookup"><span data-stu-id="50970-108">When you stop a VM, it gets deallocated.</span></span> <span data-ttu-id="50970-109">Pendant l’arrêt de l’équipement de cloud hello, son état est **Deallocating**.</span><span class="sxs-lookup"><span data-stu-id="50970-109">While hello cloud appliance is stopping, its status is **Deallocating**.</span></span> <span data-ttu-id="50970-110">Une fois que le matériel de cloud hello est arrêté, son état est **arrêté (désallouée)**.</span><span class="sxs-lookup"><span data-stu-id="50970-110">After hello cloud appliance is stopped, its status is **Stopped (deallocated)**.</span></span>

    ![Machine virtuelle StorSimple Cloud Appliance](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart4.png)

5. <span data-ttu-id="50970-112">Une fois qu’une machine virtuelle est arrêtée, cliquez sur **Démarrer** (bouton devient disponible) toostart hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="50970-112">Once a VM is stopped, click **Start** (button becomes available) toostart hello VM.</span></span> <span data-ttu-id="50970-113">Une fois que le matériel de cloud hello a démarré, son état est **démarré**.</span><span class="sxs-lookup"><span data-stu-id="50970-113">After hello cloud appliance has started up, its status is **Started**.</span></span>

    ![Machine virtuelle StorSimple Cloud Appliance](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart5.png)

<span data-ttu-id="50970-115">Utilisez hello suivant toostop d’applets de commande et démarrer une application cloud.</span><span class="sxs-lookup"><span data-stu-id="50970-115">Use hello following cmdlets toostop and start a cloud appliance.</span></span>

`Stop-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

`Start-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

#### <a name="toorestart-a-cloud-appliance"></a><span data-ttu-id="50970-116">toorestart un dispositif de cloud</span><span class="sxs-lookup"><span data-stu-id="50970-116">toorestart a cloud appliance</span></span>

<span data-ttu-id="50970-117">toorestart un dispositif de cloud, accédez toohello machine virtuelle pour votre solution de cloud.</span><span class="sxs-lookup"><span data-stu-id="50970-117">toorestart a cloud appliance, go toohello VM for your cloud appliance.</span></span> <span data-ttu-id="50970-118">Dans la barre de commandes hello, cliquez sur **redémarrer**.</span><span class="sxs-lookup"><span data-stu-id="50970-118">From hello command bar, click **Restart**.</span></span> <span data-ttu-id="50970-119">Lorsque vous y êtes invité, confirmez hello redémarrage.</span><span class="sxs-lookup"><span data-stu-id="50970-119">When prompted, confirm hello restart.</span></span> <span data-ttu-id="50970-120">Lorsque le dispositif de cloud hello est prêt à vous toouse, son état est **en cours d’exécution**.</span><span class="sxs-lookup"><span data-stu-id="50970-120">When hello cloud appliance is ready for you toouse, its status is **Running**.</span></span>

![Machine virtuelle StorSimple Cloud Appliance](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart6.png)

<span data-ttu-id="50970-122">Utilisez hello suivant l’applet de commande toorestart un dispositif de cloud.</span><span class="sxs-lookup"><span data-stu-id="50970-122">Use hello following cmdlet toorestart a cloud appliance.</span></span>

`Restart-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

