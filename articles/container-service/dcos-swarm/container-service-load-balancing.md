---
title: "Équilibrer la charge des conteneurs dans un cluster DC/OS Azure | Microsoft Docs"
description: "Équilibrer la charge de plusieurs conteneurs dans un cluster DC/OS Azure Container Service."
services: container-service
documentationcenter: 
author: rgardler
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Conteneurs, micro-services, DC/OS, Azure
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/02/2017
ms.author: rogardle
ms.custom: mvc
ms.openlocfilehash: 78725c9d23e13d307821a188028ef573d1def038
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="load-balance-containers-in-an-azure-container-service-dcos-cluster"></a><span data-ttu-id="013e4-104">Équilibrer la charge des conteneurs dans un cluster DC/OS Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="013e4-104">Load balance containers in an Azure Container Service DC/OS cluster</span></span>
<span data-ttu-id="013e4-105">Dans cet article, nous étudions comment créer un équilibreur de charge interne dans un cluster Azure Container Service géré par DC/OS à l’aide de Marathon-LB.</span><span class="sxs-lookup"><span data-stu-id="013e4-105">In this article, we explore how to create an internal load balancer in a DC/OS managed Azure Container Service using Marathon-LB.</span></span> <span data-ttu-id="013e4-106">Cette configuration vous permet de mettre à l’échelle vos applications horizontalement.</span><span class="sxs-lookup"><span data-stu-id="013e4-106">This configuration enables you to scale your applications horizontally.</span></span> <span data-ttu-id="013e4-107">Elle vous permet également de tirer parti des clusters d’agents publics et privés en plaçant vos équilibreurs de charge sur le cluster public et vos conteneurs d’applications sur le cluster privé.</span><span class="sxs-lookup"><span data-stu-id="013e4-107">It also allows you to take advantage of the public and private agent clusters by placing your load balancers on the public cluster and your application containers on the private cluster.</span></span> <span data-ttu-id="013e4-108">Dans ce didacticiel, vous avez appris à effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="013e4-108">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="013e4-109">Configurer un équilibreur de charge Marathon</span><span class="sxs-lookup"><span data-stu-id="013e4-109">Configure a Marathon Load Balancer</span></span>
> * <span data-ttu-id="013e4-110">Déployer une application à l’aide de l’équilibreur de charge</span><span class="sxs-lookup"><span data-stu-id="013e4-110">Deploy an application using the load balancer</span></span>
> * <span data-ttu-id="013e4-111">Configurer un équilibreur de charge Azure</span><span class="sxs-lookup"><span data-stu-id="013e4-111">Configure and Azure load balancer</span></span>

<span data-ttu-id="013e4-112">Vous avez besoin d’un cluster DC/OS ACS pour suivre les étapes de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="013e4-112">You need an ACS DC/OS cluster to complete the steps in this tutorial.</span></span> <span data-ttu-id="013e4-113">Le cas échéant, cet [exemple de script](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) peut en créer un pour vous.</span><span class="sxs-lookup"><span data-stu-id="013e4-113">If needed, [this script sample](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) can create one for you.</span></span>

<span data-ttu-id="013e4-114">Ce didacticiel requiert Azure CLI version 2.0.4 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="013e4-114">This tutorial requires the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="013e4-115">Exécutez `az --version` pour trouver la version.</span><span class="sxs-lookup"><span data-stu-id="013e4-115">Run `az --version` to find the version.</span></span> <span data-ttu-id="013e4-116">Si vous devez mettre à niveau, consultez [Installation d’Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="013e4-116">If you need to upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="load-balancing-overview"></a><span data-ttu-id="013e4-117">Vue d’ensemble de l’équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="013e4-117">Load balancing overview</span></span>

<span data-ttu-id="013e4-118">Il existe deux couches d’équilibrage de charge dans un cluster DC/OS Azure Container Service :</span><span class="sxs-lookup"><span data-stu-id="013e4-118">There are two load-balancing layers in an Azure Container Service DC/OS cluster:</span></span> 

<span data-ttu-id="013e4-119">**Azure Load Balancer** fournit des points d’entrée publics (ceux auxquels les utilisateurs finaux ont accès).</span><span class="sxs-lookup"><span data-stu-id="013e4-119">**Azure Load Balancer** provides public entry points (the ones that end users access).</span></span> <span data-ttu-id="013e4-120">Un équilibreur de charge Azure Load Balancer est automatiquement fourni par Azure Container Service. Par défaut, il est configuré pour exposer les ports 80, 443 et 8080.</span><span class="sxs-lookup"><span data-stu-id="013e4-120">An Azure LB is provided automatically by Azure Container Service and is, by default, configured to expose port 80, 443 and 8080.</span></span>

<span data-ttu-id="013e4-121">L’outil **Marathon Load Balancer (marathon-lb)** achemine les demandes entrantes vers les instances de conteneur qui traitent ces demandes.</span><span class="sxs-lookup"><span data-stu-id="013e4-121">**The Marathon Load Balancer (marathon-lb)** routes inbound requests to container instances that service these requests.</span></span> <span data-ttu-id="013e4-122">L’outil marathon-lb s’adapte dynamiquement au fur et à mesure que les conteneurs fournissant notre service web sont mis à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="013e4-122">As we scale the containers providing our web service, the marathon-lb dynamically adapts.</span></span> <span data-ttu-id="013e4-123">Par défaut, cet équilibreur de charge n’est pas fourni dans votre service Container Service, mais il est facile à installer.</span><span class="sxs-lookup"><span data-stu-id="013e4-123">This load balancer is not provided by default in your Container Service, but it is easy to install.</span></span>

## <a name="configure-marathon-load-balancer"></a><span data-ttu-id="013e4-124">Configurer un équilibreur de charge Marathon</span><span class="sxs-lookup"><span data-stu-id="013e4-124">Configure Marathon Load Balancer</span></span>

<span data-ttu-id="013e4-125">L’équilibreur de charge Marathon se reconfigure dynamiquement en fonction des conteneurs que vous avez déployés.</span><span class="sxs-lookup"><span data-stu-id="013e4-125">Marathon Load Balancer dynamically reconfigures itself based on the containers that you've deployed.</span></span> <span data-ttu-id="013e4-126">Il est également résistant à la perte d’un conteneur ou d’un agent. Le cas échéant, Apache Mesos redémarre le conteneur ailleurs et l’outil marathon-lb s’adapte.</span><span class="sxs-lookup"><span data-stu-id="013e4-126">It's also resilient to the loss of a container or an agent - if this occurs, Apache Mesos restarts the container elsewhere and marathon-lb adapts.</span></span>

<span data-ttu-id="013e4-127">Exécutez la commande suivante pour installer l’équilibreur de charge marathon sur le cluster de l’agent public.</span><span class="sxs-lookup"><span data-stu-id="013e4-127">Run the following command to install the marathon load balancer on the public agent's cluster.</span></span>

```azurecli-interactive
dcos package install marathon-lb
```

## <a name="deploy-load-balanced-application"></a><span data-ttu-id="013e4-128">Déployer une application à charge équilibrée</span><span class="sxs-lookup"><span data-stu-id="013e4-128">Deploy load balanced application</span></span>

<span data-ttu-id="013e4-129">Maintenant que nous avons le package marathon-lb, nous pouvons déployer le conteneur d’applications dont nous souhaitons équilibrer la charge.</span><span class="sxs-lookup"><span data-stu-id="013e4-129">Now that we have the marathon-lb package, we can deploy an application container that we wish to load balance.</span></span> 

<span data-ttu-id="013e4-130">Tout d’abord, obtenez le nom de domaine complet des agents exposés publiquement.</span><span class="sxs-lookup"><span data-stu-id="013e4-130">First, get the FQDN of the publicly exposed agents.</span></span>

```azurecli-interactive
az acs list --resource-group myResourceGroup --query "[0].agentPoolProfiles[0].fqdn" --output tsv
```

<span data-ttu-id="013e4-131">Ensuite, créez un fichier nommé *hello-web.json* et copiez-y le contenu suivant.</span><span class="sxs-lookup"><span data-stu-id="013e4-131">Next, create a file named *hello-web.json* and copy in the following contents.</span></span> <span data-ttu-id="013e4-132">L’étiquette `HAPROXY_0_VHOST` doit être mise à jour avec le nom de domaine complet des agents DC/OS.</span><span class="sxs-lookup"><span data-stu-id="013e4-132">The `HAPROXY_0_VHOST` label needs to be updated with the FQDN of the DC/OS agents.</span></span> 

```json
{
  "id": "web",
  "container": {
    "type": "DOCKER",
    "docker": {
      "image": "yeasy/simple-web",
      "network": "BRIDGE",
      "portMappings": [
        { "hostPort": 0, "containerPort": 80, "servicePort": 10000 }
      ],
      "forcePullImage":true
    }
  },
  "instances": 3,
  "cpus": 0.1,
  "mem": 65,
  "healthChecks": [{
      "protocol": "HTTP",
      "path": "/",
      "portIndex": 0,
      "timeoutSeconds": 10,
      "gracePeriodSeconds": 10,
      "intervalSeconds": 2,
      "maxConsecutiveFailures": 10
  }],
  "labels":{
    "HAPROXY_GROUP":"external",
    "HAPROXY_0_VHOST":"YOUR FQDN",
    "HAPROXY_0_MODE":"http"
  }
}
```

<span data-ttu-id="013e4-133">Utilisez l’interface de ligne de commande DC/OS pour exécuter l’application.</span><span class="sxs-lookup"><span data-stu-id="013e4-133">Use the DC/OS CLI to run the application.</span></span> <span data-ttu-id="013e4-134">Par défaut, Marathon déploie l’application dans le cluster privé.</span><span class="sxs-lookup"><span data-stu-id="013e4-134">By default Marathon deploys the the applicaton to the private cluster.</span></span> <span data-ttu-id="013e4-135">Cela signifie que le déploiement ci-dessus est uniquement accessible via votre équilibreur de charge, ce qui correspond généralement au comportement souhaité.</span><span class="sxs-lookup"><span data-stu-id="013e4-135">This means that the above deployment is only accessible via your load balancer, which is usually the desired behavior.</span></span>

```azurecli-interactive
dcos marathon app add hello-web.json
```

<span data-ttu-id="013e4-136">Une fois que l’application a été déployée, recherchez le nom de domaine complet du cluster d’agents pour afficher l’application à charge équilibrée.</span><span class="sxs-lookup"><span data-stu-id="013e4-136">Once the application has been deployed, browse to the FQDN of the agent cluster to view load balanced application.</span></span>

![Image de l’application à charge équilibrée](./media/container-service-load-balancing/lb-app.png)

## <a name="configure-azure-load-balancer"></a><span data-ttu-id="013e4-138">Configurer Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="013e4-138">Configure Azure Load Balancer</span></span>

<span data-ttu-id="013e4-139">Par défaut, Azure Load Balancer expose les ports 80, 8080 et 443.</span><span class="sxs-lookup"><span data-stu-id="013e4-139">By default, Azure Load Balancer exposes ports 80, 8080, and 443.</span></span> <span data-ttu-id="013e4-140">Si vous utilisez l’un de ces trois ports (comme nous le faisons dans l’exemple ci-dessus), vous n’avez rien à faire.</span><span class="sxs-lookup"><span data-stu-id="013e4-140">If you're using one of these three ports (as we do in the above example), then there is nothing you need to do.</span></span> <span data-ttu-id="013e4-141">Vous devez pouvoir accéder au nom de domaine complet de l’équilibreur de charge de votre agent. À chaque actualisation, vous accéderez à l’un de vos trois serveurs web selon le principe du tourniquet (round robin).</span><span class="sxs-lookup"><span data-stu-id="013e4-141">You should be able to hit your agent load balancer's FQDN, and each time you refresh, you'll hit one of your three web servers in a round-robin fashion.</span></span> 

<span data-ttu-id="013e4-142">Si vous utilisez un port différent, vous devez ajouter une règle de tourniquet et une sonde sur l’équilibreur de charge pour le port que vous avez utilisé.</span><span class="sxs-lookup"><span data-stu-id="013e4-142">If you use a different port, you need to add a round-robin rule and a probe on the load balancer for the port that you used.</span></span> <span data-ttu-id="013e4-143">Vous pouvez le faire depuis [l’interface de ligne de commande (CLI) Azure](../../azure-resource-manager/xplat-cli-azure-resource-manager.md), avec les commandes `azure network lb rule create` et `azure network lb probe create`.</span><span class="sxs-lookup"><span data-stu-id="013e4-143">You can do this from the [Azure CLI](../../azure-resource-manager/xplat-cli-azure-resource-manager.md), with the commands `azure network lb rule create` and `azure network lb probe create`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="013e4-144">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="013e4-144">Next steps</span></span>

<span data-ttu-id="013e4-145">Dans ce didacticiel, vous avez découvert l’équilibrage de charge dans ACS avec les équilibreurs de charge Marathon et Azure, y compris les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="013e4-145">In this tutorial, you learned about load balancing in ACS with both the Marathon and Azure load balancers including the following actions:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="013e4-146">Configurer un équilibreur de charge Marathon</span><span class="sxs-lookup"><span data-stu-id="013e4-146">Configure a Marathon Load Balancer</span></span>
> * <span data-ttu-id="013e4-147">Déployer une application à l’aide de l’équilibreur de charge</span><span class="sxs-lookup"><span data-stu-id="013e4-147">Deploy an application using the load balancer</span></span>
> * <span data-ttu-id="013e4-148">Configurer un équilibreur de charge Azure</span><span class="sxs-lookup"><span data-stu-id="013e4-148">Configure and Azure load balancer</span></span>

<span data-ttu-id="013e4-149">Passez au didacticiel suivant pour en savoir plus sur l’intégration du stockage Azure à DC/OS dans Azure.</span><span class="sxs-lookup"><span data-stu-id="013e4-149">Advance to the next tutorial to learn about integrating Azure storage with DC/OS in Azure.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="013e4-150">Monter un partage de fichiers Azure dans un cluster DC/OS</span><span class="sxs-lookup"><span data-stu-id="013e4-150">Mount Azure File Share in DC/OS cluster</span></span>](container-service-dcos-fileshare.md)