---
title: "Activation des métriques de stockage dans le portail Azure | Microsoft Docs"
description: "Activation des métriques de stockage pour les services d’objet Blob, de File d’attente, de Table et de Fichier"
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
ms.openlocfilehash: 1525a2258dd6ab8e72e8607826523eca8121483c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="enabling-azure-storage-metrics-and-viewing-metrics-data"></a><span data-ttu-id="28a81-103">Activation des métriques Azure Storage et affichage des données associées</span><span class="sxs-lookup"><span data-stu-id="28a81-103">Enabling Azure Storage metrics and viewing metrics data</span></span>
[!INCLUDE [storage-selector-portal-enable-and-view-metrics](../../../includes/storage-selector-portal-enable-and-view-metrics.md)]

## <a name="overview"></a><span data-ttu-id="28a81-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="28a81-104">Overview</span></span>
<span data-ttu-id="28a81-105">Storage Metrics est activé par défaut lorsque vous créez un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="28a81-105">Storage Metrics is enabled by default when you create a new storage account.</span></span> <span data-ttu-id="28a81-106">Vous pouvez configurer la surveillance par le biais du [Portail Azure](https://portal.azure.com) ou de Windows PowerShell, ou par programme au moyen d’une des bibliothèques clientes de stockage.</span><span class="sxs-lookup"><span data-stu-id="28a81-106">You can configure monitoring via the [Azure portal](https://portal.azure.com) or Windows PowerShell, or programmatically via one of the storage client libraries.</span></span>

<span data-ttu-id="28a81-107">Vous pouvez choisir une période de rétention des données : cette période détermine combien de temps le service de stockage conserve les métriques et la durée pendant laquelle l’espace requis pour les stocker vous est facturé.</span><span class="sxs-lookup"><span data-stu-id="28a81-107">You can configure a retention period for the metrics data: this period determines for how long the storage service keeps the metrics and charges you for the space required to store them.</span></span> <span data-ttu-id="28a81-108">En règle générale, il est recommandé d’utiliser une période de rétention plus courte pour les métriques par minute que pour les métriques par heure, en raison de l’espace supplémentaire requis.</span><span class="sxs-lookup"><span data-stu-id="28a81-108">Typically, you should use a shorter retention period for minute metrics than hourly metrics because of the significant extra space required for minute metrics.</span></span> <span data-ttu-id="28a81-109">La période de rétention que vous définissez doit être suffisamment longue pour vous donner le temps d’analyser les données et de télécharger les métriques à conserver à des fins d’analyse ou de création de rapports hors connexion.</span><span class="sxs-lookup"><span data-stu-id="28a81-109">You should choose a retention period such that you have sufficient time to analyze the data and download any metrics you wish to keep for off-line analysis or reporting purposes.</span></span> <span data-ttu-id="28a81-110">N’oubliez pas que le téléchargement des données de métriques depuis votre compte de stockage est aussi facturé.</span><span class="sxs-lookup"><span data-stu-id="28a81-110">Remember that you will also be billed for downloading metrics data from your storage account.</span></span>

## <a name="how-to-enable-metrics-using-the-azure-portal"></a><span data-ttu-id="28a81-111">Activer les mesures à l’aide du Portail Azure</span><span class="sxs-lookup"><span data-stu-id="28a81-111">How to enable metrics using the Azure portal</span></span>
<span data-ttu-id="28a81-112">Pour activer les mesures dans le [Portail Azure](https://portal.azure.com), suivez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="28a81-112">Follow these steps to enable metrics in the [Azure portal](https://portal.azure.com):</span></span>

1. <span data-ttu-id="28a81-113">Accédez à votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="28a81-113">Navigate to your storage account.</span></span>
1. <span data-ttu-id="28a81-114">Sélectionnez **Diagnostics** sur le panneau **Menu**.</span><span class="sxs-lookup"><span data-stu-id="28a81-114">Select **Diagnostics** on the **Menu** blade</span></span>
1. <span data-ttu-id="28a81-115">Vérifiez que l’option **État** est définie sur **Activé**.</span><span class="sxs-lookup"><span data-stu-id="28a81-115">Ensure that **Status** is set to **On**.</span></span>
1. <span data-ttu-id="28a81-116">Sélectionnez les métriques des services que vous souhaitez surveiller.</span><span class="sxs-lookup"><span data-stu-id="28a81-116">Select the metrics for the services you wish to monitor.</span></span>
1. <span data-ttu-id="28a81-117">Spécifiez une stratégie de rétention pour indiquer la durée de conservation des métriques et de journalisation des données.</span><span class="sxs-lookup"><span data-stu-id="28a81-117">Specify a retention policy to indicate how long to retain metrics and log data.</span></span>
1. <span data-ttu-id="28a81-118">Sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="28a81-118">Select **Save**.</span></span>

<span data-ttu-id="28a81-119">Notez qu’actuellement le [Portail Azure](https://portal.azure.com) ne vous permet pas de configurer des mesures par minute dans votre compte de stockage ; vous devez les activer avec PowerShell ou par programmation.</span><span class="sxs-lookup"><span data-stu-id="28a81-119">Note that the [Azure portal](https://portal.azure.com) does not currently enable you to configure minute metrics in your storage account; you must enable minute metrics using PowerShell or programmatically.</span></span>

## <a name="how-to-enable-metrics-using-powershell"></a><span data-ttu-id="28a81-120">Comment activer les métriques à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="28a81-120">How to enable metrics using PowerShell</span></span>
<span data-ttu-id="28a81-121">Vous pouvez utiliser PowerShell sur votre ordinateur local pour configurer Storage Metrics dans votre compte de stockage. Utilisez l’applet de commande Azure PowerShell Get-AzureStorageServiceMetricsProperty pour récupérer les paramètres actuels et l’applet de commande Set-AzureStorageServiceMetricsProperty pour modifier les paramètres actuels.</span><span class="sxs-lookup"><span data-stu-id="28a81-121">You can use PowerShell on your local machine to configure Storage Metrics in your storage account by using the Azure PowerShell cmdlet Get-AzureStorageServiceMetricsProperty to retrieve the current settings, and the cmdlet Set-AzureStorageServiceMetricsProperty to change the current settings.</span></span>

<span data-ttu-id="28a81-122">Les applets de commande qui contrôlent Storage Metrics utilisent les paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="28a81-122">The cmdlets that control Storage Metrics use the following parameters:</span></span>

* <span data-ttu-id="28a81-123">MetricsType peut avoir pour valeur Hour ou Minute.</span><span class="sxs-lookup"><span data-stu-id="28a81-123">MetricsType: possible values are Hour and Minute.</span></span>
* <span data-ttu-id="28a81-124">ServiceType peut avoir pour valeur Blob, Queue ou Table.</span><span class="sxs-lookup"><span data-stu-id="28a81-124">ServiceType: possible values are Blob, Queue, and Table.</span></span>
* <span data-ttu-id="28a81-125">MetricsLevel peut avoir pour valeur None, Service et ServiceAndApi.</span><span class="sxs-lookup"><span data-stu-id="28a81-125">MetricsLevel: possible values are None, Service, and ServiceAndApi.</span></span>

<span data-ttu-id="28a81-126">Par exemple, la commande suivante active les métriques par minute pour le service BLOB dans votre compte de stockage par défaut avec une période de rétention de cinq jours :</span><span class="sxs-lookup"><span data-stu-id="28a81-126">For example, the following command switches on minute metrics for the Blob service in your default storage account with the retention period set to five days:</span></span>

```powershell
Set-AzureStorageServiceMetricsProperty -MetricsType Minute -ServiceType Blob -MetricsLevel ServiceAndApi  -RetentionDays 5`
```

<span data-ttu-id="28a81-127">La commande suivante récupère le niveau actuel des métriques par heure et la période de rétention en jours pour le service BLOB dans votre compte de stockage par défaut :</span><span class="sxs-lookup"><span data-stu-id="28a81-127">The following command retrieves the current hourly metrics level and retention days for the blob service in your default storage account:</span></span>

```powershell
Get-AzureStorageServiceMetricsProperty -MetricsType Hour -ServiceType Blob
```

<span data-ttu-id="28a81-128">Pour plus d’informations sur la configuration des applets de commande Azure PowerShell avec votre abonnement Azure et sur la sélection du compte de stockage par défaut à utiliser, voir [Installation et configuration d’Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="28a81-128">For information about how to configure the Azure PowerShell cmdlets to work with your Azure subscription and how to select the default storage account to use, see: [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="how-to-enable-storage-metrics-programmatically"></a><span data-ttu-id="28a81-129">Comment activer Storage Metrics par programmation</span><span class="sxs-lookup"><span data-stu-id="28a81-129">How to enable Storage metrics programmatically</span></span>
<span data-ttu-id="28a81-130">L’extrait de code C# suivant montre comment activer les métriques et la journalisation pour le service BLOB à l’aide de la bibliothèque cliente de stockage pour .NET :</span><span class="sxs-lookup"><span data-stu-id="28a81-130">The following C# snippet shows how to enable metrics and logging for the Blob service using the storage client library for .NET:</span></span>

```csharp
//Parse the connection string for the storage account.
const string ConnectionString = "DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key";
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);

// Create service client for credentialed access to the Blob service.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Enable Storage Analytics logging and set retention policy to 10 days.
ServiceProperties properties = new ServiceProperties();
properties.Logging.LoggingOperations = LoggingOperations.All;
properties.Logging.RetentionDays = 10;
properties.Logging.Version = "1.0";

// Configure service properties for metrics. Both metrics and logging must be set at the same time.
properties.HourMetrics.MetricsLevel = MetricsLevel.ServiceAndApi;
properties.HourMetrics.RetentionDays = 10;
properties.HourMetrics.Version = "1.0";

properties.MinuteMetrics.MetricsLevel = MetricsLevel.ServiceAndApi;
properties.MinuteMetrics.RetentionDays = 10;
properties.MinuteMetrics.Version = "1.0";

// Set the default service version to be used for anonymous requests.
properties.DefaultServiceVersion = "2015-04-05";

// Set the service properties.
blobClient.SetServiceProperties(properties);
```

## <a name="viewing-storage-metrics"></a><span data-ttu-id="28a81-131">Affichage des métriques de stockage</span><span class="sxs-lookup"><span data-stu-id="28a81-131">Viewing Storage metrics</span></span>
<span data-ttu-id="28a81-132">Après que vous avez configuré les métriques d’analyse du stockage pour surveiller votre compte de stockage, l’analyse du stockage enregistre les métriques dans des tables connues dans votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="28a81-132">After you configure Storage Analytics metrics to monitor your storage account, Storage Analytics records the metrics in a set of well-known tables in your storage account.</span></span> <span data-ttu-id="28a81-133">Vous pouvez configurer des graphiques permettant de consulter des mesures horaires dans le [Portail Azure](https://portal.azure.com) :</span><span class="sxs-lookup"><span data-stu-id="28a81-133">You can configure charts to view hourly metrics in the [Azure portal](https://portal.azure.com):</span></span>

1. <span data-ttu-id="28a81-134">Accédez à votre compte de stockage dans le [Portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="28a81-134">Navigate to your storage account in the [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="28a81-135">Sélectionnez **Mesures** dans le panneau **Menu** du service dont vous souhaitez afficher les mesures.</span><span class="sxs-lookup"><span data-stu-id="28a81-135">Select **Metrics** in the **Menu** blade for the service whose metrics you want to view.</span></span>
1. <span data-ttu-id="28a81-136">Sélectionnez **Modifier** sur le graphique que vous souhaitez configurer.</span><span class="sxs-lookup"><span data-stu-id="28a81-136">Select **Edit** on the chart you want to configure.</span></span>
1. <span data-ttu-id="28a81-137">Dans le panneau **Modifier le graphique**, sélectionnez **l’Intervalle de temps**, le **Type de graphique** et les mesures que vous souhaitez afficher dans le graphique.</span><span class="sxs-lookup"><span data-stu-id="28a81-137">In the **Edit Chart** blade, select the **Time Range**, **Chart type**, and the metrics you want displayed in the chart.</span></span>
1. <span data-ttu-id="28a81-138">Sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="28a81-138">Select **OK**</span></span>

<span data-ttu-id="28a81-139">Si vous souhaitez télécharger les métriques pour un stockage à long terme ou pour les analyser localement, vous devez :</span><span class="sxs-lookup"><span data-stu-id="28a81-139">If you want to download the metrics for long-term storage or to analyze them locally, you will need to:</span></span>

* <span data-ttu-id="28a81-140">Utiliser un outil qui prend en charge ces tables et vous permet de les afficher et de les télécharger</span><span class="sxs-lookup"><span data-stu-id="28a81-140">Use a tool that is aware of these tables and will allow you to view and download them.</span></span>
* <span data-ttu-id="28a81-141">Écrire une application ou un script personnalisé pour lire et stocker les tables</span><span class="sxs-lookup"><span data-stu-id="28a81-141">Write a custom application or script to read and store the tables.</span></span>

<span data-ttu-id="28a81-142">De nombreux outils de consultation du stockage tiers prennent en charge ces tables et vous permettent de les afficher directement.</span><span class="sxs-lookup"><span data-stu-id="28a81-142">Many third-party storage-browsing tools are aware of these tables and enable you to view them directly.</span></span>
<span data-ttu-id="28a81-143">Pour obtenir la liste des outils disponibles, consultez [Outils clients Azure Storage](storage-explorers.md) .</span><span class="sxs-lookup"><span data-stu-id="28a81-143">Please see [Azure Storage Client Tools](storage-explorers.md) for a list of available tools.</span></span>

> [!NOTE]
> <span data-ttu-id="28a81-144">À compter de la version 0.8.0 de [Microsoft Azure Storage Explorer](http://storageexplorer.com/), vous pourrez désormais afficher et télécharger les tables de métriques Analytics.</span><span class="sxs-lookup"><span data-stu-id="28a81-144">Starting with version 0.8.0 of the [Microsoft Azure Storage Explorer](http://storageexplorer.com/), you can view and download the analytics metrics tables.</span></span>
> 
> 

<span data-ttu-id="28a81-145">Pour accéder par programmation aux tables Analytics, notez qu’elles n’apparaissent pas si vous répertoriez toutes les tables dans votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="28a81-145">In order to access the analytics tables programmatically, do note that the analytics tables do not appear if you list all the tables in your storage account.</span></span> <span data-ttu-id="28a81-146">Vous pouvez y accéder directement par nom ou utiliser l [’API CloudAnalyticsClient](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.analytics.cloudanalyticsclient.aspx) dans la bibliothèque cliente .NET pour interroger les noms de tables.</span><span class="sxs-lookup"><span data-stu-id="28a81-146">You can either access them directly by name, or use the [CloudAnalyticsClient API](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.analytics.cloudanalyticsclient.aspx) in the .NET client library to query the table names.</span></span>

### <a name="hourly-metrics"></a><span data-ttu-id="28a81-147">Métriques toutes les heures</span><span class="sxs-lookup"><span data-stu-id="28a81-147">Hourly metrics</span></span>
* <span data-ttu-id="28a81-148">$MetricsHourPrimaryTransactionsBlob</span><span class="sxs-lookup"><span data-stu-id="28a81-148">$MetricsHourPrimaryTransactionsBlob</span></span>
* <span data-ttu-id="28a81-149">$MetricsHourPrimaryTransactionsTable</span><span class="sxs-lookup"><span data-stu-id="28a81-149">$MetricsHourPrimaryTransactionsTable</span></span>
* <span data-ttu-id="28a81-150">$MetricsHourPrimaryTransactionsQueue</span><span class="sxs-lookup"><span data-stu-id="28a81-150">$MetricsHourPrimaryTransactionsQueue</span></span>

### <a name="minute-metrics"></a><span data-ttu-id="28a81-151">Métriques par minute</span><span class="sxs-lookup"><span data-stu-id="28a81-151">Minute metrics</span></span>
* <span data-ttu-id="28a81-152">$MetricsMinutePrimaryTransactionsBlob</span><span class="sxs-lookup"><span data-stu-id="28a81-152">$MetricsMinutePrimaryTransactionsBlob</span></span>
* <span data-ttu-id="28a81-153">$MetricsMinutePrimaryTransactionsTable</span><span class="sxs-lookup"><span data-stu-id="28a81-153">$MetricsMinutePrimaryTransactionsTable</span></span>
* <span data-ttu-id="28a81-154">$MetricsMinutePrimaryTransactionsQueue</span><span class="sxs-lookup"><span data-stu-id="28a81-154">$MetricsMinutePrimaryTransactionsQueue</span></span>

### <a name="capacity"></a><span data-ttu-id="28a81-155">Capacité</span><span class="sxs-lookup"><span data-stu-id="28a81-155">Capacity</span></span>
* <span data-ttu-id="28a81-156">$MetricsCapacityBlob</span><span class="sxs-lookup"><span data-stu-id="28a81-156">$MetricsCapacityBlob</span></span>

<span data-ttu-id="28a81-157">Vous trouverez des informations complètes sur les schémas de ces tables dans [Schéma de table de métriques Storage Analytics](https://msdn.microsoft.com/library/azure/hh343264.aspx).</span><span class="sxs-lookup"><span data-stu-id="28a81-157">You can find full details of the schemas for these tables at [Storage Analytics Metrics Table Schema](https://msdn.microsoft.com/library/azure/hh343264.aspx).</span></span> <span data-ttu-id="28a81-158">Les exemples de lignes ci-dessous montrent uniquement un sous-ensemble des colonnes disponibles, mais ils illustrent les différentes façons dont Storage Metrics enregistre ces métriques :</span><span class="sxs-lookup"><span data-stu-id="28a81-158">The sample rows below show only a subset of the columns available, but illustrate some important features of the way Storage Metrics saves these metrics:</span></span>

| <span data-ttu-id="28a81-159">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="28a81-159">PartitionKey</span></span> | <span data-ttu-id="28a81-160">RowKey</span><span class="sxs-lookup"><span data-stu-id="28a81-160">RowKey</span></span> | <span data-ttu-id="28a81-161">Timestamp</span><span class="sxs-lookup"><span data-stu-id="28a81-161">Timestamp</span></span> | <span data-ttu-id="28a81-162">TotalRequests</span><span class="sxs-lookup"><span data-stu-id="28a81-162">TotalRequests</span></span> | <span data-ttu-id="28a81-163">TotalBillableRequests</span><span class="sxs-lookup"><span data-stu-id="28a81-163">TotalBillableRequests</span></span> | <span data-ttu-id="28a81-164">TotalIngress</span><span class="sxs-lookup"><span data-stu-id="28a81-164">TotalIngress</span></span> | <span data-ttu-id="28a81-165">TotalEgress</span><span class="sxs-lookup"><span data-stu-id="28a81-165">TotalEgress</span></span> | <span data-ttu-id="28a81-166">Availability</span><span class="sxs-lookup"><span data-stu-id="28a81-166">Availability</span></span> | <span data-ttu-id="28a81-167">AverageE2ELatency</span><span class="sxs-lookup"><span data-stu-id="28a81-167">AverageE2ELatency</span></span> | <span data-ttu-id="28a81-168">AverageServerLatency</span><span class="sxs-lookup"><span data-stu-id="28a81-168">AverageServerLatency</span></span> | <span data-ttu-id="28a81-169">PercentSuccess</span><span class="sxs-lookup"><span data-stu-id="28a81-169">PercentSuccess</span></span> |
| --- |:---:| ---:| --- | --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="28a81-170">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="28a81-170">20140522T1100</span></span> |<span data-ttu-id="28a81-171">user;All</span><span class="sxs-lookup"><span data-stu-id="28a81-171">user;All</span></span> |<span data-ttu-id="28a81-172">2014-05-22T11:01:16.7650250Z</span><span class="sxs-lookup"><span data-stu-id="28a81-172">2014-05-22T11:01:16.7650250Z</span></span> |<span data-ttu-id="28a81-173">7</span><span class="sxs-lookup"><span data-stu-id="28a81-173">7</span></span> |<span data-ttu-id="28a81-174">7</span><span class="sxs-lookup"><span data-stu-id="28a81-174">7</span></span> |<span data-ttu-id="28a81-175">4003</span><span class="sxs-lookup"><span data-stu-id="28a81-175">4003</span></span> |<span data-ttu-id="28a81-176">46801</span><span class="sxs-lookup"><span data-stu-id="28a81-176">46801</span></span> |<span data-ttu-id="28a81-177">100</span><span class="sxs-lookup"><span data-stu-id="28a81-177">100</span></span> |<span data-ttu-id="28a81-178">104.4286</span><span class="sxs-lookup"><span data-stu-id="28a81-178">104.4286</span></span> |<span data-ttu-id="28a81-179">6.857143</span><span class="sxs-lookup"><span data-stu-id="28a81-179">6.857143</span></span> |<span data-ttu-id="28a81-180">100</span><span class="sxs-lookup"><span data-stu-id="28a81-180">100</span></span> |
| <span data-ttu-id="28a81-181">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="28a81-181">20140522T1100</span></span> |<span data-ttu-id="28a81-182">user;QueryEntities</span><span class="sxs-lookup"><span data-stu-id="28a81-182">user;QueryEntities</span></span> |<span data-ttu-id="28a81-183">2014-05-22T11:01:16.7640250Z</span><span class="sxs-lookup"><span data-stu-id="28a81-183">2014-05-22T11:01:16.7640250Z</span></span> |<span data-ttu-id="28a81-184">5</span><span class="sxs-lookup"><span data-stu-id="28a81-184">5</span></span> |<span data-ttu-id="28a81-185">5</span><span class="sxs-lookup"><span data-stu-id="28a81-185">5</span></span> |<span data-ttu-id="28a81-186">2694</span><span class="sxs-lookup"><span data-stu-id="28a81-186">2694</span></span> |<span data-ttu-id="28a81-187">45951</span><span class="sxs-lookup"><span data-stu-id="28a81-187">45951</span></span> |<span data-ttu-id="28a81-188">100</span><span class="sxs-lookup"><span data-stu-id="28a81-188">100</span></span> |<span data-ttu-id="28a81-189">143.8</span><span class="sxs-lookup"><span data-stu-id="28a81-189">143.8</span></span> |<span data-ttu-id="28a81-190">7.8</span><span class="sxs-lookup"><span data-stu-id="28a81-190">7.8</span></span> |<span data-ttu-id="28a81-191">100</span><span class="sxs-lookup"><span data-stu-id="28a81-191">100</span></span> |
| <span data-ttu-id="28a81-192">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="28a81-192">20140522T1100</span></span> |<span data-ttu-id="28a81-193">user;QueryEntity</span><span class="sxs-lookup"><span data-stu-id="28a81-193">user;QueryEntity</span></span> |<span data-ttu-id="28a81-194">2014-05-22T11:01:16.7650250Z</span><span class="sxs-lookup"><span data-stu-id="28a81-194">2014-05-22T11:01:16.7650250Z</span></span> |<span data-ttu-id="28a81-195">1</span><span class="sxs-lookup"><span data-stu-id="28a81-195">1</span></span> |<span data-ttu-id="28a81-196">1</span><span class="sxs-lookup"><span data-stu-id="28a81-196">1</span></span> |<span data-ttu-id="28a81-197">538</span><span class="sxs-lookup"><span data-stu-id="28a81-197">538</span></span> |<span data-ttu-id="28a81-198">633</span><span class="sxs-lookup"><span data-stu-id="28a81-198">633</span></span> |<span data-ttu-id="28a81-199">100</span><span class="sxs-lookup"><span data-stu-id="28a81-199">100</span></span> |<span data-ttu-id="28a81-200">3</span><span class="sxs-lookup"><span data-stu-id="28a81-200">3</span></span> |<span data-ttu-id="28a81-201">3</span><span class="sxs-lookup"><span data-stu-id="28a81-201">3</span></span> |<span data-ttu-id="28a81-202">100</span><span class="sxs-lookup"><span data-stu-id="28a81-202">100</span></span> |
| <span data-ttu-id="28a81-203">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="28a81-203">20140522T1100</span></span> |<span data-ttu-id="28a81-204">user;UpdateEntity</span><span class="sxs-lookup"><span data-stu-id="28a81-204">user;UpdateEntity</span></span> |<span data-ttu-id="28a81-205">2014-05-22T11:01:16.7650250Z</span><span class="sxs-lookup"><span data-stu-id="28a81-205">2014-05-22T11:01:16.7650250Z</span></span> |<span data-ttu-id="28a81-206">1</span><span class="sxs-lookup"><span data-stu-id="28a81-206">1</span></span> |<span data-ttu-id="28a81-207">1</span><span class="sxs-lookup"><span data-stu-id="28a81-207">1</span></span> |<span data-ttu-id="28a81-208">771</span><span class="sxs-lookup"><span data-stu-id="28a81-208">771</span></span> |<span data-ttu-id="28a81-209">217</span><span class="sxs-lookup"><span data-stu-id="28a81-209">217</span></span> |<span data-ttu-id="28a81-210">100</span><span class="sxs-lookup"><span data-stu-id="28a81-210">100</span></span> |<span data-ttu-id="28a81-211">9</span><span class="sxs-lookup"><span data-stu-id="28a81-211">9</span></span> |<span data-ttu-id="28a81-212">6</span><span class="sxs-lookup"><span data-stu-id="28a81-212">6</span></span> |<span data-ttu-id="28a81-213">100</span><span class="sxs-lookup"><span data-stu-id="28a81-213">100</span></span> |

<span data-ttu-id="28a81-214">Dans cet exemple de données de métriques par minute, la clé de partition (PartitionKey) utilise une résolution d’une minute.</span><span class="sxs-lookup"><span data-stu-id="28a81-214">In this example minute metrics data, the partition key uses the time at minute resolution.</span></span> <span data-ttu-id="28a81-215">La clé de ligne (RowKey) identifie le type d’informations qui sont stockées dans la ligne. Elle se compose de deux éléments : le type d’accès et le type de demande.</span><span class="sxs-lookup"><span data-stu-id="28a81-215">The row key identifies the type of information that is stored in the row and this is composed of two pieces of information, the access type, and the request type:</span></span>

* <span data-ttu-id="28a81-216">Le type d’accès a la valeur user ou system, user correspondant à toutes les demandes de l’utilisateur au service de stockage et system correspondant à toutes les demandes formulées par Storage Analytics.</span><span class="sxs-lookup"><span data-stu-id="28a81-216">The access type is either user or system, where user refers to all user requests to the storage service, and system refers to requests made by Storage Analytics.</span></span>
* <span data-ttu-id="28a81-217">Le type de demande peut avoir la valeur all, auquel cas il s’agit d’une ligne de résumé, ou il identifie l’API spécifique comme QueryEntity ou UpdateEntity.</span><span class="sxs-lookup"><span data-stu-id="28a81-217">The request type is either all in which case it is a summary line, or it identifies the specific API such as QueryEntity or UpdateEntity.</span></span>

<span data-ttu-id="28a81-218">Les exemples de données ci-dessus montrent tous les enregistrements pour une seule minute (à partir de 11h00). Ainsi, la somme des demandes QueryEntities, QueryEntity et UpdateEntity est égale à sept, ce qui correspond bien au total indiqué sur la ligne user:All.</span><span class="sxs-lookup"><span data-stu-id="28a81-218">The sample data above shows all the records for a single minute (starting at 11:00AM), so the number of QueryEntities requests plus the number of QueryEntity requests plus the number of UpdateEntity requests add up to seven, which is the total shown on the user:All row.</span></span> <span data-ttu-id="28a81-219">De même, vous pouvez déduire la latence de bout en bout moyenne (104,4286) sur la ligne user:All en effectuant le calcul suivant : ((143,8 * 5) + 3 + 9)/7.</span><span class="sxs-lookup"><span data-stu-id="28a81-219">Similarly, you can derive the average end-to-end latency 104.4286 on the user:All row by calculating ((143.8 * 5) + 3 + 9)/7.</span></span>

## <a name="metrics-alerts"></a><span data-ttu-id="28a81-220">Alertes liées aux métriques</span><span class="sxs-lookup"><span data-stu-id="28a81-220">Metrics alerts</span></span>
<span data-ttu-id="28a81-221">Il peut être intéressant de définir des alertes dans le [Portail Azure](https://portal.azure.com), afin que Storage Metrics puisse vous avertir automatiquement de tout changement important de comportement de vos services de stockage.</span><span class="sxs-lookup"><span data-stu-id="28a81-221">You should consider setting up alerts in the [Azure portal](https://portal.azure.com) so Storage Metrics can automatically notify you of important changes in the behavior of your storage services.</span></span> <span data-ttu-id="28a81-222">Si vous utilisez un outil Explorateur de stockage pour télécharger ces données dans un format délimité, vous pouvez utiliser Microsoft Excel pour les analyser.</span><span class="sxs-lookup"><span data-stu-id="28a81-222">If you use a storage explorer tool to download this metrics data in a delimited format, you can use Microsoft Excel to analyze the data.</span></span> <span data-ttu-id="28a81-223">Pour obtenir la liste des outils d’exploration du stockage disponibles, consultez [Outils clients Azure Storage](storage-explorers.md) .</span><span class="sxs-lookup"><span data-stu-id="28a81-223">See [Azure Storage Client Tools](storage-explorers.md) for a list of available storage explorer tools.</span></span> <span data-ttu-id="28a81-224">Vous pouvez configurer des alertes dans le panneau **Règles d’alerte**, accessible sous **Surveillance** dans le panneau du menu Compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="28a81-224">You can configure alerts in the **Alert rules** blade, accessible under **Monitoring** in the Storage account menu blade.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="28a81-225">Il peut y avoir un décalage entre un événement de stockage et l’enregistrement des données métriques par heure ou par minute correspondantes.</span><span class="sxs-lookup"><span data-stu-id="28a81-225">There may be a delay between a storage event and when the corresponding hourly or minute metrics data is recorded.</span></span> <span data-ttu-id="28a81-226">Dans le cas des métriques par minute, plusieurs minutes de données peuvent être écrites à la fois.</span><span class="sxs-lookup"><span data-stu-id="28a81-226">In the case of minute metrics, several minutes of data may be written at once.</span></span> <span data-ttu-id="28a81-227">Cela peut entraîner des transactions l’agrégation de minutes précédentes dans la transaction pour la minute actuelle.</span><span class="sxs-lookup"><span data-stu-id="28a81-227">This can lead to transactions from earlier minutes being aggregated into the transaction for the current minute.</span></span> <span data-ttu-id="28a81-228">Dans ce cas, le service d’alerte peut ne pas disposer de toutes les données de métriques disponibles pour l’intervalle d’alerte configuré, ce qui peut conduire à des déclenchements d’alerte inattendus.</span><span class="sxs-lookup"><span data-stu-id="28a81-228">When this happens, the alert service may not have all available metrics data for the configured alert interval, which may lead to alerts firing unexpectedly.</span></span>
>

## <a name="accessing-metrics-data-programmatically"></a><span data-ttu-id="28a81-229">Accès aux données de métriques par programmation</span><span class="sxs-lookup"><span data-stu-id="28a81-229">Accessing metrics data programmatically</span></span>
<span data-ttu-id="28a81-230">L’exemple de code suivant en C# accède aux métriques par minute pour une plage de minutes et affiche les résultats dans une fenêtre de console.</span><span class="sxs-lookup"><span data-stu-id="28a81-230">The following listing shows sample C# code that accesses the minute metrics for a range of minutes and displays the results in a console Window.</span></span> <span data-ttu-id="28a81-231">Il utilise la version 4 de la bibliothèque de stockage Azure. Celle-ci comprend la classe CloudAnalyticsClient, qui simplifie l’accès aux tables de métriques de stockage.</span><span class="sxs-lookup"><span data-stu-id="28a81-231">It uses the Azure Storage Library version 4 that includes the CloudAnalyticsClient class that simplifies accessing the metrics tables in storage.</span></span>

```csharp
private static void PrintMinuteMetrics(CloudAnalyticsClient analyticsClient, DateTimeOffset startDateTime, DateTimeOffset endDateTime)
{
    // Convert the dates to the format used in the PartitionKey
    var start = startDateTime.ToUniversalTime().ToString("yyyyMMdd'T'HHmm");
    var end = endDateTime.ToUniversalTime().ToString("yyyyMMdd'T'HHmm");

    var services = Enum.GetValues(typeof(StorageService));
    foreach (StorageService service in services)
    {
        Console.WriteLine("Minute Metrics for Service {0} from {1} to {2} UTC", service, start, end);
        var metricsQuery = analyticsClient.CreateMinuteMetricsQuery(service, StorageLocation.Primary);
        var t = analyticsClient.GetMinuteMetricsTable(service);
        var opContext = new OperationContext();
        var query =
          from entity in metricsQuery
          // Note, you can't filter using the entity properties Time, AccessType, or TransactionType
          // because they are calculated fields in the MetricsEntity class.
          // The PartitionKey identifies the DataTime of the metrics.
          where entity.PartitionKey.CompareTo(start) >= 0 && entity.PartitionKey.CompareTo(end) <= 0
        select entity;

        // Filter on "user" transactions after fetching the metrics from Table Storage.
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

## <a name="what-charges-do-you-incur-when-you-enable-storage-metrics"></a><span data-ttu-id="28a81-232">Quels sont les frais encourus quand vous activez les métriques de stockage ?</span><span class="sxs-lookup"><span data-stu-id="28a81-232">What charges do you incur when you enable storage metrics?</span></span>
<span data-ttu-id="28a81-233">Les demandes d’écriture pour créer des entités de table pour les métriques sont facturées au tarif standard applicable à toutes les opérations Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="28a81-233">Write requests to create table entities for metrics are charged at the standard rates applicable to all Azure Storage operations.</span></span>

<span data-ttu-id="28a81-234">Les demandes de lecture et de suppression formulées par un client sur des données de métriques sont aussi facturées au tarif standard.</span><span class="sxs-lookup"><span data-stu-id="28a81-234">Read and delete requests by a client to metrics data are also billable at standard rates.</span></span> <span data-ttu-id="28a81-235">Si vous avez configuré une stratégie de rétention des données, vous n’êtes pas facturé quand Azure Storage supprime les anciennes données de métriques.</span><span class="sxs-lookup"><span data-stu-id="28a81-235">If you have configured a data retention policy, you are not charged when Azure Storage deletes old metrics data.</span></span> <span data-ttu-id="28a81-236">Toutefois, si vous supprimez des données de métriques, les opérations de suppression sont facturées à votre compte.</span><span class="sxs-lookup"><span data-stu-id="28a81-236">However, if you delete analytics data, your account is charged for the delete operations.</span></span>

<span data-ttu-id="28a81-237">La capacité utilisée par les tables de métriques est également facturée ; vous pouvez utiliser les informations suivantes pour estimer la capacité utilisée pour stocker les données de métriques :</span><span class="sxs-lookup"><span data-stu-id="28a81-237">The capacity used by the metrics tables is also billable: you can use the following to estimate the amount of capacity used for storing metrics data:</span></span>

* <span data-ttu-id="28a81-238">En une heure, pour un service qui utilise toutes les API de chaque service, environ 148 Ko de données sont stockés par heure dans les tables de transaction de métriques si vous avez activé la synthèse au niveau des services et des API.</span><span class="sxs-lookup"><span data-stu-id="28a81-238">If each hour a service utilizes every API in every service, then approximately 148KB of data is stored every hour in the metrics transaction tables if you have enabled both service and API level summary.</span></span>
* <span data-ttu-id="28a81-239">En une heure, pour un service qui utilise toutes les API de chaque service, environ 12 Ko de données sont stockés par heure dans les tables de transaction de métriques si vous avez uniquement activé la synthèse au niveau des services.</span><span class="sxs-lookup"><span data-stu-id="28a81-239">If each hour a service utilizes every API in every service, then approximately 12KB of data is stored every hour in the metrics transaction tables if you have enabled just service level summary.</span></span>
* <span data-ttu-id="28a81-240">Deux lignes supplémentaires sont ajoutées chaque jour à la table de capacité pour les objets blob (si l’utilisateur a activé les journaux). Cela signifie que la table augmente d’environ 300 octets au maximum par jour.</span><span class="sxs-lookup"><span data-stu-id="28a81-240">The capacity table for blobs has two rows added each day (provided user has opted in for logs): this implies that every day the size of this table increases by up to approximately 300 bytes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="28a81-241">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="28a81-241">Next steps</span></span>
[<span data-ttu-id="28a81-242">Activation de la journalisation du stockage et accès aux données des journaux</span><span class="sxs-lookup"><span data-stu-id="28a81-242">Enabling Storage Logging and Accessing Log Data</span></span>](/rest/api/storageservices/Enabling-Storage-Logging-and-Accessing-Log-Data)
