---
title: didacticiel de Service de conteneur aaaAzure - moniteur Kubernetes | Documents Microsoft
description: "Didacticiel Azure Container Service - Surveiller Kubernetes à l’aide de Microsoft Operations Management Suite (OMS)"
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Docker, Containers, Micro-services, Kubernetes, Azure
ms.assetid: 
ms.service: container-service
ms.devlang: aurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: 54fa789453768529deaf25d7575e5b21d0e41882
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-a-kubernetes-cluster-with-operations-management-suite"></a><span data-ttu-id="12e3c-104">Surveiller un cluster Kubernetes à l’aide d’Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="12e3c-104">Monitor a Kubernetes cluster with Operations Management Suite</span></span>

<span data-ttu-id="12e3c-105">La surveillance de votre cluster Kubernetes et des conteneurs est cruciale, particulièrement lorsque vous gérez un cluster de production à grande échelle avec plusieurs applications.</span><span class="sxs-lookup"><span data-stu-id="12e3c-105">Monitoring your Kubernetes cluster and containers is critical, especially when you manage a production cluster at scale with multiple apps.</span></span> 

<span data-ttu-id="12e3c-106">Vous pouvez tirer parti de plusieurs solutions de surveillance Kubernetes, à partir de Microsoft ou d’autres fournisseurs.</span><span class="sxs-lookup"><span data-stu-id="12e3c-106">You can take advantage of several Kubernetes monitoring solutions, either from Microsoft or other providers.</span></span> <span data-ttu-id="12e3c-107">Dans ce didacticiel, vous surveillez votre cluster Kubernetes à l’aide de solutions de conteneurs hello dans [Operations Management Suite](../../operations-management-suite/operations-management-suite-overview.md), solution de gestion informatique en nuage de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="12e3c-107">In this tutorial, you monitor your Kubernetes cluster by using hello Containers solution in [Operations Management Suite](../../operations-management-suite/operations-management-suite-overview.md), Microsoft's cloud-based IT management solution.</span></span> <span data-ttu-id="12e3c-108">(hello solution de conteneurs d’OMS est en version préliminaire.)</span><span class="sxs-lookup"><span data-stu-id="12e3c-108">(hello OMS Containers solution is in preview.)</span></span>

<span data-ttu-id="12e3c-109">Ce didacticiel, partie 7 sept et couvre hello tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="12e3c-109">This tutorial, part seven of seven, covers hello following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="12e3c-110">Obtenir les paramètres de l’espace de travail OMS</span><span class="sxs-lookup"><span data-stu-id="12e3c-110">Get OMS Workspace settings</span></span>
> * <span data-ttu-id="12e3c-111">Configurer les agents OMS sur les nœuds de Kubernetes hello</span><span class="sxs-lookup"><span data-stu-id="12e3c-111">Set up OMS agents on hello Kubernetes nodes</span></span>
> * <span data-ttu-id="12e3c-112">Accéder aux informations d’analyse dans le portail OMS est hello ou le portail Azure</span><span class="sxs-lookup"><span data-stu-id="12e3c-112">Access monitoring information in hello OMS portal or Azure portal</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="12e3c-113">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="12e3c-113">Before you begin</span></span>

<span data-ttu-id="12e3c-114">Dans les didacticiels précédents, une application a été empaquetée dans des images de conteneur, ces images téléchargées tooAzure Registre de conteneur et un cluster Kubernetes créé.</span><span class="sxs-lookup"><span data-stu-id="12e3c-114">In previous tutorials, an application was packaged into container images, these images uploaded tooAzure Container Registry, and a Kubernetes cluster created.</span></span> <span data-ttu-id="12e3c-115">Si vous n’avez pas fait ces étapes et que vous aimeriez toofollow le long, retourner trop[didacticiel 1 : créer des images de conteneur](./container-service-tutorial-kubernetes-prepare-app.md).</span><span class="sxs-lookup"><span data-stu-id="12e3c-115">If you have not done these steps, and would like toofollow along, return too[Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span></span> 

<span data-ttu-id="12e3c-116">Ce didacticiel nécessite au minimum un cluster Kubernetes avec des nœuds d’agent Linux, et un compte Operations Management Suite (OMS).</span><span class="sxs-lookup"><span data-stu-id="12e3c-116">At minimum, this tutorial requires a Kubernetes cluster with Linux agent nodes, and an Operations Management Suite (OMS) account.</span></span> <span data-ttu-id="12e3c-117">Au besoin, inscrivez-vous à un [essai OMS gratuit](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial).</span><span class="sxs-lookup"><span data-stu-id="12e3c-117">If needed, sign up for a [free OMS trial](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial).</span></span>

## <a name="get-workspace-settings"></a><span data-ttu-id="12e3c-118">Obtenir les paramètres de l’espace de travail</span><span class="sxs-lookup"><span data-stu-id="12e3c-118">Get Workspace settings</span></span>

<span data-ttu-id="12e3c-119">Lorsque vous pouvez accéder à hello [portail OMS](https://mms.microsoft.com), accédez trop**paramètres** > **Sources connectées** > **des serveurs Linux**.</span><span class="sxs-lookup"><span data-stu-id="12e3c-119">When you can access hello [OMS portal](https://mms.microsoft.com), go too**Settings** > **Connected Sources** > **Linux Servers**.</span></span> <span data-ttu-id="12e3c-120">Là, vous pouvez trouver hello *ID de l’espace de travail* et principal ou secondaire *clé de l’espace de travail*.</span><span class="sxs-lookup"><span data-stu-id="12e3c-120">There, you can find hello *Workspace ID* and a primary or secondary *Workspace Key*.</span></span> <span data-ttu-id="12e3c-121">Prenez note de ces valeurs, vous devez tooset des agents OMS sur le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="12e3c-121">Take note of these values, which you need tooset up OMS agents on hello cluster.</span></span>

## <a name="set-up-oms-agents"></a><span data-ttu-id="12e3c-122">Configurer les agents OMS</span><span class="sxs-lookup"><span data-stu-id="12e3c-122">Set up OMS agents</span></span>

<span data-ttu-id="12e3c-123">Voici un tooset de fichier YAML des agents OMS sur les nœuds de cluster Linux hello.</span><span class="sxs-lookup"><span data-stu-id="12e3c-123">Here is a YAML file tooset up OMS agents on hello Linux cluster nodes.</span></span> <span data-ttu-id="12e3c-124">Il crée un [DaemonSet](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/) Kubernetes qui exécute un seul et même pod sur chaque nœud de cluster.</span><span class="sxs-lookup"><span data-stu-id="12e3c-124">It creates a Kubernetes [DaemonSet](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/), which runs a single identical pod on each cluster node.</span></span> <span data-ttu-id="12e3c-125">Hello DaemonSet ressource est idéal pour le déploiement d’un agent de surveillance.</span><span class="sxs-lookup"><span data-stu-id="12e3c-125">hello DaemonSet resource is ideal for deploying a monitoring agent.</span></span> 

<span data-ttu-id="12e3c-126">Enregistrer hello nommé par le fichier texte tooa suivant `oms-daemonset.yaml`et remplacez les valeurs d’espace réservé hello pour *myWorkspaceID* et *myWorkspaceKey* avec votre ID d’espace de travail OMS et la clé.</span><span class="sxs-lookup"><span data-stu-id="12e3c-126">Save hello following text tooa file named `oms-daemonset.yaml`, and replace hello placeholder values for *myWorkspaceID* and *myWorkspaceKey* with your OMS Workspace ID and Key.</span></span> <span data-ttu-id="12e3c-127">(En production, vous pouvez encoder ces valeurs en tant que secrets).</span><span class="sxs-lookup"><span data-stu-id="12e3c-127">(In production, you can encode these values as secrets.)</span></span>

```YAML
apiVersion: extensions/v1beta1
kind: DaemonSet
metadata:
 name: omsagent
spec:
 template:
  metadata:
   labels:
    app: omsagent
    agentVersion: v1.3.4-127
    dockerProviderVersion: 10.0.0-25
  spec:
   containers:
     - name: omsagent 
       image: "microsoft/oms"
       imagePullPolicy: Always
       env:
       - name: WSID
         value: myWorkspaceID
       - name: KEY 
         value: myWorkspaceKey
       - name: DOMAIN
         value: opinsights.azure.com
       securityContext:
         privileged: true
       ports:
       - containerPort: 25225
         protocol: TCP 
       - containerPort: 25224
         protocol: UDP
       volumeMounts:
        - mountPath: /var/run/docker.sock
          name: docker-sock
        - mountPath: /var/log 
          name: host-log
       livenessProbe:
        exec:
         command:
         - /bin/bash
         - -c
         - ps -ef | grep omsagent | grep -v "grep"
        initialDelaySeconds: 60
        periodSeconds: 60
   volumes:
    - name: docker-sock 
      hostPath:
       path: /var/run/docker.sock
    - name: host-log
      hostPath:
       path: /var/log
```

<span data-ttu-id="12e3c-128">Créer hello DaemonSet avec hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="12e3c-128">Create hello DaemonSet with hello following command:</span></span>

```azurecli-interactive
kubectl create -f oms-daemonset.yaml
```

<span data-ttu-id="12e3c-129">toosee que hello DaemonSet est créé, exécutez :</span><span class="sxs-lookup"><span data-stu-id="12e3c-129">toosee that hello DaemonSet is created, run:</span></span>

```azurecli-interactive
kubectl get daemonset
```

<span data-ttu-id="12e3c-130">La sortie est similaire toohello suivantes :</span><span class="sxs-lookup"><span data-stu-id="12e3c-130">Output is similar toohello following:</span></span>

```azurecli-interactive
NAME       DESIRED   CURRENT   READY     UP-TO-DATE   AVAILABLE   NODE-SELECTOR   AGE
omsagent   3         3         3         0            3           <none>          5m
```

<span data-ttu-id="12e3c-131">Une fois que les agents hello sont en cours d’exécution, il prend plusieurs minutes avant que les données de salutation OMS tooingest et processus.</span><span class="sxs-lookup"><span data-stu-id="12e3c-131">After hello agents are running, it takes several minutes for OMS tooingest and process hello data.</span></span>

## <a name="access-monitoring-data"></a><span data-ttu-id="12e3c-132">Accéder aux données de surveillance</span><span class="sxs-lookup"><span data-stu-id="12e3c-132">Access monitoring data</span></span>

<span data-ttu-id="12e3c-133">Afficher et analyser le conteneur d’OMS hello analyse les données avec hello [solutions de conteneur](../../log-analytics/log-analytics-containers.md) dans hello OMS portal ou hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="12e3c-133">View and analyze hello OMS container monitoring data with hello [Container solution](../../log-analytics/log-analytics-containers.md) in either hello OMS portal or hello Azure portal.</span></span> 

<span data-ttu-id="12e3c-134">solution de conteneur de hello tooinstall à l’aide de hello [portail OMS](https://mms.microsoft.com), accédez trop**galerie des Solutions**.</span><span class="sxs-lookup"><span data-stu-id="12e3c-134">tooinstall hello Container solution using hello [OMS portal](https://mms.microsoft.com), go too**Solutions Gallery**.</span></span> <span data-ttu-id="12e3c-135">Ensuite, ajoutez **Solution Containers**.</span><span class="sxs-lookup"><span data-stu-id="12e3c-135">Then add **Container Solution**.</span></span> <span data-ttu-id="12e3c-136">Également ajouter des solutions de conteneurs hello de hello [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/microsoft.containersoms?tab=Overview).</span><span class="sxs-lookup"><span data-stu-id="12e3c-136">Alternatively, add hello Containers solution from hello [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/microsoft.containersoms?tab=Overview).</span></span>

<span data-ttu-id="12e3c-137">Dans le portail OMS : hello, recherchez un **conteneurs** vignette résumé sur le tableau de bord OMS hello.</span><span class="sxs-lookup"><span data-stu-id="12e3c-137">In hello OMS portal, look for a **Containers** summary tile on hello OMS dashboard.</span></span> <span data-ttu-id="12e3c-138">Cliquez sur la vignette hello pour plus d’informations, y compris : les événements de conteneur, les erreurs, l’état, inventaire de l’image et utilisation du processeur et mémoire.</span><span class="sxs-lookup"><span data-stu-id="12e3c-138">Click hello tile for details including: container events, errors, status, image inventory, and CPU and memory usage.</span></span> <span data-ttu-id="12e3c-139">Pour obtenir des informations plus précises, cliquez sur une ligne dans une vignette, ou effectuez une [recherche dans les journaux](../../log-analytics/log-analytics-log-searches.md).</span><span class="sxs-lookup"><span data-stu-id="12e3c-139">For more granular information, click a row on any tile, or perform a [log search](../../log-analytics/log-analytics-log-searches.md).</span></span>

![Tableau de bord Containers dans le portail OMS](./media/container-service-tutorial-kubernetes-monitor/oms-containers-dashboard.png)

<span data-ttu-id="12e3c-141">De même, Bonjour portail Azure, accédez trop**Analytique de journal** et sélectionnez le nom de votre espace de travail.</span><span class="sxs-lookup"><span data-stu-id="12e3c-141">Similarly, in hello Azure portal, go too**Log Analytics** and select your workspace name.</span></span> <span data-ttu-id="12e3c-142">toosee hello **conteneurs** vignette de résumé, cliquez sur **Solutions** > **conteneurs**.</span><span class="sxs-lookup"><span data-stu-id="12e3c-142">toosee hello **Containers** summary tile, click **Solutions** > **Containers**.</span></span> <span data-ttu-id="12e3c-143">toosee plus d’informations, cliquez sur la vignette de hello.</span><span class="sxs-lookup"><span data-stu-id="12e3c-143">toosee details, click hello tile.</span></span>

<span data-ttu-id="12e3c-144">Consultez hello [documentation de l’Analytique des journaux Azure](../../log-analytics/index.md) pour obtenir des instructions détaillées sur l’interrogation et l’analyse des données d’analyse.</span><span class="sxs-lookup"><span data-stu-id="12e3c-144">See hello [Azure Log Analytics documentation](../../log-analytics/index.md) for detailed guidance on querying and analyzing monitoring data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="12e3c-145">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="12e3c-145">Next steps</span></span>

<span data-ttu-id="12e3c-146">Dans ce didacticiel, vous surveillez votre cluster Kubernetes avec OMS.</span><span class="sxs-lookup"><span data-stu-id="12e3c-146">In this tutorial, you monitored your Kubernetes cluster with OMS.</span></span> <span data-ttu-id="12e3c-147">Les tâches traitées ont inclus :</span><span class="sxs-lookup"><span data-stu-id="12e3c-147">Tasks covered included:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="12e3c-148">Obtenir les paramètres de l’espace de travail OMS</span><span class="sxs-lookup"><span data-stu-id="12e3c-148">Get OMS Workspace settings</span></span>
> * <span data-ttu-id="12e3c-149">Configurer les agents OMS sur les nœuds de Kubernetes hello</span><span class="sxs-lookup"><span data-stu-id="12e3c-149">Set up OMS agents on hello Kubernetes nodes</span></span>
> * <span data-ttu-id="12e3c-150">Accéder aux informations d’analyse dans le portail OMS est hello ou le portail Azure</span><span class="sxs-lookup"><span data-stu-id="12e3c-150">Access monitoring information in hello OMS portal or Azure portal</span></span>


<span data-ttu-id="12e3c-151">Suivez cette toosee lien prégénérées des exemples de scripts pour le Service de conteneur.</span><span class="sxs-lookup"><span data-stu-id="12e3c-151">Follow this link toosee pre-built script samples for Container Service.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="12e3c-152">Exemples de scripts Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="12e3c-152">Azure Container Service script samples</span></span>](cli-samples.md)
