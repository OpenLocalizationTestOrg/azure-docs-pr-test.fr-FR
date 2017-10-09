---
title: "planification de mise à jour corrective aaaConfigure du système d’exploitation pour les clusters HDInsight de basés sur Linux - Azure | Documents Microsoft"
description: "Découvrez comment les clusters de planification de mise à jour corrective tooconfigure du système d’exploitation pour HDInsight de basés sur Linux."
services: hdinsight
documentationcenter: 
author: bprakash
manager: asadk
editor: bprakash
ms.assetid: 
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/21/2017
ms.author: bhanupr
ms.openlocfilehash: 1598d64e594d7e8a68573fc63dd86051a5a9d025
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="os-patching-for-hdinsight"></a>Mise à jour corrective du système d’exploitation pour HDInsight 
Un service géré de Hadoop, HDInsight prend en charge de la mise à jour corrective hello du système d’exploitation de hello machines virtuelles sous-jacente utilisées par les clusters HDInsight. À compter du 1er août 2016, nous avons remplacé la stratégie mise à jour corrective de système d’exploitation invité hello pour les clusters HDInsight de basés sur Linux (version 3.4 ou supérieure). Hello nouvelle stratégie de hello vise toosignificantly réduire le nombre de hello de redémarrages toopatching échéance. nouvelle stratégie de Hello continue toopatch, machines virtuelles (VM) sur Linux clusters chaque lundi ou un jeudi commençant à 0 h 00 UTC, Universal Time de manière progressive s’effectue entre les nœuds dans un cluster donné. Toutefois, toutes les machines virtuelles donné redémarre uniquement au maximum une fois tous les 30 jours en raison de la mise à jour corrective tooguest du système d’exploitation. En outre, premier redémarrage de hello pour un cluster nouvellement créé ne se reproduira plus tôt plus de 30 jours à partir de la date de création de cluster hello. Correctifs sera effectives une fois que les machines virtuelles de hello sont redémarrés.

## <a name="how-tooconfigure-hello-os-patching-schedule-for-linux-based-hdinsight-clusters"></a>Comment tooconfigure hello planification de mise à jour corrective du système d’exploitation pour des clusters HDInsight de basés sur Linux
machines virtuelles de Hello dans un cluster HDInsight devez toobe redémarré occasionnellement afin que les correctifs de sécurité importantes peuvent être installés. À compter du 1er août 2016, les nouveaux clusters HDInsight de basés sur Linux (version 3.4 ou supérieure,) sont redémarrés à l’aide de hello suivant planification :

1. Une machine virtuelle dans un cluster de hello peuvent uniquement redémarrer les correctifs au maximum, une seule fois dans un délai de 30 jours.
2. redémarrage de Hello se produit en commençant à 0 h 00 UTC.
3. processus de redémarrage Hello est échelonnée entre les machines virtuelles dans un cluster de hello, cluster de hello est toujours disponible pendant le processus de redémarrage hello.
4. redémarrage de première Hello pour un cluster nouvellement créé ne se reproduira plus tôt plus de 30 jours après la date de création de cluster hello.

À l’aide d’action de script hello décrite dans cet article, vous pouvez modifier planification de mise à jour corrective hello du système d’exploitation comme suit :
1. Activez ou désactivez les redémarrages automatiques.
2. Fréquence de hello du jeu de redémarrage (en jours entre les redémarrages)
3. Définissez le jour de semaine hello lorsqu’un redémarrage se produit hello

> [!NOTE]
> Cette action de script fonctionne uniquement avec les clusters HDInsight sous Linux créés après le 1er août 2016. Les correctifs seront appliqués une fois les machines virtuelles redémarrées. 
>

## <a name="how-toouse-hello-script"></a>Comment toouse hello script 

Lorsque ce script nécessite hello informations suivantes :
1. emplacement du script de Hello : https://hdiconfigactions.blob.core.windows.net/linuxospatchingrebootconfigv01/os-patching-reboot-config.sh.  HDInsight utilise cette toofind URI et exécuter le script de hello sur tous les ordinateurs virtuels hello dans un cluster de hello.
  
2. Hello des types de nœuds de cluster appliquée au script de hello : nœud principal, workernode, soigneur. Ce script doit être appliqué tooall des types de nœuds dans un cluster de hello. Si elle n’est pas appliqué tooa nœud type, puis hello virtuel machines pour ce type de nœud continuera de planification de mise à jour corrective précédente toouse hello.


3.  Paramètre : ce script accepte trois paramètres numériques :

    | Paramètre | Définition |
    | --- | --- |
    | Activation ou désactivation des redémarrages automatiques |0 ou 1. La valeur 0 désactive les redémarrages automatiques et la valeur 1 les active. |
    | Fréquence |too90 7 (inclus). nombre de Hello de toowait jours avant le redémarrage des machines virtuelles hello correctifs nécessitant un redémarrage. |
    | Jour de semaine |1 too7 (inclus). La valeur 1 indique le redémarrage de hello doit se produire sur un lundi et 7 indique un exemple Sunday.For, à l’aide des paramètres de 1 60 2 entraîne automatique redémarre tous les 60 jours (au plus) mardi. |
    | Persistance |Lorsque vous appliquez un cluster existant de script action tooan, vous pouvez marquer les script hello si elle est persistante. Scripts persistantes sont appliquées lorsque workernodes nouvelles sont ajoutées cluster toohello via les opérations de mise à l’échelle. |

> [!NOTE]
> Vous devez marquer ce script si elle est persistante lors de l’application de cluster de tooan existant. Dans le cas contraire, de nouveaux nœuds créés via la mise à l’échelle des opérations utilise par défaut de hello planification de mise à jour corrective.
Si vous appliquez le script de hello dans le cadre du processus de création de cluster hello, il est conservé automatiquement.
>

## <a name="next-steps"></a>Étapes suivantes

Pour les étapes spécifiques sur l’utilisation d’action de script hello, consultez hello les sections Bonjour suivantes [HDInsight de basée sur Linuz de personnaliser des clusters à l’aide d’action de script](hdinsight-hadoop-customize-cluster-linux.md):

* [Utiliser une action de script lors de la création du cluster](hdinsight-hadoop-customize-cluster-linux.md#use-a-script-action-during-cluster-creation)
* [Appliquer un tooa d’action de script en cours d’exécution cluster](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster)
