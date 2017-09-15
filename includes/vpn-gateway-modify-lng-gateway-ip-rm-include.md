### <span data-ttu-id="f525c-101"><a name="gwipnoconnection"></a> Pour modifier la passerelle de réseau local GatewayIpAddress - sans connexion de passerelle</span><span class="sxs-lookup"><span data-stu-id="f525c-101"><a name="gwipnoconnection"></a> To modify the local network gateway 'GatewayIpAddress' - no gateway connection</span></span>

<span data-ttu-id="f525c-102">Si le périphérique VPN auquel vous souhaitez vous connecter a changé son adresse IP publique, vous devez modifier la passerelle de réseau local pour refléter cette modification.</span><span class="sxs-lookup"><span data-stu-id="f525c-102">If the VPN device that you want to connect to has changed its public IP address, you need to modify the local network gateway to reflect that change.</span></span> <span data-ttu-id="f525c-103">Utilisez l’exemple fourni pour modifier une passerelle de réseau local sans connexion de passerelle.</span><span class="sxs-lookup"><span data-stu-id="f525c-103">Use the example to modify a local network gateway that does not have a gateway connection.</span></span>

<span data-ttu-id="f525c-104">Lorsque vous modifiez cette valeur, vous pouvez également modifier les préfixes d’adresse en même temps.</span><span class="sxs-lookup"><span data-stu-id="f525c-104">When modifying this value, you can also modify the address prefixes at the same time.</span></span> <span data-ttu-id="f525c-105">Veillez à utiliser le nom existant de votre passerelle de réseau local pour remplacer les paramètres actuels.</span><span class="sxs-lookup"><span data-stu-id="f525c-105">Be sure to use the existing name of your local network gateway in order to overwrite the current settings.</span></span> <span data-ttu-id="f525c-106">Si vous utilisez un nom différent, vous créerez une nouvelle passerelle de réseau local au lieu de remplacer la passerelle existante.</span><span class="sxs-lookup"><span data-stu-id="f525c-106">If you use a different name, you create a new local network gateway, instead of overwriting the existing one.</span></span>

```powershell
New-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName `
-Location "West US" -AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24') `
-GatewayIpAddress "5.4.3.2" -ResourceGroupName MyRGName
```

### <span data-ttu-id="f525c-107"><a name="gwipwithconnection"></a>Pour modifier la passerelle de réseau local GatewayIpAddress - avec une connexion de passerelle existante</span><span class="sxs-lookup"><span data-stu-id="f525c-107"><a name="gwipwithconnection"></a>To modify the local network gateway 'GatewayIpAddress' - existing gateway connection</span></span>

<span data-ttu-id="f525c-108">Si le périphérique VPN auquel vous souhaitez vous connecter a changé son adresse IP publique, vous devez modifier la passerelle de réseau local pour refléter cette modification.</span><span class="sxs-lookup"><span data-stu-id="f525c-108">If the VPN device that you want to connect to has changed its public IP address, you need to modify the local network gateway to reflect that change.</span></span> <span data-ttu-id="f525c-109">S’il existe déjà une connexion de passerelle, vous devez tout d’abord supprimer la connexion.</span><span class="sxs-lookup"><span data-stu-id="f525c-109">If a gateway connection already exists, you first need to remove the connection.</span></span> <span data-ttu-id="f525c-110">Une fois la connexion supprimée, vous pouvez modifier l’adresse IP de la passerelle et recréer une connexion.</span><span class="sxs-lookup"><span data-stu-id="f525c-110">After the connection is removed, you can modify the gateway IP address and recreate a new connection.</span></span> <span data-ttu-id="f525c-111">Vous pouvez également modifier les préfixes d’adresse en même temps.</span><span class="sxs-lookup"><span data-stu-id="f525c-111">You can also modify the address prefixes at the same time.</span></span> <span data-ttu-id="f525c-112">Cela entraînera une interruption de votre connexion VPN.</span><span class="sxs-lookup"><span data-stu-id="f525c-112">This results in some downtime for your VPN connection.</span></span> <span data-ttu-id="f525c-113">Lorsque vous modifiez l’adresse IP de la passerelle, vous n’avez pas besoin de supprimer la passerelle VPN.</span><span class="sxs-lookup"><span data-stu-id="f525c-113">When modifying the gateway IP address, you don't need to delete the VPN gateway.</span></span> <span data-ttu-id="f525c-114">Vous devez uniquement supprimer la connexion.</span><span class="sxs-lookup"><span data-stu-id="f525c-114">You only need to remove the connection.</span></span>
 

1. <span data-ttu-id="f525c-115">Supprimez la connexion.</span><span class="sxs-lookup"><span data-stu-id="f525c-115">Remove the connection.</span></span> <span data-ttu-id="f525c-116">Vous trouverez le nom de votre connexion en utilisant l’applet de commande « Get-AzureRmVirtualNetworkGatewayConnection ».</span><span class="sxs-lookup"><span data-stu-id="f525c-116">You can find the name of your connection by using the 'Get-AzureRmVirtualNetworkGatewayConnection' cmdlet.</span></span>

  ```powershell
  Remove-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName `
  -ResourceGroupName MyRGName
  ```
2. <span data-ttu-id="f525c-117">Modifiez la valeur « GatewayIpAddress ».</span><span class="sxs-lookup"><span data-stu-id="f525c-117">Modify the 'GatewayIpAddress' value.</span></span> <span data-ttu-id="f525c-118">Vous pouvez également modifier les préfixes d’adresse en même temps.</span><span class="sxs-lookup"><span data-stu-id="f525c-118">You can also modify the address prefixes at the same time.</span></span> <span data-ttu-id="f525c-119">Veillez à utiliser le nom existant de votre passerelle de réseau local pour remplacer les paramètres actuels.</span><span class="sxs-lookup"><span data-stu-id="f525c-119">Be sure to use the existing name of your local network gateway to overwrite the current settings.</span></span> <span data-ttu-id="f525c-120">Si vous ne le faites pas, vous créerez une nouvelle passerelle de réseau local au lieu de remplacer la passerelle existante.</span><span class="sxs-lookup"><span data-stu-id="f525c-120">If you don't, you create a new local network gateway, instead of overwriting the existing one.</span></span>

  ```powershell
  New-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName `
  -Location "West US" -AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24') `
  -GatewayIpAddress "104.40.81.124" -ResourceGroupName MyRGName
  ```
3. <span data-ttu-id="f525c-121">Créez la connexion.</span><span class="sxs-lookup"><span data-stu-id="f525c-121">Create the connection.</span></span> <span data-ttu-id="f525c-122">Dans cet exemple, nous allons configurer un type de connexion IPsec.</span><span class="sxs-lookup"><span data-stu-id="f525c-122">In this example, we configure an IPsec connection type.</span></span> <span data-ttu-id="f525c-123">Lorsque vous recréez votre connexion, utilisez le type de connexion spécifié pour votre configuration.</span><span class="sxs-lookup"><span data-stu-id="f525c-123">When you recreate your connection, use the connection type that is specified for your configuration.</span></span> <span data-ttu-id="f525c-124">Pour les autres types de connexion, consultez la page sur [les applets de commande PowerShell](https://msdn.microsoft.com/library/mt603611.aspx) .</span><span class="sxs-lookup"><span data-stu-id="f525c-124">For additional connection types, see the [PowerShell cmdlet](https://msdn.microsoft.com/library/mt603611.aspx) page.</span></span>  <span data-ttu-id="f525c-125">Pour obtenir le nom de VirtualNetworkGateway, vous pouvez exécuter l’applet de commande « Get-AzureRmVirtualNetworkGateway ».</span><span class="sxs-lookup"><span data-stu-id="f525c-125">To obtain the VirtualNetworkGateway name, you can run the 'Get-AzureRmVirtualNetworkGateway' cmdlet.</span></span>
   
    <span data-ttu-id="f525c-126">Définissez les variables.</span><span class="sxs-lookup"><span data-stu-id="f525c-126">Set the variables.</span></span>

  ```powershell
  $local = Get-AzureRMLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName `
  $vnetgw = Get-AzureRmVirtualNetworkGateway -Name RMGateway -ResourceGroupName MyRGName
  ```
   
    <span data-ttu-id="f525c-127">Créez la connexion.</span><span class="sxs-lookup"><span data-stu-id="f525c-127">Create the connection.</span></span>

  ```powershell 
  New-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName -ResourceGroupName MyRGName `
  -Location "West US" `
  -VirtualNetworkGateway1 $vnetgw `
  -LocalNetworkGateway2 $local `
  -ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
  ```