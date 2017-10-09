---
title: "vérification de tooconnectivity aaaIntroduction dans l’Observateur réseau de Azure | Documents Microsoft"
description: "Cette page fournit une vue d’ensemble de hello capacités de connectivité de l’Observateur réseau"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/11/2017
ms.author: gwallace
ms.openlocfilehash: 52fc4547f167cea2992a046859dc0550d136e80d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooconnectivity-check-in-azure-network-watcher"></a>Vérification de tooconnectivity de présentation dans l’Observateur réseau de Azure

Hello fonctionnalité de connectivité de l’Observateur réseau fournit hello fonctionnalité toocheck une connexion TCP directe à partir d’un ordinateur virtuel tooa ordinateur virtuel (VM), le nom de domaine complet (FQDN), un URI ou l’adresse IPv4. Les scénarios de réseau sont complexes. Ils sont implémentés à l’aide de groupes de sécurité réseau, de pare-feu, d’itinéraires définis par l’utilisateur et de ressources fournies par Azure. Ces configurations complexes rendent difficile la résolution des problèmes de connectivité. Observateur réseau permet de réduire hello toofind de temps et de détecter les problèmes de connectivité. résultats Hello retournés des informations des si un problème de connectivité est tooa plateforme ou d’un problème de configuration utilisateur. La connectivité peut être vérifiée avec [PowerShell](network-watcher-connectivity-powershell.md), [Azure CLI](network-watcher-connectivity-cli.md) et l’[API REST](network-watcher-connectivity-rest.md).

> [!IMPORTANT]
> La vérification de la connectivité requiert une extension de machine virtuelle `AzureNetworkWatcherExtension`. Pour installer l’extension de hello sur une machine virtuelle Windows, visitez [extension de machine virtuelle d’Agent de l’Observateur réseau Azure pour Windows](../virtual-machines/windows/extensions-nwa.md) et de, visitez Linux VM [extension de machine virtuelle Azure réseau Observateur Agent pour Linux](../virtual-machines/linux/extensions-nwa.md).

## <a name="response"></a>Réponse

Hello tableau suivant présente les propriétés de hello retournées lorsqu’une vérification de la connectivité est terminée.

|Propriété  |Description  |
|---------|---------|
|ConnectionStatus     | état de Hello de vérification de la connectivité hello. Les résultats possibles sont **Joignable** et **Inaccessible**.        |
|AvgLatencyInMs     | Latence moyenne au cours de la vérification de la connectivité hello en millisecondes. (affichée uniquement si l’état de la vérification est Joignable).        |
|MinLatencyInMs     | Latence minimale au cours de la connectivité de hello vérifier en millisecondes. (affichée uniquement si l’état de la vérification est Joignable).        |
|MaxLatencyInMs     | Vérification de la latence maximale au cours de la connectivité de hello en millisecondes. (affichée uniquement si l’état de la vérification est Joignable).        |
|ProbesSent     | Nombre de sondes envoyées lors de la vérification de hello. La valeur maximale est de 100.        |
|ProbesFailed     | Nombre de sondes a échoué lors de la vérification de hello. La valeur maximale est de 100.        |
|Hops     | Saut par chemin d’accès de saut à partir de la source toodestination.        |
|Hops[].Type     | Type de ressource. Les valeurs possibles sont **Source**, **VirtualAppliance**, **VnetLocal**, et **Internet**.        |
|Hops[].Id | Identificateur unique du tronçon de hello.|
|Hops[].Address | Adresse IP du tronçon de hello.|
|Hops[].ResourceId | ID de ressource du saut hello si tronçon de hello est une ressource Azure. S’il s’agit d’une ressource internet, l’ID de ressource est **Internet**. |
|Hops[].NextHopIds | Identificateur unique de Hello du tronçon suivant de hello prise.|
|Hops[].Issues | Collection des problèmes qui se sont produites lors de la vérification de hello à ce saut. S’il n’y a aucun problème, la valeur de hello est vide.|
|Hops[].Issues[].Origin | Tronçon actuel de hello, où le problème s’est produit. Les valeurs possibles sont les suivantes :<br/> **Trafic entrant** -problème se trouve sur le lien hello hello précédente saut toohello actuel saut<br/>**Sortant** -problème se trouve sur le lien hello de tronçon suivant hello actuel saut toohello<br/>**Local** -problème se trouve sur le tronçon d’actuel hello.|
|Hops[].Issues[].Severity | niveau de gravité Hello du problème hello détecté. Les valeurs possibles sont **Error** et **Warning**. |
|Hops[].Issues[].Type |type de Hello du problème détecté. Les valeurs possibles sont les suivantes : <br/>**UC**<br/>**Mémoire**<br/>**GuestFirewall**<br/>**DnsResolution**<br/>**NetworkSecurityRule**<br/>**UserDefinedRoute** |
|Hops[].Issues[].Context |Détails concernant le problème hello trouvé.|
|Hops[].Issues[].Context[].key |Clé de hello paire clé / valeur retournée.|
|Hops[].Issues[].Context[].value |Valeur de hello paire clé / valeur retournée.|

Hello Voici un exemple d’un problème détecté sur un saut.

```json
"Issues": [
    {
        "Origin": "Outbound",
        "Severity": "Error",
        "Type": "NetworkSecurityRule",
        "Context": [
            {
                "key": "RuleName",
                "value": "UserRule_Port80"
            }
        ]
    }
]
```
## <a name="fault-types"></a>Types d’erreur

vérification de la connectivité Hello retourne des types d’erreur sur la connexion de hello. Hello tableau suivant fournit une liste de types hello actuels erreur retournée.

|Type  |Description  |
|---------|---------|
|UC     | Utilisation élevée du processeur.       |
|Mémoire     | Utilisation élevée de la mémoire.       |
|GuestFirewall     | Le trafic est bloqué en raison de la configuration du pare-feu tooa machine virtuelle.        |
|DNSResolution     | Échec de la résolution DNS pour l’adresse de destination hello.        |
|NetworkSecurityRule    | Le trafic est bloqué par une règle de groupe de sécurité réseau (règle retournée)        |
|UserDefinedRoute|Trafic est abandonné dû tooa défini par l’utilisateur ou l’itinéraire du système. |

### <a name="next-steps"></a>Étapes suivantes

En savoir plus la ressource de connectivité de tooverify tooa en visitant le site : [vérifier la connectivité à l’aide de l’Observateur de réseau Azure](network-watcher-connectivity-powershell.md).

<!--Image references-->
[1]: ./media/network-watcher-next-hop-overview/figure1.png

