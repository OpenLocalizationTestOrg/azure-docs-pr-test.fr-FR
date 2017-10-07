---
title: "cluster de contrôleur de domaine/système d’exploitation Azure aaaManage avec une interface utilisateur Marathon | Documents Microsoft"
description: "Déployer le service de cluster du Service de conteneur Azure conteneurs tooan à l’aide de l’interface utilisateur web de Marathon hello."
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Docker, conteneurs, micro-services, Mesos, Azure
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/04/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: a90180e1b4763e6d2ddfa699ed4b7269f209f728
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-an-azure-container-service-dcos-cluster-through-hello-marathon-web-ui"></a><span data-ttu-id="07b2f-104">Gérer un cluster Azure conteneur Service contrôleur de domaine/système d’exploitation via l’interface utilisateur web de Marathon hello</span><span class="sxs-lookup"><span data-stu-id="07b2f-104">Manage an Azure Container Service DC/OS cluster through hello Marathon web UI</span></span>
<span data-ttu-id="07b2f-105">Contrôleur de domaine/système d’exploitation fournit un environnement de déploiement et de mise à l’échelle de charges de travail en cluster, tout en faisant abstraction du matériel sous-jacent de hello.</span><span class="sxs-lookup"><span data-stu-id="07b2f-105">DC/OS provides an environment for deploying and scaling clustered workloads, while abstracting hello underlying hardware.</span></span> <span data-ttu-id="07b2f-106">DC/OS sous-tend un framework qui gère la planification et l’exécution des charges de travail de calcul.</span><span class="sxs-lookup"><span data-stu-id="07b2f-106">On top of DC/OS, there is a framework that manages scheduling and executing compute workloads.</span></span>

<span data-ttu-id="07b2f-107">Alors que les infrastructures sont disponibles pour nombreuses charges de travail courantes, ce document décrit comment tooget démarrer le déploiement de conteneurs avec Marathon.</span><span class="sxs-lookup"><span data-stu-id="07b2f-107">While frameworks are available for many popular workloads, this document describes how tooget started deploying containers with Marathon.</span></span> 


## <a name="prerequisites"></a><span data-ttu-id="07b2f-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="07b2f-108">Prerequisites</span></span>
<span data-ttu-id="07b2f-109">Avant d’étudier ces exemples, vous devez avoir un cluster DC/OS configuré dans Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="07b2f-109">Before working through these examples, you need a DC/OS cluster that is configured in Azure Container Service.</span></span> <span data-ttu-id="07b2f-110">Vous devez également le cluster de toothis toohave la connectivité à distance.</span><span class="sxs-lookup"><span data-stu-id="07b2f-110">You also need toohave remote connectivity toothis cluster.</span></span> <span data-ttu-id="07b2f-111">Pour plus d’informations sur ces éléments, consultez hello suivant des articles :</span><span class="sxs-lookup"><span data-stu-id="07b2f-111">For more information on these items, see hello following articles:</span></span>

* [<span data-ttu-id="07b2f-112">Déploiement d’un cluster Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="07b2f-112">Deploy an Azure Container Service cluster</span></span>](container-service-deployment.md)
* [<span data-ttu-id="07b2f-113">Connecter le cluster du Service de conteneur Azure tooan</span><span class="sxs-lookup"><span data-stu-id="07b2f-113">Connect tooan Azure Container Service cluster</span></span>](../container-service-connect.md)

> [!NOTE]
> <span data-ttu-id="07b2f-114">Cet article suppose que vous créez un tunnel cluster du contrôleur de domaine/système d’exploitation toohello via les ports locaux 80.</span><span class="sxs-lookup"><span data-stu-id="07b2f-114">This article assumes you are tunneling toohello DC/OS cluster through your local port 80.</span></span>
>

## <a name="explore-hello-dcos-ui"></a><span data-ttu-id="07b2f-115">Explorer hello l’interface utilisateur du contrôleur de domaine/système d’exploitation</span><span class="sxs-lookup"><span data-stu-id="07b2f-115">Explore hello DC/OS UI</span></span>
<span data-ttu-id="07b2f-116">Avec un tunnel SSH (Secure Shell) [établie](../container-service-connect.md), parcourir toohttp://localhost/.</span><span class="sxs-lookup"><span data-stu-id="07b2f-116">With a Secure Shell (SSH) tunnel [established](../container-service-connect.md), browse toohttp://localhost/.</span></span> <span data-ttu-id="07b2f-117">Cela charge l’interface utilisateur web de contrôleur de domaine/système d’exploitation hello et affiche des informations sur le cluster hello, telles que les ressources utilisées, les agents actifs et les services en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="07b2f-117">This loads hello DC/OS web UI and shows information about hello cluster, such as used resources, active agents, and running services.</span></span>

![IU DC/OS](./media/container-service-mesos-marathon-ui/dcos2.png)

## <a name="explore-hello-marathon-ui"></a><span data-ttu-id="07b2f-119">Explorer hello Marathon UI</span><span class="sxs-lookup"><span data-stu-id="07b2f-119">Explore hello Marathon UI</span></span>
<span data-ttu-id="07b2f-120">toosee hello Marathon UI, accédez à toohttp://localhost/marathon.</span><span class="sxs-lookup"><span data-stu-id="07b2f-120">toosee hello Marathon UI, browse toohttp://localhost/marathon.</span></span> <span data-ttu-id="07b2f-121">À partir de cet écran, vous pouvez démarrer un nouveau conteneur ou une autre application sur le cluster du Service de conteneur Azure DC/OS hello.</span><span class="sxs-lookup"><span data-stu-id="07b2f-121">From this screen, you can start a new container or another application on hello Azure Container Service DC/OS cluster.</span></span> <span data-ttu-id="07b2f-122">Vous pouvez également voir des informations sur les conteneurs et les applications en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="07b2f-122">You can also see information about running containers and applications.</span></span>  

![IU Marathon](./media/container-service-mesos-marathon-ui/dcos3.png)

## <a name="deploy-a-docker-formatted-container"></a><span data-ttu-id="07b2f-124">Déployer un conteneur au format Docker</span><span class="sxs-lookup"><span data-stu-id="07b2f-124">Deploy a Docker-formatted container</span></span>
<span data-ttu-id="07b2f-125">toodeploy un nouveau conteneur à l’aide de Marathon, cliquez sur **créer une Application**, puis entrez hello informations suivantes dans les onglets de formulaire hello :</span><span class="sxs-lookup"><span data-stu-id="07b2f-125">toodeploy a new container by using Marathon, click **Create Application**, and enter hello following information into hello form tabs:</span></span>

| <span data-ttu-id="07b2f-126">Champ</span><span class="sxs-lookup"><span data-stu-id="07b2f-126">Field</span></span> | <span data-ttu-id="07b2f-127">Valeur</span><span class="sxs-lookup"><span data-stu-id="07b2f-127">Value</span></span> |
| --- | --- |
| <span data-ttu-id="07b2f-128">ID</span><span class="sxs-lookup"><span data-stu-id="07b2f-128">ID</span></span> |<span data-ttu-id="07b2f-129">nginx</span><span class="sxs-lookup"><span data-stu-id="07b2f-129">nginx</span></span> |
| <span data-ttu-id="07b2f-130">Mémoire</span><span class="sxs-lookup"><span data-stu-id="07b2f-130">Memory</span></span> | <span data-ttu-id="07b2f-131">32</span><span class="sxs-lookup"><span data-stu-id="07b2f-131">32</span></span> |
| <span data-ttu-id="07b2f-132">Image</span><span class="sxs-lookup"><span data-stu-id="07b2f-132">Image</span></span> |<span data-ttu-id="07b2f-133">nginx</span><span class="sxs-lookup"><span data-stu-id="07b2f-133">nginx</span></span> |
| <span data-ttu-id="07b2f-134">Réseau</span><span class="sxs-lookup"><span data-stu-id="07b2f-134">Network</span></span> |<span data-ttu-id="07b2f-135">Relié par un pont</span><span class="sxs-lookup"><span data-stu-id="07b2f-135">Bridged</span></span> |
| <span data-ttu-id="07b2f-136">Port de l’hôte</span><span class="sxs-lookup"><span data-stu-id="07b2f-136">Host Port</span></span> |<span data-ttu-id="07b2f-137">80</span><span class="sxs-lookup"><span data-stu-id="07b2f-137">80</span></span> |
| <span data-ttu-id="07b2f-138">Protocole</span><span class="sxs-lookup"><span data-stu-id="07b2f-138">Protocol</span></span> |<span data-ttu-id="07b2f-139">TCP</span><span class="sxs-lookup"><span data-stu-id="07b2f-139">TCP</span></span> |

![Nouvelle interface utilisateur d’application : général](./media/container-service-mesos-marathon-ui/dcos4.png)

![Nouvelle interface utilisateur d’application : conteneur Docker](./media/container-service-mesos-marathon-ui/dcos5.png)

![Nouvelle interface utilisateur d’application : détection de service et de ports](./media/container-service-mesos-marathon-ui/dcos6.png)

<span data-ttu-id="07b2f-143">Si vous souhaitez toostatically mappe hello port du conteneur tooa le port sur l’agent de hello, vous devez toouse en Mode de JSON.</span><span class="sxs-lookup"><span data-stu-id="07b2f-143">If you want toostatically map hello container port tooa port on hello agent, you need toouse JSON Mode.</span></span> <span data-ttu-id="07b2f-144">toodo basculer, Assistant de nouvelle Application hello trop**JSON Mode** à l’aide de bascule de hello.</span><span class="sxs-lookup"><span data-stu-id="07b2f-144">toodo so, switch hello New Application wizard too**JSON Mode** by using hello toggle.</span></span> <span data-ttu-id="07b2f-145">Puis entrez hello suivant paramètre sous hello `portMappings` section hello de définition d’application.</span><span class="sxs-lookup"><span data-stu-id="07b2f-145">Then enter hello following setting under hello `portMappings` section of hello application definition.</span></span> <span data-ttu-id="07b2f-146">Cet exemple lie le port 80 de hello conteneur tooport 80 de l’agent du contrôleur de domaine/système d’exploitation hello.</span><span class="sxs-lookup"><span data-stu-id="07b2f-146">This example binds port 80 of hello container tooport 80 of hello DC/OS agent.</span></span> <span data-ttu-id="07b2f-147">Vous pouvez basculer l’Assistant hors du mode JSON après avoir apporté cette modification.</span><span class="sxs-lookup"><span data-stu-id="07b2f-147">You can switch this wizard out of JSON Mode after you make this change.</span></span>

```none
"hostPort": 80,
```

![Nouvelle interface utilisateur d’application : exemple de port 80](./media/container-service-mesos-marathon-ui/dcos13.png)

<span data-ttu-id="07b2f-149">Si vous souhaitez que les contrôles d’intégrité de tooenable, définir un chemin d’accès sur hello **contrôles d’intégrité** onglet.</span><span class="sxs-lookup"><span data-stu-id="07b2f-149">If you want tooenable health checks, set a path on hello **Health Checks** tab.</span></span>

![Interface utilisateur de nouvelle application -- contrôles d’intégrité](./media/container-service-mesos-marathon-ui/dcos_healthcheck.png)

<span data-ttu-id="07b2f-151">cluster de contrôleur de domaine/système d’exploitation Hello est déployé avec un ensemble d’agents privés et publics.</span><span class="sxs-lookup"><span data-stu-id="07b2f-151">hello DC/OS cluster is deployed with set of private and public agents.</span></span> <span data-ttu-id="07b2f-152">Pour hello cluster toobe tooaccess en mesure d’applications des hello Internet, vous avez besoin d’un agent public de toodeploy hello applications tooa.</span><span class="sxs-lookup"><span data-stu-id="07b2f-152">For hello cluster toobe able tooaccess applications from hello Internet, you need toodeploy hello applications tooa public agent.</span></span> <span data-ttu-id="07b2f-153">toodo, sélectionnez hello **facultatif** onglet de l’Assistant de nouvelle Application hello et entrez **slave_public** pour hello **accepté les rôles de ressources**.</span><span class="sxs-lookup"><span data-stu-id="07b2f-153">toodo so, select hello **Optional** tab of hello New Application wizard and enter **slave_public** for hello **Accepted Resource Roles**.</span></span>

<span data-ttu-id="07b2f-154">Cliquez ensuite sur **Créer une application**.</span><span class="sxs-lookup"><span data-stu-id="07b2f-154">Then click **Create Application**.</span></span>

![Nouvelle interface utilisateur d’application : paramètre de l’agent public](./media/container-service-mesos-marathon-ui/dcos14.png)

<span data-ttu-id="07b2f-156">Sur la page principale de Marathon hello, vous pouvez voir l’état du déploiement hello pour le conteneur de hello.</span><span class="sxs-lookup"><span data-stu-id="07b2f-156">Back on hello Marathon main page, you can see hello deployment status for hello container.</span></span> <span data-ttu-id="07b2f-157">Initialement, vous voyez l’état **Déploiement**.</span><span class="sxs-lookup"><span data-stu-id="07b2f-157">Initially you see a status of **Deploying**.</span></span> <span data-ttu-id="07b2f-158">Après un déploiement réussi, hello les changements d’état trop**en cours d’exécution**.</span><span class="sxs-lookup"><span data-stu-id="07b2f-158">After a successful deployment, hello status changes too**Running**.</span></span>

![Interface utilisateur de la page principale de Marathon : état du déploiement du conteneur](./media/container-service-mesos-marathon-ui/dcos7.png)

<span data-ttu-id="07b2f-160">Lorsque vous basculez web de contrôleur de domaine/système d’exploitation précédent toohello UI (http://localhost/), vous consultez qu’une tâche (dans ce cas, un conteneur au format Docker) s’exécute sur le cluster de contrôleur de domaine/système d’exploitation hello.</span><span class="sxs-lookup"><span data-stu-id="07b2f-160">When you switch back toohello DC/OS web UI (http://localhost/), you see that a task (in this case, a Docker-formatted container) is running on hello DC/OS cluster.</span></span>

![Contrôleur de domaine/système d’exploitation l’interface utilisateur web--tâche en cours d’exécution sur le cluster de hello](./media/container-service-mesos-marathon-ui/dcos8.png)

<span data-ttu-id="07b2f-162">nœud de cluster toosee hello hello tâche est en cours d’exécution, cliquez sur hello **nœuds** onglet.</span><span class="sxs-lookup"><span data-stu-id="07b2f-162">toosee hello cluster node that hello task is running on, click hello **Nodes** tab.</span></span>

![IU web DC/OS : nœud du cluster de tâche](./media/container-service-mesos-marathon-ui/dcos9.png)

## <a name="reach-hello-container"></a><span data-ttu-id="07b2f-164">Atteindre le conteneur de hello</span><span class="sxs-lookup"><span data-stu-id="07b2f-164">Reach hello container</span></span>

<span data-ttu-id="07b2f-165">Dans cet exemple, application hello est en cours d’exécution sur un nœud de l’agent public.</span><span class="sxs-lookup"><span data-stu-id="07b2f-165">In this example, hello application is running on a public agent node.</span></span> <span data-ttu-id="07b2f-166">Vous atteignez application hello hello internet en parcourant toohello agent nom de domaine complet du cluster de hello : `http://[DNSPREFIX]agents.[REGION].cloudapp.azure.com`, où :</span><span class="sxs-lookup"><span data-stu-id="07b2f-166">You reach hello application from hello internet by browsing toohello agent FQDN of hello cluster: `http://[DNSPREFIX]agents.[REGION].cloudapp.azure.com`, where:</span></span>

* <span data-ttu-id="07b2f-167">**DNSPREFIX** est le préfixe du DNS hello que vous avez fourni lors du déploiement de cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="07b2f-167">**DNSPREFIX** is hello DNS prefix that you provided when you deployed hello cluster.</span></span>
* <span data-ttu-id="07b2f-168">**RÉGION** est la région de hello dans lequel se trouve votre groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="07b2f-168">**REGION** is hello region in which your resource group is located.</span></span>

    ![Nginx à partir d’Internet](./media/container-service-mesos-marathon-ui/nginx.png)


## <a name="next-steps"></a><span data-ttu-id="07b2f-170">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="07b2f-170">Next steps</span></span>
* [<span data-ttu-id="07b2f-171">Travailler avec le contrôleur de domaine/système d’exploitation et hello Marathon API</span><span class="sxs-lookup"><span data-stu-id="07b2f-171">Work with DC/OS and hello Marathon API</span></span>](container-service-mesos-marathon-rest.md)

* <span data-ttu-id="07b2f-172">Présentation approfondie sur hello Service de conteneur Azure avec Mesos</span><span class="sxs-lookup"><span data-stu-id="07b2f-172">Deep dive on hello Azure Container Service with Mesos</span></span>

    > [!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON203/player]
    > 
