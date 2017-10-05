---
title: Surveiller le cluster DC/OS Azure - Dynatrace | Microsoft Docs
description: "Surveillez un cluster DC/OS Azure Container Service avec Dynatrace. Déployez Dynatrace OneAgent à l’aide du tableau de bord DC/OS."
services: container-service
documentationcenter: 
author: MartinGoodwell
manager: 
editor: 
tags: acs, azure-container-service
keywords: Conteneurs, DC/OS, Azure
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/13/2016
ms.author: rogardle
ms.custom: mvc
ms.openlocfilehash: 6fa23728680779e33eda7bb9aa8a01b9cad9a82b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-an-azure-container-service-dcos-cluster-with-dynatrace-saasmanaged"></a><span data-ttu-id="61a2d-105">Surveiller un cluster DC/OS Azure Container Service avec Dynatrace SaaS/Managed</span><span class="sxs-lookup"><span data-stu-id="61a2d-105">Monitor an Azure Container Service DC/OS cluster with Dynatrace SaaS/Managed</span></span>
<span data-ttu-id="61a2d-106">Dans cet article, nous vous montrons comment déployer [Dynatrace](https://www.dynatrace.com/) OneAgent pour surveiller tous les nœuds d’agents de votre cluster Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="61a2d-106">In this article, we show you how to deploy the [Dynatrace](https://www.dynatrace.com/) OneAgent to monitor all the agent nodes in your Azure Container Service cluster.</span></span> <span data-ttu-id="61a2d-107">Vous avez besoin d’un compte Dynatrace SaaS/Managé pour cette configuration.</span><span class="sxs-lookup"><span data-stu-id="61a2d-107">You need an account with Dynatrace SaaS/Managed for this configuration.</span></span> 

## <a name="dynatrace-saasmanaged"></a><span data-ttu-id="61a2d-108">Dynatrace SaaS/Managé</span><span class="sxs-lookup"><span data-stu-id="61a2d-108">Dynatrace SaaS/Managed</span></span>
<span data-ttu-id="61a2d-109">Dynatrace est une solution de surveillance cloud native pour environnements de clusters et de conteneurs hautement dynamiques.</span><span class="sxs-lookup"><span data-stu-id="61a2d-109">Dynatrace is a cloud-native monitoring solution for highly dynamic container and cluster environments.</span></span> <span data-ttu-id="61a2d-110">Elle vous permet de mieux optimiser les déploiements de conteneurs et les allocations de mémoire à l’aide de données d’utilisation en temps réel.</span><span class="sxs-lookup"><span data-stu-id="61a2d-110">It allows you to better optimize your container deployments and memory allocations by using real-time usage data.</span></span> <span data-ttu-id="61a2d-111">Elle est capable d’identifier automatiquement les problèmes d’infrastructure et d’applications en fournissant une planification automatisée, une corrélation des problèmes et une détection des causes racines.</span><span class="sxs-lookup"><span data-stu-id="61a2d-111">It is capable of automatically pinpointing application and infrastructure issues by providing automated baselining, problem correlation, and root-cause detection.</span></span>

<span data-ttu-id="61a2d-112">La figure suivante illustre l’interface utilisateur de Dynatrace :</span><span class="sxs-lookup"><span data-stu-id="61a2d-112">The following figure shows the Dynatrace UI:</span></span>

![IU de Dynatrace](./media/container-service-monitoring-dynatrace/dynatrace.png)

## <a name="prerequisites"></a><span data-ttu-id="61a2d-114">Composants requis</span><span class="sxs-lookup"><span data-stu-id="61a2d-114">Prerequisites</span></span> 
<span data-ttu-id="61a2d-115">[Déployez](container-service-deployment.md) et [connectez](./../container-service-connect.md) sur un cluster configuré par Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="61a2d-115">[Deploy](container-service-deployment.md) and [connect](./../container-service-connect.md) to a cluster configured by Azure Container Service.</span></span> <span data-ttu-id="61a2d-116">Explorez [l’interface utilisateur Marathon](container-service-mesos-marathon-ui.md).</span><span class="sxs-lookup"><span data-stu-id="61a2d-116">Explore the [Marathon UI](container-service-mesos-marathon-ui.md).</span></span> <span data-ttu-id="61a2d-117">Accédez à [https://www.dynatrace.com/trial/](https://www.dynatrace.com/trial/) pour configurer un compte Dynatrace SaaS.</span><span class="sxs-lookup"><span data-stu-id="61a2d-117">Go to [https://www.dynatrace.com/trial/](https://www.dynatrace.com/trial/) to set up a Dynatrace SaaS account.</span></span>  

## <a name="configure-a-dynatrace-deployment-with-marathon"></a><span data-ttu-id="61a2d-118">Configurer un déploiement Dynatrace avec Marathon</span><span class="sxs-lookup"><span data-stu-id="61a2d-118">Configure a Dynatrace deployment with Marathon</span></span>
<span data-ttu-id="61a2d-119">Ces étapes vous expliquent comment configurer et déployer des applications Dynatrace dans votre cluster avec Marathon.</span><span class="sxs-lookup"><span data-stu-id="61a2d-119">These steps show you how to configure and deploy Dynatrace applications to your cluster with Marathon.</span></span>

1. <span data-ttu-id="61a2d-120">Accédez à l'interface utilisateur de votre contrôleur de domaine/système d’exploitation via [http://localhost:80/](http://localhost:80/).</span><span class="sxs-lookup"><span data-stu-id="61a2d-120">Access your DC/OS UI via [http://localhost:80/](http://localhost:80/).</span></span> <span data-ttu-id="61a2d-121">Une fois dans l’interface utilisateur de DC/OS, accédez à l’onglet **Univers**, puis recherchez **Dynatrace**.</span><span class="sxs-lookup"><span data-stu-id="61a2d-121">Once in the DC/OS UI, navigate to the **Universe** tab and then search for **Dynatrace**.</span></span>

    ![Dynatrace dans l’Univers DC/OS](./media/container-service-monitoring-dynatrace/dynatrace-universe.png)

2. <span data-ttu-id="61a2d-123">Pour terminer la configuration, vous avez besoin d’un compte Dynatrace SaaS ou d’un compte d’essai gratuit.</span><span class="sxs-lookup"><span data-stu-id="61a2d-123">To complete the configuration, you need a Dynatrace SaaS account or a free trial account.</span></span> <span data-ttu-id="61a2d-124">Une fois dans le tableau de bord Dynatrace, sélectionnez **Déployer Dynatrace**.</span><span class="sxs-lookup"><span data-stu-id="61a2d-124">Once you log into the Dynatrace dashboard, select **Deploy Dynatrace**.</span></span>

    ![Configurer l’intégration PaaS Dynatrace](./media/container-service-monitoring-dynatrace/setup-paas.png)

3. <span data-ttu-id="61a2d-126">Sur la page, sélectionnez **Configurer l’intégration PaaS**.</span><span class="sxs-lookup"><span data-stu-id="61a2d-126">On the page, select **Set up PaaS integration**.</span></span> 

    ![Jeton API Dynatrace](./media/container-service-monitoring-dynatrace/api-token.png) 

4. <span data-ttu-id="61a2d-128">Entrez votre jeton API dans la configuration de Dynatrace OneAgent au sein de l’Univers DC/OS.</span><span class="sxs-lookup"><span data-stu-id="61a2d-128">Enter your API token into the Dynatrace OneAgent configuration within the DC/OS Universe.</span></span> 

    ![Configuration de Dynatrace OneAgent dans l’Univers DC/OS](./media/container-service-monitoring-dynatrace/dynatrace-config.png)

5. <span data-ttu-id="61a2d-130">Donnez aux instances la valeur du nombre de nœuds que vous envisagez d’exécuter.</span><span class="sxs-lookup"><span data-stu-id="61a2d-130">Set the instances to the number of nodes you intend to run.</span></span> <span data-ttu-id="61a2d-131">Il est également possible de définir un nombre plus élevé, mais DC/OS essayera de trouver de nouvelles instances jusqu’à atteindre ce nombre.</span><span class="sxs-lookup"><span data-stu-id="61a2d-131">Setting a higher number also works, but DC/OS will keep trying to find new instances until that number is actually reached.</span></span> <span data-ttu-id="61a2d-132">Si vous préférez, vous pouvez également fixer une valeur comme 1000000.</span><span class="sxs-lookup"><span data-stu-id="61a2d-132">If you prefer, you can also set this to a value like 1000000.</span></span> <span data-ttu-id="61a2d-133">Dans ce cas, chaque fois qu’un nouveau nœud est ajouté au cluster, Dynatrace déploie automatiquement un agent sur ce nouveau nœud, l’inconvénient étant que DC/OS essaye constamment de déployer d’autres instances.</span><span class="sxs-lookup"><span data-stu-id="61a2d-133">In this case, whenever a new node is added to the cluster, Dynatrace automatically deploys an agent to that new node, at the price of DC/OS constantly trying to deploy further instances.</span></span>

    ![Configuration de Dynatrace dans l’Univers DC/OS : instances](./media/container-service-monitoring-dynatrace/dynatrace-config2.png)

## <a name="next-steps"></a><span data-ttu-id="61a2d-135">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="61a2d-135">Next steps</span></span>

<span data-ttu-id="61a2d-136">Une fois que vous avez installé le package, revenez au tableau de bord Dynatrace.</span><span class="sxs-lookup"><span data-stu-id="61a2d-136">Once you've installed the package, navigate back to the Dynatrace dashboard.</span></span> <span data-ttu-id="61a2d-137">Vous pouvez explorer les différentes métriques d’utilisation des conteneurs de votre cluster.</span><span class="sxs-lookup"><span data-stu-id="61a2d-137">You can explore the different usage metrics for the containers within your cluster.</span></span> 