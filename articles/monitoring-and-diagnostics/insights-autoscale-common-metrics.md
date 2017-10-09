---
title: "aaaAzure mesures courantes de mise à l’échelle de moniteur | Documents Microsoft"
description: "Découvrez les métriques utilisées pour la mise à l’échelle automatique de vos instances Cloud Services, Virtual Machines et Web Apps."
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 189b2a13-01c8-4aca-afd5-90711903ca59
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/6/2016
ms.author: ancav
ms.openlocfilehash: 372a40d72d7a6c22c5ff854b1460ec8a3b7ed1d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-monitor-autoscaling-common-metrics"></a>Métriques courantes pour la mise à l’échelle automatique d’Azure Monitor
Échelle d’analyse Azure permet vous tooscale hello nombre d’instances en cours d’exécution vers le haut ou vers le bas, en fonction des données de télémétrie (mesures). Ce document décrit les mesures courantes que vous pourriez toouse. Bonjour portail Azure pour les Services de cloud computing et des batteries de serveurs, vous pouvez choisir métrique tooscale de ressource hello en hello. Toutefois, vous pouvez également choisir les mesures à partir d’un tooscale de ressources différent par.

Mise à l’échelle du moniteur Azure s’applique uniquement trop[machines virtuelles identiques](https://azure.microsoft.com/services/virtual-machine-scale-sets/), [Services de cloud computing](https://azure.microsoft.com/services/cloud-services/), et [du Service d’applications - applications Web](https://azure.microsoft.com/services/app-service/web/). Les autres services Azure utilisent des méthodes de mise à l’échelle différentes.

## <a name="compute-metrics-for-resource-manager-based-vms"></a>Calcul des métriques pour les machines virtuelles basées sur Resource Manager
Par défaut, les machines virtuelles et jeux de mise à l’échelle de machine virtuelle basés sur Resource Manager émettent des métriques de base (niveau hôte). En outre, lorsque vous configurez la collecte de données de diagnostic pour une machine virtuelle Azure et la mise, hello extension de diagnostic Azure émet également les compteurs de performances du système d’exploitation invité (communément appelées « Mesures de système d’exploitation invité »).  Vous utilisez toutes ces métriques dans les règles de mise à l’échelle automatique.

Vous pouvez utiliser hello `Get MetricDefinitions` métriques de hello PoSH/API/CLI tooview disponibles pour votre ressource mise.

Si vous utilisez des jeux de mise à l’échelle de machine virtuelle et qu’une métrique que vous cherchez n’est pas répertoriée, il est probable qu’elle soit *désactivée* dans votre extension de diagnostics.

Si une mesure particulière n’est pas en cours hello échantillonnées ou transféré à fréquence vous, vous pouvez mettre à jour de configuration des diagnostics hello.

Si les deux cas précédents est true, puis examinez [tooenable utiliser PowerShell Diagnostics Azure dans une machine virtuelle exécutant Windows](../virtual-machines/windows/ps-extensions-diagnostics.md) sur PowerShell tooconfigure et mettre à jour votre tooenable d’extension de Diagnostics de machine virtuelle Windows Azure hello métrique. Cet article inclut également un exemple de fichier de configuration de diagnostics.

### <a name="host-metrics-for-resource-manager-based-windows-and-linux-vms"></a>Métriques de l’hôte pour les machines virtuelles Windows et Linux basées sur Resource Manager
Hello suivant métriques au niveau de l’hôte est émis par défaut pour la machine virtuelle Azure et mise dans les instances de Windows et Linux. Ces métriques de décrivent votre machine virtuelle Azure, mais sont collectés à partir de l’hôte de machine virtuelle Azure hello plutôt que via l’agent installé sur l’ordinateur virtuel invité de hello. Vous pouvez utiliser ces métriques dans les règles de mise à l’échelle automatique.

- [Métriques de l’hôte pour les machines virtuelles Windows et Linux basées sur Resource Manager](monitoring-supported-metrics.md#microsoftcomputevirtualmachines)
- [Métriques de l’hôte pour les jeux de mise à l’échelle de machine virtuelle Windows et Linux basées sur Resource Manager](monitoring-supported-metrics.md#microsoftcomputevirtualmachinescalesets)

### <a name="guest-os-metrics-resource-manager-based-windows-vms"></a>Métriques de SE invité pour machines virtuelles Windows basées sur Resource Manager
Lorsque vous créez une machine virtuelle dans Azure, des diagnostics est activée à l’aide d’extension de Diagnostics hello. extension de diagnostics Hello émet un ensemble de mesures extraite à l’intérieur de hello machine virtuelle. Cela signifie que vous pouvez automatiser la mise à l’échelle des métriques qui ne sont pas émises par défaut.

Vous pouvez générer une liste des mesures de hello à l’aide de hello commande dans PowerShell suivante.

```
Get-AzureRmMetricDefinition -ResourceId <resource_id> | Format-Table -Property Name,Unit
```

Vous pouvez créer une alerte pour hello suivant des métriques :

| Nom de métrique | Unité |
| --- | --- |
| \Processor(_Total)\% temps processeur |Pourcentage |
| \Processor(_Total)\\% temps privilégié |Pourcentage |
| \Processor(_Total)\\% temps utilisateur |Pourcentage |
| \Processor Information(_Total)\Fréquence du processeur |Nombre |
| \System\Processus |Nombre |
| \Process(_Total)\Nombre de threads |Nombre |
| \Process(_Total)\Nombre de handles |Nombre |
| \Memory\\% octets validés en cours d’utilisation |Pourcentage |
| \Memory\Octets disponibles |Octets |
| \Memory\Octets validés |Octets |
| \Memory\Limite de mémoire dédiée |Octets |
| \Memory\Octets de réserve paginée |Octets |
| \Memory\Octets de réserve non paginée |Octets |
| \PhysicalDisk(_Total)\\% temps disque |Pourcentage |
| \PhysicalDisk(_Total)\\% temps de lecture du disque |Pourcentage |
| \PhysicalDisk(_Total)\\% temps écriture du disque |Pourcentage |
| \PhysicalDisk(_Total)\Disk Transfers/sec |Nombre par seconde |
| \PhysicalDisk(_Total)\Lectures disque/s |Nombre par seconde |
| \PhysicalDisk(_Total)\Écritures disque/s |Nombre par seconde |
| \PhysicalDisk(_Total)\Octets disque/s |Octets par seconde |
| \PhysicalDisk(_Total)\Lectures disque, octets/s |Octets par seconde |
| \PhysicalDisk(_Total)\Écritures disque, octets/s |Octets par seconde |
| \PhysicalDisk(_Total)\Longueur moyenne Longueur de file d'attente de disque |Nombre |
| \PhysicalDisk(_Total)\Longueur moyenne de file d’attente lecture disque |Nombre |
| \PhysicalDisk(_Total)\Longueur moyenne de file d’attente écriture disque |Nombre |
| \LogicalDisk(_Total)\\% espace libre |Pourcentage |
| \LogicalDisk(_Total)\Mégaoctets libres |Nombre |

### <a name="guest-os-metrics-linux-vms"></a>Métriques de SE invité pour les machines virtuelles Linux
Lorsque vous créez une machine virtuelle dans Azure, les diagnostics sont activés par défaut grâce à l’extension Diagnostics.

Vous pouvez générer une liste des mesures de hello à l’aide de hello commande dans PowerShell suivante.

```
Get-AzureRmMetricDefinition -ResourceId <resource_id> | Format-Table -Property Name,Unit
```

 Vous pouvez créer une alerte pour hello suivant des métriques :

| Nom de métrique | Unité |
| --- | --- |
| \Mémoire\Mémoire disponible |Octets |
| \Mémoire\Pourcentage de mémoire disponible |Pourcentage |
| \Mémoire\Mémoire utilisée |Octets |
| \Mémoire\Pourcentage de mémoire utilisée |Pourcentage |
| \Mémoire\Pourcentage de mémoire utilisée par le cache |Pourcentage |
| \Mémoire\Pages par seconde |Nombre par seconde |
| \Mémoire\Pages lues par seconde |Nombre par seconde |
| \Mémoire\Pages écrites par seconde |Nombre par seconde |
| \Mémoire\Échanges disponibles |Octets |
| \Mémoire\Pourcentage d’échanges disponibles |Pourcentage |
| \Mémoire\Échanges utilisés |Octets |
| \Mémoire\Pourcentage d’échanges utilisés |Pourcentage |
| \Processeur\Pourcentage de temps d’inactivité |Pourcentage |
| \Processeur\Pourcentage de temps d’utilisateur |Pourcentage |
| \Processeur\Pourcentage de temps d’efficacité |Pourcentage |
| \Processeur\Pourcentage de temps privilégié |Pourcentage |
| \Processeur\Pourcentage de temps d’interruption |Pourcentage |
| \Processeur\Pourcentage de temps d’appels de procédure différés (DPC) |Pourcentage |
| \Processeur\Pourcentage de temps de processeur |Pourcentage |
| \Processeur\Pourcentage de temps d’attente |Pourcentage |
| \Disque physique\Octets par seconde |Octets par seconde |
| \Disque physique\Octets lus par seconde |Octets par seconde |
| \Disque physique\Octets écrits par seconde |Octets par seconde |
| \Disque physique\Transferts par seconde |Nombre par seconde |
| \Disque physique\Lectures par seconde |Nombre par seconde |
| \Disque physique\Écritures par seconde |Nombre par seconde |
| \Disque physique\Temps de lecture moyen |Secondes |
| \Disque physique\Temps d’écriture moyen |Secondes |
| \Disque physique\Temps de transfert moyen |Secondes |
| \Disque physique\Longueur moyenne de la file d’attente du disque |Nombre |
| \Interface réseau\Octets transmis |Octets |
| \Interface réseau\Octets reçus |Octets |
| \Interface réseau\Paquets transmis |Nombre |
| \Interface réseau\Paquets reçus |Nombre |
| \Interface réseau\Total des octets |Octets |
| \Interface réseau\Total des erreurs Rx |Nombre |
| \Interface réseau\Total des erreurs Tx |Nombre |
| \Interface réseau\Total des collisions |Nombre |

## <a name="commonly-used-web-server-farm-metrics"></a>Métriques web couramment utilisées (batterie de serveurs)
Vous pouvez également effectuer la mise à l’échelle en fonction des métriques de serveur web courantes telles que hello longueur de file d’attente Http. Son nom de métrique est **Longueur de file d’attente HTTP**.  Hello suivant des métriques de batterie de serveurs (applications Web) section listes disponible sur le serveur.

### <a name="web-apps-metrics"></a>Métriques Web Apps
Vous pouvez générer une liste des mesures d’applications Web hello à l’aide de hello commande dans PowerShell suivante.

```
Get-AzureRmMetricDefinition -ResourceId <resource_id> | Format-Table -Property Name,Unit
```

Ces métriques permettent d’émettre une alerte ou de procéder à un mise à l’échelle.

| Nom de métrique | Unité |
| --- | --- |
| Pourcentage UC |Pourcentage |
| Pourcentage mémoire |Pourcentage |
| Longueur de file d’attente du disque |Nombre |
| Longueur de file d’attente HTTP |Nombre |
| Octets reçus |Octets |
| Octets envoyés |Octets |

## <a name="commonly-used-storage-metrics"></a>Métriques couramment utilisées dans Azure Storage
Vous pouvez faire évoluer par la longueur de file d’attente de stockage, qui est le nombre de hello de messages dans la file d’attente de stockage hello. Longueur de file d’attente de stockage est une mesure particulière et seuil de hello est nombre hello de messages par instance. Par exemple, s’il existe deux instances, et si le seuil de hello a la valeur too100, mise à l’échelle se produit lorsque hello le nombre total de messages dans la file d’attente hello est 200. Qui peut être de 100 messages par instance, 120 et 80 ou toute autre combinaison additionne too200 ou plus.

Configurez ce paramètre Bonjour Azure portal Bonjour **paramètres** panneau. Pour les jeux de mise à l’échelle de machine virtuelle, vous pouvez mettre à jour des paramètres de mise à l’échelle hello hello Gestionnaire de ressources du modèle toouse *metricName* en tant que *ApproximateMessageCount* et passer l’ID de file d’attente de stockage hello comme hello  *metricResourceUri*.

Par exemple, avec un Bonjour du compte de stockage classique metricTrigger de paramètre de mise à l’échelle inclut :

```
"metricName": "ApproximateMessageCount",
 "metricNamespace": "",
 "metricResourceUri": "/subscriptions/SUBSCRIPTION_ID/resourceGroups/RES_GROUP_NAME/providers/Microsoft.ClassicStorage/storageAccounts/STORAGE_ACCOUNT_NAME/services/queue/queues/QUEUE_NAME"
 ```

Pour un compte de stockage de (non classique), hello metricTrigger incluent :

```
"metricName": "ApproximateMessageCount",
"metricNamespace": "",
"metricResourceUri": "/subscriptions/SUBSCRIPTION_ID/resourceGroups/RES_GROUP_NAME/providers/Microsoft.Storage/storageAccounts/STORAGE_ACCOUNT_NAME/services/queue/queues/QUEUE_NAME"
```

## <a name="commonly-used-service-bus-metrics"></a>Métriques Service Bus généralement utilisées
Vous pouvez faire évoluer par la longueur de file d’attente Service Bus, numéro hello de messages dans la file d’attente du Service Bus hello. Longueur de file d’attente Service Bus est une mesure particulière et seuil de hello est nombre hello de messages par instance. Par exemple, s’il existe deux instances, et si le seuil de hello a la valeur too100, mise à l’échelle se produit lorsque hello le nombre total de messages dans la file d’attente hello est 200. Qui peut être de 100 messages par instance, 120 et 80 ou toute autre combinaison additionne too200 ou plus.

Pour les jeux de mise à l’échelle de machine virtuelle, vous pouvez mettre à jour des paramètres de mise à l’échelle hello hello Gestionnaire de ressources du modèle toouse *metricName* en tant que *ApproximateMessageCount* et passer l’ID de file d’attente de stockage hello comme hello  *metricResourceUri*.

```
"metricName": "MessageCount",
 "metricNamespace": "",
"metricResourceUri": "/subscriptions/SUBSCRIPTION_ID/resourceGroups/RES_GROUP_NAME/providers/Microsoft.ServiceBus/namespaces/SB_NAMESPACE/queues/QUEUE_NAME"
```

> [!NOTE]
> Bus des services, concept de groupe de ressources hello n’existe pas, mais Azure Resource Manager crée un groupe de ressources par défaut par région. groupe de ressources Hello est généralement au format de 'Default - ServiceBus-[Région]' hello. Par exemple, « Est des États-Unis Service Bus par défaut », « Ouest des États-Unis Service Bus par défaut », « Est de l’Australie Service Bus par défaut », etc.
>
>
