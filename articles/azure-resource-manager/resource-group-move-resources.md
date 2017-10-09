---
title: aaaMove ressources Azure toonew abonnement ou groupe de ressources | Documents Microsoft
description: "Utilisez le Gestionnaire de ressources Azure toomove ressources tooa nouveau groupe de ressources ou d’un abonnement."
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: ab7d42bd-8434-4026-a892-df4a97b60a9b
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: tomfitz
ms.openlocfilehash: 09d35f0afbbcdc0c66779f98a982d878f0807497
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="move-resources-toonew-resource-group-or-subscription"></a><span data-ttu-id="5b637-103">Déplacer le groupe de ressources toonew ressources ou d’un abonnement</span><span class="sxs-lookup"><span data-stu-id="5b637-103">Move resources toonew resource group or subscription</span></span>
<span data-ttu-id="5b637-104">Cette rubrique vous montre comment toomove ressources tooeither un nouvel abonnement ou une ressource de groupe Bonjour même abonnement.</span><span class="sxs-lookup"><span data-stu-id="5b637-104">This topic shows you how toomove resources tooeither a new subscription or a new resource group in hello same subscription.</span></span> <span data-ttu-id="5b637-105">Vous pouvez utiliser le portail de hello, PowerShell, CLI d’Azure ou hello ressource de toomove API REST.</span><span class="sxs-lookup"><span data-stu-id="5b637-105">You can use hello portal, PowerShell, Azure CLI, or hello REST API toomove resource.</span></span> <span data-ttu-id="5b637-106">les opérations de déplacement Hello dans cette rubrique sont disponible tooyou sans l’assistance du support technique Azure.</span><span class="sxs-lookup"><span data-stu-id="5b637-106">hello move operations in this topic are available tooyou without any assistance from Azure support.</span></span>

<span data-ttu-id="5b637-107">Lors du déplacement de ressources, les groupes de source de hello et hello cible sont verrouillés au cours de l’opération de hello.</span><span class="sxs-lookup"><span data-stu-id="5b637-107">When moving resources, both hello source group and hello target group are locked during hello operation.</span></span> <span data-ttu-id="5b637-108">Écriture et suppression des opérations sont bloquées sur les groupes de ressources hello jusqu'à ce que le déplacement de hello se termine.</span><span class="sxs-lookup"><span data-stu-id="5b637-108">Write and delete operations are blocked on hello resource groups until hello move completes.</span></span> <span data-ttu-id="5b637-109">Ce verrou signifie que vous ne peut pas ajouter, mettre à jour ou supprimer des ressources dans les groupes de ressources hello, mais cela ne signifie pas les ressources hello sont figées.</span><span class="sxs-lookup"><span data-stu-id="5b637-109">This lock means you cannot add, update, or delete resources in hello resource groups, but it does not mean hello resources are frozen.</span></span> <span data-ttu-id="5b637-110">Par exemple, si vous déplacez un serveur SQL Server et son groupe de ressources de base de données tooa, une application qui utilise la base de données hello ne rencontre aucune interruption de service.</span><span class="sxs-lookup"><span data-stu-id="5b637-110">For example, if you move a SQL Server and its database tooa new resource group, an application that uses hello database experiences no downtime.</span></span> <span data-ttu-id="5b637-111">Il peut toujours lire et écrire des toohello de base de données.</span><span class="sxs-lookup"><span data-stu-id="5b637-111">It can still read and write toohello database.</span></span>

<span data-ttu-id="5b637-112">Vous ne pouvez pas modifier l’emplacement hello de ressource de hello.</span><span class="sxs-lookup"><span data-stu-id="5b637-112">You cannot change hello location of hello resource.</span></span> <span data-ttu-id="5b637-113">Déplacement d’une ressource uniquement déplace tooa nouveau groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="5b637-113">Moving a resource only moves it tooa new resource group.</span></span> <span data-ttu-id="5b637-114">nouveau groupe de ressources Hello peut avoir un emplacement différent, mais qui ne modifie pas l’emplacement hello de ressource de hello.</span><span class="sxs-lookup"><span data-stu-id="5b637-114">hello new resource group may have a different location, but that does not change hello location of hello resource.</span></span>

> [!NOTE]
> <span data-ttu-id="5b637-115">Cet article décrit comment les ressources toomove dans Azure existant compte offres.</span><span class="sxs-lookup"><span data-stu-id="5b637-115">This article describes how toomove resources within an existing Azure account offering.</span></span> <span data-ttu-id="5b637-116">Reportez-vous à votre compte Azure offre (par exemple, la mise à niveau à partir de paiement à l’utilisation de paie-toopre) tout en continuant toowork avec vos ressources existantes, si vous souhaitez réellement toochange [basculer votre offre de tooanother abonnement Azure](../billing/billing-how-to-switch-azure-offer.md).</span><span class="sxs-lookup"><span data-stu-id="5b637-116">If you actually want toochange your Azure account offering (such as upgrading from pay-as-you-go toopre-pay) while continuing toowork with your existing resources, see [Switch your Azure subscription tooanother offer](../billing/billing-how-to-switch-azure-offer.md).</span></span>
>
>

## <a name="checklist-before-moving-resources"></a><span data-ttu-id="5b637-117">Liste de contrôle avant le déplacement de ressources</span><span class="sxs-lookup"><span data-stu-id="5b637-117">Checklist before moving resources</span></span>
<span data-ttu-id="5b637-118">Il existe certains tooperform étapes importantes avant de déplacer une ressource.</span><span class="sxs-lookup"><span data-stu-id="5b637-118">There are some important steps tooperform before moving a resource.</span></span> <span data-ttu-id="5b637-119">Vérifiez ces conditions pour prévenir d'éventuelles erreurs.</span><span class="sxs-lookup"><span data-stu-id="5b637-119">By verifying these conditions, you can avoid errors.</span></span>

1. <span data-ttu-id="5b637-120">Hello abonnements source et de destination doivent exister dans hello même [client Azure Active Directory](../active-directory/active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="5b637-120">hello source and destination subscriptions must exist within hello same [Azure Active Directory tenant](../active-directory/active-directory-howto-tenant.md).</span></span> <span data-ttu-id="5b637-121">toocheck que les deux abonnements ont hello même ID de locataire, utilisez Azure PowerShell ou CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="5b637-121">toocheck that both subscriptions have hello same tenant ID, use Azure PowerShell or Azure CLI.</span></span>

  <span data-ttu-id="5b637-122">Pour Azure PowerShell, utilisez :</span><span class="sxs-lookup"><span data-stu-id="5b637-122">For Azure PowerShell, use:</span></span>

  ```powershell
  (Get-AzureRmSubscription -SubscriptionName "Example Subscription").TenantId
  ```

  <span data-ttu-id="5b637-123">Pour Azure CLI 2.0, utilisez :</span><span class="sxs-lookup"><span data-stu-id="5b637-123">For Azure CLI 2.0, use:</span></span>

  ```azurecli
  az account show --subscription "Example Subscription" --query tenantId
  ```

  <span data-ttu-id="5b637-124">Si hello client ID pour les abonnements source et destination hello ne sont pas hello même, vous pouvez tenter de répertoire de hello toochange pour l’abonnement de hello.</span><span class="sxs-lookup"><span data-stu-id="5b637-124">If hello tenant IDs for hello source and destination subscriptions are not hello same, you can attempt toochange hello directory for hello subscription.</span></span> <span data-ttu-id="5b637-125">Toutefois, cette option est uniquement disponible tooService administrateurs qui se sont connectés avec un compte Microsoft (et non pas un compte d’organisation).</span><span class="sxs-lookup"><span data-stu-id="5b637-125">However, this option is only available tooService Administrators who are signed in with a Microsoft account (not an organizational account).</span></span> <span data-ttu-id="5b637-126">tooattempt passage du répertoire hello, ouvrez une session toohello [portail classique](https://manage.windowsazure.com/), puis sélectionnez **paramètres**, puis sélectionnez l’abonnement de hello.</span><span class="sxs-lookup"><span data-stu-id="5b637-126">tooattempt changing hello directory, log in toohello [classic portal](https://manage.windowsazure.com/), and select **Settings**, and select hello subscription.</span></span> <span data-ttu-id="5b637-127">Si hello **modifier l’annuaire** icône n’est disponible, sélectionnez-la toochange hello associé à Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5b637-127">If hello **Edit Directory** icon is available, select it toochange hello associated Azure Active Directory.</span></span>

  ![Modifier l’annuaire](./media/resource-group-move-resources/edit-directory.png)

  <span data-ttu-id="5b637-129">Si cette icône n’est pas disponible, vous devez contacter le support toomove hello ressources tooa nouveau client.</span><span class="sxs-lookup"><span data-stu-id="5b637-129">If that icon is not available, you must contact support toomove hello resources tooa new tenant.</span></span>

2. <span data-ttu-id="5b637-130">service de Hello doit activer les ressources de toomove de capacité hello.</span><span class="sxs-lookup"><span data-stu-id="5b637-130">hello service must enable hello ability toomove resources.</span></span> <span data-ttu-id="5b637-131">Cette rubrique répertorie les services permettant de déplacer des ressources et les services qui ne le permettent pas.</span><span class="sxs-lookup"><span data-stu-id="5b637-131">This topic lists which services enable moving resources and which services do not enable moving resources.</span></span>
3. <span data-ttu-id="5b637-132">abonnement de destination Hello doit être inscrit pour le fournisseur de ressources hello de ressource hello en cours de déplacement.</span><span class="sxs-lookup"><span data-stu-id="5b637-132">hello destination subscription must be registered for hello resource provider of hello resource being moved.</span></span> <span data-ttu-id="5b637-133">Si non, vous recevez un message d’erreur indiquant que hello **abonnement n’est pas inscrit pour un type de ressource**.</span><span class="sxs-lookup"><span data-stu-id="5b637-133">If not, you receive an error stating that hello **subscription is not registered for a resource type**.</span></span> <span data-ttu-id="5b637-134">Vous pouvez rencontrer ce problème lors du déplacement d’un abonnement tooa ressource, mais cet abonnement n’a jamais été utilisé avec ce type de ressource.</span><span class="sxs-lookup"><span data-stu-id="5b637-134">You might encounter this problem when moving a resource tooa new subscription, but that subscription has never been used with that resource type.</span></span> <span data-ttu-id="5b637-135">toolearn toocheck hello l’état de l’inscription et inscrire des fournisseurs de ressources, voir [les types et les fournisseurs de ressources](resource-manager-supported-services.md).</span><span class="sxs-lookup"><span data-stu-id="5b637-135">toolearn how toocheck hello registration status and register resource providers, see [Resource providers and types](resource-manager-supported-services.md).</span></span>

## <a name="when-toocall-support"></a><span data-ttu-id="5b637-136">Quand toocall prennent en charge</span><span class="sxs-lookup"><span data-stu-id="5b637-136">When toocall support</span></span>
<span data-ttu-id="5b637-137">Vous pouvez déplacer la plupart des ressources via des opérations de libre-service hello présentées dans cette rubrique.</span><span class="sxs-lookup"><span data-stu-id="5b637-137">You can move most resources through hello self-service operations shown in this topic.</span></span> <span data-ttu-id="5b637-138">Utilisez hello libre-service des opérations :</span><span class="sxs-lookup"><span data-stu-id="5b637-138">Use hello self-service operations to:</span></span>

* <span data-ttu-id="5b637-139">Déplacer des ressources Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="5b637-139">Move Resource Manager resources.</span></span>
* <span data-ttu-id="5b637-140">Déplacer les ressources classiques selon toohello [limitations concernant le déploiement classique](#classic-deployment-limitations).</span><span class="sxs-lookup"><span data-stu-id="5b637-140">Move classic resources according toohello [classic deployment limitations](#classic-deployment-limitations).</span></span>

<span data-ttu-id="5b637-141">Appelez le support technique quand vous devez :</span><span class="sxs-lookup"><span data-stu-id="5b637-141">Call support when you need to:</span></span>

* <span data-ttu-id="5b637-142">Déplacez votre compte Azure tooa ressources (et le client Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="5b637-142">Move your resources tooa new Azure account (and Azure Active Directory tenant).</span></span>
* <span data-ttu-id="5b637-143">Déplacer les ressources classiques mais rencontrez des problèmes avec les limitations hello.</span><span class="sxs-lookup"><span data-stu-id="5b637-143">Move classic resources but are having trouble with hello limitations.</span></span>

## <a name="services-that-enable-move"></a><span data-ttu-id="5b637-144">Services permettant le déplacement</span><span class="sxs-lookup"><span data-stu-id="5b637-144">Services that enable move</span></span>
<span data-ttu-id="5b637-145">Pour l’instant, les services hello activez tooboth déplacer un groupe de ressources et l’abonnement sont :</span><span class="sxs-lookup"><span data-stu-id="5b637-145">For now, hello services that enable moving tooboth a new resource group and subscription are:</span></span>

* <span data-ttu-id="5b637-146">API Management</span><span class="sxs-lookup"><span data-stu-id="5b637-146">API Management</span></span>
* <span data-ttu-id="5b637-147">Applications App Service (applications web) : consultez [Limitations d’App Service](#app-service-limitations)</span><span class="sxs-lookup"><span data-stu-id="5b637-147">App Service apps (web apps) - see [App Service limitations](#app-service-limitations)</span></span>
* <span data-ttu-id="5b637-148">Application Insights</span><span class="sxs-lookup"><span data-stu-id="5b637-148">Application Insights</span></span>
* <span data-ttu-id="5b637-149">Automatisation</span><span class="sxs-lookup"><span data-stu-id="5b637-149">Automation</span></span>
* <span data-ttu-id="5b637-150">Batch</span><span class="sxs-lookup"><span data-stu-id="5b637-150">Batch</span></span>
* <span data-ttu-id="5b637-151">Bing Maps</span><span class="sxs-lookup"><span data-stu-id="5b637-151">Bing Maps</span></span>
* <span data-ttu-id="5b637-152">CDN</span><span class="sxs-lookup"><span data-stu-id="5b637-152">CDN</span></span>
* <span data-ttu-id="5b637-153">Cloud Services : consultez [Limitations relatives au déploiement Classic](#classic-deployment-limitations)</span><span class="sxs-lookup"><span data-stu-id="5b637-153">Cloud Services - see [Classic deployment limitations](#classic-deployment-limitations)</span></span>
* <span data-ttu-id="5b637-154">Cognitive Services</span><span class="sxs-lookup"><span data-stu-id="5b637-154">Cognitive Services</span></span>
* <span data-ttu-id="5b637-155">Content Moderator</span><span class="sxs-lookup"><span data-stu-id="5b637-155">Content Moderator</span></span>
* <span data-ttu-id="5b637-156">Data Catalog</span><span class="sxs-lookup"><span data-stu-id="5b637-156">Data Catalog</span></span>
* <span data-ttu-id="5b637-157">Data Factory</span><span class="sxs-lookup"><span data-stu-id="5b637-157">Data Factory</span></span>
* <span data-ttu-id="5b637-158">Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="5b637-158">Data Lake Analytics</span></span>
* <span data-ttu-id="5b637-159">Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="5b637-159">Data Lake Store</span></span>
* <span data-ttu-id="5b637-160">DNS</span><span class="sxs-lookup"><span data-stu-id="5b637-160">DNS</span></span>
* <span data-ttu-id="5b637-161">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="5b637-161">Azure Cosmos DB</span></span>
* <span data-ttu-id="5b637-162">Event Hubs</span><span class="sxs-lookup"><span data-stu-id="5b637-162">Event Hubs</span></span>
* <span data-ttu-id="5b637-163">Clusters HDInsight - voir [Limitations de HDInsight](#hdinsight-limitations)</span><span class="sxs-lookup"><span data-stu-id="5b637-163">HDInsight clusters - see [HDInsight limitations](#hdinsight-limitations)</span></span>
* <span data-ttu-id="5b637-164">IoT Hubs</span><span class="sxs-lookup"><span data-stu-id="5b637-164">IoT Hubs</span></span>
* <span data-ttu-id="5b637-165">Key Vault</span><span class="sxs-lookup"><span data-stu-id="5b637-165">Key Vault</span></span>
* <span data-ttu-id="5b637-166">Équilibreurs de charge</span><span class="sxs-lookup"><span data-stu-id="5b637-166">Load Balancers</span></span>
* <span data-ttu-id="5b637-167">Logic Apps</span><span class="sxs-lookup"><span data-stu-id="5b637-167">Logic Apps</span></span>
* <span data-ttu-id="5b637-168">Apprentissage automatique</span><span class="sxs-lookup"><span data-stu-id="5b637-168">Machine Learning</span></span>
* <span data-ttu-id="5b637-169">Media Services</span><span class="sxs-lookup"><span data-stu-id="5b637-169">Media Services</span></span>
* <span data-ttu-id="5b637-170">Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="5b637-170">Mobile Engagement</span></span>
* <span data-ttu-id="5b637-171">Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="5b637-171">Notification Hubs</span></span>
* <span data-ttu-id="5b637-172">Operational Insights</span><span class="sxs-lookup"><span data-stu-id="5b637-172">Operational Insights</span></span>
* <span data-ttu-id="5b637-173">Operations Management</span><span class="sxs-lookup"><span data-stu-id="5b637-173">Operations Management</span></span>
* <span data-ttu-id="5b637-174">Power BI</span><span class="sxs-lookup"><span data-stu-id="5b637-174">Power BI</span></span>
* <span data-ttu-id="5b637-175">Cache Redis</span><span class="sxs-lookup"><span data-stu-id="5b637-175">Redis Cache</span></span>
* <span data-ttu-id="5b637-176">Scheduler</span><span class="sxs-lookup"><span data-stu-id="5b637-176">Scheduler</span></span>
* <span data-ttu-id="5b637-177">Search</span><span class="sxs-lookup"><span data-stu-id="5b637-177">Search</span></span>
* <span data-ttu-id="5b637-178">Gestion de serveur</span><span class="sxs-lookup"><span data-stu-id="5b637-178">Server Management</span></span>
* <span data-ttu-id="5b637-179">Service Bus</span><span class="sxs-lookup"><span data-stu-id="5b637-179">Service Bus</span></span>
* <span data-ttu-id="5b637-180">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="5b637-180">Service Fabric</span></span>
* <span data-ttu-id="5b637-181">Storage</span><span class="sxs-lookup"><span data-stu-id="5b637-181">Storage</span></span>
* <span data-ttu-id="5b637-182">Storage (classique) : consultez [Limitations relatives au déploiement classique](#classic-deployment-limitations)</span><span class="sxs-lookup"><span data-stu-id="5b637-182">Storage (classic) - see [Classic deployment limitations](#classic-deployment-limitations)</span></span>
* <span data-ttu-id="5b637-183">Stream Analytics - Les tâches Stream Analytics ne peuvent pas être déplacées lorsqu’elles sont en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="5b637-183">Stream Analytics - Stream Analytics jobs cannot be moved when in running state.</span></span>
* <span data-ttu-id="5b637-184">Serveur de base de données SQL - hello base de données et le serveur doivent résider dans hello même groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="5b637-184">SQL Database server - hello database and server must reside in hello same resource group.</span></span> <span data-ttu-id="5b637-185">Lorsque vous déplacez un serveur SQL, toutes ses bases de données sont également déplacées.</span><span class="sxs-lookup"><span data-stu-id="5b637-185">When you move a SQL server, all its databases are also moved.</span></span>
* <span data-ttu-id="5b637-186">Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="5b637-186">Traffic Manager</span></span>
* <span data-ttu-id="5b637-187">Machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="5b637-187">Virtual Machines</span></span>
* <span data-ttu-id="5b637-188">Machines virtuelles avec un certificat stocké dans le coffre de clés - déplacer le groupe ressource toonew dans le même abonnement est activé, mais abonnement croisée déplacement n’est pas activé.</span><span class="sxs-lookup"><span data-stu-id="5b637-188">Virtual Machines with certificate stored in Key Vault - Move toonew resource group in same subscription is enabled, but cross subscription move is not enabled.</span></span>
* <span data-ttu-id="5b637-189">Virtual Machines (classique) : consultez [Limitations relatives au déploiement classique](#classic-deployment-limitations)</span><span class="sxs-lookup"><span data-stu-id="5b637-189">Virtual Machines (classic) - see [Classic deployment limitations](#classic-deployment-limitations)</span></span>
* <span data-ttu-id="5b637-190">Jeux de mise à l’échelle de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="5b637-190">Virtual Machine Scale Sets</span></span>
* <span data-ttu-id="5b637-191">Réseaux virtuels : actuellement, un réseau virtuel homologué ne peut pas être déplacé tant que l’homologation de réseau virtuel est activée.</span><span class="sxs-lookup"><span data-stu-id="5b637-191">Virtual Networks - Currently, a peered Virtual Network cannot be moved until VNet peering has been disabled.</span></span> <span data-ttu-id="5b637-192">Une fois désactivée, hello réseau virtuel peut être déplacé correctement et d’homologation de réseau virtuel hello peut être activée.</span><span class="sxs-lookup"><span data-stu-id="5b637-192">Once disabled, hello Virtual Network can be moved successfully and hello VNet peering can be enabled.</span></span> <span data-ttu-id="5b637-193">En outre, un réseau virtuel ne peut pas être déplacé tooa autre abonnement si hello réseau virtuel contient un sous-réseau avec des liens de navigation de ressources.</span><span class="sxs-lookup"><span data-stu-id="5b637-193">In addition, a Virtual Network cannot be moved tooa different subscription if hello Virtual Network contains any subnet with resource navigation links.</span></span> <span data-ttu-id="5b637-194">Par exemple, un sous-réseau de réseau virtuel dispose d’un lien de navigation dans les ressources lorsqu’une ressource Microsoft.Cache redis est déployée dans ce sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="5b637-194">For example, a Virtual Network subnet has a resource navigation link when a Microsoft.Cache redis resource is deployed into this subnet.</span></span>
* <span data-ttu-id="5b637-195">Passerelle VPN</span><span class="sxs-lookup"><span data-stu-id="5b637-195">VPN Gateway</span></span>


## <a name="services-that-do-not-enable-move"></a><span data-ttu-id="5b637-196">Services qui ne permettent pas le déplacement</span><span class="sxs-lookup"><span data-stu-id="5b637-196">Services that do not enable move</span></span>
<span data-ttu-id="5b637-197">services Hello actuellement n’activent pas le déplacement d’une ressource sont :</span><span class="sxs-lookup"><span data-stu-id="5b637-197">hello services that currently do not enable moving a resource are:</span></span>

* <span data-ttu-id="5b637-198">Services de domaine AD</span><span class="sxs-lookup"><span data-stu-id="5b637-198">AD Domain Services</span></span>
* <span data-ttu-id="5b637-199">Service de contrôle d’intégrité hybride Active Directory</span><span class="sxs-lookup"><span data-stu-id="5b637-199">AD Hybrid Health Service</span></span>
* <span data-ttu-id="5b637-200">Application Gateway</span><span class="sxs-lookup"><span data-stu-id="5b637-200">Application Gateway</span></span>
* <span data-ttu-id="5b637-201">Groupes à haute disponibilité comprenant des machines virtuelles avec des disques gérés</span><span class="sxs-lookup"><span data-stu-id="5b637-201">Availability sets with Virtual Machines with Managed Disks</span></span>
* <span data-ttu-id="5b637-202">BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="5b637-202">BizTalk Services</span></span>
* <span data-ttu-id="5b637-203">Service de conteneur</span><span class="sxs-lookup"><span data-stu-id="5b637-203">Container Service</span></span>
* <span data-ttu-id="5b637-204">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="5b637-204">Express Route</span></span>
* <span data-ttu-id="5b637-205">DevTest Labs - déplacer le groupe ressource toonew dans le même abonnement est activé, mais la déplacer de l’abonnement n’est pas activé.</span><span class="sxs-lookup"><span data-stu-id="5b637-205">DevTest Labs - Move toonew resource group in same subscription is enabled, but cross subscription move is not enabled.</span></span>
* <span data-ttu-id="5b637-206">Dynamics LCS</span><span class="sxs-lookup"><span data-stu-id="5b637-206">Dynamics LCS</span></span>
* <span data-ttu-id="5b637-207">Images créées à partir de disques gérés</span><span class="sxs-lookup"><span data-stu-id="5b637-207">Images created from Managed Disks</span></span>
* <span data-ttu-id="5b637-208">Managed Disks</span><span class="sxs-lookup"><span data-stu-id="5b637-208">Managed Disks</span></span>
* <span data-ttu-id="5b637-209">Applications gérées</span><span class="sxs-lookup"><span data-stu-id="5b637-209">Managed Applications</span></span>
* <span data-ttu-id="5b637-210">Coffre de Services de récupération - également pas déplacement hello calcul, réseau et stockage de ressources associés à font hello Services de récupération de coffre, consultez [limitations de Services de récupération](#recovery-services-limitations).</span><span class="sxs-lookup"><span data-stu-id="5b637-210">Recovery Services vault - also do not move hello Compute, Network, and Storage resources associated with hello Recovery Services vault, see [Recovery Services limitations](#recovery-services-limitations).</span></span>
* <span data-ttu-id="5b637-211">Sécurité</span><span class="sxs-lookup"><span data-stu-id="5b637-211">Security</span></span>
* <span data-ttu-id="5b637-212">Instantanés créés à partir de disques gérés</span><span class="sxs-lookup"><span data-stu-id="5b637-212">Snapshots created from Managed Disks</span></span>
* <span data-ttu-id="5b637-213">StorSimple Device Manager</span><span class="sxs-lookup"><span data-stu-id="5b637-213">StorSimple Device Manager</span></span>
* <span data-ttu-id="5b637-214">Machines virtuelles avec des disques managés</span><span class="sxs-lookup"><span data-stu-id="5b637-214">Virtual Machines with Managed Disks</span></span>
* <span data-ttu-id="5b637-215">Réseaux virtuels (classique) : consultez [Limitations relatives au déploiement classique](#classic-deployment-limitations)</span><span class="sxs-lookup"><span data-stu-id="5b637-215">Virtual Networks (classic) - see [Classic deployment limitations](#classic-deployment-limitations)</span></span>
* <span data-ttu-id="5b637-216">Les machines virtuelles créées à partir de ressources de la Place de marché ne peuvent pas être déplacées entre des abonnements.</span><span class="sxs-lookup"><span data-stu-id="5b637-216">Virtual Machines created from Marketplace resources - cannot be moved across subscriptions.</span></span> <span data-ttu-id="5b637-217">Besoins en ressources toobe a été annulé dans l’abonnement actif de hello et déployé à nouveau dans un nouvel abonnement hello</span><span class="sxs-lookup"><span data-stu-id="5b637-217">Resource needs toobe deprovisioned in hello current subscription and deployed again in hello new subscription</span></span>

## <a name="app-service-limitations"></a><span data-ttu-id="5b637-218">limitations d’App Service</span><span class="sxs-lookup"><span data-stu-id="5b637-218">App Service limitations</span></span>
<span data-ttu-id="5b637-219">Lorsque vous travaillez avec des applications App Service, vous ne pouvez pas déplacer uniquement un plan App Service.</span><span class="sxs-lookup"><span data-stu-id="5b637-219">When working with App Service apps, you cannot move only an App Service plan.</span></span> <span data-ttu-id="5b637-220">applications de Service d’applications toomove, les options disponibles sont :</span><span class="sxs-lookup"><span data-stu-id="5b637-220">toomove App Service apps, your options are:</span></span>

* <span data-ttu-id="5b637-221">Déplacez hello plan App Service et toutes les autres ressources du Service d’applications dans cette ressource groupe tooa nouveau groupe de ressources qui ne possède pas les ressources du Service d’applications.</span><span class="sxs-lookup"><span data-stu-id="5b637-221">Move hello App Service plan and all other App Service resources in that resource group tooa new resource group that does not already have App Service resources.</span></span> <span data-ttu-id="5b637-222">Cette exigence signifie que vous devez déplacer même hello les ressources du Service d’applications qui ne sont pas associés avec hello plan App Service.</span><span class="sxs-lookup"><span data-stu-id="5b637-222">This requirement means you must move even hello App Service resources that are not associated with hello App Service plan.</span></span>
* <span data-ttu-id="5b637-223">Déplacer le groupe de ressources différent tooa hello applications, en conservant tous les plans de Service d’applications dans le groupe de ressources d’origine hello.</span><span class="sxs-lookup"><span data-stu-id="5b637-223">Move hello apps tooa different resource group, but keep all App Service plans in hello original resource group.</span></span>

<span data-ttu-id="5b637-224">Hello du Service d’applications plan n’a pas besoin tooreside dans hello même groupe de ressources en tant qu’application hello pour hello application toofunction correctement.</span><span class="sxs-lookup"><span data-stu-id="5b637-224">hello App Service plan does not need tooreside in hello same resource group as hello app for hello app toofunction correctly.</span></span>

<span data-ttu-id="5b637-225">Par exemple, si votre groupe de ressources contient :</span><span class="sxs-lookup"><span data-stu-id="5b637-225">For example, if your resource group contains:</span></span>

* <span data-ttu-id="5b637-226">**web-a**, qui est associé à **plan-a**</span><span class="sxs-lookup"><span data-stu-id="5b637-226">**web-a** which is associated with **plan-a**</span></span>
* <span data-ttu-id="5b637-227">**web-b**, qui est associé à **plan-b**</span><span class="sxs-lookup"><span data-stu-id="5b637-227">**web-b** which is associated with **plan-b**</span></span>

<span data-ttu-id="5b637-228">Vos options sont :</span><span class="sxs-lookup"><span data-stu-id="5b637-228">Your options are:</span></span>

* <span data-ttu-id="5b637-229">Déplacer **web-a**, **plan-a**, **web-b** et **plan-b**</span><span class="sxs-lookup"><span data-stu-id="5b637-229">Move **web-a**, **plan-a**, **web-b**, and **plan-b**</span></span>
* <span data-ttu-id="5b637-230">Déplacer **web-a** et **web-b**</span><span class="sxs-lookup"><span data-stu-id="5b637-230">Move **web-a** and **web-b**</span></span>
* <span data-ttu-id="5b637-231">Déplacez **web-a**</span><span class="sxs-lookup"><span data-stu-id="5b637-231">Move **web-a**</span></span>
* <span data-ttu-id="5b637-232">Déplacez **web-b**</span><span class="sxs-lookup"><span data-stu-id="5b637-232">Move **web-b**</span></span>

<span data-ttu-id="5b637-233">Toutes les autres combinaisons impliquent l’abandon d’un type de ressource qui ne peut pas être abandonné lors du déplacement d’un plan App Service (n’importe quel type de ressource App Service).</span><span class="sxs-lookup"><span data-stu-id="5b637-233">All other combinations involve leaving behind a resource type that can't be left behind when moving an App Service plan (any type of App Service resource).</span></span>

<span data-ttu-id="5b637-234">Si votre application web réside dans un autre groupe de ressources que son plan de Service d’applications, mais que vous souhaitez toomove les deux tooa nouveau groupe de ressources, vous devez effectuer le déplacement de hello en deux étapes.</span><span class="sxs-lookup"><span data-stu-id="5b637-234">If your web app resides in a different resource group than its App Service plan but you want toomove both tooa new resource group, you must perform hello move in two steps.</span></span> <span data-ttu-id="5b637-235">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="5b637-235">For example:</span></span>

* <span data-ttu-id="5b637-236">**web-a** se trouve dans **web-group**</span><span class="sxs-lookup"><span data-stu-id="5b637-236">**web-a** resides in **web-group**</span></span>
* <span data-ttu-id="5b637-237">**plan-a** se trouve dans **plan-group**</span><span class="sxs-lookup"><span data-stu-id="5b637-237">**plan-a** resides in **plan-group**</span></span>
* <span data-ttu-id="5b637-238">Vous souhaitez **a web** et **un plan** tooreside dans **groupe combinés**</span><span class="sxs-lookup"><span data-stu-id="5b637-238">You want **web-a** and **plan-a** tooreside in **combined-group**</span></span>

<span data-ttu-id="5b637-239">tooaccomplish ce déplacement, effectuer deux opérations distinctes de déplacement Bonjour suivant séquence :</span><span class="sxs-lookup"><span data-stu-id="5b637-239">tooaccomplish this move, perform two separate move operations in hello following sequence:</span></span>

1. <span data-ttu-id="5b637-240">Déplacer hello **a web** trop**groupe de plan**</span><span class="sxs-lookup"><span data-stu-id="5b637-240">Move hello **web-a** too**plan-group**</span></span>
2. <span data-ttu-id="5b637-241">Déplacer **a web** et **un plan** trop**groupe combinés**.</span><span class="sxs-lookup"><span data-stu-id="5b637-241">Move **web-a** and **plan-a** too**combined-group**.</span></span>

<span data-ttu-id="5b637-242">Vous pouvez déplacer un certificat de Service d’application tooa nouveau groupe de ressources ou d’un abonnement sans problème.</span><span class="sxs-lookup"><span data-stu-id="5b637-242">You can move an App Service Certificate tooa new resource group or subscription without any issues.</span></span> <span data-ttu-id="5b637-243">Toutefois, si votre application web inclut un certificat SSL que vous acheté en externe et téléchargé toohello application, vous devez supprimer le certificat hello avant l’application web mobile hello.</span><span class="sxs-lookup"><span data-stu-id="5b637-243">However, if your web app includes an SSL certificate that you purchased externally and uploaded toohello app, you must delete hello certificate before moving hello web app.</span></span> <span data-ttu-id="5b637-244">Par exemple, vous pouvez effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="5b637-244">For example, you can perform hello following steps:</span></span>

1. <span data-ttu-id="5b637-245">Supprimer hello téléchargé certificat hello web app</span><span class="sxs-lookup"><span data-stu-id="5b637-245">Delete hello uploaded certificate from hello web app</span></span>
2. <span data-ttu-id="5b637-246">Déplacez l’application hello web</span><span class="sxs-lookup"><span data-stu-id="5b637-246">Move hello web app</span></span>
3. <span data-ttu-id="5b637-247">Télécharger l’application hello certificat toohello web</span><span class="sxs-lookup"><span data-stu-id="5b637-247">Upload hello certificate toohello web app</span></span>

## <a name="recovery-services-limitations"></a><span data-ttu-id="5b637-248">Limitations de Recovery Services</span><span class="sxs-lookup"><span data-stu-id="5b637-248">Recovery Services limitations</span></span>
<span data-ttu-id="5b637-249">Déplacement n’est pas activé pour le stockage, réseau, ou les ressources de calcul utilisé tooset la récupération d’urgence avec Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="5b637-249">Move is not enabled for Storage, Network, or Compute resources used tooset up disaster recovery with Azure Site Recovery.</span></span>

<span data-ttu-id="5b637-250">Par exemple, supposons que vous avez configuré la réplication de votre compte de stockage local machines tooa (Storage1) et souhaitez hello protégé machine toocome des après basculement tooAzure comme un ordinateur virtuel (VM1) attaché tooa de réseau virtuel (Network1).</span><span class="sxs-lookup"><span data-stu-id="5b637-250">For example, suppose you have set up replication of your on-premises machines tooa storage account (Storage1) and want hello protected machine toocome up after failover tooAzure as a virtual machine (VM1) attached tooa virtual network (Network1).</span></span> <span data-ttu-id="5b637-251">Vous ne pouvez pas déplacer ces ressources Azure - Storage1, VM1, et Network1 - ressources entre les groupes de hello même abonnement ou entre plusieurs abonnements.</span><span class="sxs-lookup"><span data-stu-id="5b637-251">You cannot move any of these Azure resources - Storage1, VM1, and Network1 - across resource groups within hello same subscription or across subscriptions.</span></span>

## <a name="hdinsight-limitations"></a><span data-ttu-id="5b637-252">Limitations de HDInsight</span><span class="sxs-lookup"><span data-stu-id="5b637-252">HDInsight limitations</span></span>

<span data-ttu-id="5b637-253">Vous pouvez déplacer HDInsight clusters tooa nouvel abonnement ou groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="5b637-253">You can move HDInsight clusters tooa new subscription or resource group.</span></span> <span data-ttu-id="5b637-254">Toutefois, vous ne pouvez pas déplacer entre hello abonnements mise en réseau de cluster de HDInsight ressources toohello lié (par exemple, le réseau virtuel de hello, carte réseau ou d’équilibrage de charge).</span><span class="sxs-lookup"><span data-stu-id="5b637-254">However, you cannot move across subscriptions hello networking resources linked toohello HDInsight cluster (such as hello virtual network, NIC, or load balancer).</span></span> <span data-ttu-id="5b637-255">En outre, vous ne pouvez pas déplacer tooa nouveau groupe de ressources une carte réseau qui est la machine virtuelle jointe tooa cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="5b637-255">In addition, you cannot move tooa new resource group a NIC that is attached tooa virtual machine for hello cluster.</span></span>

<span data-ttu-id="5b637-256">Lorsque vous déplacez un HDInsight cluster tooa nouvel abonnement, commencez par déplacer autres ressources (telles que le compte de stockage hello).</span><span class="sxs-lookup"><span data-stu-id="5b637-256">When moving an HDInsight cluster tooa new subscription, first move other resources (like hello storage account).</span></span> <span data-ttu-id="5b637-257">Déplacez ensuite le cluster HDInsight de hello par lui-même.</span><span class="sxs-lookup"><span data-stu-id="5b637-257">Then, move hello HDInsight cluster by itself.</span></span>

## <a name="classic-deployment-limitations"></a><span data-ttu-id="5b637-258">Limitations relatives au déploiement Classic</span><span class="sxs-lookup"><span data-stu-id="5b637-258">Classic deployment limitations</span></span>
<span data-ttu-id="5b637-259">Hello options de déplacement des ressources déployées via le modèle classique de hello diffèrent selon que vous déplacez des ressources hello au sein d’un abonnement ou tooa nouveau.</span><span class="sxs-lookup"><span data-stu-id="5b637-259">hello options for moving resources deployed through hello classic model differ based on whether you are moving hello resources within a subscription or tooa new subscription.</span></span>

### <a name="same-subscription"></a><span data-ttu-id="5b637-260">Même abonnement</span><span class="sxs-lookup"><span data-stu-id="5b637-260">Same subscription</span></span>
<span data-ttu-id="5b637-261">Déplacement de ressources à partir d’un groupe tooanother groupe de ressources au sein de hello même abonnement, hello suivant des restrictions s’appliquent lorsque :</span><span class="sxs-lookup"><span data-stu-id="5b637-261">When moving resources from one resource group tooanother resource group within hello same subscription, hello following restrictions apply:</span></span>

* <span data-ttu-id="5b637-262">Les réseaux virtuels (classiques) ne peuvent pas être déplacés.</span><span class="sxs-lookup"><span data-stu-id="5b637-262">Virtual networks (classic) cannot be moved.</span></span>
* <span data-ttu-id="5b637-263">Machines virtuelles (classiques) doivent être déplacées avec le service cloud hello.</span><span class="sxs-lookup"><span data-stu-id="5b637-263">Virtual machines (classic) must be moved with hello cloud service.</span></span>
* <span data-ttu-id="5b637-264">Service de cloud computing peut uniquement être déplacé lorsque hello déplacement inclut tous ses ordinateurs virtuels.</span><span class="sxs-lookup"><span data-stu-id="5b637-264">Cloud service can only be moved when hello move includes all its virtual machines.</span></span>
* <span data-ttu-id="5b637-265">Un seul service cloud peut être déplacé à la fois.</span><span class="sxs-lookup"><span data-stu-id="5b637-265">Only one cloud service can be moved at a time.</span></span>
* <span data-ttu-id="5b637-266">Un seul compte de stockage (classique) peut être déplacé à la fois.</span><span class="sxs-lookup"><span data-stu-id="5b637-266">Only one storage account (classic) can be moved at a time.</span></span>
* <span data-ttu-id="5b637-267">Compte de stockage (classiques) ne peut pas être déplacé dans hello même opération avec un ordinateur virtuel ou un service cloud.</span><span class="sxs-lookup"><span data-stu-id="5b637-267">Storage account (classic) cannot be moved in hello same operation with a virtual machine or a cloud service.</span></span>

<span data-ttu-id="5b637-268">toomove les ressources classiques tooa nouveau groupe de ressources dans hello même abonnement, utilisez des opérations de déplacement standard hello via hello [portal](#use-portal), [Azure PowerShell](#use-powershell), [CLI d’Azure](#use-azure-cli), ou [API REST](#use-rest-api).</span><span class="sxs-lookup"><span data-stu-id="5b637-268">toomove classic resources tooa new resource group within hello same subscription, use hello standard move operations through hello [portal](#use-portal), [Azure PowerShell](#use-powershell), [Azure CLI](#use-azure-cli), or [REST API](#use-rest-api).</span></span> <span data-ttu-id="5b637-269">Vous utilisez hello les mêmes opérations que vous utilisez pour le déplacement de ressources du Gestionnaire de ressources.</span><span class="sxs-lookup"><span data-stu-id="5b637-269">You use hello same operations as you use for moving Resource Manager resources.</span></span>

### <a name="new-subscription"></a><span data-ttu-id="5b637-270">Nouvel abonnement</span><span class="sxs-lookup"><span data-stu-id="5b637-270">New subscription</span></span>
<span data-ttu-id="5b637-271">Lors du déplacement des ressources tooa un nouvel abonnement, hello suivant des restrictions s’appliquent :</span><span class="sxs-lookup"><span data-stu-id="5b637-271">When moving resources tooa new subscription, hello following restrictions apply:</span></span>

* <span data-ttu-id="5b637-272">Toutes les ressources classiques dans l’abonnement de hello doivent être déplacées dans hello même opération.</span><span class="sxs-lookup"><span data-stu-id="5b637-272">All classic resources in hello subscription must be moved in hello same operation.</span></span>
* <span data-ttu-id="5b637-273">abonnement de Hello cible ne doit pas contenir d’autres ressources classiques.</span><span class="sxs-lookup"><span data-stu-id="5b637-273">hello target subscription must not contain any other classic resources.</span></span>
* <span data-ttu-id="5b637-274">déplacement de Hello ne peut être demandée via une API REST distincts pour les déplacements classiques.</span><span class="sxs-lookup"><span data-stu-id="5b637-274">hello move can only be requested through a separate REST API for classic moves.</span></span> <span data-ttu-id="5b637-275">commandes de déplacement de gestionnaire de ressources standard Hello ne fonctionnent pas lorsque vous déplacez les ressources classiques tooa un nouvel abonnement.</span><span class="sxs-lookup"><span data-stu-id="5b637-275">hello standard Resource Manager move commands do not work when moving classic resources tooa new subscription.</span></span>

<span data-ttu-id="5b637-276">toomove les ressources classiques tooa nouvel abonnement, utilisez hello reste des opérations qui sont des ressources de tooclassic spécifique.</span><span class="sxs-lookup"><span data-stu-id="5b637-276">toomove classic resources tooa new subscription, use hello REST operations that are specific tooclassic resources.</span></span> <span data-ttu-id="5b637-277">toouse REST, effectuez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="5b637-277">toouse REST, perform hello following steps:</span></span>

1. <span data-ttu-id="5b637-278">Vérifiez si l’abonnement source hello peut participer à un abonnement de la déplacer.</span><span class="sxs-lookup"><span data-stu-id="5b637-278">Check if hello source subscription can participate in a cross-subscription move.</span></span> <span data-ttu-id="5b637-279">Utilisez hello l’opération suivante :</span><span class="sxs-lookup"><span data-stu-id="5b637-279">Use hello following operation:</span></span>

  ```HTTP   
  POST https://management.azure.com/subscriptions/{sourceSubscriptionId}/providers/Microsoft.ClassicCompute/validateSubscriptionMoveAvailability?api-version=2016-04-01
  ```

     <span data-ttu-id="5b637-280">Dans le corps de la demande hello, sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="5b637-280">In hello request body, include:</span></span>

  ```json
  {
    "role": "source"
  }
  ```

     <span data-ttu-id="5b637-281">réponse Hello pour l’opération de validation hello est Bonjour suivant le format :</span><span class="sxs-lookup"><span data-stu-id="5b637-281">hello response for hello validation operation is in hello following format:</span></span>

  ```json
  {
    "status": "{status}",
    "reasons": [
      "reason1",
      "reason2"
    ]
  }
  ```

2. <span data-ttu-id="5b637-282">Vérifiez si l’abonnement de destination hello peut participer à un abonnement de la déplacer.</span><span class="sxs-lookup"><span data-stu-id="5b637-282">Check if hello destination subscription can participate in a cross-subscription move.</span></span> <span data-ttu-id="5b637-283">Utilisez hello l’opération suivante :</span><span class="sxs-lookup"><span data-stu-id="5b637-283">Use hello following operation:</span></span>

  ```HTTP
  POST https://management.azure.com/subscriptions/{destinationSubscriptionId}/providers/Microsoft.ClassicCompute/validateSubscriptionMoveAvailability?api-version=2016-04-01
  ```

     <span data-ttu-id="5b637-284">Dans le corps de la demande hello, sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="5b637-284">In hello request body, include:</span></span>

  ```json
  {
    "role": "target"
  }
  ```

     <span data-ttu-id="5b637-285">réponse de Hello est au même format que la validation d’abonnement source hello de hello.</span><span class="sxs-lookup"><span data-stu-id="5b637-285">hello response is in hello same format as hello source subscription validation.</span></span>
3. <span data-ttu-id="5b637-286">Si les deux abonnements ont été validés, déplacez toutes les ressources classiques de l’abonnement de tooanother un abonnement avec hello l’opération suivante :</span><span class="sxs-lookup"><span data-stu-id="5b637-286">If both subscriptions pass validation, move all classic resources from one subscription tooanother subscription with hello following operation:</span></span>

  ```HTTP
  POST https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.ClassicCompute/moveSubscriptionResources?api-version=2016-04-01
  ```

    <span data-ttu-id="5b637-287">Dans le corps de la demande hello, sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="5b637-287">In hello request body, include:</span></span>

  ```json
  {
    "target": "/subscriptions/{target-subscription-id}"
  }
  ```

<span data-ttu-id="5b637-288">opération de Hello peut-être s’exécuter pendant plusieurs minutes.</span><span class="sxs-lookup"><span data-stu-id="5b637-288">hello operation may run for several minutes.</span></span>

## <a name="use-portal"></a><span data-ttu-id="5b637-289">Utilisation du portail</span><span class="sxs-lookup"><span data-stu-id="5b637-289">Use portal</span></span>
<span data-ttu-id="5b637-290">ressources de toomove, sélectionnez le groupe de ressources hello contenant ces ressources, puis sélectionnez hello **déplacer** bouton.</span><span class="sxs-lookup"><span data-stu-id="5b637-290">toomove resources, select hello resource group containing those resources, and then select hello **Move** button.</span></span>

![Déplacer des ressources](./media/resource-group-move-resources/select-move.png)

<span data-ttu-id="5b637-292">Indiquez si vous déplacez hello ressources tooa nouveau groupe de ressources ou d’un nouvel abonnement.</span><span class="sxs-lookup"><span data-stu-id="5b637-292">Select whether you are moving hello resources tooa new resource group or a new subscription.</span></span>

<span data-ttu-id="5b637-293">Sélectionnez hello ressources toomove et le groupe de ressources de destination hello.</span><span class="sxs-lookup"><span data-stu-id="5b637-293">Select hello resources toomove and hello destination resource group.</span></span> <span data-ttu-id="5b637-294">Confirmer que vous devez tooupdate scripts pour ces ressources sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="5b637-294">Acknowledge that you need tooupdate scripts for these resources and select **OK**.</span></span> <span data-ttu-id="5b637-295">Si vous avez sélectionné l’icône d’abonnement hello modifier à l’étape précédente de hello, vous devez également sélectionner l’abonnement de destination hello.</span><span class="sxs-lookup"><span data-stu-id="5b637-295">If you selected hello edit subscription icon in hello previous step, you must also select hello destination subscription.</span></span>

![Sélectionner la destination](./media/resource-group-move-resources/select-destination.png)

<span data-ttu-id="5b637-297">Dans **Notifications**, vous voyez que hello déplacer l’opération est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="5b637-297">In **Notifications**, you see that hello move operation is running.</span></span>

![afficher l’état du déplacement](./media/resource-group-move-resources/show-status.png)

<span data-ttu-id="5b637-299">Lorsqu’il a terminé, vous êtes averti du résultat de hello.</span><span class="sxs-lookup"><span data-stu-id="5b637-299">When it has completed, you are notified of hello result.</span></span>

![afficher les résultats du déplacement](./media/resource-group-move-resources/show-result.png)

## <a name="use-powershell"></a><span data-ttu-id="5b637-301">Utiliser PowerShell</span><span class="sxs-lookup"><span data-stu-id="5b637-301">Use PowerShell</span></span>
<span data-ttu-id="5b637-302">toomove existant groupe de ressources tooanother ressources ou d’un abonnement, utilisez hello `Move-AzureRmResource` commande.</span><span class="sxs-lookup"><span data-stu-id="5b637-302">toomove existing resources tooanother resource group or subscription, use hello `Move-AzureRmResource` command.</span></span>

<span data-ttu-id="5b637-303">Hello le premier exemple montre comment toomove qu’une seule ressource tooa nouveau groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="5b637-303">hello first example shows how toomove one resource tooa new resource group.</span></span>

```powershell
$resource = Get-AzureRmResource -ResourceName ExampleApp -ResourceGroupName OldRG
Move-AzureRmResource -DestinationResourceGroupName NewRG -ResourceId $resource.ResourceId
```

<span data-ttu-id="5b637-304">Hello deuxième exemple montre comment toomove plusieurs ressources tooa nouveau groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="5b637-304">hello second example shows how toomove multiple resources tooa new resource group.</span></span>

```powershell
$webapp = Get-AzureRmResource -ResourceGroupName OldRG -ResourceName ExampleSite
$plan = Get-AzureRmResource -ResourceGroupName OldRG -ResourceName ExamplePlan
Move-AzureRmResource -DestinationResourceGroupName NewRG -ResourceId $webapp.ResourceId, $plan.ResourceId
```

<span data-ttu-id="5b637-305">toomove tooa nouvel abonnement, incluez une valeur pour hello `DestinationSubscriptionId` paramètre.</span><span class="sxs-lookup"><span data-stu-id="5b637-305">toomove tooa new subscription, include a value for hello `DestinationSubscriptionId` parameter.</span></span>

<span data-ttu-id="5b637-306">Vous êtes invité tooconfirm que vous souhaitez toomove hello les ressources spécifiées.</span><span class="sxs-lookup"><span data-stu-id="5b637-306">You are asked tooconfirm that you want toomove hello specified resources.</span></span>

```powershell
Confirm
Are you sure you want toomove these resources toohello resource group
'/subscriptions/{guid}/resourceGroups/newRG' hello resources:

/subscriptions/{guid}/resourceGroups/destinationgroup/providers/Microsoft.Web/serverFarms/exampleplan
/subscriptions/{guid}/resourceGroups/destinationgroup/providers/Microsoft.Web/sites/examplesite
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): y
```

## <a name="use-azure-cli-20"></a><span data-ttu-id="5b637-307">Utiliser Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="5b637-307">Use Azure CLI 2.0</span></span>
<span data-ttu-id="5b637-308">toomove existant groupe de ressources tooanother ressources ou d’un abonnement, utilisez hello `az resource move` commande.</span><span class="sxs-lookup"><span data-stu-id="5b637-308">toomove existing resources tooanother resource group or subscription, use hello `az resource move` command.</span></span> <span data-ttu-id="5b637-309">Fournir des ressources d’hello ID de hello ressources toomove.</span><span class="sxs-lookup"><span data-stu-id="5b637-309">Provide hello resource IDs of hello resources toomove.</span></span> <span data-ttu-id="5b637-310">Vous pouvez obtenir l’ID de ressource par hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="5b637-310">You can get resource IDs with hello following command:</span></span>

```azurecli
az resource show -g sourceGroup -n storagedemo --resource-type "Microsoft.Storage/storageAccounts" --query id
```

<span data-ttu-id="5b637-311">Bonjour à l’exemple suivant montre comment toomove un stockage compte tooa nouveau groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="5b637-311">hello following example shows how toomove a storage account tooa new resource group.</span></span> <span data-ttu-id="5b637-312">Bonjour `--ids` paramètre, fournir une liste séparée par des espaces de hello ressource ID toomove.</span><span class="sxs-lookup"><span data-stu-id="5b637-312">In hello `--ids` parameter, provide a space-separated list of hello resource IDs toomove.</span></span>

```azurecli
az resource move --destination-group newgroup --ids "/subscriptions/{guid}/resourceGroups/sourceGroup/providers/Microsoft.Storage/storageAccounts/storagedemo"
```

<span data-ttu-id="5b637-313">toomove tooa nouvel abonnement, fournissez hello `--destination-subscription-id` paramètre.</span><span class="sxs-lookup"><span data-stu-id="5b637-313">toomove tooa new subscription, provide hello `--destination-subscription-id` parameter.</span></span>

## <a name="use-azure-cli-10"></a><span data-ttu-id="5b637-314">Utiliser Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="5b637-314">Use Azure CLI 1.0</span></span>
<span data-ttu-id="5b637-315">toomove existant groupe de ressources tooanother ressources ou d’un abonnement, utilisez hello `azure resource move` commande.</span><span class="sxs-lookup"><span data-stu-id="5b637-315">toomove existing resources tooanother resource group or subscription, use hello `azure resource move` command.</span></span> <span data-ttu-id="5b637-316">Fournir des ressources d’hello ID de hello ressources toomove.</span><span class="sxs-lookup"><span data-stu-id="5b637-316">Provide hello resource IDs of hello resources toomove.</span></span> <span data-ttu-id="5b637-317">Vous pouvez obtenir l’ID de ressource par hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="5b637-317">You can get resource IDs with hello following command:</span></span>

```azurecli
azure resource list -g sourceGroup --json
```

<span data-ttu-id="5b637-318">Qui renvoie hello suivant le format :</span><span class="sxs-lookup"><span data-stu-id="5b637-318">Which returns hello following format:</span></span>

```azurecli
[
  {
    "id": "/subscriptions/{guid}/resourceGroups/sourceGroup/providers/Microsoft.Storage/storageAccounts/storagedemo",
    "name": "storagedemo",
    "type": "Microsoft.Storage/storageAccounts",
    "location": "southcentralus",
    "tags": {},
    "kind": "Storage",
    "sku": {
      "name": "Standard_RAGRS",
      "tier": "Standard"
    }
  }
]
```

<span data-ttu-id="5b637-319">Bonjour à l’exemple suivant montre comment toomove un stockage compte tooa nouveau groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="5b637-319">hello following example shows how toomove a storage account tooa new resource group.</span></span> <span data-ttu-id="5b637-320">Bonjour `-i` paramètre, fournir une liste séparée par des virgules de hello ressource ID toomove.</span><span class="sxs-lookup"><span data-stu-id="5b637-320">In hello `-i` parameter, provide a comma-separated list of hello resource IDs toomove.</span></span>

```azurecli
azure resource move -i "/subscriptions/{guid}/resourceGroups/sourceGroup/providers/Microsoft.Storage/storageAccounts/storagedemo" -d "destinationGroup"
```

<span data-ttu-id="5b637-321">Vous êtes invité tooconfirm que vous souhaitez toomove hello de la ressource spécifiée.</span><span class="sxs-lookup"><span data-stu-id="5b637-321">You are asked tooconfirm that you want toomove hello specified resource.</span></span>

## <a name="use-rest-api"></a><span data-ttu-id="5b637-322">Avec l’API REST</span><span class="sxs-lookup"><span data-stu-id="5b637-322">Use REST API</span></span>
<span data-ttu-id="5b637-323">groupe de ressources de tooanother ressources toomove existant ou d’un abonnement, exécutez :</span><span class="sxs-lookup"><span data-stu-id="5b637-323">toomove existing resources tooanother resource group or subscription, run:</span></span>

```HTTP
POST https://management.azure.com/subscriptions/{source-subscription-id}/resourcegroups/{source-resource-group-name}/moveResources?api-version={api-version}
```

<span data-ttu-id="5b637-324">Dans le corps de la demande hello, vous spécifiez le groupe de ressources cible hello et hello ressources toomove.</span><span class="sxs-lookup"><span data-stu-id="5b637-324">In hello request body, you specify hello target resource group and hello resources toomove.</span></span> <span data-ttu-id="5b637-325">Pour plus d’informations sur l’opération de déplacement de REST hello, consultez [déplacer des ressources](https://msdn.microsoft.com/library/azure/mt218710.aspx).</span><span class="sxs-lookup"><span data-stu-id="5b637-325">For more information about hello move REST operation, see [Move resources](https://msdn.microsoft.com/library/azure/mt218710.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="5b637-326">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5b637-326">Next steps</span></span>
* <span data-ttu-id="5b637-327">toolearn sur les applets de commande PowerShell pour gérer votre abonnement, consultez [à l’aide de Azure PowerShell avec le Gestionnaire de ressources](powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="5b637-327">toolearn about PowerShell cmdlets for managing your subscription, see [Using Azure PowerShell with Resource Manager](powershell-azure-resource-manager.md).</span></span>
* <span data-ttu-id="5b637-328">toolearn sur les commandes CLI d’Azure pour gérer votre abonnement, consultez [Using hello CLI d’Azure avec le Gestionnaire de ressources](xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="5b637-328">toolearn about Azure CLI commands for managing your subscription, see [Using hello Azure CLI with Resource Manager](xplat-cli-azure-resource-manager.md).</span></span>
* <span data-ttu-id="5b637-329">toolearn sur les fonctionnalités du portail de gestion de votre abonnement, consultez [à l’aide des ressources de toomanage portail Azure hello](resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="5b637-329">toolearn about portal features for managing your subscription, see [Using hello Azure portal toomanage resources](resource-group-portal.md).</span></span>
* <span data-ttu-id="5b637-330">toolearn sur l’application d’une ressource tooyour organisation logique, consultez [à l’aide des balises tooorganize vos ressources](resource-group-using-tags.md).</span><span class="sxs-lookup"><span data-stu-id="5b637-330">toolearn about applying a logical organization tooyour resources, see [Using tags tooorganize your resources](resource-group-using-tags.md).</span></span>
