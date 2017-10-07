---
title: "métriques de stockage aaaEnabling Bonjour portail Azure | Documents Microsoft"
description: "Comment tooenable les métriques de stockage pour hello services Blob, file d’attente, Table et fichier"
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 0407adfc-2a41-4126-922d-b76e90b74563
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 02/14/2017
ms.author: robinsh
ms.openlocfilehash: f157dbdf9a256da7ab186f80db746b91d1a9beb8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="enabling-azure-storage-metrics-and-viewing-metrics-data"></a><span data-ttu-id="a6481-103">Activation des métriques Azure Storage et affichage des données associées</span><span class="sxs-lookup"><span data-stu-id="a6481-103">Enabling Azure Storage metrics and viewing metrics data</span></span>
[!INCLUDE [storage-selector-portal-enable-and-view-metrics](../../../includes/storage-selector-portal-enable-and-view-metrics.md)]

## <a name="overview"></a><span data-ttu-id="a6481-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="a6481-104">Overview</span></span>
<span data-ttu-id="a6481-105">Storage Metrics est activé par défaut lorsque vous créez un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="a6481-105">Storage Metrics is enabled by default when you create a new storage account.</span></span> <span data-ttu-id="a6481-106">Vous pouvez configurer la surveillance via hello [portail Azure](https://portal.azure.com) ou Windows PowerShell, ou par programme via l’une des bibliothèques clientes de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="a6481-106">You can configure monitoring via hello [Azure portal](https://portal.azure.com) or Windows PowerShell, or programmatically via one of hello storage client libraries.</span></span>

<span data-ttu-id="a6481-107">Vous pouvez configurer une période de rétention pour les données de métriques hello : cette période détermine pour le stockage de hello la durée pendant laquelle le service maintient les métriques hello et les frais de hello espace requis toostore les.</span><span class="sxs-lookup"><span data-stu-id="a6481-107">You can configure a retention period for hello metrics data: this period determines for how long hello storage service keeps hello metrics and charges you for hello space required toostore them.</span></span> <span data-ttu-id="a6481-108">En règle générale, vous devez utiliser une période de rétention plus courte pour les métriques par minute que pour les métriques en raison de l’espace supplémentaire hello requis pour les métriques par minute.</span><span class="sxs-lookup"><span data-stu-id="a6481-108">Typically, you should use a shorter retention period for minute metrics than hourly metrics because of hello significant extra space required for minute metrics.</span></span> <span data-ttu-id="a6481-109">Vous devez choisir une période de rétention telles que des données suffisantes temps tooanalyze hello et de télécharger les métriques que vous souhaitez tookeep pour une analyse hors ligne ou à des fins de création de rapports.</span><span class="sxs-lookup"><span data-stu-id="a6481-109">You should choose a retention period such that you have sufficient time tooanalyze hello data and download any metrics you wish tookeep for off-line analysis or reporting purposes.</span></span> <span data-ttu-id="a6481-110">N’oubliez pas que le téléchargement des données de métriques depuis votre compte de stockage est aussi facturé.</span><span class="sxs-lookup"><span data-stu-id="a6481-110">Remember that you will also be billed for downloading metrics data from your storage account.</span></span>

## <a name="how-tooenable-metrics-using-hello-azure-portal"></a><span data-ttu-id="a6481-111">Comment les métriques tooenable à l’aide de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="a6481-111">How tooenable metrics using hello Azure portal</span></span>
<span data-ttu-id="a6481-112">Suivez ces métriques de tooenable étapes Bonjour [portail Azure](https://portal.azure.com):</span><span class="sxs-lookup"><span data-stu-id="a6481-112">Follow these steps tooenable metrics in hello [Azure portal](https://portal.azure.com):</span></span>

1. <span data-ttu-id="a6481-113">Recherchez le compte de stockage tooyour.</span><span class="sxs-lookup"><span data-stu-id="a6481-113">Navigate tooyour storage account.</span></span>
1. <span data-ttu-id="a6481-114">Sélectionnez **Diagnostics** sur hello **Menu** panneau</span><span class="sxs-lookup"><span data-stu-id="a6481-114">Select **Diagnostics** on hello **Menu** blade</span></span>
1. <span data-ttu-id="a6481-115">Vérifiez que **état** est défini trop**sur**.</span><span class="sxs-lookup"><span data-stu-id="a6481-115">Ensure that **Status** is set too**On**.</span></span>
1. <span data-ttu-id="a6481-116">Métriques sélectionnez hello pour les services de hello vous souhaitez toomonitor.</span><span class="sxs-lookup"><span data-stu-id="a6481-116">Select hello metrics for hello services you wish toomonitor.</span></span>
1. <span data-ttu-id="a6481-117">Spécifiez un tooindicate de stratégie de rétention combien tooretain des métriques et des journaux des données.</span><span class="sxs-lookup"><span data-stu-id="a6481-117">Specify a retention policy tooindicate how long tooretain metrics and log data.</span></span>
1. <span data-ttu-id="a6481-118">Sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="a6481-118">Select **Save**.</span></span>

<span data-ttu-id="a6481-119">Notez que hello [portail Azure](https://portal.azure.com) pas actuellement vous permette de tooconfigure les métriques par minute dans votre compte de stockage ; vous devez les activer à l’aide de PowerShell ou par programme.</span><span class="sxs-lookup"><span data-stu-id="a6481-119">Note that hello [Azure portal](https://portal.azure.com) does not currently enable you tooconfigure minute metrics in your storage account; you must enable minute metrics using PowerShell or programmatically.</span></span>

## <a name="how-tooenable-metrics-using-powershell"></a><span data-ttu-id="a6481-120">Comment les métriques tooenable à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="a6481-120">How tooenable metrics using PowerShell</span></span>
<span data-ttu-id="a6481-121">Vous pouvez utiliser PowerShell sur votre ordinateur local de tooconfigure Storage Metrics dans votre compte de stockage en utilisant les paramètres en cours hello du tooretrieve applet de commande Get-AzureStorageServiceMetricsProperty hello Azure PowerShell et hello applet de commande Set-AzureStorageServiceMetricsProperty toochange hello les paramètres actuels.</span><span class="sxs-lookup"><span data-stu-id="a6481-121">You can use PowerShell on your local machine tooconfigure Storage Metrics in your storage account by using hello Azure PowerShell cmdlet Get-AzureStorageServiceMetricsProperty tooretrieve hello current settings, and hello cmdlet Set-AzureStorageServiceMetricsProperty toochange hello current settings.</span></span>

<span data-ttu-id="a6481-122">les applets de commande Hello qui contrôlent Storage Metrics utilisent hello paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="a6481-122">hello cmdlets that control Storage Metrics use hello following parameters:</span></span>

* <span data-ttu-id="a6481-123">MetricsType peut avoir pour valeur Hour ou Minute.</span><span class="sxs-lookup"><span data-stu-id="a6481-123">MetricsType: possible values are Hour and Minute.</span></span>
* <span data-ttu-id="a6481-124">ServiceType peut avoir pour valeur Blob, Queue ou Table.</span><span class="sxs-lookup"><span data-stu-id="a6481-124">ServiceType: possible values are Blob, Queue, and Table.</span></span>
* <span data-ttu-id="a6481-125">MetricsLevel peut avoir pour valeur None, Service et ServiceAndApi.</span><span class="sxs-lookup"><span data-stu-id="a6481-125">MetricsLevel: possible values are None, Service, and ServiceAndApi.</span></span>

<span data-ttu-id="a6481-126">Par exemple, hello commande suivante active minute métriques pour le service d’objets Blob hello dans votre compte de stockage par défaut avec la période de rétention hello de définir les jours de toofive :</span><span class="sxs-lookup"><span data-stu-id="a6481-126">For example, hello following command switches on minute metrics for hello Blob service in your default storage account with hello retention period set toofive days:</span></span>

```powershell
Set-AzureStorageServiceMetricsProperty -MetricsType Minute -ServiceType Blob -MetricsLevel ServiceAndApi  -RetentionDays 5`
```

<span data-ttu-id="a6481-127">Hello commande suivante récupère hello actuel toutes les heures des métriques niveau et rétention en jours pour le service d’objets blob hello dans votre compte de stockage par défaut :</span><span class="sxs-lookup"><span data-stu-id="a6481-127">hello following command retrieves hello current hourly metrics level and retention days for hello blob service in your default storage account:</span></span>

```powershell
Get-AzureStorageServiceMetricsProperty -MetricsType Hour -ServiceType Blob
```

<span data-ttu-id="a6481-128">Pour plus d’informations sur comment tooconfigure hello le toowork d’applets de commande Azure PowerShell avec votre abonnement Azure et comment tooselect hello du stockage par défaut de compte toouse, consultez : [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a6481-128">For information about how tooconfigure hello Azure PowerShell cmdlets toowork with your Azure subscription and how tooselect hello default storage account toouse, see: [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="how-tooenable-storage-metrics-programmatically"></a><span data-ttu-id="a6481-129">Comment tooenable Storage metrics par programmation</span><span class="sxs-lookup"><span data-stu-id="a6481-129">How tooenable Storage metrics programmatically</span></span>
<span data-ttu-id="a6481-130">Hello suivant extrait de code c# montre comment tooenable métriques et la journalisation pour le service de l’objet Blob hello à l’aide hello bibliothèque cliente de stockage pour .NET :</span><span class="sxs-lookup"><span data-stu-id="a6481-130">hello following C# snippet shows how tooenable metrics and logging for hello Blob service using hello storage client library for .NET:</span></span>

```csharp
//Parse hello connection string for hello storage account.
const string ConnectionString = "DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key";
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);

// Create service client for credentialed access toohello Blob service.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Enable Storage Analytics logging and set retention policy too10 days.
ServiceProperties properties = new ServiceProperties();
properties.Logging.LoggingOperations = LoggingOperations.All;
properties.Logging.RetentionDays = 10;
properties.Logging.Version = "1.0";

// Configure service properties for metrics. Both metrics and logging must be set at hello same time.
properties.HourMetrics.MetricsLevel = MetricsLevel.ServiceAndApi;
properties.HourMetrics.RetentionDays = 10;
properties.HourMetrics.Version = "1.0";

properties.MinuteMetrics.MetricsLevel = MetricsLevel.ServiceAndApi;
properties.MinuteMetrics.RetentionDays = 10;
properties.MinuteMetrics.Version = "1.0";

// Set hello default service version toobe used for anonymous requests.
properties.DefaultServiceVersion = "2015-04-05";

// Set hello service properties.
blobClient.SetServiceProperties(properties);
```

## <a name="viewing-storage-metrics"></a><span data-ttu-id="a6481-131">Affichage des métriques de stockage</span><span class="sxs-lookup"><span data-stu-id="a6481-131">Viewing Storage metrics</span></span>
<span data-ttu-id="a6481-132">Après avoir configuré le stockage Analytique métriques toomonitor votre compte de stockage, stockage Analytique enregistre les métriques hello dans un ensemble de tables connues dans votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="a6481-132">After you configure Storage Analytics metrics toomonitor your storage account, Storage Analytics records hello metrics in a set of well-known tables in your storage account.</span></span> <span data-ttu-id="a6481-133">Vous pouvez configurer les métriques de graphiques tooview Bonjour [portail Azure](https://portal.azure.com):</span><span class="sxs-lookup"><span data-stu-id="a6481-133">You can configure charts tooview hourly metrics in hello [Azure portal](https://portal.azure.com):</span></span>

1. <span data-ttu-id="a6481-134">Accédez de compte de stockage tooyour Bonjour [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a6481-134">Navigate tooyour storage account in hello [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="a6481-135">Sélectionnez **métriques** Bonjour **Menu** panneau pour hello dont les métriques de service souhaité tooview.</span><span class="sxs-lookup"><span data-stu-id="a6481-135">Select **Metrics** in hello **Menu** blade for hello service whose metrics you want tooview.</span></span>
1. <span data-ttu-id="a6481-136">Sélectionnez **modifier** sur le graphique de hello souhaité tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="a6481-136">Select **Edit** on hello chart you want tooconfigure.</span></span>
1. <span data-ttu-id="a6481-137">Bonjour **modifier le graphique** panneau, sélectionnez hello **période**, **type de graphique**et des mesures hello à afficher dans le graphique de hello.</span><span class="sxs-lookup"><span data-stu-id="a6481-137">In hello **Edit Chart** blade, select hello **Time Range**, **Chart type**, and hello metrics you want displayed in hello chart.</span></span>
1. <span data-ttu-id="a6481-138">Sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="a6481-138">Select **OK**</span></span>

<span data-ttu-id="a6481-139">Si vous souhaitez que les métriques de hello toodownload pour le stockage à long terme ou tooanalyze les localement, vous devez :</span><span class="sxs-lookup"><span data-stu-id="a6481-139">If you want toodownload hello metrics for long-term storage or tooanalyze them locally, you will need to:</span></span>

* <span data-ttu-id="a6481-140">Utiliser un outil qui tient compte de ces tables et vous tooview et de les télécharger.</span><span class="sxs-lookup"><span data-stu-id="a6481-140">Use a tool that is aware of these tables and will allow you tooview and download them.</span></span>
* <span data-ttu-id="a6481-141">Écrire un tooread personnalisé de l’application ou le script et stocker les tables hello.</span><span class="sxs-lookup"><span data-stu-id="a6481-141">Write a custom application or script tooread and store hello tables.</span></span>

<span data-ttu-id="a6481-142">Nombreux outils de consultation du stockage tiers ont connaissance de ces tables et vous permettre de tooview directement.</span><span class="sxs-lookup"><span data-stu-id="a6481-142">Many third-party storage-browsing tools are aware of these tables and enable you tooview them directly.</span></span>
<span data-ttu-id="a6481-143">Pour obtenir la liste des outils disponibles, consultez [Outils clients Azure Storage](storage-explorers.md) .</span><span class="sxs-lookup"><span data-stu-id="a6481-143">Please see [Azure Storage Client Tools](storage-explorers.md) for a list of available tools.</span></span>

> [!NOTE]
> <span data-ttu-id="a6481-144">Depuis la version 0.8.0 de hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/), vous pouvez afficher et télécharger des tables de métriques hello analytique.</span><span class="sxs-lookup"><span data-stu-id="a6481-144">Starting with version 0.8.0 of hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/), you can view and download hello analytics metrics tables.</span></span>
> 
> 

<span data-ttu-id="a6481-145">Dans analytique de commande tooaccess hello tables par programme, notez que les tables d’analytique hello n’apparaissent pas si vous répertoriez toutes les tables hello dans votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="a6481-145">In order tooaccess hello analytics tables programmatically, do note that hello analytics tables do not appear if you list all hello tables in your storage account.</span></span> <span data-ttu-id="a6481-146">Vous pouvez y accéder directement par nom ou utilisez hello [CloudAnalyticsClient API](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.analytics.cloudanalyticsclient.aspx) dans les noms de table hello .NET client bibliothèque tooquery hello.</span><span class="sxs-lookup"><span data-stu-id="a6481-146">You can either access them directly by name, or use hello [CloudAnalyticsClient API](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.analytics.cloudanalyticsclient.aspx) in hello .NET client library tooquery hello table names.</span></span>

### <a name="hourly-metrics"></a><span data-ttu-id="a6481-147">Métriques toutes les heures</span><span class="sxs-lookup"><span data-stu-id="a6481-147">Hourly metrics</span></span>
* <span data-ttu-id="a6481-148">$MetricsHourPrimaryTransactionsBlob</span><span class="sxs-lookup"><span data-stu-id="a6481-148">$MetricsHourPrimaryTransactionsBlob</span></span>
* <span data-ttu-id="a6481-149">$MetricsHourPrimaryTransactionsTable</span><span class="sxs-lookup"><span data-stu-id="a6481-149">$MetricsHourPrimaryTransactionsTable</span></span>
* <span data-ttu-id="a6481-150">$MetricsHourPrimaryTransactionsQueue</span><span class="sxs-lookup"><span data-stu-id="a6481-150">$MetricsHourPrimaryTransactionsQueue</span></span>

### <a name="minute-metrics"></a><span data-ttu-id="a6481-151">Métriques par minute</span><span class="sxs-lookup"><span data-stu-id="a6481-151">Minute metrics</span></span>
* <span data-ttu-id="a6481-152">$MetricsMinutePrimaryTransactionsBlob</span><span class="sxs-lookup"><span data-stu-id="a6481-152">$MetricsMinutePrimaryTransactionsBlob</span></span>
* <span data-ttu-id="a6481-153">$MetricsMinutePrimaryTransactionsTable</span><span class="sxs-lookup"><span data-stu-id="a6481-153">$MetricsMinutePrimaryTransactionsTable</span></span>
* <span data-ttu-id="a6481-154">$MetricsMinutePrimaryTransactionsQueue</span><span class="sxs-lookup"><span data-stu-id="a6481-154">$MetricsMinutePrimaryTransactionsQueue</span></span>

### <a name="capacity"></a><span data-ttu-id="a6481-155">Capacité</span><span class="sxs-lookup"><span data-stu-id="a6481-155">Capacity</span></span>
* <span data-ttu-id="a6481-156">$MetricsCapacityBlob</span><span class="sxs-lookup"><span data-stu-id="a6481-156">$MetricsCapacityBlob</span></span>

<span data-ttu-id="a6481-157">Vous trouverez des informations complètes sur les schémas hello pour ces tables, consultez [schéma de Table de métriques Storage Analytique](https://msdn.microsoft.com/library/azure/hh343264.aspx).</span><span class="sxs-lookup"><span data-stu-id="a6481-157">You can find full details of hello schemas for these tables at [Storage Analytics Metrics Table Schema](https://msdn.microsoft.com/library/azure/hh343264.aspx).</span></span> <span data-ttu-id="a6481-158">lignes d’exemple Hello ci-dessous montrent uniquement un sous-ensemble de colonnes hello disponibles, mais illustrent certaines fonctionnalités importantes de façon hello que Storage Metrics enregistre ces métriques :</span><span class="sxs-lookup"><span data-stu-id="a6481-158">hello sample rows below show only a subset of hello columns available, but illustrate some important features of hello way Storage Metrics saves these metrics:</span></span>

| <span data-ttu-id="a6481-159">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="a6481-159">PartitionKey</span></span> | <span data-ttu-id="a6481-160">RowKey</span><span class="sxs-lookup"><span data-stu-id="a6481-160">RowKey</span></span> | <span data-ttu-id="a6481-161">Timestamp</span><span class="sxs-lookup"><span data-stu-id="a6481-161">Timestamp</span></span> | <span data-ttu-id="a6481-162">TotalRequests</span><span class="sxs-lookup"><span data-stu-id="a6481-162">TotalRequests</span></span> | <span data-ttu-id="a6481-163">TotalBillableRequests</span><span class="sxs-lookup"><span data-stu-id="a6481-163">TotalBillableRequests</span></span> | <span data-ttu-id="a6481-164">TotalIngress</span><span class="sxs-lookup"><span data-stu-id="a6481-164">TotalIngress</span></span> | <span data-ttu-id="a6481-165">TotalEgress</span><span class="sxs-lookup"><span data-stu-id="a6481-165">TotalEgress</span></span> | <span data-ttu-id="a6481-166">Availability</span><span class="sxs-lookup"><span data-stu-id="a6481-166">Availability</span></span> | <span data-ttu-id="a6481-167">AverageE2ELatency</span><span class="sxs-lookup"><span data-stu-id="a6481-167">AverageE2ELatency</span></span> | <span data-ttu-id="a6481-168">AverageServerLatency</span><span class="sxs-lookup"><span data-stu-id="a6481-168">AverageServerLatency</span></span> | <span data-ttu-id="a6481-169">PercentSuccess</span><span class="sxs-lookup"><span data-stu-id="a6481-169">PercentSuccess</span></span> |
| --- |:---:| ---:| --- | --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="a6481-170">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="a6481-170">20140522T1100</span></span> |<span data-ttu-id="a6481-171">user;All</span><span class="sxs-lookup"><span data-stu-id="a6481-171">user;All</span></span> |<span data-ttu-id="a6481-172">2014-05-22T11:01:16.7650250Z</span><span class="sxs-lookup"><span data-stu-id="a6481-172">2014-05-22T11:01:16.7650250Z</span></span> |<span data-ttu-id="a6481-173">7</span><span class="sxs-lookup"><span data-stu-id="a6481-173">7</span></span> |<span data-ttu-id="a6481-174">7</span><span class="sxs-lookup"><span data-stu-id="a6481-174">7</span></span> |<span data-ttu-id="a6481-175">4003</span><span class="sxs-lookup"><span data-stu-id="a6481-175">4003</span></span> |<span data-ttu-id="a6481-176">46801</span><span class="sxs-lookup"><span data-stu-id="a6481-176">46801</span></span> |<span data-ttu-id="a6481-177">100</span><span class="sxs-lookup"><span data-stu-id="a6481-177">100</span></span> |<span data-ttu-id="a6481-178">104.4286</span><span class="sxs-lookup"><span data-stu-id="a6481-178">104.4286</span></span> |<span data-ttu-id="a6481-179">6.857143</span><span class="sxs-lookup"><span data-stu-id="a6481-179">6.857143</span></span> |<span data-ttu-id="a6481-180">100</span><span class="sxs-lookup"><span data-stu-id="a6481-180">100</span></span> |
| <span data-ttu-id="a6481-181">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="a6481-181">20140522T1100</span></span> |<span data-ttu-id="a6481-182">user;QueryEntities</span><span class="sxs-lookup"><span data-stu-id="a6481-182">user;QueryEntities</span></span> |<span data-ttu-id="a6481-183">2014-05-22T11:01:16.7640250Z</span><span class="sxs-lookup"><span data-stu-id="a6481-183">2014-05-22T11:01:16.7640250Z</span></span> |<span data-ttu-id="a6481-184">5</span><span class="sxs-lookup"><span data-stu-id="a6481-184">5</span></span> |<span data-ttu-id="a6481-185">5</span><span class="sxs-lookup"><span data-stu-id="a6481-185">5</span></span> |<span data-ttu-id="a6481-186">2694</span><span class="sxs-lookup"><span data-stu-id="a6481-186">2694</span></span> |<span data-ttu-id="a6481-187">45951</span><span class="sxs-lookup"><span data-stu-id="a6481-187">45951</span></span> |<span data-ttu-id="a6481-188">100</span><span class="sxs-lookup"><span data-stu-id="a6481-188">100</span></span> |<span data-ttu-id="a6481-189">143.8</span><span class="sxs-lookup"><span data-stu-id="a6481-189">143.8</span></span> |<span data-ttu-id="a6481-190">7.8</span><span class="sxs-lookup"><span data-stu-id="a6481-190">7.8</span></span> |<span data-ttu-id="a6481-191">100</span><span class="sxs-lookup"><span data-stu-id="a6481-191">100</span></span> |
| <span data-ttu-id="a6481-192">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="a6481-192">20140522T1100</span></span> |<span data-ttu-id="a6481-193">user;QueryEntity</span><span class="sxs-lookup"><span data-stu-id="a6481-193">user;QueryEntity</span></span> |<span data-ttu-id="a6481-194">2014-05-22T11:01:16.7650250Z</span><span class="sxs-lookup"><span data-stu-id="a6481-194">2014-05-22T11:01:16.7650250Z</span></span> |<span data-ttu-id="a6481-195">1</span><span class="sxs-lookup"><span data-stu-id="a6481-195">1</span></span> |<span data-ttu-id="a6481-196">1</span><span class="sxs-lookup"><span data-stu-id="a6481-196">1</span></span> |<span data-ttu-id="a6481-197">538</span><span class="sxs-lookup"><span data-stu-id="a6481-197">538</span></span> |<span data-ttu-id="a6481-198">633</span><span class="sxs-lookup"><span data-stu-id="a6481-198">633</span></span> |<span data-ttu-id="a6481-199">100</span><span class="sxs-lookup"><span data-stu-id="a6481-199">100</span></span> |<span data-ttu-id="a6481-200">3</span><span class="sxs-lookup"><span data-stu-id="a6481-200">3</span></span> |<span data-ttu-id="a6481-201">3</span><span class="sxs-lookup"><span data-stu-id="a6481-201">3</span></span> |<span data-ttu-id="a6481-202">100</span><span class="sxs-lookup"><span data-stu-id="a6481-202">100</span></span> |
| <span data-ttu-id="a6481-203">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="a6481-203">20140522T1100</span></span> |<span data-ttu-id="a6481-204">user;UpdateEntity</span><span class="sxs-lookup"><span data-stu-id="a6481-204">user;UpdateEntity</span></span> |<span data-ttu-id="a6481-205">2014-05-22T11:01:16.7650250Z</span><span class="sxs-lookup"><span data-stu-id="a6481-205">2014-05-22T11:01:16.7650250Z</span></span> |<span data-ttu-id="a6481-206">1</span><span class="sxs-lookup"><span data-stu-id="a6481-206">1</span></span> |<span data-ttu-id="a6481-207">1</span><span class="sxs-lookup"><span data-stu-id="a6481-207">1</span></span> |<span data-ttu-id="a6481-208">771</span><span class="sxs-lookup"><span data-stu-id="a6481-208">771</span></span> |<span data-ttu-id="a6481-209">217</span><span class="sxs-lookup"><span data-stu-id="a6481-209">217</span></span> |<span data-ttu-id="a6481-210">100</span><span class="sxs-lookup"><span data-stu-id="a6481-210">100</span></span> |<span data-ttu-id="a6481-211">9</span><span class="sxs-lookup"><span data-stu-id="a6481-211">9</span></span> |<span data-ttu-id="a6481-212">6</span><span class="sxs-lookup"><span data-stu-id="a6481-212">6</span></span> |<span data-ttu-id="a6481-213">100</span><span class="sxs-lookup"><span data-stu-id="a6481-213">100</span></span> |

<span data-ttu-id="a6481-214">Dans cet exemple de données de mesure des minutes, clé de partition hello sollicitent hello à la résolution d’une minute.</span><span class="sxs-lookup"><span data-stu-id="a6481-214">In this example minute metrics data, hello partition key uses hello time at minute resolution.</span></span> <span data-ttu-id="a6481-215">clé de ligne Hello identifie le type hello des informations qui sont stockées dans la ligne de hello et elle se compose de deux éléments d’information, type d’accès hello et type de demande de hello :</span><span class="sxs-lookup"><span data-stu-id="a6481-215">hello row key identifies hello type of information that is stored in hello row and this is composed of two pieces of information, hello access type, and hello request type:</span></span>

* <span data-ttu-id="a6481-216">type d’accès Hello est utilisateur ou système, où utilisateur désigne le service de stockage tooall utilisateur demandes toohello et système toorequests apportées par stockage Analytique.</span><span class="sxs-lookup"><span data-stu-id="a6481-216">hello access type is either user or system, where user refers tooall user requests toohello storage service, and system refers toorequests made by Storage Analytics.</span></span>
* <span data-ttu-id="a6481-217">type de demande de Hello est dans ce cas il s’agit d’une ligne de résumé, ou il identifie hello les API spécifiques telles que QueryEntity ou UpdateEntity.</span><span class="sxs-lookup"><span data-stu-id="a6481-217">hello request type is either all in which case it is a summary line, or it identifies hello specific API such as QueryEntity or UpdateEntity.</span></span>

<span data-ttu-id="a6481-218">données d’exemple Hello ci-dessus montre que tous les hello enregistre pour une seule minute (commence à 11 h 00), ce nombre de hello de demandes de QueryEntities plus hello nombre de demandes de QueryEntity plus nombre hello de demandes de UpdateEntity additionner tooseven, qui est hello total indiqué sur ligne d’user : All Hello.</span><span class="sxs-lookup"><span data-stu-id="a6481-218">hello sample data above shows all hello records for a single minute (starting at 11:00AM), so hello number of QueryEntities requests plus hello number of QueryEntity requests plus hello number of UpdateEntity requests add up tooseven, which is hello total shown on hello user:All row.</span></span> <span data-ttu-id="a6481-219">De même, vous pouvez dériver la latence de bout en bout moyenne hello (104,4286) sur la ligne d’user : All hello en calculant ((143.8 * 5) + 3 + 9) / 7.</span><span class="sxs-lookup"><span data-stu-id="a6481-219">Similarly, you can derive hello average end-to-end latency 104.4286 on hello user:All row by calculating ((143.8 * 5) + 3 + 9)/7.</span></span>

## <a name="metrics-alerts"></a><span data-ttu-id="a6481-220">Alertes liées aux métriques</span><span class="sxs-lookup"><span data-stu-id="a6481-220">Metrics alerts</span></span>
<span data-ttu-id="a6481-221">Vous devez envisager de définir des alertes Bonjour [portail Azure](https://portal.azure.com) afin de Storage Metrics puisse vous avertir automatiquement d’importantes modifications de comportement hello de vos services de stockage.</span><span class="sxs-lookup"><span data-stu-id="a6481-221">You should consider setting up alerts in hello [Azure portal](https://portal.azure.com) so Storage Metrics can automatically notify you of important changes in hello behavior of your storage services.</span></span> <span data-ttu-id="a6481-222">Si vous utilisez un toodownload d’outil de l’Explorateur de stockage de ces données métriques dans un format délimité, vous pouvez utiliser les données de Microsoft Excel tooanalyze hello.</span><span class="sxs-lookup"><span data-stu-id="a6481-222">If you use a storage explorer tool toodownload this metrics data in a delimited format, you can use Microsoft Excel tooanalyze hello data.</span></span> <span data-ttu-id="a6481-223">Pour obtenir la liste des outils d’exploration du stockage disponibles, consultez [Outils clients Azure Storage](storage-explorers.md) .</span><span class="sxs-lookup"><span data-stu-id="a6481-223">See [Azure Storage Client Tools](storage-explorers.md) for a list of available storage explorer tools.</span></span> <span data-ttu-id="a6481-224">Vous pouvez configurer des alertes dans hello **règles d’alerte** panneau, accessible sous **analyse** dans le panneau de menu de compte de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="a6481-224">You can configure alerts in hello **Alert rules** blade, accessible under **Monitoring** in hello Storage account menu blade.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a6481-225">Il peut y avoir un délai entre un événement de stockage et quand hello correspondant de données de métriques par heure ou minute est enregistré.</span><span class="sxs-lookup"><span data-stu-id="a6481-225">There may be a delay between a storage event and when hello corresponding hourly or minute metrics data is recorded.</span></span> <span data-ttu-id="a6481-226">Dans les cas de hello de métriques par minute, plusieurs minutes de données peuvent être écrit à la fois.</span><span class="sxs-lookup"><span data-stu-id="a6481-226">In hello case of minute metrics, several minutes of data may be written at once.</span></span> <span data-ttu-id="a6481-227">Cela peut entraîner des tootransactions des minutes précédentes en cours d’agrégation dans une transaction de hello pour hello minute en cours.</span><span class="sxs-lookup"><span data-stu-id="a6481-227">This can lead tootransactions from earlier minutes being aggregated into hello transaction for hello current minute.</span></span> <span data-ttu-id="a6481-228">Dans ce cas, alerte hello service devra peut-être pas toutes les données de métriques disponibles pour hello configuré intervalle d’alerte, ce qui peut entraîner des tooalerts déclencher de manière inattendue.</span><span class="sxs-lookup"><span data-stu-id="a6481-228">When this happens, hello alert service may not have all available metrics data for hello configured alert interval, which may lead tooalerts firing unexpectedly.</span></span>
>

## <a name="accessing-metrics-data-programmatically"></a><span data-ttu-id="a6481-229">Accès aux données de métriques par programmation</span><span class="sxs-lookup"><span data-stu-id="a6481-229">Accessing metrics data programmatically</span></span>
<span data-ttu-id="a6481-230">Hello ci-dessous montre exemple code c# qui accède aux métriques par minute hello pour une plage de minutes et affiche les résultats de hello dans une fenêtre de console.</span><span class="sxs-lookup"><span data-stu-id="a6481-230">hello following listing shows sample C# code that accesses hello minute metrics for a range of minutes and displays hello results in a console Window.</span></span> <span data-ttu-id="a6481-231">Il utilise hello version 4 incluant hello classe CloudAnalyticsClient qui simplifie l’accès aux tables de métriques hello dans le stockage de bibliothèque de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="a6481-231">It uses hello Azure Storage Library version 4 that includes hello CloudAnalyticsClient class that simplifies accessing hello metrics tables in storage.</span></span>

```csharp
private static void PrintMinuteMetrics(CloudAnalyticsClient analyticsClient, DateTimeOffset startDateTime, DateTimeOffset endDateTime)
{
    // Convert hello dates toohello format used in hello PartitionKey
    var start = startDateTime.ToUniversalTime().ToString("yyyyMMdd'T'HHmm");
    var end = endDateTime.ToUniversalTime().ToString("yyyyMMdd'T'HHmm");

    var services = Enum.GetValues(typeof(StorageService));
    foreach (StorageService service in services)
    {
        Console.WriteLine("Minute Metrics for Service {0} from {1} too{2} UTC", service, start, end);
        var metricsQuery = analyticsClient.CreateMinuteMetricsQuery(service, StorageLocation.Primary);
        var t = analyticsClient.GetMinuteMetricsTable(service);
        var opContext = new OperationContext();
        var query =
          from entity in metricsQuery
          // Note, you can't filter using hello entity properties Time, AccessType, or TransactionType
          // because they are calculated fields in hello MetricsEntity class.
          // hello PartitionKey identifies hello DataTime of hello metrics.
          where entity.PartitionKey.CompareTo(start) >= 0 && entity.PartitionKey.CompareTo(end) <= 0
        select entity;

        // Filter on "user" transactions after fetching hello metrics from Table Storage.
        // (StartsWith is not supported using LINQ with Azure table storage)
        var results = query.ToList().Where(m => m.RowKey.StartsWith("user"));
        var resultString = results.Aggregate(new StringBuilder(), (builder, metrics) => builder.AppendLine(MetricsString(metrics, opContext))).ToString();
        Console.WriteLine(resultString);
    }
}

private static string MetricsString(MetricsEntity entity, OperationContext opContext)
{
    var entityProperties = entity.WriteEntity(opContext);
    var entityString =
      string.Format("Time: {0}, ", entity.Time) +
      string.Format("AccessType: {0}, ", entity.AccessType) +
      string.Format("TransactionType: {0}, ", entity.TransactionType) +
      string.Join(",", entityProperties.Select(e => new KeyValuePair<string, string>(e.Key.ToString(), e.Value.PropertyAsObject.ToString())));
    return entityString;
}
```

## <a name="what-charges-do-you-incur-when-you-enable-storage-metrics"></a><span data-ttu-id="a6481-232">Quels sont les frais encourus quand vous activez les métriques de stockage ?</span><span class="sxs-lookup"><span data-stu-id="a6481-232">What charges do you incur when you enable storage metrics?</span></span>
<span data-ttu-id="a6481-233">Écrire des entités de table toocreate de demandes pour les métriques sont facturées au hello des frais standard applicables tooall Azure des opérations de stockage.</span><span class="sxs-lookup"><span data-stu-id="a6481-233">Write requests toocreate table entities for metrics are charged at hello standard rates applicable tooall Azure Storage operations.</span></span>

<span data-ttu-id="a6481-234">Les demandes de lecture et de suppression par une toometrics les données client sont aussi facturées au tarif standard.</span><span class="sxs-lookup"><span data-stu-id="a6481-234">Read and delete requests by a client toometrics data are also billable at standard rates.</span></span> <span data-ttu-id="a6481-235">Si vous avez configuré une stratégie de rétention des données, vous n’êtes pas facturé quand Azure Storage supprime les anciennes données de métriques.</span><span class="sxs-lookup"><span data-stu-id="a6481-235">If you have configured a data retention policy, you are not charged when Azure Storage deletes old metrics data.</span></span> <span data-ttu-id="a6481-236">Toutefois, si vous supprimez les données analytique, votre compte est facturé pour les opérations de suppression hello.</span><span class="sxs-lookup"><span data-stu-id="a6481-236">However, if you delete analytics data, your account is charged for hello delete operations.</span></span>

<span data-ttu-id="a6481-237">capacité de Hello utilisée par les tables de métriques hello est également facturable : vous pouvez utiliser hello suivant le montant de hello tooestimate de capacité utilisée pour stocker les données de métriques :</span><span class="sxs-lookup"><span data-stu-id="a6481-237">hello capacity used by hello metrics tables is also billable: you can use hello following tooestimate hello amount of capacity used for storing metrics data:</span></span>

* <span data-ttu-id="a6481-238">Si chaque heure un service qui utilise des API de chaque service, environ 148 Ko de données sont stockée toutes les heures dans les tables de transaction de métriques hello si vous avez activé le service et le niveau de l’API résumé.</span><span class="sxs-lookup"><span data-stu-id="a6481-238">If each hour a service utilizes every API in every service, then approximately 148KB of data is stored every hour in hello metrics transaction tables if you have enabled both service and API level summary.</span></span>
* <span data-ttu-id="a6481-239">Si chaque heure un service qui utilise des API de chaque service, environ 12 Ko de données sont stockée toutes les heures dans les tables de transaction de métriques hello si vous avez activé uniquement service au niveau du résumé.</span><span class="sxs-lookup"><span data-stu-id="a6481-239">If each hour a service utilizes every API in every service, then approximately 12KB of data is stored every hour in hello metrics transaction tables if you have enabled just service level summary.</span></span>
* <span data-ttu-id="a6481-240">table de capacité pour les objets BLOB Hello a deux lignes sont ajoutées chaque jour (si l’utilisateur a activé les journaux) : cela signifie que chaque taille de hello jour de cette table augmente par des tooapproximately 300 octets.</span><span class="sxs-lookup"><span data-stu-id="a6481-240">hello capacity table for blobs has two rows added each day (provided user has opted in for logs): this implies that every day hello size of this table increases by up tooapproximately 300 bytes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a6481-241">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a6481-241">Next steps</span></span>
[<span data-ttu-id="a6481-242">Activation de la journalisation du stockage et accès aux données des journaux</span><span class="sxs-lookup"><span data-stu-id="a6481-242">Enabling Storage Logging and Accessing Log Data</span></span>](/rest/api/storageservices/Enabling-Storage-Logging-and-Accessing-Log-Data)
