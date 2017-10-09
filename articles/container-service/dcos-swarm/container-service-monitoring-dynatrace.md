---
title: "cluster de contrôleur de domaine/système d’exploitation Azure aaaMonitor - Dynatrace | Documents Microsoft"
description: "Surveillez un cluster DC/OS Azure Container Service avec Dynatrace. Déployer hello Dynatrace OneAgent à l’aide du tableau de bord hello contrôleur de domaine/système d’exploitation."
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
ms.openlocfilehash: 9e2e2d1c8b454422d1db30dac7c385d31d336853
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-dcos-cluster-with-dynatrace-saasmanaged"></a><span data-ttu-id="f1bc0-105">Surveiller un cluster DC/OS Azure Container Service avec Dynatrace SaaS/Managed</span><span class="sxs-lookup"><span data-stu-id="f1bc0-105">Monitor an Azure Container Service DC/OS cluster with Dynatrace SaaS/Managed</span></span>
<span data-ttu-id="f1bc0-106">Dans cet article, nous vous indiquons comment toodeploy hello [Dynatrace](https://www.dynatrace.com/) toomonitor OneAgent tous les hello des nœuds de l’agent de votre cluster de Service de conteneur Azure.</span><span class="sxs-lookup"><span data-stu-id="f1bc0-106">In this article, we show you how toodeploy hello [Dynatrace](https://www.dynatrace.com/) OneAgent toomonitor all hello agent nodes in your Azure Container Service cluster.</span></span> <span data-ttu-id="f1bc0-107">Vous avez besoin d’un compte Dynatrace SaaS/Managé pour cette configuration.</span><span class="sxs-lookup"><span data-stu-id="f1bc0-107">You need an account with Dynatrace SaaS/Managed for this configuration.</span></span> 

## <a name="dynatrace-saasmanaged"></a><span data-ttu-id="f1bc0-108">Dynatrace SaaS/Managé</span><span class="sxs-lookup"><span data-stu-id="f1bc0-108">Dynatrace SaaS/Managed</span></span>
<span data-ttu-id="f1bc0-109">Dynatrace est une solution de surveillance cloud native pour environnements de clusters et de conteneurs hautement dynamiques.</span><span class="sxs-lookup"><span data-stu-id="f1bc0-109">Dynatrace is a cloud-native monitoring solution for highly dynamic container and cluster environments.</span></span> <span data-ttu-id="f1bc0-110">Il vous permet de toobetter optimiser vos déploiements de conteneur et les allocations de mémoire à l’aide des données d’utilisation en temps réel.</span><span class="sxs-lookup"><span data-stu-id="f1bc0-110">It allows you toobetter optimize your container deployments and memory allocations by using real-time usage data.</span></span> <span data-ttu-id="f1bc0-111">Elle est capable d’identifier automatiquement les problèmes d’infrastructure et d’applications en fournissant une planification automatisée, une corrélation des problèmes et une détection des causes racines.</span><span class="sxs-lookup"><span data-stu-id="f1bc0-111">It is capable of automatically pinpointing application and infrastructure issues by providing automated baselining, problem correlation, and root-cause detection.</span></span>

<span data-ttu-id="f1bc0-112">la figure suivant de Hello affiche hello Dynatrace UI :</span><span class="sxs-lookup"><span data-stu-id="f1bc0-112">hello following figure shows hello Dynatrace UI:</span></span>

![IU de Dynatrace](./media/container-service-monitoring-dynatrace/dynatrace.png)

## <a name="prerequisites"></a><span data-ttu-id="f1bc0-114">Composants requis</span><span class="sxs-lookup"><span data-stu-id="f1bc0-114">Prerequisites</span></span> 
<span data-ttu-id="f1bc0-115">[Déployer](container-service-deployment.md) et [connecter](./../container-service-connect.md) cluster tooa configuré par le Service de conteneur Azure.</span><span class="sxs-lookup"><span data-stu-id="f1bc0-115">[Deploy](container-service-deployment.md) and [connect](./../container-service-connect.md) tooa cluster configured by Azure Container Service.</span></span> <span data-ttu-id="f1bc0-116">Explorer hello [Marathon UI](container-service-mesos-marathon-ui.md).</span><span class="sxs-lookup"><span data-stu-id="f1bc0-116">Explore hello [Marathon UI](container-service-mesos-marathon-ui.md).</span></span> <span data-ttu-id="f1bc0-117">Accédez trop[https://www.dynatrace.com/trial/](https://www.dynatrace.com/trial/) tooset d’un compte Dynatrace SaaS.</span><span class="sxs-lookup"><span data-stu-id="f1bc0-117">Go too[https://www.dynatrace.com/trial/](https://www.dynatrace.com/trial/) tooset up a Dynatrace SaaS account.</span></span>  

## <a name="configure-a-dynatrace-deployment-with-marathon"></a><span data-ttu-id="f1bc0-118">Configurer un déploiement Dynatrace avec Marathon</span><span class="sxs-lookup"><span data-stu-id="f1bc0-118">Configure a Dynatrace deployment with Marathon</span></span>
<span data-ttu-id="f1bc0-119">Ces étapes vous montrent comment tooconfigure et de déploiement Dynatrace applications tooyour cluster avec Marathon.</span><span class="sxs-lookup"><span data-stu-id="f1bc0-119">These steps show you how tooconfigure and deploy Dynatrace applications tooyour cluster with Marathon.</span></span>

1. <span data-ttu-id="f1bc0-120">Accédez à l'interface utilisateur de votre contrôleur de domaine/système d’exploitation via [http://localhost:80/](http://localhost:80/).</span><span class="sxs-lookup"><span data-stu-id="f1bc0-120">Access your DC/OS UI via [http://localhost:80/](http://localhost:80/).</span></span> <span data-ttu-id="f1bc0-121">Une fois dans l’interface utilisateur du contrôleur de domaine/système d’exploitation de hello, accédez toohello **univers** onglet, puis recherchez **Dynatrace**.</span><span class="sxs-lookup"><span data-stu-id="f1bc0-121">Once in hello DC/OS UI, navigate toohello **Universe** tab and then search for **Dynatrace**.</span></span>

    ![Dynatrace dans l’Univers DC/OS](./media/container-service-monitoring-dynatrace/dynatrace-universe.png)

2. <span data-ttu-id="f1bc0-123">configuration de hello toocomplete, vous devez un compte Dynatrace SaaS ou un compte d’évaluation gratuit.</span><span class="sxs-lookup"><span data-stu-id="f1bc0-123">toocomplete hello configuration, you need a Dynatrace SaaS account or a free trial account.</span></span> <span data-ttu-id="f1bc0-124">Une fois que vous ouvrez une session dans le tableau de bord Dynatrace hello, sélectionnez **Dynatrace de déployer**.</span><span class="sxs-lookup"><span data-stu-id="f1bc0-124">Once you log into hello Dynatrace dashboard, select **Deploy Dynatrace**.</span></span>

    ![Configurer l’intégration PaaS Dynatrace](./media/container-service-monitoring-dynatrace/setup-paas.png)

3. <span data-ttu-id="f1bc0-126">Sur la page de hello, sélectionnez **configurer l’intégration de PaaS**.</span><span class="sxs-lookup"><span data-stu-id="f1bc0-126">On hello page, select **Set up PaaS integration**.</span></span> 

    ![Jeton API Dynatrace](./media/container-service-monitoring-dynatrace/api-token.png) 

4. <span data-ttu-id="f1bc0-128">Entrez votre jeton d’API dans hello configuration Dynatrace OneAgent dans hello univers du contrôleur de domaine/système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="f1bc0-128">Enter your API token into hello Dynatrace OneAgent configuration within hello DC/OS Universe.</span></span> 

    ![Configuration de dynaTrace OneAgent Bonjour univers du contrôleur de domaine/système d’exploitation](./media/container-service-monitoring-dynatrace/dynatrace-config.png)

5. <span data-ttu-id="f1bc0-130">Définir des instances de hello toohello nombre de nœuds vous avez l’intention de toorun.</span><span class="sxs-lookup"><span data-stu-id="f1bc0-130">Set hello instances toohello number of nodes you intend toorun.</span></span> <span data-ttu-id="f1bc0-131">Définir un nombre plus élevé d’également fonctionne, mais contrôleur de domaine/système d’exploitation renouvellement des tentatives toofind nouvelles instances jusqu'à ce que ce nombre est atteint réellement.</span><span class="sxs-lookup"><span data-stu-id="f1bc0-131">Setting a higher number also works, but DC/OS will keep trying toofind new instances until that number is actually reached.</span></span> <span data-ttu-id="f1bc0-132">Si vous préférez, vous pouvez également définir cette valeur tooa comme 1000000.</span><span class="sxs-lookup"><span data-stu-id="f1bc0-132">If you prefer, you can also set this tooa value like 1000000.</span></span> <span data-ttu-id="f1bc0-133">Dans ce cas, chaque fois qu’un nouveau nœud est ajouté toohello cluster, Dynatrace déploie automatiquement un agent toothat nouveau nœud, à prix hello du contrôleur de domaine/système d’exploitation en permanence la tentative de toodeploy des instances supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="f1bc0-133">In this case, whenever a new node is added toohello cluster, Dynatrace automatically deploys an agent toothat new node, at hello price of DC/OS constantly trying toodeploy further instances.</span></span>

    ![Configuration dynaTrace Bonjour contrôleur de domaine, le système d’exploitation univers-les instances](./media/container-service-monitoring-dynatrace/dynatrace-config2.png)

## <a name="next-steps"></a><span data-ttu-id="f1bc0-135">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f1bc0-135">Next steps</span></span>

<span data-ttu-id="f1bc0-136">Une fois que vous avez installé le package de hello, accédez à tableau de bord Dynatrace toohello précédent.</span><span class="sxs-lookup"><span data-stu-id="f1bc0-136">Once you've installed hello package, navigate back toohello Dynatrace dashboard.</span></span> <span data-ttu-id="f1bc0-137">Vous pouvez explorer des métriques d’utilisation différentes hello pour les conteneurs de hello dans votre cluster.</span><span class="sxs-lookup"><span data-stu-id="f1bc0-137">You can explore hello different usage metrics for hello containers within your cluster.</span></span> 
