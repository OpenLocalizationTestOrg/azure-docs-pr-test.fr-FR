---
title: "cluster de contrôleur de domaine/système d’exploitation Azure aaaMonitor - gestion des opérations | Documents Microsoft"
description: Surveillez un cluster DC/OS Azure Container Service avec Microsoft Operations Management Suite.
services: container-service
documentationcenter: 
author: keikhara
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure
ms.date: 11/17/2016
ms.author: keikhara
ms.custom: mvc
ms.openlocfilehash: 0ebfa3ba3cef8f0205b15731b0e91f5b304bc8fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-dcos-cluster-with-operations-management-suite"></a><span data-ttu-id="6299d-103">Surveillez un cluster DC/OS Azure Container Service avec Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="6299d-103">Monitor an Azure Container Service DC/OS cluster with Operations Management Suite</span></span>

<span data-ttu-id="6299d-104">Microsoft Operations Management Suite (OMS) est une solution de gestion informatique de Microsoft qui vous permet de gérer et de protéger votre infrastructure locale et de cloud.</span><span class="sxs-lookup"><span data-stu-id="6299d-104">Microsoft Operations Management Suite (OMS) is Microsoft's cloud-based IT management solution that helps you manage and protect your on-premises and cloud infrastructure.</span></span> <span data-ttu-id="6299d-105">Conteneur est une solution dans Analytique de journal d’OMS, ce qui vous permet d’afficher l’inventaire hello conteneur, les performances et les journaux dans un emplacement unique.</span><span class="sxs-lookup"><span data-stu-id="6299d-105">Container Solution is a solution in OMS Log Analytics, which helps you view hello container inventory, performance, and logs in a single location.</span></span> <span data-ttu-id="6299d-106">Vous pouvez auditer, résoudre des conteneurs en consultant les journaux hello dans un emplacement centralisé et trouver bruyantes consommation excessive conteneur sur un ordinateur hôte.</span><span class="sxs-lookup"><span data-stu-id="6299d-106">You can audit, troubleshoot containers by viewing hello logs in centralized location, and find noisy consuming excess container on a host.</span></span>

![](media/container-service-monitoring-oms/image1.png)

<span data-ttu-id="6299d-107">Pour plus d’informations sur les solutions de conteneur, reportez-vous à toothe [Analytique de journal conteneur Solution](../../log-analytics/log-analytics-containers.md).</span><span class="sxs-lookup"><span data-stu-id="6299d-107">For more information about Container Solution, please refer toothe [Container Solution Log Analytics](../../log-analytics/log-analytics-containers.md).</span></span>

## <a name="setting-up-oms-from-hello-dcos-universe"></a><span data-ttu-id="6299d-108">Configuration d’OMS à partir de l’univers du contrôleur de domaine/système d’exploitation hello</span><span class="sxs-lookup"><span data-stu-id="6299d-108">Setting up OMS from hello DC/OS universe</span></span>


<span data-ttu-id="6299d-109">Cet article suppose que vous avez défini un contrôleur de domaine/système d’exploitation et que vous avez déployé des applications de conteneur web simple sur le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="6299d-109">This article assumes that you have set up an DC/OS and have deployed simple web container applications on hello cluster.</span></span>

### <a name="pre-requisite"></a><span data-ttu-id="6299d-110">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="6299d-110">Pre-requisite</span></span>
- <span data-ttu-id="6299d-111">[Abonnement Microsoft Azure](https://azure.microsoft.com/free/) : vous pouvez l’obtenir gratuitement.</span><span class="sxs-lookup"><span data-stu-id="6299d-111">[Microsoft Azure Subscription](https://azure.microsoft.com/free/) - You can get this for free.</span></span>  
- <span data-ttu-id="6299d-112">Configuration de l’espace de travail Microsoft OMS : voir l’Étape 3 ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="6299d-112">Microsoft OMS Workspace Setup - see "Step 3" below</span></span>
- <span data-ttu-id="6299d-113">[Interface CLI DC/OS](https://dcos.io/docs/1.8/usage/cli/install/) installées.</span><span class="sxs-lookup"><span data-stu-id="6299d-113">[DC/OS CLI](https://dcos.io/docs/1.8/usage/cli/install/) installed.</span></span>

1. <span data-ttu-id="6299d-114">Dans le tableau de bord du contrôleur de domaine/système d’exploitation hello, cliquez sur l’univers et de recherche à utiliser OMS comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="6299d-114">In hello DC/OS dashboard, click on Universe and search for ‘OMS’ as shown below.</span></span>

![](media/container-service-monitoring-oms/image2.png)

2. <span data-ttu-id="6299d-115">Cliquez sur **Installer**.</span><span class="sxs-lookup"><span data-stu-id="6299d-115">Click **Install**.</span></span> <span data-ttu-id="6299d-116">Vous découvrez un pop avec les informations de version hello OMS et un **installer le Package** ou **Installation avancé** bouton.</span><span class="sxs-lookup"><span data-stu-id="6299d-116">You will see a pop up with hello OMS version information and an **Install Package** or **Advanced Installation** button.</span></span> <span data-ttu-id="6299d-117">Lorsque vous cliquez sur **Installation avancé**, qui vous guide toohello **propriétés de configuration spécifiques OMS** page.</span><span class="sxs-lookup"><span data-stu-id="6299d-117">When you click **Advanced Installation**, which leads you toohello **OMS specific configuration properties** page.</span></span>

![](media/container-service-monitoring-oms/image3.png)

![](media/container-service-monitoring-oms/image4.png)

3. <span data-ttu-id="6299d-118">Ici, nous vous demanderons tooenter hello `wsid` (hello ID d’espace de travail OMS) et `wskey` (hello OMS clé primaire pour l’id d’espace de travail hello).</span><span class="sxs-lookup"><span data-stu-id="6299d-118">Here, you will be asked tooenter hello `wsid` (hello OMS workspace ID) and `wskey` (hello OMS primary key for hello workspace id).</span></span> <span data-ttu-id="6299d-119">tooget les deux `wsid` et `wskey` vous devez toocreate un compte OMS à <https://mms.microsoft.com>. Veuillez suivre hello étapes toocreate un compte.</span><span class="sxs-lookup"><span data-stu-id="6299d-119">tooget both `wsid` and `wskey` you need toocreate an OMS account at <https://mms.microsoft.com>. Please follow hello steps toocreate an account.</span></span> <span data-ttu-id="6299d-120">Une fois que vous avez terminé la création de compte de hello, vous devez tooobtain votre `wsid` et `wskey` en cliquant sur **paramètres**, puis **Sources connectées**, puis **des serveurs Linux** , comme illustré ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="6299d-120">Once you are done creating hello account, you need tooobtain your `wsid` and `wskey` by clicking **Settings**, then **Connected Sources**, and then **Linux Servers**, as shown below.</span></span>

 ![](media/container-service-monitoring-oms/image5.png)

4. <span data-ttu-id="6299d-121">Sélectionnez hello numéro vous OMS instances que vous souhaitez et cliquez sur bouton de « Examinez et installez » hello.</span><span class="sxs-lookup"><span data-stu-id="6299d-121">Select hello number you OMS instances that you want and click hello ‘Review and Install’ button.</span></span> <span data-ttu-id="6299d-122">En règle générale, vous pouvez toohave hello nombre de OMS instances toohello égale la machine virtuelle vous avez dans votre cluster de l’agent.</span><span class="sxs-lookup"><span data-stu-id="6299d-122">Typically, you will want toohave hello number of OMS instances equal toohello number of VM’s you have in your agent cluster.</span></span> <span data-ttu-id="6299d-123">Agent OMS pour Linux est installe en tant que conteneurs individuels sur chaque machine virtuelle qu’il souhaite toocollect des informations pour l’analyse et les informations de journalisation.</span><span class="sxs-lookup"><span data-stu-id="6299d-123">OMS Agent for Linux is installs as individual containers on each VM that it wants toocollect information for monitoring and logging information.</span></span>

## <a name="setting-up-a-simple-oms-dashboard"></a><span data-ttu-id="6299d-124">Configuration d’un tableau de bord OMS simple</span><span class="sxs-lookup"><span data-stu-id="6299d-124">Setting up a simple OMS dashboard</span></span>

<span data-ttu-id="6299d-125">Une fois que vous avez installé hello Agent OMS pour Linux sur les machines virtuelles de hello, étape suivante consiste à tooset de tableau de bord OMS hello.</span><span class="sxs-lookup"><span data-stu-id="6299d-125">Once you have installed hello OMS Agent for Linux on hello VMs, next step is tooset up hello OMS dashboard.</span></span> <span data-ttu-id="6299d-126">Il existe deux façons toodo cela : portail OMS ou le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="6299d-126">There are two ways toodo this: OMS Portal or Azure Portal.</span></span>

### <a name="oms-portal"></a><span data-ttu-id="6299d-127">Portail OMS</span><span class="sxs-lookup"><span data-stu-id="6299d-127">OMS Portal</span></span> 

<span data-ttu-id="6299d-128">Connectez-vous au portail OMS est toohello (<https://mms.microsoft.com>) et accédez toohello **galerie de solutions**.</span><span class="sxs-lookup"><span data-stu-id="6299d-128">Log in toohello OMS portal (<https://mms.microsoft.com>) and go toohello **Solution Gallery**.</span></span>

![](media/container-service-monitoring-oms/image6.png)

<span data-ttu-id="6299d-129">Une fois que vous êtes dans hello **galerie de solutions**, sélectionnez **conteneurs**.</span><span class="sxs-lookup"><span data-stu-id="6299d-129">Once you are in hello **Solution Gallery**, select **Containers**.</span></span>

![](media/container-service-monitoring-oms/image7.png)

<span data-ttu-id="6299d-130">Une fois que vous avez sélectionné hello conteneur Solution, vous verrez hello vignette sur la page de vue d’ensemble du tableau de bord OMS hello.</span><span class="sxs-lookup"><span data-stu-id="6299d-130">Once you’ve selected hello Container Solution, you will see hello tile on hello OMS Overview Dashboard page.</span></span> <span data-ttu-id="6299d-131">Une fois que les données de conteneur hello ingéré sont indexées, vous verrez vignette hello rempli avec les informations sur les vignettes de vue de solution.</span><span class="sxs-lookup"><span data-stu-id="6299d-131">Once hello ingested container data is indexed, you will see hello tile populated with information on the solution view tiles.</span></span>

![](media/container-service-monitoring-oms/image8.png)

### <a name="azure-portal"></a><span data-ttu-id="6299d-132">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="6299d-132">Azure Portal</span></span> 

<span data-ttu-id="6299d-133">Portail de tooAzure de connexion à l’adresse <https://portal.microsoft.com/>.</span><span class="sxs-lookup"><span data-stu-id="6299d-133">Login tooAzure portal at <https://portal.microsoft.com/>.</span></span> <span data-ttu-id="6299d-134">Go to **Marketplace**, sélectionnez **Surveillance + gestion**, puis cliquez sur **Afficher tout**.</span><span class="sxs-lookup"><span data-stu-id="6299d-134">Go to **Marketplace**, select **Monitoring + management** and click **See All**.</span></span> <span data-ttu-id="6299d-135">Ensuite, saisissez `containers` dans la recherche.</span><span class="sxs-lookup"><span data-stu-id="6299d-135">Then Type `containers` in search.</span></span> <span data-ttu-id="6299d-136">Vous verrez « conteneurs » dans les résultats de recherche hello.</span><span class="sxs-lookup"><span data-stu-id="6299d-136">You will see "containers" in hello search results.</span></span> <span data-ttu-id="6299d-137">Sélectionnez **Conteneurs**, puis cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="6299d-137">Select **Containers** and click **Create**.</span></span>

![](media/container-service-monitoring-oms/image9.png)

<span data-ttu-id="6299d-138">Une fois que vous avez cliqué sur **Créer**, vous êtes invité à saisir votre espace de travail.</span><span class="sxs-lookup"><span data-stu-id="6299d-138">Once you click **Create**, it will ask you for your workspace.</span></span> <span data-ttu-id="6299d-139">Sélectionnez votre espace de travail. Si vous n’en avez pas, créez-en un.</span><span class="sxs-lookup"><span data-stu-id="6299d-139">Select your workspace or if you do not have one, create a new workspace.</span></span>

![](media/container-service-monitoring-oms/image10.PNG)

<span data-ttu-id="6299d-140">Une fois la sélection effectuée, cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="6299d-140">Once you’ve selected your workspace, click **Create**.</span></span>

![](media/container-service-monitoring-oms/image11.png)

<span data-ttu-id="6299d-141">Pour plus d’informations sur hello OMS conteneur Solution, reportez-vous à toothe [Analytique de journal conteneur Solution](../../log-analytics/log-analytics-containers.md).</span><span class="sxs-lookup"><span data-stu-id="6299d-141">For more information about hello OMS Container Solution, please refer toothe [Container Solution Log Analytics](../../log-analytics/log-analytics-containers.md).</span></span>

### <a name="how-tooscale-oms-agent-with-acs-dcos"></a><span data-ttu-id="6299d-142">Comment tooscale l’Agent OMS avec contrôleur de domaine/système d’exploitation des services ACS</span><span class="sxs-lookup"><span data-stu-id="6299d-142">How tooscale OMS Agent with ACS DC/OS</span></span> 

<span data-ttu-id="6299d-143">Au cas où vous avez besoin de l’agent OMS de toohave installé au niveau du nombre de nœud réel hello ou mise à l’échelle de la mise en ajoutant plus d’ordinateurs virtuels, vous pouvez le faire par la mise à l’échelle hello `msoms` service.</span><span class="sxs-lookup"><span data-stu-id="6299d-143">In case you need toohave installed OMS agent short of hello actual node count or you are scaling up VMSS by adding more VM, you can do so by scaling hello `msoms` service.</span></span>

<span data-ttu-id="6299d-144">Vous pouvez soit tooMarathon ou hello onglet de Services de l’interface utilisateur de contrôleur de domaine/système d’exploitation et l’échelle votre nombre de nœuds.</span><span class="sxs-lookup"><span data-stu-id="6299d-144">You can either go tooMarathon or hello DC/OS UI Services tab and scale up your node count.</span></span>

![](media/container-service-monitoring-oms/image12.PNG)

<span data-ttu-id="6299d-145">Cette action déploie tooother les nœuds dont vous n’ont pas encore déployé l’agent OMS de hello.</span><span class="sxs-lookup"><span data-stu-id="6299d-145">This will deploy tooother nodes which have not yet deployed hello OMS agent.</span></span>

## <a name="uninstall-ms-oms"></a><span data-ttu-id="6299d-146">Désinstaller MS OMS</span><span class="sxs-lookup"><span data-stu-id="6299d-146">Uninstall MS OMS</span></span>

<span data-ttu-id="6299d-147">toouninstall MS OMS entrez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="6299d-147">toouninstall MS OMS enter hello following command:</span></span>

```bash
$ dcos package uninstall msoms
```

## <a name="let-us-know"></a><span data-ttu-id="6299d-148">Dites-le-nous !</span><span class="sxs-lookup"><span data-stu-id="6299d-148">Let us know!!!</span></span>
<span data-ttu-id="6299d-149">Qu’est-ce qui fonctionne ?</span><span class="sxs-lookup"><span data-stu-id="6299d-149">What works?</span></span> <span data-ttu-id="6299d-150">Quels sont les manquements ?</span><span class="sxs-lookup"><span data-stu-id="6299d-150">What is missing?</span></span> <span data-ttu-id="6299d-151">Quoi d’autre devez-vous pour cette toobe utiles pour vous ?</span><span class="sxs-lookup"><span data-stu-id="6299d-151">What else do you need for this toobe useful for you?</span></span> <span data-ttu-id="6299d-152">Faites-le nous savoir sur <a href="mailto:OMSContainers@microsoft.com">OMSContainers</a>.</span><span class="sxs-lookup"><span data-stu-id="6299d-152">Let us know at <a href="mailto:OMSContainers@microsoft.com">OMSContainers</a>.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6299d-153">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6299d-153">Next steps</span></span>

 <span data-ttu-id="6299d-154">Maintenant que vous avez configuré OMS toomonitor vos conteneurs,[voir votre tableau de bord du conteneur](../../log-analytics/log-analytics-containers.md).</span><span class="sxs-lookup"><span data-stu-id="6299d-154">Now that you have set up OMS toomonitor your containers,[see your container dashboard](../../log-analytics/log-analytics-containers.md).</span></span>
