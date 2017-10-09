<!--author=alkohli last changed: 07/07/17-->

#### <a name="tooinstall-an-update-from-hello-azure-portal"></a><span data-ttu-id="81ba0-101">tooinstall une mise à jour à partir de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="81ba0-101">tooinstall an update from hello Azure portal</span></span>

1. <span data-ttu-id="81ba0-102">Sur la page du service StorSimple hello, sélectionnez votre appareil.</span><span class="sxs-lookup"><span data-stu-id="81ba0-102">On hello StorSimple service page, select your device.</span></span>

    ![Sélectionnez l’appareil](./media/storsimple-8000-install-update4-via-portal/update1.png)

2. <span data-ttu-id="81ba0-104">Accédez trop**paramètres de périphérique** > **mises à jour de l’appareil**.</span><span class="sxs-lookup"><span data-stu-id="81ba0-104">Navigate too**Device settings** > **Device updates**.</span></span>

    ![Cliquez sur Mises à jour de l’appareil](./media/storsimple-8000-install-update4-via-portal/update2.png)

2. <span data-ttu-id="81ba0-106">Une notification s’affiche si de nouvelles mises à jour sont disponibles.</span><span class="sxs-lookup"><span data-stu-id="81ba0-106">A notification appears if new updates are available.</span></span> <span data-ttu-id="81ba0-107">Également, dans hello **mises à jour de l’appareil** panneau, cliquez sur **d’analyse des mises à jour**.</span><span class="sxs-lookup"><span data-stu-id="81ba0-107">Alternatively, in hello **Device updates** blade, click **Scan Updates**.</span></span> <span data-ttu-id="81ba0-108">Un travail est créé tooscan mises à jour disponibles.</span><span class="sxs-lookup"><span data-stu-id="81ba0-108">A job is created tooscan for available updates.</span></span> <span data-ttu-id="81ba0-109">Vous êtes averti lorsque la fin du travail hello.</span><span class="sxs-lookup"><span data-stu-id="81ba0-109">You are notified when hello job completes successfully.</span></span>

    ![Cliquez sur Mises à jour de l’appareil](./media/storsimple-8000-install-update4-via-portal/update3.png)

3. <span data-ttu-id="81ba0-111">Nous vous recommandons de consulter les notes de publication hello avant d’appliquer une mise à jour sur votre appareil.</span><span class="sxs-lookup"><span data-stu-id="81ba0-111">We recommend that you review hello release notes before you apply an update on your device.</span></span> <span data-ttu-id="81ba0-112">Cliquez sur les mises à jour de tooapply, **installer les mises à jour**.</span><span class="sxs-lookup"><span data-stu-id="81ba0-112">tooapply updates, click **Install updates**.</span></span> <span data-ttu-id="81ba0-113">Bonjour **confirmer les mises à jour régulières** panneau, révision hello conditions préalables toocomplete avant d’appliquer les mises à jour.</span><span class="sxs-lookup"><span data-stu-id="81ba0-113">In hello **Confirm regular updates** blade, review hello prerequisites toocomplete before you apply updates.</span></span> <span data-ttu-id="81ba0-114">Sélectionnez tooindicate de case à cocher hello que vous tooupdate prêt hello du périphérique, puis sur **installer**.</span><span class="sxs-lookup"><span data-stu-id="81ba0-114">Select hello checkbox tooindicate that you are ready tooupdate hello device and then click **Install**.</span></span>

    ![Cliquez sur Mises à jour de l’appareil](./media/storsimple-8000-install-update4-via-portal/update4.png)

6. <span data-ttu-id="81ba0-116">Un ensemble de vérifications préalables démarre.</span><span class="sxs-lookup"><span data-stu-id="81ba0-116">A set of prerequisite checks starts.</span></span> <span data-ttu-id="81ba0-117">Ces vérifications incluent :</span><span class="sxs-lookup"><span data-stu-id="81ba0-117">These checks include:</span></span>
   
   * <span data-ttu-id="81ba0-118">**Contrôles d’intégrité de contrôleur** tooverify que les deux hello contrôleurs d’appareil sont sains et en ligne.</span><span class="sxs-lookup"><span data-stu-id="81ba0-118">**Controller health checks** tooverify that both hello device controllers are healthy and online.</span></span>
   * <span data-ttu-id="81ba0-119">**Contrôles d’intégrité de composant matériel** tooverify que tous les hello des composants matériels de votre appareil StorSimple sont intègres.</span><span class="sxs-lookup"><span data-stu-id="81ba0-119">**Hardware component health checks** tooverify that all hello hardware components on your StorSimple device are healthy.</span></span>
   * <span data-ttu-id="81ba0-120">**DATA 0 vérifie** tooverify que DATA 0 est activé sur votre appareil.</span><span class="sxs-lookup"><span data-stu-id="81ba0-120">**DATA 0 checks** tooverify that DATA 0 is enabled on your device.</span></span> <span data-ttu-id="81ba0-121">Si cette interface n’est pas activée, vous devez l’activer, puis réessayer.</span><span class="sxs-lookup"><span data-stu-id="81ba0-121">If this interface is not enabled, you must enable it and then retry.</span></span>

    <span data-ttu-id="81ba0-122">mise à jour Hello est téléchargé et installé uniquement si toutes les vérifications de hello sont correctement terminées.</span><span class="sxs-lookup"><span data-stu-id="81ba0-122">hello update is downloaded and installed only if all hello checks are successfully completed.</span></span> <span data-ttu-id="81ba0-123">Vous êtes averti lorsque des vérifications de hello sont en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="81ba0-123">You are notified when hello checks are in progress.</span></span> <span data-ttu-id="81ba0-124">Si hello prechecks échouent, vous êtes fourni avec les raisons pour lesquelles les hello.</span><span class="sxs-lookup"><span data-stu-id="81ba0-124">If hello prechecks fail, then you will be provided with hello reasons for failure.</span></span> <span data-ttu-id="81ba0-125">Répondre à ces problèmes, puis recommencez les opération hello.</span><span class="sxs-lookup"><span data-stu-id="81ba0-125">Address those issues and then retry hello operation.</span></span> <span data-ttu-id="81ba0-126">Vous devrez peut-être toocontact Support technique de Microsoft si vous ne pouvez pas résoudre ces problèmes vous-même.</span><span class="sxs-lookup"><span data-stu-id="81ba0-126">You may need toocontact Microsoft Support if you cannot address these issues by yourself.</span></span>

7. <span data-ttu-id="81ba0-127">Une fois hello prechecks sont correctement effectués, création d’un travail de mise à jour.</span><span class="sxs-lookup"><span data-stu-id="81ba0-127">After hello prechecks are successfully completed, an update job is created.</span></span> <span data-ttu-id="81ba0-128">Vous êtes averti lorsque la tâche de mise à jour hello est créée.</span><span class="sxs-lookup"><span data-stu-id="81ba0-128">You are notified when hello update job is successfully created.</span></span>
   
    ![Création de la tâche de mise à jour](./media/storsimple-8000-install-update4-via-portal/update6.png)
   
    <span data-ttu-id="81ba0-130">mise à jour Hello est ensuite appliqué sur votre appareil.</span><span class="sxs-lookup"><span data-stu-id="81ba0-130">hello update is then applied on your device.</span></span>

9. <span data-ttu-id="81ba0-131">mise à jour Hello prend quelques heures toocomplete.</span><span class="sxs-lookup"><span data-stu-id="81ba0-131">hello update takes a few hours toocomplete.</span></span> <span data-ttu-id="81ba0-132">Sélectionnez la tâche de mise à jour hello et cliquez sur **détails** tooview les détails de hello du travail hello à tout moment.</span><span class="sxs-lookup"><span data-stu-id="81ba0-132">Select hello update job and click **Details** tooview hello details of hello job at any time.</span></span>

    ![Création de la tâche de mise à jour](./media/storsimple-8000-install-update4-via-portal/update8.png)

     <span data-ttu-id="81ba0-134">Vous pouvez également surveiller hello progression du travail de mise à jour hello à partir de **paramètres du périphérique > travaux**.</span><span class="sxs-lookup"><span data-stu-id="81ba0-134">You can also monitor hello progress of hello update job from **Device settings > Jobs**.</span></span> <span data-ttu-id="81ba0-135">Sur hello **travaux** panneau, vous pouvez voir hello mettre à jour de progression.</span><span class="sxs-lookup"><span data-stu-id="81ba0-135">On hello **Jobs** blade, you can see hello update progress.</span></span>

     ![Création de la tâche de mise à jour](./media/storsimple-8000-install-update4-via-portal/update7.png)

10. <span data-ttu-id="81ba0-137">Une fois le travail de hello est terminée, accédez à toohello **paramètres du périphérique > mises à jour de l’appareil**.</span><span class="sxs-lookup"><span data-stu-id="81ba0-137">After hello job is complete, navigate toohello **Device settings > Device updates**.</span></span> <span data-ttu-id="81ba0-138">version du logiciel Hello doit maintenant être mis à jour.</span><span class="sxs-lookup"><span data-stu-id="81ba0-138">hello software version should now be updated.</span></span>

    ![Création de la tâche de mise à jour](./media/storsimple-8000-install-update4-via-portal/update9.png)

