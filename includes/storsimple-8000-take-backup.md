<!--author=alkohli last changed: 01/12/17-->

### <a name="tootake-a-backup"></a><span data-ttu-id="42fef-101">tootake une sauvegarde</span><span class="sxs-lookup"><span data-stu-id="42fef-101">tootake a backup</span></span>

1. <span data-ttu-id="42fef-102">Atteindre le service du Gestionnaire de périphériques StorSimple tooyour.</span><span class="sxs-lookup"><span data-stu-id="42fef-102">Go tooyour StorSimple Device Manager service.</span></span> <span data-ttu-id="42fef-103">À partir de hello tabulaire la liste des périphériques, sélectionnez et cliquez sur votre appareil, puis cliquez **tous les paramètres**.</span><span class="sxs-lookup"><span data-stu-id="42fef-103">From hello tabular listing of devices, select and click your device and then click **All settings**.</span></span> <span data-ttu-id="42fef-104">Bonjour **paramètres** panneau, accédez trop**Paramètres > Gérer > stratégie de sauvegarde**.</span><span class="sxs-lookup"><span data-stu-id="42fef-104">In hello **Settings** blade, go too**Settings > Manage > Backup policy**.</span></span>

    ![Add-backup-policy](./media/storsimple-8000-take-backup/step8takebu1.png)

2. <span data-ttu-id="42fef-106">Bonjour **stratégie de sauvegarde** panneau, cliquez sur **+ ajouter une stratégie**.</span><span class="sxs-lookup"><span data-stu-id="42fef-106">In hello **Backup policy** blade, click **+ Add policy**.</span></span>

    ![Add-backup-policy](./media/storsimple-8000-take-backup/step8takebu2.png)

3. <span data-ttu-id="42fef-108">Bonjour **créer la stratégie de sauvegarde** panneau, fournissez un nom qui contient entre 3 et 150 caractères pour votre stratégie de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="42fef-108">In hello **Create backup policy** blade, supply a name that contains between 3 and 150 characters for your backup policy.</span></span>

4. <span data-ttu-id="42fef-109">Sélectionnez toobe de volumes hello sauvegardé.</span><span class="sxs-lookup"><span data-stu-id="42fef-109">Select hello volumes toobe backed up.</span></span> <span data-ttu-id="42fef-110">Si vous sélectionnez plusieurs volumes, ces volumes sont toocreate ensemble groupée une sauvegarde avec cohérence d’incident.</span><span class="sxs-lookup"><span data-stu-id="42fef-110">If you select more than one volume, these volumes are grouped together toocreate a crash-consistent backup.</span></span>

    ![Add-backup-policy](./media/storsimple-8000-take-backup/step8takebu4.png)

5. <span data-ttu-id="42fef-112">Dans le panneau **Ajouter la première planification** :</span><span class="sxs-lookup"><span data-stu-id="42fef-112">On **Add first schedule** blade:</span></span>

    1. <span data-ttu-id="42fef-113">Sélectionnez le type hello de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="42fef-113">Select hello type of backup.</span></span> <span data-ttu-id="42fef-114">Pour une restauration plus rapide, sélectionnez Instantané **local**.</span><span class="sxs-lookup"><span data-stu-id="42fef-114">For faster restores, select **Local** snapshot.</span></span> <span data-ttu-id="42fef-115">Pour la résilience des données, sélectionnez Instantané **cloud**.</span><span class="sxs-lookup"><span data-stu-id="42fef-115">For data resiliency, select **Cloud** snapshot.</span></span>
    2. <span data-ttu-id="42fef-116">Spécifiez la fréquence de sauvegarde hello en minutes, heures, jours ou semaines.</span><span class="sxs-lookup"><span data-stu-id="42fef-116">Specify hello backup frequency in minutes, hours, days, or weeks.</span></span>
    3. <span data-ttu-id="42fef-117">Sélectionnez une durée de conservation.</span><span class="sxs-lookup"><span data-stu-id="42fef-117">Select a retention time.</span></span> <span data-ttu-id="42fef-118">choix de rétention Hello dépend de la fréquence de sauvegarde hello.</span><span class="sxs-lookup"><span data-stu-id="42fef-118">hello retention choices depend on hello backup frequency.</span></span> <span data-ttu-id="42fef-119">Par exemple, pour une stratégie quotidienne, rétention de hello peut être spécifiée en semaines, tandis que la rétention pour une stratégie mensuelle est en mois.</span><span class="sxs-lookup"><span data-stu-id="42fef-119">For example, for a daily policy, hello retention can be specified in weeks, whereas retention for a monthly policy is in months.</span></span>
    4. <span data-ttu-id="42fef-120">Sélectionnez hello à partir des date et heure pour la stratégie de sauvegarde hello.</span><span class="sxs-lookup"><span data-stu-id="42fef-120">Select hello starting time and date for hello backup policy.</span></span>
    5. <span data-ttu-id="42fef-121">Cliquez sur **OK** stratégie de sauvegarde toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="42fef-121">Click **OK** toocreate hello backup policy.</span></span>

        ![Add-backup-policy](./media/storsimple-8000-take-backup/step8takebu5.png) 

6. <span data-ttu-id="42fef-123">Cliquez sur **créer** la création de stratégie de sauvegarde toostart hello.</span><span class="sxs-lookup"><span data-stu-id="42fef-123">Click **Create** toostart hello backup policy creation.</span></span> <span data-ttu-id="42fef-124">Vous êtes averti lorsque la stratégie de sauvegarde hello est créé avec succès.</span><span class="sxs-lookup"><span data-stu-id="42fef-124">You are notified when hello backup policy is successfully created.</span></span> <span data-ttu-id="42fef-125">Hello liste des stratégies de sauvegarde est également mise à jour.</span><span class="sxs-lookup"><span data-stu-id="42fef-125">hello list of backup policies is also updated.</span></span>
      
      ![Add-backup-policy](./media/storsimple-8000-take-backup/step8takebu9.png)
      
      <span data-ttu-id="42fef-127">Vous disposez maintenant d’une stratégie de sauvegarde, qui crée des sauvegardes planifiées des données de volume.</span><span class="sxs-lookup"><span data-stu-id="42fef-127">You now have a backup policy that creates scheduled backups of your volume data.</span></span>




