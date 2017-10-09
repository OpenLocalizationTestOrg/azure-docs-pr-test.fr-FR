---
title: "aaaLoad équilibrer Kubernetes des conteneurs dans Azure | Documents Microsoft"
description: "Connectez-vous en externe et équilibrez la charge sur plusieurs conteneurs dans un cluster Kubernetes dans Azure Container Service."
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Conteneurs, micro-services, Kubernetes, Azure
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/17/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: 8073c8d3a015a53a532c326749571cb2582e1bac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="load-balance-containers-in-a-kubernetes-cluster-in-azure-container-service"></a><span data-ttu-id="b10e5-104">Équilibrer la charge des conteneurs dans un cluster Kubernetes dans Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="b10e5-104">Load balance containers in a Kubernetes cluster in Azure Container Service</span></span> 
<span data-ttu-id="b10e5-105">Cet article présente l’équilibrage de charge dans un cluster Kubernetes dans Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="b10e5-105">This article introduces load balancing in a Kubernetes cluster in Azure Container Service.</span></span> <span data-ttu-id="b10e5-106">L’équilibrage de charge fournit une adresse IP accessible en externe pour le service de hello et distribue le trafic réseau entre les blocs hello en cours d’exécution dans des machines virtuelles de l’agent.</span><span class="sxs-lookup"><span data-stu-id="b10e5-106">Load balancing provides an externally accessible IP address for hello service and distributes network traffic among hello pods running in agent VMs.</span></span>

<span data-ttu-id="b10e5-107">Vous pouvez configurer un toouse de service Kubernetes [équilibrage de charge Azure](../../load-balancer/load-balancer-overview.md) toomanage externe (TCP) le trafic.</span><span class="sxs-lookup"><span data-stu-id="b10e5-107">You can set up a Kubernetes service toouse [Azure Load Balancer](../../load-balancer/load-balancer-overview.md) toomanage external network (TCP) traffic.</span></span> <span data-ttu-id="b10e5-108">Avec une configuration supplémentaire, l’équilibrage de charge et le routage du trafic HTTP ou HTTPS ou des scénarios plus avancés sont possibles.</span><span class="sxs-lookup"><span data-stu-id="b10e5-108">With additional configuration, load balancing and routing of HTTP or HTTPS traffic or more advanced scenarios are possible.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b10e5-109">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="b10e5-109">Prerequisites</span></span>
* <span data-ttu-id="b10e5-110">[Déployer un cluster Kubernetes](container-service-kubernetes-walkthrough.md) dans Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="b10e5-110">[Deploy a Kubernetes cluster](container-service-kubernetes-walkthrough.md) in Azure Container Service</span></span>
* <span data-ttu-id="b10e5-111">[Connectez votre client](../container-service-connect.md) tooyour cluster</span><span class="sxs-lookup"><span data-stu-id="b10e5-111">[Connect your client](../container-service-connect.md) tooyour cluster</span></span>

## <a name="azure-load-balancer"></a><span data-ttu-id="b10e5-112">Équilibrage de charge Azure</span><span class="sxs-lookup"><span data-stu-id="b10e5-112">Azure load balancer</span></span>

<span data-ttu-id="b10e5-113">Par défaut, un cluster Kubernetes déployé dans le Service de conteneur Azure comprend un équilibrage de charge Azure connecté à Internet pour l’agent hello machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="b10e5-113">By default, a Kubernetes cluster deployed in Azure Container Service includes an Internet-facing Azure load balancer for hello agent VMs.</span></span> <span data-ttu-id="b10e5-114">(Une ressource d’équilibrage de charge distinct est configurée pour le maître hello machines virtuelles). L’équilibrage de charge Azure est de type Couche 4.</span><span class="sxs-lookup"><span data-stu-id="b10e5-114">(A separate load balancer resource is configured for hello master VMs.) Azure load balancer is a Layer 4 load balancer.</span></span> <span data-ttu-id="b10e5-115">Actuellement, équilibrage de charge hello prend uniquement en charge le trafic TCP dans Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="b10e5-115">Currently, hello load balancer only supports TCP traffic in Kubernetes.</span></span>

<span data-ttu-id="b10e5-116">Lorsque vous créez un service Kubernetes, vous pouvez automatiquement configurer le service de toohello accès tooallow équilibrage de charge Azure hello.</span><span class="sxs-lookup"><span data-stu-id="b10e5-116">When creating a Kubernetes service, you can automatically configure hello Azure load balancer tooallow access toohello service.</span></span> <span data-ttu-id="b10e5-117">équilibrage de charge tooconfigure hello, jeu hello service `type` trop`LoadBalancer`.</span><span class="sxs-lookup"><span data-stu-id="b10e5-117">tooconfigure hello load balancer, set hello service `type` too`LoadBalancer`.</span></span> <span data-ttu-id="b10e5-118">équilibrage de charge Hello crée une règle toomap une adresse IP publique et de numéro de port d’entrant service trafic toohello des adresses IP privées et de numéros de port de POD de hello dans les machines virtuelles de l’agent (et vice versa pour le trafic de réponse).</span><span class="sxs-lookup"><span data-stu-id="b10e5-118">hello load balancer creates a rule toomap a public IP address and port number of incoming service traffic toohello private IP addresses and port numbers of hello pods in agent VMs (and vice versa for response traffic).</span></span> 

 <span data-ttu-id="b10e5-119">Voici deux exemples montrant comment tooset hello Kubernetes service `type` trop`LoadBalancer`.</span><span class="sxs-lookup"><span data-stu-id="b10e5-119">Following are two examples showing how tooset hello Kubernetes service `type` too`LoadBalancer`.</span></span> <span data-ttu-id="b10e5-120">(Après les exemples hello lors de la tentative, supprimez les déploiements hello si vous n’en avez plus besoin.).</span><span class="sxs-lookup"><span data-stu-id="b10e5-120">(After trying hello examples, delete hello deployments if you no longer need them.)</span></span>

### <a name="example-use-hello-kubectl-expose-command"></a><span data-ttu-id="b10e5-121">L’exemple : Hello d’utilisation `kubectl expose` commande</span><span class="sxs-lookup"><span data-stu-id="b10e5-121">Example: Use hello `kubectl expose` command</span></span> 
<span data-ttu-id="b10e5-122">Hello [Kubernetes procédure pas à pas](container-service-kubernetes-walkthrough.md) inclut un exemple de procédure tooexpose un service avec hello `kubectl expose` commande et son `--type=LoadBalancer` indicateur.</span><span class="sxs-lookup"><span data-stu-id="b10e5-122">hello [Kubernetes walkthrough](container-service-kubernetes-walkthrough.md) includes an example of how tooexpose a service with hello `kubectl expose` command and its `--type=LoadBalancer` flag.</span></span> <span data-ttu-id="b10e5-123">Voici les étapes hello :</span><span class="sxs-lookup"><span data-stu-id="b10e5-123">Here are hello steps :</span></span>

1. <span data-ttu-id="b10e5-124">Démarrez un nouveau déploiement de conteneur.</span><span class="sxs-lookup"><span data-stu-id="b10e5-124">Start a new container deployment.</span></span> <span data-ttu-id="b10e5-125">Par exemple, hello suivant de commande lance un nouveau déploiement appelé `mynginx`.</span><span class="sxs-lookup"><span data-stu-id="b10e5-125">For example, hello following command starts a new deployment called `mynginx`.</span></span> <span data-ttu-id="b10e5-126">déploiement de Hello se compose de trois conteneurs basés sur l’image de Docker hello pour le serveur de web Nginx hello.</span><span class="sxs-lookup"><span data-stu-id="b10e5-126">hello deployment consists of three containers based on hello Docker image for hello Nginx web server.</span></span>

    ```console
    kubectl run mynginx --replicas=3 --image nginx
    ```
2. <span data-ttu-id="b10e5-127">Vérifiez que les conteneurs hello sont en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="b10e5-127">Verify that hello containers are running.</span></span> <span data-ttu-id="b10e5-128">Par exemple, si vous interrogez des conteneurs hello avec `kubectl get pods`, sortie similaire toohello suivante :</span><span class="sxs-lookup"><span data-stu-id="b10e5-128">For example, if you query for hello containers with `kubectl get pods`, you see output similar toohello following:</span></span>

    ![Obtenir des conteneurs Nginx](./media/container-service-kubernetes-load-balancing/nginx-get-pods.png)

3. <span data-ttu-id="b10e5-130">tooconfigure hello équilibrage tooaccept trafic externe toohello déploiement, exécutez `kubectl expose` avec `--type=LoadBalancer`.</span><span class="sxs-lookup"><span data-stu-id="b10e5-130">tooconfigure hello load balancer tooaccept external traffic toohello deployment, run `kubectl expose` with `--type=LoadBalancer`.</span></span> <span data-ttu-id="b10e5-131">Hello commande suivante expose serveur Nginx de hello sur le port 80 :</span><span class="sxs-lookup"><span data-stu-id="b10e5-131">hello following command exposes hello Nginx server on port 80:</span></span>

    ```console
    kubectl expose deployments mynginx --port=80 --type=LoadBalancer
    ```

4. <span data-ttu-id="b10e5-132">Type `kubectl get svc` état de hello toosee hello des services inclus dans le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="b10e5-132">Type `kubectl get svc` toosee hello state of hello services in hello cluster.</span></span> <span data-ttu-id="b10e5-133">Lors de l’équilibrage de charge hello configure la règle de hello, hello `EXTERNAL-IP` Hello service apparaît en tant que `<pending>`.</span><span class="sxs-lookup"><span data-stu-id="b10e5-133">While hello load balancer configures hello rule, hello `EXTERNAL-IP` of hello service appears as `<pending>`.</span></span> <span data-ttu-id="b10e5-134">Après quelques minutes, l’adresse IP externe de hello est configurée :</span><span class="sxs-lookup"><span data-stu-id="b10e5-134">After a few minutes, hello external IP address is configured:</span></span> 

    ![Configurer l’équilibrage de charge Azure](./media/container-service-kubernetes-load-balancing/nginx-external-ip.png)

5. <span data-ttu-id="b10e5-136">Vérifiez que vous avez accès service hello à l’adresse IP externe de hello.</span><span class="sxs-lookup"><span data-stu-id="b10e5-136">Verify that you can access hello service at hello external IP address.</span></span> <span data-ttu-id="b10e5-137">Par exemple, ouvrez une adresse IP toohello navigateur web indiquée.</span><span class="sxs-lookup"><span data-stu-id="b10e5-137">For example, open a web browser toohello IP address shown.</span></span> <span data-ttu-id="b10e5-138">navigateur de Hello affiche le serveur de web Nginx hello en cours d’exécution dans un des conteneurs de hello.</span><span class="sxs-lookup"><span data-stu-id="b10e5-138">hello browser shows hello Nginx web server running in one of hello containers.</span></span> <span data-ttu-id="b10e5-139">Ou exécution hello `curl` ou `wget` commande.</span><span class="sxs-lookup"><span data-stu-id="b10e5-139">Or, run hello `curl` or `wget` command.</span></span> <span data-ttu-id="b10e5-140">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="b10e5-140">For example:</span></span>

    ```
    curl 13.82.93.130
    ```

    <span data-ttu-id="b10e5-141">La sortie doit ressembler à celle-ci :</span><span class="sxs-lookup"><span data-stu-id="b10e5-141">You should see output similar to:</span></span>

    ![Accéder à Nginx avec Curl](./media/container-service-kubernetes-load-balancing/curl-output.png)

6. <span data-ttu-id="b10e5-143">configuration de hello toosee d’équilibrage de charge Azure hello, accédez toohello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b10e5-143">toosee hello configuration of hello Azure load balancer, go toohello [Azure portal](https://portal.azure.com).</span></span>

7. <span data-ttu-id="b10e5-144">Rechercher un groupe de ressources hello pour votre cluster de service de conteneur et sélectionnez l’équilibrage de charge hello pour l’agent hello machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="b10e5-144">Browse for hello resource group for your container service cluster, and select hello load balancer for hello agent VMs.</span></span> <span data-ttu-id="b10e5-145">Son nom doit être hello même en tant que service de conteneur hello.</span><span class="sxs-lookup"><span data-stu-id="b10e5-145">Its name should be hello same as hello container service.</span></span> <span data-ttu-id="b10e5-146">(Ne pas choisir d’équilibrage de charge hello pour les nœuds principaux hello, hello une dont le nom inclut **master kg**.)</span><span class="sxs-lookup"><span data-stu-id="b10e5-146">(Don't choose hello load balancer for hello master nodes, hello one whose name includes **master-lb**.)</span></span> 

    ![Équilibrage de charge dans le groupe de ressources](./media/container-service-kubernetes-load-balancing/container-resource-group-portal.png)

8. <span data-ttu-id="b10e5-148">Détails de hello toosee de configuration d’équilibrage de charge hello, cliquez sur **règles d’équilibrage de charge** et le nom hello de règle hello qui a été configuré.</span><span class="sxs-lookup"><span data-stu-id="b10e5-148">toosee hello details of hello load balancer configuration, click **Load balancing rules** and hello name of hello rule that was configured.</span></span>

    ![Règles d'équilibrage de charge](./media/container-service-kubernetes-load-balancing/load-balancing-rules.png) 

### <a name="example-specify-type-loadbalancer-in-hello-service-configuration-file"></a><span data-ttu-id="b10e5-150">Exemple : Spécification `type: LoadBalancer` dans le fichier de configuration de service hello</span><span class="sxs-lookup"><span data-stu-id="b10e5-150">Example: Specify `type: LoadBalancer` in hello service configuration file</span></span>

<span data-ttu-id="b10e5-151">Si vous déployez une application de conteneur Kubernetes à partir de JSON YAML [fichier de configuration de service](https://kubernetes.io/docs/user-guide/services/operations/#service-configuration-file), spécifiez un équilibrage de charge externe en ajoutant hello suivant ligne toohello service spécification :</span><span class="sxs-lookup"><span data-stu-id="b10e5-151">If you deploy a Kubernetes container app from a YAML or JSON [service configuration file](https://kubernetes.io/docs/user-guide/services/operations/#service-configuration-file), specify an external load balancer by adding hello following line toohello service specification:</span></span>

```YAML
 "type": "LoadBalancer"
``` 



<span data-ttu-id="b10e5-152">Hello étapes suivantes utilisent hello Kubernetes [or exemple](https://github.com/kubernetes/kubernetes/tree/master/examples/guestbook).</span><span class="sxs-lookup"><span data-stu-id="b10e5-152">hello following steps use hello Kubernetes [Guestbook example](https://github.com/kubernetes/kubernetes/tree/master/examples/guestbook).</span></span> <span data-ttu-id="b10e5-153">Cet exemple s’appuie sur une application web multiniveau basée sur des images Redis et PHP Docker.</span><span class="sxs-lookup"><span data-stu-id="b10e5-153">This example is a multi-tier web app based on  Redis and PHP Docker images.</span></span> <span data-ttu-id="b10e5-154">Vous pouvez spécifier dans le fichier de configuration de service hello que serveur hello frontal PHP utilise l’équilibrage de charge Azure hello.</span><span class="sxs-lookup"><span data-stu-id="b10e5-154">You can specify in hello service configuration file that hello frontend PHP server uses hello Azure load balancer.</span></span>

1. <span data-ttu-id="b10e5-155">Télécharger le fichier de hello `guestbook-all-in-one.yaml` de [GitHub](https://github.com/kubernetes/kubernetes/tree/master/examples/guestbook/all-in-one).</span><span class="sxs-lookup"><span data-stu-id="b10e5-155">Download hello file `guestbook-all-in-one.yaml` from [GitHub](https://github.com/kubernetes/kubernetes/tree/master/examples/guestbook/all-in-one).</span></span> 
2. <span data-ttu-id="b10e5-156">Recherchez hello `spec` pour hello `frontend` service.</span><span class="sxs-lookup"><span data-stu-id="b10e5-156">Browse for hello `spec` for hello `frontend` service.</span></span>
3. <span data-ttu-id="b10e5-157">Supprimez les commentaires hello ligne `type: LoadBalancer`.</span><span class="sxs-lookup"><span data-stu-id="b10e5-157">Uncomment hello line `type: LoadBalancer`.</span></span>

    ![Équilibrage de charge dans la configuration du service](./media/container-service-kubernetes-load-balancing/guestbook-frontend-loadbalance.png)

4. <span data-ttu-id="b10e5-159">Enregistrer le fichier de hello et déployer l’application hello en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="b10e5-159">Save hello file, and deploy hello app by running hello following command:</span></span>

    ```
    kubectl create -f guestbook-all-in-one.yaml
    ```

5. <span data-ttu-id="b10e5-160">Type `kubectl get svc` état de hello toosee hello des services inclus dans le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="b10e5-160">Type `kubectl get svc` toosee hello state of hello services in hello cluster.</span></span> <span data-ttu-id="b10e5-161">Lors de l’équilibrage de charge hello configure la règle de hello, hello `EXTERNAL-IP` Hello `frontend` service apparaît sous la forme `<pending>`.</span><span class="sxs-lookup"><span data-stu-id="b10e5-161">While hello load balancer configures hello rule, hello `EXTERNAL-IP` of hello `frontend` service appears as `<pending>`.</span></span> <span data-ttu-id="b10e5-162">Après quelques minutes, l’adresse IP externe de hello est configurée :</span><span class="sxs-lookup"><span data-stu-id="b10e5-162">After a few minutes, hello external IP address is configured:</span></span> 

    ![Configurer l’équilibrage de charge Azure](./media/container-service-kubernetes-load-balancing/guestbook-external-ip.png)

6. <span data-ttu-id="b10e5-164">Vérifiez que vous avez accès service hello à l’adresse IP externe de hello.</span><span class="sxs-lookup"><span data-stu-id="b10e5-164">Verify that you can access hello service at hello external IP address.</span></span> <span data-ttu-id="b10e5-165">Par exemple, vous pouvez ouvrir une web navigateur toohello adresse IP externe du service de hello.</span><span class="sxs-lookup"><span data-stu-id="b10e5-165">For example, you can open a web browser toohello external IP address of hello service.</span></span>

    ![Accéder en externe au livre d’or](./media/container-service-kubernetes-load-balancing/guestbook-web.png)

    <span data-ttu-id="b10e5-167">Vous pouvez ajouter des entrées du livre d’or.</span><span class="sxs-lookup"><span data-stu-id="b10e5-167">You can add guestbook entries.</span></span>

7. <span data-ttu-id="b10e5-168">configuration de hello toosee d’équilibrage de charge Azure hello, recherchez pour la ressource de programme d’équilibrage de charge hello cluster hello Bonjour [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b10e5-168">toosee hello configuration of hello Azure load balancer, browse for hello load balancer resource for hello cluster in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="b10e5-169">Consultez les étapes dans l’exemple précédent de hello hello.</span><span class="sxs-lookup"><span data-stu-id="b10e5-169">See hello steps in hello previous example.</span></span>

### <a name="considerations"></a><span data-ttu-id="b10e5-170">Considérations</span><span class="sxs-lookup"><span data-stu-id="b10e5-170">Considerations</span></span>

* <span data-ttu-id="b10e5-171">La création de la règle d’équilibrage de charge hello se produit de façon asynchrone, et plus d’informations sur l’équilibrage de hello configuré sont publiés dans le service hello `status.loadBalancer` champ.</span><span class="sxs-lookup"><span data-stu-id="b10e5-171">Creation of hello load balancer rule happens asynchronously, and information about hello provisioned balancer is published in hello service’s `status.loadBalancer` field.</span></span>
* <span data-ttu-id="b10e5-172">Chaque service est affecté automatiquement sa propre adresse IP virtuelle de l’équilibreur de charge hello.</span><span class="sxs-lookup"><span data-stu-id="b10e5-172">Every service is automatically assigned its own virtual IP address in hello load balancer.</span></span>
* <span data-ttu-id="b10e5-173">Si vous souhaitez l’équilibrage de charge hello tooreach par un nom DNS, fonctionne avec votre toocreate de fournisseur de service de domaine un nom DNS pour l’adresse IP de la règle hello.</span><span class="sxs-lookup"><span data-stu-id="b10e5-173">If you want tooreach hello load balancer by a DNS name, work with your domain service provider toocreate a DNS name for hello rule's IP address.</span></span>

## <a name="http-or-https-traffic"></a><span data-ttu-id="b10e5-174">Trafic HTTP ou HTTPS</span><span class="sxs-lookup"><span data-stu-id="b10e5-174">HTTP or HTTPS traffic</span></span>

<span data-ttu-id="b10e5-175">Solde de tooload HTTP ou HTTPS trafic toocontainer les applications web et de gérer les certificats de sécurité de la couche transport (TLS), vous pouvez utiliser hello Kubernetes [entrée](https://kubernetes.io/docs/user-guide/ingress/) ressource.</span><span class="sxs-lookup"><span data-stu-id="b10e5-175">tooload balance HTTP or HTTPS traffic toocontainer web apps and manage certificates for transport layer security (TLS), you can use hello Kubernetes [Ingress](https://kubernetes.io/docs/user-guide/ingress/) resource.</span></span> <span data-ttu-id="b10e5-176">Une entrée est une collection de règles qui autorisent les connexions entrantes tooreach les services de cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="b10e5-176">An Ingress is a collection of rules that allow inbound connections tooreach hello cluster services.</span></span> <span data-ttu-id="b10e5-177">Pour un toowork de ressource en entrée, le cluster de Kubernetes de hello doit avoir un [contrôleur d’entrée](https://kubernetes.io/docs/user-guide/ingress/#ingress-controllers) en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="b10e5-177">For an Ingress resource toowork, hello Kubernetes cluster must have an [Ingress controller](https://kubernetes.io/docs/user-guide/ingress/#ingress-controllers) running.</span></span>

<span data-ttu-id="b10e5-178">Azure Container Service n’implémente pas automatiquement un contrôleur d’entrée Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="b10e5-178">Azure Container Service does not implement a Kubernetes Ingress controller automatically.</span></span> <span data-ttu-id="b10e5-179">Plusieurs implémentations de contrôleur sont disponibles.</span><span class="sxs-lookup"><span data-stu-id="b10e5-179">Several controller implementations are available.</span></span> <span data-ttu-id="b10e5-180">Actuellement, hello [contrôleur d’entrée de Nginx](https://github.com/kubernetes/ingress/tree/master/examples/deployment/nginx) est recommandé de règles d’entrée tooconfigure et équilibrer la charge du trafic HTTP et HTTPS.</span><span class="sxs-lookup"><span data-stu-id="b10e5-180">Currently, hello [Nginx Ingress controller](https://github.com/kubernetes/ingress/tree/master/examples/deployment/nginx) is recommended tooconfigure Ingress rules and load balance HTTP and HTTPS traffic.</span></span> 

<span data-ttu-id="b10e5-181">Pour plus d’informations, consultez hello [documentation du contrôleur Nginx entrée](https://github.com/kubernetes/ingress/tree/master/controllers/nginx/README.md).</span><span class="sxs-lookup"><span data-stu-id="b10e5-181">For more information, see hello [Nginx Ingress controller documentation](https://github.com/kubernetes/ingress/tree/master/controllers/nginx/README.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b10e5-182">Lorsque vous utilisez hello contrôleur de Nginx entrée dans le conteneur de Service Azure, vous devez exposer le déploiement de contrôleur hello en tant que service avec `type: LoadBalancer`.</span><span class="sxs-lookup"><span data-stu-id="b10e5-182">When using hello Nginx Ingress controller in Azure Container Service, you must expose hello controller deployment as a service with `type: LoadBalancer`.</span></span> <span data-ttu-id="b10e5-183">Cela configure le contrôleur de toohello hello Azure charge équilibrage tooroute le trafic.</span><span class="sxs-lookup"><span data-stu-id="b10e5-183">This configures hello Azure load balancer tooroute traffic toohello controller.</span></span> <span data-ttu-id="b10e5-184">Pour plus d’informations, consultez la section précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="b10e5-184">For more information, see hello previous section.</span></span>


## <a name="next-steps"></a><span data-ttu-id="b10e5-185">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b10e5-185">Next steps</span></span>

* <span data-ttu-id="b10e5-186">Consultez hello [Kubernetes LoadBalancer documentation](https://kubernetes.io/docs/user-guide/load-balancer/)</span><span class="sxs-lookup"><span data-stu-id="b10e5-186">See hello [Kubernetes LoadBalancer documentation](https://kubernetes.io/docs/user-guide/load-balancer/)</span></span>
* <span data-ttu-id="b10e5-187">En savoir plus sur les [contrôleurs d’entrée, en particulier le contrôleur d’entrée Kubernetes](https://kubernetes.io/docs/user-guide/ingress/)</span><span class="sxs-lookup"><span data-stu-id="b10e5-187">Learn more about [Kubernetes Ingress and Ingress controllers](https://kubernetes.io/docs/user-guide/ingress/)</span></span>
* <span data-ttu-id="b10e5-188">Consultez les [exemples Kubernetes](https://github.com/kubernetes/kubernetes/tree/master/examples)</span><span class="sxs-lookup"><span data-stu-id="b10e5-188">See [Kubernetes examples](https://github.com/kubernetes/kubernetes/tree/master/examples)</span></span>

