---
title: Azure Disk Encryption pour les machines virtuelles IaaS Windows et Linux | Microsoft Docs
description: "Cet article offre une vue d’ensemble de Microsoft Azure Disk Encryption pour les machines virtuelles IaaS Windows et Linux."
services: security
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: TomSh
ms.assetid: d3fac8bb-4829-405e-8701-fa7229fb1725
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/07/2017
ms.author: kakhan
ms.openlocfilehash: a4f20fc19ae40561d042d5cff744a030014f75c7
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-disk-encryption-for-windows-and-linux-iaas-vms"></a><span data-ttu-id="89e6a-103">Chiffrement de disque Azure pour des machines virtuelles Windows et Linux IaaS</span><span class="sxs-lookup"><span data-stu-id="89e6a-103">Azure Disk Encryption for Windows and Linux IaaS VMs</span></span>
<span data-ttu-id="89e6a-104">Microsoft Azure s’engage fermement à préserver la confidentialité, la souveraineté de vos données et vous permet de contrôler vos données Azure hébergées via une suite de technologies servant à chiffrer, contrôler et gérer les clés de chiffrement, le contrôle et l’audit de l’accès aux données.</span><span class="sxs-lookup"><span data-stu-id="89e6a-104">Microsoft Azure is strongly committed to ensuring your data privacy, data sovereignty and enables you to control your Azure hosted data through a range of advanced technologies to encrypt, control and manage encryption keys, control & audit access of data.</span></span> <span data-ttu-id="89e6a-105">Les clients Azure ont ainsi la possibilité de choisir la solution qui répond le mieux à leurs besoins professionnels.</span><span class="sxs-lookup"><span data-stu-id="89e6a-105">This provides Azure customers the flexibility to choose the solution that best meets their business needs.</span></span> <span data-ttu-id="89e6a-106">Dans ce document, nous allons vous présenter une nouvelle solution technologique « Azure Disk Encryption for Windows and Linux IaaS VM’s » pour protéger et sauvegarder vos données afin de répondre aux engagements de votre sécurité en matière d’organisation et les exigences de conformité.</span><span class="sxs-lookup"><span data-stu-id="89e6a-106">In this paper, we will introduce you to a new technology solution “Azure Disk Encryption for Windows and Linux IaaS VM’s” to help protect and safeguard your data to meet your organizational security and compliance commitments.</span></span> <span data-ttu-id="89e6a-107">Cet article fournit des instructions détaillées sur la façon d’utiliser les fonctionnalités de cryptage de disque Azure, notamment sur les scénarios pris en charge et sur les expériences utilisateur.</span><span class="sxs-lookup"><span data-stu-id="89e6a-107">The paper provides detailed guidance on how to use the Azure disk encryption features including the supported scenarios and the user experiences.</span></span>

> [!NOTE]
> <span data-ttu-id="89e6a-108">Certaines recommandations peuvent entraîner une augmentation de l’utilisation des données, des réseaux ou des ressources de calcul débouchant sur des coûts de licence ou d’abonnement supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="89e6a-108">Certain recommendations might increase data, network, or compute resource usage, resulting in additional license or subscription costs.</span></span>

## <a name="overview"></a><span data-ttu-id="89e6a-109">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="89e6a-109">Overview</span></span>
<span data-ttu-id="89e6a-110">Azure Disk Encryption est une nouvelle fonctionnalité qui vous permet de chiffrer vos disques de machine virtuelle IaaS Windows et Linux.</span><span class="sxs-lookup"><span data-stu-id="89e6a-110">Azure Disk Encryption is a new capability that helps you encrypt your Windows and Linux IaaS virtual machine disks.</span></span> <span data-ttu-id="89e6a-111">Azure Disk Encryption s’appuie sur la fonctionnalité standard [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) de Windows et la fonctionnalité [DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) de Linux afin de fournir le chiffrement de volume pour le système d’exploitation et les disques de données.</span><span class="sxs-lookup"><span data-stu-id="89e6a-111">Azure Disk Encryption leverages the industry standard [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) feature of Windows and the [DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) feature of Linux to provide volume encryption for the OS and the data disks.</span></span> <span data-ttu-id="89e6a-112">La solution est intégrée avec [Azure Key Vault](https://azure.microsoft.com/documentation/services/key-vault/), ce qui vous permet de contrôler et de gérer les clés et clés secrètes de chiffrement de disque dans votre abonnement Key Vault.</span><span class="sxs-lookup"><span data-stu-id="89e6a-112">The solution is integrated with [Azure Key Vault](https://azure.microsoft.com/documentation/services/key-vault/) to help you control and manage the disk-encryption keys and secrets in your key vault subscription.</span></span> <span data-ttu-id="89e6a-113">Elle garantit également que toutes les données sur les disques de vos machines virtuelles sont chiffrées au repos dans votre stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="89e6a-113">The solution also ensures that all data on the virtual machine disks are encrypted at rest in your Azure storage.</span></span>

<span data-ttu-id="89e6a-114">Azure Disk Encryption pour les machines virtuelles Iaas Windows et Linux est désormais à la **disponibilité générale** dans toutes les régions publiques Azure et les régions AzureGov pour les machines virtuelles standard et les machines virtuelles avec Stockage Premium.</span><span class="sxs-lookup"><span data-stu-id="89e6a-114">Azure disk encryption for Windows and Linux IaaS VMs is now in **General Availability** in all Azure public regions and AzureGov regions for Standard  VMs and VMs with premium storage.</span></span>

### <a name="encryption-scenarios"></a><span data-ttu-id="89e6a-115">Scénarios de chiffrement</span><span class="sxs-lookup"><span data-stu-id="89e6a-115">Encryption scenarios</span></span>
<span data-ttu-id="89e6a-116">Azure Disk Encryption prend en charge les scénarios client suivants :</span><span class="sxs-lookup"><span data-stu-id="89e6a-116">The Azure Disk Encryption solution supports the following customer scenarios:</span></span>

* <span data-ttu-id="89e6a-117">Activation du chiffrement sur de nouvelles machines virtuelles IaaS créées à partir de disques durs virtuels déjà chiffrés et de clés de chiffrement</span><span class="sxs-lookup"><span data-stu-id="89e6a-117">Enable encryption on new IaaS VMs created from pre-encrypted VHD and encryption keys</span></span>
* <span data-ttu-id="89e6a-118">Activation du chiffrement sur de nouvelles machines virtuelles IaaS créées à partir d’images de la galerie Azure prises en charge</span><span class="sxs-lookup"><span data-stu-id="89e6a-118">Enable encryption on new IaaS VMs created from the supported Azure Gallery images</span></span>
* <span data-ttu-id="89e6a-119">Activation du chiffrement sur des machines virtuelles IaaS existantes et fonctionnant dans Azure</span><span class="sxs-lookup"><span data-stu-id="89e6a-119">Enable encryption on existing IaaS VMs running in Azure</span></span>
* <span data-ttu-id="89e6a-120">Désactivation du chiffrement sur les machines virtuelles IaaS Windows.</span><span class="sxs-lookup"><span data-stu-id="89e6a-120">Disable encryption on Windows IaaS VMs</span></span>
* <span data-ttu-id="89e6a-121">Désactivation du chiffrement sur les lecteurs de données pour les machines virtuelles IaaS Linux</span><span class="sxs-lookup"><span data-stu-id="89e6a-121">Disable encryption on data drives for Linux IaaS VMs</span></span>
* <span data-ttu-id="89e6a-122">Activation du chiffrement des machines virtuelles avec disque managé</span><span class="sxs-lookup"><span data-stu-id="89e6a-122">Enable encryption of managed disk VMs</span></span>
* <span data-ttu-id="89e6a-123">Mise à jour des paramètres de chiffrement d’une machine virtuelle de stockage non Premium chiffrée existante</span><span class="sxs-lookup"><span data-stu-id="89e6a-123">Update encryption settings of an existing encrypted non-premium storage VM</span></span>
* <span data-ttu-id="89e6a-124">Sauvegarde et restauration de machines virtuelles chiffrées avec une clé de chiffrement de clé</span><span class="sxs-lookup"><span data-stu-id="89e6a-124">Backup and restore of encrypted VMs, encrypted with key encryption key</span></span>

<span data-ttu-id="89e6a-125">La solution prend en charge les scénarios de machines virtuelles IaaS suivants lorsqu’ils sont activés dans Microsoft Azure :</span><span class="sxs-lookup"><span data-stu-id="89e6a-125">The solution supports the following scenarios for IaaS VMs when they are enabled in Microsoft Azure:</span></span>

* <span data-ttu-id="89e6a-126">Prise en main d’Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="89e6a-126">Integration with Azure Key Vault</span></span>
* <span data-ttu-id="89e6a-127">Machines virtuelles de niveau standard : [Machines virtuelles IaaS des séries A, D, DS, G, GS, F, etc.](https://azure.microsoft.com/pricing/details/virtual-machines/)</span><span class="sxs-lookup"><span data-stu-id="89e6a-127">Standard tier VMs: [A, D, DS, G, GS, F, and so forth series IaaS VMs](https://azure.microsoft.com/pricing/details/virtual-machines/)</span></span>
* <span data-ttu-id="89e6a-128">Activation du chiffrement sur les machines virtuelles IaaS Windows et Linux et les machines virtuelles de disques gérés créées à partir d’images de la galerie Azure prises en charge</span><span class="sxs-lookup"><span data-stu-id="89e6a-128">Enable encryption on Windows and Linux IaaS VMs and managed disk VMs from the supported Azure Gallery images</span></span>
* <span data-ttu-id="89e6a-129">Désactivation du chiffrement des lecteurs de système d’exploitation et de données pour des machines virtuelles IaaS Windows et des machines virtuelles avec disque managé</span><span class="sxs-lookup"><span data-stu-id="89e6a-129">Disable encryption on OS and data drives for Windows IaaS VMs and managed disk VMs</span></span>
* <span data-ttu-id="89e6a-130">Désactivation du chiffrement des lecteurs de données pour des machines virtuelles IaaS Linux et des machines virtuelles avec disque managé</span><span class="sxs-lookup"><span data-stu-id="89e6a-130">Disable encryption on data drives for Linux IaaS VMs and managed disk VMs</span></span>
* <span data-ttu-id="89e6a-131">Activation du chiffrement sur les machines virtuelles IaaS exécutant le système d’exploitation du client Windows.</span><span class="sxs-lookup"><span data-stu-id="89e6a-131">Enable encryption on IaaS VMs running Windows Client OS</span></span>
* <span data-ttu-id="89e6a-132">Activation du chiffrement sur les volumes avec chemins d’accès de montage.</span><span class="sxs-lookup"><span data-stu-id="89e6a-132">Enable encryption on volumes with mount paths</span></span>
* <span data-ttu-id="89e6a-133">Activation du chiffrement sur des machines virtuelles Linux configurées avec une agrégation de disques (RAID) utilisant mdadm</span><span class="sxs-lookup"><span data-stu-id="89e6a-133">Enable encryption on Linux VMs configured with disk striping (RAID) using mdadm</span></span>
* <span data-ttu-id="89e6a-134">Activation du chiffrement sur des machines virtuelles Linux en utilisant LVM pour les disques de données</span><span class="sxs-lookup"><span data-stu-id="89e6a-134">Enable encryption on Linux VMs using LVM for data disks</span></span>
* <span data-ttu-id="89e6a-135">Activation du chiffrement sur les machines virtuelles Windows configurées avec des espaces de stockage</span><span class="sxs-lookup"><span data-stu-id="89e6a-135">Enable encryption on Windows VMs configured with Storage Spaces</span></span>
* <span data-ttu-id="89e6a-136">Mise à jour des paramètres de chiffrement d’une machine virtuelle de stockage non Premium chiffrée existante</span><span class="sxs-lookup"><span data-stu-id="89e6a-136">Update encryption settings of an existing encrypted non-premium storage VM</span></span>
* <span data-ttu-id="89e6a-137">Toutes les régions publiques Azure et AzureGov sont prises en charge</span><span class="sxs-lookup"><span data-stu-id="89e6a-137">All Azure Public and AzureGov regions are supported</span></span>

<span data-ttu-id="89e6a-138">La solution ne prend pas en charge les scénarios, fonctionnalités et technologies suivants :</span><span class="sxs-lookup"><span data-stu-id="89e6a-138">The solution does not support the following scenarios, features, and technology:</span></span>

* <span data-ttu-id="89e6a-139">Machines virtuelles IaaS de niveau de base</span><span class="sxs-lookup"><span data-stu-id="89e6a-139">Basic tier IaaS VMs</span></span>
* <span data-ttu-id="89e6a-140">Désactivation du chiffrement sur un lecteur de système d’exploitation pour les machines virtuelles IaaS Linux</span><span class="sxs-lookup"><span data-stu-id="89e6a-140">Disabling encryption on an OS drive for Linux IaaS VMs</span></span>
* <span data-ttu-id="89e6a-141">Désactivation du chiffrement sur un lecteur de données lorsque le lecteur du système d’exploitation est chiffré pour les machines virtuelles Iaas Linux</span><span class="sxs-lookup"><span data-stu-id="89e6a-141">Disabling encryption on a data drive if the OS drive is encrypted for Linux Iaas VMs</span></span>
* <span data-ttu-id="89e6a-142">Machines virtuelles IaaS créées à l’aide de la méthode classique de création de machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="89e6a-142">IaaS VMs that are created by using the classic VM creation method</span></span>
* <span data-ttu-id="89e6a-143">L’activation du chiffrement sur les images client personnalisées de machines virtuelles Iaas Windows et Linux n’est PAS prise en charge.</span><span class="sxs-lookup"><span data-stu-id="89e6a-143">Enable encryption on Windows and Linux IaaS VMs customer custom images is NOT supported.</span></span> <span data-ttu-id="89e6a-144">L’activation du chiffrement sur des disques de système d’exploitation LVM Linux n’est pas prise en charge actuellement.</span><span class="sxs-lookup"><span data-stu-id="89e6a-144">Enable enccryption on Linux LVM OS disk is not supported currently.</span></span> <span data-ttu-id="89e6a-145">Elles seront bientôt prise en charge.</span><span class="sxs-lookup"><span data-stu-id="89e6a-145">This support will come soon.</span></span>
* <span data-ttu-id="89e6a-146">Intégration à votre service de gestion de clés local</span><span class="sxs-lookup"><span data-stu-id="89e6a-146">Integration with your on-premises Key Management Service</span></span>
* <span data-ttu-id="89e6a-147">Azure Files (système de partage de fichiers), NFS (Network File System), volumes dynamiques et machines virtuelles Windows configurées avec des systèmes RAID logiciels</span><span class="sxs-lookup"><span data-stu-id="89e6a-147">Azure Files (shared file system), Network File System (NFS), dynamic volumes, and Windows VMs that are configured with software-based RAID systems</span></span>
* <span data-ttu-id="89e6a-148">Sauvegarde et restauration de machines virtuelles chiffrées sans clé de chiffrement de clé</span><span class="sxs-lookup"><span data-stu-id="89e6a-148">Backup and restore of encrypted VMs, encrypted without key encryption key.</span></span>
* <span data-ttu-id="89e6a-149">Mise à jour des paramètres de chiffrement d’une machine virtuelle de stockage Premium chiffrée existante</span><span class="sxs-lookup"><span data-stu-id="89e6a-149">Update encryption settings of an existing encrypted premium storage VM.</span></span>

> [!NOTE]
> <span data-ttu-id="89e6a-150">La sauvegarde et la restauration de machines virtuelles chiffrées sont prises en charge uniquement pour les machines virtuelles chiffrées à l’aide de la configuration de clé de chiffrement à clé (KEK).</span><span class="sxs-lookup"><span data-stu-id="89e6a-150">Backup and restore of encrypted VMs is supported only for VMs that are encrypted with the KEK configuration.</span></span> <span data-ttu-id="89e6a-151">Elles ne sont pas prises en charge pour les machines virtuelles chiffrées sans KEK.</span><span class="sxs-lookup"><span data-stu-id="89e6a-151">It is not supported on VMs that are encrypted without KEK.</span></span> <span data-ttu-id="89e6a-152">KEK est un paramètre facultatif permettant d’activer le chiffrement d’une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="89e6a-152">KEK is an optional parameter that enables VM encryption.</span></span> <span data-ttu-id="89e6a-153">Cette prise en charge sera bientôt disponible.</span><span class="sxs-lookup"><span data-stu-id="89e6a-153">This support is coming soon.</span></span>
> <span data-ttu-id="89e6a-154">La mise à jour des paramètres de chiffrement d’une machine virtuelle de stockage Premium chiffrée ne sont pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="89e6a-154">Update encryption settings of an existing encrypted premium storage VM are not supported.</span></span> <span data-ttu-id="89e6a-155">Cette prise en charge sera bientôt disponible.</span><span class="sxs-lookup"><span data-stu-id="89e6a-155">This support is coming soon.</span></span>

### <a name="encryption-features"></a><span data-ttu-id="89e6a-156">Fonctionnalités de chiffrement</span><span class="sxs-lookup"><span data-stu-id="89e6a-156">Encryption features</span></span>
<span data-ttu-id="89e6a-157">Lorsque vous activez et déployez Azure Disk Encryption pour les machines virtuelles IaaS Azure, les fonctionnalités suivantes sont activées en fonction de la configuration fournie :</span><span class="sxs-lookup"><span data-stu-id="89e6a-157">When you enable and deploy Azure Disk Encryption for Azure IaaS VMs, the following capabilities are enabled, depending on the configuration provided:</span></span>

* <span data-ttu-id="89e6a-158">Chiffrement du volume du système d’exploitation pour protéger le volume de démarrage au repos dans votre espace de stockage</span><span class="sxs-lookup"><span data-stu-id="89e6a-158">Encryption of the OS volume to protect the boot volume at rest in your storage</span></span>
* <span data-ttu-id="89e6a-159">Chiffrement des volumes de données pour protéger les volumes de données au repos dans votre espace de stockage</span><span class="sxs-lookup"><span data-stu-id="89e6a-159">Encryption of data volumes to protect the data volumes at rest in your storage</span></span>
* <span data-ttu-id="89e6a-160">Désactivation du chiffrement sur les systèmes d’exploitation et les lecteurs de données pour les machines virtuelles IaaS Windows</span><span class="sxs-lookup"><span data-stu-id="89e6a-160">Disabling encryption on the OS and data drives for Windows IaaS VMs</span></span>
* <span data-ttu-id="89e6a-161">Désactivation du chiffrement sur les lecteurs de données pour les machines virtuelles IaaS Linux (à condition que le lecteur de système d’exploitation NE SOIT PAS chiffré)</span><span class="sxs-lookup"><span data-stu-id="89e6a-161">Disabling encryption on the data drives for Linux IaaS VMs (only if OS drive IS NOT encrypted)</span></span>
* <span data-ttu-id="89e6a-162">Sauvegarde des clés et clés secrètes de chiffrement dans votre abonnement Key Vault</span><span class="sxs-lookup"><span data-stu-id="89e6a-162">Safeguarding the encryption keys and secrets in your key vault subscription</span></span>
* <span data-ttu-id="89e6a-163">Création de rapports concernant l’état du chiffrement des machines virtuelles IaaS chiffrées</span><span class="sxs-lookup"><span data-stu-id="89e6a-163">Reporting the encryption status of the encrypted IaaS VM</span></span>
* <span data-ttu-id="89e6a-164">Suppression des paramètres de configuration de chiffrement de disque à partir de la machine virtuelle IaaS</span><span class="sxs-lookup"><span data-stu-id="89e6a-164">Removal of disk-encryption configuration settings from the IaaS virtual machine</span></span>
* <span data-ttu-id="89e6a-165">Sauvegarde et restauration des machines virtuelles chiffrées à l’aide du service Sauvegarde Azure</span><span class="sxs-lookup"><span data-stu-id="89e6a-165">Backup and restore of encrypted VMs by using the Azure Backup service</span></span>

> [!NOTE]
> <span data-ttu-id="89e6a-166">La sauvegarde et la restauration de machines virtuelles chiffrées sont prises en charge uniquement pour les machines virtuelles chiffrées à l’aide de la configuration de clé de chiffrement à clé (KEK).</span><span class="sxs-lookup"><span data-stu-id="89e6a-166">Backup and restore of encrypted VMs is supported only for VMs that are encrypted with the KEK configuration.</span></span> <span data-ttu-id="89e6a-167">Elles ne sont pas prises en charge pour les machines virtuelles chiffrées sans KEK.</span><span class="sxs-lookup"><span data-stu-id="89e6a-167">It is not supported on VMs that are encrypted without KEK.</span></span> <span data-ttu-id="89e6a-168">KEK est un paramètre facultatif permettant d’activer le chiffrement d’une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="89e6a-168">KEK is an optional parameter that enables VM encryption.</span></span>

<span data-ttu-id="89e6a-169">La solution Azure Disk Encryption pour les machines virtuelles IaaS Windows et Linux comprend :</span><span class="sxs-lookup"><span data-stu-id="89e6a-169">Azure Disk Encryption for IaaS VMS for Windows and Linux solution includes:</span></span>

* <span data-ttu-id="89e6a-170">L’extension de chiffrement de disque pour Windows.</span><span class="sxs-lookup"><span data-stu-id="89e6a-170">The disk-encryption extension for Windows.</span></span>
* <span data-ttu-id="89e6a-171">L’extension de chiffrement de disque pour Linux.</span><span class="sxs-lookup"><span data-stu-id="89e6a-171">The disk-encryption extension for Linux.</span></span>
* <span data-ttu-id="89e6a-172">Les applets de commande PowerShell pour le chiffrement de disque.</span><span class="sxs-lookup"><span data-stu-id="89e6a-172">The disk-encryption PowerShell cmdlets.</span></span>
* <span data-ttu-id="89e6a-173">Les applets de commande de l’interface de ligne de commande Azure pour le chiffrement de disque.</span><span class="sxs-lookup"><span data-stu-id="89e6a-173">The disk-encryption Azure command-line interface (CLI) cmdlets.</span></span>
* <span data-ttu-id="89e6a-174">Les modèles Azure Resource Manager pour le chiffrement de disque.</span><span class="sxs-lookup"><span data-stu-id="89e6a-174">The disk-encryption Azure Resource Manager templates.</span></span>

<span data-ttu-id="89e6a-175">La solution Azure Disk Encryption est prise en charge sur les machines virtuelles IaaS exécutant les systèmes d’exploitation Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="89e6a-175">The Azure Disk Encryption solution is supported on IaaS VMs that are running Windows or Linux OS.</span></span> <span data-ttu-id="89e6a-176">Pour plus d’informations sur les systèmes d’exploitation pris en charge, consultez la section « Conditions préalables ».</span><span class="sxs-lookup"><span data-stu-id="89e6a-176">For more information about the supported operating systems, see the "Prerequisites" section.</span></span>

> [!NOTE]
> <span data-ttu-id="89e6a-177">Le chiffrement des disques de machine virtuelle avec Azure Disk Encryption est gratuit.</span><span class="sxs-lookup"><span data-stu-id="89e6a-177">There is no additional charge for encrypting VM disks with Azure Disk Encryption.</span></span>

### <a name="value-proposition"></a><span data-ttu-id="89e6a-178">Proposition de valeur</span><span class="sxs-lookup"><span data-stu-id="89e6a-178">Value proposition</span></span>
<span data-ttu-id="89e6a-179">La solution de gestion Azure Disk Encryption répond aux besoins professionnels suivants :</span><span class="sxs-lookup"><span data-stu-id="89e6a-179">When you apply the Azure Disk Encryption-management solution, you can satisfy the following business needs:</span></span>

* <span data-ttu-id="89e6a-180">Les machines virtuelles IaaS sont sécurisées au repos par le biais d’une technologie de chiffrement standard permettant de répondre aux exigences de sécurité organisationnelle et de conformité.</span><span class="sxs-lookup"><span data-stu-id="89e6a-180">IaaS VMs are secured at rest, because you can use industry-standard encryption technology to address organizational security and compliance requirements.</span></span>
* <span data-ttu-id="89e6a-181">Les machines virtuelles IaaS démarrent par le biais de stratégies et de clés contrôlées par les clients qui peuvent auditer leur utilisation dans le coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="89e6a-181">IaaS VMs boot under customer-controlled keys and policies, and you can audit their usage in your key vault.</span></span>

### <a name="encryption-workflow"></a><span data-ttu-id="89e6a-182">Workflow de chiffrement</span><span class="sxs-lookup"><span data-stu-id="89e6a-182">Encryption workflow</span></span>
<span data-ttu-id="89e6a-183">Pour activer le chiffrement de disque pour les machines virtuelles Windows et Linux, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="89e6a-183">To enable disk encryption for Windows and Linux VMs, do the following:</span></span>

1. <span data-ttu-id="89e6a-184">Choisissez un scénario de chiffrement parmi les scénarios de chiffrement précédents.</span><span class="sxs-lookup"><span data-stu-id="89e6a-184">Choose an encryption scenario from among the preceding encryption scenarios.</span></span>
2. <span data-ttu-id="89e6a-185">Optez pour l’activation du chiffrement de disque via le modèle Resource Manager de chiffrement de disque Azure, les applets de commande PowerShell ou les commandes CLI et spécifiez la configuration de chiffrement.</span><span class="sxs-lookup"><span data-stu-id="89e6a-185">Opt in to enabling disk encryption via the Azure Disk Encryption Resource Manager template, PowerShell cmdlets, or CLI command, and specify the encryption configuration.</span></span>

   * <span data-ttu-id="89e6a-186">Pour le scénario de disque dur virtuel chiffré par le client, téléchargez le disque dur virtuel chiffré dans votre compte de stockage et le support de clé de chiffrement dans votre coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="89e6a-186">For the customer-encrypted VHD scenario, upload the encrypted VHD to your storage account and the encryption key material to your key vault.</span></span> <span data-ttu-id="89e6a-187">Ensuite, fournissez la configuration de chiffrement pour activer le chiffrement sur une nouvelle machine virtuelle IaaS.</span><span class="sxs-lookup"><span data-stu-id="89e6a-187">Then, provide the encryption configuration to enable encryption on a new IaaS VM.</span></span>
   * <span data-ttu-id="89e6a-188">Pour les nouvelles machines virtuelles créées à partir de la Place de marché Azure et les machines virtuelles existantes en cours d’exécution dans Azure, fournissez la configuration de chiffrement pour activer le chiffrement sur la machine virtuelle IaaS.</span><span class="sxs-lookup"><span data-stu-id="89e6a-188">For new VMs that are created from the Marketplace and existing VMs that are already running in Azure, provide the encryption configuration to enable encryption on the IaaS VM.</span></span>

3. <span data-ttu-id="89e6a-189">Accordez l’accès à la plateforme Azure pour lire le support de clé de chiffrement (systèmes de clés de chiffrement BitLocker pour les systèmes Windows et phrase secrète pour Linux) du coffre de clés et activez le chiffrement sur la machine virtuelle IaaS.</span><span class="sxs-lookup"><span data-stu-id="89e6a-189">Grant access to the Azure platform to read the encryption-key material (BitLocker encryption keys for Windows systems and Passphrase for Linux) from your key vault to enable encryption on the IaaS VM.</span></span>

4. <span data-ttu-id="89e6a-190">Fournissez l’identité d’application Azure Active Directory (Azure AD) pour écrire le support de clé de chiffrement dans votre coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="89e6a-190">Provide the Azure Active Directory (Azure AD) application identity to write the encryption key material to your key vault.</span></span> <span data-ttu-id="89e6a-191">Cette opération active le chiffrement sur la machine virtuelle IaaS pour les scénarios mentionnés à l’étape 2.</span><span class="sxs-lookup"><span data-stu-id="89e6a-191">Doing so enables encryption on the IaaS VM for the scenarios mentioned in step 2.</span></span>

5. <span data-ttu-id="89e6a-192">Azure met à jour le modèle de service de machine virtuelle avec chiffrement et la configuration de coffre de clés, et configure vos machines virtuelles chiffrées.</span><span class="sxs-lookup"><span data-stu-id="89e6a-192">Azure updates the VM service model with encryption and the key vault configuration, and sets up your encrypted VM.</span></span>

 ![Microsoft Antimalware dans Azure](./media/azure-security-disk-encryption/disk-encryption-fig1.png)

### <a name="decryption-workflow"></a><span data-ttu-id="89e6a-194">Workflow de déchiffrement</span><span class="sxs-lookup"><span data-stu-id="89e6a-194">Decryption workflow</span></span>
<span data-ttu-id="89e6a-195">Pour désactiver le chiffrement de disque pour les machines virtuelles IaaS, suivez les étapes de haut niveau suivantes :</span><span class="sxs-lookup"><span data-stu-id="89e6a-195">To disable disk encryption for IaaS VMs, complete the following high-level steps:</span></span>

1. <span data-ttu-id="89e6a-196">Choisissez de désactiver le chiffrement (déchiffrement) sur une machine virtuelle IaaS en cours d’exécution dans Azure via le modèle Resource Manager Azure Disk Encryption ou via les applets de commande PowerShell, puis spécifiez la configuration de déchiffrement.</span><span class="sxs-lookup"><span data-stu-id="89e6a-196">Choose to disable encryption (decryption) on a running IaaS VM in Azure via the Azure Disk Encryption Resource Manager template or PowerShell cmdlets, and specify the decryption configuration.</span></span>

 <span data-ttu-id="89e6a-197">Cette étape désactive le chiffrement du volume de système d’exploitation ou du volume de données (ou les deux) sur la machine virtuelle IaaS Windows en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="89e6a-197">This step disables encryption of the OS or the data volume or both on the running Windows IaaS VM.</span></span> <span data-ttu-id="89e6a-198">Toutefois, comme mentionné dans la section précédente, la désactivation du chiffrement du disque de système d’exploitation pour Linux n’est pas prise en charge.</span><span class="sxs-lookup"><span data-stu-id="89e6a-198">However, as mentioned in the previous section, disabling OS disk encryption for Linux is not supported.</span></span> <span data-ttu-id="89e6a-199">L’étape de déchiffrement est autorisée uniquement pour les lecteurs de données sur les machines virtuelles Linux tant que le disque du système d’exploitation n’est pas chiffré.</span><span class="sxs-lookup"><span data-stu-id="89e6a-199">The decryption step is allowed only for data drives on Linux VMs as long as the OS disk is not encrypted.</span></span>
2. <span data-ttu-id="89e6a-200">Azure met à jour le modèle de service de machine virtuelle et la machine virtuelle Iaas est marquée comme déchiffrée.</span><span class="sxs-lookup"><span data-stu-id="89e6a-200">Azure updates the VM service model, and the IaaS VM is marked decrypted.</span></span> <span data-ttu-id="89e6a-201">Le contenu de la machine virtuelle n’est plus chiffré au repos.</span><span class="sxs-lookup"><span data-stu-id="89e6a-201">The contents of the VM are no longer encrypted at rest.</span></span>

> [!NOTE]
> <span data-ttu-id="89e6a-202">La désactivation du chiffrement ne supprime ni votre coffre de clés ni le support de clé de chiffrement (clés de chiffrement BitLocker pour Windows ou phrase secrète pour Linux).</span><span class="sxs-lookup"><span data-stu-id="89e6a-202">The disable-encryption operation does not delete your key vault and the encryption key material (BitLocker encryption keys for Windows systems or Passphrase for Linux).</span></span>
 > <span data-ttu-id="89e6a-203">La désactivation du chiffrement de disque de système d’exploitation pour Linux n’est pas prise en charge.</span><span class="sxs-lookup"><span data-stu-id="89e6a-203">Disabling OS disk encryption for Linux is not supported.</span></span> <span data-ttu-id="89e6a-204">L’étape de déchiffrement est autorisée uniquement pour les lecteurs de données sur les machines virtuelles Linux.</span><span class="sxs-lookup"><span data-stu-id="89e6a-204">The decryption step is allowed only for data drives on Linux VMs.</span></span>
<span data-ttu-id="89e6a-205">La désactivation du chiffrement des disques de données pour Linux n’est pas prise en charge si le lecteur de système d’exploitation est chiffré.</span><span class="sxs-lookup"><span data-stu-id="89e6a-205">Disabling data disk encryption for Linux is not supported if the OS drive is encrypted.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="89e6a-206">Composants requis</span><span class="sxs-lookup"><span data-stu-id="89e6a-206">Prerequisites</span></span>
<span data-ttu-id="89e6a-207">Voici les conditions requises pour activer Azure Disk Encryption sur les machines virtuelles IaaS Azure pour les scénarios pris en charge dans la section « Vue d’ensemble » :</span><span class="sxs-lookup"><span data-stu-id="89e6a-207">Before you enable Azure Disk Encryption on Azure IaaS VMs for the supported scenarios that were discussed in the "Overview" section, see the following prerequisites:</span></span>

* <span data-ttu-id="89e6a-208">Vous devez disposer d’un abonnement Azure actif valide pour créer des ressources dans Azure dans les régions prises en charge.</span><span class="sxs-lookup"><span data-stu-id="89e6a-208">You must have a valid active Azure subscription to create resources in Azure in the supported regions.</span></span>
* <span data-ttu-id="89e6a-209">Azure Disk Encryption est pris en charge sur les versions Windows Server suivantes : Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2 et Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="89e6a-209">Azure Disk Encryption is supported on the following Windows Server versions: Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2, and Windows Server 2016.</span></span>
* <span data-ttu-id="89e6a-210">Azure Disk Encryption est pris en charge sur les clients Windows suivants : client Windows 8 et client Windows 10.</span><span class="sxs-lookup"><span data-stu-id="89e6a-210">Azure Disk Encryption is supported on the following Windows client versions: Windows 8 client and Windows 10 client.</span></span>

> [!NOTE]
> <span data-ttu-id="89e6a-211">Pour Windows Server 2008 R2, .NET Framework 4.5 doit être installé avant l’activation du chiffrement dans Azure.</span><span class="sxs-lookup"><span data-stu-id="89e6a-211">For Windows Server 2008 R2, you must have .NET Framework 4.5 installed before you enable encryption in Azure.</span></span> <span data-ttu-id="89e6a-212">Vous pouvez l’installer à partir de Windows Update en installant la mise à jour facultative Microsoft .NET Framework 4.5.2 pour systèmes Windows Server 2008 R2 x64 ([KB2901983](https://support.microsoft.com/kb/2901983)).</span><span class="sxs-lookup"><span data-stu-id="89e6a-212">You can install it from Windows Update by installing the optional update Microsoft .NET Framework 4.5.2 for Windows Server 2008 R2 x64-based systems ([KB2901983](https://support.microsoft.com/kb/2901983)).</span></span>

* <span data-ttu-id="89e6a-213">Azure Disk Encryption est pris en charge sur les versions et distributions de serveur Linux basées sur la Galerie Azure suivantes :</span><span class="sxs-lookup"><span data-stu-id="89e6a-213">Azure Disk Encryption is supported on the following Azure Gallery based Linux server distributions and versions:</span></span>

| <span data-ttu-id="89e6a-214">Distribution Linux</span><span class="sxs-lookup"><span data-stu-id="89e6a-214">Linux Distribution</span></span> | <span data-ttu-id="89e6a-215">Version</span><span class="sxs-lookup"><span data-stu-id="89e6a-215">Version</span></span> | <span data-ttu-id="89e6a-216">Type de volume pris en charge pour le chiffrement</span><span class="sxs-lookup"><span data-stu-id="89e6a-216">Volume Type Supported for Encryption</span></span>|
| --- | --- |--- |
| <span data-ttu-id="89e6a-217">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="89e6a-217">Ubuntu</span></span> | <span data-ttu-id="89e6a-218">16.04-DAILY-LTS</span><span class="sxs-lookup"><span data-stu-id="89e6a-218">16.04-DAILY-LTS</span></span> | <span data-ttu-id="89e6a-219">Disque de système d’exploitation et de données</span><span class="sxs-lookup"><span data-stu-id="89e6a-219">OS and Data disk</span></span> |
| <span data-ttu-id="89e6a-220">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="89e6a-220">Ubuntu</span></span> | <span data-ttu-id="89e6a-221">14.04.5-DAILY-LTS</span><span class="sxs-lookup"><span data-stu-id="89e6a-221">14.04.5-DAILY-LTS</span></span> | <span data-ttu-id="89e6a-222">Disque de système d’exploitation et de données</span><span class="sxs-lookup"><span data-stu-id="89e6a-222">OS and Data disk</span></span> |
| <span data-ttu-id="89e6a-223">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="89e6a-223">Ubuntu</span></span> | <span data-ttu-id="89e6a-224">12.10</span><span class="sxs-lookup"><span data-stu-id="89e6a-224">12.10</span></span> | <span data-ttu-id="89e6a-225">Disque de données</span><span class="sxs-lookup"><span data-stu-id="89e6a-225">Data disk</span></span> |
| <span data-ttu-id="89e6a-226">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="89e6a-226">Ubuntu</span></span> | <span data-ttu-id="89e6a-227">12.04</span><span class="sxs-lookup"><span data-stu-id="89e6a-227">12.04</span></span> | <span data-ttu-id="89e6a-228">Disque de données</span><span class="sxs-lookup"><span data-stu-id="89e6a-228">Data disk</span></span> |
| <span data-ttu-id="89e6a-229">RHEL</span><span class="sxs-lookup"><span data-stu-id="89e6a-229">RHEL</span></span> | <span data-ttu-id="89e6a-230">7.3</span><span class="sxs-lookup"><span data-stu-id="89e6a-230">7.3</span></span> | <span data-ttu-id="89e6a-231">Disque de système d’exploitation et de données</span><span class="sxs-lookup"><span data-stu-id="89e6a-231">OS and Data disk</span></span> |
| <span data-ttu-id="89e6a-232">RHEL</span><span class="sxs-lookup"><span data-stu-id="89e6a-232">RHEL</span></span> | <span data-ttu-id="89e6a-233">7,2</span><span class="sxs-lookup"><span data-stu-id="89e6a-233">7.2</span></span> | <span data-ttu-id="89e6a-234">Disque de système d’exploitation et de données</span><span class="sxs-lookup"><span data-stu-id="89e6a-234">OS and Data disk</span></span> |
| <span data-ttu-id="89e6a-235">RHEL</span><span class="sxs-lookup"><span data-stu-id="89e6a-235">RHEL</span></span> | <span data-ttu-id="89e6a-236">6,8</span><span class="sxs-lookup"><span data-stu-id="89e6a-236">6.8</span></span> | <span data-ttu-id="89e6a-237">Disque de système d’exploitation et de données</span><span class="sxs-lookup"><span data-stu-id="89e6a-237">OS and Data disk</span></span> |
| <span data-ttu-id="89e6a-238">RHEL</span><span class="sxs-lookup"><span data-stu-id="89e6a-238">RHEL</span></span> | <span data-ttu-id="89e6a-239">6.7</span><span class="sxs-lookup"><span data-stu-id="89e6a-239">6.7</span></span> | <span data-ttu-id="89e6a-240">Disque de données</span><span class="sxs-lookup"><span data-stu-id="89e6a-240">Data disk</span></span> |
| <span data-ttu-id="89e6a-241">CentOS</span><span class="sxs-lookup"><span data-stu-id="89e6a-241">CentOS</span></span> | <span data-ttu-id="89e6a-242">7.3</span><span class="sxs-lookup"><span data-stu-id="89e6a-242">7.3</span></span> | <span data-ttu-id="89e6a-243">Disque de système d’exploitation et de données</span><span class="sxs-lookup"><span data-stu-id="89e6a-243">OS and Data disk</span></span> |
| <span data-ttu-id="89e6a-244">CentOS</span><span class="sxs-lookup"><span data-stu-id="89e6a-244">CentOS</span></span> | <span data-ttu-id="89e6a-245">7.2n</span><span class="sxs-lookup"><span data-stu-id="89e6a-245">7.2n</span></span> | <span data-ttu-id="89e6a-246">Disque de système d’exploitation et de données</span><span class="sxs-lookup"><span data-stu-id="89e6a-246">OS and Data disk</span></span> |
| <span data-ttu-id="89e6a-247">CentOS</span><span class="sxs-lookup"><span data-stu-id="89e6a-247">CentOS</span></span> | <span data-ttu-id="89e6a-248">6.8</span><span class="sxs-lookup"><span data-stu-id="89e6a-248">6.8</span></span> | <span data-ttu-id="89e6a-249">Disque de système d’exploitation et de données</span><span class="sxs-lookup"><span data-stu-id="89e6a-249">OS and Data disk</span></span> |
| <span data-ttu-id="89e6a-250">CentOS</span><span class="sxs-lookup"><span data-stu-id="89e6a-250">CentOS</span></span> | <span data-ttu-id="89e6a-251">7.1</span><span class="sxs-lookup"><span data-stu-id="89e6a-251">7.1</span></span> | <span data-ttu-id="89e6a-252">Disque de données</span><span class="sxs-lookup"><span data-stu-id="89e6a-252">Data disk</span></span> |
| <span data-ttu-id="89e6a-253">CentOS</span><span class="sxs-lookup"><span data-stu-id="89e6a-253">CentOS</span></span> | <span data-ttu-id="89e6a-254">7.0</span><span class="sxs-lookup"><span data-stu-id="89e6a-254">7.0</span></span> | <span data-ttu-id="89e6a-255">Disque de données</span><span class="sxs-lookup"><span data-stu-id="89e6a-255">Data disk</span></span> |
| <span data-ttu-id="89e6a-256">CentOS</span><span class="sxs-lookup"><span data-stu-id="89e6a-256">CentOS</span></span> | <span data-ttu-id="89e6a-257">6.7</span><span class="sxs-lookup"><span data-stu-id="89e6a-257">6.7</span></span> | <span data-ttu-id="89e6a-258">Disque de données</span><span class="sxs-lookup"><span data-stu-id="89e6a-258">Data disk</span></span> |
| <span data-ttu-id="89e6a-259">CentOS</span><span class="sxs-lookup"><span data-stu-id="89e6a-259">CentOS</span></span> | <span data-ttu-id="89e6a-260">6.6</span><span class="sxs-lookup"><span data-stu-id="89e6a-260">6.6</span></span> | <span data-ttu-id="89e6a-261">Disque de données</span><span class="sxs-lookup"><span data-stu-id="89e6a-261">Data disk</span></span> |
| <span data-ttu-id="89e6a-262">CentOS</span><span class="sxs-lookup"><span data-stu-id="89e6a-262">CentOS</span></span> | <span data-ttu-id="89e6a-263">6.5</span><span class="sxs-lookup"><span data-stu-id="89e6a-263">6.5</span></span> | <span data-ttu-id="89e6a-264">Disque de données</span><span class="sxs-lookup"><span data-stu-id="89e6a-264">Data disk</span></span> |
| <span data-ttu-id="89e6a-265">openSUSE</span><span class="sxs-lookup"><span data-stu-id="89e6a-265">openSUSE</span></span> | <span data-ttu-id="89e6a-266">13.2</span><span class="sxs-lookup"><span data-stu-id="89e6a-266">13.2</span></span> | <span data-ttu-id="89e6a-267">Disque de données</span><span class="sxs-lookup"><span data-stu-id="89e6a-267">Data disk</span></span> |
| <span data-ttu-id="89e6a-268">SLES</span><span class="sxs-lookup"><span data-stu-id="89e6a-268">SLES</span></span> | <span data-ttu-id="89e6a-269">12 SP1</span><span class="sxs-lookup"><span data-stu-id="89e6a-269">12 SP1</span></span> | <span data-ttu-id="89e6a-270">Disque de données</span><span class="sxs-lookup"><span data-stu-id="89e6a-270">Data disk</span></span> |
| <span data-ttu-id="89e6a-271">SLES</span><span class="sxs-lookup"><span data-stu-id="89e6a-271">SLES</span></span> | <span data-ttu-id="89e6a-272">12-SP1 (Premium)</span><span class="sxs-lookup"><span data-stu-id="89e6a-272">12-SP1 (Premium)</span></span> | <span data-ttu-id="89e6a-273">Disque de données</span><span class="sxs-lookup"><span data-stu-id="89e6a-273">Data disk</span></span> |
| <span data-ttu-id="89e6a-274">SLES</span><span class="sxs-lookup"><span data-stu-id="89e6a-274">SLES</span></span> | <span data-ttu-id="89e6a-275">HPC 12</span><span class="sxs-lookup"><span data-stu-id="89e6a-275">HPC 12</span></span> | <span data-ttu-id="89e6a-276">Disque de données</span><span class="sxs-lookup"><span data-stu-id="89e6a-276">Data disk</span></span> |
| <span data-ttu-id="89e6a-277">SLES</span><span class="sxs-lookup"><span data-stu-id="89e6a-277">SLES</span></span> | <span data-ttu-id="89e6a-278">11-SP4 (Premium)</span><span class="sxs-lookup"><span data-stu-id="89e6a-278">11-SP4 (Premium)</span></span> | <span data-ttu-id="89e6a-279">Disque de données</span><span class="sxs-lookup"><span data-stu-id="89e6a-279">Data disk</span></span> |
| <span data-ttu-id="89e6a-280">SLES</span><span class="sxs-lookup"><span data-stu-id="89e6a-280">SLES</span></span> | <span data-ttu-id="89e6a-281">11 SP4</span><span class="sxs-lookup"><span data-stu-id="89e6a-281">11 SP4</span></span> | <span data-ttu-id="89e6a-282">Disque de données</span><span class="sxs-lookup"><span data-stu-id="89e6a-282">Data disk</span></span> |

* <span data-ttu-id="89e6a-283">Azure Disk Encryption requiert que votre coffre de clés et vos machines virtuelles se trouvent dans la même région et le même abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="89e6a-283">Azure Disk Encryption requires that your key vault and VMs reside in the same Azure region and subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="89e6a-284">La configuration des ressources dans des régions distinctes provoque l’échec de l’activation de la fonctionnalité Azure Disk Encryption.</span><span class="sxs-lookup"><span data-stu-id="89e6a-284">Configuring the resources in separate regions causes a failure in enabling the Azure Disk Encryption feature.</span></span>

* <span data-ttu-id="89e6a-285">Pour créer et configurer votre coffre de clés pour Azure Disk Encryption, voir la section **Créer et configurer votre coffre de clés pour Azure Disk Encryption** dans la rubrique *Conditions préalables* de cet article.</span><span class="sxs-lookup"><span data-stu-id="89e6a-285">To set up and configure your key vault for Azure Disk Encryption, see section **Set up and configure your key vault for Azure Disk Encryption** in the *Prerequisites* section of this article.</span></span>
* <span data-ttu-id="89e6a-286">Pour créer et configurer l’application Azure AD dans Azure Active Directory pour Azure Disk Encryption, voir la section **Configurer l’application Azure AD dans Azure Active Directory** de la rubrique *Conditions préalables* dans cet article.</span><span class="sxs-lookup"><span data-stu-id="89e6a-286">To set up and configure Azure AD application in Azure Active directory for Azure Disk Encryption, see section **Set up the Azure AD application in Azure Active Directory** in the *Prerequisites* section of this article.</span></span>
* <span data-ttu-id="89e6a-287">Pour créer et configurer la stratégie d’accès au coffre de clés pour l’application Azure AD, voir la section **Configurer la stratégie d’accès au coffre de clés pour l’application Azure AD** de la rubrique *Conditions préalables* dans cet article.</span><span class="sxs-lookup"><span data-stu-id="89e6a-287">To set up and configure the key vault access policy for the Azure AD application, see section **Set up the key vault access policy for the Azure AD application** in the *Prerequisites* section of this article.</span></span>
* <span data-ttu-id="89e6a-288">Pour préparer un disque dur virtuel Windows pré-chiffré, voir la section **Préparer un disque dur virtuel Windows pré-chiffré** dans l’*Annexe*.</span><span class="sxs-lookup"><span data-stu-id="89e6a-288">To prepare a pre-encrypted Windows VHD, see section **Prepare a pre-encrypted Windows VHD** in the *Appendix*.</span></span>
* <span data-ttu-id="89e6a-289">Pour préparer un disque dur virtuel Linux pré-chiffré, voir la section **réparer un disque dur virtuel Linux pré-chiffré** dans l’*Annexe*.</span><span class="sxs-lookup"><span data-stu-id="89e6a-289">To prepare a pre-encrypted Linux VHD, see section **Prepare a pre-encrypted Linux VHD** in the *Appendix*.</span></span>
* <span data-ttu-id="89e6a-290">La plateforme Azure doit avoir accès aux clés ou aux clés secrètes de chiffrement dans votre coffre de clés afin de les mettre à disposition de la machine virtuelle au moment de lancer et de déchiffrer son volume de système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="89e6a-290">The Azure platform needs access to the encryption keys or secrets in your key vault to make them available to the virtual machine when it boots and decrypts the virtual machine OS volume.</span></span> <span data-ttu-id="89e6a-291">Pour accorder des autorisations pour la plateforme Azure, définissez la propriété **EnabledForDiskEncryption** dans le coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="89e6a-291">To grant permissions to Azure platform, set the **EnabledForDiskEncryption** property in the key vault.</span></span> <span data-ttu-id="89e6a-292">Pour plus d’informations, voir la section **Créer et configurer votre coffre de clés pour Azure Disk Encryption** dans l’Annexe.</span><span class="sxs-lookup"><span data-stu-id="89e6a-292">For more information, see **Set up and configure your key vault for Azure Disk Encryption** in the Appendix.</span></span>
* <span data-ttu-id="89e6a-293">Les URL de clé secrète de coffre de clés et de clé de chiffrement à clé (KEK) doivent être des versions gérées.</span><span class="sxs-lookup"><span data-stu-id="89e6a-293">Your key vault secret and KEK URLs must be versioned.</span></span> <span data-ttu-id="89e6a-294">Azure met en vigueur cette restriction de gestion de version.</span><span class="sxs-lookup"><span data-stu-id="89e6a-294">Azure enforces this restriction of versioning.</span></span> <span data-ttu-id="89e6a-295">Voici des exemples d’URL de clé secrète et de clé de chiffrement à clé valides :</span><span class="sxs-lookup"><span data-stu-id="89e6a-295">For valid secret and KEK URLs, see the following examples:</span></span>

  * <span data-ttu-id="89e6a-296">Exemple d’URL secrète valide : *https://contosovault.vault.azure.net/secrets/BitLockerEncryptionSecretWithKek/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span><span class="sxs-lookup"><span data-stu-id="89e6a-296">Example of a valid secret URL:   *https://contosovault.vault.azure.net/secrets/BitLockerEncryptionSecretWithKek/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span></span>
  * <span data-ttu-id="89e6a-297">Exemple d’URL de clé de chiffrement à clé valide : *https://contosovault.vault.azure.net/keys/diskencryptionkek/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span><span class="sxs-lookup"><span data-stu-id="89e6a-297">Example of a valid KEK URL:   *https://contosovault.vault.azure.net/keys/diskencryptionkek/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span></span>

* <span data-ttu-id="89e6a-298">Azure Disk Encryption ne prend pas en charge l’intégration de numéros de port aux clés secrètes de coffre de clés et aux URL KEK.</span><span class="sxs-lookup"><span data-stu-id="89e6a-298">Azure Disk Encryption does not support specifying port numbers as part of key vault secrets and KEK URLs.</span></span> <span data-ttu-id="89e6a-299">Voici des exemples d’URL de coffre de clés valides et non valides :</span><span class="sxs-lookup"><span data-stu-id="89e6a-299">For examples of non-supported and supported key vault URLs, see the following:</span></span>

  * <span data-ttu-id="89e6a-300">URL de coffre de clés non acceptée : *https://contosovault.vault.azure.net:443/secrets/contososecret/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span><span class="sxs-lookup"><span data-stu-id="89e6a-300">Unacceptable key vault URL  *https://contosovault.vault.azure.net:443/secrets/contososecret/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span></span>
  * <span data-ttu-id="89e6a-301">URL de coffre de clés acceptée : *https://contosovault.vault.azure.net/secrets/contososecret/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span><span class="sxs-lookup"><span data-stu-id="89e6a-301">Acceptable key vault URL:   *https://contosovault.vault.azure.net/secrets/contososecret/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span></span>

* <span data-ttu-id="89e6a-302">Pour activer la fonctionnalité Azure Disk Encryption, les machines virtuelles IaaS doivent répondre aux exigences de configuration du point de terminaison de réseau suivantes :</span><span class="sxs-lookup"><span data-stu-id="89e6a-302">To enable the Azure Disk Encryption feature, the IaaS VMs must meet the following network endpoint configuration requirements:</span></span>
  * <span data-ttu-id="89e6a-303">Pour obtenir un jeton afin de se connecter à votre coffre de clés, la machine virtuelle IaaS doit être en mesure de se connecter au point de terminaison Azure Active Directory \[Login.microsoftonline.com\].</span><span class="sxs-lookup"><span data-stu-id="89e6a-303">To get a token to connect to your key vault, the IaaS VM must be able to connect to an Azure Active Directory endpoint, \[login.microsoftonline.com\].</span></span>
  * <span data-ttu-id="89e6a-304">Pour écrire les clés de chiffrement dans votre coffre de clés, la machine virtuelle IaaS doit être en mesure de se connecter au point de terminaison Key Vault.</span><span class="sxs-lookup"><span data-stu-id="89e6a-304">To write the encryption keys to your key vault, the IaaS VM must be able to connect to the key vault endpoint.</span></span>
  * <span data-ttu-id="89e6a-305">La machine virtuelle IaaS doit être en mesure de se connecter au point de terminaison de stockage Azure qui héberge le référentiel d’extensions Azure et au compte de stockage Azure qui héberge les fichiers de disque dur virtuel.</span><span class="sxs-lookup"><span data-stu-id="89e6a-305">The IaaS VM must be able to connect to an Azure storage endpoint that hosts the Azure extension repository and an Azure storage account that hosts the VHD files.</span></span>

  > [!NOTE]
  > <span data-ttu-id="89e6a-306">Si votre stratégie de sécurité limite l’accès à Internet à partir des machines virtuelles Azure, vous pouvez résoudre l’URI ci-dessus et configurer une règle spécifique pour autoriser les connexions sortantes vers les adresses IP.</span><span class="sxs-lookup"><span data-stu-id="89e6a-306">If your security policy limits access from Azure VMs to the Internet, you can resolve the preceding URI and configure a specific rule to allow outbound connectivity to the IPs.</span></span>
  >
  ><span data-ttu-id="89e6a-307">Pour configurer un coffre de clés Azure et y accéder derrière un pare-feu (https://docs.microsoft.com/fr-fr/azure/key-vault/key-vault-access-behind-firewall)</span><span class="sxs-lookup"><span data-stu-id="89e6a-307">To configure and access Azure Key Vault behind a firewall(https://docs.microsoft.com/en-us/azure/key-vault/key-vault-access-behind-firewall)</span></span>

* <span data-ttu-id="89e6a-308">Utilisez la dernière version du kit de développement logiciel (SDK) Azure PowerShell pour configurer Azure Disk Encryption.</span><span class="sxs-lookup"><span data-stu-id="89e6a-308">Use the latest version of Azure PowerShell SDK version to configure Azure Disk Encryption.</span></span> <span data-ttu-id="89e6a-309">Téléchargez la dernière version d’[Azure PowerShell](https://github.com/Azure/azure-powershell/releases).</span><span class="sxs-lookup"><span data-stu-id="89e6a-309">Download the latest version of [Azure PowerShell release](https://github.com/Azure/azure-powershell/releases)</span></span>

 > [!NOTE]
  > <span data-ttu-id="89e6a-310">Azure Disk Encryption n’est pas pris en charge dans le [Kit de développement logiciel (SDK) Azure PowerShell version 1.1.0](https://github.com/Azure/azure-powershell/releases/tag/v1.1.0-January2016).</span><span class="sxs-lookup"><span data-stu-id="89e6a-310">Azure Disk Encryption is not supported on [Azure PowerShell SDK version 1.1.0](https://github.com/Azure/azure-powershell/releases/tag/v1.1.0-January2016).</span></span> <span data-ttu-id="89e6a-311">Si vous recevez une erreur liée à l’utilisation d’Azure PowerShell 1.1.0, consultez la rubrique [Azure Disk Encryption Error Related to Azure PowerShell 1.1.0](http://blogs.msdn.com/b/azuresecurity/archive/2016/02/10/azure-disk-encryption-error-related-to-azure-powershell-1-1-0.aspx) (Erreur Azure Disk Encryption liée à Azure PowerShell 1.1.0).</span><span class="sxs-lookup"><span data-stu-id="89e6a-311">If you are receiving an error related to using Azure PowerShell 1.1.0, see [Azure Disk Encryption Error Related to Azure PowerShell 1.1.0](http://blogs.msdn.com/b/azuresecurity/archive/2016/02/10/azure-disk-encryption-error-related-to-azure-powershell-1-1-0.aspx).</span></span>

* <span data-ttu-id="89e6a-312">Pour exécuter les commandes de l’interface de ligne de commande Azure et les associer à votre abonnement Azure, vous devez d’abord installer l’interface de ligne de commande Azure :</span><span class="sxs-lookup"><span data-stu-id="89e6a-312">To run any Azure CLI command and associate it with your Azure subscription, you must first install Azure CLI:</span></span>
  * <span data-ttu-id="89e6a-313">Pour installer l’interface de ligne de commande Azure et l’associer à votre abonnement Azure, consultez la rubrique [Installation et configuration de l’interface de ligne de commande Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="89e6a-313">To install Azure CLI and associate it with your Azure subscription, see [How to install and configure Azure CLI](../cli-install-nodejs.md).</span></span>
  * <span data-ttu-id="89e6a-314">Pour utiliser l’interface de ligne de commande Azure pour Mac, Linux et Windows avec Azure Resource Manager, consultez la rubrique [Commandes de l’interface de ligne de commande Azure en mode Resource Manager](../virtual-machines/azure-cli-arm-commands.md).</span><span class="sxs-lookup"><span data-stu-id="89e6a-314">To use Azure CLI for Mac, Linux, and Windows with Azure Resource Manager, see [Azure CLI commands in Resource Manager mode](../virtual-machines/azure-cli-arm-commands.md).</span></span>

* <span data-ttu-id="89e6a-315">Lors du chiffrement d’un disque géré, une condition préalable exige de prendre un instantané du disque géré ou une sauvegarde du disque en dehors de Azure Disk Encryption avant d’activer le chiffrement.</span><span class="sxs-lookup"><span data-stu-id="89e6a-315">When encrypting a managed disk, it is mandatory prerequisite to take a snapshot of the managed disk or a backup of the disk outside of Azure Disk Encryption prior to enabling encryption.</span></span>  <span data-ttu-id="89e6a-316">Sans une sauvegarde mise en place, tout échec inattendu au cours du chiffrement peut rendre le disque et la machine virtuelle inaccessibles sans option de récupération possible.</span><span class="sxs-lookup"><span data-stu-id="89e6a-316">Without a backup in place, any unexpected failure during encryption may render the disk and VM inaccessible without a recovery option.</span></span>  <span data-ttu-id="89e6a-317">Set-AzureRmVMDiskEncryptionExtension ne sauvegarde pas de disque géré actuellement, et il ne peut que déclencher une erreur s’il est utilisé avec un disque géré, sauf si le paramètre - skipVmBackup a été spécifié.</span><span class="sxs-lookup"><span data-stu-id="89e6a-317">Set-AzureRmVMDiskEncryptionExtension does not currently back up managed disks and will error if used against a managed disk unless the -skipVmBackup parameter has been specified.</span></span>  <span data-ttu-id="89e6a-318">L’utilisation de ce paramètre n’est pas sûre, sauf si une sauvegarde a déjà été effectuée en dehors d’Azure Disk Encryption.</span><span class="sxs-lookup"><span data-stu-id="89e6a-318">This parameter is unsafe to use unless a backup has already been made outside of Azure Disk Encryption.</span></span>   <span data-ttu-id="89e6a-319">Lorsque le paramètre - skipVmBackup est spécifié, l’applet de commande n’effectue pas de sauvegarde du disque géré avant le chiffrement.</span><span class="sxs-lookup"><span data-stu-id="89e6a-319">When the -skipVmBackup parameter is specified, the cmdlet will not make a backup of the managed disk prior to encryption.</span></span>  <span data-ttu-id="89e6a-320">Ainsi, il est considéré comme condition préalable obligatoire de vérifier qu’une sauvegarde de la machine virtuelle du disque géré est bien en place avant d’activer Azure Disk Encryption, au cas où une récupération serait ultérieurement nécessaire.</span><span class="sxs-lookup"><span data-stu-id="89e6a-320">For this reason, it is considered a mandatory prerequisite to make sure a backup of the managed disk VM is in place prior to enabling Azure Disk Encryption in case recovery is later needed.</span></span>  
> [!NOTE]
 > <span data-ttu-id="89e6a-321">Le paramètre - skipVmBackup ne doit jamais être utilisé, sauf si une sauvegarde ou un instantané a déjà été réalisé en dehors d’Azure Disk Encryption.</span><span class="sxs-lookup"><span data-stu-id="89e6a-321">The -skipVmBackup parameter should never be used unless a snapshot or backup has already been made outside of Azure Disk Encryption.</span></span> 

* <span data-ttu-id="89e6a-322">La solution Azure Disk Encryption utilise le protecteur de clé externe BitLocker pour les machines virtuelles IaaS Windows.</span><span class="sxs-lookup"><span data-stu-id="89e6a-322">The Azure Disk Encryption solution uses the BitLocker external key protector for Windows IaaS VMs.</span></span> <span data-ttu-id="89e6a-323">Pour des machines virtuelles jointes au domaine, ne distribuez PAS de stratégies de groupe qui appliquent des protecteurs de Module de plateforme sécurisée (TPM).</span><span class="sxs-lookup"><span data-stu-id="89e6a-323">For domain joined VMs, DO NOT push any group policies that enforce TPM protectors.</span></span> <span data-ttu-id="89e6a-324">Pour en savoir plus sur la stratégie de groupe pour « Autoriser BitLocker sans module de plateforme sécurisée compatible », consultez la rubrique [BitLocker Group Policy Reference](https://technet.microsoft.com/library/ee706521) (Référence de stratégie de groupe BitLocker).</span><span class="sxs-lookup"><span data-stu-id="89e6a-324">For information about the group policy for “Allow BitLocker without a compatible TPM,” see [BitLocker Group Policy Reference](https://technet.microsoft.com/library/ee706521).</span></span>
* <span data-ttu-id="89e6a-325">La stratégie BitLocker, sur les machines virtuelles jointes à un domaine et ayant une stratégie de groupe personnalisée, doit inclure le paramètre suivant : `Configure user storage of bitlocker recovery information -> Allow 256-bit recovery key` Azure Disk Encryption échoue lorsque les paramètres de stratégie de groupe personnalisée pour Bitlocker sont incompatibles.</span><span class="sxs-lookup"><span data-stu-id="89e6a-325">Bitlocker policy on domain joined virtual machines with custom group policy must include the following setting: `Configure user storage of bitlocker recovery information -> Allow 256-bit recovery key`  Azure Disk Encryption will fail when custom group policy settings for Bitlocker are incompatible.</span></span> <span data-ttu-id="89e6a-326">Sur les machines dont le paramètre de stratégie n’était pas correct, l’application de la nouvelle stratégie, la mise à jour forcée de la nouvelle stratégie (gpupdate.exe /force) et le redémarrage peuvent être nécessaires.</span><span class="sxs-lookup"><span data-stu-id="89e6a-326">On machines that did not have the correct policy setting, applying the new policy, forcing the new policy to update (gpupdate.exe /force), and then restarting may be required.</span></span>  
* <span data-ttu-id="89e6a-327">Pour créer l’application Azure AD, créer un coffre de clés ou en configurer un existant et activer le chiffrement, consultez la rubrique [Script PowerShell prérequis pour Azure Disk Encryption](https://github.com/Azure/azure-powershell/blob/master/src/ResourceManager/Compute/Commands.Compute/Extension/AzureDiskEncryption/Scripts/AzureDiskEncryptionPreRequisiteSetup.ps1).</span><span class="sxs-lookup"><span data-stu-id="89e6a-327">To create an Azure AD application, create a key vault, or set up an existing key vault and enable encryption, see the [Azure Disk Encryption prerequisite PowerShell script](https://github.com/Azure/azure-powershell/blob/master/src/ResourceManager/Compute/Commands.Compute/Extension/AzureDiskEncryption/Scripts/AzureDiskEncryptionPreRequisiteSetup.ps1).</span></span>
* <span data-ttu-id="89e6a-328">Pour configurer les composants requis de chiffrement de disque à l’aide de l’interface de ligne de commande Azure, consultez [ce script bash](https://github.com/ejarvi/ade-cli-getting-started).</span><span class="sxs-lookup"><span data-stu-id="89e6a-328">To configure disk-encryption prerequisites using the Azure CLI, see [this Bash script](https://github.com/ejarvi/ade-cli-getting-started).</span></span>
* <span data-ttu-id="89e6a-329">Pour utiliser le service Sauvegarde Azure afin de sauvegarder et de restaurer des machines virtuelles chiffrées, lorsque le chiffrement est activé avec Azure Disk Encryption, chiffrez vos machines virtuelles à l’aide de la configuration de clé Azure Disk Encryption.</span><span class="sxs-lookup"><span data-stu-id="89e6a-329">To use the Azure Backup service to back up and restore encrypted VMs, when encryption is enabled with Azure Disk Encryption, encrypt your VMs by using the Azure Disk Encryption key configuration.</span></span> <span data-ttu-id="89e6a-330">Le service de sauvegarde prend en charge les machines virtuelles chiffrées à l’aide de la configuration de clé de chiffrement à clé [KEK] uniquement.</span><span class="sxs-lookup"><span data-stu-id="89e6a-330">The Backup service supports VMs that are encrypted using KEK configuration only.</span></span> <span data-ttu-id="89e6a-331">Voir [Guide pratique de sauvegarde et restauration des machines virtuelles chiffrées avec Sauvegarde Azure](https://docs.microsoft.com/en-us/azure/backup/backup-azure-vms-encryption).</span><span class="sxs-lookup"><span data-stu-id="89e6a-331">See [How to back up and restore encrypted virtual machines with Azure Backup  encryption](https://docs.microsoft.com/en-us/azure/backup/backup-azure-vms-encryption).</span></span>

* <span data-ttu-id="89e6a-332">Lors du chiffrement d’un volume de système d’exploitation Linux, notez qu’un redémarrage de la machine virtuelle est actuellement nécessaire à la fin du processus.</span><span class="sxs-lookup"><span data-stu-id="89e6a-332">When encrypting a Linux OS volume, note that a VM restart is currently required at the end of the process.</span></span> <span data-ttu-id="89e6a-333">Il est possible de le faire via le portail, Powershell ou CLI.</span><span class="sxs-lookup"><span data-stu-id="89e6a-333">This can be done via the portal, powershell, or CLI.</span></span>   <span data-ttu-id="89e6a-334">Pour suivre la progression du chiffrement, consultez régulièrement le message d’état retourné par Get-AzureRmVMDiskEncryptionStatus https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus.</span><span class="sxs-lookup"><span data-stu-id="89e6a-334">To track the progress of encryption, periodically poll the status message returned by Get-AzureRmVMDiskEncryptionStatus https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus.</span></span>  <span data-ttu-id="89e6a-335">Une fois le chiffrement terminé, le message d’état retourné par cette commande indique le résultat de cette opération.</span><span class="sxs-lookup"><span data-stu-id="89e6a-335">Once encryption is complete, the the status message returned by this command will indicate this.</span></span>  <span data-ttu-id="89e6a-336">Par exemple, « ProgressMessage : le chiffrement du disque du système d’exploitation s’est correctement déroulé, veuillez redémarrer la machine virtuelle ». À ce stade, la machine virtuelle peut être redémarrée et utilisée.</span><span class="sxs-lookup"><span data-stu-id="89e6a-336">For example, "ProgressMessage: OS disk successfully encrypted, please reboot the VM"  At this point the VM can be restarted and used.</span></span>  

* <span data-ttu-id="89e6a-337">Azure Disk Encryption pour Linux exige que le système de fichiers des disques de données soit monté dans Linux avant l’opération de chiffrement.</span><span class="sxs-lookup"><span data-stu-id="89e6a-337">Azure Disk Encryption for Linux requires data disks to have a mounted file system in Linux prior to encryption</span></span>

* <span data-ttu-id="89e6a-338">Les disques de données montés de façon récursive ne sont pas pris en charge par Azure Disk Encryption pour Linux.</span><span class="sxs-lookup"><span data-stu-id="89e6a-338">Recursively mounted data disks are not supported by the Azure Disk Encryption for Linux.</span></span> <span data-ttu-id="89e6a-339">Par exemple, si le système cible a monté un disque sur /foo/bar, puis un autre sur /foo/bar/baz, le chiffrement de /foo/bar/baz réussit, mais le chiffrement de /foo/bar échoue.</span><span class="sxs-lookup"><span data-stu-id="89e6a-339">For example, if the target system has mounted a disk on /foo/bar and then another on /foo/bar/baz, the encryption of /foo/bar/baz will succeed, but encryption of /foo/bar will fail.</span></span> 

* <span data-ttu-id="89e6a-340">Azure Disk Encryption est uniquement pris en charge sur les images de la galerie Azure prises en charge qui remplissent les conditions préalables susmentionnées.</span><span class="sxs-lookup"><span data-stu-id="89e6a-340">Azure Disk Encryption is only supported on Azure gallery supported images that meet the aforementioned prerequisites.</span></span> <span data-ttu-id="89e6a-341">Les images client personnalisées ne sont pas prises en charge en raison de comportements de processus et de schémas de partition personnalisés pouvant exister sur ces images.</span><span class="sxs-lookup"><span data-stu-id="89e6a-341">Customer custom images are not supported due to custom partition schemes and process behaviors that may exist on these images.</span></span> <span data-ttu-id="89e6a-342">De plus, même les machines virtuelles d’image de galerie, qui initialement remplissaient les conditions préalables demandées, mais qui ont été modifiées depuis leur création, peuvent être incompatibles.</span><span class="sxs-lookup"><span data-stu-id="89e6a-342">Further, even gallery image based VM's that initially met prerequisites but have been modified after creation may be incompatible.</span></span>  <span data-ttu-id="89e6a-343">Ainsi, la procédure suggérée pour chiffrer une machine virtuelle Linux consiste à démarrer depuis une nouvelle image de galerie, à chiffrer la machine virtuelle, puis à ajouter en fonction des besoins les données ou les logiciels personnalisés à cette machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="89e6a-343">For that reason, the suggested procedure for encrypting a Linux VM is to start from a clean gallery image, encrypt the VM, and then add custom software or data to the VM as needed.</span></span>  

> [!NOTE]
> <span data-ttu-id="89e6a-344">La sauvegarde et la restauration de machines virtuelles chiffrées sont prises en charge uniquement pour les machines virtuelles chiffrées à l’aide de la configuration de clé de chiffrement à clé (KEK).</span><span class="sxs-lookup"><span data-stu-id="89e6a-344">Backup and restore of encrypted VMs is supported only for VMs that are encrypted with the KEK configuration.</span></span> <span data-ttu-id="89e6a-345">Elles ne sont pas prises en charge pour les machines virtuelles chiffrées sans KEK.</span><span class="sxs-lookup"><span data-stu-id="89e6a-345">It is not supported on VMs that are encrypted without KEK.</span></span> <span data-ttu-id="89e6a-346">KEK est un paramètre facultatif qui active une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="89e6a-346">KEK is an optional parameter that enables VM.</span></span>

#### <a name="set-up-the-azure-ad-application-in-azure-active-directory"></a><span data-ttu-id="89e6a-347">Configurer l’application Azure AD dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="89e6a-347">Set up the Azure AD application in Azure Active Directory</span></span>
<span data-ttu-id="89e6a-348">Lorsque le chiffrement doit être activé sur une machine virtuelle en cours d’exécution dans Azure, Azure Disk Encryption génère et écrit les clés de chiffrement dans votre coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="89e6a-348">When you need encryption to be enabled on a running VM in Azure, Azure Disk Encryption generates and writes the encryption keys to your key vault.</span></span> <span data-ttu-id="89e6a-349">La gestion des clés de chiffrement dans votre coffre de clés nécessite l’authentification Azure AD.</span><span class="sxs-lookup"><span data-stu-id="89e6a-349">Managing encryption keys in your key vault requires Azure AD authentication.</span></span>

<span data-ttu-id="89e6a-350">Une application Azure AD doit donc être créée à cet effet.</span><span class="sxs-lookup"><span data-stu-id="89e6a-350">For this purpose, create an Azure AD application.</span></span> <span data-ttu-id="89e6a-351">Vous trouverez la procédure détaillée d’inscription d’une application dans la section « Obtenir une identité d’application » du billet de blog [Azure Key Vault – Étape par étape](http://blogs.technet.com/b/kv/archive/2015/06/02/azure-key-vault-step-by-step.aspx).</span><span class="sxs-lookup"><span data-stu-id="89e6a-351">You can find detailed steps for registering an application in the “Get an Identity for the Application” section of the blog post [Azure Key Vault - Step by Step](http://blogs.technet.com/b/kv/archive/2015/06/02/azure-key-vault-step-by-step.aspx).</span></span> <span data-ttu-id="89e6a-352">Cet article contient également plusieurs exemples utiles sur l’installation et la configuration de votre coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="89e6a-352">This post also contains a number of helpful examples for setting up and configuring your key vault.</span></span> <span data-ttu-id="89e6a-353">Pour l’authentification, vous pouvez utiliser soit l’authentification par clé secrète de client, soit l’authentification Azure AD par certificat de client.</span><span class="sxs-lookup"><span data-stu-id="89e6a-353">For authentication purposes, you can use either client secret-based authentication or client certificate-based Azure AD authentication.</span></span>

#### <a name="client-secret-based-authentication-for-azure-ad"></a><span data-ttu-id="89e6a-354">Authentification par clé secrète de client pour Azure AD</span><span class="sxs-lookup"><span data-stu-id="89e6a-354">Client secret-based authentication for Azure AD</span></span>
<span data-ttu-id="89e6a-355">Les sections qui suivent vous expliquent comment configurer une authentification par clé secrète de client pour Azure AD.</span><span class="sxs-lookup"><span data-stu-id="89e6a-355">The sections that follow can help you configure a client secret-based authentication for Azure AD.</span></span>

##### <a name="create-an-azure-ad-application-by-using-azure-powershell"></a><span data-ttu-id="89e6a-356">Créer une application Azure AD à l’aide d’Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="89e6a-356">Create an Azure AD application by using Azure PowerShell</span></span>
<span data-ttu-id="89e6a-357">Pour créer une application Azure AD, utilisez l’applet de commande PowerShell suivante :</span><span class="sxs-lookup"><span data-stu-id="89e6a-357">Use the following PowerShell cmdlet to create an Azure AD application:</span></span>

    $aadClientSecret = "yourSecret"
    $azureAdApplication = New-AzureRmADApplication -DisplayName "<Your Application Display Name>" -HomePage "<https://YourApplicationHomePage>" -IdentifierUris "<https://YouApplicationUri>" -Password $aadClientSecret
    $servicePrincipal = New-AzureRmADServicePrincipal –ApplicationId $azureAdApplication.ApplicationId

> [!NOTE]
> <span data-ttu-id="89e6a-358">$azureAdApplication.ApplicationId est l’ID de client Azure AD et $aadClientSecret est la clé secrète de client que vous devez utiliser ultérieurement pour activer Azure Disk Encryption.</span><span class="sxs-lookup"><span data-stu-id="89e6a-358">$azureAdApplication.ApplicationId is the Azure AD ClientID and $aadClientSecret is the client secret that you should use later to enable Azure Disk Encryption.</span></span> <span data-ttu-id="89e6a-359">Prenez soin de bien sauvegarder la clé secrète de client Azure AD.</span><span class="sxs-lookup"><span data-stu-id="89e6a-359">Safeguard the Azure AD client secret appropriately.</span></span>

##### <a name="setting-up-the-azure-ad-client-id-and-secret-from-the-azure-classic-portal"></a><span data-ttu-id="89e6a-360">Configuration de l’ID de client Azure AD et de la clé secrète à partir du portail Azure Classic</span><span class="sxs-lookup"><span data-stu-id="89e6a-360">Setting up the Azure AD client ID and secret from the Azure classic portal</span></span>
<span data-ttu-id="89e6a-361">Vous pouvez également configurer votre ID de client Azure AD et la clé secrète à l’aide du [portail Azure Classic]( https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="89e6a-361">You can also set up your Azure AD client ID and secret by using the [Azure classic portal]( https://manage.windowsazure.com).</span></span> <span data-ttu-id="89e6a-362">Pour cela, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="89e6a-362">To perform this task, do the following:</span></span>

1. <span data-ttu-id="89e6a-363">Cliquez sur l’onglet **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="89e6a-363">Click the **Active Directory** tab.</span></span>

 ![Azure Disk Encryption](./media/azure-security-disk-encryption/disk-encryption-fig3.png)

2. <span data-ttu-id="89e6a-365">Cliquez sur **Ajouter une application** et saisissez le nom de l’application.</span><span class="sxs-lookup"><span data-stu-id="89e6a-365">Click **Add Application**, and then type the application name.</span></span>

 ![Azure Disk Encryption](./media/azure-security-disk-encryption/disk-encryption-fig4.png)

3. <span data-ttu-id="89e6a-367">Cliquez sur le bouton fléché et configurez les propriétés de l’application.</span><span class="sxs-lookup"><span data-stu-id="89e6a-367">Click the arrow button, and then configure the application properties.</span></span>

 ![Azure Disk Encryption](./media/azure-security-disk-encryption/disk-encryption-fig5.png)

4. <span data-ttu-id="89e6a-369">Cliquez sur la coche dans le coin inférieur gauche pour terminer.</span><span class="sxs-lookup"><span data-stu-id="89e6a-369">Click the check mark in the lower left corner to finish.</span></span> <span data-ttu-id="89e6a-370">La page de configuration d’application s’affiche et l’ID de client Azure AD s’affiche en bas de la page.</span><span class="sxs-lookup"><span data-stu-id="89e6a-370">The application configuration page appears, and the Azure AD client ID is displayed at the bottom of the page.</span></span>

 ![Azure Disk Encryption](./media/azure-security-disk-encryption/disk-encryption-fig6.png)

5. <span data-ttu-id="89e6a-372">Enregistrez la clé secrète de client Azure AD en cliquant sur le bouton **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="89e6a-372">Save the Azure AD client secret by clicking the **Save** button.</span></span> <span data-ttu-id="89e6a-373">Notez la clé secrète de client Azure AD dans la zone de texte de clé.</span><span class="sxs-lookup"><span data-stu-id="89e6a-373">Note the Azure AD client secret in the keys text box.</span></span> <span data-ttu-id="89e6a-374">Prenez soin de bien la sauvegarder.</span><span class="sxs-lookup"><span data-stu-id="89e6a-374">Safeguard it appropriately.</span></span>

 ![Azure Disk Encryption](./media/azure-security-disk-encryption/disk-encryption-fig7.png)

 > [!NOTE]
 > <span data-ttu-id="89e6a-376">Le flux ci-dessus n’est pas pris en charge sur le portail Azure Classic.</span><span class="sxs-lookup"><span data-stu-id="89e6a-376">The preceding flow is not supported on the Azure classic portal.</span></span>

##### <a name="use-an-existing-application"></a><span data-ttu-id="89e6a-377">Utiliser une application existante</span><span class="sxs-lookup"><span data-stu-id="89e6a-377">Use an existing application</span></span>
<span data-ttu-id="89e6a-378">Pour exécuter les commandes suivantes, téléchargez et utilisez le [module Azure AD PowerShell](https://technet.microsoft.com/library/jj151815.aspx).</span><span class="sxs-lookup"><span data-stu-id="89e6a-378">To execute the following commands, obtain and use the [Azure AD PowerShell module](https://technet.microsoft.com/library/jj151815.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="89e6a-379">Vous devez exécuter les commandes ci-dessous à partir d’une nouvelle fenêtre PowerShell.</span><span class="sxs-lookup"><span data-stu-id="89e6a-379">The following commands must be executed from a new PowerShell window.</span></span> <span data-ttu-id="89e6a-380">N’utilisez pas Azure PowerShell ou la fenêtre Azure Resource Manager pour exécuter ces commandes.</span><span class="sxs-lookup"><span data-stu-id="89e6a-380">Do not use Azure PowerShell or the Azure Resource Manager window to execute the commands.</span></span> <span data-ttu-id="89e6a-381">Nous vous recommandons cette approche car ces applets de commande se trouvent dans le module MSOnline ou Azure AD PowerShell.</span><span class="sxs-lookup"><span data-stu-id="89e6a-381">We recommend this approach because these cmdlets are in the MSOnline module or Azure AD PowerShell.</span></span>

    $clientSecret = ‘<yourAadClientSecret>’
    $aadClientID = '<Client ID of your Azure AD application>'
    connect-msolservice
    New-MsolServicePrincipalCredential -AppPrincipalId $aadClientID -Type password -Value $clientSecret

#### <a name="certificate-based-authentication-for-azure-ad"></a><span data-ttu-id="89e6a-382">Authentification par certificat pour Azure AD</span><span class="sxs-lookup"><span data-stu-id="89e6a-382">Certificate-based authentication for Azure AD</span></span>
> [!NOTE]
> <span data-ttu-id="89e6a-383">L’authentification par certificat Azure AD n’est actuellement pas prise en charge sur les machines virtuelles Linux.</span><span class="sxs-lookup"><span data-stu-id="89e6a-383">Azure AD certificate-based authentication is currently not supported on Linux VMs.</span></span>

<span data-ttu-id="89e6a-384">Les sections qui suivent expliquent comment configurer une authentification par certificat pour Azure AD.</span><span class="sxs-lookup"><span data-stu-id="89e6a-384">The sections that follow show how to configure a certificate-based authentication for Azure AD.</span></span>

##### <a name="create-an-azure-ad-application"></a><span data-ttu-id="89e6a-385">Créer une application Azure AD</span><span class="sxs-lookup"><span data-stu-id="89e6a-385">Create an Azure AD application</span></span>
<span data-ttu-id="89e6a-386">Pour créer une application Azure AD, utilisez les applets de commande PowerShell suivantes :</span><span class="sxs-lookup"><span data-stu-id="89e6a-386">To create an Azure AD application, execute the following PowerShell cmdlets:</span></span>

> [!NOTE]
> <span data-ttu-id="89e6a-387">Remplacez la chaîne `yourpassword` ci-dessous par votre mot de passe sécurisé et sauvegardez celui-ci.</span><span class="sxs-lookup"><span data-stu-id="89e6a-387">Replace the following `yourpassword` string with your secure password, and safeguard the password.</span></span>

    $cert = New-Object System.Security.Cryptography.X509Certificates.X509Certificate("C:\certificates\examplecert.pfx", "yourpassword")
    $keyValue = [System.Convert]::ToBase64String($cert.GetRawCertData())
    $azureAdApplication = New-AzureRmADApplication -DisplayName "<Your Application Display Name>" -HomePage "<https://YourApplicationHomePage>" -IdentifierUris "<https://YouApplicationUri>" -KeyValue $keyValue -KeyType AsymmetricX509Cert
    $servicePrincipal = New-AzureRmADServicePrincipal –ApplicationId $azureAdApplication.ApplicationId

<span data-ttu-id="89e6a-388">Une fois que vous avez terminé cette étape, téléchargez un fichier .pfx dans votre coffre de clés et activez la stratégie d’accès nécessaire pour déployer ce certificat sur une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="89e6a-388">After you finish this step, upload a PFX file to your key vault and enable the access policy needed to deploy that certificate to a VM.</span></span>

##### <a name="use-an-existing-azure-ad-application"></a><span data-ttu-id="89e6a-389">Utiliser une application Azure AD existante</span><span class="sxs-lookup"><span data-stu-id="89e6a-389">Use an existing Azure AD application</span></span>
<span data-ttu-id="89e6a-390">Si vous configurez l’authentification par certificat pour une application existante, utilisez les applets de commande PowerShell ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="89e6a-390">If you are configuring certificate-based authentication for an existing application, use the PowerShell cmdlets shown here.</span></span> <span data-ttu-id="89e6a-391">Veillez à les exécuter à partir d’une nouvelle fenêtre PowerShell.</span><span class="sxs-lookup"><span data-stu-id="89e6a-391">Be sure to execute them from a new PowerShell window.</span></span>

    $certLocalPath = 'C:\certs\myaadapp.cer'
    $aadClientID = '<Client ID of your Azure AD application>'
    connect-msolservice
    $cer = New-Object System.Security.Cryptography.X509Certificates.X509Certificate
    $cer.Import($certLocalPath)
    $binCert = $cer.GetRawCertData()
    $credValue = [System.Convert]::ToBase64String($binCert);
    New-MsolServicePrincipalCredential -AppPrincipalId $aadClientID -Type asymmetric -Value $credValue -Usage verify

<span data-ttu-id="89e6a-392">Une fois que vous avez terminé cette étape, téléchargez un fichier .pfx dans votre coffre de clés et activez la stratégie d’accès nécessaire pour déployer ce certificat sur une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="89e6a-392">After you finish this step, upload a PFX file to your key vault and enable the access policy that's needed to deploy the certificate to a VM.</span></span>

##### <a name="upload-a-pfx-file-to-your-key-vault"></a><span data-ttu-id="89e6a-393">Télécharger un fichier .pfx dans le coffre de clés</span><span class="sxs-lookup"><span data-stu-id="89e6a-393">Upload a PFX file to your key vault</span></span>
<span data-ttu-id="89e6a-394">Pour obtenir une explication détaillée de ce processus, consultez [le Blog officiel de l’équipe Azure Key Vault](http://blogs.technet.com/b/kv/archive/2015/07/14/vm_2d00_certificates.aspx).</span><span class="sxs-lookup"><span data-stu-id="89e6a-394">For a detailed explanation of this process, see [The Official Azure Key Vault Team Blog](http://blogs.technet.com/b/kv/archive/2015/07/14/vm_2d00_certificates.aspx).</span></span> <span data-ttu-id="89e6a-395">Toutefois, vous aurez uniquement besoin des applets de commande PowerShell suivantes pour exécuter cette tâche.</span><span class="sxs-lookup"><span data-stu-id="89e6a-395">However, the following PowerShell cmdlets are all you need for the task.</span></span> <span data-ttu-id="89e6a-396">Veillez à les exécuter à partir de la console Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="89e6a-396">Be sure to execute them from Azure PowerShell console.</span></span>

> [!NOTE]
> <span data-ttu-id="89e6a-397">Remplacez la chaîne `yourpassword` ci-dessous par votre mot de passe sécurisé et sauvegardez celui-ci.</span><span class="sxs-lookup"><span data-stu-id="89e6a-397">Replace the following `yourpassword` string with your secure password, and safeguard the password.</span></span>

    $certLocalPath = 'C:\certs\myaadapp.pfx'
    $certPassword = "yourpassword"
    $resourceGroupName = ‘yourResourceGroup’
    $keyVaultName = ‘yourKeyVaultName’
    $keyVaultSecretName = ‘yourAadCertSecretName’

    $fileContentBytes = get-content $certLocalPath -Encoding Byte
    $fileContentEncoded = [System.Convert]::ToBase64String($fileContentBytes)

    $jsonObject = @"
    {
    "data": "$filecontentencoded",
    "dataType" :"pfx",
    "password": "$certPassword"
    }
    "@

    $jsonObjectBytes = [System.Text.Encoding]::UTF8.GetBytes($jsonObject)
    $jsonEncoded = [System.Convert]::ToBase64String($jsonObjectBytes)

    Switch-AzureMode -Name AzureResourceManager
    $secret = ConvertTo-SecureString -String $jsonEncoded -AsPlainText -Force
    Set-AzureKeyVaultSecret -VaultName $keyVaultName -Name $keyVaultSecretName -SecretValue $secret
    Set-AzureRmKeyVaultAccessPolicy -VaultName $keyVaultName -ResourceGroupName $resourceGroupName –EnabledForDeployment

##### <a name="deploy-a-certificate-in-your-key-vault-to-an-existing-vm"></a><span data-ttu-id="89e6a-398">Déployer un certificat dans le coffre de clés sur une machine virtuelle existante</span><span class="sxs-lookup"><span data-stu-id="89e6a-398">Deploy a certificate in your key vault to an existing VM</span></span>
<span data-ttu-id="89e6a-399">Après avoir téléchargé le fichier .pfx, déployez un certificat dans le coffre de clés sur une machine virtuelle existante à l’aide de la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="89e6a-399">After you finish uploading the PFX, deploy a certificate in the key vault to an existing VM with the following:</span></span>
 ```
    $resourceGroupName = ‘yourResourceGroup’
    $keyVaultName = ‘yourKeyVaultName’
    $keyVaultSecretName = ‘yourAadCertSecretName’
    $vmName = ‘yourVMName’
    $certUrl = (Get-AzureKeyVaultSecret -VaultName $keyVaultName -Name $keyVaultSecretName).Id
    $sourceVaultId = (Get-AzureRmKeyVault -VaultName $keyVaultName -ResourceGroupName $resourceGroupName).ResourceId
    $vm = Get-AzureRmVM -ResourceGroupName $resourceGroupName -Name $vmName
    $vm = Add-AzureRmVMSecret -VM $vm -SourceVaultId $sourceVaultId -CertificateStore "My" -CertificateUrl $certUrl
    Update-AzureRmVM -VM $vm  -ResourceGroupName $resourceGroupName
 ```

#### <a name="set-up-the-key-vault-access-policy-for-the-azure-ad-application"></a><span data-ttu-id="89e6a-400">Définir la stratégie d’accès au coffre de clés pour l’application Azure AD</span><span class="sxs-lookup"><span data-stu-id="89e6a-400">Set up the key vault access policy for the Azure AD application</span></span>
<span data-ttu-id="89e6a-401">Votre application Azure AD a besoin d’autorisations d’accès aux clés ou aux clés secrètes dans le coffre.</span><span class="sxs-lookup"><span data-stu-id="89e6a-401">Your Azure AD application needs rights to access the keys or secrets in the vault.</span></span> <span data-ttu-id="89e6a-402">Utilisez l’applet de commande [`Set-AzureKeyVaultAccessPolicy`](/powershell/module/azure/set-azurekeyvaultaccesspolicy?view=azuresmps-3.7.0) pour accorder des autorisations à l’application en utilisant l’ID client (qui a été généré lors de l’enregistrement de l’application) comme valeur du paramètre _–ServicePrincipalName_.</span><span class="sxs-lookup"><span data-stu-id="89e6a-402">Use the [`Set-AzureKeyVaultAccessPolicy`](/powershell/module/azure/set-azurekeyvaultaccesspolicy?view=azuresmps-3.7.0) cmdlet to grant permissions to the application, using the client ID (which was generated when the application was registered) as the _–ServicePrincipalName_ parameter value.</span></span> <span data-ttu-id="89e6a-403">Pour en savoir plus, consultez le billet de blog [Azure Key Vault – Étape par étape](http://blogs.technet.com/b/kv/archive/2015/06/02/azure-key-vault-step-by-step.aspx).</span><span class="sxs-lookup"><span data-stu-id="89e6a-403">To learn more, see the blog post [Azure Key Vault - Step by Step](http://blogs.technet.com/b/kv/archive/2015/06/02/azure-key-vault-step-by-step.aspx).</span></span> <span data-ttu-id="89e6a-404">Voici comment exécuter cette tâche via PowerShell :</span><span class="sxs-lookup"><span data-stu-id="89e6a-404">Here is an example of how to perform this task via PowerShell:</span></span>

    $keyVaultName = '<yourKeyVaultName>'
    $aadClientID = '<yourAadAppClientID>'
    $rgname = '<yourResourceGroup>'
    Set-AzureRmKeyVaultAccessPolicy -VaultName $keyVaultName -ServicePrincipalName $aadClientID -PermissionsToKeys 'WrapKey' -PermissionsToSecrets 'Set' -ResourceGroupName $rgname

> [!NOTE]
> <span data-ttu-id="89e6a-405">Azure Disk Encryption requiert de configurer les stratégies d’accès suivantes sur votre application cliente Azure AD : autorisations _WrapKey_ et _Set_.</span><span class="sxs-lookup"><span data-stu-id="89e6a-405">Azure Disk Encryption requires you to configure the following access policies to your Azure AD client application: _WrapKey_ and _Set_ permissions.</span></span>

## <a name="terminology"></a><span data-ttu-id="89e6a-406">Terminologie</span><span class="sxs-lookup"><span data-stu-id="89e6a-406">Terminology</span></span>
<span data-ttu-id="89e6a-407">Reportez-vous au tableau de terminologie suivant pour comprendre certains des termes couramment utilisés par cette technologie :</span><span class="sxs-lookup"><span data-stu-id="89e6a-407">To understand some of the common terms used by this technology, use the following terminology table:</span></span>

| <span data-ttu-id="89e6a-408">Terminologie</span><span class="sxs-lookup"><span data-stu-id="89e6a-408">Terminology</span></span> | <span data-ttu-id="89e6a-409">Définition</span><span class="sxs-lookup"><span data-stu-id="89e6a-409">Definition</span></span> |
| --- | --- |
| <span data-ttu-id="89e6a-410">Azure AD</span><span class="sxs-lookup"><span data-stu-id="89e6a-410">Azure AD</span></span> | <span data-ttu-id="89e6a-411">Azure AD est [Azure Active Directory](https://azure.microsoft.com/documentation/services/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="89e6a-411">Azure AD is [Azure Active Directory](https://azure.microsoft.com/documentation/services/active-directory/).</span></span> <span data-ttu-id="89e6a-412">Un compte Azure AD est requis pour l’authentification, le stockage et l’extraction des clés secrètes d’un coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="89e6a-412">An Azure AD account is a prerequisite for authenticating, storing, and retrieving secrets from a key vault.</span></span> |
| <span data-ttu-id="89e6a-413">coffre de clés Azure</span><span class="sxs-lookup"><span data-stu-id="89e6a-413">Azure Key Vault</span></span> | <span data-ttu-id="89e6a-414">Key Vault est un service de gestion de clés de chiffrement basé sur des modules de sécurité matériels FIPS (Federal Information Processing Standards) qui vous permet de protéger vos clés de chiffrement et les clés secrètes sensibles.</span><span class="sxs-lookup"><span data-stu-id="89e6a-414">Key Vault is a cryptographic, key management service that's based on Federal Information Processing Standards (FIPS)-validated hardware security modules, which help safeguard your cryptographic keys and sensitive secrets.</span></span> <span data-ttu-id="89e6a-415">Pour plus d’informations, consultez la documentation relative à [Key Vault](https://azure.microsoft.com/services/key-vault/).</span><span class="sxs-lookup"><span data-stu-id="89e6a-415">For more information, see [Key Vault](https://azure.microsoft.com/services/key-vault/) documentation.</span></span> |
| <span data-ttu-id="89e6a-416">ARM</span><span class="sxs-lookup"><span data-stu-id="89e6a-416">ARM</span></span> | <span data-ttu-id="89e6a-417">Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="89e6a-417">Azure Resource Manager</span></span> |
| <span data-ttu-id="89e6a-418">BitLocker</span><span class="sxs-lookup"><span data-stu-id="89e6a-418">BitLocker</span></span> |<span data-ttu-id="89e6a-419">[BitLocker](https://technet.microsoft.com/library/hh831713.aspx) est une technologie de chiffrement de volume Windows qui permet d’activer le chiffrement de disque sur des machines virtuelles IaaS Windows.</span><span class="sxs-lookup"><span data-stu-id="89e6a-419">[BitLocker](https://technet.microsoft.com/library/hh831713.aspx) is an industry-recognized Windows volume encryption technology that's used to enable disk encryption on Windows IaaS VMs.</span></span> |
| <span data-ttu-id="89e6a-420">BEK</span><span class="sxs-lookup"><span data-stu-id="89e6a-420">BEK</span></span> | <span data-ttu-id="89e6a-421">Les clés de chiffrement BitLocker servent à chiffrer le volume de démarrage du système d’exploitation et les volumes de données.</span><span class="sxs-lookup"><span data-stu-id="89e6a-421">BitLocker encryption keys are used to encrypt the OS boot volume and data volumes.</span></span> <span data-ttu-id="89e6a-422">Les clés BitLocker sont sauvegardées dans un coffre de clés en tant que clés secrètes.</span><span class="sxs-lookup"><span data-stu-id="89e6a-422">The BitLocker keys are safeguarded in a key vault as secrets.</span></span> |
| <span data-ttu-id="89e6a-423">Interface de ligne de commande</span><span class="sxs-lookup"><span data-stu-id="89e6a-423">CLI</span></span> | <span data-ttu-id="89e6a-424">Voir [Interface de ligne de commande Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="89e6a-424">See [Azure command-line interface](../cli-install-nodejs.md).</span></span> |
| <span data-ttu-id="89e6a-425">DM-Crypt</span><span class="sxs-lookup"><span data-stu-id="89e6a-425">DM-Crypt</span></span> |<span data-ttu-id="89e6a-426">[DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) est le sous-système de chiffrement de disque transparent Linux utilisé pour activer le chiffrement de disque sur les machines virtuelles IaaS Linux.</span><span class="sxs-lookup"><span data-stu-id="89e6a-426">[DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) is the Linux-based, transparent disk-encryption subsystem that's used to enable disk encryption on Linux IaaS VMs.</span></span> |
| <span data-ttu-id="89e6a-427">KEK</span><span class="sxs-lookup"><span data-stu-id="89e6a-427">KEK</span></span> | <span data-ttu-id="89e6a-428">La clé de chiffrement à clé est la clé asymétrique (RSA 2048) que vous pouvez utiliser pour protéger ou encapsuler la clé secrète.</span><span class="sxs-lookup"><span data-stu-id="89e6a-428">Key encryption key is the asymmetric key (RSA 2048) that you can use to protect or wrap the secret.</span></span> <span data-ttu-id="89e6a-429">Vous pouvez fournir une clé protégée par le module HSM ou une clé protégée par le logiciel.</span><span class="sxs-lookup"><span data-stu-id="89e6a-429">You can provide a hardware security modules (HSM)-protected key or software-protected key.</span></span> <span data-ttu-id="89e6a-430">Pour plus d’informations, consultez la documentation relative à [Azure Key Vault](https://azure.microsoft.com/services/key-vault/).</span><span class="sxs-lookup"><span data-stu-id="89e6a-430">For more details, see [Azure Key Vault](https://azure.microsoft.com/services/key-vault/) documentation.</span></span> |
| <span data-ttu-id="89e6a-431">Applets de commande PS</span><span class="sxs-lookup"><span data-stu-id="89e6a-431">PS cmdlets</span></span> | <span data-ttu-id="89e6a-432">Voir [Applets de commande Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="89e6a-432">See [Azure PowerShell cmdlets](/powershell/azure/overview).</span></span> |

### <a name="set-up-and-configure-your-key-vault-for-azure-disk-encryption"></a><span data-ttu-id="89e6a-433">Créer et configurer votre coffre de clés pour Azure Disk Encryption</span><span class="sxs-lookup"><span data-stu-id="89e6a-433">Set up and configure your key vault for Azure Disk Encryption</span></span>
<span data-ttu-id="89e6a-434">Azure Disk Encryption protège les clés et les clés secrètes de chiffrement dans votre coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="89e6a-434">Azure Disk Encryption helps safeguard the disk-encryption keys and secrets in your key vault.</span></span> <span data-ttu-id="89e6a-435">Pour configurer votre coffre de clés pour Azure Disk Encryption, suivez les étapes de chacune des sections suivantes.</span><span class="sxs-lookup"><span data-stu-id="89e6a-435">To set up your key vault for Azure Disk Encryption, complete the steps in each of the following sections.</span></span>

#### <a name="create-a-key-vault"></a><span data-ttu-id="89e6a-436">Création d’un coffre de clés</span><span class="sxs-lookup"><span data-stu-id="89e6a-436">Create a key vault</span></span>
<span data-ttu-id="89e6a-437">Pour créer un coffre de clés, utilisez l’une des options suivantes :</span><span class="sxs-lookup"><span data-stu-id="89e6a-437">To create a key vault, use one of the following options:</span></span>

* [<span data-ttu-id="89e6a-438">Modèle Resource Manager « 101-Key-Vault-Create »</span><span class="sxs-lookup"><span data-stu-id="89e6a-438">"101-Key-Vault-Create" Resource Manager template</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-key-vault-create)
* [<span data-ttu-id="89e6a-439">Applets de commande Key Vault Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="89e6a-439">Azure PowerShell key vault cmdlets</span></span>](/powershell/module/azurerm.keyvault/#key_vault)
* <span data-ttu-id="89e6a-440">Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="89e6a-440">Azure Resource Manager</span></span>
* <span data-ttu-id="89e6a-441">Comment [Sécuriser votre coffre de clés](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-secure-your-key-vault)</span><span class="sxs-lookup"><span data-stu-id="89e6a-441">How to [Secure your key vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-secure-your-key-vault)</span></span>

> [!NOTE]
> <span data-ttu-id="89e6a-442">Si vous avez déjà configuré un coffre de clés pour votre abonnement, passez à la section suivante.</span><span class="sxs-lookup"><span data-stu-id="89e6a-442">If you have already set up a key vault for your subscription, skip to the next section.</span></span>

![coffre de clés Azure](./media/azure-security-disk-encryption/keyvault-portal-fig1.png)

#### <a name="set-up-a-key-encryption-key-optional"></a><span data-ttu-id="89e6a-444">Configurer une clé de chiffrement à clé (facultatif)</span><span class="sxs-lookup"><span data-stu-id="89e6a-444">Set up a key encryption key (optional)</span></span>
<span data-ttu-id="89e6a-445">Si vous souhaitez utiliser une clé de chiffrement à clé pour renforcer la protection des clés de chiffrement BitLocker, ajoutez une clé de chiffrement à clé à votre coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="89e6a-445">If you want to use a KEK for an additional layer of security for the BitLocker encryption keys, add a KEK to your key vault.</span></span> <span data-ttu-id="89e6a-446">Utilisez l’applet de commande [`Add-AzureKeyVaultKey`](/powershell/module/azurerm.keyvault/add-azurermkeyvaultkey) pour créer une clé de chiffrement à clé dans le coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="89e6a-446">Use the [`Add-AzureKeyVaultKey`](/powershell/module/azurerm.keyvault/add-azurermkeyvaultkey) cmdlet to create a key encryption key in the key vault.</span></span> <span data-ttu-id="89e6a-447">Vous pouvez également importer une clé de chiffrement à clé à partir de votre module de sécurité matériel de gestion des clés locales.</span><span class="sxs-lookup"><span data-stu-id="89e6a-447">You can also import a KEK from your on-premises key management HSM.</span></span> <span data-ttu-id="89e6a-448">Pour plus d’informations, consultez la [Documentation relative à Key Vault](https://azure.microsoft.com/documentation/services/key-vault/).</span><span class="sxs-lookup"><span data-stu-id="89e6a-448">For more details, see [Key Vault Documentation](https://azure.microsoft.com/documentation/services/key-vault/).</span></span>

    Add-AzureKeyVaultKey [-VaultName] <string> [-Name] <string> -Destination <string> {HSM | Software}

<span data-ttu-id="89e6a-449">Vous pouvez ajouter la clé de chiffrement à clé via Azure Resource Manager ou l’interface de votre coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="89e6a-449">You can add the KEK by going to Azure Resource Manager or by using your key vault interface.</span></span>

![coffre de clés Azure](./media/azure-security-disk-encryption/keyvault-portal-fig2.png)

#### <a name="set-key-vault-permissions"></a><span data-ttu-id="89e6a-451">Définir des autorisations d’accès au coffre de clés</span><span class="sxs-lookup"><span data-stu-id="89e6a-451">Set key vault permissions</span></span>
<span data-ttu-id="89e6a-452">La plateforme Azure doit avoir accès aux clés et aux clés secrètes de chiffrement dans votre coffre de clés afin de les mettre à disposition de la machine virtuelle pour lancer et déchiffrer les volumes.</span><span class="sxs-lookup"><span data-stu-id="89e6a-452">The Azure platform needs access to the encryption keys or secrets in your key vault to make them available to the VM for booting and decrypting the volumes.</span></span> <span data-ttu-id="89e6a-453">Pour accorder des autorisations d’accès à la plateforme Azure, définissez la propriété **EnabledForDiskEncryption** dans le coffre de clés à l’aide de l’applet de commande de coffre de clés PowerShell suivante :</span><span class="sxs-lookup"><span data-stu-id="89e6a-453">To grant permissions to the Azure platform, set the **EnabledForDiskEncryption** property in the key vault by using the key vault PowerShell cmdlet:</span></span>

    Set-AzureRmKeyVaultAccessPolicy -VaultName <yourVaultName> -ResourceGroupName <yourResourceGroup> -EnabledForDiskEncryption

<span data-ttu-id="89e6a-454">Vous pouvez également définir la propriété **EnabledForDiskEncryption** en accédant à [l’Explorateur de ressources Azure](https://resources.azure.com).</span><span class="sxs-lookup"><span data-stu-id="89e6a-454">You can also set the **EnabledForDiskEncryption** property by visiting the [Azure Resource Explorer](https://resources.azure.com).</span></span>

<span data-ttu-id="89e6a-455">Comme indiqué précédemment, vous devez définir la propriété **EnabledForDiskEncryption** dans votre coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="89e6a-455">As mentioned earlier, you must set the **EnabledForDiskEncryption** property on your key vault.</span></span> <span data-ttu-id="89e6a-456">Si ce n'est pas le cas, le déploiement échouera.</span><span class="sxs-lookup"><span data-stu-id="89e6a-456">Otherwise, the deployment will fail.</span></span>

<span data-ttu-id="89e6a-457">Vous pouvez configurer des stratégies d’accès pour votre application Azure AD à partir de l’interface du coffre de clés, comme indiqué ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="89e6a-457">You can set up access policies for your Azure AD application from the key vault interface, as shown here:</span></span>

![coffre de clés Azure](./media/azure-security-disk-encryption/keyvault-portal-fig3.png)

![coffre de clés Azure](./media/azure-security-disk-encryption/keyvault-portal-fig3b.png)

<span data-ttu-id="89e6a-460">Dans l’onglet **Stratégies d’accès avancées**, assurez-vous que votre coffre de clés est activé pour Azure Disk Encryption :</span><span class="sxs-lookup"><span data-stu-id="89e6a-460">On the **Advanced access policies** tab, make sure that your key vault is enabled for Azure Disk Encryption:</span></span>

![Coffre de clés Azure](./media/azure-security-disk-encryption/keyvault-portal-fig4.png)

## <a name="disk-encryption-deployment-scenarios-and-user-experiences"></a><span data-ttu-id="89e6a-462">Scénarios de déploiement de chiffrement de disque et expériences utilisateur</span><span class="sxs-lookup"><span data-stu-id="89e6a-462">Disk-encryption deployment scenarios and user experiences</span></span>
<span data-ttu-id="89e6a-463">Il existe de nombreux scénarios permettant d’activer le chiffrement de disque et les étapes peuvent varier selon le scénario.</span><span class="sxs-lookup"><span data-stu-id="89e6a-463">You can enable many disk-encryption scenarios, and the steps may vary according to the scenario.</span></span> <span data-ttu-id="89e6a-464">Les sections suivantes décrivent ces scénarios de manière plus détaillée.</span><span class="sxs-lookup"><span data-stu-id="89e6a-464">The following sections cover the scenarios in greater detail.</span></span>

### <a name="enable-encryption-on-new-iaas-vms-that-are-created-from-the-marketplace"></a><span data-ttu-id="89e6a-465">Activation du chiffrement sur de nouvelles machines virtuelles IaaS créées à partir de la Place de marché</span><span class="sxs-lookup"><span data-stu-id="89e6a-465">Enable encryption on new IaaS VMs that are created from the Marketplace</span></span>
<span data-ttu-id="89e6a-466">Vous pouvez activer le chiffrement de disque sur de nouvelles machines virtuelles IaaS Windows à partir de la Place de marché Azure à l’aide du [modèle Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-new-vm-gallery-image).</span><span class="sxs-lookup"><span data-stu-id="89e6a-466">You can enable disk encryption on new IaaS Windows VM from the Marketplace in Azure by using the  [Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-new-vm-gallery-image).</span></span>

1. <span data-ttu-id="89e6a-467">Dans le modèle de démarrage rapide Azure, cliquez sur **Déployer sur Azure**, saisissez la configuration de chiffrement dans le panneau **Paramètres**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="89e6a-467">On the Azure quick-start template, click **Deploy to Azure**, enter the encryption configuration on the **Parameters** blade, and then click **OK**.</span></span>

2. <span data-ttu-id="89e6a-468">Sélectionnez l’abonnement, le groupe de ressources, l’emplacement du groupe de ressources, les conditions juridiques et les accords, puis cliquez sur **Créer** pour activer le chiffrement sur une nouvelle machine virtuelle IaaS.</span><span class="sxs-lookup"><span data-stu-id="89e6a-468">Select the subscription, resource group, resource group location, legal terms, and agreement, and then click **Create** to enable encryption on a new IaaS VM.</span></span>

> [!NOTE]
> <span data-ttu-id="89e6a-469">Ce modèle crée une machine virtuelle Windows chiffrée qui utilise l’image de la galerie Windows Server 2012.</span><span class="sxs-lookup"><span data-stu-id="89e6a-469">This template creates a new encrypted Windows VM that uses the Windows Server 2012 gallery image.</span></span>

<span data-ttu-id="89e6a-470">Vous pouvez activer le chiffrement de disque sur une nouvelle machine virtuelle IaaS RedHat Linux 7.2 avec une baie RAID-0 de 200 Go à l’aide de ce [modèle Resource Manager](https://aka.ms/fde-rhel).</span><span class="sxs-lookup"><span data-stu-id="89e6a-470">You can enable disk encryption on a new IaaS RedHat Linux 7.2 VM with a 200-GB RAID-0 array by using this [Resource Manager template](https://aka.ms/fde-rhel).</span></span> <span data-ttu-id="89e6a-471">Une fois que le modèle est déployé, vérifiez l’état du chiffrement de la machine virtuelle à l’aide de l’applet de commande `Get-AzureRmVmDiskEncryptionStatus` comme décrit dans la section [Chiffrement du lecteur du système d’exploitation sur une machine virtuelle Linux en cours d’exécution](#encrypting-os-drive-on-a-running-linux-vm).</span><span class="sxs-lookup"><span data-stu-id="89e6a-471">After you deploy the template, verify the VM encryption status by using the `Get-AzureRmVmDiskEncryptionStatus` cmdlet, as described in [Encrypting OS drive on a running Linux VM](#encrypting-os-drive-on-a-running-linux-vm).</span></span> <span data-ttu-id="89e6a-472">Lorsque la machine retourne l’état _VMRestartPending_, redémarrez la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="89e6a-472">When the machine returns a status of _VMRestartPending_, restart the VM.</span></span>

<span data-ttu-id="89e6a-473">Le tableau suivant répertorie les paramètres du modèle Resource Manager pour les nouvelles machines virtuelles dans un scénario Place de marche utilisant l’ID de client Azure AD :</span><span class="sxs-lookup"><span data-stu-id="89e6a-473">The following table lists the Resource Manager template parameters for new VMs from the Marketplace scenario using Azure AD client ID:</span></span>

| <span data-ttu-id="89e6a-474">Paramètre</span><span class="sxs-lookup"><span data-stu-id="89e6a-474">Parameter</span></span> | <span data-ttu-id="89e6a-475">Description</span><span class="sxs-lookup"><span data-stu-id="89e6a-475">Description</span></span> |
| --- | --- |
| <span data-ttu-id="89e6a-476">adminUsername</span><span class="sxs-lookup"><span data-stu-id="89e6a-476">adminUserName</span></span> | <span data-ttu-id="89e6a-477">Nom de l’utilisateur administrateur de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="89e6a-477">Admin user name for the virtual machine.</span></span> |
| <span data-ttu-id="89e6a-478">adminPassword</span><span class="sxs-lookup"><span data-stu-id="89e6a-478">adminPassword</span></span> | <span data-ttu-id="89e6a-479">Mot de passe de l’utilisateur administrateur de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="89e6a-479">Admin user password for the virtual machine.</span></span> |
| <span data-ttu-id="89e6a-480">newStorageAccountName</span><span class="sxs-lookup"><span data-stu-id="89e6a-480">newStorageAccountName</span></span> | <span data-ttu-id="89e6a-481">Nom du compte de stockage pour stocker les disques durs virtuels du système d’exploitation et de données.</span><span class="sxs-lookup"><span data-stu-id="89e6a-481">Name of the storage account to store OS and data VHDs.</span></span> |
| <span data-ttu-id="89e6a-482">vmSize</span><span class="sxs-lookup"><span data-stu-id="89e6a-482">vmSize</span></span> | <span data-ttu-id="89e6a-483">Taille de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="89e6a-483">Size of the VM.</span></span> <span data-ttu-id="89e6a-484">Actuellement, seules les séries A, D et G standard sont prises en charge.</span><span class="sxs-lookup"><span data-stu-id="89e6a-484">Currently, only Standard A, D, and G series are supported.</span></span> |
| <span data-ttu-id="89e6a-485">virtualNetworkName</span><span class="sxs-lookup"><span data-stu-id="89e6a-485">virtualNetworkName</span></span> | <span data-ttu-id="89e6a-486">Nom du réseau virtuel auquel la carte d’interface réseau de machine virtuelle appartient.</span><span class="sxs-lookup"><span data-stu-id="89e6a-486">Name of the VNet that the VM NIC should belong to.</span></span> |
| <span data-ttu-id="89e6a-487">subnetName</span><span class="sxs-lookup"><span data-stu-id="89e6a-487">subnetName</span></span> | <span data-ttu-id="89e6a-488">Nom du sous-réseau du réseau virtuel auquel la carte d’interface réseau de machine virtuelle appartient.</span><span class="sxs-lookup"><span data-stu-id="89e6a-488">Name of the subnet in the VNet that the VM NIC should belong to.</span></span> |
| <span data-ttu-id="89e6a-489">AADClientID</span><span class="sxs-lookup"><span data-stu-id="89e6a-489">AADClientID</span></span> | <span data-ttu-id="89e6a-490">ID de client de l’application Azure AD qui dispose des autorisations pour écrire des clés secrètes dans le coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="89e6a-490">Client ID of the Azure AD application that has permissions to write secrets to your key vault.</span></span> |
| <span data-ttu-id="89e6a-491">AADClientSecret</span><span class="sxs-lookup"><span data-stu-id="89e6a-491">AADClientSecret</span></span> | <span data-ttu-id="89e6a-492">Clé secrète de client de l’application Azure AD qui dispose des autorisations pour écrire des clés secrètes dans le coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="89e6a-492">Client secret of the Azure AD application that has permissions to write secrets to your key vault.</span></span> |
| <span data-ttu-id="89e6a-493">keyVaultURL</span><span class="sxs-lookup"><span data-stu-id="89e6a-493">keyVaultURL</span></span> | <span data-ttu-id="89e6a-494">URL du coffre de clés dans lequel la clé BitLocker doit être téléchargée.</span><span class="sxs-lookup"><span data-stu-id="89e6a-494">URL of the key vault that the BitLocker key should be uploaded to.</span></span> <span data-ttu-id="89e6a-495">Vous pouvez l’obtenir à l’aide de l’applet de commande `(Get-AzureRmKeyVault -VaultName,-ResourceGroupName ).VaultURI`.</span><span class="sxs-lookup"><span data-stu-id="89e6a-495">You can get it by using the cmdlet `(Get-AzureRmKeyVault -VaultName,-ResourceGroupName ).VaultURI`.</span></span> |
| <span data-ttu-id="89e6a-496">keyEncryptionKeyURL</span><span class="sxs-lookup"><span data-stu-id="89e6a-496">keyEncryptionKeyURL</span></span> | <span data-ttu-id="89e6a-497">URL de la clé de chiffrement à clé utilisée pour chiffrer la clé BitLocker générée (facultatif).</span><span class="sxs-lookup"><span data-stu-id="89e6a-497">URL of the key encryption key that's used to encrypt the generated BitLocker key (optional).</span></span> |
| <span data-ttu-id="89e6a-498">keyVaultResourceGroup</span><span class="sxs-lookup"><span data-stu-id="89e6a-498">keyVaultResourceGroup</span></span> | <span data-ttu-id="89e6a-499">Groupe de ressources du coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="89e6a-499">Resource group of the key vault.</span></span> |
| <span data-ttu-id="89e6a-500">vmName</span><span class="sxs-lookup"><span data-stu-id="89e6a-500">vmName</span></span> | <span data-ttu-id="89e6a-501">Nom de la machine virtuelle sur laquelle l’opération de chiffrement doit être effectuée.</span><span class="sxs-lookup"><span data-stu-id="89e6a-501">Name of the VM that the encryption operation is to be performed on.</span></span> |

> [!NOTE]
> <span data-ttu-id="89e6a-502">_KeyEncryptionKeyURL_ est un paramètre facultatif.</span><span class="sxs-lookup"><span data-stu-id="89e6a-502">_KeyEncryptionKeyURL_ is an optional parameter.</span></span> <span data-ttu-id="89e6a-503">Vous pouvez apporter vos propres clés de chiffrement à clé (KEK) pour renforcer la clé de chiffrement des données (clé secrète de chiffrement) dans votre coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="89e6a-503">You can bring your own KEK to further safeguard the data encryption key (Passphrase secret) in your key vault.</span></span>

### <a name="enable-encryption-on-new-iaas-vms-that-are-created-from-customer-encrypted-vhd-and-encryption-keys"></a><span data-ttu-id="89e6a-504">Activation du chiffrement sur de nouvelles machines virtuelles IaaS créées à partir de disques durs virtuels chiffrés par le client et de clés de chiffrement</span><span class="sxs-lookup"><span data-stu-id="89e6a-504">Enable encryption on new IaaS VMs that are created from customer-encrypted VHD and encryption keys</span></span>
<span data-ttu-id="89e6a-505">Dans ce scénario, vous pouvez activer le chiffrement à l’aide du modèle Resource Manager, des applets de commande PowerShell ou des commandes CLI.</span><span class="sxs-lookup"><span data-stu-id="89e6a-505">In this scenario, you can enable encrypting by using the Resource Manager template, PowerShell cmdlets, or CLI commands.</span></span> <span data-ttu-id="89e6a-506">Les sections ci-dessous décrivent de façon plus détaillée le modèle Resource Manager et les commandes CLI.</span><span class="sxs-lookup"><span data-stu-id="89e6a-506">The following sections explain in greater detail the Resource Manager template and CLI commands.</span></span>

<span data-ttu-id="89e6a-507">Suivez les instructions d’une de ces sections pour la préparation d’images déjà chiffrées qui peuvent être utilisées dans Azure.</span><span class="sxs-lookup"><span data-stu-id="89e6a-507">Follow the instructions from one of these sections for preparing pre-encrypted images that can be used in Azure.</span></span> <span data-ttu-id="89e6a-508">Une fois l’image créée, vous pouvez suivre la procédure décrite dans la section suivante pour créer une machine virtuelle Azure chiffrée.</span><span class="sxs-lookup"><span data-stu-id="89e6a-508">After the image is created, you can use the steps in the next section to create an encrypted Azure VM.</span></span>

* [<span data-ttu-id="89e6a-509">Préparer un disque dur virtuel Windows déjà chiffré</span><span class="sxs-lookup"><span data-stu-id="89e6a-509">Prepare a pre-encrypted Windows VHD</span></span>](#preparing-a-pre-encrypted-windows-vhd)
* [<span data-ttu-id="89e6a-510">Préparer un disque dur virtuel Linux déjà chiffré</span><span class="sxs-lookup"><span data-stu-id="89e6a-510">Prepare a pre-encrypted Linux VHD</span></span>](#preparing-a-pre-encrypted-linux-vhd)

#### <a name="using-the-resource-manager-template"></a><span data-ttu-id="89e6a-511">Utilisation du modèle Resource Manager</span><span class="sxs-lookup"><span data-stu-id="89e6a-511">Using the Resource Manager template</span></span>
<span data-ttu-id="89e6a-512">Vous pouvez activer le chiffrement de disque sur votre disque dur virtuel chiffré à l’aide du [modèle Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-pre-encrypted-vm).</span><span class="sxs-lookup"><span data-stu-id="89e6a-512">You can enable disk encryption on your encrypted VHD by using the [Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-pre-encrypted-vm).</span></span>

1. <span data-ttu-id="89e6a-513">Dans le modèle de démarrage rapide Azure, cliquez sur **Déployer sur Azure**, saisissez la configuration de chiffrement dans le panneau **Paramètres**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="89e6a-513">On the Azure quick-start template, click **Deploy to Azure**, enter the encryption configuration on the **Parameters** blade, and then click **OK**.</span></span>

2. <span data-ttu-id="89e6a-514">Sélectionnez l’abonnement, le groupe de ressources, l’emplacement du groupe de ressources, les conditions juridiques et les accords, puis cliquez sur **Créer** pour activer le chiffrement sur la nouvelle machine virtuelle IaaS.</span><span class="sxs-lookup"><span data-stu-id="89e6a-514">Select the subscription, resource group, resource group location, legal terms, and agreement, and then click **Create** to enable encryption on the new IaaS VM.</span></span>

<span data-ttu-id="89e6a-515">Le tableau suivant répertorie les paramètres du modèle Resource Manager pour votre disque dur virtuel chiffré :</span><span class="sxs-lookup"><span data-stu-id="89e6a-515">The following table lists the Resource Manager template parameters for your encrypted VHD:</span></span>

| <span data-ttu-id="89e6a-516">Paramètre</span><span class="sxs-lookup"><span data-stu-id="89e6a-516">Parameter</span></span> | <span data-ttu-id="89e6a-517">Description</span><span class="sxs-lookup"><span data-stu-id="89e6a-517">Description</span></span> |
| --- | --- |
| <span data-ttu-id="89e6a-518">newStorageAccountName</span><span class="sxs-lookup"><span data-stu-id="89e6a-518">newStorageAccountName</span></span> | <span data-ttu-id="89e6a-519">Nom du compte de stockage pour stocker le disque dur virtuel du système d’exploitation chiffré.</span><span class="sxs-lookup"><span data-stu-id="89e6a-519">Name of the storage account to store the encrypted OS VHD.</span></span> <span data-ttu-id="89e6a-520">Ce compte de stockage doit avoir été créé dans le même groupe de ressources et le même emplacement que la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="89e6a-520">This storage account should already have been created in the same resource group and same location as the VM.</span></span> |
| <span data-ttu-id="89e6a-521">osVhdUri</span><span class="sxs-lookup"><span data-stu-id="89e6a-521">osVhdUri</span></span> | <span data-ttu-id="89e6a-522">URI du disque dur virtuel du système d’exploitation à partir du compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="89e6a-522">URI of the OS VHD from the storage account.</span></span> |
| <span data-ttu-id="89e6a-523">osType</span><span class="sxs-lookup"><span data-stu-id="89e6a-523">osType</span></span> | <span data-ttu-id="89e6a-524">Type de système d’exploitation (Windows/Linux).</span><span class="sxs-lookup"><span data-stu-id="89e6a-524">OS product type (Windows/Linux).</span></span> |
| <span data-ttu-id="89e6a-525">virtualNetworkName</span><span class="sxs-lookup"><span data-stu-id="89e6a-525">virtualNetworkName</span></span> | <span data-ttu-id="89e6a-526">Nom du réseau virtuel auquel la carte d’interface réseau de machine virtuelle appartient.</span><span class="sxs-lookup"><span data-stu-id="89e6a-526">Name of the VNet that the VM NIC should belong to.</span></span> <span data-ttu-id="89e6a-527">Le nom doit avoir été créé dans le même groupe de ressources et le même emplacement que la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="89e6a-527">The name should already have been created in the same resource group and same location as the VM.</span></span> |
| <span data-ttu-id="89e6a-528">subnetName</span><span class="sxs-lookup"><span data-stu-id="89e6a-528">subnetName</span></span> | <span data-ttu-id="89e6a-529">Nom du sous-réseau du réseau virtuel auquel la carte d’interface réseau de machine virtuelle appartient.</span><span class="sxs-lookup"><span data-stu-id="89e6a-529">Name of the subnet on the VNet that the VM NIC should belong to.</span></span> |
| <span data-ttu-id="89e6a-530">vmSize</span><span class="sxs-lookup"><span data-stu-id="89e6a-530">vmSize</span></span> | <span data-ttu-id="89e6a-531">Taille de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="89e6a-531">Size of the VM.</span></span> <span data-ttu-id="89e6a-532">Actuellement, seules les séries A, D et G standard sont prises en charge.</span><span class="sxs-lookup"><span data-stu-id="89e6a-532">Currently, only Standard A, D, and G series are supported.</span></span> |
| <span data-ttu-id="89e6a-533">keyVaultResourceID</span><span class="sxs-lookup"><span data-stu-id="89e6a-533">keyVaultResourceID</span></span> | <span data-ttu-id="89e6a-534">L’ID de ressource qui identifie la ressource de coffre de clés dans Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="89e6a-534">The ResourceID that identifies the key vault resource in Azure Resource Manager.</span></span> <span data-ttu-id="89e6a-535">Vous pouvez l’obtenir à l’aide de l’applet de commande PowerShell `(Get-AzureRmKeyVault -VaultName &lt;yourKeyVaultName&gt; -ResourceGroupName &lt;yourResourceGroupName&gt;).ResourceId`.</span><span class="sxs-lookup"><span data-stu-id="89e6a-535">You can get it by using the PowerShell cmdlet `(Get-AzureRmKeyVault -VaultName &lt;yourKeyVaultName&gt; -ResourceGroupName &lt;yourResourceGroupName&gt;).ResourceId`.</span></span> |
| <span data-ttu-id="89e6a-536">keyVaultSecretUrl</span><span class="sxs-lookup"><span data-stu-id="89e6a-536">keyVaultSecretUrl</span></span> | <span data-ttu-id="89e6a-537">URL de la clé de chiffrement de disque définie dans le coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="89e6a-537">URL of the disk-encryption key that's set up in the key vault.</span></span> |
| <span data-ttu-id="89e6a-538">keyVaultKekUrl</span><span class="sxs-lookup"><span data-stu-id="89e6a-538">keyVaultKekUrl</span></span> | <span data-ttu-id="89e6a-539">URL de la clé de chiffrement à clé utilisée pour chiffrer la clé de chiffrement de disque générée.</span><span class="sxs-lookup"><span data-stu-id="89e6a-539">URL of the key encryption key for encrypting the generated disk-encryption key.</span></span> |
| <span data-ttu-id="89e6a-540">vmName</span><span class="sxs-lookup"><span data-stu-id="89e6a-540">vmName</span></span> | <span data-ttu-id="89e6a-541">Nom de la machine virtuelle IaaS.</span><span class="sxs-lookup"><span data-stu-id="89e6a-541">Name of the IaaS VM.</span></span> |

#### <a name="using-powershell-cmdlets"></a><span data-ttu-id="89e6a-542">Utilisation d’applets de commande PowerShell</span><span class="sxs-lookup"><span data-stu-id="89e6a-542">Using PowerShell cmdlets</span></span>
<span data-ttu-id="89e6a-543">Vous pouvez activer le chiffrement de disque sur votre disque dur virtuel chiffré à l’aide de l’applet de commande PowerShell [`Set-AzureRmVMOSDisk`](/powershell/module/azurerm.compute/set-azurermvmosdisk).</span><span class="sxs-lookup"><span data-stu-id="89e6a-543">You can enable disk encryption on your encrypted VHD by using the PowerShell cmdlet [`Set-AzureRmVMOSDisk`](/powershell/module/azurerm.compute/set-azurermvmosdisk).</span></span>  

#### <a name="using-cli-commands"></a><span data-ttu-id="89e6a-544">Utilisation des commandes CLI</span><span class="sxs-lookup"><span data-stu-id="89e6a-544">Using CLI commands</span></span>
<span data-ttu-id="89e6a-545">Pour activer le chiffrement de disque de ce scénario à l’aide des commandes CLI, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="89e6a-545">To enable disk encryption for this scenario by using CLI commands, do the following:</span></span>

1. <span data-ttu-id="89e6a-546">Définissez des stratégies d’accès dans votre coffre de clés :</span><span class="sxs-lookup"><span data-stu-id="89e6a-546">Set access policies in your key vault:</span></span>

   * <span data-ttu-id="89e6a-547">Définissez l’indicateur **EnabledForDiskEncryption** :</span><span class="sxs-lookup"><span data-stu-id="89e6a-547">Set the **EnabledForDiskEncryption** flag:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --enabled-for-disk-encryption true`
   * <span data-ttu-id="89e6a-548">Autorisez l’application Azure AD à écrire des clés secrètes dans votre coffre de clés :</span><span class="sxs-lookup"><span data-stu-id="89e6a-548">Set permissions to Azure AD application to write secrets to your key vault:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --spn <aadClientID> --perms-to-keys '["wrapKey"]' --perms-to-secrets '["set"]'`

2. <span data-ttu-id="89e6a-549">Pour activer le chiffrement sur une machine virtuelle existante ou en cours d’exécution, saisissez :</span><span class="sxs-lookup"><span data-stu-id="89e6a-549">To enable encryption on an existing or running VM, type:</span></span>

 `azure vm enable-disk-encryption --resource-group <resourceGroupName> --name <vmName> --aad-client-id <aadClientId> --aad-client-secret <aadClientSecret> --disk-encryption-key-vault-url <keyVaultURL> --disk-encryption-key-vault-id <keyVaultResourceId> --volume-type [All|OS|Data]`

3. <span data-ttu-id="89e6a-550">Obtenez l’état de chiffrement :</span><span class="sxs-lookup"><span data-stu-id="89e6a-550">Get encryption status:</span></span>

 `azure vm show-disk-encryption-status --resource-group <resourceGroupName> --name <vmName> --json`

4. <span data-ttu-id="89e6a-551">Pour activer le chiffrement sur une nouvelle machine virtuelle à partir de votre disque dur virtuel chiffré, utilisez les paramètres suivants avec la commande `azure vm create` :</span><span class="sxs-lookup"><span data-stu-id="89e6a-551">To enable encryption on a new VM from your encrypted VHD, use the following parameters with the `azure vm create` command:</span></span>

 ```
   * disk-encryption-key-vault-id <disk-encryption-key-vault-id>
   * disk-encryption-key-url <disk-encryption-key-url>
   * key-encryption-key-vault-id <key-encryption-key-vault-id>
   * key-encryption-key-url <key-encryption-key-url>
 ```

### <a name="enable-encryption-on-existing-or-running-iaas-windows-vm-in-azure"></a><span data-ttu-id="89e6a-552">Activer le chiffrement sur des machines virtuelles IaaS Windows existantes/en cours de fonctionnement dans Azure</span><span class="sxs-lookup"><span data-stu-id="89e6a-552">Enable encryption on existing or running IaaS Windows VM in Azure</span></span>
<span data-ttu-id="89e6a-553">Dans ce scénario, vous pouvez activer le chiffrement à l’aide du modèle Resource Manager, des applets de commande PowerShell ou des commandes CLI.</span><span class="sxs-lookup"><span data-stu-id="89e6a-553">In this scenario, you can enable encrypting by using the Resource Manager template, PowerShell cmdlets, or CLI commands.</span></span> <span data-ttu-id="89e6a-554">Les sections ci-dessous décrivent de façon plus détaillée comment l’activer à l’aide du modèle Resource Manager et des commandes CLI.</span><span class="sxs-lookup"><span data-stu-id="89e6a-554">The following sections explain in greater detail how to enable it by using the Resource Manager template and CLI commands.</span></span>

#### <a name="using-the-resource-manager-template"></a><span data-ttu-id="89e6a-555">Utilisation du modèle Resource Manager</span><span class="sxs-lookup"><span data-stu-id="89e6a-555">Using the Resource Manager template</span></span>
<span data-ttu-id="89e6a-556">Vous pouvez activer le chiffrement de disque sur des machines virtuelles IaaS Windows existantes ou en cours d’exécution dans Azure à l’aide du [modèle Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-running-windows-vm).</span><span class="sxs-lookup"><span data-stu-id="89e6a-556">You can enable disk encryption on existing or running IaaS Windows VMs in Azure by using the [Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-running-windows-vm).</span></span>

1. <span data-ttu-id="89e6a-557">Dans le modèle de démarrage rapide Azure, cliquez sur **Déployer sur Azure**, saisissez la configuration de chiffrement dans le panneau **Paramètres**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="89e6a-557">On the Azure quick-start template, click **Deploy to Azure**, enter the encryption configuration on the **Parameters** blade, and then click **OK**.</span></span>

2. <span data-ttu-id="89e6a-558">Sélectionnez l’abonnement, le groupe de ressources, l’emplacement du groupe de ressources, les conditions juridiques et les accords, puis cliquez sur **Créer** pour activer le chiffrement sur la machine virtuelle IaaS existante ou en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="89e6a-558">Select the subscription, resource group, resource group location, legal terms, and agreement, and then click **Create** to enable encryption on the existing or running IaaS VM.</span></span>

<span data-ttu-id="89e6a-559">Le tableau suivant répertorie les paramètres du modèle Resource Manager pour les machines virtuelles existantes ou en cours d’exécution qui utilisent un ID de client Azure AD :</span><span class="sxs-lookup"><span data-stu-id="89e6a-559">The following table lists the Resource Manager template parameters for existing or running VMs that use an Azure AD client ID:</span></span>

| <span data-ttu-id="89e6a-560">Paramètre</span><span class="sxs-lookup"><span data-stu-id="89e6a-560">Parameter</span></span> | <span data-ttu-id="89e6a-561">Description</span><span class="sxs-lookup"><span data-stu-id="89e6a-561">Description</span></span> |
| --- | --- |
| <span data-ttu-id="89e6a-562">AADClientID</span><span class="sxs-lookup"><span data-stu-id="89e6a-562">AADClientID</span></span> | <span data-ttu-id="89e6a-563">ID de client de l’application Azure AD qui dispose des autorisations pour écrire des clés secrètes dans le coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="89e6a-563">Client ID of the Azure AD application that has permissions to write secrets to the key vault.</span></span> |
| <span data-ttu-id="89e6a-564">AADClientSecret</span><span class="sxs-lookup"><span data-stu-id="89e6a-564">AADClientSecret</span></span> | <span data-ttu-id="89e6a-565">Clé secrète de client de l’application Azure AD qui dispose des autorisations pour écrire des clés secrètes dans le coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="89e6a-565">Client secret of the Azure AD application that has permissions to write secrets to the key vault.</span></span> |
| <span data-ttu-id="89e6a-566">keyVaultName</span><span class="sxs-lookup"><span data-stu-id="89e6a-566">keyVaultName</span></span> | <span data-ttu-id="89e6a-567">Nom du coffre de clés dans lequel la clé BitLocker doit être téléchargée.</span><span class="sxs-lookup"><span data-stu-id="89e6a-567">Name of the key vault that the BitLocker key should be uploaded to.</span></span> <span data-ttu-id="89e6a-568">Vous pouvez l’obtenir à l’aide de l’applet de commande `(Get-AzureRmKeyVault -ResourceGroupName <yourResourceGroupName>). Vaultname`.</span><span class="sxs-lookup"><span data-stu-id="89e6a-568">You can get it by using the cmdlet `(Get-AzureRmKeyVault -ResourceGroupName <yourResourceGroupName>). Vaultname`.</span></span> |
|  <span data-ttu-id="89e6a-569">keyEncryptionKeyURL</span><span class="sxs-lookup"><span data-stu-id="89e6a-569">keyEncryptionKeyURL</span></span> | <span data-ttu-id="89e6a-570">URL de la clé de chiffrement à clé utilisée pour chiffrer la clé BitLocker générée.</span><span class="sxs-lookup"><span data-stu-id="89e6a-570">URL of the key encryption key that's used to encrypt the generated BitLocker key.</span></span> <span data-ttu-id="89e6a-571">Ce paramètre est facultatif si vous sélectionnez **nokek** dans la liste déroulante UseExistingKek.</span><span class="sxs-lookup"><span data-stu-id="89e6a-571">This parameter is optional if you select **nokek** in the UseExistingKek drop-down list.</span></span> <span data-ttu-id="89e6a-572">Si vous sélectionnez **kek** dans la liste déroulante UseExistingKek, vous devez entrer la valeur _keyEncryptionKeyURL_.</span><span class="sxs-lookup"><span data-stu-id="89e6a-572">If you select **kek** in the UseExistingKek drop-down list, you must enter the _keyEncryptionKeyURL_ value.</span></span> |
| <span data-ttu-id="89e6a-573">volumeType</span><span class="sxs-lookup"><span data-stu-id="89e6a-573">volumeType</span></span> | <span data-ttu-id="89e6a-574">Type de volume sur lequel l’opération de chiffrement est effectuée.</span><span class="sxs-lookup"><span data-stu-id="89e6a-574">Type of volume that the encryption operation is performed on.</span></span> <span data-ttu-id="89e6a-575">Les valeurs valides sont _Système d’exploitation_, _Données_ et _Tous_.</span><span class="sxs-lookup"><span data-stu-id="89e6a-575">Valid values are _OS_, _Data_, and _All_.</span></span> |
| <span data-ttu-id="89e6a-576">sequenceVersion</span><span class="sxs-lookup"><span data-stu-id="89e6a-576">sequenceVersion</span></span> | <span data-ttu-id="89e6a-577">Version de séquence de l’opération BitLocker.</span><span class="sxs-lookup"><span data-stu-id="89e6a-577">Sequence version of the BitLocker operation.</span></span> <span data-ttu-id="89e6a-578">Incrémentez ce numéro de version à chaque fois qu’une opération de chiffrement de disque est exécutée sur la même machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="89e6a-578">Increment this version number every time a disk-encryption operation is performed on the same VM.</span></span> |
| <span data-ttu-id="89e6a-579">vmName</span><span class="sxs-lookup"><span data-stu-id="89e6a-579">vmName</span></span> | <span data-ttu-id="89e6a-580">Nom de la machine virtuelle sur laquelle l’opération de chiffrement doit être effectuée.</span><span class="sxs-lookup"><span data-stu-id="89e6a-580">Name of the VM that the encryption operation is to be performed on.</span></span> |

> [!NOTE]
> <span data-ttu-id="89e6a-581">_KeyEncryptionKeyURL_ est un paramètre facultatif.</span><span class="sxs-lookup"><span data-stu-id="89e6a-581">_KeyEncryptionKeyURL_ is an optional parameter.</span></span> <span data-ttu-id="89e6a-582">Vous pouvez apporter vos propres clés de chiffrement à clé (KEK) pour renforcer la clé de chiffrement des données (clé secrète de chiffrement BitLocker) dans le coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="89e6a-582">You can bring your own KEK to further safeguard the data encryption key (BitLocker encryption secret) in the key vault.</span></span>

#### <a name="using-powershell-cmdlets"></a><span data-ttu-id="89e6a-583">Utilisation d’applets de commande PowerShell</span><span class="sxs-lookup"><span data-stu-id="89e6a-583">Using PowerShell cmdlets</span></span>
<span data-ttu-id="89e6a-584">Pour plus d’informations sur l’activation du chiffrement avec Azure Disk Encryption à l’aide des applets de commande PowerShell, consultez les billets de blog [Explorer Azure Disk Encryption avec Azure PowerShell - partie 1](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/explore-azure-disk-encryption-with-azure-powershell.aspx) et [Explorer Azure Disk Encryption avec Azure PowerShell - partie 2](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx).</span><span class="sxs-lookup"><span data-stu-id="89e6a-584">For information about enabling encryption with Azure Disk Encryption by using PowerShell cmdlets, see the blog posts [Explore Azure Disk Encryption with Azure PowerShell - Part 1](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/explore-azure-disk-encryption-with-azure-powershell.aspx) and [Explore Azure Disk Encryption with Azure PowerShell - Part 2](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx).</span></span>

#### <a name="using-cli-commands"></a><span data-ttu-id="89e6a-585">Utilisation des commandes CLI</span><span class="sxs-lookup"><span data-stu-id="89e6a-585">Using CLI commands</span></span>
<span data-ttu-id="89e6a-586">Pour activer le chiffrement sur des machines virtuelles IaaS Windows existantes ou en cours d’exécution dans Azure à l’aide des commandes CLI, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="89e6a-586">To enable encryption on existing or running IaaS Windows VM in Azure using CLI commands, do the following:</span></span>

1. <span data-ttu-id="89e6a-587">Pour définir des stratégies d’accès dans le coffre de clés :</span><span class="sxs-lookup"><span data-stu-id="89e6a-587">To set access policies in the key vault:</span></span>
   * <span data-ttu-id="89e6a-588">Définissez l’indicateur **EnabledForDiskEncryption** :</span><span class="sxs-lookup"><span data-stu-id="89e6a-588">Set the **EnabledForDiskEncryption** flag:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --enabled-for-disk-encryption true`
   * <span data-ttu-id="89e6a-589">Autorisez l’application Azure AD à écrire des clés secrètes dans votre coffre de clés :</span><span class="sxs-lookup"><span data-stu-id="89e6a-589">Set permissions to Azure AD application to write secrets to your key vault:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --spn <aadClientID> --perms-to-keys '["wrapKey"]' --perms-to-secrets '["set"]'`
2. <span data-ttu-id="89e6a-590">Pour activer le chiffrement sur une machine virtuelle existante ou en cours d’exécution :</span><span class="sxs-lookup"><span data-stu-id="89e6a-590">To enable encryption on an existing or running VM:</span></span>

 `azure vm enable-disk-encryption --resource-group <resourceGroupName> --name <vmName> --aad-client-id <aadClientId> --aad-client-secret <aadClientSecret> --disk-encryption-key-vault-url <keyVaultURL> --disk-encryption-key-vault-id <keyVaultResourceId> --volume-type [All|OS|Data]`
3. <span data-ttu-id="89e6a-591">Pour obtenir l’état de chiffrement :</span><span class="sxs-lookup"><span data-stu-id="89e6a-591">To get encryption status:</span></span>

 `azure vm show-disk-encryption-status --resource-group <resourceGroupName> --name <vmName> --json`
4. <span data-ttu-id="89e6a-592">Pour activer le chiffrement sur une nouvelle machine virtuelle à partir de votre disque dur virtuel chiffré, utilisez les paramètres suivants avec la commande `azure vm create` :</span><span class="sxs-lookup"><span data-stu-id="89e6a-592">To enable encryption on a new VM from your encrypted VHD, use the following parameters with the `azure vm create` command:</span></span>

 ```
   * disk-encryption-key-vault-id <disk-encryption-key-vault-id>
   * disk-encryption-key-url <disk-encryption-key-url>
   * key-encryption-key-vault-id <key-encryption-key-vault-id>
   * key-encryption-key-url <key-encryption-key-url>
 ```

### <a name="enable-encryption-on-an-existing-or-running-iaas-linux-vm-in-azure"></a><span data-ttu-id="89e6a-593">Activer le chiffrement sur une machine virtuelle IaaS Linux existante ou en cours d’exécution dans Azure</span><span class="sxs-lookup"><span data-stu-id="89e6a-593">Enable encryption on an existing or running IaaS Linux VM in Azure</span></span>
<span data-ttu-id="89e6a-594">Vous pouvez activer le chiffrement de disque sur une machine virtuelle IaaS Linux existante ou en cours d’exécution dans Azure à l’aide du [modèle Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-running-linux-vm).</span><span class="sxs-lookup"><span data-stu-id="89e6a-594">You can enable disk encryption on an existing or running IaaS Linux VM in Azure by using the [Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-running-linux-vm).</span></span>

1. <span data-ttu-id="89e6a-595">Cliquez sur **Déployer sur Azure** dans le modèle de démarrage rapide Azure, saisissez la configuration de chiffrement dans le panneau **Paramètres**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="89e6a-595">Click **Deploy to Azure** on the Azure quick-start template, enter the encryption configuration on the **Parameters** blade, and then click **OK**.</span></span>

2. <span data-ttu-id="89e6a-596">Sélectionnez l’abonnement, le groupe de ressources, l’emplacement du groupe de ressources, les conditions juridiques et les accords, puis cliquez sur **Créer** pour activer le chiffrement sur la machine virtuelle IaaS existante ou en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="89e6a-596">Select the subscription, resource group, resource group location, legal terms, and agreement, and then click **Create** to enable encryption on the existing or running IaaS VM.</span></span>

<span data-ttu-id="89e6a-597">Le tableau suivant répertorie les paramètres du modèle Resource Manager pour les machines virtuelles existantes ou en cours d’exécution qui utilisent un ID de client Azure AD :</span><span class="sxs-lookup"><span data-stu-id="89e6a-597">The following table lists Resource Manager template parameters for existing or running VMs that use an Azure AD client ID:</span></span>

| <span data-ttu-id="89e6a-598">Paramètre</span><span class="sxs-lookup"><span data-stu-id="89e6a-598">Parameter</span></span> | <span data-ttu-id="89e6a-599">Description</span><span class="sxs-lookup"><span data-stu-id="89e6a-599">Description</span></span> |
| --- | --- |
| <span data-ttu-id="89e6a-600">AADClientID</span><span class="sxs-lookup"><span data-stu-id="89e6a-600">AADClientID</span></span> | <span data-ttu-id="89e6a-601">ID de client de l’application Azure AD qui dispose des autorisations pour écrire des clés secrètes dans le coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="89e6a-601">Client ID of the Azure AD application that has permissions to write secrets to the key vault.</span></span> |
| <span data-ttu-id="89e6a-602">AADClientSecret</span><span class="sxs-lookup"><span data-stu-id="89e6a-602">AADClientSecret</span></span> | <span data-ttu-id="89e6a-603">Clé secrète de client de l’application Azure AD qui dispose des autorisations pour écrire des clés secrètes dans le coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="89e6a-603">Client secret of the Azure AD application that has permissions to write secrets to your key vault.</span></span> |
| <span data-ttu-id="89e6a-604">keyVaultName</span><span class="sxs-lookup"><span data-stu-id="89e6a-604">keyVaultName</span></span> | <span data-ttu-id="89e6a-605">Nom du coffre de clés dans lequel la clé BitLocker doit être téléchargée.</span><span class="sxs-lookup"><span data-stu-id="89e6a-605">Name of the key vault that the BitLocker key should be uploaded to.</span></span> <span data-ttu-id="89e6a-606">Vous pouvez l’obtenir à l’aide de l’applet de commande `(Get-AzureRmKeyVault -ResourceGroupName <yourResourceGroupName>). Vaultname`.</span><span class="sxs-lookup"><span data-stu-id="89e6a-606">You can get it by using the cmdlet `(Get-AzureRmKeyVault -ResourceGroupName <yourResourceGroupName>). Vaultname`.</span></span> |
|  <span data-ttu-id="89e6a-607">keyEncryptionKeyURL</span><span class="sxs-lookup"><span data-stu-id="89e6a-607">keyEncryptionKeyURL</span></span> | <span data-ttu-id="89e6a-608">URL de la clé de chiffrement à clé utilisée pour chiffrer la clé BitLocker générée.</span><span class="sxs-lookup"><span data-stu-id="89e6a-608">URL of the key encryption key that's used to encrypt the generated BitLocker key.</span></span> <span data-ttu-id="89e6a-609">Ce paramètre est facultatif si vous sélectionnez **nokek** dans la liste déroulante UseExistingKek.</span><span class="sxs-lookup"><span data-stu-id="89e6a-609">This parameter is optional if you select **nokek** in the UseExistingKek drop-down list.</span></span> <span data-ttu-id="89e6a-610">Si vous sélectionnez **kek** dans la liste déroulante UseExistingKek, vous devez entrer la valeur _keyEncryptionKeyURL_.</span><span class="sxs-lookup"><span data-stu-id="89e6a-610">If you select **kek** in the UseExistingKek drop-down list, you must enter the _keyEncryptionKeyURL_ value.</span></span> |
| <span data-ttu-id="89e6a-611">volumeType</span><span class="sxs-lookup"><span data-stu-id="89e6a-611">volumeType</span></span> | <span data-ttu-id="89e6a-612">Type de volume sur lequel l’opération de chiffrement est effectuée.</span><span class="sxs-lookup"><span data-stu-id="89e6a-612">Type of volume that the encryption operation is performed on.</span></span> <span data-ttu-id="89e6a-613">Les valeurs valides prises en charge sont _Système d’exploitation_ ou _Tous_ (pour RHEL 7.2, CentOS 7.2 et Ubuntu 16.04) et _Données_ (pour toutes les autres distributions).</span><span class="sxs-lookup"><span data-stu-id="89e6a-613">Valid supported values are _OS_ or _All_ (for RHEL 7.2, CentOS 7.2, and Ubuntu 16.04), and _Data_ (for all other distributions).</span></span> |
| <span data-ttu-id="89e6a-614">sequenceVersion</span><span class="sxs-lookup"><span data-stu-id="89e6a-614">sequenceVersion</span></span> | <span data-ttu-id="89e6a-615">Version de séquence de l’opération BitLocker.</span><span class="sxs-lookup"><span data-stu-id="89e6a-615">Sequence version of the BitLocker operation.</span></span> <span data-ttu-id="89e6a-616">Incrémentez ce numéro de version à chaque fois qu’une opération de chiffrement de disque est exécutée sur la même machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="89e6a-616">Increment this version number every time a disk-encryption operation is performed on the same VM.</span></span> |
| <span data-ttu-id="89e6a-617">vmName</span><span class="sxs-lookup"><span data-stu-id="89e6a-617">vmName</span></span> | <span data-ttu-id="89e6a-618">Nom de la machine virtuelle sur laquelle l’opération de chiffrement doit être effectuée.</span><span class="sxs-lookup"><span data-stu-id="89e6a-618">Name of the VM that the encryption operation is to be performed on.</span></span> |
| <span data-ttu-id="89e6a-619">passPhrase</span><span class="sxs-lookup"><span data-stu-id="89e6a-619">passPhrase</span></span> | <span data-ttu-id="89e6a-620">Saisissez une phrase secrète forte comme clé de chiffrement de données.</span><span class="sxs-lookup"><span data-stu-id="89e6a-620">Type a strong passphrase as the data encryption key.</span></span> |

> [!NOTE]
> <span data-ttu-id="89e6a-621">_KeyEncryptionKeyURL_ est un paramètre facultatif.</span><span class="sxs-lookup"><span data-stu-id="89e6a-621">_KeyEncryptionKeyURL_ is an optional parameter.</span></span> <span data-ttu-id="89e6a-622">Vous pouvez apporter vos propres clés de chiffrement à clé (KEK) pour renforcer la clé de chiffrement des données (clé secrète de chiffrement) dans votre coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="89e6a-622">You can bring your own KEK to further safeguard the data encryption key (passphrase secret) in your key vault.</span></span>

#### <a name="cli-commands"></a><span data-ttu-id="89e6a-623">Commandes CLI</span><span class="sxs-lookup"><span data-stu-id="89e6a-623">CLI commands</span></span>
<span data-ttu-id="89e6a-624">Vous pouvez activer le chiffrement de disque sur votre disque dur virtuel chiffré en installant et en utilisant les [commandes CLI](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="89e6a-624">You can enable disk encryption on your encrypted VHD by installing and using the [CLI command](../cli-install-nodejs.md).</span></span> <span data-ttu-id="89e6a-625">Pour activer le chiffrement sur des machines virtuelles IaaS Linux existantes ou en cours d’exécution dans Azure à l’aide des commandes CLI, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="89e6a-625">To enable encryption on existing or running IaaS Linux VMs in Azure by using CLI commands, do the following:</span></span>

1. <span data-ttu-id="89e6a-626">Définissez des stratégies d’accès dans le coffre de clés :</span><span class="sxs-lookup"><span data-stu-id="89e6a-626">Set access policies in the key vault:</span></span>

 * <span data-ttu-id="89e6a-627">Définissez l’indicateur **EnabledForDiskEncryption** :</span><span class="sxs-lookup"><span data-stu-id="89e6a-627">Set the **EnabledForDiskEncryption** flag:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --enabled-for-disk-encryption true`
 * <span data-ttu-id="89e6a-628">Autorisez l’application Azure AD à écrire des clés secrètes dans votre coffre de clés :</span><span class="sxs-lookup"><span data-stu-id="89e6a-628">Set permissions to Azure AD application to write secrets to your key vault:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --spn <aadClientID> --perms-to-keys '["wrapKey"]' --perms-to-secrets '["set"]'`

2. <span data-ttu-id="89e6a-629">Pour activer le chiffrement sur une machine virtuelle existante ou en cours d’exécution :</span><span class="sxs-lookup"><span data-stu-id="89e6a-629">To enable encryption on an existing or running VM:</span></span>

 `azure vm enable-disk-encryption --resource-group <resourceGroupName> --name <vmName> --aad-client-id <aadClientId> --aad-client-secret <aadClientSecret> --disk-encryption-key-vault-url <keyVaultURL> --disk-encryption-key-vault-id <keyVaultResourceId> --volume-type [All|OS|Data]`

3. <span data-ttu-id="89e6a-630">Obtenez l’état de chiffrement :</span><span class="sxs-lookup"><span data-stu-id="89e6a-630">Get encryption status:</span></span>

 `azure vm show-disk-encryption-status --resource-group <resourceGroupName> --name <vmName> --json`

4. <span data-ttu-id="89e6a-631">Pour activer le chiffrement sur une nouvelle machine virtuelle à partir de votre disque dur virtuel chiffré, utilisez les paramètres suivants avec la commande `azure vm create` :</span><span class="sxs-lookup"><span data-stu-id="89e6a-631">To enable encryption on a new VM from your encrypted VHD, use the following parameters with the `azure vm create` command:</span></span>
 ```
   * disk-encryption-key-vault-id <disk-encryption-key-vault-id>
   * disk-encryption-key-url <disk-encryption-key-url>
   * key-encryption-key-vault-id <key-encryption-key-vault-id>
   * key-encryption-key-url <key-encryption-key-url>
 ```

### <a name="get-the-encryption-status-of-an-encrypted-iaas-vm"></a><span data-ttu-id="89e6a-632">Obtenir l’état de chiffrement d’une machine virtuelle IaaS chiffrée</span><span class="sxs-lookup"><span data-stu-id="89e6a-632">Get the encryption status of an encrypted IaaS VM</span></span>
<span data-ttu-id="89e6a-633">Vous pouvez obtenir l’état de chiffrement en utilisant Azure Resource Manager, des [applets de commande PowerShell](/powershell/azure/overview) ou des commandes CLI.</span><span class="sxs-lookup"><span data-stu-id="89e6a-633">You can get the encryption status by using Azure Resource Manager, [PowerShell cmdlets](/powershell/azure/overview), or CLI commands.</span></span> <span data-ttu-id="89e6a-634">Les sections ci-dessous expliquent comment utiliser le portail Azure Classic et les commandes de l’interface de ligne de commande pour obtenir l’état de chiffrement.</span><span class="sxs-lookup"><span data-stu-id="89e6a-634">The following sections explain how to use the Azure classic portal and CLI commands to get the encryption status.</span></span>

#### <a name="get-the-encryption-status-of-an-encrypted-windows-vm-by-using-azure-resource-manager"></a><span data-ttu-id="89e6a-635">Obtenir l’état de chiffrement d’une machine virtuelle Windows chiffrée à l’aide d’Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="89e6a-635">Get the encryption status of an encrypted Windows VM by using Azure Resource Manager</span></span>
<span data-ttu-id="89e6a-636">Pour obtenir l’état de chiffrement de la machine virtuelle IaaS à partir d’Azure Resource Manager, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="89e6a-636">You can get the encryption status of the IaaS VM from Azure Resource Manager by doing the following:</span></span>

1. <span data-ttu-id="89e6a-637">Connectez-vous au [portail Azure Classic](https://portal.azure.com/), puis cliquez sur **Machines virtuelles** dans le volet gauche pour afficher un récapitulatif des machines virtuelles de votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="89e6a-637">Sign in to the [Azure classic portal](https://portal.azure.com/), and then click **Virtual machines** in the left pane to see a summary view of the virtual machines in your subscription.</span></span> <span data-ttu-id="89e6a-638">Vous pouvez filtrer la vue des machines virtuelles en sélectionnant le nom d’abonnement dans la liste déroulante**Abonnement**.</span><span class="sxs-lookup"><span data-stu-id="89e6a-638">You can filter the virtual machines view by selecting the subscription name in the **Subscription** drop-down list.</span></span>

2. <span data-ttu-id="89e6a-639">Cliquez sur **Colonnes** en haut de la page **Machines virtuelles**.</span><span class="sxs-lookup"><span data-stu-id="89e6a-639">At the top of the **Virtual machines** page, click **Columns**.</span></span>

3. <span data-ttu-id="89e6a-640">Dans le panneau **Choisir une colonne**, sélectionnez **Chiffrement de disque**, puis cliquez sur **Mettre à jour**.</span><span class="sxs-lookup"><span data-stu-id="89e6a-640">On the **Choose column** blade, select **Disk Encryption**, and then click **Update**.</span></span> <span data-ttu-id="89e6a-641">La colonne de chiffrement de disque présente l’état de chiffrement _Activé_ ou _Non activé_ pour chaque machine virtuelle, comme indiqué dans la figure ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="89e6a-641">You should see the disk-encryption column showing the encryption state _Enabled_ or _Not Enabled_ for each VM, as shown in the following figure:</span></span>

 ![Microsoft Antimalware dans Azure](./media/azure-security-disk-encryption/disk-encryption-fig2.png)

#### <a name="get-the-encryption-status-of-an-encrypted-windowslinux-iaas-vm-by-using-the-disk-encryption-powershell-cmdlet"></a><span data-ttu-id="89e6a-643">Obtenir l’état de chiffrement d’une machine virtuelle IaaS (Windows/Linux) chiffrée à l’aide de l’applet de commande PowerShell de chiffrement de disque</span><span class="sxs-lookup"><span data-stu-id="89e6a-643">Get the encryption status of an encrypted (Windows/Linux) IaaS VM by using the disk-encryption PowerShell cmdlet</span></span>
<span data-ttu-id="89e6a-644">Vous pouvez obtenir l’état de chiffrement de la machine virtuelle IaaS à l’aide de l’applet de commande PowerShell de disque de chiffrement `Get-AzureRmVMDiskEncryptionStatus`.</span><span class="sxs-lookup"><span data-stu-id="89e6a-644">You can get the encryption status of the IaaS VM from the disk-encryption PowerShell cmdlet `Get-AzureRmVMDiskEncryptionStatus`.</span></span> <span data-ttu-id="89e6a-645">Pour obtenir les paramètres de chiffrement de votre machine virtuelle, entrez les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="89e6a-645">To get the encryption settings for your VM, enter the following:</span></span>

    C:\> Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $ResourceGroupName -VMName $VMName
    -ExtensionName $ExtensionName

    OsVolumeEncrypted          : NotEncrypted
    DataVolumesEncrypted       : Encrypted
    OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
    ProgressMessage            : https://rheltest1keyvault.vault.azure.net/secrets/bdb6bfb1-5431-4c28-af46-b18d0025ef2a/abebacb83d864a5fa729508315020f8a

<span data-ttu-id="89e6a-646">Le résultat de _Get-AzureRmVMDiskEncryptionStatus_ peut être examiné à la recherche d’URL de clés de chiffrement.</span><span class="sxs-lookup"><span data-stu-id="89e6a-646">You can inspect the output of _Get-AzureRmVMDiskEncryptionStatus_ for encryption key URLs.</span></span>

    C:\> $status = Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $ResourceGroupName -VMName
    e $VMName -ExtensionName $ExtensionName
    C:\> $status.OsVolumeEncryptionSettings

    DiskEncryptionKey                                                 KeyEncryptionKey                                               Enabled
    -----------------                                                 ----------------                                               -------
    Microsoft.Azure.Management.Compute.Models.KeyVaultSecretReference Microsoft.Azure.Management.Compute.Models.KeyVaultKeyReference    True


    C:\> $status.OsVolumeEncryptionSettings.DiskEncryptionKey.SecretUrl
    https://rheltest1keyvault.vault.azure.net/secrets/bdb6bfb1-5431-4c28-af46-b18d0025ef2a/abebacb83d864a5fa729508315020f8a
    C:\> $status.OsVolumeEncryptionSettings.DiskEncryptionKey

    SecretUrl                                                                                                               SourceVault
    ---------                                                                                                               -----------
    https://rheltest1keyvault.vault.azure.net/secrets/bdb6bfb1-5431-4c28-af46-b18d0025ef2a/abebacb83d864a5fa729508315020f8a Microsoft.Azure.Management....

<span data-ttu-id="89e6a-647">Les valeurs des paramètres OSVolumeEncrypted et DataVolumesEncrypted sont définies sur _Encrypted_, indiquant que les deux volumes sont chiffrés avec Azure Disk Encryption.</span><span class="sxs-lookup"><span data-stu-id="89e6a-647">The OSVolumeEncrypted and DataVolumesEncrypted settings values are set to _Encrypted_, which shows that both volumes are encrypted using Azure Disk Encryption.</span></span> <span data-ttu-id="89e6a-648">Pour plus d’informations sur l’activation du chiffrement avec Azure Disk Encryption à l’aide des applets de commande PowerShell, consultez les billets de blog [Explorer Azure Disk Encryption avec Azure PowerShell - partie 1](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/explore-azure-disk-encryption-with-azure-powershell.aspx) et [Explorer Azure Disk Encryption avec Azure PowerShell - partie 2](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx).</span><span class="sxs-lookup"><span data-stu-id="89e6a-648">For information about enabling encryption with Azure Disk Encryption by using PowerShell cmdlets, see the blog posts [Explore Azure Disk Encryption with Azure PowerShell - Part 1](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/explore-azure-disk-encryption-with-azure-powershell.aspx) and [Explore Azure Disk Encryption with Azure PowerShell - Part 2](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="89e6a-649">Sur les machines virtuelles Linux, l’applet de commande `Get-AzureRmVMDiskEncryptionStatus` prend 3-4 minutes pour signaler l’état de chiffrement.</span><span class="sxs-lookup"><span data-stu-id="89e6a-649">On Linux VMs, it takes three to four minutes for the `Get-AzureRmVMDiskEncryptionStatus` cmdlet to report the encryption status.</span></span>

#### <a name="get-the-encryption-status-of-the-iaas-vm-from-the-disk-encryption-cli-command"></a><span data-ttu-id="89e6a-650">Obtenir l’état de chiffrement de la machine virtuelle IaaS à partir de la commande CLI de chiffrement</span><span class="sxs-lookup"><span data-stu-id="89e6a-650">Get the encryption status of the IaaS VM from the disk-encryption CLI command</span></span>
<span data-ttu-id="89e6a-651">Vous pouvez obtenir l’état de chiffrement de la machine virtuelle IaaS en utilisant la commande CLI de chiffrement de disque `azure vm show-disk-encryption-status`.</span><span class="sxs-lookup"><span data-stu-id="89e6a-651">You can get the encryption status of the IaaS VM by using the disk-encryption CLI command `azure vm show-disk-encryption-status`.</span></span> <span data-ttu-id="89e6a-652">Pour obtenir les paramètres de chiffrement de votre machine virtuelle, saisissez votre session CLI Azure :</span><span class="sxs-lookup"><span data-stu-id="89e6a-652">To get the encryption settings for your VM, enter your Azure CLI session:</span></span>

    azure vm show-disk-encryption-status --resource-group <yourResourceGroupName> --name <yourVMName> --json  

#### <a name="disable-encryption-on-running-windows-iaas-vm"></a><span data-ttu-id="89e6a-653">Désactivation du chiffrement sur une machine virtuelle IaaS Windows en cours d’exécution</span><span class="sxs-lookup"><span data-stu-id="89e6a-653">Disable encryption on running Windows IaaS VM</span></span>
<span data-ttu-id="89e6a-654">Vous pouvez désactiver le chiffrement sur une machine virtuelle IaaS Windows ou Linux en cours d’exécution via le modèle Resource Manager Azure Disk Encryption ou via les applets de commande PowerShell et spécifier la configuration de déchiffrement.</span><span class="sxs-lookup"><span data-stu-id="89e6a-654">You can disable encryption on a running Windows or Linux IaaS VM via the Azure Disk Encryption Resource Manager template or PowerShell cmdlets and specify the decryption configuration.</span></span>

##### <a name="windows-vm"></a><span data-ttu-id="89e6a-655">Machine virtuelle Windows</span><span class="sxs-lookup"><span data-stu-id="89e6a-655">Windows VM</span></span>
<span data-ttu-id="89e6a-656">L’étape de désactivation du chiffrement désactive le chiffrement du volume de système d’exploitation ou du volume de données (ou les deux) sur la machine virtuelle IaaS Windows en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="89e6a-656">The disable-encryption step disables encryption of the OS, the data volume, or both on the running Windows IaaS VM.</span></span> <span data-ttu-id="89e6a-657">Vous ne pouvez pas désactiver le volume de système d’exploitation et laisser le volume de données chiffré.</span><span class="sxs-lookup"><span data-stu-id="89e6a-657">You cannot disable the OS volume and leave the data volume encrypted.</span></span> <span data-ttu-id="89e6a-658">Une fois le chiffrement désactivé,le modèle de déploiement Azure Classic met à jour le modèle de service de machine virtuelle et la machine virtuelle IaaS Windows est marquée comme déchiffrée.</span><span class="sxs-lookup"><span data-stu-id="89e6a-658">When the disable-encryption step is performed, the Azure classic deployment model updates the VM service model, and the Windows IaaS VM is marked decrypted.</span></span> <span data-ttu-id="89e6a-659">Le contenu de la machine virtuelle n’est plus chiffré au repos.</span><span class="sxs-lookup"><span data-stu-id="89e6a-659">The contents of the VM are no longer encrypted at rest.</span></span> <span data-ttu-id="89e6a-660">Le déchiffrement ne supprime ni votre coffre de clés ni le support de clé de chiffrement (clés de chiffrement BitLocker pour Windows et phrase secrète pour Linux).</span><span class="sxs-lookup"><span data-stu-id="89e6a-660">The decryption does not delete your key vault and the encryption key material (BitLocker encryption keys for Windows and Passphrase for Linux).</span></span>

##### <a name="linux-vm"></a><span data-ttu-id="89e6a-661">Machine virtuelle Linux</span><span class="sxs-lookup"><span data-stu-id="89e6a-661">Linux VM</span></span>
<span data-ttu-id="89e6a-662">L’étape de désactivation du chiffrement désactive le chiffrement du volume de données sur la machine virtuelle IaaS Linux en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="89e6a-662">The disable-encryption step disables encryption of the data volume on the running Linux IaaS VM.</span></span> <span data-ttu-id="89e6a-663">Cette étape fonctionne uniquement si le disque du système d’exploitation n’est pas chiffré.</span><span class="sxs-lookup"><span data-stu-id="89e6a-663">This step only works if the OS disk is not encrypted.</span></span>

> [!NOTE]
> <span data-ttu-id="89e6a-664">La désactivation du chiffrement sur le lecteur du système d’exploitation n’est pas autorisée sur les machines virtuelles Linux.</span><span class="sxs-lookup"><span data-stu-id="89e6a-664">Disabling encryption on the OS disk is not allowed on Linux VMs.</span></span>

##### <a name="disable-encryption-on-an-existing-or-running-iaas-vm"></a><span data-ttu-id="89e6a-665">Désactivation du chiffrement sur une machine virtuelle IaaS existante ou en cours d’exécution</span><span class="sxs-lookup"><span data-stu-id="89e6a-665">Disable encryption on an existing or running IaaS VM</span></span>
<span data-ttu-id="89e6a-666">Vous pouvez désactiver le chiffrement de disque sur des machines virtuelles IaaS Windows en cours d’exécution à l’aide du [modèle Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-decrypt-running-windows-vm).</span><span class="sxs-lookup"><span data-stu-id="89e6a-666">You can disable disk encryption on running Windows IaaS VMs by using the [Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-decrypt-running-windows-vm).</span></span>

1. <span data-ttu-id="89e6a-667">Dans le modèle de démarrage rapide Azure, cliquez sur **Déployer sur Azure**, saisissez la configuration de déchiffrement dans le panneau **Paramètres**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="89e6a-667">On the Azure quick-start template, click **Deploy to Azure**, enter the decryption configuration on the **Parameters** blade, and then click **OK**.</span></span>

2. <span data-ttu-id="89e6a-668">Sélectionnez l’abonnement, le groupe de ressources, l’emplacement du groupe de ressources, les conditions juridiques et les accords, puis cliquez sur **Créer** pour activer le chiffrement sur une nouvelle machine virtuelle IaaS.</span><span class="sxs-lookup"><span data-stu-id="89e6a-668">Select the subscription, resource group, resource group location, legal terms, and agreement, and then click **Create** to enable encryption on a new IaaS VM.</span></span>

<span data-ttu-id="89e6a-669">Pour les machines virtuelles Linux, vous pouvez désactiver le chiffrement à l’aide du modèle [Désactiver le chiffrement sur une machine virtuelle Linux en cours d’exécution](https://aka.ms/decrypt-linuxvm).</span><span class="sxs-lookup"><span data-stu-id="89e6a-669">For Linux VMs, you can disable encryption by using the [Disable encryption on a running Linux VM](https://aka.ms/decrypt-linuxvm) template.</span></span>

<span data-ttu-id="89e6a-670">Le tableau suivant répertorie les paramètres du modèle Resource Manager pour la désactivation du chiffrement sur une machine virtuelle IaaS en cours d’exécution :</span><span class="sxs-lookup"><span data-stu-id="89e6a-670">The following table lists Resource Manager template parameters for disabling encryption on a running IaaS VM:</span></span>

| <span data-ttu-id="89e6a-671">Paramètre</span><span class="sxs-lookup"><span data-stu-id="89e6a-671">Parameter</span></span> | <span data-ttu-id="89e6a-672">Description</span><span class="sxs-lookup"><span data-stu-id="89e6a-672">Description</span></span> |
| --- | --- |
| <span data-ttu-id="89e6a-673">vmName</span><span class="sxs-lookup"><span data-stu-id="89e6a-673">vmName</span></span> | <span data-ttu-id="89e6a-674">Nom de la machine virtuelle sur laquelle l’opération de chiffrement doit être effectuée.</span><span class="sxs-lookup"><span data-stu-id="89e6a-674">Name of the VM that the encryption operation is to be performed on.</span></span>
| <span data-ttu-id="89e6a-675">volumeType</span><span class="sxs-lookup"><span data-stu-id="89e6a-675">volumeType</span></span> | <span data-ttu-id="89e6a-676">Type de volume sur lequel l’opération de déchiffrement est effectuée.</span><span class="sxs-lookup"><span data-stu-id="89e6a-676">Type of volume that a decryption operation is performed on.</span></span> <span data-ttu-id="89e6a-677">Les valeurs valides sont _Système d’exploitation_, _Données_ et _Tous_.</span><span class="sxs-lookup"><span data-stu-id="89e6a-677">Valid values are _OS_, _Data_, and _All_.</span></span> <span data-ttu-id="89e6a-678">Vous ne pouvez pas désactiver le chiffrement sur un volume de démarrage/système d’exploitation d’une machine virtuelle IaaS Windows en cours d’exécution sans désactiver le chiffrement sur le volume _Données_.</span><span class="sxs-lookup"><span data-stu-id="89e6a-678">You cannot disable encryption on running Windows IaaS VM OS/boot volume without disabling encryption on the _Data_ volume.</span></span> <span data-ttu-id="89e6a-679">Notez également que la désactivation du chiffrement sur le lecteur du système d’exploitation n’est pas autorisée sur les machines virtuelles Linux.</span><span class="sxs-lookup"><span data-stu-id="89e6a-679">Also note that disabling encryption on the OS disk is not allowed on Linux VMs.</span></span> |
| <span data-ttu-id="89e6a-680">sequenceVersion</span><span class="sxs-lookup"><span data-stu-id="89e6a-680">sequenceVersion</span></span> | <span data-ttu-id="89e6a-681">Version de séquence de l’opération BitLocker.</span><span class="sxs-lookup"><span data-stu-id="89e6a-681">Sequence version of the BitLocker operation.</span></span> <span data-ttu-id="89e6a-682">Incrémentez ce numéro de version à chaque fois qu’une opération de déchiffrement de disque est exécutée sur la même machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="89e6a-682">Increment this version number every time a disk decryption operation is performed on the same VM.</span></span> |

##### <a name="disable-encryption-on-an-existing-or-running-iaas-vm"></a><span data-ttu-id="89e6a-683">Désactivation du chiffrement sur une machine virtuelle IaaS existante ou en cours d’exécution</span><span class="sxs-lookup"><span data-stu-id="89e6a-683">Disable encryption on an existing or running IaaS VM</span></span>
<span data-ttu-id="89e6a-684">Pour désactiver le chiffrement sur une machine virtuelle IaaS existante ou en cours d’exécution à l’aide de l’applet de commande PowerShell, utilisez [`Disable-AzureRmVMDiskEncryption`](/powershell/module/azurerm.compute/disable-azurermvmdiskencryption).</span><span class="sxs-lookup"><span data-stu-id="89e6a-684">To disable encryption on an existing or running IaaS VM by using the PowerShell cmdlet, see [`Disable-AzureRmVMDiskEncryption`](/powershell/module/azurerm.compute/disable-azurermvmdiskencryption).</span></span> <span data-ttu-id="89e6a-685">Cette applet de commande prend en charge les machines virtuelles Linux et Windows.</span><span class="sxs-lookup"><span data-stu-id="89e6a-685">This cmdlet supports both Windows and Linux VMs.</span></span> <span data-ttu-id="89e6a-686">Elle installe une extension sur la machine virtuelle permettant de désactiver le chiffrement.</span><span class="sxs-lookup"><span data-stu-id="89e6a-686">To disable encryption, it installs an extension on the virtual machine.</span></span> <span data-ttu-id="89e6a-687">Si le paramètre _Nom_ n’est pas spécifié, une extension avec le nom par défaut _AzureDiskEncryption pour les machines virtuelles Windows_ est créée.</span><span class="sxs-lookup"><span data-stu-id="89e6a-687">If the _Name_ parameter is not specified, an extension with the default name _AzureDiskEncryption for Windows VMs_ is created.</span></span>

<span data-ttu-id="89e6a-688">Sur les machines virtuelles Linux, l’extension AzureDiskEncryptionForLinux est utilisée.</span><span class="sxs-lookup"><span data-stu-id="89e6a-688">On Linux VMs, the AzureDiskEncryptionForLinux extension is used.</span></span>

> [!NOTE]
> <span data-ttu-id="89e6a-689">Cette applet de commande redémarre la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="89e6a-689">This cmdlet reboots the virtual machine.</span></span>

### <a name="enable-encryption-on-pre-encrypted-iaas-vm-with-azure-managed-disk"></a><span data-ttu-id="89e6a-690">Activer le chiffrement sur une machine virtuelle IaaS pré-chiffrée avec un disque managé Azure</span><span class="sxs-lookup"><span data-stu-id="89e6a-690">Enable encryption on pre-encrypted IaaS VM with Azure Managed Disk</span></span>
<span data-ttu-id="89e6a-691">Utiliser le modèle ARM de disque managé Azure pour créer une machine virtuelle chiffrée à partir d’un disque dur virtuel pré-chiffré en utilisant le modèle ARM accessible via le lien</span><span class="sxs-lookup"><span data-stu-id="89e6a-691">Use the Azure Managed Disk ARM template to create a encrypted VM from a pre-encrypted VHD using the ARM template located at</span></span>   
<span data-ttu-id="89e6a-692">[Créer un disque managé chiffré à partir d’un disque dur virtuel/bjet blob de stockage pré-chiffré] (https://github.com/Azure/azure-quickstart-templates/tree/master/201-create-encrypted-managed-disk)</span><span class="sxs-lookup"><span data-stu-id="89e6a-692">[Create a new encrypted managed disk from a pre-encrypted VHD/storage blob] (https://github.com/Azure/azure-quickstart-templates/tree/master/201-create-encrypted-managed-disk)</span></span>

### <a name="enable-encryption-on-a-new-linux-iaas-vm-with-azure-managed-disk"></a><span data-ttu-id="89e6a-693">Activer le chiffrement sur une nouvelle machine virtuelle IaaS Linux avec disque managé Azure</span><span class="sxs-lookup"><span data-stu-id="89e6a-693">Enable encryption on a new Linux IaaS VM with Azure Managed Disk</span></span>
<span data-ttu-id="89e6a-694">Utiliser le modèle ARM de disque managé Azure pour créer une nouvelle machine virtuelle IaaS Linux chiffrée en utilisant le modèle ARM accessible via le lien</span><span class="sxs-lookup"><span data-stu-id="89e6a-694">Use the Azure Managed Disk ARM template to create a new encrypted Linux IaaS VM using the ARM template located at</span></span>   
<span data-ttu-id="89e6a-695">[Déploiement de RHEL 7.2 avec un chiffrement de disque complet] (https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-full-disk-encrypted-rhel)</span><span class="sxs-lookup"><span data-stu-id="89e6a-695">[Deployment of RHEL 7.2 with full disk encryption] (https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-full-disk-encrypted-rhel)</span></span>

### <a name="enable-encryption-on-a-new-windows-iaas-vm-with-azure-managed-disk"></a><span data-ttu-id="89e6a-696">Activer le chiffrement sur une nouvelle machine virtuelle IaaS Windows avec disque managé Azure</span><span class="sxs-lookup"><span data-stu-id="89e6a-696">Enable encryption on a new Windows IaaS VM with Azure Managed Disk</span></span>
 <span data-ttu-id="89e6a-697">Utiliser le modèle ARM de disque managé Azure pour créer une nouvelle machine virtuelle IaaS Linux chiffrée en utilisant le modèle ARM accessible via le lien</span><span class="sxs-lookup"><span data-stu-id="89e6a-697">Use the Azure Managed Disk ARM template to create a new encrypted Linux IaaS VM using the ARM template located at</span></span>   
 <span data-ttu-id="89e6a-698">[Créer une machine virtuelle avec disque managé IaaS Windows chiffré à partir d’une image de la galerie] (https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-new-vm-gallery-image-managed-disks)</span><span class="sxs-lookup"><span data-stu-id="89e6a-698">[Create a new encrypted Windows IaaS Managed Disk VM from gallery image] (https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-new-vm-gallery-image-managed-disks)</span></span>

  > [!NOTE]
  ><span data-ttu-id="89e6a-699">Il est impératif de réaliser un instantané et/ou une sauvegarde d’une instance de machine virtuelle basée sur un disque géré en dehors d’Azure Disk Encryption et avant d’activer ce service de chiffrement.</span><span class="sxs-lookup"><span data-stu-id="89e6a-699">It is mandatory to snapshot and/or backup a managed disk based VM instance outside of and prior to enabling Azure Disk Encryption.</span></span>  <span data-ttu-id="89e6a-700">Un instantané du disque géré peut être réalisé à partir du portail, sinon il est possible d’utiliser le service Sauvegarde Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="89e6a-700">A snapshot of the managed disk can be taken from the portal, or Azure Backup can be used.</span></span>  <span data-ttu-id="89e6a-701">Les sauvegardes vous garantissent une possibilité de récupération en cas de défaillance inattendue pendant le chiffrement.</span><span class="sxs-lookup"><span data-stu-id="89e6a-701">Backups ensure that a recovery option is possible in the case of any unexpected failure during encryption.</span></span>  <span data-ttu-id="89e6a-702">Une fois la sauvegarde effectuée, il est possible d’utiliser l’applet de commande Set-AzureRmVMDiskEncryptionExtension pour chiffrer des disques gérés en spécifiant le paramètre - skipVmBackup.</span><span class="sxs-lookup"><span data-stu-id="89e6a-702">Once a backup is made, the Set-AzureRmVMDiskEncryptionExtension cmdlet can be used to encrypt managed disks by specifying the -skipVmBackup parameter.</span></span>  <span data-ttu-id="89e6a-703">Cette commande échoue sur les machines virtuelles de disques gérés tant qu’une sauvegarde n’a pas été effectuée et que ce paramètre n’a pas été spécifié.</span><span class="sxs-lookup"><span data-stu-id="89e6a-703">This command will fail against managed disk based VM's until a backup has been made and this parameter has been specified.</span></span>    
 
### <a name="update-encryption-settings-of-an-existing-encrypted-non-premium-vm"></a><span data-ttu-id="89e6a-704">Mettre à jour les paramètres de chiffrement d’une machine virtuelle non Premium chiffrée existante</span><span class="sxs-lookup"><span data-stu-id="89e6a-704">Update encryption settings of an existing encrypted non-premium VM</span></span>
  <span data-ttu-id="89e6a-705">Utilisez les interfaces prises en charge de chiffrement de disque Azure existant pour une machine virtuelle en cours d’exécution [applets de commande PS, CLI ou modèles ARM] afin de mettre à jour des paramètres de chiffrement tels que ID client/secret AAD, clé de chiffrement de clé [KEK], clé de chiffrement BitLocker pour machine virtuelle Windows ou Phrase secrète pour machine virtuelle Linux, etc. Le paramètre de mise à jour de chiffrement est pris en charge uniquement pour les machines virtuelles s’appuyant sur un stockage non Premium.</span><span class="sxs-lookup"><span data-stu-id="89e6a-705">Use the existing Azure disk encryption supported interfaces for running VM [PS cmdlets, CLI or ARM templates] to update the encryption settings like AAD client ID/secret, Key encryption key [KEK], BitLocker encryption key for Windows VM or Passphrase for Linux VM etc. The update encryption setting is supported only for VMs backed by non-premium storage.</span></span> <span data-ttu-id="89e6a-706">Il n’est PAS pris en charge pour des machines virtuelles s’appuyant sur un stockage Premium.</span><span class="sxs-lookup"><span data-stu-id="89e6a-706">It is NNOT supported for VMs backed by premium storage.</span></span>

## <a name="appendix"></a><span data-ttu-id="89e6a-707">Annexe</span><span class="sxs-lookup"><span data-stu-id="89e6a-707">Appendix</span></span>
### <a name="connect-to-your-subscription"></a><span data-ttu-id="89e6a-708">Connexion à votre abonnement</span><span class="sxs-lookup"><span data-stu-id="89e6a-708">Connect to your subscription</span></span>
<span data-ttu-id="89e6a-709">Avant de poursuivre, voir la section *Conditions préalables* dans cet article.</span><span class="sxs-lookup"><span data-stu-id="89e6a-709">Before you proceed, review the *Prerequisites* section in this article.</span></span> <span data-ttu-id="89e6a-710">Après avoir vérifié que toutes les conditions préalables sont remplies, connectez-vous à votre abonnement en procédant comme suit :</span><span class="sxs-lookup"><span data-stu-id="89e6a-710">After you ensure that all prerequisites have been met, connect to your subscription by doing the following:</span></span>

1. <span data-ttu-id="89e6a-711">Démarrez une session Azure PowerShell et connectez-vous à votre compte Azure avec la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="89e6a-711">Start an Azure PowerShell session, and sign in to your Azure account with the following command:</span></span>

    `Login-AzureRmAccount`

2. <span data-ttu-id="89e6a-712">Si vous disposez de plusieurs abonnements et souhaitez spécifier un abonnement à utiliser en particulier, saisissez ce qui suit pour afficher les abonnements de votre compte :</span><span class="sxs-lookup"><span data-stu-id="89e6a-712">If you have multiple subscriptions and want to specify one to use, type the following to see the subscriptions for your account:</span></span>

    `Get-AzureRmSubscription`

3. <span data-ttu-id="89e6a-713">Pour spécifier l’abonnement que vous souhaitez utiliser, saisissez :</span><span class="sxs-lookup"><span data-stu-id="89e6a-713">To specify the subscription you want to use, type:</span></span>

    `Select-AzureRmSubscription -SubscriptionName <Yoursubscriptionname>`

4. <span data-ttu-id="89e6a-714">Pour vérifier que l’abonnement configuré est correct, saisissez :</span><span class="sxs-lookup"><span data-stu-id="89e6a-714">To verify that the subscription configured is correct, type:</span></span>

    `Get-AzureRmSubscription`

5. <span data-ttu-id="89e6a-715">Pour confirmer que les applets de commande Azure Disk Encryption sont installées, saisissez :</span><span class="sxs-lookup"><span data-stu-id="89e6a-715">To confirm the Azure Disk Encryption cmdlets are installed, type:</span></span>

    `Get-command *diskencryption*`

6. <span data-ttu-id="89e6a-716">La sortie ci-dessous confirme l’installation Powershell d’Azure Disk Encryption :</span><span class="sxs-lookup"><span data-stu-id="89e6a-716">The following output confirms the Azure Disk Encryption PowerShell installation:</span></span>

```
    PS C:\Windows\System32\WindowsPowerShell\v1.0> get-command *diskencryption*
    CommandType  Name                                         Source                                                             
    Cmdlet       Get-AzureRmVMDiskEncryptionStatus            AzureRM.Compute                                                    
    Cmdlet       Disable-AzureRmVMDiskEncryption              AzureRM.Compute                                                    
    Cmdlet       Set-AzureRmVMDiskEncryptionExtension         AzureRM.Compute                                                     
```

### <a name="prepare-a-pre-encrypted-windows-vhd"></a><span data-ttu-id="89e6a-717">Préparer un disque dur virtuel Windows déjà chiffré</span><span class="sxs-lookup"><span data-stu-id="89e6a-717">Prepare a pre-encrypted Windows VHD</span></span>
<span data-ttu-id="89e6a-718">Les sections qui suivent sont nécessaires pour préparer un disque dur virtuel Windows déjà chiffré qui sera déployé comme disque dur virtuel chiffré dans Azure IaaS.</span><span class="sxs-lookup"><span data-stu-id="89e6a-718">The sections that follow are necessary to prepare a pre-encrypted Windows VHD for deployment as an encrypted VHD in Azure IaaS.</span></span> <span data-ttu-id="89e6a-719">Utilisez ces informations pour préparer et démarrer une nouvelle machine virtuelle Windows (disque dur virtuel) sur Azure Site Recovery ou Azure.</span><span class="sxs-lookup"><span data-stu-id="89e6a-719">Use the information to prepare and boot a fresh Windows VM (VHD) on Azure Site Recovery or Azure.</span></span>

#### <a name="update-group-policy-to-allow-non-tpm-for-os-protection"></a><span data-ttu-id="89e6a-720">Mettre à jour la stratégie de groupe pour permettre la protection autre que par module de plateforme sécurisée pour la protection du système d’exploitation</span><span class="sxs-lookup"><span data-stu-id="89e6a-720">Update group policy to allow non-TPM for OS protection</span></span>
<span data-ttu-id="89e6a-721">Configurez le paramètre de stratégie de groupe BitLocker **Chiffrement de lecteur BitLocker** qui se trouve sous **Stratégie de l’ordinateur local** > **Configuration ordinateur** > **Modèles d’administration** > **Composants Windows**.</span><span class="sxs-lookup"><span data-stu-id="89e6a-721">Configure the BitLocker Group Policy setting **BitLocker Drive Encryption**, which you'll find under **Local Computer Policy** > **Computer Configuration** > **Administrative Templates** > **Windows Components**.</span></span> <span data-ttu-id="89e6a-722">Remplacez ce paramètre par **Lecteurs du système d’exploitation** > **Exiger une authentification supplémentaire au démarrage** > **Autoriser BitLocker sans un module de plateforme sécurisée compatible** comme indiqué dans la figure ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="89e6a-722">Change this setting to **Operating System Drives** > **Require additional authentication at startup** > **Allow BitLocker without a compatible TPM**, as shown in the following figure:</span></span>

![Microsoft Antimalware dans Azure](./media/azure-security-disk-encryption/disk-encryption-fig8.png)

#### <a name="install-bitlocker-feature-components"></a><span data-ttu-id="89e6a-724">Installer les composants de fonctionnalité BitLocker</span><span class="sxs-lookup"><span data-stu-id="89e6a-724">Install BitLocker feature components</span></span>
<span data-ttu-id="89e6a-725">Pour Windows Server 2012 ou version ultérieure, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="89e6a-725">For Windows Server 2012 and later, use the following command:</span></span>

    dism /online /Enable-Feature /all /FeatureName:BitLocker /quiet /norestart

<span data-ttu-id="89e6a-726">Pour Windows Server 2008 R2, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="89e6a-726">For Windows Server 2008 R2, use the following command:</span></span>

    ServerManagerCmd -install BitLockers

#### <a name="prepare-the-os-volume-for-bitlocker-by-using-bdehdcfg"></a><span data-ttu-id="89e6a-727">Préparer le volume du système d’exploitation pour BitLocker à l’aide de `bdehdcfg`</span><span class="sxs-lookup"><span data-stu-id="89e6a-727">Prepare the OS volume for BitLocker by using `bdehdcfg`</span></span>
<span data-ttu-id="89e6a-728">Exécutez la commande suivante pour compresser la partition du système d’exploitation et préparer la machine pour BitLocker :</span><span class="sxs-lookup"><span data-stu-id="89e6a-728">To compress the OS partition and prepare the machine for BitLocker, execute the following command:</span></span>

    bdehdcfg -target c: shrink -quiet

#### <a name="protect-the-os-volume-by-using-bitlocker"></a><span data-ttu-id="89e6a-729">Protéger le volume du système d’exploitation à l’aide de BitLocker</span><span class="sxs-lookup"><span data-stu-id="89e6a-729">Protect the OS volume by using BitLocker</span></span>
<span data-ttu-id="89e6a-730">Utilisez la commande [`manage-bde`](https://technet.microsoft.com/library/ff829849.aspx) pour activer le chiffrement sur le volume de démarrage à l’aide d’un protecteur de clé externe.</span><span class="sxs-lookup"><span data-stu-id="89e6a-730">Use the [`manage-bde`](https://technet.microsoft.com/library/ff829849.aspx) command to enable encryption on the boot volume using an external key protector.</span></span> <span data-ttu-id="89e6a-731">Placez également la clé externe (fichier .bek) sur le disque ou le volume externe.</span><span class="sxs-lookup"><span data-stu-id="89e6a-731">Also place the external key (.bek file) on the external drive or volume.</span></span> <span data-ttu-id="89e6a-732">Le chiffrement sera activé sur le volume système/de démarrage au prochain redémarrage.</span><span class="sxs-lookup"><span data-stu-id="89e6a-732">Encryption is enabled on the system/boot volume after the next reboot.</span></span>

    manage-bde -on %systemdrive% -sk [ExternalDriveOrVolume]
    reboot

> [!NOTE]
> <span data-ttu-id="89e6a-733">Préparez la machine virtuelle avec un disque dur virtuel de données/de ressources distinct pour obtenir la clé externe à l’aide de BitLocker.</span><span class="sxs-lookup"><span data-stu-id="89e6a-733">Prepare the VM with a separate data/resource VHD for getting the external key by using BitLocker.</span></span>

#### <a name="encrypting-an-os-drive-on-a-running-linux-vm"></a><span data-ttu-id="89e6a-734">Chiffrement d’un lecteur du système d’exploitation sur une machine virtuelle Linux en cours d’exécution</span><span class="sxs-lookup"><span data-stu-id="89e6a-734">Encrypting an OS drive on a running Linux VM</span></span>
<span data-ttu-id="89e6a-735">Le chiffrement d’un lecteur du système d’exploitation sur une machine virtuelle Linux en cours d’exécution est pris en charge sur les distributions suivantes :</span><span class="sxs-lookup"><span data-stu-id="89e6a-735">Encryption of an OS drive on a running Linux VM is supported on the following distributions:</span></span>

* <span data-ttu-id="89e6a-736">RHEL 7.2</span><span class="sxs-lookup"><span data-stu-id="89e6a-736">RHEL 7.2</span></span>
* <span data-ttu-id="89e6a-737">CentOS 7.2</span><span class="sxs-lookup"><span data-stu-id="89e6a-737">CentOS 7.2</span></span>
* <span data-ttu-id="89e6a-738">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="89e6a-738">Ubuntu 16.04</span></span>

##### <a name="prerequisites-for-os-disk-encryption"></a><span data-ttu-id="89e6a-739">Configuration requise pour le chiffrement du lecteur du système d’exploitation</span><span class="sxs-lookup"><span data-stu-id="89e6a-739">Prerequisites for OS disk encryption</span></span>

* <span data-ttu-id="89e6a-740">La machine virtuelle doit être créée à partir de l’image Marketplace dans Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="89e6a-740">The VM must be created from the Marketplace image in Azure Resource Manager.</span></span>
* <span data-ttu-id="89e6a-741">Machine virtuelle Azure au moins 4 Go de RAM (la taille recommandée est de 7 Go).</span><span class="sxs-lookup"><span data-stu-id="89e6a-741">Azure VM with at least 4 GB of RAM (recommended size is 7 GB).</span></span>
* <span data-ttu-id="89e6a-742">(Pour RHEL et CentOS) Désactivez SELinux.</span><span class="sxs-lookup"><span data-stu-id="89e6a-742">(For RHEL and CentOS) Disable SELinux.</span></span> <span data-ttu-id="89e6a-743">Pour désactiver SELinux, consultez la rubrique « 4.4.2.</span><span class="sxs-lookup"><span data-stu-id="89e6a-743">To disable SELinux, see "4.4.2.</span></span> <span data-ttu-id="89e6a-744">Désactivation de SELinux » dans le [Guide d’utilisation et d’administration SELinux](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/SELinux_Users_and_Administrators_Guide/sect-Security-Enhanced_Linux-Working_with_SELinux-Changing_SELinux_Modes.html#sect-Security-Enhanced_Linux-Enabling_and_Disabling_SELinux-Disabling_SELinux) sur la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="89e6a-744">Disabling SELinux" in the [SELinux User's and Administrator's Guide](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/SELinux_Users_and_Administrators_Guide/sect-Security-Enhanced_Linux-Working_with_SELinux-Changing_SELinux_Modes.html#sect-Security-Enhanced_Linux-Enabling_and_Disabling_SELinux-Disabling_SELinux) on the VM.</span></span>
* <span data-ttu-id="89e6a-745">Après avoir désactivé SELinux, redémarrez au moins une fois la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="89e6a-745">After you disable SELinux, reboot the VM at least once.</span></span>

##### <a name="steps"></a><span data-ttu-id="89e6a-746">Étapes</span><span class="sxs-lookup"><span data-stu-id="89e6a-746">Steps</span></span>
1. <span data-ttu-id="89e6a-747">Créez une machine virtuelle en utilisant l’une des distributions spécifiées précédemment.</span><span class="sxs-lookup"><span data-stu-id="89e6a-747">Create a VM by using one of the distributions specified previously.</span></span>

 <span data-ttu-id="89e6a-748">Pour CentOS 7.2, le chiffrement du lecteur du système d’exploitation est pris en charge via une image spécifique.</span><span class="sxs-lookup"><span data-stu-id="89e6a-748">For CentOS 7.2, OS disk encryption is supported via a special image.</span></span> <span data-ttu-id="89e6a-749">Pour utiliser cette image, spécifiez « 7.2n » en tant que référence lorsque vous créez la machine virtuelle :</span><span class="sxs-lookup"><span data-stu-id="89e6a-749">To use this image, specify "7.2n" as the SKU when you create the VM:</span></span>
 ```
    Set-AzureRmVMSourceImage -VM $VirtualMachine -PublisherName "OpenLogic" -Offer "CentOS" -Skus "7.2n" -Version "latest"
 ```
2. <span data-ttu-id="89e6a-750">Configurez la machine virtuelle selon vos besoins.</span><span class="sxs-lookup"><span data-stu-id="89e6a-750">Configure the VM according to your needs.</span></span> <span data-ttu-id="89e6a-751">Si vous souhaitez chiffrer tous les lecteurs (de données et du système d’exploitation), les lecteurs de données doivent être spécifiés et montables à partir de /etc/fstab.</span><span class="sxs-lookup"><span data-stu-id="89e6a-751">If you are going to encrypt all the (OS + data) drives, the data drives need to be specified and mountable from /etc/fstab.</span></span>

 > [!NOTE]
 > <span data-ttu-id="89e6a-752">Utilisez UUID =... pour définir les lecteurs de données dans /etc/fstab au lieu de spécifier le nom de l’appareil de traitement par blocs (par exemple, /dev/sdb1).</span><span class="sxs-lookup"><span data-stu-id="89e6a-752">Use UUID=... to specify data drives in /etc/fstab instead of specifying the block device name (for example, /dev/sdb1).</span></span> <span data-ttu-id="89e6a-753">L’ordre des lecteurs sur la machine virtuelle est modifié au cours du chiffrement.</span><span class="sxs-lookup"><span data-stu-id="89e6a-753">During encryption, the order of drives changes on the VM.</span></span> <span data-ttu-id="89e6a-754">Si votre machine virtuelle s’appuie sur un ordre spécifique d’appareils de traitement par blocs, leur montage échouera après le chiffrement.</span><span class="sxs-lookup"><span data-stu-id="89e6a-754">If your VM relies on a specific order of block devices, it will fail to mount them after encryption.</span></span>

3. <span data-ttu-id="89e6a-755">Déconnectez-vous des sessions SSH.</span><span class="sxs-lookup"><span data-stu-id="89e6a-755">Sign out of the SSH sessions.</span></span>

4. <span data-ttu-id="89e6a-756">Pour chiffrer le système d’exploitation, définissez volumeType sur **Tous** ou **Système d’exploitation** lors de [l’activation du chiffrement](#enable-encryption-on-existing-or-running-iaas-linux-vm-in-azure).</span><span class="sxs-lookup"><span data-stu-id="89e6a-756">To encrypt the OS, specify volumeType as **All** or **OS** when you [enable encryption](#enable-encryption-on-existing-or-running-iaas-linux-vm-in-azure).</span></span>

 > [!NOTE]
 > <span data-ttu-id="89e6a-757">Tous les processus d’espace utilisateur qui ne s’exécutent pas en tant que services `systemd` doivent être arrêtés avec un `SIGKILL`.</span><span class="sxs-lookup"><span data-stu-id="89e6a-757">All user-space processes that are not running as `systemd` services should be killed with a `SIGKILL`.</span></span> <span data-ttu-id="89e6a-758">Redémarrez la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="89e6a-758">Reboot the VM.</span></span> <span data-ttu-id="89e6a-759">Lorsque vous activez le chiffrement du lecteur du système d’exploitation sur une machine virtuelle en cours d’exécution, prévoyez un temps d’arrêt de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="89e6a-759">When you enable OS disk encryption on a running VM, plan on VM downtime.</span></span>

5. <span data-ttu-id="89e6a-760">Surveillez régulièrement la progression du chiffrement à l’aide des instructions fournies dans la [section suivante](#monitoring-os-encryption-progress).</span><span class="sxs-lookup"><span data-stu-id="89e6a-760">Periodically monitor the progress of encryption by using the instructions in the [next section](#monitoring-os-encryption-progress).</span></span>

6. <span data-ttu-id="89e6a-761">Lorsque Get-AzureRmVmDiskEncryptionStatus indique « VMRestartPending », redémarrez votre machine virtuelle en vous y connectant ou en utilisant le portail, PowerShell ou CLI.</span><span class="sxs-lookup"><span data-stu-id="89e6a-761">After Get-AzureRmVmDiskEncryptionStatus shows "VMRestartPending," restart your VM either by signing in to it or by using the portal, PowerShell, or CLI.</span></span>
    ```
    C:\> Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $ResourceGroupName -VMName $VMName
    -ExtensionName $ExtensionName

    OsVolumeEncrypted          : VMRestartPending
    DataVolumesEncrypted       : NotMounted
    OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
    ProgressMessage            : OS disk successfully encrypted, reboot the VM
    ```
<span data-ttu-id="89e6a-762">Avant le redémarrage, nous vous recommandons d’enregistrer les [diagnostics de démarrage](https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/) de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="89e6a-762">Before you reboot, we recommend that you save [boot diagnostics](https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/) of the VM.</span></span>

#### <a name="monitoring-os-encryption-progress"></a><span data-ttu-id="89e6a-763">Surveillance de la progression du chiffrement du système d’exploitation</span><span class="sxs-lookup"><span data-stu-id="89e6a-763">Monitoring OS encryption progress</span></span>
<span data-ttu-id="89e6a-764">Il existe trois façons de surveiller la progression du chiffrement du système d’exploitation :</span><span class="sxs-lookup"><span data-stu-id="89e6a-764">You can monitor OS encryption progress in three ways:</span></span>

* <span data-ttu-id="89e6a-765">Utilisez l’applet de commande `Get-AzureRmVmDiskEncryptionStatus` et examinez le champ ProgressMessage :</span><span class="sxs-lookup"><span data-stu-id="89e6a-765">Use the `Get-AzureRmVmDiskEncryptionStatus` cmdlet and inspect the ProgressMessage field:</span></span>
    ```
    OsVolumeEncrypted          : EncryptionInProgress
    DataVolumesEncrypted       : NotMounted
    OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
    ProgressMessage            : OS disk encryption started
    ```
 <span data-ttu-id="89e6a-766">Dès que l’état « Le chiffrement du lecteur du système d’exploitation a démarré » s’affiche sur la machine virtuelle, l’opération prendra entre 40 et 50 minutes sur une machine virtuelle enregistrée dans un compte de stockage Premium.</span><span class="sxs-lookup"><span data-stu-id="89e6a-766">After the VM reaches "OS disk encryption started," it takes about 40 to 50 minutes on a Premium-storage backed VM.</span></span>

 <span data-ttu-id="89e6a-767">En raison de [l’erreur #388](https://github.com/Azure/WALinuxAgent/issues/388) dans WALinuxAgent, `OsVolumeEncrypted` et `DataVolumesEncrypted` apparaissent comme `Unknown` dans certaines distributions.</span><span class="sxs-lookup"><span data-stu-id="89e6a-767">Because of [issue #388](https://github.com/Azure/WALinuxAgent/issues/388) in WALinuxAgent, `OsVolumeEncrypted` and `DataVolumesEncrypted` show up as `Unknown` in some distributions.</span></span> <span data-ttu-id="89e6a-768">Ce problème est résolu automatiquement dans WALinuxAgent version 2.1.5 et ultérieure.</span><span class="sxs-lookup"><span data-stu-id="89e6a-768">With WALinuxAgent version 2.1.5 and later, this issue is fixed automatically.</span></span> <span data-ttu-id="89e6a-769">Si `Unknown` s’affiche dans la sortie, vous pouvez vérifier l’état du chiffrement du disque en utilisant l’Explorateur de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="89e6a-769">If you see `Unknown` in the output, you can verify disk-encryption status by using the Azure Resource Explorer.</span></span>

 <span data-ttu-id="89e6a-770">Accédez à [l’Explorateur de ressources Azure](https://resources.azure.com/), puis développez cette hiérarchie dans le panneau de sélection de gauche :</span><span class="sxs-lookup"><span data-stu-id="89e6a-770">Go to [Azure Resource Explorer](https://resources.azure.com/), and then expand this hierarchy in the selection panel on left:</span></span>

 ~~~~
 |-- subscriptions
     |-- [Your subscription]
          |-- resourceGroups
               |-- [Your resource group]
                    |-- providers
                         |-- Microsoft.Compute
                              |-- virtualMachines
                                   |-- [Your virtual machine]
                                        |-- InstanceView
~~~~                

 <span data-ttu-id="89e6a-771">Faites défiler InstanceView pour afficher l’état de chiffrement de vos lecteurs.</span><span class="sxs-lookup"><span data-stu-id="89e6a-771">In the InstanceView, scroll down to see the encryption status of your drives.</span></span>

 ![Vue d’instance de machine virtuelle](./media/azure-security-disk-encryption/vm-instanceview.png)

* <span data-ttu-id="89e6a-773">Recherchez les [diagnostics de démarrage](https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/).</span><span class="sxs-lookup"><span data-stu-id="89e6a-773">Look at [boot diagnostics](https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/).</span></span> <span data-ttu-id="89e6a-774">Les messages de l’extension ADE doivent être précédés du préfixe `[AzureDiskEncryption]`.</span><span class="sxs-lookup"><span data-stu-id="89e6a-774">Messages from the ADE extension should be prefixed with `[AzureDiskEncryption]`.</span></span>

* <span data-ttu-id="89e6a-775">Connectez-vous à la machine virtuelle via SSH et obtenez le journal des extensions à partir de :</span><span class="sxs-lookup"><span data-stu-id="89e6a-775">Sign in to the VM via SSH, and get the extension log from:</span></span>

    <span data-ttu-id="89e6a-776">/var/log/azure/Microsoft.Azure.Security.AzureDiskEncryptionForLinux</span><span class="sxs-lookup"><span data-stu-id="89e6a-776">/var/log/azure/Microsoft.Azure.Security.AzureDiskEncryptionForLinux</span></span>

 <span data-ttu-id="89e6a-777">Nous vous déconseillons de vous connecter à la machine virtuelle lorsque le chiffrement du système d’exploitation est en cours.</span><span class="sxs-lookup"><span data-stu-id="89e6a-777">We recommend that you do not sign in to the VM while OS encryption is in progress.</span></span> <span data-ttu-id="89e6a-778">Copiez les journaux uniquement lorsque les deux autres méthodes ont échoué.</span><span class="sxs-lookup"><span data-stu-id="89e6a-778">Copy the logs only when the other two methods have failed.</span></span>

#### <a name="prepare-a-pre-encrypted-linux-vhd"></a><span data-ttu-id="89e6a-779">Préparer un disque dur virtuel Linux déjà chiffré</span><span class="sxs-lookup"><span data-stu-id="89e6a-779">Prepare a pre-encrypted Linux VHD</span></span>
##### <a name="ubuntu-16"></a><span data-ttu-id="89e6a-780">Ubuntu 16</span><span class="sxs-lookup"><span data-stu-id="89e6a-780">Ubuntu 16</span></span>
<span data-ttu-id="89e6a-781">Configurez le chiffrement lors de l’installation de la distribution en procédant comme suit :</span><span class="sxs-lookup"><span data-stu-id="89e6a-781">Configure encryption during the distribution installation by doing the following:</span></span>

1. <span data-ttu-id="89e6a-782">Sélectionnez **Configure encrypted volumes** (Configurer les volumes chiffrés) lors du partitionnement des disques.</span><span class="sxs-lookup"><span data-stu-id="89e6a-782">Select **Configure encrypted volumes** when you partition the disks.</span></span>

 ![Configuration d’Ubuntu 16.04](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig1.png)

2. <span data-ttu-id="89e6a-784">Créez un lecteur de démarrage séparé qui ne doit pas être chiffré.</span><span class="sxs-lookup"><span data-stu-id="89e6a-784">Create a separate boot drive, which must not be encrypted.</span></span> <span data-ttu-id="89e6a-785">Chiffrez votre lecteur racine.</span><span class="sxs-lookup"><span data-stu-id="89e6a-785">Encrypt your root drive.</span></span>

 ![Configuration d’Ubuntu 16.04](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig2.png)

3. <span data-ttu-id="89e6a-787">Indiquez une phrase secrète.</span><span class="sxs-lookup"><span data-stu-id="89e6a-787">Provide a passphrase.</span></span> <span data-ttu-id="89e6a-788">Il s’agit de la phrase secrète que vous chargez dans le coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="89e6a-788">This is the passphrase that you upload to the key vault.</span></span>

 ![Configuration d’Ubuntu 16.04](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig3.png)

4. <span data-ttu-id="89e6a-790">Terminez le partitionnement.</span><span class="sxs-lookup"><span data-stu-id="89e6a-790">Finish partitioning.</span></span>

 ![Configuration d’Ubuntu 16.04](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig4.png)

5. <span data-ttu-id="89e6a-792">Lorsque vous démarrez la machine virtuelle et devez fournir une phrase secrète, utilisez la phrase secrète que vous avez fournie à l’étape 3.</span><span class="sxs-lookup"><span data-stu-id="89e6a-792">When you boot the VM and are asked for a passphrase, use the passphrase you provided in step 3.</span></span>

 ![Configuration d’Ubuntu 16.04](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig5.png)

6. <span data-ttu-id="89e6a-794">Préparez la machine virtuelle au chargement dans Azure en suivant [ces instructions](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-create-upload-ubuntu/).</span><span class="sxs-lookup"><span data-stu-id="89e6a-794">Prepare the VM for uploading into Azure using [these instructions](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-create-upload-ubuntu/).</span></span> <span data-ttu-id="89e6a-795">N’exécutez pas encore la dernière étape (annulation de l’approvisionnement de la machine virtuelle).</span><span class="sxs-lookup"><span data-stu-id="89e6a-795">Do not run the last step (deprovisioning the VM) yet.</span></span>

<span data-ttu-id="89e6a-796">Configurez le chiffrement pour l’utiliser dans Azure en procédant comme suit :</span><span class="sxs-lookup"><span data-stu-id="89e6a-796">Configure encryption to work with Azure by doing the following:</span></span>

1. <span data-ttu-id="89e6a-797">Créez un fichier sous /usr/local/sbin/azure_crypt_key.sh, avec le contenu du script ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="89e6a-797">Create a file under /usr/local/sbin/azure_crypt_key.sh, with the content in the following script.</span></span> <span data-ttu-id="89e6a-798">Prêtez une attention particulière à KeyFileName, car il s’agit du nom de fichier de phrase secrète utilisé par Azure.</span><span class="sxs-lookup"><span data-stu-id="89e6a-798">Pay attention to the KeyFileName, because it is the passphrase file name used by Azure.</span></span>

    ```
    #!/bin/sh
    MountPoint=/tmp-keydisk-mount
    KeyFileName=LinuxPassPhraseFileName
    echo "Trying to get the key from disks ..." >&2
    mkdir -p $MountPoint
    modprobe vfat >/dev/null 2>&1
    modprobe ntfs >/dev/null 2>&1
    sleep 2
    OPENED=0
    cd /sys/block
    for DEV in sd*; do

        echo "> Trying device: $DEV ..." >&2
        mount -t vfat -r /dev/${DEV}1 $MountPoint >/dev/null||
        mount -t ntfs -r /dev/${DEV}1 $MountPoint >/dev/null
        if [ -f $MountPoint/$KeyFileName ]; then
                cat $MountPoint/$KeyFileName
                umount $MountPoint 2>/dev/null
                OPENED=1
                break
        fi
        umount $MountPoint 2>/dev/null
    done

      if [ $OPENED -eq 0 ]; then
        echo "FAILED to find suitable passphrase file ..." >&2
        echo -n "Try to enter your password: " >&2
        read -s -r A </dev/console
        echo -n "$A"
     else
        echo "Success loading keyfile!" >&2
    fi
```

2. <span data-ttu-id="89e6a-799">Modifiez la configuration du chiffrement dans */etc/crypttab*.</span><span class="sxs-lookup"><span data-stu-id="89e6a-799">Change the crypt config in */etc/crypttab*.</span></span> <span data-ttu-id="89e6a-800">Il doit se présenter comme suit :</span><span class="sxs-lookup"><span data-stu-id="89e6a-800">It should look like this:</span></span>
 ```
    xxx_crypt uuid=xxxxxxxxxxxxxxxxxxxxx none luks,discard,keyscript=/usr/local/sbin/azure_crypt_key.sh
    ```

3. <span data-ttu-id="89e6a-801">Si vous modifiez *azure_crypt_key.sh* dans Windows et que vous le copiez sur Linux, exécutez `dos2unix /usr/local/sbin/azure_crypt_key.sh`.</span><span class="sxs-lookup"><span data-stu-id="89e6a-801">If you are editing *azure_crypt_key.sh* in Windows and you copied it to Linux, run `dos2unix /usr/local/sbin/azure_crypt_key.sh`.</span></span>

4. <span data-ttu-id="89e6a-802">Ajoutez des autorisations exécutables au script :</span><span class="sxs-lookup"><span data-stu-id="89e6a-802">Add executable permissions to the script:</span></span>
 ```
    chmod +x /usr/local/sbin/azure_crypt_key.sh
 ```
5. <span data-ttu-id="89e6a-803">Éditez */etc/initramfs-tools/modules* en ajoutant des lignes :</span><span class="sxs-lookup"><span data-stu-id="89e6a-803">Edit */etc/initramfs-tools/modules* by appending lines:</span></span>
 ```
    vfat
    ntfs
    nls_cp437
    nls_utf8
    nls_iso8859-1
```
6. <span data-ttu-id="89e6a-804">Exécutez `update-initramfs -u -k all` pour mettre à jour l’initramfs afin de mettre en vigueur le `keyscript`.</span><span class="sxs-lookup"><span data-stu-id="89e6a-804">Run `update-initramfs -u -k all` to update the initramfs to make the `keyscript` take effect.</span></span>

7. <span data-ttu-id="89e6a-805">Vous pouvez maintenant annuler l’approvisionnement de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="89e6a-805">Now you can deprovision the VM.</span></span>

 ![Configuration d’Ubuntu 16.04](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig6.png)

8. <span data-ttu-id="89e6a-807">Passez à l’étape suivante et [chargez votre disque dur virtuel](#upload-encrypted-vhd-to-an-azure-storage-account) dans Azure.</span><span class="sxs-lookup"><span data-stu-id="89e6a-807">Continue to the next step and [upload your VHD](#upload-encrypted-vhd-to-an-azure-storage-account) into Azure.</span></span>

##### <a name="opensuse-132"></a><span data-ttu-id="89e6a-808">openSUSE 13.2</span><span class="sxs-lookup"><span data-stu-id="89e6a-808">openSUSE 13.2</span></span>
<span data-ttu-id="89e6a-809">Pour configurer le chiffrement lors de l’installation de la distribution, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="89e6a-809">To configure encryption during the distribution installation, do the following:</span></span>
1. <span data-ttu-id="89e6a-810">Lorsque vous partitionnez les disques, sélectionnez **Chiffrer le groupe de volumes**, puis entrez un mot de passe.</span><span class="sxs-lookup"><span data-stu-id="89e6a-810">When you partition the disks, select **Encrypt Volume Group**, and then enter a password.</span></span> <span data-ttu-id="89e6a-811">Il s’agit du mot de passe que vous allez charger dans votre coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="89e6a-811">This is the password that you will upload to your key vault.</span></span>

 ![Configuration d’openSUSE 13.2](./media/azure-security-disk-encryption/opensuse-encrypt-fig1.png)

2. <span data-ttu-id="89e6a-813">Démarrez la machine virtuelle à l’aide de votre mot de passe.</span><span class="sxs-lookup"><span data-stu-id="89e6a-813">Boot the VM using your password.</span></span>

 ![Configuration d’openSUSE 13.2](./media/azure-security-disk-encryption/opensuse-encrypt-fig2.png)

3. <span data-ttu-id="89e6a-815">Préparez la machine virtuelle pour le chargement dans Azure en suivant les instructions de la rubrique [Préparation d’une machine virtuelle SLES ou openSUSE pour Azure](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-suse-create-upload-vhd/#prepare-opensuse-131).</span><span class="sxs-lookup"><span data-stu-id="89e6a-815">Prepare the VM for uploading to Azure by following the instructions in [Prepare a SLES or openSUSE virtual machine for Azure](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-suse-create-upload-vhd/#prepare-opensuse-131).</span></span> <span data-ttu-id="89e6a-816">N’exécutez pas encore la dernière étape (annulation de l’approvisionnement de la machine virtuelle).</span><span class="sxs-lookup"><span data-stu-id="89e6a-816">Do not run the last step (deprovisioning the VM) yet.</span></span>

<span data-ttu-id="89e6a-817">Pour configurer le chiffrement afin de l’utiliser dans Azure, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="89e6a-817">To configure encryption to work with Azure, do the following:</span></span>
1. <span data-ttu-id="89e6a-818">Modifiez le fichier /etc/dracut.conf et ajoutez la ligne suivante :</span><span class="sxs-lookup"><span data-stu-id="89e6a-818">Edit the /etc/dracut.conf, and add the following line:</span></span>
    ```
    add_drivers+=" vfat ntfs nls_cp437 nls_iso8859-1"
    ```
2. <span data-ttu-id="89e6a-819">Mettez ces lignes en commentaire à la fin du fichier /usr/lib/dracut/modules.d/90crypt/module-setup.sh :</span><span class="sxs-lookup"><span data-stu-id="89e6a-819">Comment out these lines by the end of the file /usr/lib/dracut/modules.d/90crypt/module-setup.sh:</span></span>
 ```
    #        inst_multiple -o \
    #        $systemdutildir/system-generators/systemd-cryptsetup-generator \
    #        $systemdutildir/systemd-cryptsetup \
    #        $systemdsystemunitdir/systemd-ask-password-console.path \
    #        $systemdsystemunitdir/systemd-ask-password-console.service \
    #        $systemdsystemunitdir/cryptsetup.target \
    #        $systemdsystemunitdir/sysinit.target.wants/cryptsetup.target \
    #        systemd-ask-password systemd-tty-ask-password-agent
    #        inst_script "$moddir"/crypt-run-generator.sh /sbin/crypt-run-generator
 ```

3. <span data-ttu-id="89e6a-820">Ajoutez la ligne suivante au début du fichier /usr/lib/dracut/modules.d/90crypt/parse-crypt.sh :</span><span class="sxs-lookup"><span data-stu-id="89e6a-820">Append the following line at the beginning of the file /usr/lib/dracut/modules.d/90crypt/parse-crypt.sh:</span></span>
 ```
    DRACUT_SYSTEMD=0
 ```
<span data-ttu-id="89e6a-821">Puis, remplacez toutes les occurrences de :</span><span class="sxs-lookup"><span data-stu-id="89e6a-821">And change all occurrences of:</span></span>
 ```
    if [ -z "$DRACUT_SYSTEMD" ]; then
 ```
<span data-ttu-id="89e6a-822">to:</span><span class="sxs-lookup"><span data-stu-id="89e6a-822">to:</span></span>
```
    if [ 1 ]; then
```
4. <span data-ttu-id="89e6a-823">Modifiez /usr/lib/dracut/modules.d/90crypt/cryptroot-ask.sh et ajoutez-le à « # Open LUKS device » :</span><span class="sxs-lookup"><span data-stu-id="89e6a-823">Edit /usr/lib/dracut/modules.d/90crypt/cryptroot-ask.sh and append it to “# Open LUKS device”:</span></span>

    ```
    MountPoint=/tmp-keydisk-mount
    KeyFileName=LinuxPassPhraseFileName
    echo "Trying to get the key from disks ..." >&2
    mkdir -p $MountPoint >&2
    modprobe vfat >/dev/null >&2
    modprobe ntfs >/dev/null >&2
    for SFS in /dev/sd*; do
    echo "> Trying device:$SFS..." >&2
    mount ${SFS}1 $MountPoint -t vfat -r >&2 ||
    mount ${SFS}1 $MountPoint -t ntfs -r >&2
    if [ -f $MountPoint/$KeyFileName ]; then
        echo "> keyfile got..." >&2
        cp $MountPoint/$KeyFileName /tmp-keyfile >&2
        luksfile=/tmp-keyfile
        umount $MountPoint >&2
        break
    fi
    done
    ```
5. <span data-ttu-id="89e6a-824">Exécutez `/usr/sbin/dracut -f -v` pour mettre à jour le fichier initrd.</span><span class="sxs-lookup"><span data-stu-id="89e6a-824">Run `/usr/sbin/dracut -f -v` to update the initrd.</span></span>

6. <span data-ttu-id="89e6a-825">Vous pouvez désormais annuler l’approvisionnement de la machine virtuelle et [charger votre disque dur virtuel](#upload-encrypted-vhd-to-an-azure-storage-account) dans Azure.</span><span class="sxs-lookup"><span data-stu-id="89e6a-825">Now you can deprovision the VM and [upload your VHD](#upload-encrypted-vhd-to-an-azure-storage-account) into Azure.</span></span>

##### <a name="centos-7"></a><span data-ttu-id="89e6a-826">CentOS 7</span><span class="sxs-lookup"><span data-stu-id="89e6a-826">CentOS 7</span></span>
<span data-ttu-id="89e6a-827">Pour configurer le chiffrement lors de l’installation de la distribution, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="89e6a-827">To configure encryption during the distribution installation, do the following:</span></span>
1. <span data-ttu-id="89e6a-828">Sélectionnez **Chiffrer mes données** lors du partitionnement des disques.</span><span class="sxs-lookup"><span data-stu-id="89e6a-828">Select **Encrypt my data** when you partition disks.</span></span>

 ![Configuration de centOS 7](./media/azure-security-disk-encryption/centos-encrypt-fig1.png)

2. <span data-ttu-id="89e6a-830">Vérifiez que **Chiffrer** est sélectionné pour la partition racine.</span><span class="sxs-lookup"><span data-stu-id="89e6a-830">Make sure **Encrypt** is selected for root partition.</span></span>

 ![Configuration de centOS 7](./media/azure-security-disk-encryption/centos-encrypt-fig2.png)

3. <span data-ttu-id="89e6a-832">Indiquez une phrase secrète.</span><span class="sxs-lookup"><span data-stu-id="89e6a-832">Provide a passphrase.</span></span> <span data-ttu-id="89e6a-833">Il s’agit de la phrase secrète que vous allez charger dans votre coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="89e6a-833">This is the passphrase that you will upload to your key vault.</span></span>

 ![Configuration de centOS 7](./media/azure-security-disk-encryption/centos-encrypt-fig3.png)

4. <span data-ttu-id="89e6a-835">Lorsque vous démarrez la machine virtuelle et devez fournir une phrase secrète, utilisez la phrase secrète que vous avez fournie à l’étape 3.</span><span class="sxs-lookup"><span data-stu-id="89e6a-835">When you boot the VM and are asked for a passphrase, use the passphrase you provided in step 3.</span></span>

 ![Configuration de centOS 7](./media/azure-security-disk-encryption/centos-encrypt-fig4.png)

5. <span data-ttu-id="89e6a-837">Préparez la machine virtuelle pour le chargement dans Azure en suivant les instructions « CentOS 7.0+ » dans la rubrique [Préparation d’une machine virtuelle CentOS pour Azure](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-create-upload-centos/#centos-70).</span><span class="sxs-lookup"><span data-stu-id="89e6a-837">Prepare the VM for uploading into Azure by using the "CentOS 7.0+" instructions in [Prepare a CentOS-based virtual machine for Azure](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-create-upload-centos/#centos-70).</span></span> <span data-ttu-id="89e6a-838">N’exécutez pas encore la dernière étape (annulation de l’approvisionnement de la machine virtuelle).</span><span class="sxs-lookup"><span data-stu-id="89e6a-838">Do not run the last step (deprovisioning the VM) yet.</span></span>

6. <span data-ttu-id="89e6a-839">Vous pouvez désormais annuler l’approvisionnement de la machine virtuelle et [charger votre disque dur virtuel](#upload-encrypted-vhd-to-an-azure-storage-account) dans Azure.</span><span class="sxs-lookup"><span data-stu-id="89e6a-839">Now you can deprovision the VM and [upload your VHD](#upload-encrypted-vhd-to-an-azure-storage-account) into Azure.</span></span>

<span data-ttu-id="89e6a-840">Pour configurer le chiffrement afin de l’utiliser dans Azure, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="89e6a-840">To configure encryption to work with Azure, do the following:</span></span>

1. <span data-ttu-id="89e6a-841">Modifiez le fichier /etc/dracut.conf et ajoutez la ligne suivante :</span><span class="sxs-lookup"><span data-stu-id="89e6a-841">Edit the /etc/dracut.conf, and add the following line:</span></span>
    ```
    add_drivers+=" vfat ntfs nls_cp437 nls_iso8859-1"
    ```

2. <span data-ttu-id="89e6a-842">Mettez ces lignes en commentaire à la fin du fichier /usr/lib/dracut/modules.d/90crypt/module-setup.sh :</span><span class="sxs-lookup"><span data-stu-id="89e6a-842">Comment out these lines by the end of the file /usr/lib/dracut/modules.d/90crypt/module-setup.sh:</span></span>
```
    #        inst_multiple -o \
    #        $systemdutildir/system-generators/systemd-cryptsetup-generator \
    #        $systemdutildir/systemd-cryptsetup \
    #        $systemdsystemunitdir/systemd-ask-password-console.path \
    #        $systemdsystemunitdir/systemd-ask-password-console.service \
    #        $systemdsystemunitdir/cryptsetup.target \
    #        $systemdsystemunitdir/sysinit.target.wants/cryptsetup.target \
    #        systemd-ask-password systemd-tty-ask-password-agent
    #        inst_script "$moddir"/crypt-run-generator.sh /sbin/crypt-run-generator
```

3. <span data-ttu-id="89e6a-843">Ajoutez la ligne suivante au début du fichier /usr/lib/dracut/modules.d/90crypt/parse-crypt.sh :</span><span class="sxs-lookup"><span data-stu-id="89e6a-843">Append the following line at the beginning of the file /usr/lib/dracut/modules.d/90crypt/parse-crypt.sh:</span></span>
```
    DRACUT_SYSTEMD=0
```
<span data-ttu-id="89e6a-844">Puis, remplacez toutes les occurrences de :</span><span class="sxs-lookup"><span data-stu-id="89e6a-844">And change all occurrences of:</span></span>
```
    if [ -z "$DRACUT_SYSTEMD" ]; then
```
<span data-ttu-id="89e6a-845">to</span><span class="sxs-lookup"><span data-stu-id="89e6a-845">to</span></span>
```
    if [ 1 ]; then
```
4. <span data-ttu-id="89e6a-846">Modifiez /usr/lib/dracut/modules.d/90crypt/cryptroot-ask.sh et ajoutez-le après « # Open LUKS device » :</span><span class="sxs-lookup"><span data-stu-id="89e6a-846">Edit /usr/lib/dracut/modules.d/90crypt/cryptroot-ask.sh and append this after the “# Open LUKS device”:</span></span>
    ```
    MountPoint=/tmp-keydisk-mount
    KeyFileName=LinuxPassPhraseFileName
    echo "Trying to get the key from disks ..." >&2
    mkdir -p $MountPoint >&2
    modprobe vfat >/dev/null >&2
    modprobe ntfs >/dev/null >&2
    for SFS in /dev/sd*; do
    echo "> Trying device:$SFS..." >&2
    mount ${SFS}1 $MountPoint -t vfat -r >&2 ||
    mount ${SFS}1 $MountPoint -t ntfs -r >&2
    if [ -f $MountPoint/$KeyFileName ]; then
        echo "> keyfile got..." >&2
        cp $MountPoint/$KeyFileName /tmp-keyfile >&2
        luksfile=/tmp-keyfile
        umount $MountPoint >&2
        break
    fi
    done
    ```    
5. <span data-ttu-id="89e6a-847">Exécutez « /usr/sbin/dracut -f -v » pour mettre à jour le fichier initrd.</span><span class="sxs-lookup"><span data-stu-id="89e6a-847">Run the “/usr/sbin/dracut -f -v” to update the initrd.</span></span>

![Configuration de centOS 7](./media/azure-security-disk-encryption/centos-encrypt-fig5.png)

### <a name="upload-encrypted-vhd-to-an-azure-storage-account"></a><span data-ttu-id="89e6a-849">Télécharger des disques durs virtuels cryptés dans un compte de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="89e6a-849">Upload encrypted VHD to an Azure storage account</span></span>
<span data-ttu-id="89e6a-850">Une fois le chiffrement BitLocker ou DM-Crypt activé, le disque dur virtuel chiffré local doit être chargé sur votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="89e6a-850">After BitLocker encryption or DM-Crypt encryption is enabled, the local encrypted VHD needs to be uploaded to your storage account.</span></span>

    Add-AzureRmVhd [-Destination] <Uri> [-LocalFilePath] <FileInfo> [[-NumberOfUploaderThreads] <Int32> ] [[-BaseImageUriToPatch] <Uri> ] [[-OverWrite]] [ <CommonParameters>]

### <a name="upload-the-disk-encryption-secret-for-the-pre-encrypted-vm-to-your-key-vault"></a><span data-ttu-id="89e6a-851">Télécharger la clé secrète de chiffrement de disque pour la machine virtuelle déjà chiffrée dans le coffre de clés</span><span class="sxs-lookup"><span data-stu-id="89e6a-851">Upload the disk-encryption secret for the pre-encrypted VM to your key vault</span></span>
<span data-ttu-id="89e6a-852">La clé secrète de chiffrement de disque obtenue précédemment doit être téléchargée en tant que clé secrète dans votre coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="89e6a-852">The disk-encryption secret that you obtained previously must be uploaded as a secret in your key vault.</span></span> <span data-ttu-id="89e6a-853">Le chiffrement de disque et les autorisations du coffre de clés doivent être activés pour votre client Azure AD.</span><span class="sxs-lookup"><span data-stu-id="89e6a-853">The key vault needs to have disk encryption and permissions enabled for your Azure AD client.</span></span>

    $AadClientId = "YourAADClientId"
    $AadClientSecret = "YourAADClientSecret"

    $key vault = New-AzureRmKeyVault -VaultName $KeyVaultName -ResourceGroupName $ResourceGroupName -Location $Location

    Set-AzureRmKeyVaultAccessPolicy -VaultName $KeyVaultName -ResourceGroupName $ResourceGroupName -ServicePrincipalName $AadClientId -PermissionsToKeys all -PermissionsToSecrets all
    Set-AzureRmKeyVaultAccessPolicy -VaultName $KeyVaultName -ResourceGroupName $ResourceGroupName -EnabledForDiskEncryption


#### <a name="disk-encryption-secret-not-encrypted-with-a-kek"></a><span data-ttu-id="89e6a-854">La clé secrète de chiffrement de disque non chiffré avec une clé de chiffrement à clé KEK</span><span class="sxs-lookup"><span data-stu-id="89e6a-854">Disk encryption secret not encrypted with a KEK</span></span>
<span data-ttu-id="89e6a-855">Utilisez [Set-AzureKeyVaultSecret](/powershell/module/azurerm.keyvault/set-azurekeyvaultsecret) pour configurer la clé secrète dans votre coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="89e6a-855">To set up the secret in your key vault, use [Set-AzureKeyVaultSecret](/powershell/module/azurerm.keyvault/set-azurekeyvaultsecret).</span></span> <span data-ttu-id="89e6a-856">Si vous disposez d’une machine virtuelle Windows, le fichier bek est encodé sous forme de chaîne en base64, puis téléchargé dans le coffre de clés à l’aide de l’applet de commande `Set-AzureKeyVaultSecret`.</span><span class="sxs-lookup"><span data-stu-id="89e6a-856">If you have a Windows virtual machine, the bek file is encoded as a base64 string and then uploaded to your key vault using the `Set-AzureKeyVaultSecret` cmdlet.</span></span> <span data-ttu-id="89e6a-857">Pour Linux, la phrase secrète est encodée sous forme de chaîne en base64, puis téléchargée dans le coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="89e6a-857">For Linux, the passphrase is encoded as a base64 string and then uploaded to the key vault.</span></span> <span data-ttu-id="89e6a-858">Assurez-vous également que les balises suivantes sont définies lors de la création de la clé secrète dans le coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="89e6a-858">In addition, make sure that the following tags are set when you create the secret in the key vault.</span></span>

    # This is the passphrase that was provided for encryption during the distribution installation
    $passphrase = "contoso-password"

    $tags = @{"DiskEncryptionKeyEncryptionAlgorithm" = "RSA-OAEP"; "DiskEncryptionKeyFileName" = "LinuxPassPhraseFileName"}
    $secretName = [guid]::NewGuid().ToString()
    $secretValue = [Convert]::ToBase64String([System.Text.Encoding]::ASCII.GetBytes($passphrase))
    $secureSecretValue = ConvertTo-SecureString $secretValue -AsPlainText -Force

    $secret = Set-AzureKeyVaultSecret -VaultName $KeyVaultName -Name $secretName -SecretValue $secureSecretValue -tags $tags
    $secretUrl = $secret.Id

<span data-ttu-id="89e6a-859">Utilisez `$secretUrl` à l’étape suivante pour [attacher le lecteur du système d’exploitation sans utiliser de clé de chiffrement à clé](#without-using-a-kek).</span><span class="sxs-lookup"><span data-stu-id="89e6a-859">Use the `$secretUrl` in the next step for [attaching the OS disk without using KEK](#without-using-a-kek).</span></span>

#### <a name="disk-encryption-secret-encrypted-with-a-kek"></a><span data-ttu-id="89e6a-860">Disque chiffré avec une clé secrète de chiffrement de disque à clé KEK</span><span class="sxs-lookup"><span data-stu-id="89e6a-860">Disk encryption secret encrypted with a KEK</span></span>
<span data-ttu-id="89e6a-861">Avant de télécharger la clé secrète dans le coffre de clés, vous pouvez éventuellement la chiffrer à l’aide d’une clé de chiffrement à clé.</span><span class="sxs-lookup"><span data-stu-id="89e6a-861">Before you upload the secret to the key vault, you can optionally encrypt it by using a key encryption key.</span></span> <span data-ttu-id="89e6a-862">Utilisez [l’API](https://msdn.microsoft.com/library/azure/dn878066.aspx) de retour à la ligne pour chiffrer d’abord la clé secrète à l’aide de la clé de chiffrement à clé.</span><span class="sxs-lookup"><span data-stu-id="89e6a-862">Use the wrap [API](https://msdn.microsoft.com/library/azure/dn878066.aspx) to first encrypt the secret using the key encryption key.</span></span> <span data-ttu-id="89e6a-863">La sortie de cette opération de retour à la ligne est une chaîne d’URL encodée en base64 que vous pouvez ensuite charger comme clé secrète à l’aide de l’applet de commande [`Set-AzureKeyVaultSecret`](/powershell/module/azurerm.keyvault/set-azurekeyvaultsecret).</span><span class="sxs-lookup"><span data-stu-id="89e6a-863">The output of this wrap operation is a base64 URL encoded string, which you can then upload as a secret by using the [`Set-AzureKeyVaultSecret`](/powershell/module/azurerm.keyvault/set-azurekeyvaultsecret) cmdlet.</span></span>

    # This is the passphrase that was provided for encryption during the distribution installation
    $passphrase = "contoso-password"

    Add-AzureKeyVaultKey -VaultName $KeyVaultName -Name "keyencryptionkey" -Destination Software
    $KeyEncryptionKey = Get-AzureKeyVaultKey -VaultName $KeyVault.OriginalVault.Name -Name "keyencryptionkey"

    $apiversion = "2015-06-01"

    ##############################
    # Get Auth URI
    ##############################

    $uri = $KeyVault.VaultUri + "/keys"
    $headers = @{}

    $response = try { Invoke-RestMethod -Method GET -Uri $uri -Headers $headers } catch { $_.Exception.Response }

    $authHeader = $response.Headers["www-authenticate"]
    $authUri = [regex]::match($authHeader, 'authorization="(.*?)"').Groups[1].Value

    Write-Host "Got Auth URI successfully"

    ##############################
    # Get Auth Token
    ##############################

    $uri = $authUri + "/oauth2/token"
    $body = "grant_type=client_credentials"
    $body += "&client_id=" + $AadClientId
    $body += "&client_secret=" + [Uri]::EscapeDataString($AadClientSecret)
    $body += "&resource=" + [Uri]::EscapeDataString("https://vault.azure.net")
    $headers = @{}

    $response = Invoke-RestMethod -Method POST -Uri $uri -Headers $headers -Body $body

    $access_token = $response.access_token

    Write-Host "Got Auth Token successfully"

    ##############################
    # Get KEK info
    ##############################

    $uri = $KeyEncryptionKey.Id + "?api-version=" + $apiversion
    $headers = @{"Authorization" = "Bearer " + $access_token}

    $response = Invoke-RestMethod -Method GET -Uri $uri -Headers $headers

    $keyid = $response.key.kid

    Write-Host "Got KEK info successfully"

    ##############################
    # Encrypt passphrase using KEK
    ##############################

    $passphraseB64 = [Convert]::ToBase64String([System.Text.Encoding]::ASCII.GetBytes($Passphrase))
    $uri = $keyid + "/encrypt?api-version=" + $apiversion
    $headers = @{"Authorization" = "Bearer " + $access_token; "Content-Type" = "application/json"}
    $bodyObj = @{"alg" = "RSA-OAEP"; "value" = $passphraseB64}
    $body = $bodyObj | ConvertTo-Json

    $response = Invoke-RestMethod -Method POST -Uri $uri -Headers $headers -Body $body

    $wrappedSecret = $response.value

    Write-Host "Encrypted passphrase successfully"

    ##############################
    # Store secret
    ##############################

    $secretName = [guid]::NewGuid().ToString()
    $uri = $KeyVault.VaultUri + "/secrets/" + $secretName + "?api-version=" + $apiversion
    $secretAttributes = @{"enabled" = $true}
    $secretTags = @{"DiskEncryptionKeyEncryptionAlgorithm" = "RSA-OAEP"; "DiskEncryptionKeyFileName" = "LinuxPassPhraseFileName"}
    $headers = @{"Authorization" = "Bearer " + $access_token; "Content-Type" = "application/json"}
    $bodyObj = @{"value" = $wrappedSecret; "attributes" = $secretAttributes; "tags" = $secretTags}
    $body = $bodyObj | ConvertTo-Json

    $response = Invoke-RestMethod -Method PUT -Uri $uri -Headers $headers -Body $body

    Write-Host "Stored secret successfully"

    $secretUrl = $response.id

<span data-ttu-id="89e6a-864">Utilisez `$KeyEncryptionKey` et `$secretUrl` à l’étape suivante pour [attacher le lecteur du système d’exploitation à l’aide de la clé de chiffrement à clé](#using-a-kek).</span><span class="sxs-lookup"><span data-stu-id="89e6a-864">Use `$KeyEncryptionKey` and `$secretUrl` in the next step for [attaching the OS disk using KEK](#using-a-kek).</span></span>

### <a name="specify-a-secret-url-when-you-attach-an-os-disk"></a><span data-ttu-id="89e6a-865">Spécifier une URL secrète lorsque vous attachez un lecteur de système d’exploitation</span><span class="sxs-lookup"><span data-stu-id="89e6a-865">Specify a secret URL when you attach an OS disk</span></span>
#### <a name="without-using-a-kek"></a><span data-ttu-id="89e6a-866">Sans utiliser de clé de chiffrement à clé KEK</span><span class="sxs-lookup"><span data-stu-id="89e6a-866">Without using a KEK</span></span>
<span data-ttu-id="89e6a-867">Lorsque vous attachez le lecteur du système d’exploitation, exécutez la commande `$secretUrl`.</span><span class="sxs-lookup"><span data-stu-id="89e6a-867">While you are attaching the OS disk, you need to pass `$secretUrl`.</span></span> <span data-ttu-id="89e6a-868">L’URL a été générée dans la section « La clé secrète de chiffrement de disque non chiffrée avec une clé de chiffrement à clé ».</span><span class="sxs-lookup"><span data-stu-id="89e6a-868">The URL was generated in the "Disk-encryption secret not encrypted with a KEK" section.</span></span>

    Set-AzureRmVMOSDisk `
            -VM $VirtualMachine `
            -Name $OSDiskName `
            -SourceImageUri $VhdUri `
            -VhdUri $OSDiskUri `
            -Linux `
            -CreateOption FromImage `
            -DiskEncryptionKeyVaultId $KeyVault.ResourceId `
            -DiskEncryptionKeyUrl $SecretUrl

#### <a name="using-a-kek"></a><span data-ttu-id="89e6a-869">À l’aide d’une clé de chiffrement à clé KEK</span><span class="sxs-lookup"><span data-stu-id="89e6a-869">Using a KEK</span></span>
<span data-ttu-id="89e6a-870">Lorsque vous attachez le lecteur du système d’exploitation, exécutez les commandes `$KeyEncryptionKey` et `$secretUrl`.</span><span class="sxs-lookup"><span data-stu-id="89e6a-870">When you attach the OS disk, pass `$KeyEncryptionKey` and `$secretUrl`.</span></span> <span data-ttu-id="89e6a-871">L’URL a été générée dans la section « La clé secrète de chiffrement de disque non chiffrée avec une clé de chiffrement à clé ».</span><span class="sxs-lookup"><span data-stu-id="89e6a-871">The URL was generated in the "Disk-encryption secret not encrypted with a KEK" section.</span></span>

    Set-AzureRmVMOSDisk `
            -VM $VirtualMachine `
            -Name $OSDiskName `
            -SourceImageUri $CopiedTemplateBlobUri `
            -VhdUri $OSDiskUri `
            -Linux `
            -CreateOption FromImage `
            -DiskEncryptionKeyVaultId $KeyVault.ResourceId `
            -DiskEncryptionKeyUrl $SecretUrl `
            -KeyEncryptionKeyVaultId $KeyVault.ResourceId `
            -KeyEncryptionKeyURL $KeyEncryptionKey.Id

## <a name="download-this-guide"></a><span data-ttu-id="89e6a-872">Télécharger ce guide</span><span class="sxs-lookup"><span data-stu-id="89e6a-872">Download this guide</span></span>
<span data-ttu-id="89e6a-873">Vous pouvez télécharger ce guide à partir de la [Galerie TechNet](https://gallery.technet.microsoft.com/Azure-Disk-Encryption-for-a0018eb0).</span><span class="sxs-lookup"><span data-stu-id="89e6a-873">You can download this guide from the [TechNet Gallery](https://gallery.technet.microsoft.com/Azure-Disk-Encryption-for-a0018eb0).</span></span>

## <a name="for-more-information"></a><span data-ttu-id="89e6a-874">Pour plus d’informations</span><span class="sxs-lookup"><span data-stu-id="89e6a-874">For more information</span></span>
[<span data-ttu-id="89e6a-875">Explorer Azure Disk Encryption avec Azure PowerShell - partie 1</span><span class="sxs-lookup"><span data-stu-id="89e6a-875">Explore Azure Disk Encryption with Azure PowerShell - Part 1</span></span>](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/16/explore-azure-disk-encryption-with-azure-powershell.aspx?wa=wsignin1.0)  
[<span data-ttu-id="89e6a-876">Explorer Azure Disk Encryption avec Azure PowerShell - partie 2</span><span class="sxs-lookup"><span data-stu-id="89e6a-876">Explore Azure Disk Encryption with Azure PowerShell - Part 2</span></span>](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx)
