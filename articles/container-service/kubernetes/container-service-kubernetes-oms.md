---
title: "cluster de Azure Kubernetes aaaMonitor - gestion des opérations | Documents Microsoft"
description: "Surveillance d’un cluster Kubernetes dans Azure Container Service à l’aide de Microsoft Operations Management Suite"
services: container-service
documentationcenter: 
author: bburns
manager: timlt
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/09/2016
ms.author: bburns
ms.custom: mvc
ms.openlocfilehash: 7474ee1571134ffe43ff8e4041cf5a64f5635bb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-cluster-with-microsoft-operations-management-suite-oms"></a><span data-ttu-id="410db-103">Surveiller un cluster Azure Container Service avec Microsoft Operations Management Suite (OMS)</span><span class="sxs-lookup"><span data-stu-id="410db-103">Monitor an Azure Container Service cluster with Microsoft Operations Management Suite (OMS)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="410db-104">Composants requis</span><span class="sxs-lookup"><span data-stu-id="410db-104">Prerequisites</span></span>
<span data-ttu-id="410db-105">Cette procédure pas à pas suppose que vous avez [créé un cluster Kubernetes à l’aide d’Azure Container Service](container-service-kubernetes-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="410db-105">This walkthrough assumes that you have [created a Kubernetes cluster using Azure Container Service](container-service-kubernetes-walkthrough.md).</span></span>

<span data-ttu-id="410db-106">Il suppose également que vous avez hello `az` cli Azure et `kubectl` outils sont installés.</span><span class="sxs-lookup"><span data-stu-id="410db-106">It also assumes that you have hello `az` Azure cli and `kubectl` tools installed.</span></span>

<span data-ttu-id="410db-107">Vous pouvez tester si vous avez hello `az` outil est installé en exécutant :</span><span class="sxs-lookup"><span data-stu-id="410db-107">You can test if you have hello `az` tool installed by running:</span></span>

```console
$ az --version
```

<span data-ttu-id="410db-108">Si vous n’avez pas hello `az` outil est installé, il existe des instructions [ici](https://github.com/azure/azure-cli#installation).</span><span class="sxs-lookup"><span data-stu-id="410db-108">If you don't have hello `az` tool installed, there are instructions [here](https://github.com/azure/azure-cli#installation).</span></span>  
<span data-ttu-id="410db-109">Vous pouvez également utiliser [Azure Cloud Shell](https://docs.microsoft.com/en-us/azure/cloud-shell/overview), qui a hello `az` cli Azure et `kubectl` outils déjà installés pour vous.</span><span class="sxs-lookup"><span data-stu-id="410db-109">Alternatively, you can use [Azure Cloud Shell](https://docs.microsoft.com/en-us/azure/cloud-shell/overview), which has hello `az` Azure cli and `kubectl` tools already installed for you.</span></span>  

<span data-ttu-id="410db-110">Vous pouvez tester si vous avez hello `kubectl` outil est installé en exécutant :</span><span class="sxs-lookup"><span data-stu-id="410db-110">You can test if you have hello `kubectl` tool installed by running:</span></span>

```console
$ kubectl version
```

<span data-ttu-id="410db-111">Si `kubectl` n’est pas installé, vous pouvez exécuter :</span><span class="sxs-lookup"><span data-stu-id="410db-111">If you don't have `kubectl` installed, you can run:</span></span>
```console
$ az acs kubernetes install-cli
```

<span data-ttu-id="410db-112">tootest si vous avez des clés kubernetes installés dans votre outil kubectl que vous pouvez exécuter :</span><span class="sxs-lookup"><span data-stu-id="410db-112">tootest if you have kubernetes keys installed in your kubectl tool you can run:</span></span>
```console
$ kubectl get nodes
```

<span data-ttu-id="410db-113">Si hello ci-dessus erreurs de commande out, vous avez besoin de clés de cluster tooinstall kubernetes dans votre outil kubectl.</span><span class="sxs-lookup"><span data-stu-id="410db-113">If hello above command errors out, you need tooinstall kubernetes cluster keys into your kubectl tool.</span></span> <span data-ttu-id="410db-114">Vous pouvez faire cela avec hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="410db-114">You can do that with hello following command:</span></span>
```console
RESOURCE_GROUP=my-resource-group
CLUSTER_NAME=my-acs-name
az acs kubernetes get-credentials --resource-group=$RESOURCE_GROUP --name=$CLUSTER_NAME
```

## <a name="monitoring-containers-with-operations-management-suite-oms"></a><span data-ttu-id="410db-115">Surveillance de conteneurs avec Operations Management Suite (OMS)</span><span class="sxs-lookup"><span data-stu-id="410db-115">Monitoring Containers with Operations Management Suite (OMS)</span></span>

<span data-ttu-id="410db-116">Microsoft Operations Management Suite (OMS) est une solution de gestion informatique basée sur le cloud de Microsoft qui vous permet de gérer et de protéger votre infrastructure locale et de cloud.</span><span class="sxs-lookup"><span data-stu-id="410db-116">Microsoft Operations Management (OMS) is Microsoft's cloud-based IT management solution that helps you manage and protect your on-premises and cloud infrastructure.</span></span> <span data-ttu-id="410db-117">Conteneur est une solution dans Analytique de journal d’OMS, ce qui vous permet d’afficher l’inventaire hello conteneur, les performances et les journaux dans un emplacement unique.</span><span class="sxs-lookup"><span data-stu-id="410db-117">Container Solution is a solution in OMS Log Analytics, which helps you view hello container inventory, performance, and logs in a single location.</span></span> <span data-ttu-id="410db-118">Vous pouvez auditer, résoudre des conteneurs en consultant les journaux hello dans un emplacement centralisé et trouver bruyantes consommation excessive conteneur sur un ordinateur hôte.</span><span class="sxs-lookup"><span data-stu-id="410db-118">You can audit, troubleshoot containers by viewing hello logs in centralized location, and find noisy consuming excess container on a host.</span></span>

![](media/container-service-monitoring-oms/image1.png)

<span data-ttu-id="410db-119">Pour plus d’informations sur les solutions de conteneur, reportez-vous à toothe [Analytique de journal conteneur Solution](../../log-analytics/log-analytics-containers.md).</span><span class="sxs-lookup"><span data-stu-id="410db-119">For more information about Container Solution, please refer toothe [Container Solution Log Analytics](../../log-analytics/log-analytics-containers.md).</span></span>

## <a name="installing-oms-on-kubernetes"></a><span data-ttu-id="410db-120">Installation d’OMS sur Kubernetes</span><span class="sxs-lookup"><span data-stu-id="410db-120">Installing OMS on Kubernetes</span></span>

### <a name="obtain-your-workspace-id-and-key"></a><span data-ttu-id="410db-121">Obtenir l’ID et la clé d’espace de travail</span><span class="sxs-lookup"><span data-stu-id="410db-121">Obtain your workspace ID and key</span></span>
<span data-ttu-id="410db-122">Pourquoi le service de toohello tootalk OMS agent, elle doit toobe configuré avec un id de l’espace de travail et une clé de l’espace de travail.</span><span class="sxs-lookup"><span data-stu-id="410db-122">For hello OMS agent tootalk toohello service it needs toobe configured with a workspace id and a workspace key.</span></span> <span data-ttu-id="410db-123">compte tooget hello id et la clé que vous avez besoin de toocreate un OMS <https://mms.microsoft.com>. Veuillez suivre hello étapes toocreate un compte.</span><span class="sxs-lookup"><span data-stu-id="410db-123">tooget hello workspace id and key you need toocreate an OMS account at <https://mms.microsoft.com>. Please follow hello steps toocreate an account.</span></span> <span data-ttu-id="410db-124">Une fois que vous avez terminé la création de compte de hello, vous devez tooobtain id et votre clé en cliquant sur **paramètres**, puis **Sources connectées**, puis **des serveurs Linux**, comme illustré ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="410db-124">Once you are done creating hello account, you need tooobtain your id and key by clicking **Settings**, then **Connected Sources**, and then **Linux Servers**, as shown below.</span></span>

 ![](media/container-service-monitoring-oms/image5.png)

### <a name="install-hello-oms-agent-using-a-daemonset"></a><span data-ttu-id="410db-125">Installer l’agent OMS de hello à l’aide d’un DaemonSet</span><span class="sxs-lookup"><span data-stu-id="410db-125">Install hello OMS agent using a DaemonSet</span></span>
<span data-ttu-id="410db-126">DaemonSets sont utilisés par Kubernetes toorun une instance unique d’un conteneur sur chaque hôte de cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="410db-126">DaemonSets are used by Kubernetes toorun a single instance of a container on each host in hello cluster.</span></span>
<span data-ttu-id="410db-127">Ils sont parfaits pour exécuter des agents de surveillance.</span><span class="sxs-lookup"><span data-stu-id="410db-127">They're perfect for running monitoring agents.</span></span>

<span data-ttu-id="410db-128">Voici hello [fichier de DaemonSet YAML](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes).</span><span class="sxs-lookup"><span data-stu-id="410db-128">Here is hello [DaemonSet YAML file](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes).</span></span> <span data-ttu-id="410db-129">Enregistrer les fichiers tooa nommé `oms-daemonset.yaml` et remplacer des valeurs d’espace réservé hello pour `WSID` et `KEY` avec l’id de l’espace de travail et votre clé dans le fichier de hello.</span><span class="sxs-lookup"><span data-stu-id="410db-129">Save it tooa file named `oms-daemonset.yaml` and replace hello place-holder values for `WSID` and `KEY` with your workspace id and key in hello file.</span></span>

<span data-ttu-id="410db-130">Une fois que vous avez ajouté votre ID d’espace de travail et de la configuration de DaemonSet toohello clé, vous pouvez installer l’agent OMS de hello sur votre cluster avec hello `kubectl` outil de ligne de commande :</span><span class="sxs-lookup"><span data-stu-id="410db-130">Once you have added your workspace ID and key toohello DaemonSet configuration, you can install hello OMS agent on your cluster with hello `kubectl` command line tool:</span></span>

```console
$ kubectl create -f oms-daemonset.yaml
```

### <a name="installing-hello-oms-agent-using-a-kubernetes-secret"></a><span data-ttu-id="410db-131">L’installation de l’agent OMS de hello à l’aide d’une clé secrète Kubernetes</span><span class="sxs-lookup"><span data-stu-id="410db-131">Installing hello OMS agent using a Kubernetes Secret</span></span>
<span data-ttu-id="410db-132">tooprotect votre ID d’espace de travail OMS et la clé que vous pouvez utiliser Kubernetes Secret comme une partie du fichier de DaemonSet YAML.</span><span class="sxs-lookup"><span data-stu-id="410db-132">tooprotect your OMS workspace ID and key you can use Kubernetes Secret as a part of DaemonSet YAML file.</span></span>

 - <span data-ttu-id="410db-133">Copier les script hello, fichier modèle secrète et hello fichier de DaemonSet YAML (à partir de [référentiel](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes)) et assurez-vous qu’ils sont sur hello même répertoire.</span><span class="sxs-lookup"><span data-stu-id="410db-133">Copy hello script, secret template file and hello DaemonSet YAML file (from [repository](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes)) and make sure they are on hello same directory.</span></span> 
      - <span data-ttu-id="410db-134">clé de secret générant le script - secret-gen.sh</span><span class="sxs-lookup"><span data-stu-id="410db-134">secret generating script - secret-gen.sh</span></span>
      - <span data-ttu-id="410db-135">modèle de clé de secret - secret-template.yaml</span><span class="sxs-lookup"><span data-stu-id="410db-135">secret template - secret-template.yaml</span></span>
   - <span data-ttu-id="410db-136">Fichier DaemonSet YAML - omsagent-ds-secrets.yaml</span><span class="sxs-lookup"><span data-stu-id="410db-136">DaemonSet YAML file - omsagent-ds-secrets.yaml</span></span>
 - <span data-ttu-id="410db-137">Exécutez le script de hello.</span><span class="sxs-lookup"><span data-stu-id="410db-137">Run hello script.</span></span> <span data-ttu-id="410db-138">script de Hello demandera hello ID d’espace de travail OMS et la clé primaire.</span><span class="sxs-lookup"><span data-stu-id="410db-138">hello script will ask for hello OMS Workspace ID and Primary Key.</span></span> <span data-ttu-id="410db-139">Veuillez insérer qui et hello script crée un fichier yaml secrète, vous pouvez l’exécuter.</span><span class="sxs-lookup"><span data-stu-id="410db-139">Please insert that and hello script will create a secret yaml file so you can run it.</span></span>   
   ```
   #> sudo bash ./secret-gen.sh 
   ```

   - <span data-ttu-id="410db-140">Créer des pod de secrets hello en exécutant hello suivante :``` kubectl create -f omsagentsecret.yaml ```</span><span class="sxs-lookup"><span data-stu-id="410db-140">Create hello secrets pod by running hello following: ``` kubectl create -f omsagentsecret.yaml ```</span></span>
 
   - <span data-ttu-id="410db-141">toocheck, exécutez hello suivante :</span><span class="sxs-lookup"><span data-stu-id="410db-141">toocheck, run hello following:</span></span> 

   ``` 
   root@ubuntu16-13db:~# kubectl get secrets
   NAME                  TYPE                                  DATA      AGE
   default-token-gvl91   kubernetes.io/service-account-token   3         50d
   omsagent-secret       Opaque                                2         1d
   root@ubuntu16-13db:~# kubectl describe secrets omsagent-secret
   Name:           omsagent-secret
   Namespace:      default
   Labels:         <none>
   Annotations:    <none>

   Type:   Opaque

   Data
   ====
   WSID:   36 bytes
   KEY:    88 bytes 
   ```
 
  - <span data-ttu-id="410db-142">Créer votre DaemonsSet de l’agent OMS en exécutant ``` kubectl create -f omsagent-ds-secrets.yaml ```</span><span class="sxs-lookup"><span data-stu-id="410db-142">Create your omsagent daemon-set by running ``` kubectl create -f omsagent-ds-secrets.yaml ```</span></span>

### <a name="conclusion"></a><span data-ttu-id="410db-143">Conclusion</span><span class="sxs-lookup"><span data-stu-id="410db-143">Conclusion</span></span>
<span data-ttu-id="410db-144">Et voilà !</span><span class="sxs-lookup"><span data-stu-id="410db-144">That's it!</span></span> <span data-ttu-id="410db-145">Après quelques minutes, vous devez être en mesure de toosee transferts de données du tableau de bord OMS tooyour.</span><span class="sxs-lookup"><span data-stu-id="410db-145">After a few minutes, you should be able toosee data flowing tooyour OMS dashboard.</span></span>
