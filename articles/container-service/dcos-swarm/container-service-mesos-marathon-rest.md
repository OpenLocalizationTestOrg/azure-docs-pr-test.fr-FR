---
title: "cluster de contrôleur de domaine/système d’exploitation Azure aaaManage avec l’API REST Marathon | Documents Microsoft"
description: "Déployer le cluster de conteneurs tooan conteneur Service contrôleur de domaine/système d’exploitation Azure à l’aide de hello Marathon REST API."
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
ms.openlocfilehash: d926b9b90f5d4eda85a015d9ea0d96fea2c4b566
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="dcos-container-management-through-hello-marathon-rest-api"></a><span data-ttu-id="ab801-104">Gestion des conteneurs de contrôleur de domaine/système d’exploitation via l’API REST de Marathon de hello</span><span class="sxs-lookup"><span data-stu-id="ab801-104">DC/OS container management through hello Marathon REST API</span></span>
<span data-ttu-id="ab801-105">Contrôleur de domaine/système d’exploitation fournit un environnement de déploiement et de mise à l’échelle de charges de travail en cluster, tout en faisant abstraction du matériel sous-jacent de hello.</span><span class="sxs-lookup"><span data-stu-id="ab801-105">DC/OS provides an environment for deploying and scaling clustered workloads, while abstracting hello underlying hardware.</span></span> <span data-ttu-id="ab801-106">DC/OS sous-tend un framework qui gère la planification et l’exécution des charges de travail de calcul.</span><span class="sxs-lookup"><span data-stu-id="ab801-106">On top of DC/OS, there is a framework that manages scheduling and executing compute workloads.</span></span> <span data-ttu-id="ab801-107">Bien que les infrastructures sont disponibles pour nombreuses charges de travail courantes, ce document s’obtient à commencer la création et la mise à l’échelle des déploiements de conteneur à l’aide de hello Marathon REST API.</span><span class="sxs-lookup"><span data-stu-id="ab801-107">Although frameworks are available for many popular workloads, this document gets you started creating and scaling container deployments by using hello Marathon REST API.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="ab801-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="ab801-108">Prerequisites</span></span>

<span data-ttu-id="ab801-109">Avant d’étudier ces exemples, vous devez avoir un cluster DC/OS configuré dans Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="ab801-109">Before working through these examples, you need a DC/OS cluster that is configured in Azure Container Service.</span></span> <span data-ttu-id="ab801-110">Vous devez également le cluster de toothis toohave la connectivité à distance.</span><span class="sxs-lookup"><span data-stu-id="ab801-110">You also need toohave remote connectivity toothis cluster.</span></span> <span data-ttu-id="ab801-111">Pour plus d’informations sur ces éléments, consultez hello suivant des articles :</span><span class="sxs-lookup"><span data-stu-id="ab801-111">For more information on these items, see hello following articles:</span></span>

* [<span data-ttu-id="ab801-112">Déploiement d’un cluster Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="ab801-112">Deploying an Azure Container Service cluster</span></span>](container-service-deployment.md)
* [<span data-ttu-id="ab801-113">Connexion de cluster du Service de conteneur Azure tooan</span><span class="sxs-lookup"><span data-stu-id="ab801-113">Connecting tooan Azure Container Service cluster</span></span>](../container-service-connect.md)

## <a name="access-hello-dcos-apis"></a><span data-ttu-id="ab801-114">Hello d’accès aux API de contrôleur de domaine/système d’exploitation</span><span class="sxs-lookup"><span data-stu-id="ab801-114">Access hello DC/OS APIs</span></span>
<span data-ttu-id="ab801-115">Une fois que vous êtes cluster du Service de conteneur Azure toohello connecté, vous pouvez accéder hello contrôleur de domaine/système d’exploitation et les API REST associées via le port de http://localhost:local.</span><span class="sxs-lookup"><span data-stu-id="ab801-115">After you are connected toohello Azure Container Service cluster, you can access hello DC/OS and related REST APIs through http://localhost:local-port.</span></span> <span data-ttu-id="ab801-116">exemples de Hello dans ce document supposent que vous créez un tunnel sur le port 80.</span><span class="sxs-lookup"><span data-stu-id="ab801-116">hello examples in this document assume that you are tunneling on port 80.</span></span> <span data-ttu-id="ab801-117">Par exemple, les points de terminaison hello Marathon peuvent être atteint à l’URI commençant par `http://localhost/marathon/v2/`.</span><span class="sxs-lookup"><span data-stu-id="ab801-117">For example, hello Marathon endpoints can be reached at URIs beginning with `http://localhost/marathon/v2/`.</span></span> 

<span data-ttu-id="ab801-118">Pour plus d’informations sur hello diverses API, consultez la documentation mésosphère hello hello [Marathon API](https://mesosphere.github.io/marathon/docs/rest-api.html) et [Chronos API](https://mesos.github.io/chronos/docs/api.html)et la documentation d’Apache pour hello [API du Planificateur de Mesos ](http://mesos.apache.org/documentation/latest/scheduler-http-api/).</span><span class="sxs-lookup"><span data-stu-id="ab801-118">For more information on hello various APIs, see hello Mesosphere documentation for hello [Marathon API](https://mesosphere.github.io/marathon/docs/rest-api.html) and the [Chronos API](https://mesos.github.io/chronos/docs/api.html), and the Apache documentation for hello [Mesos Scheduler API](http://mesos.apache.org/documentation/latest/scheduler-http-api/).</span></span>

## <a name="gather-information-from-dcos-and-marathon"></a><span data-ttu-id="ab801-119">Collecte d’informations à partir de DC/OS et de Marathon</span><span class="sxs-lookup"><span data-stu-id="ab801-119">Gather information from DC/OS and Marathon</span></span>
<span data-ttu-id="ab801-120">Avant de déployer des clusters de contrôleur de domaine/système d’exploitation de conteneurs toohello, rassembler des informations sur le cluster de contrôleur de domaine/système d’exploitation hello, telles que les noms de hello et l’état des agents de contrôleur de domaine/système d’exploitation hello.</span><span class="sxs-lookup"><span data-stu-id="ab801-120">Before you deploy containers toohello DC/OS cluster, gather some information about hello DC/OS cluster, such as hello names and status of hello DC/OS agents.</span></span> <span data-ttu-id="ab801-121">toodo requête donc hello `master/slaves` point de terminaison de hello API REST de contrôleur de domaine/système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="ab801-121">toodo so, query hello `master/slaves` endpoint of hello DC/OS REST API.</span></span> <span data-ttu-id="ab801-122">Si tout se passe bien, requête de hello retourne une liste des agents de contrôleur de domaine/système d’exploitation et de plusieurs propriétés pour chacun.</span><span class="sxs-lookup"><span data-stu-id="ab801-122">If everything goes well, hello query returns a list of DC/OS agents and several properties for each.</span></span>

```bash
curl http://localhost/mesos/master/slaves
```

<span data-ttu-id="ab801-123">À présent, utiliser hello Marathon `/apps` toocheck de point de terminaison de cluster du contrôleur de domaine/système d’exploitation toohello de déploiements application actuel.</span><span class="sxs-lookup"><span data-stu-id="ab801-123">Now, use hello Marathon `/apps` endpoint toocheck for current application deployments toohello DC/OS cluster.</span></span> <span data-ttu-id="ab801-124">S’il s’agit d’un nouveau cluster, un tableau vide s’affiche pour les applications.</span><span class="sxs-lookup"><span data-stu-id="ab801-124">If this is a new cluster, you see an empty array for apps.</span></span>

```bash
curl localhost/marathon/v2/apps

{"apps":[]}
```

## <a name="deploy-a-docker-formatted-container"></a><span data-ttu-id="ab801-125">Déployer un conteneur au format Docker</span><span class="sxs-lookup"><span data-stu-id="ab801-125">Deploy a Docker-formatted container</span></span>
<span data-ttu-id="ab801-126">Vous déployez au format Docker de conteneurs via hello Marathon REST API à l’aide d’un fichier JSON qui décrit le déploiement de hello destiné.</span><span class="sxs-lookup"><span data-stu-id="ab801-126">You deploy Docker-formatted containers through hello Marathon REST API by using a JSON file that describes hello intended deployment.</span></span> <span data-ttu-id="ab801-127">Hello exemple suivant déploie un agent Nginx conteneur tooa privé dans un cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="ab801-127">hello following sample deploys an Nginx container tooa private agent in hello cluster.</span></span> 

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

<span data-ttu-id="ab801-128">toodeploy un conteneur au format Docker, stocker le fichier JSON de hello dans un emplacement accessible.</span><span class="sxs-lookup"><span data-stu-id="ab801-128">toodeploy a Docker-formatted container, store hello JSON file in an accessible location.</span></span> <span data-ttu-id="ab801-129">Ensuite, toodeploy hello conteneur exécuter hello commande suivante.</span><span class="sxs-lookup"><span data-stu-id="ab801-129">Next, toodeploy hello container, run hello following command.</span></span> <span data-ttu-id="ab801-130">Spécifiez le nom hello du fichier JSON de hello (`marathon.json` dans cet exemple).</span><span class="sxs-lookup"><span data-stu-id="ab801-130">Specify hello name of hello JSON file (`marathon.json` in this example).</span></span>

```bash
curl -X POST http://localhost/marathon/v2/apps -d @marathon.json -H "Content-type: application/json"
```

<span data-ttu-id="ab801-131">sortie de Hello est similaire toohello suivantes :</span><span class="sxs-lookup"><span data-stu-id="ab801-131">hello output is similar toohello following:</span></span>

```json
{"version":"2015-11-20T18:59:00.494Z","deploymentId":"b12f8a73-f56a-4eb1-9375-4ac026d6cdec"}
```

<span data-ttu-id="ab801-132">Maintenant, si vous interrogez Marathon pour les applications, cette nouvelle application s’affiche dans la sortie de hello.</span><span class="sxs-lookup"><span data-stu-id="ab801-132">Now, if you query Marathon for applications, this new application appears in hello output.</span></span>

```bash
curl localhost/marathon/v2/apps
```

## <a name="reach-hello-container"></a><span data-ttu-id="ab801-133">Atteindre le conteneur de hello</span><span class="sxs-lookup"><span data-stu-id="ab801-133">Reach hello container</span></span>

<span data-ttu-id="ab801-134">Vous pouvez vérifier que hello que nginx est en cours d’exécution dans un conteneur sur l’un des agents de hello privé dans un cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="ab801-134">You can verify that hello Nginx is running in a container on one of hello private agents in hello cluster.</span></span> <span data-ttu-id="ab801-135">hôte de hello toofind et port où le conteneur de hello est en cours d’exécution, requête Marathon pourquoi les tâches en cours d’exécution :</span><span class="sxs-lookup"><span data-stu-id="ab801-135">toofind hello host and port where hello container is running, query Marathon for hello running tasks:</span></span> 

```bash
curl localhost/marathon/v2/tasks
```

<span data-ttu-id="ab801-136">Rechercher la valeur hello `host` dans la sortie de hello (une adresse IP similaire trop`10.32.0.x`) et la valeur hello de `ports`.</span><span class="sxs-lookup"><span data-stu-id="ab801-136">Find hello value of `host` in hello output (an IP address similar too`10.32.0.x`), and hello value of `ports`.</span></span>


<span data-ttu-id="ab801-137">Maintenant vous une gestion toohello des connexions Terminal Server (et non pas une connexion tunnel) SSH nom de domaine complet du cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="ab801-137">Now make an SSH terminal connection (not a tunneled connection) toohello management FQDN of hello cluster.</span></span> <span data-ttu-id="ab801-138">Une fois connecté, rendre hello demande, en remplaçant les valeurs correctes de hello de `host` et `ports`:</span><span class="sxs-lookup"><span data-stu-id="ab801-138">Once connected, make hello following request, substituting hello correct values of `host` and `ports`:</span></span>

```bash
curl http://host:ports
```

<span data-ttu-id="ab801-139">Hello Nginx résultat du serveur est semblable toohello suivantes :</span><span class="sxs-lookup"><span data-stu-id="ab801-139">hello Nginx server output is similar toohello following:</span></span>

![Nginx à partir d’un conteneur](./media/container-service-mesos-marathon-rest/nginx.png)




## <a name="scale-your-containers"></a><span data-ttu-id="ab801-141">Mettre vos conteneurs à l’échelle</span><span class="sxs-lookup"><span data-stu-id="ab801-141">Scale your containers</span></span>
<span data-ttu-id="ab801-142">Vous pouvez utiliser tooscale de Marathon API hello out ou d’échelle dans les déploiements d’applications.</span><span class="sxs-lookup"><span data-stu-id="ab801-142">You can use hello Marathon API tooscale out or scale in application deployments.</span></span> <span data-ttu-id="ab801-143">Dans l’exemple précédent de hello, vous avez déployé une instance d’une application.</span><span class="sxs-lookup"><span data-stu-id="ab801-143">In hello previous example, you deployed one instance of an application.</span></span> <span data-ttu-id="ab801-144">Nous allons mettre à l’échelle cela toothree des instances d’une application.</span><span class="sxs-lookup"><span data-stu-id="ab801-144">Let's scale this out toothree instances of an application.</span></span> <span data-ttu-id="ab801-145">toodo par conséquent, créer un fichier JSON à l’aide de hello suivant le texte JSON et stockez-le dans un emplacement accessible.</span><span class="sxs-lookup"><span data-stu-id="ab801-145">toodo so, create a JSON file by using hello following JSON text, and store it in an accessible location.</span></span>

```json
{ "instances": 3 }
```

<span data-ttu-id="ab801-146">À partir de votre connexion tunnel, exécutez hello suivant tooscale de commande d’application hello.</span><span class="sxs-lookup"><span data-stu-id="ab801-146">From your tunneled connection, run hello following command tooscale out hello application.</span></span>

> [!NOTE]
> <span data-ttu-id="ab801-147">Hello URI est http://localhost/marathon/v2/apps/ suivi par ID hello de hello application tooscale.</span><span class="sxs-lookup"><span data-stu-id="ab801-147">hello URI is http://localhost/marathon/v2/apps/ followed by hello ID of hello application tooscale.</span></span> <span data-ttu-id="ab801-148">Si vous utilisez l’exemple hello Nginx fourni ici, hello URI serait http://localhost/marathon/v2/apps/nginx.</span><span class="sxs-lookup"><span data-stu-id="ab801-148">If you are using hello Nginx sample that is provided here, hello URI would be http://localhost/marathon/v2/apps/nginx.</span></span>
> 
> 

```bash
curl http://localhost/marathon/v2/apps/nginx -H "Content-type: application/json" -X PUT -d @scale.json
```

<span data-ttu-id="ab801-149">Enfin, requête de point de terminaison de Marathon hello pour les applications.</span><span class="sxs-lookup"><span data-stu-id="ab801-149">Finally, query hello Marathon endpoint for applications.</span></span> <span data-ttu-id="ab801-150">Vous constatez qu’il existe désormais trois conteneurs Nginx.</span><span class="sxs-lookup"><span data-stu-id="ab801-150">You see that there are now three Nginx containers.</span></span>

```bash
curl localhost/marathon/v2/apps
```

## <a name="equivalent-powershell-commands"></a><span data-ttu-id="ab801-151">Commandes PowerShell équivalentes</span><span class="sxs-lookup"><span data-stu-id="ab801-151">Equivalent PowerShell commands</span></span>
<span data-ttu-id="ab801-152">Vous pouvez effectuer les mêmes opérations sur un système Windows à l’aide des commandes PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ab801-152">You can perform these same actions by using PowerShell commands on a Windows system.</span></span>

<span data-ttu-id="ab801-153">toogather plus d’informations sur le cluster de contrôleur de domaine/système d’exploitation hello, tels que les noms d’agent et l’état de l’agent, exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="ab801-153">toogather information about hello DC/OS cluster, such as agent names and agent status, run hello following command:</span></span>

```powershell
Invoke-WebRequest -Uri http://localhost/mesos/master/slaves
```

<span data-ttu-id="ab801-154">Vous déployez des mises en forme de Docker de conteneurs via Marathon à l’aide d’un fichier JSON qui décrit le déploiement de hello destinée.</span><span class="sxs-lookup"><span data-stu-id="ab801-154">You deploy Docker-formatted containers through Marathon by using a JSON file that describes hello intended deployment.</span></span> <span data-ttu-id="ab801-155">Hello exemple suivant déploie conteneur Nginx de hello, lier le port 80 de hello DC/OS agent tooport 80 du conteneur de hello.</span><span class="sxs-lookup"><span data-stu-id="ab801-155">hello following sample deploys hello Nginx container, binding port 80 of hello DC/OS agent tooport 80 of hello container.</span></span>

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

<span data-ttu-id="ab801-156">toodeploy un conteneur au format Docker, stocker le fichier JSON de hello dans un emplacement accessible.</span><span class="sxs-lookup"><span data-stu-id="ab801-156">toodeploy a Docker-formatted container, store hello JSON file in an accessible location.</span></span> <span data-ttu-id="ab801-157">Ensuite, toodeploy hello conteneur exécuter hello commande suivante.</span><span class="sxs-lookup"><span data-stu-id="ab801-157">Next, toodeploy hello container, run hello following command.</span></span> <span data-ttu-id="ab801-158">Spécifier le fichier JSON de hello chemin d’accès toohello (`marathon.json` dans cet exemple).</span><span class="sxs-lookup"><span data-stu-id="ab801-158">Specify hello path toohello JSON file (`marathon.json` in this example).</span></span>

```powershell
Invoke-WebRequest -Method Post -Uri http://localhost/marathon/v2/apps -ContentType application/json -InFile 'c:\marathon.json'
```

<span data-ttu-id="ab801-159">Vous pouvez également utiliser tooscale de Marathon API hello out ou d’échelle dans les déploiements d’applications.</span><span class="sxs-lookup"><span data-stu-id="ab801-159">You can also use hello Marathon API tooscale out or scale in application deployments.</span></span> <span data-ttu-id="ab801-160">Dans l’exemple précédent de hello, vous avez déployé une instance d’une application.</span><span class="sxs-lookup"><span data-stu-id="ab801-160">In hello previous example, you deployed one instance of an application.</span></span> <span data-ttu-id="ab801-161">Nous allons mettre à l’échelle cela toothree des instances d’une application.</span><span class="sxs-lookup"><span data-stu-id="ab801-161">Let's scale this out toothree instances of an application.</span></span> <span data-ttu-id="ab801-162">toodo par conséquent, créer un fichier JSON à l’aide de hello suivant le texte JSON et stockez-le dans un emplacement accessible.</span><span class="sxs-lookup"><span data-stu-id="ab801-162">toodo so, create a JSON file by using hello following JSON text, and store it in an accessible location.</span></span>

```json
{ "instances": 3 }
```

<span data-ttu-id="ab801-163">Exécutez hello suivant tooscale de commande d’application hello :</span><span class="sxs-lookup"><span data-stu-id="ab801-163">Run hello following command tooscale out hello application:</span></span>

> [!NOTE]
> <span data-ttu-id="ab801-164">Hello URI est http://localhost/marathon/v2/apps/ suivi par ID hello de hello application tooscale.</span><span class="sxs-lookup"><span data-stu-id="ab801-164">hello URI is http://localhost/marathon/v2/apps/ followed by hello ID of hello application tooscale.</span></span> <span data-ttu-id="ab801-165">Si vous utilisez hello Nginx exemple fourni ici, hello URI serait http://localhost/marathon/v2/apps/nginx.</span><span class="sxs-lookup"><span data-stu-id="ab801-165">If you are using hello Nginx sample provided here, hello URI would be http://localhost/marathon/v2/apps/nginx.</span></span>
> 
> 

```powershell
Invoke-WebRequest -Method Put -Uri http://localhost/marathon/v2/apps/nginx -ContentType application/json -InFile 'c:\scale.json'
```

## <a name="next-steps"></a><span data-ttu-id="ab801-166">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ab801-166">Next steps</span></span>
* [<span data-ttu-id="ab801-167">En savoir plus sur les points de terminaison hello Mesos HTTP</span><span class="sxs-lookup"><span data-stu-id="ab801-167">Read more about hello Mesos HTTP endpoints</span></span>](http://mesos.apache.org/documentation/latest/endpoints/)
* [<span data-ttu-id="ab801-168">En savoir plus sur l’API REST de Marathon de hello</span><span class="sxs-lookup"><span data-stu-id="ab801-168">Read more about hello Marathon REST API</span></span>](https://mesosphere.github.io/marathon/docs/rest-api.html)

