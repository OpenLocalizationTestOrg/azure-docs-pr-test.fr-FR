---
title: "Archiver le journal d’activité Azure | Microsoft Docs"
description: "Découvrez comment archiver votre journal d’activité Azure pour une conservation à long terme dans un compte de stockage."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: d37d3fda-8ef1-477c-a360-a855b418de84
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/09/2016
ms.author: johnkem
ms.openlocfilehash: 0e3a5b84f57eac96249430fa1c2c4cc076c2926a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="archive-the-azure-activity-log"></a><span data-ttu-id="fd9c8-103">Archiver le journal d’activité Azure</span><span class="sxs-lookup"><span data-stu-id="fd9c8-103">Archive the Azure Activity Log</span></span>
<span data-ttu-id="fd9c8-104">Dans cet article, nous vous expliquons comment vous pouvez utiliser le portail Azure, les applets de commande PowerShell ou l’interface de ligne de commande multiplateforme pour archiver votre [**journal d’activité Azure dans un compte de stockage**](monitoring-overview-activity-logs.md).</span><span class="sxs-lookup"><span data-stu-id="fd9c8-104">In this article, we show how you can use the Azure portal, PowerShell Cmdlets, or Cross-Platform CLI to archive your [**Azure Activity Log**](monitoring-overview-activity-logs.md) in a storage account.</span></span> <span data-ttu-id="fd9c8-105">Cette option est utile si vous souhaitez conserver votre journal d’activité pendant une période supérieure à 90 jours (en disposant d’un contrôle total sur la stratégie de rétention) à des fins d’audit, d’analyse statique ou de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="fd9c8-105">This option is useful if you would like to retain your Activity Log longer than 90 days (with full control over the retention policy) for audit, static analysis, or backup.</span></span> <span data-ttu-id="fd9c8-106">Si vous devez conserver vos événements pendant 90 jours ou moins, il est inutile de configurer l’archivage sur un compte de stockage, puisque les événements du journal d’activité sont conservés dans la plateforme Azure pendant 90 jours sans que l’archivage ne soit activé.</span><span class="sxs-lookup"><span data-stu-id="fd9c8-106">If you only need to retain your events for 90 days or less you do not need to set up archival to a storage account, since Activity Log events are retained in the Azure platform for 90 days without enabling archival.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fd9c8-107">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="fd9c8-107">Prerequisites</span></span>
<span data-ttu-id="fd9c8-108">Avant de commencer, vous devez [créer un compte de stockage](../storage/common/storage-create-storage-account.md#create-a-storage-account) sur lequel vous pouvez archiver votre journal d’activité.</span><span class="sxs-lookup"><span data-stu-id="fd9c8-108">Before you begin, you need to [create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) to which you can archive your Activity Log.</span></span> <span data-ttu-id="fd9c8-109">Nous vous recommandons vivement de ne pas utiliser un compte de stockage existant sur lequel sont stockées d’autres données de non-analyse, afin de pouvoir mieux contrôler l’accès aux données d’analyse.</span><span class="sxs-lookup"><span data-stu-id="fd9c8-109">We highly recommend that you do not use an existing storage account that has other, non-monitoring data stored in it so that you can better control access to monitoring data.</span></span> <span data-ttu-id="fd9c8-110">En revanche, si vous archivez également des journaux de diagnostic et des métriques sur un compte de stockage, il peut être judicieux d’utiliser ce compte pour votre journal d’activité afin de regrouper toutes vos données d’analyse au même emplacement.</span><span class="sxs-lookup"><span data-stu-id="fd9c8-110">However, if you are also archiving Diagnostic Logs and metrics to a storage account, it may make sense to use that storage account for your Activity Log as well to keep all monitoring data in a central location.</span></span> <span data-ttu-id="fd9c8-111">Le compte de stockage que vous utilisez doit être un compte de stockage à usage général, et non un compte de stockage Blob.</span><span class="sxs-lookup"><span data-stu-id="fd9c8-111">The storage account you use must be a general purpose storage account, not a blob storage account.</span></span> <span data-ttu-id="fd9c8-112">Il n’est pas nécessaire que le compte de stockage se trouve dans le même abonnement que l’abonnement générant des journaux, à condition que l’utilisateur qui configure le paramètre ait un accès RBAC approprié aux deux abonnements.</span><span class="sxs-lookup"><span data-stu-id="fd9c8-112">The storage account does not have to be in the same subscription as the subscription emitting logs as long as the user who configures the setting has appropriate RBAC access to both subscriptions.</span></span>

## <a name="log-profile"></a><span data-ttu-id="fd9c8-113">Profil de journal</span><span class="sxs-lookup"><span data-stu-id="fd9c8-113">Log Profile</span></span>
<span data-ttu-id="fd9c8-114">Pour archiver le journal d’activité à l’aide de l’une des méthodes ci-dessous, définissez le **profil journal** pour un abonnement.</span><span class="sxs-lookup"><span data-stu-id="fd9c8-114">To archive the Activity Log using any of the methods below, you set the **Log Profile** for a subscription.</span></span> <span data-ttu-id="fd9c8-115">Le profil de journal définit le type d’événements qui sont stockés ou diffusés et les types de sortie : compte de stockage et/ou hub d’événements.</span><span class="sxs-lookup"><span data-stu-id="fd9c8-115">The Log Profile defines the type of events that are stored or streamed and the outputs—storage account and/or event hub.</span></span> <span data-ttu-id="fd9c8-116">Il définit également la stratégie de rétention (nombre de jours de conservation) pour les événements stockés dans un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="fd9c8-116">It also defines the retention policy (number of days to retain) for events stored in a storage account.</span></span> <span data-ttu-id="fd9c8-117">Si la stratégie de rétention est définie sur zéro, les événements sont stockés indéfiniment.</span><span class="sxs-lookup"><span data-stu-id="fd9c8-117">If the retention policy is set to zero, events are stored indefinitely.</span></span> <span data-ttu-id="fd9c8-118">Elle peut également être définie sur n’importe quelle valeur comprise entre 1 et 2147483647.</span><span class="sxs-lookup"><span data-stu-id="fd9c8-118">Otherwise, this can be set to any value between 1 and 2147483647.</span></span> <span data-ttu-id="fd9c8-119">Les stratégies de rétention sont appliquées sur une base quotidienne. Donc, à la fin d’une journée (UTC), les journaux de la journée qui est désormais au-delà de la stratégie de rétention sont supprimés.</span><span class="sxs-lookup"><span data-stu-id="fd9c8-119">Retention policies are applied per-day, so at the end of a day (UTC), logs from the day that is now beyond the retention policy will be deleted.</span></span> <span data-ttu-id="fd9c8-120">Par exemple, si vous aviez une stratégie de rétention d’une journée, au début de la journée d’aujourd’hui les journaux d’avant-hier seront supprimés.</span><span class="sxs-lookup"><span data-stu-id="fd9c8-120">For example, if you had a retention policy of one day, at the beginning of the day today the logs from the day before yesterday would be deleted.</span></span> <span data-ttu-id="fd9c8-121">[Vous trouverez plus d’informations sur les profils de journal ici](monitoring-overview-activity-logs.md#export-the-activity-log-with-a-log-profile).</span><span class="sxs-lookup"><span data-stu-id="fd9c8-121">[You can read more about log profiles here](monitoring-overview-activity-logs.md#export-the-activity-log-with-a-log-profile).</span></span> 

## <a name="archive-the-activity-log-using-the-portal"></a><span data-ttu-id="fd9c8-122">Archiver le journal d’activité à l’aide du portail</span><span class="sxs-lookup"><span data-stu-id="fd9c8-122">Archive the Activity Log using the portal</span></span>
1. <span data-ttu-id="fd9c8-123">Dans le portail, cliquez sur le lien **Journal d’activité** dans le volet de navigation de gauche.</span><span class="sxs-lookup"><span data-stu-id="fd9c8-123">In the portal, click the **Activity Log** link on the left-side navigation.</span></span> <span data-ttu-id="fd9c8-124">Si vous ne voyez pas de lien pour le journal d’activité, cliquez d’abord sur le lien **More Services** (Plus de services).</span><span class="sxs-lookup"><span data-stu-id="fd9c8-124">If you don’t see a link for the Activity Log, click the **More Services** link first.</span></span>
   
    ![Accéder au panneau Journal d’activité](media/monitoring-archive-activity-log/act-log-portal-navigate.png)
2. <span data-ttu-id="fd9c8-126">En haut du panneau, cliquez sur **Exporter**.</span><span class="sxs-lookup"><span data-stu-id="fd9c8-126">At the top of the blade, click **Export**.</span></span>
   
    ![Cliquer sur le bouton Exporter](media/monitoring-archive-activity-log/act-log-portal-export-button.png)
3. <span data-ttu-id="fd9c8-128">Dans le panneau qui s’affiche, cochez la case pour **exporter vers un compte de stockage** et sélectionnez un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="fd9c8-128">In the blade that appears, check the box for **Export to a storage account** and select a storage account.</span></span>
   
    ![Créer un compte de stockage](media/monitoring-archive-activity-log/act-log-portal-export-blade.png)
4. <span data-ttu-id="fd9c8-130">À l’aide du curseur ou dans la zone de texte, définissez le nombre de jours pendant lesquels les événements du journal d’activité doivent être conservés dans votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="fd9c8-130">Using the slider or text box, define a number of days for which Activity Log events should be kept in your storage account.</span></span> <span data-ttu-id="fd9c8-131">Si vous préférez que vos données soient conservées indéfiniment dans le compte de stockage, indiquez zéro.</span><span class="sxs-lookup"><span data-stu-id="fd9c8-131">If you prefer to have your data persisted in the storage account indefinitely, set this number to zero.</span></span>
5. <span data-ttu-id="fd9c8-132">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="fd9c8-132">Click **Save**.</span></span>

## <a name="archive-the-activity-log-via-powershell"></a><span data-ttu-id="fd9c8-133">Archiver le journal d’activité avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="fd9c8-133">Archive the Activity Log via PowerShell</span></span>
```
Add-AzureRmLogProfile -Name my_log_profile -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Locations global,westus,eastus -RetentionInDays 180 -Categories Write,Delete,Action
```

| <span data-ttu-id="fd9c8-134">Propriété</span><span class="sxs-lookup"><span data-stu-id="fd9c8-134">Property</span></span> | <span data-ttu-id="fd9c8-135">Requis</span><span class="sxs-lookup"><span data-stu-id="fd9c8-135">Required</span></span> | <span data-ttu-id="fd9c8-136">Description</span><span class="sxs-lookup"><span data-stu-id="fd9c8-136">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="fd9c8-137">StorageAccountId</span><span class="sxs-lookup"><span data-stu-id="fd9c8-137">StorageAccountId</span></span> |<span data-ttu-id="fd9c8-138">Non</span><span class="sxs-lookup"><span data-stu-id="fd9c8-138">No</span></span> |<span data-ttu-id="fd9c8-139">ID de ressource du compte de stockage dans lequel les journaux d’activité doivent être enregistrés.</span><span class="sxs-lookup"><span data-stu-id="fd9c8-139">Resource ID of the Storage Account to which Activity Logs should be saved.</span></span> |
| <span data-ttu-id="fd9c8-140">Emplacements</span><span class="sxs-lookup"><span data-stu-id="fd9c8-140">Locations</span></span> |<span data-ttu-id="fd9c8-141">yes</span><span class="sxs-lookup"><span data-stu-id="fd9c8-141">Yes</span></span> |<span data-ttu-id="fd9c8-142">Liste séparée par des virgules des régions pour lesquelles vous souhaitez collecter les événements du journal d’activité.</span><span class="sxs-lookup"><span data-stu-id="fd9c8-142">Comma-separated list of regions for which you would like to collect Activity Log events.</span></span> <span data-ttu-id="fd9c8-143">Vous pouvez afficher une liste de toutes les régions [en consultant cette page](https://azure.microsoft.com/en-us/regions) ou en utilisant [l’API REST de gestion Azure](https://msdn.microsoft.com/library/azure/gg441293.aspx).</span><span class="sxs-lookup"><span data-stu-id="fd9c8-143">You can view a list of all regions [by visiting this page](https://azure.microsoft.com/en-us/regions) or by using [the Azure Management REST API](https://msdn.microsoft.com/library/azure/gg441293.aspx).</span></span> |
| <span data-ttu-id="fd9c8-144">RetentionInDays</span><span class="sxs-lookup"><span data-stu-id="fd9c8-144">RetentionInDays</span></span> |<span data-ttu-id="fd9c8-145">OUI</span><span class="sxs-lookup"><span data-stu-id="fd9c8-145">Yes</span></span> |<span data-ttu-id="fd9c8-146">Nombre de jours pendant lesquels les événements doivent être conservés, compris entre 1 et 2147483647.</span><span class="sxs-lookup"><span data-stu-id="fd9c8-146">Number of days for which events should be retained, between 1 and 2147483647.</span></span> <span data-ttu-id="fd9c8-147">Une valeur de zéro signifie que les journaux seront stockés pour une durée indéfinie (pour toujours).</span><span class="sxs-lookup"><span data-stu-id="fd9c8-147">A value of zero stores the logs indefinitely (forever).</span></span> |
| <span data-ttu-id="fd9c8-148">Catégories</span><span class="sxs-lookup"><span data-stu-id="fd9c8-148">Categories</span></span> |<span data-ttu-id="fd9c8-149">OUI</span><span class="sxs-lookup"><span data-stu-id="fd9c8-149">Yes</span></span> |<span data-ttu-id="fd9c8-150">Liste séparée par des virgules des catégories d’événements qui doivent être collectées.</span><span class="sxs-lookup"><span data-stu-id="fd9c8-150">Comma-separated list of event categories that should be collected.</span></span> <span data-ttu-id="fd9c8-151">Les valeurs possibles sont Write, Delete et Action.</span><span class="sxs-lookup"><span data-stu-id="fd9c8-151">Possible values are Write, Delete, and Action.</span></span> |

## <a name="archive-the-activity-log-via-cli"></a><span data-ttu-id="fd9c8-152">Archiver le journal d’activité avec l’interface de ligne de commande</span><span class="sxs-lookup"><span data-stu-id="fd9c8-152">Archive the Activity Log via CLI</span></span>
```
azure insights logprofile add --name my_log_profile --storageId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/my_storage --locations global,westus,eastus,northeurope --retentionInDays 180 –categories Write,Delete,Action
```

| <span data-ttu-id="fd9c8-153">Propriété</span><span class="sxs-lookup"><span data-stu-id="fd9c8-153">Property</span></span> | <span data-ttu-id="fd9c8-154">Requis</span><span class="sxs-lookup"><span data-stu-id="fd9c8-154">Required</span></span> | <span data-ttu-id="fd9c8-155">Description</span><span class="sxs-lookup"><span data-stu-id="fd9c8-155">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="fd9c8-156">name</span><span class="sxs-lookup"><span data-stu-id="fd9c8-156">name</span></span> |<span data-ttu-id="fd9c8-157">OUI</span><span class="sxs-lookup"><span data-stu-id="fd9c8-157">Yes</span></span> |<span data-ttu-id="fd9c8-158">Nom de votre profil de journal.</span><span class="sxs-lookup"><span data-stu-id="fd9c8-158">Name of your log profile.</span></span> |
| <span data-ttu-id="fd9c8-159">storageId</span><span class="sxs-lookup"><span data-stu-id="fd9c8-159">storageId</span></span> |<span data-ttu-id="fd9c8-160">Non</span><span class="sxs-lookup"><span data-stu-id="fd9c8-160">No</span></span> |<span data-ttu-id="fd9c8-161">ID de ressource du compte de stockage dans lequel les journaux d’activité doivent être enregistrés.</span><span class="sxs-lookup"><span data-stu-id="fd9c8-161">Resource ID of the Storage Account to which Activity Logs should be saved.</span></span> |
| <span data-ttu-id="fd9c8-162">Emplacements</span><span class="sxs-lookup"><span data-stu-id="fd9c8-162">locations</span></span> |<span data-ttu-id="fd9c8-163">OUI</span><span class="sxs-lookup"><span data-stu-id="fd9c8-163">Yes</span></span> |<span data-ttu-id="fd9c8-164">Liste séparée par des virgules des régions pour lesquelles vous souhaitez collecter les événements du journal d’activité.</span><span class="sxs-lookup"><span data-stu-id="fd9c8-164">Comma-separated list of regions for which you would like to collect Activity Log events.</span></span> <span data-ttu-id="fd9c8-165">Vous pouvez afficher une liste de toutes les régions [en consultant cette page](https://azure.microsoft.com/en-us/regions) ou en utilisant [l’API REST de gestion Azure](https://msdn.microsoft.com/library/azure/gg441293.aspx).</span><span class="sxs-lookup"><span data-stu-id="fd9c8-165">You can view a list of all regions [by visiting this page](https://azure.microsoft.com/en-us/regions) or by using [the Azure Management REST API](https://msdn.microsoft.com/library/azure/gg441293.aspx).</span></span> |
| <span data-ttu-id="fd9c8-166">RetentionInDays</span><span class="sxs-lookup"><span data-stu-id="fd9c8-166">retentionInDays</span></span> |<span data-ttu-id="fd9c8-167">OUI</span><span class="sxs-lookup"><span data-stu-id="fd9c8-167">Yes</span></span> |<span data-ttu-id="fd9c8-168">Nombre de jours pendant lesquels les événements doivent être conservés, compris entre 1 et 2147483647.</span><span class="sxs-lookup"><span data-stu-id="fd9c8-168">Number of days for which events should be retained, between 1 and 2147483647.</span></span> <span data-ttu-id="fd9c8-169">Une valeur de zéro signifie que les journaux seront stockés pour une durée indéfinie (pour toujours).</span><span class="sxs-lookup"><span data-stu-id="fd9c8-169">A value of zero will store the logs indefinitely (forever).</span></span> |
| <span data-ttu-id="fd9c8-170">Catégories</span><span class="sxs-lookup"><span data-stu-id="fd9c8-170">categories</span></span> |<span data-ttu-id="fd9c8-171">OUI</span><span class="sxs-lookup"><span data-stu-id="fd9c8-171">Yes</span></span> |<span data-ttu-id="fd9c8-172">Liste séparée par des virgules des catégories d’événements qui doivent être collectées.</span><span class="sxs-lookup"><span data-stu-id="fd9c8-172">Comma-separated list of event categories that should be collected.</span></span> <span data-ttu-id="fd9c8-173">Les valeurs possibles sont Write, Delete et Action.</span><span class="sxs-lookup"><span data-stu-id="fd9c8-173">Possible values are Write, Delete, and Action.</span></span> |

## <a name="storage-schema-of-the-activity-log"></a><span data-ttu-id="fd9c8-174">Schéma de stockage du journal d’activité</span><span class="sxs-lookup"><span data-stu-id="fd9c8-174">Storage schema of the Activity Log</span></span>
<span data-ttu-id="fd9c8-175">Une fois que vous avez configuré l’archivage, un conteneur de stockage est créé dans le compte de stockage dès qu’un événement de journal d’activité se produit.</span><span class="sxs-lookup"><span data-stu-id="fd9c8-175">Once you have set up archival, a storage container will be created in the storage account as soon as an Activity Log event occurs.</span></span> <span data-ttu-id="fd9c8-176">Les objets blob au sein du conteneur suivent le même format dans le journal d’activité et les journaux de diagnostic.</span><span class="sxs-lookup"><span data-stu-id="fd9c8-176">The blobs within the container follow the same format across the Activity Log and Diagnostic Logs.</span></span> <span data-ttu-id="fd9c8-177">La structure de ces objets blob est la suivante :</span><span class="sxs-lookup"><span data-stu-id="fd9c8-177">The structure of these blobs is:</span></span>

> <span data-ttu-id="fd9c8-178">insights-operational-logs/name=default/resourceId=/SUBSCRIPTIONS/{ID de l’abonnement}/y={année, quatre chiffes}/m={mois, deux chiffres}/d={jour, deux chiffres}/h={heure, deux chiffres, format 24 heures}/m=00/PT1H.json</span><span class="sxs-lookup"><span data-stu-id="fd9c8-178">insights-operational-logs/name=default/resourceId=/SUBSCRIPTIONS/{subscription ID}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json</span></span>
> 
> 

<span data-ttu-id="fd9c8-179">Voici un exemple de nom d’objet blob :</span><span class="sxs-lookup"><span data-stu-id="fd9c8-179">For example, a blob name might be:</span></span>

> <span data-ttu-id="fd9c8-180">insights-operational-logs/name=default/resourceId=/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/y=2016/m=08/d=22/h=18/m=00/PT1H.json</span><span class="sxs-lookup"><span data-stu-id="fd9c8-180">insights-operational-logs/name=default/resourceId=/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/y=2016/m=08/d=22/h=18/m=00/PT1H.json</span></span>
> 
> 

<span data-ttu-id="fd9c8-181">Chaque objet blob PT1H.json contient un objet blob d’événements JSON qui se sont produits pendant l’heure spécifiée dans l’URL de l’objet blob (par exemple, h = 12).</span><span class="sxs-lookup"><span data-stu-id="fd9c8-181">Each PT1H.json blob contains a JSON blob of events that occurred within the hour specified in the blob URL (e.g. h=12).</span></span> <span data-ttu-id="fd9c8-182">Pendant l’heure en cours, les événements sont ajoutés au fichier PT1H.json à mesure qu’ils se produisent.</span><span class="sxs-lookup"><span data-stu-id="fd9c8-182">During the present hour, events are appended to the PT1H.json file as they occur.</span></span> <span data-ttu-id="fd9c8-183">La valeur de minute (m = 00) est toujours 00, étant donné que les événements du journal d’activité sont répartis en différents objets blob par heure.</span><span class="sxs-lookup"><span data-stu-id="fd9c8-183">The minute value (m=00) is always 00, since Activity Log events are broken into individual blobs per hour.</span></span>

<span data-ttu-id="fd9c8-184">Dans le fichier PT1H.json, chaque événement est stocké dans le tableau « enregistrements », au format suivant :</span><span class="sxs-lookup"><span data-stu-id="fd9c8-184">Within the PT1H.json file, each event is stored in the “records” array, following this format:</span></span>

```
{
    "records": [
        {
            "time": "2015-01-21T22:14:26.9792776Z",
            "resourceId": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841",
            "operationName": "microsoft.support/supporttickets/write",
            "category": "Write",
            "resultType": "Success",
            "resultSignature": "Succeeded.Created",
            "durationMs": 2826,
            "callerIpAddress": "111.111.111.11",
            "correlationId": "c776f9f4-36e5-4e0e-809b-c9b3c3fb62a8",
            "identity": {
                "authorization": {
                    "scope": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841",
                    "action": "microsoft.support/supporttickets/write",
                    "evidence": {
                        "role": "Subscription Admin"
                    }
                },
                "claims": {
                    "aud": "https://management.core.windows.net/",
                    "iss": "https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db47/",
                    "iat": "1421876371",
                    "nbf": "1421876371",
                    "exp": "1421880271",
                    "ver": "1.0",
                    "http://schemas.microsoft.com/identity/claims/tenantid": "1e8d8218-c5e7-4578-9acc-9abbd5d23315 ",
                    "http://schemas.microsoft.com/claims/authnmethodsreferences": "pwd",
                    "http://schemas.microsoft.com/identity/claims/objectidentifier": "2468adf0-8211-44e3-95xq-85137af64708",
                    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn": "admin@contoso.com",
                    "puid": "20030000801A118C",
                    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier": "9vckmEGF7zDKk1YzIY8k0t1_EAPaXoeHyPRn6f413zM",
                    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname": "John",
                    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname": "Smith",
                    "name": "John Smith",
                    "groups": "cacfe77c-e058-4712-83qw-f9b08849fd60,7f71d11d-4c41-4b23-99d2-d32ce7aa621c,31522864-0578-4ea0-9gdc-e66cc564d18c",
                    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name": " admin@contoso.com",
                    "appid": "c44b4083-3bq0-49c1-b47d-974e53cbdf3c",
                    "appidacr": "2",
                    "http://schemas.microsoft.com/identity/claims/scope": "user_impersonation",
                    "http://schemas.microsoft.com/claims/authnclassreference": "1"
                }
            },
            "level": "Information",
            "location": "global",
            "properties": {
                "statusCode": "Created",
                "serviceRequestId": "50d5cddb-8ca0-47ad-9b80-6cde2207f97c"
            }
        }
    ]
}
```


| <span data-ttu-id="fd9c8-185">Nom de l'élément</span><span class="sxs-lookup"><span data-stu-id="fd9c8-185">Element name</span></span> | <span data-ttu-id="fd9c8-186">Description</span><span class="sxs-lookup"><span data-stu-id="fd9c8-186">Description</span></span> |
| --- | --- |
| <span data-ttu-id="fd9c8-187">time</span><span class="sxs-lookup"><span data-stu-id="fd9c8-187">time</span></span> |<span data-ttu-id="fd9c8-188">Horodatage lorsque l’événement a été généré par le service Azure traitant la demande correspondant à l’événement.</span><span class="sxs-lookup"><span data-stu-id="fd9c8-188">Timestamp when the event was generated by the Azure service processing the request corresponding the event.</span></span> |
| <span data-ttu-id="fd9c8-189">resourceId</span><span class="sxs-lookup"><span data-stu-id="fd9c8-189">resourceId</span></span> |<span data-ttu-id="fd9c8-190">ID de ressource de la ressource affectée.</span><span class="sxs-lookup"><span data-stu-id="fd9c8-190">Resource ID of the impacted resource.</span></span> |
| <span data-ttu-id="fd9c8-191">operationName</span><span class="sxs-lookup"><span data-stu-id="fd9c8-191">operationName</span></span> |<span data-ttu-id="fd9c8-192">Nom de l’opération.</span><span class="sxs-lookup"><span data-stu-id="fd9c8-192">Name of the operation.</span></span> |
| <span data-ttu-id="fd9c8-193">category</span><span class="sxs-lookup"><span data-stu-id="fd9c8-193">category</span></span> |<span data-ttu-id="fd9c8-194">Catégorie de l’action, par ex.</span><span class="sxs-lookup"><span data-stu-id="fd9c8-194">Category of the action, eg.</span></span> <span data-ttu-id="fd9c8-195">Écriture, Lecture, Action.</span><span class="sxs-lookup"><span data-stu-id="fd9c8-195">Write, Read, Action.</span></span> |
| <span data-ttu-id="fd9c8-196">resultType</span><span class="sxs-lookup"><span data-stu-id="fd9c8-196">resultType</span></span> |<span data-ttu-id="fd9c8-197">Le type du résultat, par ex.</span><span class="sxs-lookup"><span data-stu-id="fd9c8-197">The type of the result, eg.</span></span> <span data-ttu-id="fd9c8-198">Réussite, échec, démarrage</span><span class="sxs-lookup"><span data-stu-id="fd9c8-198">Success, Failure, Start</span></span> |
| <span data-ttu-id="fd9c8-199">resultSignature</span><span class="sxs-lookup"><span data-stu-id="fd9c8-199">resultSignature</span></span> |<span data-ttu-id="fd9c8-200">Dépend du type de ressource.</span><span class="sxs-lookup"><span data-stu-id="fd9c8-200">Depends on the resource type.</span></span> |
| <span data-ttu-id="fd9c8-201">durationMS</span><span class="sxs-lookup"><span data-stu-id="fd9c8-201">durationMs</span></span> |<span data-ttu-id="fd9c8-202">Durée de l’opération en millisecondes</span><span class="sxs-lookup"><span data-stu-id="fd9c8-202">Duration of the operation in milliseconds</span></span> |
| <span data-ttu-id="fd9c8-203">callerIpAddress</span><span class="sxs-lookup"><span data-stu-id="fd9c8-203">callerIpAddress</span></span> |<span data-ttu-id="fd9c8-204">Adresse IP de l’utilisateur qui a effectué l’opération, la revendication UPN ou la revendication SPN basée sur la disponibilité.</span><span class="sxs-lookup"><span data-stu-id="fd9c8-204">IP address of the user who has performed the operation, UPN claim, or SPN claim based on availability.</span></span> |
| <span data-ttu-id="fd9c8-205">correlationId</span><span class="sxs-lookup"><span data-stu-id="fd9c8-205">correlationId</span></span> |<span data-ttu-id="fd9c8-206">Généralement un GUID au format chaîne.</span><span class="sxs-lookup"><span data-stu-id="fd9c8-206">Usually a GUID in the string format.</span></span> <span data-ttu-id="fd9c8-207">Les événements qui partagent un correlationId appartiennent à la même action uber.</span><span class="sxs-lookup"><span data-stu-id="fd9c8-207">Events that share a correlationId belong to the same uber action.</span></span> |
| <span data-ttu-id="fd9c8-208">identité</span><span class="sxs-lookup"><span data-stu-id="fd9c8-208">identity</span></span> |<span data-ttu-id="fd9c8-209">Objet blob JSON décrivant l’autorisation et les revendications.</span><span class="sxs-lookup"><span data-stu-id="fd9c8-209">JSON blob describing the authorization and claims.</span></span> |
| <span data-ttu-id="fd9c8-210">autorisation</span><span class="sxs-lookup"><span data-stu-id="fd9c8-210">authorization</span></span> |<span data-ttu-id="fd9c8-211">Objet blob des propriétés RBAC de l’événement.</span><span class="sxs-lookup"><span data-stu-id="fd9c8-211">Blob of RBAC properties of the event.</span></span> <span data-ttu-id="fd9c8-212">Inclut généralement les propriétés « action », « role » et « scope ».</span><span class="sxs-lookup"><span data-stu-id="fd9c8-212">Usually includes the “action”, “role” and “scope” properties.</span></span> |
| <span data-ttu-id="fd9c8-213">level</span><span class="sxs-lookup"><span data-stu-id="fd9c8-213">level</span></span> |<span data-ttu-id="fd9c8-214">Niveau de l’événement.</span><span class="sxs-lookup"><span data-stu-id="fd9c8-214">Level of the event.</span></span> <span data-ttu-id="fd9c8-215">Une des valeurs suivantes : Critical, Error, Warning, Informational et Verbose</span><span class="sxs-lookup"><span data-stu-id="fd9c8-215">One of the following values: “Critical”, “Error”, “Warning”, “Informational” and “Verbose”</span></span> |
| <span data-ttu-id="fd9c8-216">location</span><span class="sxs-lookup"><span data-stu-id="fd9c8-216">location</span></span> |<span data-ttu-id="fd9c8-217">Région dans laquelle se trouve l’emplacement (ou global).</span><span class="sxs-lookup"><span data-stu-id="fd9c8-217">Region in which the location occurred (or global).</span></span> |
| <span data-ttu-id="fd9c8-218">properties</span><span class="sxs-lookup"><span data-stu-id="fd9c8-218">properties</span></span> |<span data-ttu-id="fd9c8-219">Jeu de paires `<Key, Value>` (p. ex. Dictionary) décrivant les détails de l’événement.</span><span class="sxs-lookup"><span data-stu-id="fd9c8-219">Set of `<Key, Value>` pairs (i.e. Dictionary) describing the details of the event.</span></span> |

> [!NOTE]
> <span data-ttu-id="fd9c8-220">Les propriétés et l’utilisation de ces propriétés peuvent varier en fonction de la ressource.</span><span class="sxs-lookup"><span data-stu-id="fd9c8-220">The properties and usage of those properties can vary depending on the resource.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="fd9c8-221">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="fd9c8-221">Next steps</span></span>
* [<span data-ttu-id="fd9c8-222">Télécharger des objets blob pour analyse</span><span class="sxs-lookup"><span data-stu-id="fd9c8-222">Download blobs for analysis</span></span>](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs)
* [<span data-ttu-id="fd9c8-223">Transférer le journal d’activité vers Event Hubs</span><span class="sxs-lookup"><span data-stu-id="fd9c8-223">Stream the Activity Log to Event Hubs</span></span>](monitoring-stream-activity-logs-event-hubs.md)
* [<span data-ttu-id="fd9c8-224">En savoir plus sur le journal d’activité</span><span class="sxs-lookup"><span data-stu-id="fd9c8-224">Read more about the Activity Log</span></span>](monitoring-overview-activity-logs.md)
