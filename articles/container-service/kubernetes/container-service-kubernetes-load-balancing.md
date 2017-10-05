---
title: "Équilibrer la charge des conteneurs Kubernetes dans un cluster Azure | Microsoft Docs"
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
ms.openlocfilehash: ab46bb204f14424e394ced499ffbc0ef1cada15b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="load-balance-containers-in-a-kubernetes-cluster-in-azure-container-service"></a><span data-ttu-id="cad05-104">Équilibrer la charge des conteneurs dans un cluster Kubernetes dans Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="cad05-104">Load balance containers in a Kubernetes cluster in Azure Container Service</span></span> 
<span data-ttu-id="cad05-105">Cet article présente l’équilibrage de charge dans un cluster Kubernetes dans Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="cad05-105">This article introduces load balancing in a Kubernetes cluster in Azure Container Service.</span></span> <span data-ttu-id="cad05-106">L’équilibrage de charge fournit une adresse IP accessible en externe pour le service et distribue le trafic réseau entre les blocs en cours d’exécution dans les machines virtuelles de l’agent.</span><span class="sxs-lookup"><span data-stu-id="cad05-106">Load balancing provides an externally accessible IP address for the service and distributes network traffic among the pods running in agent VMs.</span></span>

<span data-ttu-id="cad05-107">Vous pouvez configurer un service Kubernetes pour utiliser l’[équilibrage de charge Azure](../../load-balancer/load-balancer-overview.md) afin de gérer le trafic réseau externe (TCP).</span><span class="sxs-lookup"><span data-stu-id="cad05-107">You can set up a Kubernetes service to use [Azure Load Balancer](../../load-balancer/load-balancer-overview.md) to manage external network (TCP) traffic.</span></span> <span data-ttu-id="cad05-108">Avec une configuration supplémentaire, l’équilibrage de charge et le routage du trafic HTTP ou HTTPS ou des scénarios plus avancés sont possibles.</span><span class="sxs-lookup"><span data-stu-id="cad05-108">With additional configuration, load balancing and routing of HTTP or HTTPS traffic or more advanced scenarios are possible.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cad05-109">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="cad05-109">Prerequisites</span></span>
* <span data-ttu-id="cad05-110">[Déployer un cluster Kubernetes](container-service-kubernetes-walkthrough.md) dans Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="cad05-110">[Deploy a Kubernetes cluster](container-service-kubernetes-walkthrough.md) in Azure Container Service</span></span>
* <span data-ttu-id="cad05-111">[Connecter votre client](../container-service-connect.md) à votre cluster</span><span class="sxs-lookup"><span data-stu-id="cad05-111">[Connect your client](../container-service-connect.md) to your cluster</span></span>

## <a name="azure-load-balancer"></a><span data-ttu-id="cad05-112">Équilibrage de charge Azure</span><span class="sxs-lookup"><span data-stu-id="cad05-112">Azure load balancer</span></span>

<span data-ttu-id="cad05-113">Par défaut, un cluster Kubernetes déployé dans le Azure Container Service inclut un équilibrage de charge Azure accessible sur Internet pour les machines virtuelles de l’agent.</span><span class="sxs-lookup"><span data-stu-id="cad05-113">By default, a Kubernetes cluster deployed in Azure Container Service includes an Internet-facing Azure load balancer for the agent VMs.</span></span> <span data-ttu-id="cad05-114">(Une ressource d’équilibrage de charge distincte est configurée pour les machines virtuelles principales). L’équilibrage de charge Azure est de type Couche 4.</span><span class="sxs-lookup"><span data-stu-id="cad05-114">(A separate load balancer resource is configured for the master VMs.) Azure load balancer is a Layer 4 load balancer.</span></span> <span data-ttu-id="cad05-115">Actuellement, l’équilibrage de charge ne prend en charge que le trafic TCP Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="cad05-115">Currently, the load balancer only supports TCP traffic in Kubernetes.</span></span>

<span data-ttu-id="cad05-116">Lorsque vous créez un service Kubernetes, vous pouvez configurer automatiquement l’équilibrage de charge Azure afin d’autoriser l’accès au service.</span><span class="sxs-lookup"><span data-stu-id="cad05-116">When creating a Kubernetes service, you can automatically configure the Azure load balancer to allow access to the service.</span></span> <span data-ttu-id="cad05-117">Pour configurer l’équilibrage de charge, définissez le service `type` sur `LoadBalancer`.</span><span class="sxs-lookup"><span data-stu-id="cad05-117">To configure the load balancer, set the service `type` to `LoadBalancer`.</span></span> <span data-ttu-id="cad05-118">L'équilibrage de charge crée une règle qui mappe l'adresse IP publique et le numéro de port du trafic du service entrant aux adresses IP privées et aux numéros de port des blocs dans les machines virtuelles de l’agent (et inversement pour le trafic de réponse.</span><span class="sxs-lookup"><span data-stu-id="cad05-118">The load balancer creates a rule to map a public IP address and port number of incoming service traffic to the private IP addresses and port numbers of the pods in agent VMs (and vice versa for response traffic).</span></span> 

 <span data-ttu-id="cad05-119">Voici deux exemples montrant comment définir le service Kubernetes `type` sur `LoadBalancer`.</span><span class="sxs-lookup"><span data-stu-id="cad05-119">Following are two examples showing how to set the Kubernetes service `type` to `LoadBalancer`.</span></span> <span data-ttu-id="cad05-120">(Après avoir testé ces exemples, supprimez les déploiements si vous n’en avez plus besoin).</span><span class="sxs-lookup"><span data-stu-id="cad05-120">(After trying the examples, delete the deployments if you no longer need them.)</span></span>

### <a name="example-use-the-kubectl-expose-command"></a><span data-ttu-id="cad05-121">Par exemple : utilisez la commande `kubectl expose`</span><span class="sxs-lookup"><span data-stu-id="cad05-121">Example: Use the `kubectl expose` command</span></span> 
<span data-ttu-id="cad05-122">La [procédure pas à pas Kubernetes](container-service-kubernetes-walkthrough.md) inclut un exemple montrant comment exposer un service avec la commande `kubectl expose` et son indicateur `--type=LoadBalancer`.</span><span class="sxs-lookup"><span data-stu-id="cad05-122">The [Kubernetes walkthrough](container-service-kubernetes-walkthrough.md) includes an example of how to expose a service with the `kubectl expose` command and its `--type=LoadBalancer` flag.</span></span> <span data-ttu-id="cad05-123">Voici la procédure à suivre :</span><span class="sxs-lookup"><span data-stu-id="cad05-123">Here are the steps :</span></span>

1. <span data-ttu-id="cad05-124">Démarrez un nouveau déploiement de conteneur.</span><span class="sxs-lookup"><span data-stu-id="cad05-124">Start a new container deployment.</span></span> <span data-ttu-id="cad05-125">Par exemple, la commande suivante démarre un nouveau déploiement appelé `mynginx`.</span><span class="sxs-lookup"><span data-stu-id="cad05-125">For example, the following command starts a new deployment called `mynginx`.</span></span> <span data-ttu-id="cad05-126">Le déploiement se compose de trois conteneurs en fonction de l’image Docker pour le serveur web Nginx.</span><span class="sxs-lookup"><span data-stu-id="cad05-126">The deployment consists of three containers based on the Docker image for the Nginx web server.</span></span>

    ```console
    kubectl run mynginx --replicas=3 --image nginx
    ```
2. <span data-ttu-id="cad05-127">Vérifiez que les contrôleurs sont en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="cad05-127">Verify that the containers are running.</span></span> <span data-ttu-id="cad05-128">Par exemple, si vous interrogez les conteneurs avec `kubectl get pods`, vous voyez une sortie similaire à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="cad05-128">For example, if you query for the containers with `kubectl get pods`, you see output similar to the following:</span></span>

    ![Obtenir des conteneurs Nginx](./media/container-service-kubernetes-load-balancing/nginx-get-pods.png)

3. <span data-ttu-id="cad05-130">Pour configurer l’équilibrage de charge afin d’accepter le trafic externe au déploiement, exécutez `kubectl expose` avec `--type=LoadBalancer`.</span><span class="sxs-lookup"><span data-stu-id="cad05-130">To configure the load balancer to accept external traffic to the deployment, run `kubectl expose` with `--type=LoadBalancer`.</span></span> <span data-ttu-id="cad05-131">La commande suivante expose le serveur Nginx sur le port 80 :</span><span class="sxs-lookup"><span data-stu-id="cad05-131">The following command exposes the Nginx server on port 80:</span></span>

    ```console
    kubectl expose deployments mynginx --port=80 --type=LoadBalancer
    ```

4. <span data-ttu-id="cad05-132">Tapez `kubectl get svc` pour afficher l’état des services dans le cluster.</span><span class="sxs-lookup"><span data-stu-id="cad05-132">Type `kubectl get svc` to see the state of the services in the cluster.</span></span> <span data-ttu-id="cad05-133">Pendant que l’équilibrage de charge configure la règle, l’élément `EXTERNAL-IP` du service apparaît en tant que `<pending>`.</span><span class="sxs-lookup"><span data-stu-id="cad05-133">While the load balancer configures the rule, the `EXTERNAL-IP` of the service appears as `<pending>`.</span></span> <span data-ttu-id="cad05-134">Après quelques minutes, l’adresse IP externe est configurée :</span><span class="sxs-lookup"><span data-stu-id="cad05-134">After a few minutes, the external IP address is configured:</span></span> 

    ![Configurer l’équilibrage de charge Azure](./media/container-service-kubernetes-load-balancing/nginx-external-ip.png)

5. <span data-ttu-id="cad05-136">Vérifiez que vous pouvez accéder au service avec l’adresse IP externe.</span><span class="sxs-lookup"><span data-stu-id="cad05-136">Verify that you can access the service at the external IP address.</span></span> <span data-ttu-id="cad05-137">Par exemple, ouvrez un navigateur web à l’adresse IP indiquée.</span><span class="sxs-lookup"><span data-stu-id="cad05-137">For example, open a web browser to the IP address shown.</span></span> <span data-ttu-id="cad05-138">Le navigateur affiche le serveur web Nginx en cours d’exécution dans un des conteneurs.</span><span class="sxs-lookup"><span data-stu-id="cad05-138">The browser shows the Nginx web server running in one of the containers.</span></span> <span data-ttu-id="cad05-139">Ou exécutez la commande `curl` ou `wget`.</span><span class="sxs-lookup"><span data-stu-id="cad05-139">Or, run the `curl` or `wget` command.</span></span> <span data-ttu-id="cad05-140">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="cad05-140">For example:</span></span>

    ```
    curl 13.82.93.130
    ```

    <span data-ttu-id="cad05-141">La sortie doit ressembler à celle-ci :</span><span class="sxs-lookup"><span data-stu-id="cad05-141">You should see output similar to:</span></span>

    ![Accéder à Nginx avec Curl](./media/container-service-kubernetes-load-balancing/curl-output.png)

6. <span data-ttu-id="cad05-143">Pour afficher la configuration de l’équilibrage de charge Azure, accédez au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="cad05-143">To see the configuration of the Azure load balancer, go to the [Azure portal](https://portal.azure.com).</span></span>

7. <span data-ttu-id="cad05-144">Recherchez le groupe de ressources du cluster de votre service de conteneur et sélectionnez l’équilibrage de charge pour les machines virtuelles de l’agent.</span><span class="sxs-lookup"><span data-stu-id="cad05-144">Browse for the resource group for your container service cluster, and select the load balancer for the agent VMs.</span></span> <span data-ttu-id="cad05-145">Son nom devrait être identique à celui du service de conteneur.</span><span class="sxs-lookup"><span data-stu-id="cad05-145">Its name should be the same as the container service.</span></span> <span data-ttu-id="cad05-146">(Ne choisissez pas l’équilibrage de charge pour les nœuds principaux, celui dont le nom inclut **master kg**.)</span><span class="sxs-lookup"><span data-stu-id="cad05-146">(Don't choose the load balancer for the master nodes, the one whose name includes **master-lb**.)</span></span> 

    ![Équilibrage de charge dans le groupe de ressources](./media/container-service-kubernetes-load-balancing/container-resource-group-portal.png)

8. <span data-ttu-id="cad05-148">Pour afficher les détails de la configuration d’équilibrage de charge, cliquez sur **Règles d’équilibrage de la charge** et sur le nom de la règle qui a été configurée.</span><span class="sxs-lookup"><span data-stu-id="cad05-148">To see the details of the load balancer configuration, click **Load balancing rules** and the name of the rule that was configured.</span></span>

    ![Règles d'équilibrage de charge](./media/container-service-kubernetes-load-balancing/load-balancing-rules.png) 

### <a name="example-specify-type-loadbalancer-in-the-service-configuration-file"></a><span data-ttu-id="cad05-150">Exemple : spécifiez `type: LoadBalancer` dans le fichier de configuration de service</span><span class="sxs-lookup"><span data-stu-id="cad05-150">Example: Specify `type: LoadBalancer` in the service configuration file</span></span>

<span data-ttu-id="cad05-151">Si vous déployez une application de conteneur Kubernetes à partir d’un [fichier de configuration de service](https://kubernetes.io/docs/user-guide/services/operations/#service-configuration-file) YAML ou JSON, spécifiez un équilibreur de charge externe en ajoutant la ligne suivante à la spécification du service :</span><span class="sxs-lookup"><span data-stu-id="cad05-151">If you deploy a Kubernetes container app from a YAML or JSON [service configuration file](https://kubernetes.io/docs/user-guide/services/operations/#service-configuration-file), specify an external load balancer by adding the following line to the service specification:</span></span>

```YAML
 "type": "LoadBalancer"
``` 



<span data-ttu-id="cad05-152">Les étapes suivantes utilisent l’[exemple Guestbook (livre d’or)](https://github.com/kubernetes/kubernetes/tree/master/examples/guestbook) Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="cad05-152">The following steps use the Kubernetes [Guestbook example](https://github.com/kubernetes/kubernetes/tree/master/examples/guestbook).</span></span> <span data-ttu-id="cad05-153">Cet exemple s’appuie sur une application web multiniveau basée sur des images Redis et PHP Docker.</span><span class="sxs-lookup"><span data-stu-id="cad05-153">This example is a multi-tier web app based on  Redis and PHP Docker images.</span></span> <span data-ttu-id="cad05-154">Dans le fichier de configuration de service, vous pouvez spécifier que le serveur PHP frontal utilise l’équilibrage de charge Azure.</span><span class="sxs-lookup"><span data-stu-id="cad05-154">You can specify in the service configuration file that the frontend PHP server uses the Azure load balancer.</span></span>

1. <span data-ttu-id="cad05-155">Téléchargez le fichier `guestbook-all-in-one.yaml` à partir de [GitHub](https://github.com/kubernetes/kubernetes/tree/master/examples/guestbook/all-in-one).</span><span class="sxs-lookup"><span data-stu-id="cad05-155">Download the file `guestbook-all-in-one.yaml` from [GitHub](https://github.com/kubernetes/kubernetes/tree/master/examples/guestbook/all-in-one).</span></span> 
2. <span data-ttu-id="cad05-156">Recherchez l’élément `spec` pour le service `frontend`.</span><span class="sxs-lookup"><span data-stu-id="cad05-156">Browse for the `spec` for the `frontend` service.</span></span>
3. <span data-ttu-id="cad05-157">Supprimez les marques de commentaire de la ligne `type: LoadBalancer`.</span><span class="sxs-lookup"><span data-stu-id="cad05-157">Uncomment the line `type: LoadBalancer`.</span></span>

    ![Équilibrage de charge dans la configuration du service](./media/container-service-kubernetes-load-balancing/guestbook-frontend-loadbalance.png)

4. <span data-ttu-id="cad05-159">Enregistrez le fichier, puis déployez l’app en exécutant la commande ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="cad05-159">Save the file, and deploy the app by running the following command:</span></span>

    ```
    kubectl create -f guestbook-all-in-one.yaml
    ```

5. <span data-ttu-id="cad05-160">Tapez `kubectl get svc` pour afficher l’état des services dans le cluster.</span><span class="sxs-lookup"><span data-stu-id="cad05-160">Type `kubectl get svc` to see the state of the services in the cluster.</span></span> <span data-ttu-id="cad05-161">Pendant que l’équilibrage de charge configure la règle, l’élément `EXTERNAL-IP` du service `frontend` apparaît sous la forme `<pending>`.</span><span class="sxs-lookup"><span data-stu-id="cad05-161">While the load balancer configures the rule, the `EXTERNAL-IP` of the `frontend` service appears as `<pending>`.</span></span> <span data-ttu-id="cad05-162">Après quelques minutes, l’adresse IP externe est configurée :</span><span class="sxs-lookup"><span data-stu-id="cad05-162">After a few minutes, the external IP address is configured:</span></span> 

    ![Configurer l’équilibrage de charge Azure](./media/container-service-kubernetes-load-balancing/guestbook-external-ip.png)

6. <span data-ttu-id="cad05-164">Vérifiez que vous pouvez accéder au service avec l’adresse IP externe.</span><span class="sxs-lookup"><span data-stu-id="cad05-164">Verify that you can access the service at the external IP address.</span></span> <span data-ttu-id="cad05-165">Par exemple, vous pouvez ouvrir un navigateur web à l’adresse IP externe du service.</span><span class="sxs-lookup"><span data-stu-id="cad05-165">For example, you can open a web browser to the external IP address of the service.</span></span>

    ![Accéder en externe au livre d’or](./media/container-service-kubernetes-load-balancing/guestbook-web.png)

    <span data-ttu-id="cad05-167">Vous pouvez ajouter des entrées du livre d’or.</span><span class="sxs-lookup"><span data-stu-id="cad05-167">You can add guestbook entries.</span></span>

7. <span data-ttu-id="cad05-168">Pour afficher la configuration de l’équilibrage de charge Azure, recherchez la ressource d’équilibrage de charge du cluster dans le [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="cad05-168">To see the configuration of the Azure load balancer, browse for the load balancer resource for the cluster in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="cad05-169">Consultez les étapes décrites dans l’exemple précédent.</span><span class="sxs-lookup"><span data-stu-id="cad05-169">See the steps in the previous example.</span></span>

### <a name="considerations"></a><span data-ttu-id="cad05-170">Considérations</span><span class="sxs-lookup"><span data-stu-id="cad05-170">Considerations</span></span>

* <span data-ttu-id="cad05-171">La création de la règle d’équilibrage de charge est effectuée de façon asynchrone, et des informations concernant l’équilibrage approvisionné sont publiées dans le champ `status.loadBalancer` du service.</span><span class="sxs-lookup"><span data-stu-id="cad05-171">Creation of the load balancer rule happens asynchronously, and information about the provisioned balancer is published in the service’s `status.loadBalancer` field.</span></span>
* <span data-ttu-id="cad05-172">Une adresse IP virtuelle est automatiquement attribuée à chaque service dans l’équilibreur de charge.</span><span class="sxs-lookup"><span data-stu-id="cad05-172">Every service is automatically assigned its own virtual IP address in the load balancer.</span></span>
* <span data-ttu-id="cad05-173">Si vous souhaitez accéder à l’équilibrage de charge à l’aide d’un nom DNS, contactez votre fournisseur de services de domaine afin de créer un nom DNS pour l’adresse IP de la règle.</span><span class="sxs-lookup"><span data-stu-id="cad05-173">If you want to reach the load balancer by a DNS name, work with your domain service provider to create a DNS name for the rule's IP address.</span></span>

## <a name="http-or-https-traffic"></a><span data-ttu-id="cad05-174">Trafic HTTP ou HTTPS</span><span class="sxs-lookup"><span data-stu-id="cad05-174">HTTP or HTTPS traffic</span></span>

<span data-ttu-id="cad05-175">Pour équilibrer le trafic HTTP ou HTTPS des applications web de conteneur et gérer les certificats du protocole TLS (Transport Security Layer), vous pouvez utiliser la ressource [Entrée](https://kubernetes.io/docs/user-guide/ingress/) de Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="cad05-175">To load balance HTTP or HTTPS traffic to container web apps and manage certificates for transport layer security (TLS), you can use the Kubernetes [Ingress](https://kubernetes.io/docs/user-guide/ingress/) resource.</span></span> <span data-ttu-id="cad05-176">Une entrée est une collection de règles qui autorisent les connexions entrantes à joindre les services du cluster.</span><span class="sxs-lookup"><span data-stu-id="cad05-176">An Ingress is a collection of rules that allow inbound connections to reach the cluster services.</span></span> <span data-ttu-id="cad05-177">Pour qu’une ressource Entrée fonctionne, le cluster Kubernetes doit avoir un [contrôleur d’entrée](https://kubernetes.io/docs/user-guide/ingress/#ingress-controllers) en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="cad05-177">For an Ingress resource to work, the Kubernetes cluster must have an [Ingress controller](https://kubernetes.io/docs/user-guide/ingress/#ingress-controllers) running.</span></span>

<span data-ttu-id="cad05-178">Azure Container Service n’implémente pas automatiquement un contrôleur d’entrée Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="cad05-178">Azure Container Service does not implement a Kubernetes Ingress controller automatically.</span></span> <span data-ttu-id="cad05-179">Plusieurs implémentations de contrôleur sont disponibles.</span><span class="sxs-lookup"><span data-stu-id="cad05-179">Several controller implementations are available.</span></span> <span data-ttu-id="cad05-180">Actuellement, le [contrôleur d’entrée Nginx](https://github.com/kubernetes/ingress/tree/master/examples/deployment/nginx) est recommandé pour configurer les règles d’entrée et équilibrer la charge du trafic HTTP et HTTPS.</span><span class="sxs-lookup"><span data-stu-id="cad05-180">Currently, the [Nginx Ingress controller](https://github.com/kubernetes/ingress/tree/master/examples/deployment/nginx) is recommended to configure Ingress rules and load balance HTTP and HTTPS traffic.</span></span> 

<span data-ttu-id="cad05-181">Pour plus d’informations, consultez la [documentation du contrôleur d’entrée Nginx](https://github.com/kubernetes/ingress/tree/master/controllers/nginx/README.md).</span><span class="sxs-lookup"><span data-stu-id="cad05-181">For more information, see the [Nginx Ingress controller documentation](https://github.com/kubernetes/ingress/tree/master/controllers/nginx/README.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cad05-182">Lorsque vous utilisez le contrôleur d’entrée Nginx dans Azure Container Service, vous devez exposer le déploiement du contrôleur en tant que service avec `type: LoadBalancer`.</span><span class="sxs-lookup"><span data-stu-id="cad05-182">When using the Nginx Ingress controller in Azure Container Service, you must expose the controller deployment as a service with `type: LoadBalancer`.</span></span> <span data-ttu-id="cad05-183">Cette opération configure l’équilibrage de charge Azure pour acheminer le trafic vers le contrôleur.</span><span class="sxs-lookup"><span data-stu-id="cad05-183">This configures the Azure load balancer to route traffic to the controller.</span></span> <span data-ttu-id="cad05-184">Pour plus d'informations, consultez la section précédente.</span><span class="sxs-lookup"><span data-stu-id="cad05-184">For more information, see the previous section.</span></span>


## <a name="next-steps"></a><span data-ttu-id="cad05-185">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="cad05-185">Next steps</span></span>

* <span data-ttu-id="cad05-186">Consultez la [documentation de l’équilibrage de charge Kubernetes](https://kubernetes.io/docs/user-guide/load-balancer/)</span><span class="sxs-lookup"><span data-stu-id="cad05-186">See the [Kubernetes LoadBalancer documentation](https://kubernetes.io/docs/user-guide/load-balancer/)</span></span>
* <span data-ttu-id="cad05-187">En savoir plus sur les [contrôleurs d’entrée, en particulier le contrôleur d’entrée Kubernetes](https://kubernetes.io/docs/user-guide/ingress/)</span><span class="sxs-lookup"><span data-stu-id="cad05-187">Learn more about [Kubernetes Ingress and Ingress controllers](https://kubernetes.io/docs/user-guide/ingress/)</span></span>
* <span data-ttu-id="cad05-188">Consultez les [exemples Kubernetes](https://github.com/kubernetes/kubernetes/tree/master/examples)</span><span class="sxs-lookup"><span data-stu-id="cad05-188">See [Kubernetes examples](https://github.com/kubernetes/kubernetes/tree/master/examples)</span></span>

