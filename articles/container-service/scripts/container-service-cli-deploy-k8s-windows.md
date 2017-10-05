---
title: "Exemple de script Azure CLI - Créer un cluster ACS Windows Kubernetes | Microsoft Docs"
description: "Exemple de script Azure CLI - Créer un cluster ACS Windows Kubernetes"
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
ms.openlocfilehash: 3cba915e3cf3aaaeb3faf14c2000ca94f61d28a5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-container-service-kubernetes-windows-cluster"></a><span data-ttu-id="56140-104">Créer un cluster Windows Kubernetes Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="56140-104">Create an Azure Container Service Kubernetes Windows Cluster</span></span>

<span data-ttu-id="56140-105">Cet exemple crée un cluster Azure Container Service exécutant Kubernetes pour des conteneurs basés sur Windows.</span><span class="sxs-lookup"><span data-stu-id="56140-105">This sample creates an Azure Container Service cluster running Kubernetes for Windows based containers.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="56140-106">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="56140-106">Sample script</span></span>

```azurecli
az group create --name myResourceGroup --location eastus

az acs create \
  --orchestrator-type kubernetes \
  --resource-group myResourceGroup \
  --name myK8SCluster \
  --generate-ssh-keys \
  --admin-username azureuser \
  --admin-password Password12 \
  --windows
```

## <a name="clean-up-deployment"></a><span data-ttu-id="56140-107">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="56140-107">Clean up deployment</span></span> 

<span data-ttu-id="56140-108">Exécutez la commande suivante pour supprimer le groupe de ressources, la machine virtuelle et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="56140-108">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="56140-109">Explication du script</span><span class="sxs-lookup"><span data-stu-id="56140-109">Script explanation</span></span>

<span data-ttu-id="56140-110">Ce script a recours aux commandes suivantes pour créer le déploiement.</span><span class="sxs-lookup"><span data-stu-id="56140-110">This script uses the following commands to create the deployment.</span></span> <span data-ttu-id="56140-111">Chaque élément du tableau renvoie à une documentation spécifique.</span><span class="sxs-lookup"><span data-stu-id="56140-111">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="56140-112">Commande</span><span class="sxs-lookup"><span data-stu-id="56140-112">Command</span></span> | <span data-ttu-id="56140-113">Remarques</span><span class="sxs-lookup"><span data-stu-id="56140-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="56140-114">az group create</span><span class="sxs-lookup"><span data-stu-id="56140-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="56140-115">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="56140-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="56140-116">az acs create</span><span class="sxs-lookup"><span data-stu-id="56140-116">az acs create</span></span>](https://docs.microsoft.com/cli/azure/acs#create) | <span data-ttu-id="56140-117">Crée un cluster ACS.</span><span class="sxs-lookup"><span data-stu-id="56140-117">Creates and ACS cluster.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="56140-118">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="56140-118">Next steps</span></span>

<span data-ttu-id="56140-119">Pour plus d’informations sur l’interface Azure CLI, consultez la [documentation relative à l’interface Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="56140-119">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="56140-120">Vous trouverez des exemples supplémentaires de scripts CLI Azure Container Service dans la [documentation sur Azure Container Service](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="56140-120">Additional Azure Container Service CLI script samples can be found in the [Azure Container Service documentation](../cli-samples.md).</span></span>
