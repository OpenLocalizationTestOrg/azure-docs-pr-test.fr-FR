---
title: "Déplacer des ressources Azure vers un nouveau groupe de ressources ou abonnement | Microsoft Docs"
description: "Utilisez Azure Resource Manager ou une API REST pour déplacer des ressources vers un nouveau groupe de ressources ou abonnement."
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
ms.openlocfilehash: e138f80e808968ab4bf5c11cfd5fd46fe4a1bcce
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="move-resources-to-new-resource-group-or-subscription"></a><span data-ttu-id="21c0d-103">Déplacer des ressources vers un nouveau groupe de ressource ou un nouvel abonnement</span><span class="sxs-lookup"><span data-stu-id="21c0d-103">Move resources to new resource group or subscription</span></span>
<span data-ttu-id="21c0d-104">Cette rubrique vous montre comment déplacer des ressources vers un nouvel abonnement ou un nouveau groupe de ressources dans le même abonnement.</span><span class="sxs-lookup"><span data-stu-id="21c0d-104">This topic shows you how to move resources to either a new subscription or a new resource group in the same subscription.</span></span> <span data-ttu-id="21c0d-105">Vous pouvez utiliser le portail, PowerShell, Azure CLI ou l’API REST pour déplacer des ressources.</span><span class="sxs-lookup"><span data-stu-id="21c0d-105">You can use the portal, PowerShell, Azure CLI, or the REST API to move resource.</span></span> <span data-ttu-id="21c0d-106">Les opérations de déplacement de cette rubrique sont disponibles sans assistance du support technique Azure.</span><span class="sxs-lookup"><span data-stu-id="21c0d-106">The move operations in this topic are available to you without any assistance from Azure support.</span></span>

<span data-ttu-id="21c0d-107">Lorsque vous déplacez des ressources, le groupe source et le groupe cible sont verrouillés pendant l’opération.</span><span class="sxs-lookup"><span data-stu-id="21c0d-107">When moving resources, both the source group and the target group are locked during the operation.</span></span> <span data-ttu-id="21c0d-108">Les opérations d’écriture et de suppression sont bloquées sur les groupes de ressources tant que le déplacement n’est pas terminé.</span><span class="sxs-lookup"><span data-stu-id="21c0d-108">Write and delete operations are blocked on the resource groups until the move completes.</span></span> <span data-ttu-id="21c0d-109">Ce verrou signifie que vous ne pouvez pas ajouter, mettre à jour ou supprimer des ressources dans les groupes de ressources, mais il ne signifie pas que les ressources sont figées.</span><span class="sxs-lookup"><span data-stu-id="21c0d-109">This lock means you cannot add, update, or delete resources in the resource groups, but it does not mean the resources are frozen.</span></span> <span data-ttu-id="21c0d-110">Par exemple, si vous déplacez un serveur SQL Server et sa base de données vers un nouveau groupe de ressources, une application qui utilise la base de données ne rencontre aucune interruption de service.</span><span class="sxs-lookup"><span data-stu-id="21c0d-110">For example, if you move a SQL Server and its database to a new resource group, an application that uses the database experiences no downtime.</span></span> <span data-ttu-id="21c0d-111">Elle peut toujours lire et écrire dans la base de données.</span><span class="sxs-lookup"><span data-stu-id="21c0d-111">It can still read and write to the database.</span></span>

<span data-ttu-id="21c0d-112">Vous ne pouvez pas modifier l’emplacement de la ressource.</span><span class="sxs-lookup"><span data-stu-id="21c0d-112">You cannot change the location of the resource.</span></span> <span data-ttu-id="21c0d-113">Le déplacement d’une ressource consiste uniquement en sa translation vers un nouveau groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="21c0d-113">Moving a resource only moves it to a new resource group.</span></span> <span data-ttu-id="21c0d-114">Le nouveau groupe de ressources peut présenter à un autre emplacement, mais l’emplacement de la ressource n’est aucunement modifié.</span><span class="sxs-lookup"><span data-stu-id="21c0d-114">The new resource group may have a different location, but that does not change the location of the resource.</span></span>

> [!NOTE]
> <span data-ttu-id="21c0d-115">Cet article décrit le déplacement des ressources dans une offre de compte Azure.</span><span class="sxs-lookup"><span data-stu-id="21c0d-115">This article describes how to move resources within an existing Azure account offering.</span></span> <span data-ttu-id="21c0d-116">Si vous souhaitez en fait modifier votre offre de compte Azure (par exemple, en procédant à une mise à niveau d’une version par paiement à l’utilisation vers une version par prépaiement) tout en continuant à utiliser vos ressources existantes, consultez [Changer d’offre pour votre abonnement Azure](../billing/billing-how-to-switch-azure-offer.md).</span><span class="sxs-lookup"><span data-stu-id="21c0d-116">If you actually want to change your Azure account offering (such as upgrading from pay-as-you-go to pre-pay) while continuing to work with your existing resources, see [Switch your Azure subscription to another offer](../billing/billing-how-to-switch-azure-offer.md).</span></span>
>
>

## <a name="checklist-before-moving-resources"></a><span data-ttu-id="21c0d-117">Liste de contrôle avant le déplacement de ressources</span><span class="sxs-lookup"><span data-stu-id="21c0d-117">Checklist before moving resources</span></span>
<span data-ttu-id="21c0d-118">Plusieurs étapes importantes doivent être effectuées avant de déplacer une ressource.</span><span class="sxs-lookup"><span data-stu-id="21c0d-118">There are some important steps to perform before moving a resource.</span></span> <span data-ttu-id="21c0d-119">Vérifiez ces conditions pour prévenir d'éventuelles erreurs.</span><span class="sxs-lookup"><span data-stu-id="21c0d-119">By verifying these conditions, you can avoid errors.</span></span>

1. <span data-ttu-id="21c0d-120">Les abonnements source et de destination doivent exister dans le même [client Azure Active Directory](../active-directory/active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="21c0d-120">The source and destination subscriptions must exist within the same [Azure Active Directory tenant](../active-directory/active-directory-howto-tenant.md).</span></span> <span data-ttu-id="21c0d-121">Pour vérifier que les deux abonnements ont le même ID client, utilisez Azure PowerShell ou Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="21c0d-121">To check that both subscriptions have the same tenant ID, use Azure PowerShell or Azure CLI.</span></span>

  <span data-ttu-id="21c0d-122">Pour Azure PowerShell, utilisez :</span><span class="sxs-lookup"><span data-stu-id="21c0d-122">For Azure PowerShell, use:</span></span>

  ```powershell
  (Get-AzureRmSubscription -SubscriptionName "Example Subscription").TenantId
  ```

  <span data-ttu-id="21c0d-123">Pour Azure CLI 2.0, utilisez :</span><span class="sxs-lookup"><span data-stu-id="21c0d-123">For Azure CLI 2.0, use:</span></span>

  ```azurecli
  az account show --subscription "Example Subscription" --query tenantId
  ```

  <span data-ttu-id="21c0d-124">Si les ID clients des abonnements source et de destination ne sont pas identiques, vous pouvez essayer de changer l’annuaire de l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="21c0d-124">If the tenant IDs for the source and destination subscriptions are not the same, you can attempt to change the directory for the subscription.</span></span> <span data-ttu-id="21c0d-125">Toutefois, cette option est uniquement disponible pour les administrateurs de service qui sont connectés avec un compte Microsoft (pas un compte de société).</span><span class="sxs-lookup"><span data-stu-id="21c0d-125">However, this option is only available to Service Administrators who are signed in with a Microsoft account (not an organizational account).</span></span> <span data-ttu-id="21c0d-126">Pour essayer de changer l’annuaire, connectez-vous au [portail classique](https://manage.windowsazure.com/) et sélectionnez **Paramètres**, puis l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="21c0d-126">To attempt changing the directory, log in to the [classic portal](https://manage.windowsazure.com/), and select **Settings**, and select the subscription.</span></span> <span data-ttu-id="21c0d-127">Si l’icône **Modifier l’annuaire** est disponible, sélectionnez-la pour modifier l’annuaire Azure Active Directory associé.</span><span class="sxs-lookup"><span data-stu-id="21c0d-127">If the **Edit Directory** icon is available, select it to change the associated Azure Active Directory.</span></span>

  ![Modifier l’annuaire](./media/resource-group-move-resources/edit-directory.png)

  <span data-ttu-id="21c0d-129">Si cette icône n’est pas disponible, vous devez contacter le support pour déplacer les ressources vers un nouveau client.</span><span class="sxs-lookup"><span data-stu-id="21c0d-129">If that icon is not available, you must contact support to move the resources to a new tenant.</span></span>

2. <span data-ttu-id="21c0d-130">Le service doit activer la possibilité de déplacer des ressources.</span><span class="sxs-lookup"><span data-stu-id="21c0d-130">The service must enable the ability to move resources.</span></span> <span data-ttu-id="21c0d-131">Cette rubrique répertorie les services permettant de déplacer des ressources et les services qui ne le permettent pas.</span><span class="sxs-lookup"><span data-stu-id="21c0d-131">This topic lists which services enable moving resources and which services do not enable moving resources.</span></span>
3. <span data-ttu-id="21c0d-132">L’abonnement de destination doit être inscrit pour le fournisseur de la ressource déplacée.</span><span class="sxs-lookup"><span data-stu-id="21c0d-132">The destination subscription must be registered for the resource provider of the resource being moved.</span></span> <span data-ttu-id="21c0d-133">Sinon, vous recevez une erreur indiquant que **l’abonnement n’est pas inscrit pour un type de ressource**.</span><span class="sxs-lookup"><span data-stu-id="21c0d-133">If not, you receive an error stating that the **subscription is not registered for a resource type**.</span></span> <span data-ttu-id="21c0d-134">Vous pouvez rencontrer ce problème lors du déplacement d’une ressource vers un nouvel abonnement qui n’a jamais été utilisé avec ce type de ressource.</span><span class="sxs-lookup"><span data-stu-id="21c0d-134">You might encounter this problem when moving a resource to a new subscription, but that subscription has never been used with that resource type.</span></span> <span data-ttu-id="21c0d-135">Pour découvrir comment vérifier l’état d’inscription et inscrire des fournisseurs de ressources, consultez [Fournisseurs et types de ressources](resource-manager-supported-services.md).</span><span class="sxs-lookup"><span data-stu-id="21c0d-135">To learn how to check the registration status and register resource providers, see [Resource providers and types](resource-manager-supported-services.md).</span></span>

## <a name="when-to-call-support"></a><span data-ttu-id="21c0d-136">Quand appeler le support technique</span><span class="sxs-lookup"><span data-stu-id="21c0d-136">When to call support</span></span>
<span data-ttu-id="21c0d-137">Vous pouvez déplacer la plupart des ressources via les opérations en libre-service présentées dans cette rubrique.</span><span class="sxs-lookup"><span data-stu-id="21c0d-137">You can move most resources through the self-service operations shown in this topic.</span></span> <span data-ttu-id="21c0d-138">Utilisez les opérations en libre-service pour :</span><span class="sxs-lookup"><span data-stu-id="21c0d-138">Use the self-service operations to:</span></span>

* <span data-ttu-id="21c0d-139">Déplacer des ressources Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="21c0d-139">Move Resource Manager resources.</span></span>
* <span data-ttu-id="21c0d-140">Déplacer des ressources classiques conformément aux [limitations du déploiement classique](#classic-deployment-limitations).</span><span class="sxs-lookup"><span data-stu-id="21c0d-140">Move classic resources according to the [classic deployment limitations](#classic-deployment-limitations).</span></span>

<span data-ttu-id="21c0d-141">Appelez le support technique quand vous devez :</span><span class="sxs-lookup"><span data-stu-id="21c0d-141">Call support when you need to:</span></span>

* <span data-ttu-id="21c0d-142">Déplacer vos ressources vers un nouveau compte Azure (et un locataire Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="21c0d-142">Move your resources to a new Azure account (and Azure Active Directory tenant).</span></span>
* <span data-ttu-id="21c0d-143">Déplacer des ressources classiques, mais que vous rencontrez des problèmes avec les limitations.</span><span class="sxs-lookup"><span data-stu-id="21c0d-143">Move classic resources but are having trouble with the limitations.</span></span>

## <a name="services-that-enable-move"></a><span data-ttu-id="21c0d-144">Services permettant le déplacement</span><span class="sxs-lookup"><span data-stu-id="21c0d-144">Services that enable move</span></span>
<span data-ttu-id="21c0d-145">Pour l’instant, les services qui permettent le déplacement vers un nouveau groupe de ressources et un nouvel abonnement sont les suivants :</span><span class="sxs-lookup"><span data-stu-id="21c0d-145">For now, the services that enable moving to both a new resource group and subscription are:</span></span>

* <span data-ttu-id="21c0d-146">API Management</span><span class="sxs-lookup"><span data-stu-id="21c0d-146">API Management</span></span>
* <span data-ttu-id="21c0d-147">Applications App Service (applications web) : consultez [Limitations d’App Service](#app-service-limitations)</span><span class="sxs-lookup"><span data-stu-id="21c0d-147">App Service apps (web apps) - see [App Service limitations](#app-service-limitations)</span></span>
* <span data-ttu-id="21c0d-148">Application Insights</span><span class="sxs-lookup"><span data-stu-id="21c0d-148">Application Insights</span></span>
* <span data-ttu-id="21c0d-149">Automatisation</span><span class="sxs-lookup"><span data-stu-id="21c0d-149">Automation</span></span>
* <span data-ttu-id="21c0d-150">Batch</span><span class="sxs-lookup"><span data-stu-id="21c0d-150">Batch</span></span>
* <span data-ttu-id="21c0d-151">Bing Maps</span><span class="sxs-lookup"><span data-stu-id="21c0d-151">Bing Maps</span></span>
* <span data-ttu-id="21c0d-152">CDN</span><span class="sxs-lookup"><span data-stu-id="21c0d-152">CDN</span></span>
* <span data-ttu-id="21c0d-153">Cloud Services : consultez [Limitations relatives au déploiement Classic](#classic-deployment-limitations)</span><span class="sxs-lookup"><span data-stu-id="21c0d-153">Cloud Services - see [Classic deployment limitations](#classic-deployment-limitations)</span></span>
* <span data-ttu-id="21c0d-154">Cognitive Services</span><span class="sxs-lookup"><span data-stu-id="21c0d-154">Cognitive Services</span></span>
* <span data-ttu-id="21c0d-155">Content Moderator</span><span class="sxs-lookup"><span data-stu-id="21c0d-155">Content Moderator</span></span>
* <span data-ttu-id="21c0d-156">Data Catalog</span><span class="sxs-lookup"><span data-stu-id="21c0d-156">Data Catalog</span></span>
* <span data-ttu-id="21c0d-157">Data Factory</span><span class="sxs-lookup"><span data-stu-id="21c0d-157">Data Factory</span></span>
* <span data-ttu-id="21c0d-158">Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="21c0d-158">Data Lake Analytics</span></span>
* <span data-ttu-id="21c0d-159">Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="21c0d-159">Data Lake Store</span></span>
* <span data-ttu-id="21c0d-160">DNS</span><span class="sxs-lookup"><span data-stu-id="21c0d-160">DNS</span></span>
* <span data-ttu-id="21c0d-161">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="21c0d-161">Azure Cosmos DB</span></span>
* <span data-ttu-id="21c0d-162">Event Hubs</span><span class="sxs-lookup"><span data-stu-id="21c0d-162">Event Hubs</span></span>
* <span data-ttu-id="21c0d-163">Clusters HDInsight - voir [Limitations de HDInsight](#hdinsight-limitations)</span><span class="sxs-lookup"><span data-stu-id="21c0d-163">HDInsight clusters - see [HDInsight limitations](#hdinsight-limitations)</span></span>
* <span data-ttu-id="21c0d-164">IoT Hubs</span><span class="sxs-lookup"><span data-stu-id="21c0d-164">IoT Hubs</span></span>
* <span data-ttu-id="21c0d-165">Key Vault</span><span class="sxs-lookup"><span data-stu-id="21c0d-165">Key Vault</span></span>
* <span data-ttu-id="21c0d-166">Équilibreurs de charge</span><span class="sxs-lookup"><span data-stu-id="21c0d-166">Load Balancers</span></span>
* <span data-ttu-id="21c0d-167">Logic Apps</span><span class="sxs-lookup"><span data-stu-id="21c0d-167">Logic Apps</span></span>
* <span data-ttu-id="21c0d-168">Apprentissage automatique</span><span class="sxs-lookup"><span data-stu-id="21c0d-168">Machine Learning</span></span>
* <span data-ttu-id="21c0d-169">Media Services</span><span class="sxs-lookup"><span data-stu-id="21c0d-169">Media Services</span></span>
* <span data-ttu-id="21c0d-170">Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="21c0d-170">Mobile Engagement</span></span>
* <span data-ttu-id="21c0d-171">Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="21c0d-171">Notification Hubs</span></span>
* <span data-ttu-id="21c0d-172">Operational Insights</span><span class="sxs-lookup"><span data-stu-id="21c0d-172">Operational Insights</span></span>
* <span data-ttu-id="21c0d-173">Operations Management</span><span class="sxs-lookup"><span data-stu-id="21c0d-173">Operations Management</span></span>
* <span data-ttu-id="21c0d-174">Power BI</span><span class="sxs-lookup"><span data-stu-id="21c0d-174">Power BI</span></span>
* <span data-ttu-id="21c0d-175">Cache Redis</span><span class="sxs-lookup"><span data-stu-id="21c0d-175">Redis Cache</span></span>
* <span data-ttu-id="21c0d-176">Scheduler</span><span class="sxs-lookup"><span data-stu-id="21c0d-176">Scheduler</span></span>
* <span data-ttu-id="21c0d-177">Search</span><span class="sxs-lookup"><span data-stu-id="21c0d-177">Search</span></span>
* <span data-ttu-id="21c0d-178">Gestion de serveur</span><span class="sxs-lookup"><span data-stu-id="21c0d-178">Server Management</span></span>
* <span data-ttu-id="21c0d-179">Service Bus</span><span class="sxs-lookup"><span data-stu-id="21c0d-179">Service Bus</span></span>
* <span data-ttu-id="21c0d-180">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="21c0d-180">Service Fabric</span></span>
* <span data-ttu-id="21c0d-181">Storage</span><span class="sxs-lookup"><span data-stu-id="21c0d-181">Storage</span></span>
* <span data-ttu-id="21c0d-182">Storage (classique) : consultez [Limitations relatives au déploiement classique](#classic-deployment-limitations)</span><span class="sxs-lookup"><span data-stu-id="21c0d-182">Storage (classic) - see [Classic deployment limitations](#classic-deployment-limitations)</span></span>
* <span data-ttu-id="21c0d-183">Stream Analytics - Les tâches Stream Analytics ne peuvent pas être déplacées lorsqu’elles sont en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="21c0d-183">Stream Analytics - Stream Analytics jobs cannot be moved when in running state.</span></span>
* <span data-ttu-id="21c0d-184">Serveur de base de données SQL : la base de données et le serveur doivent résider dans le même groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="21c0d-184">SQL Database server - The database and server must reside in the same resource group.</span></span> <span data-ttu-id="21c0d-185">Lorsque vous déplacez un serveur SQL, toutes ses bases de données sont également déplacées.</span><span class="sxs-lookup"><span data-stu-id="21c0d-185">When you move a SQL server, all its databases are also moved.</span></span>
* <span data-ttu-id="21c0d-186">Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="21c0d-186">Traffic Manager</span></span>
* <span data-ttu-id="21c0d-187">Machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="21c0d-187">Virtual Machines</span></span>
* <span data-ttu-id="21c0d-188">Machines virtuelles avec un certificat stocké dans Key Vault : le déplacement vers un nouveau groupe de ressources dans le même abonnement est activé, mais le déplacement entre abonnements n’est pas activé.</span><span class="sxs-lookup"><span data-stu-id="21c0d-188">Virtual Machines with certificate stored in Key Vault - Move to new resource group in same subscription is enabled, but cross subscription move is not enabled.</span></span>
* <span data-ttu-id="21c0d-189">Virtual Machines (classique) : consultez [Limitations relatives au déploiement classique](#classic-deployment-limitations)</span><span class="sxs-lookup"><span data-stu-id="21c0d-189">Virtual Machines (classic) - see [Classic deployment limitations](#classic-deployment-limitations)</span></span>
* <span data-ttu-id="21c0d-190">Jeux de mise à l’échelle de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="21c0d-190">Virtual Machine Scale Sets</span></span>
* <span data-ttu-id="21c0d-191">Réseaux virtuels : actuellement, un réseau virtuel homologué ne peut pas être déplacé tant que l’homologation de réseau virtuel est activée.</span><span class="sxs-lookup"><span data-stu-id="21c0d-191">Virtual Networks - Currently, a peered Virtual Network cannot be moved until VNet peering has been disabled.</span></span> <span data-ttu-id="21c0d-192">Une fois cette dernière désactivée, le réseau virtuel peut être déplacé correctement et l’homologation de réseau virtuel peut être activée.</span><span class="sxs-lookup"><span data-stu-id="21c0d-192">Once disabled, the Virtual Network can be moved successfully and the VNet peering can be enabled.</span></span> <span data-ttu-id="21c0d-193">En outre, un réseau virtuel ne peut pas être déplacé vers un autre abonnement s’il contient un sous-réseau avec des liens de navigation dans les ressources.</span><span class="sxs-lookup"><span data-stu-id="21c0d-193">In addition, a Virtual Network cannot be moved to a different subscription if the Virtual Network contains any subnet with resource navigation links.</span></span> <span data-ttu-id="21c0d-194">Par exemple, un sous-réseau de réseau virtuel dispose d’un lien de navigation dans les ressources lorsqu’une ressource Microsoft.Cache redis est déployée dans ce sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="21c0d-194">For example, a Virtual Network subnet has a resource navigation link when a Microsoft.Cache redis resource is deployed into this subnet.</span></span>
* <span data-ttu-id="21c0d-195">Passerelle VPN</span><span class="sxs-lookup"><span data-stu-id="21c0d-195">VPN Gateway</span></span>


## <a name="services-that-do-not-enable-move"></a><span data-ttu-id="21c0d-196">Services qui ne permettent pas le déplacement</span><span class="sxs-lookup"><span data-stu-id="21c0d-196">Services that do not enable move</span></span>
<span data-ttu-id="21c0d-197">Les services qui ne permettent pas actuellement le déplacement d’une ressource sont les suivants :</span><span class="sxs-lookup"><span data-stu-id="21c0d-197">The services that currently do not enable moving a resource are:</span></span>

* <span data-ttu-id="21c0d-198">Services de domaine AD</span><span class="sxs-lookup"><span data-stu-id="21c0d-198">AD Domain Services</span></span>
* <span data-ttu-id="21c0d-199">Service de contrôle d’intégrité hybride Active Directory</span><span class="sxs-lookup"><span data-stu-id="21c0d-199">AD Hybrid Health Service</span></span>
* <span data-ttu-id="21c0d-200">Application Gateway</span><span class="sxs-lookup"><span data-stu-id="21c0d-200">Application Gateway</span></span>
* <span data-ttu-id="21c0d-201">Groupes à haute disponibilité comprenant des machines virtuelles avec des disques gérés</span><span class="sxs-lookup"><span data-stu-id="21c0d-201">Availability sets with Virtual Machines with Managed Disks</span></span>
* <span data-ttu-id="21c0d-202">BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="21c0d-202">BizTalk Services</span></span>
* <span data-ttu-id="21c0d-203">Service de conteneur</span><span class="sxs-lookup"><span data-stu-id="21c0d-203">Container Service</span></span>
* <span data-ttu-id="21c0d-204">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="21c0d-204">Express Route</span></span>
* <span data-ttu-id="21c0d-205">Laboratoires DevTest : le déplacement vers un nouveau groupe de ressources dans le même abonnement est activé, mais le déplacement entre abonnements n’est pas activé.</span><span class="sxs-lookup"><span data-stu-id="21c0d-205">DevTest Labs - Move to new resource group in same subscription is enabled, but cross subscription move is not enabled.</span></span>
* <span data-ttu-id="21c0d-206">Dynamics LCS</span><span class="sxs-lookup"><span data-stu-id="21c0d-206">Dynamics LCS</span></span>
* <span data-ttu-id="21c0d-207">Images créées à partir de disques gérés</span><span class="sxs-lookup"><span data-stu-id="21c0d-207">Images created from Managed Disks</span></span>
* <span data-ttu-id="21c0d-208">Managed Disks</span><span class="sxs-lookup"><span data-stu-id="21c0d-208">Managed Disks</span></span>
* <span data-ttu-id="21c0d-209">Applications gérées</span><span class="sxs-lookup"><span data-stu-id="21c0d-209">Managed Applications</span></span>
* <span data-ttu-id="21c0d-210">Coffre Recovery Services : par ailleurs, ne déplacez pas les ressources de calcul, de réseau et de stockage associées au coffre Recovery Services. Consultez [Limitations de Recovery Services](#recovery-services-limitations).</span><span class="sxs-lookup"><span data-stu-id="21c0d-210">Recovery Services vault - also do not move the Compute, Network, and Storage resources associated with the Recovery Services vault, see [Recovery Services limitations](#recovery-services-limitations).</span></span>
* <span data-ttu-id="21c0d-211">Sécurité</span><span class="sxs-lookup"><span data-stu-id="21c0d-211">Security</span></span>
* <span data-ttu-id="21c0d-212">Instantanés créés à partir de disques gérés</span><span class="sxs-lookup"><span data-stu-id="21c0d-212">Snapshots created from Managed Disks</span></span>
* <span data-ttu-id="21c0d-213">StorSimple Device Manager</span><span class="sxs-lookup"><span data-stu-id="21c0d-213">StorSimple Device Manager</span></span>
* <span data-ttu-id="21c0d-214">Machines virtuelles avec des disques managés</span><span class="sxs-lookup"><span data-stu-id="21c0d-214">Virtual Machines with Managed Disks</span></span>
* <span data-ttu-id="21c0d-215">Réseaux virtuels (classique) : consultez [Limitations relatives au déploiement classique](#classic-deployment-limitations)</span><span class="sxs-lookup"><span data-stu-id="21c0d-215">Virtual Networks (classic) - see [Classic deployment limitations](#classic-deployment-limitations)</span></span>
* <span data-ttu-id="21c0d-216">Les machines virtuelles créées à partir de ressources de la Place de marché ne peuvent pas être déplacées entre des abonnements.</span><span class="sxs-lookup"><span data-stu-id="21c0d-216">Virtual Machines created from Marketplace resources - cannot be moved across subscriptions.</span></span> <span data-ttu-id="21c0d-217">La ressource doit être déprovisionnée dans l’abonnement actuel et déployée à nouveau dans le nouvel abonnement.</span><span class="sxs-lookup"><span data-stu-id="21c0d-217">Resource needs to be deprovisioned in the current subscription and deployed again in the new subscription</span></span>

## <a name="app-service-limitations"></a><span data-ttu-id="21c0d-218">limitations d’App Service</span><span class="sxs-lookup"><span data-stu-id="21c0d-218">App Service limitations</span></span>
<span data-ttu-id="21c0d-219">Lorsque vous travaillez avec des applications App Service, vous ne pouvez pas déplacer uniquement un plan App Service.</span><span class="sxs-lookup"><span data-stu-id="21c0d-219">When working with App Service apps, you cannot move only an App Service plan.</span></span> <span data-ttu-id="21c0d-220">Pour déplacer des applications App Service, les options disponibles sont :</span><span class="sxs-lookup"><span data-stu-id="21c0d-220">To move App Service apps, your options are:</span></span>

* <span data-ttu-id="21c0d-221">Déplacez le plan App Service et toutes les autres ressources d’App Service dans ce groupe de ressources vers un nouveau groupe de ressources qui ne dispose pas encore des ressources d’App Service.</span><span class="sxs-lookup"><span data-stu-id="21c0d-221">Move the App Service plan and all other App Service resources in that resource group to a new resource group that does not already have App Service resources.</span></span> <span data-ttu-id="21c0d-222">Cette exigence signifie que vous devez déplacer même les ressources d’App Service qui ne sont pas associées au plan App Service.</span><span class="sxs-lookup"><span data-stu-id="21c0d-222">This requirement means you must move even the App Service resources that are not associated with the App Service plan.</span></span>
* <span data-ttu-id="21c0d-223">Déplacer les applications vers un autre groupe de ressources, mais conserver tous les plans App Service dans le groupe de ressources d'origine.</span><span class="sxs-lookup"><span data-stu-id="21c0d-223">Move the apps to a different resource group, but keep all App Service plans in the original resource group.</span></span>

<span data-ttu-id="21c0d-224">Le plan App Service ne doit pas forcément résider dans le même groupe de ressources que l’application pour que cette dernière fonctionne correctement.</span><span class="sxs-lookup"><span data-stu-id="21c0d-224">The App Service plan does not need to reside in the same resource group as the app for the app to function correctly.</span></span>

<span data-ttu-id="21c0d-225">Par exemple, si votre groupe de ressources contient :</span><span class="sxs-lookup"><span data-stu-id="21c0d-225">For example, if your resource group contains:</span></span>

* <span data-ttu-id="21c0d-226">**web-a**, qui est associé à **plan-a**</span><span class="sxs-lookup"><span data-stu-id="21c0d-226">**web-a** which is associated with **plan-a**</span></span>
* <span data-ttu-id="21c0d-227">**web-b**, qui est associé à **plan-b**</span><span class="sxs-lookup"><span data-stu-id="21c0d-227">**web-b** which is associated with **plan-b**</span></span>

<span data-ttu-id="21c0d-228">Vos options sont :</span><span class="sxs-lookup"><span data-stu-id="21c0d-228">Your options are:</span></span>

* <span data-ttu-id="21c0d-229">Déplacer **web-a**, **plan-a**, **web-b** et **plan-b**</span><span class="sxs-lookup"><span data-stu-id="21c0d-229">Move **web-a**, **plan-a**, **web-b**, and **plan-b**</span></span>
* <span data-ttu-id="21c0d-230">Déplacer **web-a** et **web-b**</span><span class="sxs-lookup"><span data-stu-id="21c0d-230">Move **web-a** and **web-b**</span></span>
* <span data-ttu-id="21c0d-231">Déplacez **web-a**</span><span class="sxs-lookup"><span data-stu-id="21c0d-231">Move **web-a**</span></span>
* <span data-ttu-id="21c0d-232">Déplacez **web-b**</span><span class="sxs-lookup"><span data-stu-id="21c0d-232">Move **web-b**</span></span>

<span data-ttu-id="21c0d-233">Toutes les autres combinaisons impliquent l’abandon d’un type de ressource qui ne peut pas être abandonné lors du déplacement d’un plan App Service (n’importe quel type de ressource App Service).</span><span class="sxs-lookup"><span data-stu-id="21c0d-233">All other combinations involve leaving behind a resource type that can't be left behind when moving an App Service plan (any type of App Service resource).</span></span>

<span data-ttu-id="21c0d-234">Si votre application web réside dans un autre groupe de ressources que son plan App Service mais que vous souhaitez déplacer les deux dans un nouveau groupe de ressources, vous devez effectuer le déplacement en deux étapes.</span><span class="sxs-lookup"><span data-stu-id="21c0d-234">If your web app resides in a different resource group than its App Service plan but you want to move both to a new resource group, you must perform the move in two steps.</span></span> <span data-ttu-id="21c0d-235">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="21c0d-235">For example:</span></span>

* <span data-ttu-id="21c0d-236">**web-a** se trouve dans **web-group**</span><span class="sxs-lookup"><span data-stu-id="21c0d-236">**web-a** resides in **web-group**</span></span>
* <span data-ttu-id="21c0d-237">**plan-a** se trouve dans **plan-group**</span><span class="sxs-lookup"><span data-stu-id="21c0d-237">**plan-a** resides in **plan-group**</span></span>
* <span data-ttu-id="21c0d-238">Vous voulez que **web-a** et **plan-a** se trouvent dans **combined-group**</span><span class="sxs-lookup"><span data-stu-id="21c0d-238">You want **web-a** and **plan-a** to reside in **combined-group**</span></span>

<span data-ttu-id="21c0d-239">Pour effectuer ce déplacement, effectuez deux opérations de déplacement distinctes dans l’ordre suivant :</span><span class="sxs-lookup"><span data-stu-id="21c0d-239">To accomplish this move, perform two separate move operations in the following sequence:</span></span>

1. <span data-ttu-id="21c0d-240">Déplacez **web-a** vers **plan-group**</span><span class="sxs-lookup"><span data-stu-id="21c0d-240">Move the **web-a** to **plan-group**</span></span>
2. <span data-ttu-id="21c0d-241">Déplacez **web-a** et **plan-a** vers **combined-group**.</span><span class="sxs-lookup"><span data-stu-id="21c0d-241">Move **web-a** and **plan-a** to **combined-group**.</span></span>

<span data-ttu-id="21c0d-242">Vous pouvez déplacer un certificat App Service vers un nouveau groupe de ressources ou abonnement sans aucun problème.</span><span class="sxs-lookup"><span data-stu-id="21c0d-242">You can move an App Service Certificate to a new resource group or subscription without any issues.</span></span> <span data-ttu-id="21c0d-243">Toutefois, si votre application web inclut un certificat SSL que vous avez acheté en externe et chargé sur l’application, vous devez supprimer le certificat avant de déplacer l’application web.</span><span class="sxs-lookup"><span data-stu-id="21c0d-243">However, if your web app includes an SSL certificate that you purchased externally and uploaded to the app, you must delete the certificate before moving the web app.</span></span> <span data-ttu-id="21c0d-244">Par exemple, vous pouvez effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="21c0d-244">For example, you can perform the following steps:</span></span>

1. <span data-ttu-id="21c0d-245">Supprimer le certificat chargé de l’application web</span><span class="sxs-lookup"><span data-stu-id="21c0d-245">Delete the uploaded certificate from the web app</span></span>
2. <span data-ttu-id="21c0d-246">Déplacer l’application web</span><span class="sxs-lookup"><span data-stu-id="21c0d-246">Move the web app</span></span>
3. <span data-ttu-id="21c0d-247">Charger le certificat sur l’application web</span><span class="sxs-lookup"><span data-stu-id="21c0d-247">Upload the certificate to the web app</span></span>

## <a name="recovery-services-limitations"></a><span data-ttu-id="21c0d-248">Limitations de Recovery Services</span><span class="sxs-lookup"><span data-stu-id="21c0d-248">Recovery Services limitations</span></span>
<span data-ttu-id="21c0d-249">Le déplacement n’est pas possible pour les ressources de stockage, de réseau ou de calcul utilisées pour configurer la récupération d’urgence avec Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="21c0d-249">Move is not enabled for Storage, Network, or Compute resources used to set up disaster recovery with Azure Site Recovery.</span></span>

<span data-ttu-id="21c0d-250">Par exemple, supposons que vous avez configuré la réplication de vos machines locales vers un compte de stockage (Storage1) et que vous souhaitez que la machine protégée apparaisse après le basculement vers Azure comme une machine virtuelle (VM1) connectée à un réseau virtuel (Network1).</span><span class="sxs-lookup"><span data-stu-id="21c0d-250">For example, suppose you have set up replication of your on-premises machines to a storage account (Storage1) and want the protected machine to come up after failover to Azure as a virtual machine (VM1) attached to a virtual network (Network1).</span></span> <span data-ttu-id="21c0d-251">Vous ne pouvez pas déplacer ces ressources Azure (Storage1, VM1 et Network1) sur différents groupes de ressources dans le même abonnement ou sur différents abonnements.</span><span class="sxs-lookup"><span data-stu-id="21c0d-251">You cannot move any of these Azure resources - Storage1, VM1, and Network1 - across resource groups within the same subscription or across subscriptions.</span></span>

## <a name="hdinsight-limitations"></a><span data-ttu-id="21c0d-252">Limitations de HDInsight</span><span class="sxs-lookup"><span data-stu-id="21c0d-252">HDInsight limitations</span></span>

<span data-ttu-id="21c0d-253">Vous pouvez déplacer des clusters HDInsight vers un nouvel abonnement ou groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="21c0d-253">You can move HDInsight clusters to a new subscription or resource group.</span></span> <span data-ttu-id="21c0d-254">Toutefois, vous ne pouvez pas déplacer sur différents abonnements les ressources réseau liées au cluster HDInsight (par exemple le réseau virtuel, une carte réseau ou un équilibrage de charge).</span><span class="sxs-lookup"><span data-stu-id="21c0d-254">However, you cannot move across subscriptions the networking resources linked to the HDInsight cluster (such as the virtual network, NIC, or load balancer).</span></span> <span data-ttu-id="21c0d-255">En outre, vous ne pouvez pas déplacer vers un nouveau groupe de ressources une carte réseau connectée à une machine virtuelle pour le cluster.</span><span class="sxs-lookup"><span data-stu-id="21c0d-255">In addition, you cannot move to a new resource group a NIC that is attached to a virtual machine for the cluster.</span></span>

<span data-ttu-id="21c0d-256">Lorsque vous déplacez un cluster HDInsight vers un nouvel abonnement, déplacez tout d’abord les autres ressources (le compte de stockage, par exemple).</span><span class="sxs-lookup"><span data-stu-id="21c0d-256">When moving an HDInsight cluster to a new subscription, first move other resources (like the storage account).</span></span> <span data-ttu-id="21c0d-257">Puis, déplacez le cluster HDInsight par lui-même.</span><span class="sxs-lookup"><span data-stu-id="21c0d-257">Then, move the HDInsight cluster by itself.</span></span>

## <a name="classic-deployment-limitations"></a><span data-ttu-id="21c0d-258">Limitations relatives au déploiement Classic</span><span class="sxs-lookup"><span data-stu-id="21c0d-258">Classic deployment limitations</span></span>
<span data-ttu-id="21c0d-259">Les options de déplacement des ressources déployées avec le modèle classique diffèrent selon que vous déplaciez les ressources au sein d’un abonnement ou vers un nouvel abonnement.</span><span class="sxs-lookup"><span data-stu-id="21c0d-259">The options for moving resources deployed through the classic model differ based on whether you are moving the resources within a subscription or to a new subscription.</span></span>

### <a name="same-subscription"></a><span data-ttu-id="21c0d-260">Même abonnement</span><span class="sxs-lookup"><span data-stu-id="21c0d-260">Same subscription</span></span>
<span data-ttu-id="21c0d-261">Lors du déplacement de ressources d’un groupe de ressources vers un autre au sein du même abonnement, les restrictions suivantes s’appliquent :</span><span class="sxs-lookup"><span data-stu-id="21c0d-261">When moving resources from one resource group to another resource group within the same subscription, the following restrictions apply:</span></span>

* <span data-ttu-id="21c0d-262">Les réseaux virtuels (classiques) ne peuvent pas être déplacés.</span><span class="sxs-lookup"><span data-stu-id="21c0d-262">Virtual networks (classic) cannot be moved.</span></span>
* <span data-ttu-id="21c0d-263">Les machines virtuelles (classiques) doivent être déplacées avec le service cloud.</span><span class="sxs-lookup"><span data-stu-id="21c0d-263">Virtual machines (classic) must be moved with the cloud service.</span></span>
* <span data-ttu-id="21c0d-264">Le service cloud ne peut être déplacé que lorsque le déplacement comprend toutes ses machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="21c0d-264">Cloud service can only be moved when the move includes all its virtual machines.</span></span>
* <span data-ttu-id="21c0d-265">Un seul service cloud peut être déplacé à la fois.</span><span class="sxs-lookup"><span data-stu-id="21c0d-265">Only one cloud service can be moved at a time.</span></span>
* <span data-ttu-id="21c0d-266">Un seul compte de stockage (classique) peut être déplacé à la fois.</span><span class="sxs-lookup"><span data-stu-id="21c0d-266">Only one storage account (classic) can be moved at a time.</span></span>
* <span data-ttu-id="21c0d-267">Vous ne pouvez pas déplacer un compte de stockage (classique) dans la même opération avec une machine virtuelle ou un service cloud.</span><span class="sxs-lookup"><span data-stu-id="21c0d-267">Storage account (classic) cannot be moved in the same operation with a virtual machine or a cloud service.</span></span>

<span data-ttu-id="21c0d-268">Pour déplacer des ressources classiques vers un nouveau groupe de ressources dans le même abonnement, les opérations de déplacement standard via le [portail](#use-portal), [Azure PowerShell](#use-powershell), [l’interface CLI Azure](#use-azure-cli) ou [l’API REST](#use-rest-api).</span><span class="sxs-lookup"><span data-stu-id="21c0d-268">To move classic resources to a new resource group within the same subscription, use the standard move operations through the [portal](#use-portal), [Azure PowerShell](#use-powershell), [Azure CLI](#use-azure-cli), or [REST API](#use-rest-api).</span></span> <span data-ttu-id="21c0d-269">Vous utilisez les mêmes opérations que vous celles que vous utilisez pour déplacer des ressources Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="21c0d-269">You use the same operations as you use for moving Resource Manager resources.</span></span>

### <a name="new-subscription"></a><span data-ttu-id="21c0d-270">Nouvel abonnement</span><span class="sxs-lookup"><span data-stu-id="21c0d-270">New subscription</span></span>
<span data-ttu-id="21c0d-271">Lors du déplacement de ressources vers un nouvel abonnement, les restrictions suivantes s’appliquent :</span><span class="sxs-lookup"><span data-stu-id="21c0d-271">When moving resources to a new subscription, the following restrictions apply:</span></span>

* <span data-ttu-id="21c0d-272">Toutes les ressources classiques de l’abonnement doivent être déplacées au cours de la même opération.</span><span class="sxs-lookup"><span data-stu-id="21c0d-272">All classic resources in the subscription must be moved in the same operation.</span></span>
* <span data-ttu-id="21c0d-273">L’abonnement cible ne doit pas contenir d’autres ressources classiques.</span><span class="sxs-lookup"><span data-stu-id="21c0d-273">The target subscription must not contain any other classic resources.</span></span>
* <span data-ttu-id="21c0d-274">Le déplacement peut uniquement être demandé par le biais d’une API REST distincte pour les déplacements classiques.</span><span class="sxs-lookup"><span data-stu-id="21c0d-274">The move can only be requested through a separate REST API for classic moves.</span></span> <span data-ttu-id="21c0d-275">Les commandes de déplacement standard de Resource Manager ne fonctionnent pas lors du déplacement de ressources classiques vers un nouvel abonnement.</span><span class="sxs-lookup"><span data-stu-id="21c0d-275">The standard Resource Manager move commands do not work when moving classic resources to a new subscription.</span></span>

<span data-ttu-id="21c0d-276">Pour déplacer des ressources classiques vers un nouvel abonnement, utilisez des opérations REST spécifiques aux ressources classiques.</span><span class="sxs-lookup"><span data-stu-id="21c0d-276">To move classic resources to a new subscription, use the REST operations that are specific to classic resources.</span></span> <span data-ttu-id="21c0d-277">Pour utiliser REST, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="21c0d-277">To use REST, perform the following steps:</span></span>

1. <span data-ttu-id="21c0d-278">Vérifiez si l’abonnement source peut participer à un déplacement entre abonnements.</span><span class="sxs-lookup"><span data-stu-id="21c0d-278">Check if the source subscription can participate in a cross-subscription move.</span></span> <span data-ttu-id="21c0d-279">Utilisez l’opération suivante :</span><span class="sxs-lookup"><span data-stu-id="21c0d-279">Use the following operation:</span></span>

  ```HTTP   
  POST https://management.azure.com/subscriptions/{sourceSubscriptionId}/providers/Microsoft.ClassicCompute/validateSubscriptionMoveAvailability?api-version=2016-04-01
  ```

     <span data-ttu-id="21c0d-280">Dans le corps de la demande, spécifiez :</span><span class="sxs-lookup"><span data-stu-id="21c0d-280">In the request body, include:</span></span>

  ```json
  {
    "role": "source"
  }
  ```

     <span data-ttu-id="21c0d-281">La réponse pour l’opération de validation est au format suivant :</span><span class="sxs-lookup"><span data-stu-id="21c0d-281">The response for the validation operation is in the following format:</span></span>

  ```json
  {
    "status": "{status}",
    "reasons": [
      "reason1",
      "reason2"
    ]
  }
  ```

2. <span data-ttu-id="21c0d-282">Vérifiez si l’abonnement de destination peut participer à un déplacement entre abonnements.</span><span class="sxs-lookup"><span data-stu-id="21c0d-282">Check if the destination subscription can participate in a cross-subscription move.</span></span> <span data-ttu-id="21c0d-283">Utilisez l’opération suivante :</span><span class="sxs-lookup"><span data-stu-id="21c0d-283">Use the following operation:</span></span>

  ```HTTP
  POST https://management.azure.com/subscriptions/{destinationSubscriptionId}/providers/Microsoft.ClassicCompute/validateSubscriptionMoveAvailability?api-version=2016-04-01
  ```

     <span data-ttu-id="21c0d-284">Dans le corps de la demande, spécifiez :</span><span class="sxs-lookup"><span data-stu-id="21c0d-284">In the request body, include:</span></span>

  ```json
  {
    "role": "target"
  }
  ```

     <span data-ttu-id="21c0d-285">La réponse est dans le même format que la validation de l’abonnement source.</span><span class="sxs-lookup"><span data-stu-id="21c0d-285">The response is in the same format as the source subscription validation.</span></span>
3. <span data-ttu-id="21c0d-286">Si les deux abonnements sont validés, déplacez toutes les ressources classiques d’un abonnement à l’autre via l’opération suivante :</span><span class="sxs-lookup"><span data-stu-id="21c0d-286">If both subscriptions pass validation, move all classic resources from one subscription to another subscription with the following operation:</span></span>

  ```HTTP
  POST https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.ClassicCompute/moveSubscriptionResources?api-version=2016-04-01
  ```

    <span data-ttu-id="21c0d-287">Dans le corps de la demande, spécifiez :</span><span class="sxs-lookup"><span data-stu-id="21c0d-287">In the request body, include:</span></span>

  ```json
  {
    "target": "/subscriptions/{target-subscription-id}"
  }
  ```

<span data-ttu-id="21c0d-288">Cette opération peut prendre plusieurs minutes.</span><span class="sxs-lookup"><span data-stu-id="21c0d-288">The operation may run for several minutes.</span></span>

## <a name="use-portal"></a><span data-ttu-id="21c0d-289">Utilisation du portail</span><span class="sxs-lookup"><span data-stu-id="21c0d-289">Use portal</span></span>
<span data-ttu-id="21c0d-290">Pour déplacer des ressources, sélectionnez le groupe de ressources contenant ces ressources, puis sélectionnez le bouton **Déplacer**.</span><span class="sxs-lookup"><span data-stu-id="21c0d-290">To move resources, select the resource group containing those resources, and then select the **Move** button.</span></span>

![Déplacer des ressources](./media/resource-group-move-resources/select-move.png)

<span data-ttu-id="21c0d-292">Indiquez si vous déplacez les ressources vers un nouveau groupe de ressources ou vers un nouvel abonnement.</span><span class="sxs-lookup"><span data-stu-id="21c0d-292">Select whether you are moving the resources to a new resource group or a new subscription.</span></span>

<span data-ttu-id="21c0d-293">Sélectionnez les ressources à déplacer et le groupe de ressources de destination.</span><span class="sxs-lookup"><span data-stu-id="21c0d-293">Select the resources to move and the destination resource group.</span></span> <span data-ttu-id="21c0d-294">Confirmez que vous devez mettre à jour les scripts de ces ressources et sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="21c0d-294">Acknowledge that you need to update scripts for these resources and select **OK**.</span></span> <span data-ttu-id="21c0d-295">Si vous avez sélectionné l’icône Modifier l’abonnement à l’étape précédente, vous devez également sélectionner l’abonnement de destination.</span><span class="sxs-lookup"><span data-stu-id="21c0d-295">If you selected the edit subscription icon in the previous step, you must also select the destination subscription.</span></span>

![Sélectionner la destination](./media/resource-group-move-resources/select-destination.png)

<span data-ttu-id="21c0d-297">Dans **Notifications**, vous voyez que l’opération de déplacement est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="21c0d-297">In **Notifications**, you see that the move operation is running.</span></span>

![afficher l’état du déplacement](./media/resource-group-move-resources/show-status.png)

<span data-ttu-id="21c0d-299">Lorsqu’elle est terminée, vous êtes informé du résultat.</span><span class="sxs-lookup"><span data-stu-id="21c0d-299">When it has completed, you are notified of the result.</span></span>

![afficher les résultats du déplacement](./media/resource-group-move-resources/show-result.png)

## <a name="use-powershell"></a><span data-ttu-id="21c0d-301">Utiliser PowerShell</span><span class="sxs-lookup"><span data-stu-id="21c0d-301">Use PowerShell</span></span>
<span data-ttu-id="21c0d-302">Pour déplacer des ressources existantes vers un autre groupe de ressources ou un autre abonnement, utilisez la commande `Move-AzureRmResource`.</span><span class="sxs-lookup"><span data-stu-id="21c0d-302">To move existing resources to another resource group or subscription, use the `Move-AzureRmResource` command.</span></span>

<span data-ttu-id="21c0d-303">Le premier exemple vous indique comment déplacer une ressource vers un nouveau groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="21c0d-303">The first example shows how to move one resource to a new resource group.</span></span>

```powershell
$resource = Get-AzureRmResource -ResourceName ExampleApp -ResourceGroupName OldRG
Move-AzureRmResource -DestinationResourceGroupName NewRG -ResourceId $resource.ResourceId
```

<span data-ttu-id="21c0d-304">Le second exemple vous indique comment déplacer plusieurs ressources vers un nouveau groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="21c0d-304">The second example shows how to move multiple resources to a new resource group.</span></span>

```powershell
$webapp = Get-AzureRmResource -ResourceGroupName OldRG -ResourceName ExampleSite
$plan = Get-AzureRmResource -ResourceGroupName OldRG -ResourceName ExamplePlan
Move-AzureRmResource -DestinationResourceGroupName NewRG -ResourceId $webapp.ResourceId, $plan.ResourceId
```

<span data-ttu-id="21c0d-305">Pour déplacer des ressources vers un nouvel abonnement, renseignez une valeur pour le paramètre `DestinationSubscriptionId`.</span><span class="sxs-lookup"><span data-stu-id="21c0d-305">To move to a new subscription, include a value for the `DestinationSubscriptionId` parameter.</span></span>

<span data-ttu-id="21c0d-306">Vous devez confirmer que vous souhaitez déplacer les ressources spécifiées.</span><span class="sxs-lookup"><span data-stu-id="21c0d-306">You are asked to confirm that you want to move the specified resources.</span></span>

```powershell
Confirm
Are you sure you want to move these resources to the resource group
'/subscriptions/{guid}/resourceGroups/newRG' the resources:

/subscriptions/{guid}/resourceGroups/destinationgroup/providers/Microsoft.Web/serverFarms/exampleplan
/subscriptions/{guid}/resourceGroups/destinationgroup/providers/Microsoft.Web/sites/examplesite
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): y
```

## <a name="use-azure-cli-20"></a><span data-ttu-id="21c0d-307">Utiliser Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="21c0d-307">Use Azure CLI 2.0</span></span>
<span data-ttu-id="21c0d-308">Pour déplacer des ressources existantes vers un autre groupe de ressources ou un autre abonnement, utilisez la commande `az resource move`.</span><span class="sxs-lookup"><span data-stu-id="21c0d-308">To move existing resources to another resource group or subscription, use the `az resource move` command.</span></span> <span data-ttu-id="21c0d-309">Fournissez les ID des ressources à déplacer.</span><span class="sxs-lookup"><span data-stu-id="21c0d-309">Provide the resource IDs of the resources to move.</span></span> <span data-ttu-id="21c0d-310">Vous pouvez obtenir les ID des ressources avec la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="21c0d-310">You can get resource IDs with the following command:</span></span>

```azurecli
az resource show -g sourceGroup -n storagedemo --resource-type "Microsoft.Storage/storageAccounts" --query id
```

<span data-ttu-id="21c0d-311">L’exemple suivant montre comment déplacer un compte de stockage vers un nouveau groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="21c0d-311">The following example shows how to move a storage account to a new resource group.</span></span> <span data-ttu-id="21c0d-312">Dans le paramètre `--ids`, spécifiez une liste séparée par des espaces des ID des ressources à déplacer.</span><span class="sxs-lookup"><span data-stu-id="21c0d-312">In the `--ids` parameter, provide a space-separated list of the resource IDs to move.</span></span>

```azurecli
az resource move --destination-group newgroup --ids "/subscriptions/{guid}/resourceGroups/sourceGroup/providers/Microsoft.Storage/storageAccounts/storagedemo"
```

<span data-ttu-id="21c0d-313">Pour déplacer des ressources vers un nouvel abonnement, spécifiez le paramètre `--destination-subscription-id`.</span><span class="sxs-lookup"><span data-stu-id="21c0d-313">To move to a new subscription, provide the `--destination-subscription-id` parameter.</span></span>

## <a name="use-azure-cli-10"></a><span data-ttu-id="21c0d-314">Utiliser Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="21c0d-314">Use Azure CLI 1.0</span></span>
<span data-ttu-id="21c0d-315">Pour déplacer des ressources existantes vers un autre groupe de ressources ou un autre abonnement, utilisez la commande `azure resource move`.</span><span class="sxs-lookup"><span data-stu-id="21c0d-315">To move existing resources to another resource group or subscription, use the `azure resource move` command.</span></span> <span data-ttu-id="21c0d-316">Fournissez les ID des ressources à déplacer.</span><span class="sxs-lookup"><span data-stu-id="21c0d-316">Provide the resource IDs of the resources to move.</span></span> <span data-ttu-id="21c0d-317">Vous pouvez obtenir les ID des ressources avec la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="21c0d-317">You can get resource IDs with the following command:</span></span>

```azurecli
azure resource list -g sourceGroup --json
```

<span data-ttu-id="21c0d-318">Elle retourne les informations au format suivant :</span><span class="sxs-lookup"><span data-stu-id="21c0d-318">Which returns the following format:</span></span>

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

<span data-ttu-id="21c0d-319">L’exemple suivant montre comment déplacer un compte de stockage vers un nouveau groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="21c0d-319">The following example shows how to move a storage account to a new resource group.</span></span> <span data-ttu-id="21c0d-320">Dans le paramètre `-i`, spécifiez une liste séparée par des virgules des ID des ressources à déplacer.</span><span class="sxs-lookup"><span data-stu-id="21c0d-320">In the `-i` parameter, provide a comma-separated list of the resource IDs to move.</span></span>

```azurecli
azure resource move -i "/subscriptions/{guid}/resourceGroups/sourceGroup/providers/Microsoft.Storage/storageAccounts/storagedemo" -d "destinationGroup"
```

<span data-ttu-id="21c0d-321">Vous devez confirmer que vous souhaitez déplacer la ressource spécifiée.</span><span class="sxs-lookup"><span data-stu-id="21c0d-321">You are asked to confirm that you want to move the specified resource.</span></span>

## <a name="use-rest-api"></a><span data-ttu-id="21c0d-322">Avec l’API REST</span><span class="sxs-lookup"><span data-stu-id="21c0d-322">Use REST API</span></span>
<span data-ttu-id="21c0d-323">Pour déplacer des ressources existantes vers un autre groupe de ressources ou un autre abonnement, exécutez :</span><span class="sxs-lookup"><span data-stu-id="21c0d-323">To move existing resources to another resource group or subscription, run:</span></span>

```HTTP
POST https://management.azure.com/subscriptions/{source-subscription-id}/resourcegroups/{source-resource-group-name}/moveResources?api-version={api-version}
```

<span data-ttu-id="21c0d-324">Dans le corps de la requête, vous indiquez le groupe de ressources cible et les ressources à déplacer.</span><span class="sxs-lookup"><span data-stu-id="21c0d-324">In the request body, you specify the target resource group and the resources to move.</span></span> <span data-ttu-id="21c0d-325">Pour plus d’informations sur l’opération REST de déplacement, consultez [Déplacer des ressources](https://msdn.microsoft.com/library/azure/mt218710.aspx).</span><span class="sxs-lookup"><span data-stu-id="21c0d-325">For more information about the move REST operation, see [Move resources](https://msdn.microsoft.com/library/azure/mt218710.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="21c0d-326">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="21c0d-326">Next steps</span></span>
* <span data-ttu-id="21c0d-327">Pour plus d’informations sur les applets de commande PowerShell permettant de gérer votre abonnement, consultez [Utilisation d’Azure PowerShell avec Resource Manager](powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="21c0d-327">To learn about PowerShell cmdlets for managing your subscription, see [Using Azure PowerShell with Resource Manager](powershell-azure-resource-manager.md).</span></span>
* <span data-ttu-id="21c0d-328">Pour plus d’informations sur les commandes de l’interface de ligne de commande Azure permettant de gérer votre abonnement, consultez [Utilisation de l’interface de ligne de commande Azure avec Azure Resource Manager](xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="21c0d-328">To learn about Azure CLI commands for managing your subscription, see [Using the Azure CLI with Resource Manager](xplat-cli-azure-resource-manager.md).</span></span>
* <span data-ttu-id="21c0d-329">Pour plus d’informations sur les fonctionnalités du portail permettant de gérer votre abonnement, consultez [Utilisation du Portail Azure pour gérer les ressources](resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="21c0d-329">To learn about portal features for managing your subscription, see [Using the Azure portal to manage resources](resource-group-portal.md).</span></span>
* <span data-ttu-id="21c0d-330">Pour plus d’informations sur l’application d’une organisation logique à vos ressources, consultez [Organisation des ressources Azure à l’aide de balises](resource-group-using-tags.md).</span><span class="sxs-lookup"><span data-stu-id="21c0d-330">To learn about applying a logical organization to your resources, see [Using tags to organize your resources](resource-group-using-tags.md).</span></span>
