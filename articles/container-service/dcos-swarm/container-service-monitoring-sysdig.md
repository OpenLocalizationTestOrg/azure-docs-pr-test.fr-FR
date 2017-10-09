---
title: aaaMonitor un Service de conteneur Azure cluster avec Sysdig | Documents Microsoft
description: Surveillez un cluster Azure Container Service avec Sysdig.
services: container-service
documentationcenter: 
author: sauryadas
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Conteneurs, DC/OS, Azure
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2016
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: 72f2d3d6f6885f9876fa158b88aae58b84a4610f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-cluster-with-sysdig"></a><span data-ttu-id="b4b41-104">Surveiller un cluster Azure Container Service avec Sysdig</span><span class="sxs-lookup"><span data-stu-id="b4b41-104">Monitor an Azure Container Service cluster with Sysdig</span></span>
<span data-ttu-id="b4b41-105">Dans cet article, nous déploierez des nœuds d’agent Sysdig agents tooall hello dans votre cluster de Service de conteneur Azure.</span><span class="sxs-lookup"><span data-stu-id="b4b41-105">In this article, we will deploy Sysdig agents tooall hello agent nodes in your Azure Container Service cluster.</span></span> <span data-ttu-id="b4b41-106">Vous avez besoin d’un compte Sysdig pour cette configuration.</span><span class="sxs-lookup"><span data-stu-id="b4b41-106">You need an account with Sysdig for this configuration.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="b4b41-107">Composants requis</span><span class="sxs-lookup"><span data-stu-id="b4b41-107">Prerequisites</span></span>
<span data-ttu-id="b4b41-108">[Déployez](container-service-deployment.md) et [connectez](../container-service-connect.md) un cluster configuré par Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="b4b41-108">[Deploy](container-service-deployment.md) and [connect](../container-service-connect.md) a cluster configured by Azure Container Service.</span></span> <span data-ttu-id="b4b41-109">Explorer hello [Marathon UI](container-service-mesos-marathon-ui.md).</span><span class="sxs-lookup"><span data-stu-id="b4b41-109">Explore hello [Marathon UI](container-service-mesos-marathon-ui.md).</span></span> <span data-ttu-id="b4b41-110">Accédez trop[http://app.sysdigcloud.com](http://app.sysdigcloud.com) tooset d’un compte de cloud Sysdig.</span><span class="sxs-lookup"><span data-stu-id="b4b41-110">Go too[http://app.sysdigcloud.com](http://app.sysdigcloud.com) tooset up a Sysdig cloud account.</span></span> 

## <a name="sysdig"></a><span data-ttu-id="b4b41-111">Sysdig</span><span class="sxs-lookup"><span data-stu-id="b4b41-111">Sysdig</span></span>
<span data-ttu-id="b4b41-112">Sysdig est un service de surveillance qui vous permet de toomonitor vos conteneurs au sein de votre cluster.</span><span class="sxs-lookup"><span data-stu-id="b4b41-112">Sysdig is a monitoring service that allows you toomonitor your containers within your cluster.</span></span> <span data-ttu-id="b4b41-113">Sysdig est connu toohelp résolution des problèmes, mais il a également vos métriques de surveillance de base pour l’UC, la mise en réseau, mémoire et d’e/s.</span><span class="sxs-lookup"><span data-stu-id="b4b41-113">Sysdig is known toohelp with troubleshooting but it also has your basic monitoring metrics for CPU, Networking, Memory, and I/O.</span></span> <span data-ttu-id="b4b41-114">Sysdig rend toosee facile, utilisez les conteneurs plus difficiles ou essentiellement à l’aide de hello hello mémoire et processeur.</span><span class="sxs-lookup"><span data-stu-id="b4b41-114">Sysdig makes it easy toosee which containers are working hello hardest or essentially using hello most memory and CPU.</span></span> <span data-ttu-id="b4b41-115">Cette vue est dans la section « Présentation », ce qui est actuellement en version bêta de hello.</span><span class="sxs-lookup"><span data-stu-id="b4b41-115">This view is in hello “Overview” section, which is currently in beta.</span></span> 

![IU Sysdig](./media/container-service-monitoring-sysdig/sysdig6.png) 

## <a name="configure-a-sysdig-deployment-with-marathon"></a><span data-ttu-id="b4b41-117">Configurer un déploiement Sysdig avec Marathon</span><span class="sxs-lookup"><span data-stu-id="b4b41-117">Configure a Sysdig deployment with Marathon</span></span>
<span data-ttu-id="b4b41-118">Ces étapes vous indiquent comment tooconfigure et de déploiement Sysdig applications tooyour cluster avec Marathon.</span><span class="sxs-lookup"><span data-stu-id="b4b41-118">These steps will show you how tooconfigure and deploy Sysdig applications tooyour cluster with Marathon.</span></span> 

<span data-ttu-id="b4b41-119">Accéder à votre interface utilisateur de contrôleur de domaine/système d’exploitation via [http://localhost : 80 /](http://localhost:80/) qu’une seule fois dans l’interface utilisateur du contrôleur de domaine/système d’exploitation de hello accédez toohello « Univers », qui se trouve sur hello inférieur gauche, puis recherchez « Sysdig ».</span><span class="sxs-lookup"><span data-stu-id="b4b41-119">Access your DC/OS UI via [http://localhost:80/](http://localhost:80/) Once in hello DC/OS UI navigate toohello "Universe", which is on hello bottom left and then search for "Sysdig."</span></span>

![Sysdig dans l’Univers DC/OS](./media/container-service-monitoring-sysdig/sysdig1.png)

<span data-ttu-id="b4b41-121">Maintenant les configuration hello toocomplete vous avez besoin d’un Sysdig cloud compte ou un compte d’évaluation gratuit.</span><span class="sxs-lookup"><span data-stu-id="b4b41-121">Now toocomplete hello configuration you need a Sysdig cloud account or a free trial account.</span></span> <span data-ttu-id="b4b41-122">Une fois que vous êtes connecté dans le site Web du cloud toohello Sysdig, cliquez sur votre nom d’utilisateur et sur la page de hello, vous devez voir votre « clé d’accès ».</span><span class="sxs-lookup"><span data-stu-id="b4b41-122">Once you're logged in toohello Sysdig cloud website, click on your user name, and on hello page you should see your "Access Key."</span></span> 

![Clé d’API Sysdig](./media/container-service-monitoring-sysdig/sysdig2.png) 

<span data-ttu-id="b4b41-124">Ensuite, entrez votre clé d’accès à la configuration Sysdig hello dans hello univers du contrôleur de domaine/système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="b4b41-124">Next enter your Access Key into hello Sysdig configuration within hello DC/OS Universe.</span></span> 

![Configuration Sysdig Bonjour univers du contrôleur de domaine/système d’exploitation](./media/container-service-monitoring-sysdig/sysdig3.png)

<span data-ttu-id="b4b41-126">Maintenant défini hello instances too10000000 afin que chaque fois qu’un nouveau nœud est ajouté le cluster toohello Sysdig déploiera automatiquement un agent toothat nouveau nœud.</span><span class="sxs-lookup"><span data-stu-id="b4b41-126">Now set hello instances too10000000 so whenever a new node is added toohello cluster Sysdig will automatically deploy an agent toothat new node.</span></span> <span data-ttu-id="b4b41-127">Il s’agit d’une solution intermédiaire de toomake assurer que sysdig se déploiera tooall nouveaux agents dans un cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="b4b41-127">This is an interim solution toomake sure Sysdig will deploy tooall new agents within hello cluster.</span></span> 

![Configuration Sysdig Bonjour contrôleur de domaine, le système d’exploitation univers-les instances](./media/container-service-monitoring-sysdig/sysdig4.png)

<span data-ttu-id="b4b41-129">Une fois que vous avez installé le package de hello accédez arrière toohello Sysdig UI et vous pourrez tooexplore en mesure de métriques de l’utilisation de différents hello pour les conteneurs de hello dans votre cluster.</span><span class="sxs-lookup"><span data-stu-id="b4b41-129">Once you've installed hello package navigate back toohello Sysdig UI and you'll be able tooexplore hello different usage metrics for hello containers within your cluster.</span></span> 

<span data-ttu-id="b4b41-130">Vous pouvez également installer des tableaux de bords spécifiques de Mesos et Marathon en utilisant [l’Assistant Nouveau tableau de bord](https://app.sysdigcloud.com/#/dashboards/new).</span><span class="sxs-lookup"><span data-stu-id="b4b41-130">You can also install Mesos and Marathon specific dashboards via the [new dashboard wizard](https://app.sysdigcloud.com/#/dashboards/new).</span></span>
