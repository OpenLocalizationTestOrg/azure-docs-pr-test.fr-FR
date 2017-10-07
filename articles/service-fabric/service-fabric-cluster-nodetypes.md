---
title: "l’ensemble fibre optique d’aaaService types de nœuds et les jeux de mise à l’échelle de machine virtuelle | Documents Microsoft"
description: "Décrit l’interaction avec les types de nœud de Service Fabric tooVM identiques et comment tooremote connecter instance d’ensemble d’échelle de machine virtuelle tooa ou un nœud de cluster."
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: 
ms.assetid: 5441e7e0-d842-4398-b060-8c9d34b07c48
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/05/2017
ms.author: chackdan
ms.openlocfilehash: 830ea2816f5864de146a77483c85de26f91c2425
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="hello-relationship-between-service-fabric-node-types-and-virtual-machine-scale-sets"></a>relation Hello entre les types de nœuds de l’infrastructure de Service et les machines virtuelles identiques
Machines virtuelles identiques sont une ressource de calcul Azure, vous pouvez utiliser toodeploy et gérer une collection d’ordinateurs virtuels en tant qu’ensemble. Chaque type de nœud qui est défini dans un cluster Service Fabric est configuré en tant que jeu de mise à l’échelle de machine virtuelle distinct. Chaque type de nœud peut ensuite faire l’objet d’une montée ou descente en puissance de manière indépendante, avoir différents jeux de ports ouverts et présenter différentes métriques de capacité.

Hello suivant capture d’écran montre un cluster qui possède deux types de nœuds : serveur frontal et principal.  Chaque type de nœud comporte cinq nœuds.

![Capture d’écran d’un cluster qui a deux types de nœuds][NodeTypes]

## <a name="mapping-vm-scale-set-instances-toonodes"></a>Mappage toonodes d’instances ensemble d’échelle de machine virtuelle
Comme vous pouvez le voir ci-dessus, les instances d’ensemble d’échelle de machine virtuelle hello démarrer à partir de l’instance 0 et puis remonte. la numérotation Hello est répercutée dans les noms de hello. Par exemple, BackEnd_0 est instance 0 du hello ensemble d’échelle de machine virtuelle principale. Ce groupe a cinq instances, nommées BackEnd_0, BackEnd_1, BackEnd_2, BackEnd_3 et BackEnd_4.

Quand vous effectuez une montée en puissance sur un groupe de machines virtuelles identiques, une instance est créée. Hello nouvel ensemble d’échelle de machine virtuelle nom de l’instance sera généralement le nom d’ensemble d’échelle de machine virtuelle hello + numéro d’instance suivant hello. Dans notre exemple, il s’agit de BackEnd_5.

## <a name="mapping-vm-scale-set-load-balancers-tooeach-node-typevm-scale-set"></a>Mappage des machines virtuelles identiques charger équilibrages tooeach nœud type/machine virtuelle ensemble d’échelle
Si vous avez déployé votre cluster à partir du portail de hello ou que vous avez utilisé hello exemple Gestionnaire de ressources de modèle que nous avons fournis, puis lorsque vous obtenez une liste de toutes les ressources sous un groupe de ressources vous verrez les équilibreurs de charge hello pour chaque type de nœud ou ensemble d’échelle de machine virtuelle.

Hello nom serait quelque chose comme : **LB -&lt;NodeType nom&gt;**. Par exemple, LB-sfcluster4doc-0, comme indiqué dans cette capture d’écran :

![Ressources][Resources]

## <a name="remote-connect-tooa-vm-scale-set-instance-or-a-cluster-node"></a>Instance de tooa ensemble d’échelle de machine virtuelle ou un nœud de cluster de connexion à distance
Chaque type de nœud qui est défini dans un cluster est configuré comme un jeu de mise à l’échelle de machine virtuelle distinct.  Que signifie hello des types de nœud peut être mis à l’échelle vers le haut ou vers le bas de manière indépendante et vous pouvez établir des références SKU de machine virtuelle différente. Contrairement aux ordinateurs virtuels d’instance unique, les instances d’ensemble d’échelle de machine virtuelle hello n’obtiennent pas une adresse IP virtuelle de leurs propres. Il peut être un peu difficile lorsque vous recherchez une adresse IP adresse et le port que vous pouvez utiliser tooremote connectent instance spécifique de tooa.

Voici les étapes hello vous pouvez suivre toodiscover les.

### <a name="step-1-find-out-hello-virtual-ip-address-for-hello-node-type-and-then-inbound-nat-rules-for-rdp"></a>Étape 1 : Découvrir les adresse IP virtuelle hello hello type de nœud, puis les règles NAT entrantes pour RDP
Dans tooget de commande, vous avez besoin tooget hello NAT de trafic entrant règles des valeurs qui ont été définies dans le cadre de la définition de ressource hello pour **Microsoft.Network/loadBalancers**.

Dans le portail hello, accédez au panneau de programme d’équilibrage de charge toohello, puis **paramètres**.

![Panneau Équilibrage de charge][LBBlade]

Dans **Paramètres**, cliquez sur **Règles NAT de trafic entrant**. Cela maintenant donne vous hello d’adresse IP et port que vous pouvez utiliser tooremote connecter toohello première instance ensemble d’échelle de machine virtuelle. Dans la capture d’écran de hello ci-dessous, il est **104.42.106.156** et **3389**

![Règles NAT][NATRules]

### <a name="step-2-find-out-hello-port-that-you-can-use-tooremote-connect-toohello-specific-vm-scale-set-instancenode"></a>Étape 2 : Découvrez les port hello que vous pouvez utiliser tooremote connecter toohello ensemble d’échelle de machine virtuelle instance/nœud spécifique
Plus haut dans ce document, j’ai parlé comment mappent des nœuds de toohello par les instances de hello ensemble d’échelle de machine virtuelle. Nous utiliserons cette toofigure port exact de hello.

ports de Hello sont allouées dans l’ordre croissant d’instance d’ensemble d’échelle de machine virtuelle hello. Par conséquent, dans mon exemple pour le type de nœud de serveur frontal de hello, ports hello pour chacun des cinq instances de hello sont suivant de hello. vous maintenant toodo devez hello même mappage de votre instance de l’ensemble d’échelle de machine virtuelle.

| **Instance de jeu de mise à l’échelle de machine virtuelle** | **Port** |
| --- | --- |
| FrontEnd_0 |3389 |
| FrontEnd_1 |3390 |
| FrontEnd_2 |3391 |
| FrontEnd_3 |3392 |
| FrontEnd_4 |3393 |
| FrontEnd_5 |3394 |

### <a name="step-3-remote-connect-toohello-specific-vm-scale-set-instance"></a>Étape 3 : Instance d’ensemble d’échelle de machine virtuelle spécifique toohello de se connecter à distance
Dans la capture d’écran hello ci-dessous utiliser Connexion Bureau à distance tooconnect toohello FrontEnd_1 :

![RDP][RDP]

## <a name="how-toochange-hello-rdp-port-range-values"></a>Comment les valeurs de plage de toochange hello port RDP
### <a name="before-cluster-deployment"></a>Avant le déploiement du cluster
Lorsque vous configurez un cluster hello à l’aide d’un modèle de gestionnaire de ressources, vous pouvez spécifier la plage de hello Bonjour **inboundNatPools**.

Obtenir la définition de ressource toohello **Microsoft.Network/loadBalancers**. Sous que vous recherchez description hello pour **inboundNatPools**.  Remplacez hello *frontal* et *frontal* valeurs.

![inboundNatPools][InboundNatPools]

### <a name="after-cluster-deployment"></a>Après le déploiement du cluster
Cela est un peu plus complexe et peut entraîner des machines virtuelles de hello recyclés. Vous avez maintenant tooset nouvelles valeurs à l’aide d’Azure PowerShell. Vérifiez qu’Azure PowerShell 1.0 ou version ultérieure est installé sur votre ordinateur. Si vous n’avez pas fait avant, je vous recommande vivement que vous suivez hello étapes [comment tooinstall et configurer Azure PowerShell.](/powershell/azure/overview)

Se connecter tooyour compte Azure. Si cette commande PowerShell échoue pour une raison quelconque, vous devez vérifier si Azure PowerShell est correctement installé.

```
Login-AzureRmAccount
```

Exécutez hello suivant détaille tooget de votre équilibreur de charge et vous pouvez voir description hello pour les valeurs hello **inboundNatPools**:

```
Get-AzureRmResource -ResourceGroupName <RGname> -ResourceType Microsoft.Network/loadBalancers -ResourceName <load balancer name>
```

À présent définir *frontal* et *frontal* toohello les valeurs souhaitées.

```
$PropertiesObject = @{
    #Property = value;
}
Set-AzureRmResource -PropertyObject $PropertiesObject -ResourceGroupName <RG name> -ResourceType Microsoft.Network/loadBalancers -ResourceName <load Balancer name> -ApiVersion <use hello API version that get returned> -Force
```


## <a name="next-steps"></a>Étapes suivantes
* [Vue d’ensemble de la fonctionnalité de « Déployer n’importe où » hello et une comparaison avec des clusters de géré Azure](service-fabric-deploy-anywhere.md)
* [Sécurité des clusters](service-fabric-cluster-security.md)
* [ Kit de développement logiciel (SDK) de Service Fabric et prise en main](service-fabric-get-started.md)

<!--Image references-->
[NodeTypes]: ./media/service-fabric-cluster-nodetypes/NodeTypes.png
[Resources]: ./media/service-fabric-cluster-nodetypes/Resources.png
[InboundNatPools]: ./media/service-fabric-cluster-nodetypes/InboundNatPools.png
[LBBlade]: ./media/service-fabric-cluster-nodetypes/LBBlade.png
[NATRules]: ./media/service-fabric-cluster-nodetypes/NATRules.png
[RDP]: ./media/service-fabric-cluster-nodetypes/RDP.png
