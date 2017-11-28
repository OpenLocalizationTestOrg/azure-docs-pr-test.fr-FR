---
title: "vue d’ensemble des Instances de conteneurs d’aaaAzure | Documentation Azure"
description: Comprendre Azure Container Instances
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: na
ms.topic: overview
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/20/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: c0662ede1260b15d9841bfc2c3c4cec4c30338d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-container-instances"></a><span data-ttu-id="2aa71-103">Azure Container Instances</span><span class="sxs-lookup"><span data-stu-id="2aa71-103">Azure Container Instances</span></span>

<span data-ttu-id="2aa71-104">Conteneurs devient rapidement toopackage de façon hello préféré, déployer et gérer des applications de cloud.</span><span class="sxs-lookup"><span data-stu-id="2aa71-104">Containers are quickly becoming hello preferred way toopackage, deploy, and manage cloud applications.</span></span> <span data-ttu-id="2aa71-105">Les Instances du conteneur Azure offre hello plus rapide et plus simple façon toorun un conteneur dans Azure, sans avoir à tooprovision toutes les machines virtuelles et sans avoir à tooadopt un service de niveau supérieur.</span><span class="sxs-lookup"><span data-stu-id="2aa71-105">Azure Container Instances offers hello fastest and simplest way toorun a container in Azure, without having tooprovision any virtual machines and without having tooadopt a higher-level service.</span></span> 

<span data-ttu-id="2aa71-106">Azure Container Instances est une excellente solution pour les scénarios qui peuvent fonctionner dans des conteneurs isolés, y compris les applications basiques, automatiser des tâches et créer des travaux.</span><span class="sxs-lookup"><span data-stu-id="2aa71-106">Azure Container Instances is a great solution for any scenario that can operate in isolated containers, including simple applications, task automation, and build jobs.</span></span> <span data-ttu-id="2aa71-107">Pour les scénarios où vous devez disposer d’orchestration de conteneur, y compris de détection du service sur plusieurs conteneurs, la mise à l’échelle automatique et mises à niveau de l’application coordonnée, nous vous recommandons de hello [Service de conteneur Azure](https://docs.microsoft.com/azure/container-service/).</span><span class="sxs-lookup"><span data-stu-id="2aa71-107">For scenarios where you need full container orchestration, including service discovery across multiple containers, automatic scaling, and coordinated application upgrades, we recommend hello [Azure Container Service](https://docs.microsoft.com/azure/container-service/).</span></span>

## <a name="fast-startup-times"></a><span data-ttu-id="2aa71-108">Temps de démarrage rapide</span><span class="sxs-lookup"><span data-stu-id="2aa71-108">Fast startup times</span></span>

<span data-ttu-id="2aa71-109">Le service Containers offre des avantages de démarrage conséquents sur les machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="2aa71-109">Containers offer significant startup benefits over virtual machines.</span></span> <span data-ttu-id="2aa71-110">Avec les Instances du conteneur Azure, vous pouvez démarrer un conteneur dans Azure en quelques secondes sans hello besoin tooprovision et gérer des ordinateurs virtuels.</span><span class="sxs-lookup"><span data-stu-id="2aa71-110">With Azure Container Instances, you can start a container in Azure in seconds without hello need tooprovision and manage VMs.</span></span>

## <a name="hypervisor-level-security"></a><span data-ttu-id="2aa71-111">Sécurité au niveau de l’hyperviseur</span><span class="sxs-lookup"><span data-stu-id="2aa71-111">Hypervisor-level security</span></span>

<span data-ttu-id="2aa71-112">D’un point de vue historique, les conteneurs ont offert l’isolation de dépendance d’application et la gouvernance des ressources, mais n’ont pas été considérés suffisamment renforcés pour une utilisation de plusieurs locataires hostile.</span><span class="sxs-lookup"><span data-stu-id="2aa71-112">Historically, containers have offered application dependency isolation and resource governance but have not been considered sufficiently hardened for hostile multi-tenant usage.</span></span> <span data-ttu-id="2aa71-113">Avec Azure Container Instances, votre application se retrouve aussi isolée dans un conteneur que dans une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="2aa71-113">With Azure Container Instances, your application is as isolated in a container as it would be in a VM.</span></span>

## <a name="custom-sizes"></a><span data-ttu-id="2aa71-114">Tailles personnalisées</span><span class="sxs-lookup"><span data-stu-id="2aa71-114">Custom sizes</span></span>

<span data-ttu-id="2aa71-115">Les conteneurs sont généralement optimisé toorun seulement une application unique, mais besoins hello de ces applications peuvent varier considérablement.</span><span class="sxs-lookup"><span data-stu-id="2aa71-115">Containers are typically optimized toorun just a single application, but hello exact needs of those applications can differ greatly.</span></span> <span data-ttu-id="2aa71-116">Avec Azure Container Instances, vous pouvez demander ce dont vous avez besoin en termes de mémoire et de noyaux processeur.</span><span class="sxs-lookup"><span data-stu-id="2aa71-116">With Azure Container Instances, you can request exactly what you need in terms of CPU cores and memory.</span></span> <span data-ttu-id="2aa71-117">Vous payez en fonction de ce que vous demandez, facturé par hello seconde, afin de pouvoir finement optimiser vos dépenses selon vos besoins.</span><span class="sxs-lookup"><span data-stu-id="2aa71-117">You pay based on what you request, billed by hello second, so you can finely optimize your spending based on your needs.</span></span>

## <a name="public-ip-connectivity"></a><span data-ttu-id="2aa71-118">Connectivité IP publique</span><span class="sxs-lookup"><span data-stu-id="2aa71-118">Public IP connectivity</span></span>

<span data-ttu-id="2aa71-119">Avec les Instances du conteneur Azure, vous pouvez exposer vos conteneurs directement toohello internet avec une adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="2aa71-119">With Azure Container Instances, you can expose your containers directly toohello internet with a public IP address.</span></span> <span data-ttu-id="2aa71-120">Bonjour future, nous sera développez intégration tooinclude fonctionnalités réseau avec des réseaux virtuels, charge équilibrages et autres parties de hello infrastructure de mise en réseau Azure.</span><span class="sxs-lookup"><span data-stu-id="2aa71-120">In hello future, we will expand our networking capabilities tooinclude integration with virtual networks, load balancers, and other core parts of hello Azure networking infrastructure.</span></span>

## <a name="persistent-storage"></a><span data-ttu-id="2aa71-121">Stockage persistant</span><span class="sxs-lookup"><span data-stu-id="2aa71-121">Persistent storage</span></span>

<span data-ttu-id="2aa71-122">tooretrieve et conserver l’état avec les Instances du conteneur Azure, nous proposons des partages de fichiers de montage direct d’Azure.</span><span class="sxs-lookup"><span data-stu-id="2aa71-122">tooretrieve and persist state with Azure Container Instances, we offer direct mounting of Azure files shares.</span></span>

## <a name="linux-and-windows-containers"></a><span data-ttu-id="2aa71-123">Conteneurs Windows et Linux</span><span class="sxs-lookup"><span data-stu-id="2aa71-123">Linux and Windows containers</span></span>

<span data-ttu-id="2aa71-124">Avec les Instances du conteneur Azure, vous pouvez planifier des fenêtres et les conteneurs Linux avec hello même API.</span><span class="sxs-lookup"><span data-stu-id="2aa71-124">With Azure Container Instances, you can schedule both Windows and Linux containers with hello same API.</span></span> <span data-ttu-id="2aa71-125">Indiquent simplement le type de système d’exploitation de base hello et tout le reste est identique.</span><span class="sxs-lookup"><span data-stu-id="2aa71-125">Simply indicate hello base OS type and everything else is identical.</span></span>

## <a name="co-scheduled-groups"></a><span data-ttu-id="2aa71-126">Groupes co-planifiés</span><span class="sxs-lookup"><span data-stu-id="2aa71-126">Co-scheduled groups</span></span>

<span data-ttu-id="2aa71-127">Azure Container Instances prend en charge la planification de groupes de plusieurs conteneurs qui partagent un même hôte, réseau local, stockage et cycle de vie.</span><span class="sxs-lookup"><span data-stu-id="2aa71-127">Azure Container Instances supports scheduling of multi-container groups that share a host machine, local network, storage, and lifecycle.</span></span> <span data-ttu-id="2aa71-128">Cela permet de vous toocombine votre application principale avec d’autres utilisateurs dans un rôle de prise en charge, tel que la journalisation.</span><span class="sxs-lookup"><span data-stu-id="2aa71-128">This enables you toocombine your main application with others acting in a supporting role, such as logging.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2aa71-129">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2aa71-129">Next steps</span></span>

<span data-ttu-id="2aa71-130">Essayez de déployer un tooAzure conteneur avec une seule commande à l’aide de notre [guide de démarrage rapide](container-instances-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="2aa71-130">Try deploying a container tooAzure with a single command using our [quickstart guide](container-instances-quickstart.md).</span></span>
