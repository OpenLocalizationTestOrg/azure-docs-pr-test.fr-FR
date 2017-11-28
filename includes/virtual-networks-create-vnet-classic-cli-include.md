## <a name="how-to-create-a-classic-vnet-using-azure-cli"></a><span data-ttu-id="24e2b-101">Création d'un réseau virtuel classique à l'aide de l'interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="24e2b-101">How to create a classic VNet using Azure CLI</span></span>
<span data-ttu-id="24e2b-102">Vous pouvez utiliser l'interface de ligne de commande Azure pour gérer vos ressources Azure à partir de l'invite de commande sur n'importe quel ordinateur exécutant Windows, Linux ou OSX.</span><span class="sxs-lookup"><span data-stu-id="24e2b-102">You can use the Azure CLI to manage your Azure resources from the command prompt from any computer running Windows, Linux, or OSX.</span></span> <span data-ttu-id="24e2b-103">Pour créer un réseau virtuel à l'aide de l'interface de ligne de commande Azure, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="24e2b-103">To create a VNet by using the Azure CLI, follow the steps below.</span></span>

1. <span data-ttu-id="24e2b-104">Si vous n’avez jamais utilisé l’interface de ligne de commande Azure, voir [Installation et configuration de l’interface de ligne de commande Azure](../articles/cli-install-nodejs.md) et suivez les instructions jusqu’à l’étape où vous sélectionnez votre compte et votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="24e2b-104">If you have never used Azure CLI, see [Install and Configure the Azure CLI](../articles/cli-install-nodejs.md) and follow the instructions up to the point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="24e2b-105">Exécutez la commande **azure network vnet create** pour créer un réseau virtuel et un sous-réseau, comme illustré ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="24e2b-105">Run the **azure network vnet create** command to create a VNet and a subnet, as shown below.</span></span> <span data-ttu-id="24e2b-106">La liste affichée après le résultat présente les différents paramètres utilisés.</span><span class="sxs-lookup"><span data-stu-id="24e2b-106">The list shown after the output explains the parameters used.</span></span>
   
            azure network vnet create --vnet TestVNet -e 192.168.0.0 -i 16 -n FrontEnd -p 192.168.1.0 -r 24 -l "Central US"
   
    <span data-ttu-id="24e2b-107">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="24e2b-107">Expected output:</span></span>
   
            info:    Executing command network vnet create
            + Looking up network configuration
            + Looking up locations
            + Setting network configuration
            info:    network vnet create command OK
   
   * <span data-ttu-id="24e2b-108">**--vnet**.</span><span class="sxs-lookup"><span data-stu-id="24e2b-108">**--vnet**.</span></span> <span data-ttu-id="24e2b-109">Nom du réseau virtuel à créer.</span><span class="sxs-lookup"><span data-stu-id="24e2b-109">Name of the VNet to be created.</span></span> <span data-ttu-id="24e2b-110">Pour notre scénario, *TestVNet*</span><span class="sxs-lookup"><span data-stu-id="24e2b-110">For our scenario, *TestVNet*</span></span>
   * <span data-ttu-id="24e2b-111">**-e (ou --address-space)**.</span><span class="sxs-lookup"><span data-stu-id="24e2b-111">**-e (or --address-space)**.</span></span> <span data-ttu-id="24e2b-112">Espace d'adressage du réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="24e2b-112">VNet address space.</span></span> <span data-ttu-id="24e2b-113">Pour notre scénario, *192.168.0.0*</span><span class="sxs-lookup"><span data-stu-id="24e2b-113">For our scenario, *192.168.0.0*</span></span>
   * <span data-ttu-id="24e2b-114">**-i (ou -cidr)**.</span><span class="sxs-lookup"><span data-stu-id="24e2b-114">**-i (or -cidr)**.</span></span> <span data-ttu-id="24e2b-115">Masque de réseau au format CIDR.</span><span class="sxs-lookup"><span data-stu-id="24e2b-115">Network mask in CIDR format.</span></span> <span data-ttu-id="24e2b-116">Pour notre scénario, *16*.</span><span class="sxs-lookup"><span data-stu-id="24e2b-116">For our scenario, *16*.</span></span>
   * <span data-ttu-id="24e2b-117">**-n (ou --subnet-name**).</span><span class="sxs-lookup"><span data-stu-id="24e2b-117">**-n (or --subnet-name**).</span></span> <span data-ttu-id="24e2b-118">Nom du premier sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="24e2b-118">Name of the first subnet.</span></span> <span data-ttu-id="24e2b-119">Pour notre scénario, *FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="24e2b-119">For our scenario, *FrontEnd*.</span></span>
   * <span data-ttu-id="24e2b-120">**-p (ou --subnet-start-ip)**.</span><span class="sxs-lookup"><span data-stu-id="24e2b-120">**-p (or --subnet-start-ip)**.</span></span> <span data-ttu-id="24e2b-121">Adresse IP de début pour le sous-réseau, ou espace d'adressage du sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="24e2b-121">Starting IP address for subnet, or subnet address space.</span></span> <span data-ttu-id="24e2b-122">Pour notre scénario, *192.168.1.0*.</span><span class="sxs-lookup"><span data-stu-id="24e2b-122">For our scenario, *192.168.1.0*.</span></span>
   * <span data-ttu-id="24e2b-123">**-r (ou --subnet-cidr)**.</span><span class="sxs-lookup"><span data-stu-id="24e2b-123">**-r (or --subnet-cidr)**.</span></span> <span data-ttu-id="24e2b-124">Masque de réseau au format CIDR pour le sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="24e2b-124">Network mask in CIDR format for subnet.</span></span> <span data-ttu-id="24e2b-125">Pour notre scénario, *24*.</span><span class="sxs-lookup"><span data-stu-id="24e2b-125">For our scenario, *24*.</span></span>
   * <span data-ttu-id="24e2b-126">**-l (ou --location)**.</span><span class="sxs-lookup"><span data-stu-id="24e2b-126">**-l (or --location)**.</span></span> <span data-ttu-id="24e2b-127">Région Azure où le réseau virtuel doit être créé.</span><span class="sxs-lookup"><span data-stu-id="24e2b-127">Azure region where the VNet will be created.</span></span> <span data-ttu-id="24e2b-128">Pour notre scénario, *Centre des États-Unis*.</span><span class="sxs-lookup"><span data-stu-id="24e2b-128">For our scenario, *Central US*.</span></span>
3. <span data-ttu-id="24e2b-129">Exécutez la commande **azure network vnet subnet create** pour créer un sous-réseau, comme illustré ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="24e2b-129">Run the **azure network vnet subnet create** command to create a subnet as shown below.</span></span> <span data-ttu-id="24e2b-130">La liste affichée après le résultat présente les différents paramètres utilisés.</span><span class="sxs-lookup"><span data-stu-id="24e2b-130">The list shown after the output explains the parameters used.</span></span>
   
            azure network vnet subnet create -t TestVNet -n BackEnd -a 192.168.2.0/24
   
    <span data-ttu-id="24e2b-131">Voici le résultat attendu pour la commande ci-dessus :</span><span class="sxs-lookup"><span data-stu-id="24e2b-131">Here is the expected output for the command above:</span></span>
   
            info:    Executing command network vnet subnet create
            + Looking up network configuration
            + Creating subnet "BackEnd"
            + Setting network configuration
            + Looking up the subnet "BackEnd"
            + Looking up network configuration
            data:    Name                            : BackEnd
            data:    Address prefix                  : 192.168.2.0/24
            info:    network vnet subnet create command OK
   
   * <span data-ttu-id="24e2b-132">**-t (ou --vnet-name**.</span><span class="sxs-lookup"><span data-stu-id="24e2b-132">**-t (or --vnet-name**.</span></span> <span data-ttu-id="24e2b-133">Nom du réseau virtuel où sera créé le sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="24e2b-133">Name of the VNet where the subnet will be created.</span></span> <span data-ttu-id="24e2b-134">Pour notre scénario, *TestVNet*.</span><span class="sxs-lookup"><span data-stu-id="24e2b-134">For our scenario, *TestVNet*.</span></span>
   * <span data-ttu-id="24e2b-135">**-n (ou --name)**.</span><span class="sxs-lookup"><span data-stu-id="24e2b-135">**-n (or --name)**.</span></span> <span data-ttu-id="24e2b-136">Nom du nouveau sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="24e2b-136">Name of the new subnet.</span></span> <span data-ttu-id="24e2b-137">Pour notre scénario, *BackEnd*.</span><span class="sxs-lookup"><span data-stu-id="24e2b-137">For our scenario, *BackEnd*.</span></span>
   * <span data-ttu-id="24e2b-138">**-a (ou --address-prefix)**.</span><span class="sxs-lookup"><span data-stu-id="24e2b-138">**-a (or --address-prefix)**.</span></span> <span data-ttu-id="24e2b-139">Bloc CIDR de sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="24e2b-139">Subnet CIDR block.</span></span> <span data-ttu-id="24e2b-140">Pour notre scénario, *192.168.2.0/24*.</span><span class="sxs-lookup"><span data-stu-id="24e2b-140">Four our scenario, *192.168.2.0/24*.</span></span>
4. <span data-ttu-id="24e2b-141">Exécutez la commande **azure network vnet show** pour afficher les propriétés du nouveau réseau virtuel, comme illustré ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="24e2b-141">Run the **azure network vnet show** command to view the properties of the new vnet, as shown below.</span></span>
   
            azure network vnet show
   
    <span data-ttu-id="24e2b-142">Voici le résultat attendu pour la commande ci-dessus :</span><span class="sxs-lookup"><span data-stu-id="24e2b-142">Here is the expected output for the command above:</span></span>
   
            info:    Executing command network vnet show
            Virtual network name: TestVNet
            + Looking up the virtual network sites
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

