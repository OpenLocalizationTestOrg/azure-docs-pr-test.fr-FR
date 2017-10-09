## <a name="how-toocreate-a-classic-vnet-using-azure-cli"></a><span data-ttu-id="e281d-101">Comment toocreate un virtuel classique à l’aide de la CLI d’Azure</span><span class="sxs-lookup"><span data-stu-id="e281d-101">How toocreate a classic VNet using Azure CLI</span></span>
<span data-ttu-id="e281d-102">Vous pouvez utiliser hello CLI d’Azure toomanage vos ressources Azure à partir de l’invite de commandes hello à partir de n’importe quel ordinateur exécutant Windows, Linux ou OSX.</span><span class="sxs-lookup"><span data-stu-id="e281d-102">You can use hello Azure CLI toomanage your Azure resources from hello command prompt from any computer running Windows, Linux, or OSX.</span></span> <span data-ttu-id="e281d-103">toocreate un réseau virtuel à l’aide de hello CLI d’Azure, suivez les étapes de hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="e281d-103">toocreate a VNet by using hello Azure CLI, follow hello steps below.</span></span>

1. <span data-ttu-id="e281d-104">Si vous n’avez jamais utilisé CLI d’Azure, consultez [installer et configurer hello CLI d’Azure](../articles/cli-install-nodejs.md) et suivez les instructions de hello point toohello où vous sélectionnez votre compte Azure et votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="e281d-104">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../articles/cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="e281d-105">Exécutez hello **créer un réseau virtuel du réseau azure** commande toocreate un réseau virtuel et un sous-réseau, comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="e281d-105">Run hello **azure network vnet create** command toocreate a VNet and a subnet, as shown below.</span></span> <span data-ttu-id="e281d-106">liste de Hello affiché après la sortie de hello explique paramètres hello utilisés.</span><span class="sxs-lookup"><span data-stu-id="e281d-106">hello list shown after hello output explains hello parameters used.</span></span>
   
            azure network vnet create --vnet TestVNet -e 192.168.0.0 -i 16 -n FrontEnd -p 192.168.1.0 -r 24 -l "Central US"
   
    <span data-ttu-id="e281d-107">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="e281d-107">Expected output:</span></span>
   
            info:    Executing command network vnet create
            + Looking up network configuration
            + Looking up locations
            + Setting network configuration
            info:    network vnet create command OK
   
   * <span data-ttu-id="e281d-108">**--vnet**.</span><span class="sxs-lookup"><span data-stu-id="e281d-108">**--vnet**.</span></span> <span data-ttu-id="e281d-109">Nom de hello toobe de réseau virtuel créé.</span><span class="sxs-lookup"><span data-stu-id="e281d-109">Name of hello VNet toobe created.</span></span> <span data-ttu-id="e281d-110">Pour notre scénario, *TestVNet*</span><span class="sxs-lookup"><span data-stu-id="e281d-110">For our scenario, *TestVNet*</span></span>
   * <span data-ttu-id="e281d-111">**-e (ou --address-space)**.</span><span class="sxs-lookup"><span data-stu-id="e281d-111">**-e (or --address-space)**.</span></span> <span data-ttu-id="e281d-112">Espace d'adressage du réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="e281d-112">VNet address space.</span></span> <span data-ttu-id="e281d-113">Pour notre scénario, *192.168.0.0*</span><span class="sxs-lookup"><span data-stu-id="e281d-113">For our scenario, *192.168.0.0*</span></span>
   * <span data-ttu-id="e281d-114">**-i (ou -cidr)**.</span><span class="sxs-lookup"><span data-stu-id="e281d-114">**-i (or -cidr)**.</span></span> <span data-ttu-id="e281d-115">Masque de réseau au format CIDR.</span><span class="sxs-lookup"><span data-stu-id="e281d-115">Network mask in CIDR format.</span></span> <span data-ttu-id="e281d-116">Pour notre scénario, *16*.</span><span class="sxs-lookup"><span data-stu-id="e281d-116">For our scenario, *16*.</span></span>
   * <span data-ttu-id="e281d-117">**-n (ou --subnet-name**).</span><span class="sxs-lookup"><span data-stu-id="e281d-117">**-n (or --subnet-name**).</span></span> <span data-ttu-id="e281d-118">Nom du sous-réseau de première hello.</span><span class="sxs-lookup"><span data-stu-id="e281d-118">Name of hello first subnet.</span></span> <span data-ttu-id="e281d-119">Pour notre scénario, *FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="e281d-119">For our scenario, *FrontEnd*.</span></span>
   * <span data-ttu-id="e281d-120">**-p (ou --subnet-start-ip)**.</span><span class="sxs-lookup"><span data-stu-id="e281d-120">**-p (or --subnet-start-ip)**.</span></span> <span data-ttu-id="e281d-121">Adresse IP de début pour le sous-réseau, ou espace d'adressage du sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="e281d-121">Starting IP address for subnet, or subnet address space.</span></span> <span data-ttu-id="e281d-122">Pour notre scénario, *192.168.1.0*.</span><span class="sxs-lookup"><span data-stu-id="e281d-122">For our scenario, *192.168.1.0*.</span></span>
   * <span data-ttu-id="e281d-123">**-r (ou --subnet-cidr)**.</span><span class="sxs-lookup"><span data-stu-id="e281d-123">**-r (or --subnet-cidr)**.</span></span> <span data-ttu-id="e281d-124">Masque de réseau au format CIDR pour le sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="e281d-124">Network mask in CIDR format for subnet.</span></span> <span data-ttu-id="e281d-125">Pour notre scénario, *24*.</span><span class="sxs-lookup"><span data-stu-id="e281d-125">For our scenario, *24*.</span></span>
   * <span data-ttu-id="e281d-126">**-l (ou --location)**.</span><span class="sxs-lookup"><span data-stu-id="e281d-126">**-l (or --location)**.</span></span> <span data-ttu-id="e281d-127">Région Azure où hello réseau virtuel sera créé.</span><span class="sxs-lookup"><span data-stu-id="e281d-127">Azure region where hello VNet will be created.</span></span> <span data-ttu-id="e281d-128">Pour notre scénario, *Centre des États-Unis*.</span><span class="sxs-lookup"><span data-stu-id="e281d-128">For our scenario, *Central US*.</span></span>
3. <span data-ttu-id="e281d-129">Exécutez hello **créer de sous-réseau de réseau virtuel azure réseau** commande toocreate un sous-réseau, comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="e281d-129">Run hello **azure network vnet subnet create** command toocreate a subnet as shown below.</span></span> <span data-ttu-id="e281d-130">liste de Hello affiché après la sortie de hello explique paramètres hello utilisés.</span><span class="sxs-lookup"><span data-stu-id="e281d-130">hello list shown after hello output explains hello parameters used.</span></span>
   
            azure network vnet subnet create -t TestVNet -n BackEnd -a 192.168.2.0/24
   
    <span data-ttu-id="e281d-131">Voici la sortie hello attendu pour la commande hello ci-dessus :</span><span class="sxs-lookup"><span data-stu-id="e281d-131">Here is hello expected output for hello command above:</span></span>
   
            info:    Executing command network vnet subnet create
            + Looking up network configuration
            + Creating subnet "BackEnd"
            + Setting network configuration
            + Looking up hello subnet "BackEnd"
            + Looking up network configuration
            data:    Name                            : BackEnd
            data:    Address prefix                  : 192.168.2.0/24
            info:    network vnet subnet create command OK
   
   * <span data-ttu-id="e281d-132">**-t (ou --vnet-name**.</span><span class="sxs-lookup"><span data-stu-id="e281d-132">**-t (or --vnet-name**.</span></span> <span data-ttu-id="e281d-133">Nom de hello réseau virtuel où le sous-réseau de hello doit être créé.</span><span class="sxs-lookup"><span data-stu-id="e281d-133">Name of hello VNet where hello subnet will be created.</span></span> <span data-ttu-id="e281d-134">Pour notre scénario, *TestVNet*.</span><span class="sxs-lookup"><span data-stu-id="e281d-134">For our scenario, *TestVNet*.</span></span>
   * <span data-ttu-id="e281d-135">**-n (ou --name)**.</span><span class="sxs-lookup"><span data-stu-id="e281d-135">**-n (or --name)**.</span></span> <span data-ttu-id="e281d-136">Nom du sous-réseau hello.</span><span class="sxs-lookup"><span data-stu-id="e281d-136">Name of hello new subnet.</span></span> <span data-ttu-id="e281d-137">Pour notre scénario, *BackEnd*.</span><span class="sxs-lookup"><span data-stu-id="e281d-137">For our scenario, *BackEnd*.</span></span>
   * <span data-ttu-id="e281d-138">**-a (ou --address-prefix)**.</span><span class="sxs-lookup"><span data-stu-id="e281d-138">**-a (or --address-prefix)**.</span></span> <span data-ttu-id="e281d-139">Bloc CIDR de sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="e281d-139">Subnet CIDR block.</span></span> <span data-ttu-id="e281d-140">Pour notre scénario, *192.168.2.0/24*.</span><span class="sxs-lookup"><span data-stu-id="e281d-140">Four our scenario, *192.168.2.0/24*.</span></span>
4. <span data-ttu-id="e281d-141">Exécutez hello **afficher de réseau virtuel azure réseau** commande tooview des propriétés de hello de hello nouveau réseau virtuel, comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="e281d-141">Run hello **azure network vnet show** command tooview hello properties of hello new vnet, as shown below.</span></span>
   
            azure network vnet show
   
    <span data-ttu-id="e281d-142">Voici la sortie hello attendu pour la commande hello ci-dessus :</span><span class="sxs-lookup"><span data-stu-id="e281d-142">Here is hello expected output for hello command above:</span></span>
   
            info:    Executing command network vnet show
            Virtual network name: TestVNet
            + Looking up hello virtual network sites
            data:    Name                            : TestVNet
            data:    Location                        : Central US
            data:    State                           : Created
            data:    Address space                   : 192.168.0.0/16
            data:    Subnets:
            data:      Name                          : FrontEnd
            data:      Address prefix                : 192.168.1.0/24
            data:
            data:      Name                          : BackEnd
            data:      Address prefix                : 192.168.2.0/24
            data:
            info:    network vnet show command OK

