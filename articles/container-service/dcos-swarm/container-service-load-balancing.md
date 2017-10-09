---
title: "conteneurs de solde aaaLoad dans un cluster de contrôleur de domaine/système d’exploitation Azure | Documents Microsoft"
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
ms.openlocfilehash: 2249cb06880cdb7e9a3aa94c0750c6a27316d349
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="load-balance-containers-in-an-azure-container-service-dcos-cluster"></a><span data-ttu-id="c7412-104">Équilibrer la charge des conteneurs dans un cluster DC/OS Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="c7412-104">Load balance containers in an Azure Container Service DC/OS cluster</span></span>
<span data-ttu-id="c7412-105">Dans cet article, nous explorons comment toocreate un équilibreur de charge interne dans un contrôleur de domaine/système d’exploitation géré Azure Service de conteneur à l’aide de Marathon kg.</span><span class="sxs-lookup"><span data-stu-id="c7412-105">In this article, we explore how toocreate an internal load balancer in a DC/OS managed Azure Container Service using Marathon-LB.</span></span> <span data-ttu-id="c7412-106">Cette configuration permet de vous tooscale vos applications horizontalement.</span><span class="sxs-lookup"><span data-stu-id="c7412-106">This configuration enables you tooscale your applications horizontally.</span></span> <span data-ttu-id="c7412-107">Il vous permet également parti tootake de clusters public et privé de l’agent de hello en plaçant les équilibreurs de charge sur les clusters public hello et vos conteneurs d’applications sur les clusters privé hello.</span><span class="sxs-lookup"><span data-stu-id="c7412-107">It also allows you tootake advantage of hello public and private agent clusters by placing your load balancers on hello public cluster and your application containers on hello private cluster.</span></span> <span data-ttu-id="c7412-108">Dans ce didacticiel, vous avez appris à effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="c7412-108">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="c7412-109">Configurer un équilibreur de charge Marathon</span><span class="sxs-lookup"><span data-stu-id="c7412-109">Configure a Marathon Load Balancer</span></span>
> * <span data-ttu-id="c7412-110">Déployer une application à l’aide d’équilibrage de charge hello</span><span class="sxs-lookup"><span data-stu-id="c7412-110">Deploy an application using hello load balancer</span></span>
> * <span data-ttu-id="c7412-111">Configurer un équilibreur de charge Azure</span><span class="sxs-lookup"><span data-stu-id="c7412-111">Configure and Azure load balancer</span></span>

<span data-ttu-id="c7412-112">Vous avez besoin d’un contrôleur de domaine/OS ACS hello toocomplete de cluster les étapes de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="c7412-112">You need an ACS DC/OS cluster toocomplete hello steps in this tutorial.</span></span> <span data-ttu-id="c7412-113">Le cas échéant, cet [exemple de script](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) peut en créer un pour vous.</span><span class="sxs-lookup"><span data-stu-id="c7412-113">If needed, [this script sample](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) can create one for you.</span></span>

<span data-ttu-id="c7412-114">Ce didacticiel requiert hello CLI d’Azure version 2.0.4 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="c7412-114">This tutorial requires hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="c7412-115">Exécutez `az --version` version de hello toofind.</span><span class="sxs-lookup"><span data-stu-id="c7412-115">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="c7412-116">Si vous avez besoin de tooupgrade, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="c7412-116">If you need tooupgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="load-balancing-overview"></a><span data-ttu-id="c7412-117">Vue d’ensemble de l’équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="c7412-117">Load balancing overview</span></span>

<span data-ttu-id="c7412-118">Il existe deux couches d’équilibrage de charge dans un cluster DC/OS Azure Container Service :</span><span class="sxs-lookup"><span data-stu-id="c7412-118">There are two load-balancing layers in an Azure Container Service DC/OS cluster:</span></span> 

<span data-ttu-id="c7412-119">**Équilibrage de charge Azure** fournit des points d’entrée publics (hello celles que les utilisateurs finaux d’accès).</span><span class="sxs-lookup"><span data-stu-id="c7412-119">**Azure Load Balancer** provides public entry points (hello ones that end users access).</span></span> <span data-ttu-id="c7412-120">Un équilibrage de charge Azure est fourni automatiquement par le Service de conteneur Azure et est, par défaut, le port configuré tooexpose 80, 443 et 8080.</span><span class="sxs-lookup"><span data-stu-id="c7412-120">An Azure LB is provided automatically by Azure Container Service and is, by default, configured tooexpose port 80, 443 and 8080.</span></span>

<span data-ttu-id="c7412-121">**Hello Marathon équilibrage de charge (marathon kg)** itinéraires entrant instances toocontainer demandes ces demandes de service.</span><span class="sxs-lookup"><span data-stu-id="c7412-121">**hello Marathon Load Balancer (marathon-lb)** routes inbound requests toocontainer instances that service these requests.</span></span> <span data-ttu-id="c7412-122">Comme nous l’échelle conteneurs hello fournissant notre service web, hello marathon kg s’adapte dynamiquement.</span><span class="sxs-lookup"><span data-stu-id="c7412-122">As we scale hello containers providing our web service, hello marathon-lb dynamically adapts.</span></span> <span data-ttu-id="c7412-123">Cet équilibrage de charge n’est pas fourni par défaut dans votre Service de conteneur, mais il est facile tooinstall.</span><span class="sxs-lookup"><span data-stu-id="c7412-123">This load balancer is not provided by default in your Container Service, but it is easy tooinstall.</span></span>

## <a name="configure-marathon-load-balancer"></a><span data-ttu-id="c7412-124">Configurer un équilibreur de charge Marathon</span><span class="sxs-lookup"><span data-stu-id="c7412-124">Configure Marathon Load Balancer</span></span>

<span data-ttu-id="c7412-125">Équilibrage de charge marathon reconfigure dynamiquement elle-même en se basant sur les conteneurs hello que vous avez déployés.</span><span class="sxs-lookup"><span data-stu-id="c7412-125">Marathon Load Balancer dynamically reconfigures itself based on hello containers that you've deployed.</span></span> <span data-ttu-id="c7412-126">Il est également perte résilient toohello d’un conteneur ou un agent - si cela se produit, Apache Mesos redémarre conteneur hello ailleurs et marathon kg adapte.</span><span class="sxs-lookup"><span data-stu-id="c7412-126">It's also resilient toohello loss of a container or an agent - if this occurs, Apache Mesos restarts hello container elsewhere and marathon-lb adapts.</span></span>

<span data-ttu-id="c7412-127">Exécutez hello suivant d’équilibrage de charge de commande tooinstall hello marathon sur le cluster de l’agent hello publique.</span><span class="sxs-lookup"><span data-stu-id="c7412-127">Run hello following command tooinstall hello marathon load balancer on hello public agent's cluster.</span></span>

```azurecli-interactive
dcos package install marathon-lb
```

## <a name="deploy-load-balanced-application"></a><span data-ttu-id="c7412-128">Déployer une application à charge équilibrée</span><span class="sxs-lookup"><span data-stu-id="c7412-128">Deploy load balanced application</span></span>

<span data-ttu-id="c7412-129">Maintenant que nous avons package kg marathon de hello, nous pouvons déployer un conteneur d’application que nous souhaitons solde de tooload.</span><span class="sxs-lookup"><span data-stu-id="c7412-129">Now that we have hello marathon-lb package, we can deploy an application container that we wish tooload balance.</span></span> 

<span data-ttu-id="c7412-130">Tout d’abord, obtenez hello nom de domaine complet d’agents de hello exposée publiquement.</span><span class="sxs-lookup"><span data-stu-id="c7412-130">First, get hello FQDN of hello publicly exposed agents.</span></span>

```azurecli-interactive
az acs list --resource-group myResourceGroup --query "[0].agentPoolProfiles[0].fqdn" --output tsv
```

<span data-ttu-id="c7412-131">Ensuite, créez un fichier nommé *hello-web.json* et copie Bonjour suivant le contenu.</span><span class="sxs-lookup"><span data-stu-id="c7412-131">Next, create a file named *hello-web.json* and copy in hello following contents.</span></span> <span data-ttu-id="c7412-132">Hello `HAPROXY_0_VHOST` étiquette doit toobe mis à jour avec hello nom de domaine complet d’agents de contrôleur de domaine/système d’exploitation hello.</span><span class="sxs-lookup"><span data-stu-id="c7412-132">hello `HAPROXY_0_VHOST` label needs toobe updated with hello FQDN of hello DC/OS agents.</span></span> 

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

<span data-ttu-id="c7412-133">Utilisez application de hello toorun hello CLI de contrôleur de domaine/système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="c7412-133">Use hello DC/OS CLI toorun hello application.</span></span> <span data-ttu-id="c7412-134">Par défaut Marathon déploie hello hello application toohello privé de clusters.</span><span class="sxs-lookup"><span data-stu-id="c7412-134">By default Marathon deploys hello hello applicaton toohello private cluster.</span></span> <span data-ttu-id="c7412-135">Cela signifie que hello au-dessus de déploiement est uniquement accessible via votre équilibreur de charge, qui est généralement le comportement de hello souhaité.</span><span class="sxs-lookup"><span data-stu-id="c7412-135">This means that hello above deployment is only accessible via your load balancer, which is usually hello desired behavior.</span></span>

```azurecli-interactive
dcos marathon app add hello-web.json
```

<span data-ttu-id="c7412-136">Une fois que l’application hello a été déployée, parcourir toohello FQDN de l’application à charge équilibrée de hello agent cluster tooview.</span><span class="sxs-lookup"><span data-stu-id="c7412-136">Once hello application has been deployed, browse toohello FQDN of hello agent cluster tooview load balanced application.</span></span>

![Image de l’application à charge équilibrée](./media/container-service-load-balancing/lb-app.png)

## <a name="configure-azure-load-balancer"></a><span data-ttu-id="c7412-138">Configurer Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="c7412-138">Configure Azure Load Balancer</span></span>

<span data-ttu-id="c7412-139">Par défaut, Azure Load Balancer expose les ports 80, 8080 et 443.</span><span class="sxs-lookup"><span data-stu-id="c7412-139">By default, Azure Load Balancer exposes ports 80, 8080, and 443.</span></span> <span data-ttu-id="c7412-140">Si vous utilisez une de ces trois ports (comme nous le faisons Bonjour à l’exemple ci-dessus), alors il n’avez rien toodo.</span><span class="sxs-lookup"><span data-stu-id="c7412-140">If you're using one of these three ports (as we do in hello above example), then there is nothing you need toodo.</span></span> <span data-ttu-id="c7412-141">Vous devez être en mesure de toohit nom de domaine complet de l’équilibrage de charge de votre agent, et chaque fois que vous actualisez, vous devez appuyer sur un de vos serveurs trois web dans un tourniquet.</span><span class="sxs-lookup"><span data-stu-id="c7412-141">You should be able toohit your agent load balancer's FQDN, and each time you refresh, you'll hit one of your three web servers in a round-robin fashion.</span></span> 

<span data-ttu-id="c7412-142">Si vous utilisez un autre port, vous devez tooadd un tourniquet règle et une sonde d’équilibrage de charge hello pour le port hello que vous avez utilisé.</span><span class="sxs-lookup"><span data-stu-id="c7412-142">If you use a different port, you need tooadd a round-robin rule and a probe on hello load balancer for hello port that you used.</span></span> <span data-ttu-id="c7412-143">Vous pouvez les spécifier cela via hello [CLI d’Azure](../../azure-resource-manager/xplat-cli-azure-resource-manager.md), avec les commandes hello `azure network lb rule create` et `azure network lb probe create`.</span><span class="sxs-lookup"><span data-stu-id="c7412-143">You can do this from hello [Azure CLI](../../azure-resource-manager/xplat-cli-azure-resource-manager.md), with hello commands `azure network lb rule create` and `azure network lb probe create`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c7412-144">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c7412-144">Next steps</span></span>

<span data-ttu-id="c7412-145">Dans ce didacticiel, vous avez appris dans ACS avec hello Marathon et charge Azure équilibrages notamment hello suit les actions d’équilibrage de charge :</span><span class="sxs-lookup"><span data-stu-id="c7412-145">In this tutorial, you learned about load balancing in ACS with both hello Marathon and Azure load balancers including hello following actions:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="c7412-146">Configurer un équilibreur de charge Marathon</span><span class="sxs-lookup"><span data-stu-id="c7412-146">Configure a Marathon Load Balancer</span></span>
> * <span data-ttu-id="c7412-147">Déployer une application à l’aide d’équilibrage de charge hello</span><span class="sxs-lookup"><span data-stu-id="c7412-147">Deploy an application using hello load balancer</span></span>
> * <span data-ttu-id="c7412-148">Configurer un équilibreur de charge Azure</span><span class="sxs-lookup"><span data-stu-id="c7412-148">Configure and Azure load balancer</span></span>

<span data-ttu-id="c7412-149">Avance toohello toolearn de didacticiel suivant sur l’intégration du stockage Azure avec contrôleur de domaine/système d’exploitation dans Azure.</span><span class="sxs-lookup"><span data-stu-id="c7412-149">Advance toohello next tutorial toolearn about integrating Azure storage with DC/OS in Azure.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c7412-150">Monter un partage de fichiers Azure dans un cluster DC/OS</span><span class="sxs-lookup"><span data-stu-id="c7412-150">Mount Azure File Share in DC/OS cluster</span></span>](container-service-dcos-fileshare.md)