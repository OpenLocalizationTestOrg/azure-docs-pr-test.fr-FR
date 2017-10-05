---
title: "Utilisation d’un Stockage Blob pour IIS et d’un Stockage Table pour les événements dans Azure Log Analytics | Microsoft Docs"
description: "Log Analytics peut lire les journaux pour des services Azure qui écrivent des diagnostics dans un Stockage Table ou des journaux IIS écrits dans un Stockage Blob."
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
ms.openlocfilehash: 459ef90ca1d76bada6565bfefd7b4bd1086197d5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-blob-storage-for-iis-and-azure-table-storage-for-events-with-log-analytics"></a><span data-ttu-id="b7c54-103">Utilisation d’un Stockage Blob Azure pour IIS et d’un Stockage Table Azure pour les événements avec Log Analytics</span><span class="sxs-lookup"><span data-stu-id="b7c54-103">Use Azure blob storage for IIS and Azure table storage for events with Log Analytics</span></span>

<span data-ttu-id="b7c54-104">Log Analytics peut lire les journaux pour des services suivants qui écrivent des diagnostics dans un Stockage Table ou des journaux IIS écrits dans un Stockage Blob :</span><span class="sxs-lookup"><span data-stu-id="b7c54-104">Log Analytics can read the logs for the following services that write diagnostics to table storage or IIS logs written to blob storage:</span></span>

* <span data-ttu-id="b7c54-105">Clusters Service Fabric (version préliminaire)</span><span class="sxs-lookup"><span data-stu-id="b7c54-105">Service Fabric clusters (Preview)</span></span>
* <span data-ttu-id="b7c54-106">Machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="b7c54-106">Virtual Machines</span></span>
* <span data-ttu-id="b7c54-107">Rôle de travail/web</span><span class="sxs-lookup"><span data-stu-id="b7c54-107">Web/Worker Roles</span></span>

<span data-ttu-id="b7c54-108">Pour que Log Analytics puisse collecter les données pour ces ressources, les diagnostics Azure doivent être activés.</span><span class="sxs-lookup"><span data-stu-id="b7c54-108">Before Log Analytics can collect data for these resources, Azure diagnostics must be enabled.</span></span>

<span data-ttu-id="b7c54-109">Une fois les diagnostics activés, vous pouvez utiliser le portail Azure ou PowerShell pour configurer Log Analytics afin de collecter les journaux.</span><span class="sxs-lookup"><span data-stu-id="b7c54-109">Once diagnostics are enabled, you can use the Azure portal or PowerShell configure Log Analytics to collect the logs.</span></span>

<span data-ttu-id="b7c54-110">Les diagnostics Azure sont une extension vous permettant de collecter des données de diagnostic à partir d’un rôle de travail, d’un rôle Web ou d’une machine virtuelle exécuté dans Azure.</span><span class="sxs-lookup"><span data-stu-id="b7c54-110">Azure Diagnostics is an Azure extension that enables you to collect diagnostic data from a worker role, web role, or virtual machine running in Azure.</span></span> <span data-ttu-id="b7c54-111">Les données sont stockées dans un compte de stockage Azure à partir duquel Log Analytics peut les collecter.</span><span class="sxs-lookup"><span data-stu-id="b7c54-111">The data is stored in an Azure storage account and can then be collected by Log Analytics.</span></span>

<span data-ttu-id="b7c54-112">Pour que Log Analytics collecte ces journaux de diagnostics Azure, ceux-ci doivent être dans les emplacements suivants :</span><span class="sxs-lookup"><span data-stu-id="b7c54-112">For Log Analytics to collect these Azure Diagnostics logs, the logs must be in the following locations:</span></span>

| <span data-ttu-id="b7c54-113">Type de journal</span><span class="sxs-lookup"><span data-stu-id="b7c54-113">Log Type</span></span> | <span data-ttu-id="b7c54-114">Type de ressource</span><span class="sxs-lookup"><span data-stu-id="b7c54-114">Resource Type</span></span> | <span data-ttu-id="b7c54-115">Lieu</span><span class="sxs-lookup"><span data-stu-id="b7c54-115">Location</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b7c54-116">Journaux IIS</span><span class="sxs-lookup"><span data-stu-id="b7c54-116">IIS logs</span></span> |<span data-ttu-id="b7c54-117">Machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="b7c54-117">Virtual Machines</span></span> <br> <span data-ttu-id="b7c54-118">Rôles web</span><span class="sxs-lookup"><span data-stu-id="b7c54-118">Web roles</span></span> <br> <span data-ttu-id="b7c54-119">Rôles de travail</span><span class="sxs-lookup"><span data-stu-id="b7c54-119">Worker roles</span></span> |<span data-ttu-id="b7c54-120">wad-iis-logfiles (Stockage Blob)</span><span class="sxs-lookup"><span data-stu-id="b7c54-120">wad-iis-logfiles (Blob Storage)</span></span> |
| <span data-ttu-id="b7c54-121">syslog</span><span class="sxs-lookup"><span data-stu-id="b7c54-121">Syslog</span></span> |<span data-ttu-id="b7c54-122">Machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="b7c54-122">Virtual Machines</span></span> |<span data-ttu-id="b7c54-123">LinuxSyslogVer2v0 (Stockage Table)</span><span class="sxs-lookup"><span data-stu-id="b7c54-123">LinuxsyslogVer2v0 (Table Storage)</span></span> |
| <span data-ttu-id="b7c54-124">Événements opérationnels Service Fabric</span><span class="sxs-lookup"><span data-stu-id="b7c54-124">Service Fabric Operational Events</span></span> |<span data-ttu-id="b7c54-125">Nœuds Service Fabric</span><span class="sxs-lookup"><span data-stu-id="b7c54-125">Service Fabric nodes</span></span> |<span data-ttu-id="b7c54-126">WADServiceFabricSystemEventTable</span><span class="sxs-lookup"><span data-stu-id="b7c54-126">WADServiceFabricSystemEventTable</span></span> |
| <span data-ttu-id="b7c54-127">Événements Reliable Actor Service Fabric</span><span class="sxs-lookup"><span data-stu-id="b7c54-127">Service Fabric Reliable Actor Events</span></span> |<span data-ttu-id="b7c54-128">Nœuds Service Fabric</span><span class="sxs-lookup"><span data-stu-id="b7c54-128">Service Fabric nodes</span></span> |<span data-ttu-id="b7c54-129">WADServiceFabricReliableActorEventTable</span><span class="sxs-lookup"><span data-stu-id="b7c54-129">WADServiceFabricReliableActorEventTable</span></span> |
| <span data-ttu-id="b7c54-130">Événements de service fiable Service Fabric</span><span class="sxs-lookup"><span data-stu-id="b7c54-130">Service Fabric Reliable Service Events</span></span> |<span data-ttu-id="b7c54-131">Nœuds Service Fabric</span><span class="sxs-lookup"><span data-stu-id="b7c54-131">Service Fabric nodes</span></span> |<span data-ttu-id="b7c54-132">WADServiceFabricReliableServiceEventTable</span><span class="sxs-lookup"><span data-stu-id="b7c54-132">WADServiceFabricReliableServiceEventTable</span></span> |
| <span data-ttu-id="b7c54-133">Journaux d'événements Windows</span><span class="sxs-lookup"><span data-stu-id="b7c54-133">Windows Event logs</span></span> |<span data-ttu-id="b7c54-134">Nœuds Service Fabric</span><span class="sxs-lookup"><span data-stu-id="b7c54-134">Service Fabric nodes</span></span> <br> <span data-ttu-id="b7c54-135">Machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="b7c54-135">Virtual Machines</span></span> <br> <span data-ttu-id="b7c54-136">Rôles web</span><span class="sxs-lookup"><span data-stu-id="b7c54-136">Web roles</span></span> <br> <span data-ttu-id="b7c54-137">Rôles de travail</span><span class="sxs-lookup"><span data-stu-id="b7c54-137">Worker roles</span></span> |<span data-ttu-id="b7c54-138">WADWindowsEventLogsTable (Stockage Table)</span><span class="sxs-lookup"><span data-stu-id="b7c54-138">WADWindowsEventLogsTable (Table Storage)</span></span> |
| <span data-ttu-id="b7c54-139">Journaux de suivi des événements ETW Windows</span><span class="sxs-lookup"><span data-stu-id="b7c54-139">Windows ETW logs</span></span> |<span data-ttu-id="b7c54-140">Nœuds Service Fabric</span><span class="sxs-lookup"><span data-stu-id="b7c54-140">Service Fabric nodes</span></span> <br> <span data-ttu-id="b7c54-141">Machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="b7c54-141">Virtual Machines</span></span> <br> <span data-ttu-id="b7c54-142">Rôles web</span><span class="sxs-lookup"><span data-stu-id="b7c54-142">Web roles</span></span> <br> <span data-ttu-id="b7c54-143">Rôles de travail</span><span class="sxs-lookup"><span data-stu-id="b7c54-143">Worker roles</span></span> |<span data-ttu-id="b7c54-144">WADETWEventTable (Stockage Table)</span><span class="sxs-lookup"><span data-stu-id="b7c54-144">WADETWEventTable (Table Storage)</span></span> |

> [!NOTE]
> <span data-ttu-id="b7c54-145">Les journaux IIS des sites Web Azure ne sont actuellement pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="b7c54-145">IIS logs from Azure Websites are not currently supported.</span></span>
>
>

<span data-ttu-id="b7c54-146">Pour les machines virtuelles, vous pouvez installer [l’agent Log Analytics](log-analytics-azure-vm-extension.md) sur votre machine virtuelle pour activer des informations supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="b7c54-146">For virtual machines, you have the option of installing the [Log Analytics agent](log-analytics-azure-vm-extension.md) into your virtual machine to enable additional insights.</span></span> <span data-ttu-id="b7c54-147">Cela vous permet d’analyser les journaux IIS et les journaux des événements, mais également d'effectuer des analyses supplémentaires, notamment le suivi des modifications de configuration, l’évaluation SQL et l’évaluation de la mise à jour.</span><span class="sxs-lookup"><span data-stu-id="b7c54-147">In addition to being able to analyze IIS logs and Event Logs, you can perform additional analysis including configuration change tracking, SQL assessment, and update assessment.</span></span>

## <a name="enable-azure-diagnostics-in-a-virtual-machine-for-event-log-and-iis-log-collection"></a><span data-ttu-id="b7c54-148">Activation des diagnostics Azure dans une machine virtuelle pour la collecte des journaux IIS et des journaux des événements</span><span class="sxs-lookup"><span data-stu-id="b7c54-148">Enable Azure diagnostics in a virtual machine for event log and IIS log collection</span></span>
<span data-ttu-id="b7c54-149">Utilisez la procédure suivante pour activer les diagnostics Azure dans une machine virtuelle pour la collecte de journaux IIS et de journaux des événements à l’aide du portail Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="b7c54-149">Use the following procedure to enable Azure diagnostics in a virtual machine for Event Log and IIS log collection using the Microsoft Azure portal.</span></span>

### <a name="to-enable-azure-diagnostics-in-a-virtual-machine-with-the-azure-portal"></a><span data-ttu-id="b7c54-150">Activation des diagnostics Azure dans une machine virtuelle à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="b7c54-150">To enable Azure diagnostics in a virtual machine with the Azure portal</span></span>
1. <span data-ttu-id="b7c54-151">Installez l’agent de machine virtuelle lorsque vous créez une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="b7c54-151">Install the VM Agent when you create a virtual machine.</span></span> <span data-ttu-id="b7c54-152">Si la machine virtuelle existe déjà, vérifiez que l’agent de machine virtuelle est déjà installé.</span><span class="sxs-lookup"><span data-stu-id="b7c54-152">If the virtual machine already exists, verify that the VM Agent is already installed.</span></span>

   * <span data-ttu-id="b7c54-153">Dans le portail Azure, accédez à la machine virtuelle, sélectionnez **Configuration facultative**, puis **Diagnostics**, et définissez **État** sur **Activé**.</span><span class="sxs-lookup"><span data-stu-id="b7c54-153">In the Azure portal, navigate to the virtual machine, select **Optional Configuration**, then **Diagnostics** and set **Status** to **On**.</span></span>

     <span data-ttu-id="b7c54-154">Une fois cela terminé, la machine virtuelle a l’extension Azure Diagnostics installée et en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="b7c54-154">Upon completion, the VM has the Azure Diagnostics extension installed and running.</span></span> <span data-ttu-id="b7c54-155">Cette extension est chargée de collecter vos données de diagnostic.</span><span class="sxs-lookup"><span data-stu-id="b7c54-155">This extension is responsible for collecting your diagnostics data.</span></span>
2. <span data-ttu-id="b7c54-156">Activation de l’analyse et configuration de la journalisation des événements sur une machine virtuelle existante.</span><span class="sxs-lookup"><span data-stu-id="b7c54-156">Enable monitoring and configure event logging on an existing VM.</span></span> <span data-ttu-id="b7c54-157">Vous pouvez activer les diagnostics au niveau de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="b7c54-157">You can enable diagnostics at the VM level.</span></span> <span data-ttu-id="b7c54-158">Pour activer les diagnostics et configurer la journalisation des événements par la suite, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="b7c54-158">To enable diagnostics and then configure event logging, perform the following steps:</span></span>

   1. <span data-ttu-id="b7c54-159">Sélectionnez la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="b7c54-159">Select the VM.</span></span>
   2. <span data-ttu-id="b7c54-160">Cliquez sur **Analyse**.</span><span class="sxs-lookup"><span data-stu-id="b7c54-160">Click **Monitoring**.</span></span>
   3. <span data-ttu-id="b7c54-161">Cliquez sur **Diagnostics**.</span><span class="sxs-lookup"><span data-stu-id="b7c54-161">Click **Diagnostics**.</span></span>
   4. <span data-ttu-id="b7c54-162">Définissez **État** sur **ACTIVÉ**.</span><span class="sxs-lookup"><span data-stu-id="b7c54-162">Set the **Status** to **ON**.</span></span>
   5. <span data-ttu-id="b7c54-163">Cliquez sur les métriques de diagnostic que vous souhaitez utiliser.</span><span class="sxs-lookup"><span data-stu-id="b7c54-163">Select each diagnostics log that you want to collect.</span></span>
   6. <span data-ttu-id="b7c54-164">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="b7c54-164">Click **OK**.</span></span>

## <a name="enable-azure-diagnostics-in-a-web-role-for-iis-log-and-event-collection"></a><span data-ttu-id="b7c54-165">Activation des diagnostics Azure dans un rôle Web pour la collecte de journaux IIS et des événements</span><span class="sxs-lookup"><span data-stu-id="b7c54-165">Enable Azure diagnostics in a Web role for IIS log and event collection</span></span>
<span data-ttu-id="b7c54-166">Reportez-vous à [Procédure : activer les diagnostics dans un service cloud](../cloud-services/cloud-services-dotnet-diagnostics.md) pour connaître les étapes générales d’activation des diagnostics Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="b7c54-166">Refer to [How To Enable Diagnostics in a Cloud Service](../cloud-services/cloud-services-dotnet-diagnostics.md) for general steps on enabling Azure diagnostics.</span></span> <span data-ttu-id="b7c54-167">Les instructions ci-dessous utilisent ces informations et les personnalisent pour une utilisation avec Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="b7c54-167">The instructions below use this information and customize it for use with Log Analytics.</span></span>

<span data-ttu-id="b7c54-168">Avec les diagnostics Azure activés :</span><span class="sxs-lookup"><span data-stu-id="b7c54-168">With Azure diagnostics enabled:</span></span>

* <span data-ttu-id="b7c54-169">Les journaux IIS sont stockés par défaut et les données de journal sont transférées selon l’intervalle de transfert scheduledTransferPeriod.</span><span class="sxs-lookup"><span data-stu-id="b7c54-169">IIS logs are stored by default, with log data transferred at the scheduledTransferPeriod transfer interval.</span></span>
* <span data-ttu-id="b7c54-170">Les journaux des événements Windows ne sont pas transférés par défaut.</span><span class="sxs-lookup"><span data-stu-id="b7c54-170">Windows Event Logs are not transferred by default.</span></span>

### <a name="to-enable-diagnostics"></a><span data-ttu-id="b7c54-171">Activation des diagnostics</span><span class="sxs-lookup"><span data-stu-id="b7c54-171">To enable diagnostics</span></span>
<span data-ttu-id="b7c54-172">Pour activer les journaux des événements Windows, ou pour modifier l’intervalle scheduledTransferPeriod, configurez Azure Diagnostics à l’aide du fichier de configuration XML (diagnostics.wadcfg), comme indiqué dans [Étape 4 : création de votre fichier de configuration Diagnostics et installation de l’extension](../cloud-services/cloud-services-dotnet-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="b7c54-172">To enable Windows Event Logs, or to change the scheduledTransferPeriod, configure Azure Diagnostics using the XML configuration file (diagnostics.wadcfg), as shown in [Step 4: Create your Diagnostics configuration file and install the extension](../cloud-services/cloud-services-dotnet-diagnostics.md)</span></span>

<span data-ttu-id="b7c54-173">L’exemple de fichier de configuration suivant collecte des journaux IIS et tous les événements des journaux de l’application et du système :</span><span class="sxs-lookup"><span data-stu-id="b7c54-173">The following example configuration file collects IIS Logs and all Events from the Application and System logs:</span></span>

```
    <?xml version="1.0" encoding="utf-8" ?>
    <DiagnosticMonitorConfiguration xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration"
          configurationChangePollInterval="PT1M"
          overallQuotaInMB="4096">

      <Directories bufferQuotaInMB="0"
         scheduledTransferPeriod="PT10M">  
        <!-- IISLogs are only relevant to Web roles -->
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

<span data-ttu-id="b7c54-174">Assurez-vous que votre paramètres ConfigurationSettings spécifient un compte de stockage, comme dans l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="b7c54-174">Ensure that your ConfigurationSettings specifies a storage account, as in the following example:</span></span>

```
    <ConfigurationSettings>
       <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="DefaultEndpointsProtocol=https;AccountName=<AccountName>;AccountKey=<AccountKey>"/>
    </ConfigurationSettings>
```

<span data-ttu-id="b7c54-175">Les valeurs **AccountName** et **AccountKey** figurent dans le portail Azure, sur le tableau de bord du compte de stockage, sous Gérer les clés d’accès.</span><span class="sxs-lookup"><span data-stu-id="b7c54-175">The **AccountName** and **AccountKey** values are found in the Azure portal in the storage account dashboard, under Manage Access Keys.</span></span> <span data-ttu-id="b7c54-176">Le protocole de la chaîne de connexion doit être **https**.</span><span class="sxs-lookup"><span data-stu-id="b7c54-176">The protocol for the connection string must be **https**.</span></span>

<span data-ttu-id="b7c54-177">Une fois que la configuration de diagnostic mise à jour est appliquée à votre service cloud et écrit des diagnostics dans Stockage Azure, vous êtes prêt à configurer Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="b7c54-177">Once the updated diagnostic configuration is applied to your cloud service and it is writing diagnostics to Azure Storage, then you are ready to configure Log Analytics.</span></span>

## <a name="use-the-azure-portal-to-collect-logs-from-azure-storage"></a><span data-ttu-id="b7c54-178">Utiliser le portail Azure pour collecter les journaux à partir de Stockage Azure</span><span class="sxs-lookup"><span data-stu-id="b7c54-178">Use the Azure portal to collect logs from Azure Storage</span></span>
<span data-ttu-id="b7c54-179">Vous pouvez utiliser le portail Azure pour configurer Log Analytics afin de collecter les journaux pour les services Azure suivants :</span><span class="sxs-lookup"><span data-stu-id="b7c54-179">You can use the Azure portal to configure Log Analytics to collect the logs for the following Azure services:</span></span>

* <span data-ttu-id="b7c54-180">Clusters Service Fabric</span><span class="sxs-lookup"><span data-stu-id="b7c54-180">Service Fabric clusters</span></span>
* <span data-ttu-id="b7c54-181">Machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="b7c54-181">Virtual Machines</span></span>
* <span data-ttu-id="b7c54-182">Rôle de travail/web</span><span class="sxs-lookup"><span data-stu-id="b7c54-182">Web/Worker Roles</span></span>

<span data-ttu-id="b7c54-183">Dans le portail Azure, accédez à votre espace de travail Log Analytics, puis effectuer les tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="b7c54-183">In the Azure portal, navigate to your Log Analytics workspace and perform the following tasks:</span></span>

1. <span data-ttu-id="b7c54-184">Cliquez sur *Journaux des comptes de stockage*.</span><span class="sxs-lookup"><span data-stu-id="b7c54-184">Click *Storage accounts logs*</span></span>
2. <span data-ttu-id="b7c54-185">Cliquez sur la tâche *Ajouter*.</span><span class="sxs-lookup"><span data-stu-id="b7c54-185">Click the *Add* task</span></span>
3. <span data-ttu-id="b7c54-186">Sélectionnez le compte de stockage contenant les journaux de diagnostic.</span><span class="sxs-lookup"><span data-stu-id="b7c54-186">Select the Storage account that contains the diagnostics logs</span></span>
   * <span data-ttu-id="b7c54-187">Ce compte peut être un compte de stockage classique ou un compte de stockage Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b7c54-187">This account can be either a classic storage account or an Azure Resource Manager storage account</span></span>
4. <span data-ttu-id="b7c54-188">Sélectionnez le Type de données pour lequel vous souhaitez collecter des journaux.</span><span class="sxs-lookup"><span data-stu-id="b7c54-188">Select the Data Type you want to collect logs for</span></span>
   * <span data-ttu-id="b7c54-189">Les choix sont Journaux IIS, Événements, Syslog (Linux), Journaux de suivi des événements ETW, Événements Service Fabric</span><span class="sxs-lookup"><span data-stu-id="b7c54-189">The choices are IIS Logs; Events; Syslog (Linux); ETW Logs; Service Fabric Events</span></span>
5. <span data-ttu-id="b7c54-190">La valeur de Source est automatiquement complétée selon le type de données, et ne peut pas être modifiée</span><span class="sxs-lookup"><span data-stu-id="b7c54-190">The value for Source is automatically populated based on the data type and cannot be changed</span></span>
6. <span data-ttu-id="b7c54-191">Cliquez sur OK pour enregistrer la configuration.</span><span class="sxs-lookup"><span data-stu-id="b7c54-191">Click OK to save the configuration</span></span>

<span data-ttu-id="b7c54-192">Répétez les étapes 2 à 6 pour les autres comptes de stockage et types de données que Log Analytics doit collecter.</span><span class="sxs-lookup"><span data-stu-id="b7c54-192">Repeat steps 2-6 for additional storage accounts and data types that you want Log Analytics to collect.</span></span>

<span data-ttu-id="b7c54-193">Après environ 30 minutes, vous pourrez voir les données du compte de stockage dans Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="b7c54-193">In approximately 30 minutes, you are able to see data from the storage account in Log Analytics.</span></span> <span data-ttu-id="b7c54-194">Vous voyez les données écrites dans le stockage uniquement après application de la configuration.</span><span class="sxs-lookup"><span data-stu-id="b7c54-194">You will only see data that is written to storage after the configuration is applied.</span></span> <span data-ttu-id="b7c54-195">Log Analytics ne lit pas les données préexistantes du compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="b7c54-195">Log Analytics does not read the pre-existing data from the storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="b7c54-196">Le portail ne valide pas l’existence de la Source dans le compte de stockage ou le fait que de nouvelles données sont écrites.</span><span class="sxs-lookup"><span data-stu-id="b7c54-196">The portal does not validate that the Source exists in the storage account or if new data is being written.</span></span>
>
>

## <a name="enable-azure-diagnostics-in-a-virtual-machine-for-event-log-and-iis-log-collection-using-powershell"></a><span data-ttu-id="b7c54-197">Activer les diagnostics Azure dans une machine virtuelle pour la collecte des journaux IIS et des journaux des événements avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="b7c54-197">Enable Azure diagnostics in a virtual machine for event log and IIS log collection using PowerShell</span></span>
<span data-ttu-id="b7c54-198">Utilisez les étapes de [Configuration de Log Analytics pour indexer les diagnostics Azure](log-analytics-powershell-workspace-configuration.md#configuring-log-analytics-to-index-azure-diagnostics) pour utiliser PowerShell afin de lire à partir des diagnostics Azure écrits dans le stockage de table.</span><span class="sxs-lookup"><span data-stu-id="b7c54-198">Use the steps in [Configuring Log Analytics to index Azure diagnostics](log-analytics-powershell-workspace-configuration.md#configuring-log-analytics-to-index-azure-diagnostics) to use PowerShell to read from Azure diagnostics that are written to table storage.</span></span>

<span data-ttu-id="b7c54-199">Vous pouvez spécifier les événements écrits dans Azure Storage plus précisément à l’aide d’Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b7c54-199">Using Azure PowerShell you can more precisely specify the events that are written to Azure Storage.</span></span>
<span data-ttu-id="b7c54-200">Pour plus d'informations, consultez la page [Activation des diagnostics dans les machines virtuelles Azure](../virtual-machines-dotnet-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="b7c54-200">For more information, see [Enabling Diagnostics in Azure Virtual Machines](../virtual-machines-dotnet-diagnostics.md).</span></span>

<span data-ttu-id="b7c54-201">Vous pouvez activer et mettre à jour les diagnostics Azure en utilisant le script PowerShell suivant.</span><span class="sxs-lookup"><span data-stu-id="b7c54-201">You can enable and update Azure diagnostics using the following PowerShell script.</span></span>
<span data-ttu-id="b7c54-202">Vous pouvez également utiliser ce script avec une configuration de journalisation personnalisée.</span><span class="sxs-lookup"><span data-stu-id="b7c54-202">You can also use this script with a custom logging configuration.</span></span>
<span data-ttu-id="b7c54-203">Modifiez le script pour définir le compte de stockage, le nom du service et le nom de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="b7c54-203">Modify the script to set the storage account, service name, and virtual machine name.</span></span>
<span data-ttu-id="b7c54-204">Le script utilise des applets de commande pour les machines virtuelles classiques.</span><span class="sxs-lookup"><span data-stu-id="b7c54-204">The script uses cmdlets for classic virtual machines.</span></span>

<span data-ttu-id="b7c54-205">Examinez l’exemple de script suivant, copiez-le et modifiez-le si nécessaire, enregistrez l’exemple dans un fichier de script PowerShell, puis exécutez le script.</span><span class="sxs-lookup"><span data-stu-id="b7c54-205">Review the following script sample, copy it, modify it as needed, save the sample as a PowerShell script file, and then run the script.</span></span>

```
    #Connect to Azure
    Add-AzureAccount

    # settings to change:
    $wad_storage_account_name = "myStorageAccount"
    $service_name = "myService"
    $vm_name = "myVM"

    #Construct Azure Diagnostics public config and convert to config format

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
    $wad_version = (Get-AzureVMAvailableExtension -Publisher $wad_publisher -ExtensionName $wad_extension_name).Version # Gets latest version of the extension

    (Get-AzureVM -ServiceName $service_name -Name $vm_name) | Set-AzureVMExtension -ExtensionName $wad_extension_name -Publisher $wad_publisher -PublicConfiguration $wad_public_config -PrivateConfiguration $wad_private_config -Version $wad_version | Update-AzureVM
```


## <a name="next-steps"></a><span data-ttu-id="b7c54-206">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b7c54-206">Next steps</span></span>
* <span data-ttu-id="b7c54-207">[Collecter les journaux et les indicateurs de performance des services Azure](log-analytics-azure-storage.md) pour les services pris en charge par Azure.</span><span class="sxs-lookup"><span data-stu-id="b7c54-207">[Collect logs and metrics for Azure services](log-analytics-azure-storage.md) for supported Azure services.</span></span>
* <span data-ttu-id="b7c54-208">[Activer les solutions](log-analytics-add-solutions.md) pour fournir des informations sur les données.</span><span class="sxs-lookup"><span data-stu-id="b7c54-208">[Enable Solutions](log-analytics-add-solutions.md) to provide insight into the data.</span></span>
* <span data-ttu-id="b7c54-209">[Utiliser les requêtes de recherche](log-analytics-log-searches.md) pour analyser les données.</span><span class="sxs-lookup"><span data-stu-id="b7c54-209">[Use search queries](log-analytics-log-searches.md) to analyze the data.</span></span>
