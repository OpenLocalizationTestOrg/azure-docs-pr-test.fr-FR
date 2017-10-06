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
# <a name="scale-an-azure-container-service-cluster"></a><span data-ttu-id="2916e-104">Mettre à l’échelle un cluster Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="2916e-104">Scale an Azure Container Service Cluster</span></span>

<span data-ttu-id="2916e-105">Cet exemple met à l’échelle un environnement Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="2916e-105">This sample scales and Azure Container Service.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="2916e-106">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="2916e-106">Sample script</span></span>

```azurecli
az acs scale --resource-group myResourceGroup --name myK8SCluster --new-agent-count 5
```

## <a name="clean-up-deployment"></a><span data-ttu-id="2916e-107">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="2916e-107">Clean up deployment</span></span> 

<span data-ttu-id="2916e-108">Exécutez hello suivant du groupe de ressources de commande tooremove hello, machine virtuelle et toutes les ressources.</span><span class="sxs-lookup"><span data-stu-id="2916e-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="2916e-109">Explication du script</span><span class="sxs-lookup"><span data-stu-id="2916e-109">Script explanation</span></span>

<span data-ttu-id="2916e-110">Ce script utilise hello après le déploiement de commandes toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="2916e-110">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="2916e-111">Chaque élément de la documentation spécifique du toocommand liens table hello.</span><span class="sxs-lookup"><span data-stu-id="2916e-111">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="2916e-112">Commande</span><span class="sxs-lookup"><span data-stu-id="2916e-112">Command</span></span> | <span data-ttu-id="2916e-113">Remarques</span><span class="sxs-lookup"><span data-stu-id="2916e-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="2916e-114">az acs scale</span><span class="sxs-lookup"><span data-stu-id="2916e-114">az acs scale</span></span>](/cli/azure/acs#scale) | <span data-ttu-id="2916e-115">Met à l’échelle un cluster ACS.</span><span class="sxs-lookup"><span data-stu-id="2916e-115">Scale an ACS cluster.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="2916e-116">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2916e-116">Next steps</span></span>

<span data-ttu-id="2916e-117">Pour plus d’informations sur hello CLI d’Azure, consultez [documentation relative à Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="2916e-117">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="2916e-118">Vous trouverez des exemples supplémentaires de script CLI de Service de conteneur Azure Bonjour [documentation sur le Service de conteneur Azure](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="2916e-118">Additional Azure Container Service CLI script samples can be found in hello [Azure Container Service documentation](../cli-samples.md).</span></span>

