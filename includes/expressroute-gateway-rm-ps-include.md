<span data-ttu-id="94204-101">étapes Hello pour cette tâche, utilisez un réseau virtuel en fonction des valeurs hello hello suivant liste de référence de configuration.</span><span class="sxs-lookup"><span data-stu-id="94204-101">hello steps for this task use a VNet based on hello values in hello following configuration reference list.</span></span> <span data-ttu-id="94204-102">Les noms et paramètres supplémentaires sont également présentés dans cette liste.</span><span class="sxs-lookup"><span data-stu-id="94204-102">Additional settings and names are also outlined in this list.</span></span> <span data-ttu-id="94204-103">Nous n’utilisons cette liste directement dans une des étapes de hello, bien que nous ajoutez des variables en fonction des valeurs hello dans cette liste.</span><span class="sxs-lookup"><span data-stu-id="94204-103">We don't use this list directly in any of hello steps, although we do add variables based on hello values in this list.</span></span> <span data-ttu-id="94204-104">Vous pouvez copier hello liste toouse en tant que référence, en remplaçant les valeurs hello par les vôtres.</span><span class="sxs-lookup"><span data-stu-id="94204-104">You can copy hello list toouse as a reference, replacing hello values with your own.</span></span>

<span data-ttu-id="94204-105">**Liste de référence de configuration**</span><span class="sxs-lookup"><span data-stu-id="94204-105">**Configuration reference list**</span></span>

* <span data-ttu-id="94204-106">Nom du réseau virtuel : « TestVNet »</span><span class="sxs-lookup"><span data-stu-id="94204-106">Virtual Network Name = "TestVNet"</span></span>
* <span data-ttu-id="94204-107">Espace d’adressage du réseau virtuel : 192.168.0.0/16</span><span class="sxs-lookup"><span data-stu-id="94204-107">Virtual Network address space = 192.168.0.0/16</span></span>
* <span data-ttu-id="94204-108">Groupe de ressources : « TestRG »</span><span class="sxs-lookup"><span data-stu-id="94204-108">Resource Group = "TestRG"</span></span>
* <span data-ttu-id="94204-109">Nom du sous-réseau 1 : « FrontEnd »</span><span class="sxs-lookup"><span data-stu-id="94204-109">Subnet1 Name = "FrontEnd"</span></span> 
* <span data-ttu-id="94204-110">Espace d’adressage du sous-réseau 1 = "192.168.1.0/24"</span><span class="sxs-lookup"><span data-stu-id="94204-110">Subnet1 address space = "192.168.1.0/24"</span></span>
* <span data-ttu-id="94204-111">Nom de sous-réseau de passerelle : « GatewaySubnet » Vous devez toujours nommer un sous-réseau de passerelle *GatewaySubnet*.</span><span class="sxs-lookup"><span data-stu-id="94204-111">Gateway Subnet name: "GatewaySubnet" You must always name a gateway subnet *GatewaySubnet*.</span></span>
* <span data-ttu-id="94204-112">Espace d'adressage du sous-réseau de passerelle : « 192.168.200.0/26 »</span><span class="sxs-lookup"><span data-stu-id="94204-112">Gateway Subnet address space = "192.168.200.0/26"</span></span>
* <span data-ttu-id="94204-113">Région : « Est des États-Unis »</span><span class="sxs-lookup"><span data-stu-id="94204-113">Region = "East US"</span></span>
* <span data-ttu-id="94204-114">Nom de la passerelle : « GW »</span><span class="sxs-lookup"><span data-stu-id="94204-114">Gateway Name = "GW"</span></span>
* <span data-ttu-id="94204-115">Nom d’adresse IP de la passerelle : « GWIP »</span><span class="sxs-lookup"><span data-stu-id="94204-115">Gateway IP Name = "GWIP"</span></span>
* <span data-ttu-id="94204-116">Nom de configuration IP de la passerelle : « gwipconf »</span><span class="sxs-lookup"><span data-stu-id="94204-116">Gateway IP configuration Name = "gwipconf"</span></span>
* <span data-ttu-id="94204-117">Type : « ExpressRoute » Ce type est requis pour une configuration ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="94204-117">Type = "ExpressRoute" This type is required for an ExpressRoute configuration.</span></span>
* <span data-ttu-id="94204-118">Nom d’adresse IP publique de passerelle = « gwpip »</span><span class="sxs-lookup"><span data-stu-id="94204-118">Gateway Public IP Name = "gwpip"</span></span>

## <a name="add-a-gateway"></a><span data-ttu-id="94204-119">Ajout d’une passerelle</span><span class="sxs-lookup"><span data-stu-id="94204-119">Add a gateway</span></span>
1. <span data-ttu-id="94204-120">Se connecter tooyour abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="94204-120">Connect tooyour Azure Subscription.</span></span>

  ```powershell 
  Login-AzureRmAccount
  Get-AzureRmSubscription 
  Select-AzureRmSubscription -SubscriptionName "Name of subscription"
  ```
2. <span data-ttu-id="94204-121">Déclarez vos variables pour cet exercice.</span><span class="sxs-lookup"><span data-stu-id="94204-121">Declare your variables for this exercise.</span></span> <span data-ttu-id="94204-122">Être tooedit vraiment hello exemple tooreflect hello de paramètres que vous souhaitez toouse.</span><span class="sxs-lookup"><span data-stu-id="94204-122">Be sure tooedit hello sample tooreflect hello settings that you want toouse.</span></span>

  ```powershell 
  $RG = "TestRG"
  $Location = "East US"
  $GWName = "GW"
  $GWIPName = "GWIP"
  $GWIPconfName = "gwipconf"
  $VNetName = "TestVNet"
  ```
3. <span data-ttu-id="94204-123">Stocker l’objet de réseau virtuel hello comme une variable.</span><span class="sxs-lookup"><span data-stu-id="94204-123">Store hello virtual network object as a variable.</span></span>

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG
  ```
4. <span data-ttu-id="94204-124">Ajouter un tooyour de sous-réseau de passerelle réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="94204-124">Add a gateway subnet tooyour Virtual Network.</span></span> <span data-ttu-id="94204-125">sous-réseau de passerelle Hello doit être nommé « GatewaySubnet ».</span><span class="sxs-lookup"><span data-stu-id="94204-125">hello gateway subnet must be named "GatewaySubnet".</span></span> <span data-ttu-id="94204-126">Vous devez créer un sous-réseau de passerelle défini sur /27 ou plus (/26, /25, etc.).</span><span class="sxs-lookup"><span data-stu-id="94204-126">You should create a gateway subnet that is /27 or larger (/26, /25, etc.).</span></span>

  ```powershell
  Add-AzureRmVirtualNetworkSubnetConfig -Name GatewaySubnet -VirtualNetwork $vnet -AddressPrefix 192.168.200.0/26
  ```
5. <span data-ttu-id="94204-127">Définir la configuration hello.</span><span class="sxs-lookup"><span data-stu-id="94204-127">Set hello configuration.</span></span>

  ```powershell
  Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
6. <span data-ttu-id="94204-128">Stocker le sous-réseau de passerelle hello comme une variable.</span><span class="sxs-lookup"><span data-stu-id="94204-128">Store hello gateway subnet as a variable.</span></span>

  ```powershell
  $subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -VirtualNetwork $vnet
  ```
7. <span data-ttu-id="94204-129">Demandez une adresse IP publique</span><span class="sxs-lookup"><span data-stu-id="94204-129">Request a public IP address.</span></span> <span data-ttu-id="94204-130">une adresse IP Hello est requise avant de créer la passerelle de hello.</span><span class="sxs-lookup"><span data-stu-id="94204-130">hello IP address is requested before creating hello gateway.</span></span> <span data-ttu-id="94204-131">Vous ne pouvez pas spécifier hello adresse IP que toouse ; elle est allouée dynamiquement.</span><span class="sxs-lookup"><span data-stu-id="94204-131">You cannot specify hello IP address that you want toouse; it’s dynamically allocated.</span></span> <span data-ttu-id="94204-132">Vous utiliserez cette adresse IP dans la section de configuration suivante hello.</span><span class="sxs-lookup"><span data-stu-id="94204-132">You'll use this IP address in hello next configuration section.</span></span> <span data-ttu-id="94204-133">Hello AllocationMethod doit être dynamiques.</span><span class="sxs-lookup"><span data-stu-id="94204-133">hello AllocationMethod must be Dynamic.</span></span>

  ```powershell
  $pip = New-AzureRmPublicIpAddress -Name $GWIPName  -ResourceGroupName $RG -Location $Location -AllocationMethod Dynamic
  ```
8. <span data-ttu-id="94204-134">Créer la configuration hello pour votre passerelle.</span><span class="sxs-lookup"><span data-stu-id="94204-134">Create hello configuration for your gateway.</span></span> <span data-ttu-id="94204-135">configuration de la passerelle Hello définit le sous-réseau de hello et toouse adresse IP publique de hello.</span><span class="sxs-lookup"><span data-stu-id="94204-135">hello gateway configuration defines hello subnet and hello public IP address toouse.</span></span> <span data-ttu-id="94204-136">Dans cette étape, vous spécifiez configuration hello qui sera utilisée lors de la création de la passerelle de hello.</span><span class="sxs-lookup"><span data-stu-id="94204-136">In this step, you are specifying hello configuration that will be used when you create hello gateway.</span></span> <span data-ttu-id="94204-137">Cette étape ne crée pas réellement l’objet de passerelle hello.</span><span class="sxs-lookup"><span data-stu-id="94204-137">This step does not actually create hello gateway object.</span></span> <span data-ttu-id="94204-138">Utilisez exemple hello ci-dessous toocreate votre configuration de la passerelle.</span><span class="sxs-lookup"><span data-stu-id="94204-138">Use hello sample below toocreate your gateway configuration.</span></span>

  ```powershell
  $ipconf = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName -Subnet $subnet -PublicIpAddress $pip
  ```
9. <span data-ttu-id="94204-139">Créer la passerelle de hello.</span><span class="sxs-lookup"><span data-stu-id="94204-139">Create hello gateway.</span></span> <span data-ttu-id="94204-140">Dans cette étape, hello **- le type de passerelle** est particulièrement important.</span><span class="sxs-lookup"><span data-stu-id="94204-140">In this step, hello **-GatewayType** is especially important.</span></span> <span data-ttu-id="94204-141">Vous devez utiliser la valeur de hello **ExpressRoute**.</span><span class="sxs-lookup"><span data-stu-id="94204-141">You must use hello value **ExpressRoute**.</span></span> <span data-ttu-id="94204-142">Après l’exécution de ces applets de commande, passerelle de hello peut prendre entre 45 minutes ou plus toocreate.</span><span class="sxs-lookup"><span data-stu-id="94204-142">After running these cmdlets, hello gateway can take 45 minutes or more toocreate.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG -Location $Location -IpConfigurations $ipconf -GatewayType Expressroute -GatewaySku Standard
  ```

## <a name="verify-hello-gateway-was-created"></a><span data-ttu-id="94204-143">Vérifiez les passerelle hello a été créé.</span><span class="sxs-lookup"><span data-stu-id="94204-143">Verify hello gateway was created</span></span>
<span data-ttu-id="94204-144">Utilisez hello suivant les commandes tooverify qui hello passerelle a été créé :</span><span class="sxs-lookup"><span data-stu-id="94204-144">Use hello following commands tooverify that hello gateway has been created:</span></span>

```powershell
Get-AzureRmVirtualNetworkGateway -ResourceGroupName $RG
```

## <a name="resize-a-gateway"></a><span data-ttu-id="94204-145">Redimensionner une passerelle</span><span class="sxs-lookup"><span data-stu-id="94204-145">Resize a gateway</span></span>
<span data-ttu-id="94204-146">Il existe un certain nombre de [Références (SKU) de passerelle](../articles/expressroute/expressroute-about-virtual-network-gateways.md).</span><span class="sxs-lookup"><span data-stu-id="94204-146">There are a number of [Gateway SKUs](../articles/expressroute/expressroute-about-virtual-network-gateways.md).</span></span> <span data-ttu-id="94204-147">Vous pouvez utiliser hello suivant commande toochange hello SKU de passerelle à tout moment.</span><span class="sxs-lookup"><span data-stu-id="94204-147">You can use hello following command toochange hello Gateway SKU at any time.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="94204-148">Cette commande ne fonctionne pas pour la passerelle UltraPerformance.</span><span class="sxs-lookup"><span data-stu-id="94204-148">This command doesn't work for UltraPerformance gateway.</span></span> <span data-ttu-id="94204-149">toochange votre passerelle tooan UltraPerformance passerelle, supprimez d’abord hello existant passerelle ExpressRoute et puis créer une passerelle UltraPerformance.</span><span class="sxs-lookup"><span data-stu-id="94204-149">toochange your gateway tooan UltraPerformance gateway, first remove hello existing ExpressRoute gateway, and then create a new UltraPerformance gateway.</span></span> <span data-ttu-id="94204-150">toodowngrade votre passerelle à partir d’une passerelle UltraPerformance, supprimez d’abord hello UltraPerformance passerelle, puis créer une passerelle.</span><span class="sxs-lookup"><span data-stu-id="94204-150">toodowngrade your gateway from an UltraPerformance gateway, first remove hello UltraPerformance gateway, and then create a new gateway.</span></span>
> 
> 

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG
Resize-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -GatewaySku HighPerformance
```

## <a name="remove-a-gateway"></a><span data-ttu-id="94204-151">Supprimer une passerelle</span><span class="sxs-lookup"><span data-stu-id="94204-151">Remove a gateway</span></span>
<span data-ttu-id="94204-152">Hello suivant commande tooremove une passerelle, utilisez :</span><span class="sxs-lookup"><span data-stu-id="94204-152">Use hello following command tooremove a gateway:</span></span>

```powershell
Remove-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG
```