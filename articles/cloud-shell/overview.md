---
title: "vue d’ensemble du Cloud Shell (version préliminaire) aaaAzure | Documents Microsoft"
description: "Vue d’ensemble de hello Azure Cloud Shell."
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
ms.openlocfilehash: 45c6c85b167a90947a333f44a9186e2c01b4fa7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-azure-cloud-shell-preview"></a><span data-ttu-id="c3f5c-103">Vue d’ensemble d’Azure Cloud Shell (version préliminaire)</span><span class="sxs-lookup"><span data-stu-id="c3f5c-103">Overview of Azure Cloud Shell (Preview)</span></span>
<span data-ttu-id="c3f5c-104">Azure Cloud Shell est un shell interactif, accessible par navigateur pour la gestion des ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="c3f5c-104">Azure Cloud Shell is an interactive, browser-accessible shell for managing Azure resources.</span></span>

![](media/overview-pic.png)

## <a name="features"></a><span data-ttu-id="c3f5c-105">Caractéristiques</span><span class="sxs-lookup"><span data-stu-id="c3f5c-105">Features</span></span>
### <a name="browser-based-shell-experience"></a><span data-ttu-id="c3f5c-106">Expérience shell basée sur navigateur</span><span class="sxs-lookup"><span data-stu-id="c3f5c-106">Browser-based shell experience</span></span>
<span data-ttu-id="c3f5c-107">Interpréteur de commandes permet l’accès tooa basée sur navigateur de ligne de commande expérience générée à l’aide des tâches de gestion Azure à l’esprit le cloud.</span><span class="sxs-lookup"><span data-stu-id="c3f5c-107">Cloud Shell enables access tooa browser-based command-line experience built with Azure management tasks in mind.</span></span> <span data-ttu-id="c3f5c-108">Tirer parti de toowork Cloud Shell disposerez à partir d’un ordinateur local de façon uniquement des cloud hello peut fournir.</span><span class="sxs-lookup"><span data-stu-id="c3f5c-108">Leverage Cloud Shell toowork untethered from a local machine in a way only hello cloud can provide.</span></span>

### <a name="pre-configured-azure-workstation"></a><span data-ttu-id="c3f5c-109">Station de travail Azure préconfigurée</span><span class="sxs-lookup"><span data-stu-id="c3f5c-109">Pre-configured Azure workstation</span></span>
<span data-ttu-id="c3f5c-110">Cloud Shell est préinstallé avec des outils de ligne de commande et la prise en charge de langages populaires afin de pouvoir travailler plus rapidement.</span><span class="sxs-lookup"><span data-stu-id="c3f5c-110">Cloud Shell comes pre-installed with popular command-line tools and language support so you can work faster.</span></span>

[<span data-ttu-id="c3f5c-111">Hello complète d’outils liste d’affichage pour Azure Cloud Shell ici.</span><span class="sxs-lookup"><span data-stu-id="c3f5c-111">View hello full tooling list for Azure Cloud Shell here.</span></span>](features.md#tools)

### <a name="automatic-authentication"></a><span data-ttu-id="c3f5c-112">Authentification automatique</span><span class="sxs-lookup"><span data-stu-id="c3f5c-112">Automatic authentication</span></span>
<span data-ttu-id="c3f5c-113">Interpréteur de commandes de nuage en toute sécurité authentifie automatiquement sur chaque session pour les ressources de tooyour accès instantané via hello Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="c3f5c-113">Cloud Shell securely authenticates automatically on each session for instant access tooyour resources through hello Azure CLI 2.0.</span></span>

### <a name="connect-your-azure-file-storage"></a><span data-ttu-id="c3f5c-114">Connexion à votre stockage de fichiers Azure</span><span class="sxs-lookup"><span data-stu-id="c3f5c-114">Connect your Azure File storage</span></span>
<span data-ttu-id="c3f5c-115">Cloud Shell machines sont temporaires et ainsi nécessiter une toobe de partage de fichiers Azure monté en tant que `clouddrive` toopersist votre répertoire $Home.</span><span class="sxs-lookup"><span data-stu-id="c3f5c-115">Cloud Shell machines are temporary and as a result require an Azure file share toobe mounted as `clouddrive` toopersist your $Home directory.</span></span>
<span data-ttu-id="c3f5c-116">Au premier lancement Cloud Shell invite toocreate qu'un groupe de ressources, compte de stockage et partage de fichiers à votre place.</span><span class="sxs-lookup"><span data-stu-id="c3f5c-116">On first launch Cloud Shell prompts toocreate a resource group, storage account, and file share on your behalf.</span></span> <span data-ttu-id="c3f5c-117">Il s’agit d’une étape unique, et ces ressources sont automatiquement jointes pour toutes les sessions.</span><span class="sxs-lookup"><span data-stu-id="c3f5c-117">This is a one-time step and will be automatically attached for all sessions.</span></span> 

#### <a name="create-new-storage"></a><span data-ttu-id="c3f5c-118">Créer un stockage</span><span class="sxs-lookup"><span data-stu-id="c3f5c-118">Create new storage</span></span>
![](media/basic-storage.png)

<span data-ttu-id="c3f5c-119">Un compte de stockage localement redondant (LRS) peut être créé en votre nom avec un partage de fichiers Azure contenant une image de disque de 5 Go par défaut.</span><span class="sxs-lookup"><span data-stu-id="c3f5c-119">A locally-redundant storage (LRS) account can be created on your behalf with an Azure file share containing a default 5-GB disk image.</span></span> <span data-ttu-id="c3f5c-120">partage de fichiers Hello monte comme `clouddrive` pour le fichier partagent une interaction avec l’image de disque hello en cours toosync utilisé et conserver votre répertoire $Home.</span><span class="sxs-lookup"><span data-stu-id="c3f5c-120">hello file share mounts as `clouddrive` for file share interaction with hello disk image being used toosync and persist your $Home directory.</span></span> <span data-ttu-id="c3f5c-121">Les coûts de stockage standard s’appliquent.</span><span class="sxs-lookup"><span data-stu-id="c3f5c-121">Regular storage costs apply.</span></span>

<span data-ttu-id="c3f5c-122">Trois ressources sont créées en votre nom :</span><span class="sxs-lookup"><span data-stu-id="c3f5c-122">Three resources will be created on your behalf:</span></span>
1. <span data-ttu-id="c3f5c-123">Groupe de ressources nommé : `cloud-shell-storage-<region>`</span><span class="sxs-lookup"><span data-stu-id="c3f5c-123">Resource Group named: `cloud-shell-storage-<region>`</span></span>
2. <span data-ttu-id="c3f5c-124">Compte de stockage nommé : `cs<uniqueGuid>`</span><span class="sxs-lookup"><span data-stu-id="c3f5c-124">Storage Account named: `cs<uniqueGuid>`</span></span>
3. <span data-ttu-id="c3f5c-125">Partage de fichiers nommé : `cs-<user>-<domain>-com-uniqueGuid`</span><span class="sxs-lookup"><span data-stu-id="c3f5c-125">File Share named: `cs-<user>-<domain>-com-uniqueGuid`</span></span>

> [!Note]
> <span data-ttu-id="c3f5c-126">Tous les fichiers figurant dans votre répertoire $Home, tels que les clés SSH, sont conservés dans l’image de disque utilisateur stockée dans votre partage de fichiers monté.</span><span class="sxs-lookup"><span data-stu-id="c3f5c-126">All files in your $Home directory such as SSH keys are persisted in your user disk image stored in your mounted file share.</span></span> <span data-ttu-id="c3f5c-127">Appliquez les meilleures pratiques lors de l’enregistrement des fichiers dans votre répertoire $Home et le partage de fichiers monté.</span><span class="sxs-lookup"><span data-stu-id="c3f5c-127">Apply best practices when saving files in your $Home directory and mounted file share.</span></span>

#### <a name="use-existing-resources"></a><span data-ttu-id="c3f5c-128">Utiliser les ressources existantes</span><span class="sxs-lookup"><span data-stu-id="c3f5c-128">Use existing resources</span></span>
![](media/advanced-storage.png)

<span data-ttu-id="c3f5c-129">Une option avancée est également autoriser vous tooassociate existant ressources tooCloud Shell.</span><span class="sxs-lookup"><span data-stu-id="c3f5c-129">An advanced option is also provided allowing you tooassociate existing resources tooCloud Shell.</span></span> <span data-ttu-id="c3f5c-130">Présenté avec l’invite de commandes d’installation de stockage hello, cliquez sur « Paramètres Show advanced » tooselect des options supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="c3f5c-130">When presented with hello storage setup prompt, click "Show advanced settings" tooselect additional options.</span></span> <span data-ttu-id="c3f5c-131">Les listes déroulantes sont filtrées pour la région Cloud Shell qui vous a été attribuée et pour les comptes de stockage localement/globalement redondant.</span><span class="sxs-lookup"><span data-stu-id="c3f5c-131">Dropdowns are filtered for your assigned Cloud Shell region and locally/globally-redundant storage accounts.</span></span>

<span data-ttu-id="c3f5c-132">[Découvrez le stockage Cloud Shell, la mise à jour des partages de fichiers et le chargement/téléchargement de fichiers.] (persisting-shell-storage.md)</span><span class="sxs-lookup"><span data-stu-id="c3f5c-132">[Learn about Cloud Shell storage, updating file shares, and uploading/downloading files.] (persisting-shell-storage.md)</span></span>

## <a name="concepts"></a><span data-ttu-id="c3f5c-133">Concepts</span><span class="sxs-lookup"><span data-stu-id="c3f5c-133">Concepts</span></span>
* <span data-ttu-id="c3f5c-134">Cloud Shell s’exécute sur une machine temporaire fournie par session et par utilisateur</span><span class="sxs-lookup"><span data-stu-id="c3f5c-134">Cloud Shell runs on a temporary machine provided on a per-session, per-user basis</span></span>
* <span data-ttu-id="c3f5c-135">Cloud Shell expire après 20 minutes sans activité interactive</span><span class="sxs-lookup"><span data-stu-id="c3f5c-135">Cloud Shell times out after 20 minutes without interactive activity</span></span>
* <span data-ttu-id="c3f5c-136">Cloud Shell est accessible uniquement avec un partage de fichiers attaché</span><span class="sxs-lookup"><span data-stu-id="c3f5c-136">Cloud Shell can only be accessed with a file share attached</span></span>
* <span data-ttu-id="c3f5c-137">Cloud Shell est affecté à une machine par compte d’utilisateur</span><span class="sxs-lookup"><span data-stu-id="c3f5c-137">Cloud Shell is assigned one machine per user account</span></span>
* <span data-ttu-id="c3f5c-138">Les autorisations sont définies en tant qu’utilisateur Linux standard</span><span class="sxs-lookup"><span data-stu-id="c3f5c-138">Permissions are set as a regular Linux user</span></span>

[<span data-ttu-id="c3f5c-139">Découvrez-en davantage sur toutes les fonctionnalités de Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="c3f5c-139">Learn more about all Cloud Shell features.</span></span>](features.md)

## <a name="examples"></a><span data-ttu-id="c3f5c-140">Exemples</span><span class="sxs-lookup"><span data-stu-id="c3f5c-140">Examples</span></span>
* <span data-ttu-id="c3f5c-141">Créer ou modifier des scripts tooautomate gestion Azure</span><span class="sxs-lookup"><span data-stu-id="c3f5c-141">Create or edit scripts tooautomate Azure management</span></span>
* <span data-ttu-id="c3f5c-142">Gérer simultanément des ressources via le portail Azure et Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="c3f5c-142">Simultaneously manage resources via Azure portal and Azure CLI 2.0</span></span>
* <span data-ttu-id="c3f5c-143">Essayer Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="c3f5c-143">Test-drive Azure CLI 2.0</span></span>

[<span data-ttu-id="c3f5c-144">Essayer tous ces exemples au démarrage rapide du Cloud Shell hello.</span><span class="sxs-lookup"><span data-stu-id="c3f5c-144">Try out all these examples at hello Cloud Shell quickstart.</span></span>](quickstart.md)

## <a name="pricing"></a><span data-ttu-id="c3f5c-145">Tarification</span><span class="sxs-lookup"><span data-stu-id="c3f5c-145">Pricing</span></span>
<span data-ttu-id="c3f5c-146">ordinateur Hello Shell de Cloud d’hébergement est libre, avec un composant requis d’un fichier Azure monté partager toopersist votre répertoire $Home.</span><span class="sxs-lookup"><span data-stu-id="c3f5c-146">hello machine hosting Cloud Shell is free, with a pre-requisite of a mounted Azure file share toopersist your $Home directory.</span></span> <span data-ttu-id="c3f5c-147">Les coûts de stockage standard s’appliquent.</span><span class="sxs-lookup"><span data-stu-id="c3f5c-147">Regular storage costs apply.</span></span>

## <a name="supported-browsers"></a><span data-ttu-id="c3f5c-148">Navigateurs pris en charge</span><span class="sxs-lookup"><span data-stu-id="c3f5c-148">Supported browsers</span></span>
<span data-ttu-id="c3f5c-149">Cloud Shell est recommandé pour Chrome, Safari et Edge.</span><span class="sxs-lookup"><span data-stu-id="c3f5c-149">Cloud Shell is recommended for Chrome, Edge, and Safari.</span></span> <span data-ttu-id="c3f5c-150">Interface de Cloud est pris en charge de Chrome, Firefox, Safari, Internet Explorer et session, interpréteur de commandes de Cloud est paramètres du navigateur toospecific sujet.</span><span class="sxs-lookup"><span data-stu-id="c3f5c-150">While Cloud Shell is supported for Chrome, Firefox, Safari, IE, and Edge, Cloud Shell is subject toospecific browser settings.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="c3f5c-151">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="c3f5c-151">Troubleshooting</span></span>
1. <span data-ttu-id="c3f5c-152">Lorsque vous utilisez un abonnement Azure Active Directory, je ne peux pas créer de stockage tooError échéance : DisallowedOperation 400.</span><span class="sxs-lookup"><span data-stu-id="c3f5c-152">When using an Azure Active Directory subscription, I cannot create storage due tooError: 400 DisallowedOperation.</span></span> <span data-ttu-id="c3f5c-153">tooresolve, veuillez utiliser un abonnement Azure capable de créer des ressources de stockage.</span><span class="sxs-lookup"><span data-stu-id="c3f5c-153">tooresolve this, please use an Azure subscription capable of creating storage resources.</span></span> <span data-ttu-id="c3f5c-154">Les abonnements AD est des ressources Azure n’a pas pu toocreate.</span><span class="sxs-lookup"><span data-stu-id="c3f5c-154">AD subscriptions are not able toocreate Azure resources.</span></span>

<span data-ttu-id="c3f5c-155">Pour connaître les limitations spécifiques connues, consultez les [limitations de Cloud Shell](limitations.md).</span><span class="sxs-lookup"><span data-stu-id="c3f5c-155">For specific known limitations, visit [limitations of Cloud Shell](limitations.md).</span></span>
