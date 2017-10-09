---
title: "équilibrage de charge aaaConfigure pour SQL always on | Documents Microsoft"
description: "Configurer toowork d’équilibrage de charge avec SQL toujours sur et comment tooleverage powershell toocreate l’équilibrage de charge pour l’implémentation de SQL hello"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
ms.assetid: d7bc3790-47d3-4e95-887c-c533011e4afd
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: ac6200b18f725dadee2555b80055327d379417d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-load-balancer-for-sql-always-on"></a>Configuration de l'équilibrage de charge pour SQL Always On

Les groupes de disponibilité Always On de SQL Server peuvent maintenant être exécutés avec l’équilibrage de charge interne (ILB). Le groupe de disponibilité constitue la solution phare de SQL Server pour une haute disponibilité et la récupération d’urgence. Hello écouteur du groupe de disponibilité permet aux applications clientes tooseamlessly connecter toohello réplica principal, quel que soit le nombre de hello de réplicas hello dans la configuration de hello.

nom de l’écouteur (DNS) Hello est adresse tooa mappé avec équilibrage de charge et équilibrage de charge de Azure dirige le serveur principal de hello entrants trafic tooonly hello dans le jeu de réplicas hello.

Vous pouvez utiliser le support de l'équilibrage de charge pour les points de terminaison (écouteur) de SQL Server AlwaysOn. Maintenant, vous contrôlez accessibilité hello d’écouteur de hello et que vous pouvez choisir l’adresse IP de charge équilibrée hello à partir d’un sous-réseau spécifique dans votre réseau virtuel (VNet).

En utilisant l’équilibrage de charge interne sur le port d’écoute hello, hello le point de terminaison SQL server (par exemple, Server = tcp:ListenerName, 1433 ; base de données = DatabaseName) est accessible uniquement par :

* Services et machines virtuelles dans hello même réseau virtuel
* Services et machines virtuelles d’un réseau local connecté
* Services et machines virtuelles de réseaux virtuels interconnectés

![ILB_SQLAO_NewPic](./media/load-balancer-configure-sqlao/sqlao1.png)

Figure 1 : SQL AlwaysOn configuré avec équilibrage de charge côté Internet

## <a name="add-internal-load-balancer-toohello-service"></a>Ajouter un service de toohello d’équilibrage de charge interne

1. Bonjour l’exemple suivant, nous configure un réseau virtuel qui contient un sous-réseau nommé 'Sous-réseau-1' :

    ```powershell
    Add-AzureInternalLoadBalancer -InternalLoadBalancerName ILB_SQL_AO -SubnetName Subnet-1 -ServiceName SqlSvc
    ```
2. Ajout des points de terminaison avec une charge équilibrée pour l'ILB sur chaque machine virtuelle

    ```powershell
    Get-AzureVM -ServiceName SqlSvc -Name sqlsvc1 | Add-AzureEndpoint -Name "LisEUep" -LBSetName "ILBSet1" -Protocol tcp -LocalPort 1433 -PublicPort 1433 -ProbePort 59999 -ProbeProtocol tcp -ProbeIntervalInSeconds 10 -
    DirectServerReturn $true -InternalLoadBalancerName ILB_SQL_AO | Update-AzureVM

    Get-AzureVM -ServiceName SqlSvc -Name sqlsvc2 | Add-AzureEndpoint -Name "LisEUep" -LBSetName "ILBSet1" -Protocol tcp -LocalPort 1433 -PublicPort 1433 -ProbePort 59999 -ProbeProtocol tcp -ProbeIntervalInSeconds 10 -DirectServerReturn $true -InternalLoadBalancerName ILB_SQL_AO | Update-AzureVM
    ```

    Dans l’exemple hello ci-dessus, vous avez appelé « sqlsvc1 » et « sqlsvc2 » en cours d’exécution de la machine 2 virtuelle dans le cloud de hello de service « Sqlsvc ». Après la création d’hello avec équilibrage de charge interne `DirectServerReturn` commutateur, vous ajoutez des points de terminaison à charge équilibrée toohello équilibrage de charge interne tooallow SQL tooconfigure hello écouteurs de groupes de disponibilité hello de charge.

Pour plus d’informations sur SQL AlwaysOn, voir [Configurer un équilibrage de charge interne pour un groupe de disponibilité AlwaysOn dans Azure](../virtual-machines/windows/sql/virtual-machines-windows-portal-sql-alwayson-int-listener.md).

## <a name="see-also"></a>Voir aussi
[Prise en main de la configuration d’un équilibrage de charge sur Internet](load-balancer-get-started-internet-arm-ps.md)

[Prise en main de la configuration d’un équilibrage de charge interne](load-balancer-get-started-ilb-arm-ps.md)

[Configuration d’un mode de distribution d’équilibrage de charge](load-balancer-distribution-mode.md)

[Configuration des paramètres du délai d’expiration TCP inactif pour votre équilibrage de charge](load-balancer-tcp-idle-timeout.md)
