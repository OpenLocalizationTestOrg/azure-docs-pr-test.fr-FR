---
title: "Surveiller le cluster DC/OS - Gestion des opérations | Microsoft Docs"
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
ms.openlocfilehash: 9b8f96b34b53982c469273a3df9751ceb7930d60
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-an-azure-container-service-dcos-cluster-with-operations-management-suite"></a><span data-ttu-id="33494-103">Surveillez un cluster DC/OS Azure Container Service avec Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="33494-103">Monitor an Azure Container Service DC/OS cluster with Operations Management Suite</span></span>

<span data-ttu-id="33494-104">Microsoft Operations Management Suite (OMS) est une solution de gestion informatique de Microsoft qui vous permet de gérer et de protéger votre infrastructure locale et de cloud.</span><span class="sxs-lookup"><span data-stu-id="33494-104">Microsoft Operations Management Suite (OMS) is Microsoft's cloud-based IT management solution that helps you manage and protect your on-premises and cloud infrastructure.</span></span> <span data-ttu-id="33494-105">La solution Conteneurs fait partie intégrante d’OMS Log Analytics, qui vous octroie une visibilité sur le stock, les performances et les fichiers journaux des conteneurs à un emplacement unique.</span><span class="sxs-lookup"><span data-stu-id="33494-105">Container Solution is a solution in OMS Log Analytics, which helps you view the container inventory, performance, and logs in a single location.</span></span> <span data-ttu-id="33494-106">Vous pouvez auditer les conteneurs, résoudre les problèmes en consultant les fichiers journaux de manière centralisée, et identifier les conteneurs bruyants à consommation supérieure sur un hôte.</span><span class="sxs-lookup"><span data-stu-id="33494-106">You can audit, troubleshoot containers by viewing the logs in centralized location, and find noisy consuming excess container on a host.</span></span>

![](media/container-service-monitoring-oms/image1.png)

<span data-ttu-id="33494-107">Pour plus d’informations sur la solution Conteneurs, reportez-vous à [Solution Conteneurs (version préliminaire) Log Analytics](../../log-analytics/log-analytics-containers.md).</span><span class="sxs-lookup"><span data-stu-id="33494-107">For more information about Container Solution, please refer to the [Container Solution Log Analytics](../../log-analytics/log-analytics-containers.md).</span></span>

## <a name="setting-up-oms-from-the-dcos-universe"></a><span data-ttu-id="33494-108">Configuration d’OMS à partir de l’univers DC/OS</span><span class="sxs-lookup"><span data-stu-id="33494-108">Setting up OMS from the DC/OS universe</span></span>


<span data-ttu-id="33494-109">Cet article suppose que vous avez configuré un univers DC/OS et avez déployé des applications web simples de conteneurs sur le cluster.</span><span class="sxs-lookup"><span data-stu-id="33494-109">This article assumes that you have set up an DC/OS and have deployed simple web container applications on the cluster.</span></span>

### <a name="pre-requisite"></a><span data-ttu-id="33494-110">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="33494-110">Pre-requisite</span></span>
- <span data-ttu-id="33494-111">[Abonnement Microsoft Azure](https://azure.microsoft.com/free/) : vous pouvez l’obtenir gratuitement.</span><span class="sxs-lookup"><span data-stu-id="33494-111">[Microsoft Azure Subscription](https://azure.microsoft.com/free/) - You can get this for free.</span></span>  
- <span data-ttu-id="33494-112">Configuration de l’espace de travail Microsoft OMS : voir l’Étape 3 ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="33494-112">Microsoft OMS Workspace Setup - see "Step 3" below</span></span>
- <span data-ttu-id="33494-113">[Interface CLI DC/OS](https://dcos.io/docs/1.8/usage/cli/install/) installées.</span><span class="sxs-lookup"><span data-stu-id="33494-113">[DC/OS CLI](https://dcos.io/docs/1.8/usage/cli/install/) installed.</span></span>

1. <span data-ttu-id="33494-114">Dans le tableau de bord DC/OS, cliquez sur l’univers, puis recherchez « OMS », tel que représenté ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="33494-114">In the DC/OS dashboard, click on Universe and search for ‘OMS’ as shown below.</span></span>

![](media/container-service-monitoring-oms/image2.png)

2. <span data-ttu-id="33494-115">Cliquez sur **Installer**.</span><span class="sxs-lookup"><span data-stu-id="33494-115">Click **Install**.</span></span> <span data-ttu-id="33494-116">Vous découvrez une fenêtre contextuelle avec les informations de version OMS et un bouton **Installer le package** ou **Installation avancée**.</span><span class="sxs-lookup"><span data-stu-id="33494-116">You will see a pop up with the OMS version information and an **Install Package** or **Advanced Installation** button.</span></span> <span data-ttu-id="33494-117">Lorsque vous cliquez sur **Installation avancée**, vous accédez à la page des **propriétés de configuration spécifique OMS**.</span><span class="sxs-lookup"><span data-stu-id="33494-117">When you click **Advanced Installation**, which leads you to the **OMS specific configuration properties** page.</span></span>

![](media/container-service-monitoring-oms/image3.png)

![](media/container-service-monitoring-oms/image4.png)

3. <span data-ttu-id="33494-118">Ici, vous êtes invité à entrer `wsid` (l’ID d’espace de travail OMS) et `wskey` (la clé primaire OMS pour l’ID d’espace de travail).</span><span class="sxs-lookup"><span data-stu-id="33494-118">Here, you will be asked to enter the `wsid` (the OMS workspace ID) and `wskey` (the OMS primary key for the workspace id).</span></span> <span data-ttu-id="33494-119">Pour obtenir à la fois `wsid` et `wskey`, vous devez créer un compte OMS à l’adresse <https://mms.microsoft.com>. Suivez la procédure de création de compte.</span><span class="sxs-lookup"><span data-stu-id="33494-119">To get both `wsid` and `wskey` you need to create an OMS account at <https://mms.microsoft.com>. Please follow the steps to create an account.</span></span> <span data-ttu-id="33494-120">Une fois que vous avez créé le compte, pour obtenir votre `wsid` et votre `wskey`, cliquez sur **Paramètres**, puis sur **Sources connectés**, puis sur **Serveurs Linux**, tel que représenté ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="33494-120">Once you are done creating the account, you need to obtain your `wsid` and `wskey` by clicking **Settings**, then **Connected Sources**, and then **Linux Servers**, as shown below.</span></span>

 ![](media/container-service-monitoring-oms/image5.png)

4. <span data-ttu-id="33494-121">Sélectionnez le nombre d’instances OMS souhaité, puis cliquez sur le bouton Vérifier et installer.</span><span class="sxs-lookup"><span data-stu-id="33494-121">Select the number you OMS instances that you want and click the ‘Review and Install’ button.</span></span> <span data-ttu-id="33494-122">Généralement, vous avez intérêt à ce que le nombre d’instances OMS soit équivalent au nombre de machines virtuelles dans votre cluster d’agent.</span><span class="sxs-lookup"><span data-stu-id="33494-122">Typically, you will want to have the number of OMS instances equal to the number of VM’s you have in your agent cluster.</span></span> <span data-ttu-id="33494-123">L’Agent OMS pour Linux s’installe en tant que conteneurs individuels sur chaque machine virtuelle qu’il souhaite affecter à la collecte d’informations pour la surveillance et la consignation des données.</span><span class="sxs-lookup"><span data-stu-id="33494-123">OMS Agent for Linux is installs as individual containers on each VM that it wants to collect information for monitoring and logging information.</span></span>

## <a name="setting-up-a-simple-oms-dashboard"></a><span data-ttu-id="33494-124">Configuration d’un tableau de bord OMS simple</span><span class="sxs-lookup"><span data-stu-id="33494-124">Setting up a simple OMS dashboard</span></span>

<span data-ttu-id="33494-125">Une fois que vous avez installé l’Agent OMS pour Linux sur les machines virtuelles, il vous faut configurer le tableau de bord OMS.</span><span class="sxs-lookup"><span data-stu-id="33494-125">Once you have installed the OMS Agent for Linux on the VMs, next step is to set up the OMS dashboard.</span></span> <span data-ttu-id="33494-126">Il existe deux manières de procéder : via le portail OMS et via le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="33494-126">There are two ways to do this: OMS Portal or Azure Portal.</span></span>

### <a name="oms-portal"></a><span data-ttu-id="33494-127">Portail OMS</span><span class="sxs-lookup"><span data-stu-id="33494-127">OMS Portal</span></span> 

<span data-ttu-id="33494-128">Connectez-vous au portail OMS (<https://mms.microsoft.com>), puis accédez à la **Galerie de solutions**.</span><span class="sxs-lookup"><span data-stu-id="33494-128">Log in to the OMS portal (<https://mms.microsoft.com>) and go to the **Solution Gallery**.</span></span>

![](media/container-service-monitoring-oms/image6.png)

<span data-ttu-id="33494-129">Une fois dans la **Galerie de solutions**, sélectionnez **Conteneurs**.</span><span class="sxs-lookup"><span data-stu-id="33494-129">Once you are in the **Solution Gallery**, select **Containers**.</span></span>

![](media/container-service-monitoring-oms/image7.png)

<span data-ttu-id="33494-130">Une fois que vous avez sélectionné la solution de conteneur, la vignette s’affiche sur la page du tableau de bord de présentation OMS.</span><span class="sxs-lookup"><span data-stu-id="33494-130">Once you’ve selected the Container Solution, you will see the tile on the OMS Overview Dashboard page.</span></span> <span data-ttu-id="33494-131">Dès que les données de conteneurs fournies sont indexées, les vignettes de vue de la solution sont renseignées avec les informations.</span><span class="sxs-lookup"><span data-stu-id="33494-131">Once the ingested container data is indexed, you will see the tile populated with information on the solution view tiles.</span></span>

![](media/container-service-monitoring-oms/image8.png)

### <a name="azure-portal"></a><span data-ttu-id="33494-132">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="33494-132">Azure Portal</span></span> 

<span data-ttu-id="33494-133">Connectez-vous au portail Azure, à l’adresse <https://portal.microsoft.com/>.</span><span class="sxs-lookup"><span data-stu-id="33494-133">Login to Azure portal at <https://portal.microsoft.com/>.</span></span> <span data-ttu-id="33494-134">Go to **Marketplace**, sélectionnez **Surveillance + gestion**, puis cliquez sur **Afficher tout**.</span><span class="sxs-lookup"><span data-stu-id="33494-134">Go to **Marketplace**, select **Monitoring + management** and click **See All**.</span></span> <span data-ttu-id="33494-135">Ensuite, saisissez `containers` dans la recherche.</span><span class="sxs-lookup"><span data-stu-id="33494-135">Then Type `containers` in search.</span></span> <span data-ttu-id="33494-136">L’indication « conteneurs » apparaît dans les résultats de la recherche.</span><span class="sxs-lookup"><span data-stu-id="33494-136">You will see "containers" in the search results.</span></span> <span data-ttu-id="33494-137">Sélectionnez **Conteneurs**, puis cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="33494-137">Select **Containers** and click **Create**.</span></span>

![](media/container-service-monitoring-oms/image9.png)

<span data-ttu-id="33494-138">Une fois que vous avez cliqué sur **Créer**, vous êtes invité à saisir votre espace de travail.</span><span class="sxs-lookup"><span data-stu-id="33494-138">Once you click **Create**, it will ask you for your workspace.</span></span> <span data-ttu-id="33494-139">Sélectionnez votre espace de travail. Si vous n’en avez pas, créez-en un.</span><span class="sxs-lookup"><span data-stu-id="33494-139">Select your workspace or if you do not have one, create a new workspace.</span></span>

![](media/container-service-monitoring-oms/image10.PNG)

<span data-ttu-id="33494-140">Une fois la sélection effectuée, cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="33494-140">Once you’ve selected your workspace, click **Create**.</span></span>

![](media/container-service-monitoring-oms/image11.png)

<span data-ttu-id="33494-141">Pour plus d’informations sur la solution de conteneur OMS, reportez-vous [Solution Conteneurs (version préliminaire) Log Analytics](../../log-analytics/log-analytics-containers.md).</span><span class="sxs-lookup"><span data-stu-id="33494-141">For more information about the OMS Container Solution, please refer to the [Container Solution Log Analytics](../../log-analytics/log-analytics-containers.md).</span></span>

### <a name="how-to-scale-oms-agent-with-acs-dcos"></a><span data-ttu-id="33494-142">Mise à l’échelle de l’Agent OMS avec ACS DC/OS</span><span class="sxs-lookup"><span data-stu-id="33494-142">How to scale OMS Agent with ACS DC/OS</span></span> 

<span data-ttu-id="33494-143">Si vous devez avoir installé l’Agent OMS en-deçà du nombre réel de nœuds ou si vous mettez à l’échelle VMSS en ajoutant davantage de machines virtuelles, vous pouvez mettre à l’échelle le service `msoms`.</span><span class="sxs-lookup"><span data-stu-id="33494-143">In case you need to have installed OMS agent short of the actual node count or you are scaling up VMSS by adding more VM, you can do so by scaling the `msoms` service.</span></span>

<span data-ttu-id="33494-144">Pour ce faire, accédez à Marathon ou à l’onglet des services d’interface utilisateur DC/OS, puis augmentez le nombre de nœuds.</span><span class="sxs-lookup"><span data-stu-id="33494-144">You can either go to Marathon or the DC/OS UI Services tab and scale up your node count.</span></span>

![](media/container-service-monitoring-oms/image12.PNG)

<span data-ttu-id="33494-145">Cette action se déploie sur d’autres nœuds qui n’ont pas encore déployé l’Agent OMS.</span><span class="sxs-lookup"><span data-stu-id="33494-145">This will deploy to other nodes which have not yet deployed the OMS agent.</span></span>

## <a name="uninstall-ms-oms"></a><span data-ttu-id="33494-146">Désinstaller MS OMS</span><span class="sxs-lookup"><span data-stu-id="33494-146">Uninstall MS OMS</span></span>

<span data-ttu-id="33494-147">Pour désinstaller MS OMS, saisissez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="33494-147">To uninstall MS OMS enter the following command:</span></span>

```bash
$ dcos package uninstall msoms
```

## <a name="let-us-know"></a><span data-ttu-id="33494-148">Dites-le-nous !</span><span class="sxs-lookup"><span data-stu-id="33494-148">Let us know!!!</span></span>
<span data-ttu-id="33494-149">Qu’est-ce qui fonctionne ?</span><span class="sxs-lookup"><span data-stu-id="33494-149">What works?</span></span> <span data-ttu-id="33494-150">Quels sont les manquements ?</span><span class="sxs-lookup"><span data-stu-id="33494-150">What is missing?</span></span> <span data-ttu-id="33494-151">Quels éléments pourraient vous être utiles ?</span><span class="sxs-lookup"><span data-stu-id="33494-151">What else do you need for this to be useful for you?</span></span> <span data-ttu-id="33494-152">Faites-le nous savoir sur <a href="mailto:OMSContainers@microsoft.com">OMSContainers</a>.</span><span class="sxs-lookup"><span data-stu-id="33494-152">Let us know at <a href="mailto:OMSContainers@microsoft.com">OMSContainers</a>.</span></span>

## <a name="next-steps"></a><span data-ttu-id="33494-153">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="33494-153">Next steps</span></span>

 <span data-ttu-id="33494-154">Maintenant que vous avez configuré OMS pour surveiller vos conteneurs, [consultez le tableau de bord des conteneurs](../../log-analytics/log-analytics-containers.md).</span><span class="sxs-lookup"><span data-stu-id="33494-154">Now that you have set up OMS to monitor your containers,[see your container dashboard](../../log-analytics/log-analytics-containers.md).</span></span>
