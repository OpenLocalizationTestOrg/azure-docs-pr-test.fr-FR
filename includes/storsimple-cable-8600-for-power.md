<!--author=alkohli last changed: 9/16/15-->


#### <a name="to-cable-your-device-for-power"></a><span data-ttu-id="6c1e1-101">Raccorder votre appareil à l'alimentation électrique</span><span class="sxs-lookup"><span data-stu-id="6c1e1-101">To cable your device for power</span></span>
> [!NOTE]
> <span data-ttu-id="6c1e1-102">Les deux boîtiers sur votre appareil StorSimple incluent des PCM redondants.</span><span class="sxs-lookup"><span data-stu-id="6c1e1-102">Both enclosures on your StorSimple device include redundant PCMs.</span></span> <span data-ttu-id="6c1e1-103">Pour chaque boîtier, les PCM doivent être installés et connectés à des sources d'alimentation différentes pour garantir une haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="6c1e1-103">For each enclosure, the PCMs must be installed and connected to different power sources to ensure high availability.</span></span>
> 
> 

1. <span data-ttu-id="6c1e1-104">Assurez-vous que les commutateurs d’alimentation sont en position d’arrêt sur tous les PCM.</span><span class="sxs-lookup"><span data-stu-id="6c1e1-104">Make sure that the power switches on all the PCMs are in the OFF position.</span></span>
2. <span data-ttu-id="6c1e1-105">Dans le boîtier principal, branchez les câbles d'alimentation aux deux PCM.</span><span class="sxs-lookup"><span data-stu-id="6c1e1-105">On the primary enclosure, connect the power cords to both PCMs.</span></span> <span data-ttu-id="6c1e1-106">Les câbles d'alimentation sont représentés en rouge dans le schéma de branchement des câbles d'alimentation suivant.</span><span class="sxs-lookup"><span data-stu-id="6c1e1-106">The power cords are identified in red in the power cabling diagram, below.</span></span>
3. <span data-ttu-id="6c1e1-107">Vérifiez que les deux PCM du boîtier principal utilisent des sources d'alimentation distinctes.</span><span class="sxs-lookup"><span data-stu-id="6c1e1-107">Make sure that the two PCMs on the primary enclosure use separate power sources.</span></span>
4. <span data-ttu-id="6c1e1-108">Fixez les câbles d'alimentation aux unités de distribution de l'alimentation du rack, comme illustré sur le schéma de branchement des câbles d'alimentation suivant.</span><span class="sxs-lookup"><span data-stu-id="6c1e1-108">Attach the power cords to the power on the rack distribution units as shown in the power cabling diagram.</span></span>
5. <span data-ttu-id="6c1e1-109">Répétez les étapes 2 à 4 pour le boîtier EBOD.</span><span class="sxs-lookup"><span data-stu-id="6c1e1-109">Repeat steps 2 through 4 for the EBOD enclosure.</span></span>
6. <span data-ttu-id="6c1e1-110">Activez le boîtier EBOD en positionnant les commutateurs d'alimentation de chaque PCM sur ON.</span><span class="sxs-lookup"><span data-stu-id="6c1e1-110">Turn on the EBOD enclosure by flipping the power switch on each PCM to the ON position.</span></span>
7. <span data-ttu-id="6c1e1-111">Assurez-vous que le boîtier EBOD est activé en vérifiant que les LED vertes à l'arrière du contrôleur EBOD sont allumées.</span><span class="sxs-lookup"><span data-stu-id="6c1e1-111">Verify that the EBOD enclosure is turned on by checking that the green LEDs on the back of the EBOD controller are turned ON.</span></span>
8. <span data-ttu-id="6c1e1-112">Activez le boîtier principal en positionnant chaque commutateur d'alimentation de PCM sur ON.</span><span class="sxs-lookup"><span data-stu-id="6c1e1-112">Turn on the primary enclosure by flipping each PCM switch to the ON position.</span></span>
9. <span data-ttu-id="6c1e1-113">Assurez-vous que le système fonctionne en vérifiant que les LED du contrôleur sont allumés.</span><span class="sxs-lookup"><span data-stu-id="6c1e1-113">Verify that the system is on by ensuring the device controller LEDs have turned ON.</span></span>
10. <span data-ttu-id="6c1e1-114">Assurez-vous que la connexion entre le contrôleur EBOD et le contrôleur de l'appareil est active en vérifiant que les quatre LED à côté du port SAS sur le contrôleur du boîtier EBOD sont vertes.</span><span class="sxs-lookup"><span data-stu-id="6c1e1-114">Make sure that the connection between the EBOD controller and the device controller is active by verifying that the four LEDs next to the SAS port on the EBOD controller are green.</span></span>
    
    > [!IMPORTANT]
    > <span data-ttu-id="6c1e1-115">Pour garantir une haute disponibilité de votre système, nous vous recommandons de vous conformer strictement au schéma de branchement des câbles d'alimentation illustré dans le diagramme suivant.</span><span class="sxs-lookup"><span data-stu-id="6c1e1-115">To ensure high availability for your system, we recommend that you strictly adhere to the power cabling scheme shown in the following diagram.</span></span>
    > 
    > 
    
    ![Raccorder votre appareil à l’alimentation électrique](./media/storsimple-cable-8600-for-power/HCSCableYour4UDeviceforPower.png)
    
    <span data-ttu-id="6c1e1-117">**Branchement des câbles d’alimentation**</span><span class="sxs-lookup"><span data-stu-id="6c1e1-117">**Power cabling**</span></span>
    
    | <span data-ttu-id="6c1e1-118">Étiquette</span><span class="sxs-lookup"><span data-stu-id="6c1e1-118">Label</span></span> | <span data-ttu-id="6c1e1-119">Description</span><span class="sxs-lookup"><span data-stu-id="6c1e1-119">Description</span></span> |
    |:--- |:--- |
    | <span data-ttu-id="6c1e1-120">1</span><span class="sxs-lookup"><span data-stu-id="6c1e1-120">1</span></span> |<span data-ttu-id="6c1e1-121">Boîtier principal</span><span class="sxs-lookup"><span data-stu-id="6c1e1-121">Primary enclosure</span></span> |
    | <span data-ttu-id="6c1e1-122">2</span><span class="sxs-lookup"><span data-stu-id="6c1e1-122">2</span></span> |<span data-ttu-id="6c1e1-123">PCM 0</span><span class="sxs-lookup"><span data-stu-id="6c1e1-123">PCM 0</span></span> |
    | <span data-ttu-id="6c1e1-124">3</span><span class="sxs-lookup"><span data-stu-id="6c1e1-124">3</span></span> |<span data-ttu-id="6c1e1-125">PCM 1</span><span class="sxs-lookup"><span data-stu-id="6c1e1-125">PCM 1</span></span> |
    | <span data-ttu-id="6c1e1-126">4</span><span class="sxs-lookup"><span data-stu-id="6c1e1-126">4</span></span> |<span data-ttu-id="6c1e1-127">Contrôleur 0</span><span class="sxs-lookup"><span data-stu-id="6c1e1-127">Controller 0</span></span> |
    | <span data-ttu-id="6c1e1-128">5</span><span class="sxs-lookup"><span data-stu-id="6c1e1-128">5</span></span> |<span data-ttu-id="6c1e1-129">Contrôleur 1</span><span class="sxs-lookup"><span data-stu-id="6c1e1-129">Controller 1</span></span> |
    | <span data-ttu-id="6c1e1-130">6</span><span class="sxs-lookup"><span data-stu-id="6c1e1-130">6</span></span> |<span data-ttu-id="6c1e1-131">Contrôleur 0 du boîtier EBOD</span><span class="sxs-lookup"><span data-stu-id="6c1e1-131">EBOD controller 0</span></span> |
    | <span data-ttu-id="6c1e1-132">7</span><span class="sxs-lookup"><span data-stu-id="6c1e1-132">7</span></span> |<span data-ttu-id="6c1e1-133">Contrôleur 1 du boîtier EBOD</span><span class="sxs-lookup"><span data-stu-id="6c1e1-133">EBOD controller 1</span></span> |
    | <span data-ttu-id="6c1e1-134">8</span><span class="sxs-lookup"><span data-stu-id="6c1e1-134">8</span></span> |<span data-ttu-id="6c1e1-135">Boîtier EBOD</span><span class="sxs-lookup"><span data-stu-id="6c1e1-135">EBOD enclosure</span></span> |
    | <span data-ttu-id="6c1e1-136">9</span><span class="sxs-lookup"><span data-stu-id="6c1e1-136">9</span></span> |<span data-ttu-id="6c1e1-137">PDU</span><span class="sxs-lookup"><span data-stu-id="6c1e1-137">PDUs</span></span> |

