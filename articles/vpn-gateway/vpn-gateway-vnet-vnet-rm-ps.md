---
title: "Se connecter à un réseau virtuel de tooanother réseau virtuel Azure : PowerShell | Documents Microsoft"
description: "Cet article vous guide dans l’interconnexion de réseaux virtuels avec Azure Resource Manager et PowerShell"
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 0683c664-9c03-40a4-b198-a6529bf1ce8b
ms.service: vpn-gateway
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/02/2017
ms.author: cherylmc
ms.openlocfilehash: 2da30c76867cc3f71d040e63e0dd15d153e15c10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-vnet-to-vnet-vpn-gateway-connection-using-powershell"></a>Configurer une connexion de passerelle VPN de réseau virtuel à réseau virtuel à l’aide de PowerShell

Cet article vous montre comment toocreate une connexion de passerelle VPN entre les réseaux virtuels. Hello réseaux virtuels peuvent être hello identiques ou différentes régions, et à partir de hello identiques ou différents abonnements. Lors de la connexion des réseaux virtuels à partir de différents abonnements, les abonnements hello n’est pas nécessaire de toobe associé hello même client Active Directory. 

étapes de Hello dans cet article appliquent le modèle de déploiement du Gestionnaire de ressources toohello et utilisant de PowerShell. Vous pouvez également créer cette configuration à l’aide d’un outil de déploiement différentes ou d’un modèle de déploiement en sélectionnant une option différente de hello suivant liste :

> [!div class="op_single_selector"]
> * [Portail Azure](vpn-gateway-howto-vnet-vnet-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-vnet-vnet-rm-ps.md)
> * [Interface de ligne de commande Azure](vpn-gateway-howto-vnet-vnet-cli.md)
> * [Portail Azure (classique)](vpn-gateway-howto-vnet-vnet-portal-classic.md)
> * [Connexions entre différents modèles de déploiement - Portail Azure](vpn-gateway-connect-different-deployment-models-portal.md)
> * [Connexions entre différents modèles de déploiement - PowerShell](vpn-gateway-connect-different-deployment-models-powershell.md)
>
>

Connexion d’un réseau virtuel de réseau virtuel tooanother (au réseau) est tooconnecting comme emplacement d’un site réseau virtuel tooan local. Les deux types de connectivité utilisent un tooprovide de passerelle VPN un tunnel sécurisé utilisant IPsec/IKE. Si vos réseaux virtuels sont Bonjour même région, vous souhaiterez peut-être tooconsider les connectant à l’aide de l’homologation de réseau virtuel. L’homologation de réseaux virtuels (ou VNet Peering) n’utilise pas de passerelle VPN. Pour plus d’informations, consultez l’article [Homologation de réseaux virtuels](../virtual-network/virtual-network-peering-overview.md).

Vous pouvez combiner une communication de réseau virtuel à réseau virtuel avec des configurations multisites. Cela vous permet d’établir des topologies de réseau qui combinent une connectivité intersite de connectivité de réseau virtuel entre, comme indiqué dans hello suivant schéma :

![À propos des connexions](./media/vpn-gateway-vnet-vnet-rm-ps/aboutconnections.png)

### <a name="why-connect-virtual-networks"></a>Pourquoi connecter des réseaux virtuels ?

Vous souhaiterez peut-être les réseaux virtuels tooconnect pour hello suivant raisons :

* **Géo-redondance et présence géographique dans plusieurs régions**

  * Vous pouvez configurer la géo-réplication ou la synchronisation avec une connectivité sécurisée sans passer par les points de terminaison accessibles sur Internet.
  * Avec Traffic Manager et l’équilibreur de charge Azure, vous pouvez configurer une charge de travail hautement disponible avec la géo-redondance dans plusieurs régions Azure. Par exemple important, tooset des SQL Always On avec des groupes de disponibilité répartis dans plusieurs régions Azure.
* **Applications multiniveaux régionales avec une limite d’isolement ou administrative**

  * Dans hello même région, vous pouvez définir des applications à plusieurs niveaux avec plusieurs réseaux virtuels interconnectés tooisolation ou exigences administratives.

Pour plus d’informations sur les connexions de réseau virtuel à réseau virtuel, consultez hello [FAQ sur le réseau à](#faq) à fin hello de cet article.

## <a name="which-set-of-steps-should-i-use"></a>Quelle procédure dois-je utiliser ?

Cet article inclut deux ensembles d’étapes distincts. Un ensemble d’étapes pour [qui résident dans des réseaux virtuels hello même abonnement](#samesub)et l’autre pour [des réseaux virtuels qui résident dans différents abonnements](#difsub). Bonjour principale différence entre les jeux de hello est que vous pouvez créer et configurer toutes les ressources réseau et passerelle virtuels au sein de hello même session PowerShell.

Hello étapes dans cet article utilisent les variables qui sont déclarées au début de hello de chaque section. Si vous travaillez déjà avec les réseaux virtuels existants, modifier des paramètres hello variables tooreflect hello votre propre environnement. Si vous souhaitez une résolution de noms pour vos réseaux virtuels, consultez la page [Résolution de noms](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).

## <a name="samesub"></a>Comment tooconnect des réseaux virtuels qui se trouvent dans hello même abonnement

![Diagramme v2v](./media/vpn-gateway-vnet-vnet-rm-ps/v2vrmps.png)

### <a name="before-you-begin"></a>Avant de commencer

Avant de commencer, vous devez tooinstall hello dernière version de hello Azure Resource Manager applets de commande PowerShell, au moins 4.0 ou version ultérieure. Pour plus d’informations sur l’installation des applets de commande PowerShell hello, consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview).

### <a name="Step1"></a>Étape 1 : planifier vos plages d’adresses IP

Bonjour comme suit, nous créer deux réseaux virtuels, ainsi que leurs sous-réseaux de passerelle respectives et les configurations. Nous puis créez une connexion VPN entre hello deux réseaux virtuels. Il s’agit des plages d’adresses IP important tooplan hello pour votre configuration réseau. N’oubliez pas que vous devez vous assurer qu’aucune plage de réseaux virtuels ou de réseaux locaux ne se chevauche. Dans ces exemples, nous n’incluons pas de serveur DNS. Si vous souhaitez une résolution de noms pour vos réseaux virtuels, consultez la page [Résolution de noms](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).

Nous utilisons hello valeurs dans les exemples hello suivantes :

**Valeurs pour TestVNet1 :**

* Nom du réseau virtuel : TestVNet1
* Groupe de ressources : TestRG1
* Emplacement : Est des États-Unis
* TestVNet1 : 10.11.0.0/16 et 10.12.0.0/16
* FrontEnd : 10.11.0.0/24
* BackEnd : 10.12.0.0/24
* GatewaySubnet : 10.12.255.0/27
* GatewayName : VNet1GW
* Adresse IP publique : VNet1GWIP
* Type de VPN : RouteBased
* Connection(1to4) : VNet1toVNet4
* Connection(1to5) : VNet1toVNet5
* Type de connexion : VNet2VNet

**Valeurs pour TestVNet4 :**

* Nom du réseau virtuel : TestVNet4
* TestVNet2 : 10.41.0.0/16 et 10.42.0.0/16
* Serveur frontal : 10.41.0.0/24
* Serveur principal : 10.42.0.0/24
* Sous-réseau de passerelle : 10.42.255.0/27
* Groupe de ressources : TestRG4
* Emplacement : États-Unis de l’Ouest
* Nom de la passerelle : VNet4GW
* Adresse IP publique : VNet4GWIP
* Type de VPN : RouteBased
* Connexion : VNet4toVNet1
* Type de connexion : VNet2VNet


### <a name="Step2"></a>Étape 2 : créez et configurez TestVNet1

1. Déclarez vos variables. Cet exemple déclare les variables de hello en utilisant les valeurs de hello pour cet exercice. Dans la plupart des cas, vous devez remplacer les valeurs hello par les vôtres. Toutefois, vous pouvez utiliser ces variables si vous exécutez via toobecome d’étapes hello familiarisé avec ce type de configuration. Modifier les variables hello si nécessaire, puis copiez et collez-les dans votre console PowerShell.

  ```powershell
  $Sub1 = "Replace_With_Your_Subcription_Name"
  $RG1 = "TestRG1"
  $Location1 = "East US"
  $VNetName1 = "TestVNet1"
  $FESubName1 = "FrontEnd"
  $BESubName1 = "Backend"
  $GWSubName1 = "GatewaySubnet"
  $VNetPrefix11 = "10.11.0.0/16"
  $VNetPrefix12 = "10.12.0.0/16"
  $FESubPrefix1 = "10.11.0.0/24"
  $BESubPrefix1 = "10.12.0.0/24"
  $GWSubPrefix1 = "10.12.255.0/27"
  $GWName1 = "VNet1GW"
  $GWIPName1 = "VNet1GWIP"
  $GWIPconfName1 = "gwipconf1"
  $Connection14 = "VNet1toVNet4"
  $Connection15 = "VNet1toVNet5"
  ```

2. Se connecter tooyour compte. Utilisez hello suivant toohelp exemple que vous connectez :

  ```powershell
  Login-AzureRmAccount
  ```

  Vérifiez les abonnements hello pour le compte de hello.

  ```powershell
  Get-AzureRmSubscription
  ```

  Spécifiez un abonnement hello que vous souhaitez toouse.

  ```powershell
  Select-AzureRmSubscription -SubscriptionName $Sub1
  ```
3. Créez un groupe de ressources.

  ```powershell
  New-AzureRmResourceGroup -Name $RG1 -Location $Location1
  ```
4. Créer des configurations de sous-réseaux pour TestVNet1 hello. Cet exemple crée un réseau virtuel nommé TestVNet1 et trois sous-réseaux nommés GatewaySubnet, FrontEnd et Backend. Lorsque vous remplacez les valeurs, pensez à toujours nommer votre sous-réseau de passerelle « GatewaySubnet ». Si vous le nommez autrement, la création de votre passerelle échoue.

  Hello exemple suivant utilise des variables de hello que vous avez définis précédemment. Dans cet exemple, sous-réseau de passerelle hello utilise un /27. Bien qu’il soit possible de toocreate un sous-réseau de passerelle aussi petit que /29, nous vous recommandons de créer un sous-réseau plus grand qui inclut plusieurs adresses en sélectionnant au moins /28 ou /27. Cette opération permettra suffisamment adresses tooaccommodate possibles des configurations supplémentaires que vous pouvez Bonjour futures.

  ```powershell
  $fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1
  $besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
  $gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1
  ```
5. Créez TestVNet1.

  ```powershell
  New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 `
  -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1
  ```
6. Demander une passerelle publique de toohello alloué toobe adresse IP que vous allez créer pour votre réseau virtuel. Notez que hello AllocationMethod est dynamique. Vous ne pouvez pas spécifier hello adresse IP que vous toouse. Il est alloué dynamiquement tooyour passerelle. 

  ```powershell
  $gwpip1 = New-AzureRmPublicIpAddress -Name $GWIPName1 -ResourceGroupName $RG1 `
  -Location $Location1 -AllocationMethod Dynamic
  ```
7. Créer la configuration de la passerelle hello. configuration de la passerelle Hello définit le sous-réseau de hello et toouse adresse IP publique de hello. Utilisez hello exemple toocreate votre configuration de la passerelle.

  ```powershell
  $vnet1 = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
  $subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
  $gwipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName1 `
  -Subnet $subnet1 -PublicIpAddress $gwpip1
  ```
8. Créer la passerelle de hello pour TestVNet1. Dans cette étape, vous créez passerelle de réseau virtuel hello pour votre TestVNet1. Les configurations de réseau virtuel à réseau virtuel requièrent un VPN de type RouteBased. Création d’une passerelle peut souvent prendre entre 45 minutes ou plus, selon la passerelle sélectionnée de hello référence (SKU).

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 `
  -Location $Location1 -IpConfigurations $gwipconf1 -GatewayType Vpn `
  -VpnType RouteBased -GatewaySku VpnGw1
  ```

### <a name="step-3---create-and-configure-testvnet4"></a>Étape 3 : créez et configurez TestVNet4

Une fois que vous avez configuré TestVNet1, créez TestVNet4. Suivez les étapes de hello ci-dessous, en remplaçant les valeurs de hello par votre propre si nécessaire. Cette étape peut être effectuée dans hello même session PowerShell, car il est hello même abonnement.

1. Déclarez vos variables. Être tooreplace que les valeurs hello avec hello ceux que vous souhaitez toouse pour votre configuration.

  ```powershell
  $RG4 = "TestRG4"
  $Location4 = "West US"
  $VnetName4 = "TestVNet4"
  $FESubName4 = "FrontEnd"
  $BESubName4 = "Backend"
  $GWSubName4 = "GatewaySubnet"
  $VnetPrefix41 = "10.41.0.0/16"
  $VnetPrefix42 = "10.42.0.0/16"
  $FESubPrefix4 = "10.41.0.0/24"
  $BESubPrefix4 = "10.42.0.0/24"
  $GWSubPrefix4 = "10.42.255.0/27"
  $GWName4 = "VNet4GW"
  $GWIPName4 = "VNet4GWIP"
  $GWIPconfName4 = "gwipconf4"
  $Connection41 = "VNet4toVNet1"
  ```
2. Créez un groupe de ressources.

  ```powershell
  New-AzureRmResourceGroup -Name $RG4 -Location $Location4
  ```
3. Créer des configurations de sous-réseaux pour TestVNet4 hello.

  ```powershell
  $fesub4 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName4 -AddressPrefix $FESubPrefix4
  $besub4 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName4 -AddressPrefix $BESubPrefix4
  $gwsub4 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName4 -AddressPrefix $GWSubPrefix4
  ```
4. Créez TestVNet4.

  ```powershell
  New-AzureRmVirtualNetwork -Name $VnetName4 -ResourceGroupName $RG4 `
  -Location $Location4 -AddressPrefix $VnetPrefix41,$VnetPrefix42 -Subnet $fesub4,$besub4,$gwsub4
  ```
5. Demandez une adresse IP publique

  ```powershell
  $gwpip4 = New-AzureRmPublicIpAddress -Name $GWIPName4 -ResourceGroupName $RG4 `
  -Location $Location4 -AllocationMethod Dynamic
  ```
6. Créer la configuration de la passerelle hello.

  ```powershell
  $vnet4 = Get-AzureRmVirtualNetwork -Name $VnetName4 -ResourceGroupName $RG4
  $subnet4 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet4
  $gwipconf4 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName4 -Subnet $subnet4 -PublicIpAddress $gwpip4
  ```
7. Créez hello TestVNet4 passerelle. Création d’une passerelle peut souvent prendre entre 45 minutes ou plus, selon la passerelle sélectionnée de hello référence (SKU).

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName4 -ResourceGroupName $RG4 `
  -Location $Location4 -IpConfigurations $gwipconf4 -GatewayType Vpn `
  -VpnType RouteBased -GatewaySku VpnGw1
  ```

### <a name="step-4---create-hello-connections"></a>Étape 4 : créer des connexions de hello

1. Obtenez les passerelles de réseau virtuel. Si les deux passerelles de hello sont Bonjour même abonnement, comme dans l’exemple de hello, vous pouvez effectuer cette étape Bonjour même session PowerShell.

  ```powershell
  $vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
  $vnet4gw = Get-AzureRmVirtualNetworkGateway -Name $GWName4 -ResourceGroupName $RG4
  ```
2. Créer hello TestVNet1 tooTestVNet4 connexion. Dans cette étape, vous créez des connexions de hello à partir de TestVNet1 tooTestVNet4. Vous verrez une clé partagée est référencée dans les exemples hello. Vous pouvez utiliser vos propres valeurs pour la clé partagée de hello. Hello important est que clé partagée hello doit correspondre pour les deux connexions. Création d’une connexion peut prendre quelques instants toocomplete.

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection14 -ResourceGroupName $RG1 `
  -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet4gw -Location $Location1 `
  -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```
3. Créer hello TestVNet4 tooTestVNet1 connexion. Cette étape est similaire toohello une version ultérieure, mais vous créez hello connexion à partir de TestVNet4 tooTestVNet1. Vérifiez que hello partagé clés correspondent. Hello connexion sera établie après quelques minutes.

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection41 -ResourceGroupName $RG4 `
  -VirtualNetworkGateway1 $vnet4gw -VirtualNetworkGateway2 $vnet1gw -Location $Location4 `
  -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```
4. Vérifiez votre connexion. Consultez la section de hello [comment tooverify votre connexion](#verify).

## <a name="difsub"></a>Comment tooconnect des réseaux virtuels qui se trouvent dans différents abonnements

![Diagramme v2v](./media/vpn-gateway-vnet-vnet-rm-ps/v2vdiffsub.png)

Dans ce scénario, nous connectons TestVNet1 et TestVNet5. TestVNet1 et TestVNet5 se trouvent dans des abonnements différents. les abonnements Hello n’est pas nécessaire de toobe associé hello même client Active Directory. Hello différences entre ces étapes et hello précédente est que certaines des étapes de configuration hello doivent toobe effectuée dans une autre session de PowerShell dans un contexte hello d’abonnement de deuxième hello. En particulier lorsque les abonnements hello deux appartiennent toodifferent organisations.

### <a name="step-5---create-and-configure-testvnet1"></a>Étape 5 : créez et configurez TestVNet1

Vous devez effectuer [étape 1](#Step1) et [étape 2](#Step2) de hello précédente section toocreate et configurer TestVNet1 hello passerelle VPN pour TestVNet1. Pour cette configuration, vous n’êtes pas requis toocreate TestVNet4 à partir de la section précédente de hello, bien que si vous créez il, il ne sera pas en conflit avec ces étapes. Après avoir terminé l’étape 1 et l’étape 2, passez à l’étape 6 toocreate TestVNet5. 

### <a name="step-6---verify-hello-ip-address-ranges"></a>Étape 6 : vérifier les plages d’adresses IP hello

Il est important toomake que l’espace d’adressage IP hello du nouveau réseau virtuel hello TestVNet5, ne se chevauche pas avec les plages VNet ou de plages de passerelle de réseau local. Dans cet exemple, les réseaux virtuels hello peuvent appartenir aux organisations de toodifferent. Dans cet exercice, vous pouvez utiliser hello valeurs pour hello TestVNet5 suivantes :

**Valeurs pour TestVNet5 :**

* Nom du réseau virtuel : TestVNet5
* Groupe de ressources : TestRG5
* Emplacement : Japon de l’Est
* TestVNet5 : 10.51.0.0/16 et 10.52.0.0/16
* Serveur frontal : 10.51.0.0/24
* Serveur principal : 10.52.0.0/24
* Sous-réseau de passerelle : 10.52.255.0.0/27
* Nom de la passerelle : VNet5GW
* Adresse IP publique : VNet5GWIP
* Type de VPN : RouteBased
* Connexion : VNet5toVNet1
* Type de connexion : VNet2VNet

### <a name="step-7---create-and-configure-testvnet5"></a>Étape 7 : créez et configurez TestVNet5

Cette étape doit être effectuée dans le contexte de hello d’abonnement hello. Cette partie ne peut être effectuée par administrateur hello dans une autre organisation qui possède l’abonnement de hello.

1. Déclarez vos variables. Être tooreplace que les valeurs hello avec hello ceux que vous souhaitez toouse pour votre configuration.

  ```powershell
  $Sub5 = "Replace_With_the_New_Subcription_Name"
  $RG5 = "TestRG5"
  $Location5 = "Japan East"
  $VnetName5 = "TestVNet5"
  $FESubName5 = "FrontEnd"
  $BESubName5 = "Backend"
  $GWSubName5 = "GatewaySubnet"
  $VnetPrefix51 = "10.51.0.0/16"
  $VnetPrefix52 = "10.52.0.0/16"
  $FESubPrefix5 = "10.51.0.0/24"
  $BESubPrefix5 = "10.52.0.0/24"
  $GWSubPrefix5 = "10.52.255.0/27"
  $GWName5 = "VNet5GW"
  $GWIPName5 = "VNet5GWIP"
  $GWIPconfName5 = "gwipconf5"
  $Connection51 = "VNet5toVNet1"
  ```
2. Se connecter toosubscription 5. Ouvrez la console PowerShell et tooyour compte de connexion. Utilisez hello suivant toohelp exemple que vous connectez :

  ```powershell
  Login-AzureRmAccount
  ```

  Vérifiez les abonnements hello pour le compte de hello.

  ```powershell
  Get-AzureRmSubscription
  ```

  Spécifiez un abonnement hello que vous souhaitez toouse.

  ```powershell
  Select-AzureRmSubscription -SubscriptionName $Sub5
  ```
3. Créez un groupe de ressources.

  ```powershell
  New-AzureRmResourceGroup -Name $RG5 -Location $Location5
  ```
4. Créer des configurations de sous-réseaux pour TestVNet5 hello.

  ```powershell
  $fesub5 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName5 -AddressPrefix $FESubPrefix5
  $besub5 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName5 -AddressPrefix $BESubPrefix5
  $gwsub5 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName5 -AddressPrefix $GWSubPrefix5
  ```
5. Créez TestVNet5.

  ```powershell
  New-AzureRmVirtualNetwork -Name $VnetName5 -ResourceGroupName $RG5 -Location $Location5 `
  -AddressPrefix $VnetPrefix51,$VnetPrefix52 -Subnet $fesub5,$besub5,$gwsub5
  ```
6. Demandez une adresse IP publique

  ```powershell
  $gwpip5 = New-AzureRmPublicIpAddress -Name $GWIPName5 -ResourceGroupName $RG5 `
  -Location $Location5 -AllocationMethod Dynamic
  ```
7. Créer la configuration de la passerelle hello.

  ```powershell
  $vnet5 = Get-AzureRmVirtualNetwork -Name $VnetName5 -ResourceGroupName $RG5
  $subnet5  = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet5
  $gwipconf5 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName5 -Subnet $subnet5 -PublicIpAddress $gwpip5
  ```
8. Créez hello TestVNet5 passerelle.

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName5 -ResourceGroupName $RG5 -Location $Location5 `
  -IpConfigurations $gwipconf5 -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1
  ```

### <a name="step-8---create-hello-connections"></a>Étape 8 - créer des connexions de hello

Dans cet exemple, étant donné que les passerelles hello sont dans des abonnements différents hello, nous avons fractionner cette étape en deux sessions PowerShell marquées comme [1 abonnement] et [abonnement 5].

1. **[Abonnement 1]**  Passerelle de réseau virtuel get hello pour 1 de l’abonnement. Se connecter et se connecter tooSubscription 1 avant d’exécuter hello l’exemple suivant :

  ```powershell
  $vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
  ```

  Copier le résultat de hello Hello suivant d’éléments et envoyer ces administrateur toohello 5 d’abonnement par courrier électronique ou une autre méthode.

  ```powershell
  $vnet1gw.Name
  $vnet1gw.Id
  ```

  Ces deux éléments aura toohello similaire de valeurs suivant l’exemple de sortie :

  ```
  PS D:\> $vnet1gw.Name
  VNet1GW
  PS D:\> $vnet1gw.Id
  /subscriptions/b636ca99-6f88-4df4-a7c3-2f8dc4545509/resourceGroupsTestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW
  ```
2. **[Abonnement 5]**  Passerelle de réseau virtuel get hello pour 5 de l’abonnement. Se connecter et se connecter tooSubscription 5 avant d’exécuter hello l’exemple suivant :

  ```powershell
  $vnet5gw = Get-AzureRmVirtualNetworkGateway -Name $GWName5 -ResourceGroupName $RG5
  ```

  Copier le résultat de hello Hello suivant d’éléments et envoyer ces administrateur toohello 1 d’abonnement par courrier électronique ou une autre méthode.

  ```powershell
  $vnet5gw.Name
  $vnet5gw.Id
  ```

  Ces deux éléments aura toohello similaire de valeurs suivant l’exemple de sortie :

  ```
  PS C:\> $vnet5gw.Name
  VNet5GW
  PS C:\> $vnet5gw.Id
  /subscriptions/66c8e4f1-ecd6-47ed-9de7-7e530de23994/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW
  ```
3. **[Abonnement 1]**  Créer hello TestVNet1 tooTestVNet5 connexion. Dans cette étape, vous créez des connexions de hello à partir de TestVNet1 tooTestVNet5. Hello différence est que vnet5gw $ Impossible d’obtenir directement, car il est dans un autre abonnement. Vous devez toocreate un nouvel objet PowerShell avec des valeurs hello communiquées à partir de 1 de l’abonnement dans les étapes de hello ci-dessus. Utilisez l’exemple hello ci-dessous. Remplacez hello nom, Id et clé partagée par vos propres valeurs. Hello important est que clé partagée hello doit correspondre pour les deux connexions. Création d’une connexion peut prendre quelques instants toocomplete.

  Se connecter tooSubscription 1 avant d’exécuter hello l’exemple suivant :

  ```powershell
  $vnet5gw = New-Object Microsoft.Azure.Commands.Network.Models.PSVirtualNetworkGateway
  $vnet5gw.Name = "VNet5GW"
  $vnet5gw.Id   = "/subscriptions/66c8e4f1-ecd6-47ed-9de7-7e530de23994/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW"
  $Connection15 = "VNet1toVNet5"
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet5gw -Location $Location1 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```
4. **[Abonnement 5]**  Créer hello TestVNet5 tooTestVNet1 connexion. Cette étape est similaire toohello une version ultérieure, mais vous créez hello connexion à partir de TestVNet5 tooTestVNet1. Hello même processus de création d’un objet PowerShell selon les valeurs hello obtenues à l’abonnement 1 applique ici. Dans cette étape, assurez-vous que les clés de hello partagé correspondent.

  Se connecter tooSubscription 5 avant d’exécuter hello l’exemple suivant :

  ```powershell
  $vnet1gw = New-Object Microsoft.Azure.Commands.Network.Models.PSVirtualNetworkGateway
  $vnet1gw.Name = "VNet1GW"
  $vnet1gw.Id = "/subscriptions/b636ca99-6f88-4df4-a7c3-2f8dc4545509/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW "
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection51 -ResourceGroupName $RG5 -VirtualNetworkGateway1 $vnet5gw -VirtualNetworkGateway2 $vnet1gw -Location $Location5 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```

## <a name="verify"></a>Comment tooverify une connexion

[!INCLUDE [vpn-gateway-no-nsg-include](../../includes/vpn-gateway-no-nsg-include.md)]

[!INCLUDE [verify connections powershell](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

## <a name="faq"></a>Forum Aux Questions sur l’interconnexion de réseaux virtuels

[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]

## <a name="next-steps"></a>Étapes suivantes

* Une fois que votre connexion est terminée, vous pouvez ajouter des machines virtuelles tooyour des réseaux virtuels. Consultez hello [documentation de Machines virtuelles](https://docs.microsoft.com/azure/#pivot=services&panel=Compute) pour plus d’informations.
* Pour plus d’informations sur BGP, consultez hello [vue d’ensemble du protocole BGP](vpn-gateway-bgp-overview.md) et [comment tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).
