<!--author=alkohli last changed: 01/12/17-->

### <a name="to-take-a-backup"></a><span data-ttu-id="e7833-101">Pour effectuer une sauvegarde</span><span class="sxs-lookup"><span data-stu-id="e7833-101">To take a backup</span></span>

1. <span data-ttu-id="e7833-102">Accédez à votre service StorSimple Device Manager.</span><span class="sxs-lookup"><span data-stu-id="e7833-102">Go to your StorSimple Device Manager service.</span></span> <span data-ttu-id="e7833-103">Sélectionnez votre appareil et cliquez dessus dans la liste tabulaire des appareils, puis cliquez sur **Tous les paramètres**.</span><span class="sxs-lookup"><span data-stu-id="e7833-103">From the tabular listing of devices, select and click your device and then click **All settings**.</span></span> <span data-ttu-id="e7833-104">Dans le panneau **Paramètres**, accédez à **Paramètres > Gérer > Stratégie de sauvegarde**.</span><span class="sxs-lookup"><span data-stu-id="e7833-104">In the **Settings** blade, go to **Settings > Manage > Backup policy**.</span></span>

    ![Add-backup-policy](./media/storsimple-8000-take-backup/step8takebu1.png)

2. <span data-ttu-id="e7833-106">Dans le panneau **Stratégie de sauvegarde**, cliquez sur **+ Ajouter une stratégie**.</span><span class="sxs-lookup"><span data-stu-id="e7833-106">In the **Backup policy** blade, click **+ Add policy**.</span></span>

    ![Add-backup-policy](./media/storsimple-8000-take-backup/step8takebu2.png)

3. <span data-ttu-id="e7833-108">Spécifiez un nom comprenant entre 3 et 150 caractères pour votre stratégie de sauvegarde dans le panneau **Créer une stratégie de sauvegarde**.</span><span class="sxs-lookup"><span data-stu-id="e7833-108">In the **Create backup policy** blade, supply a name that contains between 3 and 150 characters for your backup policy.</span></span>

4. <span data-ttu-id="e7833-109">Sélectionnez les volumes à sauvegarder.</span><span class="sxs-lookup"><span data-stu-id="e7833-109">Select the volumes to be backed up.</span></span> <span data-ttu-id="e7833-110">Si vous sélectionnez plusieurs volumes, ceux-ci sont regroupés pour créer une sauvegarde afin d’assurer la cohérence des données.</span><span class="sxs-lookup"><span data-stu-id="e7833-110">If you select more than one volume, these volumes are grouped together to create a crash-consistent backup.</span></span>

    ![Add-backup-policy](./media/storsimple-8000-take-backup/step8takebu4.png)

5. <span data-ttu-id="e7833-112">Dans le panneau **Ajouter la première planification** :</span><span class="sxs-lookup"><span data-stu-id="e7833-112">On **Add first schedule** blade:</span></span>

    1. <span data-ttu-id="e7833-113">Sélectionnez le type de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="e7833-113">Select the type of backup.</span></span> <span data-ttu-id="e7833-114">Pour une restauration plus rapide, sélectionnez Instantané **local**.</span><span class="sxs-lookup"><span data-stu-id="e7833-114">For faster restores, select **Local** snapshot.</span></span> <span data-ttu-id="e7833-115">Pour la résilience des données, sélectionnez Instantané **cloud**.</span><span class="sxs-lookup"><span data-stu-id="e7833-115">For data resiliency, select **Cloud** snapshot.</span></span>
    2. <span data-ttu-id="e7833-116">Spécifiez la fréquence de sauvegarde en minutes, heures, jours ou semaines.</span><span class="sxs-lookup"><span data-stu-id="e7833-116">Specify the backup frequency in minutes, hours, days, or weeks.</span></span>
    3. <span data-ttu-id="e7833-117">Sélectionnez une durée de conservation.</span><span class="sxs-lookup"><span data-stu-id="e7833-117">Select a retention time.</span></span> <span data-ttu-id="e7833-118">La durée de conservation dépend de la fréquence de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="e7833-118">The retention choices depend on the backup frequency.</span></span> <span data-ttu-id="e7833-119">Par exemple, si vous sélectionnez une stratégie quotidienne, vous pouvez spécifier une durée de conservation en semaines, alors que pour une stratégie mensuelle, la durée de conservation est en mois.</span><span class="sxs-lookup"><span data-stu-id="e7833-119">For example, for a daily policy, the retention can be specified in weeks, whereas retention for a monthly policy is in months.</span></span>
    4. <span data-ttu-id="e7833-120">Sélectionnez l’heure et la date de début de la stratégie de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="e7833-120">Select the starting time and date for the backup policy.</span></span>
    5. <span data-ttu-id="e7833-121">Cliquez sur **OK** pour créer la stratégie de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="e7833-121">Click **OK** to create the backup policy.</span></span>

        ![Add-backup-policy](./media/storsimple-8000-take-backup/step8takebu5.png) 

6. <span data-ttu-id="e7833-123">Cliquez sur **Créer** pour démarrer la création de la stratégie de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="e7833-123">Click **Create** to start the backup policy creation.</span></span> <span data-ttu-id="e7833-124">Un message s’affiche une fois la stratégie de sauvegarde créée.</span><span class="sxs-lookup"><span data-stu-id="e7833-124">You are notified when the backup policy is successfully created.</span></span> <span data-ttu-id="e7833-125">La liste des stratégies de sauvegarde est également mise à jour.</span><span class="sxs-lookup"><span data-stu-id="e7833-125">The list of backup policies is also updated.</span></span>
      
      ![Add-backup-policy](./media/storsimple-8000-take-backup/step8takebu9.png)
      
      <span data-ttu-id="e7833-127">Vous disposez maintenant d’une stratégie de sauvegarde, qui crée des sauvegardes planifiées des données de volume.</span><span class="sxs-lookup"><span data-stu-id="e7833-127">You now have a backup policy that creates scheduled backups of your volume data.</span></span>




