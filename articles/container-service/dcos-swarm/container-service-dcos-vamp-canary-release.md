---
title: "version aaaCanary avec une EMPEIGNE sur le cluster de contrôleur de domaine/système d’exploitation Azure | Documents Microsoft"
description: Comment toouse Vamp des services de mise en production toocanary et appliquer le filtrage sur un cluster du Service de conteneur Azure DC/OS du trafic actif
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
ms.openlocfilehash: e7b8658a161a7cddcf718e3e1c12a889a330d3d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="canary-release-microservices-with-vamp-on-an-azure-container-service-dcos-cluster"></a><span data-ttu-id="ac509-103">Contrôler la validité de microservices de mise en production avec Vamp sur un cluster de contrôleur de domaine/système d’exploitation Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="ac509-103">Canary release microservices with Vamp on an Azure Container Service DC/OS cluster</span></span>

<span data-ttu-id="ac509-104">Dans cette procédure pas à pas, nous configurons Vamp sur Azure Container Service avec un cluster de contrôleur de domaine/système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="ac509-104">In this walkthrough, we set up Vamp on Azure Container Service with a DC/OS cluster.</span></span> <span data-ttu-id="ac509-105">Nous canary version du service de démo hello une EMPEIGNE « sava », puis résolvez un problème d’incompatibilité du service hello avec Firefox en appliquant un filtrage du trafic actif.</span><span class="sxs-lookup"><span data-stu-id="ac509-105">We canary release hello Vamp demo service "sava", and then resolve an incompatibility of hello service with Firefox by applying smart traffic filtering.</span></span> 

> [!TIP] 
> <span data-ttu-id="ac509-106">Dans cette procédure pas à pas une EMPEIGNE s’exécute sur un cluster de contrôleur de domaine/système d’exploitation, mais vous pouvez également utiliser une EMPEIGNE avec Kubernetes en tant qu’orchestrateur de hello.</span><span class="sxs-lookup"><span data-stu-id="ac509-106">In this walkthrough Vamp runs on a DC/OS cluster, but you can also use Vamp with Kubernetes as hello orchestrator.</span></span>
>

## <a name="about-canary-releases-and-vamp"></a><span data-ttu-id="ac509-107">À propos du contrôle de la validité des mises en production et de Vamp</span><span class="sxs-lookup"><span data-stu-id="ac509-107">About canary releases and Vamp</span></span>


<span data-ttu-id="ac509-108">Le [contrôle de la validité des mises en production](https://martinfowler.com/bliki/CanaryRelease.html) est une stratégie de déploiement intelligent adoptée par des entreprises innovantes telles que Netflix, Facebook et Spotify.</span><span class="sxs-lookup"><span data-stu-id="ac509-108">[Canary releasing](https://martinfowler.com/bliki/CanaryRelease.html) is a smart deployment strategy adopted by innovative organizations like Netflix, Facebook, and Spotify.</span></span> <span data-ttu-id="ac509-109">Cette approche est intéressante, car elle réduit les problèmes, introduit des filets de sécurité et stimule l’innovation.</span><span class="sxs-lookup"><span data-stu-id="ac509-109">It’s an approach that makes sense, because it reduces issues, introduces safety-nets, and increases innovation.</span></span> <span data-ttu-id="ac509-110">Alors pourquoi toutes les entreprises ne l’adoptent-elles pas ?</span><span class="sxs-lookup"><span data-stu-id="ac509-110">So why aren’t all companies using it?</span></span> <span data-ttu-id="ac509-111">Étendre un tooinclude de pipeline de l’élément de configuration/CD stratégies canary ajoute une complexité et requiert l’expérience et devops complète de base de connaissances.</span><span class="sxs-lookup"><span data-stu-id="ac509-111">Extending a CI/CD pipeline tooinclude canary strategies adds complexity, and requires extensive devops knowledge and experience.</span></span> <span data-ttu-id="ac509-112">C’est assez tooblock plus petites entreprises et les entreprises avant qu’ils même prise en main.</span><span class="sxs-lookup"><span data-stu-id="ac509-112">That’s enough tooblock smaller companies and enterprises alike before they even get started.</span></span> 

<span data-ttu-id="ac509-113">[Vamp](http://vamp.io/) est un tooease système open source conçu cette transition et mettre canary libération fonctionnalités tooyour préféré conteneur du planificateur.</span><span class="sxs-lookup"><span data-stu-id="ac509-113">[Vamp](http://vamp.io/) is an open-source system designed tooease this transition and bring canary releasing features tooyour preferred container scheduler.</span></span> <span data-ttu-id="ac509-114">La fonctionnalité de contrôle de validité de Vamp va au-delà des déploiements basés sur un pourcentage.</span><span class="sxs-lookup"><span data-stu-id="ac509-114">Vamp’s canary functionality goes beyond percentage-based rollouts.</span></span> <span data-ttu-id="ac509-115">Le trafic peut filtré et divisent sur un large éventail de conditions, par exemple des tootarget des utilisateurs spécifiques, des plages d’IP ou appareils.</span><span class="sxs-lookup"><span data-stu-id="ac509-115">Traffic can be filtered and split on a wide range of conditions, for example tootarget specific users, IP-ranges, or devices.</span></span> <span data-ttu-id="ac509-116">Vamp suit et analyse les métriques de performances, permettant ainsi une automatisation basée sur des données réelles.</span><span class="sxs-lookup"><span data-stu-id="ac509-116">Vamp tracks and analyzes performance metrics, allowing for automation based on real-world data.</span></span> <span data-ttu-id="ac509-117">Vous pouvez configurer une restauration automatique en cas d’erreurs ou mettre à l’échelle des variantes de service en fonction de la charge ou de la latence.</span><span class="sxs-lookup"><span data-stu-id="ac509-117">You can set up automatic rollback on errors, or scale individual service variants based on load or latency.</span></span>

## <a name="set-up-azure-container-service-with-dcos"></a><span data-ttu-id="ac509-118">Configurer Azure Container Service avec un contrôleur de domaine/système d’exploitation</span><span class="sxs-lookup"><span data-stu-id="ac509-118">Set up Azure Container Service with DC/OS</span></span>



1. <span data-ttu-id="ac509-119">[Déployez un cluster de contrôleur de domaine/système d’exploitation](container-service-deployment.md) avec un maître et deux agents de la taille par défaut.</span><span class="sxs-lookup"><span data-stu-id="ac509-119">[Deploy a DC/OS cluster](container-service-deployment.md) with one master and two agents of default size.</span></span> 

2. <span data-ttu-id="ac509-120">[Créer un tunnel SSH](../container-service-connect.md) cluster de contrôleur de domaine/système d’exploitation tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="ac509-120">[Create an SSH tunnel](../container-service-connect.md) tooconnect toohello DC/OS cluster.</span></span> <span data-ttu-id="ac509-121">Cet article suppose que vous tunnel cluster toohello sur le port local 80.</span><span class="sxs-lookup"><span data-stu-id="ac509-121">This article assumes that you tunnel toohello cluster on local port 80.</span></span>


## <a name="set-up-vamp"></a><span data-ttu-id="ac509-122">Configurer Vamp</span><span class="sxs-lookup"><span data-stu-id="ac509-122">Set up Vamp</span></span>

<span data-ttu-id="ac509-123">Maintenant que vous disposez d’un cluster de contrôleur de domaine/système d’exploitation en cours d’exécution, vous pouvez installer une EMPEIGNE depuis hello l’interface utilisateur du contrôleur de domaine/système d’exploitation (http://localhost : 80).</span><span class="sxs-lookup"><span data-stu-id="ac509-123">Now that you have a running DC/OS cluster, you can install Vamp from hello DC/OS UI (http://localhost:80).</span></span> 

![IU DC/OS](./media/container-service-dcos-vamp-canary-release/01_set_up_vamp.png)

<span data-ttu-id="ac509-125">L’installation s’effectue en deux étapes :</span><span class="sxs-lookup"><span data-stu-id="ac509-125">Installation is done in two stages:</span></span>

1. <span data-ttu-id="ac509-126">**Déploiement d’Elasticsearch**,</span><span class="sxs-lookup"><span data-stu-id="ac509-126">**Deploy Elasticsearch**.</span></span>

2. <span data-ttu-id="ac509-127">Puis **déployer une EMPEIGNE** en installant le package d’univers hello Vamp contrôleur de domaine/système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="ac509-127">Then **deploy Vamp** by installing hello Vamp DC/OS universe package.</span></span>

### <a name="deploy-elasticsearch"></a><span data-ttu-id="ac509-128">Déployer Elasticsearch</span><span class="sxs-lookup"><span data-stu-id="ac509-128">Deploy Elasticsearch</span></span>

<span data-ttu-id="ac509-129">Vamp a besoin d’Elasticsearch pour la collecte et l’agrégation des métriques.</span><span class="sxs-lookup"><span data-stu-id="ac509-129">Vamp requires Elasticsearch for metrics collection and aggregation.</span></span> <span data-ttu-id="ac509-130">Vous pouvez utiliser hello [magneticio Docker images](https://hub.docker.com/r/magneticio/elastic/) toodeploy une pile de Elasticsearch de Vamp compatible.</span><span class="sxs-lookup"><span data-stu-id="ac509-130">You can use hello [magneticio Docker images](https://hub.docker.com/r/magneticio/elastic/) toodeploy a compatible Vamp Elasticsearch stack.</span></span>

1. <span data-ttu-id="ac509-131">Dans l’interface utilisateur du contrôleur de domaine/système d’exploitation de hello, accédez trop**Services** et cliquez sur **déployer le Service**.</span><span class="sxs-lookup"><span data-stu-id="ac509-131">In hello DC/OS UI, go too**Services** and click **Deploy Service**.</span></span>

2. <span data-ttu-id="ac509-132">Sélectionnez **mode JSON** de hello **déployer un nouveau Service** contextuelle.</span><span class="sxs-lookup"><span data-stu-id="ac509-132">Select **JSON mode** from hello **Deploy New Service** pop-up.</span></span>

  ![Sélectionnez le mode JSON](./media/container-service-dcos-vamp-canary-release/02_deploy_service_json_mode.png)

3. <span data-ttu-id="ac509-134">Collez hello suivant JSON.</span><span class="sxs-lookup"><span data-stu-id="ac509-134">Paste in hello following JSON.</span></span> <span data-ttu-id="ac509-135">Cette configuration s’exécute conteneur de hello avec 1 Go de RAM et une vérification d’intégrité de base sur le port Elasticsearch hello.</span><span class="sxs-lookup"><span data-stu-id="ac509-135">This configuration runs hello container with 1 GB of RAM and a basic health check on hello Elasticsearch port.</span></span>
  
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
  

3. <span data-ttu-id="ac509-136">Cliquez sur **Déployer**.</span><span class="sxs-lookup"><span data-stu-id="ac509-136">Click **Deploy**.</span></span>

  <span data-ttu-id="ac509-137">Contrôleur de domaine/système d’exploitation déploie le conteneur de Elasticsearch hello.</span><span class="sxs-lookup"><span data-stu-id="ac509-137">DC/OS deploys hello Elasticsearch container.</span></span> <span data-ttu-id="ac509-138">Vous pouvez suivre la progression sur hello **Services** page.</span><span class="sxs-lookup"><span data-stu-id="ac509-138">You can track progress on hello **Services** page.</span></span>  

  ![déployer Elasticsearch](./media/container-service-dcos-vamp-canary-release/03_deply_elasticsearch.png)

### <a name="deploy-vamp"></a><span data-ttu-id="ac509-140">Déployer Vamp</span><span class="sxs-lookup"><span data-stu-id="ac509-140">Deploy Vamp</span></span>

<span data-ttu-id="ac509-141">Une fois que Elasticsearch signale comme **en cours d’exécution**, vous pouvez ajouter le package d’univers de contrôleur de domaine/système d’exploitation Vamp hello.</span><span class="sxs-lookup"><span data-stu-id="ac509-141">Once Elasticsearch reports as **Running**, you can add hello Vamp DC/OS Universe package.</span></span> 

1. <span data-ttu-id="ac509-142">Accédez trop**univers** et recherchez **vamp**.</span><span class="sxs-lookup"><span data-stu-id="ac509-142">Go too**Universe** and search for **vamp**.</span></span> 
  <span data-ttu-id="ac509-143">![Vamp sur un univers de contrôleur de domaine/système d’exploitation](./media/container-service-dcos-vamp-canary-release/04_universe_deploy_vamp.png)</span><span class="sxs-lookup"><span data-stu-id="ac509-143">![Vamp on DC/OS universe](./media/container-service-dcos-vamp-canary-release/04_universe_deploy_vamp.png)</span></span>

2. <span data-ttu-id="ac509-144">Cliquez sur **installer** toohello suivant vamp package, puis choisissez **Installation avancé**.</span><span class="sxs-lookup"><span data-stu-id="ac509-144">Click **install** next toohello vamp package, and choose **Advanced Installation**.</span></span>

3. <span data-ttu-id="ac509-145">Faites défiler la liste et entrez hello suivant elasticsearch-url : `http://elasticsearch.marathon.mesos:9200`.</span><span class="sxs-lookup"><span data-stu-id="ac509-145">Scroll down and enter hello following elasticsearch-url: `http://elasticsearch.marathon.mesos:9200`.</span></span> 

  ![Entrer l’URL d’Elasticsearch](./media/container-service-dcos-vamp-canary-release/05_universe_elasticsearch_url.png)

4. <span data-ttu-id="ac509-147">Cliquez sur **Examinez et installez**, puis cliquez sur **installer** déploiement de hello toostart.</span><span class="sxs-lookup"><span data-stu-id="ac509-147">Click **Review and Install**, then click **Install** toostart hello deployment.</span></span>  

  <span data-ttu-id="ac509-148">Le contrôleur de domaine/système d’exploitation déploie tous les composants Vamp requis.</span><span class="sxs-lookup"><span data-stu-id="ac509-148">DC/OS deploys all required Vamp components.</span></span> <span data-ttu-id="ac509-149">Vous pouvez suivre la progression sur hello **Services** page.</span><span class="sxs-lookup"><span data-stu-id="ac509-149">You can track progress on hello **Services** page.</span></span>
  
  ![Déployer Vamp en tant que package d’univers](./media/container-service-dcos-vamp-canary-release/06_deploy_vamp.png)
  
5. <span data-ttu-id="ac509-151">Une fois le déploiement terminé, vous pouvez accéder hello Vamp de l’interface utilisateur :</span><span class="sxs-lookup"><span data-stu-id="ac509-151">Once deployment has completed, you can access hello Vamp UI:</span></span>

  ![Service Vamp sur contrôleur de domaine/système d’exploitation](./media/container-service-dcos-vamp-canary-release/07_deploy_vamp_complete.png)
  
  ![Interface utilisateur de Vamp](./media/container-service-dcos-vamp-canary-release/08_vamp_ui.png)


## <a name="deploy-your-first-service"></a><span data-ttu-id="ac509-154">Déployer votre premier service</span><span class="sxs-lookup"><span data-stu-id="ac509-154">Deploy your first service</span></span>

<span data-ttu-id="ac509-155">À présent que Vamp est opérationnel, déployez un service à partir d’un schéma.</span><span class="sxs-lookup"><span data-stu-id="ac509-155">Now that Vamp is up and running, deploy a service from a blueprint.</span></span> 

<span data-ttu-id="ac509-156">Dans sa forme la plus simple, un [une EMPEIGNE plan](http://vamp.io/documentation/using-vamp/blueprints/) décrit les points de terminaison hello (passerelles), des clusters et des services toodeploy.</span><span class="sxs-lookup"><span data-stu-id="ac509-156">In its simplest form, a [Vamp blueprint](http://vamp.io/documentation/using-vamp/blueprints/) describes hello endpoints (gateways), clusters, and services toodeploy.</span></span> <span data-ttu-id="ac509-157">Vamp utilise clusters toogroup différentes variantes de hello même service en groupes logiques pour libérer canary ou A / B de test.</span><span class="sxs-lookup"><span data-stu-id="ac509-157">Vamp uses clusters toogroup different variants of hello same service into logical groups for canary releasing or A/B testing.</span></span>  

<span data-ttu-id="ac509-158">Ce scénario utilise un exemple d’application monolithique appelé [ **sava**](https://github.com/magneticio/sava), qui en est à la version 1.0.</span><span class="sxs-lookup"><span data-stu-id="ac509-158">This scenario uses a sample monolithic application called [**sava**](https://github.com/magneticio/sava), which is at version 1.0.</span></span> <span data-ttu-id="ac509-159">monolithique de Hello est empaqueté dans un conteneur Docker, qui est dans le Hub d’ancrage sous magneticio/sava:1.0.0.</span><span class="sxs-lookup"><span data-stu-id="ac509-159">hello monolith is packaged in a Docker container, which is in Docker Hub under magneticio/sava:1.0.0.</span></span> <span data-ttu-id="ac509-160">application Hello s’exécute normalement sur le port 8080, mais vous souhaitez tooexpose sous port 9050 dans ce cas.</span><span class="sxs-lookup"><span data-stu-id="ac509-160">hello app normally runs on port 8080, but you want tooexpose it under port 9050 in this case.</span></span> <span data-ttu-id="ac509-161">Déploiement d’une application hello via une EMPEIGNE à l’aide d’un modèle simple.</span><span class="sxs-lookup"><span data-stu-id="ac509-161">Deploy hello app through Vamp using a simple blueprint.</span></span>

1. <span data-ttu-id="ac509-162">Accédez trop**déploiements**.</span><span class="sxs-lookup"><span data-stu-id="ac509-162">Go too**Deployments**.</span></span>

2. <span data-ttu-id="ac509-163">Cliquez sur **Add**.</span><span class="sxs-lookup"><span data-stu-id="ac509-163">Click **Add**.</span></span>

3. <span data-ttu-id="ac509-164">Coller dans hello suivant Géomètre YAML.</span><span class="sxs-lookup"><span data-stu-id="ac509-164">Paste in hello following blueprint YAML.</span></span> <span data-ttu-id="ac509-165">Ce schéma contient un seul cluster avec une seule variante de service, que nous allons changer ultérieurement :</span><span class="sxs-lookup"><span data-stu-id="ac509-165">This blueprint contains one cluster with only one service variant, which we change in a later step:</span></span>

  ```YAML
  name: sava                        # deployment name
  gateways:
    9050: sava_cluster/webport      # stable endpoint
  clusters:
    sava_cluster:               # cluster toocreate
     services:
        -
          breed:
            name: sava:1.0.0        # service variant name
            deployable: magneticio/sava:1.0.0
            ports:
              webport: 8080/http # cluster endpoint, used for canary releasing
  ```

4. <span data-ttu-id="ac509-166">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="ac509-166">Click **Save**.</span></span> <span data-ttu-id="ac509-167">Une EMPEIGNE lance le déploiement de hello.</span><span class="sxs-lookup"><span data-stu-id="ac509-167">Vamp initiates hello deployment.</span></span>

<span data-ttu-id="ac509-168">déploiement de Hello est répertorié sur hello **déploiements** page.</span><span class="sxs-lookup"><span data-stu-id="ac509-168">hello deployment is listed on hello **Deployments** page.</span></span> <span data-ttu-id="ac509-169">Cliquez sur hello déploiement toomonitor son état.</span><span class="sxs-lookup"><span data-stu-id="ac509-169">Click hello deployment toomonitor its status.</span></span>

![Interface utilisateur de Vamp - Déploiement de sava](./media/container-service-dcos-vamp-canary-release/09_sava100.png)

![service Sava dans l’interface utilisateur de Vamp](./media/container-service-dcos-vamp-canary-release/09a_sava100.png)

<span data-ttu-id="ac509-172">Deux passerelles sont créés, qui sont répertoriées sur hello **passerelles** page :</span><span class="sxs-lookup"><span data-stu-id="ac509-172">Two gateways are created, which are listed on hello **Gateways** page:</span></span>

* <span data-ttu-id="ac509-173">un Bonjour de tooaccess stable de point de terminaison (port 9050) de service en cours d’exécution</span><span class="sxs-lookup"><span data-stu-id="ac509-173">a stable endpoint tooaccess hello running service (port 9050)</span></span> 
* <span data-ttu-id="ac509-174">une passerelle interne gérée par Vamp (que nous décrirons plus en détail ultérieurement).</span><span class="sxs-lookup"><span data-stu-id="ac509-174">a Vamp-managed internal gateway (more on this gateway later).</span></span> 

![Interface utilisateur de Vamp - Passerelles sava](./media/container-service-dcos-vamp-canary-release/10_vamp_sava_gateways.png)

<span data-ttu-id="ac509-176">Hello sava service a maintenant déployé, mais vous ne peut pas y accéder en externe car hello équilibrage de charge Azure ne connaît pas encore tooforward trafic tooit.</span><span class="sxs-lookup"><span data-stu-id="ac509-176">hello sava service has now deployed, but you can’t access it externally because hello Azure Load Balancer doesn’t know tooforward traffic tooit yet.</span></span> <span data-ttu-id="ac509-177">service hello tooaccess, hello de mise à jour de configuration de mise en réseau Azure.</span><span class="sxs-lookup"><span data-stu-id="ac509-177">tooaccess hello service, update hello Azure networking configuration.</span></span>


## <a name="update-hello-azure-network-configuration"></a><span data-ttu-id="ac509-178">Mettre à jour la configuration du réseau Azure hello</span><span class="sxs-lookup"><span data-stu-id="ac509-178">Update hello Azure network configuration</span></span>

<span data-ttu-id="ac509-179">Une EMPEIGNE déployé le service sava hello sur des nœuds de l’agent de contrôleur de domaine/système d’exploitation hello, exposer un point de terminaison stable au port 9050.</span><span class="sxs-lookup"><span data-stu-id="ac509-179">Vamp deployed hello sava service on hello DC/OS agent nodes, exposing a stable endpoint at port 9050.</span></span> <span data-ttu-id="ac509-180">service de hello tooaccess cluster du contrôleur de domaine/système d’exploitation hello extérieur, apporter hello suivant la configuration de réseau Azure toohello de modifications dans votre déploiement de cluster :</span><span class="sxs-lookup"><span data-stu-id="ac509-180">tooaccess hello service from outside hello DC/OS cluster, make hello following changes toohello Azure network configuration in your cluster deployment:</span></span> 

1. <span data-ttu-id="ac509-181">**Configurer hello équilibrage de charge Azure** pour les agents de hello (hello ressource nommée **dcos-agent-lb-xxxx**) avec une sonde d’intégrité et de trafic tooforward de règle sur les instances de port 9050 toohello sava.</span><span class="sxs-lookup"><span data-stu-id="ac509-181">**Configure hello Azure Load Balancer** for hello agents (hello resource named **dcos-agent-lb-xxxx**) with a health probe and a rule tooforward traffic on port 9050 toohello sava instances.</span></span> 

2. <span data-ttu-id="ac509-182">**Groupe de sécurité réseau de mise à jour hello** pour les agents publics hello (hello ressource nommée **XXXX-agent-public-groupe de sécurité réseau-XXXX**) le trafic de tooallow sur le port 9050.</span><span class="sxs-lookup"><span data-stu-id="ac509-182">**Update hello network security group** for hello public agents (hello resource named **XXXX-agent-public-nsg-XXXX**) tooallow traffic on port 9050.</span></span>

<span data-ttu-id="ac509-183">Pour obtenir des instructions détaillées toocomplete ces tâches à l’aide de hello Azure portail, consultez [activer l’application de Service de conteneur Azure accès public tooan](container-service-enable-public-access.md).</span><span class="sxs-lookup"><span data-stu-id="ac509-183">For detailed steps toocomplete these tasks using hello Azure portal, see [Enable public access tooan Azure Container Service application](container-service-enable-public-access.md).</span></span> <span data-ttu-id="ac509-184">Spécifiez le port 9050 pour tous les paramètres de port.</span><span class="sxs-lookup"><span data-stu-id="ac509-184">Specify port 9050 for all port settings.</span></span>


<span data-ttu-id="ac509-185">Une fois que tout a été créé, accédez à toohello **vue d’ensemble** panneau d’équilibrage de charge de l’agent de contrôleur de domaine/système d’exploitation hello (hello ressource nommée **dcos-agent-lb-xxxx**).</span><span class="sxs-lookup"><span data-stu-id="ac509-185">Once everything has been created, go toohello **Overview** blade of hello DC/OS agent load balancer (hello resource named **dcos-agent-lb-xxxx**).</span></span> <span data-ttu-id="ac509-186">Recherche hello **adresse IP publique**et utilisez hello adresse tooaccess sava port 9050.</span><span class="sxs-lookup"><span data-stu-id="ac509-186">Find hello **Public IP address**, and use hello address tooaccess sava at port 9050.</span></span>

![Portail Azure - Obtenir un adresse IP publique](./media/container-service-dcos-vamp-canary-release/18_public_ip_address.png)

![sava](./media/container-service-dcos-vamp-canary-release/19_sava100.png)


## <a name="run-a-canary-release"></a><span data-ttu-id="ac509-189">Exécuter un contrôle de validité de mise en production</span><span class="sxs-lookup"><span data-stu-id="ac509-189">Run a canary release</span></span>

<span data-ttu-id="ac509-190">Vous disposez d’une nouvelle version de cette application que vous souhaitez version toocanary en production.</span><span class="sxs-lookup"><span data-stu-id="ac509-190">Suppose you have a new version of this application that you want toocanary release into production.</span></span> <span data-ttu-id="ac509-191">Vous avez placées dans des conteneurs en tant que magneticio/sava:1.1.0 et toogo prêt.</span><span class="sxs-lookup"><span data-stu-id="ac509-191">You have it containerized as magneticio/sava:1.1.0 and are ready toogo.</span></span> <span data-ttu-id="ac509-192">Une EMPEIGNE vous permet d’ajouter facilement de nouveaux services toohello déploiement en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="ac509-192">Vamp lets you easily add new services toohello running deployment.</span></span> <span data-ttu-id="ac509-193">Ces services « fusionnées » sont déployés en même temps que les services existants de hello dans un cluster de hello et une pondération de 0 %.</span><span class="sxs-lookup"><span data-stu-id="ac509-193">These "merged" services are deployed alongside hello existing services in hello cluster, and assigned a weight of 0%.</span></span> <span data-ttu-id="ac509-194">Aucun trafic n’est routé tooa qui vient d’être fusionnée service jusqu'à ce que vous ajustez la distribution du trafic hello.</span><span class="sxs-lookup"><span data-stu-id="ac509-194">No traffic is routed tooa newly merged service until you adjust hello traffic distribution.</span></span> <span data-ttu-id="ac509-195">curseur de poids Hello Bonjour Vamp de l’interface utilisateur procure un contrôle total sur distribution hello, en tenant compte d’ajustements incrémentielle (version canary) ou une restauration instantanée.</span><span class="sxs-lookup"><span data-stu-id="ac509-195">hello weight slider in hello Vamp UI gives you complete control over hello distribution, allowing for incremental adjustments (canary release) or an instant rollback.</span></span>

### <a name="merge-a-new-service-variant"></a><span data-ttu-id="ac509-196">Fusionner une nouvelle variante de service</span><span class="sxs-lookup"><span data-stu-id="ac509-196">Merge a new service variant</span></span>

<span data-ttu-id="ac509-197">toomerge hello nouveau sava 1.1 service avec hello déploiement en cours d’exécution :</span><span class="sxs-lookup"><span data-stu-id="ac509-197">toomerge hello new sava 1.1 service with hello running deployment:</span></span>

1. <span data-ttu-id="ac509-198">Bonjour Vamp de l’interface utilisateur, cliquez sur **projets**.</span><span class="sxs-lookup"><span data-stu-id="ac509-198">In hello Vamp UI, click **Blueprints**.</span></span>

2. <span data-ttu-id="ac509-199">Cliquez sur **ajouter** et coller dans hello suivant Géomètre YAML : ce modèle décrit un nouveau toodeploy de variante (sava : 1.1.0) de service dans un cluster existant de hello (sava_cluster).</span><span class="sxs-lookup"><span data-stu-id="ac509-199">Click **Add** and paste in hello following blueprint YAML: This blueprint describes a new service variant (sava:1.1.0) toodeploy within hello existing cluster (sava_cluster).</span></span>

  ```YAML
  name: sava:1.1.0      # blueprint name
  clusters:
    sava_cluster:       # cluster tooupdate
      services:
        -
          breed:
            name: sava:1.1.0    # service variant name
            deployable: magneticio/sava:1.1.0    
            ports:
              webport: 8080/http # cluster endpoint tooupdate
  ```
  
3. <span data-ttu-id="ac509-200">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="ac509-200">Click **Save**.</span></span> <span data-ttu-id="ac509-201">plan de Hello est stocké et répertorié sur hello **projets** page.</span><span class="sxs-lookup"><span data-stu-id="ac509-201">hello blueprint is stored and listed on hello **Blueprints** page.</span></span>

4. <span data-ttu-id="ac509-202">Menu action de hello ouvert sur le plan de sava : 1.1 hello et cliquez sur **de fusion pour**.</span><span class="sxs-lookup"><span data-stu-id="ac509-202">Open hello action menu on hello sava:1.1 blueprint and click **Merge to**.</span></span>

  ![Interface utilisateur de Vamp - Schémas](./media/container-service-dcos-vamp-canary-release/20_sava110_mergeto.png)

5. <span data-ttu-id="ac509-204">Sélectionnez hello **sava** déploiement et cliquez sur **fusion**.</span><span class="sxs-lookup"><span data-stu-id="ac509-204">Select hello **sava** deployment and click **Merge**.</span></span>

  ![Vamp UI - plan toodeployment de fusion](./media/container-service-dcos-vamp-canary-release/21_sava110_merge.png)

<span data-ttu-id="ac509-206">Une EMPEIGNE déploie hello nouvelle sava : 1.1.0 variante de service décrite dans le plan de hello en même temps que sava : 1.0.0 Bonjour **sava_cluster** Hello déploiement en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="ac509-206">Vamp deploys hello new sava:1.1.0 service variant described in hello blueprint alongside sava:1.0.0 in hello **sava_cluster** of hello running deployment.</span></span> 

![Interface utilisateur de Vamp - Déploiement de sava mis à jour](./media/container-service-dcos-vamp-canary-release/22_sava_cluster.png)

<span data-ttu-id="ac509-208">Hello **sava/sava_cluster/webport** passerelle (point de terminaison de cluster hello) est également mise à jour de, l’ajout d’un itinéraire toohello qui vient d’être déployé sava : 1.1.0.</span><span class="sxs-lookup"><span data-stu-id="ac509-208">hello **sava/sava_cluster/webport** gateway (hello cluster endpoint) is also updated, adding a route toohello newly deployed sava:1.1.0.</span></span> <span data-ttu-id="ac509-209">À ce stade, aucun trafic n’est routé ici (hello **poids** a la valeur too0 %).</span><span class="sxs-lookup"><span data-stu-id="ac509-209">At this point, no traffic is routed here (hello **WEIGHT** is set too0%).</span></span>

![Interface utilisateur de Vamp - Passerelle de cluster](./media/container-service-dcos-vamp-canary-release/23_sava_cluster_webport.png)

### <a name="canary-release"></a><span data-ttu-id="ac509-211">Contrôle la validité de la mise en production</span><span class="sxs-lookup"><span data-stu-id="ac509-211">Canary release</span></span>

<span data-ttu-id="ac509-212">Les deux versions de sava déployé Bonjour même cluster, ajuster la distribution de hello du trafic entre eux en déplaçant hello **poids** curseur.</span><span class="sxs-lookup"><span data-stu-id="ac509-212">With both versions of sava deployed in hello same cluster, adjust hello distribution of traffic between them by moving hello **WEIGHT** slider.</span></span>

1. <span data-ttu-id="ac509-213">Cliquez sur ![Vamp UI - modifier](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) suivant trop**poids**.</span><span class="sxs-lookup"><span data-stu-id="ac509-213">Click ![Vamp UI - edit](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) next too**WEIGHT**.</span></span>

2. <span data-ttu-id="ac509-214">Définissez hello poids distribution too50%/50% et cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="ac509-214">Set hello weight distribution too50%/50% and click **Save**.</span></span>

  ![Interface utilisateur de Vamp - Curseur de poids de passerelle](./media/container-service-dcos-vamp-canary-release/24_sava_cluster_webport_weight.png)

3. <span data-ttu-id="ac509-216">Revenir en arrière tooyour navigateur et actualiser la page de sava hello plusieurs fois.</span><span class="sxs-lookup"><span data-stu-id="ac509-216">Go back tooyour browser and refresh hello sava page a few more times.</span></span> <span data-ttu-id="ac509-217">application de sava Hello maintenant bascule entre une page sava : 1.0 et une page sava : 1.1.</span><span class="sxs-lookup"><span data-stu-id="ac509-217">hello sava application now switches between a sava:1.0 page and a sava:1.1 page.</span></span>

  ![alternance des services sava1.0 et sava1.1](./media/container-service-dcos-vamp-canary-release/25_sava_100_101.png)


  > [!NOTE]
  > <span data-ttu-id="ac509-219">Cette alternative de page de hello fonctionne mieux avec hello « Furtif » ou « Anonymous » en mode de votre navigateur en raison de hello mise en cache des éléments statiques.</span><span class="sxs-lookup"><span data-stu-id="ac509-219">This alternation of hello page works best with hello "Incognito" or “Anonymous” mode of your browser because of hello caching of static assets.</span></span>
  >

### <a name="filter-traffic"></a><span data-ttu-id="ac509-220">Filtrer le trafic</span><span class="sxs-lookup"><span data-stu-id="ac509-220">Filter traffic</span></span>

<span data-ttu-id="ac509-221">Supposons qu’après déploiement vous ayez découvert une incompatibilité dans sava:1.1.0 qui entraîne des problèmes d’affichage dans les navigateurs Firefox.</span><span class="sxs-lookup"><span data-stu-id="ac509-221">Suppose after deployment that you discovered an incompatibility in sava:1.1.0 that causes display problems in Firefox browsers.</span></span> <span data-ttu-id="ac509-222">Vous pouvez définir une EMPEIGNE toofilter du trafic entrant et diriger que tous les utilisateurs de Firefox sauvegarder toohello connu sava : 1.0.0 stable.</span><span class="sxs-lookup"><span data-stu-id="ac509-222">You can set Vamp toofilter incoming traffic and direct all Firefox users back toohello known stable sava:1.0.0.</span></span> <span data-ttu-id="ac509-223">Ce filtre instantanément résout hello interruption pour les utilisateurs de Firefox, tandis que celles des autres locataires continue tooenjoy les avantages de hello Hello améliorées sava : 1.1.0.</span><span class="sxs-lookup"><span data-stu-id="ac509-223">This filter instantly resolves hello disruption for Firefox users, while everybody else continues tooenjoy hello benefits of hello improved sava:1.1.0.</span></span>

<span data-ttu-id="ac509-224">Vamp utilise **conditions** trafic toofilter entre les itinéraires dans une passerelle.</span><span class="sxs-lookup"><span data-stu-id="ac509-224">Vamp uses **conditions** toofilter traffic between routes in a gateway.</span></span> <span data-ttu-id="ac509-225">Le trafic est tout d’abord filtré et dirigées conséquente toohello conditions appliquées tooeach itinéraire.</span><span class="sxs-lookup"><span data-stu-id="ac509-225">Traffic is first filtered and directed according toohello conditions applied tooeach route.</span></span> <span data-ttu-id="ac509-226">Tout le trafic restant est distribué en fonction du paramètre d’épaisseur toohello passerelle.</span><span class="sxs-lookup"><span data-stu-id="ac509-226">All remaining traffic is distributed according toohello gateway weight setting.</span></span>

<span data-ttu-id="ac509-227">Vous pouvez créer une condition toofilter tous les utilisateurs de Firefox et diriger les toohello ancien sava : 1.0.0 :</span><span class="sxs-lookup"><span data-stu-id="ac509-227">You can create a condition toofilter all Firefox users and direct them toohello old sava:1.0.0:</span></span>

1. <span data-ttu-id="ac509-228">Sur hello sava/sava_cluster/webport **passerelles** , cliquez sur ![Vamp UI - modifier](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) tooadd un **CONDITION** toohello itinéraire sava/sava_cluster/sava:1.0.0/webport.</span><span class="sxs-lookup"><span data-stu-id="ac509-228">On hello sava/sava_cluster/webport **Gateways** page, click ![Vamp UI - edit](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) tooadd a **CONDITION** toohello route sava/sava_cluster/sava:1.0.0/webport.</span></span> 

2. <span data-ttu-id="ac509-229">Entrez la condition de hello **agent utilisateur == Firefox** et cliquez sur ![Vamp UI - enregistrer](./media/container-service-dcos-vamp-canary-release/vamp_ui_save.png).</span><span class="sxs-lookup"><span data-stu-id="ac509-229">Enter hello condition **user-agent == Firefox** and click ![Vamp UI - save](./media/container-service-dcos-vamp-canary-release/vamp_ui_save.png).</span></span>

  <span data-ttu-id="ac509-230">Une EMPEIGNE ajoute la condition hello avec un niveau par défaut de 0 %.</span><span class="sxs-lookup"><span data-stu-id="ac509-230">Vamp adds hello condition with a default strength of 0%.</span></span> <span data-ttu-id="ac509-231">toostart filtrant le trafic, vous avez besoin de puissance de condition tooadjust hello.</span><span class="sxs-lookup"><span data-stu-id="ac509-231">toostart filtering traffic, you need tooadjust hello condition strength.</span></span>

3. <span data-ttu-id="ac509-232">Cliquez sur ![Vamp UI - modifier](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) toochange hello **force** appliqué toohello condition.</span><span class="sxs-lookup"><span data-stu-id="ac509-232">Click ![Vamp UI - edit](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) toochange hello **STRENGTH** applied toohello condition.</span></span>
 
4. <span data-ttu-id="ac509-233">Ensemble hello **force** too100 % et cliquez sur ![Vamp UI - enregistrer](./media/container-service-dcos-vamp-canary-release/vamp_ui_save.png) toosave.</span><span class="sxs-lookup"><span data-stu-id="ac509-233">Set hello **STRENGTH** too100% and click ![Vamp UI - save](./media/container-service-dcos-vamp-canary-release/vamp_ui_save.png) toosave.</span></span>

  <span data-ttu-id="ac509-234">Désormais, une EMPEIGNE envoie tout le trafic correspondant hello condition (tous les utilisateurs de Firefox) toosava:1.0.0.</span><span class="sxs-lookup"><span data-stu-id="ac509-234">Vamp now sends all traffic matching hello condition (all Firefox users) toosava:1.0.0.</span></span>

  ![Vamp UI - appliquer la condition toogateway](./media/container-service-dcos-vamp-canary-release/26_apply_condition.png)

5. <span data-ttu-id="ac509-236">Enfin, ajuster hello passerelle poids toosend tous les autres le trafic (tous les utilisateurs non-Firefox) toohello nouveau sava : 1.1.0.</span><span class="sxs-lookup"><span data-stu-id="ac509-236">Finally, adjust hello gateway weight toosend all remaining traffic (all non-Firefox users) toohello new sava:1.1.0.</span></span> <span data-ttu-id="ac509-237">Cliquez sur ![Vamp UI - modifier](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) suivant trop**poids** et définissez la distribution du poids hello 100 % est dirigée toohello itinéraire sava/sava_cluster/sava:1.1.0/webport.</span><span class="sxs-lookup"><span data-stu-id="ac509-237">Click ![Vamp UI - edit](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) next too**WEIGHT** and set hello weight distribution so 100% is directed toohello route sava/sava_cluster/sava:1.1.0/webport.</span></span>

  <span data-ttu-id="ac509-238">Tout le trafic non filtré par la condition de hello est maintenant dirigée toohello nouveau sava : 1.1.0.</span><span class="sxs-lookup"><span data-stu-id="ac509-238">All traffic not filtered by hello condition is now directed toohello new sava:1.1.0.</span></span>

6. <span data-ttu-id="ac509-239">filtre de hello de toosee en action, ouvrez deux différents navigateurs (un Firefox et un autre navigateur) et accéder au service de sava hello à partir des deux.</span><span class="sxs-lookup"><span data-stu-id="ac509-239">toosee hello filter in action, open two different browsers (one Firefox and one other browser) and access hello sava service from both.</span></span> <span data-ttu-id="ac509-240">Toutes les demandes de Firefox sont envoyés toosava:1.0.0, alors que tous les autres navigateurs sont toosava:1.1.0 dirigée.</span><span class="sxs-lookup"><span data-stu-id="ac509-240">All Firefox requests are sent toosava:1.0.0, while all other browsers are directed toosava:1.1.0.</span></span>

  ![Interface utilisateur de Vamp - Filtrer le trafic](./media/container-service-dcos-vamp-canary-release/27_filter_traffic.png)

## <a name="summing-up"></a><span data-ttu-id="ac509-242">Résumé</span><span class="sxs-lookup"><span data-stu-id="ac509-242">Summing up</span></span>

<span data-ttu-id="ac509-243">Cet article a été un tooVamp brève introduction sur un cluster de contrôleur de domaine/système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="ac509-243">This article was a quick introduction tooVamp on a DC/OS cluster.</span></span> <span data-ttu-id="ac509-244">Pour commencer, que vous avez obtenu une EMPEIGNE et en cours d’exécution sur votre conteneur de Service de contrôleur de domaine/système d’exploitation Azure cluster, déployé un service avec un plan d’une EMPEIGNE et consulté au point de terminaison hello exposé (passerelle).</span><span class="sxs-lookup"><span data-stu-id="ac509-244">For starters, you got Vamp up and running on your Azure Container Service DC/OS cluster, deployed a service with a Vamp blueprint, and accessed it at hello exposed endpoint (gateway).</span></span>

<span data-ttu-id="ac509-245">Nous avons abordé également certaines fonctionnalités puissantes d’une EMPEIGNE : la fusion d’un nouveau toohello variant service déploiement en cours d’exécution et présentation de façon incrémentielle, puis le filtrage du trafic tooresolve une incompatibilité connue.</span><span class="sxs-lookup"><span data-stu-id="ac509-245">We also touched on some powerful features of Vamp:  merging a new service variant toohello running deployment and introducing it incrementally, then filtering traffic tooresolve a known incompatibility.</span></span>


## <a name="next-steps"></a><span data-ttu-id="ac509-246">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ac509-246">Next steps</span></span>

* <span data-ttu-id="ac509-247">En savoir plus sur la gestion des actions d’une EMPEIGNE via hello [Vamp des API REST](http://vamp.io/documentation/api/api-reference/).</span><span class="sxs-lookup"><span data-stu-id="ac509-247">Learn about managing Vamp actions through hello [Vamp REST API](http://vamp.io/documentation/api/api-reference/).</span></span>

* <span data-ttu-id="ac509-248">Générez des scripts d’automatisation de Vamp dans Node.js et exécutez-les en tant que [flux de travail Vamp](http://vamp.io/documentation/tutorials/create-a-workflow/).</span><span class="sxs-lookup"><span data-stu-id="ac509-248">Build Vamp automation scripts in Node.js and run them as [Vamp workflows](http://vamp.io/documentation/tutorials/create-a-workflow/).</span></span>

* <span data-ttu-id="ac509-249">Consultez des [didacticiels Vamp](http://vamp.io/documentation/tutorials/overview/) supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="ac509-249">See additional [VAMP tutorials](http://vamp.io/documentation/tutorials/overview/).</span></span>

