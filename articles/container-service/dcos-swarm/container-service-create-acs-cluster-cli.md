---
title: "aaaDeploy un cluster de conteneur Docker - CLI d’Azure | Documents Microsoft"
description: "Déployer une solution Kubernetes, DC/OS ou Docker Swarm dans Azure Container Service à l’aide d’Azure CLI 2.0"
services: container-service
documentationcenter: 
author: sauryadas
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: 
ms.assetid: 8da267e8-2aeb-4c24-9a7a-65bdca3a82d6
ms.service: container-service
ms.devlang: azurecli
ms.topic: quickstart
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/01/2017
ms.author: saudas
ms.custom: H1Hack27Feb2017, mvc
ms.openlocfilehash: cdfa4ce69de343dcc7070bc2c58b5132c4062084
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-docker-container-hosting-solution-using-hello-azure-cli-20"></a><span data-ttu-id="bbb70-103">Déployer un conteneur Docker à l’aide de hello Azure CLI 2.0 de solution d’hébergement</span><span class="sxs-lookup"><span data-stu-id="bbb70-103">Deploy a Docker container hosting solution using hello Azure CLI 2.0</span></span>

<span data-ttu-id="bbb70-104">Hello d’utilisation `az acs` hello Azure CLI 2.0 toocreate des commandes et de gérer des clusters dans le Service de conteneur Azure.</span><span class="sxs-lookup"><span data-stu-id="bbb70-104">Use hello `az acs` commands in hello Azure CLI 2.0 toocreate and manage clusters in Azure Container Service.</span></span> <span data-ttu-id="bbb70-105">Vous pouvez également déployer un cluster du Service de conteneur Azure à l’aide de hello [portail Azure](container-service-deployment.md) ou hello API de Service de conteneur Azure.</span><span class="sxs-lookup"><span data-stu-id="bbb70-105">You can also deploy an Azure Container Service cluster by using hello [Azure portal](container-service-deployment.md) or hello Azure Container Service APIs.</span></span>

<span data-ttu-id="bbb70-106">Pour une aide sur `az acs` commandes, passez hello `-h` commande tooany de paramètre.</span><span class="sxs-lookup"><span data-stu-id="bbb70-106">For help on `az acs` commands, pass hello `-h` parameter tooany command.</span></span> <span data-ttu-id="bbb70-107">Par exemple : `az acs create -h`.</span><span class="sxs-lookup"><span data-stu-id="bbb70-107">For example: `az acs create -h`.</span></span>



## <a name="prerequisites"></a><span data-ttu-id="bbb70-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="bbb70-108">Prerequisites</span></span>
<span data-ttu-id="bbb70-109">un cluster de Service de conteneur Azure à l’aide de toocreate hello Azure CLI 2.0, vous devez :</span><span class="sxs-lookup"><span data-stu-id="bbb70-109">toocreate an Azure Container Service cluster using hello Azure CLI 2.0, you must:</span></span>
* <span data-ttu-id="bbb70-110">disposer d’un compte Azure ([obtenir une version d’évaluation gratuite](https://azure.microsoft.com/pricing/free-trial/))</span><span class="sxs-lookup"><span data-stu-id="bbb70-110">have an Azure account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/))</span></span>
* <span data-ttu-id="bbb70-111">avoir installé et configuré hello [Azure CLI 2.0](/cli/azure/install-az-cli2)</span><span class="sxs-lookup"><span data-stu-id="bbb70-111">have installed and set up hello [Azure CLI 2.0](/cli/azure/install-az-cli2)</span></span>

## <a name="get-started"></a><span data-ttu-id="bbb70-112">Prise en main</span><span class="sxs-lookup"><span data-stu-id="bbb70-112">Get started</span></span> 
### <a name="log-in-tooyour-account"></a><span data-ttu-id="bbb70-113">Connectez-vous au compte de tooyour</span><span class="sxs-lookup"><span data-stu-id="bbb70-113">Log in tooyour account</span></span>
```azurecli
az login 
```

<span data-ttu-id="bbb70-114">Suivez toolog des invites hello dans interactivement.</span><span class="sxs-lookup"><span data-stu-id="bbb70-114">Follow hello prompts toolog in interactively.</span></span> <span data-ttu-id="bbb70-115">Pour les autres toolog méthodes dans, consultez [prise en main Azure CLI 2.0](/cli/azure/get-started-with-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="bbb70-115">For other methods toolog in, see [Get started with Azure CLI 2.0](/cli/azure/get-started-with-az-cli2).</span></span>

### <a name="set-your-azure-subscription"></a><span data-ttu-id="bbb70-116">Définir votre abonnement Azure</span><span class="sxs-lookup"><span data-stu-id="bbb70-116">Set your Azure subscription</span></span>

<span data-ttu-id="bbb70-117">Si vous avez plusieurs abonnements Azure, définissez l’abonnement par défaut de hello.</span><span class="sxs-lookup"><span data-stu-id="bbb70-117">If you have more than one Azure subscription, set hello default subscription.</span></span> <span data-ttu-id="bbb70-118">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="bbb70-118">For example:</span></span>

```
az account set --subscription "f66xxxxx-xxxx-xxxx-xxx-zgxxxx33cha5"
```


### <a name="create-a-resource-group"></a><span data-ttu-id="bbb70-119">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="bbb70-119">Create a resource group</span></span>
<span data-ttu-id="bbb70-120">Nous vous recommandons de créer un groupe de ressources pour chaque cluster.</span><span class="sxs-lookup"><span data-stu-id="bbb70-120">We recommend that you create a resource group for every cluster.</span></span> <span data-ttu-id="bbb70-121">Spécifiez une région Azure dans laquelle Azure Container Service est [disponible](https://azure.microsoft.com/en-us/regions/services/).</span><span class="sxs-lookup"><span data-stu-id="bbb70-121">Specify an Azure region in which Azure Container Service is [available](https://azure.microsoft.com/en-us/regions/services/).</span></span> <span data-ttu-id="bbb70-122">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="bbb70-122">For example:</span></span>

```azurecli
az group create -n acsrg1 -l "westus"
```
<span data-ttu-id="bbb70-123">La sortie est similaire toohello suivantes :</span><span class="sxs-lookup"><span data-stu-id="bbb70-123">Output is similar toohello following:</span></span>

![Créer un groupe de ressources](./media/container-service-create-acs-cluster-cli/rg-create.png)


## <a name="create-an-azure-container-service-cluster"></a><span data-ttu-id="bbb70-125">Créer un cluster Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="bbb70-125">Create an Azure Container Service cluster</span></span>

<span data-ttu-id="bbb70-126">toocreate un cluster, utilisez `az acs create`.</span><span class="sxs-lookup"><span data-stu-id="bbb70-126">toocreate a cluster, use `az acs create`.</span></span>
<span data-ttu-id="bbb70-127">Un nom pour le cluster de hello et hello hello du groupe de ressources créé à l’étape précédente de hello sont les paramètres obligatoires.</span><span class="sxs-lookup"><span data-stu-id="bbb70-127">A name for hello cluster and hello name of hello resource group created in hello previous step are mandatory parameters.</span></span> 

<span data-ttu-id="bbb70-128">Autres entrées sont les valeurs toodefault (voir hello suivant écran), sauf si remplacé à l’aide de leurs commutateurs respectifs.</span><span class="sxs-lookup"><span data-stu-id="bbb70-128">Other inputs are set toodefault values (see hello following screen) unless overwritten using their respective switches.</span></span> <span data-ttu-id="bbb70-129">Par exemple, les orchestrator hello a la valeur par défaut tooDC/système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="bbb70-129">For example, hello orchestrator is set by default tooDC/OS.</span></span> <span data-ttu-id="bbb70-130">Et si vous ne précisez aucun, un préfixe de nom DNS est créé en fonction du nom du cluster hello.</span><span class="sxs-lookup"><span data-stu-id="bbb70-130">And if you don't specify one, a DNS name prefix is created based on hello cluster name.</span></span>

![création d’un cluster acs az](./media/container-service-create-acs-cluster-cli/create-help.png)


### <a name="quick-acs-create-using-defaults"></a><span data-ttu-id="bbb70-132">`acs create` rapide à l’aide des valeurs par défaut</span><span class="sxs-lookup"><span data-stu-id="bbb70-132">Quick `acs create` using defaults</span></span>
<span data-ttu-id="bbb70-133">Si vous avez un fichier de clé publique SSH RSA `id_rsa.pub` dans l’emplacement par défaut de hello (ou créé un pour [OS X et Linux](../../virtual-machines/linux/mac-create-ssh-keys.md) ou [Windows](../../virtual-machines/linux/ssh-from-windows.md)), utilisez une commande semblable à hello suivante :</span><span class="sxs-lookup"><span data-stu-id="bbb70-133">If you have an SSH RSA public key file `id_rsa.pub` in hello default location (or created one for [OS X and Linux](../../virtual-machines/linux/mac-create-ssh-keys.md) or [Windows](../../virtual-machines/linux/ssh-from-windows.md)), use a command like hello following:</span></span>

```azurecli
az acs create -n acs-cluster -g acsrg1 -d applink789
```
<span data-ttu-id="bbb70-134">Si vous n’avez pas de clé publique SSH, utilisez cette seconde commande.</span><span class="sxs-lookup"><span data-stu-id="bbb70-134">If you don't have an SSH public key, use this second command.</span></span> <span data-ttu-id="bbb70-135">Cette commande avec hello `--generate-ssh-keys` commutateur crée une pour vous.</span><span class="sxs-lookup"><span data-stu-id="bbb70-135">This command with hello `--generate-ssh-keys` switch creates one for you.</span></span>

```azurecli
az acs create -n acs-cluster -g acsrg1 -d applink789 --generate-ssh-keys
```

<span data-ttu-id="bbb70-136">Après avoir entré la commande hello, attendez environ 10 minutes pour hello cluster toobe est créé.</span><span class="sxs-lookup"><span data-stu-id="bbb70-136">After you enter hello command, wait for about 10 minutes for hello cluster toobe created.</span></span> <span data-ttu-id="bbb70-137">sortie de la commande Hello inclut les noms de domaine complet (FQDN) de masque de hello et de des nœuds de l’agent et d’une commande SSH tooconnect toohello premier masque.</span><span class="sxs-lookup"><span data-stu-id="bbb70-137">hello command output includes fully qualified domain names (FQDNs) of hello master and agent nodes and an SSH command tooconnect toohello first master.</span></span> <span data-ttu-id="bbb70-138">Voici la sortie abrégée :</span><span class="sxs-lookup"><span data-stu-id="bbb70-138">Here is abbreviated output:</span></span>

![Image création du cluster ACS](./media/container-service-create-acs-cluster-cli/cluster-create.png)

> [!TIP]
> <span data-ttu-id="bbb70-140">Hello [Kubernetes procédure pas à pas](../kubernetes/container-service-kubernetes-walkthrough.md) montre comment toouse `az acs create` avec toocreate de valeurs par défaut un Kubernetes de cluster.</span><span class="sxs-lookup"><span data-stu-id="bbb70-140">hello [Kubernetes walkthrough](../kubernetes/container-service-kubernetes-walkthrough.md) shows how toouse `az acs create` with default values toocreate a Kubernetes cluster.</span></span>
>

## <a name="manage-acs-clusters"></a><span data-ttu-id="bbb70-141">Gérer des clusters ACS</span><span class="sxs-lookup"><span data-stu-id="bbb70-141">Manage ACS clusters</span></span>

<span data-ttu-id="bbb70-142">Utilisez supplémentaire `az acs` commandes toomanage votre cluster.</span><span class="sxs-lookup"><span data-stu-id="bbb70-142">Use additional `az acs` commands toomanage your cluster.</span></span> <span data-ttu-id="bbb70-143">Voici quelques exemples.</span><span class="sxs-lookup"><span data-stu-id="bbb70-143">Here are some examples.</span></span>

### <a name="list-clusters-under-a-subscription"></a><span data-ttu-id="bbb70-144">Répertorier les clusters dans un abonnement</span><span class="sxs-lookup"><span data-stu-id="bbb70-144">List clusters under a subscription</span></span>

```azurecli
az acs list --output table
```

### <a name="list-clusters-in-a-resource-group"></a><span data-ttu-id="bbb70-145">Répertorier les clusters au sein d’un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="bbb70-145">List clusters in a resource group</span></span>

```azurecli
az acs list -g acsrg1 --output table
```

![liste des clusters acs](./media/container-service-create-acs-cluster-cli/acs-list.png)


### <a name="display-details-of-a-container-service-cluster"></a><span data-ttu-id="bbb70-147">Afficher les détails d’un cluster Container Service</span><span class="sxs-lookup"><span data-stu-id="bbb70-147">Display details of a container service cluster</span></span>

```azurecli
az acs show -g acsrg1 -n acs-cluster --output list
```

![affichage du cluster acs](./media/container-service-create-acs-cluster-cli/acs-show.png)


### <a name="scale-hello-cluster"></a><span data-ttu-id="bbb70-149">Cluster hello de mise à l’échelle</span><span class="sxs-lookup"><span data-stu-id="bbb70-149">Scale hello cluster</span></span>
<span data-ttu-id="bbb70-150">Vous pouvez effectuer une mise à l’échelle verticale ou horizontale des nœuds d’agent.</span><span class="sxs-lookup"><span data-stu-id="bbb70-150">Both scaling in and scaling out of agent nodes are allowed.</span></span> <span data-ttu-id="bbb70-151">Hello paramètre `new-agent-count` est hello nouveau nombre d’agents dans le cluster de hello ACS.</span><span class="sxs-lookup"><span data-stu-id="bbb70-151">hello parameter `new-agent-count` is hello new number of agents in hello ACS cluster.</span></span>

```azurecli
az acs scale -g acsrg1 -n acs-cluster --new-agent-count 4
```

![mise à l’échelle du cluster acs](./media/container-service-create-acs-cluster-cli/acs-scale.png)

## <a name="delete-a-container-service-cluster"></a><span data-ttu-id="bbb70-153">Supprimer un cluster Container Service</span><span class="sxs-lookup"><span data-stu-id="bbb70-153">Delete a container service cluster</span></span>
```azurecli
az acs delete -g acsrg1 -n acs-cluster 
```
<span data-ttu-id="bbb70-154">Cette commande ne supprime pas toutes les ressources (réseau et stockage) sont créées lors de la création du service de conteneur hello.</span><span class="sxs-lookup"><span data-stu-id="bbb70-154">This command does not delete all resources (network and storage) created while creating hello container service.</span></span> <span data-ttu-id="bbb70-155">toodelete toutes les ressources facilement, il est recommandé de déployer chaque cluster dans un groupe de ressources distinct.</span><span class="sxs-lookup"><span data-stu-id="bbb70-155">toodelete all resources easily, it is recommended you deploy each cluster in a distinct resource group.</span></span> <span data-ttu-id="bbb70-156">Supprimez ensuite le groupe de ressources hello lorsque hello cluster n’est plus nécessaire.</span><span class="sxs-lookup"><span data-stu-id="bbb70-156">Then, delete hello resource group when hello cluster is no longer required.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bbb70-157">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="bbb70-157">Next steps</span></span>
<span data-ttu-id="bbb70-158">À présent que vous disposez d’un cluster opérationnel, consultez les documents suivants pour obtenir des informations supplémentaires concernant la connexion et la gestion du cluster :</span><span class="sxs-lookup"><span data-stu-id="bbb70-158">Now that you have a functioning cluster, see these documents for connection and management details:</span></span>

* [<span data-ttu-id="bbb70-159">Connecter le cluster du Service de conteneur Azure tooan</span><span class="sxs-lookup"><span data-stu-id="bbb70-159">Connect tooan Azure Container Service cluster</span></span>](../container-service-connect.md)
* [<span data-ttu-id="bbb70-160">Gestion de conteneur via l’API REST</span><span class="sxs-lookup"><span data-stu-id="bbb70-160">Work with Azure Container Service and DC/OS</span></span>](container-service-mesos-marathon-rest.md)
* [<span data-ttu-id="bbb70-161">Gestion des conteneurs avec Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="bbb70-161">Work with Azure Container Service and Docker Swarm</span></span>](container-service-docker-swarm.md)
* [<span data-ttu-id="bbb70-162">Gestion des conteneurs avec Kubernetes</span><span class="sxs-lookup"><span data-stu-id="bbb70-162">Work with Azure Container Service and Kubernetes</span></span>](../kubernetes/container-service-kubernetes-walkthrough.md)