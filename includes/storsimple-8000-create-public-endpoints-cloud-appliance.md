#### <a name="toocreate-public-endpoints-on-hello-cloud-appliance"></a><span data-ttu-id="18ecc-101">toocreate des points de terminaison publics sur l’équipement de cloud hello</span><span class="sxs-lookup"><span data-stu-id="18ecc-101">toocreate public endpoints on hello cloud appliance</span></span>

1. <span data-ttu-id="18ecc-102">Se connecter toohello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="18ecc-102">Sign in toohello Azure portal.</span></span>
2. <span data-ttu-id="18ecc-103">Accédez trop**virtuels**, puis sélectionnez et sur l’ordinateur virtuel hello qui est utilisé en tant que votre solution de cloud.</span><span class="sxs-lookup"><span data-stu-id="18ecc-103">Go too**Virtual Machines**, and then select and click hello virtual machine that is being used as your cloud appliance.</span></span>
    
3. <span data-ttu-id="18ecc-104">Vous devez toocreate un flux réseau sécurité (groupe) règle toocontrol hello du trafic vers et depuis votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="18ecc-104">You need toocreate a network security group (NSG) rule toocontrol hello flow of traffic in and out of your virtual machine.</span></span> <span data-ttu-id="18ecc-105">Effectuer hello suivant les étapes toocreate une règle de groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="18ecc-105">Perform hello following steps toocreate an NSG rule.</span></span>
    1. <span data-ttu-id="18ecc-106">Sélectionnez **Groupe de sécurité réseau**.</span><span class="sxs-lookup"><span data-stu-id="18ecc-106">Select **Network security group**.</span></span>
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt1.png)

    2. <span data-ttu-id="18ecc-107">Cliquez sur le groupe de sécurité de réseau de valeur par défaut de hello est présenté.</span><span class="sxs-lookup"><span data-stu-id="18ecc-107">Click hello default network security group that is presented.</span></span>
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt2.png)

    3. <span data-ttu-id="18ecc-108">Sélectionnez **Règles de sécurité de trafic entrant**.</span><span class="sxs-lookup"><span data-stu-id="18ecc-108">Select **Inbound security rules**.</span></span>
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt3.png)

    4. <span data-ttu-id="18ecc-109">Cliquez sur **+ ajouter** toocreate une règle de sécurité de trafic entrant.</span><span class="sxs-lookup"><span data-stu-id="18ecc-109">Click **+ Add** toocreate an inbound security rule.</span></span>
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt4.png)

        <span data-ttu-id="18ecc-110">Dans Panneau de règle hello ajouter sécurité de trafic entrant :</span><span class="sxs-lookup"><span data-stu-id="18ecc-110">In hello Add inbound security rule blade:</span></span>

        1. <span data-ttu-id="18ecc-111">Pourquoi **nom**, tapez ce qui suit hello nom pour le point de terminaison hello : WinRMHttps.</span><span class="sxs-lookup"><span data-stu-id="18ecc-111">For hello **Name**, type hello following name for hello endpoint: WinRMHttps.</span></span>
        
        2. <span data-ttu-id="18ecc-112">Pourquoi **priorité**, sélectionnez un nombre inférieur à 1 000 (qui est la priorité de hello pour la règle par défaut de hello).</span><span class="sxs-lookup"><span data-stu-id="18ecc-112">For hello **Priority**, select a number lesser than 1000 (which is hello priority for hello default rule).</span></span> <span data-ttu-id="18ecc-113">Valeur hello est élevée, une priorité plus faible hello.</span><span class="sxs-lookup"><span data-stu-id="18ecc-113">Higher hello value, lower hello priority.</span></span>

        3. <span data-ttu-id="18ecc-114">Ensemble hello **Source** trop**tout**.</span><span class="sxs-lookup"><span data-stu-id="18ecc-114">Set hello **Source** too**Any**.</span></span>

        4. <span data-ttu-id="18ecc-115">Pourquoi **Service**, sélectionnez **WinRM**.</span><span class="sxs-lookup"><span data-stu-id="18ecc-115">For hello **Service**, select **WinRM**.</span></span> <span data-ttu-id="18ecc-116">Hello **protocole** est défini automatiquement trop**TCP** et hello **étendue du Port** est défini trop**5986**.</span><span class="sxs-lookup"><span data-stu-id="18ecc-116">hello **Protocol** is automatically set too**TCP** and hello **Port range** is set too**5986**.</span></span>

        5. <span data-ttu-id="18ecc-117">Cliquez sur **OK** règle de hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="18ecc-117">Click **OK** toocreate hello rule.</span></span>

            ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt5.png)

4. <span data-ttu-id="18ecc-118">L’étape finale consiste tooassociate groupe de sécurité de votre réseau avec un sous-réseau ou une interface réseau spécifique.</span><span class="sxs-lookup"><span data-stu-id="18ecc-118">Your final step is tooassociate your network security group with a subnet or a specific network interface.</span></span> <span data-ttu-id="18ecc-119">Effectuer hello suivant les étapes tooassociate votre groupe de sécurité réseau avec un sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="18ecc-119">Perform hello following steps tooassociate your network security group with a subnet.</span></span>
    1. <span data-ttu-id="18ecc-120">Accédez trop**sous-réseaux**.</span><span class="sxs-lookup"><span data-stu-id="18ecc-120">Go too**Subnets**.</span></span>
    2. <span data-ttu-id="18ecc-121">Cliquez sur **+ Associer**.</span><span class="sxs-lookup"><span data-stu-id="18ecc-121">Click **+ Associate**.</span></span>
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt7.png)

    3. <span data-ttu-id="18ecc-122">Sélectionnez votre réseau virtuel, puis sous-réseau approprié de hello.</span><span class="sxs-lookup"><span data-stu-id="18ecc-122">Select your virtual network, and then select hello appropriate subnet.</span></span>
    4. <span data-ttu-id="18ecc-123">Cliquez sur **OK** règle de hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="18ecc-123">Click **OK** toocreate hello rule.</span></span>

        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt11.png)

<span data-ttu-id="18ecc-124">Une fois que la règle de hello est créée, vous pouvez afficher son adresse IP virtuelle publique (VIP) de détails toodetermine hello.</span><span class="sxs-lookup"><span data-stu-id="18ecc-124">After hello rule is created, you can view its details toodetermine hello Public Virtual IP (VIP) address.</span></span> <span data-ttu-id="18ecc-125">Enregistrez cette adresse.</span><span class="sxs-lookup"><span data-stu-id="18ecc-125">Record this address.</span></span>


