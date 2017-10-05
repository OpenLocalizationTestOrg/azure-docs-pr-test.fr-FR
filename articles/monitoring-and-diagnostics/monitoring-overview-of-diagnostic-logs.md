---
title: "Présentation des journaux de diagnostic Azure | Microsoft Docs"
description: "Découvrez les journaux de diagnostic Azure et comment les utiliser pour comprendre les événements qui se produisent au sein d’une ressource Azure."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: fe8887df-b0e6-46f8-b2c0-11994d28e44f
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: johnkem; magoedte
ms.openlocfilehash: d59abde29fc7b73a799e5bf3659b02f824b693de
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="collect-and-consume-log-data-from-your-azure-resources"></a><span data-ttu-id="14b1c-103">Collecter et utiliser des données de journaux à partir de vos ressources Azure</span><span class="sxs-lookup"><span data-stu-id="14b1c-103">Collect and consume log data from your Azure resources</span></span>

## <a name="what-are-azure-resource-diagnostic-logs"></a><span data-ttu-id="14b1c-104">Présentation des journaux de diagnostic des ressources Azure</span><span class="sxs-lookup"><span data-stu-id="14b1c-104">What are Azure resource diagnostic logs</span></span>
<span data-ttu-id="14b1c-105">Les **journaux de diagnostic au niveau des ressources Azure** sont des journaux émis par une ressource, qui fournissent des informations détaillées et riches sur l’utilisation de celle-ci, à intervalles réguliers.</span><span class="sxs-lookup"><span data-stu-id="14b1c-105">**Azure resource-level diagnostic logs** are logs emitted by a resource that provide rich, frequent data about the operation of that resource.</span></span> <span data-ttu-id="14b1c-106">Le contenu de ces journaux varie en fonction du type de ressource.</span><span class="sxs-lookup"><span data-stu-id="14b1c-106">The content of these logs varies by resource type.</span></span> <span data-ttu-id="14b1c-107">Les compteurs de règles du groupe de sécurité réseau et les audits de coffres de clés sont deux exemples de catégories de journaux de ressource.</span><span class="sxs-lookup"><span data-stu-id="14b1c-107">For example, Network Security Group rule counters and Key Vault audits are two categories of resource logs.</span></span>

<span data-ttu-id="14b1c-108">Les journaux de diagnostic des ressources ne fournissent pas les mêmes informations que le [Journal d’activité](monitoring-overview-activity-logs.md).</span><span class="sxs-lookup"><span data-stu-id="14b1c-108">Resource-level diagnostic logs differ from the [Activity Log](monitoring-overview-activity-logs.md).</span></span> <span data-ttu-id="14b1c-109">Le journal d’activité fournit un aperçu des opérations qui ont été effectuées sur les ressources de votre abonnement à l’aide de Resource Manager (par exemple, la création d’une machine virtuelle ou la suppression d’une application logique).</span><span class="sxs-lookup"><span data-stu-id="14b1c-109">The Activity Log provides insight into the operations that were performed on resources in your subscription using Resource Manager, for example, creating a virtual machine or deleting a logic app.</span></span> <span data-ttu-id="14b1c-110">Il s’intéresse aux opérations effectuées au niveau de l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="14b1c-110">The Activity Log is a subscription-level log.</span></span> <span data-ttu-id="14b1c-111">Les journaux de diagnostic des ressources, quant à eux, donnent un aperçu des opérations qui ont été effectuées au sein d’une ressource (par exemple, l’obtention d’un secret à partir d’un coffre de clés).</span><span class="sxs-lookup"><span data-stu-id="14b1c-111">Resource-level diagnostic logs provide insight into operations that were performed within that resource itself, for example, getting a secret from a Key Vault.</span></span>

<span data-ttu-id="14b1c-112">Les journaux de diagnostic des ressources diffèrent également des journaux de diagnostic de système d’exploitation invité.</span><span class="sxs-lookup"><span data-stu-id="14b1c-112">Resource-level diagnostic logs also differ from guest OS-level diagnostic logs.</span></span> <span data-ttu-id="14b1c-113">Les journaux de diagnostic de système d’exploitation invité sont collectés par un agent exécuté sur une machine virtuelle ou un autre type de ressource pris en charge.</span><span class="sxs-lookup"><span data-stu-id="14b1c-113">Guest OS diagnostic logs are those collected by an agent running inside of a virtual machine or other supported resource type.</span></span> <span data-ttu-id="14b1c-114">Les journaux de diagnostic des ressources ne nécessitent aucun agent et capturent les données relatives à la ressource à partir de la plateforme Azure, alors que les journaux de diagnostic du système d’exploitation invité capturent les données provenant du système d’exploitation et des applications exécutées sur la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="14b1c-114">Resource-level diagnostic logs require no agent and capture resource-specific data from the Azure platform itself, while guest OS-level diagnostic logs capture data from the operating system and applications running on a virtual machine.</span></span>

<span data-ttu-id="14b1c-115">Le nouveau type de journal de diagnostic décrit ici n’est cependant pas pris en charge par toutes les ressources.</span><span class="sxs-lookup"><span data-stu-id="14b1c-115">Not all resources support the new type of resource diagnostic logs described here.</span></span> <span data-ttu-id="14b1c-116">Cet article comprend une section répertoriant les types de ressources qui prennent en charge les nouveaux journaux de diagnostic des ressources.</span><span class="sxs-lookup"><span data-stu-id="14b1c-116">This article contains a section listing which resource types support the new resource-level diagnostic logs.</span></span>

![<span data-ttu-id="14b1c-117">Comparaison entre les journaux de diagnostic des ressources et les autres types de journaux</span><span class="sxs-lookup"><span data-stu-id="14b1c-117">Resource diagnostics logs vs other types of logs</span></span> ](./media/monitoring-overview-of-diagnostic-logs/Diagnostics_Logs_vs_other_logs_v5.png)

## <a name="what-you-can-do-with-resource-level-diagnostic-logs"></a><span data-ttu-id="14b1c-118">Comment utiliser les journaux de diagnostic au niveau des ressources</span><span class="sxs-lookup"><span data-stu-id="14b1c-118">What you can do with resource-level diagnostic logs</span></span>
<span data-ttu-id="14b1c-119">Voici ce que vous pouvez faire avec les journaux de diagnostic des ressources :</span><span class="sxs-lookup"><span data-stu-id="14b1c-119">Here are some of the things you can do with resource diagnostic logs:</span></span>

![Positionnement logique des journaux de diagnostic des ressources](./media/monitoring-overview-of-diagnostic-logs/Diagnostics_Logs_Actions.png)


* <span data-ttu-id="14b1c-121">Enregistrez-les dans un [**compte de stockage**](monitoring-archive-diagnostic-logs.md) pour l’audit ou l’inspection manuelle.</span><span class="sxs-lookup"><span data-stu-id="14b1c-121">Save them to a [**Storage Account**](monitoring-archive-diagnostic-logs.md) for auditing or manual inspection.</span></span> <span data-ttu-id="14b1c-122">Vous pouvez spécifier la durée de rétention (en jours) à l’aide des **paramètres de diagnostic des ressources**.</span><span class="sxs-lookup"><span data-stu-id="14b1c-122">You can specify the retention time (in days) using **resource diagnostic settings**.</span></span>
* <span data-ttu-id="14b1c-123">[Diffusez-les en streaming sur **Event Hubs**](monitoring-stream-diagnostic-logs-to-event-hubs.md) pour qu’un service tiers ou une solution d’analyse personnalisée (comme PowerBI) les ingère.</span><span class="sxs-lookup"><span data-stu-id="14b1c-123">[Stream them to **Event Hubs**](monitoring-stream-diagnostic-logs-to-event-hubs.md) for ingestion by a third-party service or custom analytics solution such as PowerBI.</span></span>
* <span data-ttu-id="14b1c-124">Analysez-les avec [OMS Log Analytics](../log-analytics/log-analytics-azure-storage.md)</span><span class="sxs-lookup"><span data-stu-id="14b1c-124">Analyze them with [OMS Log Analytics](../log-analytics/log-analytics-azure-storage.md)</span></span>

<span data-ttu-id="14b1c-125">Vous pouvez utiliser un compte de stockage ou un espace de noms Event Hubs qui n’est pas dans le même abonnement que celui générant des journaux.</span><span class="sxs-lookup"><span data-stu-id="14b1c-125">You can use a storage account or Event Hubs namespace that is not in the same subscription as the one emitting logs.</span></span> <span data-ttu-id="14b1c-126">L’utilisateur qui configure le paramètre doit disposer d’un accès RBAC approprié aux deux abonnements.</span><span class="sxs-lookup"><span data-stu-id="14b1c-126">The user who configures the setting must have the appropriate RBAC access to both subscriptions.</span></span>

## <a name="resource-diagnostic-settings"></a><span data-ttu-id="14b1c-127">Paramètres de diagnostic des ressources</span><span class="sxs-lookup"><span data-stu-id="14b1c-127">Resource diagnostic settings</span></span>
<span data-ttu-id="14b1c-128">Les journaux de diagnostic des ressources non liées au calcul sont configurés à l’aide des paramètres de diagnostic des ressources.</span><span class="sxs-lookup"><span data-stu-id="14b1c-128">Resource diagnostic logs for non-Compute resources are configured using resource diagnostic settings.</span></span> <span data-ttu-id="14b1c-129">**Paramètres de diagnostic des ressources** pour un contrôle des ressources :</span><span class="sxs-lookup"><span data-stu-id="14b1c-129">**Resource diagnostic settings** for a resource control:</span></span>

* <span data-ttu-id="14b1c-130">Où les journaux de diagnostic des ressources et les mesures sont envoyés (compte de stockage, Concentrateurs d’événements et/ou Analyse des journaux OMS).</span><span class="sxs-lookup"><span data-stu-id="14b1c-130">Where resource diagnostic logs and metrics are sent (Storage Account, Event Hubs, and/or OMS Log Analytics).</span></span>
* <span data-ttu-id="14b1c-131">Les catégories de journal envoyées et les données de mesure également envoyées.</span><span class="sxs-lookup"><span data-stu-id="14b1c-131">Which log categories are sent and whether metric data is also sent.</span></span>
* <span data-ttu-id="14b1c-132">La durée pendant laquelle chaque catégorie de journal doit être conservée dans un compte de stockage</span><span class="sxs-lookup"><span data-stu-id="14b1c-132">How long each log category should be retained in a storage account</span></span>
    - <span data-ttu-id="14b1c-133">Une durée de rétention de zéro jour signifie que les journaux sont conservés indéfiniment.</span><span class="sxs-lookup"><span data-stu-id="14b1c-133">A retention of zero days means logs are kept forever.</span></span> <span data-ttu-id="14b1c-134">La valeur peut également être n’importe quel nombre de jours, compris entre 1 et 2147483647.</span><span class="sxs-lookup"><span data-stu-id="14b1c-134">Otherwise, the value can be any number of days between 1 and 2147483647.</span></span>
    - <span data-ttu-id="14b1c-135">Si des stratégies de rétention sont définies, mais que le stockage des journaux dans un compte de stockage est désactivé (par exemple si seules les options Event Hubs ou OMS sont sélectionnées), les stratégies de rétention n’ont aucun effet.</span><span class="sxs-lookup"><span data-stu-id="14b1c-135">If retention policies are set but storing logs in a Storage Account is disabled (for example, if only Event Hubs or OMS options are selected), the retention policies have no effect.</span></span>
    - <span data-ttu-id="14b1c-136">Les stratégies de rétention sont appliquées sur une base quotidienne. Donc, à la fin d’une journée (UTC), les journaux de la journée qui est désormais au-delà de la stratégie de rétention sont supprimés.</span><span class="sxs-lookup"><span data-stu-id="14b1c-136">Retention policies are applied per-day, so at the end of a day (UTC), logs from the day that is now beyond the retention policy are deleted.</span></span> <span data-ttu-id="14b1c-137">Par exemple, si vous aviez une stratégie de rétention d’une journée, au début de la journée d’aujourd’hui les journaux d’avant-hier seront supprimés.</span><span class="sxs-lookup"><span data-stu-id="14b1c-137">For example, if you had a retention policy of one day, at the beginning of the day today the logs from the day before yesterday would be deleted.</span></span>

<span data-ttu-id="14b1c-138">Ces paramètres peuvent être facilement configurés via les paramètres de diagnostics pour une ressource dans le portail Azure, via les commandes Azure PowerShell et de l’interface CLI ou via [Azure Monitor REST API](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span><span class="sxs-lookup"><span data-stu-id="14b1c-138">These settings are easily configured via the diagnostic settings for a resource in the Azure portal, via Azure PowerShell and CLI commands, or via the [Azure Monitor REST API](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span></span>

> [!WARNING]
> <span data-ttu-id="14b1c-139">Mesures et journaux de diagnostic depuis la couche de système d’exploitation invité des ressources Compute (comme les machines virtuelles ou Service Fabric) utilisent [un mécanisme distinct pour la configuration et la sélection des sorties](../azure-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="14b1c-139">Diagnostic logs and metrics for from the guest OS layer of Compute resources (for example, VMs or Service Fabric) use [a separate mechanism for configuration and selection of outputs](../azure-diagnostics.md).</span></span>
>
>

## <a name="how-to-enable-collection-of-resource-diagnostic-logs"></a><span data-ttu-id="14b1c-140">Comment activer la collecte des journaux de diagnostic des ressources</span><span class="sxs-lookup"><span data-stu-id="14b1c-140">How to enable collection of resource diagnostic logs</span></span>
<span data-ttu-id="14b1c-141">La collecte des journaux de diagnostic des ressources peut être activée [dans le cadre de la création d’une ressource dans un modèle Resource Manager](./monitoring-enable-diagnostic-logs-using-template.md) ou après la création d’une ressource via la page d’une ressource dans le portail.</span><span class="sxs-lookup"><span data-stu-id="14b1c-141">Collection of resource diagnostic logs can be enabled [as part of creating a resource in a Resource Manager template](./monitoring-enable-diagnostic-logs-using-template.md) or after a resource is created from that resource's page in the portal.</span></span> <span data-ttu-id="14b1c-142">Vous pouvez également activer la collecte à tout moment via les commandes de l’interface de ligne de commande ou d’Azure PowerShell, ou via l’API REST Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="14b1c-142">You can also enable collection at any point using Azure PowerShell or CLI commands, or using the Azure Monitor REST API.</span></span>

> [!TIP]
> <span data-ttu-id="14b1c-143">Ces instructions peuvent ne pas s’appliquer directement à toutes les ressources.</span><span class="sxs-lookup"><span data-stu-id="14b1c-143">These instructions may not apply directly to every resource.</span></span> <span data-ttu-id="14b1c-144">Consultez les liens de schéma en bas de cette page pour comprendre les étapes spécifiques qui peuvent concerner certains types de ressources.</span><span class="sxs-lookup"><span data-stu-id="14b1c-144">See the schema links at the bottom of this page to understand special steps that may apply to certain resource types.</span></span>
>
>

### <a name="enable-collection-of-resource-diagnostic-logs-in-the-portal"></a><span data-ttu-id="14b1c-145">Activer la collecte des journaux de diagnostic des ressources dans le portail</span><span class="sxs-lookup"><span data-stu-id="14b1c-145">Enable collection of resource diagnostic logs in the portal</span></span>
<span data-ttu-id="14b1c-146">Vous pouvez activer la collecte des journaux de diagnostic des ressources dans le portail Azure après la création d’une ressource, en allant vers une ressource spécifique ou en navigant vers Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="14b1c-146">You can enable collection of resource diagnostic logs in the Azure portal after a resource has been created either by going to a specific resource or by navigating to Azure Monitor.</span></span> <span data-ttu-id="14b1c-147">Pour activer cette option via Azure Monitor :</span><span class="sxs-lookup"><span data-stu-id="14b1c-147">To enable this via Azure Monitor:</span></span>

1. <span data-ttu-id="14b1c-148">Dans le [portail Azure](http://portal.azure.com), naviguez jusqu’à Azure Monitor, puis cliquez sur **Paramètres de diagnostic**</span><span class="sxs-lookup"><span data-stu-id="14b1c-148">In the [Azure portal](http://portal.azure.com), navigate to Azure Monitor and click on **Diagnostic Settings**</span></span>

    ![Section Surveillance d’Azure Monitor](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-blade.png)

2. <span data-ttu-id="14b1c-150">Vous pouvez également filtrer la liste par type ou groupe de ressources, puis cliquez sur la ressource pour laquelle vous souhaitez définir un paramètre de diagnostic.</span><span class="sxs-lookup"><span data-stu-id="14b1c-150">Optionally filter the list by resource group or resource type, then click on the resource for which you would like to set a diagnostic setting.</span></span>

3. <span data-ttu-id="14b1c-151">S’il n’existe aucun paramètre sur la ressource que vous avez sélectionnée, vous êtes invité à créer un paramètre.</span><span class="sxs-lookup"><span data-stu-id="14b1c-151">If no settings exist on the resource you have selected, you are prompted to create a setting.</span></span> <span data-ttu-id="14b1c-152">Cliquez sur « Activer les diagnostics ».</span><span class="sxs-lookup"><span data-stu-id="14b1c-152">Click "Turn on diagnostics."</span></span>

   ![Ajouter le paramètre de diagnostic - aucun paramètre existant](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-none.png)

   <span data-ttu-id="14b1c-154">S’il existe des paramètres existants sur la ressource, vous verrez une liste de paramètres déjà configurés sur cette ressource.</span><span class="sxs-lookup"><span data-stu-id="14b1c-154">If there are existing settings on the resource, you will see a list of settings already configured on this resource.</span></span> <span data-ttu-id="14b1c-155">Cliquez sur « Ajouter le paramètre de diagnostic ».</span><span class="sxs-lookup"><span data-stu-id="14b1c-155">Click "Add diagnostic setting."</span></span>

   ![Ajouter le paramètre de diagnostic - paramètres existants](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-multiple.png)

3. <span data-ttu-id="14b1c-157">Donnez un nom à votre définition, cochez les cases pour chaque destination vers laquelle vous souhaitez envoyer des données et configurez la ressource utilisée pour chaque destination.</span><span class="sxs-lookup"><span data-stu-id="14b1c-157">Give your setting a name, check the boxes for each destination to which you would like to send data, and configure which resource is used for each destination.</span></span> <span data-ttu-id="14b1c-158">Si vous le souhaitez, vous pouvez définir un nombre de jours pour conserver ces journaux à l’aide des curseurs **Rétention (jours)** (uniquement applicable à la destination du compte de stockage).</span><span class="sxs-lookup"><span data-stu-id="14b1c-158">Optionally, set a number of days to retain these logs by using the **Retention (days)** sliders (only applicable to the storage account destination).</span></span> <span data-ttu-id="14b1c-159">Si la valeur zéro est appliquée à la rétention, les journaux sont stockés pour une durée indéfinie.</span><span class="sxs-lookup"><span data-stu-id="14b1c-159">A retention of zero days stores the logs indefinitely.</span></span>
   
   ![Ajouter le paramètre de diagnostic - paramètres existants](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-configure.png)
    
4. <span data-ttu-id="14b1c-161">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="14b1c-161">Click **Save**.</span></span>

<span data-ttu-id="14b1c-162">Après quelques instants, le nouveau paramètre apparaît dans la liste des paramètres de cette ressource et les journaux de diagnostic sont envoyés vers les destinations spécifiées dès la génération de nouvelles données d’événements.</span><span class="sxs-lookup"><span data-stu-id="14b1c-162">After a few moments, the new setting appears in your list of settings for this resource, and diagnostic logs are sent to the specified destinations as soon as new event data is generated.</span></span>

### <a name="enable-collection-of-resource-diagnostic-logs-via-powershell"></a><span data-ttu-id="14b1c-163">Activer la collecte des journaux de diagnostic des ressources via PowerShell</span><span class="sxs-lookup"><span data-stu-id="14b1c-163">Enable collection of resource diagnostic logs via PowerShell</span></span>
<span data-ttu-id="14b1c-164">Pour activer la collecte des journaux de diagnostic des ressources via Azure PowerShell, utilisez les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="14b1c-164">To enable collection of resource diagnostic logs via Azure PowerShell, use the following commands:</span></span>

<span data-ttu-id="14b1c-165">Pour activer le stockage des journaux de diagnostic dans un compte de stockage, utilisez cette commande :</span><span class="sxs-lookup"><span data-stu-id="14b1c-165">To enable storage of diagnostic logs in a storage account, use this command:</span></span>

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -StorageAccountId [your storage account id] -Enabled $true
```

<span data-ttu-id="14b1c-166">L’ID de compte de stockage est l’ID de ressource du compte de stockage auquel vous souhaitez envoyer les journaux.</span><span class="sxs-lookup"><span data-stu-id="14b1c-166">The storage account ID is the resource ID for the storage account to which you want to send the logs.</span></span>

<span data-ttu-id="14b1c-167">Pour activer le streaming des journaux de diagnostic vers un hub d’événements, utilisez cette commande :</span><span class="sxs-lookup"><span data-stu-id="14b1c-167">To enable streaming of diagnostic logs to an event hub, use this command:</span></span>

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -ServiceBusRuleId [your Service Bus rule id] -Enabled $true
```

<span data-ttu-id="14b1c-168">L’ID de règle Service Bus est une chaîne au format suivant : `{Service Bus resource ID}/authorizationrules/{key name}`.</span><span class="sxs-lookup"><span data-stu-id="14b1c-168">The service bus rule ID is a string with this format: `{Service Bus resource ID}/authorizationrules/{key name}`.</span></span>

<span data-ttu-id="14b1c-169">Pour activer l’envoi des journaux de diagnostic vers un espace de travail Log Analytics, utilisez cette commande :</span><span class="sxs-lookup"><span data-stu-id="14b1c-169">To enable sending of diagnostic logs to a Log Analytics workspace, use this command:</span></span>

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -WorkspaceId [resource id of the log analytics workspace] -Enabled $true
```

<span data-ttu-id="14b1c-170">Vous pouvez obtenir l’ID de ressource de votre espace de travail Log Analytics à l’aide de la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="14b1c-170">You can obtain the resource ID of your Log Analytics workspace using the following command:</span></span>

```powershell
(Get-AzureRmOperationalInsightsWorkspace).ResourceId
```

<span data-ttu-id="14b1c-171">Vous pouvez combiner ces paramètres pour activer plusieurs options de sortie.</span><span class="sxs-lookup"><span data-stu-id="14b1c-171">You can combine these parameters to enable multiple output options.</span></span>

### <a name="enable-collection-of-resource-diagnostic-logs-via-cli"></a><span data-ttu-id="14b1c-172">Activer la collecte des journaux de diagnostic des ressources via l’interface de ligne de commande (CLI)</span><span class="sxs-lookup"><span data-stu-id="14b1c-172">Enable collection of resource diagnostic logs via CLI</span></span>
<span data-ttu-id="14b1c-173">Pour activer la collecte des journaux de diagnostic des ressources via Azure CLI, utilisez les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="14b1c-173">To enable collection of resource diagnostic logs via the Azure CLI, use the following commands:</span></span>

<span data-ttu-id="14b1c-174">Pour activer le stockage des journaux de diagnostic dans un compte de stockage, utilisez cette commande :</span><span class="sxs-lookup"><span data-stu-id="14b1c-174">To enable storage of diagnostic logs in a Storage Account, use this command:</span></span>

```azurecli
azure insights diagnostic set --resourceId <resourceId> --storageId <storageAccountId> --enabled true
```

<span data-ttu-id="14b1c-175">L’ID de compte de stockage est l’ID de ressource du compte de stockage auquel vous souhaitez envoyer les journaux.</span><span class="sxs-lookup"><span data-stu-id="14b1c-175">The storage account ID is the resource ID for the storage account to which you want to send the logs.</span></span>

<span data-ttu-id="14b1c-176">Pour activer le streaming des journaux de diagnostic vers un hub d’événements, utilisez cette commande :</span><span class="sxs-lookup"><span data-stu-id="14b1c-176">To enable streaming of diagnostic logs to an event hub, use this command:</span></span>

```azurecli
azure insights diagnostic set --resourceId <resourceId> --serviceBusRuleId <serviceBusRuleId> --enabled true
```

<span data-ttu-id="14b1c-177">L’ID de règle Service Bus est une chaîne au format suivant : `{Service Bus resource ID}/authorizationrules/{key name}`.</span><span class="sxs-lookup"><span data-stu-id="14b1c-177">The service bus rule ID is a string with this format: `{Service Bus resource ID}/authorizationrules/{key name}`.</span></span>

<span data-ttu-id="14b1c-178">Pour activer l’envoi des journaux de diagnostic vers un espace de travail Log Analytics, utilisez cette commande :</span><span class="sxs-lookup"><span data-stu-id="14b1c-178">To enable sending of diagnostic logs to a Log Analytics workspace, use this command:</span></span>

```azurecli
azure insights diagnostic set --resourceId <resourceId> --workspaceId <resource id of the log analytics workspace> --enabled true
```

<span data-ttu-id="14b1c-179">Vous pouvez combiner ces paramètres pour activer plusieurs options de sortie.</span><span class="sxs-lookup"><span data-stu-id="14b1c-179">You can combine these parameters to enable multiple output options.</span></span>

### <a name="enable-collection-of-resource-diagnostic-logs-via-rest-api"></a><span data-ttu-id="14b1c-180">Activer la collecte des journaux de diagnostic des ressources via l’API REST</span><span class="sxs-lookup"><span data-stu-id="14b1c-180">Enable collection of resource diagnostic logs via REST API</span></span>
<span data-ttu-id="14b1c-181">Pour modifier les paramètres de diagnostic à l’aide de Azure Monitor REST API, consultez [ce document](https://msdn.microsoft.com/library/azure/dn931931.aspx).</span><span class="sxs-lookup"><span data-stu-id="14b1c-181">To change diagnostic settings using the Azure Monitor REST API, see [this document](https://msdn.microsoft.com/library/azure/dn931931.aspx).</span></span>

## <a name="manage-resource-diagnostic-settings-in-the-portal"></a><span data-ttu-id="14b1c-182">Gérer les paramètres de diagnostic des ressources dans le portail</span><span class="sxs-lookup"><span data-stu-id="14b1c-182">Manage resource diagnostic settings in the portal</span></span>
<span data-ttu-id="14b1c-183">Assurez-vous que toutes vos ressources sont configurées avec des paramètres de diagnostic.</span><span class="sxs-lookup"><span data-stu-id="14b1c-183">Ensure that all of your resources are set up with diagnostic settings.</span></span> <span data-ttu-id="14b1c-184">Accédez à **Moniteur** dans le portail et ouvrez **Paramètres de diagnostic**.</span><span class="sxs-lookup"><span data-stu-id="14b1c-184">Navigate to **Monitor** in the portal and open **Diagnostic settings**.</span></span>

![Panneau Journaux de diagnostic dans le portail](./media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-nav.png)

<span data-ttu-id="14b1c-186">Vous devrez peut-être cliquer sur « Plus de services » pour trouver la section Moniteur.</span><span class="sxs-lookup"><span data-stu-id="14b1c-186">You may have to click "More services" to find the Monitor section.</span></span>

<span data-ttu-id="14b1c-187">Dans cette section, vous pouvez afficher et filtrer toutes les ressources qui prennent en charge les paramètres de diagnostic pour voir si les diagnostics y sont activés.</span><span class="sxs-lookup"><span data-stu-id="14b1c-187">Here you can view and filter all resources that support diagnostic settings to see if they have diagnostics enabled.</span></span> <span data-ttu-id="14b1c-188">Vous pouvez également explorer pour voir si plusieurs paramètres sont définis sur une ressource et vérifier quel compte de stockage, espace de noms des concentrateurs d’événements et/ou espace de travail Log Analytics vers lesquels sont diffusées les données.</span><span class="sxs-lookup"><span data-stu-id="14b1c-188">You can also drill down to see if multiple settings are set on a resource and check which storage account, Event Hubs namespace, and/or Log Analytics workspace that data are flowing to.</span></span>

![Résultats des Journaux de diagnostic dans le portail](./media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-blade.png)

<span data-ttu-id="14b1c-190">L’ajout d’un paramètre de diagnostic permet d’afficher le panneau Paramètres de diagnostic, où vous pouvez activer, désactiver ou modifier vos paramètres de diagnostic pour la ressource sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="14b1c-190">Adding a diagnostic setting brings up the Diagnostic Settings view, where you can enable, disable, or modify your diagnostic settings for the selected resource.</span></span>

## <a name="supported-services-categories-and-schemas-for-resource-diagnostic-logs"></a><span data-ttu-id="14b1c-191">Services, catégories et schémas pris en charge pour les journaux de diagnostic de ressources</span><span class="sxs-lookup"><span data-stu-id="14b1c-191">Supported services, categories, and schemas for resource diagnostic logs</span></span>
<span data-ttu-id="14b1c-192">[Consultez cet article](monitoring-diagnostic-logs-schema.md) pour obtenir la liste complète des services pris en charge et des catégories de journaux et des schémas utilisés par ces services.</span><span class="sxs-lookup"><span data-stu-id="14b1c-192">[See this article](monitoring-diagnostic-logs-schema.md) for a complete list of supported services and the log categories and schemas used by those services.</span></span>

## <a name="next-steps"></a><span data-ttu-id="14b1c-193">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="14b1c-193">Next steps</span></span>

* [<span data-ttu-id="14b1c-194">Diffuser en continu les journaux de diagnostic des ressources vers **Event Hubs**</span><span class="sxs-lookup"><span data-stu-id="14b1c-194">Stream resource diagnostic logs to **Event Hubs**</span></span>](monitoring-stream-diagnostic-logs-to-event-hubs.md)
* [<span data-ttu-id="14b1c-195">Modifier les paramètres de diagnostic des ressources via l’API REST Azure Monitor</span><span class="sxs-lookup"><span data-stu-id="14b1c-195">Change resource diagnostic settings using the Azure Monitor REST API</span></span>](https://msdn.microsoft.com/library/azure/dn931931.aspx)
* [<span data-ttu-id="14b1c-196">Analyser les journaux du stockage Azure avec Log Analytics</span><span class="sxs-lookup"><span data-stu-id="14b1c-196">Analyze logs from Azure storage with Log Analytics</span></span>](../log-analytics/log-analytics-azure-storage.md)
