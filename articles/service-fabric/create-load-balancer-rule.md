---
title: "aaaCreate une règle d’équilibrage de charge Azure pour un cluster"
description: "Configurer un équilibrage de charge Azure tooopen des ports pour votre cluster Azure Service Fabric."
services: service-fabric
documentationcenter: na
author: thraka
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/22/2017
ms.author: adegeo
ms.openlocfilehash: 4a40f62422bd895d782be8cbaace5f4e1af81db3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="open-ports-for-a-service-fabric-cluster"></a>Ouvrir des ports pour un cluster Service Fabric

équilibrage de charge Hello déployé avec votre cluster Azure Service Fabric dirige le trafic tooyour application est en cours d’exécution sur un nœud. Si vous modifiez votre application de toouse un autre port, vous devez exposer ce port (ou acheminer un autre port) Bonjour équilibrage de charge Azure.

Lorsque vous avez déployé votre tooAzure de cluster service fabric, un équilibreur de charge a été créé automatiquement pour vous. Si vous ne disposez pas d’un équilibrage de charge, consultez [Configurer un équilibreur de charge connecté à Internet](..\load-balancer\load-balancer-get-started-internet-portal.md).

## <a name="configure-service-fabric"></a>Configurer Service Fabric

Votre application de Service Fabric **ServiceManifest.xml** le fichier de configuration définit les points de terminaison hello toouse que votre application attend. Une fois que le fichier de configuration hello a été mis à jour toodefine un point de terminaison, équilibrage de charge hello doit être mis à jour tooexpose que (ou une autre) port. Pour plus d’informations sur la façon dont toocreate hello point de terminaison de service fabric, consultez [le programme d’installation d’un point de terminaison](service-fabric-service-manifest-resources.md).

## <a name="create-a-load-balancer-rule"></a>Créer une règle d’équilibreur de charge

Une règle d’équilibreur de charge s’ouvre un port connecté à internet et transmet le port du nœud de l’intérieur du trafic toohello utilisé par votre application. Si vous ne disposez pas d’un équilibrage de charge, consultez [Configurer un équilibreur de charge connecté à Internet](..\load-balancer\load-balancer-get-started-internet-portal.md).

règle de toocreate un équilibreur de charge, vous devez hello toocollect informations suivantes :

- Nom de l’équilibreur de charge.
- Groupe de ressources de hello équilibreur de charge et cluster service fabric.
- Port externe.
- Port interne.

## <a name="azure-cli"></a>Interface de ligne de commande Azure
>[!NOTE]
>Si vous avez besoin de nom de hello toodetermine d’équilibrage de charge hello, vous pouvez utiliser cette get tooquickly de commande une liste de tous les équilibreurs de charge et les groupes de ressources hello associé.
>
>`az network lb list --query "[].{ResourceGroup: resourceGroup, Name: name}"`
>

Il n’accepte qu’une commande unique de toocreate une règle d’équilibreur de charge avec hello **CLI d’Azure**. Vous devez simplement tooknow à la fois nom hello de hello charge équilibrage et ressource groupe toocreate une nouvelle règle.

```azurecli
az network lb rule create --backend-port 40000 --frontend-port 39999 --protocol Tcp --lb-name LB-svcfab3 -g svcfab_cli -n my-app-rule
```

Hello commande CLI d’Azure a quelques paramètres décrits dans hello tableau suivant :

| Paramètre | Description |
| --------- | ----------- |
| `--backend-port`  | application de l’ensemble fibre optique Hello port hello service écoute. |
| `--frontend-port` | Bonjour Bonjour de port de charge expose équilibrage pour les connexions externes. |
| `-lb-name` | toochange d’équilibrage de charge nom Hello Hello. |
| `-g`       | groupe de ressources Hello qui a l’équilibrage de charge hello et cluster service fabric. |
| `-n`       | Hello choisi le nom de règle de hello. |


>[!NOTE]
>Pour plus d’informations sur comment toocreate un équilibreur de charge avec hello CLI d’Azure, consultez [créer un équilibreur de charge avec hello CLI d’Azure](..\load-balancer\load-balancer-get-started-internet-arm-cli.md).

## <a name="powershell"></a>PowerShell

>[!NOTE]
>Si vous avez besoin de nom de hello toodetermine d’équilibrage de charge hello, utilisez cette get tooquickly de commandes une liste de tous les équilibrages de charge et les groupes de ressources associé.
>
>`Get-AzureRmLoadBalancer | Select Name, ResourceGroupName`

PowerShell est un peu plus compliqué que hello CLI d’Azure. Point de vue conceptuel, faire hello suivant les étapes toocreate une règle.

1. Obtenir l’équilibrage de charge hello à partir d’Azure.
2. Créez une règle.
3. Ajouter un équilibrage de charge hello règle toohello.
4. Mettre à jour d’équilibrage de charge hello.

```powershell
# Get hello load balancer
$lb = Get-AzureRmLoadBalancer -Name LB-svcfab3 -ResourceGroupName svcfab_cli

# Create hello rule based on information from hello load balancer.
$lbrule = New-AzureRmLoadBalancerRuleConfig -Name my-app-rule7 -Protocol Tcp -FrontendPort 39990 -BackendPort 40009 `
                                            -FrontendIpConfiguration $lb.FrontendIpConfigurations[0] `
                                            -BackendAddressPool  $lb.BackendAddressPools[0] `
                                            -Probe $lb.Probes[0]

# Add hello rule toohello load balancer
$lb.LoadBalancingRules.Add($lbrule)

# Update hello load balancer on Azure
$lb | Set-AzureRmLoadBalancer
```

En ce qui concerne les hello `New-AzureRmLoadBalancerRuleConfig` commande hello `-FrontendPort` équilibrage de charge représente hello port hello expose pour les connexions externes et hello `-BackendPort` représente hello port hello service fabric application écoute.

>[!NOTE]
>Pour plus d’informations sur comment toocreate un équilibreur de charge avec PowerShell, consultez [créer un équilibreur de charge avec PowerShell](..\load-balancer\load-balancer-get-started-internet-arm-ps.md).

