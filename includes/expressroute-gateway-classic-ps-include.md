Vous devez créer un réseau virtuel et un sous-réseau de passerelle tout d’abord, avant d’utiliser hello tâches suivantes. Consultez l’article hello [configurer un réseau virtuel à l’aide du portail classique de hello](../articles/expressroute/expressroute-howto-vnet-portal-classic.md) pour plus d’informations.   

## <a name="add-a-gateway"></a>Ajout d’une passerelle
Utilisez la commande hello ci-dessous toocreate une passerelle. Être toosubstitute que toutes les valeurs de votre propre.

    New-AzureVirtualNetworkGateway -VNetName "MyAzureVNET" -GatewayName "ERGateway" -GatewayType Dedicated -GatewaySKU  Standard

## <a name="verify-hello-gateway-was-created"></a>Vérifiez les passerelle hello a été créé.
Utilisez les commandes de hello ci-dessous tooverify qui hello passerelle a été créé. Cette commande récupère également l’ID de passerelle hello, dont vous avez besoin pour d’autres opérations.

    Get-AzureVirtualNetworkGateway

## <a name="resize-a-gateway"></a>Redimensionner une passerelle
Il existe un certain nombre de [Références (SKU) de passerelle](../articles/expressroute/expressroute-about-virtual-network-gateways.md). Vous pouvez utiliser hello suivant commande toochange hello SKU de passerelle à tout moment.

> [!IMPORTANT]
> Cette commande ne fonctionne pas pour la passerelle UltraPerformance. toochange votre passerelle tooan UltraPerformance passerelle, supprimez d’abord hello existant passerelle ExpressRoute et puis créer une passerelle UltraPerformance. toodowngrade votre passerelle à partir d’une passerelle UltraPerformance, supprimez d’abord hello UltraPerformance passerelle, puis créer une passerelle. 
> 
> 

    Resize-AzureVirtualNetworkGateway -GatewayId <Gateway ID> -GatewaySKU HighPerformance

## <a name="remove-a-gateway"></a>Supprimer une passerelle
Utilisez la commande hello ci-dessous tooremove une passerelle

    Remove-AzureVirtualNetworkGateway -GatewayId <Gateway ID>