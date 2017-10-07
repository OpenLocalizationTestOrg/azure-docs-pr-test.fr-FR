---
title: "didacticiel de Service de conteneur aaaAzure - gérer les contrôleurs de domaine/système d’exploitation | Documents Microsoft"
description: "Didacticiel Azure Container Service - Gérer DC/OS"
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
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/17/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: b91c433bfd7e48ec405cc62be1486d9d4662839d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-container-service-tutorial---manage-dcos"></a><span data-ttu-id="92989-104">Didacticiel Azure Container Service - Gérer DC/OS</span><span class="sxs-lookup"><span data-stu-id="92989-104">Azure Container Service tutorial - Manage DC/OS</span></span>

<span data-ttu-id="92989-105">DC/OS propose une plateforme distribuée destinée à exécuter des applications en conteneur modernes.</span><span class="sxs-lookup"><span data-stu-id="92989-105">DC/OS provides a distributed platform for running modern and containerized applications.</span></span> <span data-ttu-id="92989-106">Avec Azure Container Service, l’approvisionnement d’un cluster DC/OS prêt pour la production est une opération simple et rapide.</span><span class="sxs-lookup"><span data-stu-id="92989-106">With Azure Container Service, provisioning of a production ready DC/OS cluster is simple and quick.</span></span> <span data-ttu-id="92989-107">Ce démarrage rapide Détails des étapes base nécessaires toodeploy un cluster de contrôleur de domaine/système d’exploitation et de la charge de travail de base exécution.</span><span class="sxs-lookup"><span data-stu-id="92989-107">This quick start details basic steps needed toodeploy a DC/OS cluster and run basic workload.</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="92989-108">Créer un cluster ACS DC/OS</span><span class="sxs-lookup"><span data-stu-id="92989-108">Create an ACS DC/OS cluster</span></span>
> * <span data-ttu-id="92989-109">Se connecter toohello cluster</span><span class="sxs-lookup"><span data-stu-id="92989-109">Connect toohello cluster</span></span>
> * <span data-ttu-id="92989-110">Installer hello CLI de contrôleur de domaine/système d’exploitation</span><span class="sxs-lookup"><span data-stu-id="92989-110">Install hello DC/OS CLI</span></span>
> * <span data-ttu-id="92989-111">Déployer un cluster de toohello d’application</span><span class="sxs-lookup"><span data-stu-id="92989-111">Deploy an application toohello cluster</span></span>
> * <span data-ttu-id="92989-112">L’échelle d’une application sur un cluster de hello</span><span class="sxs-lookup"><span data-stu-id="92989-112">Scale an application on hello cluster</span></span>
> * <span data-ttu-id="92989-113">Mettre à l’échelle des nœuds de cluster de contrôleur de domaine/système d’exploitation hello</span><span class="sxs-lookup"><span data-stu-id="92989-113">Scale hello DC/OS cluster nodes</span></span>
> * <span data-ttu-id="92989-114">Gestion DC/OS de base</span><span class="sxs-lookup"><span data-stu-id="92989-114">Basic DC/OS management</span></span>
> * <span data-ttu-id="92989-115">Supprimer le cluster de contrôleur de domaine/système d’exploitation hello</span><span class="sxs-lookup"><span data-stu-id="92989-115">Delete hello DC/OS cluster</span></span>

<span data-ttu-id="92989-116">Ce didacticiel requiert hello CLI d’Azure version 2.0.4 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="92989-116">This tutorial requires hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="92989-117">Exécutez `az --version` version de hello toofind.</span><span class="sxs-lookup"><span data-stu-id="92989-117">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="92989-118">Si vous avez besoin de tooupgrade, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="92989-118">If you need tooupgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-dcos-cluster"></a><span data-ttu-id="92989-119">Créer un cluster DC/OS</span><span class="sxs-lookup"><span data-stu-id="92989-119">Create DC/OS cluster</span></span>

<span data-ttu-id="92989-120">Commencez par créer un groupe de ressources avec hello [création de groupe de az](/cli/azure/group#create) commande.</span><span class="sxs-lookup"><span data-stu-id="92989-120">First, create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="92989-121">Un groupe de ressources Azure est un conteneur logique dans lequel les ressources Azure sont déployées et gérées.</span><span class="sxs-lookup"><span data-stu-id="92989-121">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="92989-122">Hello exemple suivant crée un groupe de ressources nommé *myResourceGroup* Bonjour *westeurope* emplacement.</span><span class="sxs-lookup"><span data-stu-id="92989-122">hello following example creates a resource group named *myResourceGroup* in hello *westeurope* location.</span></span>

```azurecli
az group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="92989-123">Ensuite, créez un cluster de contrôleur de domaine/système d’exploitation avec hello [az acs créer](/cli/azure/acs#create) commande.</span><span class="sxs-lookup"><span data-stu-id="92989-123">Next, create a DC/OS cluster with hello [az acs create](/cli/azure/acs#create) command.</span></span>

<span data-ttu-id="92989-124">Hello exemple suivant crée un cluster de contrôleur de domaine/système d’exploitation nommé *myDCOSCluster* et crée des clés SSH s’ils n’existent pas déjà.</span><span class="sxs-lookup"><span data-stu-id="92989-124">hello following example creates a DC/OS cluster named *myDCOSCluster* and creates SSH keys if they do not already exist.</span></span> <span data-ttu-id="92989-125">toouse un ensemble spécifique de clés, utilisez hello `--ssh-key-value` option.</span><span class="sxs-lookup"><span data-stu-id="92989-125">toouse a specific set of keys, use hello `--ssh-key-value` option.</span></span>  

```azurecli
az acs create \
  --orchestrator-type dcos \
  --resource-group myResourceGroup \
  --name myDCOSCluster \
  --generate-ssh-keys
```

<span data-ttu-id="92989-126">Après quelques minutes, commande hello se termine et retourne des informations sur le déploiement de hello.</span><span class="sxs-lookup"><span data-stu-id="92989-126">After several minutes, hello command completes, and returns information about hello deployment.</span></span>

## <a name="connect-toodcos-cluster"></a><span data-ttu-id="92989-127">Connectez le cluster de tooDC/OS</span><span class="sxs-lookup"><span data-stu-id="92989-127">Connect tooDC/OS cluster</span></span>

<span data-ttu-id="92989-128">Dès lors qu’un cluster DC/OS est créé, il est accessible via un tunnel SSH.</span><span class="sxs-lookup"><span data-stu-id="92989-128">Once a DC/OS cluster has been created, it can be accesses through an SSH tunnel.</span></span> <span data-ttu-id="92989-129">Exécutez hello suivant commande tooreturn hello adresse IP publique du principal du contrôleur de domaine/système d’exploitation hello.</span><span class="sxs-lookup"><span data-stu-id="92989-129">Run hello following command tooreturn hello public IP address of hello DC/OS master.</span></span> <span data-ttu-id="92989-130">Cette adresse IP est stockée dans une variable et utilisée à l’étape suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="92989-130">This IP address is stored in a variable and used in hello next step.</span></span>

```azurecli
ip=$(az network public-ip list --resource-group myResourceGroup --query "[?contains(name,'dcos-master')].[ipAddress]" -o tsv)
```

<span data-ttu-id="92989-131">toocreate hello tunnel SSH, exécutez hello commande suivante et suivez hello les instructions à l’écran.</span><span class="sxs-lookup"><span data-stu-id="92989-131">toocreate hello SSH tunnel, run hello following command and follow hello on-screen instructions.</span></span> <span data-ttu-id="92989-132">Si le port 80 est déjà en cours d’utilisation, la commande hello échoue.</span><span class="sxs-lookup"><span data-stu-id="92989-132">If port 80 is already in use, hello command fails.</span></span> <span data-ttu-id="92989-133">Hello de mise à jour en tunnel tooone port pas en cours d’utilisation, telles que `85:localhost:80`.</span><span class="sxs-lookup"><span data-stu-id="92989-133">Update hello tunneled port tooone not in use, such as `85:localhost:80`.</span></span> 

```azurecli
sudo ssh -i ~/.ssh/id_rsa -fNL 80:localhost:80 -p 2200 azureuser@$ip
```

## <a name="install-dcos-cli"></a><span data-ttu-id="92989-134">Installer l’interface de ligne de commande DC/OS</span><span class="sxs-lookup"><span data-stu-id="92989-134">Install DC/OS CLI</span></span>

<span data-ttu-id="92989-135">Installez hello cli de contrôleur de domaine/système d’exploitation à l’aide de hello [az acs dcos install-cli](/azure/acs/dcos#install-cli) commande.</span><span class="sxs-lookup"><span data-stu-id="92989-135">Install hello DC/OS cli using hello [az acs dcos install-cli](/azure/acs/dcos#install-cli) command.</span></span> <span data-ttu-id="92989-136">Si vous utilisez Azure CloudShell, hello CLI de contrôleur de domaine/système d’exploitation est déjà installé.</span><span class="sxs-lookup"><span data-stu-id="92989-136">If you are using Azure CloudShell, hello DC/OS CLI is already installed.</span></span> <span data-ttu-id="92989-137">Si vous exécutez hello CLI d’Azure sur macOS ou Linux, vous devrez peut-être commande hello toorun sudo.</span><span class="sxs-lookup"><span data-stu-id="92989-137">If you are running hello Azure CLI on macOS or Linux, you might need toorun hello command with sudo.</span></span>

```azurecli
az acs dcos install-cli
```

<span data-ttu-id="92989-138">Avant de hello que CLI peut être utilisé avec un cluster de hello, il doit être tunnel SSH de hello toouse configuré.</span><span class="sxs-lookup"><span data-stu-id="92989-138">Before hello CLI can be used with hello cluster, it must be configured toouse hello SSH tunnel.</span></span> <span data-ttu-id="92989-139">toodo exécuter donc hello commande suivante, en ajustant le port de hello si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="92989-139">toodo so, run hello following command, adjusting hello port if needed.</span></span>

```azurecli
dcos config set core.dcos_url http://localhost
```

## <a name="run-an-application"></a><span data-ttu-id="92989-140">Exécuter une application</span><span class="sxs-lookup"><span data-stu-id="92989-140">Run an application</span></span>

<span data-ttu-id="92989-141">mécanisme pour un cluster ACS contrôleur de domaine/système d’exploitation de planification de la valeur par défaut Hello est Marathon.</span><span class="sxs-lookup"><span data-stu-id="92989-141">hello default scheduling mechanism for an ACS DC/OS cluster is Marathon.</span></span> <span data-ttu-id="92989-142">Marathon est toostart utilisé une application et gérer l’état de l’application hello sur le cluster de contrôleur de domaine/système d’exploitation hello hello.</span><span class="sxs-lookup"><span data-stu-id="92989-142">Marathon is used toostart an application and manage hello state of hello application on hello DC/OS cluster.</span></span> <span data-ttu-id="92989-143">tooschedule une application via Marathon, créez un fichier nommé **marathon-app.json**, et en hello de copie suivant contenu dans celui-ci.</span><span class="sxs-lookup"><span data-stu-id="92989-143">tooschedule an application through Marathon, create a file named **marathon-app.json**, and copy hello following contents into it.</span></span> 

```json
{
  "id": "demo-app-private",
  "cmd": null,
  "cpus": 1,
  "mem": 32,
  "disk": 0,
  "instances": 1,
  "container": {
    "docker": {
      "image": "nginx",
      "network": "BRIDGE",
      "portMappings": [
        {
          "containerPort": 80,
          "protocol": "tcp",
          "name": "80",
          "labels": null
        }
      ]
    },
    "type": "DOCKER"
  }
}
```

<span data-ttu-id="92989-144">Exécutez hello suivant de commande tooschedule hello application toorun de cluster de contrôleur de domaine/système d’exploitation hello.</span><span class="sxs-lookup"><span data-stu-id="92989-144">Run hello following command tooschedule hello application toorun on hello DC/OS cluster.</span></span>

```azurecli
dcos marathon app add marathon-app.json
```

<span data-ttu-id="92989-145">état du déploiement toosee hello pour l’application hello, exécutez hello commande suivante.</span><span class="sxs-lookup"><span data-stu-id="92989-145">toosee hello deployment status for hello app, run hello following command.</span></span>

```azurecli
dcos marathon app list
```

<span data-ttu-id="92989-146">Hello lorsque **tâches** bascule de valeur de la colonne à partir de *0/1* trop*1/1*, déploiement d’application est terminée.</span><span class="sxs-lookup"><span data-stu-id="92989-146">When hello **TASKS** column value switches from *0/1* too*1/1*, application deployment has completed.</span></span>

```azurecli
ID     MEM  CPUS  TASKS  HEALTH  DEPLOYMENT  WAITING  CONTAINER  CMD   
/test   32   1     0/1    ---       ---      False      DOCKER   None
```

## <a name="scale-marathon-application"></a><span data-ttu-id="92989-147">Mettre à l’échelle l’application Marathon</span><span class="sxs-lookup"><span data-stu-id="92989-147">Scale Marathon application</span></span>

<span data-ttu-id="92989-148">Dans l’exemple précédent de hello, une application à instance unique a été créée.</span><span class="sxs-lookup"><span data-stu-id="92989-148">In hello previous example, a single instance application was created.</span></span> <span data-ttu-id="92989-149">tooupdate ce déploiement afin que les trois instances de l’application hello sont disponibles, ouvrez hello **marathon-app.json** de fichiers et mettre à jour too3 de propriété d’instance hello.</span><span class="sxs-lookup"><span data-stu-id="92989-149">tooupdate this deployment so that three instances of hello application are available, open up hello **marathon-app.json** file, and update hello instance property too3.</span></span>

```json
{
  "id": "demo-app-private",
  "cmd": null,
  "cpus": 1,
  "mem": 32,
  "disk": 0,
  "instances": 3,
  "container": {
    "docker": {
      "image": "nginx",
      "network": "BRIDGE",
      "portMappings": [
        {
          "containerPort": 80,
          "protocol": "tcp",
          "name": "80",
          "labels": null
        }
      ]
    },
    "type": "DOCKER"
  }
}
```

<span data-ttu-id="92989-150">Mettre à jour d’application hello utilisant hello `dcos marathon app update` commande.</span><span class="sxs-lookup"><span data-stu-id="92989-150">Update hello application using hello `dcos marathon app update` command.</span></span>

```azurecli
dcos marathon app update demo-app-private < marathon-app.json
```

<span data-ttu-id="92989-151">état du déploiement toosee hello pour l’application hello, exécutez hello commande suivante.</span><span class="sxs-lookup"><span data-stu-id="92989-151">toosee hello deployment status for hello app, run hello following command.</span></span>

```azurecli
dcos marathon app list
```

<span data-ttu-id="92989-152">Hello lorsque **tâches** bascule de valeur de la colonne à partir de *1/3* trop*3/1*, déploiement d’application est terminée.</span><span class="sxs-lookup"><span data-stu-id="92989-152">When hello **TASKS** column value switches from *1/3* too*3/1*, application deployment has completed.</span></span>

```azurecli
ID     MEM  CPUS  TASKS  HEALTH  DEPLOYMENT  WAITING  CONTAINER  CMD   
/test   32   1     1/3    ---       ---      False      DOCKER   None
```

## <a name="run-internet-accessible-app"></a><span data-ttu-id="92989-153">Exécuter l’application accessible par Internet</span><span class="sxs-lookup"><span data-stu-id="92989-153">Run internet accessible app</span></span>

<span data-ttu-id="92989-154">Hello ACS DC/OS cluster se compose de deux ensembles de nœuds, un public qui est accessible sur hello internet et l’autre privée qui n’est pas accessible sur hello internet.</span><span class="sxs-lookup"><span data-stu-id="92989-154">hello ACS DC/OS cluster consists of two node sets, one public which is accessible on hello internet, and one private which is not accessible on hello internet.</span></span> <span data-ttu-id="92989-155">ensemble par défaut de Hello est nœuds privé de hello, qui a été utilisé dans le dernier exemple de hello.</span><span class="sxs-lookup"><span data-stu-id="92989-155">hello default set is hello private nodes, which was used in hello last example.</span></span>

<span data-ttu-id="92989-156">toomake une application accessible sur hello internet, déployez-les toohello nœud publique ensemble.</span><span class="sxs-lookup"><span data-stu-id="92989-156">toomake an application accessible on hello internet, deploy them toohello public node set.</span></span> <span data-ttu-id="92989-157">toodo, laissez-vous hello `acceptedResourceRoles` une valeur de l’objet `slave_public`.</span><span class="sxs-lookup"><span data-stu-id="92989-157">toodo so, give hello `acceptedResourceRoles` object a value of `slave_public`.</span></span>

<span data-ttu-id="92989-158">Créez un fichier nommé **nginx-public.json** et hello de copie suivant contenu dans celui-ci.</span><span class="sxs-lookup"><span data-stu-id="92989-158">Create a file named **nginx-public.json** and copy hello following contents into it.</span></span>

```json
{
  "id": "demo-app",
  "cmd": null,
  "cpus": 1,
  "mem": 32,
  "disk": 0,
  "instances": 1,
  "container": {
    "docker": {
      "image": "nginx",
      "network": "BRIDGE",
      "portMappings": [
        {
          "containerPort": 80,
          "hostPort": 80,
          "protocol": "tcp",
          "name": "80",
          "labels": null
        }
      ]
    },
    "type": "DOCKER"
  },
  "acceptedResourceRoles": [
    "slave_public"
  ]
}
```

<span data-ttu-id="92989-159">Exécutez hello suivant de commande tooschedule hello application toorun de cluster de contrôleur de domaine/système d’exploitation hello.</span><span class="sxs-lookup"><span data-stu-id="92989-159">Run hello following command tooschedule hello application toorun on hello DC/OS cluster.</span></span>

```azurecli 
dcos marathon app add nginx-public.json
```

<span data-ttu-id="92989-160">Obtenir l’adresse IP publique de hello d’agents de clusters public hello contrôleur de domaine/système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="92989-160">Get hello public IP address of hello DC/OS public cluster agents.</span></span>

```azurecli 
az network public-ip list --resource-group myResourceGroup --query "[?contains(name,'dcos-agent')].[ipAddress]" -o tsv
```

<span data-ttu-id="92989-161">Navigation toothis adresse retourne site NGINX hello par défaut.</span><span class="sxs-lookup"><span data-stu-id="92989-161">Browsing toothis address returns hello default NGINX site.</span></span>

![NGINX](./media/container-service-dcos-manage-tutorial/nginx.png)

## <a name="scale-dcos-cluster"></a><span data-ttu-id="92989-163">Mettre à l’échelle un cluster DC/OS</span><span class="sxs-lookup"><span data-stu-id="92989-163">Scale DC/OS cluster</span></span>

<span data-ttu-id="92989-164">Dans les exemples précédents hello, une application a été mis à l’échelle toomultiple instance.</span><span class="sxs-lookup"><span data-stu-id="92989-164">In hello previous examples, an application was scaled toomultiple instance.</span></span> <span data-ttu-id="92989-165">infrastructure de contrôleur de domaine/système d’exploitation Hello peut également être mis à l’échelle tooprovide plus ou moins de capacité de calcul.</span><span class="sxs-lookup"><span data-stu-id="92989-165">hello DC/OS infrastructure can also be scaled tooprovide more or less compute capacity.</span></span> <span data-ttu-id="92989-166">Cette opération s’effectue par hello [mettre à l’échelle des services acs az]() commande.</span><span class="sxs-lookup"><span data-stu-id="92989-166">This is done with hello [az acs scale]() command.</span></span> 

<span data-ttu-id="92989-167">Nombre actuel de hello toosee d’agents de contrôleur de domaine/système d’exploitation, utilisez hello [afficher d’acs az](/cli/azure/acs#show) commande.</span><span class="sxs-lookup"><span data-stu-id="92989-167">toosee hello current count of DC/OS agents, use hello [az acs show](/cli/azure/acs#show) command.</span></span>

```azurecli
az acs show --resource-group myResourceGroup --name myDCOSCluster --query "agentPoolProfiles[0].count"
```

<span data-ttu-id="92989-168">tooincrease hello nombre too5, utilisez hello [mettre à l’échelle des services acs az](/cli/azure/acs#scale) commande.</span><span class="sxs-lookup"><span data-stu-id="92989-168">tooincrease hello count too5, use hello [az acs scale](/cli/azure/acs#scale) command.</span></span> 

```azurecli
az acs scale --resource-group myResourceGroup --name myDCOSCluster --new-agent-count 5
```

## <a name="delete-dcos-cluster"></a><span data-ttu-id="92989-169">Supprimer un cluster DC/OS</span><span class="sxs-lookup"><span data-stu-id="92989-169">Delete DC/OS cluster</span></span>

<span data-ttu-id="92989-170">Lorsque vous n’est plus nécessaire, vous pouvez utiliser hello [suppression du groupe az](/cli/azure/group#delete) groupe de ressources tooremove hello, cluster de contrôleur de domaine/système d’exploitation et toutes les ressources de la commande.</span><span class="sxs-lookup"><span data-stu-id="92989-170">When no longer needed, you can use hello [az group delete](/cli/azure/group#delete) command tooremove hello resource group, DC/OS cluster, and all related resources.</span></span>

```azurecli 
az group delete --name myResourceGroup --no-wait
```

## <a name="next-steps"></a><span data-ttu-id="92989-171">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="92989-171">Next steps</span></span>

<span data-ttu-id="92989-172">Dans ce didacticiel, vous avez appris à propos de la tâche de gestion de contrôleur de domaine/système d’exploitation de base notamment hello suivantes.</span><span class="sxs-lookup"><span data-stu-id="92989-172">In this tutorial, you have learned about basic DC/OS management task including hello following.</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="92989-173">Créer un cluster ACS DC/OS</span><span class="sxs-lookup"><span data-stu-id="92989-173">Create an ACS DC/OS cluster</span></span>
> * <span data-ttu-id="92989-174">Se connecter toohello cluster</span><span class="sxs-lookup"><span data-stu-id="92989-174">Connect toohello cluster</span></span>
> * <span data-ttu-id="92989-175">Installer hello CLI de contrôleur de domaine/système d’exploitation</span><span class="sxs-lookup"><span data-stu-id="92989-175">Install hello DC/OS CLI</span></span>
> * <span data-ttu-id="92989-176">Déployer un cluster de toohello d’application</span><span class="sxs-lookup"><span data-stu-id="92989-176">Deploy an application toohello cluster</span></span>
> * <span data-ttu-id="92989-177">L’échelle d’une application sur un cluster de hello</span><span class="sxs-lookup"><span data-stu-id="92989-177">Scale an application on hello cluster</span></span>
> * <span data-ttu-id="92989-178">Mettre à l’échelle des nœuds de cluster de contrôleur de domaine/système d’exploitation hello</span><span class="sxs-lookup"><span data-stu-id="92989-178">Scale hello DC/OS cluster nodes</span></span>
> * <span data-ttu-id="92989-179">Supprimer le cluster de contrôleur de domaine/système d’exploitation hello</span><span class="sxs-lookup"><span data-stu-id="92989-179">Delete hello DC/OS cluster</span></span>

<span data-ttu-id="92989-180">Avance toohello suivant didacticiel toolearn sur Charger équilibrage d’application dans le contrôleur de domaine/système d’exploitation sur Azure.</span><span class="sxs-lookup"><span data-stu-id="92989-180">Advance toohello next tutorial toolearn about load balancing application in DC/OS on Azure.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="92989-181">Équilibrer la charge des applications</span><span class="sxs-lookup"><span data-stu-id="92989-181">Load balance applications</span></span>](container-service-load-balancing.md)