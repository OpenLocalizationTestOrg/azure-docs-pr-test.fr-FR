---
title: "aaaAzure exemple de Script CLI - créer le Cluster ACS Linux Kubernetes | Documents Microsoft"
description: "Exemple de script d’interface CLI Azure - Créer un cluster ACS Linux Kubernetes"
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
ms.openlocfilehash: cf3798ea8b08e3fc32acb35dabab4b2fbea179dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-container-service-kubernetes-linux-cluster"></a><span data-ttu-id="84939-104">Créer un cluster Azure Container Service Kubernetes Linux</span><span class="sxs-lookup"><span data-stu-id="84939-104">Create an Azure Container Service Kubernetes Linux Cluster</span></span>

<span data-ttu-id="84939-105">Cet exemple crée un cluster Azure Container Service exécutant Kubernetes pour des conteneurs Linux.</span><span class="sxs-lookup"><span data-stu-id="84939-105">This sample creates an Azure Container Service cluster running Kubernetes for Linux based containers.</span></span>

[!INCLUDE [sample-cli-install](../../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="84939-106">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="84939-106">Sample script</span></span>

```azurecli
az group create --name myResourceGroup --location eastus

az acs create \
  --orchestrator-type kubernetes \
  --resource-group myResourceGroup \
  --name myK8SCluster \
  --generate-ssh-keys
```

## <a name="clean-up-deployment"></a><span data-ttu-id="84939-107">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="84939-107">Clean up deployment</span></span> 

<span data-ttu-id="84939-108">Exécutez hello suivant du groupe de ressources de commande tooremove hello, machine virtuelle et toutes les ressources.</span><span class="sxs-lookup"><span data-stu-id="84939-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="84939-109">Explication du script</span><span class="sxs-lookup"><span data-stu-id="84939-109">Script explanation</span></span>

<span data-ttu-id="84939-110">Ce script utilise hello après le déploiement de commandes toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="84939-110">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="84939-111">Chaque élément de la documentation spécifique du toocommand liens table hello.</span><span class="sxs-lookup"><span data-stu-id="84939-111">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="84939-112">Commande</span><span class="sxs-lookup"><span data-stu-id="84939-112">Command</span></span> | <span data-ttu-id="84939-113">Remarques</span><span class="sxs-lookup"><span data-stu-id="84939-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="84939-114">az group create</span><span class="sxs-lookup"><span data-stu-id="84939-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="84939-115">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="84939-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="84939-116">az acs create</span><span class="sxs-lookup"><span data-stu-id="84939-116">az acs create</span></span>](https://docs.microsoft.com/cli/azure/acs#create) | <span data-ttu-id="84939-117">Crée un cluster ACS.</span><span class="sxs-lookup"><span data-stu-id="84939-117">Creates and ACS cluster.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="84939-118">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="84939-118">Next steps</span></span>

<span data-ttu-id="84939-119">Pour plus d’informations sur hello CLI d’Azure, consultez [documentation relative à Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="84939-119">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="84939-120">Vous trouverez des exemples supplémentaires de script CLI de Service de conteneur Azure Bonjour [documentation sur le Service de conteneur Azure](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="84939-120">Additional Azure Container Service CLI script samples can be found in hello [Azure Container Service documentation](../cli-samples.md).</span></span>

