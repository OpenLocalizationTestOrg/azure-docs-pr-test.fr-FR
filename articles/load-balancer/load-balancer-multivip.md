---
title: aaaMutiple les adresses IP virtuelles pour un service cloud
description: "Vue d’ensemble de plusieurs adresses IP virtuelles et comment tooset plusieurs adresses IP virtuelles sur un service cloud"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
ms.assetid: 85f6d26a-3df5-4b8e-96a1-92b2793b5284
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: b3e0f2b24968cb75a7064484a09ffe94505bb70b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-multiple-vips-for-a-cloud-service"></a>Configuration de plusieurs adresses IP virtuelles pour un service cloud

Vous pouvez accéder à des services cloud Azure sur hello Internet public à l’aide d’une adresse IP fournie par Azure. Cette adresse IP publique est tooas auxquels une adresse IP virtuelle (adresse IP virtuelle), car il est lié toohello Azure l’équilibrage de charge et hello pas les instances de Machine virtuelle (VM) au sein du service de cloud computing hello. Vous pouvez accéder à une instance de machine virtuelle dans un service cloud à l’aide d’une adresse IP virtuelle unique.

Toutefois, il existe des scénarios dans lesquels vous devrez peut-être plusieurs VIP comme un toohello de point d’entrée même service cloud. Par exemple, votre service cloud peut héberger plusieurs sites Web qui nécessitent une connectivité SSL à l’aide du port par défaut 443, hello que chaque site est hébergé pour un autre client ou de client. Dans ce scénario, vous devez toohave une autre adresse IP publique pour chaque site Web. Hello diagramme ci-dessous illustre un hébergement web d’architecture mutualisée classique avec un besoin de certificats SSL multiples sur hello même port public.

![Scénario avec plusieurs adresses IP virtuelles SSL](./media/load-balancer-multivip/Figure1.png)

Dans l’exemple hello ci-dessus, hello d’utiliser toutes les adresses IP virtuelles même port public (443) et le trafic est redirigé tooone ou plus de charge équilibrée de machines virtuelles sur un seul port privé pour hello adresse IP interne du service de cloud hello qui héberge tous les sites Web de hello.

> [!NOTE]
> Une autre situation nécessitant Bonjour utilisez Bonjour plusieurs adresses IP virtuelles héberge plusieurs écouteurs de groupe de disponibilité AlwaysOn de SQL sur le même ensemble d’ordinateurs virtuels de hello.

Adresses IP virtuelles sont dynamiques par défaut, ce qui signifie que l’adresse IP réelle hello affecté le service de cloud computing toohello peut-être changer au fil du temps. tooprevent que se produise, vous pouvez réserver une adresse IP virtuelle pour votre service. toolearn en savoir plus sur les adresses IP virtuelles réservées, consultez [adresse IP publique réservée](../virtual-network/virtual-networks-reserved-public-ip.md).

> [!NOTE]
> Consultez [Tarification des adresses IP](https://azure.microsoft.com/pricing/details/ip-addresses/) pour plus d’informations sur la tarification des adresses IP virtuelles et réservées.

Vous pouvez utiliser PowerShell tooverify hello utilisés par vos services cloud, les adresses IP virtuelles ainsi ajouter et supprimer des adresses IP virtuelles, associer un point de terminaison tooan VIP et configurer l’équilibrage de charge sur une adresse IP virtuelle spécifique.

## <a name="limitations"></a>Limites

À ce stade, les fonctionnalités des adresses IP virtuelles multiples sont toohello limité les scénarios suivants :

* **IaaS uniquement**. Vous ne pouvez activer les adresses IP virtuelles multiples que pour les services cloud qui contiennent des machines virtuelles. Vous ne pouvez pas utiliser les adresses IP virtuelles multiples dans les scénarios PaaS avec des instances de rôles.
* **PowerShell uniquement**. Vous pouvez gérer les adresses IP virtuelles multiples uniquement à l'aide de PowerShell.

Ces limitations sont temporaires et peuvent changer à tout moment. Modifier la toorevisit que cette page tooverify futures.

## <a name="how-tooadd-a-vip-tooa-cloud-service"></a>Service de cloud tooadd une adresse IP virtuelle tooa
service de tooyour tooadd une adresse IP virtuelle, exécutez hello suivant de commande PowerShell :

```powershell
Add-AzureVirtualIP -VirtualIPName Vip3 -ServiceName myService
```

Cette commande affiche un toohello similaire de résultats suivant l’exemple :

    OperationDescription OperationId                          OperationStatus
    -------------------- -----------                          ---------------
    Add-AzureVirtualIP   4bd7b638-d2e7-216f-ba38-5221233d70ce Succeeded

## <a name="how-tooremove-a-vip-from-a-cloud-service"></a>Comment tooremove une adresse IP virtuelle à partir d’un service cloud
tooremove hello VIP ajouté tooyour service dans l’exemple hello ci-dessus, hello exécution suivant de commande PowerShell :

```powershell
Remove-AzureVirtualIP -VirtualIPName Vip3 -ServiceName myService
```

> [!IMPORTANT]
> Vous ne pouvez supprimer une adresse IP virtuelle que s’il n’a aucun tooit de points de terminaison associés.


## <a name="how-tooretrieve-vip-information-from-a-cloud-service"></a>Comment les informations tooretrieve adresse IP virtuelle à partir d’un Service Cloud
tooretrieve hello adresses IP virtuelles associés à un service cloud, exécutez hello PowerShell script suivant :

```powershell
$deployment = Get-AzureDeployment -ServiceName myService
$deployment.VirtualIPs
```

script de Hello affiche un toohello similaire de résultats suivant l’exemple :

    Address         : 191.238.74.148
    IsDnsProgrammed : True
    Name            : Vip1
    ReservedIPName  :
    ExtensionData   :

    Address         :
    IsDnsProgrammed :
    Name            : Vip2
    ReservedIPName  :
    ExtensionData   :

    Address         :
    IsDnsProgrammed :
    Name            : Vip3
    ReservedIPName  :
    ExtensionData   :

Dans cet exemple, le service de cloud computing hello a 3 VIP :

* **Vip1** est hello l’adresse IP virtuelle par défaut, vous savez que car hello IsDnsProgrammedName a pour valeur tootrue.
* **Vip2** et **Vip3** ne sont pas utilisées étant donné qu’elles n’ont pas d’adresses IP. Ils seront uniquement être utilisés si vous associez une adresse IP virtuelle de toohello point de terminaison.

> [!NOTE]
> Votre abonnement est uniquement facturé pour les adresses IP virtuelles supplémentaires après leur association à un point de terminaison. Pour plus d’informations sur la tarification, voir la page [Tarification des adresses IP](https://azure.microsoft.com/pricing/details/ip-addresses/).

## <a name="how-tooassociate-a-vip-tooan-endpoint"></a>Comment tooassociate une adresse IP virtuelle tooan point de terminaison

tooassociate une adresse IP virtuelle sur un cloud service tooan point de terminaison, exécutez hello suivant de commande PowerShell :

```powershell
Get-AzureVM -ServiceName myService -Name myVM1 |
    Add-AzureEndpoint -Name myEndpoint -Protocol tcp -LocalPort 8080 -PublicPort 80 -VirtualIPName Vip2 |
    Update-AzureVM
```

commande Hello crée un point de terminaison toohello lié VIP appelé *Vip2* sur le port *80*et le lie toohello ordinateur virtuel nommé *myVM1* dans un service cloud nommé  *myService* à l’aide de *TCP* sur le port *8080*.

configuration de hello tooverify, exécutez hello suivant de commande PowerShell :

```powershell
$deployment = Get-AzureDeployment -ServiceName myService
$deployment.VirtualIPs
```

sortie de Hello semble similaire toohello l’exemple suivant :

    Address         : 191.238.74.148
    IsDnsProgrammed : True
    Name            : Vip1
    ReservedIPName  :
    ExtensionData   :

    Address         : 191.238.74.13
    IsDnsProgrammed :
    Name            : Vip2
    ReservedIPName  :
    ExtensionData   :

    Address         :
    IsDnsProgrammed :
    Name            : Vip3
    ReservedIPName  :
    ExtensionData   :

## <a name="how-tooenable-load-balancing-on-a-specific-vip"></a>Comment tooenable l’équilibrage de charge sur une adresse IP virtuelle spécifique

Vous pouvez associer une adresse IP virtuelle unique à plusieurs machines virtuelles à des fins d’équilibrage de charge. Par exemple, supposons que vous avez un service cloud nommé *myService*, et deux machines virtuelles nommées *myVM1* et *myVM2*. Votre service cloud dispose de plusieurs adresses IP virtuelles, dont une nommée *Vip2*. Si vous souhaitez que tout le trafic tooport de tooensure *81* sur *Vip2* est équilibrée entre *myVM1* et *myVM2* sur le port *8181* , exécutez hello après le script PowerShell :

```powershell
Get-AzureVM -ServiceName myService -Name myVM1 |
    Add-AzureEndpoint -Name myEndpoint -LoadBalancedEndpointSetName myLBSet -Protocol tcp -LocalPort 8181 -PublicPort 81 -VirtualIPName Vip2 -DefaultProbe |
    Update-AzureVM

Get-AzureVM -ServiceName myService -Name myVM2 |
    Add-AzureEndpoint -Name myEndpoint -LoadBalancedEndpointSetName myLBSet -Protocol tcp -LocalPort 8181 -PublicPort 81 -VirtualIPName Vip2  -DefaultProbe |
    Update-AzureVM
```

Vous pouvez également mettre à jour votre toouse d’équilibrage de charge une adresse IP virtuelle différente. Par exemple, si vous exécutez hello commande PowerShell suivante, vous allez modifier le jeu toouse une adresse IP virtuelle nommée Vip1 d’équilibrage de charge hello :

```powershell
Set-AzureLoadBalancedEndpoint -ServiceName myService -LBSetName myLBSet -VirtualIPName Vip1
```

## <a name="next-steps"></a>Étapes suivantes

[Analyse des journaux d’Azure Load Balancer](load-balancer-monitor-log.md)

[Présentation de l’équilibrage de charge accessible sur Internet](load-balancer-internet-overview.md)

[Prise en main de l’équilibrage de charge accessible sur Internet](load-balancer-get-started-internet-arm-ps.md)

[Présentation du réseau virtuel.](../virtual-network/virtual-networks-overview.md)

[API REST d’adresse IP réservée](https://msdn.microsoft.com/library/azure/dn722420.aspx)
