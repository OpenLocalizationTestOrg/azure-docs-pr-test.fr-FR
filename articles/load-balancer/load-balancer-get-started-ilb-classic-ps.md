---
title: "aaaCreate Azure interne l’équilibrage de charge - PowerShell classique | Documents Microsoft"
description: "Découvrez comment toocreate un interne l’équilibrage de charge à l’aide de PowerShell dans le modèle de déploiement classique de hello"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 3be93168-3787-45a5-a194-9124fe386493
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 382db80c42ffab09905513019b72e85a4f9dfeff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internal-load-balancer-classic-using-powershell"></a>Prise en main de la création d’un équilibreur de charge interne (classique) à l’aide de PowerShell

> [!div class="op_single_selector"]
> * [PowerShell](../load-balancer/load-balancer-get-started-ilb-classic-ps.md)
> * [interface de ligne de commande Azure](../load-balancer/load-balancer-get-started-ilb-classic-cli.md)
> * [Services cloud](../load-balancer/load-balancer-get-started-ilb-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!IMPORTANT]
> Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [Resource Manager et classique](../azure-resource-manager/resource-manager-deployment-model.md).  Cet article décrit à l’aide du modèle de déploiement classique hello. Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello. Découvrez comment trop[effectuer ces étapes à l’aide du modèle de gestionnaire de ressources hello](load-balancer-get-started-ilb-arm-ps.md).

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-an-internal-load-balancer-set-for-virtual-machines"></a>Créer un jeu d’équilibrage de charge interne pour les machines virtuelles

toocreate un équilibreur de charge interne défini et hello serveurs qui y enverront leur tooit le trafic, vous disposer de toodo hello :

1. Créer une instance d’interne l’équilibrage de charge qui sera le point de terminaison hello d’entrant trafic toobe équilibrée entre les serveurs hello d’un jeu d’équilibrage de la charge.
2. Ajoutez les machines virtuelles toohello qui recevront le trafic entrant de hello correspondantes des points de terminaison.
3. Configurez les serveurs hello qui enverront hello trafic toobe à charge équilibrée toosend leur trafic toohello adresse IP virtuelle (VIP) de l’instance d’équilibrage de charge interne hello.

### <a name="step-1-create-an-internal-load-balancing-instance"></a>Étape 1 : Créer une instance d’équilibrage de charge interne

Pour un service cloud existant ou un service cloud déployé dans un réseau virtuel régional, vous pouvez créer une instance de l’équilibrage de charge interne avec hello suivant de commandes Windows PowerShell :

```powershell
$svc="<Cloud Service Name>"
$ilb="<Name of your ILB instance>"
$subnet="<Name of hello subnet within your virtual network>"
$IP="<hello IPv4 address toouse on hello subnet-optional>"

Add-AzureInternalLoadBalancer -ServiceName $svc -InternalLoadBalancerName $ilb –SubnetName $subnet –StaticVNetIPAddress $IP
```

Notez que cette utilisation de hello [Add-AzureEndpoint](https://msdn.microsoft.com/library/dn495300.aspx) applet de commande Windows PowerShell utilise hello de paramètres defaultprobe. Pour plus d'informations sur les jeux de paramètres supplémentaires, consultez [Add-AzureEndpoint](https://msdn.microsoft.com/library/dn495300.aspx).

### <a name="step-2-add-endpoints-toohello-internal-load-balancing-instance"></a>Étape 2 : Ajouter l’instance d’équilibrage de charge interne toohello points de terminaison

Voici un exemple :

```powershell
$svc="mytestcloud"
$vmname="DB1"
$epname="TCP-1433-1433"
$lbsetname="lbset"
$prot="tcp"
$locport=1433
$pubport=1433
$ilb="ilbset"
Get-AzureVM –ServiceName $svc –Name $vmname | Add-AzureEndpoint -Name $epname -Lbset $lbsetname -Protocol $prot -LocalPort $locport -PublicPort $pubport –DefaultProbe -InternalLoadBalancerName $ilb | Update-AzureVM
```

### <a name="step-3-configure-your-servers-toosend-their-traffic-toohello-new-internal-load-balancing-endpoint"></a>Étape 3 : Configurer votre toosend serveurs leur trafic toohello nouveau équilibrage de charge interne point de terminaison

Vous avez trop configurer serveurs hello dont le trafic est continu toobe à charge équilibrée toouse hello nouvelle adresse IP (hello VIP) de hello instance d’équilibrage de charge interne. Il s’agit d’adresse hello sur quel hello équilibrage de charge interne de l’instance écoute. Dans la plupart des cas, vous devez toojust ajouter ou modifier un enregistrement DNS pour hello VIP de l’instance de l’équilibrage de charge interne hello.

Si vous avez spécifié l’adresse IP de hello lors de la création de hello d’instance d’équilibrage de charge interne hello, vous disposez déjà d’adresses IP virtuelles hello. Sinon, vous pouvez voir VIP hello de hello suivant de commandes :

```powershell
$svc="<Cloud Service Name>"
Get-AzureService -ServiceName $svc | Get-AzureInternalLoadBalancer
```

toouse ces commandes, renseignez les valeurs hello et remove hello < et >. Voici un exemple :

```powershell
$svc="mytestcloud"
Get-AzureService -ServiceName $svc | Get-AzureInternalLoadBalancer
```

À partir de l’affichage hello Hello de commande Get-AzureInternalLoadBalancer, notez l’adresse IP de hello et rendre les serveurs tooyour hello les modifications nécessaires ou tooensure d’enregistrements DNS que le trafic est envoyé toohello VIP.

> [!NOTE]
> plateforme de Microsoft Azure Hello utilise une adresse IPv4 statique routable publiquement pour un éventail de scénarios d’administration. adresse IP de Hello est 168.63.129.16. Cette adresse IP ne doit pas être bloquée par les pare-feu, car cela peut entraîner un comportement inattendu.
> Avec tooAzure égard équilibrage de charge interne, cette adresse IP est utilisée par l’analyse des sondes de l’état d’intégrité de hello charge équilibrage toodetermine hello pour les ordinateurs virtuels dans un jeu d’équilibrage de charge. Si un groupe de sécurité réseau est utilisé toorestrict virtuels trafic tooAzure dans un jeu d’équilibrage de charge en interne ou tooa appliqué sous-réseau de réseau virtuel, assurez-vous qu’une règle de sécurité réseau est ajoutée tooallow trafic à partir de 168.63.129.16.

## <a name="example-of-internal-load-balancing"></a>Exemple d’équilibrage de charge interne

toostep vous guide dans hello des processus de tooend à la fin de la création d’un jeu d’équilibrage de la charge pour les deux exemples de configuration, consultez hello suivants sections.

### <a name="an-internet-facing-multi-tier-application"></a>Une application multi-niveau sur Internet

Vous souhaitez tooprovide un service de base de données d’équilibrage de charge pour un ensemble de serveurs de web exposés à Internet. Les deux ensembles de serveurs sont hébergés dans un seul service cloud Azure. TooTCP port 1433 du trafic serveur Web doit être réparti entre deux ordinateurs virtuels dans la couche de base de données hello. Figure 1 illustre la configuration de hello.

![Jeu d’équilibrage de charge interne pour le niveau de base de données hello](./media/load-balancer-internal-getstarted/IC736321.png)

configuration de Hello se compose d’éléments suivants de hello :

* service cloud existant Hello hébergeant des ordinateurs virtuels de hello est nommé mytestcloud.
* deux serveurs de base de données existante Hello sont nommés DB1 et DB2.
* Serveurs Web dans la couche web de hello connectent toohello des serveurs de base de données dans la couche de base de données hello en utilisant l’adresse IP privée de hello. Une autre option est toouse votre propre DNS pour le réseau virtuel de hello et inscrire manuellement un enregistrement A pour le jeu d’équilibrage de charge interne de hello.

Hello commandes suivantes configurent une nouvelle instance de l’équilibrage de charge interne nommée **ILBset** et ajoutez des machines virtuelles de points de terminaison toohello correspondant des serveurs de base de données toohello deux :

```powershell
$svc="mytestcloud"
$ilb="ilbset"
Add-AzureInternalLoadBalancer -ServiceName $svc -InternalLoadBalancerName $ilb
$prot="tcp"
$locport=1433
$pubport=1433
$epname="TCP-1433-1433"
$lbsetname="lbset"
$vmname="DB1"
Get-AzureVM –ServiceName $svc –Name $vmname | Add-AzureEndpoint -Name $epname -LbSetName $lbsetname -Protocol $prot -LocalPort $locport -PublicPort $pubport –DefaultProbe -InternalLoadBalancerName $ilb | Update-AzureVM

$epname="TCP-1433-1433-2"
$vmname="DB2"
Get-AzureVM –ServiceName $svc –Name $vmname | Add-AzureEndpoint -Name $epname -LbSetName $lbsetname -Protocol $prot -LocalPort $locport -PublicPort $pubport –DefaultProbe -InternalLoadBalancerName $ilb | Update-AzureVM
```

## <a name="remove-an-internal-load-balancing-configuration"></a>Supprimer une configuration d’équilibrage de charge interne

tooremove une machine virtuelle comme un point de terminaison à partir d’une instance d’équilibrage de charge interne, hello utilisation suivant de commandes :

```powershell
$svc="<Cloud service name>"
$vmname="<Name of hello VM>"
$epname="<Name of hello endpoint>"
Get-AzureVM -ServiceName $svc -Name $vmname | Remove-AzureEndpoint -Name $epname | Update-AzureVM
```

toouse ces commandes, renseignez les valeurs hello, suppression hello < et >.

Voici un exemple :

```powershell
$svc="mytestcloud"
$vmname="DB1"
$epname="TCP-1433-1433"
Get-AzureVM -ServiceName $svc -Name $vmname | Remove-AzureEndpoint -Name $epname | Update-AzureVM
```

tooremove une instance d’équilibrage de charge interne à partir d’un service cloud, hello utilisation suivant de commandes :

```powershell
$svc="<Cloud service name>"
Remove-AzureInternalLoadBalancer -ServiceName $svc
```

toouse ces commandes, renseignez les valeur hello et supprimer hello < et >.

Voici un exemple :

```powershell
$svc="mytestcloud"
Remove-AzureInternalLoadBalancer -ServiceName $svc
```

## <a name="additional-information-about-internal-load-balancer-cmdlets"></a>Informations supplémentaires sur les applets de commande de l’équilibreur de charge interne

tooobtain plus d’informations sur l’équilibrage de charge interne applets de commande, exécutez hello suivant de commandes à partir d’une invite Windows PowerShell :

```powershell
Get-Help New-AzureInternalLoadBalancerConfig -full
Get-Help Add-AzureInternalLoadBalancer -full
Get-Help Get-AzureInternalLoadbalancer -full
Get-Help Remove-AzureInternalLoadBalancer -full
```

## <a name="next-steps"></a>Étapes suivantes

[Configurer le mode de distribution d’équilibreur de charge à l’aide de l’affinité d’IP source](load-balancer-distribution-mode.md)

[Configuration des paramètres de délai d’expiration TCP inactif pour votre équilibrage de charge](load-balancer-tcp-idle-timeout.md)

