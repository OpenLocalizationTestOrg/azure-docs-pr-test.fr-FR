---
title: "Pools d’agents DC/OS pour Azure Container Service | Microsoft Docs"
description: "Fonctionnement des pools d’agents publics et privés avec un cluster Azure Container Service DC/OS"
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
ms.date: 01/04/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: da4a196b1a73c78dfff7d8310edcc349b8d10665
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="dcos-agent-pools-for-azure-container-service"></a><span data-ttu-id="d3f0a-104">Pools d’agents DC/OS pour Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="d3f0a-104">DC/OS agent pools for Azure Container Service</span></span>
<span data-ttu-id="d3f0a-105">Des clusters DC/OS d’Azure Container Service contiennent des nœuds d’agent dans deux pools, un pool public et un pool privé.</span><span class="sxs-lookup"><span data-stu-id="d3f0a-105">DC/OS clusters in Azure Container Service contain agent nodes in two pools, a public pool and a private pool.</span></span> <span data-ttu-id="d3f0a-106">Une application peut être déployée dans un pool, ce qui affecte l’accessibilité entre les machines de votre service de conteneur.</span><span class="sxs-lookup"><span data-stu-id="d3f0a-106">An application can be deployed to either pool, affecting accessibility between machines in your container service.</span></span> <span data-ttu-id="d3f0a-107">Les machines peuvent être exposées à internet (publiques) ou conservées en interne (privées).</span><span class="sxs-lookup"><span data-stu-id="d3f0a-107">The machines can be exposed to the internet (public) or kept internal (private).</span></span> <span data-ttu-id="d3f0a-108">Cet article explique brièvement pourquoi il existe des pools publics et privés.</span><span class="sxs-lookup"><span data-stu-id="d3f0a-108">This article gives a brief overview of why there are public and private pools.</span></span>


* <span data-ttu-id="d3f0a-109">**Agents privés** : les nœuds d’un agent privé sont exécutés via un réseau non routable.</span><span class="sxs-lookup"><span data-stu-id="d3f0a-109">**Private agents**: Private agent nodes run through a non-routable network.</span></span> <span data-ttu-id="d3f0a-110">Ce réseau n’est accessible qu’à partir de la zone administrateur ou par le biais du routeur Edge de la zone publique.</span><span class="sxs-lookup"><span data-stu-id="d3f0a-110">This network is only accessible from the admin zone or through the public zone edge router.</span></span> <span data-ttu-id="d3f0a-111">Par défaut, DC/OS lance les applications sur les nœuds de l’agent privé.</span><span class="sxs-lookup"><span data-stu-id="d3f0a-111">By default, DC/OS launches apps on private agent nodes.</span></span> 

* <span data-ttu-id="d3f0a-112">**Agents publics** : les nœuds d’un agent public exécutent des services et des applications DC/OS sur un réseau accessible publiquement.</span><span class="sxs-lookup"><span data-stu-id="d3f0a-112">**Public agents**: Public agent nodes run DC/OS apps and services through a publicly accessible network.</span></span> 

<span data-ttu-id="d3f0a-113">Pour plus d’informations sur la sécurité réseau DC/OS, consultez la [documentation DC/OS](https://dcos.io/docs/1.7/administration/securing-your-cluster/) .</span><span class="sxs-lookup"><span data-stu-id="d3f0a-113">For more information about DC/OS network security, see the [DC/OS documentation](https://dcos.io/docs/1.7/administration/securing-your-cluster/).</span></span>

## <a name="deploy-agent-pools"></a><span data-ttu-id="d3f0a-114">Déploiement de pools d’agents</span><span class="sxs-lookup"><span data-stu-id="d3f0a-114">Deploy agent pools</span></span>

<span data-ttu-id="d3f0a-115">Les pools d’agents DC/OS d’Azure Container Service sont créés comme suit :</span><span class="sxs-lookup"><span data-stu-id="d3f0a-115">The DC/OS agent pools In Azure Container Service are created as follows:</span></span>

* <span data-ttu-id="d3f0a-116">Le **pool privé** contient le nombre de nœuds d’agent que vous spécifiez lorsque vous [déployez le cluster DC/OS](container-service-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="d3f0a-116">The **private pool** contains the number of agent nodes that you specify when you [deploy the DC/OS cluster](container-service-deployment.md).</span></span> 

* <span data-ttu-id="d3f0a-117">Le **pool public** contient initialement un nombre prédéterminé de nœuds d’agent.</span><span class="sxs-lookup"><span data-stu-id="d3f0a-117">The **public pool** initially contains a predetermined number of agent nodes.</span></span> <span data-ttu-id="d3f0a-118">Ce pool est automatiquement ajouté lorsque le cluster DC/OS est approvisionné.</span><span class="sxs-lookup"><span data-stu-id="d3f0a-118">This pool is added automatically when the DC/OS cluster is provisioned.</span></span>

<span data-ttu-id="d3f0a-119">Le pool privé et le pool public sont des groupes de machines virtuelles Azure identiques.</span><span class="sxs-lookup"><span data-stu-id="d3f0a-119">The private pool and the public pool are Azure virtual machine scale sets.</span></span> <span data-ttu-id="d3f0a-120">Vous pouvez redimensionner ces pools après le déploiement.</span><span class="sxs-lookup"><span data-stu-id="d3f0a-120">You can resize these pools after deployment.</span></span>

## <a name="use-agent-pools"></a><span data-ttu-id="d3f0a-121">Utilisation de pools d’agents</span><span class="sxs-lookup"><span data-stu-id="d3f0a-121">Use agent pools</span></span>
<span data-ttu-id="d3f0a-122">Par défaut, **Marathon** déploie toute nouvelle application sur les nœuds de l’agent *privé* .</span><span class="sxs-lookup"><span data-stu-id="d3f0a-122">By default, **Marathon** deploys any new application to the *private* agent nodes.</span></span> <span data-ttu-id="d3f0a-123">Vous devez déployer explicitement l’application sur les nœuds *publics* pendant la création de l’application.</span><span class="sxs-lookup"><span data-stu-id="d3f0a-123">You have to explicitly deploy the application to the *public* nodes during the creation of the application.</span></span> <span data-ttu-id="d3f0a-124">Sélectionnez l’onglet **Facultatif** et saisissez **slave_public** pour la valeur **Rôles de ressources acceptés**.</span><span class="sxs-lookup"><span data-stu-id="d3f0a-124">Select the **Optional** tab and enter **slave_public** for the **Accepted Resource Roles** value.</span></span> <span data-ttu-id="d3f0a-125">Ce processus est décrit [ici](container-service-mesos-marathon-ui.md#deploy-a-docker-formatted-container) et dans la documentation [DC/OS](https://dcos.io/docs/1.7/administration/installing/custom/create-public-agent/).</span><span class="sxs-lookup"><span data-stu-id="d3f0a-125">This process is documented [here](container-service-mesos-marathon-ui.md#deploy-a-docker-formatted-container) and in the [DC/OS](https://dcos.io/docs/1.7/administration/installing/custom/create-public-agent/) documentation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d3f0a-126">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d3f0a-126">Next steps</span></span>
* <span data-ttu-id="d3f0a-127">En savoir plus sur la [gestion de vos conteneurs DC/OS](container-service-mesos-marathon-ui.md).</span><span class="sxs-lookup"><span data-stu-id="d3f0a-127">Read more about [managing your DC/OS containers](container-service-mesos-marathon-ui.md).</span></span>

* <span data-ttu-id="d3f0a-128">Découvrez comment [ouvrir le pare-feu](container-service-enable-public-access.md) fourni par Azure pour autoriser l’accès public à vos conteneurs DC/OS.</span><span class="sxs-lookup"><span data-stu-id="d3f0a-128">Learn how to [open the firewall](container-service-enable-public-access.md) provided by Azure to allow public access to your DC/OS containers.</span></span>

