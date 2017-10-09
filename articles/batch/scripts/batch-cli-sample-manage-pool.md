---
title: aaaAzure exemple de Script CLI - gestion de Pools dans le traitement par lots | Documents Microsoft
description: Exemple de script CLI Azure - Gestion de pools dans Batch
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
ms.openlocfilehash: 6c9ca9515565aff42752231a080943be8e4c810b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-batch-pools-with-azure-cli"></a>Gérer des pools Azure Batch avec l’interface CLI Azure

Ces script présente quelques-unes des outils de hello disponibles dans hello CLI d’Azure toocreate et gérer les pools de nœuds de calcul dans le service de traitement par lots Azure hello.

> [!NOTE]
> commandes de Hello dans cet exemple créent des machines virtuelles. Machines virtuelles s’exécutant provisionner le compte de frais tooyour. toominimize ces frais et supprimer des machines virtuelles de hello une fois que vous avez terminé les exemple hello en cours d’exécution. Consultez la page [Nettoyer les pools](#clean-up-pools).

Les pools Batch peuvent être configurés de deux manières, soit via une configuration de Services cloud (Windows uniquement), soit via une configuration de machine virtuelle (Windows et Linux). Hello exemples de scripts ci-dessous montrent comment toocreate regroupe avec les deux configurations.

## <a name="prerequisites"></a>Composants requis

- Installation hello CLI d’Azure à l’aide d’instructions hello de hello [guide d’installation Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli), si vous n’avez pas déjà fait.
- Créez un compte Azure si vous n’en avez pas. Consultez [créer un compte de traitement par lots avec hello CLI d’Azure](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) pour un exemple de script qui crée un compte.
- Configurer un toorun d’application à partir d’une tâche de démarrage si vous n’avez pas encore fait. Consultez [Ajout d’applications tooAzure lot avec Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-add-application) pour un exemple de script qui crée une application et télécharge un tooAzure de package d’application.

## <a name="pool-with-cloud-service-configuration-sample-script"></a>Pool avec exemple de script pour la configuration du service cloud

[!code-azurecli[main](../../../cli_scripts/batch/manage-pool/manage-pool-windows.sh "Manage Cloud Services Pools")]

## <a name="pool-with-virtual-machine-configuration-sample-script"></a>Pool avec exemple de script pour la configuration de machine virtuelle

[!code-azurecli[main](../../../cli_scripts/batch/manage-pool/manage-pool-linux.sh "Manage Virtual Machine Pools")]

## <a name="clean-up-pools"></a>Nettoyer les pools

Après avoir exécuté hello ci-dessus un exemple de script, exécutez hello suivant des pools de commande toodelete hello.
```azurecli
az batch pool delete --pool-id mypool-windows
az batch pool delete --pool-id mypool-linux
```

## <a name="script-explanation"></a>Explication du script

Ce script utilise hello suivant toocreate de commandes et de manipuler les pools de lot.
Chaque commande dans la table de hello lie documentation toocommand spécifique.

| Commande | Remarques |
|---|---|
| [az batch account login](https://docs.microsoft.com/cli/azure/batch/account#login) | Permet de s’authentifier avec un compte Batch.  |
| [az batch application summary list](https://docs.microsoft.com/cli/azure/batch/application/summary#list) | Répertorier les applications disponibles de hello Bonjour compte Batch.  |
| [az batch pool create](https://docs.microsoft.com/cli/azure/batch/pool#create) | Permet de créer un pool de machines virtuelles.  |
| [az batch pool set](https://docs.microsoft.com/cli/azure/batch/pool#set) | Permet de mettre à jour les propriétés d’un pool.  |
| [az batch pool node-agent-skus list](https://docs.microsoft.com/cli/azure/batch/pool/node-agent-skus#list) | Permet de répertorier les SKU de l’agent de nœud et les informations de l’image.  |
| [az batch pool resize](https://docs.microsoft.com/cli/azure/batch/pool#resize) | Nombre de hello de redimensionnement de machines virtuelles s’exécutant dans hello spécifié de pool.  |
| [az batch pool show](https://docs.microsoft.com/cli/azure/batch/pool#show) | Afficher les propriétés de hello d’un pool.  |
| [az batch pool delete](https://docs.microsoft.com/cli/azure/batch/pool#delete) | Supprimer hello spécifié pool.  |
| [az batch pool autoscale enable](https://docs.microsoft.com/cli/azure/batch/pool/autoscale#enable) | Permet d’activer la mise à l’échelle automatique sur un pool et d’appliquer une formule.  |
| [az batch pool autoscale disable](https://docs.microsoft.com/cli/azure/batch/pool/autoscale#disable) | Permet de désactiver la mise à l’échelle automatique sur un pool.  |
| [az batch node list](https://docs.microsoft.com/cli/azure/batch/node#list) | Liste de tous les de nœud de calcul hello Bonjour spécifié de pool.  |
| [az batch node reboot](https://docs.microsoft.com/cli/azure/batch/node#reboot) | Redémarrer le nœud de calcul spécifié hello.  |
| [az batch node delete](https://docs.microsoft.com/cli/azure/batch/node#delete) | Supprimer des nœuds de hello répertorié de hello spécifié pool.  |

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur hello CLI d’Azure, consultez [documentation relative à Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Vous trouverez des exemples supplémentaires de script CLI de lot Bonjour [documentation d’Azure Batch CLI](../batch-cli-samples.md).

