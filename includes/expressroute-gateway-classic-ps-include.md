<span data-ttu-id="b259f-101">Vous devez créer un réseau virtuel et un sous-réseau de passerelle avant d’effectuer les tâches suivantes.</span><span class="sxs-lookup"><span data-stu-id="b259f-101">You must create a VNet and a gateway subnet first, before working on the following tasks.</span></span> <span data-ttu-id="b259f-102">Pour plus d’informations, consultez [Configurer un réseau virtuel à l’aide du portail Azure Classic](../articles/expressroute/expressroute-howto-vnet-portal-classic.md) .</span><span class="sxs-lookup"><span data-stu-id="b259f-102">See the article [Configure a Virtual Network using the classic portal](../articles/expressroute/expressroute-howto-vnet-portal-classic.md) for more information.</span></span>   

## <a name="add-a-gateway"></a><span data-ttu-id="b259f-103">Ajout d’une passerelle</span><span class="sxs-lookup"><span data-stu-id="b259f-103">Add a gateway</span></span>
<span data-ttu-id="b259f-104">Utilisez la commande suivante pour créer une passerelle.</span><span class="sxs-lookup"><span data-stu-id="b259f-104">Use the command below to create a gateway.</span></span> <span data-ttu-id="b259f-105">Veillez à remplacer les valeurs pas les vôtres.</span><span class="sxs-lookup"><span data-stu-id="b259f-105">Be sure to substitute any values for your own.</span></span>

    New-AzureVirtualNetworkGateway -VNetName "MyAzureVNET" -GatewayName "ERGateway" -GatewayType Dedicated -GatewaySKU  Standard

## <a name="verify-the-gateway-was-created"></a><span data-ttu-id="b259f-106">Vérification de la création de la passerelle</span><span class="sxs-lookup"><span data-stu-id="b259f-106">Verify the gateway was created</span></span>
<span data-ttu-id="b259f-107">Utilisez la commande suivante pour vérifier que la passerelle a été créée.</span><span class="sxs-lookup"><span data-stu-id="b259f-107">Use the command below to verify that the gateway has been created.</span></span> <span data-ttu-id="b259f-108">Cette commande récupère également l’ID de passerelle dont vous avez besoin pour d’autres opérations.</span><span class="sxs-lookup"><span data-stu-id="b259f-108">This command also retrieves the gateway ID, which you need for other operations.</span></span>

    Get-AzureVirtualNetworkGateway

## <a name="resize-a-gateway"></a><span data-ttu-id="b259f-109">Redimensionner une passerelle</span><span class="sxs-lookup"><span data-stu-id="b259f-109">Resize a gateway</span></span>
<span data-ttu-id="b259f-110">Il existe un certain nombre de [Références (SKU) de passerelle](../articles/expressroute/expressroute-about-virtual-network-gateways.md).</span><span class="sxs-lookup"><span data-stu-id="b259f-110">There are a number of [Gateway SKUs](../articles/expressroute/expressroute-about-virtual-network-gateways.md).</span></span> <span data-ttu-id="b259f-111">Vous pouvez utiliser la commande suivante pour modifier la référence de passerelle à tout moment.</span><span class="sxs-lookup"><span data-stu-id="b259f-111">You can use the following command to change the Gateway SKU at any time.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b259f-112">Cette commande ne fonctionne pas pour la passerelle UltraPerformance.</span><span class="sxs-lookup"><span data-stu-id="b259f-112">This command doesn't work for UltraPerformance gateway.</span></span> <span data-ttu-id="b259f-113">Pour modifier votre passerelle en passerelle UltraPerformance, commencez par supprimer la passerelle ExpressRoute, puis créez une passerelle UltraPerformance.</span><span class="sxs-lookup"><span data-stu-id="b259f-113">To change your gateway to an UltraPerformance gateway, first remove the existing ExpressRoute gateway, and then create a new UltraPerformance gateway.</span></span> <span data-ttu-id="b259f-114">Pour mettre à niveau votre passerelle à partir d’une passerelle UltraPerformance, commencez par supprimer la passerelle UltraPerformance, puis créez-en une.</span><span class="sxs-lookup"><span data-stu-id="b259f-114">To downgrade your gateway from an UltraPerformance gateway, first remove the UltraPerformance gateway, and then create a new gateway.</span></span> 
> 
> 

    Resize-AzureVirtualNetworkGateway -GatewayId <Gateway ID> -GatewaySKU HighPerformance

## <a name="remove-a-gateway"></a><span data-ttu-id="b259f-115">Supprimer une passerelle</span><span class="sxs-lookup"><span data-stu-id="b259f-115">Remove a gateway</span></span>
<span data-ttu-id="b259f-116">Utilisez la commande suivante pour supprimer une passerelle.</span><span class="sxs-lookup"><span data-stu-id="b259f-116">Use the command below to remove a gateway</span></span>

    Remove-AzureVirtualNetworkGateway -GatewayId <Gateway ID>