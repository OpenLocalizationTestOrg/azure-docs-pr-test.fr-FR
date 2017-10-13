---
title: Types de quotas dans Azure Stack | Microsoft Docs
description: "Passez en revue les différents types de quotas disponibles pour les services et les ressources dans Azure Stack."
services: azure-stack
documentationcenter: 
author: ErikjeMS
manager: byronr
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 8/23/2017
ms.author: erikje
ms.openlocfilehash: 33906514955b76a3d6587b19899a0c76a09018a2
ms.sourcegitcommit: 90e2cced6a773b1b52f999ba73cd8877305d270b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/13/2017
---
# <a name="quota-types-in-azure-stack"></a><span data-ttu-id="bc063-103">Types de quotas dans Azure Stack</span><span class="sxs-lookup"><span data-stu-id="bc063-103">Quota types in Azure Stack</span></span>

<span data-ttu-id="bc063-104">*S’applique à : systèmes intégrés Azure Stack et Kit de développement Azure Stack*</span><span class="sxs-lookup"><span data-stu-id="bc063-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

<span data-ttu-id="bc063-105">Les [quotas](azure-stack-plan-offer-quota-overview.md#plans) définissent les limites de ressources qu’un abonnement utilisateur peut approvisionner ou consommer.</span><span class="sxs-lookup"><span data-stu-id="bc063-105">[Quotas](azure-stack-plan-offer-quota-overview.md#plans) define the limits of resources that a user subscription can provision or consume.</span></span> <span data-ttu-id="bc063-106">Par exemple, un quota peut autoriser un utilisateur de créer jusqu’à cinq machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="bc063-106">For example, a quota might allow a user to create up to five VMs.</span></span> <span data-ttu-id="bc063-107">Chaque ressource peut avoir ses propres types de quotas.</span><span class="sxs-lookup"><span data-stu-id="bc063-107">Each resource can have its own types of quotas.</span></span>

## <a name="compute-quota-types"></a><span data-ttu-id="bc063-108">Types de quotas de capacité de traitement (compute)</span><span class="sxs-lookup"><span data-stu-id="bc063-108">Compute quota types</span></span>
| <span data-ttu-id="bc063-109">**Type**</span><span class="sxs-lookup"><span data-stu-id="bc063-109">**Type**</span></span> | <span data-ttu-id="bc063-110">**Valeur par défaut**</span><span class="sxs-lookup"><span data-stu-id="bc063-110">**Default value**</span></span> | <span data-ttu-id="bc063-111">**Description**</span><span class="sxs-lookup"><span data-stu-id="bc063-111">**Description**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="bc063-112">Nombre maximal de machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="bc063-112">Max number of virtual machines</span></span> |<span data-ttu-id="bc063-113">50</span><span class="sxs-lookup"><span data-stu-id="bc063-113">50</span></span> | <span data-ttu-id="bc063-114">Nombre maximal de machines virtuelles qu’un abonnement peut créer à cet emplacement.</span><span class="sxs-lookup"><span data-stu-id="bc063-114">The maximum number of virtual machines that a subscription can create in this location.</span></span> |
| <span data-ttu-id="bc063-115">Nombre maximal de cœurs de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="bc063-115">Max number of virtual machine cores</span></span> |<span data-ttu-id="bc063-116">100</span><span class="sxs-lookup"><span data-stu-id="bc063-116">100</span></span> | <span data-ttu-id="bc063-117">Nombre maximal de cœurs qu’un abonnement peut créer à cet emplacement (par exemple, une machine virtuelle A3 a quatre cœurs).</span><span class="sxs-lookup"><span data-stu-id="bc063-117">The maximum number of cores that a subscription can create in this location (for example, an A3 VM has four cores).</span></span> |
| <span data-ttu-id="bc063-118">Nombre maximal de groupes à haute disponibilité</span><span class="sxs-lookup"><span data-stu-id="bc063-118">Max number of availability sets</span></span> |<span data-ttu-id="bc063-119">10</span><span class="sxs-lookup"><span data-stu-id="bc063-119">10</span></span> | <span data-ttu-id="bc063-120">Nombre maximal de groupes à haute disponibilité qui peuvent être créés à cet emplacement.</span><span class="sxs-lookup"><span data-stu-id="bc063-120">The maximum number of availability sets that can be created in this location.</span></span> |
| <span data-ttu-id="bc063-121">Nombre maximal de groupes de machines virtuelles identiques</span><span class="sxs-lookup"><span data-stu-id="bc063-121">Max number of virtual machine scale sets</span></span> |<span data-ttu-id="bc063-122">100</span><span class="sxs-lookup"><span data-stu-id="bc063-122">100</span></span> | <span data-ttu-id="bc063-123">Nombre maximal de groupes de machines virtuelles identiques qui peuvent être créés à cet emplacement.</span><span class="sxs-lookup"><span data-stu-id="bc063-123">The maximum number of virtual machine scale sets that can be created in this location.</span></span> |

> [!NOTE]
> <span data-ttu-id="bc063-124">Les quotas de capacité de traitement (compute) ne sont pas appliqués dans cette version Technical Preview.</span><span class="sxs-lookup"><span data-stu-id="bc063-124">Compute quotas are not enforced in this technical preview.</span></span>
> 
> 

## <a name="storage-quota-types"></a><span data-ttu-id="bc063-125">Types de quotas de stockage</span><span class="sxs-lookup"><span data-stu-id="bc063-125">Storage quota types</span></span>
| <span data-ttu-id="bc063-126">**Item**</span><span class="sxs-lookup"><span data-stu-id="bc063-126">**Item**</span></span> | <span data-ttu-id="bc063-127">**Valeur par défaut**</span><span class="sxs-lookup"><span data-stu-id="bc063-127">**Default value**</span></span> | <span data-ttu-id="bc063-128">**Description**</span><span class="sxs-lookup"><span data-stu-id="bc063-128">**Description**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="bc063-129">Capacité maximale (Go)</span><span class="sxs-lookup"><span data-stu-id="bc063-129">Maximum capacity (GB)</span></span> |<span data-ttu-id="bc063-130">500</span><span class="sxs-lookup"><span data-stu-id="bc063-130">500</span></span> |<span data-ttu-id="bc063-131">Capacité de stockage totale qui peut être consommée par un abonnement à cet emplacement.</span><span class="sxs-lookup"><span data-stu-id="bc063-131">Total storage capacity that can be consumed by a subscription in this location.</span></span> |
| <span data-ttu-id="bc063-132">Nombre total de comptes de stockage</span><span class="sxs-lookup"><span data-stu-id="bc063-132">Total number of storage accounts</span></span> |<span data-ttu-id="bc063-133">20</span><span class="sxs-lookup"><span data-stu-id="bc063-133">20</span></span> |<span data-ttu-id="bc063-134">Nombre maximal de comptes de stockage qu’un abonnement peut créer à cet emplacement.</span><span class="sxs-lookup"><span data-stu-id="bc063-134">The maximum number of storage accounts that a subscription can create in this location.</span></span> |

## <a name="network-quota-types"></a><span data-ttu-id="bc063-135">Types de quotas pour les réseaux</span><span class="sxs-lookup"><span data-stu-id="bc063-135">Network quota types</span></span>
| <span data-ttu-id="bc063-136">**Item**</span><span class="sxs-lookup"><span data-stu-id="bc063-136">**Item**</span></span> | <span data-ttu-id="bc063-137">**Valeur par défaut**</span><span class="sxs-lookup"><span data-stu-id="bc063-137">**Default value**</span></span> | <span data-ttu-id="bc063-138">**Description**</span><span class="sxs-lookup"><span data-stu-id="bc063-138">**Description**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="bc063-139">Nombre maximal d’adresses IP publiques</span><span class="sxs-lookup"><span data-stu-id="bc063-139">Max public IPs</span></span> |<span data-ttu-id="bc063-140">50</span><span class="sxs-lookup"><span data-stu-id="bc063-140">50</span></span> |<span data-ttu-id="bc063-141">Nombre maximal d’adresses IP publiques qu’un abonnement peut créer à cet emplacement.</span><span class="sxs-lookup"><span data-stu-id="bc063-141">The maximum number of public IPs that a subscription can create in this location.</span></span> |
| <span data-ttu-id="bc063-142">Nombre maximal de réseaux virtuels</span><span class="sxs-lookup"><span data-stu-id="bc063-142">Max virtual networks</span></span> |<span data-ttu-id="bc063-143">50</span><span class="sxs-lookup"><span data-stu-id="bc063-143">50</span></span> |<span data-ttu-id="bc063-144">Nombre maximal de réseaux virtuels qu’un abonnement peut créer à cet emplacement.</span><span class="sxs-lookup"><span data-stu-id="bc063-144">The maximum number of virtual networks that a subscription can create in this location.</span></span> |
| <span data-ttu-id="bc063-145">Nombre maximal de passerelles de réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="bc063-145">Max virtual network gateways</span></span> |<span data-ttu-id="bc063-146">1</span><span class="sxs-lookup"><span data-stu-id="bc063-146">1</span></span> |<span data-ttu-id="bc063-147">Nombre maximal de passerelles de réseau virtuel qu’un abonnement peut créer à cet emplacement.</span><span class="sxs-lookup"><span data-stu-id="bc063-147">The maximum number of virtual network gateways (VPN Gateways) that a subscription can create in this location.</span></span> |
| <span data-ttu-id="bc063-148">Nombre maximal de connexions réseau</span><span class="sxs-lookup"><span data-stu-id="bc063-148">Max network connections</span></span> |<span data-ttu-id="bc063-149">2</span><span class="sxs-lookup"><span data-stu-id="bc063-149">2</span></span> |<span data-ttu-id="bc063-150">Nombre maximal de connexions réseau (point à point ou site à site) qu’un abonnement peut créer pour toutes les passerelles de réseau virtuel à cet emplacement.</span><span class="sxs-lookup"><span data-stu-id="bc063-150">The maximum number of network connections (point-to-point or site-to-site) that a subscription can create across all virtual network gateways in this location.</span></span> |
| <span data-ttu-id="bc063-151">Nombre maximal d’équilibreurs de charge</span><span class="sxs-lookup"><span data-stu-id="bc063-151">Max load balancers</span></span> |<span data-ttu-id="bc063-152">50</span><span class="sxs-lookup"><span data-stu-id="bc063-152">50</span></span> |<span data-ttu-id="bc063-153">Nombre maximal d’équilibreurs de charge qu’un abonnement peut créer à cet emplacement.</span><span class="sxs-lookup"><span data-stu-id="bc063-153">The maximum number of load balancers that a subscription can create in this location.</span></span> |
| <span data-ttu-id="bc063-154">Nombre max de cartes réseau</span><span class="sxs-lookup"><span data-stu-id="bc063-154">Max NICs</span></span> |<span data-ttu-id="bc063-155">100</span><span class="sxs-lookup"><span data-stu-id="bc063-155">100</span></span> |<span data-ttu-id="bc063-156">Nombre maximal d’interfaces réseau qu’un abonnement peut créer à cet emplacement.</span><span class="sxs-lookup"><span data-stu-id="bc063-156">The maximum number of network interfaces that a subscription can create in this location.</span></span> |
| <span data-ttu-id="bc063-157">Nombre maximal de groupes de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="bc063-157">Max network security groups</span></span> |<span data-ttu-id="bc063-158">50</span><span class="sxs-lookup"><span data-stu-id="bc063-158">50</span></span> |<span data-ttu-id="bc063-159">Nombre maximal de groupes de sécurité réseau qu’un abonnement peut créer à cet emplacement.</span><span class="sxs-lookup"><span data-stu-id="bc063-159">The maximum number of network security groups that a subscription can create in this location.</span></span> |

## <a name="view-an-existing-quota"></a><span data-ttu-id="bc063-160">Afficher un quota existant</span><span class="sxs-lookup"><span data-stu-id="bc063-160">View an existing quota</span></span>
1. <span data-ttu-id="bc063-161">Cliquez sur **Autres services** > **Fournisseurs de ressources**.</span><span class="sxs-lookup"><span data-stu-id="bc063-161">Click **More services** > **Resource Providers**.</span></span>
2. <span data-ttu-id="bc063-162">Sélectionnez le service avec le quota que vous voulez afficher.</span><span class="sxs-lookup"><span data-stu-id="bc063-162">Select the service with the quota that you want to view.</span></span>
3. <span data-ttu-id="bc063-163">Cliquez sur **Quotas**, puis sélectionnez le quota que vous voulez afficher.</span><span class="sxs-lookup"><span data-stu-id="bc063-163">Click **Quotas**, and select the quota you want to view.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bc063-164">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="bc063-164">Next steps</span></span>
[<span data-ttu-id="bc063-165">Découvrez plus d’informations sur les plans, les offres et les quotas.</span><span class="sxs-lookup"><span data-stu-id="bc063-165">Learn more about plans, offers, and quotas.</span></span>](azure-stack-plan-offer-quota-overview.md)

[<span data-ttu-id="bc063-166">Créez des quotas lors de la création d’un plan.</span><span class="sxs-lookup"><span data-stu-id="bc063-166">Create quotas while creating a plan.</span></span>](azure-stack-create-plan.md)
