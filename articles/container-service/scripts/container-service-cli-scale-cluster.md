---
title: "Exemple de script Azure CLI - Mettre à l’échelle un cluster ACS | Microsoft Docs"
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
ms.openlocfilehash: 0ea2c73436e650fdb37535538baccc565369fa9d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="scale-an-azure-container-service-cluster"></a><span data-ttu-id="1935d-104">Mettre à l’échelle un cluster Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="1935d-104">Scale an Azure Container Service Cluster</span></span>

<span data-ttu-id="1935d-105">Cet exemple met à l’échelle un environnement Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="1935d-105">This sample scales and Azure Container Service.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="1935d-106">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="1935d-106">Sample script</span></span>

```azurecli
az acs scale --resource-group myResourceGroup --name myK8SCluster --new-agent-count 5
```

## <a name="clean-up-deployment"></a><span data-ttu-id="1935d-107">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="1935d-107">Clean up deployment</span></span> 

<span data-ttu-id="1935d-108">Exécutez la commande suivante pour supprimer le groupe de ressources, la machine virtuelle et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="1935d-108">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="1935d-109">Explication du script</span><span class="sxs-lookup"><span data-stu-id="1935d-109">Script explanation</span></span>

<span data-ttu-id="1935d-110">Ce script a recours aux commandes suivantes pour créer le déploiement.</span><span class="sxs-lookup"><span data-stu-id="1935d-110">This script uses the following commands to create the deployment.</span></span> <span data-ttu-id="1935d-111">Chaque élément du tableau renvoie à une documentation spécifique.</span><span class="sxs-lookup"><span data-stu-id="1935d-111">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="1935d-112">Commande</span><span class="sxs-lookup"><span data-stu-id="1935d-112">Command</span></span> | <span data-ttu-id="1935d-113">Remarques</span><span class="sxs-lookup"><span data-stu-id="1935d-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="1935d-114">az acs scale</span><span class="sxs-lookup"><span data-stu-id="1935d-114">az acs scale</span></span>](/cli/azure/acs#scale) | <span data-ttu-id="1935d-115">Met à l’échelle un cluster ACS.</span><span class="sxs-lookup"><span data-stu-id="1935d-115">Scale an ACS cluster.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="1935d-116">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1935d-116">Next steps</span></span>

<span data-ttu-id="1935d-117">Pour plus d’informations sur l’interface Azure CLI, consultez la [documentation relative à l’interface Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="1935d-117">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="1935d-118">Vous trouverez des exemples supplémentaires de scripts CLI Azure Container Service dans la [documentation sur Azure Container Service](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="1935d-118">Additional Azure Container Service CLI script samples can be found in the [Azure Container Service documentation](../cli-samples.md).</span></span>

