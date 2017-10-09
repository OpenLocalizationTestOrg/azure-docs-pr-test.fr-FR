---
title: "aaaAzure exemple de Script CLI - exécutez un travail de traitement par lots | Documents Microsoft"
description: "Exemple de script Azure CLI : exécution d’un travail avec Batch"
services: batch
documentationcenter: 
author: annatisch
manager: daryls
editor: tysonn
ms.assetid: 
ms.service: batch
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/02/2017
ms.author: antisch
ms.openlocfilehash: f73a7cb341e550fd1c92f92201e20b27fa20d238
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="running-jobs-on-azure-batch-with-azure-cli"></a>Exécution de travaux sur Azure Batch avec l’interface Azure CLI

Ce script crée une tâche de traitement par lots et ajoute une série de travail toohello de tâches. Il montre également comment toomonitor une tâche et ses tâches. Enfin, il montre comment tooquery hello service Batch efficacement pour plus d’informations sur les tâches du travail hello.

## <a name="prerequisites"></a>Composants requis

- Installation hello CLI d’Azure à l’aide d’instructions hello de hello [guide d’installation Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli), si vous n’avez pas déjà fait.
- Créez un compte Azure si vous n’en avez pas. Consultez [créer un compte de traitement par lots avec hello CLI d’Azure](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) pour un exemple de script qui crée un compte.
- Configurer un toorun d’application à partir d’une tâche de démarrage si vous n’avez pas encore fait. Consultez [Ajout d’applications tooAzure lot avec Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-add-application) pour un exemple de script qui crée une application et télécharge un tooAzure de package d’application.
- Configurer un pool d’exécution de la tâche sur le hello. Pour un exemple de script qui crée un pool avec une configuration de service cloud ou une configuration de machine virtuelle, voir [Gérer des pools Azure Batch avec CLI Azure](https://docs.microsoft.com/azure/batch/batch-cli-sample-manage-pool).

## <a name="sample-script"></a>Exemple de script

[!code-azurecli[main](../../../cli_scripts/batch/run-job/run-job.sh "Run Job")]

## <a name="clean-up-job"></a>Travail de nettoyage

Après avoir exécuté hello ci-dessus un exemple de script, exécutez hello suivant commande tooremove le travail et toutes ses tâches. Notez que le pool de hello devez toobe supprimée séparément. Pour plus d’informations sur la création et la suppression de pools, voir [Gérer des pools Azure Batch avec CLI Azure](./batch-cli-sample-manage-pool.md).

```azurecli
az batch job delete --job-id myjob
```

## <a name="script-explanation"></a>Explication du script

Ce script utilise hello suivant de commandes toocreate un traitement par lots et les tâches. Chaque commande dans la table de hello lie documentation toocommand spécifique.

| Commande | Remarques |
|---|---|
| [az batch account login](https://docs.microsoft.com/cli/azure/batch/account#login) | Permet de s’authentifier avec un compte Batch.  |
| [az batch job create](https://docs.microsoft.com/cli/azure/batch/job#create) | Crée un travail Batch.  |
| [az batch job set](https://docs.microsoft.com/cli/azure/batch/job#set) | Met à jour les propriétés d’un travail Batch.  |
| [az batch job show](https://docs.microsoft.com/cli/azure/batch/job#show) | Récupère les détails relatifs au travail Batch spécifié.  |
| [az batch task create](https://docs.microsoft.com/cli/azure/batch/task#create) | Ajoute qu'un toohello de la tâche spécifiée par lots.  |
| [az batch task show](https://docs.microsoft.com/cli/azure/batch/task#show) | Récupère les détails de hello d’une tâche à partir de hello spécifié par lots.  |
| [az batch task list](https://docs.microsoft.com/cli/azure/batch/task#list) | Répertorie les tâches hello associés au travail spécifié de hello.  |

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur hello CLI d’Azure, consultez [documentation relative à Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Vous trouverez des exemples supplémentaires de script CLI de lot Bonjour [documentation d’Azure Batch CLI](../batch-cli-samples.md).
