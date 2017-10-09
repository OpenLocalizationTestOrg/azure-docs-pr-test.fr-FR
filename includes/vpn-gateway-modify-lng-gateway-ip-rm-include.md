### <span data-ttu-id="766bd-101"><a name="gwipnoconnection"></a>passerelle de réseau local toomodify hello 'GatewayIpAddress' - aucune connexion de passerelle</span><span class="sxs-lookup"><span data-stu-id="766bd-101"><a name="gwipnoconnection"></a> toomodify hello local network gateway 'GatewayIpAddress' - no gateway connection</span></span>

<span data-ttu-id="766bd-102">Si le périphérique VPN de hello que vous souhaitez tooconnect toohas modifié son adresse IP publique, vous devez tooreflect de passerelle du réseau local d’hello toomodify qui changent.</span><span class="sxs-lookup"><span data-stu-id="766bd-102">If hello VPN device that you want tooconnect toohas changed its public IP address, you need toomodify hello local network gateway tooreflect that change.</span></span> <span data-ttu-id="766bd-103">Utilisez hello exemple toomodify une passerelle de réseau local qui n’a pas d’une connexion de passerelle.</span><span class="sxs-lookup"><span data-stu-id="766bd-103">Use hello example toomodify a local network gateway that does not have a gateway connection.</span></span>

<span data-ttu-id="766bd-104">Lorsque vous modifiez cette valeur, vous pouvez également modifier les préfixes d’adresse hello en hello même temps.</span><span class="sxs-lookup"><span data-stu-id="766bd-104">When modifying this value, you can also modify hello address prefixes at hello same time.</span></span> <span data-ttu-id="766bd-105">Être vraiment toouse hello nom existant de votre passerelle de réseau local dans les paramètres actuels de commande toooverwrite hello.</span><span class="sxs-lookup"><span data-stu-id="766bd-105">Be sure toouse hello existing name of your local network gateway in order toooverwrite hello current settings.</span></span> <span data-ttu-id="766bd-106">Si vous utilisez un autre nom, vous créez une nouvelle passerelle de réseau local, au lieu de remplacer hello existant.</span><span class="sxs-lookup"><span data-stu-id="766bd-106">If you use a different name, you create a new local network gateway, instead of overwriting hello existing one.</span></span>

```powershell
New-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName `
-Location "West US" -AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24') `
-GatewayIpAddress "5.4.3.2" -ResourceGroupName MyRGName
```

### <span data-ttu-id="766bd-107"><a name="gwipwithconnection"></a>passerelle de réseau local toomodify hello 'GatewayIpAddress' - connexion à la passerelle existante</span><span class="sxs-lookup"><span data-stu-id="766bd-107"><a name="gwipwithconnection"></a>toomodify hello local network gateway 'GatewayIpAddress' - existing gateway connection</span></span>

<span data-ttu-id="766bd-108">Si le périphérique VPN de hello que vous souhaitez tooconnect toohas modifié son adresse IP publique, vous devez tooreflect de passerelle du réseau local d’hello toomodify qui changent.</span><span class="sxs-lookup"><span data-stu-id="766bd-108">If hello VPN device that you want tooconnect toohas changed its public IP address, you need toomodify hello local network gateway tooreflect that change.</span></span> <span data-ttu-id="766bd-109">Si une passerelle connexion existe déjà, vous devez d’abord connexion de hello tooremove.</span><span class="sxs-lookup"><span data-stu-id="766bd-109">If a gateway connection already exists, you first need tooremove hello connection.</span></span> <span data-ttu-id="766bd-110">Une fois la connexion de hello est supprimée, vous pouvez modifier l’adresse IP de passerelle hello et recréez une nouvelle connexion.</span><span class="sxs-lookup"><span data-stu-id="766bd-110">After hello connection is removed, you can modify hello gateway IP address and recreate a new connection.</span></span> <span data-ttu-id="766bd-111">Vous pouvez également modifier les préfixes d’adresse hello en hello même temps.</span><span class="sxs-lookup"><span data-stu-id="766bd-111">You can also modify hello address prefixes at hello same time.</span></span> <span data-ttu-id="766bd-112">Cela entraînera une interruption de votre connexion VPN.</span><span class="sxs-lookup"><span data-stu-id="766bd-112">This results in some downtime for your VPN connection.</span></span> <span data-ttu-id="766bd-113">Lorsque vous modifiez l’adresse IP de passerelle hello, vous n’avez pas besoin passerelle VPN de hello toodelete.</span><span class="sxs-lookup"><span data-stu-id="766bd-113">When modifying hello gateway IP address, you don't need toodelete hello VPN gateway.</span></span> <span data-ttu-id="766bd-114">Vous devez uniquement la connexion de hello tooremove.</span><span class="sxs-lookup"><span data-stu-id="766bd-114">You only need tooremove hello connection.</span></span>
 

1. <span data-ttu-id="766bd-115">Supprimer la connexion de hello.</span><span class="sxs-lookup"><span data-stu-id="766bd-115">Remove hello connection.</span></span> <span data-ttu-id="766bd-116">Vous trouverez le nom hello de la connexion à l’aide d’applet de commande hello 'Get-AzureRmVirtualNetworkGatewayConnection'.</span><span class="sxs-lookup"><span data-stu-id="766bd-116">You can find hello name of your connection by using hello 'Get-AzureRmVirtualNetworkGatewayConnection' cmdlet.</span></span>

  ```powershell
  Remove-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName `
  -ResourceGroupName MyRGName
  ```
2. <span data-ttu-id="766bd-117">Modifiez la valeur de 'GatewayIpAddress' hello.</span><span class="sxs-lookup"><span data-stu-id="766bd-117">Modify hello 'GatewayIpAddress' value.</span></span> <span data-ttu-id="766bd-118">Vous pouvez également modifier les préfixes d’adresse hello en hello même temps.</span><span class="sxs-lookup"><span data-stu-id="766bd-118">You can also modify hello address prefixes at hello same time.</span></span> <span data-ttu-id="766bd-119">Être vraiment toouse hello nom existant de vos paramètres actuels de réseau local passerelle toooverwrite hello.</span><span class="sxs-lookup"><span data-stu-id="766bd-119">Be sure toouse hello existing name of your local network gateway toooverwrite hello current settings.</span></span> <span data-ttu-id="766bd-120">Si vous ne le faites pas, vous créez une nouvelle passerelle de réseau local, au lieu de remplacer hello existant.</span><span class="sxs-lookup"><span data-stu-id="766bd-120">If you don't, you create a new local network gateway, instead of overwriting hello existing one.</span></span>

  ```powershell
  New-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName `
  -Location "West US" -AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24') `
  -GatewayIpAddress "104.40.81.124" -ResourceGroupName MyRGName
  ```
3. <span data-ttu-id="766bd-121">Créer la connexion de hello.</span><span class="sxs-lookup"><span data-stu-id="766bd-121">Create hello connection.</span></span> <span data-ttu-id="766bd-122">Dans cet exemple, nous allons configurer un type de connexion IPsec.</span><span class="sxs-lookup"><span data-stu-id="766bd-122">In this example, we configure an IPsec connection type.</span></span> <span data-ttu-id="766bd-123">Lorsque vous recréez votre connexion, utilisez le type de connexion hello est spécifié pour votre configuration.</span><span class="sxs-lookup"><span data-stu-id="766bd-123">When you recreate your connection, use hello connection type that is specified for your configuration.</span></span> <span data-ttu-id="766bd-124">Pour les types de connexion supplémentaires, consultez hello [applet de commande PowerShell](https://msdn.microsoft.com/library/mt603611.aspx) page.</span><span class="sxs-lookup"><span data-stu-id="766bd-124">For additional connection types, see hello [PowerShell cmdlet](https://msdn.microsoft.com/library/mt603611.aspx) page.</span></span>  <span data-ttu-id="766bd-125">nom de VirtualNetworkGateway tooobtain hello, vous pouvez exécuter l’applet de commande 'Get-AzureRmVirtualNetworkGateway' hello.</span><span class="sxs-lookup"><span data-stu-id="766bd-125">tooobtain hello VirtualNetworkGateway name, you can run hello 'Get-AzureRmVirtualNetworkGateway' cmdlet.</span></span>
   
    <span data-ttu-id="766bd-126">Définir les variables de hello.</span><span class="sxs-lookup"><span data-stu-id="766bd-126">Set hello variables.</span></span>

  ```powershell
  $local = Get-AzureRMLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName `
  $vnetgw = Get-AzureRmVirtualNetworkGateway -Name RMGateway -ResourceGroupName MyRGName
  ```
   
    <span data-ttu-id="766bd-127">Créer la connexion de hello.</span><span class="sxs-lookup"><span data-stu-id="766bd-127">Create hello connection.</span></span>

  ```powershell 
  New-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName -ResourceGroupName MyRGName `
  -Location "West US" `
  -VirtualNetworkGateway1 $vnetgw `
  -LocalNetworkGateway2 $local `
  -ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
  ```