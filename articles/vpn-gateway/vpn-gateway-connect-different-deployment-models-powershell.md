---
title: "Connecter des réseaux virtuels classiques tooAzure Gestionnaire de ressources VNets : PowerShell | Documents Microsoft"
description: "Découvrez comment toocreate une connexion VPN entre classique des réseaux virtuels et VNets Gestionnaire de ressources à l’aide de la passerelle VPN et PowerShell"
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: f17c3bf0-5cc9-4629-9928-1b72d0c9340b
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/21/2017
ms.author: cherylmc
ms.openlocfilehash: 8b1cf6ae4becf1829fa99961c5dd09a422fcc1fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-virtual-networks-from-different-deployment-models-using-powershell"></a>Connecter des réseaux virtuels utilisant des modèles de déploiement différents à l’aide de PowerShell



Cet article vous explique comment tooconnect classique des réseaux virtuels tooResource Manager VNets tooallow hello ressources situées dans toocommunicate de modèles de déploiement distinct hello entre eux. étapes de Hello dans cet article utilisent PowerShell, mais vous pouvez également créer cette configuration à l’aide de hello portail Azure en sélectionnant l’article de hello dans cette liste.

> [!div class="op_single_selector"]
> * [Portail](vpn-gateway-connect-different-deployment-models-portal.md)
> * [PowerShell](vpn-gateway-connect-different-deployment-models-powershell.md)
> 
> 

La connexion d’un tooa de réseau virtuel classique Gestionnaire de ressources du VNet est tooconnecting comme emplacement d’un site réseau virtuel tooan local. Les deux types de connectivité utilisent un tooprovide de passerelle VPN un tunnel sécurisé utilisant IPsec/IKE. Vous pouvez créer une connexion entre des réseaux virtuels situés dans des abonnements différents et des régions différentes. Vous pouvez également connecter des réseaux virtuels qui ont déjà des connexions tooon des réseaux locaux, tant que passerelle hello qui ils ont été configurés avec est dynamique ou basée sur un itinéraire. Pour plus d’informations sur les connexions de réseau virtuel à réseau virtuel, consultez hello [FAQ sur le réseau à](#faq) à fin hello de cet article. 

Si vos réseaux virtuels sont Bonjour même région, vous souhaiterez peut-être tooinstead connectent à l’aide de l’homologation de réseau virtuel. L’homologation de réseaux virtuels (ou VNet Peering) n’utilise pas de passerelle VPN. Pour plus d’informations, consultez l’article [Homologation de réseaux virtuels](../virtual-network/virtual-network-peering-overview.md). 

## <a name="before-beginning"></a>Avant tout chose

Bonjour étapes suivantes vous guident tooconfigure nécessaires de paramètres hello une passerelle dynamique ou basée sur un itinéraire pour chaque réseau virtuel et créer une connexion VPN entre les passerelles hello. Cette configuration ne prend pas en charge les passerelles statiques ou basées sur des stratégies.

### <a name="prerequisites"></a>Conditions préalables

* Les deux réseaux virtuels ont déjà été créés.
* plages d’adresses Hello pour hello réseaux virtuels ne se chevauchent entre eux, ni ne se chevauchent avec les plages hello pour les autres connexions qui les passerelles hello peuvent être connectés à.
* Vous avez installé les applets de commande PowerShell dernière hello. Consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview) pour plus d’informations. Veillez à qu'installer hello Management Service (SM) et hello applets de commande Gestionnaire de ressources (RM). 

### <a name="exampleref"></a>Exemples de paramètres

Vous pouvez utiliser ces valeurs de toocreate un environnement de test, ou consultez toothem toobetter comprendre les exemples hello dans cet article.

**Paramètres de réseau virtuel classique**

Nom du réseau virtuel = ClassicVNet  <br>
Emplacement = Ouest des États-Unis <br>
Espaces d’adressage du réseau virtuel = 10.0.0.0/24 <br>
Sous-réseau-1 = 10.0.0.0/27 <br>
Sous-réseau de passerelle : 10.0.0.32/29 <br>
Nom du réseau local = RMVNetLocal <br>
Type de passerelle = DynamicRouting

**Paramètres de réseau virtuel Resource Manager**

Nom du réseau virtuel = RMVNet  <br>
Groupe de ressources = RG1 <br>
Espaces d’adressage IP du réseau virtuel = 192.168.0.0/16 <br>
Sous-réseau-1 = 192.168.1.0/24 <br>
Sous-réseau de passerelle = 192.168.0.0/26 <br>
Emplacement = Est des États-Unis <br>
Nom d’adresse IP publique de passerelle = gwpip <br>
Passerelle de réseau local = ClassicVNetLocal <br>
Nom de passerelle de réseau virtuel = RMGateway <br>
Configuration d’adressage IP de la passerelle = gwipconfig

## <a name="createsmgw"></a>Section 1 : configurer hello réseau virtuel classique
### <a name="part-1---download-your-network-configuration-file"></a>Partie 1 : Télécharger votre fichier de configuration réseau
1. Ouvrez une session dans tooyour compte Azure dans la console PowerShell hello avec des droits élevés. Hello applet de commande suivante vous demande les informations d’identification de hello pour votre compte Azure. Une fois connecté, il télécharge les paramètres de votre compte afin qu’ils soient disponible tooAzure PowerShell. Vous utilisez hello toocomplete d’applets de commande PowerShell de SM cette partie de la configuration de hello.

  ```powershell
  Add-AzureAccount
  ```
2. Exportez votre fichier de configuration réseau Azure en exécutant hello commande suivante. Vous pouvez modifier l’emplacement de hello de hello tooexport tooa autre emplacement de fichier si nécessaire.

  ```powershell
  Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
  ```
3. Fichier .xml de hello ouverts que vous avez téléchargé tooedit il. Pour obtenir un exemple de fichier de configuration de réseau hello, consultez hello [schéma de Configuration réseau](https://msdn.microsoft.com/library/jj157100.aspx).

### <a name="part-2--verify-hello-gateway-subnet"></a>Partie 2 - Vérifiez le sous-réseau de passerelle hello
Bonjour **VirtualNetworkSites** élément, ajouter un tooyour de sous-réseau de passerelle réseau virtuel si aucun n’a pas encore été créé. Lorsque vous travaillez avec un fichier de configuration de réseau hello, sous-réseau de passerelle hello doit être nommé « GatewaySubnet » ou Azure ne peut pas reconnaître et utilisez-le comme un sous-réseau de passerelle.

[!INCLUDE [vpn-gateway-no-nsg-include](../../includes/vpn-gateway-no-nsg-include.md)]

**Exemple :**

    <VirtualNetworkSites>
      <VirtualNetworkSite name="ClassicVNet" Location="West US">
        <AddressSpace>
          <AddressPrefix>10.0.0.0/24</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="Subnet-1">
            <AddressPrefix>10.0.0.0/27</AddressPrefix>
          </Subnet>
          <Subnet name="GatewaySubnet">
            <AddressPrefix>10.0.0.32/29</AddressPrefix>
          </Subnet>
        </Subnets>
      </VirtualNetworkSite>
    </VirtualNetworkSites>

### <a name="part-3---add-hello-local-network-site"></a>Partie 3 - Ajouter un site de réseau local hello
vous ajoutez le site réseau local Hello représente hello toowhich de réseau virtuel du Gestionnaire de ressources vous souhaitez tooconnect. Ajouter un **LocalNetworkSites** toohello fichier s’il n’existe pas déjà. À ce stade dans la configuration de hello, hello élément VPNGatewayAddress peut être une adresse IP publique valide, car nous n’avons pas encore créé la passerelle hello pour hello Gestionnaire de ressources VNet. Une fois que nous créons la passerelle de hello, nous remplacez cette adresse de l’espace réservé par hello correct adresse IP publique qui a été attribué de passerelle de RM toohello.

    <LocalNetworkSites>
      <LocalNetworkSite name="RMVNetLocal">
        <AddressSpace>
          <AddressPrefix>192.168.0.0/16</AddressPrefix>
        </AddressSpace>
        <VPNGatewayAddress>13.68.210.16</VPNGatewayAddress>
      </LocalNetworkSite>
    </LocalNetworkSites>

### <a name="part-4---associate-hello-vnet-with-hello-local-network-site"></a>Partie 4 : associer hello réseau virtuel avec un site de réseau local hello
Dans cette section, nous spécifions le site de réseau local que vous souhaitez tooconnect hello hello virtuel à. Dans ce cas, il est hello VNet Gestionnaire de ressources que vous avez référencé précédemment. Assurez-vous que noms de hello correspondent. Cette étape ne vise pas à créer une passerelle. Il spécifie le réseau local, hello hello passerelle se connectera à.

        <Gateway>
          <ConnectionsToLocalNetwork>
            <LocalNetworkSiteRef name="RMVNetLocal">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
          </ConnectionsToLocalNetwork>
        </Gateway>

### <a name="part-5---save-hello-file-and-upload"></a>Partie 5 : enregistrer le fichier de hello et le téléchargement
Enregistrez le fichier de hello, puis l’importer tooAzure en exécutant hello commande suivante. Assurez-vous que vous modifiez le chemin d’accès du fichier hello en fonction de votre environnement.

```powershell
Set-AzureVNetConfig -ConfigurationPath C:\AzureNet\NetworkConfig.xml
```

Vous verrez un résultat similaire indiquant que l’importation de hello a réussi.

        OperationDescription        OperationId                      OperationStatus                                                
        --------------------        -----------                      ---------------                                                
        Set-AzureVNetConfig        e0ee6e66-9167-cfa7-a746-7casb9    Succeeded 

### <a name="part-6---create-hello-gateway"></a>Partie 6 - créer une passerelle de hello

Avant d’exécuter cet exemple, consultez toohello fichier de configuration réseau que vous avez téléchargé pour hello exacte des noms que Azure attend toosee. fichier de configuration de réseau Hello contient des valeurs de hello pour vos réseaux virtuels classiques. Parfois, les noms de hello pour classique des réseaux virtuels sont modifiées dans le fichier de configuration de réseau hello lors de la création des paramètres de réseau virtuel classiques dans hello portail Azure en raison de différences toohello dans les modèles de déploiement hello. Par exemple, si vous avez utilisé hello Azure toocreate portail un réseau virtuel classique nommé « Réseau virtuel classique » et créé un conteneur dans un groupe de ressources nommé 'ClassicRG', nom hello qui est contenue dans le fichier de configuration de réseau hello est converti too'Group réseau virtuel classique de ClassicRG'. Lorsque vous spécifiez le nom hello d’un réseau virtuel qui contient des espaces, placez-la entre guillemets les valeur hello.


Utilisez hello suivant exemple toocreate une passerelle avec routage dynamique :

```powershell
New-AzureVNetGateway -VNetName ClassicVNet -GatewayType DynamicRouting
```

Vous pouvez vérifier l’état de hello de passerelle de hello à l’aide de hello **Get-AzureVNetGateway** applet de commande.

## <a name="creatermgw"></a>Section 2 : Configurer hello passerelle de réseau virtuel du Gestionnaire de ressources
toocreate une passerelle VPN pour hello réseau virtuel RM, suivez hello suivant les instructions. Ne pas démarrer les étapes hello jusqu'à ce qu’après avoir récupéré les adresse IP publique hello pour la passerelle de hello classique de réseau virtuel. 

1. Ouvrez une session dans tooyour compte Azure dans la console PowerShell hello. Hello applet de commande suivante vous demande les informations d’identification de hello pour votre compte Azure. Après la connexion, les paramètres de votre compte sont téléchargés afin qu’ils soient disponible tooAzure PowerShell.

  ```powershell
  Login-AzureRmAccount
  ``` 
   
  Si vous possédez plusieurs abonnements, procurez-vous la liste de vos abonnements Azure.

  ```powershell
  Get-AzureRmSubscription
  ```
   
  Spécifiez un abonnement hello que vous souhaitez toouse.

  ```powershell
  Select-AzureRmSubscription -SubscriptionName "Name of subscription"
  ```
2. Créer une passerelle de réseau local. Dans un réseau virtuel, passerelle de réseau local hello fait généralement référence emplacement local de tooyour. Dans ce cas, passerelle de réseau local hello fait référence tooyour classique de réseau virtuel. Lui donner un nom par lequel Azure permettre faire référence tooit et également spécifier le préfixe d’espace adresse hello. Azure utilise le préfixe d’adresse IP hello vous spécifiez tooidentify les tooyour toosend de trafic emplacement local. Si vous avez besoin d’informations tooadjust hello ici une version ultérieure, avant de créer votre passerelle, vous pouvez modifier les valeurs hello et exemple hello exécuter à nouveau.
   
   **-Name** est hello nom de passerelle de réseau local tooassign toorefer toohello.<br>
   **Préfixe d’adresse -** est hello espace d’adressage de votre réseau virtuel classique.<br>
   **-GatewayIpAddress** est hello une adresse IP publique de la passerelle de hello classique de réseau virtuel. Veillez à suivant de hello toochange exemple tooreflect hello adresse IP.<br>

  ```powershell
  New-AzureRmLocalNetworkGateway -Name ClassicVNetLocal `
  -Location "West US" -AddressPrefix "10.0.0.0/24" `
  -GatewayIpAddress "n.n.n.n" -ResourceGroupName RG1
  ```
3. La demande publique IP adresse toobe toohello alloué passerelle de réseau virtuel pour hello Gestionnaire de ressources VNet. Vous ne pouvez pas spécifier hello adresse IP que vous toouse. adresse IP de Hello est allouée dynamiquement la passerelle de réseau virtuel toohello. Toutefois, cela ne signifie pas de changements d’adresses IP hello. Hello seule fois changements d’adresses IP passerelle hello réseau virtuel est hello lorsque la passerelle est supprimée et recréée. Il ne change pas sur le redimensionnement, la réinitialisation ou autre maintenance/mise à niveau interne de la passerelle de hello.

  Dans cette étape, nous définissons également une variable qui sera utilisée à une étape ultérieure.

  ```powershell
  $ipaddress = New-AzureRmPublicIpAddress -Name gwpip `
  -ResourceGroupName RG1 -Location 'EastUS' `
  -AllocationMethod Dynamic
  ```

4. Vérifiez que votre réseau virtuel possède un sous-réseau de passerelle. S’il n’existe aucun sous-réseau de passerelle, ajoutez-en un. Assurez-vous que le sous-réseau de passerelle hello est nommé *GatewaySubnet*.
5. Récupérer le sous-réseau hello utilisé pour la passerelle de hello en exécutant hello commande suivante. Dans cette étape, nous définissons également une variable toobe utilisé à l’étape suivante de hello.
   
   **-Name** hello désigne votre VNet Gestionnaire de ressources.<br>
   **-ResourceGroupName** est groupe de ressources hello que hello réseau virtuel est associé. sous-réseau de passerelle Hello pour ce réseau virtuel doivent déjà exister et doit être nommé *GatewaySubnet* toowork correctement.<br>

  ```powershell
  $subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name GatewaySubnet `
  -VirtualNetwork (Get-AzureRmVirtualNetwork -Name RMVNet -ResourceGroupName RG1)
  ``` 

6. Créer la configuration d’adressage IP de la passerelle hello. configuration de la passerelle Hello définit le sous-réseau de hello et toouse adresse IP publique de hello. Les exemples suivants de hello utilisation toocreate votre configuration de la passerelle.

  Dans cette étape, hello **- IDSousRéseau** et **- PublicIpAddressId** paramètres doivent être passés propriété d’id hello à partir du sous-réseau de hello et objets d’adresse IP, respectivement. Vous ne pouvez pas utiliser une chaîne simple. Ces variables sont définies dans hello étape toorequest une adresse IP publique et hello étape tooretrieve hello sous-réseau.

  ```powershell
  $gwipconfig = New-AzureRmVirtualNetworkGatewayIpConfig `
  -Name gwipconfig -SubnetId $subnet.id `
  -PublicIpAddressId $ipaddress.id
  ```
7. Créer des passerelle de réseau virtuel du Gestionnaire de ressources hello en hello suivant de commande en cours d’exécution. Hello `-VpnType` doit être *RouteBased*. Il peut prendre entre 45 minutes ou plus pour hello passerelle toocreate.

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name RMGateway -ResourceGroupName RG1 `
  -Location "EastUS" -GatewaySKU Standard -GatewayType Vpn `
  -IpConfigurations $gwipconfig `
  -EnableBgp $false -VpnType RouteBased
  ```
8. Copiez l’adresse IP publique de hello une fois la passerelle VPN de hello a été créé. Utilisez-la lorsque vous configurez les paramètres de réseau local hello pour votre réseau virtuel classique. Vous pouvez utiliser hello suivant l’adresse IP publique d’applet de commande tooretrieve hello. adresse IP publique Hello est répertoriée dans hello retour en tant que *IpAddress*.

  ```powershell
  Get-AzureRmPublicIpAddress -Name gwpip -ResourceGroupName RG1
  ```

## <a name="section-3-modify-hello-classic-vnet-local-site-settings"></a>Section 3 : Modifier les paramètres de site local de réseau virtuel classiques hello

Dans cette section, vous travaillez avec hello réseau virtuel classique. Vous remplacez les adresses IP hello espace réservé que vous avez utilisé lors de la spécification des paramètres du site local hello qui seront utilisé tooconnect toohello passerelle du Gestionnaire de ressources VNet. 

1. Exporter le fichier de configuration de réseau hello.

  ```powershell
  Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
  ```
2. À l’aide d’un éditeur de texte, de modifier la valeur de hello pour l’élément VPNGatewayAddress. Remplacez adresse espace réservé de hello hello adresse IP publique de passerelle du Gestionnaire de ressources hello, puis enregistrez les modifications hello.

  ```
  <VPNGatewayAddress>13.68.210.16</VPNGatewayAddress>
  ```
3. Hello d’importation modifiée tooAzure de fichier de configuration de réseau.

  ```powershell
  Set-AzureVNetConfig -ConfigurationPath C:\AzureNet\NetworkConfig.xml
  ```

## <a name="connect"></a>Dans la section 4 : Créer une connexion entre les passerelles hello
Création d’une connexion entre les passerelles hello requiert PowerShell. Vous devrez peut-être tooadd votre version compte Azure toouse hello classique d’applets de commande PowerShell hello. toodo donc utiliser **Add-AzureAccount**.

1. Dans la console PowerShell hello, définissez votre clé partagée. Avant d’exécuter les applets de commande hello, consultez toohello fichier de configuration réseau que vous avez téléchargé pour hello exacte des noms que Azure attend toosee. Lorsque vous spécifiez le nom hello d’un réseau virtuel qui contient des espaces, utilisez des guillemets simples autour de valeur de hello.<br><br>Dans l’exemple suivant, **- VNetName** hello désigne hello réseau virtuel classique et **LocalNetworkSiteName -** est le nom hello spécifié pour le site de réseau local hello. Hello **SharedKey -** est une valeur que vous générez et que vous spécifiez. Dans l’exemple de hello, nous avons utilisé « abc123 », mais vous pouvez également générer et utiliser quelque chose de plus complexe. Hello important est cette valeur hello que vous spécifiez ici doit être hello que même valeur que vous spécifiez dans l’étape suivante de hello lorsque vous créez votre connexion. Hello retour doit afficher **état : réussite**.

  ```powershell
  Set-AzureVNetGatewayKey -VNetName ClassicVNet `
  -LocalNetworkSiteName RMVNetLocal -SharedKey abc123
  ```
2. Créer la connexion de VPN de hello en hello suivant les commandes en cours d’exécution :
   
  Définir les variables de hello.

  ```powershell
  $vnet01gateway = Get-AzureRMLocalNetworkGateway -Name ClassicVNetLocal -ResourceGroupName RG1
  $vnet02gateway = Get-AzureRmVirtualNetworkGateway -Name RMGateway -ResourceGroupName RG1
  ```
   
  Créer la connexion de hello. Notez que hello **- ConnectionType** IPSec, Vnet2Vnet pas.

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name RM-Classic -ResourceGroupName RG1 `
  -Location "East US" -VirtualNetworkGateway1 `
  $vnet02gateway -LocalNetworkGateway2 `
  $vnet01gateway -ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
  ```

## <a name="section-5-verify-your-connections"></a>Section 5 : Vérifier vos connexions

### <a name="tooverify-hello-connection-from-your-classic-vnet-tooyour-resource-manager-vnet"></a>connexion de hello tooverify à partir de votre tooyour de réseau virtuel classique Gestionnaire de ressources VNet

#### <a name="powershell"></a>PowerShell

[!INCLUDE [vpn-gateway-verify-connection-ps-classic](../../includes/vpn-gateway-verify-connection-ps-classic-include.md)]

#### <a name="azure-portal"></a>Portail Azure

[!INCLUDE [vpn-gateway-verify-connection-azureportal-classic](../../includes/vpn-gateway-verify-connection-azureportal-classic-include.md)]


### <a name="tooverify-hello-connection-from-your-resource-manager-vnet-tooyour-classic-vnet"></a>connexion de hello tooverify à partir de votre gestionnaire de ressources du VNet de tooyour réseau virtuel classique

#### <a name="powershell"></a>PowerShell

[!INCLUDE [vpn-gateway-verify-ps-rm](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

#### <a name="azure-portal"></a>Portail Azure

[!INCLUDE [vpn-gateway-verify-connection-portal-rm](../../includes/vpn-gateway-verify-connection-portal-rm-include.md)]

## <a name="faq"></a>Forum Aux Questions sur l’interconnexion de réseaux virtuels

[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]

