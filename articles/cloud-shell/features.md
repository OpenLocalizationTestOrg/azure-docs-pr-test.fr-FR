---
title: "fonctionnalités du Shell du Cloud (version préliminaire) aaaAzure | Documents Microsoft"
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
ms.openlocfilehash: 65482ca6caeac01dda18a6b12eabe943e3d68a96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="features-and-tools-for-azure-cloud-shell"></a><span data-ttu-id="f9258-103">Fonctionnalités et outils pour Azure Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="f9258-103">Features and Tools for Azure Cloud Shell</span></span>
<span data-ttu-id="f9258-104">Azure Cloud Shell est un toomanage d’expérience basée sur navigateur de shell et développer des ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="f9258-104">Azure Cloud Shell is a browser-based shell experience toomanage and develop Azure resources.</span></span>

<span data-ttu-id="f9258-105">Shell de cloud computing offre un navigateur accessible, préconfiguré expérience d’interpréteur de commandes pour la gestion des ressources Azure sans surcharge hello de l’installation, le contrôle de version et la gestion d’un ordinateur vous-même.</span><span class="sxs-lookup"><span data-stu-id="f9258-105">Cloud Shell offers a browser-accessible, pre-configured shell experience for managing Azure resources without hello overhead of installing, versioning, and maintaining a machine yourself.</span></span>

<span data-ttu-id="f9258-106">Cloud Shell approvisionne les machines à la demande ; par conséquent, leur état n’est pas persistant d’une session à l’autre.</span><span class="sxs-lookup"><span data-stu-id="f9258-106">Cloud Shell provisions machines on a per-request basis and as a result machine state will not persist across sessions.</span></span> <span data-ttu-id="f9258-107">Cloud Shell étant conçu pour les sessions interactives, les shells s’arrêtent automatiquement après 20 minutes d’inactivité.</span><span class="sxs-lookup"><span data-stu-id="f9258-107">Since Cloud Shell is built for interactive sessions, shells automatically terminate after 20 minutes of shell inactivity.</span></span>

## <a name="bash-in-cloud-shell"></a><span data-ttu-id="f9258-108">Bash dans Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="f9258-108">Bash in Cloud Shell</span></span>
### <a name="tools"></a><span data-ttu-id="f9258-109">Outils</span><span class="sxs-lookup"><span data-stu-id="f9258-109">Tools</span></span>
|<span data-ttu-id="f9258-110">Catégorie</span><span class="sxs-lookup"><span data-stu-id="f9258-110">Category</span></span>   |<span data-ttu-id="f9258-111">Nom</span><span class="sxs-lookup"><span data-stu-id="f9258-111">Name</span></span>   |
|---|---|
|<span data-ttu-id="f9258-112">Interpréteur de commandes Linux</span><span class="sxs-lookup"><span data-stu-id="f9258-112">Linux shell interpreter</span></span>|<span data-ttu-id="f9258-113">Bash</span><span class="sxs-lookup"><span data-stu-id="f9258-113">Bash</span></span><br> <span data-ttu-id="f9258-114">sh</span><span class="sxs-lookup"><span data-stu-id="f9258-114">sh</span></span>               |
|<span data-ttu-id="f9258-115">Outils Azure</span><span class="sxs-lookup"><span data-stu-id="f9258-115">Azure tools</span></span>            |<span data-ttu-id="f9258-116">[Azure CLI 2.0](https://github.com/Azure/azure-cli) et [1.0](https://github.com/Azure/azure-xplat-cli)</span><span class="sxs-lookup"><span data-stu-id="f9258-116">[Azure CLI 2.0](https://github.com/Azure/azure-cli) and [1.0](https://github.com/Azure/azure-xplat-cli)</span></span><br> [<span data-ttu-id="f9258-117">AZCopy</span><span class="sxs-lookup"><span data-stu-id="f9258-117">AzCopy</span></span>](https://docs.microsoft.com/azure/storage/storage-use-azcopy)<br> [<span data-ttu-id="f9258-118">Lot chantier</span><span class="sxs-lookup"><span data-stu-id="f9258-118">Batch Shipyard</span></span>](https://github.com/Azure/batch-shipyard)     |
|<span data-ttu-id="f9258-119">Éditeurs de texte</span><span class="sxs-lookup"><span data-stu-id="f9258-119">Text editors</span></span>           |<span data-ttu-id="f9258-120">vim</span><span class="sxs-lookup"><span data-stu-id="f9258-120">vim</span></span><br> <span data-ttu-id="f9258-121">nano</span><span class="sxs-lookup"><span data-stu-id="f9258-121">nano</span></span><br> <span data-ttu-id="f9258-122">emacs</span><span class="sxs-lookup"><span data-stu-id="f9258-122">emacs</span></span>       |
|<span data-ttu-id="f9258-123">Contrôle de code source</span><span class="sxs-lookup"><span data-stu-id="f9258-123">Source control</span></span>         |<span data-ttu-id="f9258-124">git</span><span class="sxs-lookup"><span data-stu-id="f9258-124">git</span></span>                    |
|<span data-ttu-id="f9258-125">Outils de génération</span><span class="sxs-lookup"><span data-stu-id="f9258-125">Build tools</span></span>            |<span data-ttu-id="f9258-126">make</span><span class="sxs-lookup"><span data-stu-id="f9258-126">make</span></span><br> <span data-ttu-id="f9258-127">maven</span><span class="sxs-lookup"><span data-stu-id="f9258-127">maven</span></span><br> <span data-ttu-id="f9258-128">npm</span><span class="sxs-lookup"><span data-stu-id="f9258-128">npm</span></span><br> <span data-ttu-id="f9258-129">pip</span><span class="sxs-lookup"><span data-stu-id="f9258-129">pip</span></span>         |
|<span data-ttu-id="f9258-130">Conteneurs</span><span class="sxs-lookup"><span data-stu-id="f9258-130">Containers</span></span>             |<span data-ttu-id="f9258-131">[Docker CLI](https://github.com/docker/cli)/[Docker Machine](https://github.com/docker/machine)</span><span class="sxs-lookup"><span data-stu-id="f9258-131">[Docker CLI](https://github.com/docker/cli)/[Docker Machine](https://github.com/docker/machine)</span></span><br> [<span data-ttu-id="f9258-132">Kubectl</span><span class="sxs-lookup"><span data-stu-id="f9258-132">Kubectl</span></span>](https://kubernetes.io/docs/user-guide/kubectl-overview/)<br> [<span data-ttu-id="f9258-133">Draft</span><span class="sxs-lookup"><span data-stu-id="f9258-133">Draft</span></span>](https://github.com/Azure/draft)<br> [<span data-ttu-id="f9258-134">CLI DC/OS</span><span class="sxs-lookup"><span data-stu-id="f9258-134">DC/OS CLI</span></span>](https://github.com/dcos/dcos-cli)         |
|<span data-ttu-id="f9258-135">Bases de données</span><span class="sxs-lookup"><span data-stu-id="f9258-135">Databases</span></span>              |<span data-ttu-id="f9258-136">Client MySQL</span><span class="sxs-lookup"><span data-stu-id="f9258-136">MySQL client</span></span><br> <span data-ttu-id="f9258-137">Client PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="f9258-137">PostgreSql client</span></span><br> [<span data-ttu-id="f9258-138">Utilitaire sqlcmd</span><span class="sxs-lookup"><span data-stu-id="f9258-138">sqlcmd Utility</span></span>](https://docs.microsoft.com/sql/tools/sqlcmd-utility)<br> [<span data-ttu-id="f9258-139">mssql-scripter</span><span class="sxs-lookup"><span data-stu-id="f9258-139">mssql-scripter</span></span>](https://github.com/Microsoft/sql-xplat-cli) |
|<span data-ttu-id="f9258-140">Autres</span><span class="sxs-lookup"><span data-stu-id="f9258-140">Other</span></span>                  |<span data-ttu-id="f9258-141">Client iPython</span><span class="sxs-lookup"><span data-stu-id="f9258-141">iPython Client</span></span><br> [<span data-ttu-id="f9258-142">CLI Cloud Foundry</span><span class="sxs-lookup"><span data-stu-id="f9258-142">Cloud Foundry CLI</span></span>](https://github.com/cloudfoundry/cli)<br> |

### <a name="language-support"></a><span data-ttu-id="f9258-143">Support multilingue</span><span class="sxs-lookup"><span data-stu-id="f9258-143">Language support</span></span>
|<span data-ttu-id="f9258-144">language</span><span class="sxs-lookup"><span data-stu-id="f9258-144">Language</span></span>   |<span data-ttu-id="f9258-145">Version</span><span class="sxs-lookup"><span data-stu-id="f9258-145">Version</span></span>   |
|---|---|
|<span data-ttu-id="f9258-146">.NET</span><span class="sxs-lookup"><span data-stu-id="f9258-146">.NET</span></span>       |<span data-ttu-id="f9258-147">1.01</span><span class="sxs-lookup"><span data-stu-id="f9258-147">1.01</span></span>       |
|<span data-ttu-id="f9258-148">Go</span><span class="sxs-lookup"><span data-stu-id="f9258-148">Go</span></span>         |<span data-ttu-id="f9258-149">1.7</span><span class="sxs-lookup"><span data-stu-id="f9258-149">1.7</span></span>        |
|<span data-ttu-id="f9258-150">Java</span><span class="sxs-lookup"><span data-stu-id="f9258-150">Java</span></span>       |<span data-ttu-id="f9258-151">1.8</span><span class="sxs-lookup"><span data-stu-id="f9258-151">1.8</span></span>        |
|<span data-ttu-id="f9258-152">Node.js</span><span class="sxs-lookup"><span data-stu-id="f9258-152">Node.js</span></span>    |<span data-ttu-id="f9258-153">6.9.4</span><span class="sxs-lookup"><span data-stu-id="f9258-153">6.9.4</span></span>      |
|<span data-ttu-id="f9258-154">Python</span><span class="sxs-lookup"><span data-stu-id="f9258-154">Python</span></span>     |<span data-ttu-id="f9258-155">2.7 et 3.5 (par défaut)</span><span class="sxs-lookup"><span data-stu-id="f9258-155">2.7 and 3.5 (default)</span></span>|

## <a name="secure-automatic-authentication"></a><span data-ttu-id="f9258-156">Authentification automatique sécurisée</span><span class="sxs-lookup"><span data-stu-id="f9258-156">Secure automatic authentication</span></span>
<span data-ttu-id="f9258-157">Cloud Shell automatiquement et en toute sécurité authentifie l’accès de compte pour hello Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="f9258-157">Cloud Shell securely and automatically authenticates account access for hello Azure CLI 2.0.</span></span>

## <a name="azure-files-persistence"></a><span data-ttu-id="f9258-158">Persistance Azure Files</span><span class="sxs-lookup"><span data-stu-id="f9258-158">Azure Files persistence</span></span>
<span data-ttu-id="f9258-159">Cloud Shell étant alloué à la demande à l’aide d’un ordinateur temporaire, les fichiers qui ne se trouvent pas dans $Home et l’état de l’ordinateur ne sont pas persistants d’une session à l’autre.</span><span class="sxs-lookup"><span data-stu-id="f9258-159">Since Cloud Shell is allocated on a per-request basis using a temporary machine, files outside of your $Home and machine state are not persisted across sessions.</span></span>
<span data-ttu-id="f9258-160">fichiers toopersist entre les sessions, vous guident dans l’attachement d’un fichier Azure partagez parcours de Cloud Shell sur le premier lancement.</span><span class="sxs-lookup"><span data-stu-id="f9258-160">toopersist files across sessions, Cloud Shell walks you through attaching an Azure file share on first launch.</span></span>
<span data-ttu-id="f9258-161">Par la suite, Cloud Shell associera automatiquement votre espace de stockage pour toutes les sessions à venir.</span><span class="sxs-lookup"><span data-stu-id="f9258-161">Once completed Cloud Shell will automatically attach your storage for all future sessions.</span></span>

[<span data-ttu-id="f9258-162">En savoir plus sur l’attachement de partages de fichiers Azure tooCloud Shell.</span><span class="sxs-lookup"><span data-stu-id="f9258-162">Learn more about attaching Azure file shares tooCloud Shell.</span></span>](persisting-shell-storage.md)

## <a name="next-steps"></a><span data-ttu-id="f9258-163">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f9258-163">Next steps</span></span>
[<span data-ttu-id="f9258-164">Démarrage rapide de Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="f9258-164">Cloud Shell Quickstart</span></span>](quickstart.md) <br><span data-ttu-id="f9258-165">
[En savoir plus sur Azure CLI 2.0](https://docs.microsoft.com/cli/azure/)</span><span class="sxs-lookup"><span data-stu-id="f9258-165">
[Learn about Azure CLI 2.0](https://docs.microsoft.com/cli/azure/)</span></span> <br>