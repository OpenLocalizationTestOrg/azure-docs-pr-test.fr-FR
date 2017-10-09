### <a name="noconnection"></a>préfixes d’adresses toomodify réseau local passerelle IP - aucune connexion de passerelle

préfixes d’adresse supplémentaires tooadd :

```powershell
$local = Get-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName `
Set-AzureRmLocalNetworkGateway -LocalNetworkGateway $local `
-AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24')
```

préfixes d’adresse tooremove :<br>
Exclut les préfixes hello que vous n’avez plus besoin. Dans cet exemple, nous devons de ne plus préfixe 20.0.0.0/24 (à partir de l’exemple précédent hello), afin de nous mettre à jour de passerelle de réseau local hello, à l’exclusion de ce préfixe.

```powershell
$local = Get-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName `
Set-AzureRmLocalNetworkGateway -LocalNetworkGateway $local `
-AddressPrefix @('10.0.0.0/24','30.0.0.0/24')
```

### <a name="withconnection"></a>toomodify réseau local passerelle préfixes d’adresses IP - connexion de passerelle existante

Si vous disposez d’une connexion de passerelle et souhaitez tooadd ou supprimez des préfixes d’adresses IP hello contenues dans votre passerelle de réseau local, vous devez hello toodo comme suit, dans l’ordre. Cela entraînera une interruption de votre connexion VPN. Lorsque vous modifiez des préfixes d’adresses IP, vous n’avez pas besoin passerelle VPN de hello toodelete. Vous devez uniquement la connexion de hello tooremove.


1. Supprimer la connexion de hello.

  ```powershell
  Remove-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName -ResourceGroupName MyRGName
  ```
2. Modifier les préfixes d’adresse hello pour votre passerelle de réseau local.
   
  Définissez la variable hello pour hello passerelle de réseau local.

  ```powershell
  $local = Get-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName
  ```
   
  Modifier les préfixes hello.
   
  ```powershell
  Set-AzureRmLocalNetworkGateway -LocalNetworkGateway $local `
  -AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24')
  ```
3. Créer la connexion de hello. Dans cet exemple, nous allons configurer un type de connexion IPsec. Lorsque vous recréez votre connexion, utilisez le type de connexion hello est spécifié pour votre configuration. Pour les types de connexion supplémentaires, consultez hello [applet de commande PowerShell](https://msdn.microsoft.com/library/mt603611.aspx) page.
   
  Définissez la variable hello pour hello VirtualNetworkGateway.

  ```powershell
  $gateway1 = Get-AzureRmVirtualNetworkGateway -Name RMGateway  -ResourceGroupName MyRGName
  ```
   
  Créer la connexion de hello. Cet exemple utilise la variable de hello $local que vous définissez à l’étape 2.

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName `
  -ResourceGroupName MyRGName -Location 'West US' `
  -VirtualNetworkGateway1 $gateway1 -LocalNetworkGateway2 $local `
  -ConnectionType IPsec `
  -RoutingWeight 10 -SharedKey 'abc123'
  ```