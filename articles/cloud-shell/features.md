---
title: "Fonctionnalités d’Azure Cloud Shell (préversion) | Microsoft Docs"
description: "Vue d’ensemble des fonctionnalités d’Azure Cloud Shell"
services: 
documentationcenter: 
author: jluk
manager: timlt
tags: azure-resource-manager
ms.assetid: 
ms.service: azure
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: juluk
ms.openlocfilehash: 67f03d5857e37b253ac57536e289b5468d69e9b5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="features-and-tools-for-azure-cloud-shell"></a><span data-ttu-id="1d8eb-103">Fonctionnalités et outils pour Azure Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="1d8eb-103">Features and Tools for Azure Cloud Shell</span></span>
<span data-ttu-id="1d8eb-104">Azure Cloud Shell est une expérience shell sur navigateur de gestion et de développement des ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="1d8eb-104">Azure Cloud Shell is a browser-based shell experience to manage and develop Azure resources.</span></span>

<span data-ttu-id="1d8eb-105">Cloud Shell offre une expérience shell, préconfigurée et accessible par le biais d’un navigateur, de gestion des ressources Azure qui dispense de la surcharge associée à l’installation, au contrôle de version et à la maintenance d’un ordinateur.</span><span class="sxs-lookup"><span data-stu-id="1d8eb-105">Cloud Shell offers a browser-accessible, pre-configured shell experience for managing Azure resources without the overhead of installing, versioning, and maintaining a machine yourself.</span></span>

<span data-ttu-id="1d8eb-106">Cloud Shell approvisionne les machines à la demande ; par conséquent, leur état n’est pas persistant d’une session à l’autre.</span><span class="sxs-lookup"><span data-stu-id="1d8eb-106">Cloud Shell provisions machines on a per-request basis and as a result machine state will not persist across sessions.</span></span> <span data-ttu-id="1d8eb-107">Cloud Shell étant conçu pour les sessions interactives, les shells s’arrêtent automatiquement après 20 minutes d’inactivité.</span><span class="sxs-lookup"><span data-stu-id="1d8eb-107">Since Cloud Shell is built for interactive sessions, shells automatically terminate after 20 minutes of shell inactivity.</span></span>

## <a name="bash-in-cloud-shell"></a><span data-ttu-id="1d8eb-108">Bash dans Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="1d8eb-108">Bash in Cloud Shell</span></span>
### <a name="tools"></a><span data-ttu-id="1d8eb-109">Outils</span><span class="sxs-lookup"><span data-stu-id="1d8eb-109">Tools</span></span>
|<span data-ttu-id="1d8eb-110">Catégorie</span><span class="sxs-lookup"><span data-stu-id="1d8eb-110">Category</span></span>   |<span data-ttu-id="1d8eb-111">Nom</span><span class="sxs-lookup"><span data-stu-id="1d8eb-111">Name</span></span>   |
|---|---|
|<span data-ttu-id="1d8eb-112">Interpréteur de commandes Linux</span><span class="sxs-lookup"><span data-stu-id="1d8eb-112">Linux shell interpreter</span></span>|<span data-ttu-id="1d8eb-113">Bash</span><span class="sxs-lookup"><span data-stu-id="1d8eb-113">Bash</span></span><br> <span data-ttu-id="1d8eb-114">sh</span><span class="sxs-lookup"><span data-stu-id="1d8eb-114">sh</span></span>               |
|<span data-ttu-id="1d8eb-115">Outils Azure</span><span class="sxs-lookup"><span data-stu-id="1d8eb-115">Azure tools</span></span>            |<span data-ttu-id="1d8eb-116">[Azure CLI 2.0](https://github.com/Azure/azure-cli) et [1.0](https://github.com/Azure/azure-xplat-cli)</span><span class="sxs-lookup"><span data-stu-id="1d8eb-116">[Azure CLI 2.0](https://github.com/Azure/azure-cli) and [1.0](https://github.com/Azure/azure-xplat-cli)</span></span><br> [<span data-ttu-id="1d8eb-117">AZCopy</span><span class="sxs-lookup"><span data-stu-id="1d8eb-117">AzCopy</span></span>](https://docs.microsoft.com/azure/storage/storage-use-azcopy)<br> [<span data-ttu-id="1d8eb-118">Lot chantier</span><span class="sxs-lookup"><span data-stu-id="1d8eb-118">Batch Shipyard</span></span>](https://github.com/Azure/batch-shipyard)     |
|<span data-ttu-id="1d8eb-119">Éditeurs de texte</span><span class="sxs-lookup"><span data-stu-id="1d8eb-119">Text editors</span></span>           |<span data-ttu-id="1d8eb-120">vim</span><span class="sxs-lookup"><span data-stu-id="1d8eb-120">vim</span></span><br> <span data-ttu-id="1d8eb-121">nano</span><span class="sxs-lookup"><span data-stu-id="1d8eb-121">nano</span></span><br> <span data-ttu-id="1d8eb-122">emacs</span><span class="sxs-lookup"><span data-stu-id="1d8eb-122">emacs</span></span>       |
|<span data-ttu-id="1d8eb-123">Contrôle de code source</span><span class="sxs-lookup"><span data-stu-id="1d8eb-123">Source control</span></span>         |<span data-ttu-id="1d8eb-124">git</span><span class="sxs-lookup"><span data-stu-id="1d8eb-124">git</span></span>                    |
|<span data-ttu-id="1d8eb-125">Outils de génération</span><span class="sxs-lookup"><span data-stu-id="1d8eb-125">Build tools</span></span>            |<span data-ttu-id="1d8eb-126">make</span><span class="sxs-lookup"><span data-stu-id="1d8eb-126">make</span></span><br> <span data-ttu-id="1d8eb-127">maven</span><span class="sxs-lookup"><span data-stu-id="1d8eb-127">maven</span></span><br> <span data-ttu-id="1d8eb-128">npm</span><span class="sxs-lookup"><span data-stu-id="1d8eb-128">npm</span></span><br> <span data-ttu-id="1d8eb-129">pip</span><span class="sxs-lookup"><span data-stu-id="1d8eb-129">pip</span></span>         |
|<span data-ttu-id="1d8eb-130">Conteneurs</span><span class="sxs-lookup"><span data-stu-id="1d8eb-130">Containers</span></span>             |<span data-ttu-id="1d8eb-131">[Docker CLI](https://github.com/docker/cli)/[Docker Machine](https://github.com/docker/machine)</span><span class="sxs-lookup"><span data-stu-id="1d8eb-131">[Docker CLI](https://github.com/docker/cli)/[Docker Machine](https://github.com/docker/machine)</span></span><br> [<span data-ttu-id="1d8eb-132">Kubectl</span><span class="sxs-lookup"><span data-stu-id="1d8eb-132">Kubectl</span></span>](https://kubernetes.io/docs/user-guide/kubectl-overview/)<br> [<span data-ttu-id="1d8eb-133">Draft</span><span class="sxs-lookup"><span data-stu-id="1d8eb-133">Draft</span></span>](https://github.com/Azure/draft)<br> [<span data-ttu-id="1d8eb-134">CLI DC/OS</span><span class="sxs-lookup"><span data-stu-id="1d8eb-134">DC/OS CLI</span></span>](https://github.com/dcos/dcos-cli)         |
|<span data-ttu-id="1d8eb-135">Bases de données</span><span class="sxs-lookup"><span data-stu-id="1d8eb-135">Databases</span></span>              |<span data-ttu-id="1d8eb-136">Client MySQL</span><span class="sxs-lookup"><span data-stu-id="1d8eb-136">MySQL client</span></span><br> <span data-ttu-id="1d8eb-137">Client PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="1d8eb-137">PostgreSql client</span></span><br> [<span data-ttu-id="1d8eb-138">Utilitaire sqlcmd</span><span class="sxs-lookup"><span data-stu-id="1d8eb-138">sqlcmd Utility</span></span>](https://docs.microsoft.com/sql/tools/sqlcmd-utility)<br> [<span data-ttu-id="1d8eb-139">mssql-scripter</span><span class="sxs-lookup"><span data-stu-id="1d8eb-139">mssql-scripter</span></span>](https://github.com/Microsoft/sql-xplat-cli) |
|<span data-ttu-id="1d8eb-140">Autres</span><span class="sxs-lookup"><span data-stu-id="1d8eb-140">Other</span></span>                  |<span data-ttu-id="1d8eb-141">Client iPython</span><span class="sxs-lookup"><span data-stu-id="1d8eb-141">iPython Client</span></span><br> [<span data-ttu-id="1d8eb-142">CLI Cloud Foundry</span><span class="sxs-lookup"><span data-stu-id="1d8eb-142">Cloud Foundry CLI</span></span>](https://github.com/cloudfoundry/cli)<br> |

### <a name="language-support"></a><span data-ttu-id="1d8eb-143">Support multilingue</span><span class="sxs-lookup"><span data-stu-id="1d8eb-143">Language support</span></span>
|<span data-ttu-id="1d8eb-144">language</span><span class="sxs-lookup"><span data-stu-id="1d8eb-144">Language</span></span>   |<span data-ttu-id="1d8eb-145">Version</span><span class="sxs-lookup"><span data-stu-id="1d8eb-145">Version</span></span>   |
|---|---|
|<span data-ttu-id="1d8eb-146">.NET</span><span class="sxs-lookup"><span data-stu-id="1d8eb-146">.NET</span></span>       |<span data-ttu-id="1d8eb-147">1.01</span><span class="sxs-lookup"><span data-stu-id="1d8eb-147">1.01</span></span>       |
|<span data-ttu-id="1d8eb-148">Go</span><span class="sxs-lookup"><span data-stu-id="1d8eb-148">Go</span></span>         |<span data-ttu-id="1d8eb-149">1.7</span><span class="sxs-lookup"><span data-stu-id="1d8eb-149">1.7</span></span>        |
|<span data-ttu-id="1d8eb-150">Java</span><span class="sxs-lookup"><span data-stu-id="1d8eb-150">Java</span></span>       |<span data-ttu-id="1d8eb-151">1.8</span><span class="sxs-lookup"><span data-stu-id="1d8eb-151">1.8</span></span>        |
|<span data-ttu-id="1d8eb-152">Node.js</span><span class="sxs-lookup"><span data-stu-id="1d8eb-152">Node.js</span></span>    |<span data-ttu-id="1d8eb-153">6.9.4</span><span class="sxs-lookup"><span data-stu-id="1d8eb-153">6.9.4</span></span>      |
|<span data-ttu-id="1d8eb-154">Python</span><span class="sxs-lookup"><span data-stu-id="1d8eb-154">Python</span></span>     |<span data-ttu-id="1d8eb-155">2.7 et 3.5 (par défaut)</span><span class="sxs-lookup"><span data-stu-id="1d8eb-155">2.7 and 3.5 (default)</span></span>|

## <a name="secure-automatic-authentication"></a><span data-ttu-id="1d8eb-156">Authentification automatique sécurisée</span><span class="sxs-lookup"><span data-stu-id="1d8eb-156">Secure automatic authentication</span></span>
<span data-ttu-id="1d8eb-157">Cloud Shell authentifie automatiquement et en toute sécurité l’accès au compte pour Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="1d8eb-157">Cloud Shell securely and automatically authenticates account access for the Azure CLI 2.0.</span></span>

## <a name="azure-files-persistence"></a><span data-ttu-id="1d8eb-158">Persistance Azure Files</span><span class="sxs-lookup"><span data-stu-id="1d8eb-158">Azure Files persistence</span></span>
<span data-ttu-id="1d8eb-159">Cloud Shell étant alloué à la demande à l’aide d’un ordinateur temporaire, les fichiers qui ne se trouvent pas dans $Home et l’état de l’ordinateur ne sont pas persistants d’une session à l’autre.</span><span class="sxs-lookup"><span data-stu-id="1d8eb-159">Since Cloud Shell is allocated on a per-request basis using a temporary machine, files outside of your $Home and machine state are not persisted across sessions.</span></span>
<span data-ttu-id="1d8eb-160">Pour conserver les fichiers entre les sessions, Cloud Shell vous guide à travers le processus d’association d’un partage de fichiers Azure au premier lancement.</span><span class="sxs-lookup"><span data-stu-id="1d8eb-160">To persist files across sessions, Cloud Shell walks you through attaching an Azure file share on first launch.</span></span>
<span data-ttu-id="1d8eb-161">Par la suite, Cloud Shell associera automatiquement votre espace de stockage pour toutes les sessions à venir.</span><span class="sxs-lookup"><span data-stu-id="1d8eb-161">Once completed Cloud Shell will automatically attach your storage for all future sessions.</span></span>

[<span data-ttu-id="1d8eb-162">En savoir plus sur l’association de partages de fichiers Azure à Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="1d8eb-162">Learn more about attaching Azure file shares to Cloud Shell.</span></span>](persisting-shell-storage.md)

## <a name="next-steps"></a><span data-ttu-id="1d8eb-163">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1d8eb-163">Next steps</span></span>
[<span data-ttu-id="1d8eb-164">Démarrage rapide de Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="1d8eb-164">Cloud Shell Quickstart</span></span>](quickstart.md) <br><span data-ttu-id="1d8eb-165">
[En savoir plus sur Azure CLI 2.0](https://docs.microsoft.com/cli/azure/)</span><span class="sxs-lookup"><span data-stu-id="1d8eb-165">
[Learn about Azure CLI 2.0](https://docs.microsoft.com/cli/azure/)</span></span> <br>