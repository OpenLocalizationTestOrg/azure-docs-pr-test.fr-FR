étapes Hello pour cette tâche, utilisez un réseau virtuel en fonction des valeurs hello hello suivant liste de référence de configuration. Les noms et paramètres supplémentaires sont également présentés dans cette liste. Nous n’utilisons cette liste directement dans une des étapes de hello, bien que nous ajoutez des variables en fonction des valeurs hello dans cette liste. Vous pouvez copier hello liste toouse en tant que référence, en remplaçant les valeurs hello par les vôtres.

**Liste de référence de configuration**

* Nom du réseau virtuel : « TestVNet »
* Espace d’adressage du réseau virtuel : 192.168.0.0/16
* Groupe de ressources : « TestRG »
* Nom du sous-réseau 1 : « FrontEnd » 
* Espace d’adressage du sous-réseau 1 = "192.168.1.0/24"
* Nom de sous-réseau de passerelle : « GatewaySubnet » Vous devez toujours nommer un sous-réseau de passerelle *GatewaySubnet*.
* Espace d'adressage du sous-réseau de passerelle : « 192.168.200.0/26 »
* Région : « Est des États-Unis »
* Nom de la passerelle : « GW »
* Nom d’adresse IP de la passerelle : « GWIP »
* Nom de configuration IP de la passerelle : « gwipconf »
* Type : « ExpressRoute » Ce type est requis pour une configuration ExpressRoute.
* Nom d’adresse IP publique de passerelle = « gwpip »

## <a name="add-a-gateway"></a>Ajout d’une passerelle
1. Se connecter tooyour abonnement Azure.

  ```powershell 
  Login-AzureRmAccount
  Get-AzureRmSubscription 
  Select-AzureRmSubscription -SubscriptionName "Name of subscription"
  ```
2. Déclarez vos variables pour cet exercice. Être tooedit vraiment hello exemple tooreflect hello de paramètres que vous souhaitez toouse.

  ```powershell 
  $RG = "TestRG"
  $Location = "East US"
  $GWName = "GW"
  $GWIPName = "GWIP"
  $GWIPconfName = "gwipconf"
  $VNetName = "TestVNet"
  ```
3. Stocker l’objet de réseau virtuel hello comme une variable.

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG
  ```
4. Ajouter un tooyour de sous-réseau de passerelle réseau virtuel. sous-réseau de passerelle Hello doit être nommé « GatewaySubnet ». Vous devez créer un sous-réseau de passerelle défini sur /27 ou plus (/26, /25, etc.).

  ```powershell
  Add-AzureRmVirtualNetworkSubnetConfig -Name GatewaySubnet -VirtualNetwork $vnet -AddressPrefix 192.168.200.0/26
  ```
5. Définir la configuration hello.

  ```powershell
  Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
6. Stocker le sous-réseau de passerelle hello comme une variable.

  ```powershell
  $subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -VirtualNetwork $vnet
  ```
7. Demandez une adresse IP publique une adresse IP Hello est requise avant de créer la passerelle de hello. Vous ne pouvez pas spécifier hello adresse IP que toouse ; elle est allouée dynamiquement. Vous utiliserez cette adresse IP dans la section de configuration suivante hello. Hello AllocationMethod doit être dynamiques.

  ```powershell
  $pip = New-AzureRmPublicIpAddress -Name $GWIPName  -ResourceGroupName $RG -Location $Location -AllocationMethod Dynamic
  ```
8. Créer la configuration hello pour votre passerelle. configuration de la passerelle Hello définit le sous-réseau de hello et toouse adresse IP publique de hello. Dans cette étape, vous spécifiez configuration hello qui sera utilisée lors de la création de la passerelle de hello. Cette étape ne crée pas réellement l’objet de passerelle hello. Utilisez exemple hello ci-dessous toocreate votre configuration de la passerelle.

  ```powershell
  $ipconf = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName -Subnet $subnet -PublicIpAddress $pip
  ```
9. Créer la passerelle de hello. Dans cette étape, hello **- le type de passerelle** est particulièrement important. Vous devez utiliser la valeur de hello **ExpressRoute**. Après l’exécution de ces applets de commande, passerelle de hello peut prendre entre 45 minutes ou plus toocreate.

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG -Location $Location -IpConfigurations $ipconf -GatewayType Expressroute -GatewaySku Standard
  ```

## <a name="verify-hello-gateway-was-created"></a>Vérifiez les passerelle hello a été créé.
Utilisez hello suivant les commandes tooverify qui hello passerelle a été créé :

```powershell
Get-AzureRmVirtualNetworkGateway -ResourceGroupName $RG
```

## <a name="resize-a-gateway"></a>Redimensionner une passerelle
Il existe un certain nombre de [Références (SKU) de passerelle](../articles/expressroute/expressroute-about-virtual-network-gateways.md). Vous pouvez utiliser hello suivant commande toochange hello SKU de passerelle à tout moment.

> [!IMPORTANT]
> Cette commande ne fonctionne pas pour la passerelle UltraPerformance. toochange votre passerelle tooan UltraPerformance passerelle, supprimez d’abord hello existant passerelle ExpressRoute et puis créer une passerelle UltraPerformance. toodowngrade votre passerelle à partir d’une passerelle UltraPerformance, supprimez d’abord hello UltraPerformance passerelle, puis créer une passerelle.
> 
> 

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG
Resize-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -GatewaySku HighPerformance
```

## <a name="remove-a-gateway"></a>Supprimer une passerelle
Hello suivant commande tooremove une passerelle, utilisez :

```powershell
Remove-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG
```