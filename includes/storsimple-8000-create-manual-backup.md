
<!--author=alkohli last changed: 01/20/2017-->

#### <a name="toocreate-a-manual-backup"></a><span data-ttu-id="6f894-101">toocreate une sauvegarde manuelle</span><span class="sxs-lookup"><span data-stu-id="6f894-101">toocreate a manual backup</span></span>

1. <span data-ttu-id="6f894-102">Atteindre le service du Gestionnaire de périphériques StorSimple tooyour, puis cliquez sur **périphériques**.</span><span class="sxs-lookup"><span data-stu-id="6f894-102">Go tooyour StorSimple Device Manager service and then click **Devices**.</span></span> <span data-ttu-id="6f894-103">À partir de hello Liste tabulaire des périphériques, sélectionnez votre appareil.</span><span class="sxs-lookup"><span data-stu-id="6f894-103">From hello tabular listing of devices, select your device.</span></span> <span data-ttu-id="6f894-104">Accédez trop**Paramètres > Gérer > stratégies de sauvegarde**.</span><span class="sxs-lookup"><span data-stu-id="6f894-104">Go too**Settings > Manage > Backup policies**.</span></span>

2. <span data-ttu-id="6f894-105">Hello **stratégies de sauvegarde** panneau répertorie toutes les stratégies de sauvegarde hello dans un format tabulaire, y compris la stratégie hello pour hello volume souhaité tooback des.</span><span class="sxs-lookup"><span data-stu-id="6f894-105">hello **Backup policies** blade lists all hello backup policies in a tabular format, including hello policy for hello volume that you want tooback up.</span></span> <span data-ttu-id="6f894-106">Sélectionnez stratégie hello associée hello volume de tooback haut et menu contextuel tooinvoke hello.</span><span class="sxs-lookup"><span data-stu-id="6f894-106">Select hello policy associated with hello volume you want tooback up and right-click tooinvoke hello context menu.</span></span> <span data-ttu-id="6f894-107">Dans la liste déroulante de hello, sélectionnez **sauvegarder maintenant**.</span><span class="sxs-lookup"><span data-stu-id="6f894-107">From hello dropdown list, select **Back up now**.</span></span>

    ![Création d’une sauvegarde manuelle](./media/storsimple-8000-create-manual-backup/createmanualbu1.png)

3. <span data-ttu-id="6f894-109">Bonjour **sauvegarder maintenant** panneau, hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="6f894-109">In hello **Back up now** blade, do hello following steps:</span></span>

    1. <span data-ttu-id="6f894-110">Choisissez hello approprié **type instantané** à partir de la liste déroulante de hello : **Local** instantané ou **Cloud** instantané.</span><span class="sxs-lookup"><span data-stu-id="6f894-110">Choose hello appropriate **Snapshot type** from hello dropdown list: **Local** snapshot or **Cloud** snapshot.</span></span> <span data-ttu-id="6f894-111">Sélectionnez une capture instantanée locale pour les restaurations ou sauvegardes rapides et une capture instantanée cloud pour la résilience des données.</span><span class="sxs-lookup"><span data-stu-id="6f894-111">Select local snapshot for fast backups or restores, and cloud snapshot for data resiliency.</span></span>

        ![Création d’une sauvegarde manuelle](./media/storsimple-8000-create-manual-backup/createmanualbu2.png)

    2. <span data-ttu-id="6f894-113">Cliquez sur **OK** toostart un toocreate de travail un instantané.</span><span class="sxs-lookup"><span data-stu-id="6f894-113">Click **OK** toostart a job toocreate a snapshot.</span></span> <span data-ttu-id="6f894-114">Vous voyez une notification en hello haut hello après que hello tâche est créée.</span><span class="sxs-lookup"><span data-stu-id="6f894-114">You will see a notification at hello top of hello page after hello job is successfully created.</span></span>

        ![Création d’une sauvegarde manuelle](./media/storsimple-8000-create-manual-backup/createmanualbu4.png)

    3. <span data-ttu-id="6f894-116">toomonitor hello des tâches, cliquez sur la notification de hello.</span><span class="sxs-lookup"><span data-stu-id="6f894-116">toomonitor hello job, click hello notification.</span></span> <span data-ttu-id="6f894-117">Vous accéderez toohello **travaux** panneau où vous pouvez afficher la progression de la tâche hello.</span><span class="sxs-lookup"><span data-stu-id="6f894-117">This takes you toohello **Jobs** blade where you can view hello job progress.</span></span>


5. <span data-ttu-id="6f894-118">À la fin du travail de sauvegarde hello, accédez à toohello **catalogue de sauvegarde** onglet.</span><span class="sxs-lookup"><span data-stu-id="6f894-118">After hello backup job is finished, go toohello **Backup catalog** tab.</span></span>

6. <span data-ttu-id="6f894-119">Définir le périphérique approprié du toohello sélections filtre hello, la stratégie de sauvegarde et plage de temps.</span><span class="sxs-lookup"><span data-stu-id="6f894-119">Set hello filter selections toohello appropriate device, backup policy, and time range.</span></span> <span data-ttu-id="6f894-120">sauvegarde de Hello doit apparaître dans la liste de hello des jeux de sauvegarde qui s’affiche dans le catalogue de hello.</span><span class="sxs-lookup"><span data-stu-id="6f894-120">hello backup should appear in hello list of backup sets that is displayed in hello catalog.</span></span>

