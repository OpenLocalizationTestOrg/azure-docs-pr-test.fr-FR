---
title: "Stocker et afficher des données de diagnostic dans Azure Storage | Microsoft Docs"
description: "Obtenir des données de diagnostics Microsoft Azure dans Azure Storage et les afficher"
services: cloud-services
documentationcenter: .net
author: rboucher
manager: jwhit
editor: tysonn
ms.assetid: 18e0780d-43e7-41e4-b8e9-f1fb9a36eb03
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2016
ms.author: robb
ms.openlocfilehash: 374cc179e13c00e439415e3df16e0c6d5ccba5e3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="store-and-view-diagnostic-data-in-azure-storage"></a><span data-ttu-id="59c42-103">Stocker et afficher des données de diagnostic dans Azure Storage</span><span class="sxs-lookup"><span data-stu-id="59c42-103">Store and view diagnostic data in Azure Storage</span></span>
<span data-ttu-id="59c42-104">Les données de diagnostic ne sont pas définitivement stockées, sauf si vous les transférez vers l’émulateur de stockage Microsoft Azure ou dans le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="59c42-104">Diagnostic data is not permanently stored unless you transfer it to the Microsoft Azure storage emulator or to Azure storage.</span></span> <span data-ttu-id="59c42-105">Une fois dans le stockage, elles peuvent être affichées avec un des outils disponibles.</span><span class="sxs-lookup"><span data-stu-id="59c42-105">Once in storage, it can be viewed with one of several available tools.</span></span>

## <a name="specify-a-storage-account"></a><span data-ttu-id="59c42-106">Spécifiez un compte de stockage</span><span class="sxs-lookup"><span data-stu-id="59c42-106">Specify a storage account</span></span>
<span data-ttu-id="59c42-107">Spécifiez le compte de stockage que vous souhaitez utiliser dans le fichier ServiceConfiguration.cscfg.</span><span class="sxs-lookup"><span data-stu-id="59c42-107">You specify the storage account that you want to use in the ServiceConfiguration.cscfg file.</span></span> <span data-ttu-id="59c42-108">Les informations de compte sont définies en tant que chaîne de connexion dans un paramètre de configuration.</span><span class="sxs-lookup"><span data-stu-id="59c42-108">The account information is defined as a connection string in a configuration setting.</span></span> <span data-ttu-id="59c42-109">L’exemple suivant montre la chaîne de connexion par défaut créée pour un nouveau projet de service cloud dans Visual Studio :</span><span class="sxs-lookup"><span data-stu-id="59c42-109">The following example shows the default connection string created for a new Cloud Service project in  Visual Studio:</span></span>

```
    <ConfigurationSettings>
       <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="UseDevelopmentStorage=true" />
    </ConfigurationSettings>
```

<span data-ttu-id="59c42-110">Vous pouvez modifier cette chaîne de connexion pour fournir des informations de compte pour un compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="59c42-110">You can change this connection string to provide account information for an Azure storage account.</span></span>

<span data-ttu-id="59c42-111">Selon le type de données de diagnostic recueillies, Diagnostics Microsoft Azure utilise le service Blob ou le service de Table.</span><span class="sxs-lookup"><span data-stu-id="59c42-111">Depending on the type of diagnostic data that is being collected, Azure Diagnostics uses either the Blob service or the Table service.</span></span> <span data-ttu-id="59c42-112">Le tableau qui suit présente les sources de données permanentes et leur format.</span><span class="sxs-lookup"><span data-stu-id="59c42-112">The following table shows the data sources that are persisted and their format.</span></span>

| <span data-ttu-id="59c42-113">Source de données</span><span class="sxs-lookup"><span data-stu-id="59c42-113">Data source</span></span> | <span data-ttu-id="59c42-114">Format de stockage</span><span class="sxs-lookup"><span data-stu-id="59c42-114">Storage format</span></span> |
| --- | --- |
| <span data-ttu-id="59c42-115">Journaux Azure</span><span class="sxs-lookup"><span data-stu-id="59c42-115">Azure logs</span></span> |<span data-ttu-id="59c42-116">Table</span><span class="sxs-lookup"><span data-stu-id="59c42-116">Table</span></span> |
| <span data-ttu-id="59c42-117">Journaux IIS 7.0</span><span class="sxs-lookup"><span data-stu-id="59c42-117">IIS 7.0 logs</span></span> |<span data-ttu-id="59c42-118">Blob</span><span class="sxs-lookup"><span data-stu-id="59c42-118">Blob</span></span> |
| <span data-ttu-id="59c42-119">Journaux d’infrastructure de diagnostics Azure</span><span class="sxs-lookup"><span data-stu-id="59c42-119">Azure Diagnostics infrastructure logs</span></span> |<span data-ttu-id="59c42-120">Table</span><span class="sxs-lookup"><span data-stu-id="59c42-120">Table</span></span> |
| <span data-ttu-id="59c42-121">Journaux de suivi de requête ayant échoué</span><span class="sxs-lookup"><span data-stu-id="59c42-121">Failed Request Trace logs</span></span> |<span data-ttu-id="59c42-122">Blob</span><span class="sxs-lookup"><span data-stu-id="59c42-122">Blob</span></span> |
| <span data-ttu-id="59c42-123">Journaux d'événements Windows</span><span class="sxs-lookup"><span data-stu-id="59c42-123">Windows Event logs</span></span> |<span data-ttu-id="59c42-124">Table</span><span class="sxs-lookup"><span data-stu-id="59c42-124">Table</span></span> |
| <span data-ttu-id="59c42-125">Compteurs de performances</span><span class="sxs-lookup"><span data-stu-id="59c42-125">Performance counters</span></span> |<span data-ttu-id="59c42-126">Table</span><span class="sxs-lookup"><span data-stu-id="59c42-126">Table</span></span> |
| <span data-ttu-id="59c42-127">Vidages sur incident</span><span class="sxs-lookup"><span data-stu-id="59c42-127">Crash dumps</span></span> |<span data-ttu-id="59c42-128">Blob</span><span class="sxs-lookup"><span data-stu-id="59c42-128">Blob</span></span> |
| <span data-ttu-id="59c42-129">Journaux d'erreurs personnalisés</span><span class="sxs-lookup"><span data-stu-id="59c42-129">Custom error logs</span></span> |<span data-ttu-id="59c42-130">Blob</span><span class="sxs-lookup"><span data-stu-id="59c42-130">Blob</span></span> |

## <a name="transfer-diagnostic-data"></a><span data-ttu-id="59c42-131">Transférer les données de diagnostic</span><span class="sxs-lookup"><span data-stu-id="59c42-131">Transfer diagnostic data</span></span>
<span data-ttu-id="59c42-132">Pour le kit de développement logiciel 2.5 et versions ultérieures, la demande de transfert de données de diagnostic peut se produire dans le fichier de configuration.</span><span class="sxs-lookup"><span data-stu-id="59c42-132">For SDK 2.5 and later, the request to transfer diagnostic data can occur through the configuration file.</span></span> <span data-ttu-id="59c42-133">Vous pouvez transférer les données de diagnostic à des intervalles programmés, comme indiqué dans la configuration.</span><span class="sxs-lookup"><span data-stu-id="59c42-133">You can transfer diagnostic data at scheduled intervals as specified in the configuration.</span></span>

<span data-ttu-id="59c42-134">Pour le kit de développement logiciel 2.4 et versions antérieures, vous pouvez demander le transfert de données de diagnostic via le fichier de configuration et par programmation.</span><span class="sxs-lookup"><span data-stu-id="59c42-134">For SDK 2.4 and previous you can request to transfer the diagnostic data through the configuration file as well as programmatically.</span></span> <span data-ttu-id="59c42-135">L’approche par programmation vous permet également d’effectuer des transferts à la demande.</span><span class="sxs-lookup"><span data-stu-id="59c42-135">The programmatic approach also allows you to do on-demand transfers.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="59c42-136">Lorsque vous transférez des données de diagnostic vers un compte de stockage Microsoft Azure, vous encourez des frais pour les ressources de stockage qui utilise vos données de diagnostic.</span><span class="sxs-lookup"><span data-stu-id="59c42-136">When you transfer diagnostic data to an Azure storage account, you incur costs for the storage resources that your diagnostic data uses.</span></span>
> 
> 

## <a name="store-diagnostic-data"></a><span data-ttu-id="59c42-137">Stockez les données de diagnostic</span><span class="sxs-lookup"><span data-stu-id="59c42-137">Store diagnostic data</span></span>
<span data-ttu-id="59c42-138">Les données du journal sont stockées dans le stockage Blob ou de Table avec les noms suivants :</span><span class="sxs-lookup"><span data-stu-id="59c42-138">Log data is stored in either Blob or Table storage with the following names:</span></span>

<span data-ttu-id="59c42-139">**Tables**</span><span class="sxs-lookup"><span data-stu-id="59c42-139">**Tables**</span></span>

* <span data-ttu-id="59c42-140">**WadLogsTable** : journaux rédigés dans le code à l’aide de l’écouteur de suivi.</span><span class="sxs-lookup"><span data-stu-id="59c42-140">**WadLogsTable** - Logs written in code using the trace listener.</span></span>
* <span data-ttu-id="59c42-141">**WADDiagnosticInfrastructureLogsTable** : modifications de configuration et d’analyse de diagnostic.</span><span class="sxs-lookup"><span data-stu-id="59c42-141">**WADDiagnosticInfrastructureLogsTable** - Diagnostic monitor and configuration changes.</span></span>
* <span data-ttu-id="59c42-142">**WADDirectoriesTable** : répertoires que le moniteur de diagnostic surveille.</span><span class="sxs-lookup"><span data-stu-id="59c42-142">**WADDirectoriesTable** – Directories that the diagnostic monitor is monitoring.</span></span>  <span data-ttu-id="59c42-143">Cela inclut les journaux IIS, les journaux de requêtes ayant échoué et les répertoires personnalisés IIS.</span><span class="sxs-lookup"><span data-stu-id="59c42-143">This includes IIS logs, IIS failed request logs, and custom directories.</span></span>  <span data-ttu-id="59c42-144">L’emplacement du fichier journal blob est spécifié dans le champ de conteneur et le nom de l’objet blob se trouve dans le champ RelativePath.</span><span class="sxs-lookup"><span data-stu-id="59c42-144">The location of the blob log file is specified in the Container field and the name of the blob is in the RelativePath field.</span></span>  <span data-ttu-id="59c42-145">Le champ AbsolutePath indique l’emplacement et le nom du fichier tel qu’il existait sur la machine virtuelle Azure.</span><span class="sxs-lookup"><span data-stu-id="59c42-145">The AbsolutePath field indicates the location and name of the file as it existed on the Azure virtual machine.</span></span>
* <span data-ttu-id="59c42-146">**WADPerformanceCountersTable** : les compteurs de performance.</span><span class="sxs-lookup"><span data-stu-id="59c42-146">**WADPerformanceCountersTable** – Performance counters.</span></span>
* <span data-ttu-id="59c42-147">**WADWindowsEventLogsTable** : journaux des événements Windows.</span><span class="sxs-lookup"><span data-stu-id="59c42-147">**WADWindowsEventLogsTable** – Windows Event logs.</span></span>

<span data-ttu-id="59c42-148">**Objets blob**</span><span class="sxs-lookup"><span data-stu-id="59c42-148">**Blobs**</span></span>

* <span data-ttu-id="59c42-149">**wad-control-container** : (uniquement pour le kit de développement logiciel 2.4 et précédents) contient les fichiers de configuration XML qui contrôlent les diagnostics Azure.</span><span class="sxs-lookup"><span data-stu-id="59c42-149">**wad-control-container** – (Only for SDK 2.4 and previous) Contains the XML configuration files that controls the Azure diagnostics .</span></span>
* <span data-ttu-id="59c42-150">**wad-iis-failedreqlogfiles** : contient des informations tirées des journaux de requêtes de IIS ayant échoué.</span><span class="sxs-lookup"><span data-stu-id="59c42-150">**wad-iis-failedreqlogfiles** – Contains information from IIS Failed Request logs.</span></span>
* <span data-ttu-id="59c42-151">**wad-iis-logfiles** : contient des informations sur les journaux IIS.</span><span class="sxs-lookup"><span data-stu-id="59c42-151">**wad-iis-logfiles** – Contains information about IIS logs.</span></span>
* <span data-ttu-id="59c42-152">**« personnalisé »** – conteneur personnalisé basé sur la configuration des répertoires contrôlés par la surveillance de diagnostic.</span><span class="sxs-lookup"><span data-stu-id="59c42-152">**"custom"** – A custom container based on configuring directories that are monitored by the diagnostic monitor.</span></span>  <span data-ttu-id="59c42-153">Le nom de ce conteneur d’objets blobs est spécifié dans WADDirectoriesTable.</span><span class="sxs-lookup"><span data-stu-id="59c42-153">The name of this blob container will be specified in WADDirectoriesTable.</span></span>

## <a name="tools-to-view-diagnostic-data"></a><span data-ttu-id="59c42-154">Outils permettant d’afficher les données de diagnostic</span><span class="sxs-lookup"><span data-stu-id="59c42-154">Tools to view diagnostic data</span></span>
<span data-ttu-id="59c42-155">Plusieurs outils sont disponibles pour afficher les données après leur transfert vers le stockage.</span><span class="sxs-lookup"><span data-stu-id="59c42-155">Several tools are available to view the data after it is transferred to storage.</span></span> <span data-ttu-id="59c42-156">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="59c42-156">For example:</span></span>

* <span data-ttu-id="59c42-157">Explorateur de serveurs dans Visual Studio : si vous avez installé Microsoft Azure Tools pour Microsoft Visual Studio, vous pouvez utiliser le nœud de stockage Azure dans l’Explorateur de serveurs pour afficher des objets blobs en lecture seule et les données du tableau depuis vos comptes de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="59c42-157">Server Explorer in Visual Studio - If you have installed the Azure Tools for Microsoft Visual Studio, you can use the Azure Storage node in Server Explorer to view read-only blob and table data from your Azure storage accounts.</span></span> <span data-ttu-id="59c42-158">Vous pouvez afficher des données à partir de votre compte d’émulateur de stockage local et de comptes de stockage que vous avez créés pour Azure.</span><span class="sxs-lookup"><span data-stu-id="59c42-158">You can display data from your local storage emulator account and also from storage accounts you have created for Azure.</span></span> <span data-ttu-id="59c42-159">Pour plus d’informations, consultez [Consultation et gestion des ressources de stockage avec l’Explorateur de serveurs](../vs-azure-tools-storage-resources-server-explorer-browse-manage.md).</span><span class="sxs-lookup"><span data-stu-id="59c42-159">For more information, see [Browsing and Managing Storage Resources with Server Explorer](../vs-azure-tools-storage-resources-server-explorer-browse-manage.md).</span></span>
* <span data-ttu-id="59c42-160">[L’explorateur de stockage Microsoft Azure](../vs-azure-tools-storage-manage-with-storage-explorer.md) est une application autonome qui vous permet d’utiliser facilement les données Azure Storage sur Windows, OSX et Linux.</span><span class="sxs-lookup"><span data-stu-id="59c42-160">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a standalone app that enables you to easily work with Azure Storage data on Windows, OSX, and Linux.</span></span>
* <span data-ttu-id="59c42-161">[Azure Management Studio](http://www.cerebrata.com/products/azure-management-studio/introduction) inclut Azure Diagnostics Manager qui vous permet d’afficher, de télécharger et de gérer les données de diagnostic collectées par les applications s’exécutant dans Azure.</span><span class="sxs-lookup"><span data-stu-id="59c42-161">[Azure Management Studio](http://www.cerebrata.com/products/azure-management-studio/introduction) includes Azure Diagnostics Manager which allows you to view, download and manage the diagnostics data collected by the applications running on Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="59c42-162">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="59c42-162">Next Steps</span></span>
[<span data-ttu-id="59c42-163">Assurer le suivi du flux dans une application Cloud Services avec Diagnostics Azure</span><span class="sxs-lookup"><span data-stu-id="59c42-163">Trace the flow in a Cloud Services application with Azure Diagnostics</span></span>](cloud-services-dotnet-diagnostics-trace-flow.md)

