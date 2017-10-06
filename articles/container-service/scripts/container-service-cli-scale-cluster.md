---
title: "aaaAzure exemple de Script CLI - mise à l’échelle un Cluster ACS | Documents Microsoft"
description: "Exemple de script Azure CLI - Mettre à l’échelle un cluster ACS"
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Docker, conteneurs, micro-services, Kubernetes, DC/OS, Azure
ms.assetid: 
ms.service: container-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/30/2017
ms.author: nepeters
ms.openlocfilehash: b1c214d7cca615257ec8cd6e9993cd15f694289b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="scale-an-azure-container-service-cluster"></a>Mettre à l’échelle un cluster Azure Container Service

Cet exemple met à l’échelle un environnement Azure Container Service. 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Exemple de script

```azurecli
az acs scale --resource-group myResourceGroup --name myK8SCluster --new-agent-count 5
```

## <a name="clean-up-deployment"></a>Nettoyer le déploiement 

Exécutez hello suivant du groupe de ressources de commande tooremove hello, machine virtuelle et toutes les ressources.

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>Explication du script

Ce script utilise hello après le déploiement de commandes toocreate hello. Chaque élément de la documentation spécifique du toocommand liens table hello.

| Commande | Remarques |
|---|---|
| [az acs scale](/cli/azure/acs#scale) | Met à l’échelle un cluster ACS. |

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur hello CLI d’Azure, consultez [documentation relative à Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Vous trouverez des exemples supplémentaires de script CLI de Service de conteneur Azure Bonjour [documentation sur le Service de conteneur Azure](../cli-samples.md).

