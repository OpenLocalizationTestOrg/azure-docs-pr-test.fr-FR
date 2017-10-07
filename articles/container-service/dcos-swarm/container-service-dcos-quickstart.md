---
title: "aaaAzure démarrage rapide du conteneur de Service - déployer un Cluster de contrôleur de domaine/système d’exploitation | Documents Microsoft"
description: "Démarrage rapide avec Azure Container Service - Déployer un cluster DC/OS"
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
ms.topic: quickstart
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/04/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: b961f15bd73deeafda5a3fc25ab53c839195219b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-dcos-cluster"></a><span data-ttu-id="eba1a-104">Déployer un cluster DC/OS</span><span class="sxs-lookup"><span data-stu-id="eba1a-104">Deploy a DC/OS cluster</span></span>

<span data-ttu-id="eba1a-105">DC/OS propose une plateforme distribuée destinée à exécuter des applications en conteneur modernes.</span><span class="sxs-lookup"><span data-stu-id="eba1a-105">DC/OS provides a distributed platform for running modern and containerized applications.</span></span> <span data-ttu-id="eba1a-106">Avec Azure Container Service, l’approvisionnement d’un cluster DC/OS prêt pour la production est une opération simple et rapide.</span><span class="sxs-lookup"><span data-stu-id="eba1a-106">With Azure Container Service, provisioning of a production ready DC/OS cluster is simple and quick.</span></span> <span data-ttu-id="eba1a-107">Cette détails de démarrage rapide hello des étapes de base nécessaires toodeploy un cluster de contrôleur de domaine/système d’exploitation et de la charge de travail de base exécution.</span><span class="sxs-lookup"><span data-stu-id="eba1a-107">This quick start details hello basic steps needed toodeploy a DC/OS cluster and run basic workload.</span></span>

<span data-ttu-id="eba1a-108">Si vous n’avez pas d’abonnement Azure, créez un [compte gratuit](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) avant de commencer.</span><span class="sxs-lookup"><span data-stu-id="eba1a-108">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

<span data-ttu-id="eba1a-109">Ce didacticiel requiert hello CLI d’Azure version 2.0.4 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="eba1a-109">This tutorial requires hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="eba1a-110">Exécutez `az --version` version de hello toofind.</span><span class="sxs-lookup"><span data-stu-id="eba1a-110">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="eba1a-111">Si vous avez besoin de tooupgrade, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="eba1a-111">If you need tooupgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="log-in-tooazure"></a><span data-ttu-id="eba1a-112">Connectez-vous à tooAzure</span><span class="sxs-lookup"><span data-stu-id="eba1a-112">Log in tooAzure</span></span> 

<span data-ttu-id="eba1a-113">Connectez-vous à tooyour abonnement Azure avec hello [ouverture de session az](/cli/azure/#login) commande et suivez hello à l’écran.</span><span class="sxs-lookup"><span data-stu-id="eba1a-113">Log in tooyour Azure subscription with hello [az login](/cli/azure/#login) command and follow hello on-screen directions.</span></span>

```azurecli
az login
```

## <a name="create-a-resource-group"></a><span data-ttu-id="eba1a-114">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="eba1a-114">Create a resource group</span></span>

<span data-ttu-id="eba1a-115">Créer un groupe de ressources avec hello [création de groupe de az](/cli/azure/group#create) commande.</span><span class="sxs-lookup"><span data-stu-id="eba1a-115">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="eba1a-116">Un groupe de ressources Azure est un conteneur logique dans lequel les ressources Azure sont déployées et gérées.</span><span class="sxs-lookup"><span data-stu-id="eba1a-116">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="eba1a-117">Hello exemple suivant crée un groupe de ressources nommé *myResourceGroup* Bonjour *eastus* emplacement.</span><span class="sxs-lookup"><span data-stu-id="eba1a-117">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location.</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

## <a name="create-dcos-cluster"></a><span data-ttu-id="eba1a-118">Créer un cluster DC/OS</span><span class="sxs-lookup"><span data-stu-id="eba1a-118">Create DC/OS cluster</span></span>

<span data-ttu-id="eba1a-119">Créez un cluster de contrôleur de domaine/système d’exploitation avec hello [az acs créer](/cli/azure/acs#create) commande.</span><span class="sxs-lookup"><span data-stu-id="eba1a-119">Create a DC/OS cluster with hello [az acs create](/cli/azure/acs#create) command.</span></span>

<span data-ttu-id="eba1a-120">Hello exemple suivant crée un cluster de contrôleur de domaine/système d’exploitation nommé *myDCOSCluster* et crée des clés SSH s’ils n’existent pas déjà.</span><span class="sxs-lookup"><span data-stu-id="eba1a-120">hello following example creates a DC/OS cluster named *myDCOSCluster* and creates SSH keys if they do not already exist.</span></span> <span data-ttu-id="eba1a-121">toouse un ensemble spécifique de clés, utilisez hello `--ssh-key-value` option.</span><span class="sxs-lookup"><span data-stu-id="eba1a-121">toouse a specific set of keys, use hello `--ssh-key-value` option.</span></span>  

```azurecli
az acs create \
  --orchestrator-type dcos \
  --resource-group myResourceGroup \
  --name myDCOSCluster \
  --generate-ssh-keys
```

<span data-ttu-id="eba1a-122">Après quelques minutes, commande hello se termine et retourne des informations sur le déploiement de hello.</span><span class="sxs-lookup"><span data-stu-id="eba1a-122">After several minutes, hello command completes, and returns information about hello deployment.</span></span>

## <a name="connect-toodcos-cluster"></a><span data-ttu-id="eba1a-123">Connectez le cluster de tooDC/OS</span><span class="sxs-lookup"><span data-stu-id="eba1a-123">Connect tooDC/OS cluster</span></span>

<span data-ttu-id="eba1a-124">Dès lors qu’un cluster DC/OS est créé, il est accessible via un tunnel SSH.</span><span class="sxs-lookup"><span data-stu-id="eba1a-124">Once a DC/OS cluster has been created, it can be accesses through an SSH tunnel.</span></span> <span data-ttu-id="eba1a-125">Exécutez hello suivant commande tooreturn hello adresse IP publique du principal du contrôleur de domaine/système d’exploitation hello.</span><span class="sxs-lookup"><span data-stu-id="eba1a-125">Run hello following command tooreturn hello public IP address of hello DC/OS master.</span></span> <span data-ttu-id="eba1a-126">Cette adresse IP est stockée dans une variable et utilisée à l’étape suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="eba1a-126">This IP address is stored in a variable and used in hello next step.</span></span>

```azurecli
ip=$(az network public-ip list --resource-group myResourceGroup --query "[?contains(name,'dcos-master')].[ipAddress]" -o tsv)
```

<span data-ttu-id="eba1a-127">toocreate hello tunnel SSH, exécutez hello commande suivante et suivez hello les instructions à l’écran.</span><span class="sxs-lookup"><span data-stu-id="eba1a-127">toocreate hello SSH tunnel, run hello following command and follow hello on-screen instructions.</span></span> <span data-ttu-id="eba1a-128">Si le port 80 est déjà en cours d’utilisation, la commande hello échoue.</span><span class="sxs-lookup"><span data-stu-id="eba1a-128">If port 80 is already in use, hello command fails.</span></span> <span data-ttu-id="eba1a-129">Hello de mise à jour en tunnel tooone port pas en cours d’utilisation, telles que `85:localhost:80`.</span><span class="sxs-lookup"><span data-stu-id="eba1a-129">Update hello tunneled port tooone not in use, such as `85:localhost:80`.</span></span> 

```azurecli
sudo ssh -i ~/.ssh/id_rsa -fNL 80:localhost:80 -p 2200 azureuser@$ip
```

<span data-ttu-id="eba1a-130">tunnel SSH de Hello peut être testée en parcourant trop`http://localhost`.</span><span class="sxs-lookup"><span data-stu-id="eba1a-130">hello SSH tunnel can be tested by browsing too`http://localhost`.</span></span> <span data-ttu-id="eba1a-131">Si un port autre que 80 a été utilisé, ajuster hello emplacement toomatch.</span><span class="sxs-lookup"><span data-stu-id="eba1a-131">If a port other that 80 has been used, adjust hello location toomatch.</span></span> 

<span data-ttu-id="eba1a-132">Tunnel SSH de hello a été créé avec succès, portail de contrôleur de domaine/système d’exploitation hello est retournée.</span><span class="sxs-lookup"><span data-stu-id="eba1a-132">If hello SSH tunnel was successfully created, hello DC/OS portal is returned.</span></span>

![Interface utilisateur DC/OS](./media/container-service-dcos-quickstart/dcos-ui.png)

## <a name="install-dcos-cli"></a><span data-ttu-id="eba1a-134">Installer l’interface de ligne de commande DC/OS</span><span class="sxs-lookup"><span data-stu-id="eba1a-134">Install DC/OS CLI</span></span>

<span data-ttu-id="eba1a-135">interface de ligne de commande de contrôleur de domaine/système d’exploitation Hello est toomanage utilisé un cluster de contrôleur de domaine/système d’exploitation à partir de hello de ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="eba1a-135">hello DC/OS command line interface is used toomanage a DC/OS cluster from hello command-line.</span></span> <span data-ttu-id="eba1a-136">Installez hello cli de contrôleur de domaine/système d’exploitation à l’aide de hello [az acs dcos install-cli](/azure/acs/dcos#install-cli) commande.</span><span class="sxs-lookup"><span data-stu-id="eba1a-136">Install hello DC/OS cli using hello [az acs dcos install-cli](/azure/acs/dcos#install-cli) command.</span></span> <span data-ttu-id="eba1a-137">Si vous utilisez Azure CloudShell, hello CLI de contrôleur de domaine/système d’exploitation est déjà installé.</span><span class="sxs-lookup"><span data-stu-id="eba1a-137">If you are using Azure CloudShell, hello DC/OS CLI is already installed.</span></span> 

<span data-ttu-id="eba1a-138">Si vous exécutez hello CLI d’Azure sur macOS ou Linux, vous devrez peut-être commande hello toorun sudo.</span><span class="sxs-lookup"><span data-stu-id="eba1a-138">If you are running hello Azure CLI on macOS or Linux, you might need toorun hello command with sudo.</span></span>

```azurecli
az acs dcos install-cli
```

<span data-ttu-id="eba1a-139">Avant de hello que CLI peut être utilisé avec un cluster de hello, il doit être tunnel SSH de hello toouse configuré.</span><span class="sxs-lookup"><span data-stu-id="eba1a-139">Before hello CLI can be used with hello cluster, it must be configured toouse hello SSH tunnel.</span></span> <span data-ttu-id="eba1a-140">toodo exécuter donc hello commande suivante, en ajustant le port de hello si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="eba1a-140">toodo so, run hello following command, adjusting hello port if needed.</span></span>

```azurecli
dcos config set core.dcos_url http://localhost
```

## <a name="run-an-application"></a><span data-ttu-id="eba1a-141">Exécuter une application</span><span class="sxs-lookup"><span data-stu-id="eba1a-141">Run an application</span></span>

<span data-ttu-id="eba1a-142">mécanisme pour un cluster ACS contrôleur de domaine/système d’exploitation de planification de la valeur par défaut Hello est Marathon.</span><span class="sxs-lookup"><span data-stu-id="eba1a-142">hello default scheduling mechanism for an ACS DC/OS cluster is Marathon.</span></span> <span data-ttu-id="eba1a-143">Marathon est toostart utilisé une application et gérer l’état de l’application hello sur le cluster de contrôleur de domaine/système d’exploitation hello hello.</span><span class="sxs-lookup"><span data-stu-id="eba1a-143">Marathon is used toostart an application and manage hello state of hello application on hello DC/OS cluster.</span></span> <span data-ttu-id="eba1a-144">tooschedule une application via Marathon, créez un fichier nommé *marathon-app.json*, et en hello de copie suivant contenu dans celui-ci.</span><span class="sxs-lookup"><span data-stu-id="eba1a-144">tooschedule an application through Marathon, create a file named *marathon-app.json*, and copy hello following contents into it.</span></span> 

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

<span data-ttu-id="eba1a-145">Exécutez hello suivant de commande tooschedule hello application toorun de cluster de contrôleur de domaine/système d’exploitation hello.</span><span class="sxs-lookup"><span data-stu-id="eba1a-145">Run hello following command tooschedule hello application toorun on hello DC/OS cluster.</span></span>

```azurecli
dcos marathon app add marathon-app.json
```

<span data-ttu-id="eba1a-146">état du déploiement toosee hello pour l’application hello, exécutez hello commande suivante.</span><span class="sxs-lookup"><span data-stu-id="eba1a-146">toosee hello deployment status for hello app, run hello following command.</span></span>

```azurecli
dcos marathon app list
```

<span data-ttu-id="eba1a-147">Hello lorsque **attente** bascule de valeur de la colonne à partir de *True* trop*False*, déploiement d’application est terminée.</span><span class="sxs-lookup"><span data-stu-id="eba1a-147">When hello **WAITING** column value switches from *True* too*False*, application deployment has completed.</span></span>

```azurecli
ID     MEM  CPUS  TASKS  HEALTH  DEPLOYMENT  WAITING  CONTAINER  CMD   
/test   32   1     1/1    ---       ---      False      DOCKER   None
```

<span data-ttu-id="eba1a-148">Obtenir l’adresse IP publique de hello d’agents de cluster de contrôleur de domaine/système d’exploitation hello.</span><span class="sxs-lookup"><span data-stu-id="eba1a-148">Get hello public IP address of hello DC/OS cluster agents.</span></span>

```azurecli
az network public-ip list --resource-group myResourceGroup --query "[?contains(name,'dcos-agent')].[ipAddress]" -o tsv
```

<span data-ttu-id="eba1a-149">Navigation toothis adresse retourne site NGINX hello par défaut.</span><span class="sxs-lookup"><span data-stu-id="eba1a-149">Browsing toothis address returns hello default NGINX site.</span></span>

![NGINX](./media/container-service-dcos-quickstart/nginx.png)

## <a name="delete-dcos-cluster"></a><span data-ttu-id="eba1a-151">Supprimer un cluster DC/OS</span><span class="sxs-lookup"><span data-stu-id="eba1a-151">Delete DC/OS cluster</span></span>

<span data-ttu-id="eba1a-152">Lorsque vous n’est plus nécessaire, vous pouvez utiliser hello [suppression du groupe az](/cli/azure/group#delete) groupe de ressources tooremove hello, cluster de contrôleur de domaine/système d’exploitation et toutes les ressources de la commande.</span><span class="sxs-lookup"><span data-stu-id="eba1a-152">When no longer needed, you can use hello [az group delete](/cli/azure/group#delete) command tooremove hello resource group, DC/OS cluster, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup --no-wait
```

## <a name="next-steps"></a><span data-ttu-id="eba1a-153">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="eba1a-153">Next steps</span></span>

<span data-ttu-id="eba1a-154">Dans ce guide de démarrage rapide, vous avez déployé un cluster de contrôleur de domaine/système d’exploitation et exécutez un simple conteneur Docker sur le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="eba1a-154">In this quick start, you’ve deployed a DC/OS cluster and have run a simple Docker container on hello cluster.</span></span> <span data-ttu-id="eba1a-155">toolearn en savoir plus sur le Service de conteneur Azure, continuer toohello ACS didacticiels.</span><span class="sxs-lookup"><span data-stu-id="eba1a-155">toolearn more about Azure Container Service, continue toohello ACS tutorials.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="eba1a-156">Gérer un cluster ACS DC/OS</span><span class="sxs-lookup"><span data-stu-id="eba1a-156">Manage an ACS DC/OS Cluster</span></span>](container-service-dcos-manage-tutorial.md)