---
title: "AAA « variables d’environnement de nœud de calcul Azure Batch | Documents Microsoft »"
description: "Référence de variable d’environnement de nœud de calcul pour Azure Batch Analytics."
services: batch
author: tamram
manager: timlt
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 05/05/2017
ms.author: tamram
ms.openlocfilehash: 860f34b530579a81fbd5cf8ffa31df79d917c080
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-batch-compute-node-environment-variables"></a>Variables d’environnement de nœud de calcul Azure Batch
Hello [service Azure Batch](https://azure.microsoft.com/services/batch/) définit hello suivant des variables d’environnement sur les nœuds de calcul. Vous pouvez référencer ces variables d’environnement dans les lignes de commande de tâche et les programmes hello et les scripts exécutés par des lignes de commande hello.

Pour plus d’informations sur l’utilisation de variables d’environnement, voir [Paramètres d’environnement des tâches](https://docs.microsoft.com/azure/batch/batch-api-basics#environment-settings-for-tasks).

## <a name="environment-variable-visibility"></a>Visibilité des variables d’environnement

Ces variables d’environnement sont visibles uniquement dans un contexte de hello hello **utilisateur de la tâche**, hello du compte d’utilisateur sur le nœud hello sous lequel une tâche est exécutée. Vous allez *pas* consultez ces si vous [se connecter à distance](https://azure.microsoft.com/documentation/articles/batch-api-basics/#connecting-to-compute-nodes) tooa calcul nœud via le protocole RDP (Remote Desktop) ou Secure Shell (SSH) et liste de variables d’environnement hello. Il s’agit, car le compte d’utilisateur hello qui est utilisé pour la connexion à distance n’est pas hello compte hello qui est utilisé par la tâche hello.

## <a name="command-line-expansion-of-environment-variables"></a>Expansion par ligne de commande des variables d’environnement

les lignes de commande Hello exécutées par des tâches sur calcul nœuds s’exécute ne pas sous un interpréteur de commandes. Par conséquent, ces lignes de commande ne peuvent pas en mode natif parti des fonctionnalités du shell comme expansion de variables d’environnement (Cela inclut hello `PATH`). tootake parti de ces fonctionnalités, vous devez **appeler l’interpréteur de commandes hello** dans la ligne de commande hello. Par exemple, lancez `cmd.exe` sur des nœuds de calcul Windows ou `/bin/sh` sur des nœuds Linux :

`cmd /c MyTaskApplication.exe %MY_ENV_VAR%`

`/bin/sh -c MyTaskApplication $MY_ENV_VAR`

## <a name="environment-variables"></a>Variables d’environnement

| Nom de la variable                     | Description                                                              | Availability | Exemple |
|-----------------------------------|--------------------------------------------------------------------------|--------------|---------|
| AZ_BATCH_ACCOUNT_NAME           | nom Hello du compte de traitement par lots hello hello tâche appartient.                  | Toutes les tâches.   | mybatchaccount |
| AZ_BATCH_CERTIFICATES_DIR       | Un répertoire au sein de hello [répertoire de travail de tâche] [ files_dirs] dans les certificats qui sont stockées pour Linux des nœuds de calcul. Notez que cette variable d’environnement ne s’applique pas tooWindows les nœuds de calcul.                                                  | Toutes les tâches.   |  /mnt/batch/tasks/workitems/batchjob001/job-1/task001/certs |
| AZ_BATCH_JOB_ID                 | ID de Hello de tâche hello hello tâche appartient. | Toutes les tâches, sauf la tâche de démarrage. | batchjob001 |
| AZ_BATCH_JOB_PREP_DIR           | chemin d’accès complet de Hello de préparation du travail hello [répertoire tâches] [ files_dirs] sur le nœud de hello. | Toutes les tâches, sauf la tâche de démarrage et la tâche de préparation du travail. Disponible uniquement si le travail de hello est configuré avec une tâche de préparation du travail. | C:\user\tasks\workitems\jobprepreleasesamplejob\job-1\jobpreparation |
| AZ_BATCH_JOB_PREP_DIR   | chemin d’accès complet de Hello de préparation du travail hello [répertoire de travail de tâche] [ files_dirs] sur le nœud de hello. | Toutes les tâches, sauf la tâche de démarrage et la tâche de préparation du travail. Disponible uniquement si le travail de hello est configuré avec une tâche de préparation du travail. | C:\user\tasks\workitems\jobprepreleasesamplejob\job-1\jobpreparation\wd |
| AZ_BATCH_NODE_ID                | ID de Hello du nœud hello hello tâche est affecté à. | Toutes les tâches. | tvm-1219235766_3-20160919t172711z |
| AZ_BATCH_NODE_ROOT_DIR          | chemin d’accès complet de Hello de racine hello de tous les [lot répertoires] [ files_dirs] sur le nœud de hello. | Toutes les tâches. | C:\user\tasks |
| AZ_BATCH_NODE_ROOT_DIR        | chemin d’accès complet de Hello Hello [répertoire partagé] [ files_dirs] sur le nœud de hello. Toutes les tâches qui s’exécutent sur un nœud ont active de toothis d’accès en lecture/écriture. Les tâches qui s’exécutent sur d’autres nœuds ne disposent pas de répertoire de toothis d’accès à distance (il n’est pas un répertoire réseau « partagé »). | Toutes les tâches. | C:\user\tasks\shared |
| AZ_BATCH_NODE_STARTUP_DIR       | chemin d’accès complet de Hello Hello [répertoire de tâche de démarrage] [ files_dirs] sur le nœud de hello. | Toutes les tâches. | C:\user\tasks\startup |
| AZ_BATCH_POOL_ID                | ID Hello de pool hello hello tâche s’exécute sur. | Toutes les tâches. | batchpool001 |
| AZ_BATCH_TASK_DIR               | chemin d’accès complet de Hello Hello [répertoire tâches] [ files_dirs] sur le nœud de hello. Ce répertoire contient hello `stdout.txt` et `stderr.txt` pour la tâche hello et hello AZ_BATCH_TASK_WORKING_DIR. | Toutes les tâches. | C:\user\tasks\workitems\batchjob001\job-1\task001 |
| AZ_BATCH_TASK_ID                | Hello l’ID de tâche en cours de hello. | Toutes les tâches, sauf la tâche de démarrage. | task001 |
| AZ_BATCH_TASK_WORKING_DIR       | chemin d’accès complet de Hello Hello [répertoire de travail de tâche] [ files_dirs] sur le nœud de hello. Hello tâche en cours d’exécution a un répertoire de toothis d’accès en lecture/écriture. | Toutes les tâches. | C:\user\tasks\workitems\batchjob001\job-1\task001\wd |
| CCP_NODES                       | liste de Hello des nœuds et le nombre de cœurs par nœud allouées tooa [tâche d’instances multiples][multi_instance]. Nœuds et les cœurs sont répertoriées dans le format de hello`numNodes<space>node1IP<space>node1Cores<space>`<br/>`node2IP<space>node2Cores<space> ...`, où nombre hello de nœuds est suivie par une ou plusieurs adresses IP de nœud et nombre hello de cœurs pour chacun. |  Tâche principale multi-instance et tâches subordonnées. |`2 10.0.0.4 1 10.0.0.5 1` |
| AZ_BATCH_NODE_LIST              | Hello liste des nœuds qui sont alloués tooa [tâche d’instances multiples] [ multi_instance] au format de hello `nodeIP;nodeIP`. | Tâche principale multi-instance et tâches subordonnées. | `10.0.0.4;10.0.0.5` |
| AZ_BATCH_HOST_LIST              | Hello liste des nœuds qui sont alloués tooa [tâche d’instances multiples] [ multi_instance] au format de hello `nodeIP,nodeIP`. | Tâche principale multi-instance et tâches subordonnées. | `10.0.0.4,10.0.0.5` |
| AZ_BATCH_MASTER_NODE            | Hello adresse IP et port de hello nœud de calcul selon la tâche hello principal d’un [tâche d’instances multiples] [ multi_instance] s’exécute. | Tâche principale multi-instance et tâches subordonnées. | `10.0.0.4:6000`|
| AZ_BATCH_TASK_SHARED_DIR | Un chemin d’accès du répertoire qui est identique pour la tâche principale de hello et chaque sous-tâche d’un [tâche d’instances multiples][multi_instance]. Hello chemin existe sur chaque nœud sur lequel s’exécute de hello multi-instance tâche et est en lecture/écriture toohello accessible commandes de tâche en cours d’exécution sur ce nœud (les deux hello [commande de coordination] [ coord_cmd] et hello [commande application][app_cmd]). Tâches subordonnées ou une tâche principale qui s’exécutent sur d’autres nœuds n’ont pas de répertoire de toothis d’accès à distance (il n’est pas un répertoire réseau « partagé »). | Tâche principale multi-instance et tâches subordonnées. | C:\user\tasks\workitems\multiinstancesamplejob\job-1\multiinstancesampletask |
| AZ_BATCH_IS_CURRENT_NODE_MASTER | Spécifie si hello nœud en cours est hello maître pour un [tâche d’instances multiples][multi_instance]. Les valeurs possibles sont `true` et `false`.| Tâche principale multi-instance et tâches subordonnées. | `true` |
| AZ_BATCH_NODE_IS_DEDICATED | Si `true`, nœud en cours de hello est un nœud dédié. Si `false`, c’est un [nœud basse priorité](batch-low-pri-vms.md). | Toutes les tâches. | `true` |

[files_dirs]: https://azure.microsoft.com/documentation/articles/batch-api-basics/#files-and-directories
[multi_instance]: https://azure.microsoft.com/documentation/articles/batch-mpi/
[coord_cmd]: https://azure.microsoft.com/documentation/articles/batch-mpi/#coordination-command
[app_cmd]: https://azure.microsoft.com/documentation/articles/batch-mpi/#application-command
