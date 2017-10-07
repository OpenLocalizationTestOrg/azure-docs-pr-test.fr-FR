---
title: "cluster de contrôleur de domaine/système d’exploitation Azure aaaMonitor - Datadog | Documents Microsoft"
description: Surveillez un cluster Azure Container Service avec Datadog. Utilisez hello DC/OS web UI toodeploy hello Datadog agents tooyour cluster.
services: container-service
documentationcenter: 
author: sauryadas
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Conteneurs, contrôleur de domaine/système d’exploitation, Docker Swarm, Azure"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure
ms.date: 07/28/2016
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: 10268c04b5c2ef393429e706ed4a467fff80f718
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-dcos-cluster-with-datadog"></a><span data-ttu-id="50c5e-105">Surveiller un cluster DC/OS Azure Container Service avec Datadog</span><span class="sxs-lookup"><span data-stu-id="50c5e-105">Monitor an Azure Container Service DC/OS cluster with Datadog</span></span>
<span data-ttu-id="50c5e-106">Dans cet article, nous déploierez des nœuds d’agent Datadog agents tooall hello dans votre cluster de Service de conteneur Azure.</span><span class="sxs-lookup"><span data-stu-id="50c5e-106">In this article we will deploy Datadog agents tooall hello agent nodes in your Azure Container Service cluster.</span></span> <span data-ttu-id="50c5e-107">Vous aurez besoin d’un compte Datadog pour cette configuration.</span><span class="sxs-lookup"><span data-stu-id="50c5e-107">You will need an account with Datadog for this configuration.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="50c5e-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="50c5e-108">Prerequisites</span></span>
<span data-ttu-id="50c5e-109">[Déployez](container-service-deployment.md) et [connectez](../container-service-connect.md) un cluster configuré par Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="50c5e-109">[Deploy](container-service-deployment.md) and [connect](../container-service-connect.md) a cluster configured by Azure Container Service.</span></span> <span data-ttu-id="50c5e-110">Explorer hello [Marathon UI](container-service-mesos-marathon-ui.md).</span><span class="sxs-lookup"><span data-stu-id="50c5e-110">Explore hello [Marathon UI](container-service-mesos-marathon-ui.md).</span></span> <span data-ttu-id="50c5e-111">Accédez trop[http://datadoghq.com](http://datadoghq.com) tooset d’un compte Datadog.</span><span class="sxs-lookup"><span data-stu-id="50c5e-111">Go too[http://datadoghq.com](http://datadoghq.com) tooset up a Datadog account.</span></span> 

## <a name="datadog"></a><span data-ttu-id="50c5e-112">Datadog</span><span class="sxs-lookup"><span data-stu-id="50c5e-112">Datadog</span></span>
<span data-ttu-id="50c5e-113">Datadog est un service de surveillance qui regroupe les données de surveillance provenant de vos conteneurs dans votre cluster Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="50c5e-113">Datadog is a monitoring service that gathers monitoring data from your containers within your Azure Container Service cluster.</span></span> <span data-ttu-id="50c5e-114">Datadog intègre un tableau de bord Docker Integration qui affiche des mesures spécifiques dans vos conteneurs.</span><span class="sxs-lookup"><span data-stu-id="50c5e-114">Datadog has a Docker Integration Dashboard where you can see specific metrics within your containers.</span></span> <span data-ttu-id="50c5e-115">Les mesures recueillies à partir de vos conteneurs sont classées par processeur, mémoire, réseau et E/S.</span><span class="sxs-lookup"><span data-stu-id="50c5e-115">Metrics gathered from your containers are organized by CPU, Memory, Network and I/O.</span></span> <span data-ttu-id="50c5e-116">Datadog fractionne les mesures en conteneurs et images.</span><span class="sxs-lookup"><span data-stu-id="50c5e-116">Datadog splits metrics into containers and images.</span></span> <span data-ttu-id="50c5e-117">Un exemple de quel hello l’interface utilisateur semble de l’UC, l’utilisation est inférieur.</span><span class="sxs-lookup"><span data-stu-id="50c5e-117">An example of what hello UI looks like for CPU usage is below.</span></span>

![Interface utilisateur Datadog](./media/container-service-monitoring/datadog4.png)

## <a name="configure-a-datadog-deployment-with-marathon"></a><span data-ttu-id="50c5e-119">Configurer un déploiement Datadog avec Marathon</span><span class="sxs-lookup"><span data-stu-id="50c5e-119">Configure a Datadog deployment with Marathon</span></span>
<span data-ttu-id="50c5e-120">Ces étapes vous indiquent comment tooconfigure et de déploiement Datadog applications tooyour cluster avec Marathon.</span><span class="sxs-lookup"><span data-stu-id="50c5e-120">These steps will show you how tooconfigure and deploy Datadog applications tooyour cluster with Marathon.</span></span> 

<span data-ttu-id="50c5e-121">Accédez à l'interface utilisateur de votre contrôleur de domaine/système d’exploitation via [http://localhost:80/](http://localhost:80/).</span><span class="sxs-lookup"><span data-stu-id="50c5e-121">Access your DC/OS UI via [http://localhost:80/](http://localhost:80/).</span></span> <span data-ttu-id="50c5e-122">Une fois Bonjour accédez de l’interface utilisateur du contrôleur de domaine/système d’exploitation toohello « Univers », qui se trouve sur hello inférieur gauche et recherchez « Datadog » puis cliquez sur « Installer ».</span><span class="sxs-lookup"><span data-stu-id="50c5e-122">Once in hello DC/OS UI navigate toohello "Universe" which is on hello bottom left and then search for "Datadog" and click "Install."</span></span>

![Package Datadog dans hello univers du contrôleur de domaine/système d’exploitation](./media/container-service-monitoring/datadog1.png)

<span data-ttu-id="50c5e-124">Maintenant toocomplete hello configuration avoir un compte Datadog ou un compte d’évaluation gratuit.</span><span class="sxs-lookup"><span data-stu-id="50c5e-124">Now toocomplete hello configuration you will need a Datadog account or a free trial account.</span></span> <span data-ttu-id="50c5e-125">Une fois que vous êtes connecté dans le site Web de Datadog toohello rechercher toohello gauche et accédez tooIntegrations -> puis [API](https://app.datadoghq.com/account/settings#api).</span><span class="sxs-lookup"><span data-stu-id="50c5e-125">Once you're logged in toohello Datadog website look toohello left and go tooIntegrations -> then [APIs](https://app.datadoghq.com/account/settings#api).</span></span> 

![Clé d’API Datadog](./media/container-service-monitoring/datadog2.png)

<span data-ttu-id="50c5e-127">Ensuite, entrez votre clé API à la configuration Datadog hello dans hello univers du contrôleur de domaine/système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="50c5e-127">Next enter your API key into hello Datadog configuration within hello DC/OS Universe.</span></span> 

![Configuration Datadog Bonjour univers du contrôleur de domaine/système d’exploitation](./media/container-service-monitoring/datadog3.png) 

<span data-ttu-id="50c5e-129">Bonjour au-dessus de configuration instances sont définies too10000000 donc chaque fois qu’un nouveau nœud est ajouté le cluster toohello Datadog déploiera automatiquement un nœud toothat d’agent.</span><span class="sxs-lookup"><span data-stu-id="50c5e-129">In hello above configuration instances are set too10000000 so whenever a new node is added toohello cluster Datadog will automatically deploy an agent toothat node.</span></span> <span data-ttu-id="50c5e-130">Il s’agit d’une solution temporaire.</span><span class="sxs-lookup"><span data-stu-id="50c5e-130">This is an interim solution.</span></span> <span data-ttu-id="50c5e-131">Une fois que vous avez installé le package de hello vous devez naviguer dans site Web de Datadog toohello précédent et rechercher «[tableaux de bord](https://app.datadoghq.com/dash/list). »</span><span class="sxs-lookup"><span data-stu-id="50c5e-131">Once you've installed hello package you should navigate back toohello Datadog website and find "[Dashboards](https://app.datadoghq.com/dash/list)."</span></span> <span data-ttu-id="50c5e-132">Vous y verrez des tableaux de bord personnalisés (Custom) et d'intégration (Integration).</span><span class="sxs-lookup"><span data-stu-id="50c5e-132">From there you will see Custom and Integration Dashboards.</span></span> <span data-ttu-id="50c5e-133">Hello [tableau de bord Docker](https://app.datadoghq.com/screen/integration/docker) auront toutes les métriques de conteneur hello vous avez besoin pour l’analyse de votre cluster.</span><span class="sxs-lookup"><span data-stu-id="50c5e-133">hello [Docker dashboard](https://app.datadoghq.com/screen/integration/docker) will have all hello container metrics you need for monitoring your cluster.</span></span> 

