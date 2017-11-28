---
title: "pools d’agents aaaDC/système d’exploitation pour le Service de conteneur Azure | Documents Microsoft"
description: "Fonctionnement des pools d’agents publics et privés de hello avec un cluster du Service de conteneur Azure DC/OS"
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
ms.openlocfilehash: c7d3889db07cb9908e8b68b668bd8a14ef3c2552
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="dcos-agent-pools-for-azure-container-service"></a><span data-ttu-id="a92df-104">Pools d’agents DC/OS pour Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="a92df-104">DC/OS agent pools for Azure Container Service</span></span>
<span data-ttu-id="a92df-105">Des clusters DC/OS d’Azure Container Service contiennent des nœuds d’agent dans deux pools, un pool public et un pool privé.</span><span class="sxs-lookup"><span data-stu-id="a92df-105">DC/OS clusters in Azure Container Service contain agent nodes in two pools, a public pool and a private pool.</span></span> <span data-ttu-id="a92df-106">Une application peut être déployée pool tooeither, affecter l’accessibilité entre des ordinateurs dans votre service de conteneur.</span><span class="sxs-lookup"><span data-stu-id="a92df-106">An application can be deployed tooeither pool, affecting accessibility between machines in your container service.</span></span> <span data-ttu-id="a92df-107">Hello machines peuvent être exposé toohello internet (public) ou interne (privé) à conserver.</span><span class="sxs-lookup"><span data-stu-id="a92df-107">hello machines can be exposed toohello internet (public) or kept internal (private).</span></span> <span data-ttu-id="a92df-108">Cet article explique brièvement pourquoi il existe des pools publics et privés.</span><span class="sxs-lookup"><span data-stu-id="a92df-108">This article gives a brief overview of why there are public and private pools.</span></span>


* <span data-ttu-id="a92df-109">**Agents privés** : les nœuds d’un agent privé sont exécutés via un réseau non routable.</span><span class="sxs-lookup"><span data-stu-id="a92df-109">**Private agents**: Private agent nodes run through a non-routable network.</span></span> <span data-ttu-id="a92df-110">Ce réseau est accessible uniquement à partir de la zone d’administration hello ou via un routeur de périphérie hello zone publique.</span><span class="sxs-lookup"><span data-stu-id="a92df-110">This network is only accessible from hello admin zone or through hello public zone edge router.</span></span> <span data-ttu-id="a92df-111">Par défaut, DC/OS lance les applications sur les nœuds de l’agent privé.</span><span class="sxs-lookup"><span data-stu-id="a92df-111">By default, DC/OS launches apps on private agent nodes.</span></span> 

* <span data-ttu-id="a92df-112">**Agents publics** : les nœuds d’un agent public exécutent des services et des applications DC/OS sur un réseau accessible publiquement.</span><span class="sxs-lookup"><span data-stu-id="a92df-112">**Public agents**: Public agent nodes run DC/OS apps and services through a publicly accessible network.</span></span> 

<span data-ttu-id="a92df-113">Pour plus d’informations sur la sécurité de réseau de contrôleur de domaine/système d’exploitation, consultez hello [documentation du contrôleur de domaine/système d’exploitation](https://dcos.io/docs/1.7/administration/securing-your-cluster/).</span><span class="sxs-lookup"><span data-stu-id="a92df-113">For more information about DC/OS network security, see hello [DC/OS documentation](https://dcos.io/docs/1.7/administration/securing-your-cluster/).</span></span>

## <a name="deploy-agent-pools"></a><span data-ttu-id="a92df-114">Déploiement de pools d’agents</span><span class="sxs-lookup"><span data-stu-id="a92df-114">Deploy agent pools</span></span>

<span data-ttu-id="a92df-115">pools d’agents Hello/OS du contrôleur de domaine dans le Service de conteneur Azure sont créés comme suit :</span><span class="sxs-lookup"><span data-stu-id="a92df-115">hello DC/OS agent pools In Azure Container Service are created as follows:</span></span>

* <span data-ttu-id="a92df-116">Hello **pool privé** contient le numéro hello de nœuds de l’agent que vous spécifiez lorsque vous [déployer le cluster de contrôleur de domaine/système d’exploitation hello](container-service-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="a92df-116">hello **private pool** contains hello number of agent nodes that you specify when you [deploy hello DC/OS cluster](container-service-deployment.md).</span></span> 

* <span data-ttu-id="a92df-117">Hello **public pool** initialement contient un nombre prédéterminé de nœuds de l’agent.</span><span class="sxs-lookup"><span data-stu-id="a92df-117">hello **public pool** initially contains a predetermined number of agent nodes.</span></span> <span data-ttu-id="a92df-118">Ce pool est ajouté automatiquement lors de la configuration de cluster de contrôleur de domaine/système d’exploitation hello.</span><span class="sxs-lookup"><span data-stu-id="a92df-118">This pool is added automatically when hello DC/OS cluster is provisioned.</span></span>

<span data-ttu-id="a92df-119">pool privé de Hello et pool de public de hello sont des machines virtuelles Azure identiques.</span><span class="sxs-lookup"><span data-stu-id="a92df-119">hello private pool and hello public pool are Azure virtual machine scale sets.</span></span> <span data-ttu-id="a92df-120">Vous pouvez redimensionner ces pools après le déploiement.</span><span class="sxs-lookup"><span data-stu-id="a92df-120">You can resize these pools after deployment.</span></span>

## <a name="use-agent-pools"></a><span data-ttu-id="a92df-121">Utilisation de pools d’agents</span><span class="sxs-lookup"><span data-stu-id="a92df-121">Use agent pools</span></span>
<span data-ttu-id="a92df-122">Par défaut, **Marathon** déploie toute nouvelle toohello d’application *privé* des nœuds de l’agent.</span><span class="sxs-lookup"><span data-stu-id="a92df-122">By default, **Marathon** deploys any new application toohello *private* agent nodes.</span></span> <span data-ttu-id="a92df-123">Vous avez tooexplicitly déployer hello application toohello *public* nœuds pendant la création de l’application hello hello.</span><span class="sxs-lookup"><span data-stu-id="a92df-123">You have tooexplicitly deploy hello application toohello *public* nodes during hello creation of hello application.</span></span> <span data-ttu-id="a92df-124">Sélectionnez hello **facultatif** onglet et entrez **slave_public** pour hello **accepté les rôles de ressources** valeur.</span><span class="sxs-lookup"><span data-stu-id="a92df-124">Select hello **Optional** tab and enter **slave_public** for hello **Accepted Resource Roles** value.</span></span> <span data-ttu-id="a92df-125">Ce processus est documenté [ici](container-service-mesos-marathon-ui.md#deploy-a-docker-formatted-container) et Bonjour [DC/OS](https://dcos.io/docs/1.7/administration/installing/custom/create-public-agent/) documentation.</span><span class="sxs-lookup"><span data-stu-id="a92df-125">This process is documented [here](container-service-mesos-marathon-ui.md#deploy-a-docker-formatted-container) and in hello [DC/OS](https://dcos.io/docs/1.7/administration/installing/custom/create-public-agent/) documentation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a92df-126">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a92df-126">Next steps</span></span>
* <span data-ttu-id="a92df-127">En savoir plus sur la [gestion de vos conteneurs DC/OS](container-service-mesos-marathon-ui.md).</span><span class="sxs-lookup"><span data-stu-id="a92df-127">Read more about [managing your DC/OS containers](container-service-mesos-marathon-ui.md).</span></span>

* <span data-ttu-id="a92df-128">Découvrez comment trop[ouvrir le pare-feu hello](container-service-enable-public-access.md) fournie par les conteneurs de contrôleur de domaine/système d’exploitation tooyour tooallow Azure accès public.</span><span class="sxs-lookup"><span data-stu-id="a92df-128">Learn how too[open hello firewall](container-service-enable-public-access.md) provided by Azure tooallow public access tooyour DC/OS containers.</span></span>

