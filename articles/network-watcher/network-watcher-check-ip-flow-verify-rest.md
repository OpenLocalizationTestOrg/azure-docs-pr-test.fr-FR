---
title: "vérification du trafic aaaVerify le transfert IP de l’Observateur réseau Azure - REST | Documents Microsoft"
description: "Cet article décrit comment toocheck si tooor le trafic à partir d’un ordinateur virtuel est autorisé ou refusé"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 3307a79f-03be-46a0-aaaf-b2079cb5f3b2
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 956db0d326db597c6c402a9e8d4a5522c47c02d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-with-ip-flow-verify-a-component-of-azure-network-watcher"></a>Vérifier si le trafic est autorisé ou refusé avec le composant de vérification des flux IP d’Azure Network Watcher

> [!div class="op_single_selector"]
> - [Portail Azure](network-watcher-check-ip-flow-verify-portal.md)
> - [PowerShell](network-watcher-check-ip-flow-verify-powershell.md)
> - [CLI 1.0](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [CLI 2.0](network-watcher-check-ip-flow-verify-cli.md)
> - [API REST Azure](network-watcher-check-ip-flow-verify-rest.md)


Vérifiez que les flux IP est une fonctionnalité de l’Observateur réseau qui vous permet de tooverify si le trafic est autorisé à tooor à partir d’un ordinateur virtuel. la validation de Hello peut être exécutée pour le trafic entrant ou sortant. Ce scénario est utile tooget un état actuel de si un ordinateur virtuel peut communiquer avec les ressources externes tooan ou principal. Les flux IP vérifier peut être utilisé tooverify si vos règles de groupe de sécurité réseau (NSG) sont correctement configurés et résoudre les problèmes de flux qui sont bloqués par les règles du groupe de sécurité réseau. Une autre raison de l’utilisation de IP flux Vérifiez à bloquer le trafic de tooensure est bloqué correctement par hello groupe de sécurité réseau.

## <a name="before-you-begin"></a>Avant de commencer

ARMclient est utilisé toocall hello REST API à l’aide de PowerShell. ARMClient est accessible sur le site chocolatey à partir de la page [ARMClient sur Chocolatey](https://chocolatey.org/packages/ARMClient).

Ce scénario suppose que vous avez déjà suivi les étapes hello dans [créer un observateur réseau](network-watcher-create.md) toocreate un observateur réseau.

## <a name="scenario"></a>Scénario

Ce scénario utilise IP flux Vérifiez tooverify si une machine virtuelle peut communiquer avec l’ordinateur de tooanother sur le port 443. Si le trafic de hello est refusé, elle retourne la règle de sécurité hello refuse ce trafic. toolearn en savoir plus sur les flux d’IP Verify, visitez [les flux IP vérifier la vue d’ensemble](network-watcher-ip-flow-verify-overview.md)

Dans ce scénario, vous allez :

* Récupérer une machine virtuelle
* Appeler la vérification des flux IP
* Vérifier les résultats

## <a name="log-in-with-armclient"></a>Se connecter à ARMClient

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a>Récupérer une machine virtuelle

Exécutez hello suivant script tooreturn une machine virtuelle. Hello suivant code a besoin de valeurs pour les variables de hello :

* **ID d’abonnement** -hello toouse de Id d’abonnement.
* **resourceGroupName** hello - nom du groupe de ressources qui contient des machines virtuelles.

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>"

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

informations nécessaires Hello sont id hello sous le type hello `Microsoft.Compute/virtualMachines`. les résultats de Hello doivent être similaires toohello suivant l’exemple de code :

```json
...,
        "networkProfile": {
          "networkInterfaces": [
            {
              "id": "/subscriptions/{00000000-0000-0000-0000-000000000000}/resourceGroups/ContosoExampleRG/providers/Microsoft
.Network/networkInterfaces/contosovm842"
            }
          ]
        },
        "provisioningState": "Succeeded"
      },
      "resources": [
        {
          "id": "/subscriptions/{00000000-0000-0000-0000-000000000000}/resourceGroups/ContosoExampleRG/providers/Microsoft.Com
pute/virtualMachines/ContosoVM/extensions/CustomScriptExtension"
        }
      ],
      "type": "Microsoft.Compute/virtualMachines",
      "location": "westcentralus",
      "id": "/subscriptions/{00000000-0000-0000-0000-000000000000}/resourceGroups/ContosoExampleRG/providers/Microsoft.Compute
/virtualMachines/ContosoVM",
      "name": "ContosoVM"
    }
  ]
}
```

## <a name="call-ip-flow-verify"></a>Appeler la vérification des flux IP

Hello exemple suivant crée un demande tooverify hello du trafic d’un ordinateur virtuel spécifié. réponse de Hello retourne si hello le trafic est autorisé ou si le trafic de hello est refusé. Si le trafic est refusé qu'il retourne également les blocs de règles hello du trafic.

> [!NOTE]
> Les flux IP vérifier requiert que la ressource de machine virtuelle hello est allouée.

script de Hello nécessite un Id d’un ordinateur virtuel et d’une carte d’interface réseau sur l’ordinateur virtuel de hello de la ressource hello. Ces valeurs sont fournies par hello précédant la sortie.

> [!Important]
> Pour le reste de l’Observateur réseau tous les appels hello nom de groupe de ressources dans l’URI est hello qui contient d’instance de l’Observateur réseau hello, pas les ressources hello vous effectuez des actions de diagnostic hello sur la demande hello.

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>"
$networkWatcherName = "<network watcher name>"
$vmName = "<vm name>"
$vmNICName = "<vm NIC name>"
$direction = "<direction of traffic>" # Examples are: Inbound or Outbound
$localIP = "<source IP>"
$localPort = "<source Port>"
$remoteIP = "<destination IP>"
$remotePort = "<destination Port>" # Examples are: 80, or 80-120
$protocol = "<UDP, TCP or *>"
$targetUri = "<uri of target resource>" # Example: /subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.compute/virtualMachine/${vmName}
$targetNic = "<uri of target nic resource>" # Example: /subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkInterfaces/${vmNICName}

$requestBody = @"
{
    'targetResourceId':  '$targetUri',
    'direction':  '$direction',
    'protocol':  '$protocol',
    'localPort':  '$localPort',
    'remotePort':  '$remotePort',
    'localIPAddress':  '$localIP',
    'remoteIPAddress':  '$remoteIP',
    'targetNICResourceId':  '$targetNic'
}
"@
        
armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/ipFlowVerify?api-version=2016-12-01" $requestBody -verbose
```

## <a name="understanding-hello-results"></a>Présentation des résultats de hello

Hello réponse renvoyée indique si le trafic de hello est autorisé ou refusé. réponse de Hello ressemble à un des hello exemple suivant :

**Autorisé**

```json
{
  "access": "Allow",
  "ruleName": "defaultSecurityRules/AllowInternetOutBound"
}
```

**Refusé**

```json
{
  "access": "Deny",
  "ruleName": "defaultSecurityRules/DefaultInboundDenyAll"
}
```

## <a name="next-steps"></a>Étapes suivantes

Si le trafic est bloqué et ne doit pas être, consultez [gérer les groupes de sécurité réseau](../virtual-network/virtual-network-manage-nsg-arm-portal.md) toolearn plus d’informations sur les groupes de sécurité réseau.












