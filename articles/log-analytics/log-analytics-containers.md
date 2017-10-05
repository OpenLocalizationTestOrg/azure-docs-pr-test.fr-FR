---
title: "Solution Container Monitoring d’Azure Log Analytics | Microsoft Docs"
description: "La solution Container Monitoring de Log Analytics vous aide à afficher et à gérer vos hôtes de conteneur Docker et Windows dans un emplacement unique."
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
ms.openlocfilehash: b2e03531ee401f4552198e5dd50fbfe1d970f0e5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="container-monitoring-solution-in-log-analytics"></a><span data-ttu-id="1cf30-103">Solution Container Monitoring dans Log Analytics</span><span class="sxs-lookup"><span data-stu-id="1cf30-103">Container Monitoring solution in Log Analytics</span></span>

![Symbole Containers](./media/log-analytics-containers/containers-symbol.png)

<span data-ttu-id="1cf30-105">Cet article explique comment configurer et utiliser la solution Container Monitoring de Log Analytics, qui vous permet d’afficher et de gérer vos hôtes de conteneur Docker et Windows dans un emplacement unique.</span><span class="sxs-lookup"><span data-stu-id="1cf30-105">This article describes how to set up and use the Container Monitoring solution in Log Analytics, which helps you view and manage your Docker and Windows container hosts in a single location.</span></span> <span data-ttu-id="1cf30-106">Docker est un système de virtualisation logicielle utilisé pour créer des conteneurs qui automatisent le déploiement de logiciels dans leur infrastructure informatique.</span><span class="sxs-lookup"><span data-stu-id="1cf30-106">Docker is a software virtualization system used to create containers that automate software deployment to their IT infrastructure.</span></span>

<span data-ttu-id="1cf30-107">La solution montre les conteneurs qui sont actuellement exécutés, l’image conteneur qu’ils exécutent et où ils s’exécutent.</span><span class="sxs-lookup"><span data-stu-id="1cf30-107">The solution shows which containers are running, what container image they’re running, and where containers are running.</span></span> <span data-ttu-id="1cf30-108">Vous pouvez afficher des informations d’audit détaillées montrant les commandes utilisées avec les conteneurs.</span><span class="sxs-lookup"><span data-stu-id="1cf30-108">You can view detailed audit information showing commands used with containers.</span></span> <span data-ttu-id="1cf30-109">Vous pouvez résoudre des problèmes de conteneurs en consultant des journaux centralisés et en y effectuant des recherches sans devoir afficher à distance les hôtes Docker ou Windows.</span><span class="sxs-lookup"><span data-stu-id="1cf30-109">And, you can troubleshoot containers by viewing and searching centralized logs without having to remotely view Docker or Windows hosts.</span></span> <span data-ttu-id="1cf30-110">Vous pouvez rechercher des conteneurs bruyants et consommant des ressources excessives sur un ordinateur hôte.</span><span class="sxs-lookup"><span data-stu-id="1cf30-110">You can find containers that may be noisy and consuming excess resources on a host.</span></span> <span data-ttu-id="1cf30-111">Et vous pouvez consulter des informations centralisées sur le processeur, la mémoire, le stockage ainsi que l’utilisation et les performances du réseau.</span><span class="sxs-lookup"><span data-stu-id="1cf30-111">And, you can view centralized CPU, memory, storage, and network usage and performance information for containers.</span></span> <span data-ttu-id="1cf30-112">Sur les ordinateurs exécutant Windows, vous pouvez centraliser et comparer les journaux des conteneurs Windows Server, Hyper-V et Docker.</span><span class="sxs-lookup"><span data-stu-id="1cf30-112">On computers running Windows, you can centralize and compare logs from Windows Server, Hyper-V, and Docker containers.</span></span> <span data-ttu-id="1cf30-113">La solution prend en charge les orchestrateurs de conteneur suivants :</span><span class="sxs-lookup"><span data-stu-id="1cf30-113">The solution supports the following container orchestrators:</span></span>

- <span data-ttu-id="1cf30-114">Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="1cf30-114">Docker Swarm</span></span>
- <span data-ttu-id="1cf30-115">DC/OS</span><span class="sxs-lookup"><span data-stu-id="1cf30-115">DC/OS</span></span>
- <span data-ttu-id="1cf30-116">kubernetes</span><span class="sxs-lookup"><span data-stu-id="1cf30-116">Kubernetes</span></span>
- <span data-ttu-id="1cf30-117">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="1cf30-117">Service Fabric</span></span>
- <span data-ttu-id="1cf30-118">Red Hat OpenShift</span><span class="sxs-lookup"><span data-stu-id="1cf30-118">Red Hat OpenShift</span></span>


<span data-ttu-id="1cf30-119">Le schéma suivant illustre les relations entre les différents hôtes de conteneurs et agents dans OMS.</span><span class="sxs-lookup"><span data-stu-id="1cf30-119">The following diagram shows the relationships between various container hosts and agents with OMS.</span></span>

![Schéma des conteneurs](./media/log-analytics-containers/containers-diagram.png)

## <a name="system-requirements"></a><span data-ttu-id="1cf30-121">Conditions requises pour le système</span><span class="sxs-lookup"><span data-stu-id="1cf30-121">System requirements</span></span>

<span data-ttu-id="1cf30-122">Avant de commencer, prenez connaissance des informations suivantes pour vérifier que les conditions préalables sont remplies.</span><span class="sxs-lookup"><span data-stu-id="1cf30-122">Before starting, review the following details to verify you meet the prerequisites.</span></span>

### <a name="container-monitoring-solution-support-for-docker-orchestrator-and-os-platform"></a><span data-ttu-id="1cf30-123">Prise en charge de solution de surveillance de conteneur pour la plateforme Docker Orchestrator et celle du système d’exploitation</span><span class="sxs-lookup"><span data-stu-id="1cf30-123">Container monitoring solution support for Docker Orchestrator and OS platform</span></span>
<span data-ttu-id="1cf30-124">Le tableau suivant présente l’orchestration de Docker et la prise en charge de la surveillance du système d’exploitation pour ce qui est des journaux, de la performance et de l’inventaire du conteneur avec Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="1cf30-124">The following table outlines the Docker orchestration and operating system monitoring support of container inventory, performance, and logs with Log Analytics.</span></span>   

| | <span data-ttu-id="1cf30-125">ACS</span><span class="sxs-lookup"><span data-stu-id="1cf30-125">ACS</span></span> | <span data-ttu-id="1cf30-126">Linux</span><span class="sxs-lookup"><span data-stu-id="1cf30-126">Linux</span></span> | <span data-ttu-id="1cf30-127">Windows</span><span class="sxs-lookup"><span data-stu-id="1cf30-127">Windows</span></span> | <span data-ttu-id="1cf30-128">Conteneur</span><span class="sxs-lookup"><span data-stu-id="1cf30-128">Container</span></span><br><span data-ttu-id="1cf30-129">Inventaire</span><span class="sxs-lookup"><span data-stu-id="1cf30-129">Inventory</span></span> | <span data-ttu-id="1cf30-130">Image</span><span class="sxs-lookup"><span data-stu-id="1cf30-130">Image</span></span><br><span data-ttu-id="1cf30-131">Inventaire</span><span class="sxs-lookup"><span data-stu-id="1cf30-131">Inventory</span></span> | <span data-ttu-id="1cf30-132">Nœud</span><span class="sxs-lookup"><span data-stu-id="1cf30-132">Node</span></span><br><span data-ttu-id="1cf30-133">Inventaire</span><span class="sxs-lookup"><span data-stu-id="1cf30-133">Inventory</span></span> | <span data-ttu-id="1cf30-134">Conteneur</span><span class="sxs-lookup"><span data-stu-id="1cf30-134">Container</span></span><br><span data-ttu-id="1cf30-135">Performances</span><span class="sxs-lookup"><span data-stu-id="1cf30-135">Performance</span></span> | <span data-ttu-id="1cf30-136">Conteneur</span><span class="sxs-lookup"><span data-stu-id="1cf30-136">Container</span></span><br><span data-ttu-id="1cf30-137">Événement</span><span class="sxs-lookup"><span data-stu-id="1cf30-137">Event</span></span> | <span data-ttu-id="1cf30-138">Événement</span><span class="sxs-lookup"><span data-stu-id="1cf30-138">Event</span></span><br><span data-ttu-id="1cf30-139">Journal</span><span class="sxs-lookup"><span data-stu-id="1cf30-139">Log</span></span> | <span data-ttu-id="1cf30-140">Conteneur</span><span class="sxs-lookup"><span data-stu-id="1cf30-140">Container</span></span><br><span data-ttu-id="1cf30-141">Journal</span><span class="sxs-lookup"><span data-stu-id="1cf30-141">Log</span></span> |
|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|
| <span data-ttu-id="1cf30-142">kubernetes</span><span class="sxs-lookup"><span data-stu-id="1cf30-142">Kubernetes</span></span> | <span data-ttu-id="1cf30-143">&#8226;</span><span class="sxs-lookup"><span data-stu-id="1cf30-143">&#8226;</span></span> | <span data-ttu-id="1cf30-144">&#8226;</span><span class="sxs-lookup"><span data-stu-id="1cf30-144">&#8226;</span></span> | | <span data-ttu-id="1cf30-145">&#8226;</span><span class="sxs-lookup"><span data-stu-id="1cf30-145">&#8226;</span></span> | <span data-ttu-id="1cf30-146">&#8226;</span><span class="sxs-lookup"><span data-stu-id="1cf30-146">&#8226;</span></span> | <span data-ttu-id="1cf30-147">&#8226;</span><span class="sxs-lookup"><span data-stu-id="1cf30-147">&#8226;</span></span> | <span data-ttu-id="1cf30-148">&#8226;</span><span class="sxs-lookup"><span data-stu-id="1cf30-148">&#8226;</span></span> | <span data-ttu-id="1cf30-149">&#8226;</span><span class="sxs-lookup"><span data-stu-id="1cf30-149">&#8226;</span></span> | <span data-ttu-id="1cf30-150">&#8226;</span><span class="sxs-lookup"><span data-stu-id="1cf30-150">&#8226;</span></span> | <span data-ttu-id="1cf30-151">&#8226;</span><span class="sxs-lookup"><span data-stu-id="1cf30-151">&#8226;</span></span> |
| <span data-ttu-id="1cf30-152">Mésosphère</span><span class="sxs-lookup"><span data-stu-id="1cf30-152">Mesosphere</span></span><br><span data-ttu-id="1cf30-153">DC/OS</span><span class="sxs-lookup"><span data-stu-id="1cf30-153">DC/OS</span></span> | <span data-ttu-id="1cf30-154">&#8226;</span><span class="sxs-lookup"><span data-stu-id="1cf30-154">&#8226;</span></span> | <span data-ttu-id="1cf30-155">&#8226;</span><span class="sxs-lookup"><span data-stu-id="1cf30-155">&#8226;</span></span> | | <span data-ttu-id="1cf30-156">&#8226;</span><span class="sxs-lookup"><span data-stu-id="1cf30-156">&#8226;</span></span> | <span data-ttu-id="1cf30-157">&#8226;</span><span class="sxs-lookup"><span data-stu-id="1cf30-157">&#8226;</span></span> | <span data-ttu-id="1cf30-158">&#8226;</span><span class="sxs-lookup"><span data-stu-id="1cf30-158">&#8226;</span></span> | <span data-ttu-id="1cf30-159">&#8226;</span><span class="sxs-lookup"><span data-stu-id="1cf30-159">&#8226;</span></span>| <span data-ttu-id="1cf30-160">&#8226;</span><span class="sxs-lookup"><span data-stu-id="1cf30-160">&#8226;</span></span> | <span data-ttu-id="1cf30-161">&#8226;</span><span class="sxs-lookup"><span data-stu-id="1cf30-161">&#8226;</span></span> | <span data-ttu-id="1cf30-162">&#8226;</span><span class="sxs-lookup"><span data-stu-id="1cf30-162">&#8226;</span></span> |
| <span data-ttu-id="1cf30-163">Docker</span><span class="sxs-lookup"><span data-stu-id="1cf30-163">Docker</span></span><br><span data-ttu-id="1cf30-164">Swarm</span><span class="sxs-lookup"><span data-stu-id="1cf30-164">Swarm</span></span> | <span data-ttu-id="1cf30-165">&#8226;</span><span class="sxs-lookup"><span data-stu-id="1cf30-165">&#8226;</span></span> | <span data-ttu-id="1cf30-166">&#8226;</span><span class="sxs-lookup"><span data-stu-id="1cf30-166">&#8226;</span></span> | <span data-ttu-id="1cf30-167">&#8226;</span><span class="sxs-lookup"><span data-stu-id="1cf30-167">&#8226;</span></span> | <span data-ttu-id="1cf30-168">&#8226;</span><span class="sxs-lookup"><span data-stu-id="1cf30-168">&#8226;</span></span> | <span data-ttu-id="1cf30-169">&#8226;</span><span class="sxs-lookup"><span data-stu-id="1cf30-169">&#8226;</span></span> | <span data-ttu-id="1cf30-170">&#8226;</span><span class="sxs-lookup"><span data-stu-id="1cf30-170">&#8226;</span></span> | <span data-ttu-id="1cf30-171">&#8226;</span><span class="sxs-lookup"><span data-stu-id="1cf30-171">&#8226;</span></span> | <span data-ttu-id="1cf30-172">&#8226;</span><span class="sxs-lookup"><span data-stu-id="1cf30-172">&#8226;</span></span> | | <span data-ttu-id="1cf30-173">&#8226;</span><span class="sxs-lookup"><span data-stu-id="1cf30-173">&#8226;</span></span> |
| <span data-ttu-id="1cf30-174">Service</span><span class="sxs-lookup"><span data-stu-id="1cf30-174">Service</span></span><br><span data-ttu-id="1cf30-175">Structure</span><span class="sxs-lookup"><span data-stu-id="1cf30-175">Fabric</span></span> | | | <span data-ttu-id="1cf30-176">&#8226;</span><span class="sxs-lookup"><span data-stu-id="1cf30-176">&#8226;</span></span> | <span data-ttu-id="1cf30-177">&#8226;</span><span class="sxs-lookup"><span data-stu-id="1cf30-177">&#8226;</span></span> | <span data-ttu-id="1cf30-178">&#8226;</span><span class="sxs-lookup"><span data-stu-id="1cf30-178">&#8226;</span></span> | <span data-ttu-id="1cf30-179">&#8226;</span><span class="sxs-lookup"><span data-stu-id="1cf30-179">&#8226;</span></span> | <span data-ttu-id="1cf30-180">&#8226;</span><span class="sxs-lookup"><span data-stu-id="1cf30-180">&#8226;</span></span> | <span data-ttu-id="1cf30-181">&#8226;</span><span class="sxs-lookup"><span data-stu-id="1cf30-181">&#8226;</span></span> | <span data-ttu-id="1cf30-182">&#8226;</span><span class="sxs-lookup"><span data-stu-id="1cf30-182">&#8226;</span></span> | <span data-ttu-id="1cf30-183">&#8226;</span><span class="sxs-lookup"><span data-stu-id="1cf30-183">&#8226;</span></span> |
| <span data-ttu-id="1cf30-184">Red Hat Open</span><span class="sxs-lookup"><span data-stu-id="1cf30-184">Red Hat Open</span></span><br><span data-ttu-id="1cf30-185">Shift</span><span class="sxs-lookup"><span data-stu-id="1cf30-185">Shift</span></span> | | <span data-ttu-id="1cf30-186">&#8226;</span><span class="sxs-lookup"><span data-stu-id="1cf30-186">&#8226;</span></span> | | <span data-ttu-id="1cf30-187">&#8226;</span><span class="sxs-lookup"><span data-stu-id="1cf30-187">&#8226;</span></span> | <span data-ttu-id="1cf30-188">&#8226;</span><span class="sxs-lookup"><span data-stu-id="1cf30-188">&#8226;</span></span>| <span data-ttu-id="1cf30-189">&#8226;</span><span class="sxs-lookup"><span data-stu-id="1cf30-189">&#8226;</span></span> | <span data-ttu-id="1cf30-190">&#8226;</span><span class="sxs-lookup"><span data-stu-id="1cf30-190">&#8226;</span></span> | <span data-ttu-id="1cf30-191">&#8226;</span><span class="sxs-lookup"><span data-stu-id="1cf30-191">&#8226;</span></span> | | <span data-ttu-id="1cf30-192">&#8226;</span><span class="sxs-lookup"><span data-stu-id="1cf30-192">&#8226;</span></span> |
| <span data-ttu-id="1cf30-193">Windows Server</span><span class="sxs-lookup"><span data-stu-id="1cf30-193">Windows Server</span></span><br><span data-ttu-id="1cf30-194">(autonome)</span><span class="sxs-lookup"><span data-stu-id="1cf30-194">(standalone)</span></span> | | | <span data-ttu-id="1cf30-195">&#8226;</span><span class="sxs-lookup"><span data-stu-id="1cf30-195">&#8226;</span></span> | <span data-ttu-id="1cf30-196">&#8226;</span><span class="sxs-lookup"><span data-stu-id="1cf30-196">&#8226;</span></span> | <span data-ttu-id="1cf30-197">&#8226;</span><span class="sxs-lookup"><span data-stu-id="1cf30-197">&#8226;</span></span> | <span data-ttu-id="1cf30-198">&#8226;</span><span class="sxs-lookup"><span data-stu-id="1cf30-198">&#8226;</span></span> | <span data-ttu-id="1cf30-199">&#8226;</span><span class="sxs-lookup"><span data-stu-id="1cf30-199">&#8226;</span></span> | <span data-ttu-id="1cf30-200">&#8226;</span><span class="sxs-lookup"><span data-stu-id="1cf30-200">&#8226;</span></span> | | <span data-ttu-id="1cf30-201">&#8226;</span><span class="sxs-lookup"><span data-stu-id="1cf30-201">&#8226;</span></span> |
| <span data-ttu-id="1cf30-202">Serveur Linux</span><span class="sxs-lookup"><span data-stu-id="1cf30-202">Linux Server</span></span><br><span data-ttu-id="1cf30-203">(autonome)</span><span class="sxs-lookup"><span data-stu-id="1cf30-203">(standalone)</span></span> | | <span data-ttu-id="1cf30-204">&#8226;</span><span class="sxs-lookup"><span data-stu-id="1cf30-204">&#8226;</span></span> | | <span data-ttu-id="1cf30-205">&#8226;</span><span class="sxs-lookup"><span data-stu-id="1cf30-205">&#8226;</span></span> | <span data-ttu-id="1cf30-206">&#8226;</span><span class="sxs-lookup"><span data-stu-id="1cf30-206">&#8226;</span></span> | <span data-ttu-id="1cf30-207">&#8226;</span><span class="sxs-lookup"><span data-stu-id="1cf30-207">&#8226;</span></span> | <span data-ttu-id="1cf30-208">&#8226;</span><span class="sxs-lookup"><span data-stu-id="1cf30-208">&#8226;</span></span> | <span data-ttu-id="1cf30-209">&#8226;</span><span class="sxs-lookup"><span data-stu-id="1cf30-209">&#8226;</span></span> | | <span data-ttu-id="1cf30-210">&#8226;</span><span class="sxs-lookup"><span data-stu-id="1cf30-210">&#8226;</span></span> |


### <a name="docker-versions-supported-on-linux"></a><span data-ttu-id="1cf30-211">Versions de Docker prises en charge sur Linux</span><span class="sxs-lookup"><span data-stu-id="1cf30-211">Docker versions supported on Linux</span></span>

- <span data-ttu-id="1cf30-212">Docker 1.11 à 1.13</span><span class="sxs-lookup"><span data-stu-id="1cf30-212">Docker 1.11 to 1.13</span></span>
- <span data-ttu-id="1cf30-213">Docker CE et EE v17.06</span><span class="sxs-lookup"><span data-stu-id="1cf30-213">Docker CE and EE v17.06</span></span>

### <a name="x64-linux-distributions-supported-as-container-hosts"></a><span data-ttu-id="1cf30-214">Distributions Linux x64 suivantes prises en charge en tant qu’hôtes de conteneur</span><span class="sxs-lookup"><span data-stu-id="1cf30-214">x64 Linux distributions supported as container hosts</span></span>

- <span data-ttu-id="1cf30-215">Ubuntu 14.04 LTS et 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="1cf30-215">Ubuntu 14.04 LTS and 16.04 LTS</span></span>
- <span data-ttu-id="1cf30-216">CoreOS(stable)</span><span class="sxs-lookup"><span data-stu-id="1cf30-216">CoreOS(stable)</span></span>
- <span data-ttu-id="1cf30-217">Amazon Linux 2016.09.0</span><span class="sxs-lookup"><span data-stu-id="1cf30-217">Amazon Linux 2016.09.0</span></span>
- <span data-ttu-id="1cf30-218">openSUSE 13.2</span><span class="sxs-lookup"><span data-stu-id="1cf30-218">openSUSE 13.2</span></span>
- <span data-ttu-id="1cf30-219">openSUSE LEAP 42.2</span><span class="sxs-lookup"><span data-stu-id="1cf30-219">openSUSE LEAP 42.2</span></span>
- <span data-ttu-id="1cf30-220">CentOS 7.2 et 7.3</span><span class="sxs-lookup"><span data-stu-id="1cf30-220">CentOS 7.2 and 7.3</span></span>
- <span data-ttu-id="1cf30-221">SLES 12</span><span class="sxs-lookup"><span data-stu-id="1cf30-221">SLES 12</span></span>
- <span data-ttu-id="1cf30-222">RHEL 7.2 et 7.3</span><span class="sxs-lookup"><span data-stu-id="1cf30-222">RHEL 7.2 and 7.3</span></span>
- <span data-ttu-id="1cf30-223">Red Hat OpenShift Container Platform (OCP) 3.4 et 3.5</span><span class="sxs-lookup"><span data-stu-id="1cf30-223">Red Hat OpenShift Container Platform (OCP) 3.4 and 3.5</span></span>
- <span data-ttu-id="1cf30-224">ACS Mesosphere DC/OS 1.7.3 à 1.8.8</span><span class="sxs-lookup"><span data-stu-id="1cf30-224">ACS Mesosphere DC/OS 1.7.3 to 1.8.8</span></span>
- <span data-ttu-id="1cf30-225">ACS Kubernetes 1.4.5 à 1.6</span><span class="sxs-lookup"><span data-stu-id="1cf30-225">ACS Kubernetes 1.4.5 to 1.6</span></span>
- <span data-ttu-id="1cf30-226">ACS Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="1cf30-226">ACS Docker Swarm</span></span>

### <a name="supported-windows-operating-system"></a><span data-ttu-id="1cf30-227">Système d’exploitation Windows pris en charge</span><span class="sxs-lookup"><span data-stu-id="1cf30-227">Supported Windows operating system</span></span>

- <span data-ttu-id="1cf30-228">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="1cf30-228">Windows Server 2016</span></span>
- <span data-ttu-id="1cf30-229">Édition Anniversaire Windows 10 (Professionnel ou Entreprise)</span><span class="sxs-lookup"><span data-stu-id="1cf30-229">Windows 10 Anniversary Edition (Professional or Enterprise)</span></span>

### <a name="docker-versions-supported-on-windows"></a><span data-ttu-id="1cf30-230">Versions de docker prises en charge sur Windows</span><span class="sxs-lookup"><span data-stu-id="1cf30-230">Docker versions supported on Windows</span></span>

- <span data-ttu-id="1cf30-231">Docker 1.12 et 1.13</span><span class="sxs-lookup"><span data-stu-id="1cf30-231">Docker 1.12 and 1.13</span></span>
- <span data-ttu-id="1cf30-232">Docker 17.03.0 et versions ultérieures</span><span class="sxs-lookup"><span data-stu-id="1cf30-232">Docker 17.03.0 and later</span></span>

## <a name="installing-and-configuring-the-solution"></a><span data-ttu-id="1cf30-233">Installation et configuration de la solution</span><span class="sxs-lookup"><span data-stu-id="1cf30-233">Installing and configuring the solution</span></span>
<span data-ttu-id="1cf30-234">Utilisez les informations suivantes pour installer et configurer la solution.</span><span class="sxs-lookup"><span data-stu-id="1cf30-234">Use the following information to install and configure the solution.</span></span>

1. <span data-ttu-id="1cf30-235">Ajoutez la solution Container Monitoring à votre espace de travail OMS depuis la [Place de marché Azure](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.ContainersOMS?tab=Overview) ou en procédant de la manière décrite dans [Ajouter des solutions Log Analytics à partir de la galerie de solutions](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="1cf30-235">Add the Container Monitoring solution to your OMS workspace from [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.ContainersOMS?tab=Overview) or by using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span>

2. <span data-ttu-id="1cf30-236">Installez et utilisez Docker avec un agent OMS.</span><span class="sxs-lookup"><span data-stu-id="1cf30-236">Install and use Docker with an OMS agent.</span></span>  <span data-ttu-id="1cf30-237">Selon votre système d’exploitation, vous pouvez choisir parmi les méthodes suivantes :</span><span class="sxs-lookup"><span data-stu-id="1cf30-237">Based on your operating system, you can choose from the following methods:</span></span>

  * <span data-ttu-id="1cf30-238">Sur les systèmes d’exploitation Linux pris en charge, installez et exécutez Docker, puis installez et configurez [l’Agent OMS pour Linux](log-analytics-agent-linux.md).</span><span class="sxs-lookup"><span data-stu-id="1cf30-238">On supported Linux operating systems, install and run Docker and then install and configure the [OMS Agent for Linux](log-analytics-agent-linux.md).</span></span>  
  * <span data-ttu-id="1cf30-239">Sur CoreOS, vous ne pouvez pas exécuter l’Agent OMS pour Linux.</span><span class="sxs-lookup"><span data-stu-id="1cf30-239">On CoreOS, you cannot run the OMS Agent for Linux.</span></span> <span data-ttu-id="1cf30-240">Au lieu de cela, vous exécutez une version en conteneur de l’Agent OMS pour Linux.</span><span class="sxs-lookup"><span data-stu-id="1cf30-240">Instead, you run a containerized version of the OMS Agent for Linux.</span></span> <span data-ttu-id="1cf30-241">Si vous utilisez des conteneurs dans Azure Government Cloud, consultez les sections relatives aux [hôtes de conteneurs Linux, y compris CoreOS](#for-all-linux-container-hosts-including-coreos) ou aux [hôtes de conteneurs Linux Azure Government, y compris CoreOS](#for-all-azure-government-linux-container-hosts-including-coreos).</span><span class="sxs-lookup"><span data-stu-id="1cf30-241">Review [Linux container hosts including CoreOS](#for-all-linux-container-hosts-including-coreos) or [Azure Government Linux container hosts including CoreOS](#for-all-azure-government-linux-container-hosts-including-coreos) if you are working with containers in Azure Government Cloud.</span></span>
  * <span data-ttu-id="1cf30-242">Sur Windows Server 2016 et Windows 10, installez le moteur et le client Docker, puis connectez un agent afin de collecter les données et les transmettre à Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="1cf30-242">On Windows Server 2016 and Windows 10, install the Docker Engine and client then connect an agent to gather information and send it to Log Analytics.</span></span>  

### <a name="container-services"></a><span data-ttu-id="1cf30-243">Services de conteneur</span><span class="sxs-lookup"><span data-stu-id="1cf30-243">Container services</span></span>

- <span data-ttu-id="1cf30-244">Si vous disposez d’un environnement Red Hat OpenShift, consultez [Configurer un agent OMS pour Red Hat OpenShift](#configure-an-oms-agent-for-red-hat-openshift).</span><span class="sxs-lookup"><span data-stu-id="1cf30-244">If you have a Red Hat OpenShift environment, review [Configure an OMS agent for Red Hat OpenShift](#configure-an-oms-agent-for-red-hat-openshift).</span></span>
- <span data-ttu-id="1cf30-245">Si vous disposez d’un cluster Kubernetes qui utilise Azure Container Service, consultez [Surveiller un cluster Azure Container Service avec Microsoft Operations Management Suite (OMS)](../container-service/kubernetes/container-service-kubernetes-oms.md).</span><span class="sxs-lookup"><span data-stu-id="1cf30-245">If you have a Kubernetes cluster using the Azure Container Service, review [Monitor an Azure Container Service cluster with Microsoft Operations Management Suite (OMS)](../container-service/kubernetes/container-service-kubernetes-oms.md).</span></span>
- <span data-ttu-id="1cf30-246">Si vous possédez un cluster DC/OS Azure Container Service, consultez l’article [Surveiller un cluster DC/OS Azure Container Service avec Operations Management Suite](../container-service/dcos-swarm/container-service-monitoring-oms.md).</span><span class="sxs-lookup"><span data-stu-id="1cf30-246">If you have an Azure Container Service DC/OS cluster, learn more at [Monitor an Azure Container Service DC/OS cluster with Operations Management Suite](../container-service/dcos-swarm/container-service-monitoring-oms.md).</span></span>
- <span data-ttu-id="1cf30-247">Si vous avez un environnement en mode Docker Swarm, apprenez en plus en lisant [Configurer un agent OMS pour Docker Swarm](#configure-an-oms-agent-for-docker-swarm).</span><span class="sxs-lookup"><span data-stu-id="1cf30-247">If you have a Docker Swarm mode environment, learn more at [Configure an OMS agent for Docker Swarm](#configure-an-oms-agent-for-docker-swarm).</span></span>
- <span data-ttu-id="1cf30-248">Si vous utilisez des conteneurs avec Service Fabric, consultez [Vue d’ensemble d’Azure Service Fabric](../service-fabric/service-fabric-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1cf30-248">If you use containers with Service Fabric, learn more at [Overview of Azure Service Fabric](../service-fabric/service-fabric-overview.md).</span></span>
- <span data-ttu-id="1cf30-249">Examinez l’article relatif au [moteur Docker sur Windows](https://docs.microsoft.com/virtualization/windowscontainers/manage-docker/configure-docker-daemon) pour en savoir plus sur l’installation et la configuration de vos moteurs Docker sur les ordinateurs exécutant Windows.</span><span class="sxs-lookup"><span data-stu-id="1cf30-249">Review the [Docker Engine on Windows](https://docs.microsoft.com/virtualization/windowscontainers/manage-docker/configure-docker-daemon) article for additional information about how to install and configure your Docker Engines on computers running Windows.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1cf30-250">Docker doit être en cours d’exécution **avant** l’installation de l’[Agent OMS pour Linux](log-analytics-agent-linux.md) sur vos hôtes de conteneur.</span><span class="sxs-lookup"><span data-stu-id="1cf30-250">Docker must be running **before** you install the [OMS Agent for Linux](log-analytics-agent-linux.md) on your container hosts.</span></span> <span data-ttu-id="1cf30-251">Si vous avez installé l’agent avant d’installer Docker, vous devez réinstaller l’agent OMS pour Linux.</span><span class="sxs-lookup"><span data-stu-id="1cf30-251">If you've already installed the agent before installing Docker, you need to reinstall the OMS Agent for Linux.</span></span> <span data-ttu-id="1cf30-252">Pour plus d’informations sur Docker, voir le [site web Docker](https://www.docker.com).</span><span class="sxs-lookup"><span data-stu-id="1cf30-252">For more information about Docker, see the [Docker website](https://www.docker.com).</span></span>


## <a name="linux-container-hosts"></a><span data-ttu-id="1cf30-253">Hôtes de conteneur Linux</span><span class="sxs-lookup"><span data-stu-id="1cf30-253">Linux container hosts</span></span>

<span data-ttu-id="1cf30-254">Après avoir installé Docker, utilisez les paramètres suivants pour votre hôte de conteneur afin de configurer l’agent en vue d’une utilisation avec Docker.</span><span class="sxs-lookup"><span data-stu-id="1cf30-254">After you've installed Docker, use the following settings for your container host to configure the agent for use with Docker.</span></span> <span data-ttu-id="1cf30-255">Tout d’abord, vous avez besoin de l’ID et de la clé de votre espace de travail OMS, qui se trouvent dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="1cf30-255">First you need your OMS workspace ID and key, which you can find in the Azure portal.</span></span> <span data-ttu-id="1cf30-256">Dans votre espace de travail, cliquez sur **Démarrage rapide** > **Ordinateurs** pour afficher votre **ID d’espace de travail** et votre **Clé primaire**.</span><span class="sxs-lookup"><span data-stu-id="1cf30-256">In your workspace, click **Quick Start** > **Computers** to view your **Workspace ID** and **Primary Key**.</span></span>  <span data-ttu-id="1cf30-257">Copiez-collez ces deux valeurs dans votre éditeur favori.</span><span class="sxs-lookup"><span data-stu-id="1cf30-257">Copy and paste both into your favorite editor.</span></span>

### <a name="for-all-linux-container-hosts-except-coreos"></a><span data-ttu-id="1cf30-258">Pour tous les hôtes de conteneur Linux, à l’exception de CoreOS</span><span class="sxs-lookup"><span data-stu-id="1cf30-258">For all Linux container hosts except CoreOS</span></span>

- <span data-ttu-id="1cf30-259">Pour plus d’informations sur l’installation de l’agent OMS pour Linux, consultez [Connecter des ordinateurs Linux à Operations Management Suite (OMS)](log-analytics-agent-linux.md).</span><span class="sxs-lookup"><span data-stu-id="1cf30-259">For more information and steps on how to install the OMS Agent for Linux, see [Connect your Linux Computers to Operations Management Suite (OMS)](log-analytics-agent-linux.md).</span></span>

### <a name="for-all-linux-container-hosts-including-coreos"></a><span data-ttu-id="1cf30-260">Pour tous les hôtes de conteneur Linux, avec CoreOS</span><span class="sxs-lookup"><span data-stu-id="1cf30-260">For all Linux container hosts including CoreOS</span></span>

<span data-ttu-id="1cf30-261">Démarrez le conteneur OMS que vous souhaitez analyser.</span><span class="sxs-lookup"><span data-stu-id="1cf30-261">Start the OMS container that you want to monitor.</span></span> <span data-ttu-id="1cf30-262">Modifiez et utilisez l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="1cf30-262">Modify and use the following example:</span></span>

```
sudo docker run --privileged -d -v /var/run/docker.sock:/var/run/docker.sock -e WSID="your workspace id" -e KEY="your key" -h=`hostname` -p 127.0.0.1:25225:25225 --name="omsagent" --restart=always microsoft/oms
```

### <a name="for-all-azure-government-linux-container-hosts-including-coreos"></a><span data-ttu-id="1cf30-263">Pour tous les hôtes de conteneur Linux Azure Government, y compris CoreOS</span><span class="sxs-lookup"><span data-stu-id="1cf30-263">For all Azure Government Linux container hosts including CoreOS</span></span>

<span data-ttu-id="1cf30-264">Démarrez le conteneur OMS que vous souhaitez analyser.</span><span class="sxs-lookup"><span data-stu-id="1cf30-264">Start the OMS container that you want to monitor.</span></span> <span data-ttu-id="1cf30-265">Modifiez et utilisez l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="1cf30-265">Modify and use the following example:</span></span>

```
sudo docker run --privileged -d -v /var/run/docker.sock:/var/run/docker.sock -v /var/log:/var/log -e WSID="your workspace id" -e KEY="your key" -e DOMAIN="opinsights.azure.us" -p 127.0.0.1:25225:25225 -p 127.0.0.1:25224:25224/udp --name="omsagent" -h=`hostname` --restart=always microsoft/oms
```

### <a name="switching-from-using-an-installed-linux-agent-to-one-in-a-container"></a><span data-ttu-id="1cf30-266">Passage de l’utilisation d’un agent installé Linux à un agent dans un conteneur</span><span class="sxs-lookup"><span data-stu-id="1cf30-266">Switching from using an installed Linux agent to one in a container</span></span>
<span data-ttu-id="1cf30-267">Si vous utilisiez précédemment l’agent directement installé et souhaitez désormais utiliser un agent qui s’exécute dans un conteneur, vous devez commencer par supprimer l’agent OMS pour Linux.</span><span class="sxs-lookup"><span data-stu-id="1cf30-267">If you previously used the directly-installed agent and want to instead use an agent running in a container, you must first remove the OMS Agent for Linux.</span></span> <span data-ttu-id="1cf30-268">Pour comprendre comment désinstaller l’agent, consultez [Désinstallation de l’Agent OMS pour Linux](log-analytics-agent-linux.md#uninstalling-the-oms-agent-for-linux).</span><span class="sxs-lookup"><span data-stu-id="1cf30-268">See [Uninstalling the OMS Agent for Linux](log-analytics-agent-linux.md#uninstalling-the-oms-agent-for-linux) to understand how to successfully uninstall the agent.</span></span>  

### <a name="configure-an-oms-agent-for-docker-swarm"></a><span data-ttu-id="1cf30-269">Configurer un agent OMS pour Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="1cf30-269">Configure an OMS agent for Docker Swarm</span></span>

<span data-ttu-id="1cf30-270">Vous pouvez exécuter l’agent OMS en tant que service global sur Docker Swarm.</span><span class="sxs-lookup"><span data-stu-id="1cf30-270">You can run the OMS Agent as a global service on Docker Swarm.</span></span> <span data-ttu-id="1cf30-271">Utilisez les informations suivantes pour créer un service d’agent OMS.</span><span class="sxs-lookup"><span data-stu-id="1cf30-271">Use the following information to create an OMS Agent service.</span></span> <span data-ttu-id="1cf30-272">Vous devez insérer l’ID de votre espace de travail OMS et votre clé primaire.</span><span class="sxs-lookup"><span data-stu-id="1cf30-272">You need to insert your OMS Workspace ID and Primary Key.</span></span>

- <span data-ttu-id="1cf30-273">Exécutez la commande suivante sur le nœud principal.</span><span class="sxs-lookup"><span data-stu-id="1cf30-273">Run the following on the master node.</span></span>

    ```
    sudo docker service create  --name omsagent --mode global  --mount type=bind,source=/var/run/docker.sock,destination=/var/run/docker.sock  -e WSID="<WORKSPACE ID>" -e KEY="<PRIMARY KEY>" -p 25225:25225 -p 25224:25224/udp  --restart-condition=on-failure microsoft/oms
    ```

### <a name="configure-an-oms-agent-for-red-hat-openshift"></a><span data-ttu-id="1cf30-274">Configurer un agent OMS pour Red Hat OpenShift</span><span class="sxs-lookup"><span data-stu-id="1cf30-274">Configure an OMS Agent for Red Hat OpenShift</span></span>
<span data-ttu-id="1cf30-275">Il existe trois façons d’ajouter l’agent OMS pour Red Hat OpenShift dans le but de démarrer la collecte des données de surveillance des conteneurs.</span><span class="sxs-lookup"><span data-stu-id="1cf30-275">There are three ways to add the OMS Agent to Red Hat OpenShift to start collecting container monitoring data.</span></span>

* <span data-ttu-id="1cf30-276">[Installer l’agent OMS pour Linux](log-analytics-agent-linux.md) directement sur chaque nœud OpenShift</span><span class="sxs-lookup"><span data-stu-id="1cf30-276">[Install the OMS Agent for Linux](log-analytics-agent-linux.md) directly on each OpenShift node</span></span>  
* <span data-ttu-id="1cf30-277">[Activer l’extension de machine virtuelle Log Analytics](log-analytics-azure-vm-extension.md) sur chaque nœud OpenShift résidant dans Azure</span><span class="sxs-lookup"><span data-stu-id="1cf30-277">[Enable Log Analytics VM Extension](log-analytics-azure-vm-extension.md) on each OpenShift node residing in Azure</span></span>  
* <span data-ttu-id="1cf30-278">Installer l’agent OMS comme un daemon-set OpenShift</span><span class="sxs-lookup"><span data-stu-id="1cf30-278">Install the OMS Agent as a OpenShift daemon-set</span></span>  

<span data-ttu-id="1cf30-279">Dans cette section, nous allons aborder les étapes nécessaires à l’installation de l’agent OMS comme un daemon-set OpenShift.</span><span class="sxs-lookup"><span data-stu-id="1cf30-279">In this section we cover the steps required to install the OMS Agent as an OpenShift daemon-set.</span></span>  

1. <span data-ttu-id="1cf30-280">Connectez-vous au nœud principal OpenShift, puis copiez le fichier yaml [ocp-omsagent.yaml](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-omsagent.yaml) de GitHub vers votre nœud principal. Ensuite, remplacez la valeur par l’ID de votre espace de travail OMS et votre clé primaire.</span><span class="sxs-lookup"><span data-stu-id="1cf30-280">Sign on to the OpenShift master node and copy the yaml file [ocp-omsagent.yaml](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-omsagent.yaml) from GitHub to your master node and modify the value with your OMS Workspace ID and with your Primary Key.</span></span>
2. <span data-ttu-id="1cf30-281">Exécutez les commandes suivantes pour créer un projet OMS et configurer le compte d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="1cf30-281">Run the following commands to create a project for OMS and set the user account.</span></span>

    ```
    oadm new-project omslogging --node-selector='zone=default'
    oc project omslogging  
    oc create serviceaccount omsagent  
    oadm policy add-cluster-role-to-user cluster-reader   system:serviceaccount:omslogging:omsagent  
    oadm policy add-scc-to-user privileged system:serviceaccount:omslogging:omsagent  
    ```

4. <span data-ttu-id="1cf30-282">Pour déployer le daemon-set, exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="1cf30-282">To deploy the daemon-set, run the following:</span></span>

    `oc create -f ocp-omsagent.yaml`

5. <span data-ttu-id="1cf30-283">Pour vérifier qu’il est configuré et fonctionne correctement, tapez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="1cf30-283">To verify it is configured and working correctly, type the following:</span></span>

    `oc describe daemonset omsagent`  

    <span data-ttu-id="1cf30-284">La sortie doit ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="1cf30-284">and the output should resemble:</span></span>

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

<span data-ttu-id="1cf30-285">Si vous souhaitez utiliser des secrets pour sécuriser l’ID de votre espace de travail OMS et votre clé primaire lorsque vous utilisez le fichier yaml daemon-set de l’agent OMS, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="1cf30-285">If you want to use secrets to secure your OMS Workspace ID and Primary Key when using the OMS Agent daemon-set yaml file, perform the following steps.</span></span>

1. <span data-ttu-id="1cf30-286">Connectez-vous au nœud principal OpenShift, puis copiez le fichier yaml [ocp-ds-omsagent.yaml](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-ds-omsagent.yaml) et le script de génération de secrets [ocp-secretgen.sh](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-secretgen.sh) à partir de GitHub.</span><span class="sxs-lookup"><span data-stu-id="1cf30-286">Sign on to the OpenShift master node and copy the yaml file [ocp-ds-omsagent.yaml](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-ds-omsagent.yaml) and secret generating script [ocp-secretgen.sh](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-secretgen.sh) from GitHub.</span></span>  <span data-ttu-id="1cf30-287">Ce script va générer le fichier yaml de secrets pour l’ID d’espace de travail OMS et la clé primaire afin de sécuriser vos informations secrètes.</span><span class="sxs-lookup"><span data-stu-id="1cf30-287">This script will generate the secrets yaml file for OMS Workspace ID and Primary Key to secure your secrete information.</span></span>  
2. <span data-ttu-id="1cf30-288">Exécutez les commandes suivantes pour créer un projet OMS et configurer le compte d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="1cf30-288">Run the following commands to create a project for OMS and set the user account.</span></span> <span data-ttu-id="1cf30-289">Le script de génération de secrets vous demande de fournir l’ID d’espace de travail OMS <WSID> et la clé primaire <KEY> afin de créer le fichier ocp-secret.yaml.</span><span class="sxs-lookup"><span data-stu-id="1cf30-289">The secret generating script asks for your OMS Workspace ID <WSID> and Primary Key <KEY> and upon completion, it creates the ocp-secret.yaml file.</span></span>  

    ```
    oadm new-project omslogging --node-selector='zone=default'  
    oc project omslogging  
    oc create serviceaccount omsagent  
    oadm policy add-cluster-role-to-user cluster-reader   system:serviceaccount:omslogging:omsagent  
    oadm policy add-scc-to-user privileged system:serviceaccount:omslogging:omsagent  
    ```

4. <span data-ttu-id="1cf30-290">Déployez le fichier de secret en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="1cf30-290">Deploy the secret file by running the following:</span></span>

    `oc create -f ocp-secret.yaml`

5. <span data-ttu-id="1cf30-291">Vérifiez le déploiement en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="1cf30-291">Verify deployment by running the following:</span></span>

    `oc describe secret omsagent-secret`  

    <span data-ttu-id="1cf30-292">La sortie doit ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="1cf30-292">and the  output should resemble:</span></span>  

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

6. <span data-ttu-id="1cf30-293">Déployer le fichier yaml daemon-set de l’agent OMS en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="1cf30-293">Deploy the OMS Agent daemon-set yaml file by running the following:</span></span>

    `oc create -f ocp-ds-omsagent.yaml`  

7. <span data-ttu-id="1cf30-294">Vérifiez le déploiement en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="1cf30-294">Verify deployment by running the following:</span></span>

    `oc describe ds oms`

    <span data-ttu-id="1cf30-295">La sortie doit ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="1cf30-295">and the output should resemble:</span></span>

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

### <a name="secure-your-secret-information-for-docker-swarm-and-kubernetes"></a><span data-ttu-id="1cf30-296">Sécuriser vos informations secrètes pour Docker Swarm et Kubernetes</span><span class="sxs-lookup"><span data-stu-id="1cf30-296">Secure your secret information for Docker Swarm and Kubernetes</span></span>

<span data-ttu-id="1cf30-297">Vous pouvez sécuriser l’ID d’espace de travail OMS et les clés primaires pour les services de conteneur Docker Swarm et Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="1cf30-297">You can secure your secret OMS Workspace ID and Primary Keys for Docker Swarm and Kubernetes container services.</span></span>

#### <a name="secure-secrets-for-docker-swarm"></a><span data-ttu-id="1cf30-298">Sécuriser les secrets pour Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="1cf30-298">Secure secrets for Docker Swarm</span></span>

<span data-ttu-id="1cf30-299">Pour Docker Swarm, une fois les secrets de l’ID de l’espace de travail et de la clé primaire créés, vous pouvez exécuter le service Docker pour l’agent OMS.</span><span class="sxs-lookup"><span data-stu-id="1cf30-299">For Docker Swarm, once the secret for Workspace ID and Primary Key is created, you can run the create the Docker service for OMSagent.</span></span> <span data-ttu-id="1cf30-300">Utilisez les informations suivantes pour créer vos informations secrètes.</span><span class="sxs-lookup"><span data-stu-id="1cf30-300">Use the following information to create your secret information.</span></span>

1. <span data-ttu-id="1cf30-301">Exécutez la commande suivante sur le nœud principal.</span><span class="sxs-lookup"><span data-stu-id="1cf30-301">Run the following on the master node.</span></span>

    ```
    echo "WSID" | docker secret create WSID -
    echo "KEY" | docker secret create KEY -
    ```

2. <span data-ttu-id="1cf30-302">Vérifiez que les secrets ont été créés correctement.</span><span class="sxs-lookup"><span data-stu-id="1cf30-302">Verify that secrets were created properly.</span></span>

    ```
    keiko@swarmm-master-13957614-0:/run# sudo docker secret ls
    ```

    ```
    ID                          NAME                CREATED             UPDATED
    j2fj153zxy91j8zbcitnjxjiv   WSID                43 minutes ago      43 minutes ago
    l9rh3n987g9c45zffuxdxetd9   KEY                 38 minutes ago      38 minutes ago
    ```

3. <span data-ttu-id="1cf30-303">Exécutez la commande suivante pour monter les secrets sur l’agent OMS en conteneur.</span><span class="sxs-lookup"><span data-stu-id="1cf30-303">Run the following command to mount the secrets to the containerized OMS Agent.</span></span>

    ```
    sudo docker service create  --name omsagent --mode global  --mount type=bind,source=/var/run/docker.sock,destination=/var/run/docker.sock --secret source=WSID,target=WSID --secret source=KEY,target=KEY  -p 25225:25225 -p 25224:25224/udp --restart-condition=on-failure microsoft/oms
    ```

#### <a name="secure-secrets-for-kubernetes-with-yaml-files"></a><span data-ttu-id="1cf30-304">Sécuriser des secrets pour Kubernetes avec des fichiers yaml</span><span class="sxs-lookup"><span data-stu-id="1cf30-304">Secure secrets for Kubernetes with yaml files</span></span>

<span data-ttu-id="1cf30-305">Pour Kubernetes, vous utilisez un script afin de générer le fichier .yaml de secrets pour votre ID d’espace de travail et votre clé primaire.</span><span class="sxs-lookup"><span data-stu-id="1cf30-305">For Kubernetes, you use a script to generate the secrets yaml file for your Workspace ID and Primary Key.</span></span> <span data-ttu-id="1cf30-306">Sur la page [OMS Docker Kubernetes GitHub](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes) (GitHub Kubernetes Docker OMS), il existe des fichiers que vous pouvez utiliser avec ou sans vos informations secrètes.</span><span class="sxs-lookup"><span data-stu-id="1cf30-306">At the [OMS Docker Kubernetes GitHub](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes) page, there are files that you can use with or without your secret information.</span></span>

- <span data-ttu-id="1cf30-307">Le daemon-set par défaut de l’agent OMS ne comprend pas d’informations secrètes (omsagent.yaml).</span><span class="sxs-lookup"><span data-stu-id="1cf30-307">The Default OMS Agent DaemonSet does not have secret information (omsagent.yaml)</span></span>
- <span data-ttu-id="1cf30-308">Le fichier yaml daemon-set de l’agent OMS utilise les informations secrètes (omsagent-ds-secrets.yaml) avec des scripts de génération de secrets pour générer le fichier yaml de secrets (omsagentsecret.yaml).</span><span class="sxs-lookup"><span data-stu-id="1cf30-308">The OMS Agent DaemonSet yaml file uses secret information (omsagent-ds-secrets.yaml) with secret generation scripts to generate the secrets yaml (omsagentsecret.yaml) file.</span></span>

<span data-ttu-id="1cf30-309">Vous pouvez choisir de créer le DaemonSet de l’agent OMS avec ou sans secrets.</span><span class="sxs-lookup"><span data-stu-id="1cf30-309">You can choose to create omsagent DaemonSets with or without secrets.</span></span>

##### <a name="default-omsagent-daemonset-yaml-file-without-secrets"></a><span data-ttu-id="1cf30-310">Le fichier yaml par défaut DaemonSet de l’agent OMS sans secrets</span><span class="sxs-lookup"><span data-stu-id="1cf30-310">Default OMSagent DaemonSet yaml file without secrets</span></span>

- <span data-ttu-id="1cf30-311">Pour le fichier yaml par défaut DaemonSet de l’agent OMS, remplacez `<WSID>` et `<KEY>` par votre ID d’espace de travail et clé.</span><span class="sxs-lookup"><span data-stu-id="1cf30-311">For the default OMS Agent DaemonSet yaml file, replace the `<WSID>` and `<KEY>` to your WSID and KEY.</span></span> <span data-ttu-id="1cf30-312">Copiez le fichier sur votre nœud principal et exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="1cf30-312">Copy the file to your master node and run the following:</span></span>

    ```
    sudo kubectl create -f omsagent.yaml
    ```

##### <a name="default-omsagent-daemonset-yaml-file-with-secrets"></a><span data-ttu-id="1cf30-313">Le fichier yaml par défaut DaemonSet de l’agent OMS avec secrets</span><span class="sxs-lookup"><span data-stu-id="1cf30-313">Default OMSagent DaemonSet yaml file with secrets</span></span>

1. <span data-ttu-id="1cf30-314">Pour utiliser le DaemonSet de l’agent OMS à l’aide des informations secrètes, créez d’abord les secrets.</span><span class="sxs-lookup"><span data-stu-id="1cf30-314">To use OMS Agent DaemonSet using secret information, create the secrets first.</span></span>
    1. <span data-ttu-id="1cf30-315">Copiez le fichier de modèle de secret et le script, et assurez-vous qu’ils se trouvent dans le même répertoire.</span><span class="sxs-lookup"><span data-stu-id="1cf30-315">Copy the script and secret template file and make sure they are on the same directory.</span></span>
        - <span data-ttu-id="1cf30-316">Script de génération de secrets - secret-gen.sh</span><span class="sxs-lookup"><span data-stu-id="1cf30-316">Secret generating script - secret-gen.sh</span></span>
        - <span data-ttu-id="1cf30-317">Modèle de secret - secret-template.yaml</span><span class="sxs-lookup"><span data-stu-id="1cf30-317">secret template - secret-template.yaml</span></span>
    2. <span data-ttu-id="1cf30-318">Exécutez le script, comme l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="1cf30-318">Run the script, like the following example.</span></span> <span data-ttu-id="1cf30-319">Le script demande l’ID d’espace de travail OMS et la clé primaire, et une fois que vous les entrez, le script crée un fichier .yaml de secrets que vous pouvez exécuter.</span><span class="sxs-lookup"><span data-stu-id="1cf30-319">The script asks for the OMS Workspace ID and Primary Key and after you enter them, the script creates a secret yaml file so you can run it.</span></span>   

        ```
        #> sudo bash ./secret-gen.sh
        ```

    3. <span data-ttu-id="1cf30-320">Créez le pod de secrets en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="1cf30-320">Create the secrets pod by running the following:</span></span>
        ```
        sudo kubectl create -f omsagentsecret.yaml
        ```

    4. <span data-ttu-id="1cf30-321">Pour vérifier, exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="1cf30-321">To verify, run the following:</span></span>

        ```
        keiko@ubuntu16-13db:~# sudo kubectl get secrets
        ```

        <span data-ttu-id="1cf30-322">La sortie doit ressembler à :</span><span class="sxs-lookup"><span data-stu-id="1cf30-322">Output should resemble:</span></span>

        ```
        NAME                  TYPE                                  DATA      AGE
        default-token-gvl91   kubernetes.io/service-account-token   3         50d
        omsagent-secret       Opaque                                2         1d
        ```

        ```
        keiko@ubuntu16-13db:~# sudo kubectl describe secrets omsagent-secret
        ```

        <span data-ttu-id="1cf30-323">La sortie doit ressembler à :</span><span class="sxs-lookup"><span data-stu-id="1cf30-323">Output should resemble:</span></span>

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

    5. <span data-ttu-id="1cf30-324">Créer votre DaemonsSet de l’agent OMS en exécutant ``` sudo kubectl create -f omsagent-ds-secrets.yaml ```</span><span class="sxs-lookup"><span data-stu-id="1cf30-324">Create your omsagent daemon-set by running ``` sudo kubectl create -f omsagent-ds-secrets.yaml ```</span></span>

2. <span data-ttu-id="1cf30-325">Vérifiez que le DaemonSet de l’agent OMS s’exécute, comme ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="1cf30-325">Verify that the OMS Agent DaemonSet is running, similar to the following:</span></span>

    ```
    keiko@ubuntu16-13db:~# sudo kubectl get ds omsagent
    ```

    ```
    NAME       DESIRED   CURRENT   NODE-SELECTOR   AGE
    omsagent   3         3         <none>          1h
    ```


<span data-ttu-id="1cf30-326">Pour Kubernetes, utilisez un script afin de générer le fichier .yaml de secrets pour l’ID d’espace de travail et la clé primaire.</span><span class="sxs-lookup"><span data-stu-id="1cf30-326">For Kubernetes, use a script to generate the secrets yaml file for Workspace ID and Primary Key.</span></span> <span data-ttu-id="1cf30-327">Utilisez les informations de l’exemple suivant avec le [fichier yaml de l’agent OMS](https://github.com/Microsoft/OMS-docker/blob/master/Kubernetes/omsagent.yaml) pour sécuriser vos informations secrètes.</span><span class="sxs-lookup"><span data-stu-id="1cf30-327">Use the following example information with the [omsagent yaml file](https://github.com/Microsoft/OMS-docker/blob/master/Kubernetes/omsagent.yaml) to secure your secret information.</span></span>

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

## <a name="windows-container-hosts"></a><span data-ttu-id="1cf30-328">Hôtes de conteneur Windows</span><span class="sxs-lookup"><span data-stu-id="1cf30-328">Windows container hosts</span></span>

### <a name="preparation-before-installing-windows-agents"></a><span data-ttu-id="1cf30-329">Préparation préalable à l’installation des agents Windows</span><span class="sxs-lookup"><span data-stu-id="1cf30-329">Preparation before installing Windows agents</span></span>

<span data-ttu-id="1cf30-330">Avant d’installer les agents sur les ordinateurs exécutant Windows, vous devez configurer le service Docker.</span><span class="sxs-lookup"><span data-stu-id="1cf30-330">Before you install agents on computers running Windows, you need to configure the Docker service.</span></span> <span data-ttu-id="1cf30-331">La configuration permet à l’agent Windows ou à l’extension de machine virtuelle Log Analytics d’utiliser le socket Docker TCP afin d’autoriser les agents à accéder à distance au démon Docker et de collecter les données pour la surveillance.</span><span class="sxs-lookup"><span data-stu-id="1cf30-331">The configuration allows the Windows agent or the Log Analytics virtual machine extension to use the Docker TCP socket so that the agents can access the Docker daemon remotely and to capture data for monitoring.</span></span>

#### <a name="to-start-docker-and-verify-its-configuration"></a><span data-ttu-id="1cf30-332">Pour démarrer Docker et vérifier sa configuration</span><span class="sxs-lookup"><span data-stu-id="1cf30-332">To start Docker and verify its configuration</span></span>

<span data-ttu-id="1cf30-333">Voici les étapes nécessaires à la configuration du canal nommé TCP pour Windows Server :</span><span class="sxs-lookup"><span data-stu-id="1cf30-333">There are steps needed to set up TCP named pipe for Windows Server:</span></span>

1. <span data-ttu-id="1cf30-334">Dans Windows PowerShell, activez les canaux TCP et nommé.</span><span class="sxs-lookup"><span data-stu-id="1cf30-334">In Windows PowerShell, enable TCP pipe and named pipe.</span></span>

    ```
    Stop-Service docker
    dockerd --unregister-service
    dockerd --register-service -H npipe:// -H 0.0.0.0:2375  
    Start-Service docker
    ```

2. <span data-ttu-id="1cf30-335">Configurez Docker à l’aide du fichier de configuration pour le canal TCP et le canal nommé.</span><span class="sxs-lookup"><span data-stu-id="1cf30-335">Configure Docker with the configuration file for TCP pipe and named pipe.</span></span> <span data-ttu-id="1cf30-336">Le fichier de configuration se trouve à l’emplacement suivant : C:\ProgramData\docker\config\daemon.json.</span><span class="sxs-lookup"><span data-stu-id="1cf30-336">The configuration file is located at C:\ProgramData\docker\config\daemon.json.</span></span>

    <span data-ttu-id="1cf30-337">Dans le fichier daemon.json, vous aurez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="1cf30-337">In the daemon.json file, you will need the following:</span></span>

    ```
    {
    "hosts": ["tcp://0.0.0.0:2375", "npipe://"]
    }
    ```

<span data-ttu-id="1cf30-338">Pour plus d’informations sur la configuration du démon Docker utilisée avec les conteneurs de Windows, reportez-vous à [Moteur Docker sur Windows](https://docs.microsoft.com/virtualization/windowscontainers/manage-docker/configure-docker-daemon).</span><span class="sxs-lookup"><span data-stu-id="1cf30-338">For more information about the Docker daemon configuration used with Windows Containers, see [Docker Engine on Windows](https://docs.microsoft.com/virtualization/windowscontainers/manage-docker/configure-docker-daemon).</span></span>


### <a name="install-windows-agents"></a><span data-ttu-id="1cf30-339">Installer les agents Windows</span><span class="sxs-lookup"><span data-stu-id="1cf30-339">Install Windows agents</span></span>

<span data-ttu-id="1cf30-340">Pour activer la surveillance des conteneurs Windows et Hyper-V, installez Microsoft Monitoring Agent (MMA) sur les ordinateurs Windows qui sont des hôtes de conteneurs.</span><span class="sxs-lookup"><span data-stu-id="1cf30-340">To enable Windows and Hyper-V container monitoring, install the Microsoft Monitoring Agent (MMA) on Windows computers that are container hosts.</span></span> <span data-ttu-id="1cf30-341">Pour les ordinateurs exécutant Windows dans votre environnement local, consultez la page [Connecter des ordinateurs Windows à Log Analytics](log-analytics-windows-agents.md).</span><span class="sxs-lookup"><span data-stu-id="1cf30-341">For computers running Windows in your on-premises environment, see [Connect Windows computers to Log Analytics](log-analytics-windows-agents.md).</span></span> <span data-ttu-id="1cf30-342">Connectez les machines virtuelles exécutées dans Azure à Log Analytics à l’aide de l’[extension de machine virtuelle](log-analytics-azure-vm-extension.md).</span><span class="sxs-lookup"><span data-stu-id="1cf30-342">For virtual machines running in Azure, connect them to Log Analytics using the [virtual machine extension](log-analytics-azure-vm-extension.md).</span></span>

<span data-ttu-id="1cf30-343">Vous pouvez surveiller les conteneurs Windows en cours d’exécution sur Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="1cf30-343">You can monitor Windows containers running on Service Fabric.</span></span> <span data-ttu-id="1cf30-344">Toutefois, seules les [machines virtuelles qui s’exécutent dans Azure](log-analytics-azure-vm-extension.md) et les [ordinateurs exécutant Windows dans votre environnement local](log-analytics-windows-agents.md) sont actuellement pris en charge pour Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="1cf30-344">However, only [virtual machines running in Azure](log-analytics-azure-vm-extension.md) and [computers running Windows in your on-premises environment](log-analytics-windows-agents.md) are currently supported for Service Fabric.</span></span>

<span data-ttu-id="1cf30-345">Vous pouvez vérifier que la solution Container Monitoring est correctement configurée pour Windows.</span><span class="sxs-lookup"><span data-stu-id="1cf30-345">You can verify that the Container Monitoring solution is set correctly for Windows.</span></span> <span data-ttu-id="1cf30-346">Pour vérifier que le pack d’administration a été correctement téléchargé, recherchez *ContainerManagement.xxx*.</span><span class="sxs-lookup"><span data-stu-id="1cf30-346">To check whether the management pack was download properly, look for *ContainerManagement.xxx*.</span></span> <span data-ttu-id="1cf30-347">Les fichiers doivent se trouver dans le dossier C:\Program Files\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs.</span><span class="sxs-lookup"><span data-stu-id="1cf30-347">The files should be in the C:\Program Files\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs folder.</span></span>


## <a name="solution-components"></a><span data-ttu-id="1cf30-348">Composants de la solution</span><span class="sxs-lookup"><span data-stu-id="1cf30-348">Solution components</span></span>

<span data-ttu-id="1cf30-349">Si vous utilisez des agents Windows, le pack d’administration suivant est installé sur chaque ordinateur où se trouve un agent lorsque vous ajoutez cette solution.</span><span class="sxs-lookup"><span data-stu-id="1cf30-349">If you are using Windows agents, then the following management pack is installed on each computer with an agent when you add this solution.</span></span> <span data-ttu-id="1cf30-350">Le pack d’administration ne nécessite aucune opération de configuration ou de maintenance.</span><span class="sxs-lookup"><span data-stu-id="1cf30-350">No configuration or maintenance is required for the management pack.</span></span>

- <span data-ttu-id="1cf30-351">*ContainerManagement.xxx* installé dans le dossier C:\Program Files\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs</span><span class="sxs-lookup"><span data-stu-id="1cf30-351">*ContainerManagement.xxx* installed in C:\Program Files\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs</span></span>

## <a name="container-data-collection-details"></a><span data-ttu-id="1cf30-352">Détails sur la collecte de données des conteneurs</span><span class="sxs-lookup"><span data-stu-id="1cf30-352">Container data collection details</span></span>
<span data-ttu-id="1cf30-353">La solution Container Monitoring collecte diverses métriques de performances et données de journaux à partir des hôtes de conteneur et des conteneurs utilisant les agents que vous avez activés.</span><span class="sxs-lookup"><span data-stu-id="1cf30-353">The Container Monitoring solution collects various performance metrics and log data from container hosts and containers using agents that you enable.</span></span>

<span data-ttu-id="1cf30-354">Les données sont collectées toutes les trois minutes par les types d’agents suivants.</span><span class="sxs-lookup"><span data-stu-id="1cf30-354">Data is collected every three minutes by the following agent types.</span></span>

- [<span data-ttu-id="1cf30-355">Agent OMS pour Linux</span><span class="sxs-lookup"><span data-stu-id="1cf30-355">OMS Agent for Linux</span></span>](log-analytics-linux-agents.md)
- [<span data-ttu-id="1cf30-356">Agent Windows</span><span class="sxs-lookup"><span data-stu-id="1cf30-356">Windows agent</span></span>](log-analytics-windows-agents.md)
- [<span data-ttu-id="1cf30-357">Extension de machine virtuelle Log Analytics</span><span class="sxs-lookup"><span data-stu-id="1cf30-357">Log Analytics VM extension</span></span>](log-analytics-azure-vm-extension.md)


### <a name="container-records"></a><span data-ttu-id="1cf30-358">Enregistrements de conteneur</span><span class="sxs-lookup"><span data-stu-id="1cf30-358">Container records</span></span>

<span data-ttu-id="1cf30-359">Le tableau suivant présente des exemples d’enregistrements collectés par la solution Container Monitoring, ainsi que les types de données qui s’affichent dans les résultats de recherche des journaux.</span><span class="sxs-lookup"><span data-stu-id="1cf30-359">The following table shows examples of records collected by the Container Monitoring solution and the data types that appear in log search results.</span></span>

| <span data-ttu-id="1cf30-360">Type de données</span><span class="sxs-lookup"><span data-stu-id="1cf30-360">Data type</span></span> | <span data-ttu-id="1cf30-361">Type de données dans Recherche de journaux</span><span class="sxs-lookup"><span data-stu-id="1cf30-361">Data type in Log Search</span></span> | <span data-ttu-id="1cf30-362">Champs</span><span class="sxs-lookup"><span data-stu-id="1cf30-362">Fields</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1cf30-363">Performances des hôtes et des conteneurs</span><span class="sxs-lookup"><span data-stu-id="1cf30-363">Performance for hosts and containers</span></span> | `Type=Perf` | <span data-ttu-id="1cf30-364">Computer, ObjectName, CounterName &#40;%Processor Time, Disk Reads MB, Disk Writes MB, Memory Usage MB, Network Receive Bytes, Network Send Bytes, Processor Usage sec, Network&#41;, CounterValue,TimeGenerated, CounterPath, SourceSystem</span><span class="sxs-lookup"><span data-stu-id="1cf30-364">Computer, ObjectName, CounterName &#40;%Processor Time, Disk Reads MB, Disk Writes MB, Memory Usage MB, Network Receive Bytes, Network Send Bytes, Processor Usage sec, Network&#41;, CounterValue,TimeGenerated, CounterPath, SourceSystem</span></span> |
| <span data-ttu-id="1cf30-365">Inventaire de conteneur</span><span class="sxs-lookup"><span data-stu-id="1cf30-365">Container inventory</span></span> | `Type=ContainerInventory` | <span data-ttu-id="1cf30-366">TimeGenerated, Computer, container name, ContainerHostname, Image, ImageTag, ContainerState, ExitCode, EnvironmentVar, Command, CreatedTime, StartedTime, FinishedTime, SourceSystem, ContainerID, ImageID</span><span class="sxs-lookup"><span data-stu-id="1cf30-366">TimeGenerated, Computer, container name, ContainerHostname, Image, ImageTag, ContainerState, ExitCode, EnvironmentVar, Command, CreatedTime, StartedTime, FinishedTime, SourceSystem, ContainerID, ImageID</span></span> |
| <span data-ttu-id="1cf30-367">Inventaire d’image de conteneur</span><span class="sxs-lookup"><span data-stu-id="1cf30-367">Container image inventory</span></span> | `Type=ContainerImageInventory` | <span data-ttu-id="1cf30-368">TimeGenerated, Computer, Image, ImageTag, ImageSize, VirtualSize, Running, Paused, Stopped, Failed, SourceSystem, ImageID, TotalContainer</span><span class="sxs-lookup"><span data-stu-id="1cf30-368">TimeGenerated, Computer, Image, ImageTag, ImageSize, VirtualSize, Running, Paused, Stopped, Failed, SourceSystem, ImageID, TotalContainer</span></span> |
| <span data-ttu-id="1cf30-369">Journal de conteneur</span><span class="sxs-lookup"><span data-stu-id="1cf30-369">Container log</span></span> | `Type=ContainerLog` | <span data-ttu-id="1cf30-370">TimeGenerated, Computer, image ID, container name, LogEntrySource, LogEntry, SourceSystem, ContainerID</span><span class="sxs-lookup"><span data-stu-id="1cf30-370">TimeGenerated, Computer, image ID, container name, LogEntrySource, LogEntry, SourceSystem, ContainerID</span></span> |
| <span data-ttu-id="1cf30-371">Journal de service de conteneur</span><span class="sxs-lookup"><span data-stu-id="1cf30-371">Container service log</span></span> | `Type=ContainerServiceLog`  | <span data-ttu-id="1cf30-372">TimeGenerated, Computer, TimeOfCommand, Image, Command, SourceSystem, ContainerID</span><span class="sxs-lookup"><span data-stu-id="1cf30-372">TimeGenerated, Computer, TimeOfCommand, Image, Command, SourceSystem, ContainerID</span></span> |
| <span data-ttu-id="1cf30-373">Inventaire du nœud de conteneur</span><span class="sxs-lookup"><span data-stu-id="1cf30-373">Container node inventory</span></span> | `Type=ContainerNodeInventory_CL`| <span data-ttu-id="1cf30-374">TimeGenerated, Computer, ClassName_s, DockerVersion_s, OperatingSystem_s, Volume_s, Network_s, NodeRole_s, OrchestratorType_s, InstanceID_g, SourceSystem</span><span class="sxs-lookup"><span data-stu-id="1cf30-374">TimeGenerated, Computer, ClassName_s, DockerVersion_s, OperatingSystem_s, Volume_s, Network_s, NodeRole_s, OrchestratorType_s, InstanceID_g, SourceSystem</span></span>|
| <span data-ttu-id="1cf30-375">Inventaire de Kubernetes</span><span class="sxs-lookup"><span data-stu-id="1cf30-375">Kubernetes inventory</span></span> | `Type=KubePodInventory_CL` | <span data-ttu-id="1cf30-376">TimeGenerated, Computer, PodLabel_deployment_s, PodLabel_deploymentconfig_s, PodLabel_docker_registry_s, Name_s, Namespace_s, PodStatus_s, PodIp_s, PodUid_g, PodCreationTimeStamp_t, SourceSystem</span><span class="sxs-lookup"><span data-stu-id="1cf30-376">TimeGenerated, Computer, PodLabel_deployment_s, PodLabel_deploymentconfig_s, PodLabel_docker_registry_s, Name_s, Namespace_s, PodStatus_s, PodIp_s, PodUid_g, PodCreationTimeStamp_t, SourceSystem</span></span> |
| <span data-ttu-id="1cf30-377">Processus de conteneur</span><span class="sxs-lookup"><span data-stu-id="1cf30-377">Container process</span></span> | `Type=ContainerProcess_CL` | <span data-ttu-id="1cf30-378">TimeGenerated, Computer, Pod_s, Namespace_s, ClassName_s, InstanceID_s, Uid_s, PID_s, PPID_s, C_s, STIME_s, Tty_s, TIME_s, Cmd_s, Id_s, Name_s, SourceSystem</span><span class="sxs-lookup"><span data-stu-id="1cf30-378">TimeGenerated, Computer, Pod_s, Namespace_s, ClassName_s, InstanceID_s, Uid_s, PID_s, PPID_s, C_s, STIME_s, Tty_s, TIME_s, Cmd_s, Id_s, Name_s, SourceSystem</span></span> |
| <span data-ttu-id="1cf30-379">Événements Kubernetes</span><span class="sxs-lookup"><span data-stu-id="1cf30-379">Kubernetes events</span></span> | `Type=KubeEvents_CL` | <span data-ttu-id="1cf30-380">TimeGenerated, Computer, Name_s, ObjectKind_s, Namespace_s, Reason_s, Type_s, SourceComponent_s, SourceSystem, Message</span><span class="sxs-lookup"><span data-stu-id="1cf30-380">TimeGenerated, Computer, Name_s, ObjectKind_s, Namespace_s, Reason_s, Type_s, SourceComponent_s, SourceSystem, Message</span></span> |

<span data-ttu-id="1cf30-381">Les étiquettes ajoutées aux types de données *PodLabel* sont vos propres étiquettes personnalisées.</span><span class="sxs-lookup"><span data-stu-id="1cf30-381">Labels appended to *PodLabel* data types are your own custom labels.</span></span> <span data-ttu-id="1cf30-382">Les étiquettes PodLabel ajoutées contenues dans le tableau sont des exemples.</span><span class="sxs-lookup"><span data-stu-id="1cf30-382">The appended PodLabel labels shown in the table are examples.</span></span> <span data-ttu-id="1cf30-383">Par conséquent, `PodLabel_deployment_s`, `PodLabel_deploymentconfig_s`, `PodLabel_docker_registry_s` seront différentes dans le jeu de données de votre environnement et ressembleront à `PodLabel_yourlabel_s`.</span><span class="sxs-lookup"><span data-stu-id="1cf30-383">So, `PodLabel_deployment_s`, `PodLabel_deploymentconfig_s`, `PodLabel_docker_registry_s` will differ in your environment's data set and generically resemble `PodLabel_yourlabel_s`.</span></span>


## <a name="monitor-containers"></a><span data-ttu-id="1cf30-384">Analyser les conteneurs</span><span class="sxs-lookup"><span data-stu-id="1cf30-384">Monitor containers</span></span>
<span data-ttu-id="1cf30-385">Une fois la solution activée dans le portail OMS, vous voyez la vignette **Containers** qui contient des informations récapitulatives sur vos hôtes de conteneur et les conteneurs s’exécutant dans les hôtes.</span><span class="sxs-lookup"><span data-stu-id="1cf30-385">After you have the solution enabled in the OMS portal, the **Containers** tile shows summary information about your container hosts and the containers running in hosts.</span></span>

![Vignette Conteneurs](./media/log-analytics-containers/containers-title.png)

<span data-ttu-id="1cf30-387">La vignette affiche une vue d’ensemble du nombre de conteneurs présents dans l’environnement, et indique s’ils sont en échec, en cours d’exécution ou arrêtés.</span><span class="sxs-lookup"><span data-stu-id="1cf30-387">The tile shows an overview of how many containers you have in the environment and whether they're failed, running, or stopped.</span></span>

### <a name="using-the-containers-dashboard"></a><span data-ttu-id="1cf30-388">Utilisation du tableau de bord Conteneurs</span><span class="sxs-lookup"><span data-stu-id="1cf30-388">Using the Containers dashboard</span></span>
<span data-ttu-id="1cf30-389">Cliquez sur la vignette **Conteneurs**.</span><span class="sxs-lookup"><span data-stu-id="1cf30-389">Click the **Containers** tile.</span></span> <span data-ttu-id="1cf30-390">À partir de là, vous voyez les vues organisées par :</span><span class="sxs-lookup"><span data-stu-id="1cf30-390">From there you'll see views organized by:</span></span>

- <span data-ttu-id="1cf30-391">**Événements de conteneur** : affiche l’état du conteneur et les ordinateurs dont le conteneur a échoué.</span><span class="sxs-lookup"><span data-stu-id="1cf30-391">**Container Events** - Shows container status and computers with failed containers.</span></span>
- <span data-ttu-id="1cf30-392">**Journaux de conteneur** : affiche un graphique montrant les fichiers journaux de conteneur générés jusqu’à maintenant, ainsi que la liste des ordinateurs contenant le plus grand nombre de fichiers journaux.</span><span class="sxs-lookup"><span data-stu-id="1cf30-392">**Container Logs** - Shows a chart of container log files generated over time and a list of computers with the highest number of log files.</span></span>
- <span data-ttu-id="1cf30-393">**Événements Kubernetes** : affiche un graphique montrant les événements Kubernetes générés jusqu’à maintenant, ainsi que la liste des raisons pour lesquelles les pods ont généré ces événements.</span><span class="sxs-lookup"><span data-stu-id="1cf30-393">**Kubernetes Events** - Shows a chart of Kubernetes events generated over time and a list of the reasons why pods generated the events.</span></span> <span data-ttu-id="1cf30-394">*Ce jeu de données est utilisé uniquement dans les environnements Linux.*</span><span class="sxs-lookup"><span data-stu-id="1cf30-394">*This data set is used only in Linux environments.*</span></span>
- <span data-ttu-id="1cf30-395">**Inventaire des espaces de noms Kubernetes** : indique le nombre d’espaces de noms et de pods, et montre leur hiérarchie.</span><span class="sxs-lookup"><span data-stu-id="1cf30-395">**Kubernetes Namespace Inventory** - Shows the number of namespaces and pods and shows their hierarchy.</span></span> <span data-ttu-id="1cf30-396">*Ce jeu de données est utilisé uniquement dans les environnements Linux.*</span><span class="sxs-lookup"><span data-stu-id="1cf30-396">*This data set is used only in Linux environments.*</span></span>
- <span data-ttu-id="1cf30-397">**Inventaire des nœuds de conteneur** : affiche le nombre de types d’orchestration utilisés sur les nœuds/hôtes de conteneur.</span><span class="sxs-lookup"><span data-stu-id="1cf30-397">**Container Node Inventory** - Shows the number of orchestration types used on container nodes/hosts.</span></span> <span data-ttu-id="1cf30-398">Les nœuds/hôtes d’ordinateur sont également répertoriés avec le nombre de conteneurs.</span><span class="sxs-lookup"><span data-stu-id="1cf30-398">The computer nodes/hosts are also listed by the number of containers.</span></span> <span data-ttu-id="1cf30-399">*Ce jeu de données est utilisé uniquement dans les environnements Linux.*</span><span class="sxs-lookup"><span data-stu-id="1cf30-399">*This data set is used only in Linux environments.*</span></span>
- <span data-ttu-id="1cf30-400">**Inventaire des images de conteneur** : affiche le nombre total des images de conteneur utilisées, ainsi que le nombre de types d’images.</span><span class="sxs-lookup"><span data-stu-id="1cf30-400">**Container Images Inventory** - Shows the total number of container images used and number of image types.</span></span> <span data-ttu-id="1cf30-401">Le nombre d’images est également répertorié avec la balise d’image.</span><span class="sxs-lookup"><span data-stu-id="1cf30-401">The number of images are also listed by the image tag.</span></span>
- <span data-ttu-id="1cf30-402">**État des conteneurs** : affiche le nombre total de nœuds de conteneur/ordinateurs hôtes comprenant des conteneurs en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="1cf30-402">**Containers Status** - Shows the total number of container nodes/host computers that have running containers.</span></span> <span data-ttu-id="1cf30-403">Les ordinateurs sont également répertoriés avec le nombre d’ordinateurs hôtes en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="1cf30-403">Computers are also listed by the number of running hosts.</span></span>
- <span data-ttu-id="1cf30-404">**Processus de conteneur** : affiche un graphique en courbes représentant les processus de conteneur exécutés jusqu’à maintenant.</span><span class="sxs-lookup"><span data-stu-id="1cf30-404">**Container Process** - Shows a line chart of container processes running over time.</span></span> <span data-ttu-id="1cf30-405">Les conteneurs peuvent également être répertoriés en exécutant la commande /process dans les conteneurs.</span><span class="sxs-lookup"><span data-stu-id="1cf30-405">Containers are also listed by running command/process within containers.</span></span> <span data-ttu-id="1cf30-406">*Ce jeu de données est utilisé uniquement dans les environnements Linux.*</span><span class="sxs-lookup"><span data-stu-id="1cf30-406">*This data set is used only in Linux environments.*</span></span>
- <span data-ttu-id="1cf30-407">**Performances de l’UC du conteneur** : affiche un graphique en courbes représentant l’utilisation moyenne de l’UC jusqu’à maintenant pour les nœuds/hôtes d’ordinateur.</span><span class="sxs-lookup"><span data-stu-id="1cf30-407">**Container CPU Performance** - Shows a line chart of the average CPU utilization over time for computer nodes/hosts.</span></span> <span data-ttu-id="1cf30-408">Répertorie également les nœuds/hôtes d’ordinateur en fonction de l’utilisation moyenne de l’UC.</span><span class="sxs-lookup"><span data-stu-id="1cf30-408">Also lists the computer nodes/hosts based on average CPU utilization.</span></span>
- <span data-ttu-id="1cf30-409">**Performances de la mémoire du conteneur** : affiche un graphique en courbes représentant l’utilisation de la mémoire jusqu’à maintenant.</span><span class="sxs-lookup"><span data-stu-id="1cf30-409">**Container Memory Performance** - Shows a line chart of memory usage over time.</span></span> <span data-ttu-id="1cf30-410">Répertorie également l’utilisation de la mémoire par l’ordinateur en fonction du nom de l’instance.</span><span class="sxs-lookup"><span data-stu-id="1cf30-410">Also lists computer memory utilization based on instance name.</span></span>
- <span data-ttu-id="1cf30-411">**Performances de l’ordinateur** : affiche des graphiques en courbes représentant le pourcentage de performance de l’UC, le pourcentage d’utilisation de la mémoire et les mégaoctets d’espace disque libre dans le temps.</span><span class="sxs-lookup"><span data-stu-id="1cf30-411">**Computer Performance** - Shows line charts of the percent of CPU performance over time, percent of memory usage over time, and megabytes of free disk space over time.</span></span> <span data-ttu-id="1cf30-412">Vous pouvez pointer sur une ligne du graphique pour afficher plus de détails.</span><span class="sxs-lookup"><span data-stu-id="1cf30-412">You can hover over any line in a chart to view more details.</span></span>


<span data-ttu-id="1cf30-413">Chaque zone du tableau de bord est une représentation visuelle d’une recherche exécutée sur des données collectées.</span><span class="sxs-lookup"><span data-stu-id="1cf30-413">Each area of the dashboard is a visual representation of a search that is run on collected data.</span></span>

![Tableau de bord Conteneurs](./media/log-analytics-containers/containers-dash01.png)

![Tableau de bord Conteneurs](./media/log-analytics-containers/containers-dash02.png)

<span data-ttu-id="1cf30-416">Dans la zone **État du conteneur**, cliquez sur la zone supérieure, comme illustré ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="1cf30-416">In the **Container Status** area, click the top area, as shown below.</span></span>

![État des conteneurs](./media/log-analytics-containers/containers-status.png)

<span data-ttu-id="1cf30-418">La fenêtre Recherche dans les journaux s’ouvre et affiche des informations sur l’état de vos conteneurs.</span><span class="sxs-lookup"><span data-stu-id="1cf30-418">Log Search opens, displaying information about the state of your containers.</span></span>

![Recherche de journal pour les conteneurs](./media/log-analytics-containers/containers-log-search.png)

<span data-ttu-id="1cf30-420">À partir d’ici, vous pouvez modifier la requête de recherche de façon à trouver les informations spécifiques qui vous intéressent.</span><span class="sxs-lookup"><span data-stu-id="1cf30-420">From here, you can edit the search query to modify it to find the specific information you're interested in.</span></span> <span data-ttu-id="1cf30-421">Pour plus d’informations sur les recherches dans les journaux, voir [Recherches de journal dans Log Analytics](log-analytics-log-searches.md).</span><span class="sxs-lookup"><span data-stu-id="1cf30-421">For more information about Log Searches, see [Log searches in Log Analytics](log-analytics-log-searches.md).</span></span>

## <a name="troubleshoot-by-finding-a-failed-container"></a><span data-ttu-id="1cf30-422">Résoudre des problèmes en recherchant un conteneur en échec</span><span class="sxs-lookup"><span data-stu-id="1cf30-422">Troubleshoot by finding a failed container</span></span>

<span data-ttu-id="1cf30-423">Log Analytics marque un conteneur comme étant en **Échec** s’il a été fermé avec un code de sortie autre que zéro.</span><span class="sxs-lookup"><span data-stu-id="1cf30-423">Log Analytics marks a container as **Failed** if it has exited with a non-zero exit code.</span></span> <span data-ttu-id="1cf30-424">Vous pouvez consulter un aperçu des erreurs et des échecs de l’environnement dans la zone **Conteneurs défectueux**.</span><span class="sxs-lookup"><span data-stu-id="1cf30-424">You can see an overview of the errors and failures in the environment in the **Failed Containers** area.</span></span>

### <a name="to-find-failed-containers"></a><span data-ttu-id="1cf30-425">Pour rechercher les conteneurs défectueux</span><span class="sxs-lookup"><span data-stu-id="1cf30-425">To find failed containers</span></span>
1. <span data-ttu-id="1cf30-426">Cliquez sur la zone **État du conteneur**.</span><span class="sxs-lookup"><span data-stu-id="1cf30-426">Click the **Container Status** area.</span></span>  
   <span data-ttu-id="1cf30-427">![État des conteneurs](./media/log-analytics-containers/containers-status.png)</span><span class="sxs-lookup"><span data-stu-id="1cf30-427">![containers status](./media/log-analytics-containers/containers-status.png)</span></span>
2. <span data-ttu-id="1cf30-428">La fenêtre Recherche dans les journaux s’ouvre et affiche l’état de vos conteneurs, comme ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="1cf30-428">Log Search opens and displays the state of your containers, similar to the following.</span></span>  
   ![État des conteneurs](./media/log-analytics-containers/containers-log-search.png)
3. <span data-ttu-id="1cf30-430">Ensuite, cliquez sur la valeur agrégée des conteneurs en échec pour afficher des informations supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="1cf30-430">Next, click the aggregated value of failed containers to view additional information.</span></span> <span data-ttu-id="1cf30-431">Développez **Afficher plus** pour afficher l’ID de l’image.</span><span class="sxs-lookup"><span data-stu-id="1cf30-431">Expand **show more** to view the image ID.</span></span>  
   <span data-ttu-id="1cf30-432">![Conteneurs défectueux](./media/log-analytics-containers/containers-state-failed.png)</span><span class="sxs-lookup"><span data-stu-id="1cf30-432">![failed containers](./media/log-analytics-containers/containers-state-failed.png)</span></span>  
4. <span data-ttu-id="1cf30-433">Ensuite, tapez ce qui suit dans la requête de recherche.</span><span class="sxs-lookup"><span data-stu-id="1cf30-433">Next, type the following in the search query.</span></span> <span data-ttu-id="1cf30-434">`Type=ContainerInventory <ImageID>` pour afficher des détails sur l’image, tels que sa taille ou le nombre d’images arrêtées et en échec.</span><span class="sxs-lookup"><span data-stu-id="1cf30-434">`Type=ContainerInventory <ImageID>` to see details about the image such as image size and number of stopped and failed images.</span></span>  
   <span data-ttu-id="1cf30-435">![Conteneurs défectueux](./media/log-analytics-containers/containers-failed04.png)</span><span class="sxs-lookup"><span data-stu-id="1cf30-435">![failed containers](./media/log-analytics-containers/containers-failed04.png)</span></span>

## <a name="search-logs-for-container-data"></a><span data-ttu-id="1cf30-436">Rechercher des données de conteneur dans les journaux</span><span class="sxs-lookup"><span data-stu-id="1cf30-436">Search logs for container data</span></span>
<span data-ttu-id="1cf30-437">Lorsque vous résolvez une erreur spécifique, il peut être utile de voir l’emplacement où elle se produit dans votre environnement.</span><span class="sxs-lookup"><span data-stu-id="1cf30-437">When you're troubleshooting a specific error, it can help to see where it is occurring in your environment.</span></span> <span data-ttu-id="1cf30-438">Les types de journaux suivants vous aident à créer des requêtes qui retournent les informations souhaitées.</span><span class="sxs-lookup"><span data-stu-id="1cf30-438">The following log types will help you create queries to return the information you want.</span></span>


- <span data-ttu-id="1cf30-439">**ContainerImageInventory** : utilisez ce type de journal lorsque vous recherchez des informations organisées par image, et de consulter des informations sur les images, telles que leurs ID ou tailles.</span><span class="sxs-lookup"><span data-stu-id="1cf30-439">**ContainerImageInventory** – Use this type when you're trying to find information organized by image and to view image information such as image IDs or sizes.</span></span>
- <span data-ttu-id="1cf30-440">**ContainerInventory** : utilisez ce type de journal lorsque vous recherchez des informations sur l’emplacement des conteneurs, leurs noms et les images qu’ils exécutent.</span><span class="sxs-lookup"><span data-stu-id="1cf30-440">**ContainerInventory** – Use this type when you want information about container location, what their names are, and what images they're running.</span></span>
- <span data-ttu-id="1cf30-441">**ContainerLog** : utilisez ce type de journal lorsque vous recherchez des informations et entrées spécifiques du journal des erreurs.</span><span class="sxs-lookup"><span data-stu-id="1cf30-441">**ContainerLog** – Use this type when you want to find specific error log information and entries.</span></span>
- <span data-ttu-id="1cf30-442">**ContainerNodeInventory_CL** Utilisez ce type lorsque vous souhaitez obtenir les informations sur le nœud ou l’hôte où résident les conteneurs.</span><span class="sxs-lookup"><span data-stu-id="1cf30-442">**ContainerNodeInventory_CL**  Use this type when you want the information about host/node where containers are residing.</span></span> <span data-ttu-id="1cf30-443">Il fournit la version Docker, le type d’orchestration, ainsi que des informations relatives au stockage et au réseau.</span><span class="sxs-lookup"><span data-stu-id="1cf30-443">It provides you Docker version, orchestration type, storage, and network information.</span></span>
- <span data-ttu-id="1cf30-444">**ContainerProcess_CL** Ce type permet de visualiser rapidement le processus actuellement exécuté dans le conteneur.</span><span class="sxs-lookup"><span data-stu-id="1cf30-444">**ContainerProcess_CL** Use this type to quickly see the process running within the container.</span></span>
- <span data-ttu-id="1cf30-445">**ContainerServiceLog** : utilisez ce type de journal lorsque vous recherchez des informations de piste d’audit pour le démon Docker, telles que les commandes de démarrage, d’arrêter, de suppression ou d’extraction.</span><span class="sxs-lookup"><span data-stu-id="1cf30-445">**ContainerServiceLog** – Use this type when you're trying to find audit trail information for the Docker daemon, such as start, stop, delete, or pull commands.</span></span>
- <span data-ttu-id="1cf30-446">**KubeEvents_CL** Ce type permet d’afficher les événements Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="1cf30-446">**KubeEvents_CL**  Use this type to see the Kubernetes events.</span></span>
- <span data-ttu-id="1cf30-447">**KubePodInventory_CL** Utilisez ce type lorsque vous voulez comprendre les informations de hiérarchie du cluster.</span><span class="sxs-lookup"><span data-stu-id="1cf30-447">**KubePodInventory_CL**  Use this type when you want to understand the cluster hierarchy information.</span></span>


### <a name="to-search-logs-for-container-data"></a><span data-ttu-id="1cf30-448">Pour rechercher des données de conteneur dans les journaux</span><span class="sxs-lookup"><span data-stu-id="1cf30-448">To search logs for container data</span></span>
* <span data-ttu-id="1cf30-449">Choisissez une image qui a échoué récemment et recherchez-la dans les journaux des erreurs.</span><span class="sxs-lookup"><span data-stu-id="1cf30-449">Choose an image that you know has failed recently and find the error logs for it.</span></span> <span data-ttu-id="1cf30-450">Commencez par rechercher un nom de conteneur exécutant cette image avec une recherche **ContainerInventory**.</span><span class="sxs-lookup"><span data-stu-id="1cf30-450">Start by finding a container name that is running that image with a **ContainerInventory** search.</span></span> <span data-ttu-id="1cf30-451">Par exemple, recherchez `Type=ContainerInventory ubuntu Failed`</span><span class="sxs-lookup"><span data-stu-id="1cf30-451">For example, search for `Type=ContainerInventory ubuntu Failed`</span></span>  
    <span data-ttu-id="1cf30-452">![Recherche de conteneurs Ubuntu](./media/log-analytics-containers/search-ubuntu.png)</span><span class="sxs-lookup"><span data-stu-id="1cf30-452">![Search for Ubuntu containers](./media/log-analytics-containers/search-ubuntu.png)</span></span>

  <span data-ttu-id="1cf30-453">Notez le nom du conteneur en regard de **Nom**, puis recherchez ces journaux.</span><span class="sxs-lookup"><span data-stu-id="1cf30-453">The name of the container next to **Name**, and search for those logs.</span></span> <span data-ttu-id="1cf30-454">Dans cet exemple, il s’agit de `Type=ContainerLog cranky_stonebreaker`.</span><span class="sxs-lookup"><span data-stu-id="1cf30-454">In this example, it is `Type=ContainerLog cranky_stonebreaker`.</span></span>

<span data-ttu-id="1cf30-455">**Afficher les informations de performances**</span><span class="sxs-lookup"><span data-stu-id="1cf30-455">**View performance information**</span></span>

<span data-ttu-id="1cf30-456">Lorsque vous commencez à créer des requêtes, il peut être utile de voir d’abord ce qui est possible.</span><span class="sxs-lookup"><span data-stu-id="1cf30-456">When you're beginning to construct queries, it can help to see what's possible first.</span></span> <span data-ttu-id="1cf30-457">Par exemple, pour afficher toutes les données de performances, essayez d’utiliser une large requête en tapant la requête de recherche suivante.</span><span class="sxs-lookup"><span data-stu-id="1cf30-457">For example, to see all performance data, try a broad query by typing the following search query.</span></span>

```
Type=Perf
```

![Performances des conteneurs](./media/log-analytics-containers/containers-perf01.png)

<span data-ttu-id="1cf30-459">Vous pouvez limiter les données de performances que vous voyez à un conteneur spécifique en tapant le nom de celui-ci à droite de votre requête.</span><span class="sxs-lookup"><span data-stu-id="1cf30-459">You can scope the performance data you're seeing to a specific container by typing the name of it to the right of your query.</span></span>

```
Type=Perf <containerName>
```

<span data-ttu-id="1cf30-460">Cela a pour effet d’afficher la liste des mesures de performances collectées pour un conteneur spécifique.</span><span class="sxs-lookup"><span data-stu-id="1cf30-460">That shows the list of performance metrics that are collected for an individual container.</span></span>

![Performances des conteneurs](./media/log-analytics-containers/containers-perf03.png)

## <a name="example-log-search-queries"></a><span data-ttu-id="1cf30-462">Exemples de requêtes de recherche de journal</span><span class="sxs-lookup"><span data-stu-id="1cf30-462">Example log search queries</span></span>
<span data-ttu-id="1cf30-463">Il est souvent utile de créer des requêtes en commençant par un exemple ou deux, puis en les modifiant afin de les adapter à votre environnement.</span><span class="sxs-lookup"><span data-stu-id="1cf30-463">It's often useful to build queries starting with an example or two and then modifying them to fit your environment.</span></span> <span data-ttu-id="1cf30-464">Comme point de départ, vous pouvez utiliser la zone **Exemples de requêtes** pour vous aider à créer des requêtes plus avancées.</span><span class="sxs-lookup"><span data-stu-id="1cf30-464">As a starting point, you can experiment with the **Sample Queries** area to help you build more advanced queries.</span></span>

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

![Requêtes de conteneurs](./media/log-analytics-containers/containers-queries.png)


## <a name="saving-log-search-queries"></a><span data-ttu-id="1cf30-466">Enregistrement de requêtes de recherche de journal</span><span class="sxs-lookup"><span data-stu-id="1cf30-466">Saving log search queries</span></span>
<span data-ttu-id="1cf30-467">L’enregistrement des requêtes est une fonctionnalité standard dans Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="1cf30-467">Saving queries is a standard feature in Log Analytics.</span></span> <span data-ttu-id="1cf30-468">En les enregistrant, vous aurez aisément accès à celles que vous avez trouvées utiles pour une utilisation ultérieure.</span><span class="sxs-lookup"><span data-stu-id="1cf30-468">By saving them, you'll have those that you've found useful handy for future use.</span></span>

<span data-ttu-id="1cf30-469">Après avoir créé une requête qui vous semble utile, enregistrez-la en cliquant sur **Favorites** en haut de la page Recherche de journal.</span><span class="sxs-lookup"><span data-stu-id="1cf30-469">After you create a query that you find useful, save it by clicking **Favorites** at the top of the Log Search page.</span></span> <span data-ttu-id="1cf30-470">Vous pourrez ainsi y accéder facilement par la suite à partir de la page **Mon tableau de bord**.</span><span class="sxs-lookup"><span data-stu-id="1cf30-470">Then you can easily access it later from the **My Dashboard** page.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1cf30-471">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1cf30-471">Next steps</span></span>
* <span data-ttu-id="1cf30-472">[Rechercher dans les journaux](log-analytics-log-searches.md) pour consulter des enregistrements de données de conteneur détaillées.</span><span class="sxs-lookup"><span data-stu-id="1cf30-472">[Search logs](log-analytics-log-searches.md) to view detailed container data records.</span></span>
