---
title: aaaContainer solution de surveillance dans Azure journal Analytique | Documents Microsoft
description: "Hello solution d’analyse de conteneur dans le journal Analytique vous aide à afficher et gérer vos Docker et les fenêtres hôtes de conteneur dans un emplacement unique."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: e1e4b52b-92d5-4bfa-8a09-ff8c6b5a9f78
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: magoedte;banders
ms.openlocfilehash: 2eed1dd81c22faef78a375fca3ebece9e5300c09
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="container-monitoring-solution-in-log-analytics"></a><span data-ttu-id="c8a0c-103">Solution Container Monitoring dans Log Analytics</span><span class="sxs-lookup"><span data-stu-id="c8a0c-103">Container Monitoring solution in Log Analytics</span></span>

![Symbole Containers](./media/log-analytics-containers/containers-symbol.png)

<span data-ttu-id="c8a0c-105">Cet article décrit comment tooset configuration et utilisation hello solution d’analyse de conteneur dans le journal Analytique, ce qui vous permet d’afficher et gérer vos Docker et les fenêtres hôtes de conteneur dans un emplacement unique.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-105">This article describes how tooset up and use hello Container Monitoring solution in Log Analytics, which helps you view and manage your Docker and Windows container hosts in a single location.</span></span> <span data-ttu-id="c8a0c-106">Docker est un système logiciel de virtualisation utilisée conteneurs toocreate qui automatisent tootheir de déploiement de logiciel informatique infrastructure.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-106">Docker is a software virtualization system used toocreate containers that automate software deployment tootheir IT infrastructure.</span></span>

<span data-ttu-id="c8a0c-107">Hello solution montre quels conteneurs sont en cours d’exécution, image de conteneur qu’ils s’exécutent, et où les conteneurs sont en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-107">hello solution shows which containers are running, what container image they’re running, and where containers are running.</span></span> <span data-ttu-id="c8a0c-108">Vous pouvez afficher des informations d’audit détaillées montrant les commandes utilisées avec les conteneurs.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-108">You can view detailed audit information showing commands used with containers.</span></span> <span data-ttu-id="c8a0c-109">Et, vous pouvez résoudre les conteneurs en affichant et en recherche de journaux centralisées sans avoir tooremotely vue Docker ou des hôtes Windows.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-109">And, you can troubleshoot containers by viewing and searching centralized logs without having tooremotely view Docker or Windows hosts.</span></span> <span data-ttu-id="c8a0c-110">Vous pouvez rechercher des conteneurs bruyants et consommant des ressources excessives sur un ordinateur hôte.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-110">You can find containers that may be noisy and consuming excess resources on a host.</span></span> <span data-ttu-id="c8a0c-111">Et vous pouvez consulter des informations centralisées sur le processeur, la mémoire, le stockage ainsi que l’utilisation et les performances du réseau.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-111">And, you can view centralized CPU, memory, storage, and network usage and performance information for containers.</span></span> <span data-ttu-id="c8a0c-112">Sur les ordinateurs exécutant Windows, vous pouvez centraliser et comparer les journaux des conteneurs Windows Server, Hyper-V et Docker.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-112">On computers running Windows, you can centralize and compare logs from Windows Server, Hyper-V, and Docker containers.</span></span> <span data-ttu-id="c8a0c-113">solution de Hello prend en charge hello suivant orchestrators de conteneur :</span><span class="sxs-lookup"><span data-stu-id="c8a0c-113">hello solution supports hello following container orchestrators:</span></span>

- <span data-ttu-id="c8a0c-114">Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="c8a0c-114">Docker Swarm</span></span>
- <span data-ttu-id="c8a0c-115">DC/OS</span><span class="sxs-lookup"><span data-stu-id="c8a0c-115">DC/OS</span></span>
- <span data-ttu-id="c8a0c-116">kubernetes</span><span class="sxs-lookup"><span data-stu-id="c8a0c-116">Kubernetes</span></span>
- <span data-ttu-id="c8a0c-117">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="c8a0c-117">Service Fabric</span></span>
- <span data-ttu-id="c8a0c-118">Red Hat OpenShift</span><span class="sxs-lookup"><span data-stu-id="c8a0c-118">Red Hat OpenShift</span></span>


<span data-ttu-id="c8a0c-119">Hello diagramme suivant montre les relations entre différents hôtes de conteneurs et les agents OMS hello.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-119">hello following diagram shows hello relationships between various container hosts and agents with OMS.</span></span>

![Schéma des conteneurs](./media/log-analytics-containers/containers-diagram.png)

## <a name="system-requirements"></a><span data-ttu-id="c8a0c-121">Conditions requises pour le système</span><span class="sxs-lookup"><span data-stu-id="c8a0c-121">System requirements</span></span>

<span data-ttu-id="c8a0c-122">Avant de commencer, passez en revue hello suivant tooverify détails préalables hello.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-122">Before starting, review hello following details tooverify you meet hello prerequisites.</span></span>

### <a name="container-monitoring-solution-support-for-docker-orchestrator-and-os-platform"></a><span data-ttu-id="c8a0c-123">Prise en charge de solution de surveillance de conteneur pour la plateforme Docker Orchestrator et celle du système d’exploitation</span><span class="sxs-lookup"><span data-stu-id="c8a0c-123">Container monitoring solution support for Docker Orchestrator and OS platform</span></span>
<span data-ttu-id="c8a0c-124">Hello tableau suivant indique hello orchestration de Docker et le système d’exploitation prise en charge de l’inventaire de conteneur, les performances et les journaux avec Analytique de journal d’analyse.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-124">hello following table outlines hello Docker orchestration and operating system monitoring support of container inventory, performance, and logs with Log Analytics.</span></span>   

| | <span data-ttu-id="c8a0c-125">ACS</span><span class="sxs-lookup"><span data-stu-id="c8a0c-125">ACS</span></span> | <span data-ttu-id="c8a0c-126">Linux</span><span class="sxs-lookup"><span data-stu-id="c8a0c-126">Linux</span></span> | <span data-ttu-id="c8a0c-127">Windows</span><span class="sxs-lookup"><span data-stu-id="c8a0c-127">Windows</span></span> | <span data-ttu-id="c8a0c-128">Conteneur</span><span class="sxs-lookup"><span data-stu-id="c8a0c-128">Container</span></span><br><span data-ttu-id="c8a0c-129">Inventaire</span><span class="sxs-lookup"><span data-stu-id="c8a0c-129">Inventory</span></span> | <span data-ttu-id="c8a0c-130">Image</span><span class="sxs-lookup"><span data-stu-id="c8a0c-130">Image</span></span><br><span data-ttu-id="c8a0c-131">Inventaire</span><span class="sxs-lookup"><span data-stu-id="c8a0c-131">Inventory</span></span> | <span data-ttu-id="c8a0c-132">Nœud</span><span class="sxs-lookup"><span data-stu-id="c8a0c-132">Node</span></span><br><span data-ttu-id="c8a0c-133">Inventaire</span><span class="sxs-lookup"><span data-stu-id="c8a0c-133">Inventory</span></span> | <span data-ttu-id="c8a0c-134">Conteneur</span><span class="sxs-lookup"><span data-stu-id="c8a0c-134">Container</span></span><br><span data-ttu-id="c8a0c-135">Performances</span><span class="sxs-lookup"><span data-stu-id="c8a0c-135">Performance</span></span> | <span data-ttu-id="c8a0c-136">Conteneur</span><span class="sxs-lookup"><span data-stu-id="c8a0c-136">Container</span></span><br><span data-ttu-id="c8a0c-137">Événement</span><span class="sxs-lookup"><span data-stu-id="c8a0c-137">Event</span></span> | <span data-ttu-id="c8a0c-138">Événement</span><span class="sxs-lookup"><span data-stu-id="c8a0c-138">Event</span></span><br><span data-ttu-id="c8a0c-139">Journal</span><span class="sxs-lookup"><span data-stu-id="c8a0c-139">Log</span></span> | <span data-ttu-id="c8a0c-140">Conteneur</span><span class="sxs-lookup"><span data-stu-id="c8a0c-140">Container</span></span><br><span data-ttu-id="c8a0c-141">Journal</span><span class="sxs-lookup"><span data-stu-id="c8a0c-141">Log</span></span> |
|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|
| <span data-ttu-id="c8a0c-142">kubernetes</span><span class="sxs-lookup"><span data-stu-id="c8a0c-142">Kubernetes</span></span> | <span data-ttu-id="c8a0c-143">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c8a0c-143">&#8226;</span></span> | <span data-ttu-id="c8a0c-144">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c8a0c-144">&#8226;</span></span> | | <span data-ttu-id="c8a0c-145">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c8a0c-145">&#8226;</span></span> | <span data-ttu-id="c8a0c-146">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c8a0c-146">&#8226;</span></span> | <span data-ttu-id="c8a0c-147">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c8a0c-147">&#8226;</span></span> | <span data-ttu-id="c8a0c-148">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c8a0c-148">&#8226;</span></span> | <span data-ttu-id="c8a0c-149">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c8a0c-149">&#8226;</span></span> | <span data-ttu-id="c8a0c-150">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c8a0c-150">&#8226;</span></span> | <span data-ttu-id="c8a0c-151">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c8a0c-151">&#8226;</span></span> |
| <span data-ttu-id="c8a0c-152">Mésosphère</span><span class="sxs-lookup"><span data-stu-id="c8a0c-152">Mesosphere</span></span><br><span data-ttu-id="c8a0c-153">DC/OS</span><span class="sxs-lookup"><span data-stu-id="c8a0c-153">DC/OS</span></span> | <span data-ttu-id="c8a0c-154">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c8a0c-154">&#8226;</span></span> | <span data-ttu-id="c8a0c-155">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c8a0c-155">&#8226;</span></span> | | <span data-ttu-id="c8a0c-156">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c8a0c-156">&#8226;</span></span> | <span data-ttu-id="c8a0c-157">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c8a0c-157">&#8226;</span></span> | <span data-ttu-id="c8a0c-158">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c8a0c-158">&#8226;</span></span> | <span data-ttu-id="c8a0c-159">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c8a0c-159">&#8226;</span></span>| <span data-ttu-id="c8a0c-160">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c8a0c-160">&#8226;</span></span> | <span data-ttu-id="c8a0c-161">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c8a0c-161">&#8226;</span></span> | <span data-ttu-id="c8a0c-162">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c8a0c-162">&#8226;</span></span> |
| <span data-ttu-id="c8a0c-163">Docker</span><span class="sxs-lookup"><span data-stu-id="c8a0c-163">Docker</span></span><br><span data-ttu-id="c8a0c-164">Swarm</span><span class="sxs-lookup"><span data-stu-id="c8a0c-164">Swarm</span></span> | <span data-ttu-id="c8a0c-165">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c8a0c-165">&#8226;</span></span> | <span data-ttu-id="c8a0c-166">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c8a0c-166">&#8226;</span></span> | <span data-ttu-id="c8a0c-167">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c8a0c-167">&#8226;</span></span> | <span data-ttu-id="c8a0c-168">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c8a0c-168">&#8226;</span></span> | <span data-ttu-id="c8a0c-169">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c8a0c-169">&#8226;</span></span> | <span data-ttu-id="c8a0c-170">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c8a0c-170">&#8226;</span></span> | <span data-ttu-id="c8a0c-171">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c8a0c-171">&#8226;</span></span> | <span data-ttu-id="c8a0c-172">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c8a0c-172">&#8226;</span></span> | | <span data-ttu-id="c8a0c-173">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c8a0c-173">&#8226;</span></span> |
| <span data-ttu-id="c8a0c-174">Service</span><span class="sxs-lookup"><span data-stu-id="c8a0c-174">Service</span></span><br><span data-ttu-id="c8a0c-175">Structure</span><span class="sxs-lookup"><span data-stu-id="c8a0c-175">Fabric</span></span> | | | <span data-ttu-id="c8a0c-176">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c8a0c-176">&#8226;</span></span> | <span data-ttu-id="c8a0c-177">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c8a0c-177">&#8226;</span></span> | <span data-ttu-id="c8a0c-178">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c8a0c-178">&#8226;</span></span> | <span data-ttu-id="c8a0c-179">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c8a0c-179">&#8226;</span></span> | <span data-ttu-id="c8a0c-180">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c8a0c-180">&#8226;</span></span> | <span data-ttu-id="c8a0c-181">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c8a0c-181">&#8226;</span></span> | <span data-ttu-id="c8a0c-182">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c8a0c-182">&#8226;</span></span> | <span data-ttu-id="c8a0c-183">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c8a0c-183">&#8226;</span></span> |
| <span data-ttu-id="c8a0c-184">Red Hat Open</span><span class="sxs-lookup"><span data-stu-id="c8a0c-184">Red Hat Open</span></span><br><span data-ttu-id="c8a0c-185">Shift</span><span class="sxs-lookup"><span data-stu-id="c8a0c-185">Shift</span></span> | | <span data-ttu-id="c8a0c-186">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c8a0c-186">&#8226;</span></span> | | <span data-ttu-id="c8a0c-187">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c8a0c-187">&#8226;</span></span> | <span data-ttu-id="c8a0c-188">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c8a0c-188">&#8226;</span></span>| <span data-ttu-id="c8a0c-189">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c8a0c-189">&#8226;</span></span> | <span data-ttu-id="c8a0c-190">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c8a0c-190">&#8226;</span></span> | <span data-ttu-id="c8a0c-191">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c8a0c-191">&#8226;</span></span> | | <span data-ttu-id="c8a0c-192">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c8a0c-192">&#8226;</span></span> |
| <span data-ttu-id="c8a0c-193">Windows Server</span><span class="sxs-lookup"><span data-stu-id="c8a0c-193">Windows Server</span></span><br><span data-ttu-id="c8a0c-194">(autonome)</span><span class="sxs-lookup"><span data-stu-id="c8a0c-194">(standalone)</span></span> | | | <span data-ttu-id="c8a0c-195">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c8a0c-195">&#8226;</span></span> | <span data-ttu-id="c8a0c-196">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c8a0c-196">&#8226;</span></span> | <span data-ttu-id="c8a0c-197">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c8a0c-197">&#8226;</span></span> | <span data-ttu-id="c8a0c-198">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c8a0c-198">&#8226;</span></span> | <span data-ttu-id="c8a0c-199">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c8a0c-199">&#8226;</span></span> | <span data-ttu-id="c8a0c-200">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c8a0c-200">&#8226;</span></span> | | <span data-ttu-id="c8a0c-201">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c8a0c-201">&#8226;</span></span> |
| <span data-ttu-id="c8a0c-202">Serveur Linux</span><span class="sxs-lookup"><span data-stu-id="c8a0c-202">Linux Server</span></span><br><span data-ttu-id="c8a0c-203">(autonome)</span><span class="sxs-lookup"><span data-stu-id="c8a0c-203">(standalone)</span></span> | | <span data-ttu-id="c8a0c-204">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c8a0c-204">&#8226;</span></span> | | <span data-ttu-id="c8a0c-205">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c8a0c-205">&#8226;</span></span> | <span data-ttu-id="c8a0c-206">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c8a0c-206">&#8226;</span></span> | <span data-ttu-id="c8a0c-207">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c8a0c-207">&#8226;</span></span> | <span data-ttu-id="c8a0c-208">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c8a0c-208">&#8226;</span></span> | <span data-ttu-id="c8a0c-209">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c8a0c-209">&#8226;</span></span> | | <span data-ttu-id="c8a0c-210">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c8a0c-210">&#8226;</span></span> |


### <a name="docker-versions-supported-on-linux"></a><span data-ttu-id="c8a0c-211">Versions de Docker prises en charge sur Linux</span><span class="sxs-lookup"><span data-stu-id="c8a0c-211">Docker versions supported on Linux</span></span>

- <span data-ttu-id="c8a0c-212">Docker 1.11 too1.13</span><span class="sxs-lookup"><span data-stu-id="c8a0c-212">Docker 1.11 too1.13</span></span>
- <span data-ttu-id="c8a0c-213">Docker CE et EE v17.06</span><span class="sxs-lookup"><span data-stu-id="c8a0c-213">Docker CE and EE v17.06</span></span>

### <a name="x64-linux-distributions-supported-as-container-hosts"></a><span data-ttu-id="c8a0c-214">Distributions Linux x64 suivantes prises en charge en tant qu’hôtes de conteneur</span><span class="sxs-lookup"><span data-stu-id="c8a0c-214">x64 Linux distributions supported as container hosts</span></span>

- <span data-ttu-id="c8a0c-215">Ubuntu 14.04 LTS et 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="c8a0c-215">Ubuntu 14.04 LTS and 16.04 LTS</span></span>
- <span data-ttu-id="c8a0c-216">CoreOS(stable)</span><span class="sxs-lookup"><span data-stu-id="c8a0c-216">CoreOS(stable)</span></span>
- <span data-ttu-id="c8a0c-217">Amazon Linux 2016.09.0</span><span class="sxs-lookup"><span data-stu-id="c8a0c-217">Amazon Linux 2016.09.0</span></span>
- <span data-ttu-id="c8a0c-218">openSUSE 13.2</span><span class="sxs-lookup"><span data-stu-id="c8a0c-218">openSUSE 13.2</span></span>
- <span data-ttu-id="c8a0c-219">openSUSE LEAP 42.2</span><span class="sxs-lookup"><span data-stu-id="c8a0c-219">openSUSE LEAP 42.2</span></span>
- <span data-ttu-id="c8a0c-220">CentOS 7.2 et 7.3</span><span class="sxs-lookup"><span data-stu-id="c8a0c-220">CentOS 7.2 and 7.3</span></span>
- <span data-ttu-id="c8a0c-221">SLES 12</span><span class="sxs-lookup"><span data-stu-id="c8a0c-221">SLES 12</span></span>
- <span data-ttu-id="c8a0c-222">RHEL 7.2 et 7.3</span><span class="sxs-lookup"><span data-stu-id="c8a0c-222">RHEL 7.2 and 7.3</span></span>
- <span data-ttu-id="c8a0c-223">Red Hat OpenShift Container Platform (OCP) 3.4 et 3.5</span><span class="sxs-lookup"><span data-stu-id="c8a0c-223">Red Hat OpenShift Container Platform (OCP) 3.4 and 3.5</span></span>
- <span data-ttu-id="c8a0c-224">ACS mésosphère DC/OS 1.7.3 too1.8.8</span><span class="sxs-lookup"><span data-stu-id="c8a0c-224">ACS Mesosphere DC/OS 1.7.3 too1.8.8</span></span>
- <span data-ttu-id="c8a0c-225">ACS Kubernetes 1.4.5 too1.6</span><span class="sxs-lookup"><span data-stu-id="c8a0c-225">ACS Kubernetes 1.4.5 too1.6</span></span>
- <span data-ttu-id="c8a0c-226">ACS Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="c8a0c-226">ACS Docker Swarm</span></span>

### <a name="supported-windows-operating-system"></a><span data-ttu-id="c8a0c-227">Système d’exploitation Windows pris en charge</span><span class="sxs-lookup"><span data-stu-id="c8a0c-227">Supported Windows operating system</span></span>

- <span data-ttu-id="c8a0c-228">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="c8a0c-228">Windows Server 2016</span></span>
- <span data-ttu-id="c8a0c-229">Édition Anniversaire Windows 10 (Professionnel ou Entreprise)</span><span class="sxs-lookup"><span data-stu-id="c8a0c-229">Windows 10 Anniversary Edition (Professional or Enterprise)</span></span>

### <a name="docker-versions-supported-on-windows"></a><span data-ttu-id="c8a0c-230">Versions de docker prises en charge sur Windows</span><span class="sxs-lookup"><span data-stu-id="c8a0c-230">Docker versions supported on Windows</span></span>

- <span data-ttu-id="c8a0c-231">Docker 1.12 et 1.13</span><span class="sxs-lookup"><span data-stu-id="c8a0c-231">Docker 1.12 and 1.13</span></span>
- <span data-ttu-id="c8a0c-232">Docker 17.03.0 et versions ultérieures</span><span class="sxs-lookup"><span data-stu-id="c8a0c-232">Docker 17.03.0 and later</span></span>

## <a name="installing-and-configuring-hello-solution"></a><span data-ttu-id="c8a0c-233">L’installation et la configuration de solution de hello</span><span class="sxs-lookup"><span data-stu-id="c8a0c-233">Installing and configuring hello solution</span></span>
<span data-ttu-id="c8a0c-234">Utilisez hello suivant tooinstall des informations et configurer une solution de hello.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-234">Use hello following information tooinstall and configure hello solution.</span></span>

1. <span data-ttu-id="c8a0c-235">Ajouter hello conteneur analyse solution tooyour espace de travail OMS à partir de [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.ContainersOMS?tab=Overview) ou à l’aide de hello est décrite dans [solutions Analytique de journal ajouter à partir de la galerie des Solutions de hello](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="c8a0c-235">Add hello Container Monitoring solution tooyour OMS workspace from [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.ContainersOMS?tab=Overview) or by using hello process described in [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md).</span></span>

2. <span data-ttu-id="c8a0c-236">Installez et utilisez Docker avec un agent OMS.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-236">Install and use Docker with an OMS agent.</span></span>  <span data-ttu-id="c8a0c-237">Selon votre système d’exploitation, vous pouvez choisir parmi hello méthodes suivantes :</span><span class="sxs-lookup"><span data-stu-id="c8a0c-237">Based on your operating system, you can choose from hello following methods:</span></span>

  * <span data-ttu-id="c8a0c-238">Sur les systèmes d’exploitation Linux pris en charge, vous devez installer et exécuter Docker et puis installer et configurer hello [Agent OMS pour Linux](log-analytics-agent-linux.md).</span><span class="sxs-lookup"><span data-stu-id="c8a0c-238">On supported Linux operating systems, install and run Docker and then install and configure hello [OMS Agent for Linux](log-analytics-agent-linux.md).</span></span>  
  * <span data-ttu-id="c8a0c-239">CoreOS, Impossible d’exécuter hello Agent OMS pour Linux.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-239">On CoreOS, you cannot run hello OMS Agent for Linux.</span></span> <span data-ttu-id="c8a0c-240">Au lieu de cela, vous exécutez une version en conteneur Hello Agent OMS pour Linux.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-240">Instead, you run a containerized version of hello OMS Agent for Linux.</span></span> <span data-ttu-id="c8a0c-241">Si vous utilisez des conteneurs dans Azure Government Cloud, consultez les sections relatives aux [hôtes de conteneurs Linux, y compris CoreOS](#for-all-linux-container-hosts-including-coreos) ou aux [hôtes de conteneurs Linux Azure Government, y compris CoreOS](#for-all-azure-government-linux-container-hosts-including-coreos).</span><span class="sxs-lookup"><span data-stu-id="c8a0c-241">Review [Linux container hosts including CoreOS](#for-all-linux-container-hosts-including-coreos) or [Azure Government Linux container hosts including CoreOS](#for-all-azure-government-linux-container-hosts-including-coreos) if you are working with containers in Azure Government Cloud.</span></span>
  * <span data-ttu-id="c8a0c-242">Sur Windows Server 2016 et Windows 10, installez hello moteur Docker et le client, puis se connecter informations toogather agent et l’envoyer tooLog Analytique.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-242">On Windows Server 2016 and Windows 10, install hello Docker Engine and client then connect an agent toogather information and send it tooLog Analytics.</span></span>  

### <a name="container-services"></a><span data-ttu-id="c8a0c-243">Services de conteneur</span><span class="sxs-lookup"><span data-stu-id="c8a0c-243">Container services</span></span>

- <span data-ttu-id="c8a0c-244">Si vous disposez d’un environnement Red Hat OpenShift, consultez [Configurer un agent OMS pour Red Hat OpenShift](#configure-an-oms-agent-for-red-hat-openshift).</span><span class="sxs-lookup"><span data-stu-id="c8a0c-244">If you have a Red Hat OpenShift environment, review [Configure an OMS agent for Red Hat OpenShift](#configure-an-oms-agent-for-red-hat-openshift).</span></span>
- <span data-ttu-id="c8a0c-245">Si vous avez un cluster Kubernetes à l’aide de hello Service de conteneur Azure, consultez [surveiller un cluster du Service de conteneur Azure avec Microsoft Operations Management Suite (OMS)](../container-service/kubernetes/container-service-kubernetes-oms.md).</span><span class="sxs-lookup"><span data-stu-id="c8a0c-245">If you have a Kubernetes cluster using hello Azure Container Service, review [Monitor an Azure Container Service cluster with Microsoft Operations Management Suite (OMS)](../container-service/kubernetes/container-service-kubernetes-oms.md).</span></span>
- <span data-ttu-id="c8a0c-246">Si vous possédez un cluster DC/OS Azure Container Service, consultez l’article [Surveiller un cluster DC/OS Azure Container Service avec Operations Management Suite](../container-service/dcos-swarm/container-service-monitoring-oms.md).</span><span class="sxs-lookup"><span data-stu-id="c8a0c-246">If you have an Azure Container Service DC/OS cluster, learn more at [Monitor an Azure Container Service DC/OS cluster with Operations Management Suite](../container-service/dcos-swarm/container-service-monitoring-oms.md).</span></span>
- <span data-ttu-id="c8a0c-247">Si vous avez un environnement en mode Docker Swarm, apprenez en plus en lisant [Configurer un agent OMS pour Docker Swarm](#configure-an-oms-agent-for-docker-swarm).</span><span class="sxs-lookup"><span data-stu-id="c8a0c-247">If you have a Docker Swarm mode environment, learn more at [Configure an OMS agent for Docker Swarm](#configure-an-oms-agent-for-docker-swarm).</span></span>
- <span data-ttu-id="c8a0c-248">Si vous utilisez des conteneurs avec Service Fabric, consultez [Vue d’ensemble d’Azure Service Fabric](../service-fabric/service-fabric-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c8a0c-248">If you use containers with Service Fabric, learn more at [Overview of Azure Service Fabric](../service-fabric/service-fabric-overview.md).</span></span>
- <span data-ttu-id="c8a0c-249">Hello de révision [moteur Docker sur Windows](https://docs.microsoft.com/virtualization/windowscontainers/manage-docker/configure-docker-daemon) article pour plus d’informations sur la façon tooinstall et configurer vos moteurs Docker sur les ordinateurs exécutant Windows.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-249">Review hello [Docker Engine on Windows](https://docs.microsoft.com/virtualization/windowscontainers/manage-docker/configure-docker-daemon) article for additional information about how tooinstall and configure your Docker Engines on computers running Windows.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c8a0c-250">Docker doit être en cours d’exécution **avant** vous installez hello [Agent OMS pour Linux](log-analytics-agent-linux.md) sur vos ordinateurs hôtes de conteneur.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-250">Docker must be running **before** you install hello [OMS Agent for Linux](log-analytics-agent-linux.md) on your container hosts.</span></span> <span data-ttu-id="c8a0c-251">Si vous avez déjà installé l’agent de hello avant d’installer Docker, vous devez tooreinstall hello Agent OMS pour Linux.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-251">If you've already installed hello agent before installing Docker, you need tooreinstall hello OMS Agent for Linux.</span></span> <span data-ttu-id="c8a0c-252">Pour plus d’informations sur Docker, consultez hello [site Web de Docker](https://www.docker.com).</span><span class="sxs-lookup"><span data-stu-id="c8a0c-252">For more information about Docker, see hello [Docker website](https://www.docker.com).</span></span>


## <a name="linux-container-hosts"></a><span data-ttu-id="c8a0c-253">Hôtes de conteneur Linux</span><span class="sxs-lookup"><span data-stu-id="c8a0c-253">Linux container hosts</span></span>

<span data-ttu-id="c8a0c-254">Une fois que vous avez installé Docker, utilisez hello suivant les paramètres de votre agent de hello conteneur hôte tooconfigure pour une utilisation avec Docker.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-254">After you've installed Docker, use hello following settings for your container host tooconfigure hello agent for use with Docker.</span></span> <span data-ttu-id="c8a0c-255">Vous devez commencer votre ID d’espace de travail OMS et la clé que vous pouvez trouver dans hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-255">First you need your OMS workspace ID and key, which you can find in hello Azure portal.</span></span> <span data-ttu-id="c8a0c-256">Dans votre espace de travail, cliquez sur **Quick Start** > **ordinateurs** tooview votre **ID de l’espace de travail** et **clé primaire**.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-256">In your workspace, click **Quick Start** > **Computers** tooview your **Workspace ID** and **Primary Key**.</span></span>  <span data-ttu-id="c8a0c-257">Copiez-collez ces deux valeurs dans votre éditeur favori.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-257">Copy and paste both into your favorite editor.</span></span>

### <a name="for-all-linux-container-hosts-except-coreos"></a><span data-ttu-id="c8a0c-258">Pour tous les hôtes de conteneur Linux, à l’exception de CoreOS</span><span class="sxs-lookup"><span data-stu-id="c8a0c-258">For all Linux container hosts except CoreOS</span></span>

- <span data-ttu-id="c8a0c-259">Pour plus d’informations sur la façon dont tooinstall hello Agent OMS pour Linux, consultez [connecter vos ordinateurs Linux de tooOperations Management Suite (OMS)](log-analytics-agent-linux.md).</span><span class="sxs-lookup"><span data-stu-id="c8a0c-259">For more information and steps on how tooinstall hello OMS Agent for Linux, see [Connect your Linux Computers tooOperations Management Suite (OMS)](log-analytics-agent-linux.md).</span></span>

### <a name="for-all-linux-container-hosts-including-coreos"></a><span data-ttu-id="c8a0c-260">Pour tous les hôtes de conteneur Linux, avec CoreOS</span><span class="sxs-lookup"><span data-stu-id="c8a0c-260">For all Linux container hosts including CoreOS</span></span>

<span data-ttu-id="c8a0c-261">Démarrer le conteneur d’OMS hello que vous souhaitez toomonitor.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-261">Start hello OMS container that you want toomonitor.</span></span> <span data-ttu-id="c8a0c-262">Modifier et utiliser hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="c8a0c-262">Modify and use hello following example:</span></span>

```
sudo docker run --privileged -d -v /var/run/docker.sock:/var/run/docker.sock -e WSID="your workspace id" -e KEY="your key" -h=`hostname` -p 127.0.0.1:25225:25225 --name="omsagent" --restart=always microsoft/oms
```

### <a name="for-all-azure-government-linux-container-hosts-including-coreos"></a><span data-ttu-id="c8a0c-263">Pour tous les hôtes de conteneur Linux Azure Government, y compris CoreOS</span><span class="sxs-lookup"><span data-stu-id="c8a0c-263">For all Azure Government Linux container hosts including CoreOS</span></span>

<span data-ttu-id="c8a0c-264">Démarrer le conteneur d’OMS hello que vous souhaitez toomonitor.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-264">Start hello OMS container that you want toomonitor.</span></span> <span data-ttu-id="c8a0c-265">Modifier et utiliser hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="c8a0c-265">Modify and use hello following example:</span></span>

```
sudo docker run --privileged -d -v /var/run/docker.sock:/var/run/docker.sock -v /var/log:/var/log -e WSID="your workspace id" -e KEY="your key" -e DOMAIN="opinsights.azure.us" -p 127.0.0.1:25225:25225 -p 127.0.0.1:25224:25224/udp --name="omsagent" -h=`hostname` --restart=always microsoft/oms
```

### <a name="switching-from-using-an-installed-linux-agent-tooone-in-a-container"></a><span data-ttu-id="c8a0c-266">Basculement à partir de l’aide d’un tooone de l’agent Linux installé dans un conteneur</span><span class="sxs-lookup"><span data-stu-id="c8a0c-266">Switching from using an installed Linux agent tooone in a container</span></span>
<span data-ttu-id="c8a0c-267">Si vous utilisé agent de hello directement installé précédemment et que vous souhaitez utiliser tooinstead un agent en cours d’exécution dans un conteneur, vous devez d’abord supprimer hello Agent OMS pour Linux.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-267">If you previously used hello directly-installed agent and want tooinstead use an agent running in a container, you must first remove hello OMS Agent for Linux.</span></span> <span data-ttu-id="c8a0c-268">Consultez [désinstallation hello Agent OMS pour Linux](log-analytics-agent-linux.md#uninstalling-the-oms-agent-for-linux) toounderstand comment toosuccessfully désinstaller hello agent.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-268">See [Uninstalling hello OMS Agent for Linux](log-analytics-agent-linux.md#uninstalling-the-oms-agent-for-linux) toounderstand how toosuccessfully uninstall hello agent.</span></span>  

### <a name="configure-an-oms-agent-for-docker-swarm"></a><span data-ttu-id="c8a0c-269">Configurer un agent OMS pour Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="c8a0c-269">Configure an OMS agent for Docker Swarm</span></span>

<span data-ttu-id="c8a0c-270">Vous pouvez exécuter hello Agent OMS en tant qu’un service global sur Docker Swarm.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-270">You can run hello OMS Agent as a global service on Docker Swarm.</span></span> <span data-ttu-id="c8a0c-271">Utilisez hello suivant informations toocreate un service de l’Agent OMS.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-271">Use hello following information toocreate an OMS Agent service.</span></span> <span data-ttu-id="c8a0c-272">Vous devez tooinsert votre ID d’espace de travail OMS et la clé primaire.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-272">You need tooinsert your OMS Workspace ID and Primary Key.</span></span>

- <span data-ttu-id="c8a0c-273">Exécutez la procédure suivante hello sur le nœud principal de hello.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-273">Run hello following on hello master node.</span></span>

    ```
    sudo docker service create  --name omsagent --mode global  --mount type=bind,source=/var/run/docker.sock,destination=/var/run/docker.sock  -e WSID="<WORKSPACE ID>" -e KEY="<PRIMARY KEY>" -p 25225:25225 -p 25224:25224/udp  --restart-condition=on-failure microsoft/oms
    ```

### <a name="configure-an-oms-agent-for-red-hat-openshift"></a><span data-ttu-id="c8a0c-274">Configurer un agent OMS pour Red Hat OpenShift</span><span class="sxs-lookup"><span data-stu-id="c8a0c-274">Configure an OMS Agent for Red Hat OpenShift</span></span>
<span data-ttu-id="c8a0c-275">Il existe trois façons tooadd hello Agent OMS tooRed Hat OpenShift toostart collecte conteneur analyse des données.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-275">There are three ways tooadd hello OMS Agent tooRed Hat OpenShift toostart collecting container monitoring data.</span></span>

* <span data-ttu-id="c8a0c-276">[Installer hello Agent OMS pour Linux](log-analytics-agent-linux.md) directement sur chaque nœud OpenShift</span><span class="sxs-lookup"><span data-stu-id="c8a0c-276">[Install hello OMS Agent for Linux](log-analytics-agent-linux.md) directly on each OpenShift node</span></span>  
* <span data-ttu-id="c8a0c-277">[Activer l’extension de machine virtuelle Log Analytics](log-analytics-azure-vm-extension.md) sur chaque nœud OpenShift résidant dans Azure</span><span class="sxs-lookup"><span data-stu-id="c8a0c-277">[Enable Log Analytics VM Extension](log-analytics-azure-vm-extension.md) on each OpenShift node residing in Azure</span></span>  
* <span data-ttu-id="c8a0c-278">Installer hello Agent OMS en tant qu’un ensemble de démon OpenShift</span><span class="sxs-lookup"><span data-stu-id="c8a0c-278">Install hello OMS Agent as a OpenShift daemon-set</span></span>  

<span data-ttu-id="c8a0c-279">Dans cette section nous couvrent hello étapes tooinstall requis hello OMS Agent comme un ensemble de démon OpenShift.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-279">In this section we cover hello steps required tooinstall hello OMS Agent as an OpenShift daemon-set.</span></span>  

1. <span data-ttu-id="c8a0c-280">Ouverture de session toohello OpenShift nœud et copie hello yaml fichier maître [ocp-omsagent.yaml](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-omsagent.yaml) à partir de GitHub tooyour maître de nœud et de modifier la valeur hello avec votre ID d’espace de travail OMS et votre clé primaire.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-280">Sign on toohello OpenShift master node and copy hello yaml file [ocp-omsagent.yaml](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-omsagent.yaml) from GitHub tooyour master node and modify hello value with your OMS Workspace ID and with your Primary Key.</span></span>
2. <span data-ttu-id="c8a0c-281">Exécution d’un projet hello suivant de commandes toocreate pour OMS et définir le compte d’utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-281">Run hello following commands toocreate a project for OMS and set hello user account.</span></span>

    ```
    oadm new-project omslogging --node-selector='zone=default'
    oc project omslogging  
    oc create serviceaccount omsagent  
    oadm policy add-cluster-role-to-user cluster-reader   system:serviceaccount:omslogging:omsagent  
    oadm policy add-scc-to-user privileged system:serviceaccount:omslogging:omsagent  
    ```

4. <span data-ttu-id="c8a0c-282">toodeploy hello démon-set, exécutez la commande suivante hello :</span><span class="sxs-lookup"><span data-stu-id="c8a0c-282">toodeploy hello daemon-set, run hello following:</span></span>

    `oc create -f ocp-omsagent.yaml`

5. <span data-ttu-id="c8a0c-283">tooverify, il est configuré et fonctionne correctement, tapez hello qui suit :</span><span class="sxs-lookup"><span data-stu-id="c8a0c-283">tooverify it is configured and working correctly, type hello following:</span></span>

    `oc describe daemonset omsagent`  

    <span data-ttu-id="c8a0c-284">et hello sortie doit ressembler à :</span><span class="sxs-lookup"><span data-stu-id="c8a0c-284">and hello output should resemble:</span></span>

    ```
    [ocpadmin@khm-0 ~]$ oc describe ds oms  
    Name:           oms  
    Image(s):       microsoft/oms  
    Selector:       name=omsagent  
    Node-Selector:  zone=default  
    Labels:         agentVersion=1.4.0-12  
                    dockerProviderVersion=10.0.0-25  
                    name=omsagent  
    Desired Number of Nodes Scheduled: 3  
    Current Number of Nodes Scheduled: 3  
    Number of Nodes Misscheduled: 0  
    Pods Status:    3 Running / 0 Waiting / 0 Succeeded / 0 Failed  
    No events.  
    ```

<span data-ttu-id="c8a0c-285">Si vous souhaitez toouse secrets toosecure votre ID d’espace de travail OMS et la clé primaire lors de l’utilisation du fichier de jeu de démon yaml hello Agent OMS, effectuer hello comme suit.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-285">If you want toouse secrets toosecure your OMS Workspace ID and Primary Key when using hello OMS Agent daemon-set yaml file, perform hello following steps.</span></span>

1. <span data-ttu-id="c8a0c-286">Ouverture de session toohello OpenShift nœud et copie hello yaml fichier maître [ocp-ds-omsagent.yaml](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-ds-omsagent.yaml) et la clé secrète de la génération du script [ocp-secretgen.sh](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-secretgen.sh) à partir de GitHub.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-286">Sign on toohello OpenShift master node and copy hello yaml file [ocp-ds-omsagent.yaml](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-ds-omsagent.yaml) and secret generating script [ocp-secretgen.sh](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-secretgen.sh) from GitHub.</span></span>  <span data-ttu-id="c8a0c-287">Ce script générera le fichier d’yaml hello secrets pour l’ID d’espace de travail OMS et la clé primaire toosecure votre SÉCRÉTER plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-287">This script will generate hello secrets yaml file for OMS Workspace ID and Primary Key toosecure your secrete information.</span></span>  
2. <span data-ttu-id="c8a0c-288">Exécution d’un projet hello suivant de commandes toocreate pour OMS et définir le compte d’utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-288">Run hello following commands toocreate a project for OMS and set hello user account.</span></span> <span data-ttu-id="c8a0c-289">secret Hello génération du script vous demande votre ID d’espace de travail OMS <WSID> et la clé primaire <KEY> à la fin, il crée des fichiers d’ocp-secret.yaml hello.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-289">hello secret generating script asks for your OMS Workspace ID <WSID> and Primary Key <KEY> and upon completion, it creates hello ocp-secret.yaml file.</span></span>  

    ```
    oadm new-project omslogging --node-selector='zone=default'  
    oc project omslogging  
    oc create serviceaccount omsagent  
    oadm policy add-cluster-role-to-user cluster-reader   system:serviceaccount:omslogging:omsagent  
    oadm policy add-scc-to-user privileged system:serviceaccount:omslogging:omsagent  
    ```

4. <span data-ttu-id="c8a0c-290">Déployer le fichier de secret principal hello en exécutant hello suivante :</span><span class="sxs-lookup"><span data-stu-id="c8a0c-290">Deploy hello secret file by running hello following:</span></span>

    `oc create -f ocp-secret.yaml`

5. <span data-ttu-id="c8a0c-291">Vérifier le déploiement en exécutant hello suivante :</span><span class="sxs-lookup"><span data-stu-id="c8a0c-291">Verify deployment by running hello following:</span></span>

    `oc describe secret omsagent-secret`  

    <span data-ttu-id="c8a0c-292">et hello sortie doit ressembler à :</span><span class="sxs-lookup"><span data-stu-id="c8a0c-292">and hello  output should resemble:</span></span>  

    ```
    [ocpadmin@khocp-master-0 ~]$ oc describe ds oms  
    Name:           oms  
    Image(s):       microsoft/oms  
    Selector:       name=omsagent  
    Node-Selector:  zone=default  
    Labels:         agentVersion=1.4.0-12  
                    dockerProviderVersion=10.0.0-25  
                    name=omsagent  
    Desired Number of Nodes Scheduled: 3  
    Current Number of Nodes Scheduled: 3  
    Number of Nodes Misscheduled: 0  
    Pods Status:    3 Running / 0 Waiting / 0 Succeeded / 0 Failed  
    No events.  
    ```

6. <span data-ttu-id="c8a0c-293">Déployer le fichier de jeu de démon yaml de l’Agent OMS hello en exécutant hello suivante :</span><span class="sxs-lookup"><span data-stu-id="c8a0c-293">Deploy hello OMS Agent daemon-set yaml file by running hello following:</span></span>

    `oc create -f ocp-ds-omsagent.yaml`  

7. <span data-ttu-id="c8a0c-294">Vérifier le déploiement en exécutant hello suivante :</span><span class="sxs-lookup"><span data-stu-id="c8a0c-294">Verify deployment by running hello following:</span></span>

    `oc describe ds oms`

    <span data-ttu-id="c8a0c-295">et hello sortie doit ressembler à :</span><span class="sxs-lookup"><span data-stu-id="c8a0c-295">and hello output should resemble:</span></span>

    ```
    [ocpadmin@khocp-master-0 ~]$ oc describe secret omsagent-secret  
    Name:           omsagent-secret  
    Namespace:      omslogging  
    Labels:         <none>  
    Annotations:    <none>  

    Type:   Opaque  

     Data  
     ====  
     KEY:    89 bytes  
     WSID:   37 bytes  
    ```

### <a name="secure-your-secret-information-for-docker-swarm-and-kubernetes"></a><span data-ttu-id="c8a0c-296">Sécuriser vos informations secrètes pour Docker Swarm et Kubernetes</span><span class="sxs-lookup"><span data-stu-id="c8a0c-296">Secure your secret information for Docker Swarm and Kubernetes</span></span>

<span data-ttu-id="c8a0c-297">Vous pouvez sécuriser l’ID d’espace de travail OMS et les clés primaires pour les services de conteneur Docker Swarm et Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-297">You can secure your secret OMS Workspace ID and Primary Keys for Docker Swarm and Kubernetes container services.</span></span>

#### <a name="secure-secrets-for-docker-swarm"></a><span data-ttu-id="c8a0c-298">Sécuriser les secrets pour Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="c8a0c-298">Secure secrets for Docker Swarm</span></span>

<span data-ttu-id="c8a0c-299">Pour Docker Swarm, une fois le secret hello pour l’ID de l’espace de travail et la clé primaire est créé, vous pouvez exécuter hello créer le service de Docker hello pour OMSagent.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-299">For Docker Swarm, once hello secret for Workspace ID and Primary Key is created, you can run hello create hello Docker service for OMSagent.</span></span> <span data-ttu-id="c8a0c-300">Utilisez hello suivant informations toocreate vos informations confidentielles.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-300">Use hello following information toocreate your secret information.</span></span>

1. <span data-ttu-id="c8a0c-301">Exécutez la procédure suivante hello sur le nœud principal de hello.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-301">Run hello following on hello master node.</span></span>

    ```
    echo "WSID" | docker secret create WSID -
    echo "KEY" | docker secret create KEY -
    ```

2. <span data-ttu-id="c8a0c-302">Vérifiez que les secrets ont été créés correctement.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-302">Verify that secrets were created properly.</span></span>

    ```
    keiko@swarmm-master-13957614-0:/run# sudo docker secret ls
    ```

    ```
    ID                          NAME                CREATED             UPDATED
    j2fj153zxy91j8zbcitnjxjiv   WSID                43 minutes ago      43 minutes ago
    l9rh3n987g9c45zffuxdxetd9   KEY                 38 minutes ago      38 minutes ago
    ```

3. <span data-ttu-id="c8a0c-303">Exécution hello suivant commande toomount hello secrets toohello placées dans des conteneurs de l’Agent OMS.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-303">Run hello following command toomount hello secrets toohello containerized OMS Agent.</span></span>

    ```
    sudo docker service create  --name omsagent --mode global  --mount type=bind,source=/var/run/docker.sock,destination=/var/run/docker.sock --secret source=WSID,target=WSID --secret source=KEY,target=KEY  -p 25225:25225 -p 25224:25224/udp --restart-condition=on-failure microsoft/oms
    ```

#### <a name="secure-secrets-for-kubernetes-with-yaml-files"></a><span data-ttu-id="c8a0c-304">Sécuriser des secrets pour Kubernetes avec des fichiers yaml</span><span class="sxs-lookup"><span data-stu-id="c8a0c-304">Secure secrets for Kubernetes with yaml files</span></span>

<span data-ttu-id="c8a0c-305">Pour Kubernetes, vous utilisez un fichier de script toogenerate hello secrets yaml pour votre ID d’espace de travail et la clé primaire.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-305">For Kubernetes, you use a script toogenerate hello secrets yaml file for your Workspace ID and Primary Key.</span></span> <span data-ttu-id="c8a0c-306">À hello [OMS Docker Kubernetes GitHub](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes) page, il existe des fichiers que vous pouvez utiliser avec ou sans vos informations confidentielles.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-306">At hello [OMS Docker Kubernetes GitHub](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes) page, there are files that you can use with or without your secret information.</span></span>

- <span data-ttu-id="c8a0c-307">Hello DaemonSet de l’Agent OMS par défaut n’a pas d’informations confidentielles (omsagent.yaml)</span><span class="sxs-lookup"><span data-stu-id="c8a0c-307">hello Default OMS Agent DaemonSet does not have secret information (omsagent.yaml)</span></span>
- <span data-ttu-id="c8a0c-308">fichier d’yaml Hello DaemonSet de l’Agent OMS utilise des informations confidentielles (omsagent-ds-secrets.yaml) avec secret fichier génération de scripts toogenerate hello secrets yaml (omsagentsecret.yaml).</span><span class="sxs-lookup"><span data-stu-id="c8a0c-308">hello OMS Agent DaemonSet yaml file uses secret information (omsagent-ds-secrets.yaml) with secret generation scripts toogenerate hello secrets yaml (omsagentsecret.yaml) file.</span></span>

<span data-ttu-id="c8a0c-309">Vous pouvez choisir toocreate omsagent DaemonSets avec ou sans les clés secrètes.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-309">You can choose toocreate omsagent DaemonSets with or without secrets.</span></span>

##### <a name="default-omsagent-daemonset-yaml-file-without-secrets"></a><span data-ttu-id="c8a0c-310">Le fichier yaml par défaut DaemonSet de l’agent OMS sans secrets</span><span class="sxs-lookup"><span data-stu-id="c8a0c-310">Default OMSagent DaemonSet yaml file without secrets</span></span>

- <span data-ttu-id="c8a0c-311">Hello fichier par défaut OMS Agent DaemonSet yaml, remplacez hello `<WSID>` et `<KEY>` tooyour WSID et la clé.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-311">For hello default OMS Agent DaemonSet yaml file, replace hello `<WSID>` and `<KEY>` tooyour WSID and KEY.</span></span> <span data-ttu-id="c8a0c-312">Copiez nœud maître du tooyour fichier hello et suivante d’exécution hello :</span><span class="sxs-lookup"><span data-stu-id="c8a0c-312">Copy hello file tooyour master node and run hello following:</span></span>

    ```
    sudo kubectl create -f omsagent.yaml
    ```

##### <a name="default-omsagent-daemonset-yaml-file-with-secrets"></a><span data-ttu-id="c8a0c-313">Le fichier yaml par défaut DaemonSet de l’agent OMS avec secrets</span><span class="sxs-lookup"><span data-stu-id="c8a0c-313">Default OMSagent DaemonSet yaml file with secrets</span></span>

1. <span data-ttu-id="c8a0c-314">toouse DaemonSet de l’Agent OMS à l’aide des informations confidentielles, les secrets hello d’abord créer.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-314">toouse OMS Agent DaemonSet using secret information, create hello secrets first.</span></span>
    1. <span data-ttu-id="c8a0c-315">Copiez le script de hello et fichier de modèle de secret principal et assurez-vous qu’ils sont sur hello même répertoire.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-315">Copy hello script and secret template file and make sure they are on hello same directory.</span></span>
        - <span data-ttu-id="c8a0c-316">Script de génération de secrets - secret-gen.sh</span><span class="sxs-lookup"><span data-stu-id="c8a0c-316">Secret generating script - secret-gen.sh</span></span>
        - <span data-ttu-id="c8a0c-317">Modèle de secret - secret-template.yaml</span><span class="sxs-lookup"><span data-stu-id="c8a0c-317">secret template - secret-template.yaml</span></span>
    2. <span data-ttu-id="c8a0c-318">Exécutez le script de hello comme hello l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-318">Run hello script, like hello following example.</span></span> <span data-ttu-id="c8a0c-319">script de Hello demande hello ID d’espace de travail OMS et la clé primaire et une fois que vous les entrez, script de hello crée un fichier de secret principal yaml, vous pouvez l’exécuter.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-319">hello script asks for hello OMS Workspace ID and Primary Key and after you enter them, hello script creates a secret yaml file so you can run it.</span></span>   

        ```
        #> sudo bash ./secret-gen.sh
        ```

    3. <span data-ttu-id="c8a0c-320">Créer des pod de secrets hello en exécutant hello suivante :</span><span class="sxs-lookup"><span data-stu-id="c8a0c-320">Create hello secrets pod by running hello following:</span></span>
        ```
        sudo kubectl create -f omsagentsecret.yaml
        ```

    4. <span data-ttu-id="c8a0c-321">tooverify, exécutez hello suivante :</span><span class="sxs-lookup"><span data-stu-id="c8a0c-321">tooverify, run hello following:</span></span>

        ```
        keiko@ubuntu16-13db:~# sudo kubectl get secrets
        ```

        <span data-ttu-id="c8a0c-322">La sortie doit ressembler à :</span><span class="sxs-lookup"><span data-stu-id="c8a0c-322">Output should resemble:</span></span>

        ```
        NAME                  TYPE                                  DATA      AGE
        default-token-gvl91   kubernetes.io/service-account-token   3         50d
        omsagent-secret       Opaque                                2         1d
        ```

        ```
        keiko@ubuntu16-13db:~# sudo kubectl describe secrets omsagent-secret
        ```

        <span data-ttu-id="c8a0c-323">La sortie doit ressembler à :</span><span class="sxs-lookup"><span data-stu-id="c8a0c-323">Output should resemble:</span></span>

        ```
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

    5. <span data-ttu-id="c8a0c-324">Créer votre DaemonsSet de l’agent OMS en exécutant ``` sudo kubectl create -f omsagent-ds-secrets.yaml ```</span><span class="sxs-lookup"><span data-stu-id="c8a0c-324">Create your omsagent daemon-set by running ``` sudo kubectl create -f omsagent-ds-secrets.yaml ```</span></span>

2. <span data-ttu-id="c8a0c-325">Vérifiez que hello que daemonset de l’Agent OMS est en cours d’exécution, toohello comme suit :</span><span class="sxs-lookup"><span data-stu-id="c8a0c-325">Verify that hello OMS Agent DaemonSet is running, similar toohello following:</span></span>

    ```
    keiko@ubuntu16-13db:~# sudo kubectl get ds omsagent
    ```

    ```
    NAME       DESIRED   CURRENT   NODE-SELECTOR   AGE
    omsagent   3         3         <none>          1h
    ```


<span data-ttu-id="c8a0c-326">Pour Kubernetes, utilisez un fichier de script toogenerate hello secrets yaml pour l’ID de l’espace de travail et la clé primaire.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-326">For Kubernetes, use a script toogenerate hello secrets yaml file for Workspace ID and Primary Key.</span></span> <span data-ttu-id="c8a0c-327">Hello utilisez informations exemple avec hello suivantes [omsagent yaml fichier](https://github.com/Microsoft/OMS-docker/blob/master/Kubernetes/omsagent.yaml) toosecure vos informations confidentielles.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-327">Use hello following example information with hello [omsagent yaml file](https://github.com/Microsoft/OMS-docker/blob/master/Kubernetes/omsagent.yaml) toosecure your secret information.</span></span>

```
keiko@ubuntu16-13db:~# sudo kubectl describe secrets omsagent-secret
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

## <a name="windows-container-hosts"></a><span data-ttu-id="c8a0c-328">Hôtes de conteneur Windows</span><span class="sxs-lookup"><span data-stu-id="c8a0c-328">Windows container hosts</span></span>

### <a name="preparation-before-installing-windows-agents"></a><span data-ttu-id="c8a0c-329">Préparation préalable à l’installation des agents Windows</span><span class="sxs-lookup"><span data-stu-id="c8a0c-329">Preparation before installing Windows agents</span></span>

<span data-ttu-id="c8a0c-330">Avant d’installer des agents sur les ordinateurs exécutant Windows, vous devez le service de Docker tooconfigure hello.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-330">Before you install agents on computers running Windows, you need tooconfigure hello Docker service.</span></span> <span data-ttu-id="c8a0c-331">configuration de Hello autorise hello Windows hello ou l’agent Analytique de journal machine virtuelle extension toouse hello de socket TCP de Docker afin que les agents hello peuvent accéder au démon Docker de hello à distance et les données toocapture l’analyse.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-331">hello configuration allows hello Windows agent or hello Log Analytics virtual machine extension toouse hello Docker TCP socket so that hello agents can access hello Docker daemon remotely and toocapture data for monitoring.</span></span>

#### <a name="toostart-docker-and-verify-its-configuration"></a><span data-ttu-id="c8a0c-332">toostart Docker et vérifiez sa configuration.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-332">toostart Docker and verify its configuration</span></span>

<span data-ttu-id="c8a0c-333">Il existe tooset étapes nécessaires de TCP, canal nommé pour Windows Server :</span><span class="sxs-lookup"><span data-stu-id="c8a0c-333">There are steps needed tooset up TCP named pipe for Windows Server:</span></span>

1. <span data-ttu-id="c8a0c-334">Dans Windows PowerShell, activez les canaux TCP et nommé.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-334">In Windows PowerShell, enable TCP pipe and named pipe.</span></span>

    ```
    Stop-Service docker
    dockerd --unregister-service
    dockerd --register-service -H npipe:// -H 0.0.0.0:2375  
    Start-Service docker
    ```

2. <span data-ttu-id="c8a0c-335">Configurer Docker avec le fichier de configuration hello pour le canal de communication TCP et le canal nommé.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-335">Configure Docker with hello configuration file for TCP pipe and named pipe.</span></span> <span data-ttu-id="c8a0c-336">fichier de configuration Hello se trouve dans C:\ProgramData\docker\config\daemon.json.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-336">hello configuration file is located at C:\ProgramData\docker\config\daemon.json.</span></span>

    <span data-ttu-id="c8a0c-337">Dans le fichier de daemon.json hello, vous devrez suivant de hello :</span><span class="sxs-lookup"><span data-stu-id="c8a0c-337">In hello daemon.json file, you will need hello following:</span></span>

    ```
    {
    "hosts": ["tcp://0.0.0.0:2375", "npipe://"]
    }
    ```

<span data-ttu-id="c8a0c-338">Pour plus d’informations sur la configuration du démon Docker hello utilisée avec des conteneurs Windows, consultez [moteur Docker sur Windows](https://docs.microsoft.com/virtualization/windowscontainers/manage-docker/configure-docker-daemon).</span><span class="sxs-lookup"><span data-stu-id="c8a0c-338">For more information about hello Docker daemon configuration used with Windows Containers, see [Docker Engine on Windows](https://docs.microsoft.com/virtualization/windowscontainers/manage-docker/configure-docker-daemon).</span></span>


### <a name="install-windows-agents"></a><span data-ttu-id="c8a0c-339">Installer les agents Windows</span><span class="sxs-lookup"><span data-stu-id="c8a0c-339">Install Windows agents</span></span>

<span data-ttu-id="c8a0c-340">tooenable Windows et conteneur Hyper-V à l’analyse, installez hello Microsoft Monitoring Agent (MMA) sur les ordinateurs Windows qui sont des hôtes de conteneur.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-340">tooenable Windows and Hyper-V container monitoring, install hello Microsoft Monitoring Agent (MMA) on Windows computers that are container hosts.</span></span> <span data-ttu-id="c8a0c-341">Pour les ordinateurs exécutant Windows dans votre environnement local, consultez [tooLog d’ordinateurs Windows de se connecter Analytique](log-analytics-windows-agents.md).</span><span class="sxs-lookup"><span data-stu-id="c8a0c-341">For computers running Windows in your on-premises environment, see [Connect Windows computers tooLog Analytics](log-analytics-windows-agents.md).</span></span> <span data-ttu-id="c8a0c-342">Pour les ordinateurs virtuels en cours d’exécution dans Azure, les connecter tooLog Analytique à l’aide de hello [extension de machine virtuelle](log-analytics-azure-vm-extension.md).</span><span class="sxs-lookup"><span data-stu-id="c8a0c-342">For virtual machines running in Azure, connect them tooLog Analytics using hello [virtual machine extension](log-analytics-azure-vm-extension.md).</span></span>

<span data-ttu-id="c8a0c-343">Vous pouvez surveiller les conteneurs Windows en cours d’exécution sur Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-343">You can monitor Windows containers running on Service Fabric.</span></span> <span data-ttu-id="c8a0c-344">Toutefois, seules les [machines virtuelles qui s’exécutent dans Azure](log-analytics-azure-vm-extension.md) et les [ordinateurs exécutant Windows dans votre environnement local](log-analytics-windows-agents.md) sont actuellement pris en charge pour Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-344">However, only [virtual machines running in Azure](log-analytics-azure-vm-extension.md) and [computers running Windows in your on-premises environment](log-analytics-windows-agents.md) are currently supported for Service Fabric.</span></span>

<span data-ttu-id="c8a0c-345">Vous pouvez vérifier que hello solution d’analyse de conteneur est correctement configuré pour Windows.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-345">You can verify that hello Container Monitoring solution is set correctly for Windows.</span></span> <span data-ttu-id="c8a0c-346">toocheck si le pack d’administration hello était téléchargement correctement, recherchez *ContainerManagement.xxx*.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-346">toocheck whether hello management pack was download properly, look for *ContainerManagement.xxx*.</span></span> <span data-ttu-id="c8a0c-347">fichiers de Hello doivent être dans le dossier C:\Program Files\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs de hello.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-347">hello files should be in hello C:\Program Files\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs folder.</span></span>


## <a name="solution-components"></a><span data-ttu-id="c8a0c-348">Composants de la solution</span><span class="sxs-lookup"><span data-stu-id="c8a0c-348">Solution components</span></span>

<span data-ttu-id="c8a0c-349">Si vous utilisez des agents Windows, puis hello Pack d’administration suivant est installé sur chaque ordinateur sur lequel un agent lorsque vous ajoutez cette solution.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-349">If you are using Windows agents, then hello following management pack is installed on each computer with an agent when you add this solution.</span></span> <span data-ttu-id="c8a0c-350">Aucune configuration ou maintenance n’est requis pour le pack d’administration hello.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-350">No configuration or maintenance is required for hello management pack.</span></span>

- <span data-ttu-id="c8a0c-351">*ContainerManagement.xxx* installé dans le dossier C:\Program Files\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs</span><span class="sxs-lookup"><span data-stu-id="c8a0c-351">*ContainerManagement.xxx* installed in C:\Program Files\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs</span></span>

## <a name="container-data-collection-details"></a><span data-ttu-id="c8a0c-352">Détails sur la collecte de données des conteneurs</span><span class="sxs-lookup"><span data-stu-id="c8a0c-352">Container data collection details</span></span>
<span data-ttu-id="c8a0c-353">Hello solution d’analyse de conteneur collecte diverses données de journaux et des métriques de performances à partir des hôtes de conteneurs et les conteneurs à l’aide d’agents que vous activez.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-353">hello Container Monitoring solution collects various performance metrics and log data from container hosts and containers using agents that you enable.</span></span>

<span data-ttu-id="c8a0c-354">Données sont collectées toutes les trois minutes par hello suivant les types d’agents.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-354">Data is collected every three minutes by hello following agent types.</span></span>

- [<span data-ttu-id="c8a0c-355">Agent OMS pour Linux</span><span class="sxs-lookup"><span data-stu-id="c8a0c-355">OMS Agent for Linux</span></span>](log-analytics-linux-agents.md)
- [<span data-ttu-id="c8a0c-356">Agent Windows</span><span class="sxs-lookup"><span data-stu-id="c8a0c-356">Windows agent</span></span>](log-analytics-windows-agents.md)
- [<span data-ttu-id="c8a0c-357">Extension de machine virtuelle Log Analytics</span><span class="sxs-lookup"><span data-stu-id="c8a0c-357">Log Analytics VM extension</span></span>](log-analytics-azure-vm-extension.md)


### <a name="container-records"></a><span data-ttu-id="c8a0c-358">Enregistrements de conteneur</span><span class="sxs-lookup"><span data-stu-id="c8a0c-358">Container records</span></span>

<span data-ttu-id="c8a0c-359">Hello tableau suivant présente des exemples d’enregistrements collectées par la solution d’analyse de conteneur hello et types de données hello qui s’affichent dans les résultats de recherche de journal.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-359">hello following table shows examples of records collected by hello Container Monitoring solution and hello data types that appear in log search results.</span></span>

| <span data-ttu-id="c8a0c-360">Type de données</span><span class="sxs-lookup"><span data-stu-id="c8a0c-360">Data type</span></span> | <span data-ttu-id="c8a0c-361">Type de données dans Recherche de journaux</span><span class="sxs-lookup"><span data-stu-id="c8a0c-361">Data type in Log Search</span></span> | <span data-ttu-id="c8a0c-362">Champs</span><span class="sxs-lookup"><span data-stu-id="c8a0c-362">Fields</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c8a0c-363">Performances des hôtes et des conteneurs</span><span class="sxs-lookup"><span data-stu-id="c8a0c-363">Performance for hosts and containers</span></span> | `Type=Perf` | <span data-ttu-id="c8a0c-364">Computer, ObjectName, CounterName &#40;%Processor Time, Disk Reads MB, Disk Writes MB, Memory Usage MB, Network Receive Bytes, Network Send Bytes, Processor Usage sec, Network&#41;, CounterValue,TimeGenerated, CounterPath, SourceSystem</span><span class="sxs-lookup"><span data-stu-id="c8a0c-364">Computer, ObjectName, CounterName &#40;%Processor Time, Disk Reads MB, Disk Writes MB, Memory Usage MB, Network Receive Bytes, Network Send Bytes, Processor Usage sec, Network&#41;, CounterValue,TimeGenerated, CounterPath, SourceSystem</span></span> |
| <span data-ttu-id="c8a0c-365">Inventaire de conteneur</span><span class="sxs-lookup"><span data-stu-id="c8a0c-365">Container inventory</span></span> | `Type=ContainerInventory` | <span data-ttu-id="c8a0c-366">TimeGenerated, Computer, container name, ContainerHostname, Image, ImageTag, ContainerState, ExitCode, EnvironmentVar, Command, CreatedTime, StartedTime, FinishedTime, SourceSystem, ContainerID, ImageID</span><span class="sxs-lookup"><span data-stu-id="c8a0c-366">TimeGenerated, Computer, container name, ContainerHostname, Image, ImageTag, ContainerState, ExitCode, EnvironmentVar, Command, CreatedTime, StartedTime, FinishedTime, SourceSystem, ContainerID, ImageID</span></span> |
| <span data-ttu-id="c8a0c-367">Inventaire d’image de conteneur</span><span class="sxs-lookup"><span data-stu-id="c8a0c-367">Container image inventory</span></span> | `Type=ContainerImageInventory` | <span data-ttu-id="c8a0c-368">TimeGenerated, Computer, Image, ImageTag, ImageSize, VirtualSize, Running, Paused, Stopped, Failed, SourceSystem, ImageID, TotalContainer</span><span class="sxs-lookup"><span data-stu-id="c8a0c-368">TimeGenerated, Computer, Image, ImageTag, ImageSize, VirtualSize, Running, Paused, Stopped, Failed, SourceSystem, ImageID, TotalContainer</span></span> |
| <span data-ttu-id="c8a0c-369">Journal de conteneur</span><span class="sxs-lookup"><span data-stu-id="c8a0c-369">Container log</span></span> | `Type=ContainerLog` | <span data-ttu-id="c8a0c-370">TimeGenerated, Computer, image ID, container name, LogEntrySource, LogEntry, SourceSystem, ContainerID</span><span class="sxs-lookup"><span data-stu-id="c8a0c-370">TimeGenerated, Computer, image ID, container name, LogEntrySource, LogEntry, SourceSystem, ContainerID</span></span> |
| <span data-ttu-id="c8a0c-371">Journal de service de conteneur</span><span class="sxs-lookup"><span data-stu-id="c8a0c-371">Container service log</span></span> | `Type=ContainerServiceLog`  | <span data-ttu-id="c8a0c-372">TimeGenerated, Computer, TimeOfCommand, Image, Command, SourceSystem, ContainerID</span><span class="sxs-lookup"><span data-stu-id="c8a0c-372">TimeGenerated, Computer, TimeOfCommand, Image, Command, SourceSystem, ContainerID</span></span> |
| <span data-ttu-id="c8a0c-373">Inventaire du nœud de conteneur</span><span class="sxs-lookup"><span data-stu-id="c8a0c-373">Container node inventory</span></span> | `Type=ContainerNodeInventory_CL`| <span data-ttu-id="c8a0c-374">TimeGenerated, Computer, ClassName_s, DockerVersion_s, OperatingSystem_s, Volume_s, Network_s, NodeRole_s, OrchestratorType_s, InstanceID_g, SourceSystem</span><span class="sxs-lookup"><span data-stu-id="c8a0c-374">TimeGenerated, Computer, ClassName_s, DockerVersion_s, OperatingSystem_s, Volume_s, Network_s, NodeRole_s, OrchestratorType_s, InstanceID_g, SourceSystem</span></span>|
| <span data-ttu-id="c8a0c-375">Inventaire de Kubernetes</span><span class="sxs-lookup"><span data-stu-id="c8a0c-375">Kubernetes inventory</span></span> | `Type=KubePodInventory_CL` | <span data-ttu-id="c8a0c-376">TimeGenerated, Computer, PodLabel_deployment_s, PodLabel_deploymentconfig_s, PodLabel_docker_registry_s, Name_s, Namespace_s, PodStatus_s, PodIp_s, PodUid_g, PodCreationTimeStamp_t, SourceSystem</span><span class="sxs-lookup"><span data-stu-id="c8a0c-376">TimeGenerated, Computer, PodLabel_deployment_s, PodLabel_deploymentconfig_s, PodLabel_docker_registry_s, Name_s, Namespace_s, PodStatus_s, PodIp_s, PodUid_g, PodCreationTimeStamp_t, SourceSystem</span></span> |
| <span data-ttu-id="c8a0c-377">Processus de conteneur</span><span class="sxs-lookup"><span data-stu-id="c8a0c-377">Container process</span></span> | `Type=ContainerProcess_CL` | <span data-ttu-id="c8a0c-378">TimeGenerated, Computer, Pod_s, Namespace_s, ClassName_s, InstanceID_s, Uid_s, PID_s, PPID_s, C_s, STIME_s, Tty_s, TIME_s, Cmd_s, Id_s, Name_s, SourceSystem</span><span class="sxs-lookup"><span data-stu-id="c8a0c-378">TimeGenerated, Computer, Pod_s, Namespace_s, ClassName_s, InstanceID_s, Uid_s, PID_s, PPID_s, C_s, STIME_s, Tty_s, TIME_s, Cmd_s, Id_s, Name_s, SourceSystem</span></span> |
| <span data-ttu-id="c8a0c-379">Événements Kubernetes</span><span class="sxs-lookup"><span data-stu-id="c8a0c-379">Kubernetes events</span></span> | `Type=KubeEvents_CL` | <span data-ttu-id="c8a0c-380">TimeGenerated, Computer, Name_s, ObjectKind_s, Namespace_s, Reason_s, Type_s, SourceComponent_s, SourceSystem, Message</span><span class="sxs-lookup"><span data-stu-id="c8a0c-380">TimeGenerated, Computer, Name_s, ObjectKind_s, Namespace_s, Reason_s, Type_s, SourceComponent_s, SourceSystem, Message</span></span> |

<span data-ttu-id="c8a0c-381">Étiquettes ajouté trop*PodLabel* des types de données sont vos propres étiquettes personnalisées.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-381">Labels appended too*PodLabel* data types are your own custom labels.</span></span> <span data-ttu-id="c8a0c-382">Hello ajouté PodLabel étiquettes indiqués dans la table de hello sont des exemples.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-382">hello appended PodLabel labels shown in hello table are examples.</span></span> <span data-ttu-id="c8a0c-383">Par conséquent, `PodLabel_deployment_s`, `PodLabel_deploymentconfig_s`, `PodLabel_docker_registry_s` seront différentes dans le jeu de données de votre environnement et ressembleront à `PodLabel_yourlabel_s`.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-383">So, `PodLabel_deployment_s`, `PodLabel_deploymentconfig_s`, `PodLabel_docker_registry_s` will differ in your environment's data set and generically resemble `PodLabel_yourlabel_s`.</span></span>


## <a name="monitor-containers"></a><span data-ttu-id="c8a0c-384">Analyser les conteneurs</span><span class="sxs-lookup"><span data-stu-id="c8a0c-384">Monitor containers</span></span>
<span data-ttu-id="c8a0c-385">Après avoir configuré solution hello activée dans le portail OMS de hello, hello **conteneurs** vignette affiche des informations résumées concernant vos hôtes de conteneurs et les conteneurs hello en cours d’exécution dans des hôtes.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-385">After you have hello solution enabled in hello OMS portal, hello **Containers** tile shows summary information about your container hosts and hello containers running in hosts.</span></span>

![Vignette Conteneurs](./media/log-analytics-containers/containers-title.png)

<span data-ttu-id="c8a0c-387">vignette de Hello montre une vue d’ensemble des conteneurs combien vous avez dans l’environnement de hello et si elles sont ont échoué, en cours d’exécution ou arrêté.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-387">hello tile shows an overview of how many containers you have in hello environment and whether they're failed, running, or stopped.</span></span>

### <a name="using-hello-containers-dashboard"></a><span data-ttu-id="c8a0c-388">À l’aide du tableau de bord hello conteneurs</span><span class="sxs-lookup"><span data-stu-id="c8a0c-388">Using hello Containers dashboard</span></span>
<span data-ttu-id="c8a0c-389">Cliquez sur hello **conteneurs** vignette.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-389">Click hello **Containers** tile.</span></span> <span data-ttu-id="c8a0c-390">À partir de là, vous voyez les vues organisées par :</span><span class="sxs-lookup"><span data-stu-id="c8a0c-390">From there you'll see views organized by:</span></span>

- <span data-ttu-id="c8a0c-391">**Événements de conteneur** : affiche l’état du conteneur et les ordinateurs dont le conteneur a échoué.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-391">**Container Events** - Shows container status and computers with failed containers.</span></span>
- <span data-ttu-id="c8a0c-392">**Journaux du conteneur** -affiche un graphique des fichiers journaux de conteneur générés au fil du temps et une liste d’ordinateurs avec hello plus grand nombre de fichiers journaux.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-392">**Container Logs** - Shows a chart of container log files generated over time and a list of computers with hello highest number of log files.</span></span>
- <span data-ttu-id="c8a0c-393">**Événements de Kubernetes** -affiche un graphique des événements Kubernetes générés au fil du temps et une liste des raisons hello pourquoi POD généré les événements hello.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-393">**Kubernetes Events** - Shows a chart of Kubernetes events generated over time and a list of hello reasons why pods generated hello events.</span></span> <span data-ttu-id="c8a0c-394">*Ce jeu de données est utilisé uniquement dans les environnements Linux.*</span><span class="sxs-lookup"><span data-stu-id="c8a0c-394">*This data set is used only in Linux environments.*</span></span>
- <span data-ttu-id="c8a0c-395">**Inventaire de Namespace Kubernetes** - affiche le nombre de hello d’espaces de noms et les blocs et affiche leur hiérarchie.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-395">**Kubernetes Namespace Inventory** - Shows hello number of namespaces and pods and shows their hierarchy.</span></span> <span data-ttu-id="c8a0c-396">*Ce jeu de données est utilisé uniquement dans les environnements Linux.*</span><span class="sxs-lookup"><span data-stu-id="c8a0c-396">*This data set is used only in Linux environments.*</span></span>
- <span data-ttu-id="c8a0c-397">**Inventaire de nœud conteneur** -affiche le nombre hello des types d’orchestration utilisé sur les nœuds/hôtes de conteneur.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-397">**Container Node Inventory** - Shows hello number of orchestration types used on container nodes/hosts.</span></span> <span data-ttu-id="c8a0c-398">nœuds d’ordinateur Hello/hôtes sont également répertoriés par nombre hello de conteneurs.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-398">hello computer nodes/hosts are also listed by hello number of containers.</span></span> <span data-ttu-id="c8a0c-399">*Ce jeu de données est utilisé uniquement dans les environnements Linux.*</span><span class="sxs-lookup"><span data-stu-id="c8a0c-399">*This data set is used only in Linux environments.*</span></span>
- <span data-ttu-id="c8a0c-400">**Inventaire des Images de conteneur** -affiche le nombre total de hello d’images de conteneur utilisé et le nombre de types d’images.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-400">**Container Images Inventory** - Shows hello total number of container images used and number of image types.</span></span> <span data-ttu-id="c8a0c-401">nombre de Hello d’images est également répertorié par balise d’image hello.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-401">hello number of images are also listed by hello image tag.</span></span>
- <span data-ttu-id="c8a0c-402">**État de conteneurs** -affiche nombre total de hello du conteneur ordinateurs nœuds/hôte conteneurs en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-402">**Containers Status** - Shows hello total number of container nodes/host computers that have running containers.</span></span> <span data-ttu-id="c8a0c-403">Les ordinateurs sont également répertoriés par nombre hello des ordinateurs hôtes en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-403">Computers are also listed by hello number of running hosts.</span></span>
- <span data-ttu-id="c8a0c-404">**Processus de conteneur** : affiche un graphique en courbes représentant les processus de conteneur exécutés jusqu’à maintenant.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-404">**Container Process** - Shows a line chart of container processes running over time.</span></span> <span data-ttu-id="c8a0c-405">Les conteneurs peuvent également être répertoriés en exécutant la commande /process dans les conteneurs.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-405">Containers are also listed by running command/process within containers.</span></span> <span data-ttu-id="c8a0c-406">*Ce jeu de données est utilisé uniquement dans les environnements Linux.*</span><span class="sxs-lookup"><span data-stu-id="c8a0c-406">*This data set is used only in Linux environments.*</span></span>
- <span data-ttu-id="c8a0c-407">**Les performances de l’UC de conteneur** -affiche un graphique en courbes de hello utilisation moyenne du processeur au fil du temps pour les nœuds/hôtes d’ordinateur.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-407">**Container CPU Performance** - Shows a line chart of hello average CPU utilization over time for computer nodes/hosts.</span></span> <span data-ttu-id="c8a0c-408">Également listes hello ordinateur/hôtes de nœuds en fonction de moyenne de l’UC.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-408">Also lists hello computer nodes/hosts based on average CPU utilization.</span></span>
- <span data-ttu-id="c8a0c-409">**Performances de la mémoire du conteneur** : affiche un graphique en courbes représentant l’utilisation de la mémoire jusqu’à maintenant.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-409">**Container Memory Performance** - Shows a line chart of memory usage over time.</span></span> <span data-ttu-id="c8a0c-410">Répertorie également l’utilisation de la mémoire par l’ordinateur en fonction du nom de l’instance.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-410">Also lists computer memory utilization based on instance name.</span></span>
- <span data-ttu-id="c8a0c-411">**Performances de l’ordinateur** -affiche les graphiques en courbes de % hello de performances de l’UC au fil du temps, pourcentage d’utilisation de mémoire dans le temps et mégaoctets d’espace disque libre au fil du temps.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-411">**Computer Performance** - Shows line charts of hello percent of CPU performance over time, percent of memory usage over time, and megabytes of free disk space over time.</span></span> <span data-ttu-id="c8a0c-412">Vous pouvez pointer sur n’importe quelle ligne dans un graphique de tooview plus de détails.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-412">You can hover over any line in a chart tooview more details.</span></span>


<span data-ttu-id="c8a0c-413">Chaque zone du tableau de bord hello est une représentation visuelle d’une recherche qui est exécutée sur les données collectées.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-413">Each area of hello dashboard is a visual representation of a search that is run on collected data.</span></span>

![Tableau de bord Conteneurs](./media/log-analytics-containers/containers-dash01.png)

![Tableau de bord Conteneurs](./media/log-analytics-containers/containers-dash02.png)

<span data-ttu-id="c8a0c-416">Bonjour **état du conteneur** zone, cliquez sur zone supérieure de hello, comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-416">In hello **Container Status** area, click hello top area, as shown below.</span></span>

![État des conteneurs](./media/log-analytics-containers/containers-status.png)

<span data-ttu-id="c8a0c-418">Recherche de journal s’ouvre et affiche des informations sur l’état de hello vos conteneurs.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-418">Log Search opens, displaying information about hello state of your containers.</span></span>

![Recherche de journal pour les conteneurs](./media/log-analytics-containers/containers-log-search.png)

<span data-ttu-id="c8a0c-420">À ce stade, vous pouvez modifier toomodify de requête de recherche hello elle des informations spécifiques hello toofind vous intéresse.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-420">From here, you can edit hello search query toomodify it toofind hello specific information you're interested in.</span></span> <span data-ttu-id="c8a0c-421">Pour plus d’informations sur les recherches dans les journaux, voir [Recherches de journal dans Log Analytics](log-analytics-log-searches.md).</span><span class="sxs-lookup"><span data-stu-id="c8a0c-421">For more information about Log Searches, see [Log searches in Log Analytics](log-analytics-log-searches.md).</span></span>

## <a name="troubleshoot-by-finding-a-failed-container"></a><span data-ttu-id="c8a0c-422">Résoudre des problèmes en recherchant un conteneur en échec</span><span class="sxs-lookup"><span data-stu-id="c8a0c-422">Troubleshoot by finding a failed container</span></span>

<span data-ttu-id="c8a0c-423">Log Analytics marque un conteneur comme étant en **Échec** s’il a été fermé avec un code de sortie autre que zéro.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-423">Log Analytics marks a container as **Failed** if it has exited with a non-zero exit code.</span></span> <span data-ttu-id="c8a0c-424">Vous pouvez voir une vue d’ensemble des erreurs de hello et des défaillances dans un environnement hello Bonjour **Échec de conteneurs** zone.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-424">You can see an overview of hello errors and failures in hello environment in hello **Failed Containers** area.</span></span>

### <a name="toofind-failed-containers"></a><span data-ttu-id="c8a0c-425">conteneurs de toofind a échoué</span><span class="sxs-lookup"><span data-stu-id="c8a0c-425">toofind failed containers</span></span>
1. <span data-ttu-id="c8a0c-426">Cliquez sur hello **état du conteneur** zone.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-426">Click hello **Container Status** area.</span></span>  
   <span data-ttu-id="c8a0c-427">![État des conteneurs](./media/log-analytics-containers/containers-status.png)</span><span class="sxs-lookup"><span data-stu-id="c8a0c-427">![containers status](./media/log-analytics-containers/containers-status.png)</span></span>
2. <span data-ttu-id="c8a0c-428">Recherche de journal s’ouvre et affiche hello de l’état de vos conteneurs, toohello comme suit.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-428">Log Search opens and displays hello state of your containers, similar toohello following.</span></span>  
   ![État des conteneurs](./media/log-analytics-containers/containers-log-search.png)
3. <span data-ttu-id="c8a0c-430">Ensuite, cliquez sur la valeur hello agrégé des informations supplémentaires de tooview de conteneurs ayant échoué.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-430">Next, click hello aggregated value of failed containers tooview additional information.</span></span> <span data-ttu-id="c8a0c-431">Développez **afficher plus** tooview hello image ID.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-431">Expand **show more** tooview hello image ID.</span></span>  
   <span data-ttu-id="c8a0c-432">![Conteneurs défectueux](./media/log-analytics-containers/containers-state-failed.png)</span><span class="sxs-lookup"><span data-stu-id="c8a0c-432">![failed containers](./media/log-analytics-containers/containers-state-failed.png)</span></span>  
4. <span data-ttu-id="c8a0c-433">Ensuite, tapez hello texte suivant dans la requête de recherche hello.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-433">Next, type hello following in hello search query.</span></span> <span data-ttu-id="c8a0c-434">`Type=ContainerInventory <ImageID>`toosee des détails sur l’image hello telles que la taille de l’image et le nombre d’images arrêtés et a échoué.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-434">`Type=ContainerInventory <ImageID>` toosee details about hello image such as image size and number of stopped and failed images.</span></span>  
   <span data-ttu-id="c8a0c-435">![Conteneurs défectueux](./media/log-analytics-containers/containers-failed04.png)</span><span class="sxs-lookup"><span data-stu-id="c8a0c-435">![failed containers](./media/log-analytics-containers/containers-failed04.png)</span></span>

## <a name="search-logs-for-container-data"></a><span data-ttu-id="c8a0c-436">Rechercher des données de conteneur dans les journaux</span><span class="sxs-lookup"><span data-stu-id="c8a0c-436">Search logs for container data</span></span>
<span data-ttu-id="c8a0c-437">Lorsque vous êtes à résoudre une erreur spécifique, il peut aider à toosee où il se produit dans votre environnement.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-437">When you're troubleshooting a specific error, it can help toosee where it is occurring in your environment.</span></span> <span data-ttu-id="c8a0c-438">Hello, les types de journaux suivants vous aideront à créer des requêtes tooreturn hello informations.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-438">hello following log types will help you create queries tooreturn hello information you want.</span></span>


- <span data-ttu-id="c8a0c-439">**ContainerImageInventory** : utilisez ce type lorsque vous essayez d’informations toofind organisées par image et tooview image les informations telles que les ID d’image ou des tailles.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-439">**ContainerImageInventory** – Use this type when you're trying toofind information organized by image and tooview image information such as image IDs or sizes.</span></span>
- <span data-ttu-id="c8a0c-440">**ContainerInventory** : utilisez ce type de journal lorsque vous recherchez des informations sur l’emplacement des conteneurs, leurs noms et les images qu’ils exécutent.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-440">**ContainerInventory** – Use this type when you want information about container location, what their names are, and what images they're running.</span></span>
- <span data-ttu-id="c8a0c-441">**ContainerLog** : utilisez ce type lorsque vous souhaitez que les informations concernant les journaux d’erreurs toofind et les entrées.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-441">**ContainerLog** – Use this type when you want toofind specific error log information and entries.</span></span>
- <span data-ttu-id="c8a0c-442">**ContainerNodeInventory_CL** Utilisez ce type lorsque vous souhaitez que des informations sur le nœud d’hôte hello où résident des conteneurs.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-442">**ContainerNodeInventory_CL**  Use this type when you want hello information about host/node where containers are residing.</span></span> <span data-ttu-id="c8a0c-443">Il fournit la version Docker, le type d’orchestration, ainsi que des informations relatives au stockage et au réseau.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-443">It provides you Docker version, orchestration type, storage, and network information.</span></span>
- <span data-ttu-id="c8a0c-444">**ContainerProcess_CL** tooquickly de ce type d’utilisation Voir processus hello en cours d’exécution dans le conteneur de hello.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-444">**ContainerProcess_CL** Use this type tooquickly see hello process running within hello container.</span></span>
- <span data-ttu-id="c8a0c-445">**ContainerServiceLog** : utilisez ce type lorsque vous essayez d’informations de piste d’audit toofind pour hello démon Docker, telles que Démarrer, arrêter, supprimer ou extraire les commandes.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-445">**ContainerServiceLog** – Use this type when you're trying toofind audit trail information for hello Docker daemon, such as start, stop, delete, or pull commands.</span></span>
- <span data-ttu-id="c8a0c-446">**KubeEvents_CL** utiliser ce type toosee hello Kubernetes les événements.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-446">**KubeEvents_CL**  Use this type toosee hello Kubernetes events.</span></span>
- <span data-ttu-id="c8a0c-447">**KubePodInventory_CL** Utilisez ce type lorsque vous souhaitez que les informations de hiérarchie toounderstand hello cluster.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-447">**KubePodInventory_CL**  Use this type when you want toounderstand hello cluster hierarchy information.</span></span>


### <a name="toosearch-logs-for-container-data"></a><span data-ttu-id="c8a0c-448">journaux toosearch pour les données de conteneur</span><span class="sxs-lookup"><span data-stu-id="c8a0c-448">toosearch logs for container data</span></span>
* <span data-ttu-id="c8a0c-449">Choisissez une image que vous connaissez récemment a échoué et rechercher les journaux d’erreurs hello.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-449">Choose an image that you know has failed recently and find hello error logs for it.</span></span> <span data-ttu-id="c8a0c-450">Commencez par rechercher un nom de conteneur exécutant cette image avec une recherche **ContainerInventory**.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-450">Start by finding a container name that is running that image with a **ContainerInventory** search.</span></span> <span data-ttu-id="c8a0c-451">Par exemple, recherchez `Type=ContainerInventory ubuntu Failed`</span><span class="sxs-lookup"><span data-stu-id="c8a0c-451">For example, search for `Type=ContainerInventory ubuntu Failed`</span></span>  
    <span data-ttu-id="c8a0c-452">![Recherche de conteneurs Ubuntu](./media/log-analytics-containers/search-ubuntu.png)</span><span class="sxs-lookup"><span data-stu-id="c8a0c-452">![Search for Ubuntu containers](./media/log-analytics-containers/search-ubuntu.png)</span></span>

  <span data-ttu-id="c8a0c-453">Hello le nom du conteneur de hello ensuite trop**nom**et recherchez ces journaux.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-453">hello name of hello container next too**Name**, and search for those logs.</span></span> <span data-ttu-id="c8a0c-454">Dans cet exemple, il s’agit de `Type=ContainerLog cranky_stonebreaker`.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-454">In this example, it is `Type=ContainerLog cranky_stonebreaker`.</span></span>

<span data-ttu-id="c8a0c-455">**Afficher les informations de performances**</span><span class="sxs-lookup"><span data-stu-id="c8a0c-455">**View performance information**</span></span>

<span data-ttu-id="c8a0c-456">Lorsque vous êtes à partir de requêtes de tooconstruct, il peut aider à toosee ce qui est tout d’abord possible.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-456">When you're beginning tooconstruct queries, it can help toosee what's possible first.</span></span> <span data-ttu-id="c8a0c-457">Par exemple, toosee toutes les données de performances, essayez une requête large en tapant hello suivant recherche de requête.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-457">For example, toosee all performance data, try a broad query by typing hello following search query.</span></span>

```
Type=Perf
```

![Performances des conteneurs](./media/log-analytics-containers/containers-perf01.png)

<span data-ttu-id="c8a0c-459">Vous pouvez limiter les données de performances hello que vous voyez tooa les conteneur spécifique en tapant le nom hello de celui-ci toohello à droite de votre requête.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-459">You can scope hello performance data you're seeing tooa specific container by typing hello name of it toohello right of your query.</span></span>

```
Type=Perf <containerName>
```

<span data-ttu-id="c8a0c-460">Qui affiche la liste hello des métriques de performances sont collectées pour un conteneur.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-460">That shows hello list of performance metrics that are collected for an individual container.</span></span>

![Performances des conteneurs](./media/log-analytics-containers/containers-perf03.png)

## <a name="example-log-search-queries"></a><span data-ttu-id="c8a0c-462">Exemples de requêtes de recherche de journal</span><span class="sxs-lookup"><span data-stu-id="c8a0c-462">Example log search queries</span></span>
<span data-ttu-id="c8a0c-463">Toobuild souvent utile de ses requêtes en commençant par un exemple d’une ou deux, puis en modifiant les toofit votre environnement.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-463">It's often useful toobuild queries starting with an example or two and then modifying them toofit your environment.</span></span> <span data-ttu-id="c8a0c-464">Comme point de départ, vous pouvez expérimenter hello **exemples de requêtes** toohelp zone vous générez des requêtes plus avancées.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-464">As a starting point, you can experiment with hello **Sample Queries** area toohelp you build more advanced queries.</span></span>

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

![Requêtes de conteneurs](./media/log-analytics-containers/containers-queries.png)


## <a name="saving-log-search-queries"></a><span data-ttu-id="c8a0c-466">Enregistrement de requêtes de recherche de journal</span><span class="sxs-lookup"><span data-stu-id="c8a0c-466">Saving log search queries</span></span>
<span data-ttu-id="c8a0c-467">L’enregistrement des requêtes est une fonctionnalité standard dans Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-467">Saving queries is a standard feature in Log Analytics.</span></span> <span data-ttu-id="c8a0c-468">En les enregistrant, vous aurez aisément accès à celles que vous avez trouvées utiles pour une utilisation ultérieure.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-468">By saving them, you'll have those that you've found useful handy for future use.</span></span>

<span data-ttu-id="c8a0c-469">Après avoir créé une requête qui vous être utiles, l’enregistrer en cliquant sur **favoris** haut hello de page de recherche de journal hello.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-469">After you create a query that you find useful, save it by clicking **Favorites** at hello top of hello Log Search page.</span></span> <span data-ttu-id="c8a0c-470">Ensuite, vous pouvez facilement y accéder ultérieurement à partir de hello **mon tableau de bord** page.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-470">Then you can easily access it later from hello **My Dashboard** page.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c8a0c-471">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c8a0c-471">Next steps</span></span>
* <span data-ttu-id="c8a0c-472">[Rechercher des journaux](log-analytics-log-searches.md) tooview détaillé des enregistrements de données de conteneur.</span><span class="sxs-lookup"><span data-stu-id="c8a0c-472">[Search logs](log-analytics-log-searches.md) tooview detailed container data records.</span></span>
