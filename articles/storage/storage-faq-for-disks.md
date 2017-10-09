---
title: Forum aux questions (FAQ) sur les disques de machine virtuelle Azure IaaS | Microsoft Docs
description: "Forum aux questions sur les disques de machines virtuelles et les disques Premium (gérés et non gérés) Azure IaaS"
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: e2a20625-6224-4187-8401-abadc8f1de91
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: robinsh
ms.openlocfilehash: 31d0aa67b6ca58b75b432ae94f93ebcf6d730380
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-about-azure-iaas-vm-disks-and-managed-and-unmanaged-premium-disks"></a><span data-ttu-id="fbb8f-103">Forum aux questions sur les disques de machines virtuelles et les disques Premium gérés et non gérés Azure IaaS</span><span class="sxs-lookup"><span data-stu-id="fbb8f-103">Frequently asked questions about Azure IaaS VM disks and managed and unmanaged premium disks</span></span>

<span data-ttu-id="fbb8f-104">Dans cet article, nous étudierons les questions fréquentes relatives à Azure Managed Disks et Azure Stockage Premium.</span><span class="sxs-lookup"><span data-stu-id="fbb8f-104">This article answers some frequently asked questions about Azure Managed Disks and Azure Premium Storage.</span></span>

## <a name="managed-disks"></a><span data-ttu-id="fbb8f-105">Managed Disks</span><span class="sxs-lookup"><span data-stu-id="fbb8f-105">Managed Disks</span></span>

<span data-ttu-id="fbb8f-106">**Qu’est-ce qu’Azure Managed Disks ?**</span><span class="sxs-lookup"><span data-stu-id="fbb8f-106">**What is Azure Managed Disks?**</span></span>

<span data-ttu-id="fbb8f-107">Managed Disks est une fonctionnalité qui simplifie la gestion des disques associés aux machines virtuelles Azure IaaS en prenant en charge pour vous la gestion des comptes de stockage.</span><span class="sxs-lookup"><span data-stu-id="fbb8f-107">Managed Disks is a feature that simplifies disk management for Azure IaaS VMs by handling storage account management for you.</span></span> <span data-ttu-id="fbb8f-108">Pour plus d’informations, consultez hello [vue d’ensemble de disques gérés](storage-managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="fbb8f-108">For more information, see hello [Managed Disks overview](storage-managed-disks-overview.md).</span></span>

<span data-ttu-id="fbb8f-109">**Si je crée un disque géré standard à partir d’un disque dur virtuel existant de 80 Go, combien cela me coûte-t-il ?**</span><span class="sxs-lookup"><span data-stu-id="fbb8f-109">**If I create a standard managed disk from an existing VHD that's 80 GB, how much will that cost me?**</span></span>

<span data-ttu-id="fbb8f-110">Un disque géré standard créé à partir d’un disque dur virtuel de 80 Go est traité comme taille de disque standard disponible suivant hello, qui est un disque S10.</span><span class="sxs-lookup"><span data-stu-id="fbb8f-110">A standard managed disk created from an 80-GB VHD is treated as hello next available standard disk size, which is an S10 disk.</span></span> <span data-ttu-id="fbb8f-111">Vous êtes facturé en fonction toohello S10 disque tarification.</span><span class="sxs-lookup"><span data-stu-id="fbb8f-111">You're charged according toohello S10 disk pricing.</span></span> <span data-ttu-id="fbb8f-112">Pour plus d’informations, consultez hello [page de tarification](https://azure.microsoft.com/pricing/details/storage).</span><span class="sxs-lookup"><span data-stu-id="fbb8f-112">For more information, see hello [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="fbb8f-113">**Des frais de transaction s’appliquent-ils aux disques gérés Standard ?**</span><span class="sxs-lookup"><span data-stu-id="fbb8f-113">**Are there any transaction costs for standard managed disks?**</span></span>

<span data-ttu-id="fbb8f-114">Oui.</span><span class="sxs-lookup"><span data-stu-id="fbb8f-114">Yes.</span></span> <span data-ttu-id="fbb8f-115">Vous êtes facturé pour chaque transaction.</span><span class="sxs-lookup"><span data-stu-id="fbb8f-115">You're charged for each transaction.</span></span> <span data-ttu-id="fbb8f-116">Pour plus d’informations, consultez hello [page de tarification](https://azure.microsoft.com/pricing/details/storage).</span><span class="sxs-lookup"><span data-stu-id="fbb8f-116">For more information, see hello [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="fbb8f-117">**Pour un disque géré standard, me seront-elles facturées pour hello de taille réelle des données hello sur le disque de hello ou hello configuré capacité de hello disque ?**</span><span class="sxs-lookup"><span data-stu-id="fbb8f-117">**For a standard managed disk, will I be charged for hello actual size of hello data on hello disk or for hello provisioned capacity of hello disk?**</span></span>

<span data-ttu-id="fbb8f-118">Vous êtes facturé en fonction de la capacité de hello mis en service du disque de hello.</span><span class="sxs-lookup"><span data-stu-id="fbb8f-118">You're charged based on hello provisioned capacity of hello disk.</span></span> <span data-ttu-id="fbb8f-119">Pour plus d’informations, consultez hello [page de tarification](https://azure.microsoft.com/pricing/details/storage).</span><span class="sxs-lookup"><span data-stu-id="fbb8f-119">For more information, see hello [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="fbb8f-120">**En quoi la tarification appliquée aux disques gérés Premium est-elle différente de celle associée aux disques non gérés ?**</span><span class="sxs-lookup"><span data-stu-id="fbb8f-120">**How is pricing of premium managed disks different from unmanaged disks?**</span></span>

<span data-ttu-id="fbb8f-121">Hello tarification des disques premium géré est hello identique à celui des disques premium non managé.</span><span class="sxs-lookup"><span data-stu-id="fbb8f-121">hello pricing of premium managed disks is hello same as unmanaged premium disks.</span></span>

<span data-ttu-id="fbb8f-122">**Puis-je modifier hello stockage type de compte (Standard ou Premium) de mes disques gérés ?**</span><span class="sxs-lookup"><span data-stu-id="fbb8f-122">**Can I change hello storage account type (Standard or Premium) of my managed disks?**</span></span>

<span data-ttu-id="fbb8f-123">Oui.</span><span class="sxs-lookup"><span data-stu-id="fbb8f-123">Yes.</span></span> <span data-ttu-id="fbb8f-124">Vous pouvez modifier le type de compte de stockage hello vos disques gérés à l’aide de hello portail Azure, PowerShell ou hello CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="fbb8f-124">You can change hello storage account type of your managed disks by using hello Azure portal, PowerShell, or hello Azure CLI.</span></span>

<span data-ttu-id="fbb8f-125">**Existe-t-il un moyen que je puisse copier ou exporter un compte de stockage privé tooa disque géré ?**</span><span class="sxs-lookup"><span data-stu-id="fbb8f-125">**Is there a way that I can copy or export a managed disk tooa private storage account?**</span></span>

<span data-ttu-id="fbb8f-126">Oui.</span><span class="sxs-lookup"><span data-stu-id="fbb8f-126">Yes.</span></span> <span data-ttu-id="fbb8f-127">Vous pouvez exporter vos disques gérés à l’aide de hello portail Azure, PowerShell ou hello CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="fbb8f-127">You can export your managed disks by using hello Azure portal, PowerShell, or hello Azure CLI.</span></span>

<span data-ttu-id="fbb8f-128">**Puis-je utiliser un fichier de disque dur virtuel dans un toocreate de compte de stockage Azure un disque géré avec un autre abonnement ?**</span><span class="sxs-lookup"><span data-stu-id="fbb8f-128">**Can I use a VHD file in an Azure storage account toocreate a managed disk with a different subscription?**</span></span>

<span data-ttu-id="fbb8f-129">Non.</span><span class="sxs-lookup"><span data-stu-id="fbb8f-129">No.</span></span>

<span data-ttu-id="fbb8f-130">**Puis-je utiliser un fichier de disque dur virtuel dans un toocreate de compte de stockage Azure un disque géré dans une autre région ?**</span><span class="sxs-lookup"><span data-stu-id="fbb8f-130">**Can I use a VHD file in an Azure storage account toocreate a managed disk in a different region?**</span></span>

<span data-ttu-id="fbb8f-131">Non.</span><span class="sxs-lookup"><span data-stu-id="fbb8f-131">No.</span></span>

<span data-ttu-id="fbb8f-132">**Existe-t-il des restrictions de mise à l’échelle pour les clients utilisant des disques gérés ?**</span><span class="sxs-lookup"><span data-stu-id="fbb8f-132">**Are there any scale limitations for customers that use managed disks?**</span></span>

<span data-ttu-id="fbb8f-133">Disques gérés élimine les limites de hello associées aux comptes de stockage.</span><span class="sxs-lookup"><span data-stu-id="fbb8f-133">Managed Disks eliminates hello limits associated with storage accounts.</span></span> <span data-ttu-id="fbb8f-134">Toutefois, nombre de hello de disques gérés par abonnement est limité too2, 000 par défaut.</span><span class="sxs-lookup"><span data-stu-id="fbb8f-134">However, hello number of managed disks per subscription is limited too2,000 by default.</span></span> <span data-ttu-id="fbb8f-135">Vous pouvez appeler tooincrease de prise en charge ce nombre.</span><span class="sxs-lookup"><span data-stu-id="fbb8f-135">You can call support tooincrease this number.</span></span>

<span data-ttu-id="fbb8f-136">**Puis-je prendre une capture instantanée incrémentielle d’un disque géré ?**</span><span class="sxs-lookup"><span data-stu-id="fbb8f-136">**Can I take an incremental snapshot of a managed disk?**</span></span>

<span data-ttu-id="fbb8f-137">Non.</span><span class="sxs-lookup"><span data-stu-id="fbb8f-137">No.</span></span> <span data-ttu-id="fbb8f-138">fonctionnalité de capture instantanée actuelle Hello effectue une copie complète d’un disque géré.</span><span class="sxs-lookup"><span data-stu-id="fbb8f-138">hello current snapshot capability makes a full copy of a managed disk.</span></span> <span data-ttu-id="fbb8f-139">Toutefois, nous avons l’intention toosupport création d’instantanés incrémentiels hello futures.</span><span class="sxs-lookup"><span data-stu-id="fbb8f-139">However, we are planning toosupport incremental snapshots in hello future.</span></span>

<span data-ttu-id="fbb8f-140">**Les machines virtuelles d’un groupe à haute disponibilité peuvent-elles consister en une combinaison de disques gérés et non gérés ?**</span><span class="sxs-lookup"><span data-stu-id="fbb8f-140">**Can VMs in an availability set consist of a combination of managed and unmanaged disks?**</span></span>

<span data-ttu-id="fbb8f-141">Non.</span><span class="sxs-lookup"><span data-stu-id="fbb8f-141">No.</span></span> <span data-ttu-id="fbb8f-142">Hello machines virtuelles dans un ensemble de disponibilité doit utiliser tous les disques ou tous les disques non managés.</span><span class="sxs-lookup"><span data-stu-id="fbb8f-142">hello VMs in an availability set must use either all managed disks or all unmanaged disks.</span></span> <span data-ttu-id="fbb8f-143">Lorsque vous créez un ensemble de disponibilité, vous pouvez choisir le type de disques souhaité toouse.</span><span class="sxs-lookup"><span data-stu-id="fbb8f-143">When you create an availability set, you can choose which type of disks you want toouse.</span></span>

<span data-ttu-id="fbb8f-144">**Est l’option par défaut de disques gérés hello Bonjour portail Azure ?**</span><span class="sxs-lookup"><span data-stu-id="fbb8f-144">**Is Managed Disks hello default option in hello Azure portal?**</span></span>

<span data-ttu-id="fbb8f-145">Pas actuellement, mais il sera fait défaut hello Bonjour futures.</span><span class="sxs-lookup"><span data-stu-id="fbb8f-145">Not currently, but it will become hello default in hello future.</span></span>

<span data-ttu-id="fbb8f-146">**Est-il possible de créer un disque géré vide ?**</span><span class="sxs-lookup"><span data-stu-id="fbb8f-146">**Can I create an empty managed disk?**</span></span>

<span data-ttu-id="fbb8f-147">Oui.</span><span class="sxs-lookup"><span data-stu-id="fbb8f-147">Yes.</span></span> <span data-ttu-id="fbb8f-148">Vous pouvez tout à fait créer un disque vide.</span><span class="sxs-lookup"><span data-stu-id="fbb8f-148">You can create an empty disk.</span></span> <span data-ttu-id="fbb8f-149">Un disque géré peut être créé indépendamment d’une machine virtuelle, par exemple, sans l’attacher tooa machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="fbb8f-149">A managed disk can be created independently of a VM, for example, without attaching it tooa VM.</span></span>

<span data-ttu-id="fbb8f-150">**Quel est le nombre de domaines d’erreur hello pris en charge pour un ensemble de disponibilité qui utilise des disques gérés ?**</span><span class="sxs-lookup"><span data-stu-id="fbb8f-150">**What is hello supported fault domain count for an availability set that uses Managed Disks?**</span></span>

<span data-ttu-id="fbb8f-151">En fonction de la région de hello où se trouve le groupe à haute disponibilité hello qui utilise des disques gérés, le nombre de domaines d’erreur hello pris en charge est 2 ou 3.</span><span class="sxs-lookup"><span data-stu-id="fbb8f-151">Depending on hello region where hello availability set that uses Managed Disks is located, hello supported fault domain count is 2 or 3.</span></span>

<span data-ttu-id="fbb8f-152">**Comment est le compte de stockage standard hello pour configurer des diagnostics ?**</span><span class="sxs-lookup"><span data-stu-id="fbb8f-152">**How is hello standard storage account for diagnostics set up?**</span></span>

<span data-ttu-id="fbb8f-153">Vous configurez un compte de stockage privé pour les diagnostics de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="fbb8f-153">You set up a private storage account for VM diagnostics.</span></span> <span data-ttu-id="fbb8f-154">Bonjour future, nous prévoyons de diagnostics de tooswitch tooManaged ainsi des disques.</span><span class="sxs-lookup"><span data-stu-id="fbb8f-154">In hello future, we plan tooswitch diagnostics tooManaged Disks as well.</span></span>

<span data-ttu-id="fbb8f-155">**Quel type de prise en charge du contrôle d’accès en fonction du rôle est disponible pour Managed Disks ?**</span><span class="sxs-lookup"><span data-stu-id="fbb8f-155">**What kind of Role-Based Access Control support is available for Managed Disks?**</span></span>

<span data-ttu-id="fbb8f-156">Managed Disks prend en charge trois rôles principaux par défaut :</span><span class="sxs-lookup"><span data-stu-id="fbb8f-156">Managed Disks supports three key default roles:</span></span>

* <span data-ttu-id="fbb8f-157">Propriétaire : il dispose d’une liberté totale de gestion et contrôle l’accès</span><span class="sxs-lookup"><span data-stu-id="fbb8f-157">Owner: Can manage everything, including access</span></span>
* <span data-ttu-id="fbb8f-158">Contributeur : il dispose d’une liberté totale de gestion, mais ne contrôle pas l’accès</span><span class="sxs-lookup"><span data-stu-id="fbb8f-158">Contributor: Can manage everything except access</span></span>
* <span data-ttu-id="fbb8f-159">Lecteur : il peut afficher tous les éléments, mais ne peut y apporter de modifications</span><span class="sxs-lookup"><span data-stu-id="fbb8f-159">Reader: Can view everything, but can't make changes</span></span>

<span data-ttu-id="fbb8f-160">**Existe-t-il un moyen que je puisse copier ou exporter un compte de stockage privé tooa disque géré ?**</span><span class="sxs-lookup"><span data-stu-id="fbb8f-160">**Is there a way that I can copy or export a managed disk tooa private storage account?**</span></span>

<span data-ttu-id="fbb8f-161">Vous pouvez obtenir une signature d’accès partagé en lecture seule URI pour hello géré de disque et l’utiliser toocopy hello contenu tooa privé local ou compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="fbb8f-161">You can get a read-only shared access signature URI for hello managed disk and use it toocopy hello contents tooa private storage account or on-premises storage.</span></span>

<span data-ttu-id="fbb8f-162">**Puis-je créer une copie de mon disque géré ?**</span><span class="sxs-lookup"><span data-stu-id="fbb8f-162">**Can I create a copy of my managed disk?**</span></span>

<span data-ttu-id="fbb8f-163">Les clients peuvent prendre un instantané de leurs disques gérés, puis utilisez hello instantané toocreate à un autre disque géré.</span><span class="sxs-lookup"><span data-stu-id="fbb8f-163">Customers can take a snapshot of their managed disks and then use hello snapshot toocreate another managed disk.</span></span>

<span data-ttu-id="fbb8f-164">**Les disques non gérés sont-ils encore pris en charge ?**</span><span class="sxs-lookup"><span data-stu-id="fbb8f-164">**Are unmanaged disks still supported?**</span></span>

<span data-ttu-id="fbb8f-165">Oui.</span><span class="sxs-lookup"><span data-stu-id="fbb8f-165">Yes.</span></span> <span data-ttu-id="fbb8f-166">Nous prenons à la fois en charge les disques gérés et non gérés.</span><span class="sxs-lookup"><span data-stu-id="fbb8f-166">We support unmanaged and managed disks.</span></span> <span data-ttu-id="fbb8f-167">Nous vous recommandons d’utiliser des disques gérés pour les nouvelles charges de travail et de migrer vos disques toomanaged de charges de travail en cours.</span><span class="sxs-lookup"><span data-stu-id="fbb8f-167">We recommend that you use managed disks for new workloads and migrate your current workloads toomanaged disks.</span></span>


<span data-ttu-id="fbb8f-168">**Si vous créez un disque de 128 Go et augmentez hello taille too130 Go, sera être facturé pour la taille du disque suivant hello (512 Go) ?**</span><span class="sxs-lookup"><span data-stu-id="fbb8f-168">**If I create a 128-GB disk and then increase hello size too130 GB, will I be charged for hello next disk size (512 GB)?**</span></span>

<span data-ttu-id="fbb8f-169">Oui.</span><span class="sxs-lookup"><span data-stu-id="fbb8f-169">Yes.</span></span>

<span data-ttu-id="fbb8f-170">**Puis-je créer des disques gérés disposant du stockage localement redondant, géoredondant ou redondant dans une zone ?**</span><span class="sxs-lookup"><span data-stu-id="fbb8f-170">**Can I create locally redundant storage, geo-redundant storage, and zone-redundant storage managed disks?**</span></span>

<span data-ttu-id="fbb8f-171">Actuellement, Azure Managed Disks prend uniquement en charge les disques gérés disposant du stockage localement redondant.</span><span class="sxs-lookup"><span data-stu-id="fbb8f-171">Azure Managed Disks currently supports only locally redundant storage managed disks.</span></span>

<span data-ttu-id="fbb8f-172">**Puis-je réduire la taille de mes disques gérés ?**</span><span class="sxs-lookup"><span data-stu-id="fbb8f-172">**Can I shrink or downsize my managed disks?**</span></span>

<span data-ttu-id="fbb8f-173">Non.</span><span class="sxs-lookup"><span data-stu-id="fbb8f-173">No.</span></span> <span data-ttu-id="fbb8f-174">Cette fonctionnalité n’est pas prise en charge pour l’instant.</span><span class="sxs-lookup"><span data-stu-id="fbb8f-174">This feature is not supported currently.</span></span> 

<span data-ttu-id="fbb8f-175">**Puis-je modifier propriété de nom d’ordinateur hello lorsque spécialisé (Impossible de créer en utilisant l’outil de préparation système hello ou généralisé) d’exploitation du disque du système est utilisée tooprovision une machine virtuelle ?**</span><span class="sxs-lookup"><span data-stu-id="fbb8f-175">**Can I change hello computer name property when a specialized (not created by using hello System Preparation tool or generalized) operating system disk is used tooprovision a VM?**</span></span>

<span data-ttu-id="fbb8f-176">Non.</span><span class="sxs-lookup"><span data-stu-id="fbb8f-176">No.</span></span> <span data-ttu-id="fbb8f-177">Vous ne pouvez pas mettre à jour propriété de nom d’ordinateur hello.</span><span class="sxs-lookup"><span data-stu-id="fbb8f-177">You can't update hello computer name property.</span></span> <span data-ttu-id="fbb8f-178">Hello nouvelle machine virtuelle hérite du parent de hello machine virtuelle, ce qui était le disque de système d’exploitation utilisé toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="fbb8f-178">hello new VM inherits it from hello parent VM, which was used toocreate hello operating system disk.</span></span> 

<span data-ttu-id="fbb8f-179">**Où puis-je trouver exemple Azure Resource Manager modèles toocreate machines virtuelles avec des disques gérés ?**</span><span class="sxs-lookup"><span data-stu-id="fbb8f-179">**Where can I find sample Azure Resource Manager templates toocreate VMs with managed disks?**</span></span>
* [<span data-ttu-id="fbb8f-180">Liste de modèles utilisant des disques gérés</span><span class="sxs-lookup"><span data-stu-id="fbb8f-180">List of templates using Managed Disks</span></span>](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md)
* <span data-ttu-id="fbb8f-181">https://github.com/chagarw/MDPP</span><span class="sxs-lookup"><span data-stu-id="fbb8f-181">https://github.com/chagarw/MDPP</span></span>

## <a name="managed-disks-and-storage-service-encryption"></a><span data-ttu-id="fbb8f-182">Managed Disks et Storage Service Encryption</span><span class="sxs-lookup"><span data-stu-id="fbb8f-182">Managed Disks and Storage Service Encryption</span></span> 

<span data-ttu-id="fbb8f-183">**Azure Storage Encryption est-il activé par défaut lors de la création d’un disque géré ?**</span><span class="sxs-lookup"><span data-stu-id="fbb8f-183">**Is Azure Storage Service Encryption enabled by default when I create a managed disk?**</span></span>

<span data-ttu-id="fbb8f-184">Oui.</span><span class="sxs-lookup"><span data-stu-id="fbb8f-184">Yes.</span></span>

<span data-ttu-id="fbb8f-185">**Qui gère les clés de chiffrement hello ?**</span><span class="sxs-lookup"><span data-stu-id="fbb8f-185">**Who manages hello encryption keys?**</span></span>

<span data-ttu-id="fbb8f-186">Microsoft gère les clés de chiffrement hello.</span><span class="sxs-lookup"><span data-stu-id="fbb8f-186">Microsoft manages hello encryption keys.</span></span>

<span data-ttu-id="fbb8f-187">**Puis-je désactiver Storage Service Encryption pour mes disques gérés ?**</span><span class="sxs-lookup"><span data-stu-id="fbb8f-187">**Can I disable Storage Service Encryption for my managed disks?**</span></span>

<span data-ttu-id="fbb8f-188">Non.</span><span class="sxs-lookup"><span data-stu-id="fbb8f-188">No.</span></span>

<span data-ttu-id="fbb8f-189">**Storage Service Encryption est-il disponible dans toutes les régions ?**</span><span class="sxs-lookup"><span data-stu-id="fbb8f-189">**Is Storage Service Encryption only available in specific regions?**</span></span>

<span data-ttu-id="fbb8f-190">Non.</span><span class="sxs-lookup"><span data-stu-id="fbb8f-190">No.</span></span> <span data-ttu-id="fbb8f-191">Il est disponible dans toutes les régions hello où disques gérés est disponible.</span><span class="sxs-lookup"><span data-stu-id="fbb8f-191">It's available in all hello regions where Managed Disks is available.</span></span> <span data-ttu-id="fbb8f-192">Managed Disks est disponible dans toutes les zones publiques et en Allemagne.</span><span class="sxs-lookup"><span data-stu-id="fbb8f-192">Managed Disks is available in all public regions and Germany.</span></span>

<span data-ttu-id="fbb8f-193">**Comment puis-je savoir si mon disque géré est chiffré ?**</span><span class="sxs-lookup"><span data-stu-id="fbb8f-193">**How can I find out if my managed disk is encrypted?**</span></span>

<span data-ttu-id="fbb8f-194">Vous pouvez trouver des temps hello quand un disque géré a été créé à partir de hello portail Azure, hello CLI d’Azure et PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fbb8f-194">You can find out hello time when a managed disk was created from hello Azure portal, hello Azure CLI, and PowerShell.</span></span> <span data-ttu-id="fbb8f-195">Si hello est après le 9 juin 2017, votre disque est chiffré.</span><span class="sxs-lookup"><span data-stu-id="fbb8f-195">If hello time is after June 9, 2017, then your disk is encrypted.</span></span> 

<span data-ttu-id="fbb8f-196">**Comment puis-je chiffrer mes disques existants qui ont été créés avant le 10 juin 2017 ?**</span><span class="sxs-lookup"><span data-stu-id="fbb8f-196">**How can I encrypt my existing disks that were created before June 10, 2017?**</span></span>

<span data-ttu-id="fbb8f-197">À compter du 10 juin 2017, nouvelles données écrites tooexisting géré disques sont automatiquement chiffrées.</span><span class="sxs-lookup"><span data-stu-id="fbb8f-197">As of June 10, 2017, new data written tooexisting managed disks is automatically encrypted.</span></span> <span data-ttu-id="fbb8f-198">Nous avons également l’intention tooencrypt les données existantes, et le chiffrement hello aura lieu de façon asynchrone en arrière-plan de hello.</span><span class="sxs-lookup"><span data-stu-id="fbb8f-198">We are also planning tooencrypt existing data, and hello encryption will happen asynchronously in hello background.</span></span> <span data-ttu-id="fbb8f-199">Si vous devez chiffrer des données existantes maintenant, créez une copie de votre disque.</span><span class="sxs-lookup"><span data-stu-id="fbb8f-199">If you must encrypt existing data now, create a copy of your disk.</span></span> <span data-ttu-id="fbb8f-200">Les nouveaux disques seront chiffrés.</span><span class="sxs-lookup"><span data-stu-id="fbb8f-200">New disks will be encrypted.</span></span>

* [<span data-ttu-id="fbb8f-201">Copier les disques gérés à l’aide de hello CLI d’Azure</span><span class="sxs-lookup"><span data-stu-id="fbb8f-201">Copy managed disks by using hello Azure CLI</span></span>](https://docs.microsoft.com/en-us/azure/storage/scripts/storage-linux-cli-sample-copy-managed-disks-to-same-or-different-subscription?toc=%2fcli%2fmodule%2ftoc.json)
* [<span data-ttu-id="fbb8f-202">Copier les disques gérés à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="fbb8f-202">Copy managed disks by using PowerShell</span></span>](https://docs.microsoft.com/en-us/azure/storage/scripts/storage-windows-powershell-sample-copy-managed-disks-to-same-or-different-subscription?toc=%2fcli%2fmodule%2ftoc.json)

<span data-ttu-id="fbb8f-203">**Les instantanés et les images gérés sont-ils chiffrés ?**</span><span class="sxs-lookup"><span data-stu-id="fbb8f-203">**Are managed snapshots and images encrypted?**</span></span>

<span data-ttu-id="fbb8f-204">Oui.</span><span class="sxs-lookup"><span data-stu-id="fbb8f-204">Yes.</span></span> <span data-ttu-id="fbb8f-205">Tous les instantanés et les images gérés créés après le 9 juin 2017 sont automatiquement chiffrés.</span><span class="sxs-lookup"><span data-stu-id="fbb8f-205">All managed snapshots and images created after June 9, 2017, are automatically encrypted.</span></span> 

<span data-ttu-id="fbb8f-206">**Puis-je convertir des machines virtuelles avec des disques non managés qui sont trouvent sur des comptes de stockage qui sont ou ont été précédemment chiffrée toomanaged disques ?**</span><span class="sxs-lookup"><span data-stu-id="fbb8f-206">**Can I convert VMs with unmanaged disks that are located on storage accounts that are or were previously encrypted toomanaged disks?**</span></span>

<span data-ttu-id="fbb8f-207">Oui</span><span class="sxs-lookup"><span data-stu-id="fbb8f-207">Yes</span></span>

<span data-ttu-id="fbb8f-208">**Un disque dur virtuel exporté à partir d’un disque géré ou un instantané seront-ils également chiffrés ?**</span><span class="sxs-lookup"><span data-stu-id="fbb8f-208">**Will an exported VHD from a managed disk or a snapshot also be encrypted?**</span></span>

<span data-ttu-id="fbb8f-209">Non.</span><span class="sxs-lookup"><span data-stu-id="fbb8f-209">No.</span></span> <span data-ttu-id="fbb8f-210">Mais si vous exportez un tooan de disque dur virtuel chiffrée compte de stockage d’un disque géré chiffrée ou d’instantané, puis il est chiffré.</span><span class="sxs-lookup"><span data-stu-id="fbb8f-210">But if you export a VHD tooan encrypted storage account from an encrypted managed disk or snapshot, then it's encrypted.</span></span> 

## <a name="premium-disks-managed-and-unmanaged"></a><span data-ttu-id="fbb8f-211">Disques Premium : gérés et non gérés</span><span class="sxs-lookup"><span data-stu-id="fbb8f-211">Premium disks: Managed and unmanaged</span></span>

<span data-ttu-id="fbb8f-212">**Si une machine virtuelle utilise une taille qui prend en charge le stockage Premium, comme DSv2, puis-je joindre des disques de données Standard et Premium ?**</span><span class="sxs-lookup"><span data-stu-id="fbb8f-212">**If a VM uses a size series that supports Premium Storage, such as a DSv2, can I attach both premium and standard data disks?**</span></span> 

<span data-ttu-id="fbb8f-213">Oui.</span><span class="sxs-lookup"><span data-stu-id="fbb8f-213">Yes.</span></span>

<span data-ttu-id="fbb8f-214">**Puis-je attacher premium et la série de taille de tooa de disques de données standard ne prend pas en charge le stockage Premium, série D, Dv2, G ou F ?**</span><span class="sxs-lookup"><span data-stu-id="fbb8f-214">**Can I attach both premium and standard data disks tooa size series that doesn't support Premium Storage, such as D, Dv2, G, or F series?**</span></span>

<span data-ttu-id="fbb8f-215">Non.</span><span class="sxs-lookup"><span data-stu-id="fbb8f-215">No.</span></span> <span data-ttu-id="fbb8f-216">Vous pouvez joindre uniquement les tooVMs de disques de données standard qui n’utilisent pas une série de taille qui prend en charge le stockage Premium.</span><span class="sxs-lookup"><span data-stu-id="fbb8f-216">You can attach only standard data disks tooVMs that don't use a size series that supports Premium Storage.</span></span>

<span data-ttu-id="fbb8f-217">**Si je crée un disque de données Premium à partir d’un disque dur virtuel existant de 80 Go, combien cela me coûte-t-il ?**</span><span class="sxs-lookup"><span data-stu-id="fbb8f-217">**If I create a premium data disk from an existing VHD that was 80 GB, how much will that cost?**</span></span>

<span data-ttu-id="fbb8f-218">Un disque de données premium créé à partir d’un disque dur virtuel de 80 Go est traité comme la taille du disque hello premium disponible suivant, qui est un disque P10.</span><span class="sxs-lookup"><span data-stu-id="fbb8f-218">A premium data disk created from an 80-GB VHD is treated as hello next-available premium disk size, which is a P10 disk.</span></span> <span data-ttu-id="fbb8f-219">Vous êtes facturé en fonction toohello P10 disque tarification.</span><span class="sxs-lookup"><span data-stu-id="fbb8f-219">You're charged according toohello P10 disk pricing.</span></span>

<span data-ttu-id="fbb8f-220">**Existe-t-il des coûts de transaction toouse stockage Premium ?**</span><span class="sxs-lookup"><span data-stu-id="fbb8f-220">**Are there transaction costs toouse Premium Storage?**</span></span>

<span data-ttu-id="fbb8f-221">Il existe un coût fixe pour chaque taille de disque. Il s’ajoute aux limites spécifiques d’E/S par seconde et de débit.</span><span class="sxs-lookup"><span data-stu-id="fbb8f-221">There is a fixed cost for each disk size, which comes provisioned with specific limits on IOPS and throughput.</span></span> <span data-ttu-id="fbb8f-222">Hello autres coûts sont la bande passante sortante et la capacité d’instantané, le cas échéant.</span><span class="sxs-lookup"><span data-stu-id="fbb8f-222">hello other costs are outbound bandwidth and snapshot capacity, if applicable.</span></span> <span data-ttu-id="fbb8f-223">Pour plus d’informations, consultez hello [page de tarification](https://azure.microsoft.com/pricing/details/storage).</span><span class="sxs-lookup"><span data-stu-id="fbb8f-223">For more information, see hello [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="fbb8f-224">**Quelles sont les limites de hello pour e/s et un débit puis-je obtenir à partir du cache de disque hello ?**</span><span class="sxs-lookup"><span data-stu-id="fbb8f-224">**What are hello limits for IOPS and throughput that I can get from hello disk cache?**</span></span>

<span data-ttu-id="fbb8f-225">Hello combiné des limites pour le cache disque SSD local pour une série DS 4 000 IOPS par cœur et et 33 Mo par seconde par cœur.</span><span class="sxs-lookup"><span data-stu-id="fbb8f-225">hello combined limits for cache and local SSD for a DS series are 4,000 IOPS per core and 33 MB per second per core.</span></span> <span data-ttu-id="fbb8f-226">Hello série GS offre 5 000 IOPS par cœur et 50 Mo par seconde par cœur.</span><span class="sxs-lookup"><span data-stu-id="fbb8f-226">hello GS series offers 5,000 IOPS per core and 50 MB per second per core.</span></span>

<span data-ttu-id="fbb8f-227">**Est hello que SSD local pris en charge pour une machine virtuelle de disques gérés ?**</span><span class="sxs-lookup"><span data-stu-id="fbb8f-227">**Is hello local SSD supported for a Managed Disks VM?**</span></span>

<span data-ttu-id="fbb8f-228">Hello SSD local correspond au stockage temporaire qui est inclus dans une machine virtuelle de disques gérés.</span><span class="sxs-lookup"><span data-stu-id="fbb8f-228">hello local SSD is temporary storage that is included with a Managed Disks VM.</span></span> <span data-ttu-id="fbb8f-229">Ce stockage temporaire n’occasionne aucun frais supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="fbb8f-229">There is no extra cost for this temporary storage.</span></span> <span data-ttu-id="fbb8f-230">Nous vous recommandons de ne pas utiliser cette toostore SSD local vos données d’application, car il n’est pas rendu persistant dans le stockage d’objets Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="fbb8f-230">We recommend that you do not use this local SSD toostore your application data because it isn't persisted in Azure Blob storage.</span></span>

<span data-ttu-id="fbb8f-231">**Sont des répercussions sur hello utilisez de découpage sur des disques premium ?**</span><span class="sxs-lookup"><span data-stu-id="fbb8f-231">**Are there any repercussions for hello use of TRIM on premium disks?**</span></span>

<span data-ttu-id="fbb8f-232">Il n’est pas inconvénient toohello de découpage sur disques Azure sur soit premium ou standard.</span><span class="sxs-lookup"><span data-stu-id="fbb8f-232">There is no downside toohello use of TRIM on Azure disks on either premium or standard disks.</span></span>

## <a name="new-disk-sizes-managed-and-unmanaged"></a><span data-ttu-id="fbb8f-233">Nouvelles tailles de disque : gérés et non-gérés</span><span class="sxs-lookup"><span data-stu-id="fbb8f-233">New disk sizes: Managed and unmanaged</span></span>

<span data-ttu-id="fbb8f-234">**Quelle est la plus grande taille de disque hello pris en charge pour le système d’exploitation et des disques de données ?**</span><span class="sxs-lookup"><span data-stu-id="fbb8f-234">**What is hello largest disk size supported for operating system and data disks?**</span></span>

<span data-ttu-id="fbb8f-235">type de partition de Hello Azure prend en charge pour un disque de système d’exploitation est hello MBR master boot record ().</span><span class="sxs-lookup"><span data-stu-id="fbb8f-235">hello partition type that Azure supports for an operating system disk is hello master boot record (MBR).</span></span> <span data-ttu-id="fbb8f-236">Hello MBR prend en charge une taille de disque jusqu'à too2 to.</span><span class="sxs-lookup"><span data-stu-id="fbb8f-236">hello MBR format supports a disk size up too2 TB.</span></span> <span data-ttu-id="fbb8f-237">Hello plus grande taille que Azure prend en charge pour un disque de système d’exploitation est de 2 To.</span><span class="sxs-lookup"><span data-stu-id="fbb8f-237">hello largest size that Azure supports for an operating system disk is 2 TB.</span></span> <span data-ttu-id="fbb8f-238">Azure prend en charge jusqu'à to too4 pour les disques de données.</span><span class="sxs-lookup"><span data-stu-id="fbb8f-238">Azure supports up too4 TB for data disks.</span></span> 

<span data-ttu-id="fbb8f-239">**Qu’est hello plus grand blob taille de page qui est pris en charge ?**</span><span class="sxs-lookup"><span data-stu-id="fbb8f-239">**What is hello largest page blob size that's supported?**</span></span>

<span data-ttu-id="fbb8f-240">Hello plus grand blob taille de page Azure prend en charge est de 8 To (8 191 Go).</span><span class="sxs-lookup"><span data-stu-id="fbb8f-240">hello largest page blob size that Azure supports is 8 TB (8,191 GB).</span></span> <span data-ttu-id="fbb8f-241">Nous ne prennent en charge les objets BLOB de pages plus de 4 To (4 095 Go) attaché tooa machine virtuelle en tant que données ou disques du système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="fbb8f-241">We don't support page blobs larger than 4 TB (4,095 GB) attached tooa VM as data or operating system disks.</span></span>

<span data-ttu-id="fbb8f-242">**Ai-je besoin toouse une nouvelle version de Windows Azure tools toocreate, attacher, redimensionner et télécharger des disques de taille supérieures à 1 to ?**</span><span class="sxs-lookup"><span data-stu-id="fbb8f-242">**Do I need toouse a new version of Azure tools toocreate, attach, resize, and upload disks larger than 1 TB?**</span></span>

<span data-ttu-id="fbb8f-243">Vous n’avez pas besoin tooupgrade votre toocreate outils Azure existant, attacher ou redimensionner des disques de taille supérieures à 1 To.</span><span class="sxs-lookup"><span data-stu-id="fbb8f-243">You don't need tooupgrade your existing Azure tools toocreate, attach, or resize disks larger than 1 TB.</span></span> <span data-ttu-id="fbb8f-244">tooupload de fichiers à partir de votre disque dur virtuel local directement tooAzure comme un objet blob de pages ou d’un disque non managé, vous devez toouse ensembles hello plus récente de l’outil :</span><span class="sxs-lookup"><span data-stu-id="fbb8f-244">tooupload your VHD file from on-premises directly tooAzure as a page blob or unmanaged disk, you need toouse hello latest tool sets:</span></span>

|<span data-ttu-id="fbb8f-245">Outils Azure</span><span class="sxs-lookup"><span data-stu-id="fbb8f-245">Azure tools</span></span>      | <span data-ttu-id="fbb8f-246">Versions prises en charge</span><span class="sxs-lookup"><span data-stu-id="fbb8f-246">Supported versions</span></span>                                |
|-----------------|---------------------------------------------------|
|<span data-ttu-id="fbb8f-247">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="fbb8f-247">Azure PowerShell</span></span> | <span data-ttu-id="fbb8f-248">Numéro de version 4.1.0 : version de juin 2017 ou version ultérieure</span><span class="sxs-lookup"><span data-stu-id="fbb8f-248">Version number 4.1.0: June 2017 release or later</span></span>|
|<span data-ttu-id="fbb8f-249">Azure CLI v1</span><span class="sxs-lookup"><span data-stu-id="fbb8f-249">Azure CLI v1</span></span>     | <span data-ttu-id="fbb8f-250">Numéro de version 0.10.13 : version de mai 2017 ou version ultérieure</span><span class="sxs-lookup"><span data-stu-id="fbb8f-250">Version number 0.10.13: May 2017 release or later</span></span>|
|<span data-ttu-id="fbb8f-251">AzCopy</span><span class="sxs-lookup"><span data-stu-id="fbb8f-251">AzCopy</span></span>           | <span data-ttu-id="fbb8f-252">Numéro de version 6.1.0 : version de juin 2017 ou version ultérieure</span><span class="sxs-lookup"><span data-stu-id="fbb8f-252">Version number 6.1.0: June 2017 release or later</span></span>|

<span data-ttu-id="fbb8f-253">prise en charge Hello v2 de CLI d’Azure et d’Azure Storage Explorer sera bientôt disponible.</span><span class="sxs-lookup"><span data-stu-id="fbb8f-253">hello support for Azure CLI v2 and Azure Storage Explorer is coming soon.</span></span> 

<span data-ttu-id="fbb8f-254">**Les tailles de disque P4 et P6 sont-elles prises en charge pour les disques non gérés ou les objets blob de pages ?**</span><span class="sxs-lookup"><span data-stu-id="fbb8f-254">**Are P4 and P6 disk sizes supported for unmanaged disks or page blobs?**</span></span>

<span data-ttu-id="fbb8f-255">Non.</span><span class="sxs-lookup"><span data-stu-id="fbb8f-255">No.</span></span> <span data-ttu-id="fbb8f-256">Les tailles de disque P4 (32 Go) et P6 (64 Go) sont prises en charge uniquement pour les disques gérés.</span><span class="sxs-lookup"><span data-stu-id="fbb8f-256">P4 (32 GB) and P6 (64 GB) disk sizes are supported only for managed disks.</span></span> <span data-ttu-id="fbb8f-257">La prise en charge des disques non gérés et des objets BLOB de page sera bientôt disponible.</span><span class="sxs-lookup"><span data-stu-id="fbb8f-257">Support for unmanaged disks and page blobs is coming soon.</span></span>

<span data-ttu-id="fbb8f-258">**Si mon premium existant géré disque moins de 64 Go a été créé avant l’activation de disque hello (environ 15 juin 2017), comment est elle facturée ?**</span><span class="sxs-lookup"><span data-stu-id="fbb8f-258">**If my existing premium managed disk less than 64 GB was created before hello small disk was enabled (around June 15, 2017), how is it billed?**</span></span>

<span data-ttu-id="fbb8f-259">Les disques premium petit existants inférieure à 64 Go continuer toobe facturé en fonction toohello P10 avec la tarification.</span><span class="sxs-lookup"><span data-stu-id="fbb8f-259">Existing small premium disks less than 64 GB continue toobe billed according toohello P10 pricing tier.</span></span> 

<span data-ttu-id="fbb8f-260">**Comment puis-je changer de niveau de disque hello des disques premium petit inférieur à 64 Go à partir de P10 tooP4 ou P6 ?**</span><span class="sxs-lookup"><span data-stu-id="fbb8f-260">**How can I switch hello disk tier of small premium disks less than 64 GB from P10 tooP4 or P6?**</span></span>

<span data-ttu-id="fbb8f-261">Vous pouvez prendre un instantané de vos disques de petite et créez ensuite un Bonjour de commutateur tooautomatically disque tooP4 de niveau de tarification ou P6 en fonction de la taille de hello configuré.</span><span class="sxs-lookup"><span data-stu-id="fbb8f-261">You can take a snapshot of your small disks and then create a disk tooautomatically switch hello pricing tier tooP4 or P6 based on hello provisioned size.</span></span> 


## <a name="what-if-my-question-isnt-answered-here"></a><span data-ttu-id="fbb8f-262">Que dois-je faire si je n’ai pas trouvé de réponse à ma question ici ?</span><span class="sxs-lookup"><span data-stu-id="fbb8f-262">What if my question isn't answered here?</span></span>

<span data-ttu-id="fbb8f-263">Si votre question n’est pas répertoriée ici, faites-le-nous savoir et nous vous aiderons à trouver une réponse.</span><span class="sxs-lookup"><span data-stu-id="fbb8f-263">If your question isn't listed here, let us know and we'll help you find an answer.</span></span> <span data-ttu-id="fbb8f-264">Vous pouvez poser une question à fin hello de cet article dans les commentaires de hello.</span><span class="sxs-lookup"><span data-stu-id="fbb8f-264">You can post a question at hello end of this article in hello comments.</span></span> <span data-ttu-id="fbb8f-265">tooengage avec l’équipe du stockage Azure hello et autres membres de la Communauté sur cet article, utilisez hello MSDN [forum Azure Storage](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata).</span><span class="sxs-lookup"><span data-stu-id="fbb8f-265">tooengage with hello Azure Storage team and other community members about this article, use hello MSDN [Azure Storage forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata).</span></span>

<span data-ttu-id="fbb8f-266">toorequest fonctionnalités, envoyez votre toohello demandes et idées [forum de commentaires de stockage Azure](https://feedback.azure.com/forums/217298-storage).</span><span class="sxs-lookup"><span data-stu-id="fbb8f-266">toorequest features, submit your requests and ideas toohello [Azure Storage feedback forum](https://feedback.azure.com/forums/217298-storage).</span></span>
