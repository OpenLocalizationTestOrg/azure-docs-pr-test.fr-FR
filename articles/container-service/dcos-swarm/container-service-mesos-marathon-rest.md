---
title: "Gérer le cluster DC/OS Azure avec l’API REST Marathon | Microsoft Docs"
description: "Déployez des conteneurs vers un cluster DC/OS Azure Container Service à l’aide de l’API REST Marathon."
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Docker, conteneurs, micro-services, Mesos, Azure
ms.assetid: c7175446-4507-4a33-a7a2-63583e5996e3
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/04/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: 65f8e0170fa7b89162e811a1d5dd58775fd20d7b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="dcos-container-management-through-the-marathon-rest-api"></a><span data-ttu-id="b0466-104">Gestion de conteneur DC/OS au moyen de l’API REST Marathon</span><span class="sxs-lookup"><span data-stu-id="b0466-104">DC/OS container management through the Marathon REST API</span></span>
<span data-ttu-id="b0466-105">DC/OS offre un environnement de déploiement et de mise à l’échelle des charges de travail en cluster tout en faisant abstraction du matériel sous-jacent.</span><span class="sxs-lookup"><span data-stu-id="b0466-105">DC/OS provides an environment for deploying and scaling clustered workloads, while abstracting the underlying hardware.</span></span> <span data-ttu-id="b0466-106">DC/OS sous-tend une infrastructure qui gère la planification et l’exécution des charges de travail de calcul.</span><span class="sxs-lookup"><span data-stu-id="b0466-106">On top of DC/OS, there is a framework that manages scheduling and executing compute workloads.</span></span> <span data-ttu-id="b0466-107">Bien qu’il existe des infrastructures pour de nombreuses charges de travail courantes, ce document décrit la création et la mise à l’échelle des déploiements de conteneurs avec l’API REST Marathon.</span><span class="sxs-lookup"><span data-stu-id="b0466-107">Although frameworks are available for many popular workloads, this document gets you started creating and scaling container deployments by using the Marathon REST API.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="b0466-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="b0466-108">Prerequisites</span></span>

<span data-ttu-id="b0466-109">Avant d’étudier ces exemples, vous devez avoir un cluster DC/OS configuré dans Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="b0466-109">Before working through these examples, you need a DC/OS cluster that is configured in Azure Container Service.</span></span> <span data-ttu-id="b0466-110">Vous devez également disposer d’une connectivité à distance à ce cluster.</span><span class="sxs-lookup"><span data-stu-id="b0466-110">You also need to have remote connectivity to this cluster.</span></span> <span data-ttu-id="b0466-111">Pour plus d’informations sur ces éléments, voir les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="b0466-111">For more information on these items, see the following articles:</span></span>

* [<span data-ttu-id="b0466-112">Déploiement d’un cluster Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="b0466-112">Deploying an Azure Container Service cluster</span></span>](container-service-deployment.md)
* [<span data-ttu-id="b0466-113">Connexion à un cluster Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="b0466-113">Connecting to an Azure Container Service cluster</span></span>](../container-service-connect.md)

## <a name="access-the-dcos-apis"></a><span data-ttu-id="b0466-114">Accéder aux API DC/OS</span><span class="sxs-lookup"><span data-stu-id="b0466-114">Access the DC/OS APIs</span></span>
<span data-ttu-id="b0466-115">Une fois que vous êtes connecté au cluster Azure Container Service, vous pouvez accéder à DC/OS et aux API REST associées via http://localhost:local-port.</span><span class="sxs-lookup"><span data-stu-id="b0466-115">After you are connected to the Azure Container Service cluster, you can access the DC/OS and related REST APIs through http://localhost:local-port.</span></span> <span data-ttu-id="b0466-116">Les exemples cités dans ce document partent du principe que vous créez un tunnel sur le port 80.</span><span class="sxs-lookup"><span data-stu-id="b0466-116">The examples in this document assume that you are tunneling on port 80.</span></span> <span data-ttu-id="b0466-117">Par exemple, les points de terminaison Marathon peuvent être atteints via les URI commençant par `http://localhost/marathon/v2/`.</span><span class="sxs-lookup"><span data-stu-id="b0466-117">For example, the Marathon endpoints can be reached at URIs beginning with `http://localhost/marathon/v2/`.</span></span> 

<span data-ttu-id="b0466-118">Pour plus d’informations sur les différentes API, consultez la documentation Mesosphere relative à l’[API Marathon](https://mesosphere.github.io/marathon/docs/rest-api.html) et à l’[API Chronos](https://mesos.github.io/chronos/docs/api.html), ainsi que la documentation Apache relative à l’[API Mesos Scheduler](http://mesos.apache.org/documentation/latest/scheduler-http-api/).</span><span class="sxs-lookup"><span data-stu-id="b0466-118">For more information on the various APIs, see the Mesosphere documentation for the [Marathon API](https://mesosphere.github.io/marathon/docs/rest-api.html) and the [Chronos API](https://mesos.github.io/chronos/docs/api.html), and the Apache documentation for the [Mesos Scheduler API](http://mesos.apache.org/documentation/latest/scheduler-http-api/).</span></span>

## <a name="gather-information-from-dcos-and-marathon"></a><span data-ttu-id="b0466-119">Collecte d’informations à partir de DC/OS et de Marathon</span><span class="sxs-lookup"><span data-stu-id="b0466-119">Gather information from DC/OS and Marathon</span></span>
<span data-ttu-id="b0466-120">Avant de déployer des conteneurs vers le cluster DC/OS, vous devez recueillir certaines informations sur le cluster DC/OS, notamment le nom et l’état des agents DC/OS.</span><span class="sxs-lookup"><span data-stu-id="b0466-120">Before you deploy containers to the DC/OS cluster, gather some information about the DC/OS cluster, such as the names and status of the DC/OS agents.</span></span> <span data-ttu-id="b0466-121">Pour ce faire, interrogez le point de terminaison `master/slaves` sur l’API REST DC/OS.</span><span class="sxs-lookup"><span data-stu-id="b0466-121">To do so, query the `master/slaves` endpoint of the DC/OS REST API.</span></span> <span data-ttu-id="b0466-122">Si tout se déroule correctement, la requête renvoie une liste d’agents DC/OS accompagnée de quelques-unes de leurs propriétés.</span><span class="sxs-lookup"><span data-stu-id="b0466-122">If everything goes well, the query returns a list of DC/OS agents and several properties for each.</span></span>

```bash
curl http://localhost/mesos/master/slaves
```

<span data-ttu-id="b0466-123">À présent, utilisez le point de terminaison `/apps` de Marathon pour vérifier les déploiements d’application actuels vers le cluster DC/OS.</span><span class="sxs-lookup"><span data-stu-id="b0466-123">Now, use the Marathon `/apps` endpoint to check for current application deployments to the DC/OS cluster.</span></span> <span data-ttu-id="b0466-124">S’il s’agit d’un nouveau cluster, un tableau vide s’affiche pour les applications.</span><span class="sxs-lookup"><span data-stu-id="b0466-124">If this is a new cluster, you see an empty array for apps.</span></span>

```bash
curl localhost/marathon/v2/apps

{"apps":[]}
```

## <a name="deploy-a-docker-formatted-container"></a><span data-ttu-id="b0466-125">Déployer un conteneur au format Docker</span><span class="sxs-lookup"><span data-stu-id="b0466-125">Deploy a Docker-formatted container</span></span>
<span data-ttu-id="b0466-126">Vous déployez les conteneurs au format Docker via l’API REST Marathon à l’aide d’un fichier JSON décrivant le déploiement souhaité.</span><span class="sxs-lookup"><span data-stu-id="b0466-126">You deploy Docker-formatted containers through the Marathon REST API by using a JSON file that describes the intended deployment.</span></span> <span data-ttu-id="b0466-127">L’exemple suivant déploie un conteneur Nginx vers un agent privé dans le cluster.</span><span class="sxs-lookup"><span data-stu-id="b0466-127">The following sample deploys an Nginx container to a private agent in the cluster.</span></span> 

```json
{
  "id": "nginx",
  "cpus": 0.1,
  "mem": 32.0,
  "instances": 1,
  "container": {
    "type": "DOCKER",
    "docker": {
      "image": "nginx",
      "network": "BRIDGE",
      "portMappings": [
        { "containerPort": 80, "servicePort": 9000, "protocol": "tcp" }
      ]
    }
  }
}
```

<span data-ttu-id="b0466-128">Pour déployer un conteneur au format Docker, stockez le fichier JSON dans un emplacement accessible.</span><span class="sxs-lookup"><span data-stu-id="b0466-128">To deploy a Docker-formatted container, store the JSON file in an accessible location.</span></span> <span data-ttu-id="b0466-129">Ensuite, exécutez la commande suivante pour déployer le conteneur.</span><span class="sxs-lookup"><span data-stu-id="b0466-129">Next, to deploy the container, run the following command.</span></span> <span data-ttu-id="b0466-130">Spécifiez le nom du fichier JSON (`marathon.json` dans cet exemple).</span><span class="sxs-lookup"><span data-stu-id="b0466-130">Specify the name of the JSON file (`marathon.json` in this example).</span></span>

```bash
curl -X POST http://localhost/marathon/v2/apps -d @marathon.json -H "Content-type: application/json"
```

<span data-ttu-id="b0466-131">Le résultat ressemble à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="b0466-131">The output is similar to the following:</span></span>

```json
{"version":"2015-11-20T18:59:00.494Z","deploymentId":"b12f8a73-f56a-4eb1-9375-4ac026d6cdec"}
```

<span data-ttu-id="b0466-132">À présent, si vous interrogez Marathon à propos des applications, cette nouvelle application apparaît dans la sortie.</span><span class="sxs-lookup"><span data-stu-id="b0466-132">Now, if you query Marathon for applications, this new application appears in the output.</span></span>

```bash
curl localhost/marathon/v2/apps
```

## <a name="reach-the-container"></a><span data-ttu-id="b0466-133">Atteindre le conteneur</span><span class="sxs-lookup"><span data-stu-id="b0466-133">Reach the container</span></span>

<span data-ttu-id="b0466-134">Vous pouvez vérifier que Nginx s’exécute dans un conteneur sur un des agents privés du cluster.</span><span class="sxs-lookup"><span data-stu-id="b0466-134">You can verify that the Nginx is running in a container on one of the private agents in the cluster.</span></span> <span data-ttu-id="b0466-135">Pour trouver l’hôte et le port sur lesquels le conteneur s’exécute, demandez à Marathon les tâches en cours d’exécution :</span><span class="sxs-lookup"><span data-stu-id="b0466-135">To find the host and port where the container is running, query Marathon for the running tasks:</span></span> 

```bash
curl localhost/marathon/v2/tasks
```

<span data-ttu-id="b0466-136">Recherchez la valeur de `host` dans la sortie (une adresse IP similaire à `10.32.0.x`) et la valeur de `ports`.</span><span class="sxs-lookup"><span data-stu-id="b0466-136">Find the value of `host` in the output (an IP address similar to `10.32.0.x`), and the value of `ports`.</span></span>


<span data-ttu-id="b0466-137">À présent, établissez une connexion au terminal SSH (pas une connexion par tunnel) au nom de domaine complet de gestion du cluster.</span><span class="sxs-lookup"><span data-stu-id="b0466-137">Now make an SSH terminal connection (not a tunneled connection) to the management FQDN of the cluster.</span></span> <span data-ttu-id="b0466-138">Une fois la connexion établie, effectuez la demande suivante, en remplaçant les valeurs correctes de `host` et `ports` :</span><span class="sxs-lookup"><span data-stu-id="b0466-138">Once connected, make the following request, substituting the correct values of `host` and `ports`:</span></span>

```bash
curl http://host:ports
```

<span data-ttu-id="b0466-139">Le résultat du serveur Nginx ressemble à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="b0466-139">The Nginx server output is similar to the following:</span></span>

![Nginx à partir d’un conteneur](./media/container-service-mesos-marathon-rest/nginx.png)




## <a name="scale-your-containers"></a><span data-ttu-id="b0466-141">Mettre vos conteneurs à l’échelle</span><span class="sxs-lookup"><span data-stu-id="b0466-141">Scale your containers</span></span>
<span data-ttu-id="b0466-142">Vous pouvez utiliser l’API Marathon pour diminuer ou augmenter la taille des déploiements des instances d’application.</span><span class="sxs-lookup"><span data-stu-id="b0466-142">You can use the Marathon API to scale out or scale in application deployments.</span></span> <span data-ttu-id="b0466-143">Dans l’exemple précédent, vous avez déployé une instance d’une application.</span><span class="sxs-lookup"><span data-stu-id="b0466-143">In the previous example, you deployed one instance of an application.</span></span> <span data-ttu-id="b0466-144">Nous allons augmenter la taille de déploiement pour obtenir trois instances d’une application.</span><span class="sxs-lookup"><span data-stu-id="b0466-144">Let's scale this out to three instances of an application.</span></span> <span data-ttu-id="b0466-145">Pour ce faire, créez un fichier JSON avec le texte JSON suivant et stockez-le dans un emplacement accessible.</span><span class="sxs-lookup"><span data-stu-id="b0466-145">To do so, create a JSON file by using the following JSON text, and store it in an accessible location.</span></span>

```json
{ "instances": 3 }
```

<span data-ttu-id="b0466-146">À partir de la connexion par tunnel, exécutez la commande suivante pour augmenter la taille des instances de l’application.</span><span class="sxs-lookup"><span data-stu-id="b0466-146">From your tunneled connection, run the following command to scale out the application.</span></span>

> [!NOTE]
> <span data-ttu-id="b0466-147">L’URI est http://localhost/marathon/v2/apps/, suivi de l’ID de l’application que vous souhaitez mettre à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="b0466-147">The URI is http://localhost/marathon/v2/apps/ followed by the ID of the application to scale.</span></span> <span data-ttu-id="b0466-148">Si vous utilisiez l’exemple Nginx fourni ici, l’URI serait http://localhost/marathon/v2/apps/nginx.</span><span class="sxs-lookup"><span data-stu-id="b0466-148">If you are using the Nginx sample that is provided here, the URI would be http://localhost/marathon/v2/apps/nginx.</span></span>
> 
> 

```bash
curl http://localhost/marathon/v2/apps/nginx -H "Content-type: application/json" -X PUT -d @scale.json
```

<span data-ttu-id="b0466-149">Pour finir, interrogez le point de terminaison Marathon sur les applications.</span><span class="sxs-lookup"><span data-stu-id="b0466-149">Finally, query the Marathon endpoint for applications.</span></span> <span data-ttu-id="b0466-150">Vous constatez qu’il existe désormais trois conteneurs Nginx.</span><span class="sxs-lookup"><span data-stu-id="b0466-150">You see that there are now three Nginx containers.</span></span>

```bash
curl localhost/marathon/v2/apps
```

## <a name="equivalent-powershell-commands"></a><span data-ttu-id="b0466-151">Commandes PowerShell équivalentes</span><span class="sxs-lookup"><span data-stu-id="b0466-151">Equivalent PowerShell commands</span></span>
<span data-ttu-id="b0466-152">Vous pouvez effectuer les mêmes opérations sur un système Windows à l’aide des commandes PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b0466-152">You can perform these same actions by using PowerShell commands on a Windows system.</span></span>

<span data-ttu-id="b0466-153">Pour collecter des informations sur le cluster DC/OS (par exemple, le nom et l’état de l’agent), exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="b0466-153">To gather information about the DC/OS cluster, such as agent names and agent status, run the following command:</span></span>

```powershell
Invoke-WebRequest -Uri http://localhost/mesos/master/slaves
```

<span data-ttu-id="b0466-154">Vous déployez les conteneurs au format Docker via Marathon à l’aide d’un fichier JSON décrivant le déploiement souhaité.</span><span class="sxs-lookup"><span data-stu-id="b0466-154">You deploy Docker-formatted containers through Marathon by using a JSON file that describes the intended deployment.</span></span> <span data-ttu-id="b0466-155">L’exemple ci-après déploie le conteneur Nginx en liant le port 80 de l’agent DC/OS au port 80 du conteneur.</span><span class="sxs-lookup"><span data-stu-id="b0466-155">The following sample deploys the Nginx container, binding port 80 of the DC/OS agent to port 80 of the container.</span></span>

```json
{
  "id": "nginx",
  "cpus": 0.1,
  "mem": 32.0,
  "instances": 1,
  "container": {
    "type": "DOCKER",
    "docker": {
      "image": "nginx",
      "network": "BRIDGE",
      "portMappings": [
        { "containerPort": 80, "servicePort": 9000, "protocol": "tcp" }
      ]
    }
  }
}
```

<span data-ttu-id="b0466-156">Pour déployer un conteneur au format Docker, stockez le fichier JSON dans un emplacement accessible.</span><span class="sxs-lookup"><span data-stu-id="b0466-156">To deploy a Docker-formatted container, store the JSON file in an accessible location.</span></span> <span data-ttu-id="b0466-157">Ensuite, exécutez la commande suivante pour déployer le conteneur.</span><span class="sxs-lookup"><span data-stu-id="b0466-157">Next, to deploy the container, run the following command.</span></span> <span data-ttu-id="b0466-158">Spécifiez le chemin d’accès au fichier JSON (`marathon.json` dans cet exemple).</span><span class="sxs-lookup"><span data-stu-id="b0466-158">Specify the path to the JSON file (`marathon.json` in this example).</span></span>

```powershell
Invoke-WebRequest -Method Post -Uri http://localhost/marathon/v2/apps -ContentType application/json -InFile 'c:\marathon.json'
```

<span data-ttu-id="b0466-159">Vous pouvez également utiliser l’API Marathon pour diminuer ou augmenter la taille des déploiements des instances d’application.</span><span class="sxs-lookup"><span data-stu-id="b0466-159">You can also use the Marathon API to scale out or scale in application deployments.</span></span> <span data-ttu-id="b0466-160">Dans l’exemple précédent, vous avez déployé une instance d’une application.</span><span class="sxs-lookup"><span data-stu-id="b0466-160">In the previous example, you deployed one instance of an application.</span></span> <span data-ttu-id="b0466-161">Nous allons augmenter la taille de déploiement pour obtenir trois instances d’une application.</span><span class="sxs-lookup"><span data-stu-id="b0466-161">Let's scale this out to three instances of an application.</span></span> <span data-ttu-id="b0466-162">Pour ce faire, créez un fichier JSON avec le texte JSON suivant et stockez-le dans un emplacement accessible.</span><span class="sxs-lookup"><span data-stu-id="b0466-162">To do so, create a JSON file by using the following JSON text, and store it in an accessible location.</span></span>

```json
{ "instances": 3 }
```

<span data-ttu-id="b0466-163">Exécutez la commande suivante pour augmenter la taille des instances de l’application :</span><span class="sxs-lookup"><span data-stu-id="b0466-163">Run the following command to scale out the application:</span></span>

> [!NOTE]
> <span data-ttu-id="b0466-164">L’URI est http://localhost/marathon/v2/apps/, suivi de l’ID de l’application que vous souhaitez mettre à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="b0466-164">The URI is http://localhost/marathon/v2/apps/ followed by the ID of the application to scale.</span></span> <span data-ttu-id="b0466-165">Si vous utilisiez l’exemple Nginx fourni ici, l’URI serait http://localhost/marathon/v2/apps/nginx.</span><span class="sxs-lookup"><span data-stu-id="b0466-165">If you are using the Nginx sample provided here, the URI would be http://localhost/marathon/v2/apps/nginx.</span></span>
> 
> 

```powershell
Invoke-WebRequest -Method Put -Uri http://localhost/marathon/v2/apps/nginx -ContentType application/json -InFile 'c:\scale.json'
```

## <a name="next-steps"></a><span data-ttu-id="b0466-166">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b0466-166">Next steps</span></span>
* [<span data-ttu-id="b0466-167">En savoir plus sur les points de terminaison HTTP Mesos</span><span class="sxs-lookup"><span data-stu-id="b0466-167">Read more about the Mesos HTTP endpoints</span></span>](http://mesos.apache.org/documentation/latest/endpoints/)
* [<span data-ttu-id="b0466-168">En savoir plus sur l’API REST Marathon</span><span class="sxs-lookup"><span data-stu-id="b0466-168">Read more about the Marathon REST API</span></span>](https://mesosphere.github.io/marathon/docs/rest-api.html)

