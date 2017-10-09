---
title: "aaaStore et afficher les données de Diagnostic dans le stockage Azure | Documents Microsoft"
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
ms.openlocfilehash: dd47a2ef6d6488c80c102c72b2ebf6ca6d2e473f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="store-and-view-diagnostic-data-in-azure-storage"></a><span data-ttu-id="e110d-103">Stocker et afficher des données de diagnostic dans Azure Storage</span><span class="sxs-lookup"><span data-stu-id="e110d-103">Store and view diagnostic data in Azure Storage</span></span>
<span data-ttu-id="e110d-104">Données de diagnostic ne sont pas définitivement stockées, sauf si vous le transférez toohello l’émulateur de stockage Microsoft Azure ou tooAzure stockage.</span><span class="sxs-lookup"><span data-stu-id="e110d-104">Diagnostic data is not permanently stored unless you transfer it toohello Microsoft Azure storage emulator or tooAzure storage.</span></span> <span data-ttu-id="e110d-105">Une fois dans le stockage, elles peuvent être affichées avec un des outils disponibles.</span><span class="sxs-lookup"><span data-stu-id="e110d-105">Once in storage, it can be viewed with one of several available tools.</span></span>

## <a name="specify-a-storage-account"></a><span data-ttu-id="e110d-106">Spécifiez un compte de stockage</span><span class="sxs-lookup"><span data-stu-id="e110d-106">Specify a storage account</span></span>
<span data-ttu-id="e110d-107">Vous spécifiez le compte de stockage hello que vous souhaitez toouse dans le fichier ServiceConfiguration.cscfg de hello.</span><span class="sxs-lookup"><span data-stu-id="e110d-107">You specify hello storage account that you want toouse in hello ServiceConfiguration.cscfg file.</span></span> <span data-ttu-id="e110d-108">les informations de compte Hello sont définies comme une chaîne de connexion dans un paramètre de configuration.</span><span class="sxs-lookup"><span data-stu-id="e110d-108">hello account information is defined as a connection string in a configuration setting.</span></span> <span data-ttu-id="e110d-109">Hello exemple suivant montre hello chaîne de connexion par défaut créé pour un nouveau projet de Service Cloud dans Visual Studio :</span><span class="sxs-lookup"><span data-stu-id="e110d-109">hello following example shows hello default connection string created for a new Cloud Service project in  Visual Studio:</span></span>

```
    <ConfigurationSettings>
       <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="UseDevelopmentStorage=true" />
    </ConfigurationSettings>
```

<span data-ttu-id="e110d-110">Vous pouvez modifier ces informations de compte de connexion chaîne tooprovide pour un compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="e110d-110">You can change this connection string tooprovide account information for an Azure storage account.</span></span>

<span data-ttu-id="e110d-111">Selon le type de données de diagnostic qui sont collectées de hello, Azure Diagnostics utilise le service d’objets Blob hello ou service de Table hello.</span><span class="sxs-lookup"><span data-stu-id="e110d-111">Depending on hello type of diagnostic data that is being collected, Azure Diagnostics uses either hello Blob service or hello Table service.</span></span> <span data-ttu-id="e110d-112">Hello tableau suivant répertorie les sources de données hello qui sont conservées et leur format.</span><span class="sxs-lookup"><span data-stu-id="e110d-112">hello following table shows hello data sources that are persisted and their format.</span></span>

| <span data-ttu-id="e110d-113">Source de données</span><span class="sxs-lookup"><span data-stu-id="e110d-113">Data source</span></span> | <span data-ttu-id="e110d-114">Format de stockage</span><span class="sxs-lookup"><span data-stu-id="e110d-114">Storage format</span></span> |
| --- | --- |
| <span data-ttu-id="e110d-115">Journaux Azure</span><span class="sxs-lookup"><span data-stu-id="e110d-115">Azure logs</span></span> |<span data-ttu-id="e110d-116">Table</span><span class="sxs-lookup"><span data-stu-id="e110d-116">Table</span></span> |
| <span data-ttu-id="e110d-117">Journaux IIS 7.0</span><span class="sxs-lookup"><span data-stu-id="e110d-117">IIS 7.0 logs</span></span> |<span data-ttu-id="e110d-118">Blob</span><span class="sxs-lookup"><span data-stu-id="e110d-118">Blob</span></span> |
| <span data-ttu-id="e110d-119">Journaux d’infrastructure de diagnostics Azure</span><span class="sxs-lookup"><span data-stu-id="e110d-119">Azure Diagnostics infrastructure logs</span></span> |<span data-ttu-id="e110d-120">Table</span><span class="sxs-lookup"><span data-stu-id="e110d-120">Table</span></span> |
| <span data-ttu-id="e110d-121">Journaux de suivi de requête ayant échoué</span><span class="sxs-lookup"><span data-stu-id="e110d-121">Failed Request Trace logs</span></span> |<span data-ttu-id="e110d-122">Blob</span><span class="sxs-lookup"><span data-stu-id="e110d-122">Blob</span></span> |
| <span data-ttu-id="e110d-123">Journaux d'événements Windows</span><span class="sxs-lookup"><span data-stu-id="e110d-123">Windows Event logs</span></span> |<span data-ttu-id="e110d-124">Table</span><span class="sxs-lookup"><span data-stu-id="e110d-124">Table</span></span> |
| <span data-ttu-id="e110d-125">Compteurs de performances</span><span class="sxs-lookup"><span data-stu-id="e110d-125">Performance counters</span></span> |<span data-ttu-id="e110d-126">Table</span><span class="sxs-lookup"><span data-stu-id="e110d-126">Table</span></span> |
| <span data-ttu-id="e110d-127">Vidages sur incident</span><span class="sxs-lookup"><span data-stu-id="e110d-127">Crash dumps</span></span> |<span data-ttu-id="e110d-128">Blob</span><span class="sxs-lookup"><span data-stu-id="e110d-128">Blob</span></span> |
| <span data-ttu-id="e110d-129">Journaux d'erreurs personnalisés</span><span class="sxs-lookup"><span data-stu-id="e110d-129">Custom error logs</span></span> |<span data-ttu-id="e110d-130">Blob</span><span class="sxs-lookup"><span data-stu-id="e110d-130">Blob</span></span> |

## <a name="transfer-diagnostic-data"></a><span data-ttu-id="e110d-131">Transférer les données de diagnostic</span><span class="sxs-lookup"><span data-stu-id="e110d-131">Transfer diagnostic data</span></span>
<span data-ttu-id="e110d-132">Pour le SDK 2.5 et versions ultérieures, les données de diagnostic hello demande tootransfer peuvent se produire via le fichier de configuration hello.</span><span class="sxs-lookup"><span data-stu-id="e110d-132">For SDK 2.5 and later, hello request tootransfer diagnostic data can occur through hello configuration file.</span></span> <span data-ttu-id="e110d-133">Vous pouvez transférer des données de diagnostic à intervalles planifiés, tel que spécifié dans la configuration de hello.</span><span class="sxs-lookup"><span data-stu-id="e110d-133">You can transfer diagnostic data at scheduled intervals as specified in hello configuration.</span></span>

<span data-ttu-id="e110d-134">Pour 2.4 du Kit de développement logiciel précédent et vous pouvez demander des données de diagnostic hello tootransfer via le fichier de configuration hello ainsi que par programme.</span><span class="sxs-lookup"><span data-stu-id="e110d-134">For SDK 2.4 and previous you can request tootransfer hello diagnostic data through hello configuration file as well as programmatically.</span></span> <span data-ttu-id="e110d-135">méthode Hello vous permet également de toodo les transferts à la demande.</span><span class="sxs-lookup"><span data-stu-id="e110d-135">hello programmatic approach also allows you toodo on-demand transfers.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e110d-136">Lorsque vous transférez des données de diagnostic tooan compte de stockage Azure, vous encourez des frais pour les ressources de stockage hello par des données de diagnostic.</span><span class="sxs-lookup"><span data-stu-id="e110d-136">When you transfer diagnostic data tooan Azure storage account, you incur costs for hello storage resources that your diagnostic data uses.</span></span>
> 
> 

## <a name="store-diagnostic-data"></a><span data-ttu-id="e110d-137">Stockez les données de diagnostic</span><span class="sxs-lookup"><span data-stu-id="e110d-137">Store diagnostic data</span></span>
<span data-ttu-id="e110d-138">Données du journal sont stockées dans le stockage Blob ou de Table avec hello nom :</span><span class="sxs-lookup"><span data-stu-id="e110d-138">Log data is stored in either Blob or Table storage with hello following names:</span></span>

<span data-ttu-id="e110d-139">**Tables**</span><span class="sxs-lookup"><span data-stu-id="e110d-139">**Tables**</span></span>

* <span data-ttu-id="e110d-140">**WadLogsTable** - journaux écrits dans le code à l’aide d’écouteur de suivi hello.</span><span class="sxs-lookup"><span data-stu-id="e110d-140">**WadLogsTable** - Logs written in code using hello trace listener.</span></span>
* <span data-ttu-id="e110d-141">**WADDiagnosticInfrastructureLogsTable** : modifications de configuration et d’analyse de diagnostic.</span><span class="sxs-lookup"><span data-stu-id="e110d-141">**WADDiagnosticInfrastructureLogsTable** - Diagnostic monitor and configuration changes.</span></span>
* <span data-ttu-id="e110d-142">**WADDirectoriesTable** – répertoires de contrôle qui analyse le diagnostic hello.</span><span class="sxs-lookup"><span data-stu-id="e110d-142">**WADDirectoriesTable** – Directories that hello diagnostic monitor is monitoring.</span></span>  <span data-ttu-id="e110d-143">Cela inclut les journaux IIS, les journaux de requêtes ayant échoué et les répertoires personnalisés IIS.</span><span class="sxs-lookup"><span data-stu-id="e110d-143">This includes IIS logs, IIS failed request logs, and custom directories.</span></span>  <span data-ttu-id="e110d-144">emplacement Hello du fichier journal de blob hello est spécifié dans le champ de conteneur hello et hello nom de hello blob est dans le champ RelativePath de hello.</span><span class="sxs-lookup"><span data-stu-id="e110d-144">hello location of hello blob log file is specified in hello Container field and hello name of hello blob is in hello RelativePath field.</span></span>  <span data-ttu-id="e110d-145">champ de AbsolutePath Hello indique l’emplacement de hello et le nom du fichier de hello tel qu’il existait sur hello machine virtuelle Azure.</span><span class="sxs-lookup"><span data-stu-id="e110d-145">hello AbsolutePath field indicates hello location and name of hello file as it existed on hello Azure virtual machine.</span></span>
* <span data-ttu-id="e110d-146">**WADPerformanceCountersTable** : les compteurs de performance.</span><span class="sxs-lookup"><span data-stu-id="e110d-146">**WADPerformanceCountersTable** – Performance counters.</span></span>
* <span data-ttu-id="e110d-147">**WADWindowsEventLogsTable** : journaux des événements Windows.</span><span class="sxs-lookup"><span data-stu-id="e110d-147">**WADWindowsEventLogsTable** – Windows Event logs.</span></span>

<span data-ttu-id="e110d-148">**Objets blob**</span><span class="sxs-lookup"><span data-stu-id="e110d-148">**Blobs**</span></span>

* <span data-ttu-id="e110d-149">**WAD-control-container** : (uniquement pour les SDK 2.4 et précédente) contient les fichiers de configuration XML hello qui contrôle hello diagnostics Azure.</span><span class="sxs-lookup"><span data-stu-id="e110d-149">**wad-control-container** – (Only for SDK 2.4 and previous) Contains hello XML configuration files that controls hello Azure diagnostics .</span></span>
* <span data-ttu-id="e110d-150">**wad-iis-failedreqlogfiles** : contient des informations tirées des journaux de requêtes de IIS ayant échoué.</span><span class="sxs-lookup"><span data-stu-id="e110d-150">**wad-iis-failedreqlogfiles** – Contains information from IIS Failed Request logs.</span></span>
* <span data-ttu-id="e110d-151">**wad-iis-logfiles** : contient des informations sur les journaux IIS.</span><span class="sxs-lookup"><span data-stu-id="e110d-151">**wad-iis-logfiles** – Contains information about IIS logs.</span></span>
* <span data-ttu-id="e110d-152">**« custom »** – conteneur personnalisé basé sur la configuration des répertoires qui sont contrôlés par le moniteur de diagnostic hello.</span><span class="sxs-lookup"><span data-stu-id="e110d-152">**"custom"** – A custom container based on configuring directories that are monitored by hello diagnostic monitor.</span></span>  <span data-ttu-id="e110d-153">nom de Hello de ce conteneur d’objets blob est spécifié dans WADDirectoriesTable.</span><span class="sxs-lookup"><span data-stu-id="e110d-153">hello name of this blob container will be specified in WADDirectoriesTable.</span></span>

## <a name="tools-tooview-diagnostic-data"></a><span data-ttu-id="e110d-154">Données de diagnostic Tools tooview</span><span class="sxs-lookup"><span data-stu-id="e110d-154">Tools tooview diagnostic data</span></span>
<span data-ttu-id="e110d-155">Plusieurs outils sont les données de salutation tooview disponibles une fois qu’il toostorage transféré.</span><span class="sxs-lookup"><span data-stu-id="e110d-155">Several tools are available tooview hello data after it is transferred toostorage.</span></span> <span data-ttu-id="e110d-156">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="e110d-156">For example:</span></span>

* <span data-ttu-id="e110d-157">L’Explorateur de serveurs dans Visual Studio - si vous avez installé hello Windows Azure Tools pour Microsoft Visual Studio, vous pouvez utiliser nœud hello Azure dans l’Explorateur de serveurs tooview données en lecture seule blob et de table à partir de vos comptes de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="e110d-157">Server Explorer in Visual Studio - If you have installed hello Azure Tools for Microsoft Visual Studio, you can use hello Azure Storage node in Server Explorer tooview read-only blob and table data from your Azure storage accounts.</span></span> <span data-ttu-id="e110d-158">Vous pouvez afficher des données à partir de votre compte d’émulateur de stockage local et de comptes de stockage que vous avez créés pour Azure.</span><span class="sxs-lookup"><span data-stu-id="e110d-158">You can display data from your local storage emulator account and also from storage accounts you have created for Azure.</span></span> <span data-ttu-id="e110d-159">Pour plus d’informations, consultez [Consultation et gestion des ressources de stockage avec l’Explorateur de serveurs](../vs-azure-tools-storage-resources-server-explorer-browse-manage.md).</span><span class="sxs-lookup"><span data-stu-id="e110d-159">For more information, see [Browsing and Managing Storage Resources with Server Explorer](../vs-azure-tools-storage-resources-server-explorer-browse-manage.md).</span></span>
* <span data-ttu-id="e110d-160">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) est une application autonome qui vous permet de travail tooeasily avec des données de stockage Azure sur Windows, OSX et Linux.</span><span class="sxs-lookup"><span data-stu-id="e110d-160">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a standalone app that enables you tooeasily work with Azure Storage data on Windows, OSX, and Linux.</span></span>
* <span data-ttu-id="e110d-161">[Azure Management Studio](http://www.cerebrata.com/products/azure-management-studio/introduction) inclut Azure Diagnostics Manager qui vous permet de tooview, télécharger et gérer des données de diagnostic hello collectées par les applications de hello s’exécutant sur Azure.</span><span class="sxs-lookup"><span data-stu-id="e110d-161">[Azure Management Studio](http://www.cerebrata.com/products/azure-management-studio/introduction) includes Azure Diagnostics Manager which allows you tooview, download and manage hello diagnostics data collected by hello applications running on Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e110d-162">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e110d-162">Next Steps</span></span>
[<span data-ttu-id="e110d-163">Flux de hello de trace dans une application de Services de Cloud avec Azure Diagnostics</span><span class="sxs-lookup"><span data-stu-id="e110d-163">Trace hello flow in a Cloud Services application with Azure Diagnostics</span></span>](cloud-services-dotnet-diagnostics-trace-flow.md)

