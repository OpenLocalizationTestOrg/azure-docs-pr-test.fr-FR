### <span data-ttu-id="f543e-101"><a name="noconnection"></a>préfixes d’adresses toomodify réseau local passerelle IP - aucune connexion de passerelle</span><span class="sxs-lookup"><span data-stu-id="f543e-101"><a name="noconnection"></a>toomodify local network gateway IP address prefixes - no gateway connection</span></span>

<span data-ttu-id="f543e-102">préfixes d’adresse supplémentaires tooadd :</span><span class="sxs-lookup"><span data-stu-id="f543e-102">tooadd additional address prefixes:</span></span>

```powershell
$local = Get-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName `
Set-AzureRmLocalNetworkGateway -LocalNetworkGateway $local `
-AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24')
```

<span data-ttu-id="f543e-103">préfixes d’adresse tooremove :</span><span class="sxs-lookup"><span data-stu-id="f543e-103">tooremove address prefixes:</span></span><br>
<span data-ttu-id="f543e-104">Exclut les préfixes hello que vous n’avez plus besoin.</span><span class="sxs-lookup"><span data-stu-id="f543e-104">Leave out hello prefixes that you no longer need.</span></span> <span data-ttu-id="f543e-105">Dans cet exemple, nous devons de ne plus préfixe 20.0.0.0/24 (à partir de l’exemple précédent hello), afin de nous mettre à jour de passerelle de réseau local hello, à l’exclusion de ce préfixe.</span><span class="sxs-lookup"><span data-stu-id="f543e-105">In this example, we no longer need prefix 20.0.0.0/24 (from hello previous example), so we update hello local network gateway, excluding that prefix.</span></span>

```powershell
$local = Get-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName `
Set-AzureRmLocalNetworkGateway -LocalNetworkGateway $local `
-AddressPrefix @('10.0.0.0/24','30.0.0.0/24')
```

### <span data-ttu-id="f543e-106"><a name="withconnection"></a>toomodify réseau local passerelle préfixes d’adresses IP - connexion de passerelle existante</span><span class="sxs-lookup"><span data-stu-id="f543e-106"><a name="withconnection"></a>toomodify local network gateway IP address prefixes - existing gateway connection</span></span>

<span data-ttu-id="f543e-107">Si vous disposez d’une connexion de passerelle et souhaitez tooadd ou supprimez des préfixes d’adresses IP hello contenues dans votre passerelle de réseau local, vous devez hello toodo comme suit, dans l’ordre.</span><span class="sxs-lookup"><span data-stu-id="f543e-107">If you have a gateway connection and want tooadd or remove hello IP address prefixes contained in your local network gateway, you need toodo hello following steps, in order.</span></span> <span data-ttu-id="f543e-108">Cela entraînera une interruption de votre connexion VPN.</span><span class="sxs-lookup"><span data-stu-id="f543e-108">This results in some downtime for your VPN connection.</span></span> <span data-ttu-id="f543e-109">Lorsque vous modifiez des préfixes d’adresses IP, vous n’avez pas besoin passerelle VPN de hello toodelete.</span><span class="sxs-lookup"><span data-stu-id="f543e-109">When modifying IP address prefixes, you don't need toodelete hello VPN gateway.</span></span> <span data-ttu-id="f543e-110">Vous devez uniquement la connexion de hello tooremove.</span><span class="sxs-lookup"><span data-stu-id="f543e-110">You only need tooremove hello connection.</span></span>


1. <span data-ttu-id="f543e-111">Supprimer la connexion de hello.</span><span class="sxs-lookup"><span data-stu-id="f543e-111">Remove hello connection.</span></span>

  ```powershell
  Remove-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName -ResourceGroupName MyRGName
  ```
2. <span data-ttu-id="f543e-112">Modifier les préfixes d’adresse hello pour votre passerelle de réseau local.</span><span class="sxs-lookup"><span data-stu-id="f543e-112">Modify hello address prefixes for your local network gateway.</span></span>
   
  <span data-ttu-id="f543e-113">Définissez la variable hello pour hello passerelle de réseau local.</span><span class="sxs-lookup"><span data-stu-id="f543e-113">Set hello variable for hello LocalNetworkGateway.</span></span>

  ```powershell
  $local = Get-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName
  ```
   
  <span data-ttu-id="f543e-114">Modifier les préfixes hello.</span><span class="sxs-lookup"><span data-stu-id="f543e-114">Modify hello prefixes.</span></span>
   
  ```powershell
  Set-AzureRmLocalNetworkGateway -LocalNetworkGateway $local `
  -AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24')
  ```
3. <span data-ttu-id="f543e-115">Créer la connexion de hello.</span><span class="sxs-lookup"><span data-stu-id="f543e-115">Create hello connection.</span></span> <span data-ttu-id="f543e-116">Dans cet exemple, nous allons configurer un type de connexion IPsec.</span><span class="sxs-lookup"><span data-stu-id="f543e-116">In this example, we configure an IPsec connection type.</span></span> <span data-ttu-id="f543e-117">Lorsque vous recréez votre connexion, utilisez le type de connexion hello est spécifié pour votre configuration.</span><span class="sxs-lookup"><span data-stu-id="f543e-117">When you recreate your connection, use hello connection type that is specified for your configuration.</span></span> <span data-ttu-id="f543e-118">Pour les types de connexion supplémentaires, consultez hello [applet de commande PowerShell](https://msdn.microsoft.com/library/mt603611.aspx) page.</span><span class="sxs-lookup"><span data-stu-id="f543e-118">For additional connection types, see hello [PowerShell cmdlet](https://msdn.microsoft.com/library/mt603611.aspx) page.</span></span>
   
  <span data-ttu-id="f543e-119">Définissez la variable hello pour hello VirtualNetworkGateway.</span><span class="sxs-lookup"><span data-stu-id="f543e-119">Set hello variable for hello VirtualNetworkGateway.</span></span>

  ```powershell
  $gateway1 = Get-AzureRmVirtualNetworkGateway -Name RMGateway  -ResourceGroupName MyRGName
  ```
   
  <span data-ttu-id="f543e-120">Créer la connexion de hello.</span><span class="sxs-lookup"><span data-stu-id="f543e-120">Create hello connection.</span></span> <span data-ttu-id="f543e-121">Cet exemple utilise la variable de hello $local que vous définissez à l’étape 2.</span><span class="sxs-lookup"><span data-stu-id="f543e-121">This example uses hello variable $local that you set in step 2.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName `
  -ResourceGroupName MyRGName -Location 'West US' `
  -VirtualNetworkGateway1 $gateway1 -LocalNetworkGateway2 $local `
  -ConnectionType IPsec `
  -RoutingWeight 10 -SharedKey 'abc123'
  ```