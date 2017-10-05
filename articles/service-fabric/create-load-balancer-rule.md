---
title: "Créer une règle Azure Load Balancer pour un cluster"
description: Configurez Azure Load Balancer pour ouvrir les ports pour votre cluster Azure Service Fabric.
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
ms.openlocfilehash: c99c4d9f343ca97fd3cd363fb54feaf5507bb77c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="open-ports-for-a-service-fabric-cluster"></a>Ouvrir des ports pour un cluster Service Fabric

L’équilibreur de charge déployé avec votre cluster Azure Service Fabric dirige le trafic vers votre application en cours d’exécution sur un nœud. Si vous modifiez votre application pour utiliser un autre port, vous devez exposer ce port (ou acheminer un port différent) dans Azure Load Balancer.

Une fois votre cluster Service Fabric déployé vers Azure, un équilibreur de charge est créé automatiquement pour vous. Si vous ne disposez pas d’un équilibrage de charge, consultez [Configurer un équilibreur de charge connecté à Internet](..\load-balancer\load-balancer-get-started-internet-portal.md).

## <a name="configure-service-fabric"></a>Configurer Service Fabric

Le fichier de configuration de votre application Service Fabric **ServiceManifest.xml** définit les points de terminaison que votre application s’attend à utiliser. Une fois le fichier de configuration mis à jour pour définir un point de terminaison, l’équilibreur de charge doit être mis à jour pour exposer ce port (ou un autre). Pour plus d’informations sur la façon de créer le point de terminaison Service Fabric, consultez [Configurer un point de terminaison](service-fabric-service-manifest-resources.md).

## <a name="create-a-load-balancer-rule"></a>Créer une règle d’équilibreur de charge

Une règle d’équilibreur de charge ouvre un port connecté à internet et transfère le trafic vers le port du nœud interne utilisé par votre application. Si vous ne disposez pas d’un équilibrage de charge, consultez [Configurer un équilibreur de charge connecté à Internet](..\load-balancer\load-balancer-get-started-internet-portal.md).

Pour créer une règle d’équilibreur de charge, vous devez collecter les informations suivantes :

- Nom de l’équilibreur de charge.
- Groupe de ressources de l’équilibreur de charge et du cluster Service Fabric.
- Port externe.
- Port interne.

## <a name="azure-cli"></a>Interface de ligne de commande Azure
>[!NOTE]
>Si vous avez besoin déterminer le nom de l’équilibreur de charge, utilisez cette commande pour obtenir rapidement une liste de tous les équilibreurs de charge et des groupes de ressources associés.
>
>`az network lb list --query "[].{ResourceGroup: resourceGroup, Name: name}"`
>

Il suffit d’une seule commande pour créer une règle d’équilibreur de charge avec l’interface **Azure CLI**. Vous devez simplement connaître le nom de l’équilibreur de charge et du groupe de ressources pour créer une nouvelle règle.

```azurecli
az network lb rule create --backend-port 40000 --frontend-port 39999 --protocol Tcp --lb-name LB-svcfab3 -g svcfab_cli -n my-app-rule
```

La commande Azure CLI dispose de quelques paramètres décrits dans le tableau suivant :

| Paramètre | Description |
| --------- | ----------- |
| `--backend-port`  | Le port que l’application Service Fabric écoute. |
| `--frontend-port` | Le port que l’équilibreur de charge expose aux connexions externes. |
| `-lb-name` | Le nom de l’équilibreur de charge à modifier. |
| `-g`       | Le groupe de ressources qui dispose de l’équilibreur de charge et du cluster Service Fabric. |
| `-n`       | Le nom de la règle choisi. |


>[!NOTE]
>Pour plus d’informations sur la création d’un équilibreur de charge avec l’interface Azure CLI, consultez [Créer un équilibreur de charge avec l’interface Azure CLI](..\load-balancer\load-balancer-get-started-internet-arm-cli.md).

## <a name="powershell"></a>PowerShell

>[!NOTE]
>Si vous devez déterminer le nom de l’équilibreur de charge, utilisez cette commande pour obtenir rapidement une liste de tous les équilibreurs de charge et des groupes de ressources associés.
>
>`Get-AzureRmLoadBalancer | Select Name, ResourceGroupName`

PowerShell est un peu plus compliqué que l’interface Azure CLI. Sur le plan conceptuel, procédez comme suit pour créer une règle.

1. Récupérez l’équilibreur de charge d’Azure.
2. Créez une règle.
3. Ajoutez la règle pour l'équilibreur de charge.
4. Mettez à jour l’équilibreur de charge.

```powershell
# Get the load balancer
$lb = Get-AzureRmLoadBalancer -Name LB-svcfab3 -ResourceGroupName svcfab_cli

# Create the rule based on information from the load balancer.
$lbrule = New-AzureRmLoadBalancerRuleConfig -Name my-app-rule7 -Protocol Tcp -FrontendPort 39990 -BackendPort 40009 `
                                            -FrontendIpConfiguration $lb.FrontendIpConfigurations[0] `
                                            -BackendAddressPool  $lb.BackendAddressPools[0] `
                                            -Probe $lb.Probes[0]

# Add the rule to the load balancer
$lb.LoadBalancingRules.Add($lbrule)

# Update the load balancer on Azure
$lb | Set-AzureRmLoadBalancer
```

En ce qui concerne la commande `New-AzureRmLoadBalancerRuleConfig`, le `-FrontendPort` représente le port que l’équilibrage de charge expose aux connexions externes, et le `-BackendPort` représente le port d’écoute de l’application Service Fabric.

>[!NOTE]
>Pour plus d’informations sur la création d’un équilibreur de charge avec l’interface PowerShellI, consultez [Créer un équilibreur de charge avec PowerShell](..\load-balancer\load-balancer-get-started-internet-arm-ps.md).

