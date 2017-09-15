### <span data-ttu-id="894e6-101"><a name="noconnection"></a>Pour modifier des préfixes d’adresses IP de passerelle de réseau local - sans connexion de passerelle</span><span class="sxs-lookup"><span data-stu-id="894e6-101"><a name="noconnection"></a>To modify local network gateway IP address prefixes - no gateway connection</span></span>

#### <a name="to-add-additional-address-prefixes"></a><span data-ttu-id="894e6-102">Pour ajouter des préfixes d’adresses :</span><span class="sxs-lookup"><span data-stu-id="894e6-102">To add additional address prefixes:</span></span>

1. <span data-ttu-id="894e6-103">Sur la ressource de la passerelle de réseau local, dans la section **Paramètres** , cliquez sur **Configuration**.</span><span class="sxs-lookup"><span data-stu-id="894e6-103">On the Local Network Gateway resource, in the **Settings** section, click **Configuration**.</span></span>
2. <span data-ttu-id="894e6-104">Ajoutez l’espace d’adressage IP dans la zone *Ajouter une autre plage d’adresses*.</span><span class="sxs-lookup"><span data-stu-id="894e6-104">Add the IP address space in the *Add additional address range* box.</span></span>
3. <span data-ttu-id="894e6-105">Cliquez sur **Save** pour enregistrer vos paramètres.</span><span class="sxs-lookup"><span data-stu-id="894e6-105">Click **Save** to save your settings.</span></span>

#### <a name="to-remove-address-prefixes"></a><span data-ttu-id="894e6-106">Pour supprimer des préfixes d’adresses :</span><span class="sxs-lookup"><span data-stu-id="894e6-106">To remove address prefixes:</span></span>

1. <span data-ttu-id="894e6-107">Sur la ressource de la passerelle de réseau local, dans la section **Paramètres** , cliquez sur **Configuration**.</span><span class="sxs-lookup"><span data-stu-id="894e6-107">On the Local Network Gateway resource, in the **Settings** section, click **Configuration**.</span></span>
2. <span data-ttu-id="894e6-108">Cliquez sur **’...’**</span><span class="sxs-lookup"><span data-stu-id="894e6-108">Click the **'...'**</span></span> <span data-ttu-id="894e6-109">sur la ligne qui contient le préfixe que vous souhaitez supprimer.</span><span class="sxs-lookup"><span data-stu-id="894e6-109">on the line containing the prefix you want to remove.</span></span>
3. <span data-ttu-id="894e6-110">Cliquez sur **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="894e6-110">Click **Remove**.</span></span>
4. <span data-ttu-id="894e6-111">Cliquez sur **Save** pour enregistrer vos paramètres.</span><span class="sxs-lookup"><span data-stu-id="894e6-111">Click **Save** to save your settings.</span></span>

### <span data-ttu-id="894e6-112"><a name="withconnection"></a>Pour modifier des préfixes d’adresses IP de passerelle de réseau local - avec une connexion de passerelle existante</span><span class="sxs-lookup"><span data-stu-id="894e6-112"><a name="withconnection"></a>To modify local network gateway IP address prefixes - existing gateway connection</span></span>

<span data-ttu-id="894e6-113">Si vous disposez d’une connexion de passerelle et que vous souhaitez ajouter ou supprimer des préfixes d’adresses IP contenues dans votre passerelle de réseau local, vous devez suivre les étapes suivantes dans l’ordre.</span><span class="sxs-lookup"><span data-stu-id="894e6-113">If you have a gateway connection and want to add or remove the IP address prefixes contained in your local network gateway, you need to do the following steps, in order.</span></span> <span data-ttu-id="894e6-114">Cela entraînera une interruption de votre connexion VPN.</span><span class="sxs-lookup"><span data-stu-id="894e6-114">This results in some downtime for your VPN connection.</span></span> <span data-ttu-id="894e6-115">Lorsque vous modifiez des préfixes d’adresses IP, vous n’avez pas besoin de supprimer la passerelle VPN.</span><span class="sxs-lookup"><span data-stu-id="894e6-115">When modifying IP address prefixes, you don't need to delete the VPN gateway.</span></span> <span data-ttu-id="894e6-116">Vous devez uniquement supprimer la connexion.</span><span class="sxs-lookup"><span data-stu-id="894e6-116">You only need to remove the connection.</span></span>

#### <a name="1-remove-the-connection"></a><span data-ttu-id="894e6-117">1. Supprimez la connexion.</span><span class="sxs-lookup"><span data-stu-id="894e6-117">1. Remove the connection.</span></span>

1. <span data-ttu-id="894e6-118">Sur la ressource de la passerelle de réseau local, dans la section **Paramètres**, cliquez sur **Connexions**.</span><span class="sxs-lookup"><span data-stu-id="894e6-118">On the Local Network Gateway resource, in the **Settings** section, click **Connections**.</span></span>
2. <span data-ttu-id="894e6-119">Cliquez sur **...**  sur la ligne pour chaque connexion, puis cliquez sur **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="894e6-119">Click the **...** on the line for each connection, then click **Delete**.</span></span>
3. <span data-ttu-id="894e6-120">Cliquez sur **Save** pour enregistrer vos paramètres.</span><span class="sxs-lookup"><span data-stu-id="894e6-120">Click **Save** to save your settings.</span></span>

#### <a name="2-modify-the-address-prefixes"></a><span data-ttu-id="894e6-121">2. Modifiez les préfixes d’adresse.</span><span class="sxs-lookup"><span data-stu-id="894e6-121">2. Modify the address prefixes.</span></span>

<span data-ttu-id="894e6-122">Pour ajouter des préfixes d’adresses :</span><span class="sxs-lookup"><span data-stu-id="894e6-122">To add additional address prefixes:</span></span>

1. <span data-ttu-id="894e6-123">Sur la ressource de la passerelle de réseau local, dans la section **Paramètres** , cliquez sur **Configuration**.</span><span class="sxs-lookup"><span data-stu-id="894e6-123">On the Local Network Gateway resource, in the **Settings** section, click **Configuration**.</span></span>
2. <span data-ttu-id="894e6-124">Ajoutez l’espace d’adressage IP.</span><span class="sxs-lookup"><span data-stu-id="894e6-124">Add the IP address space.</span></span>
3. <span data-ttu-id="894e6-125">Cliquez sur **Save** pour enregistrer vos paramètres.</span><span class="sxs-lookup"><span data-stu-id="894e6-125">Click **Save** to save your settings.</span></span>

<span data-ttu-id="894e6-126">Pour supprimer des préfixes d’adresses :</span><span class="sxs-lookup"><span data-stu-id="894e6-126">To remove address prefixes:</span></span>

1. <span data-ttu-id="894e6-127">Sur la ressource de la passerelle de réseau local, dans la section **Paramètres** , cliquez sur **Configuration**.</span><span class="sxs-lookup"><span data-stu-id="894e6-127">On the Local Network Gateway resource, in the **Settings** section, click **Configuration**.</span></span>
2. <span data-ttu-id="894e6-128">Cliquez sur **...** sur la ligne contenant le préfixe que vous souhaitez supprimer.</span><span class="sxs-lookup"><span data-stu-id="894e6-128">Click the **...** on the line containing the prefix you want to remove.</span></span>
3. <span data-ttu-id="894e6-129">Cliquez sur **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="894e6-129">Click **Remove**.</span></span>
4. <span data-ttu-id="894e6-130">Cliquez sur **Save** pour enregistrer vos paramètres.</span><span class="sxs-lookup"><span data-stu-id="894e6-130">Click **Save** to save your settings.</span></span>

#### <a name="3-recreate-the-connection"></a><span data-ttu-id="894e6-131">3. Recréez la connexion.</span><span class="sxs-lookup"><span data-stu-id="894e6-131">3. Recreate the connection.</span></span>

1. <span data-ttu-id="894e6-132">Accédez à la passerelle de réseau virtuel de votre réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="894e6-132">Navigate to the Virtual Network Gateway for your VNet.</span></span> <span data-ttu-id="894e6-133">(pas la passerelle de réseau local.)</span><span class="sxs-lookup"><span data-stu-id="894e6-133">(Not the Local Network Gateway.)</span></span>
2. <span data-ttu-id="894e6-134">Sur la passerelle de réseau virtuel, dans la section **Paramètres**, cliquez sur **Connexions**.</span><span class="sxs-lookup"><span data-stu-id="894e6-134">On the Virtual Network Gateway, in the **Settings** section, click **Connections**.</span></span>
3. <span data-ttu-id="894e6-135">Cliquez sur **+Ajouter** pour ouvrir le panneau **Ajouter une connexion**.</span><span class="sxs-lookup"><span data-stu-id="894e6-135">Click the **+ Add** to open the **Add connection** blade.</span></span>
4. <span data-ttu-id="894e6-136">Recréez votre connexion.</span><span class="sxs-lookup"><span data-stu-id="894e6-136">Recreate your connection.</span></span>
5. <span data-ttu-id="894e6-137">Cliquez sur **OK** pour créer la connexion.</span><span class="sxs-lookup"><span data-stu-id="894e6-137">Click **OK** to create the connection.</span></span>