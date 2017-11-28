---
title: "Instructions de dénomination d’infrastructure Azure - Windows | Microsoft Docs"
description: "Découvrez-en plus sur les principales instructions de conception et d’implémentation pour la dénomination dans des services d’infrastructure Azure."
documentationcenter: 
services: virtual-machines-windows
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 660765fa-4d42-49cb-a9c6-8c596d26d221
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 70a595d5c2f0316b5214af7b8939f1af8da187ff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-infrastructure-naming-guidelines-for-windows-vms"></a><span data-ttu-id="41931-103">Instructions de dénomination d’infrastructure Azure pour machines virtuelles Windows</span><span class="sxs-lookup"><span data-stu-id="41931-103">Azure infrastructure naming guidelines for Windows VMs</span></span>

[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-intro](../../../includes/virtual-machines-windows-infrastructure-guidelines-intro.md)]

<span data-ttu-id="41931-104">Cet article se concentre sur la compréhension de l’approche des conventions de dénomination de vos diverses ressources Azure afin de créer un ensemble de ressources logique et facilement identifiable au sein de votre environnement.</span><span class="sxs-lookup"><span data-stu-id="41931-104">This article focuses on understanding how to approach naming conventions for all your various Azure resources to build a logical and easily identifiable set of resources across your environment.</span></span>

## <a name="implementation-guidelines-for-naming-conventions"></a><span data-ttu-id="41931-105">Instructions d’implémentation pour les conventions d’affectation de noms</span><span class="sxs-lookup"><span data-stu-id="41931-105">Implementation guidelines for naming conventions</span></span>
<span data-ttu-id="41931-106">Décisions :</span><span class="sxs-lookup"><span data-stu-id="41931-106">Decisions:</span></span>

* <span data-ttu-id="41931-107">Quelles sont vos conventions d’affectation de noms pour les ressources Azure ?</span><span class="sxs-lookup"><span data-stu-id="41931-107">What are your naming conventions for Azure resources?</span></span>

<span data-ttu-id="41931-108">Tâches :</span><span class="sxs-lookup"><span data-stu-id="41931-108">Tasks:</span></span>

* <span data-ttu-id="41931-109">Définissez les affixes à utiliser parmi vos ressources pour assurer la cohérence.</span><span class="sxs-lookup"><span data-stu-id="41931-109">Define the affixes to use across your resources to maintain consistency.</span></span>
* <span data-ttu-id="41931-110">Définissez des noms de compte de stockage devant être globalement uniques.</span><span class="sxs-lookup"><span data-stu-id="41931-110">Define storage account names given the requirement for them to be globally unique.</span></span>
* <span data-ttu-id="41931-111">Documentez la convention de dénomination à utiliser et à distribuer à toutes les parties impliquées pour assurer la conformité à travers les déploiements.</span><span class="sxs-lookup"><span data-stu-id="41931-111">Document the naming convention to be used and distribute to all parties involved to ensure consistency across deployments.</span></span>

## <a name="naming-conventions"></a><span data-ttu-id="41931-112">Conventions d’affectation de noms</span><span class="sxs-lookup"><span data-stu-id="41931-112">Naming conventions</span></span>
<span data-ttu-id="41931-113">Vous devez avoir une convention d’affectation de noms adaptée avant tout processus de création dans Azure.</span><span class="sxs-lookup"><span data-stu-id="41931-113">You should have a good naming convention in place before creating anything in Azure.</span></span> <span data-ttu-id="41931-114">Une convention d’affectation de noms garantit que toutes les ressources ont un nom prévisible, afin de réduire la charge administrative associée à leur gestion.</span><span class="sxs-lookup"><span data-stu-id="41931-114">A naming convention ensures that all the resources have a predictable name, which helps lower the administrative burden associated with managing those resources.</span></span>

<span data-ttu-id="41931-115">Vous pouvez choisir de suivre un ensemble spécifique de conventions d’affectation de noms définies pour votre organisation, ou pour un compte ou abonnement Azure spécifique.</span><span class="sxs-lookup"><span data-stu-id="41931-115">You might choose to follow a specific set of naming conventions defined for your entire organization or for a specific Azure subscription or account.</span></span> <span data-ttu-id="41931-116">Bien qu’il soit facile d’établir des règles implicites au sein d’entreprises lorsque vous travaillez avec des ressources Azure, ce modèle n’est pas très souple lorsqu’une équipe doit travailler sur un projet sur Azure.</span><span class="sxs-lookup"><span data-stu-id="41931-116">Although it is easy for individuals within organizations to establish implicit rules when working with Azure resources, when a team needs to work on a project on Azure, that model does not scale well.</span></span>

<span data-ttu-id="41931-117">Convenez d’un ensemble de conventions d’affectation de noms en amont.</span><span class="sxs-lookup"><span data-stu-id="41931-117">Agree on a set of naming conventions up front.</span></span> <span data-ttu-id="41931-118">Certains facteurs sont à prendre en compte pour cet ensemble de règles de dénomination.</span><span class="sxs-lookup"><span data-stu-id="41931-118">There are some considerations regarding naming conventions that cut across this set of rules.</span></span>

## <a name="affixes"></a><span data-ttu-id="41931-119">Affixes</span><span class="sxs-lookup"><span data-stu-id="41931-119">Affixes</span></span>
<span data-ttu-id="41931-120">Lorsque vous cherchez à définir une convention de dénomination, vous devez décider de l’emplacement de l’affixe :</span><span class="sxs-lookup"><span data-stu-id="41931-120">As you look to define a naming convention, one decision comes whether the affix is at:</span></span>

* <span data-ttu-id="41931-121">au début du nom (préfixe)</span><span class="sxs-lookup"><span data-stu-id="41931-121">The beginning of the name (prefix)</span></span>
* <span data-ttu-id="41931-122">à la fin du nom (suffixe)</span><span class="sxs-lookup"><span data-stu-id="41931-122">The end of the name (suffix)</span></span>

<span data-ttu-id="41931-123">Voici deux exemples de noms possibles pour un groupe de ressources avec l’affixe `rg` :</span><span class="sxs-lookup"><span data-stu-id="41931-123">For instance, here are two possible names for a Resource Group using the `rg` affix:</span></span>

* <span data-ttu-id="41931-124">Rg-WebApp (préfixe)</span><span class="sxs-lookup"><span data-stu-id="41931-124">Rg-WebApp (prefix)</span></span>
* <span data-ttu-id="41931-125">WebApp-Rg (suffixe)</span><span class="sxs-lookup"><span data-stu-id="41931-125">WebApp-Rg (suffix)</span></span>

<span data-ttu-id="41931-126">Les affixes peuvent faire référence à différents aspects des ressources spécifiques.</span><span class="sxs-lookup"><span data-stu-id="41931-126">Affixes can refer to different aspects that describe the particular resources.</span></span> <span data-ttu-id="41931-127">Le tableau suivant présente des exemples généralement utilisés.</span><span class="sxs-lookup"><span data-stu-id="41931-127">The following table shows some examples typically used.</span></span>

| <span data-ttu-id="41931-128">Aspect</span><span class="sxs-lookup"><span data-stu-id="41931-128">Aspect</span></span> | <span data-ttu-id="41931-129">Exemples</span><span class="sxs-lookup"><span data-stu-id="41931-129">Examples</span></span> | <span data-ttu-id="41931-130">Remarques</span><span class="sxs-lookup"><span data-stu-id="41931-130">Notes</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="41931-131">Environnement</span><span class="sxs-lookup"><span data-stu-id="41931-131">Environment</span></span> |<span data-ttu-id="41931-132">dev, stg, prod</span><span class="sxs-lookup"><span data-stu-id="41931-132">dev, stg, prod</span></span> |<span data-ttu-id="41931-133">En fonction de l’objectif et du nom de chaque environnement.</span><span class="sxs-lookup"><span data-stu-id="41931-133">Depending on the purpose and name of each environment.</span></span> |
| <span data-ttu-id="41931-134">Lieu</span><span class="sxs-lookup"><span data-stu-id="41931-134">Location</span></span> |<span data-ttu-id="41931-135">usw (West US), use (East US 2)</span><span class="sxs-lookup"><span data-stu-id="41931-135">usw (West US), use (East US 2)</span></span> |<span data-ttu-id="41931-136">En fonction de la région du centre de données et de l’organisation.</span><span class="sxs-lookup"><span data-stu-id="41931-136">Depending on the region of the datacenter or the region of the organization.</span></span> |
| <span data-ttu-id="41931-137">Composant, service ou produit Azure</span><span class="sxs-lookup"><span data-stu-id="41931-137">Azure component, service, or product</span></span> |<span data-ttu-id="41931-138">Rg pour groupe de ressources, VNet pour réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="41931-138">Rg for resource group, VNet for virtual network</span></span> |<span data-ttu-id="41931-139">En fonction du produit auquel la ressource est associée.</span><span class="sxs-lookup"><span data-stu-id="41931-139">Depending on the product for which the resource provides support.</span></span> |
| <span data-ttu-id="41931-140">Rôle</span><span class="sxs-lookup"><span data-stu-id="41931-140">Role</span></span> |<span data-ttu-id="41931-141">sql, ora, sp, iis</span><span class="sxs-lookup"><span data-stu-id="41931-141">sql, ora, sp, iis</span></span> |<span data-ttu-id="41931-142">En fonction du rôle de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="41931-142">Depending on the role of the virtual machine.</span></span> |
| <span data-ttu-id="41931-143">Instance</span><span class="sxs-lookup"><span data-stu-id="41931-143">Instance</span></span> |<span data-ttu-id="41931-144">01, 02, 03, etc.</span><span class="sxs-lookup"><span data-stu-id="41931-144">01, 02, 03, etc.</span></span> |<span data-ttu-id="41931-145">Pour les ressources possédant plusieurs instances.</span><span class="sxs-lookup"><span data-stu-id="41931-145">For resources that have more than one instance.</span></span> <span data-ttu-id="41931-146">Par exemple, des serveurs Web à charge équilibrée dans un service cloud.</span><span class="sxs-lookup"><span data-stu-id="41931-146">For example, load balanced web servers in a cloud service.</span></span> |

<span data-ttu-id="41931-147">Lors de l’établissement de conventions d’affectation de noms, assurez-vous qu’elles indiquent clairement les affixes à utiliser pour chaque type de ressource et à quelle position (suffixe ou préfixe).</span><span class="sxs-lookup"><span data-stu-id="41931-147">When establishing your naming conventions, make sure that they clearly state which affixes to use for each type of resource, and in which position (prefix vs suffix).</span></span>

## <a name="dates"></a><span data-ttu-id="41931-148">Dates</span><span class="sxs-lookup"><span data-stu-id="41931-148">Dates</span></span>
<span data-ttu-id="41931-149">Dans de nombreux cas, il est important de déterminer la date de création à partir du nom d’une ressource.</span><span class="sxs-lookup"><span data-stu-id="41931-149">It is often important to determine the date of creation from the name of a resource.</span></span> <span data-ttu-id="41931-150">Nous recommandons le format de date AAAAMMJJ.</span><span class="sxs-lookup"><span data-stu-id="41931-150">We recommend the YYYYMMDD date format.</span></span> <span data-ttu-id="41931-151">Ce format permet non seulement d’enregistrer la date complète, mais également de trier simultanément par ordre alphabétique et par ordre chronologique deux ressources dont les noms diffèrent uniquement au niveau de la date.</span><span class="sxs-lookup"><span data-stu-id="41931-151">This format ensures that not only the full date is recorded, but also that two resources whose names differ only on the date is sorted alphabetically and chronologically at the same time.</span></span>

## <a name="naming-resources"></a><span data-ttu-id="41931-152">Ressources d’affectation de noms</span><span class="sxs-lookup"><span data-stu-id="41931-152">Naming resources</span></span>
<span data-ttu-id="41931-153">Définissez chaque type de ressource dans la convention d’affectation de noms, qui doit comprendre des règles définissant l’attribution de nom pour chaque ressource créée.</span><span class="sxs-lookup"><span data-stu-id="41931-153">Define each type of resource in the naming convention, which should have rules that define how to assign names to each resource that is created.</span></span> <span data-ttu-id="41931-154">Ces règles doivent s’appliquer à tous les types de ressources, par exemple :</span><span class="sxs-lookup"><span data-stu-id="41931-154">These rules should apply to all types of resources, for example:</span></span>

* <span data-ttu-id="41931-155">Abonnements</span><span class="sxs-lookup"><span data-stu-id="41931-155">Subscriptions</span></span>
* <span data-ttu-id="41931-156">Comptes</span><span class="sxs-lookup"><span data-stu-id="41931-156">Accounts</span></span>
* <span data-ttu-id="41931-157">Comptes de stockage</span><span class="sxs-lookup"><span data-stu-id="41931-157">Storage accounts</span></span>
* <span data-ttu-id="41931-158">Réseaux virtuels</span><span class="sxs-lookup"><span data-stu-id="41931-158">Virtual networks</span></span>
* <span data-ttu-id="41931-159">Sous-réseaux</span><span class="sxs-lookup"><span data-stu-id="41931-159">Subnets</span></span>
* <span data-ttu-id="41931-160">Groupes à haute disponibilité</span><span class="sxs-lookup"><span data-stu-id="41931-160">Availability sets</span></span>
* <span data-ttu-id="41931-161">Groupes de ressources</span><span class="sxs-lookup"><span data-stu-id="41931-161">Resource groups</span></span>
* <span data-ttu-id="41931-162">Machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="41931-162">Virtual machines</span></span>
* <span data-ttu-id="41931-163">Points de terminaison</span><span class="sxs-lookup"><span data-stu-id="41931-163">Endpoints</span></span>
* <span data-ttu-id="41931-164">groupes de sécurité réseau ;</span><span class="sxs-lookup"><span data-stu-id="41931-164">Network security groups</span></span>
* <span data-ttu-id="41931-165">contrôleur</span><span class="sxs-lookup"><span data-stu-id="41931-165">Roles</span></span>

<span data-ttu-id="41931-166">Les noms doivent être descriptifs, afin de fournir suffisamment d’informations pour déterminer la ressource à laquelle ils font référence.</span><span class="sxs-lookup"><span data-stu-id="41931-166">To ensure that the name provides enough information to determine to which resource it refers, you should use descriptive names.</span></span>

## <a name="computer-names"></a><span data-ttu-id="41931-167">Noms des ordinateurs</span><span class="sxs-lookup"><span data-stu-id="41931-167">Computer names</span></span>
<span data-ttu-id="41931-168">Lorsque vous créez une machine virtuelle, Microsoft Azure requiert un nom de machine virtuelle contenant jusqu’à 15 caractères, et qui est utilisé pour le nom de la ressource.</span><span class="sxs-lookup"><span data-stu-id="41931-168">When you create a virtual machine (VM), Microsoft Azure requires a VM name of up to 15 characters which is used for the resource name.</span></span> <span data-ttu-id="41931-169">Azure utilise le même nom pour le système d’exploitation installé sur la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="41931-169">Azure uses the same name for the operating system installed in the VM.</span></span> <span data-ttu-id="41931-170">Toutefois, ces noms peuvent ne pas toujours être identiques.</span><span class="sxs-lookup"><span data-stu-id="41931-170">However, these names might not always be the same.</span></span>

<span data-ttu-id="41931-171">Si une machine virtuelle est créée à partir d’un fichier d’image .vhd qui contient déjà un système d’exploitation, le nom de la machine virtuelle dans Azure peut différer du nom d’ordinateur du système d’exploitation de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="41931-171">In case a VM is created from a .vhd image file that already contains an operating system, the VM name in Azure can differ from the VM's operating system computer name.</span></span> <span data-ttu-id="41931-172">Dans ce cas, la gestion de la machine virtuelle devient plus difficile. C’est pourquoi nous le déconseillons.</span><span class="sxs-lookup"><span data-stu-id="41931-172">This situation can add a degree of difficulty to VM management, which we therefore do not recommend.</span></span> <span data-ttu-id="41931-173">Affectez à la ressource de la machine virtuelle Azure le nom d’ordinateur attribué au système d’exploitation de cette machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="41931-173">Assign the Azure VM resource the same name as the computer name that you assign to the operating system of that VM.</span></span>

<span data-ttu-id="41931-174">Nous recommandons que le nom de la machine virtuelle Azure soit le même que le nom d’ordinateur du système d’exploitation sous-jacent.</span><span class="sxs-lookup"><span data-stu-id="41931-174">We recommend that the Azure VM name is the same as the underlying operating system computer name.</span></span>

## <a name="storage-account-names"></a><span data-ttu-id="41931-175">Noms des comptes de stockage</span><span class="sxs-lookup"><span data-stu-id="41931-175">Storage account names</span></span>
<span data-ttu-id="41931-176">Cette section ne s’applique pas aux [disques managés Azure](../../storage/storage-managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), étant donné que vous ne créez pas de compte de stockage distinct.</span><span class="sxs-lookup"><span data-stu-id="41931-176">This section does not apply to [Azure Managed Disks](../../storage/storage-managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), as you do not create a separate storage account.</span></span> <span data-ttu-id="41931-177">Pour les disques non managés, la dénomination des comptes de stockage est régie par des règles spécifiques.</span><span class="sxs-lookup"><span data-stu-id="41931-177">For unmanaged disks, storage accounts have special rules governing their names.</span></span> <span data-ttu-id="41931-178">Vous ne pouvez utiliser que des lettres minuscules et des chiffres.</span><span class="sxs-lookup"><span data-stu-id="41931-178">You can only use lowercase letters and numbers.</span></span> <span data-ttu-id="41931-179">Pour plus d’informations, consultez la rubrique [Création d’un compte de stockage](../../storage/storage-create-storage-account.md#create-a-storage-account) .</span><span class="sxs-lookup"><span data-stu-id="41931-179">For more information, see [Create a storage account](../../storage/storage-create-storage-account.md#create-a-storage-account).</span></span> <span data-ttu-id="41931-180">En outre, le nom du compte de stockage, ainsi que core.windows.net, doit être un nom DNS unique et globalement valide.</span><span class="sxs-lookup"><span data-stu-id="41931-180">Additionally, the storage account name, along with core.windows.net, should be a globally valid, unique DNS name.</span></span> <span data-ttu-id="41931-181">Par exemple, si le compte de stockage est appelé mystorageaccount, les noms DNS suivants qui en résultent doivent être uniques :</span><span class="sxs-lookup"><span data-stu-id="41931-181">For instance, if the storage account is called mystorageaccount, the following resulting DNS names should be unique:</span></span>

* <span data-ttu-id="41931-182">mystorageaccount.blob.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="41931-182">mystorageaccount.blob.core.windows.net</span></span>
* <span data-ttu-id="41931-183">mystorageaccount.table.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="41931-183">mystorageaccount.table.core.windows.net</span></span>
* <span data-ttu-id="41931-184">mystorageaccount.queue.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="41931-184">mystorageaccount.queue.core.windows.net</span></span>

## <a name="next-steps"></a><span data-ttu-id="41931-185">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="41931-185">Next steps</span></span>
[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-windows-infrastructure-guidelines-next-steps.md)]

