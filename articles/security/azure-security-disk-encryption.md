---
title: aaaAzure chiffrement de disque pour Windows et les machines virtuelles IaaS Linux | Documents Microsoft
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
ms.openlocfilehash: b685abdcc908e66d2352ec5ac2d9996aa75af1b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-disk-encryption-for-windows-and-linux-iaas-vms"></a><span data-ttu-id="08abf-103">Chiffrement de disque Azure pour des machines virtuelles Windows et Linux IaaS</span><span class="sxs-lookup"><span data-stu-id="08abf-103">Azure Disk Encryption for Windows and Linux IaaS VMs</span></span>
<span data-ttu-id="08abf-104">Microsoft Azure est tooensuring engage souveraineté de données de la confidentialité de vos données et vous permet de toocontrol votre Azure hébergé données via une gamme de technologies avancées tooencrypt, contrôler et gérer des clés de chiffrement, l’accès d’audit et de contrôle de données.</span><span class="sxs-lookup"><span data-stu-id="08abf-104">Microsoft Azure is strongly committed tooensuring your data privacy, data sovereignty and enables you toocontrol your Azure hosted data through a range of advanced technologies tooencrypt, control and manage encryption keys, control & audit access of data.</span></span> <span data-ttu-id="08abf-105">Ainsi, les clients Azure hello flexibilité toochoose hello solution qui répond le mieux à leurs besoins.</span><span class="sxs-lookup"><span data-stu-id="08abf-105">This provides Azure customers hello flexibility toochoose hello solution that best meets their business needs.</span></span> <span data-ttu-id="08abf-106">Dans ce document, nous allons tooa solution de nouvelle technologie « Chiffrement de disque Azure pour Windows et de Linux IaaS VM » toohelp protéger et sauvegarder votre toomeet données votre organisation engagements de conformité et de sécurité.</span><span class="sxs-lookup"><span data-stu-id="08abf-106">In this paper, we will introduce you tooa new technology solution “Azure Disk Encryption for Windows and Linux IaaS VM’s” toohelp protect and safeguard your data toomeet your organizational security and compliance commitments.</span></span> <span data-ttu-id="08abf-107">papier de Hello fournit des instructions détaillées sur la fonctionnalités de chiffrement toouse hello disque Azure, y compris hello prise en charge des scénarios et des expériences utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="08abf-107">hello paper provides detailed guidance on how toouse hello Azure disk encryption features including hello supported scenarios and hello user experiences.</span></span>

> [!NOTE]
> <span data-ttu-id="08abf-108">Certaines recommandations peuvent entraîner une augmentation de l’utilisation des données, des réseaux ou des ressources de calcul débouchant sur des coûts de licence ou d’abonnement supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="08abf-108">Certain recommendations might increase data, network, or compute resource usage, resulting in additional license or subscription costs.</span></span>

## <a name="overview"></a><span data-ttu-id="08abf-109">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="08abf-109">Overview</span></span>
<span data-ttu-id="08abf-110">Azure Disk Encryption est une nouvelle fonctionnalité qui vous permet de chiffrer vos disques de machine virtuelle IaaS Windows et Linux.</span><span class="sxs-lookup"><span data-stu-id="08abf-110">Azure Disk Encryption is a new capability that helps you encrypt your Windows and Linux IaaS virtual machine disks.</span></span> <span data-ttu-id="08abf-111">Le chiffrement des disques Azure s’appuie sur la norme industrielle de hello [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) la fonctionnalité de Windows et hello [DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) fonctionnalité de chiffrement de volume tooprovide Linux pour hello du système d’exploitation et des disques de données hello.</span><span class="sxs-lookup"><span data-stu-id="08abf-111">Azure Disk Encryption leverages hello industry standard [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) feature of Windows and hello [DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) feature of Linux tooprovide volume encryption for hello OS and hello data disks.</span></span> <span data-ttu-id="08abf-112">solution de Hello est intégrée à [Azure Key Vault](https://azure.microsoft.com/documentation/services/key-vault/) toohelp contrôler et de gérer les clés de chiffrement de disque hello et les secrets dans votre abonnement de coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="08abf-112">hello solution is integrated with [Azure Key Vault](https://azure.microsoft.com/documentation/services/key-vault/) toohelp you control and manage hello disk-encryption keys and secrets in your key vault subscription.</span></span> <span data-ttu-id="08abf-113">solution de Hello garantit également que toutes les données sur les disques de machine virtuelle hello sont chiffrées au repos dans votre stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="08abf-113">hello solution also ensures that all data on hello virtual machine disks are encrypted at rest in your Azure storage.</span></span>

<span data-ttu-id="08abf-114">Azure Disk Encryption pour les machines virtuelles Iaas Windows et Linux est désormais à la **disponibilité générale** dans toutes les régions publiques Azure et les régions AzureGov pour les machines virtuelles standard et les machines virtuelles avec Stockage Premium.</span><span class="sxs-lookup"><span data-stu-id="08abf-114">Azure disk encryption for Windows and Linux IaaS VMs is now in **General Availability** in all Azure public regions and AzureGov regions for Standard  VMs and VMs with premium storage.</span></span>

### <a name="encryption-scenarios"></a><span data-ttu-id="08abf-115">Scénarios de chiffrement</span><span class="sxs-lookup"><span data-stu-id="08abf-115">Encryption scenarios</span></span>
<span data-ttu-id="08abf-116">Hello solutions de chiffrement de disque Azure prend en charge hello client les scénarios suivants :</span><span class="sxs-lookup"><span data-stu-id="08abf-116">hello Azure Disk Encryption solution supports hello following customer scenarios:</span></span>

* <span data-ttu-id="08abf-117">Activation du chiffrement sur de nouvelles machines virtuelles IaaS créées à partir de disques durs virtuels déjà chiffrés et de clés de chiffrement</span><span class="sxs-lookup"><span data-stu-id="08abf-117">Enable encryption on new IaaS VMs created from pre-encrypted VHD and encryption keys</span></span>
* <span data-ttu-id="08abf-118">Activer le chiffrement sur les nouvelles machines virtuelles IaaS de créé à partir d’images de la galerie Azure hello pris en charge</span><span class="sxs-lookup"><span data-stu-id="08abf-118">Enable encryption on new IaaS VMs created from hello supported Azure Gallery images</span></span>
* <span data-ttu-id="08abf-119">Activation du chiffrement sur des machines virtuelles IaaS existantes et fonctionnant dans Azure</span><span class="sxs-lookup"><span data-stu-id="08abf-119">Enable encryption on existing IaaS VMs running in Azure</span></span>
* <span data-ttu-id="08abf-120">Désactivation du chiffrement sur les machines virtuelles IaaS Windows.</span><span class="sxs-lookup"><span data-stu-id="08abf-120">Disable encryption on Windows IaaS VMs</span></span>
* <span data-ttu-id="08abf-121">Désactivation du chiffrement sur les lecteurs de données pour les machines virtuelles IaaS Linux</span><span class="sxs-lookup"><span data-stu-id="08abf-121">Disable encryption on data drives for Linux IaaS VMs</span></span>
* <span data-ttu-id="08abf-122">Activation du chiffrement des machines virtuelles avec disque managé</span><span class="sxs-lookup"><span data-stu-id="08abf-122">Enable encryption of managed disk VMs</span></span>
* <span data-ttu-id="08abf-123">Mise à jour des paramètres de chiffrement d’une machine virtuelle de stockage non Premium chiffrée existante</span><span class="sxs-lookup"><span data-stu-id="08abf-123">Update encryption settings of an existing encrypted non-premium storage VM</span></span>
* <span data-ttu-id="08abf-124">Sauvegarde et restauration de machines virtuelles chiffrées avec une clé de chiffrement de clé</span><span class="sxs-lookup"><span data-stu-id="08abf-124">Backup and restore of encrypted VMs, encrypted with key encryption key</span></span>

<span data-ttu-id="08abf-125">solution de Hello prend en charge hello les scénarios suivants pour les machines virtuelles IaaS lorsqu’ils sont activés dans Microsoft Azure :</span><span class="sxs-lookup"><span data-stu-id="08abf-125">hello solution supports hello following scenarios for IaaS VMs when they are enabled in Microsoft Azure:</span></span>

* <span data-ttu-id="08abf-126">Prise en main d’Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="08abf-126">Integration with Azure Key Vault</span></span>
* <span data-ttu-id="08abf-127">Machines virtuelles de niveau standard : [Machines virtuelles IaaS des séries A, D, DS, G, GS, F, etc.](https://azure.microsoft.com/pricing/details/virtual-machines/)</span><span class="sxs-lookup"><span data-stu-id="08abf-127">Standard tier VMs: [A, D, DS, G, GS, F, and so forth series IaaS VMs](https://azure.microsoft.com/pricing/details/virtual-machines/)</span></span>
* <span data-ttu-id="08abf-128">Activer le chiffrement sur Windows et les machines virtuelles IaaS Linux et machines virtuelles de disque géré à partir de hello pris en charge les images de la galerie Azure</span><span class="sxs-lookup"><span data-stu-id="08abf-128">Enable encryption on Windows and Linux IaaS VMs and managed disk VMs from hello supported Azure Gallery images</span></span>
* <span data-ttu-id="08abf-129">Désactivation du chiffrement des lecteurs de système d’exploitation et de données pour des machines virtuelles IaaS Windows et des machines virtuelles avec disque managé</span><span class="sxs-lookup"><span data-stu-id="08abf-129">Disable encryption on OS and data drives for Windows IaaS VMs and managed disk VMs</span></span>
* <span data-ttu-id="08abf-130">Désactivation du chiffrement des lecteurs de données pour des machines virtuelles IaaS Linux et des machines virtuelles avec disque managé</span><span class="sxs-lookup"><span data-stu-id="08abf-130">Disable encryption on data drives for Linux IaaS VMs and managed disk VMs</span></span>
* <span data-ttu-id="08abf-131">Activation du chiffrement sur les machines virtuelles IaaS exécutant le système d’exploitation du client Windows.</span><span class="sxs-lookup"><span data-stu-id="08abf-131">Enable encryption on IaaS VMs running Windows Client OS</span></span>
* <span data-ttu-id="08abf-132">Activation du chiffrement sur les volumes avec chemins d’accès de montage.</span><span class="sxs-lookup"><span data-stu-id="08abf-132">Enable encryption on volumes with mount paths</span></span>
* <span data-ttu-id="08abf-133">Activation du chiffrement sur des machines virtuelles Linux configurées avec une agrégation de disques (RAID) utilisant mdadm</span><span class="sxs-lookup"><span data-stu-id="08abf-133">Enable encryption on Linux VMs configured with disk striping (RAID) using mdadm</span></span>
* <span data-ttu-id="08abf-134">Activation du chiffrement sur des machines virtuelles Linux en utilisant LVM pour les disques de données</span><span class="sxs-lookup"><span data-stu-id="08abf-134">Enable encryption on Linux VMs using LVM for data disks</span></span>
* <span data-ttu-id="08abf-135">Activation du chiffrement sur les machines virtuelles Windows configurées avec des espaces de stockage</span><span class="sxs-lookup"><span data-stu-id="08abf-135">Enable encryption on Windows VMs configured with Storage Spaces</span></span>
* <span data-ttu-id="08abf-136">Mise à jour des paramètres de chiffrement d’une machine virtuelle de stockage non Premium chiffrée existante</span><span class="sxs-lookup"><span data-stu-id="08abf-136">Update encryption settings of an existing encrypted non-premium storage VM</span></span>
* <span data-ttu-id="08abf-137">Toutes les régions publiques Azure et AzureGov sont prises en charge</span><span class="sxs-lookup"><span data-stu-id="08abf-137">All Azure Public and AzureGov regions are supported</span></span>

<span data-ttu-id="08abf-138">solution de Hello ne prend pas en charge hello suivant des scénarios, les fonctionnalités et technologies :</span><span class="sxs-lookup"><span data-stu-id="08abf-138">hello solution does not support hello following scenarios, features, and technology:</span></span>

* <span data-ttu-id="08abf-139">Machines virtuelles IaaS de niveau de base</span><span class="sxs-lookup"><span data-stu-id="08abf-139">Basic tier IaaS VMs</span></span>
* <span data-ttu-id="08abf-140">Désactivation du chiffrement sur un lecteur de système d’exploitation pour les machines virtuelles IaaS Linux</span><span class="sxs-lookup"><span data-stu-id="08abf-140">Disabling encryption on an OS drive for Linux IaaS VMs</span></span>
* <span data-ttu-id="08abf-141">La désactivation du chiffrement sur un lecteur de données si hello lecteur du système d’exploitation est chiffré pour les machines virtuelles Iaas Linux</span><span class="sxs-lookup"><span data-stu-id="08abf-141">Disabling encryption on a data drive if hello OS drive is encrypted for Linux Iaas VMs</span></span>
* <span data-ttu-id="08abf-142">Machines virtuelles IaaS qui sont créés à l’aide de la méthode de création VM hello classique</span><span class="sxs-lookup"><span data-stu-id="08abf-142">IaaS VMs that are created by using hello classic VM creation method</span></span>
* <span data-ttu-id="08abf-143">L’activation du chiffrement sur les images client personnalisées de machines virtuelles Iaas Windows et Linux n’est PAS prise en charge.</span><span class="sxs-lookup"><span data-stu-id="08abf-143">Enable encryption on Windows and Linux IaaS VMs customer custom images is NOT supported.</span></span> <span data-ttu-id="08abf-144">L’activation du chiffrement sur des disques de système d’exploitation LVM Linux n’est pas prise en charge actuellement.</span><span class="sxs-lookup"><span data-stu-id="08abf-144">Enable enccryption on Linux LVM OS disk is not supported currently.</span></span> <span data-ttu-id="08abf-145">Elles seront bientôt prise en charge.</span><span class="sxs-lookup"><span data-stu-id="08abf-145">This support will come soon.</span></span>
* <span data-ttu-id="08abf-146">Intégration à votre service de gestion de clés local</span><span class="sxs-lookup"><span data-stu-id="08abf-146">Integration with your on-premises Key Management Service</span></span>
* <span data-ttu-id="08abf-147">Azure Files (système de partage de fichiers), NFS (Network File System), volumes dynamiques et machines virtuelles Windows configurées avec des systèmes RAID logiciels</span><span class="sxs-lookup"><span data-stu-id="08abf-147">Azure Files (shared file system), Network File System (NFS), dynamic volumes, and Windows VMs that are configured with software-based RAID systems</span></span>
* <span data-ttu-id="08abf-148">Sauvegarde et restauration de machines virtuelles chiffrées sans clé de chiffrement de clé</span><span class="sxs-lookup"><span data-stu-id="08abf-148">Backup and restore of encrypted VMs, encrypted without key encryption key.</span></span>
* <span data-ttu-id="08abf-149">Mise à jour des paramètres de chiffrement d’une machine virtuelle de stockage Premium chiffrée existante</span><span class="sxs-lookup"><span data-stu-id="08abf-149">Update encryption settings of an existing encrypted premium storage VM.</span></span>

> [!NOTE]
> <span data-ttu-id="08abf-150">Sauvegarde et restauration de machines virtuelles chiffrés est pris en charge uniquement pour les ordinateurs virtuels qui sont chiffrés avec une configuration de clés hello.</span><span class="sxs-lookup"><span data-stu-id="08abf-150">Backup and restore of encrypted VMs is supported only for VMs that are encrypted with hello KEK configuration.</span></span> <span data-ttu-id="08abf-151">Elles ne sont pas prises en charge pour les machines virtuelles chiffrées sans KEK.</span><span class="sxs-lookup"><span data-stu-id="08abf-151">It is not supported on VMs that are encrypted without KEK.</span></span> <span data-ttu-id="08abf-152">KEK est un paramètre facultatif permettant d’activer le chiffrement d’une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="08abf-152">KEK is an optional parameter that enables VM encryption.</span></span> <span data-ttu-id="08abf-153">Cette prise en charge sera bientôt disponible.</span><span class="sxs-lookup"><span data-stu-id="08abf-153">This support is coming soon.</span></span>
> <span data-ttu-id="08abf-154">La mise à jour des paramètres de chiffrement d’une machine virtuelle de stockage Premium chiffrée ne sont pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="08abf-154">Update encryption settings of an existing encrypted premium storage VM are not supported.</span></span> <span data-ttu-id="08abf-155">Cette prise en charge sera bientôt disponible.</span><span class="sxs-lookup"><span data-stu-id="08abf-155">This support is coming soon.</span></span>

### <a name="encryption-features"></a><span data-ttu-id="08abf-156">Fonctionnalités de chiffrement</span><span class="sxs-lookup"><span data-stu-id="08abf-156">Encryption features</span></span>
<span data-ttu-id="08abf-157">Lorsque vous activez et déployez le chiffrement de disque Azure pour les machines virtuelles Azure IaaS, hello fonctionnalités suivantes sont activées, selon la configuration de hello fournie :</span><span class="sxs-lookup"><span data-stu-id="08abf-157">When you enable and deploy Azure Disk Encryption for Azure IaaS VMs, hello following capabilities are enabled, depending on hello configuration provided:</span></span>

* <span data-ttu-id="08abf-158">Chiffrement de volume de démarrage du système d’exploitation de hello volume tooprotect hello au repos dans votre espace de stockage</span><span class="sxs-lookup"><span data-stu-id="08abf-158">Encryption of hello OS volume tooprotect hello boot volume at rest in your storage</span></span>
* <span data-ttu-id="08abf-159">Chiffrement des données des volumes tooprotect hello des volumes de données au repos dans votre espace de stockage</span><span class="sxs-lookup"><span data-stu-id="08abf-159">Encryption of data volumes tooprotect hello data volumes at rest in your storage</span></span>
* <span data-ttu-id="08abf-160">La désactivation du chiffrement sur hello du système d’exploitation et les données des disques pour les machines virtuelles IaaS Windows</span><span class="sxs-lookup"><span data-stu-id="08abf-160">Disabling encryption on hello OS and data drives for Windows IaaS VMs</span></span>
* <span data-ttu-id="08abf-161">La désactivation du chiffrement sur les données de salutation disques pour les machines virtuelles IaaS Linux (uniquement si le lecteur de système d’exploitation n’est pas chiffrée)</span><span class="sxs-lookup"><span data-stu-id="08abf-161">Disabling encryption on hello data drives for Linux IaaS VMs (only if OS drive IS NOT encrypted)</span></span>
* <span data-ttu-id="08abf-162">Protection des clés de chiffrement hello et les clés secrètes dans votre abonnement de coffre de clés</span><span class="sxs-lookup"><span data-stu-id="08abf-162">Safeguarding hello encryption keys and secrets in your key vault subscription</span></span>
* <span data-ttu-id="08abf-163">Rapports d’état de chiffrement hello Hello chiffré IaaS VM</span><span class="sxs-lookup"><span data-stu-id="08abf-163">Reporting hello encryption status of hello encrypted IaaS VM</span></span>
* <span data-ttu-id="08abf-164">Suppression des paramètres de configuration de chiffrement de disque à partir de la machine virtuelle de hello IaaS</span><span class="sxs-lookup"><span data-stu-id="08abf-164">Removal of disk-encryption configuration settings from hello IaaS virtual machine</span></span>
* <span data-ttu-id="08abf-165">Sauvegarde et restauration de machines virtuelles de chiffrées à l’aide du service de sauvegarde Azure hello</span><span class="sxs-lookup"><span data-stu-id="08abf-165">Backup and restore of encrypted VMs by using hello Azure Backup service</span></span>

> [!NOTE]
> <span data-ttu-id="08abf-166">Sauvegarde et restauration de machines virtuelles chiffrés est pris en charge uniquement pour les ordinateurs virtuels qui sont chiffrés avec une configuration de clés hello.</span><span class="sxs-lookup"><span data-stu-id="08abf-166">Backup and restore of encrypted VMs is supported only for VMs that are encrypted with hello KEK configuration.</span></span> <span data-ttu-id="08abf-167">Elles ne sont pas prises en charge pour les machines virtuelles chiffrées sans KEK.</span><span class="sxs-lookup"><span data-stu-id="08abf-167">It is not supported on VMs that are encrypted without KEK.</span></span> <span data-ttu-id="08abf-168">KEK est un paramètre facultatif permettant d’activer le chiffrement d’une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="08abf-168">KEK is an optional parameter that enables VM encryption.</span></span>

<span data-ttu-id="08abf-169">La solution Azure Disk Encryption pour les machines virtuelles IaaS Windows et Linux comprend :</span><span class="sxs-lookup"><span data-stu-id="08abf-169">Azure Disk Encryption for IaaS VMS for Windows and Linux solution includes:</span></span>

* <span data-ttu-id="08abf-170">extension de chiffrement de disque Hello pour Windows.</span><span class="sxs-lookup"><span data-stu-id="08abf-170">hello disk-encryption extension for Windows.</span></span>
* <span data-ttu-id="08abf-171">extension de chiffrement de disque Hello pour Linux.</span><span class="sxs-lookup"><span data-stu-id="08abf-171">hello disk-encryption extension for Linux.</span></span>
* <span data-ttu-id="08abf-172">applets de commande PowerShell de chiffrement de disque Hello.</span><span class="sxs-lookup"><span data-stu-id="08abf-172">hello disk-encryption PowerShell cmdlets.</span></span>
* <span data-ttu-id="08abf-173">Bonjour applets de commande Azure interface de ligne de commande (CLI) de chiffrement de disque.</span><span class="sxs-lookup"><span data-stu-id="08abf-173">hello disk-encryption Azure command-line interface (CLI) cmdlets.</span></span>
* <span data-ttu-id="08abf-174">modèles Azure Resource Manager de chiffrement de disque Hello.</span><span class="sxs-lookup"><span data-stu-id="08abf-174">hello disk-encryption Azure Resource Manager templates.</span></span>

<span data-ttu-id="08abf-175">Hello solutions de chiffrement de disque Azure est prise en charge sur les machines virtuelles IaaS qui exécutent Windows ou le système d’exploitation Linux.</span><span class="sxs-lookup"><span data-stu-id="08abf-175">hello Azure Disk Encryption solution is supported on IaaS VMs that are running Windows or Linux OS.</span></span> <span data-ttu-id="08abf-176">Pour plus d’informations sur les systèmes d’exploitation hello pris en charge, consultez hello « conditions préalables » section.</span><span class="sxs-lookup"><span data-stu-id="08abf-176">For more information about hello supported operating systems, see hello "Prerequisites" section.</span></span>

> [!NOTE]
> <span data-ttu-id="08abf-177">Le chiffrement des disques de machine virtuelle avec Azure Disk Encryption est gratuit.</span><span class="sxs-lookup"><span data-stu-id="08abf-177">There is no additional charge for encrypting VM disks with Azure Disk Encryption.</span></span>

### <a name="value-proposition"></a><span data-ttu-id="08abf-178">Proposition de valeur</span><span class="sxs-lookup"><span data-stu-id="08abf-178">Value proposition</span></span>
<span data-ttu-id="08abf-179">Lorsque vous appliquez les solutions hello gestion du chiffrement de disque Azure, vous pouvez satisfaire hello suivant les besoins :</span><span class="sxs-lookup"><span data-stu-id="08abf-179">When you apply hello Azure Disk Encryption-management solution, you can satisfy hello following business needs:</span></span>

* <span data-ttu-id="08abf-180">Machines virtuelles IaaS sont sécurisés au repos, car vous pouvez utiliser le chiffrement standard technologie tooaddress sécurité et conformité besoins de l’organisation.</span><span class="sxs-lookup"><span data-stu-id="08abf-180">IaaS VMs are secured at rest, because you can use industry-standard encryption technology tooaddress organizational security and compliance requirements.</span></span>
* <span data-ttu-id="08abf-181">Les machines virtuelles IaaS démarrent par le biais de stratégies et de clés contrôlées par les clients qui peuvent auditer leur utilisation dans le coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="08abf-181">IaaS VMs boot under customer-controlled keys and policies, and you can audit their usage in your key vault.</span></span>

### <a name="encryption-workflow"></a><span data-ttu-id="08abf-182">Workflow de chiffrement</span><span class="sxs-lookup"><span data-stu-id="08abf-182">Encryption workflow</span></span>
<span data-ttu-id="08abf-183">chiffrement de disque tooenable pour Windows et les machines virtuelles Linux, procédez comme hello suivant :</span><span class="sxs-lookup"><span data-stu-id="08abf-183">tooenable disk encryption for Windows and Linux VMs, do hello following:</span></span>

1. <span data-ttu-id="08abf-184">Choisissez un scénario de chiffrement parmi hello précédant les scénarios de chiffrement.</span><span class="sxs-lookup"><span data-stu-id="08abf-184">Choose an encryption scenario from among hello preceding encryption scenarios.</span></span>
2. <span data-ttu-id="08abf-185">Inclusion de chiffrement de disque tooenabling via le modèle de chiffrement de disque Azure Resource Manager hello, applets de commande PowerShell ou commande CLI et spécifier la configuration de chiffrement hello.</span><span class="sxs-lookup"><span data-stu-id="08abf-185">Opt in tooenabling disk encryption via hello Azure Disk Encryption Resource Manager template, PowerShell cmdlets, or CLI command, and specify hello encryption configuration.</span></span>

   * <span data-ttu-id="08abf-186">Pour le scénario de disque dur virtuel chiffrée client hello, téléchargez le compte de stockage de tooyour de disque dur virtuel hello chiffré et le coffre de clés tooyour matériel clé chiffrement hello.</span><span class="sxs-lookup"><span data-stu-id="08abf-186">For hello customer-encrypted VHD scenario, upload hello encrypted VHD tooyour storage account and hello encryption key material tooyour key vault.</span></span> <span data-ttu-id="08abf-187">Ensuite, fournir hello cryptage configuration tooenable cryptage sur un VM IaaS nouvelle.</span><span class="sxs-lookup"><span data-stu-id="08abf-187">Then, provide hello encryption configuration tooenable encryption on a new IaaS VM.</span></span>
   * <span data-ttu-id="08abf-188">Pour les nouveaux ordinateurs virtuels qui sont créés à partir de hello Marketplace et des machines virtuelles existantes qui sont déjà en cours d’exécution dans Azure, permet le chiffrement de tooenable de configuration de chiffrement hello sur hello IaaS VM.</span><span class="sxs-lookup"><span data-stu-id="08abf-188">For new VMs that are created from hello Marketplace and existing VMs that are already running in Azure, provide hello encryption configuration tooenable encryption on hello IaaS VM.</span></span>

3. <span data-ttu-id="08abf-189">Grant toohello d’accès plateforme Azure tooread hello clé de chiffrement matériel (clés de chiffrement BitLocker pour les systèmes Windows) et le mot de passe Linux passe de votre coffre de clés tooenable sur hello IaaS VM.</span><span class="sxs-lookup"><span data-stu-id="08abf-189">Grant access toohello Azure platform tooread hello encryption-key material (BitLocker encryption keys for Windows systems and Passphrase for Linux) from your key vault tooenable encryption on hello IaaS VM.</span></span>

4. <span data-ttu-id="08abf-190">Fournissez hello Azure Active Directory (Azure AD) application identité toowrite hello chiffrement tooyour matériel clé coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="08abf-190">Provide hello Azure Active Directory (Azure AD) application identity toowrite hello encryption key material tooyour key vault.</span></span> <span data-ttu-id="08abf-191">Ainsi, le chiffrement sur hello IaaS VM pour les scénarios de hello mentionné à l’étape 2.</span><span class="sxs-lookup"><span data-stu-id="08abf-191">Doing so enables encryption on hello IaaS VM for hello scenarios mentioned in step 2.</span></span>

5. <span data-ttu-id="08abf-192">Azure met à jour le modèle de service de machine virtuelle hello avec le chiffrement et la configuration du coffre de clés hello et configure votre machine virtuelle chiffré.</span><span class="sxs-lookup"><span data-stu-id="08abf-192">Azure updates hello VM service model with encryption and hello key vault configuration, and sets up your encrypted VM.</span></span>

 ![Microsoft Antimalware dans Azure](./media/azure-security-disk-encryption/disk-encryption-fig1.png)

### <a name="decryption-workflow"></a><span data-ttu-id="08abf-194">Workflow de déchiffrement</span><span class="sxs-lookup"><span data-stu-id="08abf-194">Decryption workflow</span></span>
<span data-ttu-id="08abf-195">chiffrement de disque toodisable pour les machines virtuelles IaaS, hello complet suivant les étapes principales :</span><span class="sxs-lookup"><span data-stu-id="08abf-195">toodisable disk encryption for IaaS VMs, complete hello following high-level steps:</span></span>

1. <span data-ttu-id="08abf-196">Choisissez toodisable chiffrement (déchiffrement) sur un VM IaaS en cours d’exécution dans Azure via le modèle de chiffrement de disque Azure Resource Manager hello ou des applets de commande PowerShell et spécifier la configuration du déchiffrement hello.</span><span class="sxs-lookup"><span data-stu-id="08abf-196">Choose toodisable encryption (decryption) on a running IaaS VM in Azure via hello Azure Disk Encryption Resource Manager template or PowerShell cmdlets, and specify hello decryption configuration.</span></span>

 <span data-ttu-id="08abf-197">Cette étape désactive le chiffrement de volume de données du système d’exploitation ou hello hello ou les deux sur hello machine virtuelle IaaS de Windows en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="08abf-197">This step disables encryption of hello OS or hello data volume or both on hello running Windows IaaS VM.</span></span> <span data-ttu-id="08abf-198">Toutefois, comme indiqué dans la section précédente de hello, la désactivation du chiffrement de disque du système d’exploitation pour Linux n'est pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="08abf-198">However, as mentioned in hello previous section, disabling OS disk encryption for Linux is not supported.</span></span> <span data-ttu-id="08abf-199">étape de déchiffrement Hello est autorisé uniquement pour les lecteurs de données sur les machines virtuelles Linux tant que disque de système d’exploitation hello n’est pas chiffré.</span><span class="sxs-lookup"><span data-stu-id="08abf-199">hello decryption step is allowed only for data drives on Linux VMs as long as hello OS disk is not encrypted.</span></span>
2. <span data-ttu-id="08abf-200">Les mises à jour Azure hello modèle de service de machine virtuelle, et hello IaaS VM est déchiffré.</span><span class="sxs-lookup"><span data-stu-id="08abf-200">Azure updates hello VM service model, and hello IaaS VM is marked decrypted.</span></span> <span data-ttu-id="08abf-201">contenu Hello Hello machine virtuelle n’est plus chiffrés au repos.</span><span class="sxs-lookup"><span data-stu-id="08abf-201">hello contents of hello VM are no longer encrypted at rest.</span></span>

> [!NOTE]
> <span data-ttu-id="08abf-202">opération de chiffrement de la désactiver Hello ne supprime pas votre clé coffre et hello chiffrement matériel de clé (clés de chiffrement BitLocker pour les systèmes Windows) ou une phrase secrète pour Linux.</span><span class="sxs-lookup"><span data-stu-id="08abf-202">hello disable-encryption operation does not delete your key vault and hello encryption key material (BitLocker encryption keys for Windows systems or Passphrase for Linux).</span></span>
 > <span data-ttu-id="08abf-203">La désactivation du chiffrement de disque de système d’exploitation pour Linux n’est pas prise en charge.</span><span class="sxs-lookup"><span data-stu-id="08abf-203">Disabling OS disk encryption for Linux is not supported.</span></span> <span data-ttu-id="08abf-204">étape de déchiffrement Hello est autorisé uniquement pour les lecteurs de données sur les machines virtuelles Linux.</span><span class="sxs-lookup"><span data-stu-id="08abf-204">hello decryption step is allowed only for data drives on Linux VMs.</span></span>
<span data-ttu-id="08abf-205">La désactivation du chiffrement de disque de données pour Linux n’est pas prise en charge si hello lecteur du système d’exploitation est chiffré.</span><span class="sxs-lookup"><span data-stu-id="08abf-205">Disabling data disk encryption for Linux is not supported if hello OS drive is encrypted.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="08abf-206">Composants requis</span><span class="sxs-lookup"><span data-stu-id="08abf-206">Prerequisites</span></span>
<span data-ttu-id="08abf-207">Avant d’activer le chiffrement de disque Azure sur les machines virtuelles Azure IaaS pour les scénarios de hello pris en charge qui sont présentés dans la section « Présentation » de hello, consultez hello suivant des conditions préalables :</span><span class="sxs-lookup"><span data-stu-id="08abf-207">Before you enable Azure Disk Encryption on Azure IaaS VMs for hello supported scenarios that were discussed in hello "Overview" section, see hello following prerequisites:</span></span>

* <span data-ttu-id="08abf-208">Vous devez disposer d’une ressource de toocreate un abonnement Azure actif dans Azure dans des régions hello pris en charge.</span><span class="sxs-lookup"><span data-stu-id="08abf-208">You must have a valid active Azure subscription toocreate resources in Azure in hello supported regions.</span></span>
* <span data-ttu-id="08abf-209">Chiffrement de disque Azure est pris en charge sur hello des versions de Windows Server suivantes : Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2 et Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="08abf-209">Azure Disk Encryption is supported on hello following Windows Server versions: Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2, and Windows Server 2016.</span></span>
* <span data-ttu-id="08abf-210">Hello suivant les versions du client Windows est pris en charge le chiffrement des disques Azure : client de Windows 10 et Windows 8.</span><span class="sxs-lookup"><span data-stu-id="08abf-210">Azure Disk Encryption is supported on hello following Windows client versions: Windows 8 client and Windows 10 client.</span></span>

> [!NOTE]
> <span data-ttu-id="08abf-211">Pour Windows Server 2008 R2, .NET Framework 4.5 doit être installé avant l’activation du chiffrement dans Azure.</span><span class="sxs-lookup"><span data-stu-id="08abf-211">For Windows Server 2008 R2, you must have .NET Framework 4.5 installed before you enable encryption in Azure.</span></span> <span data-ttu-id="08abf-212">Vous pouvez l’installer à partir de la mise à jour Windows en installant la mise à jour facultative hello Microsoft .NET Framework 4.5.2 pour systèmes x64 64 de Windows Server 2008 R2 ([KB2901983](https://support.microsoft.com/kb/2901983)).</span><span class="sxs-lookup"><span data-stu-id="08abf-212">You can install it from Windows Update by installing hello optional update Microsoft .NET Framework 4.5.2 for Windows Server 2008 R2 x64-based systems ([KB2901983](https://support.microsoft.com/kb/2901983)).</span></span>

* <span data-ttu-id="08abf-213">Chiffrement de disque Azure est prise en charge sur hello suivant la galerie Azure en fonction des distributions Linux server et les versions :</span><span class="sxs-lookup"><span data-stu-id="08abf-213">Azure Disk Encryption is supported on hello following Azure Gallery based Linux server distributions and versions:</span></span>

| <span data-ttu-id="08abf-214">Distribution Linux</span><span class="sxs-lookup"><span data-stu-id="08abf-214">Linux Distribution</span></span> | <span data-ttu-id="08abf-215">Version</span><span class="sxs-lookup"><span data-stu-id="08abf-215">Version</span></span> | <span data-ttu-id="08abf-216">Type de volume pris en charge pour le chiffrement</span><span class="sxs-lookup"><span data-stu-id="08abf-216">Volume Type Supported for Encryption</span></span>|
| --- | --- |--- |
| <span data-ttu-id="08abf-217">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="08abf-217">Ubuntu</span></span> | <span data-ttu-id="08abf-218">16.04-DAILY-LTS</span><span class="sxs-lookup"><span data-stu-id="08abf-218">16.04-DAILY-LTS</span></span> | <span data-ttu-id="08abf-219">Disque de système d’exploitation et de données</span><span class="sxs-lookup"><span data-stu-id="08abf-219">OS and Data disk</span></span> |
| <span data-ttu-id="08abf-220">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="08abf-220">Ubuntu</span></span> | <span data-ttu-id="08abf-221">14.04.5-DAILY-LTS</span><span class="sxs-lookup"><span data-stu-id="08abf-221">14.04.5-DAILY-LTS</span></span> | <span data-ttu-id="08abf-222">Disque de système d’exploitation et de données</span><span class="sxs-lookup"><span data-stu-id="08abf-222">OS and Data disk</span></span> |
| <span data-ttu-id="08abf-223">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="08abf-223">Ubuntu</span></span> | <span data-ttu-id="08abf-224">12.10</span><span class="sxs-lookup"><span data-stu-id="08abf-224">12.10</span></span> | <span data-ttu-id="08abf-225">Disque de données</span><span class="sxs-lookup"><span data-stu-id="08abf-225">Data disk</span></span> |
| <span data-ttu-id="08abf-226">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="08abf-226">Ubuntu</span></span> | <span data-ttu-id="08abf-227">12.04</span><span class="sxs-lookup"><span data-stu-id="08abf-227">12.04</span></span> | <span data-ttu-id="08abf-228">Disque de données</span><span class="sxs-lookup"><span data-stu-id="08abf-228">Data disk</span></span> |
| <span data-ttu-id="08abf-229">RHEL</span><span class="sxs-lookup"><span data-stu-id="08abf-229">RHEL</span></span> | <span data-ttu-id="08abf-230">7.3</span><span class="sxs-lookup"><span data-stu-id="08abf-230">7.3</span></span> | <span data-ttu-id="08abf-231">Disque de système d’exploitation et de données</span><span class="sxs-lookup"><span data-stu-id="08abf-231">OS and Data disk</span></span> |
| <span data-ttu-id="08abf-232">RHEL</span><span class="sxs-lookup"><span data-stu-id="08abf-232">RHEL</span></span> | <span data-ttu-id="08abf-233">7,2</span><span class="sxs-lookup"><span data-stu-id="08abf-233">7.2</span></span> | <span data-ttu-id="08abf-234">Disque de système d’exploitation et de données</span><span class="sxs-lookup"><span data-stu-id="08abf-234">OS and Data disk</span></span> |
| <span data-ttu-id="08abf-235">RHEL</span><span class="sxs-lookup"><span data-stu-id="08abf-235">RHEL</span></span> | <span data-ttu-id="08abf-236">6,8</span><span class="sxs-lookup"><span data-stu-id="08abf-236">6.8</span></span> | <span data-ttu-id="08abf-237">Disque de système d’exploitation et de données</span><span class="sxs-lookup"><span data-stu-id="08abf-237">OS and Data disk</span></span> |
| <span data-ttu-id="08abf-238">RHEL</span><span class="sxs-lookup"><span data-stu-id="08abf-238">RHEL</span></span> | <span data-ttu-id="08abf-239">6.7</span><span class="sxs-lookup"><span data-stu-id="08abf-239">6.7</span></span> | <span data-ttu-id="08abf-240">Disque de données</span><span class="sxs-lookup"><span data-stu-id="08abf-240">Data disk</span></span> |
| <span data-ttu-id="08abf-241">CentOS</span><span class="sxs-lookup"><span data-stu-id="08abf-241">CentOS</span></span> | <span data-ttu-id="08abf-242">7.3</span><span class="sxs-lookup"><span data-stu-id="08abf-242">7.3</span></span> | <span data-ttu-id="08abf-243">Disque de système d’exploitation et de données</span><span class="sxs-lookup"><span data-stu-id="08abf-243">OS and Data disk</span></span> |
| <span data-ttu-id="08abf-244">CentOS</span><span class="sxs-lookup"><span data-stu-id="08abf-244">CentOS</span></span> | <span data-ttu-id="08abf-245">7.2n</span><span class="sxs-lookup"><span data-stu-id="08abf-245">7.2n</span></span> | <span data-ttu-id="08abf-246">Disque de système d’exploitation et de données</span><span class="sxs-lookup"><span data-stu-id="08abf-246">OS and Data disk</span></span> |
| <span data-ttu-id="08abf-247">CentOS</span><span class="sxs-lookup"><span data-stu-id="08abf-247">CentOS</span></span> | <span data-ttu-id="08abf-248">6.8</span><span class="sxs-lookup"><span data-stu-id="08abf-248">6.8</span></span> | <span data-ttu-id="08abf-249">Disque de système d’exploitation et de données</span><span class="sxs-lookup"><span data-stu-id="08abf-249">OS and Data disk</span></span> |
| <span data-ttu-id="08abf-250">CentOS</span><span class="sxs-lookup"><span data-stu-id="08abf-250">CentOS</span></span> | <span data-ttu-id="08abf-251">7.1</span><span class="sxs-lookup"><span data-stu-id="08abf-251">7.1</span></span> | <span data-ttu-id="08abf-252">Disque de données</span><span class="sxs-lookup"><span data-stu-id="08abf-252">Data disk</span></span> |
| <span data-ttu-id="08abf-253">CentOS</span><span class="sxs-lookup"><span data-stu-id="08abf-253">CentOS</span></span> | <span data-ttu-id="08abf-254">7.0</span><span class="sxs-lookup"><span data-stu-id="08abf-254">7.0</span></span> | <span data-ttu-id="08abf-255">Disque de données</span><span class="sxs-lookup"><span data-stu-id="08abf-255">Data disk</span></span> |
| <span data-ttu-id="08abf-256">CentOS</span><span class="sxs-lookup"><span data-stu-id="08abf-256">CentOS</span></span> | <span data-ttu-id="08abf-257">6.7</span><span class="sxs-lookup"><span data-stu-id="08abf-257">6.7</span></span> | <span data-ttu-id="08abf-258">Disque de données</span><span class="sxs-lookup"><span data-stu-id="08abf-258">Data disk</span></span> |
| <span data-ttu-id="08abf-259">CentOS</span><span class="sxs-lookup"><span data-stu-id="08abf-259">CentOS</span></span> | <span data-ttu-id="08abf-260">6.6</span><span class="sxs-lookup"><span data-stu-id="08abf-260">6.6</span></span> | <span data-ttu-id="08abf-261">Disque de données</span><span class="sxs-lookup"><span data-stu-id="08abf-261">Data disk</span></span> |
| <span data-ttu-id="08abf-262">CentOS</span><span class="sxs-lookup"><span data-stu-id="08abf-262">CentOS</span></span> | <span data-ttu-id="08abf-263">6.5</span><span class="sxs-lookup"><span data-stu-id="08abf-263">6.5</span></span> | <span data-ttu-id="08abf-264">Disque de données</span><span class="sxs-lookup"><span data-stu-id="08abf-264">Data disk</span></span> |
| <span data-ttu-id="08abf-265">openSUSE</span><span class="sxs-lookup"><span data-stu-id="08abf-265">openSUSE</span></span> | <span data-ttu-id="08abf-266">13.2</span><span class="sxs-lookup"><span data-stu-id="08abf-266">13.2</span></span> | <span data-ttu-id="08abf-267">Disque de données</span><span class="sxs-lookup"><span data-stu-id="08abf-267">Data disk</span></span> |
| <span data-ttu-id="08abf-268">SLES</span><span class="sxs-lookup"><span data-stu-id="08abf-268">SLES</span></span> | <span data-ttu-id="08abf-269">12 SP1</span><span class="sxs-lookup"><span data-stu-id="08abf-269">12 SP1</span></span> | <span data-ttu-id="08abf-270">Disque de données</span><span class="sxs-lookup"><span data-stu-id="08abf-270">Data disk</span></span> |
| <span data-ttu-id="08abf-271">SLES</span><span class="sxs-lookup"><span data-stu-id="08abf-271">SLES</span></span> | <span data-ttu-id="08abf-272">12-SP1 (Premium)</span><span class="sxs-lookup"><span data-stu-id="08abf-272">12-SP1 (Premium)</span></span> | <span data-ttu-id="08abf-273">Disque de données</span><span class="sxs-lookup"><span data-stu-id="08abf-273">Data disk</span></span> |
| <span data-ttu-id="08abf-274">SLES</span><span class="sxs-lookup"><span data-stu-id="08abf-274">SLES</span></span> | <span data-ttu-id="08abf-275">HPC 12</span><span class="sxs-lookup"><span data-stu-id="08abf-275">HPC 12</span></span> | <span data-ttu-id="08abf-276">Disque de données</span><span class="sxs-lookup"><span data-stu-id="08abf-276">Data disk</span></span> |
| <span data-ttu-id="08abf-277">SLES</span><span class="sxs-lookup"><span data-stu-id="08abf-277">SLES</span></span> | <span data-ttu-id="08abf-278">11-SP4 (Premium)</span><span class="sxs-lookup"><span data-stu-id="08abf-278">11-SP4 (Premium)</span></span> | <span data-ttu-id="08abf-279">Disque de données</span><span class="sxs-lookup"><span data-stu-id="08abf-279">Data disk</span></span> |
| <span data-ttu-id="08abf-280">SLES</span><span class="sxs-lookup"><span data-stu-id="08abf-280">SLES</span></span> | <span data-ttu-id="08abf-281">11 SP4</span><span class="sxs-lookup"><span data-stu-id="08abf-281">11 SP4</span></span> | <span data-ttu-id="08abf-282">Disque de données</span><span class="sxs-lookup"><span data-stu-id="08abf-282">Data disk</span></span> |

* <span data-ttu-id="08abf-283">Le chiffrement des disques Azure nécessite que votre coffre de clés et les machines virtuelles résident dans hello même région Azure et l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="08abf-283">Azure Disk Encryption requires that your key vault and VMs reside in hello same Azure region and subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="08abf-284">Configuration des ressources de hello dans des régions distinctes de provoque un échec de l’activation de fonctionnalité de chiffrement de disque Azure hello.</span><span class="sxs-lookup"><span data-stu-id="08abf-284">Configuring hello resources in separate regions causes a failure in enabling hello Azure Disk Encryption feature.</span></span>

* <span data-ttu-id="08abf-285">tooset et configurer votre coffre de clés de chiffrement de disque Azure, consultez la section **définir installer et configurer votre coffre de clés de chiffrement de disque Azure** Bonjour *conditions préalables* section de cet article.</span><span class="sxs-lookup"><span data-stu-id="08abf-285">tooset up and configure your key vault for Azure Disk Encryption, see section **Set up and configure your key vault for Azure Disk Encryption** in hello *Prerequisites* section of this article.</span></span>
* <span data-ttu-id="08abf-286">tooset et configurer l’application Azure AD dans Azure Active directory pour le chiffrement du disque Azure, consultez la section **configurer application hello Azure AD dans Azure Active Directory** Bonjour *conditions préalables* section de cet article.</span><span class="sxs-lookup"><span data-stu-id="08abf-286">tooset up and configure Azure AD application in Azure Active directory for Azure Disk Encryption, see section **Set up hello Azure AD application in Azure Active Directory** in hello *Prerequisites* section of this article.</span></span>
* <span data-ttu-id="08abf-287">tooset et configurer la stratégie d’accès de coffre de clés hello pour une application hello Azure AD, consultez la section **configurer la stratégie d’accès hello coffre de clés pour l’application hello Azure AD** Bonjour *conditions préalables* section de Cet article.</span><span class="sxs-lookup"><span data-stu-id="08abf-287">tooset up and configure hello key vault access policy for hello Azure AD application, see section **Set up hello key vault access policy for hello Azure AD application** in hello *Prerequisites* section of this article.</span></span>
* <span data-ttu-id="08abf-288">tooprepare un disque dur virtuel déjà chiffrés de Windows, consultez la section **préparer un disque dur virtuel Windows déjà chiffrés** Bonjour *annexe*.</span><span class="sxs-lookup"><span data-stu-id="08abf-288">tooprepare a pre-encrypted Windows VHD, see section **Prepare a pre-encrypted Windows VHD** in hello *Appendix*.</span></span>
* <span data-ttu-id="08abf-289">tooprepare un VHD Linux déjà chiffrés, voir la section **préparer un VHD Linux déjà chiffrés** Bonjour *annexe*.</span><span class="sxs-lookup"><span data-stu-id="08abf-289">tooprepare a pre-encrypted Linux VHD, see section **Prepare a pre-encrypted Linux VHD** in hello *Appendix*.</span></span>
* <span data-ttu-id="08abf-290">Hello plateforme Azure a besoin de clés de chiffrement toohello accès ou les clés secrètes dans votre coffre de clés de toomake leur ordinateur de virtuel toohello disponibles lorsqu’il démarre et déchiffre le volume de l’ordinateur virtuel du système d’exploitation hello.</span><span class="sxs-lookup"><span data-stu-id="08abf-290">hello Azure platform needs access toohello encryption keys or secrets in your key vault toomake them available toohello virtual machine when it boots and decrypts hello virtual machine OS volume.</span></span> <span data-ttu-id="08abf-291">plateforme de tooAzure autorisations toogrant, jeu hello **EnabledForDiskEncryption** propriété hello coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="08abf-291">toogrant permissions tooAzure platform, set hello **EnabledForDiskEncryption** property in hello key vault.</span></span> <span data-ttu-id="08abf-292">Pour plus d’informations, consultez **définir installer et configurer votre coffre de clés de chiffrement de disque Azure** Bonjour annexe.</span><span class="sxs-lookup"><span data-stu-id="08abf-292">For more information, see **Set up and configure your key vault for Azure Disk Encryption** in hello Appendix.</span></span>
* <span data-ttu-id="08abf-293">Les URL de clé secrète de coffre de clés et de clé de chiffrement à clé (KEK) doivent être des versions gérées.</span><span class="sxs-lookup"><span data-stu-id="08abf-293">Your key vault secret and KEK URLs must be versioned.</span></span> <span data-ttu-id="08abf-294">Azure met en vigueur cette restriction de gestion de version.</span><span class="sxs-lookup"><span data-stu-id="08abf-294">Azure enforces this restriction of versioning.</span></span> <span data-ttu-id="08abf-295">Pour secret valide et les URL de clés, consultez hello exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="08abf-295">For valid secret and KEK URLs, see hello following examples:</span></span>

  * <span data-ttu-id="08abf-296">Exemple d’URL secrète valide : *https://contosovault.vault.azure.net/secrets/BitLockerEncryptionSecretWithKek/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span><span class="sxs-lookup"><span data-stu-id="08abf-296">Example of a valid secret URL:   *https://contosovault.vault.azure.net/secrets/BitLockerEncryptionSecretWithKek/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span></span>
  * <span data-ttu-id="08abf-297">Exemple d’URL de clé de chiffrement à clé valide : *https://contosovault.vault.azure.net/keys/diskencryptionkek/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span><span class="sxs-lookup"><span data-stu-id="08abf-297">Example of a valid KEK URL:   *https://contosovault.vault.azure.net/keys/diskencryptionkek/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span></span>

* <span data-ttu-id="08abf-298">Azure Disk Encryption ne prend pas en charge l’intégration de numéros de port aux clés secrètes de coffre de clés et aux URL KEK.</span><span class="sxs-lookup"><span data-stu-id="08abf-298">Azure Disk Encryption does not support specifying port numbers as part of key vault secrets and KEK URLs.</span></span> <span data-ttu-id="08abf-299">Pour obtenir des exemples d’URL de coffre de clés pris en charge et non pris en charge, voir hello :</span><span class="sxs-lookup"><span data-stu-id="08abf-299">For examples of non-supported and supported key vault URLs, see hello following:</span></span>

  * <span data-ttu-id="08abf-300">URL de coffre de clés non acceptée : *https://contosovault.vault.azure.net:443/secrets/contososecret/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span><span class="sxs-lookup"><span data-stu-id="08abf-300">Unacceptable key vault URL  *https://contosovault.vault.azure.net:443/secrets/contososecret/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span></span>
  * <span data-ttu-id="08abf-301">URL de coffre de clés acceptée : *https://contosovault.vault.azure.net/secrets/contososecret/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span><span class="sxs-lookup"><span data-stu-id="08abf-301">Acceptable key vault URL:   *https://contosovault.vault.azure.net/secrets/contososecret/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span></span>

* <span data-ttu-id="08abf-302">fonctionnalité de chiffrement de disque Azure hello tooenable, hello machines virtuelles IaaS doit respecter hello suivant les exigences de configuration de point de terminaison de réseau :</span><span class="sxs-lookup"><span data-stu-id="08abf-302">tooenable hello Azure Disk Encryption feature, hello IaaS VMs must meet hello following network endpoint configuration requirements:</span></span>
  * <span data-ttu-id="08abf-303">tooget un jeton tooconnect tooyour coffre de clés, hello IaaS VM doit être en mesure de tooconnect le point de terminaison Azure Active Directory tooan, \[login.microsoftonline.com\].</span><span class="sxs-lookup"><span data-stu-id="08abf-303">tooget a token tooconnect tooyour key vault, hello IaaS VM must be able tooconnect tooan Azure Active Directory endpoint, \[login.microsoftonline.com\].</span></span>
  * <span data-ttu-id="08abf-304">toowrite hello chiffrement clés tooyour coffre de clés, hello IaaS VM doit être le point de terminaison en mesure de tooconnect toohello coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="08abf-304">toowrite hello encryption keys tooyour key vault, hello IaaS VM must be able tooconnect toohello key vault endpoint.</span></span>
  * <span data-ttu-id="08abf-305">Hello IaaS VM doit être le point de terminaison le stockage Azure de tooan tooconnect en mesure que les ordinateurs hôtes hello référentiel d’extensions Azure et un compte de stockage Azure que hôtes hello des fichiers de disque dur virtuel.</span><span class="sxs-lookup"><span data-stu-id="08abf-305">hello IaaS VM must be able tooconnect tooan Azure storage endpoint that hosts hello Azure extension repository and an Azure storage account that hosts hello VHD files.</span></span>

  > [!NOTE]
  > <span data-ttu-id="08abf-306">Si votre stratégie de sécurité limite l’accès à partir de machines virtuelles Azure toohello Internet, vous pouvez résoudre hello précédant l’URI et configurer un toohello de connectivité sortante tooallow règle spécifique des adresses IP.</span><span class="sxs-lookup"><span data-stu-id="08abf-306">If your security policy limits access from Azure VMs toohello Internet, you can resolve hello preceding URI and configure a specific rule tooallow outbound connectivity toohello IPs.</span></span>
  >
  ><span data-ttu-id="08abf-307">tooconfigure et accès Azure Key Vault derrière un pare-feu (https://docs.microsoft.com/en-us/azure/key-vault/key-vault-access-behind-firewall)</span><span class="sxs-lookup"><span data-stu-id="08abf-307">tooconfigure and access Azure Key Vault behind a firewall(https://docs.microsoft.com/en-us/azure/key-vault/key-vault-access-behind-firewall)</span></span>

* <span data-ttu-id="08abf-308">Utilisez la version la plus récente du Kit de développement logiciel Azure PowerShell version tooconfigure chiffrement de disque Azure hello.</span><span class="sxs-lookup"><span data-stu-id="08abf-308">Use hello latest version of Azure PowerShell SDK version tooconfigure Azure Disk Encryption.</span></span> <span data-ttu-id="08abf-309">Télécharger la version la plus récente de hello [Azure PowerShell version](https://github.com/Azure/azure-powershell/releases)</span><span class="sxs-lookup"><span data-stu-id="08abf-309">Download hello latest version of [Azure PowerShell release](https://github.com/Azure/azure-powershell/releases)</span></span>

 > [!NOTE]
  > <span data-ttu-id="08abf-310">Azure Disk Encryption n’est pas pris en charge dans le [Kit de développement logiciel (SDK) Azure PowerShell version 1.1.0](https://github.com/Azure/azure-powershell/releases/tag/v1.1.0-January2016).</span><span class="sxs-lookup"><span data-stu-id="08abf-310">Azure Disk Encryption is not supported on [Azure PowerShell SDK version 1.1.0](https://github.com/Azure/azure-powershell/releases/tag/v1.1.0-January2016).</span></span> <span data-ttu-id="08abf-311">Si vous recevez une erreur liés toousing Azure PowerShell 1.1.0, consultez [tooAzure Azure disque chiffrement erreur connexes PowerShell 1.1.0](http://blogs.msdn.com/b/azuresecurity/archive/2016/02/10/azure-disk-encryption-error-related-to-azure-powershell-1-1-0.aspx).</span><span class="sxs-lookup"><span data-stu-id="08abf-311">If you are receiving an error related toousing Azure PowerShell 1.1.0, see [Azure Disk Encryption Error Related tooAzure PowerShell 1.1.0](http://blogs.msdn.com/b/azuresecurity/archive/2016/02/10/azure-disk-encryption-error-related-to-azure-powershell-1-1-0.aspx).</span></span>

* <span data-ttu-id="08abf-312">toorun une commande CLI d’Azure et associez-le à votre abonnement Azure, vous devez d’abord installer CLI d’Azure :</span><span class="sxs-lookup"><span data-stu-id="08abf-312">toorun any Azure CLI command and associate it with your Azure subscription, you must first install Azure CLI:</span></span>
  * <span data-ttu-id="08abf-313">tooinstall CLI d’Azure et associez-le à votre abonnement Azure, consultez [comment tooinstall et configurer Azure CLI](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="08abf-313">tooinstall Azure CLI and associate it with your Azure subscription, see [How tooinstall and configure Azure CLI](../cli-install-nodejs.md).</span></span>
  * <span data-ttu-id="08abf-314">toouse CLI d’Azure pour Mac, Linux et Windows avec Azure Resource Manager, consultez [les commandes CLI d’Azure en mode de gestionnaire de ressources](../virtual-machines/azure-cli-arm-commands.md).</span><span class="sxs-lookup"><span data-stu-id="08abf-314">toouse Azure CLI for Mac, Linux, and Windows with Azure Resource Manager, see [Azure CLI commands in Resource Manager mode](../virtual-machines/azure-cli-arm-commands.md).</span></span>

* <span data-ttu-id="08abf-315">Lors du chiffrement d’un disque géré, il est obligatoire tootake requis un instantané du disque de hello géré ou une sauvegarde de disque hello en dehors de chiffrement tooenabling préalable de chiffrement de disque Azure.</span><span class="sxs-lookup"><span data-stu-id="08abf-315">When encrypting a managed disk, it is mandatory prerequisite tootake a snapshot of hello managed disk or a backup of hello disk outside of Azure Disk Encryption prior tooenabling encryption.</span></span>  <span data-ttu-id="08abf-316">Sans une sauvegarde en place, tout échec inattendu au cours du chiffrement peut rendre les disque hello et l’ordinateur virtuel inaccessibles sans une option de récupération.</span><span class="sxs-lookup"><span data-stu-id="08abf-316">Without a backup in place, any unexpected failure during encryption may render hello disk and VM inaccessible without a recovery option.</span></span>  <span data-ttu-id="08abf-317">Set-AzureRmVMDiskEncryptionExtension ne pas actuellement sauvegarder disques gérés et génèrent une erreur si utilisé sur un disque géré, sauf si hello - skipVmBackup paramètre a été spécifié.</span><span class="sxs-lookup"><span data-stu-id="08abf-317">Set-AzureRmVMDiskEncryptionExtension does not currently back up managed disks and will error if used against a managed disk unless hello -skipVmBackup parameter has been specified.</span></span>  <span data-ttu-id="08abf-318">Ce paramètre est toouse unsafe, sauf si une sauvegarde a déjà été apportée en dehors de chiffrement de disque Azure.</span><span class="sxs-lookup"><span data-stu-id="08abf-318">This parameter is unsafe toouse unless a backup has already been made outside of Azure Disk Encryption.</span></span>   <span data-ttu-id="08abf-319">Lorsque hello - skipVmBackup est précisé, applet de commande hello n’effectuera pas d’une sauvegarde de tooencryption préalable du disque hello géré.</span><span class="sxs-lookup"><span data-stu-id="08abf-319">When hello -skipVmBackup parameter is specified, hello cmdlet will not make a backup of hello managed disk prior tooencryption.</span></span>  <span data-ttu-id="08abf-320">Pour cette raison, il est considéré comme un toomake prérequis obligatoire vraiment besoin d’une sauvegarde de disque géré de hello que machine virtuelle est en place tooenabling préalable chiffrement de disque Azure en cas de récupération ultérieure.</span><span class="sxs-lookup"><span data-stu-id="08abf-320">For this reason, it is considered a mandatory prerequisite toomake sure a backup of hello managed disk VM is in place prior tooenabling Azure Disk Encryption in case recovery is later needed.</span></span>  
> [!NOTE]
 > <span data-ttu-id="08abf-321">paramètre de skipVmBackup - Hello ne doit jamais être utilisé sauf si une sauvegarde ou instantané a déjà été faite en dehors de chiffrement de disque Azure.</span><span class="sxs-lookup"><span data-stu-id="08abf-321">hello -skipVmBackup parameter should never be used unless a snapshot or backup has already been made outside of Azure Disk Encryption.</span></span> 

* <span data-ttu-id="08abf-322">Hello solutions de chiffrement de disque Azure utilise le protecteur de clé externe hello BitLocker pour les machines virtuelles IaaS de Windows.</span><span class="sxs-lookup"><span data-stu-id="08abf-322">hello Azure Disk Encryption solution uses hello BitLocker external key protector for Windows IaaS VMs.</span></span> <span data-ttu-id="08abf-323">Pour des machines virtuelles jointes au domaine, ne distribuez PAS de stratégies de groupe qui appliquent des protecteurs de Module de plateforme sécurisée (TPM).</span><span class="sxs-lookup"><span data-stu-id="08abf-323">For domain joined VMs, DO NOT push any group policies that enforce TPM protectors.</span></span> <span data-ttu-id="08abf-324">Pour plus d’informations sur la stratégie de groupe hello pour « Autoriser BitLocker sans un module de plateforme sécurisée compatible », consultez [référence de stratégie de groupe BitLocker](https://technet.microsoft.com/library/ee706521).</span><span class="sxs-lookup"><span data-stu-id="08abf-324">For information about hello group policy for “Allow BitLocker without a compatible TPM,” see [BitLocker Group Policy Reference](https://technet.microsoft.com/library/ee706521).</span></span>
* <span data-ttu-id="08abf-325">Stratégie de BitLocker sur les ordinateurs virtuels de joints à un domaine avec la stratégie de groupe personnalisé doit inclure hello suivant paramètre : `Configure user storage of bitlocker recovery information -> Allow 256-bit recovery key` chiffrement de disque Azure échoue lorsque les paramètres de stratégie de groupe personnalisé pour que Bitlocker sont incompatibles.</span><span class="sxs-lookup"><span data-stu-id="08abf-325">Bitlocker policy on domain joined virtual machines with custom group policy must include hello following setting: `Configure user storage of bitlocker recovery information -> Allow 256-bit recovery key`  Azure Disk Encryption will fail when custom group policy settings for Bitlocker are incompatible.</span></span> <span data-ttu-id="08abf-326">Sur les ordinateurs qui n’avaient pas hello correct paramètre de stratégie, appliquer la stratégie de nouvelle hello, forçant hello nouvelle stratégie tooupdate (gpupdate.exe /force) et le redémarrage peut être nécessaire.</span><span class="sxs-lookup"><span data-stu-id="08abf-326">On machines that did not have hello correct policy setting, applying hello new policy, forcing hello new policy tooupdate (gpupdate.exe /force), and then restarting may be required.</span></span>  
* <span data-ttu-id="08abf-327">toocreate une application Azure AD, créez un coffre de clés, ou configurer un coffre de clés existant et activer le chiffrement, consultez hello [script PowerShell requis de chiffrement de disque Azure](https://github.com/Azure/azure-powershell/blob/master/src/ResourceManager/Compute/Commands.Compute/Extension/AzureDiskEncryption/Scripts/AzureDiskEncryptionPreRequisiteSetup.ps1).</span><span class="sxs-lookup"><span data-stu-id="08abf-327">toocreate an Azure AD application, create a key vault, or set up an existing key vault and enable encryption, see hello [Azure Disk Encryption prerequisite PowerShell script](https://github.com/Azure/azure-powershell/blob/master/src/ResourceManager/Compute/Commands.Compute/Extension/AzureDiskEncryption/Scripts/AzureDiskEncryptionPreRequisiteSetup.ps1).</span></span>
* <span data-ttu-id="08abf-328">conditions préalables du chiffrement de disque tooconfigure à l’aide de hello CLI d’Azure, consultez [ce script Bash](https://github.com/ejarvi/ade-cli-getting-started).</span><span class="sxs-lookup"><span data-stu-id="08abf-328">tooconfigure disk-encryption prerequisites using hello Azure CLI, see [this Bash script](https://github.com/ejarvi/ade-cli-getting-started).</span></span>
* <span data-ttu-id="08abf-329">toouse hello Azure Backup service tooback haut et les machines virtuelles de restauration chiffrée, lorsque le chiffrement est activé avec le chiffrement du disque Azure, chiffrent vos machines virtuelles à l’aide de configuration de clé de chiffrement de disque Azure hello.</span><span class="sxs-lookup"><span data-stu-id="08abf-329">toouse hello Azure Backup service tooback up and restore encrypted VMs, when encryption is enabled with Azure Disk Encryption, encrypt your VMs by using hello Azure Disk Encryption key configuration.</span></span> <span data-ttu-id="08abf-330">Hello service de sauvegarde prend en charge les ordinateurs virtuels qui sont chiffrées à l’aide de la configuration de clés uniquement.</span><span class="sxs-lookup"><span data-stu-id="08abf-330">hello Backup service supports VMs that are encrypted using KEK configuration only.</span></span> <span data-ttu-id="08abf-331">Consultez [mode tooback configuration et restauration de chiffrement de machines virtuelles avec le chiffrement de sauvegarde Azure](https://docs.microsoft.com/en-us/azure/backup/backup-azure-vms-encryption).</span><span class="sxs-lookup"><span data-stu-id="08abf-331">See [How tooback up and restore encrypted virtual machines with Azure Backup  encryption](https://docs.microsoft.com/en-us/azure/backup/backup-azure-vms-encryption).</span></span>

* <span data-ttu-id="08abf-332">Lors du chiffrement d’un volume de système d’exploitation Linux, notez qu’un redémarrage de l’ordinateur virtuel est actuellement requis à fin hello du processus de hello.</span><span class="sxs-lookup"><span data-stu-id="08abf-332">When encrypting a Linux OS volume, note that a VM restart is currently required at hello end of hello process.</span></span> <span data-ttu-id="08abf-333">Cela est possible via le portail de hello, powershell ou CLI.</span><span class="sxs-lookup"><span data-stu-id="08abf-333">This can be done via hello portal, powershell, or CLI.</span></span>   <span data-ttu-id="08abf-334">progression de hello tootrack du chiffrement, interrogent régulièrement le message d’état hello retourné par Get-AzureRmVMDiskEncryptionStatus https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus.</span><span class="sxs-lookup"><span data-stu-id="08abf-334">tootrack hello progress of encryption, periodically poll hello status message returned by Get-AzureRmVMDiskEncryptionStatus https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus.</span></span>  <span data-ttu-id="08abf-335">Une fois que le chiffrement est terminé, message d’état hello hello retourné par cette commande indique cela.</span><span class="sxs-lookup"><span data-stu-id="08abf-335">Once encryption is complete, hello hello status message returned by this command will indicate this.</span></span>  <span data-ttu-id="08abf-336">Par exemple, « ProgressMessage : du disque du système d’exploitation a été chiffrée, redémarrez hello VM » à cette hello du point de machine virtuelle peut être redémarrée et utilisé.</span><span class="sxs-lookup"><span data-stu-id="08abf-336">For example, "ProgressMessage: OS disk successfully encrypted, please reboot hello VM"  At this point hello VM can be restarted and used.</span></span>  

* <span data-ttu-id="08abf-337">Le chiffrement des disques Azure pour Linux nécessite des disques de données toohave un système de fichiers monté tooencryption préalable de Linux</span><span class="sxs-lookup"><span data-stu-id="08abf-337">Azure Disk Encryption for Linux requires data disks toohave a mounted file system in Linux prior tooencryption</span></span>

* <span data-ttu-id="08abf-338">Récursive des disques de données montés ne sont pas pris en charge par hello chiffrement de disque Azure pour Linux.</span><span class="sxs-lookup"><span data-stu-id="08abf-338">Recursively mounted data disks are not supported by hello Azure Disk Encryption for Linux.</span></span> <span data-ttu-id="08abf-339">Par exemple, si hello système cible a été monté un disque sur /foo/bar et puis un autre sur /foo/bar/baz, chiffrement hello de /foo/bar/baz réussira, mais le chiffrement de barre/foo/échouera.</span><span class="sxs-lookup"><span data-stu-id="08abf-339">For example, if hello target system has mounted a disk on /foo/bar and then another on /foo/bar/baz, hello encryption of /foo/bar/baz will succeed, but encryption of /foo/bar will fail.</span></span> 

* <span data-ttu-id="08abf-340">Chiffrement de disque Azure est uniquement pris en charge sur les images de la galerie Azure pris en charge que les conditions préalables hello susmentionnés.</span><span class="sxs-lookup"><span data-stu-id="08abf-340">Azure Disk Encryption is only supported on Azure gallery supported images that meet hello aforementioned prerequisites.</span></span> <span data-ttu-id="08abf-341">Images personnalisées du client ne sont pas pris en charge en raison des schémas de partition toocustom et les comportements de processus qui peuvent exister sur ces images.</span><span class="sxs-lookup"><span data-stu-id="08abf-341">Customer custom images are not supported due toocustom partition schemes and process behaviors that may exist on these images.</span></span> <span data-ttu-id="08abf-342">De plus, même les machines virtuelles d’image de galerie, qui initialement remplissaient les conditions préalables demandées, mais qui ont été modifiées depuis leur création, peuvent être incompatibles.</span><span class="sxs-lookup"><span data-stu-id="08abf-342">Further, even gallery image based VM's that initially met prerequisites but have been modified after creation may be incompatible.</span></span>  <span data-ttu-id="08abf-343">Pour que raison, hello suggéré procédure pour chiffrer un VM Linux est toostart à partir d’une image de galerie nettoyer, chiffrer hello machine virtuelle, puis ajoutez personnalisée de logiciels ou des données toohello machine virtuelle en fonction des besoins.</span><span class="sxs-lookup"><span data-stu-id="08abf-343">For that reason, hello suggested procedure for encrypting a Linux VM is toostart from a clean gallery image, encrypt hello VM, and then add custom software or data toohello VM as needed.</span></span>  

> [!NOTE]
> <span data-ttu-id="08abf-344">Sauvegarde et restauration de machines virtuelles chiffrés est pris en charge uniquement pour les ordinateurs virtuels qui sont chiffrés avec une configuration de clés hello.</span><span class="sxs-lookup"><span data-stu-id="08abf-344">Backup and restore of encrypted VMs is supported only for VMs that are encrypted with hello KEK configuration.</span></span> <span data-ttu-id="08abf-345">Elles ne sont pas prises en charge pour les machines virtuelles chiffrées sans KEK.</span><span class="sxs-lookup"><span data-stu-id="08abf-345">It is not supported on VMs that are encrypted without KEK.</span></span> <span data-ttu-id="08abf-346">KEK est un paramètre facultatif qui active une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="08abf-346">KEK is an optional parameter that enables VM.</span></span>

#### <a name="set-up-hello-azure-ad-application-in-azure-active-directory"></a><span data-ttu-id="08abf-347">Configurer application Azure AD hello dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="08abf-347">Set up hello Azure AD application in Azure Active Directory</span></span>
<span data-ttu-id="08abf-348">Lorsque vous devez toobe chiffrement activé sur une machine virtuelle dans Azure, le chiffrement des disques Azure génère et écrit le coffre de clés hello chiffrement clés tooyour.</span><span class="sxs-lookup"><span data-stu-id="08abf-348">When you need encryption toobe enabled on a running VM in Azure, Azure Disk Encryption generates and writes hello encryption keys tooyour key vault.</span></span> <span data-ttu-id="08abf-349">La gestion des clés de chiffrement dans votre coffre de clés nécessite l’authentification Azure AD.</span><span class="sxs-lookup"><span data-stu-id="08abf-349">Managing encryption keys in your key vault requires Azure AD authentication.</span></span>

<span data-ttu-id="08abf-350">Une application Azure AD doit donc être créée à cet effet.</span><span class="sxs-lookup"><span data-stu-id="08abf-350">For this purpose, create an Azure AD application.</span></span> <span data-ttu-id="08abf-351">Vous trouverez des instructions détaillées pour l’inscription d’une application de section de « Obtenir une identité pour hello Application » hello de billet de blog hello [le coffre de clés Azure - étape par étape](http://blogs.technet.com/b/kv/archive/2015/06/02/azure-key-vault-step-by-step.aspx).</span><span class="sxs-lookup"><span data-stu-id="08abf-351">You can find detailed steps for registering an application in hello “Get an Identity for hello Application” section of hello blog post [Azure Key Vault - Step by Step](http://blogs.technet.com/b/kv/archive/2015/06/02/azure-key-vault-step-by-step.aspx).</span></span> <span data-ttu-id="08abf-352">Cet article contient également plusieurs exemples utiles sur l’installation et la configuration de votre coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="08abf-352">This post also contains a number of helpful examples for setting up and configuring your key vault.</span></span> <span data-ttu-id="08abf-353">Pour l’authentification, vous pouvez utiliser soit l’authentification par clé secrète de client, soit l’authentification Azure AD par certificat de client.</span><span class="sxs-lookup"><span data-stu-id="08abf-353">For authentication purposes, you can use either client secret-based authentication or client certificate-based Azure AD authentication.</span></span>

#### <a name="client-secret-based-authentication-for-azure-ad"></a><span data-ttu-id="08abf-354">Authentification par clé secrète de client pour Azure AD</span><span class="sxs-lookup"><span data-stu-id="08abf-354">Client secret-based authentication for Azure AD</span></span>
<span data-ttu-id="08abf-355">les sections Hello qui suivent peuvent vous aider à configurer une authentification basée sur une clé secrète du client pour Azure AD.</span><span class="sxs-lookup"><span data-stu-id="08abf-355">hello sections that follow can help you configure a client secret-based authentication for Azure AD.</span></span>

##### <a name="create-an-azure-ad-application-by-using-azure-powershell"></a><span data-ttu-id="08abf-356">Créer une application Azure AD à l’aide d’Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="08abf-356">Create an Azure AD application by using Azure PowerShell</span></span>
<span data-ttu-id="08abf-357">Utilisez hello suivant toocreate d’applet de commande PowerShell une application Azure AD :</span><span class="sxs-lookup"><span data-stu-id="08abf-357">Use hello following PowerShell cmdlet toocreate an Azure AD application:</span></span>

    $aadClientSecret = "yourSecret"
    $azureAdApplication = New-AzureRmADApplication -DisplayName "<Your Application Display Name>" -HomePage "<https://YourApplicationHomePage>" -IdentifierUris "<https://YouApplicationUri>" -Password $aadClientSecret
    $servicePrincipal = New-AzureRmADServicePrincipal –ApplicationId $azureAdApplication.ApplicationId

> [!NOTE]
> <span data-ttu-id="08abf-358">$azureAdApplication.ApplicationId est hello Azure AD ClientID et $aadClientSecret est la clé secrète du client hello que vous devez utiliser tooenable ultérieure le chiffrement des disques Azure.</span><span class="sxs-lookup"><span data-stu-id="08abf-358">$azureAdApplication.ApplicationId is hello Azure AD ClientID and $aadClientSecret is hello client secret that you should use later tooenable Azure Disk Encryption.</span></span> <span data-ttu-id="08abf-359">Protéger la question secrète du client hello Azure AD en conséquence.</span><span class="sxs-lookup"><span data-stu-id="08abf-359">Safeguard hello Azure AD client secret appropriately.</span></span>

##### <a name="setting-up-hello-azure-ad-client-id-and-secret-from-hello-azure-classic-portal"></a><span data-ttu-id="08abf-360">Configuration d’ID de client hello Azure AD et la clé secrète à partir de hello portail Azure classic</span><span class="sxs-lookup"><span data-stu-id="08abf-360">Setting up hello Azure AD client ID and secret from hello Azure classic portal</span></span>
<span data-ttu-id="08abf-361">Vous pouvez également configurer votre ID client Azure AD et la clé secrète à l’aide de hello [portail Azure classic]( https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="08abf-361">You can also set up your Azure AD client ID and secret by using hello [Azure classic portal]( https://manage.windowsazure.com).</span></span> <span data-ttu-id="08abf-362">tooperform cette tâche, procédez comme hello suivant :</span><span class="sxs-lookup"><span data-stu-id="08abf-362">tooperform this task, do hello following:</span></span>

1. <span data-ttu-id="08abf-363">Cliquez sur hello **Active Directory** onglet.</span><span class="sxs-lookup"><span data-stu-id="08abf-363">Click hello **Active Directory** tab.</span></span>

 ![Azure Disk Encryption](./media/azure-security-disk-encryption/disk-encryption-fig3.png)

2. <span data-ttu-id="08abf-365">Cliquez sur **ajouter une Application**et puis type hello nom de l’application.</span><span class="sxs-lookup"><span data-stu-id="08abf-365">Click **Add Application**, and then type hello application name.</span></span>

 ![Azure Disk Encryption](./media/azure-security-disk-encryption/disk-encryption-fig4.png)

3. <span data-ttu-id="08abf-367">Cliquez sur le bouton de flèche hello, puis configurez les propriétés de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="08abf-367">Click hello arrow button, and then configure hello application properties.</span></span>

 ![Azure Disk Encryption](./media/azure-security-disk-encryption/disk-encryption-fig5.png)

4. <span data-ttu-id="08abf-369">Cliquez sur case à cocher hello dans hello inférieure gauche toofinish.</span><span class="sxs-lookup"><span data-stu-id="08abf-369">Click hello check mark in hello lower left corner toofinish.</span></span> <span data-ttu-id="08abf-370">page de configuration d’application Hello s’affiche, et ID de client Azure AD hello s’affiche en bas de hello de page de hello.</span><span class="sxs-lookup"><span data-stu-id="08abf-370">hello application configuration page appears, and hello Azure AD client ID is displayed at hello bottom of hello page.</span></span>

 ![Azure Disk Encryption](./media/azure-security-disk-encryption/disk-encryption-fig6.png)

5. <span data-ttu-id="08abf-372">Enregistrer la clé secrète du client hello Azure AD en cliquant sur hello **enregistrer** bouton.</span><span class="sxs-lookup"><span data-stu-id="08abf-372">Save hello Azure AD client secret by clicking hello **Save** button.</span></span> <span data-ttu-id="08abf-373">Notez la clé secrète du client dans la zone de texte hello clés hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="08abf-373">Note hello Azure AD client secret in hello keys text box.</span></span> <span data-ttu-id="08abf-374">Prenez soin de bien la sauvegarder.</span><span class="sxs-lookup"><span data-stu-id="08abf-374">Safeguard it appropriately.</span></span>

 ![Azure Disk Encryption](./media/azure-security-disk-encryption/disk-encryption-fig7.png)

 > [!NOTE]
 > <span data-ttu-id="08abf-376">Hello précédant le flux n’est pas pris en charge sur hello portail Azure classic.</span><span class="sxs-lookup"><span data-stu-id="08abf-376">hello preceding flow is not supported on hello Azure classic portal.</span></span>

##### <a name="use-an-existing-application"></a><span data-ttu-id="08abf-377">Utiliser une application existante</span><span class="sxs-lookup"><span data-stu-id="08abf-377">Use an existing application</span></span>
<span data-ttu-id="08abf-378">tooexecute hello suivant de commandes, d’obtenir et utiliser hello [module PowerShell Azure AD](https://technet.microsoft.com/library/jj151815.aspx).</span><span class="sxs-lookup"><span data-stu-id="08abf-378">tooexecute hello following commands, obtain and use hello [Azure AD PowerShell module](https://technet.microsoft.com/library/jj151815.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="08abf-379">Hello les commandes suivantes doivent être exécutées à partir d’une nouvelle fenêtre PowerShell.</span><span class="sxs-lookup"><span data-stu-id="08abf-379">hello following commands must be executed from a new PowerShell window.</span></span> <span data-ttu-id="08abf-380">N’utilisez pas d’Azure PowerShell ou commandes de hello Azure Resource Manager fenêtre tooexecute hello.</span><span class="sxs-lookup"><span data-stu-id="08abf-380">Do not use Azure PowerShell or hello Azure Resource Manager window tooexecute hello commands.</span></span> <span data-ttu-id="08abf-381">Nous recommandons cette approche, car ces applets de commande sont dans le module MSOnline de hello ou Azure AD PowerShell.</span><span class="sxs-lookup"><span data-stu-id="08abf-381">We recommend this approach because these cmdlets are in hello MSOnline module or Azure AD PowerShell.</span></span>

    $clientSecret = ‘<yourAadClientSecret>’
    $aadClientID = '<Client ID of your Azure AD application>'
    connect-msolservice
    New-MsolServicePrincipalCredential -AppPrincipalId $aadClientID -Type password -Value $clientSecret

#### <a name="certificate-based-authentication-for-azure-ad"></a><span data-ttu-id="08abf-382">Authentification par certificat pour Azure AD</span><span class="sxs-lookup"><span data-stu-id="08abf-382">Certificate-based authentication for Azure AD</span></span>
> [!NOTE]
> <span data-ttu-id="08abf-383">L’authentification par certificat Azure AD n’est actuellement pas prise en charge sur les machines virtuelles Linux.</span><span class="sxs-lookup"><span data-stu-id="08abf-383">Azure AD certificate-based authentication is currently not supported on Linux VMs.</span></span>

<span data-ttu-id="08abf-384">Hello les sections suivantes indiquent comment tooconfigure une authentification basée sur certificat pour Azure AD.</span><span class="sxs-lookup"><span data-stu-id="08abf-384">hello sections that follow show how tooconfigure a certificate-based authentication for Azure AD.</span></span>

##### <a name="create-an-azure-ad-application"></a><span data-ttu-id="08abf-385">Créer une application Azure AD</span><span class="sxs-lookup"><span data-stu-id="08abf-385">Create an Azure AD application</span></span>
<span data-ttu-id="08abf-386">toocreate une application Azure AD, exécutez hello suivant d’applets de commande PowerShell :</span><span class="sxs-lookup"><span data-stu-id="08abf-386">toocreate an Azure AD application, execute hello following PowerShell cmdlets:</span></span>

> [!NOTE]
> <span data-ttu-id="08abf-387">Remplacez hello suit `yourpassword` avec votre mot de passe sécurisé et le mot de passe de sauvegarde hello de chaîne.</span><span class="sxs-lookup"><span data-stu-id="08abf-387">Replace hello following `yourpassword` string with your secure password, and safeguard hello password.</span></span>

    $cert = New-Object System.Security.Cryptography.X509Certificates.X509Certificate("C:\certificates\examplecert.pfx", "yourpassword")
    $keyValue = [System.Convert]::ToBase64String($cert.GetRawCertData())
    $azureAdApplication = New-AzureRmADApplication -DisplayName "<Your Application Display Name>" -HomePage "<https://YourApplicationHomePage>" -IdentifierUris "<https://YouApplicationUri>" -KeyValue $keyValue -KeyType AsymmetricX509Cert
    $servicePrincipal = New-AzureRmADServicePrincipal –ApplicationId $azureAdApplication.ApplicationId

<span data-ttu-id="08abf-388">Une fois que vous avez terminé cette étape, téléchargez un coffre de clés tooyour de fichier PFX et activer hello accès stratégie nécessaires toodeploy que tooa certificat machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="08abf-388">After you finish this step, upload a PFX file tooyour key vault and enable hello access policy needed toodeploy that certificate tooa VM.</span></span>

##### <a name="use-an-existing-azure-ad-application"></a><span data-ttu-id="08abf-389">Utiliser une application Azure AD existante</span><span class="sxs-lookup"><span data-stu-id="08abf-389">Use an existing Azure AD application</span></span>
<span data-ttu-id="08abf-390">Si vous configurez l’authentification par certificat pour une application existante, utilisez les applets de commande PowerShell hello indiqué ici.</span><span class="sxs-lookup"><span data-stu-id="08abf-390">If you are configuring certificate-based authentication for an existing application, use hello PowerShell cmdlets shown here.</span></span> <span data-ttu-id="08abf-391">Être tooexecute vraiment à partir d’une nouvelle fenêtre PowerShell.</span><span class="sxs-lookup"><span data-stu-id="08abf-391">Be sure tooexecute them from a new PowerShell window.</span></span>

    $certLocalPath = 'C:\certs\myaadapp.cer'
    $aadClientID = '<Client ID of your Azure AD application>'
    connect-msolservice
    $cer = New-Object System.Security.Cryptography.X509Certificates.X509Certificate
    $cer.Import($certLocalPath)
    $binCert = $cer.GetRawCertData()
    $credValue = [System.Convert]::ToBase64String($binCert);
    New-MsolServicePrincipalCredential -AppPrincipalId $aadClientID -Type asymmetric -Value $credValue -Usage verify

<span data-ttu-id="08abf-392">Une fois que vous avez terminé cette étape, téléchargez un coffre de clés tooyour de fichier PFX et activer la stratégie d’accès hello toodeploy hello certificat tooa machine virtuelle que nécessaire.</span><span class="sxs-lookup"><span data-stu-id="08abf-392">After you finish this step, upload a PFX file tooyour key vault and enable hello access policy that's needed toodeploy hello certificate tooa VM.</span></span>

##### <a name="upload-a-pfx-file-tooyour-key-vault"></a><span data-ttu-id="08abf-393">Télécharger un coffre de clés tooyour de fichier PFX</span><span class="sxs-lookup"><span data-stu-id="08abf-393">Upload a PFX file tooyour key vault</span></span>
<span data-ttu-id="08abf-394">Pour obtenir une explication détaillée de ce processus, consultez [hello Blog de l’équipe officiel Azure Key Vault](http://blogs.technet.com/b/kv/archive/2015/07/14/vm_2d00_certificates.aspx).</span><span class="sxs-lookup"><span data-stu-id="08abf-394">For a detailed explanation of this process, see [hello Official Azure Key Vault Team Blog](http://blogs.technet.com/b/kv/archive/2015/07/14/vm_2d00_certificates.aspx).</span></span> <span data-ttu-id="08abf-395">Toutefois, hello suivant d’applets de commande PowerShell est nécessaire pour la tâche hello.</span><span class="sxs-lookup"><span data-stu-id="08abf-395">However, hello following PowerShell cmdlets are all you need for hello task.</span></span> <span data-ttu-id="08abf-396">Être tooexecute que les à partir de la console Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="08abf-396">Be sure tooexecute them from Azure PowerShell console.</span></span>

> [!NOTE]
> <span data-ttu-id="08abf-397">Remplacez hello suit `yourpassword` avec votre mot de passe sécurisé et le mot de passe de sauvegarde hello de chaîne.</span><span class="sxs-lookup"><span data-stu-id="08abf-397">Replace hello following `yourpassword` string with your secure password, and safeguard hello password.</span></span>

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

##### <a name="deploy-a-certificate-in-your-key-vault-tooan-existing-vm"></a><span data-ttu-id="08abf-398">Déployer un certificat dans votre tooan de coffre de clés existant de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="08abf-398">Deploy a certificate in your key vault tooan existing VM</span></span>
<span data-ttu-id="08abf-399">Après avoir terminé le téléchargement hello PFX, déployez un certificat dans hello tooan de coffre de clés existant de machine virtuelle avec les éléments suivants de hello :</span><span class="sxs-lookup"><span data-stu-id="08abf-399">After you finish uploading hello PFX, deploy a certificate in hello key vault tooan existing VM with hello following:</span></span>
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

#### <a name="set-up-hello-key-vault-access-policy-for-hello-azure-ad-application"></a><span data-ttu-id="08abf-400">Configurer la stratégie d’accès hello coffre de clés pour l’application hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="08abf-400">Set up hello key vault access policy for hello Azure AD application</span></span>
<span data-ttu-id="08abf-401">Votre application Azure AD a besoin de clés de droits tooaccess hello ou des clés secrètes dans le coffre hello.</span><span class="sxs-lookup"><span data-stu-id="08abf-401">Your Azure AD application needs rights tooaccess hello keys or secrets in hello vault.</span></span> <span data-ttu-id="08abf-402">Hello d’utilisation [ `Set-AzureKeyVaultAccessPolicy` ](/powershell/module/azure/set-azurekeyvaultaccesspolicy?view=azuresmps-3.7.0) applet de commande toogrant autorisations toohello application, en utilisant les ID de client hello (qui a été générée lors de l’application hello a été inscrit) comme hello _– ServicePrincipalName_ valeur du paramètre.</span><span class="sxs-lookup"><span data-stu-id="08abf-402">Use hello [`Set-AzureKeyVaultAccessPolicy`](/powershell/module/azure/set-azurekeyvaultaccesspolicy?view=azuresmps-3.7.0) cmdlet toogrant permissions toohello application, using hello client ID (which was generated when hello application was registered) as hello _–ServicePrincipalName_ parameter value.</span></span> <span data-ttu-id="08abf-403">toolearn plus, consultez hello billet de blog [le coffre de clés Azure - étape par étape](http://blogs.technet.com/b/kv/archive/2015/06/02/azure-key-vault-step-by-step.aspx).</span><span class="sxs-lookup"><span data-stu-id="08abf-403">toolearn more, see hello blog post [Azure Key Vault - Step by Step](http://blogs.technet.com/b/kv/archive/2015/06/02/azure-key-vault-step-by-step.aspx).</span></span> <span data-ttu-id="08abf-404">Voici un exemple de comment tooperform cette tâche PowerShell :</span><span class="sxs-lookup"><span data-stu-id="08abf-404">Here is an example of how tooperform this task via PowerShell:</span></span>

    $keyVaultName = '<yourKeyVaultName>'
    $aadClientID = '<yourAadAppClientID>'
    $rgname = '<yourResourceGroup>'
    Set-AzureRmKeyVaultAccessPolicy -VaultName $keyVaultName -ServicePrincipalName $aadClientID -PermissionsToKeys 'WrapKey' -PermissionsToSecrets 'Set' -ResourceGroupName $rgname

> [!NOTE]
> <span data-ttu-id="08abf-405">Le chiffrement des disques Azure nécessite que vous hello tooconfigure suite de l’application de client accès stratégies tooyour Azure AD : _WrapKey_ et _définir_ autorisations.</span><span class="sxs-lookup"><span data-stu-id="08abf-405">Azure Disk Encryption requires you tooconfigure hello following access policies tooyour Azure AD client application: _WrapKey_ and _Set_ permissions.</span></span>

## <a name="terminology"></a><span data-ttu-id="08abf-406">Terminologie</span><span class="sxs-lookup"><span data-stu-id="08abf-406">Terminology</span></span>
<span data-ttu-id="08abf-407">toounderstand certains des termes courants de hello utilisé par cette technologie, hello utilisez terminologie tableau suivant :</span><span class="sxs-lookup"><span data-stu-id="08abf-407">toounderstand some of hello common terms used by this technology, use hello following terminology table:</span></span>

| <span data-ttu-id="08abf-408">Terminologie</span><span class="sxs-lookup"><span data-stu-id="08abf-408">Terminology</span></span> | <span data-ttu-id="08abf-409">Définition</span><span class="sxs-lookup"><span data-stu-id="08abf-409">Definition</span></span> |
| --- | --- |
| <span data-ttu-id="08abf-410">Azure AD</span><span class="sxs-lookup"><span data-stu-id="08abf-410">Azure AD</span></span> | <span data-ttu-id="08abf-411">Azure AD est [Azure Active Directory](https://azure.microsoft.com/documentation/services/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="08abf-411">Azure AD is [Azure Active Directory](https://azure.microsoft.com/documentation/services/active-directory/).</span></span> <span data-ttu-id="08abf-412">Un compte Azure AD est requis pour l’authentification, le stockage et l’extraction des clés secrètes d’un coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="08abf-412">An Azure AD account is a prerequisite for authenticating, storing, and retrieving secrets from a key vault.</span></span> |
| <span data-ttu-id="08abf-413">coffre de clés Azure</span><span class="sxs-lookup"><span data-stu-id="08abf-413">Azure Key Vault</span></span> | <span data-ttu-id="08abf-414">Key Vault est un service de gestion de clés de chiffrement basé sur des modules de sécurité matériels FIPS (Federal Information Processing Standards) qui vous permet de protéger vos clés de chiffrement et les clés secrètes sensibles.</span><span class="sxs-lookup"><span data-stu-id="08abf-414">Key Vault is a cryptographic, key management service that's based on Federal Information Processing Standards (FIPS)-validated hardware security modules, which help safeguard your cryptographic keys and sensitive secrets.</span></span> <span data-ttu-id="08abf-415">Pour plus d’informations, consultez la documentation relative à [Key Vault](https://azure.microsoft.com/services/key-vault/).</span><span class="sxs-lookup"><span data-stu-id="08abf-415">For more information, see [Key Vault](https://azure.microsoft.com/services/key-vault/) documentation.</span></span> |
| <span data-ttu-id="08abf-416">ARM</span><span class="sxs-lookup"><span data-stu-id="08abf-416">ARM</span></span> | <span data-ttu-id="08abf-417">Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="08abf-417">Azure Resource Manager</span></span> |
| <span data-ttu-id="08abf-418">BitLocker</span><span class="sxs-lookup"><span data-stu-id="08abf-418">BitLocker</span></span> |<span data-ttu-id="08abf-419">[BitLocker](https://technet.microsoft.com/library/hh831713.aspx) est une secteur d’activité Windows volume technologie de chiffrement utilisée par un chiffrement de disque tooenable sur les machines virtuelles IaaS Windows.</span><span class="sxs-lookup"><span data-stu-id="08abf-419">[BitLocker](https://technet.microsoft.com/library/hh831713.aspx) is an industry-recognized Windows volume encryption technology that's used tooenable disk encryption on Windows IaaS VMs.</span></span> |
| <span data-ttu-id="08abf-420">BEK</span><span class="sxs-lookup"><span data-stu-id="08abf-420">BEK</span></span> | <span data-ttu-id="08abf-421">Les clés de chiffrement BitLocker sont le volume de démarrage utilisé tooencrypt hello du système d’exploitation et les volumes de données.</span><span class="sxs-lookup"><span data-stu-id="08abf-421">BitLocker encryption keys are used tooencrypt hello OS boot volume and data volumes.</span></span> <span data-ttu-id="08abf-422">les clés BitLocker Hello sont sauvegardés dans un coffre de clés en tant que clés secrètes.</span><span class="sxs-lookup"><span data-stu-id="08abf-422">hello BitLocker keys are safeguarded in a key vault as secrets.</span></span> |
| <span data-ttu-id="08abf-423">Interface de ligne de commande</span><span class="sxs-lookup"><span data-stu-id="08abf-423">CLI</span></span> | <span data-ttu-id="08abf-424">Voir [Interface de ligne de commande Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="08abf-424">See [Azure command-line interface](../cli-install-nodejs.md).</span></span> |
| <span data-ttu-id="08abf-425">DM-Crypt</span><span class="sxs-lookup"><span data-stu-id="08abf-425">DM-Crypt</span></span> |<span data-ttu-id="08abf-426">[Exploration de données-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) sous-système de chiffrement de disque basés sur Linux, transparent hello qui a utilisé un chiffrement de disque tooenable sur les machines virtuelles IaaS Linux.</span><span class="sxs-lookup"><span data-stu-id="08abf-426">[DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) is hello Linux-based, transparent disk-encryption subsystem that's used tooenable disk encryption on Linux IaaS VMs.</span></span> |
| <span data-ttu-id="08abf-427">KEK</span><span class="sxs-lookup"><span data-stu-id="08abf-427">KEK</span></span> | <span data-ttu-id="08abf-428">Clé de chiffrement est hello clé asymétrique (RSA 2048) que vous pouvez utiliser tooprotect ou encapsuler le code secret hello.</span><span class="sxs-lookup"><span data-stu-id="08abf-428">Key encryption key is hello asymmetric key (RSA 2048) that you can use tooprotect or wrap hello secret.</span></span> <span data-ttu-id="08abf-429">Vous pouvez fournir une clé protégée par le module HSM ou une clé protégée par le logiciel.</span><span class="sxs-lookup"><span data-stu-id="08abf-429">You can provide a hardware security modules (HSM)-protected key or software-protected key.</span></span> <span data-ttu-id="08abf-430">Pour plus d’informations, consultez la documentation relative à [Azure Key Vault](https://azure.microsoft.com/services/key-vault/).</span><span class="sxs-lookup"><span data-stu-id="08abf-430">For more details, see [Azure Key Vault](https://azure.microsoft.com/services/key-vault/) documentation.</span></span> |
| <span data-ttu-id="08abf-431">Applets de commande PS</span><span class="sxs-lookup"><span data-stu-id="08abf-431">PS cmdlets</span></span> | <span data-ttu-id="08abf-432">Voir [Applets de commande Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="08abf-432">See [Azure PowerShell cmdlets](/powershell/azure/overview).</span></span> |

### <a name="set-up-and-configure-your-key-vault-for-azure-disk-encryption"></a><span data-ttu-id="08abf-433">Créer et configurer votre coffre de clés pour Azure Disk Encryption</span><span class="sxs-lookup"><span data-stu-id="08abf-433">Set up and configure your key vault for Azure Disk Encryption</span></span>
<span data-ttu-id="08abf-434">Le chiffrement des disques Azure permet de protéger les clés de chiffrement de disque hello et les clés secrètes dans votre coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="08abf-434">Azure Disk Encryption helps safeguard hello disk-encryption keys and secrets in your key vault.</span></span> <span data-ttu-id="08abf-435">tooset de votre coffre de clés de chiffrement de disque Azure, hello terminé les étapes dans chacune des hello les sections suivantes.</span><span class="sxs-lookup"><span data-stu-id="08abf-435">tooset up your key vault for Azure Disk Encryption, complete hello steps in each of hello following sections.</span></span>

#### <a name="create-a-key-vault"></a><span data-ttu-id="08abf-436">Création d’un coffre de clés</span><span class="sxs-lookup"><span data-stu-id="08abf-436">Create a key vault</span></span>
<span data-ttu-id="08abf-437">toocreate un coffre de clés, utilisez une des options suivantes de hello :</span><span class="sxs-lookup"><span data-stu-id="08abf-437">toocreate a key vault, use one of hello following options:</span></span>

* [<span data-ttu-id="08abf-438">Modèle Resource Manager « 101-Key-Vault-Create »</span><span class="sxs-lookup"><span data-stu-id="08abf-438">"101-Key-Vault-Create" Resource Manager template</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-key-vault-create)
* [<span data-ttu-id="08abf-439">Applets de commande Key Vault Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="08abf-439">Azure PowerShell key vault cmdlets</span></span>](/powershell/module/azurerm.keyvault/#key_vault)
* <span data-ttu-id="08abf-440">Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="08abf-440">Azure Resource Manager</span></span>
* <span data-ttu-id="08abf-441">Comment trop[sécuriser votre coffre de clés](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-secure-your-key-vault)</span><span class="sxs-lookup"><span data-stu-id="08abf-441">How too[Secure your key vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-secure-your-key-vault)</span></span>

> [!NOTE]
> <span data-ttu-id="08abf-442">Si vous avez déjà configuré un coffre de clés pour votre abonnement, ignorer la section suivante de toohello.</span><span class="sxs-lookup"><span data-stu-id="08abf-442">If you have already set up a key vault for your subscription, skip toohello next section.</span></span>

![coffre de clés Azure](./media/azure-security-disk-encryption/keyvault-portal-fig1.png)

#### <a name="set-up-a-key-encryption-key-optional"></a><span data-ttu-id="08abf-444">Configurer une clé de chiffrement à clé (facultatif)</span><span class="sxs-lookup"><span data-stu-id="08abf-444">Set up a key encryption key (optional)</span></span>
<span data-ttu-id="08abf-445">Si vous souhaitez toouse une clés pour une couche supplémentaire de sécurité pour les clés de chiffrement BitLocker hello, ajoutez un coffre de clés tooyour de clés.</span><span class="sxs-lookup"><span data-stu-id="08abf-445">If you want toouse a KEK for an additional layer of security for hello BitLocker encryption keys, add a KEK tooyour key vault.</span></span> <span data-ttu-id="08abf-446">Hello d’utilisation [ `Add-AzureKeyVaultKey` ](/powershell/module/azurerm.keyvault/add-azurermkeyvaultkey) toocreate de l’applet de commande une clé de chiffrement dans le coffre de clés hello.</span><span class="sxs-lookup"><span data-stu-id="08abf-446">Use hello [`Add-AzureKeyVaultKey`](/powershell/module/azurerm.keyvault/add-azurermkeyvaultkey) cmdlet toocreate a key encryption key in hello key vault.</span></span> <span data-ttu-id="08abf-447">Vous pouvez également importer une clé de chiffrement à clé à partir de votre module de sécurité matériel de gestion des clés locales.</span><span class="sxs-lookup"><span data-stu-id="08abf-447">You can also import a KEK from your on-premises key management HSM.</span></span> <span data-ttu-id="08abf-448">Pour plus d’informations, consultez la [Documentation relative à Key Vault](https://azure.microsoft.com/documentation/services/key-vault/).</span><span class="sxs-lookup"><span data-stu-id="08abf-448">For more details, see [Key Vault Documentation](https://azure.microsoft.com/documentation/services/key-vault/).</span></span>

    Add-AzureKeyVaultKey [-VaultName] <string> [-Name] <string> -Destination <string> {HSM | Software}

<span data-ttu-id="08abf-449">Vous pouvez ajouter hello veillent en accédant tooAzure Gestionnaire de ressources ou à l’aide de l’interface de coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="08abf-449">You can add hello KEK by going tooAzure Resource Manager or by using your key vault interface.</span></span>

![coffre de clés Azure](./media/azure-security-disk-encryption/keyvault-portal-fig2.png)

#### <a name="set-key-vault-permissions"></a><span data-ttu-id="08abf-451">Définir des autorisations d’accès au coffre de clés</span><span class="sxs-lookup"><span data-stu-id="08abf-451">Set key vault permissions</span></span>
<span data-ttu-id="08abf-452">Hello plateforme Azure a besoin de clés de chiffrement toohello accès ou les clés secrètes dans votre coffre de clés de toomake les toohello disponible machine virtuelle pour le démarrage et le déchiffrement des volumes de hello.</span><span class="sxs-lookup"><span data-stu-id="08abf-452">hello Azure platform needs access toohello encryption keys or secrets in your key vault toomake them available toohello VM for booting and decrypting hello volumes.</span></span> <span data-ttu-id="08abf-453">toogrant autorisations toohello plateforme Azure, jeu hello **EnabledForDiskEncryption** propriété dans la clé de hello coffre à l’aide d’applet de commande PowerShell de coffre de clés hello :</span><span class="sxs-lookup"><span data-stu-id="08abf-453">toogrant permissions toohello Azure platform, set hello **EnabledForDiskEncryption** property in hello key vault by using hello key vault PowerShell cmdlet:</span></span>

    Set-AzureRmKeyVaultAccessPolicy -VaultName <yourVaultName> -ResourceGroupName <yourResourceGroup> -EnabledForDiskEncryption

<span data-ttu-id="08abf-454">Vous pouvez également définir hello **EnabledForDiskEncryption** propriété en visitant hello [Explorateur de ressources Azure](https://resources.azure.com).</span><span class="sxs-lookup"><span data-stu-id="08abf-454">You can also set hello **EnabledForDiskEncryption** property by visiting hello [Azure Resource Explorer](https://resources.azure.com).</span></span>

<span data-ttu-id="08abf-455">Comme mentionné précédemment, vous devez définir hello **EnabledForDiskEncryption** propriété sur votre coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="08abf-455">As mentioned earlier, you must set hello **EnabledForDiskEncryption** property on your key vault.</span></span> <span data-ttu-id="08abf-456">Dans le cas contraire, le déploiement de hello échoue.</span><span class="sxs-lookup"><span data-stu-id="08abf-456">Otherwise, hello deployment will fail.</span></span>

<span data-ttu-id="08abf-457">Vous pouvez définir des stratégies d’accès pour votre application Azure AD à partir de l’interface du coffre de clés hello, comme illustré ici :</span><span class="sxs-lookup"><span data-stu-id="08abf-457">You can set up access policies for your Azure AD application from hello key vault interface, as shown here:</span></span>

![coffre de clés Azure](./media/azure-security-disk-encryption/keyvault-portal-fig3.png)

![coffre de clés Azure](./media/azure-security-disk-encryption/keyvault-portal-fig3b.png)

<span data-ttu-id="08abf-460">Sur hello **des stratégies d’accès avancé** onglet, vérifiez que votre coffre de clés est activé pour le chiffrement du disque Azure :</span><span class="sxs-lookup"><span data-stu-id="08abf-460">On hello **Advanced access policies** tab, make sure that your key vault is enabled for Azure Disk Encryption:</span></span>

![Coffre de clés Azure](./media/azure-security-disk-encryption/keyvault-portal-fig4.png)

## <a name="disk-encryption-deployment-scenarios-and-user-experiences"></a><span data-ttu-id="08abf-462">Scénarios de déploiement de chiffrement de disque et expériences utilisateur</span><span class="sxs-lookup"><span data-stu-id="08abf-462">Disk-encryption deployment scenarios and user experiences</span></span>
<span data-ttu-id="08abf-463">Vous pouvez activer plusieurs scénarios de chiffrement de disque, et les étapes de hello peuvent varier en fonction toohello scénario.</span><span class="sxs-lookup"><span data-stu-id="08abf-463">You can enable many disk-encryption scenarios, and hello steps may vary according toohello scenario.</span></span> <span data-ttu-id="08abf-464">Hello sections suivantes couvrent les scénarios de hello plus en détail.</span><span class="sxs-lookup"><span data-stu-id="08abf-464">hello following sections cover hello scenarios in greater detail.</span></span>

### <a name="enable-encryption-on-new-iaas-vms-that-are-created-from-hello-marketplace"></a><span data-ttu-id="08abf-465">Activer le chiffrement sur les nouvelles machines virtuelles IaaS qui sont créés à partir de hello Marketplace</span><span class="sxs-lookup"><span data-stu-id="08abf-465">Enable encryption on new IaaS VMs that are created from hello Marketplace</span></span>
<span data-ttu-id="08abf-466">Vous pouvez activer le chiffrement de disque sur virtuelle IaaS Windows à partir de hello Marketplace dans Azure à l’aide de hello [modèle Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-new-vm-gallery-image).</span><span class="sxs-lookup"><span data-stu-id="08abf-466">You can enable disk encryption on new IaaS Windows VM from hello Marketplace in Azure by using hello  [Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-new-vm-gallery-image).</span></span>

1. <span data-ttu-id="08abf-467">Sur le modèle de hello Azure de démarrage rapide, cliquez sur **déployer tooAzure**, entrez la configuration de chiffrement hello sur hello **paramètres** panneau, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="08abf-467">On hello Azure quick-start template, click **Deploy tooAzure**, enter hello encryption configuration on hello **Parameters** blade, and then click **OK**.</span></span>

2. <span data-ttu-id="08abf-468">Sélectionnez l’abonnement de hello, groupe de ressources, emplacement du groupe de ressources, juridiques et contrat, puis cliquez sur **créer** tooenable le chiffrement sur un VM IaaS nouvelle.</span><span class="sxs-lookup"><span data-stu-id="08abf-468">Select hello subscription, resource group, resource group location, legal terms, and agreement, and then click **Create** tooenable encryption on a new IaaS VM.</span></span>

> [!NOTE]
> <span data-ttu-id="08abf-469">Ce modèle crée un nouveau chiffrées Windows VM qui utilise l’image de la galerie hello Windows Server 2012.</span><span class="sxs-lookup"><span data-stu-id="08abf-469">This template creates a new encrypted Windows VM that uses hello Windows Server 2012 gallery image.</span></span>

<span data-ttu-id="08abf-470">Vous pouvez activer le chiffrement de disque sur une nouvelle machine virtuelle IaaS RedHat Linux 7.2 avec une baie RAID-0 de 200 Go à l’aide de ce [modèle Resource Manager](https://aka.ms/fde-rhel).</span><span class="sxs-lookup"><span data-stu-id="08abf-470">You can enable disk encryption on a new IaaS RedHat Linux 7.2 VM with a 200-GB RAID-0 array by using this [Resource Manager template](https://aka.ms/fde-rhel).</span></span> <span data-ttu-id="08abf-471">Après avoir déployé le modèle de hello, vérifier état du chiffrement hello machine virtuelle à l’aide de hello `Get-AzureRmVmDiskEncryptionStatus` applet de commande, comme décrit dans [lecteur de chiffrement du système d’exploitation sur un VM Linux en cours d’exécution](#encrypting-os-drive-on-a-running-linux-vm).</span><span class="sxs-lookup"><span data-stu-id="08abf-471">After you deploy hello template, verify hello VM encryption status by using hello `Get-AzureRmVmDiskEncryptionStatus` cmdlet, as described in [Encrypting OS drive on a running Linux VM](#encrypting-os-drive-on-a-running-linux-vm).</span></span> <span data-ttu-id="08abf-472">Lorsque les ordinateurs hello retourne l’état _VMRestartPending_, redémarrez hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="08abf-472">When hello machine returns a status of _VMRestartPending_, restart hello VM.</span></span>

<span data-ttu-id="08abf-473">Hello tableau suivant répertorie les paramètres de modèle de gestionnaire de ressources hello pour les nouvelles machines virtuelles à partir du scénario de Marketplace hello à l’aide d’ID de client Azure AD :</span><span class="sxs-lookup"><span data-stu-id="08abf-473">hello following table lists hello Resource Manager template parameters for new VMs from hello Marketplace scenario using Azure AD client ID:</span></span>

| <span data-ttu-id="08abf-474">Paramètre</span><span class="sxs-lookup"><span data-stu-id="08abf-474">Parameter</span></span> | <span data-ttu-id="08abf-475">Description</span><span class="sxs-lookup"><span data-stu-id="08abf-475">Description</span></span> |
| --- | --- |
| <span data-ttu-id="08abf-476">adminUsername</span><span class="sxs-lookup"><span data-stu-id="08abf-476">adminUserName</span></span> | <span data-ttu-id="08abf-477">Nom d’utilisateur administrateur pour l’ordinateur virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="08abf-477">Admin user name for hello virtual machine.</span></span> |
| <span data-ttu-id="08abf-478">adminPassword</span><span class="sxs-lookup"><span data-stu-id="08abf-478">adminPassword</span></span> | <span data-ttu-id="08abf-479">Mot de passe administrateur pour l’ordinateur virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="08abf-479">Admin user password for hello virtual machine.</span></span> |
| <span data-ttu-id="08abf-480">newStorageAccountName</span><span class="sxs-lookup"><span data-stu-id="08abf-480">newStorageAccountName</span></span> | <span data-ttu-id="08abf-481">Nom de toostore de compte de stockage hello du système d’exploitation et des disques durs virtuels de données.</span><span class="sxs-lookup"><span data-stu-id="08abf-481">Name of hello storage account toostore OS and data VHDs.</span></span> |
| <span data-ttu-id="08abf-482">vmSize</span><span class="sxs-lookup"><span data-stu-id="08abf-482">vmSize</span></span> | <span data-ttu-id="08abf-483">Taille de machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="08abf-483">Size of hello VM.</span></span> <span data-ttu-id="08abf-484">Actuellement, seules les séries A, D et G standard sont prises en charge.</span><span class="sxs-lookup"><span data-stu-id="08abf-484">Currently, only Standard A, D, and G series are supported.</span></span> |
| <span data-ttu-id="08abf-485">virtualNetworkName</span><span class="sxs-lookup"><span data-stu-id="08abf-485">virtualNetworkName</span></span> | <span data-ttu-id="08abf-486">Nom de réseau virtuel que hello VM NIC de hello doit appartenir au.</span><span class="sxs-lookup"><span data-stu-id="08abf-486">Name of hello VNet that hello VM NIC should belong to.</span></span> |
| <span data-ttu-id="08abf-487">subnetName</span><span class="sxs-lookup"><span data-stu-id="08abf-487">subnetName</span></span> | <span data-ttu-id="08abf-488">Nom du sous-réseau hello Bonjour réseau virtuel que hello VM NIC doit appartenir au.</span><span class="sxs-lookup"><span data-stu-id="08abf-488">Name of hello subnet in hello VNet that hello VM NIC should belong to.</span></span> |
| <span data-ttu-id="08abf-489">AADClientID</span><span class="sxs-lookup"><span data-stu-id="08abf-489">AADClientID</span></span> | <span data-ttu-id="08abf-490">ID client de l’application hello Azure AD avec le coffre de clés autorisations toowrite secrets tooyour.</span><span class="sxs-lookup"><span data-stu-id="08abf-490">Client ID of hello Azure AD application that has permissions toowrite secrets tooyour key vault.</span></span> |
| <span data-ttu-id="08abf-491">AADClientSecret</span><span class="sxs-lookup"><span data-stu-id="08abf-491">AADClientSecret</span></span> | <span data-ttu-id="08abf-492">Question secrète du client de l’application hello Azure AD avec le coffre de clés autorisations toowrite secrets tooyour.</span><span class="sxs-lookup"><span data-stu-id="08abf-492">Client secret of hello Azure AD application that has permissions toowrite secrets tooyour key vault.</span></span> |
| <span data-ttu-id="08abf-493">keyVaultURL</span><span class="sxs-lookup"><span data-stu-id="08abf-493">keyVaultURL</span></span> | <span data-ttu-id="08abf-494">URL de la clé de hello coffre que BitLocker clé doit être téléchargée dans hello.</span><span class="sxs-lookup"><span data-stu-id="08abf-494">URL of hello key vault that hello BitLocker key should be uploaded to.</span></span> <span data-ttu-id="08abf-495">Vous pouvez l’obtenir à l’aide de l’applet de commande hello `(Get-AzureRmKeyVault -VaultName,-ResourceGroupName ).VaultURI`.</span><span class="sxs-lookup"><span data-stu-id="08abf-495">You can get it by using hello cmdlet `(Get-AzureRmKeyVault -VaultName,-ResourceGroupName ).VaultURI`.</span></span> |
| <span data-ttu-id="08abf-496">keyEncryptionKeyURL</span><span class="sxs-lookup"><span data-stu-id="08abf-496">keyEncryptionKeyURL</span></span> | <span data-ttu-id="08abf-497">URL de la clé de chiffrement hello est utilisé tooencrypt hello générée clé BitLocker (facultatif).</span><span class="sxs-lookup"><span data-stu-id="08abf-497">URL of hello key encryption key that's used tooencrypt hello generated BitLocker key (optional).</span></span> |
| <span data-ttu-id="08abf-498">keyVaultResourceGroup</span><span class="sxs-lookup"><span data-stu-id="08abf-498">keyVaultResourceGroup</span></span> | <span data-ttu-id="08abf-499">Groupe de ressources de coffre de clés hello.</span><span class="sxs-lookup"><span data-stu-id="08abf-499">Resource group of hello key vault.</span></span> |
| <span data-ttu-id="08abf-500">vmName</span><span class="sxs-lookup"><span data-stu-id="08abf-500">vmName</span></span> | <span data-ttu-id="08abf-501">Nom de machine virtuelle qui hello l’opération de chiffrement de hello est toobe effectuée sur.</span><span class="sxs-lookup"><span data-stu-id="08abf-501">Name of hello VM that hello encryption operation is toobe performed on.</span></span> |

> [!NOTE]
> <span data-ttu-id="08abf-502">_KeyEncryptionKeyURL_ est un paramètre facultatif.</span><span class="sxs-lookup"><span data-stu-id="08abf-502">_KeyEncryptionKeyURL_ is an optional parameter.</span></span> <span data-ttu-id="08abf-503">Vous pouvez mettre votre propre clé de chiffrement de clés toofurther sauvegarde hello données (mot de passe secret) dans votre coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="08abf-503">You can bring your own KEK toofurther safeguard hello data encryption key (Passphrase secret) in your key vault.</span></span>

### <a name="enable-encryption-on-new-iaas-vms-that-are-created-from-customer-encrypted-vhd-and-encryption-keys"></a><span data-ttu-id="08abf-504">Activation du chiffrement sur de nouvelles machines virtuelles IaaS créées à partir de disques durs virtuels chiffrés par le client et de clés de chiffrement</span><span class="sxs-lookup"><span data-stu-id="08abf-504">Enable encryption on new IaaS VMs that are created from customer-encrypted VHD and encryption keys</span></span>
<span data-ttu-id="08abf-505">Dans ce scénario, vous pouvez activer le chiffrement à l’aide des commandes CLI, applets de commande PowerShell ou modèle du Gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="08abf-505">In this scenario, you can enable encrypting by using hello Resource Manager template, PowerShell cmdlets, or CLI commands.</span></span> <span data-ttu-id="08abf-506">Hello sections suivantes expliquent dans le modèle de gestionnaire de ressources de hello détail supérieur et les commandes CLI.</span><span class="sxs-lookup"><span data-stu-id="08abf-506">hello following sections explain in greater detail hello Resource Manager template and CLI commands.</span></span>

<span data-ttu-id="08abf-507">Suivez les instructions de hello à partir d’une de ces sections pour la préparation d’images déjà chiffrés qui peuvent être utilisés dans Azure.</span><span class="sxs-lookup"><span data-stu-id="08abf-507">Follow hello instructions from one of these sections for preparing pre-encrypted images that can be used in Azure.</span></span> <span data-ttu-id="08abf-508">Après la création d’image de hello, vous pouvez utiliser les étapes de hello dans hello suivant section toocreate une machine virtuelle de Azure chiffré.</span><span class="sxs-lookup"><span data-stu-id="08abf-508">After hello image is created, you can use hello steps in hello next section toocreate an encrypted Azure VM.</span></span>

* [<span data-ttu-id="08abf-509">Préparer un disque dur virtuel Windows déjà chiffré</span><span class="sxs-lookup"><span data-stu-id="08abf-509">Prepare a pre-encrypted Windows VHD</span></span>](#preparing-a-pre-encrypted-windows-vhd)
* [<span data-ttu-id="08abf-510">Préparer un disque dur virtuel Linux déjà chiffré</span><span class="sxs-lookup"><span data-stu-id="08abf-510">Prepare a pre-encrypted Linux VHD</span></span>](#preparing-a-pre-encrypted-linux-vhd)

#### <a name="using-hello-resource-manager-template"></a><span data-ttu-id="08abf-511">À l’aide du modèle de gestionnaire de ressources hello</span><span class="sxs-lookup"><span data-stu-id="08abf-511">Using hello Resource Manager template</span></span>
<span data-ttu-id="08abf-512">Vous pouvez activer le chiffrement de disque sur votre disque dur virtuel chiffrée à l’aide de hello [modèle Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-pre-encrypted-vm).</span><span class="sxs-lookup"><span data-stu-id="08abf-512">You can enable disk encryption on your encrypted VHD by using hello [Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-pre-encrypted-vm).</span></span>

1. <span data-ttu-id="08abf-513">Sur le modèle de hello Azure de démarrage rapide, cliquez sur **déployer tooAzure**, entrez la configuration de chiffrement hello sur hello **paramètres** panneau, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="08abf-513">On hello Azure quick-start template, click **Deploy tooAzure**, enter hello encryption configuration on hello **Parameters** blade, and then click **OK**.</span></span>

2. <span data-ttu-id="08abf-514">Sélectionnez l’abonnement de hello, groupe de ressources, emplacement du groupe de ressources, juridiques et contrat, puis cliquez sur **créer** tooenable le chiffrement sur hello nouvelle IaaS VM.</span><span class="sxs-lookup"><span data-stu-id="08abf-514">Select hello subscription, resource group, resource group location, legal terms, and agreement, and then click **Create** tooenable encryption on hello new IaaS VM.</span></span>

<span data-ttu-id="08abf-515">Hello tableau suivant répertorie les paramètres de modèle de gestionnaire de ressources hello pour votre disque dur virtuel chiffrée :</span><span class="sxs-lookup"><span data-stu-id="08abf-515">hello following table lists hello Resource Manager template parameters for your encrypted VHD:</span></span>

| <span data-ttu-id="08abf-516">Paramètre</span><span class="sxs-lookup"><span data-stu-id="08abf-516">Parameter</span></span> | <span data-ttu-id="08abf-517">Description</span><span class="sxs-lookup"><span data-stu-id="08abf-517">Description</span></span> |
| --- | --- |
| <span data-ttu-id="08abf-518">newStorageAccountName</span><span class="sxs-lookup"><span data-stu-id="08abf-518">newStorageAccountName</span></span> | <span data-ttu-id="08abf-519">Nom de hello de toostore de compte de stockage hello chiffré de disque dur virtuel du système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="08abf-519">Name of hello storage account toostore hello encrypted OS VHD.</span></span> <span data-ttu-id="08abf-520">Ce compte de stockage doit déjà avoir été créé dans hello même groupe de ressources et le même emplacement que hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="08abf-520">This storage account should already have been created in hello same resource group and same location as hello VM.</span></span> |
| <span data-ttu-id="08abf-521">osVhdUri</span><span class="sxs-lookup"><span data-stu-id="08abf-521">osVhdUri</span></span> | <span data-ttu-id="08abf-522">URI de hello disque dur virtuel du système d’exploitation à partir du compte de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="08abf-522">URI of hello OS VHD from hello storage account.</span></span> |
| <span data-ttu-id="08abf-523">osType</span><span class="sxs-lookup"><span data-stu-id="08abf-523">osType</span></span> | <span data-ttu-id="08abf-524">Type de système d’exploitation (Windows/Linux).</span><span class="sxs-lookup"><span data-stu-id="08abf-524">OS product type (Windows/Linux).</span></span> |
| <span data-ttu-id="08abf-525">virtualNetworkName</span><span class="sxs-lookup"><span data-stu-id="08abf-525">virtualNetworkName</span></span> | <span data-ttu-id="08abf-526">Nom de réseau virtuel que hello VM NIC de hello doit appartenir au.</span><span class="sxs-lookup"><span data-stu-id="08abf-526">Name of hello VNet that hello VM NIC should belong to.</span></span> <span data-ttu-id="08abf-527">Hello nom doit ont déjà été créé dans hello même groupe de ressources et le même emplacement que hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="08abf-527">hello name should already have been created in hello same resource group and same location as hello VM.</span></span> |
| <span data-ttu-id="08abf-528">subnetName</span><span class="sxs-lookup"><span data-stu-id="08abf-528">subnetName</span></span> | <span data-ttu-id="08abf-529">Nom du sous-réseau hello sur hello réseau virtuel que hello VM NIC doit appartenir au.</span><span class="sxs-lookup"><span data-stu-id="08abf-529">Name of hello subnet on hello VNet that hello VM NIC should belong to.</span></span> |
| <span data-ttu-id="08abf-530">vmSize</span><span class="sxs-lookup"><span data-stu-id="08abf-530">vmSize</span></span> | <span data-ttu-id="08abf-531">Taille de machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="08abf-531">Size of hello VM.</span></span> <span data-ttu-id="08abf-532">Actuellement, seules les séries A, D et G standard sont prises en charge.</span><span class="sxs-lookup"><span data-stu-id="08abf-532">Currently, only Standard A, D, and G series are supported.</span></span> |
| <span data-ttu-id="08abf-533">keyVaultResourceID</span><span class="sxs-lookup"><span data-stu-id="08abf-533">keyVaultResourceID</span></span> | <span data-ttu-id="08abf-534">Hello ResourceID qui identifie la ressource du coffre de clés hello dans Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="08abf-534">hello ResourceID that identifies hello key vault resource in Azure Resource Manager.</span></span> <span data-ttu-id="08abf-535">Vous pouvez l’obtenir à l’aide de l’applet de commande PowerShell hello `(Get-AzureRmKeyVault -VaultName &lt;yourKeyVaultName&gt; -ResourceGroupName &lt;yourResourceGroupName&gt;).ResourceId`.</span><span class="sxs-lookup"><span data-stu-id="08abf-535">You can get it by using hello PowerShell cmdlet `(Get-AzureRmKeyVault -VaultName &lt;yourKeyVaultName&gt; -ResourceGroupName &lt;yourResourceGroupName&gt;).ResourceId`.</span></span> |
| <span data-ttu-id="08abf-536">keyVaultSecretUrl</span><span class="sxs-lookup"><span data-stu-id="08abf-536">keyVaultSecretUrl</span></span> | <span data-ttu-id="08abf-537">URL de la clé de chiffrement de disque hello qui est défini dans le coffre de clés hello.</span><span class="sxs-lookup"><span data-stu-id="08abf-537">URL of hello disk-encryption key that's set up in hello key vault.</span></span> |
| <span data-ttu-id="08abf-538">keyVaultKekUrl</span><span class="sxs-lookup"><span data-stu-id="08abf-538">keyVaultKekUrl</span></span> | <span data-ttu-id="08abf-539">URL de la clé de chiffrement à clé hello pour chiffrer la clé de chiffrement de disque hello généré.</span><span class="sxs-lookup"><span data-stu-id="08abf-539">URL of hello key encryption key for encrypting hello generated disk-encryption key.</span></span> |
| <span data-ttu-id="08abf-540">vmName</span><span class="sxs-lookup"><span data-stu-id="08abf-540">vmName</span></span> | <span data-ttu-id="08abf-541">Nom de hello IaaS VM.</span><span class="sxs-lookup"><span data-stu-id="08abf-541">Name of hello IaaS VM.</span></span> |

#### <a name="using-powershell-cmdlets"></a><span data-ttu-id="08abf-542">Utilisation d’applets de commande PowerShell</span><span class="sxs-lookup"><span data-stu-id="08abf-542">Using PowerShell cmdlets</span></span>
<span data-ttu-id="08abf-543">Vous pouvez activer le chiffrement de disque sur votre disque dur virtuel chiffrée à l’aide d’applet de commande PowerShell hello [ `Set-AzureRmVMOSDisk` ](/powershell/module/azurerm.compute/set-azurermvmosdisk).</span><span class="sxs-lookup"><span data-stu-id="08abf-543">You can enable disk encryption on your encrypted VHD by using hello PowerShell cmdlet [`Set-AzureRmVMOSDisk`](/powershell/module/azurerm.compute/set-azurermvmosdisk).</span></span>  

#### <a name="using-cli-commands"></a><span data-ttu-id="08abf-544">Utilisation des commandes CLI</span><span class="sxs-lookup"><span data-stu-id="08abf-544">Using CLI commands</span></span>
<span data-ttu-id="08abf-545">chiffrement de disque tooenable pour ce scénario à l’aide des commandes CLI, hello suivant :</span><span class="sxs-lookup"><span data-stu-id="08abf-545">tooenable disk encryption for this scenario by using CLI commands, do hello following:</span></span>

1. <span data-ttu-id="08abf-546">Définissez des stratégies d’accès dans votre coffre de clés :</span><span class="sxs-lookup"><span data-stu-id="08abf-546">Set access policies in your key vault:</span></span>

   * <span data-ttu-id="08abf-547">Ensemble hello **EnabledForDiskEncryption** indicateur :</span><span class="sxs-lookup"><span data-stu-id="08abf-547">Set hello **EnabledForDiskEncryption** flag:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --enabled-for-disk-encryption true`
   * <span data-ttu-id="08abf-548">Jeu d’autorisations tooAzure AD application toowrite secrets tooyour coffre de clés :</span><span class="sxs-lookup"><span data-stu-id="08abf-548">Set permissions tooAzure AD application toowrite secrets tooyour key vault:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --spn <aadClientID> --perms-to-keys '["wrapKey"]' --perms-to-secrets '["set"]'`

2. <span data-ttu-id="08abf-549">chiffrement tooenable sur une machine virtuelle existante ou en cours d’exécution, type :</span><span class="sxs-lookup"><span data-stu-id="08abf-549">tooenable encryption on an existing or running VM, type:</span></span>

 `azure vm enable-disk-encryption --resource-group <resourceGroupName> --name <vmName> --aad-client-id <aadClientId> --aad-client-secret <aadClientSecret> --disk-encryption-key-vault-url <keyVaultURL> --disk-encryption-key-vault-id <keyVaultResourceId> --volume-type [All|OS|Data]`

3. <span data-ttu-id="08abf-550">Obtenez l’état de chiffrement :</span><span class="sxs-lookup"><span data-stu-id="08abf-550">Get encryption status:</span></span>

 `azure vm show-disk-encryption-status --resource-group <resourceGroupName> --name <vmName> --json`

4. <span data-ttu-id="08abf-551">le chiffrement sur une machine virtuelle à partir de votre disque dur virtuel chiffrée, hello utilisez paramètres avec hello suivants tooenable `azure vm create` commande :</span><span class="sxs-lookup"><span data-stu-id="08abf-551">tooenable encryption on a new VM from your encrypted VHD, use hello following parameters with hello `azure vm create` command:</span></span>

 ```
   * disk-encryption-key-vault-id <disk-encryption-key-vault-id>
   * disk-encryption-key-url <disk-encryption-key-url>
   * key-encryption-key-vault-id <key-encryption-key-vault-id>
   * key-encryption-key-url <key-encryption-key-url>
 ```

### <a name="enable-encryption-on-existing-or-running-iaas-windows-vm-in-azure"></a><span data-ttu-id="08abf-552">Activer le chiffrement sur des machines virtuelles IaaS Windows existantes/en cours de fonctionnement dans Azure</span><span class="sxs-lookup"><span data-stu-id="08abf-552">Enable encryption on existing or running IaaS Windows VM in Azure</span></span>
<span data-ttu-id="08abf-553">Dans ce scénario, vous pouvez activer le chiffrement à l’aide des commandes CLI, applets de commande PowerShell ou modèle du Gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="08abf-553">In this scenario, you can enable encrypting by using hello Resource Manager template, PowerShell cmdlets, or CLI commands.</span></span> <span data-ttu-id="08abf-554">Hello sections suivantes expliquent en détail comment tooenable à l’aide de hello modèle du Gestionnaire de ressources et les commandes CLI.</span><span class="sxs-lookup"><span data-stu-id="08abf-554">hello following sections explain in greater detail how tooenable it by using hello Resource Manager template and CLI commands.</span></span>

#### <a name="using-hello-resource-manager-template"></a><span data-ttu-id="08abf-555">À l’aide du modèle de gestionnaire de ressources hello</span><span class="sxs-lookup"><span data-stu-id="08abf-555">Using hello Resource Manager template</span></span>
<span data-ttu-id="08abf-556">Vous pouvez activer le chiffrement de disque sur existant ou en exécutant des machines virtuelles IaaS de Windows dans Azure à l’aide de hello [modèle Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-running-windows-vm).</span><span class="sxs-lookup"><span data-stu-id="08abf-556">You can enable disk encryption on existing or running IaaS Windows VMs in Azure by using hello [Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-running-windows-vm).</span></span>

1. <span data-ttu-id="08abf-557">Sur le modèle de hello Azure de démarrage rapide, cliquez sur **déployer tooAzure**, entrez la configuration de chiffrement hello sur hello **paramètres** panneau, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="08abf-557">On hello Azure quick-start template, click **Deploy tooAzure**, enter hello encryption configuration on hello **Parameters** blade, and then click **OK**.</span></span>

2. <span data-ttu-id="08abf-558">Sélectionnez l’abonnement de hello, groupe de ressources, emplacement du groupe de ressources, juridiques et contrat, puis cliquez sur **créer** tooenable le chiffrement sur hello existant ou en cours d’exécution IaaS VM.</span><span class="sxs-lookup"><span data-stu-id="08abf-558">Select hello subscription, resource group, resource group location, legal terms, and agreement, and then click **Create** tooenable encryption on hello existing or running IaaS VM.</span></span>

<span data-ttu-id="08abf-559">Hello tableau suivant répertorie les paramètres du modèle de gestionnaire de ressources hello pour existant ou en exécutant des ordinateurs virtuels qui utilisent un ID de client Azure AD :</span><span class="sxs-lookup"><span data-stu-id="08abf-559">hello following table lists hello Resource Manager template parameters for existing or running VMs that use an Azure AD client ID:</span></span>

| <span data-ttu-id="08abf-560">Paramètre</span><span class="sxs-lookup"><span data-stu-id="08abf-560">Parameter</span></span> | <span data-ttu-id="08abf-561">Description</span><span class="sxs-lookup"><span data-stu-id="08abf-561">Description</span></span> |
| --- | --- |
| <span data-ttu-id="08abf-562">AADClientID</span><span class="sxs-lookup"><span data-stu-id="08abf-562">AADClientID</span></span> | <span data-ttu-id="08abf-563">ID client de l’application hello Azure AD avec le coffre de clés autorisations toowrite secrets toohello.</span><span class="sxs-lookup"><span data-stu-id="08abf-563">Client ID of hello Azure AD application that has permissions toowrite secrets toohello key vault.</span></span> |
| <span data-ttu-id="08abf-564">AADClientSecret</span><span class="sxs-lookup"><span data-stu-id="08abf-564">AADClientSecret</span></span> | <span data-ttu-id="08abf-565">Question secrète du client de l’application hello Azure AD avec le coffre de clés autorisations toowrite secrets toohello.</span><span class="sxs-lookup"><span data-stu-id="08abf-565">Client secret of hello Azure AD application that has permissions toowrite secrets toohello key vault.</span></span> |
| <span data-ttu-id="08abf-566">keyVaultName</span><span class="sxs-lookup"><span data-stu-id="08abf-566">keyVaultName</span></span> | <span data-ttu-id="08abf-567">Nom de clé de hello coffre que BitLocker clé doit être téléchargée dans hello.</span><span class="sxs-lookup"><span data-stu-id="08abf-567">Name of hello key vault that hello BitLocker key should be uploaded to.</span></span> <span data-ttu-id="08abf-568">Vous pouvez l’obtenir à l’aide de l’applet de commande hello `(Get-AzureRmKeyVault -ResourceGroupName <yourResourceGroupName>). Vaultname`.</span><span class="sxs-lookup"><span data-stu-id="08abf-568">You can get it by using hello cmdlet `(Get-AzureRmKeyVault -ResourceGroupName <yourResourceGroupName>). Vaultname`.</span></span> |
|  <span data-ttu-id="08abf-569">keyEncryptionKeyURL</span><span class="sxs-lookup"><span data-stu-id="08abf-569">keyEncryptionKeyURL</span></span> | <span data-ttu-id="08abf-570">URL de la clé de chiffrement hello est utilisé tooencrypt hello générée clé BitLocker.</span><span class="sxs-lookup"><span data-stu-id="08abf-570">URL of hello key encryption key that's used tooencrypt hello generated BitLocker key.</span></span> <span data-ttu-id="08abf-571">Ce paramètre est facultatif si vous sélectionnez **nokek** dans la liste de hello UseExistingKek de liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="08abf-571">This parameter is optional if you select **nokek** in hello UseExistingKek drop-down list.</span></span> <span data-ttu-id="08abf-572">Si vous sélectionnez **kek** dans la liste déroulante UseExistingKek de hello, vous devez entrer hello _keyEncryptionKeyURL_ valeur.</span><span class="sxs-lookup"><span data-stu-id="08abf-572">If you select **kek** in hello UseExistingKek drop-down list, you must enter hello _keyEncryptionKeyURL_ value.</span></span> |
| <span data-ttu-id="08abf-573">volumeType</span><span class="sxs-lookup"><span data-stu-id="08abf-573">volumeType</span></span> | <span data-ttu-id="08abf-574">Type de volume que l’opération de chiffrement hello est effectuée sur.</span><span class="sxs-lookup"><span data-stu-id="08abf-574">Type of volume that hello encryption operation is performed on.</span></span> <span data-ttu-id="08abf-575">Les valeurs valides sont _Système d’exploitation_, _Données_ et _Tous_.</span><span class="sxs-lookup"><span data-stu-id="08abf-575">Valid values are _OS_, _Data_, and _All_.</span></span> |
| <span data-ttu-id="08abf-576">sequenceVersion</span><span class="sxs-lookup"><span data-stu-id="08abf-576">sequenceVersion</span></span> | <span data-ttu-id="08abf-577">Version de la séquence de hello BitLocker opération.</span><span class="sxs-lookup"><span data-stu-id="08abf-577">Sequence version of hello BitLocker operation.</span></span> <span data-ttu-id="08abf-578">Incrémenter ce numéro de version, chaque fois qu’une opération de chiffrement de disque est exécutée sur hello même machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="08abf-578">Increment this version number every time a disk-encryption operation is performed on hello same VM.</span></span> |
| <span data-ttu-id="08abf-579">vmName</span><span class="sxs-lookup"><span data-stu-id="08abf-579">vmName</span></span> | <span data-ttu-id="08abf-580">Nom de machine virtuelle qui hello l’opération de chiffrement de hello est toobe effectuée sur.</span><span class="sxs-lookup"><span data-stu-id="08abf-580">Name of hello VM that hello encryption operation is toobe performed on.</span></span> |

> [!NOTE]
> <span data-ttu-id="08abf-581">_KeyEncryptionKeyURL_ est un paramètre facultatif.</span><span class="sxs-lookup"><span data-stu-id="08abf-581">_KeyEncryptionKeyURL_ is an optional parameter.</span></span> <span data-ttu-id="08abf-582">Vous pouvez mettre votre propre clé de chiffrement de clés toofurther sauvegarde hello données (secret de chiffrement BitLocker) dans le coffre de clés hello.</span><span class="sxs-lookup"><span data-stu-id="08abf-582">You can bring your own KEK toofurther safeguard hello data encryption key (BitLocker encryption secret) in hello key vault.</span></span>

#### <a name="using-powershell-cmdlets"></a><span data-ttu-id="08abf-583">Utilisation d’applets de commande PowerShell</span><span class="sxs-lookup"><span data-stu-id="08abf-583">Using PowerShell cmdlets</span></span>
<span data-ttu-id="08abf-584">Pour plus d’informations sur l’activation du chiffrement avec un chiffrement de disque Azure à l’aide des applets de commande PowerShell, consultez les billets de blog hello [Explorer le chiffrement de disque Azure avec Azure PowerShell - partie 1](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/explore-azure-disk-encryption-with-azure-powershell.aspx) et [Explorer de chiffrement de disque Azure avec Azure PowerShell - partie 2](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx).</span><span class="sxs-lookup"><span data-stu-id="08abf-584">For information about enabling encryption with Azure Disk Encryption by using PowerShell cmdlets, see hello blog posts [Explore Azure Disk Encryption with Azure PowerShell - Part 1](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/explore-azure-disk-encryption-with-azure-powershell.aspx) and [Explore Azure Disk Encryption with Azure PowerShell - Part 2](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx).</span></span>

#### <a name="using-cli-commands"></a><span data-ttu-id="08abf-585">Utilisation des commandes CLI</span><span class="sxs-lookup"><span data-stu-id="08abf-585">Using CLI commands</span></span>
<span data-ttu-id="08abf-586">chiffrement tooenable sur existant ou en cours d’exécution IaaS Windows VM dans Azure à l’aide des commandes CLI, hello suivant :</span><span class="sxs-lookup"><span data-stu-id="08abf-586">tooenable encryption on existing or running IaaS Windows VM in Azure using CLI commands, do hello following:</span></span>

1. <span data-ttu-id="08abf-587">stratégies d’accès tooset hello coffre de clés :</span><span class="sxs-lookup"><span data-stu-id="08abf-587">tooset access policies in hello key vault:</span></span>
   * <span data-ttu-id="08abf-588">Ensemble hello **EnabledForDiskEncryption** indicateur :</span><span class="sxs-lookup"><span data-stu-id="08abf-588">Set hello **EnabledForDiskEncryption** flag:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --enabled-for-disk-encryption true`
   * <span data-ttu-id="08abf-589">Jeu d’autorisations tooAzure AD application toowrite secrets tooyour coffre de clés :</span><span class="sxs-lookup"><span data-stu-id="08abf-589">Set permissions tooAzure AD application toowrite secrets tooyour key vault:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --spn <aadClientID> --perms-to-keys '["wrapKey"]' --perms-to-secrets '["set"]'`
2. <span data-ttu-id="08abf-590">chiffrement tooenable sur une machine virtuelle au existant ou en cours d’exécution :</span><span class="sxs-lookup"><span data-stu-id="08abf-590">tooenable encryption on an existing or running VM:</span></span>

 `azure vm enable-disk-encryption --resource-group <resourceGroupName> --name <vmName> --aad-client-id <aadClientId> --aad-client-secret <aadClientSecret> --disk-encryption-key-vault-url <keyVaultURL> --disk-encryption-key-vault-id <keyVaultResourceId> --volume-type [All|OS|Data]`
3. <span data-ttu-id="08abf-591">état du chiffrement tooget :</span><span class="sxs-lookup"><span data-stu-id="08abf-591">tooget encryption status:</span></span>

 `azure vm show-disk-encryption-status --resource-group <resourceGroupName> --name <vmName> --json`
4. <span data-ttu-id="08abf-592">le chiffrement sur une machine virtuelle à partir de votre disque dur virtuel chiffrée, hello utilisez paramètres avec hello suivants tooenable `azure vm create` commande :</span><span class="sxs-lookup"><span data-stu-id="08abf-592">tooenable encryption on a new VM from your encrypted VHD, use hello following parameters with hello `azure vm create` command:</span></span>

 ```
   * disk-encryption-key-vault-id <disk-encryption-key-vault-id>
   * disk-encryption-key-url <disk-encryption-key-url>
   * key-encryption-key-vault-id <key-encryption-key-vault-id>
   * key-encryption-key-url <key-encryption-key-url>
 ```

### <a name="enable-encryption-on-an-existing-or-running-iaas-linux-vm-in-azure"></a><span data-ttu-id="08abf-593">Activer le chiffrement sur une machine virtuelle IaaS Linux existante ou en cours d’exécution dans Azure</span><span class="sxs-lookup"><span data-stu-id="08abf-593">Enable encryption on an existing or running IaaS Linux VM in Azure</span></span>
<span data-ttu-id="08abf-594">Vous pouvez activer le chiffrement de disque sur une version existante ou en cours d’exécution IaaS Linux machine virtuelle dans Azure à l’aide de hello [modèle Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-running-linux-vm).</span><span class="sxs-lookup"><span data-stu-id="08abf-594">You can enable disk encryption on an existing or running IaaS Linux VM in Azure by using hello [Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-running-linux-vm).</span></span>

1. <span data-ttu-id="08abf-595">Cliquez sur **déployer tooAzure** sur le modèle de démarrage rapide Azure de hello, entrez la configuration de chiffrement hello sur hello **paramètres** panneau, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="08abf-595">Click **Deploy tooAzure** on hello Azure quick-start template, enter hello encryption configuration on hello **Parameters** blade, and then click **OK**.</span></span>

2. <span data-ttu-id="08abf-596">Sélectionnez l’abonnement de hello, groupe de ressources, emplacement du groupe de ressources, juridiques et contrat, puis cliquez sur **créer** tooenable le chiffrement sur hello existant ou en cours d’exécution IaaS VM.</span><span class="sxs-lookup"><span data-stu-id="08abf-596">Select hello subscription, resource group, resource group location, legal terms, and agreement, and then click **Create** tooenable encryption on hello existing or running IaaS VM.</span></span>

<span data-ttu-id="08abf-597">Hello tableau suivant répertorie les paramètres de modèle de gestionnaire de ressources pour existant ou en exécutant des ordinateurs virtuels qui utilisent un ID de client Azure AD :</span><span class="sxs-lookup"><span data-stu-id="08abf-597">hello following table lists Resource Manager template parameters for existing or running VMs that use an Azure AD client ID:</span></span>

| <span data-ttu-id="08abf-598">Paramètre</span><span class="sxs-lookup"><span data-stu-id="08abf-598">Parameter</span></span> | <span data-ttu-id="08abf-599">Description</span><span class="sxs-lookup"><span data-stu-id="08abf-599">Description</span></span> |
| --- | --- |
| <span data-ttu-id="08abf-600">AADClientID</span><span class="sxs-lookup"><span data-stu-id="08abf-600">AADClientID</span></span> | <span data-ttu-id="08abf-601">ID client de l’application hello Azure AD avec le coffre de clés autorisations toowrite secrets toohello.</span><span class="sxs-lookup"><span data-stu-id="08abf-601">Client ID of hello Azure AD application that has permissions toowrite secrets toohello key vault.</span></span> |
| <span data-ttu-id="08abf-602">AADClientSecret</span><span class="sxs-lookup"><span data-stu-id="08abf-602">AADClientSecret</span></span> | <span data-ttu-id="08abf-603">Question secrète du client de l’application hello Azure AD avec le coffre de clés autorisations toowrite secrets tooyour.</span><span class="sxs-lookup"><span data-stu-id="08abf-603">Client secret of hello Azure AD application that has permissions toowrite secrets tooyour key vault.</span></span> |
| <span data-ttu-id="08abf-604">keyVaultName</span><span class="sxs-lookup"><span data-stu-id="08abf-604">keyVaultName</span></span> | <span data-ttu-id="08abf-605">Nom de clé de hello coffre que BitLocker clé doit être téléchargée dans hello.</span><span class="sxs-lookup"><span data-stu-id="08abf-605">Name of hello key vault that hello BitLocker key should be uploaded to.</span></span> <span data-ttu-id="08abf-606">Vous pouvez l’obtenir à l’aide de l’applet de commande hello `(Get-AzureRmKeyVault -ResourceGroupName <yourResourceGroupName>). Vaultname`.</span><span class="sxs-lookup"><span data-stu-id="08abf-606">You can get it by using hello cmdlet `(Get-AzureRmKeyVault -ResourceGroupName <yourResourceGroupName>). Vaultname`.</span></span> |
|  <span data-ttu-id="08abf-607">keyEncryptionKeyURL</span><span class="sxs-lookup"><span data-stu-id="08abf-607">keyEncryptionKeyURL</span></span> | <span data-ttu-id="08abf-608">URL de la clé de chiffrement hello est utilisé tooencrypt hello générée clé BitLocker.</span><span class="sxs-lookup"><span data-stu-id="08abf-608">URL of hello key encryption key that's used tooencrypt hello generated BitLocker key.</span></span> <span data-ttu-id="08abf-609">Ce paramètre est facultatif si vous sélectionnez **nokek** dans la liste de hello UseExistingKek de liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="08abf-609">This parameter is optional if you select **nokek** in hello UseExistingKek drop-down list.</span></span> <span data-ttu-id="08abf-610">Si vous sélectionnez **kek** dans la liste déroulante UseExistingKek de hello, vous devez entrer hello _keyEncryptionKeyURL_ valeur.</span><span class="sxs-lookup"><span data-stu-id="08abf-610">If you select **kek** in hello UseExistingKek drop-down list, you must enter hello _keyEncryptionKeyURL_ value.</span></span> |
| <span data-ttu-id="08abf-611">volumeType</span><span class="sxs-lookup"><span data-stu-id="08abf-611">volumeType</span></span> | <span data-ttu-id="08abf-612">Type de volume que l’opération de chiffrement hello est effectuée sur.</span><span class="sxs-lookup"><span data-stu-id="08abf-612">Type of volume that hello encryption operation is performed on.</span></span> <span data-ttu-id="08abf-613">Les valeurs valides prises en charge sont _Système d’exploitation_ ou _Tous_ (pour RHEL 7.2, CentOS 7.2 et Ubuntu 16.04) et _Données_ (pour toutes les autres distributions).</span><span class="sxs-lookup"><span data-stu-id="08abf-613">Valid supported values are _OS_ or _All_ (for RHEL 7.2, CentOS 7.2, and Ubuntu 16.04), and _Data_ (for all other distributions).</span></span> |
| <span data-ttu-id="08abf-614">sequenceVersion</span><span class="sxs-lookup"><span data-stu-id="08abf-614">sequenceVersion</span></span> | <span data-ttu-id="08abf-615">Version de la séquence de hello BitLocker opération.</span><span class="sxs-lookup"><span data-stu-id="08abf-615">Sequence version of hello BitLocker operation.</span></span> <span data-ttu-id="08abf-616">Incrémenter ce numéro de version, chaque fois qu’une opération de chiffrement de disque est exécutée sur hello même machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="08abf-616">Increment this version number every time a disk-encryption operation is performed on hello same VM.</span></span> |
| <span data-ttu-id="08abf-617">vmName</span><span class="sxs-lookup"><span data-stu-id="08abf-617">vmName</span></span> | <span data-ttu-id="08abf-618">Nom de machine virtuelle qui hello l’opération de chiffrement de hello est toobe effectuée sur.</span><span class="sxs-lookup"><span data-stu-id="08abf-618">Name of hello VM that hello encryption operation is toobe performed on.</span></span> |
| <span data-ttu-id="08abf-619">passPhrase</span><span class="sxs-lookup"><span data-stu-id="08abf-619">passPhrase</span></span> | <span data-ttu-id="08abf-620">Tapez une phrase secrète forte en tant que clé de chiffrement de données hello.</span><span class="sxs-lookup"><span data-stu-id="08abf-620">Type a strong passphrase as hello data encryption key.</span></span> |

> [!NOTE]
> <span data-ttu-id="08abf-621">_KeyEncryptionKeyURL_ est un paramètre facultatif.</span><span class="sxs-lookup"><span data-stu-id="08abf-621">_KeyEncryptionKeyURL_ is an optional parameter.</span></span> <span data-ttu-id="08abf-622">Vous pouvez mettre votre propre clé de chiffrement de clés toofurther sauvegarde hello données (mot de passe secret) dans votre coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="08abf-622">You can bring your own KEK toofurther safeguard hello data encryption key (passphrase secret) in your key vault.</span></span>

#### <a name="cli-commands"></a><span data-ttu-id="08abf-623">Commandes CLI</span><span class="sxs-lookup"><span data-stu-id="08abf-623">CLI commands</span></span>
<span data-ttu-id="08abf-624">Vous pouvez activer le chiffrement de disque sur votre disque dur virtuel chiffrée en installant et utilisant hello [commande CLI](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="08abf-624">You can enable disk encryption on your encrypted VHD by installing and using hello [CLI command](../cli-install-nodejs.md).</span></span> <span data-ttu-id="08abf-625">chiffrement tooenable sur existant ou en exécutant les machines virtuelles Linux IaaS dans Azure à l’aide des commandes CLI, hello suivant :</span><span class="sxs-lookup"><span data-stu-id="08abf-625">tooenable encryption on existing or running IaaS Linux VMs in Azure by using CLI commands, do hello following:</span></span>

1. <span data-ttu-id="08abf-626">Définir des stratégies d’accès dans le coffre de clés hello :</span><span class="sxs-lookup"><span data-stu-id="08abf-626">Set access policies in hello key vault:</span></span>

 * <span data-ttu-id="08abf-627">Ensemble hello **EnabledForDiskEncryption** indicateur :</span><span class="sxs-lookup"><span data-stu-id="08abf-627">Set hello **EnabledForDiskEncryption** flag:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --enabled-for-disk-encryption true`
 * <span data-ttu-id="08abf-628">Jeu d’autorisations tooAzure AD application toowrite secrets tooyour coffre de clés :</span><span class="sxs-lookup"><span data-stu-id="08abf-628">Set permissions tooAzure AD application toowrite secrets tooyour key vault:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --spn <aadClientID> --perms-to-keys '["wrapKey"]' --perms-to-secrets '["set"]'`

2. <span data-ttu-id="08abf-629">chiffrement tooenable sur une machine virtuelle au existant ou en cours d’exécution :</span><span class="sxs-lookup"><span data-stu-id="08abf-629">tooenable encryption on an existing or running VM:</span></span>

 `azure vm enable-disk-encryption --resource-group <resourceGroupName> --name <vmName> --aad-client-id <aadClientId> --aad-client-secret <aadClientSecret> --disk-encryption-key-vault-url <keyVaultURL> --disk-encryption-key-vault-id <keyVaultResourceId> --volume-type [All|OS|Data]`

3. <span data-ttu-id="08abf-630">Obtenez l’état de chiffrement :</span><span class="sxs-lookup"><span data-stu-id="08abf-630">Get encryption status:</span></span>

 `azure vm show-disk-encryption-status --resource-group <resourceGroupName> --name <vmName> --json`

4. <span data-ttu-id="08abf-631">le chiffrement sur une machine virtuelle à partir de votre disque dur virtuel chiffrée, hello utilisez paramètres avec hello suivants tooenable `azure vm create` commande :</span><span class="sxs-lookup"><span data-stu-id="08abf-631">tooenable encryption on a new VM from your encrypted VHD, use hello following parameters with hello `azure vm create` command:</span></span>
 ```
   * disk-encryption-key-vault-id <disk-encryption-key-vault-id>
   * disk-encryption-key-url <disk-encryption-key-url>
   * key-encryption-key-vault-id <key-encryption-key-vault-id>
   * key-encryption-key-url <key-encryption-key-url>
 ```

### <a name="get-hello-encryption-status-of-an-encrypted-iaas-vm"></a><span data-ttu-id="08abf-632">Obtenir l’état de chiffrement hello d’une VM IaaS chiffrée</span><span class="sxs-lookup"><span data-stu-id="08abf-632">Get hello encryption status of an encrypted IaaS VM</span></span>
<span data-ttu-id="08abf-633">Vous pouvez obtenir l’état du chiffrement hello à l’aide du Gestionnaire de ressources Azure, [applets de commande PowerShell](/powershell/azure/overview), ou des commandes CLI.</span><span class="sxs-lookup"><span data-stu-id="08abf-633">You can get hello encryption status by using Azure Resource Manager, [PowerShell cmdlets](/powershell/azure/overview), or CLI commands.</span></span> <span data-ttu-id="08abf-634">Hello les sections suivantes explique comment toouse hello portail Azure classic et tooget des commandes CLI hello état du chiffrement.</span><span class="sxs-lookup"><span data-stu-id="08abf-634">hello following sections explain how toouse hello Azure classic portal and CLI commands tooget hello encryption status.</span></span>

#### <a name="get-hello-encryption-status-of-an-encrypted-windows-vm-by-using-azure-resource-manager"></a><span data-ttu-id="08abf-635">Obtenir l’état de chiffrement de hello d’une machine virtuelle de Windows chiffrées à l’aide du Gestionnaire de ressources Azure</span><span class="sxs-lookup"><span data-stu-id="08abf-635">Get hello encryption status of an encrypted Windows VM by using Azure Resource Manager</span></span>
<span data-ttu-id="08abf-636">Vous pouvez obtenir état du chiffrement hello Hello IaaS VM à partir du Gestionnaire de ressources Azure de manière hello suivante :</span><span class="sxs-lookup"><span data-stu-id="08abf-636">You can get hello encryption status of hello IaaS VM from Azure Resource Manager by doing hello following:</span></span>

1. <span data-ttu-id="08abf-637">Connectez-vous à toohello [portail Azure classic](https://portal.azure.com/), puis cliquez sur **virtuels** dans le volet gauche de hello toosee un récapitulatif des ordinateurs virtuels de hello dans votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="08abf-637">Sign in toohello [Azure classic portal](https://portal.azure.com/), and then click **Virtual machines** in hello left pane toosee a summary view of hello virtual machines in your subscription.</span></span> <span data-ttu-id="08abf-638">Vous pouvez filtrer la vue des machines virtuelles hello en sélectionnant le nom de l’abonnement hello Bonjour **abonnement** liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="08abf-638">You can filter hello virtual machines view by selecting hello subscription name in hello **Subscription** drop-down list.</span></span>

2. <span data-ttu-id="08abf-639">En haut de hello Hello **virtuels** , cliquez sur **colonnes**.</span><span class="sxs-lookup"><span data-stu-id="08abf-639">At hello top of hello **Virtual machines** page, click **Columns**.</span></span>

3. <span data-ttu-id="08abf-640">Sur hello **choisissez colonne** panneau, sélectionnez **chiffrement de disque**, puis cliquez sur **mise à jour**.</span><span class="sxs-lookup"><span data-stu-id="08abf-640">On hello **Choose column** blade, select **Disk Encryption**, and then click **Update**.</span></span> <span data-ttu-id="08abf-641">Vous devez voir État de chiffrement hello chiffrement de disque colonne affichant hello _activé_ ou _pas activé_ pour chaque machine virtuelle, comme indiqué dans la figure suivante de hello :</span><span class="sxs-lookup"><span data-stu-id="08abf-641">You should see hello disk-encryption column showing hello encryption state _Enabled_ or _Not Enabled_ for each VM, as shown in hello following figure:</span></span>

 ![Microsoft Antimalware dans Azure](./media/azure-security-disk-encryption/disk-encryption-fig2.png)

#### <a name="get-hello-encryption-status-of-an-encrypted-windowslinux-iaas-vm-by-using-hello-disk-encryption-powershell-cmdlet"></a><span data-ttu-id="08abf-643">Obtenir l’état du chiffrement hello d’un chiffrée (Windows/Linux) IaaS VM à l’aide d’applet de commande PowerShell de chiffrement de disque hello</span><span class="sxs-lookup"><span data-stu-id="08abf-643">Get hello encryption status of an encrypted (Windows/Linux) IaaS VM by using hello disk-encryption PowerShell cmdlet</span></span>
<span data-ttu-id="08abf-644">Vous pouvez obtenir l’état du chiffrement hello Hello IaaS VM à partir de l’applet de commande PowerShell de chiffrement de disque hello `Get-AzureRmVMDiskEncryptionStatus`.</span><span class="sxs-lookup"><span data-stu-id="08abf-644">You can get hello encryption status of hello IaaS VM from hello disk-encryption PowerShell cmdlet `Get-AzureRmVMDiskEncryptionStatus`.</span></span> <span data-ttu-id="08abf-645">paramètres de chiffrement tooget hello pour votre machine virtuelle, entrez hello qui suit :</span><span class="sxs-lookup"><span data-stu-id="08abf-645">tooget hello encryption settings for your VM, enter hello following:</span></span>

    C:\> Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $ResourceGroupName -VMName $VMName
    -ExtensionName $ExtensionName

    OsVolumeEncrypted          : NotEncrypted
    DataVolumesEncrypted       : Encrypted
    OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
    ProgressMessage            : https://rheltest1keyvault.vault.azure.net/secrets/bdb6bfb1-5431-4c28-af46-b18d0025ef2a/abebacb83d864a5fa729508315020f8a

<span data-ttu-id="08abf-646">Vous pouvez inspecter la sortie hello de _Get-AzureRmVMDiskEncryptionStatus_ pour le chiffrement de clé URL.</span><span class="sxs-lookup"><span data-stu-id="08abf-646">You can inspect hello output of _Get-AzureRmVMDiskEncryptionStatus_ for encryption key URLs.</span></span>

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

<span data-ttu-id="08abf-647">Hello OSVolumeEncrypted et les valeurs des paramètres DataVolumesEncrypted sont définies too_Encrypted_, ce qui indique que les deux volumes sont chiffrées à l’aide du chiffrement de disque Azure.</span><span class="sxs-lookup"><span data-stu-id="08abf-647">hello OSVolumeEncrypted and DataVolumesEncrypted settings values are set too_Encrypted_, which shows that both volumes are encrypted using Azure Disk Encryption.</span></span> <span data-ttu-id="08abf-648">Pour plus d’informations sur l’activation du chiffrement avec un chiffrement de disque Azure à l’aide des applets de commande PowerShell, consultez les billets de blog hello [Explorer le chiffrement de disque Azure avec Azure PowerShell - partie 1](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/explore-azure-disk-encryption-with-azure-powershell.aspx) et [Explorer de chiffrement de disque Azure avec Azure PowerShell - partie 2](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx).</span><span class="sxs-lookup"><span data-stu-id="08abf-648">For information about enabling encryption with Azure Disk Encryption by using PowerShell cmdlets, see hello blog posts [Explore Azure Disk Encryption with Azure PowerShell - Part 1](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/explore-azure-disk-encryption-with-azure-powershell.aspx) and [Explore Azure Disk Encryption with Azure PowerShell - Part 2](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="08abf-649">Sur les machines virtuelles Linux, il prend trois minutes toofour hello `Get-AzureRmVMDiskEncryptionStatus` état de chiffrement d’applet de commande tooreport hello.</span><span class="sxs-lookup"><span data-stu-id="08abf-649">On Linux VMs, it takes three toofour minutes for hello `Get-AzureRmVMDiskEncryptionStatus` cmdlet tooreport hello encryption status.</span></span>

#### <a name="get-hello-encryption-status-of-hello-iaas-vm-from-hello-disk-encryption-cli-command"></a><span data-ttu-id="08abf-650">Obtenir l’état du chiffrement hello Hello IaaS VM à partir de la commande CLI de chiffrement de disque hello</span><span class="sxs-lookup"><span data-stu-id="08abf-650">Get hello encryption status of hello IaaS VM from hello disk-encryption CLI command</span></span>
<span data-ttu-id="08abf-651">Vous pouvez obtenir l’état du chiffrement hello Hello IaaS VM à l’aide des commandes CLI de chiffrement de disque hello `azure vm show-disk-encryption-status`.</span><span class="sxs-lookup"><span data-stu-id="08abf-651">You can get hello encryption status of hello IaaS VM by using hello disk-encryption CLI command `azure vm show-disk-encryption-status`.</span></span> <span data-ttu-id="08abf-652">paramètres de chiffrement tooget hello pour votre machine virtuelle, entrez votre session CLI d’Azure :</span><span class="sxs-lookup"><span data-stu-id="08abf-652">tooget hello encryption settings for your VM, enter your Azure CLI session:</span></span>

    azure vm show-disk-encryption-status --resource-group <yourResourceGroupName> --name <yourVMName> --json  

#### <a name="disable-encryption-on-running-windows-iaas-vm"></a><span data-ttu-id="08abf-653">Désactivation du chiffrement sur une machine virtuelle IaaS Windows en cours d’exécution</span><span class="sxs-lookup"><span data-stu-id="08abf-653">Disable encryption on running Windows IaaS VM</span></span>
<span data-ttu-id="08abf-654">Vous pouvez désactiver le chiffrement sur un ordinateur virtuel IaaS de Linux ou Windows en cours d’exécution via le modèle de chiffrement de disque Azure Resource Manager hello ou des applets de commande PowerShell et configuration de déchiffrement hello.</span><span class="sxs-lookup"><span data-stu-id="08abf-654">You can disable encryption on a running Windows or Linux IaaS VM via hello Azure Disk Encryption Resource Manager template or PowerShell cmdlets and specify hello decryption configuration.</span></span>

##### <a name="windows-vm"></a><span data-ttu-id="08abf-655">Machine virtuelle Windows</span><span class="sxs-lookup"><span data-stu-id="08abf-655">Windows VM</span></span>
<span data-ttu-id="08abf-656">étape de chiffrement de la désactivation de Hello désactive le chiffrement de hello du système d’exploitation, le volume de données hello ou les deux sur hello machine virtuelle IaaS de Windows en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="08abf-656">hello disable-encryption step disables encryption of hello OS, hello data volume, or both on hello running Windows IaaS VM.</span></span> <span data-ttu-id="08abf-657">Vous ne peut pas désactiver le volume du système d’exploitation hello et laisser le volume de données hello chiffré.</span><span class="sxs-lookup"><span data-stu-id="08abf-657">You cannot disable hello OS volume and leave hello data volume encrypted.</span></span> <span data-ttu-id="08abf-658">Lors de l’étape de chiffrement de la désactiver hello est effectuée, modèle de déploiement classique Azure hello met à jour le modèle de service de machine virtuelle hello, et hello machine virtuelle IaaS de Windows est déchiffré.</span><span class="sxs-lookup"><span data-stu-id="08abf-658">When hello disable-encryption step is performed, hello Azure classic deployment model updates hello VM service model, and hello Windows IaaS VM is marked decrypted.</span></span> <span data-ttu-id="08abf-659">contenu Hello Hello machine virtuelle n’est plus chiffrés au repos.</span><span class="sxs-lookup"><span data-stu-id="08abf-659">hello contents of hello VM are no longer encrypted at rest.</span></span> <span data-ttu-id="08abf-660">le déchiffrement de Hello ne supprime pas votre clé coffre et hello chiffrement matériel de clé (clés de chiffrement BitLocker pour Windows et le mot de passe pour Linux).</span><span class="sxs-lookup"><span data-stu-id="08abf-660">hello decryption does not delete your key vault and hello encryption key material (BitLocker encryption keys for Windows and Passphrase for Linux).</span></span>

##### <a name="linux-vm"></a><span data-ttu-id="08abf-661">Machine virtuelle Linux</span><span class="sxs-lookup"><span data-stu-id="08abf-661">Linux VM</span></span>
<span data-ttu-id="08abf-662">étape de chiffrement de la désactivation de Hello désactive le chiffrement de volume de données hello hello machine virtuelle IaaS de Linux en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="08abf-662">hello disable-encryption step disables encryption of hello data volume on hello running Linux IaaS VM.</span></span> <span data-ttu-id="08abf-663">Cette étape fonctionne uniquement si le disque du système d’exploitation hello n’est pas chiffré.</span><span class="sxs-lookup"><span data-stu-id="08abf-663">This step only works if hello OS disk is not encrypted.</span></span>

> [!NOTE]
> <span data-ttu-id="08abf-664">La désactivation du chiffrement sur le disque du système d’exploitation hello n’est pas autorisée sur les machines virtuelles Linux.</span><span class="sxs-lookup"><span data-stu-id="08abf-664">Disabling encryption on hello OS disk is not allowed on Linux VMs.</span></span>

##### <a name="disable-encryption-on-an-existing-or-running-iaas-vm"></a><span data-ttu-id="08abf-665">Désactivation du chiffrement sur une machine virtuelle IaaS existante ou en cours d’exécution</span><span class="sxs-lookup"><span data-stu-id="08abf-665">Disable encryption on an existing or running IaaS VM</span></span>
<span data-ttu-id="08abf-666">Vous pouvez désactiver le chiffrement de disque sur les machines virtuelles IaaS Windows en cours d’exécution à l’aide de hello [modèle Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-decrypt-running-windows-vm).</span><span class="sxs-lookup"><span data-stu-id="08abf-666">You can disable disk encryption on running Windows IaaS VMs by using hello [Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-decrypt-running-windows-vm).</span></span>

1. <span data-ttu-id="08abf-667">Sur le modèle de hello Azure de démarrage rapide, cliquez sur **déployer tooAzure**, entrez la configuration du déchiffrement hello sur hello **paramètres** panneau, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="08abf-667">On hello Azure quick-start template, click **Deploy tooAzure**, enter hello decryption configuration on hello **Parameters** blade, and then click **OK**.</span></span>

2. <span data-ttu-id="08abf-668">Sélectionnez l’abonnement de hello, groupe de ressources, emplacement du groupe de ressources, juridiques et contrat, puis cliquez sur **créer** tooenable le chiffrement sur un VM IaaS nouvelle.</span><span class="sxs-lookup"><span data-stu-id="08abf-668">Select hello subscription, resource group, resource group location, legal terms, and agreement, and then click **Create** tooenable encryption on a new IaaS VM.</span></span>

<span data-ttu-id="08abf-669">Pour les machines virtuelles Linux, vous pouvez désactiver le chiffrement à l’aide de hello [désactiver le chiffrement sur un VM Linux en cours d’exécution](https://aka.ms/decrypt-linuxvm) modèle.</span><span class="sxs-lookup"><span data-stu-id="08abf-669">For Linux VMs, you can disable encryption by using hello [Disable encryption on a running Linux VM](https://aka.ms/decrypt-linuxvm) template.</span></span>

<span data-ttu-id="08abf-670">Hello tableau suivant répertorie les paramètres de modèle de gestionnaire de ressources pour la désactivation du chiffrement sur un VM IaaS en cours d’exécution :</span><span class="sxs-lookup"><span data-stu-id="08abf-670">hello following table lists Resource Manager template parameters for disabling encryption on a running IaaS VM:</span></span>

| <span data-ttu-id="08abf-671">Paramètre</span><span class="sxs-lookup"><span data-stu-id="08abf-671">Parameter</span></span> | <span data-ttu-id="08abf-672">Description</span><span class="sxs-lookup"><span data-stu-id="08abf-672">Description</span></span> |
| --- | --- |
| <span data-ttu-id="08abf-673">vmName</span><span class="sxs-lookup"><span data-stu-id="08abf-673">vmName</span></span> | <span data-ttu-id="08abf-674">Nom de machine virtuelle qui hello l’opération de chiffrement de hello est toobe effectuée sur.</span><span class="sxs-lookup"><span data-stu-id="08abf-674">Name of hello VM that hello encryption operation is toobe performed on.</span></span>
| <span data-ttu-id="08abf-675">volumeType</span><span class="sxs-lookup"><span data-stu-id="08abf-675">volumeType</span></span> | <span data-ttu-id="08abf-676">Type de volume sur lequel l’opération de déchiffrement est effectuée.</span><span class="sxs-lookup"><span data-stu-id="08abf-676">Type of volume that a decryption operation is performed on.</span></span> <span data-ttu-id="08abf-677">Les valeurs valides sont _Système d’exploitation_, _Données_ et _Tous_.</span><span class="sxs-lookup"><span data-stu-id="08abf-677">Valid values are _OS_, _Data_, and _All_.</span></span> <span data-ttu-id="08abf-678">Vous ne pouvez pas désactiver le chiffrement sur le volume du système d’exploitation Windows IaaS VM/de démarrage en cours d’exécution sans la désactivation du chiffrement sur hello _données_ volume.</span><span class="sxs-lookup"><span data-stu-id="08abf-678">You cannot disable encryption on running Windows IaaS VM OS/boot volume without disabling encryption on hello _Data_ volume.</span></span> <span data-ttu-id="08abf-679">Notez également que la désactivation du chiffrement sur le disque du système d’exploitation hello n’est pas autorisée sur les machines virtuelles Linux.</span><span class="sxs-lookup"><span data-stu-id="08abf-679">Also note that disabling encryption on hello OS disk is not allowed on Linux VMs.</span></span> |
| <span data-ttu-id="08abf-680">sequenceVersion</span><span class="sxs-lookup"><span data-stu-id="08abf-680">sequenceVersion</span></span> | <span data-ttu-id="08abf-681">Version de la séquence de hello BitLocker opération.</span><span class="sxs-lookup"><span data-stu-id="08abf-681">Sequence version of hello BitLocker operation.</span></span> <span data-ttu-id="08abf-682">Incrémenter ce numéro de version, chaque fois qu’une opération de déchiffrement de disque est exécutée sur hello même machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="08abf-682">Increment this version number every time a disk decryption operation is performed on hello same VM.</span></span> |

##### <a name="disable-encryption-on-an-existing-or-running-iaas-vm"></a><span data-ttu-id="08abf-683">Désactivation du chiffrement sur une machine virtuelle IaaS existante ou en cours d’exécution</span><span class="sxs-lookup"><span data-stu-id="08abf-683">Disable encryption on an existing or running IaaS VM</span></span>
<span data-ttu-id="08abf-684">chiffrement toodisable sur une VM IaaS existant ou en cours d’exécution à l’aide d’applet de commande PowerShell hello, consultez [ `Disable-AzureRmVMDiskEncryption` ](/powershell/module/azurerm.compute/disable-azurermvmdiskencryption).</span><span class="sxs-lookup"><span data-stu-id="08abf-684">toodisable encryption on an existing or running IaaS VM by using hello PowerShell cmdlet, see [`Disable-AzureRmVMDiskEncryption`](/powershell/module/azurerm.compute/disable-azurermvmdiskencryption).</span></span> <span data-ttu-id="08abf-685">Cette applet de commande prend en charge les machines virtuelles Linux et Windows.</span><span class="sxs-lookup"><span data-stu-id="08abf-685">This cmdlet supports both Windows and Linux VMs.</span></span> <span data-ttu-id="08abf-686">le chiffrement toodisable, il installe une extension sur l’ordinateur virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="08abf-686">toodisable encryption, it installs an extension on hello virtual machine.</span></span> <span data-ttu-id="08abf-687">Si hello _nom_ paramètre n’est pas spécifié, une extension avec le nom par défaut de hello _AzureDiskEncryption pour Windows machines virtuelles_ est créé.</span><span class="sxs-lookup"><span data-stu-id="08abf-687">If hello _Name_ parameter is not specified, an extension with hello default name _AzureDiskEncryption for Windows VMs_ is created.</span></span>

<span data-ttu-id="08abf-688">Sur les machines virtuelles Linux, hello AzureDiskEncryptionForLinux extension est utilisée.</span><span class="sxs-lookup"><span data-stu-id="08abf-688">On Linux VMs, hello AzureDiskEncryptionForLinux extension is used.</span></span>

> [!NOTE]
> <span data-ttu-id="08abf-689">Cette applet de commande redémarre l’ordinateur virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="08abf-689">This cmdlet reboots hello virtual machine.</span></span>

### <a name="enable-encryption-on-pre-encrypted-iaas-vm-with-azure-managed-disk"></a><span data-ttu-id="08abf-690">Activer le chiffrement sur une machine virtuelle IaaS pré-chiffrée avec un disque managé Azure</span><span class="sxs-lookup"><span data-stu-id="08abf-690">Enable encryption on pre-encrypted IaaS VM with Azure Managed Disk</span></span>
<span data-ttu-id="08abf-691">Utilisez hello ARM de disque géré Azure modèle toocreate une VM chiffrée à partir d’un disque dur virtuel déjà chiffré à l’aide du modèle de hello ARM située</span><span class="sxs-lookup"><span data-stu-id="08abf-691">Use hello Azure Managed Disk ARM template toocreate a encrypted VM from a pre-encrypted VHD using hello ARM template located at</span></span>   
<span data-ttu-id="08abf-692">[Créer un disque managé chiffré à partir d’un disque dur virtuel/bjet blob de stockage pré-chiffré] (https://github.com/Azure/azure-quickstart-templates/tree/master/201-create-encrypted-managed-disk)</span><span class="sxs-lookup"><span data-stu-id="08abf-692">[Create a new encrypted managed disk from a pre-encrypted VHD/storage blob] (https://github.com/Azure/azure-quickstart-templates/tree/master/201-create-encrypted-managed-disk)</span></span>

### <a name="enable-encryption-on-a-new-linux-iaas-vm-with-azure-managed-disk"></a><span data-ttu-id="08abf-693">Activer le chiffrement sur une nouvelle machine virtuelle IaaS Linux avec disque managé Azure</span><span class="sxs-lookup"><span data-stu-id="08abf-693">Enable encryption on a new Linux IaaS VM with Azure Managed Disk</span></span>
<span data-ttu-id="08abf-694">Utilisez hello ARM de disque géré Azure modèle toocreate chiffrées d’une nouvelle machine virtuelle IaaS de Linux à l’aide du modèle d’ARM hello situé</span><span class="sxs-lookup"><span data-stu-id="08abf-694">Use hello Azure Managed Disk ARM template toocreate a new encrypted Linux IaaS VM using hello ARM template located at</span></span>   
<span data-ttu-id="08abf-695">[Déploiement de RHEL 7.2 avec un chiffrement de disque complet] (https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-full-disk-encrypted-rhel)</span><span class="sxs-lookup"><span data-stu-id="08abf-695">[Deployment of RHEL 7.2 with full disk encryption] (https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-full-disk-encrypted-rhel)</span></span>

### <a name="enable-encryption-on-a-new-windows-iaas-vm-with-azure-managed-disk"></a><span data-ttu-id="08abf-696">Activer le chiffrement sur une nouvelle machine virtuelle IaaS Windows avec disque managé Azure</span><span class="sxs-lookup"><span data-stu-id="08abf-696">Enable encryption on a new Windows IaaS VM with Azure Managed Disk</span></span>
 <span data-ttu-id="08abf-697">Utilisez hello ARM de disque géré Azure modèle toocreate chiffrées d’une nouvelle machine virtuelle IaaS de Linux à l’aide du modèle d’ARM hello situé</span><span class="sxs-lookup"><span data-stu-id="08abf-697">Use hello Azure Managed Disk ARM template toocreate a new encrypted Linux IaaS VM using hello ARM template located at</span></span>   
 <span data-ttu-id="08abf-698">[Créer une machine virtuelle avec disque managé IaaS Windows chiffré à partir d’une image de la galerie] (https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-new-vm-gallery-image-managed-disks)</span><span class="sxs-lookup"><span data-stu-id="08abf-698">[Create a new encrypted Windows IaaS Managed Disk VM from gallery image] (https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-new-vm-gallery-image-managed-disks)</span></span>

  > [!NOTE]
  ><span data-ttu-id="08abf-699">Il est obligatoire toosnapshot et/ou sauvegarde un disque géré basée et instance de machine virtuelle en dehors de tooenabling préalable chiffrement de disque Azure.</span><span class="sxs-lookup"><span data-stu-id="08abf-699">It is mandatory toosnapshot and/or backup a managed disk based VM instance outside of and prior tooenabling Azure Disk Encryption.</span></span>  <span data-ttu-id="08abf-700">Un instantané de disque géré de hello peut provenir de portail de hello ou Azure Backup peut être utilisé.</span><span class="sxs-lookup"><span data-stu-id="08abf-700">A snapshot of hello managed disk can be taken from hello portal, or Azure Backup can be used.</span></span>  <span data-ttu-id="08abf-701">Sauvegardes de vous assurer qu’une option de récupération est possible dans les cas de hello de toute défaillance inattendue pendant le chiffrement.</span><span class="sxs-lookup"><span data-stu-id="08abf-701">Backups ensure that a recovery option is possible in hello case of any unexpected failure during encryption.</span></span>  <span data-ttu-id="08abf-702">Une fois qu’une sauvegarde est effectuée, applet de commande hello AzureRmVMDiskEncryptionExtension de jeu peut être utilisé tooencrypt géré disques en spécifiant le paramètre - skipVmBackup de hello.</span><span class="sxs-lookup"><span data-stu-id="08abf-702">Once a backup is made, hello Set-AzureRmVMDiskEncryptionExtension cmdlet can be used tooencrypt managed disks by specifying hello -skipVmBackup parameter.</span></span>  <span data-ttu-id="08abf-703">Cette commande échoue sur les machines virtuelles de disques gérés tant qu’une sauvegarde n’a pas été effectuée et que ce paramètre n’a pas été spécifié.</span><span class="sxs-lookup"><span data-stu-id="08abf-703">This command will fail against managed disk based VM's until a backup has been made and this parameter has been specified.</span></span>    
 
### <a name="update-encryption-settings-of-an-existing-encrypted-non-premium-vm"></a><span data-ttu-id="08abf-704">Mettre à jour les paramètres de chiffrement d’une machine virtuelle non Premium chiffrée existante</span><span class="sxs-lookup"><span data-stu-id="08abf-704">Update encryption settings of an existing encrypted non-premium VM</span></span>
  <span data-ttu-id="08abf-705">Utilisez hello disque Azure chiffrement pris en charge des interfaces existantes pour l’exécution de machine virtuelle [applets de commande PS, modèles CLI ou ARM] tooupdate paramètres de chiffrement hello comme client AAD ID/secret, clé de cryptage [KEK], clé de chiffrement BitLocker pour la machine virtuelle Windows ou le mot de passe Paramètre de chiffrement de mise à jour etc. de machine virtuelle Linux hello est pris en charge uniquement pour les machines virtuelles soutenus par un stockage non-premium.</span><span class="sxs-lookup"><span data-stu-id="08abf-705">Use hello existing Azure disk encryption supported interfaces for running VM [PS cmdlets, CLI or ARM templates] tooupdate hello encryption settings like AAD client ID/secret, Key encryption key [KEK], BitLocker encryption key for Windows VM or Passphrase for Linux VM etc. hello update encryption setting is supported only for VMs backed by non-premium storage.</span></span> <span data-ttu-id="08abf-706">Il n’est PAS pris en charge pour des machines virtuelles s’appuyant sur un stockage Premium.</span><span class="sxs-lookup"><span data-stu-id="08abf-706">It is NNOT supported for VMs backed by premium storage.</span></span>

## <a name="appendix"></a><span data-ttu-id="08abf-707">Annexe</span><span class="sxs-lookup"><span data-stu-id="08abf-707">Appendix</span></span>
### <a name="connect-tooyour-subscription"></a><span data-ttu-id="08abf-708">Se connecter tooyour abonnement</span><span class="sxs-lookup"><span data-stu-id="08abf-708">Connect tooyour subscription</span></span>
<span data-ttu-id="08abf-709">Avant de continuer, examinez hello *conditions préalables* dans cet article.</span><span class="sxs-lookup"><span data-stu-id="08abf-709">Before you proceed, review hello *Prerequisites* section in this article.</span></span> <span data-ttu-id="08abf-710">Après avoir vérifié que toutes les conditions préalables sont remplies, connexion tooyour abonnement de manière hello suivante :</span><span class="sxs-lookup"><span data-stu-id="08abf-710">After you ensure that all prerequisites have been met, connect tooyour subscription by doing hello following:</span></span>

1. <span data-ttu-id="08abf-711">Démarrez une session Azure PowerShell et connectez-vous tooyour compte Azure avec hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="08abf-711">Start an Azure PowerShell session, and sign in tooyour Azure account with hello following command:</span></span>

    `Login-AzureRmAccount`

2. <span data-ttu-id="08abf-712">Si vous avez plusieurs abonnements et que vous souhaitez les un toouse toospecify, tapez Bonjour suivant toosee les abonnements de hello pour votre compte :</span><span class="sxs-lookup"><span data-stu-id="08abf-712">If you have multiple subscriptions and want toospecify one toouse, type hello following toosee hello subscriptions for your account:</span></span>

    `Get-AzureRmSubscription`

3. <span data-ttu-id="08abf-713">toospecify hello abonnement toouse, type :</span><span class="sxs-lookup"><span data-stu-id="08abf-713">toospecify hello subscription you want toouse, type:</span></span>

    `Select-AzureRmSubscription -SubscriptionName <Yoursubscriptionname>`

4. <span data-ttu-id="08abf-714">tooverify que l’abonnement hello configuré est correct, tapez :</span><span class="sxs-lookup"><span data-stu-id="08abf-714">tooverify that hello subscription configured is correct, type:</span></span>

    `Get-AzureRmSubscription`

5. <span data-ttu-id="08abf-715">tooconfirm hello Azure chiffrement de disque applets de commande sont installés, type :</span><span class="sxs-lookup"><span data-stu-id="08abf-715">tooconfirm hello Azure Disk Encryption cmdlets are installed, type:</span></span>

    `Get-command *diskencryption*`

6. <span data-ttu-id="08abf-716">Hello suivant sortie confirme que l’installation de chiffrement de disque de Azure PowerShell hello :</span><span class="sxs-lookup"><span data-stu-id="08abf-716">hello following output confirms hello Azure Disk Encryption PowerShell installation:</span></span>

```
    PS C:\Windows\System32\WindowsPowerShell\v1.0> get-command *diskencryption*
    CommandType  Name                                         Source                                                             
    Cmdlet       Get-AzureRmVMDiskEncryptionStatus            AzureRM.Compute                                                    
    Cmdlet       Disable-AzureRmVMDiskEncryption              AzureRM.Compute                                                    
    Cmdlet       Set-AzureRmVMDiskEncryptionExtension         AzureRM.Compute                                                     
```

### <a name="prepare-a-pre-encrypted-windows-vhd"></a><span data-ttu-id="08abf-717">Préparer un disque dur virtuel Windows déjà chiffré</span><span class="sxs-lookup"><span data-stu-id="08abf-717">Prepare a pre-encrypted Windows VHD</span></span>
<span data-ttu-id="08abf-718">les sections Hello qui suivent sont nécessaire tooprepare un disque dur virtuel Windows déjà chiffrés pour le déploiement sous la forme d’un disque dur virtuel chiffré dans Azure IaaS.</span><span class="sxs-lookup"><span data-stu-id="08abf-718">hello sections that follow are necessary tooprepare a pre-encrypted Windows VHD for deployment as an encrypted VHD in Azure IaaS.</span></span> <span data-ttu-id="08abf-719">Utilisez hello informations tooprepare et démarrer une nouvelle machine virtuelle (disque dur virtuel Windows) sur Azure Site Recovery ou sur Azure.</span><span class="sxs-lookup"><span data-stu-id="08abf-719">Use hello information tooprepare and boot a fresh Windows VM (VHD) on Azure Site Recovery or Azure.</span></span>

#### <a name="update-group-policy-tooallow-non-tpm-for-os-protection"></a><span data-ttu-id="08abf-720">Mettre à jour le groupe stratégie tooallow non TPM pour la protection du système d’exploitation</span><span class="sxs-lookup"><span data-stu-id="08abf-720">Update group policy tooallow non-TPM for OS protection</span></span>
<span data-ttu-id="08abf-721">Configurer le paramètre de stratégie de groupe BitLocker hello **le chiffrement de lecteur BitLocker**, que vous trouverez sous **stratégie ordinateur Local** > **Configuration de l’ordinateur**  >  **Modèles d’administration** > **composants Windows**.</span><span class="sxs-lookup"><span data-stu-id="08abf-721">Configure hello BitLocker Group Policy setting **BitLocker Drive Encryption**, which you'll find under **Local Computer Policy** > **Computer Configuration** > **Administrative Templates** > **Windows Components**.</span></span> <span data-ttu-id="08abf-722">Modifier ce paramètre trop**lecteurs de système d’exploitation** > **exiger une authentification supplémentaire au démarrage** > **Autoriser BitLocker sans un module de plateforme sécurisée compatible**, comme illustré dans la figure suivante de hello :</span><span class="sxs-lookup"><span data-stu-id="08abf-722">Change this setting too**Operating System Drives** > **Require additional authentication at startup** > **Allow BitLocker without a compatible TPM**, as shown in hello following figure:</span></span>

![Microsoft Antimalware dans Azure](./media/azure-security-disk-encryption/disk-encryption-fig8.png)

#### <a name="install-bitlocker-feature-components"></a><span data-ttu-id="08abf-724">Installer les composants de fonctionnalité BitLocker</span><span class="sxs-lookup"><span data-stu-id="08abf-724">Install BitLocker feature components</span></span>
<span data-ttu-id="08abf-725">Pour Windows Server 2012 et versions ultérieures, utilisez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="08abf-725">For Windows Server 2012 and later, use hello following command:</span></span>

    dism /online /Enable-Feature /all /FeatureName:BitLocker /quiet /norestart

<span data-ttu-id="08abf-726">Pour Windows Server 2008 R2, utilisez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="08abf-726">For Windows Server 2008 R2, use hello following command:</span></span>

    ServerManagerCmd -install BitLockers

#### <a name="prepare-hello-os-volume-for-bitlocker-by-using-bdehdcfg"></a><span data-ttu-id="08abf-727">Préparer le volume du système d’exploitation hello pour BitLocker à l’aide`bdehdcfg`</span><span class="sxs-lookup"><span data-stu-id="08abf-727">Prepare hello OS volume for BitLocker by using `bdehdcfg`</span></span>
<span data-ttu-id="08abf-728">toocompress hello partition du système d’exploitation et préparer l’ordinateur de hello pour BitLocker, exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="08abf-728">toocompress hello OS partition and prepare hello machine for BitLocker, execute hello following command:</span></span>

    bdehdcfg -target c: shrink -quiet

#### <a name="protect-hello-os-volume-by-using-bitlocker"></a><span data-ttu-id="08abf-729">Protéger le volume du système d’exploitation hello à l’aide de BitLocker</span><span class="sxs-lookup"><span data-stu-id="08abf-729">Protect hello OS volume by using BitLocker</span></span>
<span data-ttu-id="08abf-730">Hello d’utilisation [ `manage-bde` ](https://technet.microsoft.com/library/ff829849.aspx) chiffrement tooenable de commande sur le volume de démarrage hello à l’aide d’un protecteur de clé externe.</span><span class="sxs-lookup"><span data-stu-id="08abf-730">Use hello [`manage-bde`](https://technet.microsoft.com/library/ff829849.aspx) command tooenable encryption on hello boot volume using an external key protector.</span></span> <span data-ttu-id="08abf-731">Placez également clé externe de hello (fichier .bek) sur un disque externe hello ou un volume.</span><span class="sxs-lookup"><span data-stu-id="08abf-731">Also place hello external key (.bek file) on hello external drive or volume.</span></span> <span data-ttu-id="08abf-732">Le chiffrement est activé sur le volume de système de démarrage hello hello prochain redémarrage.</span><span class="sxs-lookup"><span data-stu-id="08abf-732">Encryption is enabled on hello system/boot volume after hello next reboot.</span></span>

    manage-bde -on %systemdrive% -sk [ExternalDriveOrVolume]
    reboot

> [!NOTE]
> <span data-ttu-id="08abf-733">Préparer hello machine virtuelle avec un disque dur virtuel données/ressources distinct pour l’obtention de clé externe de hello à l’aide de BitLocker.</span><span class="sxs-lookup"><span data-stu-id="08abf-733">Prepare hello VM with a separate data/resource VHD for getting hello external key by using BitLocker.</span></span>

#### <a name="encrypting-an-os-drive-on-a-running-linux-vm"></a><span data-ttu-id="08abf-734">Chiffrement d’un lecteur du système d’exploitation sur une machine virtuelle Linux en cours d’exécution</span><span class="sxs-lookup"><span data-stu-id="08abf-734">Encrypting an OS drive on a running Linux VM</span></span>
<span data-ttu-id="08abf-735">Chiffrement d’un lecteur du système d’exploitation sur un VM Linux en cours d’exécution est pris en charge sur hello suivant distributions :</span><span class="sxs-lookup"><span data-stu-id="08abf-735">Encryption of an OS drive on a running Linux VM is supported on hello following distributions:</span></span>

* <span data-ttu-id="08abf-736">RHEL 7.2</span><span class="sxs-lookup"><span data-stu-id="08abf-736">RHEL 7.2</span></span>
* <span data-ttu-id="08abf-737">CentOS 7.2</span><span class="sxs-lookup"><span data-stu-id="08abf-737">CentOS 7.2</span></span>
* <span data-ttu-id="08abf-738">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="08abf-738">Ubuntu 16.04</span></span>

##### <a name="prerequisites-for-os-disk-encryption"></a><span data-ttu-id="08abf-739">Configuration requise pour le chiffrement du lecteur du système d’exploitation</span><span class="sxs-lookup"><span data-stu-id="08abf-739">Prerequisites for OS disk encryption</span></span>

* <span data-ttu-id="08abf-740">Hello machine virtuelle doit être créé à partir d’une image Marketplace hello dans Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="08abf-740">hello VM must be created from hello Marketplace image in Azure Resource Manager.</span></span>
* <span data-ttu-id="08abf-741">Machine virtuelle Azure au moins 4 Go de RAM (la taille recommandée est de 7 Go).</span><span class="sxs-lookup"><span data-stu-id="08abf-741">Azure VM with at least 4 GB of RAM (recommended size is 7 GB).</span></span>
* <span data-ttu-id="08abf-742">(Pour RHEL et CentOS) Désactivez SELinux.</span><span class="sxs-lookup"><span data-stu-id="08abf-742">(For RHEL and CentOS) Disable SELinux.</span></span> <span data-ttu-id="08abf-743">toodisable SELinux, consultez « 4.4.2.</span><span class="sxs-lookup"><span data-stu-id="08abf-743">toodisable SELinux, see "4.4.2.</span></span> <span data-ttu-id="08abf-744">La désactivation de SELinux « Bonjour [Guide l’utilisateur SELinux et d’administration](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/SELinux_Users_and_Administrators_Guide/sect-Security-Enhanced_Linux-Working_with_SELinux-Changing_SELinux_Modes.html#sect-Security-Enhanced_Linux-Enabling_and_Disabling_SELinux-Disabling_SELinux) sur hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="08abf-744">Disabling SELinux" in hello [SELinux User's and Administrator's Guide](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/SELinux_Users_and_Administrators_Guide/sect-Security-Enhanced_Linux-Working_with_SELinux-Changing_SELinux_Modes.html#sect-Security-Enhanced_Linux-Enabling_and_Disabling_SELinux-Disabling_SELinux) on hello VM.</span></span>
* <span data-ttu-id="08abf-745">Après avoir désactivé SELinux, redémarrez hello VM au moins une fois.</span><span class="sxs-lookup"><span data-stu-id="08abf-745">After you disable SELinux, reboot hello VM at least once.</span></span>

##### <a name="steps"></a><span data-ttu-id="08abf-746">Étapes</span><span class="sxs-lookup"><span data-stu-id="08abf-746">Steps</span></span>
1. <span data-ttu-id="08abf-747">Créer une machine virtuelle à l’aide d’une des distributions hello spécifiées précédemment.</span><span class="sxs-lookup"><span data-stu-id="08abf-747">Create a VM by using one of hello distributions specified previously.</span></span>

 <span data-ttu-id="08abf-748">Pour CentOS 7.2, le chiffrement du lecteur du système d’exploitation est pris en charge via une image spécifique.</span><span class="sxs-lookup"><span data-stu-id="08abf-748">For CentOS 7.2, OS disk encryption is supported via a special image.</span></span> <span data-ttu-id="08abf-749">toouse cette image, spécifiez « 7.2n » comme hello référence (SKU) lorsque vous créez hello machine virtuelle :</span><span class="sxs-lookup"><span data-stu-id="08abf-749">toouse this image, specify "7.2n" as hello SKU when you create hello VM:</span></span>
 ```
    Set-AzureRmVMSourceImage -VM $VirtualMachine -PublisherName "OpenLogic" -Offer "CentOS" -Skus "7.2n" -Version "latest"
 ```
2. <span data-ttu-id="08abf-750">Configurer les besoins de tooyour conséquente hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="08abf-750">Configure hello VM according tooyour needs.</span></span> <span data-ttu-id="08abf-751">Si vous vous apprêtez à tooencrypt tous les lecteurs hello (système d’exploitation + données), les lecteurs de données hello besoin toobe spécifié et montable dans/etc/fstab.</span><span class="sxs-lookup"><span data-stu-id="08abf-751">If you are going tooencrypt all hello (OS + data) drives, hello data drives need toobe specified and mountable from /etc/fstab.</span></span>

 > [!NOTE]
 > <span data-ttu-id="08abf-752">Utilisez UUID =... toospecify lecteurs de données dans/etc/fstab au lieu de spécifier le nom de périphérique du bloc hello (par exemple, / dev/sdb1).</span><span class="sxs-lookup"><span data-stu-id="08abf-752">Use UUID=... toospecify data drives in /etc/fstab instead of specifying hello block device name (for example, /dev/sdb1).</span></span> <span data-ttu-id="08abf-753">Au cours du chiffrement, hello ordre des modifications de lecteurs sur hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="08abf-753">During encryption, hello order of drives changes on hello VM.</span></span> <span data-ttu-id="08abf-754">Si votre machine virtuelle s’appuie sur un ordre spécifique de périphériques de bloc, il échouera toomount après chiffrement.</span><span class="sxs-lookup"><span data-stu-id="08abf-754">If your VM relies on a specific order of block devices, it will fail toomount them after encryption.</span></span>

3. <span data-ttu-id="08abf-755">Déconnectez-vous de sessions SSH hello.</span><span class="sxs-lookup"><span data-stu-id="08abf-755">Sign out of hello SSH sessions.</span></span>

4. <span data-ttu-id="08abf-756">tooencrypt hello du système d’exploitation, spécifiez volumeType comme **tous les** ou **système d’exploitation** lorsque vous [activer le chiffrement](#enable-encryption-on-existing-or-running-iaas-linux-vm-in-azure).</span><span class="sxs-lookup"><span data-stu-id="08abf-756">tooencrypt hello OS, specify volumeType as **All** or **OS** when you [enable encryption](#enable-encryption-on-existing-or-running-iaas-linux-vm-in-azure).</span></span>

 > [!NOTE]
 > <span data-ttu-id="08abf-757">Tous les processus d’espace utilisateur qui ne s’exécutent pas en tant que services `systemd` doivent être arrêtés avec un `SIGKILL`.</span><span class="sxs-lookup"><span data-stu-id="08abf-757">All user-space processes that are not running as `systemd` services should be killed with a `SIGKILL`.</span></span> <span data-ttu-id="08abf-758">Redémarrez hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="08abf-758">Reboot hello VM.</span></span> <span data-ttu-id="08abf-759">Lorsque vous activez le chiffrement du lecteur du système d’exploitation sur une machine virtuelle en cours d’exécution, prévoyez un temps d’arrêt de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="08abf-759">When you enable OS disk encryption on a running VM, plan on VM downtime.</span></span>

5. <span data-ttu-id="08abf-760">Contrôlez régulièrement la progression hello du chiffrement à l’aide des instructions hello Bonjour [section suivante](#monitoring-os-encryption-progress).</span><span class="sxs-lookup"><span data-stu-id="08abf-760">Periodically monitor hello progress of encryption by using hello instructions in hello [next section](#monitoring-os-encryption-progress).</span></span>

6. <span data-ttu-id="08abf-761">Une fois que Get-AzureRmVmDiskEncryptionStatus affiche « VMRestartPending », redémarrez votre machine virtuelle en vous connectant tooit ou en utilisant le portail de hello, PowerShell ou CLI.</span><span class="sxs-lookup"><span data-stu-id="08abf-761">After Get-AzureRmVmDiskEncryptionStatus shows "VMRestartPending," restart your VM either by signing in tooit or by using hello portal, PowerShell, or CLI.</span></span>
    ```
    C:\> Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $ResourceGroupName -VMName $VMName
    -ExtensionName $ExtensionName

    OsVolumeEncrypted          : VMRestartPending
    DataVolumesEncrypted       : NotMounted
    OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
    ProgressMessage            : OS disk successfully encrypted, reboot hello VM
    ```
<span data-ttu-id="08abf-762">Avant de redémarrer, nous recommandons d’enregistrer [diagnostics de démarrage](https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/) Hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="08abf-762">Before you reboot, we recommend that you save [boot diagnostics](https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/) of hello VM.</span></span>

#### <a name="monitoring-os-encryption-progress"></a><span data-ttu-id="08abf-763">Surveillance de la progression du chiffrement du système d’exploitation</span><span class="sxs-lookup"><span data-stu-id="08abf-763">Monitoring OS encryption progress</span></span>
<span data-ttu-id="08abf-764">Il existe trois façons de surveiller la progression du chiffrement du système d’exploitation :</span><span class="sxs-lookup"><span data-stu-id="08abf-764">You can monitor OS encryption progress in three ways:</span></span>

* <span data-ttu-id="08abf-765">Hello d’utilisation `Get-AzureRmVmDiskEncryptionStatus` applet de commande et d’inspecter le champ de ProgressMessage hello :</span><span class="sxs-lookup"><span data-stu-id="08abf-765">Use hello `Get-AzureRmVmDiskEncryptionStatus` cmdlet and inspect hello ProgressMessage field:</span></span>
    ```
    OsVolumeEncrypted          : EncryptionInProgress
    DataVolumesEncrypted       : NotMounted
    OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
    ProgressMessage            : OS disk encryption started
    ```
 <span data-ttu-id="08abf-766">Une fois hello VM atteint « A démarré le chiffrement du disque du système d’exploitation », il prend environ 40 minutes too50 sur un stockage Premium sauvegardé la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="08abf-766">After hello VM reaches "OS disk encryption started," it takes about 40 too50 minutes on a Premium-storage backed VM.</span></span>

 <span data-ttu-id="08abf-767">En raison de [l’erreur #388](https://github.com/Azure/WALinuxAgent/issues/388) dans WALinuxAgent, `OsVolumeEncrypted` et `DataVolumesEncrypted` apparaissent comme `Unknown` dans certaines distributions.</span><span class="sxs-lookup"><span data-stu-id="08abf-767">Because of [issue #388](https://github.com/Azure/WALinuxAgent/issues/388) in WALinuxAgent, `OsVolumeEncrypted` and `DataVolumesEncrypted` show up as `Unknown` in some distributions.</span></span> <span data-ttu-id="08abf-768">Ce problème est résolu automatiquement dans WALinuxAgent version 2.1.5 et ultérieure.</span><span class="sxs-lookup"><span data-stu-id="08abf-768">With WALinuxAgent version 2.1.5 and later, this issue is fixed automatically.</span></span> <span data-ttu-id="08abf-769">Si vous voyez `Unknown` dans le résultat de hello, vous pouvez vérifier l’état de chiffrement de disque à l’aide de l’Explorateur de ressources Azure de hello.</span><span class="sxs-lookup"><span data-stu-id="08abf-769">If you see `Unknown` in hello output, you can verify disk-encryption status by using hello Azure Resource Explorer.</span></span>

 <span data-ttu-id="08abf-770">Accédez trop[Explorateur de ressources Azure](https://resources.azure.com/), puis développez cette hiérarchie dans le volet de sélection hello sur gauche :</span><span class="sxs-lookup"><span data-stu-id="08abf-770">Go too[Azure Resource Explorer](https://resources.azure.com/), and then expand this hierarchy in hello selection panel on left:</span></span>

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

 <span data-ttu-id="08abf-771">Bonjour InstanceView, faites défiler état du chiffrement toosee hello de vos lecteurs.</span><span class="sxs-lookup"><span data-stu-id="08abf-771">In hello InstanceView, scroll down toosee hello encryption status of your drives.</span></span>

 ![Vue d’instance de machine virtuelle](./media/azure-security-disk-encryption/vm-instanceview.png)

* <span data-ttu-id="08abf-773">Recherchez les [diagnostics de démarrage](https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/).</span><span class="sxs-lookup"><span data-stu-id="08abf-773">Look at [boot diagnostics](https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/).</span></span> <span data-ttu-id="08abf-774">Les messages à partir de l’extension de ADE de hello doivent avoir pour préfixe `[AzureDiskEncryption]`.</span><span class="sxs-lookup"><span data-stu-id="08abf-774">Messages from hello ADE extension should be prefixed with `[AzureDiskEncryption]`.</span></span>

* <span data-ttu-id="08abf-775">Connectez-vous à toohello machine virtuelle via SSH, puis obtenir le journal à partir de l’extension hello :</span><span class="sxs-lookup"><span data-stu-id="08abf-775">Sign in toohello VM via SSH, and get hello extension log from:</span></span>

    <span data-ttu-id="08abf-776">/var/log/azure/Microsoft.Azure.Security.AzureDiskEncryptionForLinux</span><span class="sxs-lookup"><span data-stu-id="08abf-776">/var/log/azure/Microsoft.Azure.Security.AzureDiskEncryptionForLinux</span></span>

 <span data-ttu-id="08abf-777">Il est recommandé que vous ne signez pas dans toohello machine virtuelle alors que le chiffrement du système d’exploitation est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="08abf-777">We recommend that you do not sign in toohello VM while OS encryption is in progress.</span></span> <span data-ttu-id="08abf-778">Copier les journaux de hello uniquement lorsque hello deux autres méthodes ont échoué.</span><span class="sxs-lookup"><span data-stu-id="08abf-778">Copy hello logs only when hello other two methods have failed.</span></span>

#### <a name="prepare-a-pre-encrypted-linux-vhd"></a><span data-ttu-id="08abf-779">Préparer un disque dur virtuel Linux déjà chiffré</span><span class="sxs-lookup"><span data-stu-id="08abf-779">Prepare a pre-encrypted Linux VHD</span></span>
##### <a name="ubuntu-16"></a><span data-ttu-id="08abf-780">Ubuntu 16</span><span class="sxs-lookup"><span data-stu-id="08abf-780">Ubuntu 16</span></span>
<span data-ttu-id="08abf-781">Configurer le chiffrement lors de l’installation de distribution hello de manière hello suivante :</span><span class="sxs-lookup"><span data-stu-id="08abf-781">Configure encryption during hello distribution installation by doing hello following:</span></span>

1. <span data-ttu-id="08abf-782">Sélectionnez **configurer des volumes chiffrés** lorsque vous partitionnez les disques hello.</span><span class="sxs-lookup"><span data-stu-id="08abf-782">Select **Configure encrypted volumes** when you partition hello disks.</span></span>

 ![Configuration d’Ubuntu 16.04](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig1.png)

2. <span data-ttu-id="08abf-784">Créez un lecteur de démarrage séparé qui ne doit pas être chiffré.</span><span class="sxs-lookup"><span data-stu-id="08abf-784">Create a separate boot drive, which must not be encrypted.</span></span> <span data-ttu-id="08abf-785">Chiffrez votre lecteur racine.</span><span class="sxs-lookup"><span data-stu-id="08abf-785">Encrypt your root drive.</span></span>

 ![Configuration d’Ubuntu 16.04](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig2.png)

3. <span data-ttu-id="08abf-787">Indiquez une phrase secrète.</span><span class="sxs-lookup"><span data-stu-id="08abf-787">Provide a passphrase.</span></span> <span data-ttu-id="08abf-788">Il s’agit de hello de mot de passe que vous téléchargez toohello coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="08abf-788">This is hello passphrase that you upload toohello key vault.</span></span>

 ![Configuration d’Ubuntu 16.04](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig3.png)

4. <span data-ttu-id="08abf-790">Terminez le partitionnement.</span><span class="sxs-lookup"><span data-stu-id="08abf-790">Finish partitioning.</span></span>

 ![Configuration d’Ubuntu 16.04](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig4.png)

5. <span data-ttu-id="08abf-792">Lorsque vous démarrez hello machine virtuelle et que vous êtes invité à entrer un mot de passe, utilisez hello de mot de passe entré à l’étape 3.</span><span class="sxs-lookup"><span data-stu-id="08abf-792">When you boot hello VM and are asked for a passphrase, use hello passphrase you provided in step 3.</span></span>

 ![Configuration d’Ubuntu 16.04](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig5.png)

6. <span data-ttu-id="08abf-794">Préparer hello machine virtuelle pour le téléchargement dans Azure à l’aide [ces instructions](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-create-upload-ubuntu/).</span><span class="sxs-lookup"><span data-stu-id="08abf-794">Prepare hello VM for uploading into Azure using [these instructions](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-create-upload-ubuntu/).</span></span> <span data-ttu-id="08abf-795">N’exécutez pas encore étape de dernière hello (annulation d’approvisionnement hello machine virtuelle).</span><span class="sxs-lookup"><span data-stu-id="08abf-795">Do not run hello last step (deprovisioning hello VM) yet.</span></span>

<span data-ttu-id="08abf-796">Configurer le chiffrement toowork avec Azure en procédant comme suit de hello :</span><span class="sxs-lookup"><span data-stu-id="08abf-796">Configure encryption toowork with Azure by doing hello following:</span></span>

1. <span data-ttu-id="08abf-797">Créer un fichier sous /usr/local/sbin/azure_crypt_key.sh, avec un contenu hello Bonjour script suivant.</span><span class="sxs-lookup"><span data-stu-id="08abf-797">Create a file under /usr/local/sbin/azure_crypt_key.sh, with hello content in hello following script.</span></span> <span data-ttu-id="08abf-798">Payer une attention toohello KeyFileName, car il est le nom de fichier de mot de passe de hello utilisé par Azure.</span><span class="sxs-lookup"><span data-stu-id="08abf-798">Pay attention toohello KeyFileName, because it is hello passphrase file name used by Azure.</span></span>

    ```
    #!/bin/sh
    MountPoint=/tmp-keydisk-mount
    KeyFileName=LinuxPassPhraseFileName
    echo "Trying tooget hello key from disks ..." >&2
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
        echo "FAILED toofind suitable passphrase file ..." >&2
        echo -n "Try tooenter your password: " >&2
        read -s -r A </dev/console
        echo -n "$A"
     else
        echo "Success loading keyfile!" >&2
    fi
```

2. <span data-ttu-id="08abf-799">Modifier la configuration de chiffrement hello dans *crypttab/etc/*.</span><span class="sxs-lookup"><span data-stu-id="08abf-799">Change hello crypt config in */etc/crypttab*.</span></span> <span data-ttu-id="08abf-800">Il doit se présenter comme suit :</span><span class="sxs-lookup"><span data-stu-id="08abf-800">It should look like this:</span></span>
 ```
    xxx_crypt uuid=xxxxxxxxxxxxxxxxxxxxx none luks,discard,keyscript=/usr/local/sbin/azure_crypt_key.sh
    ```

3. <span data-ttu-id="08abf-801">Si vous modifiez *azure_crypt_key.sh* dans Windows et que vous copié tooLinux, exécutez `dos2unix /usr/local/sbin/azure_crypt_key.sh`.</span><span class="sxs-lookup"><span data-stu-id="08abf-801">If you are editing *azure_crypt_key.sh* in Windows and you copied it tooLinux, run `dos2unix /usr/local/sbin/azure_crypt_key.sh`.</span></span>

4. <span data-ttu-id="08abf-802">Ajoutez les autorisations exécutable toohello script :</span><span class="sxs-lookup"><span data-stu-id="08abf-802">Add executable permissions toohello script:</span></span>
 ```
    chmod +x /usr/local/sbin/azure_crypt_key.sh
 ```
5. <span data-ttu-id="08abf-803">Éditez */etc/initramfs-tools/modules* en ajoutant des lignes :</span><span class="sxs-lookup"><span data-stu-id="08abf-803">Edit */etc/initramfs-tools/modules* by appending lines:</span></span>
 ```
    vfat
    ntfs
    nls_cp437
    nls_utf8
    nls_iso8859-1
```
6. <span data-ttu-id="08abf-804">Exécutez `update-initramfs -u -k all` tooupdate Bonjour initramfs toomake Bonjour `keyscript` prennent effet.</span><span class="sxs-lookup"><span data-stu-id="08abf-804">Run `update-initramfs -u -k all` tooupdate hello initramfs toomake hello `keyscript` take effect.</span></span>

7. <span data-ttu-id="08abf-805">Vous pouvez désormais annuler le déploiement de hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="08abf-805">Now you can deprovision hello VM.</span></span>

 ![Configuration d’Ubuntu 16.04](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig6.png)

8. <span data-ttu-id="08abf-807">Continuer l’étape suivante de toohello et [télécharger votre disque dur virtuel](#upload-encrypted-vhd-to-an-azure-storage-account) dans Azure.</span><span class="sxs-lookup"><span data-stu-id="08abf-807">Continue toohello next step and [upload your VHD](#upload-encrypted-vhd-to-an-azure-storage-account) into Azure.</span></span>

##### <a name="opensuse-132"></a><span data-ttu-id="08abf-808">openSUSE 13.2</span><span class="sxs-lookup"><span data-stu-id="08abf-808">openSUSE 13.2</span></span>
<span data-ttu-id="08abf-809">chiffrement tooconfigure pendant l’installation de distribution de hello, procédez comme hello suivant :</span><span class="sxs-lookup"><span data-stu-id="08abf-809">tooconfigure encryption during hello distribution installation, do hello following:</span></span>
1. <span data-ttu-id="08abf-810">Lorsque vous partitionnez les disques hello, sélectionnez **chiffrer un groupe de volumes**, puis entrez un mot de passe.</span><span class="sxs-lookup"><span data-stu-id="08abf-810">When you partition hello disks, select **Encrypt Volume Group**, and then enter a password.</span></span> <span data-ttu-id="08abf-811">Il s’agit d’un mot de passe hello que vous allez télécharger tooyour coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="08abf-811">This is hello password that you will upload tooyour key vault.</span></span>

 ![Configuration d’openSUSE 13.2](./media/azure-security-disk-encryption/opensuse-encrypt-fig1.png)

2. <span data-ttu-id="08abf-813">Hello machine virtuelle à l’aide de votre mot de passe de démarrage.</span><span class="sxs-lookup"><span data-stu-id="08abf-813">Boot hello VM using your password.</span></span>

 ![Configuration d’openSUSE 13.2](./media/azure-security-disk-encryption/opensuse-encrypt-fig2.png)

3. <span data-ttu-id="08abf-815">Préparation hello machine virtuelle pour le téléchargement tooAzure en suivant les instructions de hello dans [préparer un ordinateur virtuel SLES ou openSUSE Azure](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-suse-create-upload-vhd/#prepare-opensuse-131).</span><span class="sxs-lookup"><span data-stu-id="08abf-815">Prepare hello VM for uploading tooAzure by following hello instructions in [Prepare a SLES or openSUSE virtual machine for Azure](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-suse-create-upload-vhd/#prepare-opensuse-131).</span></span> <span data-ttu-id="08abf-816">N’exécutez pas encore étape de dernière hello (annulation d’approvisionnement hello machine virtuelle).</span><span class="sxs-lookup"><span data-stu-id="08abf-816">Do not run hello last step (deprovisioning hello VM) yet.</span></span>

<span data-ttu-id="08abf-817">toowork de chiffrement tooconfigure avec Azure, procédez comme hello suivant :</span><span class="sxs-lookup"><span data-stu-id="08abf-817">tooconfigure encryption toowork with Azure, do hello following:</span></span>
1. <span data-ttu-id="08abf-818">Modifier hello /etc/dracut.conf et ajoutez hello ligne suivante :</span><span class="sxs-lookup"><span data-stu-id="08abf-818">Edit hello /etc/dracut.conf, and add hello following line:</span></span>
    ```
    add_drivers+=" vfat ntfs nls_cp437 nls_iso8859-1"
    ```
2. <span data-ttu-id="08abf-819">Commentez les lignes en fin de hello Hello du fichier /usr/lib/dracut/modules.d/90crypt/module-setup.sh :</span><span class="sxs-lookup"><span data-stu-id="08abf-819">Comment out these lines by hello end of hello file /usr/lib/dracut/modules.d/90crypt/module-setup.sh:</span></span>
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

3. <span data-ttu-id="08abf-820">Ajouter hello ligne au début de hello de hello fichier /usr/lib/dracut/modules.d/90crypt/parse-crypt.sh suivante :</span><span class="sxs-lookup"><span data-stu-id="08abf-820">Append hello following line at hello beginning of hello file /usr/lib/dracut/modules.d/90crypt/parse-crypt.sh:</span></span>
 ```
    DRACUT_SYSTEMD=0
 ```
<span data-ttu-id="08abf-821">Puis, remplacez toutes les occurrences de :</span><span class="sxs-lookup"><span data-stu-id="08abf-821">And change all occurrences of:</span></span>
 ```
    if [ -z "$DRACUT_SYSTEMD" ]; then
 ```
<span data-ttu-id="08abf-822">to:</span><span class="sxs-lookup"><span data-stu-id="08abf-822">to:</span></span>
```
    if [ 1 ]; then
```
4. <span data-ttu-id="08abf-823">Modifier /usr/lib/dracut/modules.d/90crypt/cryptroot-ask.sh et d’ajouter trop « appareil d’ouvrir LUKS # » :</span><span class="sxs-lookup"><span data-stu-id="08abf-823">Edit /usr/lib/dracut/modules.d/90crypt/cryptroot-ask.sh and append it too“# Open LUKS device”:</span></span>

    ```
    MountPoint=/tmp-keydisk-mount
    KeyFileName=LinuxPassPhraseFileName
    echo "Trying tooget hello key from disks ..." >&2
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
5. <span data-ttu-id="08abf-824">Exécutez `/usr/sbin/dracut -f -v` tooupdate hello initrd.</span><span class="sxs-lookup"><span data-stu-id="08abf-824">Run `/usr/sbin/dracut -f -v` tooupdate hello initrd.</span></span>

6. <span data-ttu-id="08abf-825">Maintenant vous pouvez annuler le déploiement de machine virtuelle hello et [télécharger votre disque dur virtuel](#upload-encrypted-vhd-to-an-azure-storage-account) dans Azure.</span><span class="sxs-lookup"><span data-stu-id="08abf-825">Now you can deprovision hello VM and [upload your VHD](#upload-encrypted-vhd-to-an-azure-storage-account) into Azure.</span></span>

##### <a name="centos-7"></a><span data-ttu-id="08abf-826">CentOS 7</span><span class="sxs-lookup"><span data-stu-id="08abf-826">CentOS 7</span></span>
<span data-ttu-id="08abf-827">chiffrement tooconfigure pendant l’installation de distribution de hello, procédez comme hello suivant :</span><span class="sxs-lookup"><span data-stu-id="08abf-827">tooconfigure encryption during hello distribution installation, do hello following:</span></span>
1. <span data-ttu-id="08abf-828">Sélectionnez **Chiffrer mes données** lors du partitionnement des disques.</span><span class="sxs-lookup"><span data-stu-id="08abf-828">Select **Encrypt my data** when you partition disks.</span></span>

 ![Configuration de centOS 7](./media/azure-security-disk-encryption/centos-encrypt-fig1.png)

2. <span data-ttu-id="08abf-830">Vérifiez que **Chiffrer** est sélectionné pour la partition racine.</span><span class="sxs-lookup"><span data-stu-id="08abf-830">Make sure **Encrypt** is selected for root partition.</span></span>

 ![Configuration de centOS 7](./media/azure-security-disk-encryption/centos-encrypt-fig2.png)

3. <span data-ttu-id="08abf-832">Indiquez une phrase secrète.</span><span class="sxs-lookup"><span data-stu-id="08abf-832">Provide a passphrase.</span></span> <span data-ttu-id="08abf-833">Il s’agit de hello de mot de passe que vous allez télécharger tooyour coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="08abf-833">This is hello passphrase that you will upload tooyour key vault.</span></span>

 ![Configuration de centOS 7](./media/azure-security-disk-encryption/centos-encrypt-fig3.png)

4. <span data-ttu-id="08abf-835">Lorsque vous démarrez hello machine virtuelle et que vous êtes invité à entrer un mot de passe, utilisez hello de mot de passe entré à l’étape 3.</span><span class="sxs-lookup"><span data-stu-id="08abf-835">When you boot hello VM and are asked for a passphrase, use hello passphrase you provided in step 3.</span></span>

 ![Configuration de centOS 7](./media/azure-security-disk-encryption/centos-encrypt-fig4.png)

5. <span data-ttu-id="08abf-837">Préparation hello machine virtuelle pour le téléchargement dans Azure à l’aide des instructions « CentOS 7.0 + » hello [préparer une machine virtuelle CentOS Azure](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-create-upload-centos/#centos-70).</span><span class="sxs-lookup"><span data-stu-id="08abf-837">Prepare hello VM for uploading into Azure by using hello "CentOS 7.0+" instructions in [Prepare a CentOS-based virtual machine for Azure](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-create-upload-centos/#centos-70).</span></span> <span data-ttu-id="08abf-838">N’exécutez pas encore étape de dernière hello (annulation d’approvisionnement hello machine virtuelle).</span><span class="sxs-lookup"><span data-stu-id="08abf-838">Do not run hello last step (deprovisioning hello VM) yet.</span></span>

6. <span data-ttu-id="08abf-839">Maintenant vous pouvez annuler le déploiement de machine virtuelle hello et [télécharger votre disque dur virtuel](#upload-encrypted-vhd-to-an-azure-storage-account) dans Azure.</span><span class="sxs-lookup"><span data-stu-id="08abf-839">Now you can deprovision hello VM and [upload your VHD](#upload-encrypted-vhd-to-an-azure-storage-account) into Azure.</span></span>

<span data-ttu-id="08abf-840">toowork de chiffrement tooconfigure avec Azure, procédez comme hello suivant :</span><span class="sxs-lookup"><span data-stu-id="08abf-840">tooconfigure encryption toowork with Azure, do hello following:</span></span>

1. <span data-ttu-id="08abf-841">Modifier hello /etc/dracut.conf et ajoutez hello ligne suivante :</span><span class="sxs-lookup"><span data-stu-id="08abf-841">Edit hello /etc/dracut.conf, and add hello following line:</span></span>
    ```
    add_drivers+=" vfat ntfs nls_cp437 nls_iso8859-1"
    ```

2. <span data-ttu-id="08abf-842">Commentez les lignes en fin de hello Hello du fichier /usr/lib/dracut/modules.d/90crypt/module-setup.sh :</span><span class="sxs-lookup"><span data-stu-id="08abf-842">Comment out these lines by hello end of hello file /usr/lib/dracut/modules.d/90crypt/module-setup.sh:</span></span>
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

3. <span data-ttu-id="08abf-843">Ajouter hello ligne au début de hello de hello fichier /usr/lib/dracut/modules.d/90crypt/parse-crypt.sh suivante :</span><span class="sxs-lookup"><span data-stu-id="08abf-843">Append hello following line at hello beginning of hello file /usr/lib/dracut/modules.d/90crypt/parse-crypt.sh:</span></span>
```
    DRACUT_SYSTEMD=0
```
<span data-ttu-id="08abf-844">Puis, remplacez toutes les occurrences de :</span><span class="sxs-lookup"><span data-stu-id="08abf-844">And change all occurrences of:</span></span>
```
    if [ -z "$DRACUT_SYSTEMD" ]; then
```
<span data-ttu-id="08abf-845">to</span><span class="sxs-lookup"><span data-stu-id="08abf-845">to</span></span>
```
    if [ 1 ]; then
```
4. <span data-ttu-id="08abf-846">Modifier /usr/lib/dracut/modules.d/90crypt/cryptroot-ask.sh et l’ajouter après hello « appareil d’ouvrir LUKS # » :</span><span class="sxs-lookup"><span data-stu-id="08abf-846">Edit /usr/lib/dracut/modules.d/90crypt/cryptroot-ask.sh and append this after hello “# Open LUKS device”:</span></span>
    ```
    MountPoint=/tmp-keydisk-mount
    KeyFileName=LinuxPassPhraseFileName
    echo "Trying tooget hello key from disks ..." >&2
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
5. <span data-ttu-id="08abf-847">Exécutez hello « / usr/sbin/dracut - f - v « tooupdate hello initrd.</span><span class="sxs-lookup"><span data-stu-id="08abf-847">Run hello “/usr/sbin/dracut -f -v” tooupdate hello initrd.</span></span>

![Configuration de centOS 7](./media/azure-security-disk-encryption/centos-encrypt-fig5.png)

### <a name="upload-encrypted-vhd-tooan-azure-storage-account"></a><span data-ttu-id="08abf-849">Télécharger le compte de stockage Azure tooan disque dur virtuel chiffrée</span><span class="sxs-lookup"><span data-stu-id="08abf-849">Upload encrypted VHD tooan Azure storage account</span></span>
<span data-ttu-id="08abf-850">Après l’activation d’un chiffrement BitLocker ou DM-Crypt, hello local chiffré compte de stockage de disque dur virtuel besoins toobe téléchargé tooyour.</span><span class="sxs-lookup"><span data-stu-id="08abf-850">After BitLocker encryption or DM-Crypt encryption is enabled, hello local encrypted VHD needs toobe uploaded tooyour storage account.</span></span>

    Add-AzureRmVhd [-Destination] <Uri> [-LocalFilePath] <FileInfo> [[-NumberOfUploaderThreads] <Int32> ] [[-BaseImageUriToPatch] <Uri> ] [[-OverWrite]] [ <CommonParameters>]

### <a name="upload-hello-disk-encryption-secret-for-hello-pre-encrypted-vm-tooyour-key-vault"></a><span data-ttu-id="08abf-851">Télécharger la clé secrète de chiffrement de disque hello pour hello déjà chiffrés VM tooyour coffre de clés</span><span class="sxs-lookup"><span data-stu-id="08abf-851">Upload hello disk-encryption secret for hello pre-encrypted VM tooyour key vault</span></span>
<span data-ttu-id="08abf-852">clé secrète de chiffrement de disque de Hello que vous avez obtenu précédemment doit être téléchargé en tant que secret dans votre coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="08abf-852">hello disk-encryption secret that you obtained previously must be uploaded as a secret in your key vault.</span></span> <span data-ttu-id="08abf-853">coffre de clés Hello doit toohave le chiffrement des disques et des autorisations activées pour votre client Azure AD.</span><span class="sxs-lookup"><span data-stu-id="08abf-853">hello key vault needs toohave disk encryption and permissions enabled for your Azure AD client.</span></span>

    $AadClientId = "YourAADClientId"
    $AadClientSecret = "YourAADClientSecret"

    $key vault = New-AzureRmKeyVault -VaultName $KeyVaultName -ResourceGroupName $ResourceGroupName -Location $Location

    Set-AzureRmKeyVaultAccessPolicy -VaultName $KeyVaultName -ResourceGroupName $ResourceGroupName -ServicePrincipalName $AadClientId -PermissionsToKeys all -PermissionsToSecrets all
    Set-AzureRmKeyVaultAccessPolicy -VaultName $KeyVaultName -ResourceGroupName $ResourceGroupName -EnabledForDiskEncryption


#### <a name="disk-encryption-secret-not-encrypted-with-a-kek"></a><span data-ttu-id="08abf-854">La clé secrète de chiffrement de disque non chiffré avec une clé de chiffrement à clé KEK</span><span class="sxs-lookup"><span data-stu-id="08abf-854">Disk encryption secret not encrypted with a KEK</span></span>
<span data-ttu-id="08abf-855">tooset secret hello dans votre coffre de clés, utilisez [Set-AzureKeyVaultSecret](/powershell/module/azurerm.keyvault/set-azurekeyvaultsecret).</span><span class="sxs-lookup"><span data-stu-id="08abf-855">tooset up hello secret in your key vault, use [Set-AzureKeyVaultSecret](/powershell/module/azurerm.keyvault/set-azurekeyvaultsecret).</span></span> <span data-ttu-id="08abf-856">Si vous avez une machine virtuelle Windows, fichier de bek hello est encodé sous forme de chaîne base64 et puis téléchargé tooyour coffre de clés à l’aide de hello `Set-AzureKeyVaultSecret` applet de commande.</span><span class="sxs-lookup"><span data-stu-id="08abf-856">If you have a Windows virtual machine, hello bek file is encoded as a base64 string and then uploaded tooyour key vault using hello `Set-AzureKeyVaultSecret` cmdlet.</span></span> <span data-ttu-id="08abf-857">Pour Linux, mot de passe hello est encodé sous forme de chaîne base64 de puis téléchargé toohello coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="08abf-857">For Linux, hello passphrase is encoded as a base64 string and then uploaded toohello key vault.</span></span> <span data-ttu-id="08abf-858">En outre, assurez-vous que ce hello les étiquettes suivantes sont définies lorsque vous créez un code secret hello hello coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="08abf-858">In addition, make sure that hello following tags are set when you create hello secret in hello key vault.</span></span>

    # This is hello passphrase that was provided for encryption during hello distribution installation
    $passphrase = "contoso-password"

    $tags = @{"DiskEncryptionKeyEncryptionAlgorithm" = "RSA-OAEP"; "DiskEncryptionKeyFileName" = "LinuxPassPhraseFileName"}
    $secretName = [guid]::NewGuid().ToString()
    $secretValue = [Convert]::ToBase64String([System.Text.Encoding]::ASCII.GetBytes($passphrase))
    $secureSecretValue = ConvertTo-SecureString $secretValue -AsPlainText -Force

    $secret = Set-AzureKeyVaultSecret -VaultName $KeyVaultName -Name $secretName -SecretValue $secureSecretValue -tags $tags
    $secretUrl = $secret.Id

<span data-ttu-id="08abf-859">Hello d’utilisation `$secretUrl` à l’étape suivante de hello pour [attachement du disque du système d’exploitation de hello sans utiliser de clés](#without-using-a-kek).</span><span class="sxs-lookup"><span data-stu-id="08abf-859">Use hello `$secretUrl` in hello next step for [attaching hello OS disk without using KEK](#without-using-a-kek).</span></span>

#### <a name="disk-encryption-secret-encrypted-with-a-kek"></a><span data-ttu-id="08abf-860">Disque chiffré avec une clé secrète de chiffrement de disque à clé KEK</span><span class="sxs-lookup"><span data-stu-id="08abf-860">Disk encryption secret encrypted with a KEK</span></span>
<span data-ttu-id="08abf-861">Avant de télécharger le coffre de clés secrètes toohello hello, vous pouvez éventuellement le chiffrer à l’aide d’une clé de chiffrement.</span><span class="sxs-lookup"><span data-stu-id="08abf-861">Before you upload hello secret toohello key vault, you can optionally encrypt it by using a key encryption key.</span></span> <span data-ttu-id="08abf-862">Retour à la ligne hello utilisation [API](https://msdn.microsoft.com/library/azure/dn878066.aspx) toofirst chiffrer secret hello à l’aide de la clé de chiffrement à clé hello.</span><span class="sxs-lookup"><span data-stu-id="08abf-862">Use hello wrap [API](https://msdn.microsoft.com/library/azure/dn878066.aspx) toofirst encrypt hello secret using hello key encryption key.</span></span> <span data-ttu-id="08abf-863">sortie de cette opération de retour à la ligne Hello est une chaîne de URL encodée en base64, ce qui vous pouvez ensuite télécharger en tant que secret à l’aide de hello [ `Set-AzureKeyVaultSecret` ](/powershell/module/azurerm.keyvault/set-azurekeyvaultsecret) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="08abf-863">hello output of this wrap operation is a base64 URL encoded string, which you can then upload as a secret by using hello [`Set-AzureKeyVaultSecret`](/powershell/module/azurerm.keyvault/set-azurekeyvaultsecret) cmdlet.</span></span>

    # This is hello passphrase that was provided for encryption during hello distribution installation
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

<span data-ttu-id="08abf-864">Utilisez `$KeyEncryptionKey` et `$secretUrl` à l’étape suivante de hello pour [attachement du disque hello du système d’exploitation à l’aide de clés](#using-a-kek).</span><span class="sxs-lookup"><span data-stu-id="08abf-864">Use `$KeyEncryptionKey` and `$secretUrl` in hello next step for [attaching hello OS disk using KEK](#using-a-kek).</span></span>

### <a name="specify-a-secret-url-when-you-attach-an-os-disk"></a><span data-ttu-id="08abf-865">Spécifier une URL secrète lorsque vous attachez un lecteur de système d’exploitation</span><span class="sxs-lookup"><span data-stu-id="08abf-865">Specify a secret URL when you attach an OS disk</span></span>
#### <a name="without-using-a-kek"></a><span data-ttu-id="08abf-866">Sans utiliser de clé de chiffrement à clé KEK</span><span class="sxs-lookup"><span data-stu-id="08abf-866">Without using a KEK</span></span>
<span data-ttu-id="08abf-867">Lorsque vous attachez un disque de hello du système d’exploitation, vous devez toopass `$secretUrl`.</span><span class="sxs-lookup"><span data-stu-id="08abf-867">While you are attaching hello OS disk, you need toopass `$secretUrl`.</span></span> <span data-ttu-id="08abf-868">URL de Hello a été générée dans la section « secret de chiffrement de disque non chiffré avec une clés » de hello.</span><span class="sxs-lookup"><span data-stu-id="08abf-868">hello URL was generated in hello "Disk-encryption secret not encrypted with a KEK" section.</span></span>

    Set-AzureRmVMOSDisk `
            -VM $VirtualMachine `
            -Name $OSDiskName `
            -SourceImageUri $VhdUri `
            -VhdUri $OSDiskUri `
            -Linux `
            -CreateOption FromImage `
            -DiskEncryptionKeyVaultId $KeyVault.ResourceId `
            -DiskEncryptionKeyUrl $SecretUrl

#### <a name="using-a-kek"></a><span data-ttu-id="08abf-869">À l’aide d’une clé de chiffrement à clé KEK</span><span class="sxs-lookup"><span data-stu-id="08abf-869">Using a KEK</span></span>
<span data-ttu-id="08abf-870">Lorsque vous attachez le disque de hello du système d’exploitation, passer `$KeyEncryptionKey` et `$secretUrl`.</span><span class="sxs-lookup"><span data-stu-id="08abf-870">When you attach hello OS disk, pass `$KeyEncryptionKey` and `$secretUrl`.</span></span> <span data-ttu-id="08abf-871">URL de Hello a été générée dans la section « secret de chiffrement de disque non chiffré avec une clés » de hello.</span><span class="sxs-lookup"><span data-stu-id="08abf-871">hello URL was generated in hello "Disk-encryption secret not encrypted with a KEK" section.</span></span>

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

## <a name="download-this-guide"></a><span data-ttu-id="08abf-872">Télécharger ce guide</span><span class="sxs-lookup"><span data-stu-id="08abf-872">Download this guide</span></span>
<span data-ttu-id="08abf-873">Vous pouvez télécharger ce guide hello [Galerie TechNet](https://gallery.technet.microsoft.com/Azure-Disk-Encryption-for-a0018eb0).</span><span class="sxs-lookup"><span data-stu-id="08abf-873">You can download this guide from hello [TechNet Gallery](https://gallery.technet.microsoft.com/Azure-Disk-Encryption-for-a0018eb0).</span></span>

## <a name="for-more-information"></a><span data-ttu-id="08abf-874">Pour plus d’informations</span><span class="sxs-lookup"><span data-stu-id="08abf-874">For more information</span></span>
[<span data-ttu-id="08abf-875">Explorer Azure Disk Encryption avec Azure PowerShell - partie 1</span><span class="sxs-lookup"><span data-stu-id="08abf-875">Explore Azure Disk Encryption with Azure PowerShell - Part 1</span></span>](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/16/explore-azure-disk-encryption-with-azure-powershell.aspx?wa=wsignin1.0)  
[<span data-ttu-id="08abf-876">Explorer Azure Disk Encryption avec Azure PowerShell - partie 2</span><span class="sxs-lookup"><span data-stu-id="08abf-876">Explore Azure Disk Encryption with Azure PowerShell - Part 2</span></span>](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx)
