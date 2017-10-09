<!--author=alkohli last changed: 9/16/15-->


#### <a name="toocable-your-device-for-power"></a><span data-ttu-id="9db90-101">toocable votre appareil pour l’alimentation</span><span class="sxs-lookup"><span data-stu-id="9db90-101">toocable your device for power</span></span>
> [!NOTE]
> <span data-ttu-id="9db90-102">Les deux boîtiers sur votre appareil StorSimple incluent des PCM redondants.</span><span class="sxs-lookup"><span data-stu-id="9db90-102">Both enclosures on your StorSimple device include redundant PCMs.</span></span> <span data-ttu-id="9db90-103">Pour chaque boîtier, hello PCM doit être installé et connecté toodifferent power sources tooensure haut niveau de disponibilité.</span><span class="sxs-lookup"><span data-stu-id="9db90-103">For each enclosure, hello PCMs must be installed and connected toodifferent power sources tooensure high availability.</span></span>
> 
> 

1. <span data-ttu-id="9db90-104">Vous assurer que les interrupteurs d’alimentation hello sur tous les hello PCM sont en position OFF de hello.</span><span class="sxs-lookup"><span data-stu-id="9db90-104">Make sure that hello power switches on all hello PCMs are in hello OFF position.</span></span>
2. <span data-ttu-id="9db90-105">Sur le boîtier principal de hello, se connecter tooboth de câbles d’alimentation hello PCM.</span><span class="sxs-lookup"><span data-stu-id="9db90-105">On hello primary enclosure, connect hello power cords tooboth PCMs.</span></span> <span data-ttu-id="9db90-106">cordons d’alimentation Hello sont indiqués en rouge dans hello câblage d’alimentation diagramme, ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="9db90-106">hello power cords are identified in red in hello power cabling diagram, below.</span></span>
3. <span data-ttu-id="9db90-107">Vérifiez que hello deux PCM sources d’alimentation distinctes utilisez hello boîtier principal.</span><span class="sxs-lookup"><span data-stu-id="9db90-107">Make sure that hello two PCMs on hello primary enclosure use separate power sources.</span></span>
4. <span data-ttu-id="9db90-108">Attachez hello power câbles toohello mise sous tension hello unités de distribution comme indiqué dans le diagramme de câblage de hello.</span><span class="sxs-lookup"><span data-stu-id="9db90-108">Attach hello power cords toohello power on hello rack distribution units as shown in hello power cabling diagram.</span></span>
5. <span data-ttu-id="9db90-109">Répétez les étapes 2 à 4 pour hello boîtiers.</span><span class="sxs-lookup"><span data-stu-id="9db90-109">Repeat steps 2 through 4 for hello EBOD enclosure.</span></span>
6. <span data-ttu-id="9db90-110">Activer les boîtiers hello en interrupteur hello sur chaque position de ON toohello PCM.</span><span class="sxs-lookup"><span data-stu-id="9db90-110">Turn on hello EBOD enclosure by flipping hello power switch on each PCM toohello ON position.</span></span>
7. <span data-ttu-id="9db90-111">Vérifiez que hello boîtiers est activé en vérifiant que hello arrière du contrôleur EBOD hello hello vert voyants sont allumés.</span><span class="sxs-lookup"><span data-stu-id="9db90-111">Verify that hello EBOD enclosure is turned on by checking that hello green LEDs on hello back of hello EBOD controller are turned ON.</span></span>
8. <span data-ttu-id="9db90-112">Allumez le boîtier principal de hello en basculant chaque position de PCM commutateur toohello ON.</span><span class="sxs-lookup"><span data-stu-id="9db90-112">Turn on hello primary enclosure by flipping each PCM switch toohello ON position.</span></span>
9. <span data-ttu-id="9db90-113">Vérifiez que le système de hello est sur en veillant à ce contrôleur de l’appareil hello que DEL ont activé.</span><span class="sxs-lookup"><span data-stu-id="9db90-113">Verify that hello system is on by ensuring hello device controller LEDs have turned ON.</span></span>
10. <span data-ttu-id="9db90-114">Vérifiez que cette connexion hello entre le contrôleur EBOD hello et contrôleur de l’appareil hello est actif en vérifiant que hello quatre DEL suivant toohello port SAS du contrôleur EBOD hello sont verts.</span><span class="sxs-lookup"><span data-stu-id="9db90-114">Make sure that hello connection between hello EBOD controller and hello device controller is active by verifying that hello four LEDs next toohello SAS port on hello EBOD controller are green.</span></span>
    
    > [!IMPORTANT]
    > <span data-ttu-id="9db90-115">tooensure haute disponibilité pour votre système, nous vous recommandons de respecter strictement toohello les schéma illustré hello suivant schéma de câblage.</span><span class="sxs-lookup"><span data-stu-id="9db90-115">tooensure high availability for your system, we recommend that you strictly adhere toohello power cabling scheme shown in hello following diagram.</span></span>
    > 
    > 
    
    ![Raccorder votre appareil à l’alimentation électrique](./media/storsimple-cable-8600-for-power/HCSCableYour4UDeviceforPower.png)
    
    <span data-ttu-id="9db90-117">**Branchement des câbles d’alimentation**</span><span class="sxs-lookup"><span data-stu-id="9db90-117">**Power cabling**</span></span>
    
    | <span data-ttu-id="9db90-118">Étiquette</span><span class="sxs-lookup"><span data-stu-id="9db90-118">Label</span></span> | <span data-ttu-id="9db90-119">Description</span><span class="sxs-lookup"><span data-stu-id="9db90-119">Description</span></span> |
    |:--- |:--- |
    | <span data-ttu-id="9db90-120">1</span><span class="sxs-lookup"><span data-stu-id="9db90-120">1</span></span> |<span data-ttu-id="9db90-121">Boîtier principal</span><span class="sxs-lookup"><span data-stu-id="9db90-121">Primary enclosure</span></span> |
    | <span data-ttu-id="9db90-122">2</span><span class="sxs-lookup"><span data-stu-id="9db90-122">2</span></span> |<span data-ttu-id="9db90-123">PCM 0</span><span class="sxs-lookup"><span data-stu-id="9db90-123">PCM 0</span></span> |
    | <span data-ttu-id="9db90-124">3</span><span class="sxs-lookup"><span data-stu-id="9db90-124">3</span></span> |<span data-ttu-id="9db90-125">PCM 1</span><span class="sxs-lookup"><span data-stu-id="9db90-125">PCM 1</span></span> |
    | <span data-ttu-id="9db90-126">4</span><span class="sxs-lookup"><span data-stu-id="9db90-126">4</span></span> |<span data-ttu-id="9db90-127">Contrôleur 0</span><span class="sxs-lookup"><span data-stu-id="9db90-127">Controller 0</span></span> |
    | <span data-ttu-id="9db90-128">5</span><span class="sxs-lookup"><span data-stu-id="9db90-128">5</span></span> |<span data-ttu-id="9db90-129">Contrôleur 1</span><span class="sxs-lookup"><span data-stu-id="9db90-129">Controller 1</span></span> |
    | <span data-ttu-id="9db90-130">6</span><span class="sxs-lookup"><span data-stu-id="9db90-130">6</span></span> |<span data-ttu-id="9db90-131">Contrôleur 0 du boîtier EBOD</span><span class="sxs-lookup"><span data-stu-id="9db90-131">EBOD controller 0</span></span> |
    | <span data-ttu-id="9db90-132">7</span><span class="sxs-lookup"><span data-stu-id="9db90-132">7</span></span> |<span data-ttu-id="9db90-133">Contrôleur 1 du boîtier EBOD</span><span class="sxs-lookup"><span data-stu-id="9db90-133">EBOD controller 1</span></span> |
    | <span data-ttu-id="9db90-134">8</span><span class="sxs-lookup"><span data-stu-id="9db90-134">8</span></span> |<span data-ttu-id="9db90-135">Boîtier EBOD</span><span class="sxs-lookup"><span data-stu-id="9db90-135">EBOD enclosure</span></span> |
    | <span data-ttu-id="9db90-136">9</span><span class="sxs-lookup"><span data-stu-id="9db90-136">9</span></span> |<span data-ttu-id="9db90-137">PDU</span><span class="sxs-lookup"><span data-stu-id="9db90-137">PDUs</span></span> |

