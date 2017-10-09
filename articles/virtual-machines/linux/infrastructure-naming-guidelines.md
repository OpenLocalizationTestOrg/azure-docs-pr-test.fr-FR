---
title: infrastructure aaaAzure affectation de noms-Linux | Documents Microsoft
description: "Découvrez hello clé conception et implémentation des recommandations pour l’affectation de noms dans les services d’infrastructure Azure."
documentationcenter: 
services: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 18ee4fb1-8297-49a1-8d3f-097880be67c7
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 333146e7b2071e43527a5d7dc2ec02ebfb316eb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-infrastructure-naming-guidelines-for-linux-vms"></a><span data-ttu-id="154da-103">Instructions de dénomination d’infrastructure Azure pour machines virtuelles Linux</span><span class="sxs-lookup"><span data-stu-id="154da-103">Azure infrastructure naming guidelines for Linux VMs</span></span> 

[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-intro](../../../includes/virtual-machines-linux-infrastructure-guidelines-intro.md)]

<span data-ttu-id="154da-104">Cet article se concentre sur comment tooapproach les conventions d’affectation de noms pour tous les votre toobuild de ressources Azure différents logique et facilement identifiable définir des ressources dans votre environnement.</span><span class="sxs-lookup"><span data-stu-id="154da-104">This article focuses on understanding how tooapproach naming conventions for all your various Azure resources toobuild a logical and easily identifiable set of resources across your environment.</span></span>

## <a name="implementation-guidelines-for-naming-conventions"></a><span data-ttu-id="154da-105">Instructions d’implémentation pour les conventions d’affectation de noms</span><span class="sxs-lookup"><span data-stu-id="154da-105">Implementation guidelines for naming conventions</span></span>
<span data-ttu-id="154da-106">Décisions :</span><span class="sxs-lookup"><span data-stu-id="154da-106">Decisions:</span></span>

* <span data-ttu-id="154da-107">Quelles sont vos conventions d’affectation de noms pour les ressources Azure ?</span><span class="sxs-lookup"><span data-stu-id="154da-107">What are your naming conventions for Azure resources?</span></span>

<span data-ttu-id="154da-108">Tâches :</span><span class="sxs-lookup"><span data-stu-id="154da-108">Tasks:</span></span>

* <span data-ttu-id="154da-109">Définir un hello affixes toouse dans votre cohérence toomaintain de ressources.</span><span class="sxs-lookup"><span data-stu-id="154da-109">Define hello affixes toouse across your resources toomaintain consistency.</span></span>
* <span data-ttu-id="154da-110">Définir le compte de stockage noms hello requis pour les toobe global unique.</span><span class="sxs-lookup"><span data-stu-id="154da-110">Define storage account names given hello requirement for them toobe globally unique.</span></span>
* <span data-ttu-id="154da-111">Hello document toobe de convention d’affectation de noms utilisé et distribuer tooall parties impliquées tooensure cohérence entre des déploiements.</span><span class="sxs-lookup"><span data-stu-id="154da-111">Document hello naming convention toobe used and distribute tooall parties involved tooensure consistency across deployments.</span></span>

## <a name="naming-conventions"></a><span data-ttu-id="154da-112">Conventions d’affectation de noms</span><span class="sxs-lookup"><span data-stu-id="154da-112">Naming conventions</span></span>
<span data-ttu-id="154da-113">Vous devez avoir une convention d’affectation de noms adaptée avant tout processus de création dans Azure.</span><span class="sxs-lookup"><span data-stu-id="154da-113">You should have a good naming convention in place before creating anything in Azure.</span></span> <span data-ttu-id="154da-114">Une convention d’affectation de noms garantit que toutes les ressources hello ont un nom prévisible, ce qui vous aide à faible charge administrative hello associée à la gestion de ces ressources.</span><span class="sxs-lookup"><span data-stu-id="154da-114">A naming convention ensures that all hello resources have a predictable name, which helps lower hello administrative burden associated with managing those resources.</span></span>

<span data-ttu-id="154da-115">Vous pouvez choisir toofollow un ensemble spécifique de conventions d’affectation de noms définies pour votre organisation ou un abonnement Azure spécifique ou un compte.</span><span class="sxs-lookup"><span data-stu-id="154da-115">You might choose toofollow a specific set of naming conventions defined for your entire organization or for a specific Azure subscription or account.</span></span> <span data-ttu-id="154da-116">Bien qu’il soit facile pour les personnes au sein des organisations tooestablish règles implicites en règles lorsque vous travaillez avec des ressources Azure, vous devez tooscale en mesure de toobe pour les équipes qui travaillent ensemble dans Azure.</span><span class="sxs-lookup"><span data-stu-id="154da-116">Although it is easy for individuals within organizations tooestablish implicit rules when working with Azure resources, you need toobe able tooscale for teams working together in Azure.</span></span>

<span data-ttu-id="154da-117">Convenez d’un ensemble de conventions d’affectation de noms en amont.</span><span class="sxs-lookup"><span data-stu-id="154da-117">Agree on a set of naming conventions up front.</span></span> <span data-ttu-id="154da-118">Certains facteurs sont à prendre en compte pour l’ensemble des règles de dénomination.</span><span class="sxs-lookup"><span data-stu-id="154da-118">There are some considerations regarding naming conventions that cut across that sets of rules.</span></span>

## <a name="affixes"></a><span data-ttu-id="154da-119">Affixes</span><span class="sxs-lookup"><span data-stu-id="154da-119">Affixes</span></span>
<span data-ttu-id="154da-120">Lorsque vous cherchez toodefine une convention d’affectation de noms, une décision est si apposer de hello est :</span><span class="sxs-lookup"><span data-stu-id="154da-120">As you look toodefine a naming convention, one decision is whether hello affix is at:</span></span>

* <span data-ttu-id="154da-121">début de Hello du nom de hello (préfixe)</span><span class="sxs-lookup"><span data-stu-id="154da-121">hello beginning of hello name (prefix)</span></span>
* <span data-ttu-id="154da-122">fin de Hello du nom de hello (suffixe)</span><span class="sxs-lookup"><span data-stu-id="154da-122">hello end of hello name (suffix)</span></span>

<span data-ttu-id="154da-123">Par exemple, voici les deux noms possibles pour un groupe de ressources à l’aide de hello `rg` apposer :</span><span class="sxs-lookup"><span data-stu-id="154da-123">For instance, here are two possible names for a Resource Group using hello `rg` affix:</span></span>

* <span data-ttu-id="154da-124">Rg-WebApp (préfixe)</span><span class="sxs-lookup"><span data-stu-id="154da-124">Rg-WebApp (prefix)</span></span>
* <span data-ttu-id="154da-125">WebApp-Rg (suffixe)</span><span class="sxs-lookup"><span data-stu-id="154da-125">WebApp-Rg (suffix)</span></span>

<span data-ttu-id="154da-126">Affixes peuvent faire référence à des aspects toodifferent qui décrivent les ressources hello.</span><span class="sxs-lookup"><span data-stu-id="154da-126">Affixes can refer toodifferent aspects that describe hello particular resources.</span></span> <span data-ttu-id="154da-127">Hello tableau suivant présente des exemples en général utilisés.</span><span class="sxs-lookup"><span data-stu-id="154da-127">hello following table shows some examples typically used.</span></span>

| <span data-ttu-id="154da-128">Aspect</span><span class="sxs-lookup"><span data-stu-id="154da-128">Aspect</span></span> | <span data-ttu-id="154da-129">Exemples</span><span class="sxs-lookup"><span data-stu-id="154da-129">Examples</span></span> | <span data-ttu-id="154da-130">Remarques</span><span class="sxs-lookup"><span data-stu-id="154da-130">Notes</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="154da-131">Environnement</span><span class="sxs-lookup"><span data-stu-id="154da-131">Environment</span></span> |<span data-ttu-id="154da-132">dev, stg, prod</span><span class="sxs-lookup"><span data-stu-id="154da-132">dev, stg, prod</span></span> |<span data-ttu-id="154da-133">Selon l’objectif de hello et le nom de chaque environnement.</span><span class="sxs-lookup"><span data-stu-id="154da-133">Depending on hello purpose and name of each environment.</span></span> |
| <span data-ttu-id="154da-134">Lieu</span><span class="sxs-lookup"><span data-stu-id="154da-134">Location</span></span> |<span data-ttu-id="154da-135">usw (West US), use (East US 2)</span><span class="sxs-lookup"><span data-stu-id="154da-135">usw (West US), use (East US 2)</span></span> |<span data-ttu-id="154da-136">En fonction de la région de hello du centre de données hello ou une région de hello d’organisation de hello.</span><span class="sxs-lookup"><span data-stu-id="154da-136">Depending on hello region of hello datacenter or hello region of hello organization.</span></span> |
| <span data-ttu-id="154da-137">Composant, service ou produit Azure</span><span class="sxs-lookup"><span data-stu-id="154da-137">Azure component, service, or product</span></span> |<span data-ttu-id="154da-138">Rg pour groupe de ressources, VNet pour réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="154da-138">Rg for resource group, VNet for virtual network</span></span> |<span data-ttu-id="154da-139">En fonction du produit hello pour le hello ressource fournit la prise en charge.</span><span class="sxs-lookup"><span data-stu-id="154da-139">Depending on hello product for which hello resource provides support.</span></span> |
| <span data-ttu-id="154da-140">Rôle</span><span class="sxs-lookup"><span data-stu-id="154da-140">Role</span></span> |<span data-ttu-id="154da-141">base de données, application, web</span><span class="sxs-lookup"><span data-stu-id="154da-141">db, app, web</span></span> |<span data-ttu-id="154da-142">En fonction du rôle hello de machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="154da-142">Depending on hello role of hello virtual machine.</span></span> |
| <span data-ttu-id="154da-143">Instance</span><span class="sxs-lookup"><span data-stu-id="154da-143">Instance</span></span> |<span data-ttu-id="154da-144">01, 02, 03, etc.</span><span class="sxs-lookup"><span data-stu-id="154da-144">01, 02, 03, etc.</span></span> |<span data-ttu-id="154da-145">Pour les ressources possédant plusieurs instances.</span><span class="sxs-lookup"><span data-stu-id="154da-145">For resources that have more than one instance.</span></span> <span data-ttu-id="154da-146">Par exemple, des serveurs Web à charge équilibrée dans un service cloud.</span><span class="sxs-lookup"><span data-stu-id="154da-146">For example, load balanced web servers in a cloud service.</span></span> |

<span data-ttu-id="154da-147">Lors de l’établissement des conventions d’affectation de noms, assurez-vous qu’ils clairement l’état qui effectue toouse pour chaque type de ressource et dans quelle position (suffixe vs de préfixe).</span><span class="sxs-lookup"><span data-stu-id="154da-147">When establishing your naming conventions, make sure that they clearly state which affixes toouse for each type of resource, and in which position (prefix vs suffix).</span></span>

## <a name="dates"></a><span data-ttu-id="154da-148">Dates</span><span class="sxs-lookup"><span data-stu-id="154da-148">Dates</span></span>
<span data-ttu-id="154da-149">Il est souvent important toodetermine hello date de création du nom de hello d’une ressource.</span><span class="sxs-lookup"><span data-stu-id="154da-149">It is often important toodetermine hello date of creation from hello name of a resource.</span></span> <span data-ttu-id="154da-150">Nous vous recommandons de format de date AAAAMMJJ hello.</span><span class="sxs-lookup"><span data-stu-id="154da-150">We recommend hello YYYYMMDD date format.</span></span> <span data-ttu-id="154da-151">Ce format garantit non seulement hello complète date est enregistrée, mais également que deux ressources dont les noms diffèrent uniquement sur la date de hello sont triés par ordre alphabétique, dans l’ordre chronologique.</span><span class="sxs-lookup"><span data-stu-id="154da-151">This format ensures that not only is hello full date is recorded, but also that two resources whose names differ only on hello date are sorted alphabetically and chronologically.</span></span>

## <a name="naming-resources"></a><span data-ttu-id="154da-152">Ressources d’affectation de noms</span><span class="sxs-lookup"><span data-stu-id="154da-152">Naming resources</span></span>
<span data-ttu-id="154da-153">Définissez chaque type de ressource dans la convention d’affectation de noms de hello, qui doit avoir des règles qui définissent comment tooassign noms tooeach ressource qui est créé.</span><span class="sxs-lookup"><span data-stu-id="154da-153">Define each type of resource in hello naming convention, which should have rules that define how tooassign names tooeach resource that is created.</span></span> <span data-ttu-id="154da-154">Ces règles doivent s’appliquer tooall des types de ressources, par exemple :</span><span class="sxs-lookup"><span data-stu-id="154da-154">These rules should apply tooall types of resources, for example:</span></span>

* <span data-ttu-id="154da-155">Abonnements</span><span class="sxs-lookup"><span data-stu-id="154da-155">Subscriptions</span></span>
* <span data-ttu-id="154da-156">Comptes</span><span class="sxs-lookup"><span data-stu-id="154da-156">Accounts</span></span>
* <span data-ttu-id="154da-157">Comptes de stockage</span><span class="sxs-lookup"><span data-stu-id="154da-157">Storage accounts</span></span>
* <span data-ttu-id="154da-158">Réseaux virtuels</span><span class="sxs-lookup"><span data-stu-id="154da-158">Virtual networks</span></span>
* <span data-ttu-id="154da-159">Sous-réseaux</span><span class="sxs-lookup"><span data-stu-id="154da-159">Subnets</span></span>
* <span data-ttu-id="154da-160">Groupes à haute disponibilité</span><span class="sxs-lookup"><span data-stu-id="154da-160">Availability sets</span></span>
* <span data-ttu-id="154da-161">Groupes de ressources</span><span class="sxs-lookup"><span data-stu-id="154da-161">Resource groups</span></span>
* <span data-ttu-id="154da-162">Machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="154da-162">Virtual machines</span></span>
* <span data-ttu-id="154da-163">Points de terminaison</span><span class="sxs-lookup"><span data-stu-id="154da-163">Endpoints</span></span>
* <span data-ttu-id="154da-164">groupes de sécurité réseau ;</span><span class="sxs-lookup"><span data-stu-id="154da-164">Network security groups</span></span>
* <span data-ttu-id="154da-165">contrôleur</span><span class="sxs-lookup"><span data-stu-id="154da-165">Roles</span></span>

<span data-ttu-id="154da-166">tooensure qui hello nom fournit suffisamment ressource toowhich de toodetermine informations qu'elle fait référence, vous devez utiliser des noms descriptifs.</span><span class="sxs-lookup"><span data-stu-id="154da-166">tooensure that hello name provides enough information toodetermine toowhich resource it refers, you should use descriptive names.</span></span>

## <a name="computer-names"></a><span data-ttu-id="154da-167">Noms des ordinateurs</span><span class="sxs-lookup"><span data-stu-id="154da-167">Computer names</span></span>
<span data-ttu-id="154da-168">Lorsque vous créez un ordinateur virtuel (VM), Azure nécessite un nom ordinateur virtuel de caractères en too64 qui est utilisé pour le nom de la ressource hello.</span><span class="sxs-lookup"><span data-stu-id="154da-168">When you create a virtual machine (VM), Azure requires a VM name of up too64 characters that is used for hello resource name.</span></span> <span data-ttu-id="154da-169">Azure utilise hello même nom pour le système d’exploitation hello Bonjour machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="154da-169">Azure uses hello same name for hello operating system installed in hello VM.</span></span> <span data-ttu-id="154da-170">Toutefois, ces noms ne peuvent pas toujours être hello même.</span><span class="sxs-lookup"><span data-stu-id="154da-170">However, these names might not always be hello same.</span></span>

<span data-ttu-id="154da-171">Si un ordinateur virtuel est créé à partir d’un fichier d’image de disque dur virtuel qui contient déjà un système d’exploitation, nom d’ordinateur virtuel hello dans Azure peut différer hello nom d’ordinateur de système d’exploitation de l’ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="154da-171">If a VM is created from a .vhd image file that already contains an operating system, hello VM name in Azure can differ from hello VM's operating system computer name.</span></span> <span data-ttu-id="154da-172">Cette situation peut ajouter un degré de gestion tooVM des difficultés, nous ne recommandons par conséquent pas.</span><span class="sxs-lookup"><span data-stu-id="154da-172">This situation can add a degree of difficulty tooVM management, which we therefore do not recommend.</span></span> <span data-ttu-id="154da-173">Affecter hello hello de ressource de machine virtuelle Azure même nom en tant que nom de l’ordinateur hello que vous attribuez le système d’exploitation de toohello de cette machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="154da-173">Assign hello Azure VM resource hello same name as hello computer name that you assign toohello operating system of that VM.</span></span>

<span data-ttu-id="154da-174">Nous vous recommandons de ce nom de machine virtuelle Azure hello est hello identique hello sous-jacent du nom d’ordinateur de système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="154da-174">We recommend that hello Azure VM name is hello same as hello underlying operating system computer name.</span></span>

## <a name="storage-account-names"></a><span data-ttu-id="154da-175">Noms des comptes de stockage</span><span class="sxs-lookup"><span data-stu-id="154da-175">Storage account names</span></span>
<span data-ttu-id="154da-176">Cette section ne s’applique pas trop[disques gérés d’Azure](../../storage/storage-managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), comme vous ne créez pas un compte de stockage distinct.</span><span class="sxs-lookup"><span data-stu-id="154da-176">This section does not apply too[Azure Managed Disks](../../storage/storage-managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), as you do not create a separate storage account.</span></span> <span data-ttu-id="154da-177">Pour les disques non managés, la dénomination des comptes de stockage est régie par des règles spécifiques.</span><span class="sxs-lookup"><span data-stu-id="154da-177">For unmanaged disks, storage accounts have special rules governing their names.</span></span> <span data-ttu-id="154da-178">Vous ne pouvez utiliser que des lettres minuscules et des chiffres.</span><span class="sxs-lookup"><span data-stu-id="154da-178">You can only use lowercase letters and numbers.</span></span> <span data-ttu-id="154da-179">Pour plus d’informations, consultez la rubrique [Création d’un compte de stockage](../../storage/storage-create-storage-account.md#create-a-storage-account) .</span><span class="sxs-lookup"><span data-stu-id="154da-179">For more information, see [Create a storage account](../../storage/storage-create-storage-account.md#create-a-storage-account).</span></span> <span data-ttu-id="154da-180">En outre, le nom du compte de stockage hello, avec core.windows.net, doit être un nom DNS valide globalement unique.</span><span class="sxs-lookup"><span data-stu-id="154da-180">Additionally, hello storage account name, with core.windows.net, should be a globally valid, unique DNS name.</span></span> <span data-ttu-id="154da-181">Par exemple, si le compte de stockage hello est appelée mystorageaccount, hello résultant de noms DNS suivants doivent être uniques :</span><span class="sxs-lookup"><span data-stu-id="154da-181">For instance, if hello storage account is called mystorageaccount, hello following resulting DNS names should be unique:</span></span>

* <span data-ttu-id="154da-182">mystorageaccount.blob.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="154da-182">mystorageaccount.blob.core.windows.net</span></span>
* <span data-ttu-id="154da-183">mystorageaccount.table.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="154da-183">mystorageaccount.table.core.windows.net</span></span>
* <span data-ttu-id="154da-184">mystorageaccount.queue.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="154da-184">mystorageaccount.queue.core.windows.net</span></span>

## <a name="next-steps"></a><span data-ttu-id="154da-185">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="154da-185">Next steps</span></span>
[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-linux-infrastructure-guidelines-next-steps.md)]

