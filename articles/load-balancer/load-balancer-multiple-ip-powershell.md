---
title: "aaaLoad équilibrage sur plusieurs configurations IP dans Azure | Documents Microsoft"
description: "Équilibrage de charge sur des configurations IP principales et secondaires."
services: load-balancer
documentationcenter: na
author: anavinahar
manager: narayan
editor: na
ms.assetid: 244907cd-b275-4494-aaf7-dcfc4d93edfe
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/16/2017
ms.author: annahar
ms.openlocfilehash: fe1cdb317350942ff759229491c2025e98dd24a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="load-balancing-on-multiple-ip-configurations-using-powershell"></a>Équilibrage de charge sur plusieurs configurations IP avec PowerShell

> [!div class="op_single_selector"]
> * [Portail](load-balancer-multiple-ip.md)
> * [INTERFACE DE LIGNE DE COMMANDE](load-balancer-multiple-ip-cli.md)
> * [PowerShell](load-balancer-multiple-ip-powershell.md)

Cet article décrit comment toouse équilibrage de charge Azure avec adresse IP de plusieurs adresses sur une interface réseau secondaire (NIC). Avec ce scénario, nous disposons de deux machines virtuelles exécutant Windows, chacune avec une carte réseau principale et secondaire. Chacun des hello secondaire cartes réseau ont deux configurations IP. Chaque machine virtuelle héberge les deux sites web contoso.com et fabrikam.com. Chaque site Web est lié tooone de configurations IP hello hello seconde. Nous utilisons équilibrage de charge Azure tooexpose deux frontal adresses IP, une pour chaque site Web, toodistribute toohello respectifs IP configuration du trafic pour le site Web de hello. Ce scénario utilise hello même numéro de port entre les serveurs frontaux, ainsi que les deux adresses IP du pool principal.

![Image du scénario LB](./media/load-balancer-multiple-ip/lb-multi-ip.PNG)

## <a name="steps-tooload-balance-on-multiple-ip-configurations"></a>Solde de tooload étapes sur plusieurs configurations IP

Suivez les étapes de hello ci-dessous le scénario de hello tooachieve présentée dans cet article :

1. Installez Azure PowerShell. Consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview) pour plus d’informations sur l’installation hello dernière version de Azure PowerShell, en sélectionnant votre abonnement et l’ouverture de session tooyour compte.
2. Créer un groupe de ressources à l’aide de hello suivant les paramètres :

    ```powershell
    $location = "westcentralus".
    $myResourceGroup = "contosofabrikam"
    ```

    Pour plus d’informations, voir l’Étape 2 de [Créer un groupe de ressources](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).

3. [Créer un groupe à haute disponibilité](../virtual-machines/windows/tutorial-availability-sets.md?toc=%2fazure%2fload-balancer%2ftoc.json) toocontain vos machines virtuelles. Pour ce scénario, utilisez hello de commande suivante :

    ```powershell
    New-AzureRmAvailabilitySet -ResourceGroupName "contosofabrikam" -Name "myAvailset" -Location "West Central US"
    ```

4. Suivez les instructions étapes 3 à 5 de [créer une machine virtuelle Windows](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json) création de hello tooprepare d’une machine virtuelle avec une carte réseau. unique de l’article Exécuter une étape 6.1, suivant et servez-vous hello au lieu de l’étape 6.2 :

    ```powershell
    $availset = Get-AzureRmAvailabilitySet -ResourceGroupName "contosofabrikam" -Name "myAvailset"
    New-AzureRmVMConfig -VMName "VM1" -VMSize "Standard_DS1_v2" -AvailabilitySetId $availset.Id
    ```

    Accomplissez ensuite les étapes 6.3 à 6.8 de l’article [Créer une machine virtuelle Windows](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).

5. Ajoutez un deuxième tooeach de configuration IP de hello machines virtuelles. Suivez les instructions de hello dans [affecter plusieurs adresses IP toovirtual machines](../virtual-network/virtual-network-multiple-ip-addresses-powershell.md#add) l’article. Utilisez hello suivant les paramètres de configuration :

    ```powershell
    $NicName = "VM1-NIC2"
    $RgName = "contosofabrikam"
    $NicLocation = "West Central US"
    $IPConfigName4 = "VM1-ipconfig2"
    $Subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "mySubnet" -VirtualNetwork $myVnet
    ```

    Il est inutile tooassociate hello secondaire configurations IP avec des adresses IP publiques à des fins de hello de ce didacticiel. Modifier la partie d’association hello commande tooremove hello publique IP.

6. Exécutez à nouveau les étapes 4 à 6 de cet article pour la machine virtuelle VM2. Être tooVM2 de nom de machine virtuelle de hello tooreplace que lors de cette opération. Notez que vous n’avez pas besoin toocreate un réseau virtuel pour hello deuxième machine virtuelle. Vous pouvez ou non créer un sous-réseau, selon votre cas d’utilisation.

7. Créez deux adresses IP publiques et les stocker dans les variables appropriées hello comme indiqué :

    ```powershell
    $publicIP1 = New-AzureRmPublicIpAddress -Name PublicIp1 -ResourceGroupName contosofabrikam -Location 'West Central US' -AllocationMethod Dynamic -DomainNameLabel contoso
    $publicIP2 = New-AzureRmPublicIpAddress -Name PublicIp2 -ResourceGroupName contosofabrikam -Location 'West Central US' -AllocationMethod Dynamic -DomainNameLabel fabrikam

    $publicIP1 = Get-AzureRmPublicIpAddress -Name PublicIp1 -ResourceGroupName contosofabrikam
    $publicIP2 = Get-AzureRmPublicIpAddress -Name PublicIp2 -ResourceGroupName contosofabrikam
    ```

8. Créez deux configurations IP frontales :

    ```powershell
    $frontendIP1 = New-AzureRmLoadBalancerFrontendIpConfig -Name contosofe -PublicIpAddress $publicIP1
    $frontendIP2 = New-AzureRmLoadBalancerFrontendIpConfig -Name fabrikamfe -PublicIpAddress $publicIP2
    ```

9. Créer vos pools d’adresses principaux, une sonde et vos règles d’équilibrage de charge :

    ```powershell
    $beaddresspool1 = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name contosopool
    $beaddresspool2 = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name fabrikampool

    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name HTTP -RequestPath 'index.html' -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2

    $lbrule1 = New-AzureRmLoadBalancerRuleConfig -Name HTTPc -FrontendIpConfiguration $frontendIP1 -BackendAddressPool $beaddresspool1 -Probe $healthprobe -Protocol Tcp -FrontendPort 80 -BackendPort 80
    $lbrule2 = New-AzureRmLoadBalancerRuleConfig -Name HTTPf -FrontendIpConfiguration $frontendIP2 -BackendAddressPool $beaddresspool2 -Probe $healthprobe -Protocol Tcp -FrontendPort 80 -BackendPort 80
    ```

10. Une fois les ressources créées, créez votre équilibreur de charge :

    ```powershell
    $mylb = New-AzureRmLoadBalancer -ResourceGroupName contosofabrikam -Name mylb -Location 'West Central US' -FrontendIpConfiguration $frontendIP1 -LoadBalancingRule $lbrule -BackendAddressPool $beAddressPool -Probe $healthProbe
    ```

11. Ajouter hello deuxième principal adresse serveur frontal et pool IP configuration tooyour nouvellement créé équilibrage de charge :

    ```powershell
    $mylb = Get-AzureRmLoadBalancer -Name "mylb" -ResourceGroupName $myResourceGroup | Add-AzureRmLoadBalancerBackendAddressPoolConfig -Name fabrikampool | Set-AzureRmLoadBalancer

    $mylb | Add-AzureRmLoadBalancerFrontendIpConfig -Name fabrikamfe -PublicIpAddress $publicIP2 | Set-AzureRmLoadBalancer
    
    Add-AzureRmLoadBalancerRuleConfig -Name HTTP -LoadBalancer $mylb -FrontendIpConfiguration $frontendIP2 -BackendAddressPool $beaddresspool2 -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 80 | Set-AzureRmLoadBalancer
    ```

12. commandes Hello ci-dessous obtenir hello cartes d’interface réseau, puis ajoutez que les deux configurations IP de chaque pool d’adresses principales du secondaire NIC toohello Hello l’équilibrage de charge :

    ```powershell
    $nic1 = Get-AzureRmNetworkInterface -Name "VM1-NIC2" -ResourceGroupName "MyResourcegroup";
    $nic2 = Get-AzureRmNetworkInterface -Name "VM2-NIC2" -ResourceGroupName "MyResourcegroup";

    $nic1.IpConfigurations[0].LoadBalancerBackendAddressPools.Add($mylb.BackendAddressPools[0]);
    $nic1.IpConfigurations[1].LoadBalancerBackendAddressPools.Add($mylb.BackendAddressPools[1]);
    $nic2.IpConfigurations[0].LoadBalancerBackendAddressPools.Add($mylb.BackendAddressPools[0]);
    $nic2.IpConfigurations[1].LoadBalancerBackendAddressPools.Add($mylb.BackendAddressPools[1]);

    $mylb = $mylb | Set-AzureRmLoadBalancer

    $nic1 | Set-AzureRmNetworkInterface
    $nic2 | Set-AzureRmNetworkInterface
    ```

13. Enfin, vous devez configurer DNS ressource enregistrements toopoint toohello respectifs adresse IP frontale de hello équilibrage de charge. Vous pouvez héberger vos domaines dans Azure DNS. Pour plus d’informations sur l’utilisation d’Azure DNS avec un équilibrage de charge, voir [Utiliser Azure DNS avec d’autres services Azure](../dns/dns-for-azure-services.md).

## <a name="next-steps"></a>Étapes suivantes
- En savoir plus sur le fonctionnement des services de l’équilibrage de charge toocombine dans Azure dans [à l’aide des services d’équilibrage de charge dans Azure](../traffic-manager/traffic-manager-load-balancing-azure.md).
- Découvrez comment vous pouvez utiliser différents types de journaux dans Azure toomanage et résoudre les problèmes d’équilibrage de charge dans [journal analytique pour l’équilibrage de charge Azure](../load-balancer/load-balancer-monitor-log.md).
