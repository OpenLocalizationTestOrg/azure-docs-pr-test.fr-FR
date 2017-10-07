---
title: "stockage d’objets blob aaaUse pour le stockage IIS et de table pour les événements de l’Analytique des journaux Azure | Documents Microsoft"
description: "Analytique de journal peut lire des journaux hello pour les services Azure qui écrivent stockage tootable de diagnostics ou journaux IIS écrits tooblob stockage."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: bf444752-ecc1-4306-9489-c29cb37d6045
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2017
ms.author: magoedte
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ff3de04dc8cb6729c1443372ec31a0e8dc47f273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-blob-storage-for-iis-and-azure-table-storage-for-events-with-log-analytics"></a><span data-ttu-id="183c7-103">Utilisation d’un Stockage Blob Azure pour IIS et d’un Stockage Table Azure pour les événements avec Log Analytics</span><span class="sxs-lookup"><span data-stu-id="183c7-103">Use Azure blob storage for IIS and Azure table storage for events with Log Analytics</span></span>

<span data-ttu-id="183c7-104">Analytique de journal peut lire les journaux hello pour hello suivant des services qui écrivent des diagnostics tootable stockage ou IIS consigne écrite tooblob stockage :</span><span class="sxs-lookup"><span data-stu-id="183c7-104">Log Analytics can read hello logs for hello following services that write diagnostics tootable storage or IIS logs written tooblob storage:</span></span>

* <span data-ttu-id="183c7-105">Clusters Service Fabric (version préliminaire)</span><span class="sxs-lookup"><span data-stu-id="183c7-105">Service Fabric clusters (Preview)</span></span>
* <span data-ttu-id="183c7-106">Machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="183c7-106">Virtual Machines</span></span>
* <span data-ttu-id="183c7-107">Rôle de travail/web</span><span class="sxs-lookup"><span data-stu-id="183c7-107">Web/Worker Roles</span></span>

<span data-ttu-id="183c7-108">Pour que Log Analytics puisse collecter les données pour ces ressources, les diagnostics Azure doivent être activés.</span><span class="sxs-lookup"><span data-stu-id="183c7-108">Before Log Analytics can collect data for these resources, Azure diagnostics must be enabled.</span></span>

<span data-ttu-id="183c7-109">Une fois les diagnostics sont activés, vous pouvez utiliser hello portail Azure ou PowerShell configurer les journaux de hello toocollect Analytique de journal.</span><span class="sxs-lookup"><span data-stu-id="183c7-109">Once diagnostics are enabled, you can use hello Azure portal or PowerShell configure Log Analytics toocollect hello logs.</span></span>

<span data-ttu-id="183c7-110">Diagnostics Azure est une extension d’Azure qui vous permet de toocollect les données de diagnostic à partir d’un rôle de travail, un rôle web ou un ordinateur virtuel en cours d’exécution dans Azure.</span><span class="sxs-lookup"><span data-stu-id="183c7-110">Azure Diagnostics is an Azure extension that enables you toocollect diagnostic data from a worker role, web role, or virtual machine running in Azure.</span></span> <span data-ttu-id="183c7-111">les données de salutation sont stockées dans un compte de stockage Azure et peuvent ensuite être recueillies en Analytique de journal.</span><span class="sxs-lookup"><span data-stu-id="183c7-111">hello data is stored in an Azure storage account and can then be collected by Log Analytics.</span></span>

<span data-ttu-id="183c7-112">Pour l’Analytique des journaux toocollect ces journaux de Diagnostics Windows Azure, hello journaux doit se trouver dans hello emplacements suivants :</span><span class="sxs-lookup"><span data-stu-id="183c7-112">For Log Analytics toocollect these Azure Diagnostics logs, hello logs must be in hello following locations:</span></span>

| <span data-ttu-id="183c7-113">Type de journal</span><span class="sxs-lookup"><span data-stu-id="183c7-113">Log Type</span></span> | <span data-ttu-id="183c7-114">Type de ressource</span><span class="sxs-lookup"><span data-stu-id="183c7-114">Resource Type</span></span> | <span data-ttu-id="183c7-115">Lieu</span><span class="sxs-lookup"><span data-stu-id="183c7-115">Location</span></span> |
| --- | --- | --- |
| <span data-ttu-id="183c7-116">Journaux IIS</span><span class="sxs-lookup"><span data-stu-id="183c7-116">IIS logs</span></span> |<span data-ttu-id="183c7-117">Machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="183c7-117">Virtual Machines</span></span> <br> <span data-ttu-id="183c7-118">Rôles web</span><span class="sxs-lookup"><span data-stu-id="183c7-118">Web roles</span></span> <br> <span data-ttu-id="183c7-119">Rôles de travail</span><span class="sxs-lookup"><span data-stu-id="183c7-119">Worker roles</span></span> |<span data-ttu-id="183c7-120">wad-iis-logfiles (Stockage Blob)</span><span class="sxs-lookup"><span data-stu-id="183c7-120">wad-iis-logfiles (Blob Storage)</span></span> |
| <span data-ttu-id="183c7-121">syslog</span><span class="sxs-lookup"><span data-stu-id="183c7-121">Syslog</span></span> |<span data-ttu-id="183c7-122">Machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="183c7-122">Virtual Machines</span></span> |<span data-ttu-id="183c7-123">LinuxSyslogVer2v0 (Stockage Table)</span><span class="sxs-lookup"><span data-stu-id="183c7-123">LinuxsyslogVer2v0 (Table Storage)</span></span> |
| <span data-ttu-id="183c7-124">Événements opérationnels Service Fabric</span><span class="sxs-lookup"><span data-stu-id="183c7-124">Service Fabric Operational Events</span></span> |<span data-ttu-id="183c7-125">Nœuds Service Fabric</span><span class="sxs-lookup"><span data-stu-id="183c7-125">Service Fabric nodes</span></span> |<span data-ttu-id="183c7-126">WADServiceFabricSystemEventTable</span><span class="sxs-lookup"><span data-stu-id="183c7-126">WADServiceFabricSystemEventTable</span></span> |
| <span data-ttu-id="183c7-127">Événements Reliable Actor Service Fabric</span><span class="sxs-lookup"><span data-stu-id="183c7-127">Service Fabric Reliable Actor Events</span></span> |<span data-ttu-id="183c7-128">Nœuds Service Fabric</span><span class="sxs-lookup"><span data-stu-id="183c7-128">Service Fabric nodes</span></span> |<span data-ttu-id="183c7-129">WADServiceFabricReliableActorEventTable</span><span class="sxs-lookup"><span data-stu-id="183c7-129">WADServiceFabricReliableActorEventTable</span></span> |
| <span data-ttu-id="183c7-130">Événements de service fiable Service Fabric</span><span class="sxs-lookup"><span data-stu-id="183c7-130">Service Fabric Reliable Service Events</span></span> |<span data-ttu-id="183c7-131">Nœuds Service Fabric</span><span class="sxs-lookup"><span data-stu-id="183c7-131">Service Fabric nodes</span></span> |<span data-ttu-id="183c7-132">WADServiceFabricReliableServiceEventTable</span><span class="sxs-lookup"><span data-stu-id="183c7-132">WADServiceFabricReliableServiceEventTable</span></span> |
| <span data-ttu-id="183c7-133">Journaux d'événements Windows</span><span class="sxs-lookup"><span data-stu-id="183c7-133">Windows Event logs</span></span> |<span data-ttu-id="183c7-134">Nœuds Service Fabric</span><span class="sxs-lookup"><span data-stu-id="183c7-134">Service Fabric nodes</span></span> <br> <span data-ttu-id="183c7-135">Machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="183c7-135">Virtual Machines</span></span> <br> <span data-ttu-id="183c7-136">Rôles web</span><span class="sxs-lookup"><span data-stu-id="183c7-136">Web roles</span></span> <br> <span data-ttu-id="183c7-137">Rôles de travail</span><span class="sxs-lookup"><span data-stu-id="183c7-137">Worker roles</span></span> |<span data-ttu-id="183c7-138">WADWindowsEventLogsTable (Stockage Table)</span><span class="sxs-lookup"><span data-stu-id="183c7-138">WADWindowsEventLogsTable (Table Storage)</span></span> |
| <span data-ttu-id="183c7-139">Journaux de suivi des événements ETW Windows</span><span class="sxs-lookup"><span data-stu-id="183c7-139">Windows ETW logs</span></span> |<span data-ttu-id="183c7-140">Nœuds Service Fabric</span><span class="sxs-lookup"><span data-stu-id="183c7-140">Service Fabric nodes</span></span> <br> <span data-ttu-id="183c7-141">Machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="183c7-141">Virtual Machines</span></span> <br> <span data-ttu-id="183c7-142">Rôles web</span><span class="sxs-lookup"><span data-stu-id="183c7-142">Web roles</span></span> <br> <span data-ttu-id="183c7-143">Rôles de travail</span><span class="sxs-lookup"><span data-stu-id="183c7-143">Worker roles</span></span> |<span data-ttu-id="183c7-144">WADETWEventTable (Stockage Table)</span><span class="sxs-lookup"><span data-stu-id="183c7-144">WADETWEventTable (Table Storage)</span></span> |

> [!NOTE]
> <span data-ttu-id="183c7-145">Les journaux IIS des sites Web Azure ne sont actuellement pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="183c7-145">IIS logs from Azure Websites are not currently supported.</span></span>
>
>

<span data-ttu-id="183c7-146">Pour les ordinateurs virtuels, vous pouvez hello installation hello [agent d’Analytique de journal](log-analytics-azure-vm-extension.md) dans votre machine virtuelle tooenable des informations supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="183c7-146">For virtual machines, you have hello option of installing hello [Log Analytics agent](log-analytics-azure-vm-extension.md) into your virtual machine tooenable additional insights.</span></span> <span data-ttu-id="183c7-147">En outre les journaux IIS en mesure de tooanalyze toobeing et les journaux des événements, vous pouvez effectuer des analyses supplémentaires, notamment l’évaluation de la mise à jour, de suivi des modifications de configuration et d’évaluation de SQL.</span><span class="sxs-lookup"><span data-stu-id="183c7-147">In addition toobeing able tooanalyze IIS logs and Event Logs, you can perform additional analysis including configuration change tracking, SQL assessment, and update assessment.</span></span>

## <a name="enable-azure-diagnostics-in-a-virtual-machine-for-event-log-and-iis-log-collection"></a><span data-ttu-id="183c7-148">Activation des diagnostics Azure dans une machine virtuelle pour la collecte des journaux IIS et des journaux des événements</span><span class="sxs-lookup"><span data-stu-id="183c7-148">Enable Azure diagnostics in a virtual machine for event log and IIS log collection</span></span>
<span data-ttu-id="183c7-149">Hello utilisation suivant la procédure tooenable diagnostics Azure dans une machine virtuelle pour le journal des événements et IIS de collecte à l’aide du portail Microsoft Azure hello des journaux.</span><span class="sxs-lookup"><span data-stu-id="183c7-149">Use hello following procedure tooenable Azure diagnostics in a virtual machine for Event Log and IIS log collection using hello Microsoft Azure portal.</span></span>

### <a name="tooenable-azure-diagnostics-in-a-virtual-machine-with-hello-azure-portal"></a><span data-ttu-id="183c7-150">tooenable diagnostics Azure dans une machine virtuelle avec hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="183c7-150">tooenable Azure diagnostics in a virtual machine with hello Azure portal</span></span>
1. <span data-ttu-id="183c7-151">Installez hello Agent de machine virtuelle lorsque vous créez une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="183c7-151">Install hello VM Agent when you create a virtual machine.</span></span> <span data-ttu-id="183c7-152">Si l’ordinateur virtuel de hello existe déjà, vérifiez que hello Qu'agent de machine virtuelle est déjà installé.</span><span class="sxs-lookup"><span data-stu-id="183c7-152">If hello virtual machine already exists, verify that hello VM Agent is already installed.</span></span>

   * <span data-ttu-id="183c7-153">Dans hello portail Azure, accédez toohello virtuels, sélectionnez **Configuration facultative**, puis **Diagnostics** et **état** trop**sur**.</span><span class="sxs-lookup"><span data-stu-id="183c7-153">In hello Azure portal, navigate toohello virtual machine, select **Optional Configuration**, then **Diagnostics** and set **Status** too**On**.</span></span>

     <span data-ttu-id="183c7-154">À l’achèvement, hello VM porte l’extension de Diagnostics Windows Azure hello installé et en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="183c7-154">Upon completion, hello VM has hello Azure Diagnostics extension installed and running.</span></span> <span data-ttu-id="183c7-155">Cette extension est chargée de collecter vos données de diagnostic.</span><span class="sxs-lookup"><span data-stu-id="183c7-155">This extension is responsible for collecting your diagnostics data.</span></span>
2. <span data-ttu-id="183c7-156">Activation de l’analyse et configuration de la journalisation des événements sur une machine virtuelle existante.</span><span class="sxs-lookup"><span data-stu-id="183c7-156">Enable monitoring and configure event logging on an existing VM.</span></span> <span data-ttu-id="183c7-157">Vous pouvez activer les diagnostics au hello au niveau de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="183c7-157">You can enable diagnostics at hello VM level.</span></span> <span data-ttu-id="183c7-158">tooenable diagnostics et ensuite configurer la journalisation des événements, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="183c7-158">tooenable diagnostics and then configure event logging, perform hello following steps:</span></span>

   1. <span data-ttu-id="183c7-159">Sélectionnez hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="183c7-159">Select hello VM.</span></span>
   2. <span data-ttu-id="183c7-160">Cliquez sur **Analyse**.</span><span class="sxs-lookup"><span data-stu-id="183c7-160">Click **Monitoring**.</span></span>
   3. <span data-ttu-id="183c7-161">Cliquez sur **Diagnostics**.</span><span class="sxs-lookup"><span data-stu-id="183c7-161">Click **Diagnostics**.</span></span>
   4. <span data-ttu-id="183c7-162">Ensemble hello **état** trop**ON**.</span><span class="sxs-lookup"><span data-stu-id="183c7-162">Set hello **Status** too**ON**.</span></span>
   5. <span data-ttu-id="183c7-163">Sélectionnez chaque journal de diagnostics que vous souhaitez toocollect.</span><span class="sxs-lookup"><span data-stu-id="183c7-163">Select each diagnostics log that you want toocollect.</span></span>
   6. <span data-ttu-id="183c7-164">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="183c7-164">Click **OK**.</span></span>

## <a name="enable-azure-diagnostics-in-a-web-role-for-iis-log-and-event-collection"></a><span data-ttu-id="183c7-165">Activation des diagnostics Azure dans un rôle Web pour la collecte de journaux IIS et des événements</span><span class="sxs-lookup"><span data-stu-id="183c7-165">Enable Azure diagnostics in a Web role for IIS log and event collection</span></span>
<span data-ttu-id="183c7-166">Consultez trop[comment tooEnable Diagnostics dans un Service Cloud](../cloud-services/cloud-services-dotnet-diagnostics.md) pour obtenir des instructions générales sur l’activation des diagnostics Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="183c7-166">Refer too[How tooEnable Diagnostics in a Cloud Service](../cloud-services/cloud-services-dotnet-diagnostics.md) for general steps on enabling Azure diagnostics.</span></span> <span data-ttu-id="183c7-167">instructions Hello ci-dessous utilisent ces informations et le personnaliser pour une utilisation avec Analytique de journal.</span><span class="sxs-lookup"><span data-stu-id="183c7-167">hello instructions below use this information and customize it for use with Log Analytics.</span></span>

<span data-ttu-id="183c7-168">Avec les diagnostics Azure activés :</span><span class="sxs-lookup"><span data-stu-id="183c7-168">With Azure diagnostics enabled:</span></span>

* <span data-ttu-id="183c7-169">Journaux IIS sont stockés par défaut, avec les données transférées à l’intervalle de transfert scheduledTransferPeriod Bonjour.</span><span class="sxs-lookup"><span data-stu-id="183c7-169">IIS logs are stored by default, with log data transferred at hello scheduledTransferPeriod transfer interval.</span></span>
* <span data-ttu-id="183c7-170">Les journaux des événements Windows ne sont pas transférés par défaut.</span><span class="sxs-lookup"><span data-stu-id="183c7-170">Windows Event Logs are not transferred by default.</span></span>

### <a name="tooenable-diagnostics"></a><span data-ttu-id="183c7-171">tooenable diagnostics</span><span class="sxs-lookup"><span data-stu-id="183c7-171">tooenable diagnostics</span></span>
<span data-ttu-id="183c7-172">tooenable journaux des événements Windows ou toochange hello scheduledTransferPeriod, configurez les Diagnostics Windows Azure à l’aide du fichier de configuration hello XML (diagnostics.wadcfg), comme indiqué dans [étape 4 : créer votre fichier de configuration de Diagnostics et installer hello extension](../cloud-services/cloud-services-dotnet-diagnostics.md)</span><span class="sxs-lookup"><span data-stu-id="183c7-172">tooenable Windows Event Logs, or toochange hello scheduledTransferPeriod, configure Azure Diagnostics using hello XML configuration file (diagnostics.wadcfg), as shown in [Step 4: Create your Diagnostics configuration file and install hello extension](../cloud-services/cloud-services-dotnet-diagnostics.md)</span></span>

<span data-ttu-id="183c7-173">Hello exemple de fichier de configuration suivant collecte les journaux IIS et tous les événements à partir de l’Application de hello et les journaux système :</span><span class="sxs-lookup"><span data-stu-id="183c7-173">hello following example configuration file collects IIS Logs and all Events from hello Application and System logs:</span></span>

```
    <?xml version="1.0" encoding="utf-8" ?>
    <DiagnosticMonitorConfiguration xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration"
          configurationChangePollInterval="PT1M"
          overallQuotaInMB="4096">

      <Directories bufferQuotaInMB="0"
         scheduledTransferPeriod="PT10M">  
        <!-- IISLogs are only relevant tooWeb roles -->
        <IISLogs container="wad-iis" directoryQuotaInMB="0" />
      </Directories>

      <WindowsEventLog bufferQuotaInMB="0"
         scheduledTransferLogLevelFilter="Verbose"
         scheduledTransferPeriod="PT10M">
        <DataSource name="Application!*" />
        <DataSource name="System!*" />
      </WindowsEventLog>

    </DiagnosticMonitorConfiguration>
```

<span data-ttu-id="183c7-174">Assurez-vous que votre élément ConfigurationSettings spécifie un compte de stockage, comme dans hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="183c7-174">Ensure that your ConfigurationSettings specifies a storage account, as in hello following example:</span></span>

```
    <ConfigurationSettings>
       <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="DefaultEndpointsProtocol=https;AccountName=<AccountName>;AccountKey=<AccountKey>"/>
    </ConfigurationSettings>
```

<span data-ttu-id="183c7-175">Hello **AccountName** et **AccountKey** valeurs trouvent Bonjour Azure portal dans le tableau de bord des comptes de stockage de hello, sous Gérer les clés d’accès.</span><span class="sxs-lookup"><span data-stu-id="183c7-175">hello **AccountName** and **AccountKey** values are found in hello Azure portal in hello storage account dashboard, under Manage Access Keys.</span></span> <span data-ttu-id="183c7-176">protocole Hello pour la chaîne de connexion hello doit être **https**.</span><span class="sxs-lookup"><span data-stu-id="183c7-176">hello protocol for hello connection string must be **https**.</span></span>

<span data-ttu-id="183c7-177">Une fois la configuration de diagnostic mise à jour hello est appliquée tooyour le service cloud et écrit les diagnostics tooAzure stockage, vous êtes prêt tooconfigure Analytique de journal.</span><span class="sxs-lookup"><span data-stu-id="183c7-177">Once hello updated diagnostic configuration is applied tooyour cloud service and it is writing diagnostics tooAzure Storage, then you are ready tooconfigure Log Analytics.</span></span>

## <a name="use-hello-azure-portal-toocollect-logs-from-azure-storage"></a><span data-ttu-id="183c7-178">Utiliser les journaux de toocollect portail Azure hello depuis le stockage Azure</span><span class="sxs-lookup"><span data-stu-id="183c7-178">Use hello Azure portal toocollect logs from Azure Storage</span></span>
<span data-ttu-id="183c7-179">Vous pouvez utiliser les journaux de hello toocollect de hello tooconfigure portail Azure Analytique de journal pour hello suivant des services Azure :</span><span class="sxs-lookup"><span data-stu-id="183c7-179">You can use hello Azure portal tooconfigure Log Analytics toocollect hello logs for hello following Azure services:</span></span>

* <span data-ttu-id="183c7-180">Clusters Service Fabric</span><span class="sxs-lookup"><span data-stu-id="183c7-180">Service Fabric clusters</span></span>
* <span data-ttu-id="183c7-181">Machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="183c7-181">Virtual Machines</span></span>
* <span data-ttu-id="183c7-182">Rôle de travail/web</span><span class="sxs-lookup"><span data-stu-id="183c7-182">Web/Worker Roles</span></span>

<span data-ttu-id="183c7-183">Bonjour portail Azure, accédez d’espace de travail tooyour Analytique de journal, exécutez les hello tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="183c7-183">In hello Azure portal, navigate tooyour Log Analytics workspace and perform hello following tasks:</span></span>

1. <span data-ttu-id="183c7-184">Cliquez sur *Journaux des comptes de stockage*.</span><span class="sxs-lookup"><span data-stu-id="183c7-184">Click *Storage accounts logs*</span></span>
2. <span data-ttu-id="183c7-185">Cliquez sur hello *ajouter* tâche</span><span class="sxs-lookup"><span data-stu-id="183c7-185">Click hello *Add* task</span></span>
3. <span data-ttu-id="183c7-186">Sélectionnez le compte de stockage hello qui contient les journaux de diagnostic hello</span><span class="sxs-lookup"><span data-stu-id="183c7-186">Select hello Storage account that contains hello diagnostics logs</span></span>
   * <span data-ttu-id="183c7-187">Ce compte peut être un compte de stockage classique ou un compte de stockage Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="183c7-187">This account can be either a classic storage account or an Azure Resource Manager storage account</span></span>
4. <span data-ttu-id="183c7-188">Sélectionnez hello, Type de données des journaux de toocollect pour</span><span class="sxs-lookup"><span data-stu-id="183c7-188">Select hello Data Type you want toocollect logs for</span></span>
   * <span data-ttu-id="183c7-189">choix de Hello sont des journaux IIS ; Événements ; Syslog (Linux) ; Journaux ETW ; Événements de l’infrastructure de service</span><span class="sxs-lookup"><span data-stu-id="183c7-189">hello choices are IIS Logs; Events; Syslog (Linux); ETW Logs; Service Fabric Events</span></span>
5. <span data-ttu-id="183c7-190">valeur Hello pour la Source est automatiquement rempli avec hello, type de données et ne peut pas être modifiées.</span><span class="sxs-lookup"><span data-stu-id="183c7-190">hello value for Source is automatically populated based on hello data type and cannot be changed</span></span>
6. <span data-ttu-id="183c7-191">Cliquez sur OK toosave hello configuration</span><span class="sxs-lookup"><span data-stu-id="183c7-191">Click OK toosave hello configuration</span></span>

<span data-ttu-id="183c7-192">Répétez les étapes 2 à 6 pour les types de comptes et les données supplémentaires de stockage que vous souhaitez Analytique de journal toocollect.</span><span class="sxs-lookup"><span data-stu-id="183c7-192">Repeat steps 2-6 for additional storage accounts and data types that you want Log Analytics toocollect.</span></span>

<span data-ttu-id="183c7-193">Dans environ 30 minutes, vous êtes en mesure de toosee données hello compte de stockage dans le journal Analytique.</span><span class="sxs-lookup"><span data-stu-id="183c7-193">In approximately 30 minutes, you are able toosee data from hello storage account in Log Analytics.</span></span> <span data-ttu-id="183c7-194">Vous verrez seulement les données écrites toostorage après que hello configuration est appliquée.</span><span class="sxs-lookup"><span data-stu-id="183c7-194">You will only see data that is written toostorage after hello configuration is applied.</span></span> <span data-ttu-id="183c7-195">Analytique de journal ne lit pas les données préexistantes hello hello compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="183c7-195">Log Analytics does not read hello pre-existing data from hello storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="183c7-196">portail de Hello ne valide pas que hello Source existe dans le compte de stockage hello ou si les données nouvelles sont écrites.</span><span class="sxs-lookup"><span data-stu-id="183c7-196">hello portal does not validate that hello Source exists in hello storage account or if new data is being written.</span></span>
>
>

## <a name="enable-azure-diagnostics-in-a-virtual-machine-for-event-log-and-iis-log-collection-using-powershell"></a><span data-ttu-id="183c7-197">Activer les diagnostics Azure dans une machine virtuelle pour la collecte des journaux IIS et des journaux des événements avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="183c7-197">Enable Azure diagnostics in a virtual machine for event log and IIS log collection using PowerShell</span></span>
<span data-ttu-id="183c7-198">Hello d’utiliser les étapes [tooindex d’Analytique de journal Configuration des diagnostics Azure](log-analytics-powershell-workspace-configuration.md#configuring-log-analytics-to-index-azure-diagnostics) tooread de PowerShell toouse des diagnostics Azure qui sont écrites tootable stockage.</span><span class="sxs-lookup"><span data-stu-id="183c7-198">Use hello steps in [Configuring Log Analytics tooindex Azure diagnostics](log-analytics-powershell-workspace-configuration.md#configuring-log-analytics-to-index-azure-diagnostics) toouse PowerShell tooread from Azure diagnostics that are written tootable storage.</span></span>

<span data-ttu-id="183c7-199">À l’aide d’Azure PowerShell vous pouvez spécifier plus précisément les événements hello écrits tooAzure stockage.</span><span class="sxs-lookup"><span data-stu-id="183c7-199">Using Azure PowerShell you can more precisely specify hello events that are written tooAzure Storage.</span></span>
<span data-ttu-id="183c7-200">Pour plus d'informations, consultez la page [Activation des diagnostics dans les machines virtuelles Azure](../virtual-machines-dotnet-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="183c7-200">For more information, see [Enabling Diagnostics in Azure Virtual Machines](../virtual-machines-dotnet-diagnostics.md).</span></span>

<span data-ttu-id="183c7-201">Vous pouvez activer et mettre à jour des diagnostics Windows Azure à l’aide de hello suite du script PowerShell.</span><span class="sxs-lookup"><span data-stu-id="183c7-201">You can enable and update Azure diagnostics using hello following PowerShell script.</span></span>
<span data-ttu-id="183c7-202">Vous pouvez également utiliser ce script avec une configuration de journalisation personnalisée.</span><span class="sxs-lookup"><span data-stu-id="183c7-202">You can also use this script with a custom logging configuration.</span></span>
<span data-ttu-id="183c7-203">Modifier le compte de stockage hello script tooset hello, nom du service et nom d’ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="183c7-203">Modify hello script tooset hello storage account, service name, and virtual machine name.</span></span>
<span data-ttu-id="183c7-204">script de Hello utilise des applets de commande pour les machines virtuelles classiques.</span><span class="sxs-lookup"><span data-stu-id="183c7-204">hello script uses cmdlets for classic virtual machines.</span></span>

<span data-ttu-id="183c7-205">Examinez hello suivant l’exemple de script, copiez-le, modifiez-le si nécessaire, enregistrez l’exemple hello dans un fichier de script PowerShell, puis exécutez le script de hello.</span><span class="sxs-lookup"><span data-stu-id="183c7-205">Review hello following script sample, copy it, modify it as needed, save hello sample as a PowerShell script file, and then run hello script.</span></span>

```
    #Connect tooAzure
    Add-AzureAccount

    # settings toochange:
    $wad_storage_account_name = "myStorageAccount"
    $service_name = "myService"
    $vm_name = "myVM"

    #Construct Azure Diagnostics public config and convert tooconfig format

    # Collect just system error events:
    $wad_xml_config = "<WadCfg><DiagnosticMonitorConfiguration><WindowsEventLog scheduledTransferPeriod=""PT1M""><DataSource name=""System!* "" /></WindowsEventLog></DiagnosticMonitorConfiguration></WadCfg>"

    $wad_b64_config = [System.Convert]::ToBase64String([System.Text.Encoding]::UTF8.GetBytes($wad_xml_config))
    $wad_public_config = [string]::Format("{{""xmlCfg"":""{0}""}}",$wad_b64_config)

    #Construct Azure diagnostics private config

    $wad_storage_account_key = (Get-AzureStorageKey $wad_storage_account_name).Primary
    $wad_private_config = [string]::Format("{{""storageAccountName"":""{0}"",""storageAccountKey"":""{1}""}}",$wad_storage_account_name,$wad_storage_account_key)

    #Enable Diagnostics Extension for Virtual Machine

    $wad_extension_name = "IaaSDiagnostics"
    $wad_publisher = "Microsoft.Azure.Diagnostics"
    $wad_version = (Get-AzureVMAvailableExtension -Publisher $wad_publisher -ExtensionName $wad_extension_name).Version # Gets latest version of hello extension

    (Get-AzureVM -ServiceName $service_name -Name $vm_name) | Set-AzureVMExtension -ExtensionName $wad_extension_name -Publisher $wad_publisher -PublicConfiguration $wad_public_config -PrivateConfiguration $wad_private_config -Version $wad_version | Update-AzureVM
```


## <a name="next-steps"></a><span data-ttu-id="183c7-206">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="183c7-206">Next steps</span></span>
* <span data-ttu-id="183c7-207">[Collecter les journaux et les indicateurs de performance des services Azure](log-analytics-azure-storage.md) pour les services pris en charge par Azure.</span><span class="sxs-lookup"><span data-stu-id="183c7-207">[Collect logs and metrics for Azure services](log-analytics-azure-storage.md) for supported Azure services.</span></span>
* <span data-ttu-id="183c7-208">[Activer des Solutions](log-analytics-add-solutions.md) tooprovide comprendre les données de hello.</span><span class="sxs-lookup"><span data-stu-id="183c7-208">[Enable Solutions](log-analytics-add-solutions.md) tooprovide insight into hello data.</span></span>
* <span data-ttu-id="183c7-209">[Utiliser des requêtes de recherche](log-analytics-log-searches.md) tooanalyze les données de salutation.</span><span class="sxs-lookup"><span data-stu-id="183c7-209">[Use search queries](log-analytics-log-searches.md) tooanalyze hello data.</span></span>
