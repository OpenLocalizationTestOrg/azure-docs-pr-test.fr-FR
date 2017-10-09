<span data-ttu-id="9605b-101">Vous devez créer un réseau virtuel et un sous-réseau de passerelle tout d’abord, avant d’utiliser hello tâches suivantes.</span><span class="sxs-lookup"><span data-stu-id="9605b-101">You must create a VNet and a gateway subnet first, before working on hello following tasks.</span></span> <span data-ttu-id="9605b-102">Consultez l’article hello [configurer un réseau virtuel à l’aide du portail classique de hello](../articles/expressroute/expressroute-howto-vnet-portal-classic.md) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="9605b-102">See hello article [Configure a Virtual Network using hello classic portal](../articles/expressroute/expressroute-howto-vnet-portal-classic.md) for more information.</span></span>   

## <a name="add-a-gateway"></a><span data-ttu-id="9605b-103">Ajout d’une passerelle</span><span class="sxs-lookup"><span data-stu-id="9605b-103">Add a gateway</span></span>
<span data-ttu-id="9605b-104">Utilisez la commande hello ci-dessous toocreate une passerelle.</span><span class="sxs-lookup"><span data-stu-id="9605b-104">Use hello command below toocreate a gateway.</span></span> <span data-ttu-id="9605b-105">Être toosubstitute que toutes les valeurs de votre propre.</span><span class="sxs-lookup"><span data-stu-id="9605b-105">Be sure toosubstitute any values for your own.</span></span>

    New-AzureVirtualNetworkGateway -VNetName "MyAzureVNET" -GatewayName "ERGateway" -GatewayType Dedicated -GatewaySKU  Standard

## <a name="verify-hello-gateway-was-created"></a><span data-ttu-id="9605b-106">Vérifiez les passerelle hello a été créé.</span><span class="sxs-lookup"><span data-stu-id="9605b-106">Verify hello gateway was created</span></span>
<span data-ttu-id="9605b-107">Utilisez les commandes de hello ci-dessous tooverify qui hello passerelle a été créé.</span><span class="sxs-lookup"><span data-stu-id="9605b-107">Use hello command below tooverify that hello gateway has been created.</span></span> <span data-ttu-id="9605b-108">Cette commande récupère également l’ID de passerelle hello, dont vous avez besoin pour d’autres opérations.</span><span class="sxs-lookup"><span data-stu-id="9605b-108">This command also retrieves hello gateway ID, which you need for other operations.</span></span>

    Get-AzureVirtualNetworkGateway

## <a name="resize-a-gateway"></a><span data-ttu-id="9605b-109">Redimensionner une passerelle</span><span class="sxs-lookup"><span data-stu-id="9605b-109">Resize a gateway</span></span>
<span data-ttu-id="9605b-110">Il existe un certain nombre de [Références (SKU) de passerelle](../articles/expressroute/expressroute-about-virtual-network-gateways.md).</span><span class="sxs-lookup"><span data-stu-id="9605b-110">There are a number of [Gateway SKUs](../articles/expressroute/expressroute-about-virtual-network-gateways.md).</span></span> <span data-ttu-id="9605b-111">Vous pouvez utiliser hello suivant commande toochange hello SKU de passerelle à tout moment.</span><span class="sxs-lookup"><span data-stu-id="9605b-111">You can use hello following command toochange hello Gateway SKU at any time.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9605b-112">Cette commande ne fonctionne pas pour la passerelle UltraPerformance.</span><span class="sxs-lookup"><span data-stu-id="9605b-112">This command doesn't work for UltraPerformance gateway.</span></span> <span data-ttu-id="9605b-113">toochange votre passerelle tooan UltraPerformance passerelle, supprimez d’abord hello existant passerelle ExpressRoute et puis créer une passerelle UltraPerformance.</span><span class="sxs-lookup"><span data-stu-id="9605b-113">toochange your gateway tooan UltraPerformance gateway, first remove hello existing ExpressRoute gateway, and then create a new UltraPerformance gateway.</span></span> <span data-ttu-id="9605b-114">toodowngrade votre passerelle à partir d’une passerelle UltraPerformance, supprimez d’abord hello UltraPerformance passerelle, puis créer une passerelle.</span><span class="sxs-lookup"><span data-stu-id="9605b-114">toodowngrade your gateway from an UltraPerformance gateway, first remove hello UltraPerformance gateway, and then create a new gateway.</span></span> 
> 
> 

    Resize-AzureVirtualNetworkGateway -GatewayId <Gateway ID> -GatewaySKU HighPerformance

## <a name="remove-a-gateway"></a><span data-ttu-id="9605b-115">Supprimer une passerelle</span><span class="sxs-lookup"><span data-stu-id="9605b-115">Remove a gateway</span></span>
<span data-ttu-id="9605b-116">Utilisez la commande hello ci-dessous tooremove une passerelle</span><span class="sxs-lookup"><span data-stu-id="9605b-116">Use hello command below tooremove a gateway</span></span>

    Remove-AzureVirtualNetworkGateway -GatewayId <Gateway ID>