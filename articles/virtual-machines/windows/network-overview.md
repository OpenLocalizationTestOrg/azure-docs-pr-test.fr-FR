---
title: "aaaVirtual réseaux et les machines virtuelles Windows Azure | Documents Microsoft"
description: "En savoir plus sur la mise en réseau en matière de bases de toohello de la création de machines virtuelles Windows dans Azure."
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 5493e9f7-7d45-4e98-be9a-657a53708746
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: davidmu
ms.openlocfilehash: e28a4782f9f6c69f6101e45dbb560ccd694a1e07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="virtual-networks-and-windows-virtual-machines-in-azure"></a>Réseaux virtuels et machines virtuelles Windows dans Azure 

Lorsque vous créez une machine virtuelle Azure, vous devez créer un [réseau virtuel](../../virtual-network/virtual-networks-overview.md) ou en utiliser un existant. Vous devez également toodecide comment vos machines virtuelles sont toobe prévu sur hello réseau virtuel. Il est important[plan avant de créer des ressources](../../virtual-network/virtual-network-vnet-plan-design-arm.md) et assurez-vous que vous comprenez hello [limites de ressources réseau](../../azure-subscription-service-limits.md#networking-limits).

Bonjour la figure suivante, les machines virtuelles sont représentées comme des serveurs web et serveurs de base de données. Chaque groupe de machines virtuelles sont affectées les sous-réseaux tooseparate Bonjour réseau virtuel.

![réseau virtuel Azure](./media/network-overview/vnetoverview.png)

Vous pouvez créer un réseau virtuel avant de créer une machine virtuelle, ou vous pouvez créer hello réseau virtuel lors de la création d’une machine virtuelle. Vous devez créer un réseau virtuel vous-même ou un réseau virtuel est créé automatiquement lorsque vous créez une machine virtuelle.

Vous créez ces ressources de toosupport communication avec une machine virtuelle :

- Interfaces réseau
- Adresses IP
- Réseau virtuel et sous-réseaux

En outre les ressources de base toothose, vous devez également envisager ces ressources facultatives :

- groupes de sécurité réseau ;
- Équilibreurs de charge 

## <a name="network-interfaces"></a>Interfaces réseau

A [l’interface réseau (NIC)](../../virtual-network/virtual-network-network-interface.md) est interconnexion hello entre un ordinateur virtuel et un réseau virtuel (VNet). Un ordinateur virtuel doit avoir au moins une carte réseau, mais il peut avoir plusieurs, selon la taille de hello Hello machine virtuelle que vous créez. Consultez l’article [Tailles des machines virtuelles dans Azure](sizes.md) pour savoir combien de cartes d’interface réseau sont requises en fonction de chaque taille de machine virtuelle. 

Si vous souhaitez toocreate une machine virtuelle avec plusieurs cartes réseau, vous devez créer hello machine virtuelle avec au moins deux.  Après sa création, vous pouvez ajouter des cartes réseau numéro toohello pris en charge par la taille de machine virtuelle hello, mais vous ne pouvez pas ajouter tooa de cartes réseau supplémentaire VM uniquement créé avec l’un, quel que soit le nombre de cartes réseau hello taille de machine virtuelle prend en charge. 

Si hello machine virtuelle est ajouté tooan à haute disponibilité, tous les ordinateurs virtuels au sein du groupe à haute disponibilité hello doivent avoir une ou plusieurs cartes réseau. Machines virtuelles avec plusieurs cartes réseau ne sont pas requis toohave hello même nombre de cartes réseau, mais ils doivent tous avoir au moins deux.

Chaque tooa de carte réseau attachée machine virtuelle doit exister dans hello même emplacement et abonnement comme hello de machine virtuelle. Chaque carte réseau doit être connectée tooa réseau virtuel qui existe dans hello même emplacement Azure et abonnement comme hello de carte réseau. Après la création d’une carte réseau, vous pouvez modifier le sous-réseau hello à qu'il est connecté, mais vous ne pouvez pas modifier hello, il est connecté à des réseaux.  Chaque carte réseau attachée tooa que machine virtuelle est affectée à une adresse MAC qui ne change pas jusqu'à ce que hello machine virtuelle est supprimé.

Ce tableau répertorie les méthodes hello que vous pouvez utiliser toocreate une interface réseau.

| Méthode | Description |
| ------ | ----------- |
| Portail Azure | Lorsque vous créez une machine virtuelle dans hello portail Azure, une interface réseau est automatiquement créée pour vous (vous ne pouvez pas utiliser une carte réseau que vous créez séparément). portail de Hello crée une machine virtuelle avec uniquement une carte réseau. Si vous souhaitez toocreate une machine virtuelle avec plusieurs cartes réseau, vous devez le créer avec une autre méthode. |
| [Azure PowerShell](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md) | Utilisez [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) avec hello **- PublicIpAddressId** paramètre tooprovide hello identificateur de l’adresse IP publique hello que vous avez créé précédemment. |
| [Interface de ligne de commande Azure](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md) | identificateur de hello tooprovide de l’adresse IP publique hello d’adresses que vous avez créé précédemment, utilisez [créer des cartes réseau du réseau az](https://docs.microsoft.com/cli/azure/network/nic#create) avec hello **--adresse ip publique** paramètre. |
| [Modèle](../../virtual-network/virtual-network-deploy-multinic-arm-template.md) | Utilisez [Network Interface in a Virtual Network with Public IP Address](https://github.com/Azure/azure-quickstart-templates/tree/master/101-nic-publicip-dns-vnet) comme guide pour le déploiement d’une interface réseau à l’aide d’un modèle. |

## <a name="ip-addresses"></a>Adresses IP 

Vous pouvez attribuer à ces types de [des adresses IP](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) tooa carte réseau dans Azure :

- **Les adresses IP publiques** -utilisé toocommunicate entrant et sortant (sans traduction d’adresses réseau (NAT)) par hello Internet et autres ressources Azure pas connecté tooa réseau virtuel. Affectation d’un tooa d’adresse IP publique de carte réseau est facultative. Les adresses IP publiques ont un coût nominal et il existe une limite maximum d’adresses IP publiques pouvant être utilisées par abonnement.
- **Adresses IP privées** - utilisés pour la communication au sein d’un réseau virtuel, votre réseau local et hello Internet (NAT). Vous devez attribuer au moins un tooa d’adresse IP privée machine virtuelle. toolearn en savoir plus sur NAT dans Azure, lisez [présentation des connexions sortantes dans Azure](../../load-balancer/load-balancer-outbound-connections.md).

Vous pouvez affecter tooVMs d’adresses IP publiques ou des équilibreurs de charge connecté à internet. Vous pouvez affecter privé tooVMs d’adresses IP et équilibreurs de charge interne. Vous affectez tooa d’adresses IP à l’aide d’une interface réseau de machine virtuelle.

Il existe deux méthodes dans lesquelles une adresse IP est allouée tooa ressource - dynamique ou statique. méthode d’allocation par défaut Hello est dynamique, où une adresse IP n’est pas allouée lors de sa création. Au lieu de cela, adresse IP de hello est allouée lorsque vous créez une machine virtuelle ou que vous démarrez une machine virtuelle arrêtée. adresse IP de Hello est libérée lorsque vous arrêtez ou supprimez hello machine virtuelle. 

adresse IP tooensure hello hello machine virtuelle reste Bonjour même, vous pouvez définir explicitement méthode d’allocation de hello toostatic. Dans ce cas, une adresse IP est attribuée immédiatement. Elle est libérée uniquement lorsque vous supprimez hello machine virtuelle ou modifiez son toodynamic de la méthode d’allocation.
    
Ce tableau répertorie les méthodes hello que vous pouvez utiliser une adresse IP de toocreate.

| Méthode | Description |
| ------ | ----------- |
| [Portail Azure](../../virtual-network/virtual-network-deploy-static-pip-arm-portal.md) | Par défaut, les adresses IP publiques sont dynamiques et hello adresse toothem peut changer lorsque hello machine virtuelle est arrêtée ou supprimée. tooguarantee qui hello toujours de machine virtuelle utilise hello la même adresse IP publique, créez une adresse IP publique statique. Par défaut, le portail de hello assigne un tooa d’adresse IP privé dynamique carte réseau lors de la création d’une machine virtuelle. Vous pouvez modifier cette toostatic après hello que machine virtuelle est créée.|
| [Azure PowerShell](../../virtual-network/virtual-network-deploy-static-pip-arm-ps.md) | Vous utilisez [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress) avec hello **- AllocationMethod** paramètre dynamique ou statique. |
| [Interface de ligne de commande Azure](../../virtual-network/virtual-network-deploy-static-pip-arm-cli.md) | Vous utilisez [az réseau public-ip créer](https://docs.microsoft.com/cli/azure/network/public-ip#create) avec hello **---méthode d’allocation** paramètre dynamique ou statique. |
| [Modèle](../../virtual-network/virtual-network-deploy-static-pip-arm-template.md) | Utilisez [Network Interface in a Virtual Network with Public IP Address](https://github.com/Azure/azure-quickstart-templates/tree/master/101-nic-publicip-dns-vnet) comme guide pour le déploiement d’une adresse IP publique à l’aide d’un modèle. |

Après avoir créé une adresse IP publique, vous pouvez l’associer à une machine virtuelle en lui assignant tooa carte réseau.

## <a name="virtual-network-and-subnets"></a>Réseau virtuel et sous-réseaux

Un sous-réseau est une plage d’adresses IP Bonjour réseau virtuel. Vous pouvez diviser un réseau virtuel en plusieurs sous-réseaux pour plus de sécurité et une meilleure organisation. Chaque carte réseau d’un ordinateur virtuel est un sous-réseau tooone connectés dans un réseau virtuel. Cartes réseau des toosubnets connectés (identiques ou différents) d’un réseau virtuel peuvent communiquer entre eux sans aucune configuration supplémentaire.

Lorsque vous configurez un réseau virtuel, vous spécifiez la topologie hello, notamment les sous-réseaux et des espaces d’adressage disponible hello. Si hello réseau virtuel est réseaux des réseaux virtuels ou locaux tooother toobe connecté, vous devez sélectionner des plages d’adresses qui ne se chevauchent pas. adresses IP de Hello sont privés et ne sont pas accessibles à partir d’Internet, ce qui a la valeur true uniquement pour les adresses IP non routables hello comme 10.0.0.0/8, 172.16.0.0/12 ou 192.168.0.0/16 de hello. Désormais, Azure traite toute plage d’adresses dans le cadre de hello VNet espace d’adressage IP qui est uniquement accessible dans hello réseau virtuel, dans des réseaux virtuels interconnectés et depuis votre emplacement local. 

Si vous travaillez dans une organisation dans laquelle une autre personne est responsable de réseaux internes de hello, vous devez contacter toothat personne avant de sélectionner votre espace d’adressage. Assurez-vous que ne se chevauchent pas et dites-leur espace hello toouse afin qu’ils n’essaient pas toouse hello même plage d’adresses IP. 

Par défaut, il n’existe aucune limite de sécurité entre les sous-réseaux, afin de machines virtuelles dans chacun de ces sous-réseaux peuvent communiquer avec tooone un autre. Toutefois, vous pouvez définir des groupes de sécurité réseau (NSG), qui vous permettent du flux du trafic toocontrol hello tooand de sous-réseaux et tooand à partir d’ordinateurs virtuels. 

Ce tableau répertorie les méthodes hello que vous pouvez utiliser toocreate un réseau virtuel et sous-réseaux.   

| Méthode | Description |
| ------ | ----------- |
| [Portail Azure](../../virtual-network/virtual-networks-create-vnet-arm-pportal.md) | Si vous permettez de créer un réseau virtuel lorsque vous créez une machine virtuelle Azure, nom de hello est une combinaison de nom de groupe de ressources hello contenant hello réseau virtuel et **- réseau virtuel**. espace d’adressage Hello est 10.0.0.0/24, nom du sous-réseau hello est **par défaut**, et de la plage d’adresses de sous-réseau de hello est 10.0.0.0/24. |
| [Azure PowerShell](../../virtual-network/virtual-networks-create-vnet-arm-ps.md) | Vous utilisez [New-AzureRmVirtualNetworkSubnetConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmVirtualNetworkSubnetConfig) et [New-AzureRmVirtualNetwork](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmVirtualNetwork) toocreate un sous-réseau et un réseau virtuel. Vous pouvez également utiliser [Add-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/add-azurermvirtualnetworksubnetconfig) tooadd un tooan sous-réseau réseau virtuel existant. |
| [Interface de ligne de commande Azure](../../virtual-network/virtual-networks-create-vnet-arm-cli.md) | Hello sous-réseau et hello réseau virtuel sont créés au niveau hello même temps. Fournir un **--nom de sous-réseau** paramètre trop[créer un réseau virtuel du réseau az](https://docs.microsoft.com/cli/azure/network/vnet#create) avec le nom du sous-réseau hello. |
| [Modèle](../../virtual-network/virtual-networks-create-vnet-arm-template-click.md) | Hello toocreate de façon simple un réseau virtuel et sous-réseaux est toodownload un modèle existant, tel que [réseau virtuel avec deux sous-réseaux](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets)et les modifier en fonction de vos besoins. |

## <a name="network-security-groups"></a>groupes de sécurité réseau ;

A [le groupe de sécurité réseau (NSG)](../../virtual-network/virtual-networks-nsg.md) contient une liste de règles de liste de contrôle d’accès (ACL) qui autorisent ou refusent toosubnets de trafic réseau, cartes réseau ou les deux. Groupes de sécurité réseau peuvent être associés à des sous-réseaux ou sous-réseau de tooa connecté de cartes réseau individuelles. Lorsqu’un groupe de sécurité réseau est associé à un sous-réseau, listes de contrôle hello s’appliquent tooall hello machines virtuelles dans ce sous-réseau. En outre, le trafic tooan NIC individuel peut être restreint en associant un groupe de sécurité réseau directement tooa carte réseau.

Les groupes de sécurité réseau contiennent deux ensembles de règles : les règles de trafic entrant et les règles de trafic sortant. priorité de Hello pour une règle doit être unique dans chaque jeu. Chaque règle possède des propriétés relatives au protocole, aux plages de ports de destination et source, aux préfixes d’adresse, à la direction du trafic, à la priorité et au type d’accès. 

Tous les groupes de ressources réseau contiennent un ensemble de règles par défaut. les règles par défaut Hello ne peut pas être supprimés, mais comme ils sont affectés de priorité la plus faible de hello, elles peuvent être remplacées par les règles hello que vous créez. 

Lorsque vous associez un tooa du groupe de sécurité réseau NIC, règles d’accès réseau hello hello NSG sont NIC de toothat uniquement appliqué. Si un groupe de sécurité réseau est appliquée tooa carte réseau simple sur une machine virtuelle multi-NIC, cela n’affecte pas le trafic toohello autres cartes réseau. Vous pouvez associer des différents groupes de sécurité réseau tooa carte réseau (ou machine virtuelle, en fonction du modèle de déploiement hello) et hello sous-réseau lié à une carte réseau ou une machine virtuelle. Priorité en fonction de direction hello du trafic.

Veillez trop[plan](../../virtual-network/virtual-networks-nsg.md#planning) vos groupes de sécurité réseau lorsque vous planifiez vos machines virtuelles et le réseau virtuel.

Ce tableau répertorie les méthodes hello que vous pouvez utiliser toocreate un groupe de sécurité réseau.

| Méthode | Description |
| ------ | ----------- |
| [Portail Azure](../../virtual-network/virtual-networks-create-nsg-arm-pportal.md) | Lorsque vous créez une machine virtuelle dans hello portail Azure, un groupe de sécurité réseau est automatiquement créé et associé toohello NIC hello portail crée. nom de Hello Hello groupe de sécurité réseau est une combinaison du nom hello Hello VM et **- groupe de sécurité réseau**. Ce groupe de sécurité réseau contient une règle de trafic entrant avec une priorité 1000, service ensemble tooRDP hello protocole ensemble tooTCP, port défini too3389 et action définie tooAllow. Si vous souhaitez tooallow n’importe quel autre toohello le trafic entrant machine virtuelle, vous devez ajouter des règles supplémentaires toohello groupe de sécurité réseau. |
| [Azure PowerShell](../../virtual-network/virtual-networks-create-nsg-arm-ps.md) | Utilisez [New-AzureRmNetworkSecurityRuleConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmNetworkSecurityRuleConfig) et fournissent des informations de règle hello requis. Utilisez [New-AzureRmNetworkSecurityGroup](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmNetworkSecurityGroup) toocreate hello groupe de sécurité réseau. Utilisez [Set-AzureRmVirtualNetworkSubnetConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/Set-AzureRmVirtualNetworkSubnetConfig) tooconfigure hello groupe de sécurité réseau pour le sous-réseau de hello. Utilisez [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork) tooadd hello NSG toohello réseau virtuel. |
| [Interface de ligne de commande Azure](../../virtual-network/virtual-networks-create-nsg-arm-cli.md) | Utilisez [az réseau nsg créer](https://docs.microsoft.com/cli/azure/network/nsg#create) tooinitially créer hello groupe de sécurité réseau. Utilisez [créer de règle de groupe de sécurité réseau du réseau az](https://docs.microsoft.com/cli/azure/network/nsg/rule#create) tooadd règles toohello groupe de sécurité réseau. Utilisez [mise à jour de sous-réseau de réseau virtuel az réseau](https://docs.microsoft.com/en-us/cli/azure/network/vnet/subnet#update) sous-réseau de toohello tooadd hello groupe de sécurité réseau. |
| [Modèle](../../virtual-network/virtual-networks-create-nsg-arm-template.md) | Utilisez [Create a Network Security Group](https://github.com/Azure/azure-quickstart-templates/tree/master/101-security-group-create) comme guide pour le déploiement d’un groupe de sécurité réseau à l’aide d’un modèle. |

## <a name="load-balancers"></a>Équilibreurs de charge

[Équilibrage de charge Azure](../../load-balancer/load-balancer-overview.md) offre une haute disponibilité et les performances réseau tooyour applications. Un équilibreur de charge peut être configuré trop[équilibrer le trafic Internet entrant](../../load-balancer/load-balancer-internet-overview.md) tooVMs ou [équilibrer le trafic entre les machines virtuelles dans un réseau virtuel](../../load-balancer/load-balancer-internal-overview.md). Un équilibreur de charge peut également équilibrer le trafic entre les ordinateurs locaux et les machines virtuelles dans un réseau entre différents locaux, ou transférer le trafic externe tooa ordinateur virtuel spécifique.

Hello charge équilibrage cartes de trafic entrant et sortant entre hello publique adresse IP et le port sur l’équilibrage de charge hello et l’adresse IP privée de hello et le port de hello machine virtuelle.

Lorsque vous créez un équilibrage de charge, vous devez également prendre en compte les éléments de configuration suivants :

- **Configuration d’une adresse IP frontale** : un équilibrage de charge peut inclure une ou plusieurs adresses IP frontales, également appelées « adresses IP virtuelles ». Ces adresses IP servent d’entrée pour le trafic de hello.
- **Pool d’adresses de serveur principal** – adresses IP qui sont associés à hello NIC toowhich de charge est distribuée.
- **Les règles NAT** -définit le trafic entrant comment parcourt IP frontale de hello et distribués toohello principal IP.
- **Règles d’équilibrage de charge** -mappe un IP frontal spécifié et port combinaison tooa des adresses IP de serveur principal et la combinaison de port. Un même équilibreur de charge peut avoir plusieurs règles d’équilibrage de charge. Chaque règle est une combinaison d’une adresse IP et d’un port frontaux et d’une adresse IP et d’un port principaux associés aux machines virtuelles.
- **[Sondes](../../load-balancer/load-balancer-custom-probe-overview.md)**  -analyses hello intégrité des machines virtuelles. Lorsqu’une sonde échoue toorespond, équilibrage de charge hello cesse d’envoyer les nouvelles connexions toohello VM défectueux. les connexions existantes Hello ne sont pas affectées, et les nouvelles connexions sont envoyées les machines virtuelles de toohealthy.

Ce tableau répertorie les méthodes hello que vous pouvez utiliser toocreate un équilibrage de charge du côté internet.

| Méthode | Description |
| ------ | ----------- |
| Portail Azure | Impossible de créer actuellement un équilibrage de charge d’exposés à internet à l’aide de hello portail Azure. |
| [Azure PowerShell](../../load-balancer/load-balancer-get-started-internet-arm-ps.md) | identificateur de hello tooprovide de l’adresse IP publique hello d’adresses que vous avez créé précédemment, utilisez [New-AzureRmLoadBalancerFrontendIpConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerFrontendIpConfig) avec hello **- adresse IP publique** paramètre. Utilisez [New-AzureRmLoadBalancerBackendAddressPoolConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerBackendAddressPoolConfig) configuration de hello toocreate hello back-end du pool d’adresses. Utilisez [New-AzureRmLoadBalancerInboundNatRuleConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerInboundNatRuleConfig) toocreate entrant de configuration IP frontale hello que vous avez créé les règles NAT. Utilisez [New-AzureRmLoadBalancerProbeConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerProbeConfig) toocreate hello sondes que vous avez besoin. Utilisez [New-AzureRmLoadBalancerRuleConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerRuleConfig) configuration d’équilibrage de charge toocreate hello. Utilisez [New-AzureRmLoadBalancer](/powershell/module/azurerm.network/new-azurermloadbalancer) équilibrage de charge toocreate hello.|
| [Interface de ligne de commande Azure](../../load-balancer/load-balancer-get-started-internet-arm-cli.md) | Utilisez [créer d’équilibrage de charge réseau az](https://docs.microsoft.com/cli/azure/network/lb#create) configuration d’équilibrage de charge initiale toocreate hello. Utilisez [az lb frontal-adresse ip de réseau créer](https://docs.microsoft.com/cli/azure/network/lb/frontend-ip#create) tooadd hello adresse IP publique que vous avez créé précédemment. Utilisez [az lb-pool d’adresses réseau créer](https://docs.microsoft.com/cli/azure/network/lb/address-pool#create) configuration de hello tooadd hello back-end du pool d’adresses. Utilisez [az réseau lb--règle de nat entrant créer](https://docs.microsoft.com/cli/azure/network/lb/inbound-nat-rule#create) tooadd les règles NAT. Utilisez [créer de règle d’équilibrage de charge réseau az](https://docs.microsoft.com/cli/azure/network/lb/rule#create) règles d’équilibrage de charge tooadd hello. Utilisez [sonde d’équilibrage de charge réseau az créer](https://docs.microsoft.com/cli/azure/network/lb/probe#create) tooadd hello sondes. |
| [Modèle](../../load-balancer/load-balancer-get-started-internet-arm-template.md) | Utilisez [2 machines virtuelles dans un équilibreur de charge et configurer des règles NAT sur hello LB](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-loadbalancer-natrules) comme guide pour déployer un équilibreur de charge à l’aide d’un modèle. |
    
Ce tableau répertorie les méthodes hello que vous pouvez utiliser toocreate un équilibreur de charge interne.

| Méthode | Description |
| ------ | ----------- |
| Portail Azure | Impossible de créer actuellement un équilibreur de charge interne à l’aide de hello portail Azure. |
| [Azure PowerShell](../../load-balancer/load-balancer-get-started-ilb-arm-ps.md) | tooprovide une adresse IP privée dans le sous-réseau de réseau hello, utilisez [New-AzureRmLoadBalancerFrontendIpConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerFrontendIpConfig) avec hello **- une adresse IP privée** paramètre. Utilisez [New-AzureRmLoadBalancerBackendAddressPoolConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerBackendAddressPoolConfig) configuration de hello toocreate hello back-end du pool d’adresses. Utilisez [New-AzureRmLoadBalancerInboundNatRuleConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerInboundNatRuleConfig) toocreate entrant de configuration IP frontale hello que vous avez créé les règles NAT. Utilisez [New-AzureRmLoadBalancerProbeConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerProbeConfig) toocreate hello sondes que vous avez besoin. Utilisez [New-AzureRmLoadBalancerRuleConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerRuleConfig) configuration d’équilibrage de charge toocreate hello. Utilisez [New-AzureRmLoadBalancer](/powershell/module/azurerm.network/new-azurermloadbalancer) équilibrage de charge toocreate hello.|
| [Interface de ligne de commande Azure](../../load-balancer/load-balancer-get-started-ilb-arm-cli.md) | Hello d’utilisation [créer d’équilibrage de charge réseau az](https://docs.microsoft.com/cli/azure/network/lb#create) configuration d’équilibrage de charge initiale commande toocreate hello. toodefine hello adresse IP privée, utilisez [az lb frontal-adresse ip de réseau créer](https://docs.microsoft.com/cli/azure/network/lb/frontend-ip#create) avec hello **--adresse ip privée** paramètre. Utilisez [az lb-pool d’adresses réseau créer](https://docs.microsoft.com/cli/azure/network/lb/address-pool#create) configuration de hello tooadd hello back-end du pool d’adresses. Utilisez [az réseau lb--règle de nat entrant créer](https://docs.microsoft.com/cli/azure/network/lb/inbound-nat-rule#create) tooadd les règles NAT. Utilisez [créer de règle d’équilibrage de charge réseau az](https://docs.microsoft.com/cli/azure/network/lb/rule#create) règles d’équilibrage de charge tooadd hello. Utilisez [sonde d’équilibrage de charge réseau az créer](https://docs.microsoft.com/cli/azure/network/lb/probe#create) tooadd hello sondes.|
| [Modèle](../../load-balancer/load-balancer-get-started-ilb-arm-template.md) | Utilisez [2 machines virtuelles dans un équilibreur de charge et configurer des règles NAT sur hello LB](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-internal-load-balancer) comme guide pour déployer un équilibreur de charge à l’aide d’un modèle. |

## <a name="vms"></a>Machines virtuelles

Machines virtuelles peuvent être créés dans hello même réseau virtuel et ils peuvent se connecter tooeach autres adresses IP privée. Ils peuvent se connecter même s’ils se trouvent dans des sous-réseaux différents sans hello besoin tooconfigure une passerelle ou utilisent des adresses IP publiques. tooput machines virtuelles dans un réseau virtuel, vous créez hello réseau virtuel, puis que vous créez chaque machine virtuelle, vous affectez toohello réseau virtuel et le sous-réseau. Les machines virtuelles acquièrent leurs paramètres réseau lors du déploiement ou du démarrage.  

Les machines virtuelles sont attribuées à une adresse IP lorsqu’elles sont déployées. Si vous déployez plusieurs machines virtuelles dans un réseau virtuel ou un sous-réseau, des adresses IP leur sont attribuées lorsqu’elles démarrent. Une adresse IP dynamique (DIP) est l’adresse IP interne hello associé à une machine virtuelle. Vous pouvez allouer un tooa adresse DIP statique machine virtuelle. Si vous allouez une adresse DIP statique, vous devez envisager d’utiliser un tooavoid de sous-réseau spécifique accidentellement réutilisation d’une adresse DIP statique pour une autre machine virtuelle.  

Si vous créez une machine virtuelle et que vous voulez toomigrate il dans un réseau virtuel, il n’est pas une modification de configuration simple. Vous devez redéployer la machine virtuelle de hello en hello réseau virtuel. tooredeploy de façon plus simple de Hello est toodelete hello machine virtuelle, mais pas les disques attachés tooit et puis recréer hello machine virtuelle à l’aide de hello disques hello réseau virtuel d’origine. 

Ce tableau répertorie les méthodes hello que vous pouvez utiliser toocreate une machine virtuelle dans un réseau virtuel.

| Méthode | Description |
| ------ | ----------- |
| [Portail Azure](../virtual-machines-windows-hero-tutorial.md) | Paramètres de réseau utilise hello par défaut qui ont été précédemment mentionné toocreate une machine virtuelle avec une seule carte toocreate une machine virtuelle avec plusieurs cartes réseau, vous devez utiliser une autre méthode. |
| [Azure PowerShell](../virtual-machines-windows-ps-create.md) | Inclut notamment hello [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface) tooadd hello carte réseau que vous avez créé précédemment toohello configuration d’ordinateur virtuel. |
| [Modèle](ps-template.md) | Utilisez [Very simple deployment of a Windows VM](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows) comme guide pour le déploiement d’une machine virtuelle à l’aide d’un modèle. |

## <a name="next-steps"></a>Étapes suivantes

- Découvrez comment tooconfigure [itinéraires définis par l’utilisateur et le transfert IP](../../virtual-network/virtual-networks-udr-overview.md). 
- Découvrez comment tooconfigure [les connexions de réseau virtuel tooVNet](../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md).
- Découvrez comment trop[résoudre les itinéraires](../../virtual-network/virtual-network-routes-troubleshoot-portal.md).
