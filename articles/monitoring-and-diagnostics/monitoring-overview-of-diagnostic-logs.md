---
title: aaaOverview de journaux de Diagnostic Azure | Documents Microsoft
description: "Découvrez ce que sont les journaux de diagnostic Azure et comment vous pouvez utiliser les événements de toounderstand qui se produisent au sein d’une ressource Azure."
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
ms.openlocfilehash: e38991c540626b4bb5b5b9a995276881ee58f368
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="collect-and-consume-log-data-from-your-azure-resources"></a><span data-ttu-id="6c31e-103">Collecter et utiliser des données de journaux à partir de vos ressources Azure</span><span class="sxs-lookup"><span data-stu-id="6c31e-103">Collect and consume log data from your Azure resources</span></span>

## <a name="what-are-azure-resource-diagnostic-logs"></a><span data-ttu-id="6c31e-104">Présentation des journaux de diagnostic des ressources Azure</span><span class="sxs-lookup"><span data-stu-id="6c31e-104">What are Azure resource diagnostic logs</span></span>
<span data-ttu-id="6c31e-105">**Les journaux de diagnostic au niveau des ressources Azure** journaux émis par une ressource qui fournissent des données riches et fréquentes relatives au fonctionnement de hello de cette ressource.</span><span class="sxs-lookup"><span data-stu-id="6c31e-105">**Azure resource-level diagnostic logs** are logs emitted by a resource that provide rich, frequent data about hello operation of that resource.</span></span> <span data-ttu-id="6c31e-106">le contenu de ces journaux Hello varie selon le type de ressource.</span><span class="sxs-lookup"><span data-stu-id="6c31e-106">hello content of these logs varies by resource type.</span></span> <span data-ttu-id="6c31e-107">Les compteurs de règles du groupe de sécurité réseau et les audits de coffres de clés sont deux exemples de catégories de journaux de ressource.</span><span class="sxs-lookup"><span data-stu-id="6c31e-107">For example, Network Security Group rule counters and Key Vault audits are two categories of resource logs.</span></span>

<span data-ttu-id="6c31e-108">Les journaux de diagnostic au niveau des ressources diffèrent hello [le journal d’activité](monitoring-overview-activity-logs.md).</span><span class="sxs-lookup"><span data-stu-id="6c31e-108">Resource-level diagnostic logs differ from hello [Activity Log](monitoring-overview-activity-logs.md).</span></span> <span data-ttu-id="6c31e-109">Hello journal d’activité fournit des indications sur les opérations de hello qui ont été effectuées sur les ressources dans votre abonnement à l’aide du Gestionnaire de ressources, par exemple, la création d’une machine virtuelle ou la suppression d’une application logique.</span><span class="sxs-lookup"><span data-stu-id="6c31e-109">hello Activity Log provides insight into hello operations that were performed on resources in your subscription using Resource Manager, for example, creating a virtual machine or deleting a logic app.</span></span> <span data-ttu-id="6c31e-110">Hello journal d’activité est un journal au niveau de l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="6c31e-110">hello Activity Log is a subscription-level log.</span></span> <span data-ttu-id="6c31e-111">Les journaux de diagnostic des ressources, quant à eux, donnent un aperçu des opérations qui ont été effectuées au sein d’une ressource (par exemple, l’obtention d’un secret à partir d’un coffre de clés).</span><span class="sxs-lookup"><span data-stu-id="6c31e-111">Resource-level diagnostic logs provide insight into operations that were performed within that resource itself, for example, getting a secret from a Key Vault.</span></span>

<span data-ttu-id="6c31e-112">Les journaux de diagnostic des ressources diffèrent également des journaux de diagnostic de système d’exploitation invité.</span><span class="sxs-lookup"><span data-stu-id="6c31e-112">Resource-level diagnostic logs also differ from guest OS-level diagnostic logs.</span></span> <span data-ttu-id="6c31e-113">Les journaux de diagnostic de système d’exploitation invité sont collectés par un agent exécuté sur une machine virtuelle ou un autre type de ressource pris en charge.</span><span class="sxs-lookup"><span data-stu-id="6c31e-113">Guest OS diagnostic logs are those collected by an agent running inside of a virtual machine or other supported resource type.</span></span> <span data-ttu-id="6c31e-114">Les journaux de diagnostic au niveau des ressources ne nécessitent aucun agent et capturer des données propres à la ressource à partir de hello plateforme Azure lui-même, les journaux de diagnostic au niveau du système d’exploitation invité de capturer les données de système d’exploitation de hello et applications en cours d’exécution sur un ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="6c31e-114">Resource-level diagnostic logs require no agent and capture resource-specific data from hello Azure platform itself, while guest OS-level diagnostic logs capture data from hello operating system and applications running on a virtual machine.</span></span>

<span data-ttu-id="6c31e-115">Pas toutes les ressources prennent en charge hello nouveau type de ressource des journaux de diagnostic décrites ici.</span><span class="sxs-lookup"><span data-stu-id="6c31e-115">Not all resources support hello new type of resource diagnostic logs described here.</span></span> <span data-ttu-id="6c31e-116">Cet article contient une liste de section quels types de ressources prend en charge les nouveaux journaux de diagnostic au niveau des ressources hello.</span><span class="sxs-lookup"><span data-stu-id="6c31e-116">This article contains a section listing which resource types support hello new resource-level diagnostic logs.</span></span>

![<span data-ttu-id="6c31e-117">Comparaison entre les journaux de diagnostic des ressources et les autres types de journaux</span><span class="sxs-lookup"><span data-stu-id="6c31e-117">Resource diagnostics logs vs other types of logs</span></span> ](./media/monitoring-overview-of-diagnostic-logs/Diagnostics_Logs_vs_other_logs_v5.png)

## <a name="what-you-can-do-with-resource-level-diagnostic-logs"></a><span data-ttu-id="6c31e-118">Comment utiliser les journaux de diagnostic au niveau des ressources</span><span class="sxs-lookup"><span data-stu-id="6c31e-118">What you can do with resource-level diagnostic logs</span></span>
<span data-ttu-id="6c31e-119">Voici quelques-unes des choses hello que vous pouvez faire avec les journaux de diagnostic de ressource :</span><span class="sxs-lookup"><span data-stu-id="6c31e-119">Here are some of hello things you can do with resource diagnostic logs:</span></span>

![Positionnement logique des journaux de diagnostic des ressources](./media/monitoring-overview-of-diagnostic-logs/Diagnostics_Logs_Actions.png)


* <span data-ttu-id="6c31e-121">Enregistrer les tooa [ **compte de stockage** ](monitoring-archive-diagnostic-logs.md) pour l’inspection de l’audit ou manuelle.</span><span class="sxs-lookup"><span data-stu-id="6c31e-121">Save them tooa [**Storage Account**](monitoring-archive-diagnostic-logs.md) for auditing or manual inspection.</span></span> <span data-ttu-id="6c31e-122">Vous pouvez spécifier à l’aide de temps (en jours) de rétention hello **les paramètres de diagnostic ressource**.</span><span class="sxs-lookup"><span data-stu-id="6c31e-122">You can specify hello retention time (in days) using **resource diagnostic settings**.</span></span>
* <span data-ttu-id="6c31e-123">[Les flux trop**concentrateurs d’événements** ](monitoring-stream-diagnostic-logs-to-event-hubs.md) pour l’ingestion par un service tiers ou d’une solution personnalisée analytique telles que Power BI.</span><span class="sxs-lookup"><span data-stu-id="6c31e-123">[Stream them too**Event Hubs**](monitoring-stream-diagnostic-logs-to-event-hubs.md) for ingestion by a third-party service or custom analytics solution such as PowerBI.</span></span>
* <span data-ttu-id="6c31e-124">Analysez-les avec [OMS Log Analytics](../log-analytics/log-analytics-azure-storage.md)</span><span class="sxs-lookup"><span data-stu-id="6c31e-124">Analyze them with [OMS Log Analytics](../log-analytics/log-analytics-azure-storage.md)</span></span>

<span data-ttu-id="6c31e-125">Vous pouvez utiliser un compte de stockage ou d’espace de noms de concentrateurs d’événements qui n’est pas hello même abonnement comme une émission journaux hello.</span><span class="sxs-lookup"><span data-stu-id="6c31e-125">You can use a storage account or Event Hubs namespace that is not in hello same subscription as hello one emitting logs.</span></span> <span data-ttu-id="6c31e-126">utilisateur de Hello qui configure hello paramètre doit avoir des abonnements tooboth d’accès appropriés RBAC hello.</span><span class="sxs-lookup"><span data-stu-id="6c31e-126">hello user who configures hello setting must have hello appropriate RBAC access tooboth subscriptions.</span></span>

## <a name="resource-diagnostic-settings"></a><span data-ttu-id="6c31e-127">Paramètres de diagnostic des ressources</span><span class="sxs-lookup"><span data-stu-id="6c31e-127">Resource diagnostic settings</span></span>
<span data-ttu-id="6c31e-128">Les journaux de diagnostic des ressources non liées au calcul sont configurés à l’aide des paramètres de diagnostic des ressources.</span><span class="sxs-lookup"><span data-stu-id="6c31e-128">Resource diagnostic logs for non-Compute resources are configured using resource diagnostic settings.</span></span> <span data-ttu-id="6c31e-129">**Paramètres de diagnostic des ressources** pour un contrôle des ressources :</span><span class="sxs-lookup"><span data-stu-id="6c31e-129">**Resource diagnostic settings** for a resource control:</span></span>

* <span data-ttu-id="6c31e-130">Où les journaux de diagnostic des ressources et les mesures sont envoyés (compte de stockage, Concentrateurs d’événements et/ou Analyse des journaux OMS).</span><span class="sxs-lookup"><span data-stu-id="6c31e-130">Where resource diagnostic logs and metrics are sent (Storage Account, Event Hubs, and/or OMS Log Analytics).</span></span>
* <span data-ttu-id="6c31e-131">Les catégories de journal envoyées et les données de mesure également envoyées.</span><span class="sxs-lookup"><span data-stu-id="6c31e-131">Which log categories are sent and whether metric data is also sent.</span></span>
* <span data-ttu-id="6c31e-132">La durée pendant laquelle chaque catégorie de journal doit être conservée dans un compte de stockage</span><span class="sxs-lookup"><span data-stu-id="6c31e-132">How long each log category should be retained in a storage account</span></span>
    - <span data-ttu-id="6c31e-133">Une durée de rétention de zéro jour signifie que les journaux sont conservés indéfiniment.</span><span class="sxs-lookup"><span data-stu-id="6c31e-133">A retention of zero days means logs are kept forever.</span></span> <span data-ttu-id="6c31e-134">Sinon, valeur de hello peut être n’importe quel nombre de jours compris entre 1 et 2147483647.</span><span class="sxs-lookup"><span data-stu-id="6c31e-134">Otherwise, hello value can be any number of days between 1 and 2147483647.</span></span>
    - <span data-ttu-id="6c31e-135">Si les stratégies de rétention sont définies, mais que le stockage des journaux dans un compte de stockage est désactivé (par exemple, si uniquement les options de concentrateurs d’événements ou OMS sont sélectionnées), les stratégies de rétention hello n’ont aucun effet.</span><span class="sxs-lookup"><span data-stu-id="6c31e-135">If retention policies are set but storing logs in a Storage Account is disabled (for example, if only Event Hubs or OMS options are selected), hello retention policies have no effect.</span></span>
    - <span data-ttu-id="6c31e-136">Stratégies de rétention sont appliquées par jour, donc à hello fin d’une journée (UTC), consigne un jour hello qui est désormais au-delà de la stratégie de rétention hello sont supprimés.</span><span class="sxs-lookup"><span data-stu-id="6c31e-136">Retention policies are applied per-day, so at hello end of a day (UTC), logs from hello day that is now beyond hello retention policy are deleted.</span></span> <span data-ttu-id="6c31e-137">Par exemple, si vous aviez une stratégie de rétention d’un jour, au début de hello du jour hello aujourd'hui hello les journaux à partir de hello avant-hier seraient supprimés.</span><span class="sxs-lookup"><span data-stu-id="6c31e-137">For example, if you had a retention policy of one day, at hello beginning of hello day today hello logs from hello day before yesterday would be deleted.</span></span>

<span data-ttu-id="6c31e-138">Ces paramètres sont configurés facilement via les paramètres de diagnostic hello pour une ressource Bonjour portail Azure, via Azure PowerShell et les commandes CLI ou hello [API REST de Azure analyse](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span><span class="sxs-lookup"><span data-stu-id="6c31e-138">These settings are easily configured via hello diagnostic settings for a resource in hello Azure portal, via Azure PowerShell and CLI commands, or via hello [Azure Monitor REST API](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span></span>

> [!WARNING]
> <span data-ttu-id="6c31e-139">Journaux de diagnostic et les mesures pour à partir de la couche de système d’exploitation invité hello d’utilisation des ressources (par exemple, les machines virtuelles ou Service Fabric) calcul [un mécanisme distinct pour la configuration et la sélection des sorties](../azure-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="6c31e-139">Diagnostic logs and metrics for from hello guest OS layer of Compute resources (for example, VMs or Service Fabric) use [a separate mechanism for configuration and selection of outputs](../azure-diagnostics.md).</span></span>
>
>

## <a name="how-tooenable-collection-of-resource-diagnostic-logs"></a><span data-ttu-id="6c31e-140">La collection tooenable des journaux de diagnostic de ressources</span><span class="sxs-lookup"><span data-stu-id="6c31e-140">How tooenable collection of resource diagnostic logs</span></span>
<span data-ttu-id="6c31e-141">Collecte des journaux de diagnostic de ressource peut être activée [dans le cadre de la création d’une ressource dans un modèle de gestionnaire de ressources](./monitoring-enable-diagnostic-logs-using-template.md) ou après avoir créé une ressource à partir de la page de cette ressource dans le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="6c31e-141">Collection of resource diagnostic logs can be enabled [as part of creating a resource in a Resource Manager template](./monitoring-enable-diagnostic-logs-using-template.md) or after a resource is created from that resource's page in hello portal.</span></span> <span data-ttu-id="6c31e-142">Vous pouvez également activer la collection à tout moment à l’aide de commandes Azure PowerShell ou CLI, ou à l’aide de hello API REST du moniteur Azure.</span><span class="sxs-lookup"><span data-stu-id="6c31e-142">You can also enable collection at any point using Azure PowerShell or CLI commands, or using hello Azure Monitor REST API.</span></span>

> [!TIP]
> <span data-ttu-id="6c31e-143">Ces instructions ne peuvent pas appliquer directement tooevery ressource.</span><span class="sxs-lookup"><span data-stu-id="6c31e-143">These instructions may not apply directly tooevery resource.</span></span> <span data-ttu-id="6c31e-144">Consultez les liens de schéma hello bas hello cette page toounderstand spéciaux comme suit qui peuvent s’appliquer à des types de ressources toocertain.</span><span class="sxs-lookup"><span data-stu-id="6c31e-144">See hello schema links at hello bottom of this page toounderstand special steps that may apply toocertain resource types.</span></span>
>
>

### <a name="enable-collection-of-resource-diagnostic-logs-in-hello-portal"></a><span data-ttu-id="6c31e-145">Activer la collecte des journaux de diagnostic de ressource dans le portail de hello</span><span class="sxs-lookup"><span data-stu-id="6c31e-145">Enable collection of resource diagnostic logs in hello portal</span></span>
<span data-ttu-id="6c31e-146">Vous pouvez activer la collecte des journaux de diagnostic de ressource Bonjour Azure portal après la création d’une ressource va de ressource spécifique tooa ou en naviguant tooAzure moniteur.</span><span class="sxs-lookup"><span data-stu-id="6c31e-146">You can enable collection of resource diagnostic logs in hello Azure portal after a resource has been created either by going tooa specific resource or by navigating tooAzure Monitor.</span></span> <span data-ttu-id="6c31e-147">tooenable cela via le moniteur de Windows Azure :</span><span class="sxs-lookup"><span data-stu-id="6c31e-147">tooenable this via Azure Monitor:</span></span>

1. <span data-ttu-id="6c31e-148">Bonjour [portail Azure](http://portal.azure.com), accédez tooAzure analyse et cliquez sur **les paramètres de Diagnostic**</span><span class="sxs-lookup"><span data-stu-id="6c31e-148">In hello [Azure portal](http://portal.azure.com), navigate tooAzure Monitor and click on **Diagnostic Settings**</span></span>

    ![Section Surveillance d’Azure Monitor](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-blade.png)

2. <span data-ttu-id="6c31e-150">Vous pouvez également filtrer la liste de hello par type de ressource ou le groupe de ressources, puis cliquez sur ressources hello pour laquelle vous aimeriez tooset un paramètre de diagnostic.</span><span class="sxs-lookup"><span data-stu-id="6c31e-150">Optionally filter hello list by resource group or resource type, then click on hello resource for which you would like tooset a diagnostic setting.</span></span>

3. <span data-ttu-id="6c31e-151">Si aucun paramètre n’existe sur la ressource hello que vous avez sélectionné, vous êtes invité à toocreate un paramètre.</span><span class="sxs-lookup"><span data-stu-id="6c31e-151">If no settings exist on hello resource you have selected, you are prompted toocreate a setting.</span></span> <span data-ttu-id="6c31e-152">Cliquez sur « Activer les diagnostics ».</span><span class="sxs-lookup"><span data-stu-id="6c31e-152">Click "Turn on diagnostics."</span></span>

   ![Ajouter le paramètre de diagnostic - aucun paramètre existant](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-none.png)

   <span data-ttu-id="6c31e-154">S’il existe des paramètres existants sur les ressources hello, vous verrez une liste de paramètres déjà configuré sur cette ressource.</span><span class="sxs-lookup"><span data-stu-id="6c31e-154">If there are existing settings on hello resource, you will see a list of settings already configured on this resource.</span></span> <span data-ttu-id="6c31e-155">Cliquez sur « Ajouter le paramètre de diagnostic ».</span><span class="sxs-lookup"><span data-stu-id="6c31e-155">Click "Add diagnostic setting."</span></span>

   ![Ajouter le paramètre de diagnostic - paramètres existants](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-multiple.png)

3. <span data-ttu-id="6c31e-157">Donnez à votre définition d’un nom, hello cases à cocher pour chaque toowhich destination vous toosend données et configurer la ressource qui est utilisée pour chaque destination.</span><span class="sxs-lookup"><span data-stu-id="6c31e-157">Give your setting a name, check hello boxes for each destination toowhich you would like toosend data, and configure which resource is used for each destination.</span></span> <span data-ttu-id="6c31e-158">Si vous le souhaitez, vous pouvez définir un nombre de jours tooretain ces journaux à l’aide de hello **rétention (jours)** curseurs (uniquement applicable toohello compte destination de stockage).</span><span class="sxs-lookup"><span data-stu-id="6c31e-158">Optionally, set a number of days tooretain these logs by using hello **Retention (days)** sliders (only applicable toohello storage account destination).</span></span> <span data-ttu-id="6c31e-159">Une durée de rétention de zéro jours stocke les journaux hello indéfiniment.</span><span class="sxs-lookup"><span data-stu-id="6c31e-159">A retention of zero days stores hello logs indefinitely.</span></span>
   
   ![Ajouter le paramètre de diagnostic - paramètres existants](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-configure.png)
    
4. <span data-ttu-id="6c31e-161">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="6c31e-161">Click **Save**.</span></span>

<span data-ttu-id="6c31e-162">Après quelques instants, hello nouveau paramètre apparaît dans la liste des paramètres pour cette ressource et les journaux de diagnostic sont envoyées toohello spécifié destinations dès que les nouvelles données d’événement sont générées.</span><span class="sxs-lookup"><span data-stu-id="6c31e-162">After a few moments, hello new setting appears in your list of settings for this resource, and diagnostic logs are sent toohello specified destinations as soon as new event data is generated.</span></span>

### <a name="enable-collection-of-resource-diagnostic-logs-via-powershell"></a><span data-ttu-id="6c31e-163">Activer la collecte des journaux de diagnostic des ressources via PowerShell</span><span class="sxs-lookup"><span data-stu-id="6c31e-163">Enable collection of resource diagnostic logs via PowerShell</span></span>
<span data-ttu-id="6c31e-164">collection de tooenable de journaux de diagnostic des ressources via Azure PowerShell, hello utilisation suivant les commandes :</span><span class="sxs-lookup"><span data-stu-id="6c31e-164">tooenable collection of resource diagnostic logs via Azure PowerShell, use hello following commands:</span></span>

<span data-ttu-id="6c31e-165">stockage tooenable de journaux de diagnostic dans un compte de stockage, utilisez cette commande :</span><span class="sxs-lookup"><span data-stu-id="6c31e-165">tooenable storage of diagnostic logs in a storage account, use this command:</span></span>

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -StorageAccountId [your storage account id] -Enabled $true
```

<span data-ttu-id="6c31e-166">stockage Hello ID de compte est hello ID de ressource pour toowhich de compte de stockage hello souhaité toosend hello se connecte.</span><span class="sxs-lookup"><span data-stu-id="6c31e-166">hello storage account ID is hello resource ID for hello storage account toowhich you want toosend hello logs.</span></span>

<span data-ttu-id="6c31e-167">tooenable de diffusion en continu de concentrateur d’événements des journaux de diagnostic tooan, utilisez cette commande :</span><span class="sxs-lookup"><span data-stu-id="6c31e-167">tooenable streaming of diagnostic logs tooan event hub, use this command:</span></span>

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -ServiceBusRuleId [your Service Bus rule id] -Enabled $true
```

<span data-ttu-id="6c31e-168">ID de règle Hello service bus est une chaîne au format suivant : `{Service Bus resource ID}/authorizationrules/{key name}`.</span><span class="sxs-lookup"><span data-stu-id="6c31e-168">hello service bus rule ID is a string with this format: `{Service Bus resource ID}/authorizationrules/{key name}`.</span></span>

<span data-ttu-id="6c31e-169">Utilisez la commande tooenable envoi de journaux de diagnostic tooa Analytique de journal espace de travail :</span><span class="sxs-lookup"><span data-stu-id="6c31e-169">tooenable sending of diagnostic logs tooa Log Analytics workspace, use this command:</span></span>

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -WorkspaceId [resource id of hello log analytics workspace] -Enabled $true
```

<span data-ttu-id="6c31e-170">Vous pouvez obtenir les ID de ressource hello de votre espace de travail Analytique des journaux à l’aide de hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="6c31e-170">You can obtain hello resource ID of your Log Analytics workspace using hello following command:</span></span>

```powershell
(Get-AzureRmOperationalInsightsWorkspace).ResourceId
```

<span data-ttu-id="6c31e-171">Vous pouvez combiner ces paramètres tooenable plusieurs options de sortie.</span><span class="sxs-lookup"><span data-stu-id="6c31e-171">You can combine these parameters tooenable multiple output options.</span></span>

### <a name="enable-collection-of-resource-diagnostic-logs-via-cli"></a><span data-ttu-id="6c31e-172">Activer la collecte des journaux de diagnostic des ressources via l’interface de ligne de commande (CLI)</span><span class="sxs-lookup"><span data-stu-id="6c31e-172">Enable collection of resource diagnostic logs via CLI</span></span>
<span data-ttu-id="6c31e-173">collection tooenable de journaux de diagnostic des ressources via hello CLI d’Azure, utilisez hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="6c31e-173">tooenable collection of resource diagnostic logs via hello Azure CLI, use hello following commands:</span></span>

<span data-ttu-id="6c31e-174">stockage tooenable de journaux de diagnostic dans un compte de stockage, utilisez cette commande :</span><span class="sxs-lookup"><span data-stu-id="6c31e-174">tooenable storage of diagnostic logs in a Storage Account, use this command:</span></span>

```azurecli
azure insights diagnostic set --resourceId <resourceId> --storageId <storageAccountId> --enabled true
```

<span data-ttu-id="6c31e-175">stockage Hello ID de compte est hello ID de ressource pour toowhich de compte de stockage hello souhaité toosend hello se connecte.</span><span class="sxs-lookup"><span data-stu-id="6c31e-175">hello storage account ID is hello resource ID for hello storage account toowhich you want toosend hello logs.</span></span>

<span data-ttu-id="6c31e-176">tooenable de diffusion en continu de concentrateur d’événements des journaux de diagnostic tooan, utilisez cette commande :</span><span class="sxs-lookup"><span data-stu-id="6c31e-176">tooenable streaming of diagnostic logs tooan event hub, use this command:</span></span>

```azurecli
azure insights diagnostic set --resourceId <resourceId> --serviceBusRuleId <serviceBusRuleId> --enabled true
```

<span data-ttu-id="6c31e-177">ID de règle Hello service bus est une chaîne au format suivant : `{Service Bus resource ID}/authorizationrules/{key name}`.</span><span class="sxs-lookup"><span data-stu-id="6c31e-177">hello service bus rule ID is a string with this format: `{Service Bus resource ID}/authorizationrules/{key name}`.</span></span>

<span data-ttu-id="6c31e-178">Utilisez la commande tooenable envoi de journaux de diagnostic tooa Analytique de journal espace de travail :</span><span class="sxs-lookup"><span data-stu-id="6c31e-178">tooenable sending of diagnostic logs tooa Log Analytics workspace, use this command:</span></span>

```azurecli
azure insights diagnostic set --resourceId <resourceId> --workspaceId <resource id of hello log analytics workspace> --enabled true
```

<span data-ttu-id="6c31e-179">Vous pouvez combiner ces paramètres tooenable plusieurs options de sortie.</span><span class="sxs-lookup"><span data-stu-id="6c31e-179">You can combine these parameters tooenable multiple output options.</span></span>

### <a name="enable-collection-of-resource-diagnostic-logs-via-rest-api"></a><span data-ttu-id="6c31e-180">Activer la collecte des journaux de diagnostic des ressources via l’API REST</span><span class="sxs-lookup"><span data-stu-id="6c31e-180">Enable collection of resource diagnostic logs via REST API</span></span>
<span data-ttu-id="6c31e-181">les paramètres de diagnostic toochange à l’aide de hello API REST de moniteur Azure, consultez [ce document](https://msdn.microsoft.com/library/azure/dn931931.aspx).</span><span class="sxs-lookup"><span data-stu-id="6c31e-181">toochange diagnostic settings using hello Azure Monitor REST API, see [this document](https://msdn.microsoft.com/library/azure/dn931931.aspx).</span></span>

## <a name="manage-resource-diagnostic-settings-in-hello-portal"></a><span data-ttu-id="6c31e-182">Gérer les paramètres de diagnostic des ressources dans le portail de hello</span><span class="sxs-lookup"><span data-stu-id="6c31e-182">Manage resource diagnostic settings in hello portal</span></span>
<span data-ttu-id="6c31e-183">Assurez-vous que toutes vos ressources sont configurées avec des paramètres de diagnostic.</span><span class="sxs-lookup"><span data-stu-id="6c31e-183">Ensure that all of your resources are set up with diagnostic settings.</span></span> <span data-ttu-id="6c31e-184">Accédez trop**moniteur** Bonjour portail et ouvrez **les paramètres de Diagnostic**.</span><span class="sxs-lookup"><span data-stu-id="6c31e-184">Navigate too**Monitor** in hello portal and open **Diagnostic settings**.</span></span>

![Diagnostic lame de journaux dans le portail de hello](./media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-nav.png)

<span data-ttu-id="6c31e-186">Vous avez peut-être tooclick section d’analyse « Services plus » toofind hello.</span><span class="sxs-lookup"><span data-stu-id="6c31e-186">You may have tooclick "More services" toofind hello Monitor section.</span></span>

<span data-ttu-id="6c31e-187">Ici, vous pouvez afficher et filtrer toutes les ressources qui prennent en charge les paramètres de diagnostic toosee si elles les diagnostics sont activés.</span><span class="sxs-lookup"><span data-stu-id="6c31e-187">Here you can view and filter all resources that support diagnostic settings toosee if they have diagnostics enabled.</span></span> <span data-ttu-id="6c31e-188">Vous pouvez également Explorer toosee si plusieurs paramètres sont définies sur une ressource et vérifiez quel compte de stockage, espace de noms de concentrateurs d’événements et/ou espace de travail Analytique de journal qui passent des données à.</span><span class="sxs-lookup"><span data-stu-id="6c31e-188">You can also drill down toosee if multiple settings are set on a resource and check which storage account, Event Hubs namespace, and/or Log Analytics workspace that data are flowing to.</span></span>

![Résultats des Journaux de diagnostic dans le portail](./media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-blade.png)

<span data-ttu-id="6c31e-190">Ajout de qu'un paramètre de diagnostic affiche hello afficher les paramètres de Diagnostic, où vous pouvez activer, désactiver ou modifier vos paramètres de diagnostic pour hello la ressource sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="6c31e-190">Adding a diagnostic setting brings up hello Diagnostic Settings view, where you can enable, disable, or modify your diagnostic settings for hello selected resource.</span></span>

## <a name="supported-services-categories-and-schemas-for-resource-diagnostic-logs"></a><span data-ttu-id="6c31e-191">Services, catégories et schémas pris en charge pour les journaux de diagnostic de ressources</span><span class="sxs-lookup"><span data-stu-id="6c31e-191">Supported services, categories, and schemas for resource diagnostic logs</span></span>
<span data-ttu-id="6c31e-192">[Consultez l’article](monitoring-diagnostic-logs-schema.md) pour une liste complète des services pris en charge et les catégories du journal hello et les schémas utilisés par ces services.</span><span class="sxs-lookup"><span data-stu-id="6c31e-192">[See this article](monitoring-diagnostic-logs-schema.md) for a complete list of supported services and hello log categories and schemas used by those services.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6c31e-193">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6c31e-193">Next steps</span></span>

* [<span data-ttu-id="6c31e-194">Flux des journaux de diagnostic de ressource trop**concentrateurs d’événements**</span><span class="sxs-lookup"><span data-stu-id="6c31e-194">Stream resource diagnostic logs too**Event Hubs**</span></span>](monitoring-stream-diagnostic-logs-to-event-hubs.md)
* [<span data-ttu-id="6c31e-195">Modifier les paramètres de diagnostic de ressources à l’aide de hello API REST du moniteur de Azure</span><span class="sxs-lookup"><span data-stu-id="6c31e-195">Change resource diagnostic settings using hello Azure Monitor REST API</span></span>](https://msdn.microsoft.com/library/azure/dn931931.aspx)
* [<span data-ttu-id="6c31e-196">Analyser les journaux du stockage Azure avec Log Analytics</span><span class="sxs-lookup"><span data-stu-id="6c31e-196">Analyze logs from Azure storage with Log Analytics</span></span>](../log-analytics/log-analytics-azure-storage.md)
