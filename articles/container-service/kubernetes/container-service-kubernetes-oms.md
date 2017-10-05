---
title: "Surveiller le cluster Kubernetes Azure - Gestion des opérations | Microsoft Docs"
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
ms.openlocfilehash: bd5c81435c091d25bc14710589b7c043e9f56a25
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-an-azure-container-service-cluster-with-microsoft-operations-management-suite-oms"></a><span data-ttu-id="f30ee-103">Surveiller un cluster Azure Container Service avec Microsoft Operations Management Suite (OMS)</span><span class="sxs-lookup"><span data-stu-id="f30ee-103">Monitor an Azure Container Service cluster with Microsoft Operations Management Suite (OMS)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f30ee-104">Composants requis</span><span class="sxs-lookup"><span data-stu-id="f30ee-104">Prerequisites</span></span>
<span data-ttu-id="f30ee-105">Cette procédure pas à pas suppose que vous avez [créé un cluster Kubernetes à l’aide d’Azure Container Service](container-service-kubernetes-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="f30ee-105">This walkthrough assumes that you have [created a Kubernetes cluster using Azure Container Service](container-service-kubernetes-walkthrough.md).</span></span>

<span data-ttu-id="f30ee-106">Elle suppose également que vous avez installé l’outil `az` de l’interface Azure CLI et l’outil `kubectl`.</span><span class="sxs-lookup"><span data-stu-id="f30ee-106">It also assumes that you have the `az` Azure cli and `kubectl` tools installed.</span></span>

<span data-ttu-id="f30ee-107">Vous pouvez tester si l’outil `az` est installé en exécutant :</span><span class="sxs-lookup"><span data-stu-id="f30ee-107">You can test if you have the `az` tool installed by running:</span></span>

```console
$ az --version
```

<span data-ttu-id="f30ee-108">Si l’outil `az` n’est pas installé, suivez les instructions figurant [ici](https://github.com/azure/azure-cli#installation).</span><span class="sxs-lookup"><span data-stu-id="f30ee-108">If you don't have the `az` tool installed, there are instructions [here](https://github.com/azure/azure-cli#installation).</span></span>  
<span data-ttu-id="f30ee-109">Sinon, vous pouvez utiliser [Azure Cloud Shell](https://docs.microsoft.com/en-us/azure/cloud-shell/overview), avec `az`l’interface de ligne Azure et les `kubectl` outils déjà installés pour vous.</span><span class="sxs-lookup"><span data-stu-id="f30ee-109">Alternatively, you can use [Azure Cloud Shell](https://docs.microsoft.com/en-us/azure/cloud-shell/overview), which has the `az` Azure cli and `kubectl` tools already installed for you.</span></span>  

<span data-ttu-id="f30ee-110">Vous pouvez tester si l’outil `kubectl` est installé en exécutant :</span><span class="sxs-lookup"><span data-stu-id="f30ee-110">You can test if you have the `kubectl` tool installed by running:</span></span>

```console
$ kubectl version
```

<span data-ttu-id="f30ee-111">Si `kubectl` n’est pas installé, vous pouvez exécuter :</span><span class="sxs-lookup"><span data-stu-id="f30ee-111">If you don't have `kubectl` installed, you can run:</span></span>
```console
$ az acs kubernetes install-cli
```

<span data-ttu-id="f30ee-112">Pour tester si les clés kubernetes sont installées dans votre outil kubectl vous pouvez exécuter :</span><span class="sxs-lookup"><span data-stu-id="f30ee-112">To test if you have kubernetes keys installed in your kubectl tool you can run:</span></span>
```console
$ kubectl get nodes
```

<span data-ttu-id="f30ee-113">Si les erreurs de commande ci-dessus sortent, vous devez installer les clés de cluster kubernetes dans votre outil kubectl.</span><span class="sxs-lookup"><span data-stu-id="f30ee-113">If the above command errors out, you need to install kubernetes cluster keys into your kubectl tool.</span></span> <span data-ttu-id="f30ee-114">Ceci peut se faire avec la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="f30ee-114">You can do that with the following command:</span></span>
```console
RESOURCE_GROUP=my-resource-group
CLUSTER_NAME=my-acs-name
az acs kubernetes get-credentials --resource-group=$RESOURCE_GROUP --name=$CLUSTER_NAME
```

## <a name="monitoring-containers-with-operations-management-suite-oms"></a><span data-ttu-id="f30ee-115">Surveillance de conteneurs avec Operations Management Suite (OMS)</span><span class="sxs-lookup"><span data-stu-id="f30ee-115">Monitoring Containers with Operations Management Suite (OMS)</span></span>

<span data-ttu-id="f30ee-116">Microsoft Operations Management Suite (OMS) est une solution de gestion informatique basée sur le cloud de Microsoft qui vous permet de gérer et de protéger votre infrastructure locale et de cloud.</span><span class="sxs-lookup"><span data-stu-id="f30ee-116">Microsoft Operations Management (OMS) is Microsoft's cloud-based IT management solution that helps you manage and protect your on-premises and cloud infrastructure.</span></span> <span data-ttu-id="f30ee-117">La solution Conteneurs fait partie intégrante d’OMS Log Analytics, qui vous octroie une visibilité sur le stock, les performances et les fichiers journaux des conteneurs à un emplacement unique.</span><span class="sxs-lookup"><span data-stu-id="f30ee-117">Container Solution is a solution in OMS Log Analytics, which helps you view the container inventory, performance, and logs in a single location.</span></span> <span data-ttu-id="f30ee-118">Vous pouvez auditer les conteneurs, résoudre les problèmes en consultant les fichiers journaux de manière centralisée, et identifier les conteneurs bruyants à consommation supérieure sur un hôte.</span><span class="sxs-lookup"><span data-stu-id="f30ee-118">You can audit, troubleshoot containers by viewing the logs in centralized location, and find noisy consuming excess container on a host.</span></span>

![](media/container-service-monitoring-oms/image1.png)

<span data-ttu-id="f30ee-119">Pour plus d’informations sur la solution Conteneurs, reportez-vous à [Solution Conteneurs (version préliminaire) Log Analytics](../../log-analytics/log-analytics-containers.md).</span><span class="sxs-lookup"><span data-stu-id="f30ee-119">For more information about Container Solution, please refer to the [Container Solution Log Analytics](../../log-analytics/log-analytics-containers.md).</span></span>

## <a name="installing-oms-on-kubernetes"></a><span data-ttu-id="f30ee-120">Installation d’OMS sur Kubernetes</span><span class="sxs-lookup"><span data-stu-id="f30ee-120">Installing OMS on Kubernetes</span></span>

### <a name="obtain-your-workspace-id-and-key"></a><span data-ttu-id="f30ee-121">Obtenir l’ID et la clé d’espace de travail</span><span class="sxs-lookup"><span data-stu-id="f30ee-121">Obtain your workspace ID and key</span></span>
<span data-ttu-id="f30ee-122">Pour que l’agent OMS puisse communiquer avec le service, il doit être configuré avec un ID et une clé d’espace de travail.</span><span class="sxs-lookup"><span data-stu-id="f30ee-122">For the OMS agent to talk to the service it needs to be configured with a workspace id and a workspace key.</span></span> <span data-ttu-id="f30ee-123">Pour les obtenir, vous devez créer un compte OMS à l’adresse <https://mms.microsoft.com>. Suivez la procédure de création de compte.</span><span class="sxs-lookup"><span data-stu-id="f30ee-123">To get the workspace id and key you need to create an OMS account at <https://mms.microsoft.com>. Please follow the steps to create an account.</span></span> <span data-ttu-id="f30ee-124">Une fois que vous avez créé le compte, vous devez obtenir votre ID et votre clé d’espace de travail en cliquant sur **Paramètres**, **Sources connectées**, puis sur **Serveurs Linux**, comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="f30ee-124">Once you are done creating the account, you need to obtain your id and key by clicking **Settings**, then **Connected Sources**, and then **Linux Servers**, as shown below.</span></span>

 ![](media/container-service-monitoring-oms/image5.png)

### <a name="install-the-oms-agent-using-a-daemonset"></a><span data-ttu-id="f30ee-125">Installer l’agent OMS à l’aide d’un DaemonSet</span><span class="sxs-lookup"><span data-stu-id="f30ee-125">Install the OMS agent using a DaemonSet</span></span>
<span data-ttu-id="f30ee-126">Les DaemonSets sont utilisés par DaemonSet pour exécuter une instance unique d’un conteneur sur chaque hôte du cluster.</span><span class="sxs-lookup"><span data-stu-id="f30ee-126">DaemonSets are used by Kubernetes to run a single instance of a container on each host in the cluster.</span></span>
<span data-ttu-id="f30ee-127">Ils sont parfaits pour exécuter des agents de surveillance.</span><span class="sxs-lookup"><span data-stu-id="f30ee-127">They're perfect for running monitoring agents.</span></span>

<span data-ttu-id="f30ee-128">Voici le [fichier DaemonSet YAML](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes).</span><span class="sxs-lookup"><span data-stu-id="f30ee-128">Here is the [DaemonSet YAML file](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes).</span></span> <span data-ttu-id="f30ee-129">Enregistrez-le sous le nom `oms-daemonset.yaml` et remplacez dans ce fichier les valeurs des espaces réservés pour `WSID` et `KEY` par l’ID et la clé de votre espace de travail.</span><span class="sxs-lookup"><span data-stu-id="f30ee-129">Save it to a file named `oms-daemonset.yaml` and replace the place-holder values for `WSID` and `KEY` with your workspace id and key in the file.</span></span>

<span data-ttu-id="f30ee-130">Une fois vos ID et clé d’espace de travail ajoutés à la configuration de DaemonSet, vous pouvez installer l’agent OMS sur votre cluster à l’aide de l’outil de ligne de commande `kubectl` :</span><span class="sxs-lookup"><span data-stu-id="f30ee-130">Once you have added your workspace ID and key to the DaemonSet configuration, you can install the OMS agent on your cluster with the `kubectl` command line tool:</span></span>

```console
$ kubectl create -f oms-daemonset.yaml
```

### <a name="installing-the-oms-agent-using-a-kubernetes-secret"></a><span data-ttu-id="f30ee-131">Installation de l’agent OMS à l’aide d’une clé secrète Kubernetes</span><span class="sxs-lookup"><span data-stu-id="f30ee-131">Installing the OMS agent using a Kubernetes Secret</span></span>
<span data-ttu-id="f30ee-132">Pour protéger votre ID d’espace de travail OMS et la clé vous pouvez utiliser les clés secrètes Kubernetes dans le cadre du fichier YAML DaemonSet.</span><span class="sxs-lookup"><span data-stu-id="f30ee-132">To protect your OMS workspace ID and key you can use Kubernetes Secret as a part of DaemonSet YAML file.</span></span>

 - <span data-ttu-id="f30ee-133">Copiez le script, le fichier modèle de la clé secrète et le fichier YAML DaemonSet (dans le [référentiel](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes)) et assurez-vous qu’ils se trouvent dans le même répertoire.</span><span class="sxs-lookup"><span data-stu-id="f30ee-133">Copy the script, secret template file and the DaemonSet YAML file (from [repository](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes)) and make sure they are on the same directory.</span></span> 
      - <span data-ttu-id="f30ee-134">clé de secret générant le script - secret-gen.sh</span><span class="sxs-lookup"><span data-stu-id="f30ee-134">secret generating script - secret-gen.sh</span></span>
      - <span data-ttu-id="f30ee-135">modèle de clé de secret - secret-template.yaml</span><span class="sxs-lookup"><span data-stu-id="f30ee-135">secret template - secret-template.yaml</span></span>
   - <span data-ttu-id="f30ee-136">Fichier DaemonSet YAML - omsagent-ds-secrets.yaml</span><span class="sxs-lookup"><span data-stu-id="f30ee-136">DaemonSet YAML file - omsagent-ds-secrets.yaml</span></span>
 - <span data-ttu-id="f30ee-137">Exécutez le script.</span><span class="sxs-lookup"><span data-stu-id="f30ee-137">Run the script.</span></span> <span data-ttu-id="f30ee-138">Le script demande l’ID d’espace de travail OMS et la clé primaire.</span><span class="sxs-lookup"><span data-stu-id="f30ee-138">The script will ask for the OMS Workspace ID and Primary Key.</span></span> <span data-ttu-id="f30ee-139">Veuillez l’insérer. Le script crée un fichier yaml secret pour que vous puissiez l’exécuter.</span><span class="sxs-lookup"><span data-stu-id="f30ee-139">Please insert that and the script will create a secret yaml file so you can run it.</span></span>   
   ```
   #> sudo bash ./secret-gen.sh 
   ```

   - <span data-ttu-id="f30ee-140">Créez le pod de clés secrètes en exécutant la commande suivante : ``` kubectl create -f omsagentsecret.yaml ```</span><span class="sxs-lookup"><span data-stu-id="f30ee-140">Create the secrets pod by running the following: ``` kubectl create -f omsagentsecret.yaml ```</span></span>
 
   - <span data-ttu-id="f30ee-141">Pour vérifier, exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="f30ee-141">To check, run the following:</span></span> 

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
 
  - <span data-ttu-id="f30ee-142">Créer votre DaemonsSet omsagent en exécutant ``` kubectl create -f omsagent-ds-secrets.yaml ```</span><span class="sxs-lookup"><span data-stu-id="f30ee-142">Create your omsagent daemon-set by running ``` kubectl create -f omsagent-ds-secrets.yaml ```</span></span>

### <a name="conclusion"></a><span data-ttu-id="f30ee-143">Conclusion</span><span class="sxs-lookup"><span data-stu-id="f30ee-143">Conclusion</span></span>
<span data-ttu-id="f30ee-144">Et voilà !</span><span class="sxs-lookup"><span data-stu-id="f30ee-144">That's it!</span></span> <span data-ttu-id="f30ee-145">Après quelques minutes, vous devez être en mesure de voir le flux de données vers votre tableau de bord OMS.</span><span class="sxs-lookup"><span data-stu-id="f30ee-145">After a few minutes, you should be able to see data flowing to your OMS dashboard.</span></span>
