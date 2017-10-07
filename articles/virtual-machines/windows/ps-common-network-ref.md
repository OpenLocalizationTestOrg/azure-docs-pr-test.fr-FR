---
title: "aaaCommon PowerShell des commandes pour les réseaux virtuels Azure | Documents Microsoft"
description: "Tooget de commandes PowerShell courants que vous aider à créer un réseau virtuel et ses ressources associées pour les machines virtuelles."
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 56e1a73c-8299-4996-bd03-f74585caa1dc
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: davidmu
ms.openlocfilehash: b46b78f1b7c5a0c5ba917fb48f568d871e5e8789
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="common-powershell-commands-for-azure-virtual-networks"></a>Commandes PowerShell courantes pour les réseaux virtuels Azure

Si vous souhaitez toocreate une machine virtuelle, vous devez toocreate une [réseau virtuel](../../virtual-network/virtual-networks-overview.md) ou savoir sur un réseau virtuel existant dans le hello machine virtuelle peut être ajouté. En règle générale, lorsque vous créez une machine virtuelle, vous devez également tooconsider création de ressources hello décrits dans cet article.

Consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview) pour plus d’informations sur l’installation hello dernière version de Azure PowerShell, en sélectionnant votre abonnement et l’ouverture de session tooyour compte.

Certaines variables peuvent être utiles si plusieurs commandes hello en cours d’exécution dans cet article :

- $location - emplacement hello hello des ressources du réseau. Vous pouvez utiliser [Get-AzureRmLocation](https://docs.microsoft.com/powershell/module/azurerm.resources/get-azurermlocation) toofind un [région géographique](https://azure.microsoft.com/regions/) qui vous convient.
- $myResourceGroup - nom hello hello du groupe de ressources dans lequel se trouvent les ressources du réseau hello.

## <a name="create-network-resources"></a>Créer des ressources réseau

| Task | Commande |
| ---- | ------- |
| Créez des configurations de sous-réseau |$subnet1 = [New-AzureRmVirtualNetworkSubnetConfig](https://docs.microsoft.com/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) -Name "mySubnet1" -AddressPrefix XX.X.X.X/XX<BR>$subnet2 = New-AzureRmVirtualNetworkSubnetConfig -Name "mySubnet2" -AddressPrefix XX.X.X.X/XX<BR><BR>Un réseau classique peut avoir un sous-réseau pour un [équilibrage de charge accessible sur Internet](../../load-balancer/load-balancer-internet-overview.md) et un sous-réseau distinct pour un [équilibrage de charge interne](../../load-balancer/load-balancer-internal-overview.md). |
| Créez un réseau virtuel |$vnet = [New-AzureRmVirtualNetwork](https://docs.microsoft.com/powershell/module/azurerm.network/new-azurermvirtualnetwork) -Name "myVNet" -ResourceGroupName $myResourceGroup -Location $location -AddressPrefix XX.X.X.X/XX -Subnet $subnet1, $subnet2 |
| Test d’un nom de domaine unique |[Test-AzureRmDnsAvailability](https://docs.microsoft.com/powershell/module/azurerm.network/test-azurermdnsavailability) -DomainNameLabel "myDNS" -Location $location<BR><BR>Vous pouvez spécifier un nom de domaine DNS pour un [ressource IP publique](../../virtual-network/virtual-network-ip-addresses-overview-arm.md), ce qui crée un mappage pour l’adresse IP publique de domainname.location.cloudapp.azure.com toohello Bonjour serveurs gérés par Azure. nom de Hello peut contenir uniquement des lettres, des chiffres et des traits d’union. Hello premier et dernier caractères doivent être une lettre ou un chiffre et le nom de domaine hello doit être unique dans son emplacement Azure. Si la valeur **True** est renvoyée, cela signifie que le nom proposé est bien unique au niveau global. |
| Créer une adresse IP publique |$pip = [New-AzureRmPublicIpAddress](https://docs.microsoft.com/powershell/module/azurerm.network/new-azurermpublicipaddress) -Name "myPublicIp" -ResourceGroupName $myResourceGroup -DomainNameLabel "myDNS" -Location $location -AllocationMethod Dynamic<BR><BR>adresse IP publique de Hello utilise le nom de domaine hello précédemment testé et est utilisé par la configuration de serveur frontal hello d’équilibrage de charge hello. |
| Créer une configuration d’adresse IP frontale |$frontendIP = [New-AzureRmLoadBalancerFrontendIpConfig](https://docs.microsoft.com/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig) -Name "myFrontendIP" -PublicIpAddress $pip<BR><BR>configuration de serveur frontal Hello comprend hello l’adresse IP publique que vous avez créé précédemment pour le trafic réseau entrant. |
| Créer un pool d’adresses principal |$beAddressPool = [New-AzureRmLoadBalancerBackendAddressPoolConfig](https://docs.microsoft.com/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig) -Name "myBackendAddressPool"<BR><BR>Fournit les adresses internes pour principal hello Hello chargement équilibrage sont accessibles via une interface réseau. |
| Créer une sonde |$healthProbe = [New-AzureRmLoadBalancerProbeConfig](https://docs.microsoft.com/powershell/module/azurerm.network/new-azurermloadbalancerprobeconfig) -Name "myProbe" -RequestPath 'HealthProbe.aspx' -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2<BR><BR>Contient le contrôle d’intégrité les sondes utilisées toocheck disponibilité des instances de machines virtuelles dans le pool d’adresses principales hello. |
| Créer une règle d’équilibrage de charge |$lbRule = [New-AzureRmLoadBalancerRuleConfig](https://docs.microsoft.com/powershell/module/azurerm.network/new-azurermloadbalancerruleconfig) -Name HTTP -FrontendIpConfiguration $frontendIP -BackendAddressPool $beAddressPool -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 80<BR><BR>Contient des règles pour affecter un port public sur l’équilibrage de charge hello port tooa dans le pool d’adresses principales hello. |
| Créer une règle NAT entrante |$inboundNATRule = [New-AzureRmLoadBalancerInboundNatRuleConfig](https://docs.microsoft.com/powershell/module/azurerm.network/new-azurermloadbalancerinboundnatruleconfig) -Name "myInboundRule1" -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3441 -BackendPort 3389<BR><BR>Contient des règles de mappage d’un port public sur le port de tooa d’équilibrage de charge de hello pour un ordinateur virtuel spécifique dans le pool d’adresses principales hello. |
| Créer un équilibrage de charge |$loadBalancer = [New-AzureRmLoadBalancer](https://docs.microsoft.com/powershell/module/azurerm.network/new-azurermloadbalancer) -ResourceGroupName $myResourceGroup -Name "myLoadBalancer" -Location $location -FrontendIpConfiguration $frontendIP -InboundNatRule $inboundNATRule -LoadBalancingRule $lbRule -BackendAddressPool $beAddressPool -Probe $healthProbe |
| Créer une interface réseau |$nic1= [New-AzureRmNetworkInterface](https://docs.microsoft.com/powershell/module/azurerm.network/new-azurermnetworkinterface) -ResourceGroupName $myResourceGroup -Name "myNIC" -Location $location -PrivateIpAddress XX.X.X.X -Subnet $subnet2 -LoadBalancerBackendAddressPool $loadBalancer.BackendAddressPools[0] -LoadBalancerInboundNatRule $loadBalancer.InboundNatRules[0]<BR><BR>Créer une interface réseau à l’aide d’adresse IP publique de hello et le sous-réseau de réseau virtuel que vous avez créé précédemment. |

## <a name="get-information-about-network-resources"></a>Obtenir des informations sur les ressources réseau

| Task | Commande |
| ---- | ------- |
| Répertorier les réseaux virtuels |[Get-AzureRmVirtualNetwork](https://docs.microsoft.com/powershell/module/azurerm.network/get-azurermvirtualnetwork) -ResourceGroupName $myResourceGroup<BR><BR>Répertorie tous les réseaux virtuels hello dans le groupe de ressources hello. |
| Obtenir des informations sur un réseau virtuel |Get-AzureRmVirtualNetwork -Name "myVNet" -ResourceGroupName $myResourceGroup |
| Répertorier les sous-réseaux d’un réseau virtuel |Get-AzureRmVirtualNetwork -Name "myVNet" -ResourceGroupName $myResourceGroup &#124; Select Subnets |
| Obtenir des informations sur un sous-réseau |[Get-AzureRmVirtualNetworkSubnetConfig](https://docs.microsoft.com/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) -Name "mySubnet1" -VirtualNetwork $vnet<BR><BR>Obtient les informations de sous-réseau de hello dans le réseau virtuel spécifié de hello. valeur de Hello $vnet représente un objet hello retourné par Get-AzureRmVirtualNetwork. |
| Répertorier des adresses IP |[Get-AzureRmPublicIpAddress](https://docs.microsoft.com/powershell/module/azurerm.network/get-azurermpublicipaddress) -ResourceGroupName $myResourceGroup<BR><BR>Répertorie les adresses IP publiques hello dans le groupe de ressources hello. |
| Répertorier les équilibrages de charge |[Get-AzureRmLoadBalancer](https://docs.microsoft.com/powershell/module/azurerm.network/get-azurermloadbalancer) -ResourceGroupName $myResourceGroup<BR><BR>Répertorie tous les équilibrages de charge hello dans le groupe de ressources hello. |
| Répertorier les interfaces réseau |[Get-AzureRmNetworkInterface](https://docs.microsoft.com/powershell/module/azurerm.network/get-azurermnetworkinterface) -ResourceGroupName $myResourceGroup<BR><BR>Répertorie toutes les interfaces réseau de hello dans le groupe de ressources hello. |
| Obtenir des informations sur une interface réseau |Get-AzureRmNetworkInterface -Name "myNIC" -ResourceGroupName $myResourceGroup<BR><BR>Obtient des informations sur une interface réseau spécifique. |
| Obtenir la configuration IP de hello d’une interface réseau |[Get-AzureRmNetworkInterfaceIPConfig](https://docs.microsoft.com/powershell/module/azurerm.network/get-azurermnetworkinterfaceipconfig) -Name "myNICIP" -NetworkInterface $nic<BR><BR>Obtient des informations sur la configuration IP de hello d’interface réseau spécifiée de hello. valeur de Hello $nic représente un objet hello retourné par Get-AzureRmNetworkInterface. |

## <a name="manage-network-resources"></a>Gérer des ressources réseau

| Task | Commande |
| ---- | ------- |
| Ajouter un réseau virtuel tooa de sous-réseau |[Add-AzureRmVirtualNetworkSubnetConfig](https://docs.microsoft.com/powershell/module/azurerm.network/add-azurermvirtualnetworksubnetconfig) -AddressPrefix XX.X.X.X/XX -Name "mySubnet1" -VirtualNetwork $vnet<BR><BR>Ajoute un réseau virtuel existant sous-réseau tooan. valeur de Hello $vnet représente un objet hello retourné par Get-AzureRmVirtualNetwork. |
| Supprimer un réseau virtuel |[Remove-AzureRmVirtualNetwork](https://docs.microsoft.com/powershell/module/azurerm.network/remove-azurermvirtualnetwork) -Name "myVNet" -ResourceGroupName $myResourceGroup<BR><BR>Supprime le réseau virtuel spécifié de hello du groupe de ressources hello. |
| Supprimer une interface réseau |[Remove-AzureRmNetworkInterface](https://docs.microsoft.com/powershell/module/azurerm.network/remove-azurermnetworkinterface) -Name "myNIC" -ResourceGroupName $myResourceGroup<BR><BR>Supprime l’interface réseau spécifiée de hello du groupe de ressources hello. |
| Suppression d’un équilibreur de charge |[Remove-AzureRmLoadBalancer](https://docs.microsoft.com/powershell/module/azurerm.network/remove-azurermloadbalancer) -Name "myLoadBalancer" -ResourceGroupName $myResourceGroup<BR><BR>Supprime hello spécifié d’équilibrage de charge du groupe de ressources hello. |
| Supprimer une adresse IP publique |[Remove-AzureRmPublicIpAddress](https://docs.microsoft.com/powershell/module/azurerm.network/remove-azurermpublicipaddress)-Name "myIPAddress" -ResourceGroupName $myResourceGroup<BR><BR>Supprime hello spécifié une adresse IP publique du groupe de ressources hello. |

## <a name="next-steps"></a>Étapes suivantes
* Utilisez hello network interface que vous venez créée lorsque vous [créer une machine virtuelle](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* Découvrez comment [créer une machine virtuelle avec plusieurs interfaces réseau](../../virtual-network/virtual-networks-multiple-nics.md).

