---
title: "aaaArchive hello journal des activités Azure | Documents Microsoft"
description: "Découvrez comment tooarchive vos activités Windows Azure du journal pour la rétention à long terme dans un compte de stockage."
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
ms.openlocfilehash: 58c6d3a3a31398287f66f76999d48f2942ab5109
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="archive-hello-azure-activity-log"></a><span data-ttu-id="7e742-103">Archiver hello journal des activités Azure</span><span class="sxs-lookup"><span data-stu-id="7e742-103">Archive hello Azure Activity Log</span></span>
<span data-ttu-id="7e742-104">Dans cet article, nous montrons comment vous pouvez utiliser hello portail Azure, les PowerShell Cmdlets ou CLI de Cross-Platform tooarchive votre [ **journal des activités Azure** ](monitoring-overview-activity-logs.md) dans un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="7e742-104">In this article, we show how you can use hello Azure portal, PowerShell Cmdlets, or Cross-Platform CLI tooarchive your [**Azure Activity Log**](monitoring-overview-activity-logs.md) in a storage account.</span></span> <span data-ttu-id="7e742-105">Cette option est utile si vous souhaitez que tooretain plus de 90 jours (avec un contrôle total sur la stratégie de rétention hello) pour votre journal des activités d’audit, analyse statique, ou de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="7e742-105">This option is useful if you would like tooretain your Activity Log longer than 90 days (with full control over hello retention policy) for audit, static analysis, or backup.</span></span> <span data-ttu-id="7e742-106">Si vous devez uniquement tooretain vos événements pendant 90 jours ou moins vous est inutile tooset archivage tooa compte de stockage, puisque les événements de journal d’activité sont conservés dans hello plateforme Azure pendant 90 jours sans l’archivage.</span><span class="sxs-lookup"><span data-stu-id="7e742-106">If you only need tooretain your events for 90 days or less you do not need tooset up archival tooa storage account, since Activity Log events are retained in hello Azure platform for 90 days without enabling archival.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7e742-107">Composants requis</span><span class="sxs-lookup"><span data-stu-id="7e742-107">Prerequisites</span></span>
<span data-ttu-id="7e742-108">Avant de commencer, vous devez trop[créer un compte de stockage](../storage/common/storage-create-storage-account.md#create-a-storage-account) toowhich, vous pouvez archiver le journal d’activité.</span><span class="sxs-lookup"><span data-stu-id="7e742-108">Before you begin, you need too[create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) toowhich you can archive your Activity Log.</span></span> <span data-ttu-id="7e742-109">Nous vous recommandons vivement de ne pas utiliser un compte de stockage existant qui comporte des données d’autres, non suivi stockées afin que vous pouvez mieux contrôler les accès toomonitoring données.</span><span class="sxs-lookup"><span data-stu-id="7e742-109">We highly recommend that you do not use an existing storage account that has other, non-monitoring data stored in it so that you can better control access toomonitoring data.</span></span> <span data-ttu-id="7e742-110">Toutefois, si vous archivez également les journaux de Diagnostic et de compte de stockage tooa de métriques, il peut être judicieux toouse ce compte de stockage pour votre activité du journal ainsi tookeep toutes les données d’analyse dans un emplacement central.</span><span class="sxs-lookup"><span data-stu-id="7e742-110">However, if you are also archiving Diagnostic Logs and metrics tooa storage account, it may make sense toouse that storage account for your Activity Log as well tookeep all monitoring data in a central location.</span></span> <span data-ttu-id="7e742-111">compte de stockage Hello que vous utilisez doit être un compte de stockage polyvalentes, pas un compte de stockage d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="7e742-111">hello storage account you use must be a general purpose storage account, not a blob storage account.</span></span> <span data-ttu-id="7e742-112">compte de stockage Hello n’a pas de toobe dans hello même abonnement que l’abonnement hello générant des journaux tant qu’utilisateur hello configure hello paramètre a des abonnements de tooboth accès RBAC appropriés.</span><span class="sxs-lookup"><span data-stu-id="7e742-112">hello storage account does not have toobe in hello same subscription as hello subscription emitting logs as long as hello user who configures hello setting has appropriate RBAC access tooboth subscriptions.</span></span>

## <a name="log-profile"></a><span data-ttu-id="7e742-113">Profil de journal</span><span class="sxs-lookup"><span data-stu-id="7e742-113">Log Profile</span></span>
<span data-ttu-id="7e742-114">tooarchive hello journal d’activité à l’aide d’une des méthodes hello ci-dessous, vous définissez hello **profil journal** pour un abonnement.</span><span class="sxs-lookup"><span data-stu-id="7e742-114">tooarchive hello Activity Log using any of hello methods below, you set hello **Log Profile** for a subscription.</span></span> <span data-ttu-id="7e742-115">définit le type hello d’événements qui sont stockés ou transmis en continu Hello profil du journal et hello sorties : concentrateur compte et/ou les événements de stockage.</span><span class="sxs-lookup"><span data-stu-id="7e742-115">hello Log Profile defines hello type of events that are stored or streamed and hello outputs—storage account and/or event hub.</span></span> <span data-ttu-id="7e742-116">Il définit également la stratégie de rétention hello (nombre de jours tooretain) pour les événements stockés dans un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="7e742-116">It also defines hello retention policy (number of days tooretain) for events stored in a storage account.</span></span> <span data-ttu-id="7e742-117">Si la stratégie de rétention hello a la valeur toozero, les événements sont stockés indéfiniment.</span><span class="sxs-lookup"><span data-stu-id="7e742-117">If hello retention policy is set toozero, events are stored indefinitely.</span></span> <span data-ttu-id="7e742-118">Dans le cas contraire, cela peut être valeur tooany compris entre 1 et 2147483647.</span><span class="sxs-lookup"><span data-stu-id="7e742-118">Otherwise, this can be set tooany value between 1 and 2147483647.</span></span> <span data-ttu-id="7e742-119">Stratégies de rétention sont appliquées par jour, donc à hello fin d’une journée (UTC), consigne un jour hello qui est désormais au-delà de la stratégie de rétention hello seront supprimés.</span><span class="sxs-lookup"><span data-stu-id="7e742-119">Retention policies are applied per-day, so at hello end of a day (UTC), logs from hello day that is now beyond hello retention policy will be deleted.</span></span> <span data-ttu-id="7e742-120">Par exemple, si vous aviez une stratégie de rétention d’un jour, au début de hello du jour hello aujourd'hui hello les journaux à partir de hello avant-hier seraient supprimés.</span><span class="sxs-lookup"><span data-stu-id="7e742-120">For example, if you had a retention policy of one day, at hello beginning of hello day today hello logs from hello day before yesterday would be deleted.</span></span> <span data-ttu-id="7e742-121">[Vous trouverez plus d’informations sur les profils de journal ici](monitoring-overview-activity-logs.md#export-the-activity-log-with-a-log-profile).</span><span class="sxs-lookup"><span data-stu-id="7e742-121">[You can read more about log profiles here](monitoring-overview-activity-logs.md#export-the-activity-log-with-a-log-profile).</span></span> 

## <a name="archive-hello-activity-log-using-hello-portal"></a><span data-ttu-id="7e742-122">Archive hello journal d’activité à l’aide du portail de hello</span><span class="sxs-lookup"><span data-stu-id="7e742-122">Archive hello Activity Log using hello portal</span></span>
1. <span data-ttu-id="7e742-123">Dans le portail hello, cliquez sur hello **le journal d’activité** lien de navigation de gauche hello.</span><span class="sxs-lookup"><span data-stu-id="7e742-123">In hello portal, click hello **Activity Log** link on hello left-side navigation.</span></span> <span data-ttu-id="7e742-124">Si vous ne voyez pas un lien pour hello journal d’activité, cliquez sur hello **plus Services** lier tout d’abord.</span><span class="sxs-lookup"><span data-stu-id="7e742-124">If you don’t see a link for hello Activity Log, click hello **More Services** link first.</span></span>
   
    ![Accédez Panneau de journal tooActivity](media/monitoring-archive-activity-log/act-log-portal-navigate.png)
2. <span data-ttu-id="7e742-126">Haut hello du Panneau de hello, cliquez sur **exporter**.</span><span class="sxs-lookup"><span data-stu-id="7e742-126">At hello top of hello blade, click **Export**.</span></span>
   
    ![Cliquez sur le bouton Exporter de hello](media/monitoring-archive-activity-log/act-log-portal-export-button.png)
3. <span data-ttu-id="7e742-128">Dans le panneau hello qui s’affiche, cochez la case hello **exporter le compte de stockage tooa** et sélectionnez un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="7e742-128">In hello blade that appears, check hello box for **Export tooa storage account** and select a storage account.</span></span>
   
    ![Créer un compte de stockage](media/monitoring-archive-activity-log/act-log-portal-export-blade.png)
4. <span data-ttu-id="7e742-130">À l’aide du curseur de hello ou zone de texte, de définir un nombre de jours pour lesquels les événements du journal d’activité doivent être conservées dans votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="7e742-130">Using hello slider or text box, define a number of days for which Activity Log events should be kept in your storage account.</span></span> <span data-ttu-id="7e742-131">Si vous préférez toohave vos données persistant dans le compte de stockage hello indéfiniment, ce nombre toozero.</span><span class="sxs-lookup"><span data-stu-id="7e742-131">If you prefer toohave your data persisted in hello storage account indefinitely, set this number toozero.</span></span>
5. <span data-ttu-id="7e742-132">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="7e742-132">Click **Save**.</span></span>

## <a name="archive-hello-activity-log-via-powershell"></a><span data-ttu-id="7e742-133">Archiver hello journal d’activité via PowerShell</span><span class="sxs-lookup"><span data-stu-id="7e742-133">Archive hello Activity Log via PowerShell</span></span>
```
Add-AzureRmLogProfile -Name my_log_profile -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Locations global,westus,eastus -RetentionInDays 180 -Categories Write,Delete,Action
```

| <span data-ttu-id="7e742-134">Propriété</span><span class="sxs-lookup"><span data-stu-id="7e742-134">Property</span></span> | <span data-ttu-id="7e742-135">Requis</span><span class="sxs-lookup"><span data-stu-id="7e742-135">Required</span></span> | <span data-ttu-id="7e742-136">Description</span><span class="sxs-lookup"><span data-stu-id="7e742-136">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7e742-137">StorageAccountId</span><span class="sxs-lookup"><span data-stu-id="7e742-137">StorageAccountId</span></span> |<span data-ttu-id="7e742-138">Non</span><span class="sxs-lookup"><span data-stu-id="7e742-138">No</span></span> |<span data-ttu-id="7e742-139">ID de ressource de hello toowhich de compte de stockage des journaux d’activité doit être enregistré.</span><span class="sxs-lookup"><span data-stu-id="7e742-139">Resource ID of hello Storage Account toowhich Activity Logs should be saved.</span></span> |
| <span data-ttu-id="7e742-140">Emplacements</span><span class="sxs-lookup"><span data-stu-id="7e742-140">Locations</span></span> |<span data-ttu-id="7e742-141">Oui</span><span class="sxs-lookup"><span data-stu-id="7e742-141">Yes</span></span> |<span data-ttu-id="7e742-142">Liste de séparées par des virgules des régions pour lequel vous souhaitez que les événements du journal d’activité toocollect.</span><span class="sxs-lookup"><span data-stu-id="7e742-142">Comma-separated list of regions for which you would like toocollect Activity Log events.</span></span> <span data-ttu-id="7e742-143">Vous pouvez afficher une liste de toutes les régions [en visitant cette page](https://azure.microsoft.com/en-us/regions) ou à l’aide de [hello API REST de gestion Azure](https://msdn.microsoft.com/library/azure/gg441293.aspx).</span><span class="sxs-lookup"><span data-stu-id="7e742-143">You can view a list of all regions [by visiting this page](https://azure.microsoft.com/en-us/regions) or by using [hello Azure Management REST API](https://msdn.microsoft.com/library/azure/gg441293.aspx).</span></span> |
| <span data-ttu-id="7e742-144">RetentionInDays</span><span class="sxs-lookup"><span data-stu-id="7e742-144">RetentionInDays</span></span> |<span data-ttu-id="7e742-145">OUI</span><span class="sxs-lookup"><span data-stu-id="7e742-145">Yes</span></span> |<span data-ttu-id="7e742-146">Nombre de jours pendant lesquels les événements doivent être conservés, compris entre 1 et 2147483647.</span><span class="sxs-lookup"><span data-stu-id="7e742-146">Number of days for which events should be retained, between 1 and 2147483647.</span></span> <span data-ttu-id="7e742-147">Une valeur égale à zéro stocke les journaux hello indéfiniment (indéfiniment).</span><span class="sxs-lookup"><span data-stu-id="7e742-147">A value of zero stores hello logs indefinitely (forever).</span></span> |
| <span data-ttu-id="7e742-148">Catégories</span><span class="sxs-lookup"><span data-stu-id="7e742-148">Categories</span></span> |<span data-ttu-id="7e742-149">OUI</span><span class="sxs-lookup"><span data-stu-id="7e742-149">Yes</span></span> |<span data-ttu-id="7e742-150">Liste séparée par des virgules des catégories d’événements qui doivent être collectées.</span><span class="sxs-lookup"><span data-stu-id="7e742-150">Comma-separated list of event categories that should be collected.</span></span> <span data-ttu-id="7e742-151">Les valeurs possibles sont Write, Delete et Action.</span><span class="sxs-lookup"><span data-stu-id="7e742-151">Possible values are Write, Delete, and Action.</span></span> |

## <a name="archive-hello-activity-log-via-cli"></a><span data-ttu-id="7e742-152">Archiver le journal d’activité via l’interface CLI de hello</span><span class="sxs-lookup"><span data-stu-id="7e742-152">Archive hello Activity Log via CLI</span></span>
```
azure insights logprofile add --name my_log_profile --storageId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/my_storage --locations global,westus,eastus,northeurope --retentionInDays 180 –categories Write,Delete,Action
```

| <span data-ttu-id="7e742-153">Propriété</span><span class="sxs-lookup"><span data-stu-id="7e742-153">Property</span></span> | <span data-ttu-id="7e742-154">Requis</span><span class="sxs-lookup"><span data-stu-id="7e742-154">Required</span></span> | <span data-ttu-id="7e742-155">Description</span><span class="sxs-lookup"><span data-stu-id="7e742-155">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7e742-156">name</span><span class="sxs-lookup"><span data-stu-id="7e742-156">name</span></span> |<span data-ttu-id="7e742-157">OUI</span><span class="sxs-lookup"><span data-stu-id="7e742-157">Yes</span></span> |<span data-ttu-id="7e742-158">Nom de votre profil de journal.</span><span class="sxs-lookup"><span data-stu-id="7e742-158">Name of your log profile.</span></span> |
| <span data-ttu-id="7e742-159">storageId</span><span class="sxs-lookup"><span data-stu-id="7e742-159">storageId</span></span> |<span data-ttu-id="7e742-160">Non</span><span class="sxs-lookup"><span data-stu-id="7e742-160">No</span></span> |<span data-ttu-id="7e742-161">ID de ressource de hello toowhich de compte de stockage des journaux d’activité doit être enregistré.</span><span class="sxs-lookup"><span data-stu-id="7e742-161">Resource ID of hello Storage Account toowhich Activity Logs should be saved.</span></span> |
| <span data-ttu-id="7e742-162">emplacements</span><span class="sxs-lookup"><span data-stu-id="7e742-162">locations</span></span> |<span data-ttu-id="7e742-163">Oui</span><span class="sxs-lookup"><span data-stu-id="7e742-163">Yes</span></span> |<span data-ttu-id="7e742-164">Liste de séparées par des virgules des régions pour lequel vous souhaitez que les événements du journal d’activité toocollect.</span><span class="sxs-lookup"><span data-stu-id="7e742-164">Comma-separated list of regions for which you would like toocollect Activity Log events.</span></span> <span data-ttu-id="7e742-165">Vous pouvez afficher une liste de toutes les régions [en visitant cette page](https://azure.microsoft.com/en-us/regions) ou à l’aide de [hello API REST de gestion Azure](https://msdn.microsoft.com/library/azure/gg441293.aspx).</span><span class="sxs-lookup"><span data-stu-id="7e742-165">You can view a list of all regions [by visiting this page](https://azure.microsoft.com/en-us/regions) or by using [hello Azure Management REST API](https://msdn.microsoft.com/library/azure/gg441293.aspx).</span></span> |
| <span data-ttu-id="7e742-166">RetentionInDays</span><span class="sxs-lookup"><span data-stu-id="7e742-166">retentionInDays</span></span> |<span data-ttu-id="7e742-167">OUI</span><span class="sxs-lookup"><span data-stu-id="7e742-167">Yes</span></span> |<span data-ttu-id="7e742-168">Nombre de jours pendant lesquels les événements doivent être conservés, compris entre 1 et 2147483647.</span><span class="sxs-lookup"><span data-stu-id="7e742-168">Number of days for which events should be retained, between 1 and 2147483647.</span></span> <span data-ttu-id="7e742-169">Une valeur égale à zéro stockera les journaux hello indéfiniment (indéfiniment).</span><span class="sxs-lookup"><span data-stu-id="7e742-169">A value of zero will store hello logs indefinitely (forever).</span></span> |
| <span data-ttu-id="7e742-170">Catégories</span><span class="sxs-lookup"><span data-stu-id="7e742-170">categories</span></span> |<span data-ttu-id="7e742-171">OUI</span><span class="sxs-lookup"><span data-stu-id="7e742-171">Yes</span></span> |<span data-ttu-id="7e742-172">Liste séparée par des virgules des catégories d’événements qui doivent être collectées.</span><span class="sxs-lookup"><span data-stu-id="7e742-172">Comma-separated list of event categories that should be collected.</span></span> <span data-ttu-id="7e742-173">Les valeurs possibles sont Write, Delete et Action.</span><span class="sxs-lookup"><span data-stu-id="7e742-173">Possible values are Write, Delete, and Action.</span></span> |

## <a name="storage-schema-of-hello-activity-log"></a><span data-ttu-id="7e742-174">Schéma de stockage de hello journal d’activité</span><span class="sxs-lookup"><span data-stu-id="7e742-174">Storage schema of hello Activity Log</span></span>
<span data-ttu-id="7e742-175">Une fois que vous avez configuré d’archivage, un conteneur de stockage sera créé dans le compte de stockage hello dès qu’un événement du journal d’activité se produit.</span><span class="sxs-lookup"><span data-stu-id="7e742-175">Once you have set up archival, a storage container will be created in hello storage account as soon as an Activity Log event occurs.</span></span> <span data-ttu-id="7e742-176">BLOB Hello conteneur hello suivez hello même format entre hello journal d’activité et des journaux de Diagnostic.</span><span class="sxs-lookup"><span data-stu-id="7e742-176">hello blobs within hello container follow hello same format across hello Activity Log and Diagnostic Logs.</span></span> <span data-ttu-id="7e742-177">structure Hello de ces objets BLOB est la suivante :</span><span class="sxs-lookup"><span data-stu-id="7e742-177">hello structure of these blobs is:</span></span>

> <span data-ttu-id="7e742-178">insights-operational-logs/name=default/resourceId=/SUBSCRIPTIONS/{ID de l’abonnement}/y={année, quatre chiffes}/m={mois, deux chiffres}/d={jour, deux chiffres}/h={heure, deux chiffres, format 24 heures}/m=00/PT1H.json</span><span class="sxs-lookup"><span data-stu-id="7e742-178">insights-operational-logs/name=default/resourceId=/SUBSCRIPTIONS/{subscription ID}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json</span></span>
> 
> 

<span data-ttu-id="7e742-179">Voici un exemple de nom d’objet blob :</span><span class="sxs-lookup"><span data-stu-id="7e742-179">For example, a blob name might be:</span></span>

> <span data-ttu-id="7e742-180">insights-operational-logs/name=default/resourceId=/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/y=2016/m=08/d=22/h=18/m=00/PT1H.json</span><span class="sxs-lookup"><span data-stu-id="7e742-180">insights-operational-logs/name=default/resourceId=/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/y=2016/m=08/d=22/h=18/m=00/PT1H.json</span></span>
> 
> 

<span data-ttu-id="7e742-181">Chaque objet blob PT1H.json contient un objet blob de JSON d’événements qui se sont produites dans heure hello spécifié dans l’URL de blob hello (par exemple, h = 12).</span><span class="sxs-lookup"><span data-stu-id="7e742-181">Each PT1H.json blob contains a JSON blob of events that occurred within hello hour specified in hello blob URL (e.g. h=12).</span></span> <span data-ttu-id="7e742-182">Pendant hello heure actuelle, les événements sont ajoutés toohello PT1H.json fichier qu’ils se produisent.</span><span class="sxs-lookup"><span data-stu-id="7e742-182">During hello present hour, events are appended toohello PT1H.json file as they occur.</span></span> <span data-ttu-id="7e742-183">valeur de minute de Hello (m = 00) est toujours 00, étant donné que les événements du journal d’activité sont divisées en objets BLOB individuels par heure.</span><span class="sxs-lookup"><span data-stu-id="7e742-183">hello minute value (m=00) is always 00, since Activity Log events are broken into individual blobs per hour.</span></span>

<span data-ttu-id="7e742-184">Dans le fichier de PT1H.json hello, chaque événement est stocké dans le tableau « enregistrements de hello », sous ce format :</span><span class="sxs-lookup"><span data-stu-id="7e742-184">Within hello PT1H.json file, each event is stored in hello “records” array, following this format:</span></span>

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


| <span data-ttu-id="7e742-185">Nom de l'élément</span><span class="sxs-lookup"><span data-stu-id="7e742-185">Element name</span></span> | <span data-ttu-id="7e742-186">Description</span><span class="sxs-lookup"><span data-stu-id="7e742-186">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7e742-187">time</span><span class="sxs-lookup"><span data-stu-id="7e742-187">time</span></span> |<span data-ttu-id="7e742-188">Horodatage lors de l’événement de hello a été généré par hello du traitement du service Azure hello demande événement hello correspondant.</span><span class="sxs-lookup"><span data-stu-id="7e742-188">Timestamp when hello event was generated by hello Azure service processing hello request corresponding hello event.</span></span> |
| <span data-ttu-id="7e742-189">resourceId</span><span class="sxs-lookup"><span data-stu-id="7e742-189">resourceId</span></span> |<span data-ttu-id="7e742-190">ID de ressource de hello affectées les ressources.</span><span class="sxs-lookup"><span data-stu-id="7e742-190">Resource ID of hello impacted resource.</span></span> |
| <span data-ttu-id="7e742-191">operationName</span><span class="sxs-lookup"><span data-stu-id="7e742-191">operationName</span></span> |<span data-ttu-id="7e742-192">Nom de l’opération de hello.</span><span class="sxs-lookup"><span data-stu-id="7e742-192">Name of hello operation.</span></span> |
| <span data-ttu-id="7e742-193">category</span><span class="sxs-lookup"><span data-stu-id="7e742-193">category</span></span> |<span data-ttu-id="7e742-194">Catégorie d’action de hello, par exemple.</span><span class="sxs-lookup"><span data-stu-id="7e742-194">Category of hello action, eg.</span></span> <span data-ttu-id="7e742-195">Écriture, Lecture, Action.</span><span class="sxs-lookup"><span data-stu-id="7e742-195">Write, Read, Action.</span></span> |
| <span data-ttu-id="7e742-196">resultType</span><span class="sxs-lookup"><span data-stu-id="7e742-196">resultType</span></span> |<span data-ttu-id="7e742-197">Bonjour type du résultat de hello, par exemple.</span><span class="sxs-lookup"><span data-stu-id="7e742-197">hello type of hello result, eg.</span></span> <span data-ttu-id="7e742-198">Réussite, échec, démarrage</span><span class="sxs-lookup"><span data-stu-id="7e742-198">Success, Failure, Start</span></span> |
| <span data-ttu-id="7e742-199">resultSignature</span><span class="sxs-lookup"><span data-stu-id="7e742-199">resultSignature</span></span> |<span data-ttu-id="7e742-200">Varie selon le type de ressource hello.</span><span class="sxs-lookup"><span data-stu-id="7e742-200">Depends on hello resource type.</span></span> |
| <span data-ttu-id="7e742-201">durationMS</span><span class="sxs-lookup"><span data-stu-id="7e742-201">durationMs</span></span> |<span data-ttu-id="7e742-202">Durée de l’opération de hello en millisecondes</span><span class="sxs-lookup"><span data-stu-id="7e742-202">Duration of hello operation in milliseconds</span></span> |
| <span data-ttu-id="7e742-203">callerIpAddress</span><span class="sxs-lookup"><span data-stu-id="7e742-203">callerIpAddress</span></span> |<span data-ttu-id="7e742-204">Adresse IP de l’utilisateur de hello qui a effectué les opération hello, revendication UPN ou revendication SPN basée sur la disponibilité.</span><span class="sxs-lookup"><span data-stu-id="7e742-204">IP address of hello user who has performed hello operation, UPN claim, or SPN claim based on availability.</span></span> |
| <span data-ttu-id="7e742-205">correlationId</span><span class="sxs-lookup"><span data-stu-id="7e742-205">correlationId</span></span> |<span data-ttu-id="7e742-206">Généralement, un GUID au format de chaîne hello.</span><span class="sxs-lookup"><span data-stu-id="7e742-206">Usually a GUID in hello string format.</span></span> <span data-ttu-id="7e742-207">Les événements qui partagent un ID de corrélation appartiennent toohello même action uber.</span><span class="sxs-lookup"><span data-stu-id="7e742-207">Events that share a correlationId belong toohello same uber action.</span></span> |
| <span data-ttu-id="7e742-208">identité</span><span class="sxs-lookup"><span data-stu-id="7e742-208">identity</span></span> |<span data-ttu-id="7e742-209">L’objet blob JSON décrivant les revendications et l’autorisation de hello.</span><span class="sxs-lookup"><span data-stu-id="7e742-209">JSON blob describing hello authorization and claims.</span></span> |
| <span data-ttu-id="7e742-210">autorisation</span><span class="sxs-lookup"><span data-stu-id="7e742-210">authorization</span></span> |<span data-ttu-id="7e742-211">Objet BLOB de propriétés RBAC de l’événement de hello.</span><span class="sxs-lookup"><span data-stu-id="7e742-211">Blob of RBAC properties of hello event.</span></span> <span data-ttu-id="7e742-212">Inclut généralement les propriétés « action », « rôle » et « portée » hello.</span><span class="sxs-lookup"><span data-stu-id="7e742-212">Usually includes hello “action”, “role” and “scope” properties.</span></span> |
| <span data-ttu-id="7e742-213">level</span><span class="sxs-lookup"><span data-stu-id="7e742-213">level</span></span> |<span data-ttu-id="7e742-214">Niveau d’événement de hello.</span><span class="sxs-lookup"><span data-stu-id="7e742-214">Level of hello event.</span></span> <span data-ttu-id="7e742-215">Une des valeurs suivantes de hello : « Critiques », « Erreur », « Avertissement », « Information » et « Commentaires »</span><span class="sxs-lookup"><span data-stu-id="7e742-215">One of hello following values: “Critical”, “Error”, “Warning”, “Informational” and “Verbose”</span></span> |
| <span data-ttu-id="7e742-216">location</span><span class="sxs-lookup"><span data-stu-id="7e742-216">location</span></span> |<span data-ttu-id="7e742-217">Région dans un emplacement hello qui s’est produite (ou global).</span><span class="sxs-lookup"><span data-stu-id="7e742-217">Region in which hello location occurred (or global).</span></span> |
| <span data-ttu-id="7e742-218">properties</span><span class="sxs-lookup"><span data-stu-id="7e742-218">properties</span></span> |<span data-ttu-id="7e742-219">Jeu de `<Key, Value>` paires (c'est-à-dire, Dictionary) hello décrivant les événements hello.</span><span class="sxs-lookup"><span data-stu-id="7e742-219">Set of `<Key, Value>` pairs (i.e. Dictionary) describing hello details of hello event.</span></span> |

> [!NOTE]
> <span data-ttu-id="7e742-220">propriétés de Hello et l’utilisation de ces propriétés peuvent varier en fonction de la ressource de hello.</span><span class="sxs-lookup"><span data-stu-id="7e742-220">hello properties and usage of those properties can vary depending on hello resource.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="7e742-221">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7e742-221">Next steps</span></span>
* [<span data-ttu-id="7e742-222">Télécharger des objets blob pour analyse</span><span class="sxs-lookup"><span data-stu-id="7e742-222">Download blobs for analysis</span></span>](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs)
* [<span data-ttu-id="7e742-223">Flux tooEvent de journal d’activité hello concentrateurs</span><span class="sxs-lookup"><span data-stu-id="7e742-223">Stream hello Activity Log tooEvent Hubs</span></span>](monitoring-stream-activity-logs-event-hubs.md)
* [<span data-ttu-id="7e742-224">En savoir plus sur hello journal d’activité</span><span class="sxs-lookup"><span data-stu-id="7e742-224">Read more about hello Activity Log</span></span>](monitoring-overview-activity-logs.md)

