---
title: "Contrôler la validité d’une mise en production avec Vamp sur un cluster de contrôleur de domaine/système d’exploitation Azure | Documents Microsoft"
description: "Comment utiliser Vamp pour contrôler la validité de services de mise en production et appliquer un filtrage de trafic intelligent sur un cluster de contrôleur de domaine/système d’exploitation Azure Container Service"
services: container-service
author: gggina
manager: rasquill
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 04/17/2017
ms.author: rasquill
ms.custom: mvc
ms.openlocfilehash: 4a20091b59f2643ea71cce99c159a5075706e35d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="canary-release-microservices-with-vamp-on-an-azure-container-service-dcos-cluster"></a><span data-ttu-id="9f781-103">Contrôler la validité de microservices de mise en production avec Vamp sur un cluster de contrôleur de domaine/système d’exploitation Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="9f781-103">Canary release microservices with Vamp on an Azure Container Service DC/OS cluster</span></span>

<span data-ttu-id="9f781-104">Dans cette procédure pas à pas, nous configurons Vamp sur Azure Container Service avec un cluster de contrôleur de domaine/système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="9f781-104">In this walkthrough, we set up Vamp on Azure Container Service with a DC/OS cluster.</span></span> <span data-ttu-id="9f781-105">Nous contrôlons la validité de la mise en production du service de démonstration Vamp « sava », puis résolvons une incompatibilité du service avec Firefox en appliquant un filtrage de trafic intelligent.</span><span class="sxs-lookup"><span data-stu-id="9f781-105">We canary release the Vamp demo service "sava", and then resolve an incompatibility of the service with Firefox by applying smart traffic filtering.</span></span> 

> [!TIP] 
> <span data-ttu-id="9f781-106">Dans cette procédure pas à pas, Vamp s’exécute sur un cluster de contrôleur de domaine/système d’exploitation, mais vous pouvez également utiliser Vamp avec Kubernetes en tant qu’orchestrateur.</span><span class="sxs-lookup"><span data-stu-id="9f781-106">In this walkthrough Vamp runs on a DC/OS cluster, but you can also use Vamp with Kubernetes as the orchestrator.</span></span>
>

## <a name="about-canary-releases-and-vamp"></a><span data-ttu-id="9f781-107">À propos du contrôle de la validité des mises en production et de Vamp</span><span class="sxs-lookup"><span data-stu-id="9f781-107">About canary releases and Vamp</span></span>


<span data-ttu-id="9f781-108">Le [contrôle de la validité des mises en production](https://martinfowler.com/bliki/CanaryRelease.html) est une stratégie de déploiement intelligent adoptée par des entreprises innovantes telles que Netflix, Facebook et Spotify.</span><span class="sxs-lookup"><span data-stu-id="9f781-108">[Canary releasing](https://martinfowler.com/bliki/CanaryRelease.html) is a smart deployment strategy adopted by innovative organizations like Netflix, Facebook, and Spotify.</span></span> <span data-ttu-id="9f781-109">Cette approche est intéressante, car elle réduit les problèmes, introduit des filets de sécurité et stimule l’innovation.</span><span class="sxs-lookup"><span data-stu-id="9f781-109">It’s an approach that makes sense, because it reduces issues, introduces safety-nets, and increases innovation.</span></span> <span data-ttu-id="9f781-110">Alors pourquoi toutes les entreprises ne l’adoptent-elles pas ?</span><span class="sxs-lookup"><span data-stu-id="9f781-110">So why aren’t all companies using it?</span></span> <span data-ttu-id="9f781-111">L’extension d’un pipeline d’intégration continue/de livraison continue en vue d’inclure des stratégies de contrôle de validité ajoute de la complexité et nécessite une connaissance et une expérience approfondies du DevOps.</span><span class="sxs-lookup"><span data-stu-id="9f781-111">Extending a CI/CD pipeline to include canary strategies adds complexity, and requires extensive devops knowledge and experience.</span></span> <span data-ttu-id="9f781-112">Cela suffit à bloquer les organisations de taille modeste avant même la prise en main.</span><span class="sxs-lookup"><span data-stu-id="9f781-112">That’s enough to block smaller companies and enterprises alike before they even get started.</span></span> 

<span data-ttu-id="9f781-113">[Vamp](http://vamp.io/) est un système open source conçu pour faciliter cette transition et apporter les fonctionnalités de contrôle de validité des mises en production à votre planificateur de conteneur favori.</span><span class="sxs-lookup"><span data-stu-id="9f781-113">[Vamp](http://vamp.io/) is an open-source system designed to ease this transition and bring canary releasing features to your preferred container scheduler.</span></span> <span data-ttu-id="9f781-114">La fonctionnalité de contrôle de validité de Vamp va au-delà des déploiements basés sur un pourcentage.</span><span class="sxs-lookup"><span data-stu-id="9f781-114">Vamp’s canary functionality goes beyond percentage-based rollouts.</span></span> <span data-ttu-id="9f781-115">Le trafic peut être filtré et fractionné en fonction d’un vaste éventail de conditions, par exemple, pour cibler des utilisateurs, des plages d’adresses IP ou des appareils spécifiques.</span><span class="sxs-lookup"><span data-stu-id="9f781-115">Traffic can be filtered and split on a wide range of conditions, for example to target specific users, IP-ranges, or devices.</span></span> <span data-ttu-id="9f781-116">Vamp suit et analyse les métriques de performances, permettant ainsi une automatisation basée sur des données réelles.</span><span class="sxs-lookup"><span data-stu-id="9f781-116">Vamp tracks and analyzes performance metrics, allowing for automation based on real-world data.</span></span> <span data-ttu-id="9f781-117">Vous pouvez configurer une restauration automatique en cas d’erreurs ou mettre à l’échelle des variantes de service en fonction de la charge ou de la latence.</span><span class="sxs-lookup"><span data-stu-id="9f781-117">You can set up automatic rollback on errors, or scale individual service variants based on load or latency.</span></span>

## <a name="set-up-azure-container-service-with-dcos"></a><span data-ttu-id="9f781-118">Configurer Azure Container Service avec un contrôleur de domaine/système d’exploitation</span><span class="sxs-lookup"><span data-stu-id="9f781-118">Set up Azure Container Service with DC/OS</span></span>



1. <span data-ttu-id="9f781-119">[Déployez un cluster de contrôleur de domaine/système d’exploitation](container-service-deployment.md) avec un maître et deux agents de la taille par défaut.</span><span class="sxs-lookup"><span data-stu-id="9f781-119">[Deploy a DC/OS cluster](container-service-deployment.md) with one master and two agents of default size.</span></span> 

2. <span data-ttu-id="9f781-120">[Créez un tunnel SSH](../container-service-connect.md) pour vous connecter au cluster de contrôleur de domaine/système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="9f781-120">[Create an SSH tunnel](../container-service-connect.md) to connect to the DC/OS cluster.</span></span> <span data-ttu-id="9f781-121">Cet article suppose que vous effectuez un tunneling vers le cluster sur le port local 80.</span><span class="sxs-lookup"><span data-stu-id="9f781-121">This article assumes that you tunnel to the cluster on local port 80.</span></span>


## <a name="set-up-vamp"></a><span data-ttu-id="9f781-122">Configurer Vamp</span><span class="sxs-lookup"><span data-stu-id="9f781-122">Set up Vamp</span></span>

<span data-ttu-id="9f781-123">À présent que vous avez un cluster de contrôleur de domaine/système d’exploitation opérationnel, vous pouvez installer Vamp à partir de l’interface utilisateur du contrôleur de domaine/système d’exploitation (http://localhost:80).</span><span class="sxs-lookup"><span data-stu-id="9f781-123">Now that you have a running DC/OS cluster, you can install Vamp from the DC/OS UI (http://localhost:80).</span></span> 

![IU DC/OS](./media/container-service-dcos-vamp-canary-release/01_set_up_vamp.png)

<span data-ttu-id="9f781-125">L’installation s’effectue en deux étapes :</span><span class="sxs-lookup"><span data-stu-id="9f781-125">Installation is done in two stages:</span></span>

1. <span data-ttu-id="9f781-126">**Déploiement d’Elasticsearch**,</span><span class="sxs-lookup"><span data-stu-id="9f781-126">**Deploy Elasticsearch**.</span></span>

2. <span data-ttu-id="9f781-127">puis **déploiement de Vamp** en installant le package de l’univers du contrôleur de domaine/système d’exploitation Vamp.</span><span class="sxs-lookup"><span data-stu-id="9f781-127">Then **deploy Vamp** by installing the Vamp DC/OS universe package.</span></span>

### <a name="deploy-elasticsearch"></a><span data-ttu-id="9f781-128">Déployer Elasticsearch</span><span class="sxs-lookup"><span data-stu-id="9f781-128">Deploy Elasticsearch</span></span>

<span data-ttu-id="9f781-129">Vamp a besoin d’Elasticsearch pour la collecte et l’agrégation des métriques.</span><span class="sxs-lookup"><span data-stu-id="9f781-129">Vamp requires Elasticsearch for metrics collection and aggregation.</span></span> <span data-ttu-id="9f781-130">Vous pouvez utiliser les [images de Docker magneticio](https://hub.docker.com/r/magneticio/elastic/) pour déployer une pile Elasticsearch Vamp compatible.</span><span class="sxs-lookup"><span data-stu-id="9f781-130">You can use the [magneticio Docker images](https://hub.docker.com/r/magneticio/elastic/) to deploy a compatible Vamp Elasticsearch stack.</span></span>

1. <span data-ttu-id="9f781-131">Dans l’interface utilisateur du contrôleur de domaine/système d’exploitation, accédez à **Services**, puis cliquez sur **Déployer le service**.</span><span class="sxs-lookup"><span data-stu-id="9f781-131">In the DC/OS UI, go to **Services** and click **Deploy Service**.</span></span>

2. <span data-ttu-id="9f781-132">Dans la fenêtre contextuelle **Deploy New Service** (Déployer un nouveau service), sélectionnez **JSON mode** (mode JSON).</span><span class="sxs-lookup"><span data-stu-id="9f781-132">Select **JSON mode** from the **Deploy New Service** pop-up.</span></span>

  ![Sélectionnez le mode JSON](./media/container-service-dcos-vamp-canary-release/02_deploy_service_json_mode.png)

3. <span data-ttu-id="9f781-134">Collez dans le code JSON suivant.</span><span class="sxs-lookup"><span data-stu-id="9f781-134">Paste in the following JSON.</span></span> <span data-ttu-id="9f781-135">Cette configuration exécute le conteneur avec 1 Go de RAM et un contrôle d’intégrité de base sur le port Elasticsearch.</span><span class="sxs-lookup"><span data-stu-id="9f781-135">This configuration runs the container with 1 GB of RAM and a basic health check on the Elasticsearch port.</span></span>
  
  ```JSON
  {
    "id": "elasticsearch",
    "instances": 1,
    "cpus": 0.2,
    "mem": 1024.0,
    "container": {
      "docker": {
        "image": "magneticio/elastic:2.2",
        "network": "HOST",
        "forcePullImage": true
      }
    },
    "healthChecks": [
      {
        "protocol": "TCP",
        "gracePeriodSeconds": 30,
        "intervalSeconds": 10,
        "timeoutSeconds": 5,
        "port": 9200,
        "maxConsecutiveFailures": 0
      }
    ]
  }
  ```
  

3. <span data-ttu-id="9f781-136">Cliquez sur **Déployer**.</span><span class="sxs-lookup"><span data-stu-id="9f781-136">Click **Deploy**.</span></span>

  <span data-ttu-id="9f781-137">Le contrôleur de domaine/système d’exploitation déploie le conteneur Elasticsearch.</span><span class="sxs-lookup"><span data-stu-id="9f781-137">DC/OS deploys the Elasticsearch container.</span></span> <span data-ttu-id="9f781-138">Vous pouvez suivre la progression dans la page **Services**.</span><span class="sxs-lookup"><span data-stu-id="9f781-138">You can track progress on the **Services** page.</span></span>  

  ![déployer Elasticsearch](./media/container-service-dcos-vamp-canary-release/03_deply_elasticsearch.png)

### <a name="deploy-vamp"></a><span data-ttu-id="9f781-140">Déployer Vamp</span><span class="sxs-lookup"><span data-stu-id="9f781-140">Deploy Vamp</span></span>

<span data-ttu-id="9f781-141">Une fois qu’Elasticsearch est **en cours d’exécution**, vous pouvez ajouter le package de l’univers du contrôleur de domaine/système d’exploitation Vamp.</span><span class="sxs-lookup"><span data-stu-id="9f781-141">Once Elasticsearch reports as **Running**, you can add the Vamp DC/OS Universe package.</span></span> 

1. <span data-ttu-id="9f781-142">Accédez à **Univers**, puis recherchez **vamp**.</span><span class="sxs-lookup"><span data-stu-id="9f781-142">Go to **Universe** and search for **vamp**.</span></span> 
  <span data-ttu-id="9f781-143">![Vamp sur un univers de contrôleur de domaine/système d’exploitation](./media/container-service-dcos-vamp-canary-release/04_universe_deploy_vamp.png)</span><span class="sxs-lookup"><span data-stu-id="9f781-143">![Vamp on DC/OS universe](./media/container-service-dcos-vamp-canary-release/04_universe_deploy_vamp.png)</span></span>

2. <span data-ttu-id="9f781-144">Cliquez sur **Installer** en regard du package Vamp, puis choisissez **Installation avancée**.</span><span class="sxs-lookup"><span data-stu-id="9f781-144">Click **install** next to the vamp package, and choose **Advanced Installation**.</span></span>

3. <span data-ttu-id="9f781-145">Faites défiler vers le bas, puis entrez l’url elasticsearch suivante : `http://elasticsearch.marathon.mesos:9200`.</span><span class="sxs-lookup"><span data-stu-id="9f781-145">Scroll down and enter the following elasticsearch-url: `http://elasticsearch.marathon.mesos:9200`.</span></span> 

  ![Entrer l’URL d’Elasticsearch](./media/container-service-dcos-vamp-canary-release/05_universe_elasticsearch_url.png)

4. <span data-ttu-id="9f781-147">Cliquez sur **Vérifier et installer**, puis sur **Installer** pour lancer le déploiement.</span><span class="sxs-lookup"><span data-stu-id="9f781-147">Click **Review and Install**, then click **Install** to start the deployment.</span></span>  

  <span data-ttu-id="9f781-148">Le contrôleur de domaine/système d’exploitation déploie tous les composants Vamp requis.</span><span class="sxs-lookup"><span data-stu-id="9f781-148">DC/OS deploys all required Vamp components.</span></span> <span data-ttu-id="9f781-149">Vous pouvez suivre la progression dans la page **Services**.</span><span class="sxs-lookup"><span data-stu-id="9f781-149">You can track progress on the **Services** page.</span></span>
  
  ![Déployer Vamp en tant que package d’univers](./media/container-service-dcos-vamp-canary-release/06_deploy_vamp.png)
  
5. <span data-ttu-id="9f781-151">Une fois le déploiement terminé, vous pouvez accéder à l’interface utilisateur de Vamp :</span><span class="sxs-lookup"><span data-stu-id="9f781-151">Once deployment has completed, you can access the Vamp UI:</span></span>

  ![Service Vamp sur contrôleur de domaine/système d’exploitation](./media/container-service-dcos-vamp-canary-release/07_deploy_vamp_complete.png)
  
  ![Interface utilisateur de Vamp](./media/container-service-dcos-vamp-canary-release/08_vamp_ui.png)


## <a name="deploy-your-first-service"></a><span data-ttu-id="9f781-154">Déployer votre premier service</span><span class="sxs-lookup"><span data-stu-id="9f781-154">Deploy your first service</span></span>

<span data-ttu-id="9f781-155">À présent que Vamp est opérationnel, déployez un service à partir d’un schéma.</span><span class="sxs-lookup"><span data-stu-id="9f781-155">Now that Vamp is up and running, deploy a service from a blueprint.</span></span> 

<span data-ttu-id="9f781-156">Dans sa forme la plus simple, un [schéma Vamp](http://vamp.io/documentation/using-vamp/blueprints/) décrit les points de terminaison (passerelles), clusters et services à déployer.</span><span class="sxs-lookup"><span data-stu-id="9f781-156">In its simplest form, a [Vamp blueprint](http://vamp.io/documentation/using-vamp/blueprints/) describes the endpoints (gateways), clusters, and services to deploy.</span></span> <span data-ttu-id="9f781-157">Vamp utilise des clusters pour regrouper des variantes du même service en groupes logiques à des fins de contrôle de validité de mise en production ou de tests A/B.</span><span class="sxs-lookup"><span data-stu-id="9f781-157">Vamp uses clusters to group different variants of the same service into logical groups for canary releasing or A/B testing.</span></span>  

<span data-ttu-id="9f781-158">Ce scénario utilise un exemple d’application monolithique appelé [ **sava**](https://github.com/magneticio/sava), qui en est à la version 1.0.</span><span class="sxs-lookup"><span data-stu-id="9f781-158">This scenario uses a sample monolithic application called [**sava**](https://github.com/magneticio/sava), which is at version 1.0.</span></span> <span data-ttu-id="9f781-159">Le monolithe est empaqueté dans un conteneur Docker qui se trouve dans un hub Docker sous magneticio/sava:1.0.0.</span><span class="sxs-lookup"><span data-stu-id="9f781-159">The monolith is packaged in a Docker container, which is in Docker Hub under magneticio/sava:1.0.0.</span></span> <span data-ttu-id="9f781-160">L’application s’exécute normalement sur le port 8080, mais vous souhaitez l’exposer sous le port 9050 dans ce cas.</span><span class="sxs-lookup"><span data-stu-id="9f781-160">The app normally runs on port 8080, but you want to expose it under port 9050 in this case.</span></span> <span data-ttu-id="9f781-161">Déployez l’application via Vamp à l’aide d’un schéma simple.</span><span class="sxs-lookup"><span data-stu-id="9f781-161">Deploy the app through Vamp using a simple blueprint.</span></span>

1. <span data-ttu-id="9f781-162">Accédez à **Deployments**.</span><span class="sxs-lookup"><span data-stu-id="9f781-162">Go to **Deployments**.</span></span>

2. <span data-ttu-id="9f781-163">Cliquez sur **Add**.</span><span class="sxs-lookup"><span data-stu-id="9f781-163">Click **Add**.</span></span>

3. <span data-ttu-id="9f781-164">Collez dans le fichier YAML de schéma suivant.</span><span class="sxs-lookup"><span data-stu-id="9f781-164">Paste in the following blueprint YAML.</span></span> <span data-ttu-id="9f781-165">Ce schéma contient un seul cluster avec une seule variante de service, que nous allons changer ultérieurement :</span><span class="sxs-lookup"><span data-stu-id="9f781-165">This blueprint contains one cluster with only one service variant, which we change in a later step:</span></span>

  ```YAML
  name: sava                        # deployment name
  gateways:
    9050: sava_cluster/webport      # stable endpoint
  clusters:
    sava_cluster:               # cluster to create
     services:
        -
          breed:
            name: sava:1.0.0        # service variant name
            deployable: magneticio/sava:1.0.0
            ports:
              webport: 8080/http # cluster endpoint, used for canary releasing
  ```

4. <span data-ttu-id="9f781-166">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="9f781-166">Click **Save**.</span></span> <span data-ttu-id="9f781-167">Vamp entame le déploiement.</span><span class="sxs-lookup"><span data-stu-id="9f781-167">Vamp initiates the deployment.</span></span>

<span data-ttu-id="9f781-168">Le déploiement est décrit dans la page **Déploiements**.</span><span class="sxs-lookup"><span data-stu-id="9f781-168">The deployment is listed on the **Deployments** page.</span></span> <span data-ttu-id="9f781-169">Pour contrôler son état, cliquez dessus.</span><span class="sxs-lookup"><span data-stu-id="9f781-169">Click the deployment to monitor its status.</span></span>

![Interface utilisateur de Vamp - Déploiement de sava](./media/container-service-dcos-vamp-canary-release/09_sava100.png)

![service Sava dans l’interface utilisateur de Vamp](./media/container-service-dcos-vamp-canary-release/09a_sava100.png)

<span data-ttu-id="9f781-172">Deux passerelles sont créées, qui sont répertoriées dans la page **Passerelles** :</span><span class="sxs-lookup"><span data-stu-id="9f781-172">Two gateways are created, which are listed on the **Gateways** page:</span></span>

* <span data-ttu-id="9f781-173">un point de terminaison stable pour accéder au service en cours d’exécution (port 9050) ;</span><span class="sxs-lookup"><span data-stu-id="9f781-173">a stable endpoint to access the running service (port 9050)</span></span> 
* <span data-ttu-id="9f781-174">une passerelle interne gérée par Vamp (que nous décrirons plus en détail ultérieurement).</span><span class="sxs-lookup"><span data-stu-id="9f781-174">a Vamp-managed internal gateway (more on this gateway later).</span></span> 

![Interface utilisateur de Vamp - Passerelles sava](./media/container-service-dcos-vamp-canary-release/10_vamp_sava_gateways.png)

<span data-ttu-id="9f781-176">Le service sava est à présent déployé, mais vous ne pouvez pas y accéder de l’extérieur, car Azure Load Balancer ignore encore comment transférer le trafic vers celui-ci.</span><span class="sxs-lookup"><span data-stu-id="9f781-176">The sava service has now deployed, but you can’t access it externally because the Azure Load Balancer doesn’t know to forward traffic to it yet.</span></span> <span data-ttu-id="9f781-177">Pour accéder au service, mettez à jour la configuration réseau Azure.</span><span class="sxs-lookup"><span data-stu-id="9f781-177">To access the service, update the Azure networking configuration.</span></span>


## <a name="update-the-azure-network-configuration"></a><span data-ttu-id="9f781-178">Mettre à jour la configuration réseau Azure</span><span class="sxs-lookup"><span data-stu-id="9f781-178">Update the Azure network configuration</span></span>

<span data-ttu-id="9f781-179">Vamp a déployé le service sava sur les nœud agents du contrôleur de domaine/système d’exploitation, en exposant un point de terminaison stable au port 9050.</span><span class="sxs-lookup"><span data-stu-id="9f781-179">Vamp deployed the sava service on the DC/OS agent nodes, exposing a stable endpoint at port 9050.</span></span> <span data-ttu-id="9f781-180">Pour accéder au service à partir de l’extérieur du cluster de contrôleur de domaine/système d’exploitation, apportez les modifications suivantes à la configuration réseau Azure dans le déploiement de votre cluster :</span><span class="sxs-lookup"><span data-stu-id="9f781-180">To access the service from outside the DC/OS cluster, make the following changes to the Azure network configuration in your cluster deployment:</span></span> 

1. <span data-ttu-id="9f781-181">**Configurez l’équilibrage de charge Azure** pour les agents (la ressource nommée **dcos-agent-lb-xxxx**) avec une sonde d’intégrité et une règle pour transférer le trafic sur le port 9050 vers les instances sava.</span><span class="sxs-lookup"><span data-stu-id="9f781-181">**Configure the Azure Load Balancer** for the agents (the resource named **dcos-agent-lb-xxxx**) with a health probe and a rule to forward traffic on port 9050 to the sava instances.</span></span> 

2. <span data-ttu-id="9f781-182">**Mettez à jour le groupe de sécurité réseau** pour les agents publics (la ressource nommée **XXXX-agent-public-nsg-XXXX**) pour autoriser le trafic sur le port 9050.</span><span class="sxs-lookup"><span data-stu-id="9f781-182">**Update the network security group** for the public agents (the resource named **XXXX-agent-public-nsg-XXXX**) to allow traffic on port 9050.</span></span>

<span data-ttu-id="9f781-183">Pour obtenir des instructions détaillées sur l’exécution de ces tâches à l’aide du portail Azure, voir [Autoriser l’accès public à une application Azure Container Service](container-service-enable-public-access.md).</span><span class="sxs-lookup"><span data-stu-id="9f781-183">For detailed steps to complete these tasks using the Azure portal, see [Enable public access to an Azure Container Service application](container-service-enable-public-access.md).</span></span> <span data-ttu-id="9f781-184">Spécifiez le port 9050 pour tous les paramètres de port.</span><span class="sxs-lookup"><span data-stu-id="9f781-184">Specify port 9050 for all port settings.</span></span>


<span data-ttu-id="9f781-185">Une fois que tout a été créé, accédez au panneau **Vue d’ensemble** de l’équilibrage de charge de l’agent du contrôleur de domaine/système d’exploitation (la ressource nommée **dcos-agent-lb-xxxx**).</span><span class="sxs-lookup"><span data-stu-id="9f781-185">Once everything has been created, go to the **Overview** blade of the DC/OS agent load balancer (the resource named **dcos-agent-lb-xxxx**).</span></span> <span data-ttu-id="9f781-186">Recherchez l’**adresse IP publique** et utilisez-la pour accéder à sava sur le port 9050.</span><span class="sxs-lookup"><span data-stu-id="9f781-186">Find the **Public IP address**, and use the address to access sava at port 9050.</span></span>

![Portail Azure - Obtenir un adresse IP publique](./media/container-service-dcos-vamp-canary-release/18_public_ip_address.png)

![sava](./media/container-service-dcos-vamp-canary-release/19_sava100.png)


## <a name="run-a-canary-release"></a><span data-ttu-id="9f781-189">Exécuter un contrôle de validité de mise en production</span><span class="sxs-lookup"><span data-stu-id="9f781-189">Run a canary release</span></span>

<span data-ttu-id="9f781-190">Supposons que vous disposez d’une nouvelle version de cette application donc vous voulez contrôler la validité de la mise en production.</span><span class="sxs-lookup"><span data-stu-id="9f781-190">Suppose you have a new version of this application that you want to canary release into production.</span></span> <span data-ttu-id="9f781-191">Vous l’avez mise en conteneur en tant que magneticio/sava:1.1.0 et êtes prêt à l’employer.</span><span class="sxs-lookup"><span data-stu-id="9f781-191">You have it containerized as magneticio/sava:1.1.0 and are ready to go.</span></span> <span data-ttu-id="9f781-192">Vamp vous permet d’ajouter facilement des services au déploiement en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="9f781-192">Vamp lets you easily add new services to the running deployment.</span></span> <span data-ttu-id="9f781-193">Ces services « fusionnés » sont déployés en même temps que les services existants dans le cluster, et une pondération de 0 % leur est affectée.</span><span class="sxs-lookup"><span data-stu-id="9f781-193">These "merged" services are deployed alongside the existing services in the cluster, and assigned a weight of 0%.</span></span> <span data-ttu-id="9f781-194">Aucun trafic n’est routé vers un service nouvellement fusionné tant que vous n’avez pas ajusté la distribution du trafic.</span><span class="sxs-lookup"><span data-stu-id="9f781-194">No traffic is routed to a newly merged service until you adjust the traffic distribution.</span></span> <span data-ttu-id="9f781-195">Le curseur de poids dans l’interface utilisateur de Vamp vous permet de contrôler totalement la distribution, en effectuant des ajustements incrémentiels (contrôle de validité de mise en production) ou une restauration instantanée.</span><span class="sxs-lookup"><span data-stu-id="9f781-195">The weight slider in the Vamp UI gives you complete control over the distribution, allowing for incremental adjustments (canary release) or an instant rollback.</span></span>

### <a name="merge-a-new-service-variant"></a><span data-ttu-id="9f781-196">Fusionner une nouvelle variante de service</span><span class="sxs-lookup"><span data-stu-id="9f781-196">Merge a new service variant</span></span>

<span data-ttu-id="9f781-197">Pour fusionner le nouveau service sava 1.1 avec le déploiement en cours d’exécution :</span><span class="sxs-lookup"><span data-stu-id="9f781-197">To merge the new sava 1.1 service with the running deployment:</span></span>

1. <span data-ttu-id="9f781-198">Dans l’interface utilisateur de Vamp, cliquez sur **Schémas**.</span><span class="sxs-lookup"><span data-stu-id="9f781-198">In the Vamp UI, click **Blueprints**.</span></span>

2. <span data-ttu-id="9f781-199">Cliquez sur **Ajouter**, puis collez dans le fichier YAML de schéma suivant : ce schéma décrit une nouvelle variante de service (sava:1.1.0) à déployer dans le cluster existant (sava_cluster).</span><span class="sxs-lookup"><span data-stu-id="9f781-199">Click **Add** and paste in the following blueprint YAML: This blueprint describes a new service variant (sava:1.1.0) to deploy within the existing cluster (sava_cluster).</span></span>

  ```YAML
  name: sava:1.1.0      # blueprint name
  clusters:
    sava_cluster:       # cluster to update
      services:
        -
          breed:
            name: sava:1.1.0    # service variant name
            deployable: magneticio/sava:1.1.0    
            ports:
              webport: 8080/http # cluster endpoint to update
  ```
  
3. <span data-ttu-id="9f781-200">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="9f781-200">Click **Save**.</span></span> <span data-ttu-id="9f781-201">Le schéma est stocké et répertorié dans la page **Schémas**.</span><span class="sxs-lookup"><span data-stu-id="9f781-201">The blueprint is stored and listed on the **Blueprints** page.</span></span>

4. <span data-ttu-id="9f781-202">Ouvrez le menu action sur le schéma sava:1.1 et cliquez sur **Fusionner vers**.</span><span class="sxs-lookup"><span data-stu-id="9f781-202">Open the action menu on the sava:1.1 blueprint and click **Merge to**.</span></span>

  ![Interface utilisateur de Vamp - Schémas](./media/container-service-dcos-vamp-canary-release/20_sava110_mergeto.png)

5. <span data-ttu-id="9f781-204">Sélectionnez le déploiement **sava**, puis cliquez sur **Fusionner**.</span><span class="sxs-lookup"><span data-stu-id="9f781-204">Select the **sava** deployment and click **Merge**.</span></span>

  ![Interface utilisateur de Vamp - Fusionner le schéma dans le déploiement](./media/container-service-dcos-vamp-canary-release/21_sava110_merge.png)

<span data-ttu-id="9f781-206">Vamp déploie la nouvelle variante de service sava:1.1.0 décrite dans le schéma en même temps que sava:1.0.0 dans le **sava_cluster** du déploiement en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="9f781-206">Vamp deploys the new sava:1.1.0 service variant described in the blueprint alongside sava:1.0.0 in the **sava_cluster** of the running deployment.</span></span> 

![Interface utilisateur de Vamp - Déploiement de sava mis à jour](./media/container-service-dcos-vamp-canary-release/22_sava_cluster.png)

<span data-ttu-id="9f781-208">La passerelle **sava/sava_cluster/webport** (point de terminaison du cluster) est également mise à jour par l’ajout d’un itinéraire au sava:1.1.0 nouvellement déployé.</span><span class="sxs-lookup"><span data-stu-id="9f781-208">The **sava/sava_cluster/webport** gateway (the cluster endpoint) is also updated, adding a route to the newly deployed sava:1.1.0.</span></span> <span data-ttu-id="9f781-209">À ce stade, aucun trafic n’est routé ici (le **POIDS** est défini sur 0 %).</span><span class="sxs-lookup"><span data-stu-id="9f781-209">At this point, no traffic is routed here (the **WEIGHT** is set to 0%).</span></span>

![Interface utilisateur de Vamp - Passerelle de cluster](./media/container-service-dcos-vamp-canary-release/23_sava_cluster_webport.png)

### <a name="canary-release"></a><span data-ttu-id="9f781-211">Contrôle la validité de la mise en production</span><span class="sxs-lookup"><span data-stu-id="9f781-211">Canary release</span></span>

<span data-ttu-id="9f781-212">Les deux versions de sava étant déployées dans le même cluster, ajustez la distribution du trafic entre elles en déplaçant le curseur **POIDS**.</span><span class="sxs-lookup"><span data-stu-id="9f781-212">With both versions of sava deployed in the same cluster, adjust the distribution of traffic between them by moving the **WEIGHT** slider.</span></span>

1. <span data-ttu-id="9f781-213">Cliquez sur ![Interface utilisateur de Vamp - Modifier](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) en regard de **POIDS**.</span><span class="sxs-lookup"><span data-stu-id="9f781-213">Click ![Vamp UI - edit](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) next to **WEIGHT**.</span></span>

2. <span data-ttu-id="9f781-214">Définissez la répartition du poids sur 50 %/50 %, puis cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="9f781-214">Set the weight distribution to 50%/50% and click **Save**.</span></span>

  ![Interface utilisateur de Vamp - Curseur de poids de passerelle](./media/container-service-dcos-vamp-canary-release/24_sava_cluster_webport_weight.png)

3. <span data-ttu-id="9f781-216">Revenez à votre navigateur et actualisez la page de sava quelques fois supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="9f781-216">Go back to your browser and refresh the sava page a few more times.</span></span> <span data-ttu-id="9f781-217">L’application sava bascule entre une page sava:1.0 et une page sava:1.1.</span><span class="sxs-lookup"><span data-stu-id="9f781-217">The sava application now switches between a sava:1.0 page and a sava:1.1 page.</span></span>

  ![alternance des services sava1.0 et sava1.1](./media/container-service-dcos-vamp-canary-release/25_sava_100_101.png)


  > [!NOTE]
  > <span data-ttu-id="9f781-219">Cette alternance de la page fonctionne de façon optimale avec les modes « Incognito » ou « Anonyme » de votre navigateur en raison de la mise en cache des ressources statiques.</span><span class="sxs-lookup"><span data-stu-id="9f781-219">This alternation of the page works best with the "Incognito" or “Anonymous” mode of your browser because of the caching of static assets.</span></span>
  >

### <a name="filter-traffic"></a><span data-ttu-id="9f781-220">Filtrer le trafic</span><span class="sxs-lookup"><span data-stu-id="9f781-220">Filter traffic</span></span>

<span data-ttu-id="9f781-221">Supposons qu’après déploiement vous ayez découvert une incompatibilité dans sava:1.1.0 qui entraîne des problèmes d’affichage dans les navigateurs Firefox.</span><span class="sxs-lookup"><span data-stu-id="9f781-221">Suppose after deployment that you discovered an incompatibility in sava:1.1.0 that causes display problems in Firefox browsers.</span></span> <span data-ttu-id="9f781-222">Vous pouvez configurer Vamp pour filtrer le trafic entrant et rediriger tous les utilisateurs de Firefox vers le sava:1.0.0 stable connu.</span><span class="sxs-lookup"><span data-stu-id="9f781-222">You can set Vamp to filter incoming traffic and direct all Firefox users back to the known stable sava:1.0.0.</span></span> <span data-ttu-id="9f781-223">Ce filtre résout instantanément l’interruption pour les utilisateurs de Firefox, tandis toutes les autres personnes continuent de profiter des avantages du sava:1.1.0 amélioré.</span><span class="sxs-lookup"><span data-stu-id="9f781-223">This filter instantly resolves the disruption for Firefox users, while everybody else continues to enjoy the benefits of the improved sava:1.1.0.</span></span>

<span data-ttu-id="9f781-224">Vamp utilise des **conditions** pour filtrer le trafic entre itinéraires au sein d’une passerelle.</span><span class="sxs-lookup"><span data-stu-id="9f781-224">Vamp uses **conditions** to filter traffic between routes in a gateway.</span></span> <span data-ttu-id="9f781-225">Le trafic est filtré, puis dirigé selon les conditions appliquées à chaque itinéraire.</span><span class="sxs-lookup"><span data-stu-id="9f781-225">Traffic is first filtered and directed according to the conditions applied to each route.</span></span> <span data-ttu-id="9f781-226">Tout le trafic restant est distribué en fonction du paramètre de poids de passerelle.</span><span class="sxs-lookup"><span data-stu-id="9f781-226">All remaining traffic is distributed according to the gateway weight setting.</span></span>

<span data-ttu-id="9f781-227">Vous pouvez créer une condition pour filtrer tous les utilisateurs de Firefox et les diriger vers l’ancien sava:1.0.0 :</span><span class="sxs-lookup"><span data-stu-id="9f781-227">You can create a condition to filter all Firefox users and direct them to the old sava:1.0.0:</span></span>

1. <span data-ttu-id="9f781-228">Dans la page sava/sava_cluster/webport **Passerelles**, cliquez sur ![Interface utilisateur de Vamp - Modifier](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) pour ajouter une **CONDITION** à l’itinéraire sava/sava_cluster/sava:1.0.0/webport.</span><span class="sxs-lookup"><span data-stu-id="9f781-228">On the sava/sava_cluster/webport **Gateways** page, click ![Vamp UI - edit](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) to add a **CONDITION** to the route sava/sava_cluster/sava:1.0.0/webport.</span></span> 

2. <span data-ttu-id="9f781-229">Entrez la condition **agent utilisateur == Firefox**, puis cliquez sur ![Interface utilisateur de Vamp - Enregistrer](./media/container-service-dcos-vamp-canary-release/vamp_ui_save.png).</span><span class="sxs-lookup"><span data-stu-id="9f781-229">Enter the condition **user-agent == Firefox** and click ![Vamp UI - save](./media/container-service-dcos-vamp-canary-release/vamp_ui_save.png).</span></span>

  <span data-ttu-id="9f781-230">Vamp ajoute la condition avec une force par défaut de 0 %.</span><span class="sxs-lookup"><span data-stu-id="9f781-230">Vamp adds the condition with a default strength of 0%.</span></span> <span data-ttu-id="9f781-231">Pour commencer à filtrer le trafic, vous devez ajuster la force de la condition.</span><span class="sxs-lookup"><span data-stu-id="9f781-231">To start filtering traffic, you need to adjust the condition strength.</span></span>

3. <span data-ttu-id="9f781-232">Cliquez sur ![Interface utilisateur de Vamp - Modifier](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) pour modifier la **FORCE** appliquée à la condition.</span><span class="sxs-lookup"><span data-stu-id="9f781-232">Click ![Vamp UI - edit](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) to change the **STRENGTH** applied to the condition.</span></span>
 
4. <span data-ttu-id="9f781-233">Définissez la **FORCE** sur 100 % et cliquez sur ![Interface utilisateur de Vamp - Enregistrer](./media/container-service-dcos-vamp-canary-release/vamp_ui_save.png) pour enregistrer.</span><span class="sxs-lookup"><span data-stu-id="9f781-233">Set the **STRENGTH** to 100% and click ![Vamp UI - save](./media/container-service-dcos-vamp-canary-release/vamp_ui_save.png) to save.</span></span>

  <span data-ttu-id="9f781-234">Vamp envoie désormais tout le trafic correspondant à la condition (tous les utilisateurs de Firefox) vers sava:1.0.0.</span><span class="sxs-lookup"><span data-stu-id="9f781-234">Vamp now sends all traffic matching the condition (all Firefox users) to sava:1.0.0.</span></span>

  ![Interface utilisateur de Vamp - Appliquer une condition à la passerelle](./media/container-service-dcos-vamp-canary-release/26_apply_condition.png)

5. <span data-ttu-id="9f781-236">Enfin, définissez le poids de passerelle pour l’envoi de tout le trafic restant (tous les utilisateurs autres que Firefox) pour le nouveau sava:1.1.0.</span><span class="sxs-lookup"><span data-stu-id="9f781-236">Finally, adjust the gateway weight to send all remaining traffic (all non-Firefox users) to the new sava:1.1.0.</span></span> <span data-ttu-id="9f781-237">Cliquez sur ![Interface utilisateur de Vamp - Modifier](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) en regard de **POIDS** et définir la distribution de poids de façon à ce que 100 % soient dirigés vers l’itinéraire sava/sava_cluster/sava:1.1.0/webport.</span><span class="sxs-lookup"><span data-stu-id="9f781-237">Click ![Vamp UI - edit](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) next to **WEIGHT** and set the weight distribution so 100% is directed to the route sava/sava_cluster/sava:1.1.0/webport.</span></span>

  <span data-ttu-id="9f781-238">Tout le trafic non filtré par la condition est maintenant dirigé vers le nouveau sava:1.1.0.</span><span class="sxs-lookup"><span data-stu-id="9f781-238">All traffic not filtered by the condition is now directed to the new sava:1.1.0.</span></span>

6. <span data-ttu-id="9f781-239">Pour afficher le filtre d’action, ouvrez deux navigateurs différents (un Firefox et un autre ), puis accédez au service sava à partir des deux.</span><span class="sxs-lookup"><span data-stu-id="9f781-239">To see the filter in action, open two different browsers (one Firefox and one other browser) and access the sava service from both.</span></span> <span data-ttu-id="9f781-240">Toutes les demandes de Firefox sont envoyées à sava:1.0.0, tandis que tous les autres navigateurs sont dirigés vers sava:1.1.0.</span><span class="sxs-lookup"><span data-stu-id="9f781-240">All Firefox requests are sent to sava:1.0.0, while all other browsers are directed to sava:1.1.0.</span></span>

  ![Interface utilisateur de Vamp - Filtrer le trafic](./media/container-service-dcos-vamp-canary-release/27_filter_traffic.png)

## <a name="summing-up"></a><span data-ttu-id="9f781-242">Résumé</span><span class="sxs-lookup"><span data-stu-id="9f781-242">Summing up</span></span>

<span data-ttu-id="9f781-243">Cet article est une présentation rapide de Vamp sur un cluster de contrôleur de domaine/système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="9f781-243">This article was a quick introduction to Vamp on a DC/OS cluster.</span></span> <span data-ttu-id="9f781-244">Les débutants ont obtenu Vamp opérationnel sur leur cluster de contrôleur de domaine/système d’exploitation Azure Container Service, déployé un service avec un schéma Vamp, et accédé à celui-ci via le point de terminaison exposé (passerelle).</span><span class="sxs-lookup"><span data-stu-id="9f781-244">For starters, you got Vamp up and running on your Azure Container Service DC/OS cluster, deployed a service with a Vamp blueprint, and accessed it at the exposed endpoint (gateway).</span></span>

<span data-ttu-id="9f781-245">Nous avons également évoqué certaines puissantes fonctionnalités de Vamp telles que la fusion d’une nouvelle variante de service dans le déploiement en cours d’exécution et son introduction incrémentielle, puis le filtrage du trafic pour résoudre une incompatibilité connue.</span><span class="sxs-lookup"><span data-stu-id="9f781-245">We also touched on some powerful features of Vamp:  merging a new service variant to the running deployment and introducing it incrementally, then filtering traffic to resolve a known incompatibility.</span></span>


## <a name="next-steps"></a><span data-ttu-id="9f781-246">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9f781-246">Next steps</span></span>

* <span data-ttu-id="9f781-247">Découvrez la gestion des actions de Vamp via l’[API REST Vamp](http://vamp.io/documentation/api/api-reference/).</span><span class="sxs-lookup"><span data-stu-id="9f781-247">Learn about managing Vamp actions through the [Vamp REST API](http://vamp.io/documentation/api/api-reference/).</span></span>

* <span data-ttu-id="9f781-248">Générez des scripts d’automatisation de Vamp dans Node.js et exécutez-les en tant que [flux de travail Vamp](http://vamp.io/documentation/tutorials/create-a-workflow/).</span><span class="sxs-lookup"><span data-stu-id="9f781-248">Build Vamp automation scripts in Node.js and run them as [Vamp workflows](http://vamp.io/documentation/tutorials/create-a-workflow/).</span></span>

* <span data-ttu-id="9f781-249">Consultez des [didacticiels Vamp](http://vamp.io/documentation/tutorials/overview/) supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="9f781-249">See additional [VAMP tutorials](http://vamp.io/documentation/tutorials/overview/).</span></span>

