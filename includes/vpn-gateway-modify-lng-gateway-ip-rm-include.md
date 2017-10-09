### <a name="gwipnoconnection"></a>passerelle de réseau local toomodify hello 'GatewayIpAddress' - aucune connexion de passerelle

Si le périphérique VPN de hello que vous souhaitez tooconnect toohas modifié son adresse IP publique, vous devez tooreflect de passerelle du réseau local d’hello toomodify qui changent. Utilisez hello exemple toomodify une passerelle de réseau local qui n’a pas d’une connexion de passerelle.

Lorsque vous modifiez cette valeur, vous pouvez également modifier les préfixes d’adresse hello en hello même temps. Être vraiment toouse hello nom existant de votre passerelle de réseau local dans les paramètres actuels de commande toooverwrite hello. Si vous utilisez un autre nom, vous créez une nouvelle passerelle de réseau local, au lieu de remplacer hello existant.

```powershell
New-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName `
-Location "West US" -AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24') `
-GatewayIpAddress "5.4.3.2" -ResourceGroupName MyRGName
```

### <a name="gwipwithconnection"></a>passerelle de réseau local toomodify hello 'GatewayIpAddress' - connexion à la passerelle existante

Si le périphérique VPN de hello que vous souhaitez tooconnect toohas modifié son adresse IP publique, vous devez tooreflect de passerelle du réseau local d’hello toomodify qui changent. Si une passerelle connexion existe déjà, vous devez d’abord connexion de hello tooremove. Une fois la connexion de hello est supprimée, vous pouvez modifier l’adresse IP de passerelle hello et recréez une nouvelle connexion. Vous pouvez également modifier les préfixes d’adresse hello en hello même temps. Cela entraînera une interruption de votre connexion VPN. Lorsque vous modifiez l’adresse IP de passerelle hello, vous n’avez pas besoin passerelle VPN de hello toodelete. Vous devez uniquement la connexion de hello tooremove.
 

1. Supprimer la connexion de hello. Vous trouverez le nom hello de la connexion à l’aide d’applet de commande hello 'Get-AzureRmVirtualNetworkGatewayConnection'.

  ```powershell
  Remove-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName `
  -ResourceGroupName MyRGName
  ```
2. Modifiez la valeur de 'GatewayIpAddress' hello. Vous pouvez également modifier les préfixes d’adresse hello en hello même temps. Être vraiment toouse hello nom existant de vos paramètres actuels de réseau local passerelle toooverwrite hello. Si vous ne le faites pas, vous créez une nouvelle passerelle de réseau local, au lieu de remplacer hello existant.

  ```powershell
  New-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName `
  -Location "West US" -AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24') `
  -GatewayIpAddress "104.40.81.124" -ResourceGroupName MyRGName
  ```
3. Créer la connexion de hello. Dans cet exemple, nous allons configurer un type de connexion IPsec. Lorsque vous recréez votre connexion, utilisez le type de connexion hello est spécifié pour votre configuration. Pour les types de connexion supplémentaires, consultez hello [applet de commande PowerShell](https://msdn.microsoft.com/library/mt603611.aspx) page.  nom de VirtualNetworkGateway tooobtain hello, vous pouvez exécuter l’applet de commande 'Get-AzureRmVirtualNetworkGateway' hello.
   
    Définir les variables de hello.

  ```powershell
  $local = Get-AzureRMLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName `
  $vnetgw = Get-AzureRmVirtualNetworkGateway -Name RMGateway -ResourceGroupName MyRGName
  ```
   
    Créer la connexion de hello.

  ```powershell 
  New-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName -ResourceGroupName MyRGName `
  -Location "West US" `
  -VirtualNetworkGateway1 $vnetgw `
  -LocalNetworkGateway2 $local `
  -ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
  ```