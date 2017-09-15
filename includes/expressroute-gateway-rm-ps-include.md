<span data-ttu-id="354ba-101">Les étapes de cette tâche utilisent un réseau virtuel basé sur les valeurs figurant dans la liste de référence de configuration suivante.</span><span class="sxs-lookup"><span data-stu-id="354ba-101">The steps for this task use a VNet based on the values in the following configuration reference list.</span></span> <span data-ttu-id="354ba-102">Les noms et paramètres supplémentaires sont également présentés dans cette liste.</span><span class="sxs-lookup"><span data-stu-id="354ba-102">Additional settings and names are also outlined in this list.</span></span> <span data-ttu-id="354ba-103">Nous n’utilisons pas cette liste directement dans la procédure, mais nous ajoutons des variables en fonction des valeurs dans cette liste.</span><span class="sxs-lookup"><span data-stu-id="354ba-103">We don't use this list directly in any of the steps, although we do add variables based on the values in this list.</span></span> <span data-ttu-id="354ba-104">Vous pouvez copier la liste et l’utiliser en tant que référence, en remplaçant les valeurs par les vôtres.</span><span class="sxs-lookup"><span data-stu-id="354ba-104">You can copy the list to use as a reference, replacing the values with your own.</span></span>

<span data-ttu-id="354ba-105">**Liste de référence de configuration**</span><span class="sxs-lookup"><span data-stu-id="354ba-105">**Configuration reference list**</span></span>

* <span data-ttu-id="354ba-106">Nom du réseau virtuel : « TestVNet »</span><span class="sxs-lookup"><span data-stu-id="354ba-106">Virtual Network Name = "TestVNet"</span></span>
* <span data-ttu-id="354ba-107">Espace d’adressage du réseau virtuel : 192.168.0.0/16</span><span class="sxs-lookup"><span data-stu-id="354ba-107">Virtual Network address space = 192.168.0.0/16</span></span>
* <span data-ttu-id="354ba-108">Groupe de ressources : « TestRG »</span><span class="sxs-lookup"><span data-stu-id="354ba-108">Resource Group = "TestRG"</span></span>
* <span data-ttu-id="354ba-109">Nom du sous-réseau 1 : « FrontEnd »</span><span class="sxs-lookup"><span data-stu-id="354ba-109">Subnet1 Name = "FrontEnd"</span></span> 
* <span data-ttu-id="354ba-110">Espace d’adressage du sous-réseau 1 = "192.168.1.0/24"</span><span class="sxs-lookup"><span data-stu-id="354ba-110">Subnet1 address space = "192.168.1.0/24"</span></span>
* <span data-ttu-id="354ba-111">Nom de sous-réseau de passerelle : « GatewaySubnet » Vous devez toujours nommer un sous-réseau de passerelle *GatewaySubnet*.</span><span class="sxs-lookup"><span data-stu-id="354ba-111">Gateway Subnet name: "GatewaySubnet" You must always name a gateway subnet *GatewaySubnet*.</span></span>
* <span data-ttu-id="354ba-112">Espace d'adressage du sous-réseau de passerelle : « 192.168.200.0/26 »</span><span class="sxs-lookup"><span data-stu-id="354ba-112">Gateway Subnet address space = "192.168.200.0/26"</span></span>
* <span data-ttu-id="354ba-113">Région : « Est des États-Unis »</span><span class="sxs-lookup"><span data-stu-id="354ba-113">Region = "East US"</span></span>
* <span data-ttu-id="354ba-114">Nom de la passerelle : « GW »</span><span class="sxs-lookup"><span data-stu-id="354ba-114">Gateway Name = "GW"</span></span>
* <span data-ttu-id="354ba-115">Nom d’adresse IP de la passerelle : « GWIP »</span><span class="sxs-lookup"><span data-stu-id="354ba-115">Gateway IP Name = "GWIP"</span></span>
* <span data-ttu-id="354ba-116">Nom de configuration IP de la passerelle : « gwipconf »</span><span class="sxs-lookup"><span data-stu-id="354ba-116">Gateway IP configuration Name = "gwipconf"</span></span>
* <span data-ttu-id="354ba-117">Type : « ExpressRoute » Ce type est requis pour une configuration ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="354ba-117">Type = "ExpressRoute" This type is required for an ExpressRoute configuration.</span></span>
* <span data-ttu-id="354ba-118">Nom d’adresse IP publique de passerelle = « gwpip »</span><span class="sxs-lookup"><span data-stu-id="354ba-118">Gateway Public IP Name = "gwpip"</span></span>

## <a name="add-a-gateway"></a><span data-ttu-id="354ba-119">Ajout d’une passerelle</span><span class="sxs-lookup"><span data-stu-id="354ba-119">Add a gateway</span></span>
1. <span data-ttu-id="354ba-120">Connectez-vous à votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="354ba-120">Connect to your Azure Subscription.</span></span>

  ```powershell 
  Login-AzureRmAccount
  Get-AzureRmSubscription 
  Select-AzureRmSubscription -SubscriptionName "Name of subscription"
  ```
2. <span data-ttu-id="354ba-121">Déclarez vos variables pour cet exercice.</span><span class="sxs-lookup"><span data-stu-id="354ba-121">Declare your variables for this exercise.</span></span> <span data-ttu-id="354ba-122">Veillez à modifier l’exemple pour refléter les paramètres que vous souhaitez utiliser.</span><span class="sxs-lookup"><span data-stu-id="354ba-122">Be sure to edit the sample to reflect the settings that you want to use.</span></span>

  ```powershell 
  $RG = "TestRG"
  $Location = "East US"
  $GWName = "GW"
  $GWIPName = "GWIP"
  $GWIPconfName = "gwipconf"
  $VNetName = "TestVNet"
  ```
3. <span data-ttu-id="354ba-123">Stockez l’objet de réseau virtuel en tant que variable.</span><span class="sxs-lookup"><span data-stu-id="354ba-123">Store the virtual network object as a variable.</span></span>

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG
  ```
4. <span data-ttu-id="354ba-124">Ajoutez un sous-réseau de passerelle à votre réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="354ba-124">Add a gateway subnet to your Virtual Network.</span></span> <span data-ttu-id="354ba-125">Le sous-réseau de passerelle doit être nommé « GatewaySubnet ».</span><span class="sxs-lookup"><span data-stu-id="354ba-125">The gateway subnet must be named "GatewaySubnet".</span></span> <span data-ttu-id="354ba-126">Vous devez créer un sous-réseau de passerelle défini sur /27 ou plus (/26, /25, etc.).</span><span class="sxs-lookup"><span data-stu-id="354ba-126">You should create a gateway subnet that is /27 or larger (/26, /25, etc.).</span></span>

  ```powershell
  Add-AzureRmVirtualNetworkSubnetConfig -Name GatewaySubnet -VirtualNetwork $vnet -AddressPrefix 192.168.200.0/26
  ```
5. <span data-ttu-id="354ba-127">Définissez la configuration.</span><span class="sxs-lookup"><span data-stu-id="354ba-127">Set the configuration.</span></span>

  ```powershell
  Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
6. <span data-ttu-id="354ba-128">Stockez le sous-réseau de passerelle en tant que variable.</span><span class="sxs-lookup"><span data-stu-id="354ba-128">Store the gateway subnet as a variable.</span></span>

  ```powershell
  $subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -VirtualNetwork $vnet
  ```
7. <span data-ttu-id="354ba-129">Demandez une adresse IP publique</span><span class="sxs-lookup"><span data-stu-id="354ba-129">Request a public IP address.</span></span> <span data-ttu-id="354ba-130">L’adresse IP est demandée avant de créer la passerelle.</span><span class="sxs-lookup"><span data-stu-id="354ba-130">The IP address is requested before creating the gateway.</span></span> <span data-ttu-id="354ba-131">Vous ne pouvez pas spécifier l’adresse IP que vous souhaitez utiliser, car elle est allouée de façon dynamique.</span><span class="sxs-lookup"><span data-stu-id="354ba-131">You cannot specify the IP address that you want to use; it’s dynamically allocated.</span></span> <span data-ttu-id="354ba-132">Vous utiliserez cette adresse IP dans la section de configuration suivante.</span><span class="sxs-lookup"><span data-stu-id="354ba-132">You'll use this IP address in the next configuration section.</span></span> <span data-ttu-id="354ba-133">La méthode AllocationMethod doit être dynamique.</span><span class="sxs-lookup"><span data-stu-id="354ba-133">The AllocationMethod must be Dynamic.</span></span>

  ```powershell
  $pip = New-AzureRmPublicIpAddress -Name $GWIPName  -ResourceGroupName $RG -Location $Location -AllocationMethod Dynamic
  ```
8. <span data-ttu-id="354ba-134">Créez la configuration de votre passerelle.</span><span class="sxs-lookup"><span data-stu-id="354ba-134">Create the configuration for your gateway.</span></span> <span data-ttu-id="354ba-135">La configuration de la passerelle définit le sous-réseau et l’adresse IP publique à utiliser.</span><span class="sxs-lookup"><span data-stu-id="354ba-135">The gateway configuration defines the subnet and the public IP address to use.</span></span> <span data-ttu-id="354ba-136">Dans cette étape, vous spécifiez la configuration qui sera utilisée lors de la création de la passerelle.</span><span class="sxs-lookup"><span data-stu-id="354ba-136">In this step, you are specifying the configuration that will be used when you create the gateway.</span></span> <span data-ttu-id="354ba-137">Cette étape ne crée pas réellement l’objet de passerelle.</span><span class="sxs-lookup"><span data-stu-id="354ba-137">This step does not actually create the gateway object.</span></span> <span data-ttu-id="354ba-138">Utilisez l’exemple ci-dessous pour créer la configuration de votre passerelle.</span><span class="sxs-lookup"><span data-stu-id="354ba-138">Use the sample below to create your gateway configuration.</span></span>

  ```powershell
  $ipconf = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName -Subnet $subnet -PublicIpAddress $pip
  ```
9. <span data-ttu-id="354ba-139">Créez la passerelle.</span><span class="sxs-lookup"><span data-stu-id="354ba-139">Create the gateway.</span></span> <span data-ttu-id="354ba-140">Dans cette étape, le type **-GatewayType** est particulièrement important.</span><span class="sxs-lookup"><span data-stu-id="354ba-140">In this step, the **-GatewayType** is especially important.</span></span> <span data-ttu-id="354ba-141">Vous devez utiliser la valeur **ExpressRoute**.</span><span class="sxs-lookup"><span data-stu-id="354ba-141">You must use the value **ExpressRoute**.</span></span> <span data-ttu-id="354ba-142">Après l’exécution de ces cmdlets, la création de la passerelle peut prendre 45 minutes ou plus.</span><span class="sxs-lookup"><span data-stu-id="354ba-142">After running these cmdlets, the gateway can take 45 minutes or more to create.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG -Location $Location -IpConfigurations $ipconf -GatewayType Expressroute -GatewaySku Standard
  ```

## <a name="verify-the-gateway-was-created"></a><span data-ttu-id="354ba-143">Vérification de la création de la passerelle</span><span class="sxs-lookup"><span data-stu-id="354ba-143">Verify the gateway was created</span></span>
<span data-ttu-id="354ba-144">Utilisez les commandes suivantes pour vérifier que la passerelle a été créée :</span><span class="sxs-lookup"><span data-stu-id="354ba-144">Use the following commands to verify that the gateway has been created:</span></span>

```powershell
Get-AzureRmVirtualNetworkGateway -ResourceGroupName $RG
```

## <a name="resize-a-gateway"></a><span data-ttu-id="354ba-145">Redimensionner une passerelle</span><span class="sxs-lookup"><span data-stu-id="354ba-145">Resize a gateway</span></span>
<span data-ttu-id="354ba-146">Il existe un certain nombre de [Références (SKU) de passerelle](../articles/expressroute/expressroute-about-virtual-network-gateways.md).</span><span class="sxs-lookup"><span data-stu-id="354ba-146">There are a number of [Gateway SKUs](../articles/expressroute/expressroute-about-virtual-network-gateways.md).</span></span> <span data-ttu-id="354ba-147">Vous pouvez utiliser la commande suivante pour modifier la référence de passerelle à tout moment.</span><span class="sxs-lookup"><span data-stu-id="354ba-147">You can use the following command to change the Gateway SKU at any time.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="354ba-148">Cette commande ne fonctionne pas pour la passerelle UltraPerformance.</span><span class="sxs-lookup"><span data-stu-id="354ba-148">This command doesn't work for UltraPerformance gateway.</span></span> <span data-ttu-id="354ba-149">Pour modifier votre passerelle en passerelle UltraPerformance, commencez par supprimer la passerelle ExpressRoute, puis créez une passerelle UltraPerformance.</span><span class="sxs-lookup"><span data-stu-id="354ba-149">To change your gateway to an UltraPerformance gateway, first remove the existing ExpressRoute gateway, and then create a new UltraPerformance gateway.</span></span> <span data-ttu-id="354ba-150">Pour mettre à niveau votre passerelle à partir d’une passerelle UltraPerformance, commencez par supprimer la passerelle UltraPerformance, puis créez-en une.</span><span class="sxs-lookup"><span data-stu-id="354ba-150">To downgrade your gateway from an UltraPerformance gateway, first remove the UltraPerformance gateway, and then create a new gateway.</span></span>
> 
> 

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG
Resize-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -GatewaySku HighPerformance
```

## <a name="remove-a-gateway"></a><span data-ttu-id="354ba-151">Supprimer une passerelle</span><span class="sxs-lookup"><span data-stu-id="354ba-151">Remove a gateway</span></span>
<span data-ttu-id="354ba-152">Pour supprimer une passerelle, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="354ba-152">Use the following command to remove a gateway:</span></span>

```powershell
Remove-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG
```