---
title: "Vue d’ensemble d’Azure Cloud Shell (version préliminaire) | Microsoft Docs"
description: "Vue d’ensemble d’Azure Cloud Shell."
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
ms.date: 07/10/2017
ms.author: juluk
ms.openlocfilehash: 7165633cd354eeea2e3619f839338e6af1524e56
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="overview-of-azure-cloud-shell-preview"></a><span data-ttu-id="1d6e7-103">Vue d’ensemble d’Azure Cloud Shell (version préliminaire)</span><span class="sxs-lookup"><span data-stu-id="1d6e7-103">Overview of Azure Cloud Shell (Preview)</span></span>
<span data-ttu-id="1d6e7-104">Azure Cloud Shell est un shell interactif, accessible par navigateur pour la gestion des ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="1d6e7-104">Azure Cloud Shell is an interactive, browser-accessible shell for managing Azure resources.</span></span>

![](media/overview-pic.png)

## <a name="features"></a><span data-ttu-id="1d6e7-105">Caractéristiques</span><span class="sxs-lookup"><span data-stu-id="1d6e7-105">Features</span></span>
### <a name="browser-based-shell-experience"></a><span data-ttu-id="1d6e7-106">Expérience shell basée sur navigateur</span><span class="sxs-lookup"><span data-stu-id="1d6e7-106">Browser-based shell experience</span></span>
<span data-ttu-id="1d6e7-107">Cloud Shell permet d’accéder à une expérience de ligne de commande basée sur navigateur avec les tâches de gestion Azure à l’esprit.</span><span class="sxs-lookup"><span data-stu-id="1d6e7-107">Cloud Shell enables access to a browser-based command-line experience built with Azure management tasks in mind.</span></span> <span data-ttu-id="1d6e7-108">Exploitez Cloud Shell pour travailler librement à partir d’une machine locale d’une façon que seul le cloud peut fournir.</span><span class="sxs-lookup"><span data-stu-id="1d6e7-108">Leverage Cloud Shell to work untethered from a local machine in a way only the cloud can provide.</span></span>

### <a name="pre-configured-azure-workstation"></a><span data-ttu-id="1d6e7-109">Station de travail Azure préconfigurée</span><span class="sxs-lookup"><span data-stu-id="1d6e7-109">Pre-configured Azure workstation</span></span>
<span data-ttu-id="1d6e7-110">Cloud Shell est préinstallé avec des outils de ligne de commande et la prise en charge de langages populaires afin de pouvoir travailler plus rapidement.</span><span class="sxs-lookup"><span data-stu-id="1d6e7-110">Cloud Shell comes pre-installed with popular command-line tools and language support so you can work faster.</span></span>

[<span data-ttu-id="1d6e7-111">Consultez la liste complète des outils pour Azure Cloud Shell ici.</span><span class="sxs-lookup"><span data-stu-id="1d6e7-111">View the full tooling list for Azure Cloud Shell here.</span></span>](features.md#tools)

### <a name="automatic-authentication"></a><span data-ttu-id="1d6e7-112">Authentification automatique</span><span class="sxs-lookup"><span data-stu-id="1d6e7-112">Automatic authentication</span></span>
<span data-ttu-id="1d6e7-113">Cloud Shell s’authentifie automatiquement de façon sécurisée sur chaque session pour accéder immédiatement à vos ressources via Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="1d6e7-113">Cloud Shell securely authenticates automatically on each session for instant access to your resources through the Azure CLI 2.0.</span></span>

### <a name="connect-your-azure-file-storage"></a><span data-ttu-id="1d6e7-114">Connexion à votre stockage de fichiers Azure</span><span class="sxs-lookup"><span data-stu-id="1d6e7-114">Connect your Azure File storage</span></span>
<span data-ttu-id="1d6e7-115">Les machines Cloud Shell sont temporaires et nécessitent ainsi qu’un partage de fichiers Azure soit monté en tant que `clouddrive` pour conserver votre répertoire $Home.</span><span class="sxs-lookup"><span data-stu-id="1d6e7-115">Cloud Shell machines are temporary and as a result require an Azure file share to be mounted as `clouddrive` to persist your $Home directory.</span></span>
<span data-ttu-id="1d6e7-116">Lors du premier lancement, Cloud Shell vous invite à créer un groupe de ressources, un compte de stockage et un partage de fichiers en votre nom.</span><span class="sxs-lookup"><span data-stu-id="1d6e7-116">On first launch Cloud Shell prompts to create a resource group, storage account, and file share on your behalf.</span></span> <span data-ttu-id="1d6e7-117">Il s’agit d’une étape unique, et ces ressources sont automatiquement jointes pour toutes les sessions.</span><span class="sxs-lookup"><span data-stu-id="1d6e7-117">This is a one-time step and will be automatically attached for all sessions.</span></span> 

#### <a name="create-new-storage"></a><span data-ttu-id="1d6e7-118">Créer un stockage</span><span class="sxs-lookup"><span data-stu-id="1d6e7-118">Create new storage</span></span>
![](media/basic-storage.png)

<span data-ttu-id="1d6e7-119">Un compte de stockage localement redondant (LRS) peut être créé en votre nom avec un partage de fichiers Azure contenant une image de disque de 5 Go par défaut.</span><span class="sxs-lookup"><span data-stu-id="1d6e7-119">A locally-redundant storage (LRS) account can be created on your behalf with an Azure file share containing a default 5-GB disk image.</span></span> <span data-ttu-id="1d6e7-120">Le partage de fichiers se monte en tant que `clouddrive` pour l’interaction du partage de fichiers avec l’image de disque utilisée pour synchroniser et conserver votre répertoire $Home.</span><span class="sxs-lookup"><span data-stu-id="1d6e7-120">The file share mounts as `clouddrive` for file share interaction with the disk image being used to sync and persist your $Home directory.</span></span> <span data-ttu-id="1d6e7-121">Les coûts de stockage standard s’appliquent.</span><span class="sxs-lookup"><span data-stu-id="1d6e7-121">Regular storage costs apply.</span></span>

<span data-ttu-id="1d6e7-122">Trois ressources sont créées en votre nom :</span><span class="sxs-lookup"><span data-stu-id="1d6e7-122">Three resources will be created on your behalf:</span></span>
1. <span data-ttu-id="1d6e7-123">Groupe de ressources nommé : `cloud-shell-storage-<region>`</span><span class="sxs-lookup"><span data-stu-id="1d6e7-123">Resource Group named: `cloud-shell-storage-<region>`</span></span>
2. <span data-ttu-id="1d6e7-124">Compte de stockage nommé : `cs<uniqueGuid>`</span><span class="sxs-lookup"><span data-stu-id="1d6e7-124">Storage Account named: `cs<uniqueGuid>`</span></span>
3. <span data-ttu-id="1d6e7-125">Partage de fichiers nommé : `cs-<user>-<domain>-com-uniqueGuid`</span><span class="sxs-lookup"><span data-stu-id="1d6e7-125">File Share named: `cs-<user>-<domain>-com-uniqueGuid`</span></span>

> [!Note]
> <span data-ttu-id="1d6e7-126">Tous les fichiers figurant dans votre répertoire $Home, tels que les clés SSH, sont conservés dans l’image de disque utilisateur stockée dans votre partage de fichiers monté.</span><span class="sxs-lookup"><span data-stu-id="1d6e7-126">All files in your $Home directory such as SSH keys are persisted in your user disk image stored in your mounted file share.</span></span> <span data-ttu-id="1d6e7-127">Appliquez les meilleures pratiques lors de l’enregistrement des fichiers dans votre répertoire $Home et le partage de fichiers monté.</span><span class="sxs-lookup"><span data-stu-id="1d6e7-127">Apply best practices when saving files in your $Home directory and mounted file share.</span></span>

#### <a name="use-existing-resources"></a><span data-ttu-id="1d6e7-128">Utiliser les ressources existantes</span><span class="sxs-lookup"><span data-stu-id="1d6e7-128">Use existing resources</span></span>
![](media/advanced-storage.png)

<span data-ttu-id="1d6e7-129">Vous disposez également d’une option avancée qui vous permet d’associer des ressources existantes à Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="1d6e7-129">An advanced option is also provided allowing you to associate existing resources to Cloud Shell.</span></span> <span data-ttu-id="1d6e7-130">Lorsque l’invite de configuration du stockage s’affiche, cliquez sur « Afficher les paramètres avancés » pour sélectionner des options supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="1d6e7-130">When presented with the storage setup prompt, click "Show advanced settings" to select additional options.</span></span> <span data-ttu-id="1d6e7-131">Les listes déroulantes sont filtrées pour la région Cloud Shell qui vous a été attribuée et pour les comptes de stockage localement/globalement redondant.</span><span class="sxs-lookup"><span data-stu-id="1d6e7-131">Dropdowns are filtered for your assigned Cloud Shell region and locally/globally-redundant storage accounts.</span></span>

<span data-ttu-id="1d6e7-132">[Découvrez le stockage Cloud Shell, la mise à jour des partages de fichiers et le chargement/téléchargement de fichiers.] (persisting-shell-storage.md)</span><span class="sxs-lookup"><span data-stu-id="1d6e7-132">[Learn about Cloud Shell storage, updating file shares, and uploading/downloading files.] (persisting-shell-storage.md)</span></span>

## <a name="concepts"></a><span data-ttu-id="1d6e7-133">Concepts</span><span class="sxs-lookup"><span data-stu-id="1d6e7-133">Concepts</span></span>
* <span data-ttu-id="1d6e7-134">Cloud Shell s’exécute sur une machine temporaire fournie par session et par utilisateur</span><span class="sxs-lookup"><span data-stu-id="1d6e7-134">Cloud Shell runs on a temporary machine provided on a per-session, per-user basis</span></span>
* <span data-ttu-id="1d6e7-135">Cloud Shell expire après 20 minutes sans activité interactive</span><span class="sxs-lookup"><span data-stu-id="1d6e7-135">Cloud Shell times out after 20 minutes without interactive activity</span></span>
* <span data-ttu-id="1d6e7-136">Cloud Shell est accessible uniquement avec un partage de fichiers attaché</span><span class="sxs-lookup"><span data-stu-id="1d6e7-136">Cloud Shell can only be accessed with a file share attached</span></span>
* <span data-ttu-id="1d6e7-137">Cloud Shell est affecté à une machine par compte d’utilisateur</span><span class="sxs-lookup"><span data-stu-id="1d6e7-137">Cloud Shell is assigned one machine per user account</span></span>
* <span data-ttu-id="1d6e7-138">Les autorisations sont définies en tant qu’utilisateur Linux standard</span><span class="sxs-lookup"><span data-stu-id="1d6e7-138">Permissions are set as a regular Linux user</span></span>

[<span data-ttu-id="1d6e7-139">Découvrez-en davantage sur toutes les fonctionnalités de Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="1d6e7-139">Learn more about all Cloud Shell features.</span></span>](features.md)

## <a name="examples"></a><span data-ttu-id="1d6e7-140">Exemples</span><span class="sxs-lookup"><span data-stu-id="1d6e7-140">Examples</span></span>
* <span data-ttu-id="1d6e7-141">Créer ou modifier des scripts pour automatiser la gestion Azure</span><span class="sxs-lookup"><span data-stu-id="1d6e7-141">Create or edit scripts to automate Azure management</span></span>
* <span data-ttu-id="1d6e7-142">Gérer simultanément des ressources via le portail Azure et Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="1d6e7-142">Simultaneously manage resources via Azure portal and Azure CLI 2.0</span></span>
* <span data-ttu-id="1d6e7-143">Essayer Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="1d6e7-143">Test-drive Azure CLI 2.0</span></span>

[<span data-ttu-id="1d6e7-144">Essayez tous ces exemples sur le démarrage rapide de Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="1d6e7-144">Try out all these examples at the Cloud Shell quickstart.</span></span>](quickstart.md)

## <a name="pricing"></a><span data-ttu-id="1d6e7-145">Tarification</span><span class="sxs-lookup"><span data-stu-id="1d6e7-145">Pricing</span></span>
<span data-ttu-id="1d6e7-146">La machine qui héberge Cloud Shell est gratuite, avec comme condition préalable le montage d’un partage de fichiers Azure pour conserver votre répertoire $Home.</span><span class="sxs-lookup"><span data-stu-id="1d6e7-146">The machine hosting Cloud Shell is free, with a pre-requisite of a mounted Azure file share to persist your $Home directory.</span></span> <span data-ttu-id="1d6e7-147">Les coûts de stockage standard s’appliquent.</span><span class="sxs-lookup"><span data-stu-id="1d6e7-147">Regular storage costs apply.</span></span>

## <a name="supported-browsers"></a><span data-ttu-id="1d6e7-148">Navigateurs pris en charge</span><span class="sxs-lookup"><span data-stu-id="1d6e7-148">Supported browsers</span></span>
<span data-ttu-id="1d6e7-149">Cloud Shell est recommandé pour Chrome, Safari et Edge.</span><span class="sxs-lookup"><span data-stu-id="1d6e7-149">Cloud Shell is recommended for Chrome, Edge, and Safari.</span></span> <span data-ttu-id="1d6e7-150">Si Cloud Shell est pris en charge par Chrome, Firefox, Safari, IE et Edge, il est soumis aux paramètres propres au navigateur.</span><span class="sxs-lookup"><span data-stu-id="1d6e7-150">While Cloud Shell is supported for Chrome, Firefox, Safari, IE, and Edge, Cloud Shell is subject to specific browser settings.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="1d6e7-151">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="1d6e7-151">Troubleshooting</span></span>
1. <span data-ttu-id="1d6e7-152">Lorsque j’utilise un abonnement Azure Active Directory, je ne peux pas créer de stockage en raison de l’erreur : 400 DisallowedOperation.</span><span class="sxs-lookup"><span data-stu-id="1d6e7-152">When using an Azure Active Directory subscription, I cannot create storage due to Error: 400 DisallowedOperation.</span></span> <span data-ttu-id="1d6e7-153">Pour résoudre ce problème, utilisez un abonnement Azure habilité à créer des ressources de stockage.</span><span class="sxs-lookup"><span data-stu-id="1d6e7-153">To resolve this, please use an Azure subscription capable of creating storage resources.</span></span> <span data-ttu-id="1d6e7-154">Les abonnements AD ne peuvent pas créer de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="1d6e7-154">AD subscriptions are not able to create Azure resources.</span></span>

<span data-ttu-id="1d6e7-155">Pour connaître les limitations spécifiques connues, consultez les [limitations de Cloud Shell](limitations.md).</span><span class="sxs-lookup"><span data-stu-id="1d6e7-155">For specific known limitations, visit [limitations of Cloud Shell](limitations.md).</span></span>
