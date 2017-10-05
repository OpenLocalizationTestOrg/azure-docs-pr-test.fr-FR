---
title: "Schéma de configuration Azure Diagnostics 1.0 | Microsoft Docs"
description: "Applicable UNIQUEMENT si vous utilisez le Kit de développement logiciel (SDK) Azure 2.4 et les versions antérieures avec Azure Virtual Machines, Virtual Machine Scale Sets, Service Fabric ou Cloud Services."
services: monitoring-and-diagnostics
documentationcenter: .net
author: rboucher
manager: carmonm
editor: 
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/15/2017
ms.author: robb
ms.openlocfilehash: a8fdfb52d5091d3fc9779657737c7430fcfada51
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-diagnostics-10-configuration-schema"></a><span data-ttu-id="58737-103">Schéma de configuration Azure Diagnostics 1.0</span><span class="sxs-lookup"><span data-stu-id="58737-103">Azure Diagnostics 1.0 Configuration Schema</span></span>
> [!NOTE]
> <span data-ttu-id="58737-104">Azure Diagnostics est le composant utilisé pour collecter les compteurs de performances et d’autres statistiques d’Azure Virtual Machines, de Virtual Machine Scale Sets, de Service Fabric et de Cloud Services.</span><span class="sxs-lookup"><span data-stu-id="58737-104">Azure Diagnostics is the component used to collect performance counters and other statistics from Azure Virtual Machines, Virtual Machine Scale Sets, Service Fabric, and Cloud Services.</span></span>  <span data-ttu-id="58737-105">Cette page vous concerne uniquement si vous utilisez l’un de ces services.</span><span class="sxs-lookup"><span data-stu-id="58737-105">This page is only relevant if you are using one of these services.</span></span>
>

<span data-ttu-id="58737-106">Azure Diagnostics est utilisé avec d’autres produits de diagnostic Microsoft tels que Azure Monitor, Application Insights et Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="58737-106">Azure Diagnostics is used with other Microsoft diagnostics products like Azure Monitor, Application Insights, and Log Analytics.</span></span>

<span data-ttu-id="58737-107">Le fichier de configuration Azure Diagnostics définit les valeurs qui sont utilisées pour initialiser le moniteur de diagnostics.</span><span class="sxs-lookup"><span data-stu-id="58737-107">The Azure Diagnostics configuration file defines values that are used to initialize the Diagnostics Monitor.</span></span> <span data-ttu-id="58737-108">Ce fichier est utilisé pour initialiser les paramètres de configuration de diagnostic lorsque le moniteur de diagnostic démarre.</span><span class="sxs-lookup"><span data-stu-id="58737-108">This file is used to initialize diagnostic configuration settings when the diagnostics monitor starts.</span></span>  

 <span data-ttu-id="58737-109">Par défaut, le fichier de schéma de configuration Azure Diagnostics est installé dans le répertoire `C:\Program Files\Microsoft SDKs\Azure\.NET SDK\<version>\schemas`.</span><span class="sxs-lookup"><span data-stu-id="58737-109">By default, the Azure Diagnostics configuration schema file is installed to the `C:\Program Files\Microsoft SDKs\Azure\.NET SDK\<version>\schemas` directory.</span></span> <span data-ttu-id="58737-110">Remplacez `<version>` par la version installée du [Kit de développement logiciel (SDK) Azure](http://www.windowsazure.com/develop/downloads/).</span><span class="sxs-lookup"><span data-stu-id="58737-110">Replace `<version>` with the installed version of the [Azure SDK](http://www.windowsazure.com/develop/downloads/).</span></span>  

> [!NOTE]
>  <span data-ttu-id="58737-111">Le fichier de configuration de diagnostic est généralement utilisé avec les tâches de démarrage qui requièrent la collecte de données de diagnostic au début du processus de démarrage.</span><span class="sxs-lookup"><span data-stu-id="58737-111">The diagnostics configuration file is typically used with startup tasks that require diagnostic data to be collected earlier in the startup process.</span></span> <span data-ttu-id="58737-112">Pour plus d’informations sur l’utilisation d’Azure Diagnostics, consultez [Collect Logging Data by Using Azure Diagnostics](assetId:///83a91c23-5ca2-4fc9-8df3-62036c37a3d7) (Collecte de données de journalisation à l’aide d’Azure Diagnostics).</span><span class="sxs-lookup"><span data-stu-id="58737-112">For more information about using Azure Diagnostics, see [Collect Logging Data by Using Azure Diagnostics](assetId:///83a91c23-5ca2-4fc9-8df3-62036c37a3d7).</span></span>  

## <a name="example-of-the-diagnostics-configuration-file"></a><span data-ttu-id="58737-113">Exemple du fichier de configuration des diagnostics</span><span class="sxs-lookup"><span data-stu-id="58737-113">Example of the diagnostics configuration file</span></span>  
 <span data-ttu-id="58737-114">L’exemple suivant montre un fichier de configuration de diagnostic standard :</span><span class="sxs-lookup"><span data-stu-id="58737-114">The following example shows a typical diagnostics configuration file:</span></span>  

```xml  
<?xml version="1.0" encoding="utf-8"?>
<DiagnosticMonitorConfiguration xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration"  
      configurationChangePollInterval="PT1M"  
      overallQuotaInMB="4096">  
   <DiagnosticInfrastructureLogs bufferQuotaInMB="1024"  
      scheduledTransferLogLevelFilter="Verbose"  
      scheduledTransferPeriod="PT1M" />  
   <Logs bufferQuotaInMB="1024"  
      scheduledTransferLogLevelFilter="Verbose"  
      scheduledTransferPeriod="PT1M" />  

   <Directories bufferQuotaInMB="1024"   
      scheduledTransferPeriod="PT1M">  

      <!-- These three elements specify the special directories   
           that are set up for the log types -->  
      <CrashDumps container="wad-crash-dumps" directoryQuotaInMB="256" />  
      <FailedRequestLogs container="wad-frq" directoryQuotaInMB="256" />  
      <IISLogs container="wad-iis" directoryQuotaInMB="256" />  

      <!-- For regular directories the DataSources element is used -->  
      <DataSources>  
         <DirectoryConfiguration container="wad-panther" directoryQuotaInMB="128">  
            <!-- Absolute specifies an absolute path with optional environment expansion -->  
            <Absolute expandEnvironment="true" path="%SystemRoot%\system32\sysprep\Panther" />  
         </DirectoryConfiguration>  
         <DirectoryConfiguration container="wad-custom" directoryQuotaInMB="128">  
            <!-- LocalResource specifies a path relative to a local   
                 resource defined in the service definition -->  
            <LocalResource name="MyLoggingLocalResource" relativePath="logs" />  
         </DirectoryConfiguration>  
      </DataSources>  
   </Directories>  

   <PerformanceCounters bufferQuotaInMB="512" scheduledTransferPeriod="PT1M">  
      <!-- The counter specifier is in the same format as the imperative   
           diagnostics configuration API -->  
      <PerformanceCounterConfiguration   
         counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT5S" />  
   </PerformanceCounters>  

   <WindowsEventLog bufferQuotaInMB="512"  
      scheduledTransferLogLevelFilter="Verbose"  
      scheduledTransferPeriod="PT1M">  
      <!-- The event log name is in the same format as the imperative   
           diagnostics configuration API -->  
      <DataSource name="System!*" />  
   </WindowsEventLog>  
</DiagnosticMonitorConfiguration>  
```  

## <a name="diagnosticsconfiguration-namespace"></a><span data-ttu-id="58737-115">Espace de noms DiagnosticsConfiguration</span><span class="sxs-lookup"><span data-stu-id="58737-115">DiagnosticsConfiguration Namespace</span></span>  
 <span data-ttu-id="58737-116">L’espace de noms XML du fichier de configuration des diagnostics est :</span><span class="sxs-lookup"><span data-stu-id="58737-116">The XML namespace for the diagnostics configuration file is:</span></span>  

```  
http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration  
```  

## <a name="schema-elements"></a><span data-ttu-id="58737-117">Éléments du schéma</span><span class="sxs-lookup"><span data-stu-id="58737-117">Schema Elements</span></span>  
 <span data-ttu-id="58737-118">Le fichier de configuration de diagnostic inclut les éléments suivants.</span><span class="sxs-lookup"><span data-stu-id="58737-118">The diagnostics configuration file includes the following elements.</span></span>


## <a name="diagnosticmonitorconfiguration-element"></a><span data-ttu-id="58737-119">Élément DiagnosticMonitorConfiguration</span><span class="sxs-lookup"><span data-stu-id="58737-119">DiagnosticMonitorConfiguration Element</span></span>  
<span data-ttu-id="58737-120">Élément de niveau supérieur du fichier de configuration de diagnostic.</span><span class="sxs-lookup"><span data-stu-id="58737-120">The top-level element of the diagnostics configuration file.</span></span>  

<span data-ttu-id="58737-121">Attributs :</span><span class="sxs-lookup"><span data-stu-id="58737-121">Attributes:</span></span>

|<span data-ttu-id="58737-122">Attribut</span><span class="sxs-lookup"><span data-stu-id="58737-122">Attribute</span></span>  |<span data-ttu-id="58737-123">Type</span><span class="sxs-lookup"><span data-stu-id="58737-123">Type</span></span>   |<span data-ttu-id="58737-124">Requis</span><span class="sxs-lookup"><span data-stu-id="58737-124">Required</span></span>| <span data-ttu-id="58737-125">Default</span><span class="sxs-lookup"><span data-stu-id="58737-125">Default</span></span> | <span data-ttu-id="58737-126">Description</span><span class="sxs-lookup"><span data-stu-id="58737-126">Description</span></span>|  
|-----------|-------|--------|---------|------------|  
|<span data-ttu-id="58737-127">**configurationChangePollInterval**</span><span class="sxs-lookup"><span data-stu-id="58737-127">**configurationChangePollInterval**</span></span>|<span data-ttu-id="58737-128">duration</span><span class="sxs-lookup"><span data-stu-id="58737-128">duration</span></span>|<span data-ttu-id="58737-129">Facultatif</span><span class="sxs-lookup"><span data-stu-id="58737-129">Optional</span></span> | <span data-ttu-id="58737-130">PT1M</span><span class="sxs-lookup"><span data-stu-id="58737-130">PT1M</span></span>| <span data-ttu-id="58737-131">Spécifie l’intervalle auquel le moniteur de diagnostic s’enquiert des modifications de configuration de diagnostic.</span><span class="sxs-lookup"><span data-stu-id="58737-131">Specifies the interval at which the diagnostic monitor polls for diagnostic configuration changes.</span></span>|  
|<span data-ttu-id="58737-132">**overallQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="58737-132">**overallQuotaInMB**</span></span>|<span data-ttu-id="58737-133">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="58737-133">unsignedInt</span></span>|<span data-ttu-id="58737-134">Facultatif</span><span class="sxs-lookup"><span data-stu-id="58737-134">Optional</span></span>| <span data-ttu-id="58737-135">4 000 Mo.</span><span class="sxs-lookup"><span data-stu-id="58737-135">4000 MB.</span></span> <span data-ttu-id="58737-136">La valeur indiquée ne doit pas dépasser ce montant</span><span class="sxs-lookup"><span data-stu-id="58737-136">If you provide a value, it must not exceed this amount</span></span> |<span data-ttu-id="58737-137">Quantité totale de stockage du système de fichiers allouée pour la journalisation de toutes les mémoires tampons.</span><span class="sxs-lookup"><span data-stu-id="58737-137">The total amount of file system storage allocated for all logging buffers.</span></span>|  

## <a name="diagnosticinfrastructurelogs-element"></a><span data-ttu-id="58737-138">Élément DiagnosticInfrastructureLogs</span><span class="sxs-lookup"><span data-stu-id="58737-138">DiagnosticInfrastructureLogs Element</span></span>  
<span data-ttu-id="58737-139">Définit la configuration de la mémoire tampon pour les journaux générés par l’infrastructure de diagnostic sous-jacente.</span><span class="sxs-lookup"><span data-stu-id="58737-139">Defines the buffer configuration for the logs that are generated by the underlying diagnostics infrastructure.</span></span>

<span data-ttu-id="58737-140">Élément parent : [Élément DiagnosticMonitorConfiguration](#DiagnosticMonitorConfiguration).</span><span class="sxs-lookup"><span data-stu-id="58737-140">Parent Element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).</span></span>  

<span data-ttu-id="58737-141">Attributs :</span><span class="sxs-lookup"><span data-stu-id="58737-141">Attributes:</span></span>

|<span data-ttu-id="58737-142">Attribut</span><span class="sxs-lookup"><span data-stu-id="58737-142">Attribute</span></span>|<span data-ttu-id="58737-143">Type</span><span class="sxs-lookup"><span data-stu-id="58737-143">Type</span></span>|<span data-ttu-id="58737-144">Description</span><span class="sxs-lookup"><span data-stu-id="58737-144">Description</span></span>|  
|---------|----|-----------------|  
|<span data-ttu-id="58737-145">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="58737-145">**bufferQuotaInMB**</span></span>|<span data-ttu-id="58737-146">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="58737-146">unsignedInt</span></span>|<span data-ttu-id="58737-147">facultatif.</span><span class="sxs-lookup"><span data-stu-id="58737-147">Optional.</span></span> <span data-ttu-id="58737-148">Définit la quantité maximale de stockage du système de fichiers disponible pour les données spécifiées.</span><span class="sxs-lookup"><span data-stu-id="58737-148">Specifies the maximum amount of file system storage that is available for the specified data.</span></span><br /><br /> <span data-ttu-id="58737-149">La valeur par défaut est 0.</span><span class="sxs-lookup"><span data-stu-id="58737-149">The default is 0.</span></span>|  
|<span data-ttu-id="58737-150">**scheduledTransferLogLevelFilter**</span><span class="sxs-lookup"><span data-stu-id="58737-150">**scheduledTransferLogLevelFilter**</span></span>|<span data-ttu-id="58737-151">string</span><span class="sxs-lookup"><span data-stu-id="58737-151">string</span></span>|<span data-ttu-id="58737-152">facultatif.</span><span class="sxs-lookup"><span data-stu-id="58737-152">Optional.</span></span> <span data-ttu-id="58737-153">Définit le niveau de gravité minimal des entrées de journal transférées.</span><span class="sxs-lookup"><span data-stu-id="58737-153">Specifies the minimum severity level for log entries that are transferred.</span></span> <span data-ttu-id="58737-154">La valeur par défaut est **Non défini**.</span><span class="sxs-lookup"><span data-stu-id="58737-154">The default value is **Undefined**.</span></span> <span data-ttu-id="58737-155">Les autres valeurs possibles sont **Détaillé**, **Informations**, **Avertissement**, **Erreur**, et **Critique**.</span><span class="sxs-lookup"><span data-stu-id="58737-155">Other possible values are **Verbose**, **Information**, **Warning**, **Error**, and **Critical**.</span></span>|  
|<span data-ttu-id="58737-156">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="58737-156">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="58737-157">duration</span><span class="sxs-lookup"><span data-stu-id="58737-157">duration</span></span>|<span data-ttu-id="58737-158">facultatif.</span><span class="sxs-lookup"><span data-stu-id="58737-158">Optional.</span></span> <span data-ttu-id="58737-159">Définit l’intervalle entre les transferts planifiés de données, arrondi à la minute la plus proche.</span><span class="sxs-lookup"><span data-stu-id="58737-159">Specifies the interval between scheduled transfers of data, rounded up to the nearest minute.</span></span><br /><br /> <span data-ttu-id="58737-160">La valeur par défaut est PT0S.</span><span class="sxs-lookup"><span data-stu-id="58737-160">The default is PT0S.</span></span>|  

## <a name="logs-element"></a><span data-ttu-id="58737-161">Élément Logs</span><span class="sxs-lookup"><span data-stu-id="58737-161">Logs Element</span></span>  
 <span data-ttu-id="58737-162">Définit la configuration de la mémoire tampon des journaux Azure de base.</span><span class="sxs-lookup"><span data-stu-id="58737-162">Defines the buffer configuration for basic Azure logs.</span></span>

 <span data-ttu-id="58737-163">Élément parent : [Élément DiagnosticMonitorConfiguration](#DiagnosticMonitorConfiguration).</span><span class="sxs-lookup"><span data-stu-id="58737-163">Parent element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).</span></span>  

<span data-ttu-id="58737-164">Attributs :</span><span class="sxs-lookup"><span data-stu-id="58737-164">Attributes:</span></span>  

|<span data-ttu-id="58737-165">Attribut</span><span class="sxs-lookup"><span data-stu-id="58737-165">Attribute</span></span>|<span data-ttu-id="58737-166">Type</span><span class="sxs-lookup"><span data-stu-id="58737-166">Type</span></span>|<span data-ttu-id="58737-167">Description</span><span class="sxs-lookup"><span data-stu-id="58737-167">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="58737-168">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="58737-168">**bufferQuotaInMB**</span></span>|<span data-ttu-id="58737-169">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="58737-169">unsignedInt</span></span>|<span data-ttu-id="58737-170">facultatif.</span><span class="sxs-lookup"><span data-stu-id="58737-170">Optional.</span></span> <span data-ttu-id="58737-171">Définit la quantité maximale de stockage du système de fichiers disponible pour les données spécifiées.</span><span class="sxs-lookup"><span data-stu-id="58737-171">Specifies the maximum amount of file system storage that is available for the specified data.</span></span><br /><br /> <span data-ttu-id="58737-172">La valeur par défaut est 0.</span><span class="sxs-lookup"><span data-stu-id="58737-172">The default is 0.</span></span>|  
|<span data-ttu-id="58737-173">**scheduledTransferLogLevelFilter**</span><span class="sxs-lookup"><span data-stu-id="58737-173">**scheduledTransferLogLevelFilter**</span></span>|<span data-ttu-id="58737-174">string</span><span class="sxs-lookup"><span data-stu-id="58737-174">string</span></span>|<span data-ttu-id="58737-175">facultatif.</span><span class="sxs-lookup"><span data-stu-id="58737-175">Optional.</span></span> <span data-ttu-id="58737-176">Définit le niveau de gravité minimal des entrées de journal transférées.</span><span class="sxs-lookup"><span data-stu-id="58737-176">Specifies the minimum severity level for log entries that are transferred.</span></span> <span data-ttu-id="58737-177">La valeur par défaut est **Non défini**.</span><span class="sxs-lookup"><span data-stu-id="58737-177">The default value is **Undefined**.</span></span> <span data-ttu-id="58737-178">Les autres valeurs possibles sont **Détaillé**, **Informations**, **Avertissement**, **Erreur**, et **Critique**.</span><span class="sxs-lookup"><span data-stu-id="58737-178">Other possible values are **Verbose**, **Information**, **Warning**, **Error**, and **Critical**.</span></span>|  
|<span data-ttu-id="58737-179">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="58737-179">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="58737-180">duration</span><span class="sxs-lookup"><span data-stu-id="58737-180">duration</span></span>|<span data-ttu-id="58737-181">facultatif.</span><span class="sxs-lookup"><span data-stu-id="58737-181">Optional.</span></span> <span data-ttu-id="58737-182">Définit l’intervalle entre les transferts planifiés de données, arrondi à la minute la plus proche.</span><span class="sxs-lookup"><span data-stu-id="58737-182">Specifies the interval between scheduled transfers of data, rounded up to the nearest minute.</span></span><br /><br /> <span data-ttu-id="58737-183">La valeur par défaut est PT0S.</span><span class="sxs-lookup"><span data-stu-id="58737-183">The default is PT0S.</span></span>|  

## <a name="directories-element"></a><span data-ttu-id="58737-184">Élément Directories</span><span class="sxs-lookup"><span data-stu-id="58737-184">Directories Element</span></span>  
<span data-ttu-id="58737-185">Définit la configuration de la mémoire tampon pour les journaux basés sur des fichiers que vous pouvez définir.</span><span class="sxs-lookup"><span data-stu-id="58737-185">Defines the buffer configuration for file-based logs that you can define.</span></span>

<span data-ttu-id="58737-186">Élément parent : [Élément DiagnosticMonitorConfiguration](#DiagnosticMonitorConfiguration).</span><span class="sxs-lookup"><span data-stu-id="58737-186">Parent element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).</span></span>  


<span data-ttu-id="58737-187">Attributs :</span><span class="sxs-lookup"><span data-stu-id="58737-187">Attributes:</span></span>  

|<span data-ttu-id="58737-188">Attribut</span><span class="sxs-lookup"><span data-stu-id="58737-188">Attribute</span></span>|<span data-ttu-id="58737-189">Type</span><span class="sxs-lookup"><span data-stu-id="58737-189">Type</span></span>|<span data-ttu-id="58737-190">Description</span><span class="sxs-lookup"><span data-stu-id="58737-190">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="58737-191">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="58737-191">**bufferQuotaInMB**</span></span>|<span data-ttu-id="58737-192">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="58737-192">unsignedInt</span></span>|<span data-ttu-id="58737-193">facultatif.</span><span class="sxs-lookup"><span data-stu-id="58737-193">Optional.</span></span> <span data-ttu-id="58737-194">Définit la quantité maximale de stockage du système de fichiers disponible pour les données spécifiées.</span><span class="sxs-lookup"><span data-stu-id="58737-194">Specifies the maximum amount of file system storage that is available for the specified data.</span></span><br /><br /> <span data-ttu-id="58737-195">La valeur par défaut est 0.</span><span class="sxs-lookup"><span data-stu-id="58737-195">The default is 0.</span></span>|  
|<span data-ttu-id="58737-196">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="58737-196">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="58737-197">duration</span><span class="sxs-lookup"><span data-stu-id="58737-197">duration</span></span>|<span data-ttu-id="58737-198">facultatif.</span><span class="sxs-lookup"><span data-stu-id="58737-198">Optional.</span></span> <span data-ttu-id="58737-199">Définit l’intervalle entre les transferts planifiés de données, arrondi à la minute la plus proche.</span><span class="sxs-lookup"><span data-stu-id="58737-199">Specifies the interval between scheduled transfers of data, rounded up to the nearest minute.</span></span><br /><br /> <span data-ttu-id="58737-200">La valeur par défaut est PT0S.</span><span class="sxs-lookup"><span data-stu-id="58737-200">The default is PT0S.</span></span>|  

## <a name="crashdumps-element"></a><span data-ttu-id="58737-201">Élément CrashDumps</span><span class="sxs-lookup"><span data-stu-id="58737-201">CrashDumps Element</span></span>  
 <span data-ttu-id="58737-202">Définit le répertoire de vidages sur incident.</span><span class="sxs-lookup"><span data-stu-id="58737-202">Defines the crash dumps directory.</span></span>

 <span data-ttu-id="58737-203">Élément parent : [élément Directories](#Directories).</span><span class="sxs-lookup"><span data-stu-id="58737-203">Parent Element: [Directories Element](#Directories).</span></span>  

<span data-ttu-id="58737-204">Attributs :</span><span class="sxs-lookup"><span data-stu-id="58737-204">Attributes:</span></span>  

|<span data-ttu-id="58737-205">Attribut</span><span class="sxs-lookup"><span data-stu-id="58737-205">Attribute</span></span>|<span data-ttu-id="58737-206">Type</span><span class="sxs-lookup"><span data-stu-id="58737-206">Type</span></span>|<span data-ttu-id="58737-207">Description</span><span class="sxs-lookup"><span data-stu-id="58737-207">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="58737-208">**container**</span><span class="sxs-lookup"><span data-stu-id="58737-208">**container**</span></span>|<span data-ttu-id="58737-209">string</span><span class="sxs-lookup"><span data-stu-id="58737-209">string</span></span>|<span data-ttu-id="58737-210">Nom du conteneur dans lequel le contenu du répertoire doit être transféré.</span><span class="sxs-lookup"><span data-stu-id="58737-210">The name of the container where the contents of the directory is to be transferred.</span></span>|  
|<span data-ttu-id="58737-211">**directoryQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="58737-211">**directoryQuotaInMB**</span></span>|<span data-ttu-id="58737-212">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="58737-212">unsignedInt</span></span>|<span data-ttu-id="58737-213">facultatif.</span><span class="sxs-lookup"><span data-stu-id="58737-213">Optional.</span></span> <span data-ttu-id="58737-214">Définit la taille maximale du répertoire en mégaoctets.</span><span class="sxs-lookup"><span data-stu-id="58737-214">Specifies the maximum size of the directory in megabytes.</span></span><br /><br /> <span data-ttu-id="58737-215">La valeur par défaut est 0.</span><span class="sxs-lookup"><span data-stu-id="58737-215">The default is 0.</span></span>|  

## <a name="failedrequestlogs-element"></a><span data-ttu-id="58737-216">Élément FailedRequestLogs</span><span class="sxs-lookup"><span data-stu-id="58737-216">FailedRequestLogs Element</span></span>  
 <span data-ttu-id="58737-217">Définit le répertoire de journaux des demandes ayant échoué.</span><span class="sxs-lookup"><span data-stu-id="58737-217">Defines the failed request log directory.</span></span>

 <span data-ttu-id="58737-218">Élément parent : [élément Directories](#Directories).</span><span class="sxs-lookup"><span data-stu-id="58737-218">Parent Element [Directories Element](#Directories).</span></span>  

<span data-ttu-id="58737-219">Attributs :</span><span class="sxs-lookup"><span data-stu-id="58737-219">Attributes:</span></span>  

|<span data-ttu-id="58737-220">Attribut</span><span class="sxs-lookup"><span data-stu-id="58737-220">Attribute</span></span>|<span data-ttu-id="58737-221">Type</span><span class="sxs-lookup"><span data-stu-id="58737-221">Type</span></span>|<span data-ttu-id="58737-222">Description</span><span class="sxs-lookup"><span data-stu-id="58737-222">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="58737-223">**container**</span><span class="sxs-lookup"><span data-stu-id="58737-223">**container**</span></span>|<span data-ttu-id="58737-224">string</span><span class="sxs-lookup"><span data-stu-id="58737-224">string</span></span>|<span data-ttu-id="58737-225">Nom du conteneur dans lequel le contenu du répertoire doit être transféré.</span><span class="sxs-lookup"><span data-stu-id="58737-225">The name of the container where the contents of the directory is to be transferred.</span></span>|  
|<span data-ttu-id="58737-226">**directoryQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="58737-226">**directoryQuotaInMB**</span></span>|<span data-ttu-id="58737-227">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="58737-227">unsignedInt</span></span>|<span data-ttu-id="58737-228">facultatif.</span><span class="sxs-lookup"><span data-stu-id="58737-228">Optional.</span></span> <span data-ttu-id="58737-229">Définit la taille maximale du répertoire en mégaoctets.</span><span class="sxs-lookup"><span data-stu-id="58737-229">Specifies the maximum size of the directory in megabytes.</span></span><br /><br /> <span data-ttu-id="58737-230">La valeur par défaut est 0.</span><span class="sxs-lookup"><span data-stu-id="58737-230">The default is 0.</span></span>|  

##  <a name="iislogs-element"></a><span data-ttu-id="58737-231">Élément IISLogs</span><span class="sxs-lookup"><span data-stu-id="58737-231">IISLogs Element</span></span>  
 <span data-ttu-id="58737-232">Définit le répertoire des journaux IIS.</span><span class="sxs-lookup"><span data-stu-id="58737-232">Defines the IIS log directory.</span></span>

 <span data-ttu-id="58737-233">Élément parent : [élément Directories](#Directories).</span><span class="sxs-lookup"><span data-stu-id="58737-233">Parent Element [Directories Element](#Directories).</span></span>  

<span data-ttu-id="58737-234">Attributs :</span><span class="sxs-lookup"><span data-stu-id="58737-234">Attributes:</span></span>  

|<span data-ttu-id="58737-235">Attribut</span><span class="sxs-lookup"><span data-stu-id="58737-235">Attribute</span></span>|<span data-ttu-id="58737-236">Type</span><span class="sxs-lookup"><span data-stu-id="58737-236">Type</span></span>|<span data-ttu-id="58737-237">Description</span><span class="sxs-lookup"><span data-stu-id="58737-237">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="58737-238">**container**</span><span class="sxs-lookup"><span data-stu-id="58737-238">**container**</span></span>|<span data-ttu-id="58737-239">string</span><span class="sxs-lookup"><span data-stu-id="58737-239">string</span></span>|<span data-ttu-id="58737-240">Nom du conteneur dans lequel le contenu du répertoire doit être transféré.</span><span class="sxs-lookup"><span data-stu-id="58737-240">The name of the container where the contents of the directory is to be transferred.</span></span>|  
|<span data-ttu-id="58737-241">**directoryQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="58737-241">**directoryQuotaInMB**</span></span>|<span data-ttu-id="58737-242">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="58737-242">unsignedInt</span></span>|<span data-ttu-id="58737-243">facultatif.</span><span class="sxs-lookup"><span data-stu-id="58737-243">Optional.</span></span> <span data-ttu-id="58737-244">Définit la taille maximale du répertoire en mégaoctets.</span><span class="sxs-lookup"><span data-stu-id="58737-244">Specifies the maximum size of the directory in megabytes.</span></span><br /><br /> <span data-ttu-id="58737-245">La valeur par défaut est 0.</span><span class="sxs-lookup"><span data-stu-id="58737-245">The default is 0.</span></span>|  

## <a name="datasources-element"></a><span data-ttu-id="58737-246">Élément DataSources</span><span class="sxs-lookup"><span data-stu-id="58737-246">DataSources Element</span></span>  
 <span data-ttu-id="58737-247">Définit zéro ou plusieurs répertoires de journaux supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="58737-247">Defines zero or more additional log directories.</span></span>

 <span data-ttu-id="58737-248">Élément parent : [élément Directories](#Directories).</span><span class="sxs-lookup"><span data-stu-id="58737-248">Parent Element: [Directories Element](#Directories).</span></span>

## <a name="directoryconfiguration-element"></a><span data-ttu-id="58737-249">Élément DirectoryConfiguration</span><span class="sxs-lookup"><span data-stu-id="58737-249">DirectoryConfiguration Element</span></span>  
 <span data-ttu-id="58737-250">Définit le répertoire de fichiers journaux à surveiller.</span><span class="sxs-lookup"><span data-stu-id="58737-250">Defines the directory of log files to monitor.</span></span>

 <span data-ttu-id="58737-251">Élément parent : [élément DataSources](#DataSources).</span><span class="sxs-lookup"><span data-stu-id="58737-251">Parent Element: [DataSources Element](#DataSources).</span></span>

<span data-ttu-id="58737-252">Attributs :</span><span class="sxs-lookup"><span data-stu-id="58737-252">Attributes:</span></span>

|<span data-ttu-id="58737-253">Attribut</span><span class="sxs-lookup"><span data-stu-id="58737-253">Attribute</span></span>|<span data-ttu-id="58737-254">Type</span><span class="sxs-lookup"><span data-stu-id="58737-254">Type</span></span>|<span data-ttu-id="58737-255">Description</span><span class="sxs-lookup"><span data-stu-id="58737-255">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="58737-256">**container**</span><span class="sxs-lookup"><span data-stu-id="58737-256">**container**</span></span>|<span data-ttu-id="58737-257">string</span><span class="sxs-lookup"><span data-stu-id="58737-257">string</span></span>|<span data-ttu-id="58737-258">Nom du conteneur dans lequel le contenu du répertoire doit être transféré.</span><span class="sxs-lookup"><span data-stu-id="58737-258">The name of the container where the contents of the directory is to be transferred.</span></span>|  
|<span data-ttu-id="58737-259">**directoryQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="58737-259">**directoryQuotaInMB**</span></span>|<span data-ttu-id="58737-260">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="58737-260">unsignedInt</span></span>|<span data-ttu-id="58737-261">facultatif.</span><span class="sxs-lookup"><span data-stu-id="58737-261">Optional.</span></span> <span data-ttu-id="58737-262">Définit la taille maximale du répertoire en mégaoctets.</span><span class="sxs-lookup"><span data-stu-id="58737-262">Specifies the maximum size of the directory in megabytes.</span></span><br /><br /> <span data-ttu-id="58737-263">La valeur par défaut est 0.</span><span class="sxs-lookup"><span data-stu-id="58737-263">The default is 0.</span></span>|  

## <a name="absolute-element"></a><span data-ttu-id="58737-264">Élément Absolute</span><span class="sxs-lookup"><span data-stu-id="58737-264">Absolute Element</span></span>  
 <span data-ttu-id="58737-265">Définit un chemin d’accès absolu du répertoire à surveiller avec une extension d’environnement facultative.</span><span class="sxs-lookup"><span data-stu-id="58737-265">Defines an absolute path of the directory to monitor with optional environment expansion.</span></span>

 <span data-ttu-id="58737-266">Élément parent : [élément DirectoryConfiguration](#DirectoryConfiguration).</span><span class="sxs-lookup"><span data-stu-id="58737-266">Parent Element: [DirectoryConfiguration Element](#DirectoryConfiguration).</span></span>  

<span data-ttu-id="58737-267">Attributs :</span><span class="sxs-lookup"><span data-stu-id="58737-267">Attributes:</span></span>  

|<span data-ttu-id="58737-268">Attribut</span><span class="sxs-lookup"><span data-stu-id="58737-268">Attribute</span></span>|<span data-ttu-id="58737-269">Type</span><span class="sxs-lookup"><span data-stu-id="58737-269">Type</span></span>|<span data-ttu-id="58737-270">Description</span><span class="sxs-lookup"><span data-stu-id="58737-270">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="58737-271">**path**</span><span class="sxs-lookup"><span data-stu-id="58737-271">**path**</span></span>|<span data-ttu-id="58737-272">string</span><span class="sxs-lookup"><span data-stu-id="58737-272">string</span></span>|<span data-ttu-id="58737-273">Obligatoire.</span><span class="sxs-lookup"><span data-stu-id="58737-273">Required.</span></span> <span data-ttu-id="58737-274">Chemin d’accès absolu au répertoire à surveiller.</span><span class="sxs-lookup"><span data-stu-id="58737-274">The absolute path to the directory to monitor.</span></span>|  
|<span data-ttu-id="58737-275">**expandEnvironment**</span><span class="sxs-lookup"><span data-stu-id="58737-275">**expandEnvironment**</span></span>|<span data-ttu-id="58737-276">booléenne</span><span class="sxs-lookup"><span data-stu-id="58737-276">boolean</span></span>|<span data-ttu-id="58737-277">Obligatoire.</span><span class="sxs-lookup"><span data-stu-id="58737-277">Required.</span></span> <span data-ttu-id="58737-278">Si la valeur **true** est attribuée, les variables d’environnement du chemin d’accès sont développées.</span><span class="sxs-lookup"><span data-stu-id="58737-278">If set to **true**, environment variables in the path are expanded.</span></span>|  

## <a name="localresource-element"></a><span data-ttu-id="58737-279">Élément LocalResource</span><span class="sxs-lookup"><span data-stu-id="58737-279">LocalResource Element</span></span>  
 <span data-ttu-id="58737-280">Définit un chemin d’accès relatif à une ressource locale spécifiée dans la définition de service.</span><span class="sxs-lookup"><span data-stu-id="58737-280">Defines a path relative to a local resource defined in the service definition.</span></span>

 <span data-ttu-id="58737-281">Élément parent : [élément DirectoryConfiguration](#DirectoryConfiguration).</span><span class="sxs-lookup"><span data-stu-id="58737-281">Parent Element: [DirectoryConfiguration Element](#DirectoryConfiguration).</span></span>  

<span data-ttu-id="58737-282">Attributs :</span><span class="sxs-lookup"><span data-stu-id="58737-282">Attributes:</span></span>  

|<span data-ttu-id="58737-283">Attribut</span><span class="sxs-lookup"><span data-stu-id="58737-283">Attribute</span></span>|<span data-ttu-id="58737-284">Type</span><span class="sxs-lookup"><span data-stu-id="58737-284">Type</span></span>|<span data-ttu-id="58737-285">Description</span><span class="sxs-lookup"><span data-stu-id="58737-285">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="58737-286">**name**</span><span class="sxs-lookup"><span data-stu-id="58737-286">**name**</span></span>|<span data-ttu-id="58737-287">string</span><span class="sxs-lookup"><span data-stu-id="58737-287">string</span></span>|<span data-ttu-id="58737-288">Obligatoire.</span><span class="sxs-lookup"><span data-stu-id="58737-288">Required.</span></span> <span data-ttu-id="58737-289">Nom de la ressource locale qui contient le répertoire à surveiller.</span><span class="sxs-lookup"><span data-stu-id="58737-289">The name of the local resource that contains the directory to monitor.</span></span>|  
|<span data-ttu-id="58737-290">**relativePath**</span><span class="sxs-lookup"><span data-stu-id="58737-290">**relativePath**</span></span>|<span data-ttu-id="58737-291">string</span><span class="sxs-lookup"><span data-stu-id="58737-291">string</span></span>|<span data-ttu-id="58737-292">Obligatoire.</span><span class="sxs-lookup"><span data-stu-id="58737-292">Required.</span></span> <span data-ttu-id="58737-293">Chemin d’accès relatif à la ressource locale à surveiller.</span><span class="sxs-lookup"><span data-stu-id="58737-293">The path relative to the local resource to monitor.</span></span>|  

## <a name="performancecounters-element"></a><span data-ttu-id="58737-294">Élément PerformanceCounters</span><span class="sxs-lookup"><span data-stu-id="58737-294">PerformanceCounters Element</span></span>  
 <span data-ttu-id="58737-295">Définit le chemin d’accès au compteur de performance à collecter.</span><span class="sxs-lookup"><span data-stu-id="58737-295">Defines the path to the performance counter to collect.</span></span>

 <span data-ttu-id="58737-296">Élément parent : [Élément DiagnosticMonitorConfiguration](#DiagnosticMonitorConfiguration).</span><span class="sxs-lookup"><span data-stu-id="58737-296">Parent Element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).</span></span>


 <span data-ttu-id="58737-297">Attributs :</span><span class="sxs-lookup"><span data-stu-id="58737-297">Attributes:</span></span>  

|<span data-ttu-id="58737-298">Attribut</span><span class="sxs-lookup"><span data-stu-id="58737-298">Attribute</span></span>|<span data-ttu-id="58737-299">Type</span><span class="sxs-lookup"><span data-stu-id="58737-299">Type</span></span>|<span data-ttu-id="58737-300">Description</span><span class="sxs-lookup"><span data-stu-id="58737-300">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="58737-301">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="58737-301">**bufferQuotaInMB**</span></span>|<span data-ttu-id="58737-302">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="58737-302">unsignedInt</span></span>|<span data-ttu-id="58737-303">facultatif.</span><span class="sxs-lookup"><span data-stu-id="58737-303">Optional.</span></span> <span data-ttu-id="58737-304">Définit la quantité maximale de stockage du système de fichiers disponible pour les données spécifiées.</span><span class="sxs-lookup"><span data-stu-id="58737-304">Specifies the maximum amount of file system storage that is available for the specified data.</span></span><br /><br /> <span data-ttu-id="58737-305">La valeur par défaut est 0.</span><span class="sxs-lookup"><span data-stu-id="58737-305">The default is 0.</span></span>|  
|<span data-ttu-id="58737-306">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="58737-306">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="58737-307">duration</span><span class="sxs-lookup"><span data-stu-id="58737-307">duration</span></span>|<span data-ttu-id="58737-308">facultatif.</span><span class="sxs-lookup"><span data-stu-id="58737-308">Optional.</span></span> <span data-ttu-id="58737-309">Définit l’intervalle entre les transferts planifiés de données, arrondi à la minute la plus proche.</span><span class="sxs-lookup"><span data-stu-id="58737-309">Specifies the interval between scheduled transfers of data, rounded up to the nearest minute.</span></span><br /><br /> <span data-ttu-id="58737-310">La valeur par défaut est PT0S.</span><span class="sxs-lookup"><span data-stu-id="58737-310">The default is PT0S.</span></span>|  

## <a name="performancecounterconfiguration-element"></a><span data-ttu-id="58737-311">Élément PerformanceCounterConfiguration</span><span class="sxs-lookup"><span data-stu-id="58737-311">PerformanceCounterConfiguration Element</span></span>  
 <span data-ttu-id="58737-312">Définit le compteur de performance à collecter.</span><span class="sxs-lookup"><span data-stu-id="58737-312">Defines the performance counter to collect.</span></span>

 <span data-ttu-id="58737-313">Élément parent : [élément PerformanceCounters](#PerformanceCounters).</span><span class="sxs-lookup"><span data-stu-id="58737-313">Parent Element: [PerformanceCounters Element](#PerformanceCounters).</span></span>  

 <span data-ttu-id="58737-314">Attributs :</span><span class="sxs-lookup"><span data-stu-id="58737-314">Attributes:</span></span>  

|<span data-ttu-id="58737-315">Attribut</span><span class="sxs-lookup"><span data-stu-id="58737-315">Attribute</span></span>|<span data-ttu-id="58737-316">Type</span><span class="sxs-lookup"><span data-stu-id="58737-316">Type</span></span>|<span data-ttu-id="58737-317">Description</span><span class="sxs-lookup"><span data-stu-id="58737-317">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="58737-318">**counterSpecifier**</span><span class="sxs-lookup"><span data-stu-id="58737-318">**counterSpecifier**</span></span>|<span data-ttu-id="58737-319">string</span><span class="sxs-lookup"><span data-stu-id="58737-319">string</span></span>|<span data-ttu-id="58737-320">Obligatoire.</span><span class="sxs-lookup"><span data-stu-id="58737-320">Required.</span></span> <span data-ttu-id="58737-321">Chemin d’accès au compteur de performance à collecter.</span><span class="sxs-lookup"><span data-stu-id="58737-321">The path to the performance counter to collect.</span></span>|  
|<span data-ttu-id="58737-322">**sampleRate**</span><span class="sxs-lookup"><span data-stu-id="58737-322">**sampleRate**</span></span>|<span data-ttu-id="58737-323">duration</span><span class="sxs-lookup"><span data-stu-id="58737-323">duration</span></span>|<span data-ttu-id="58737-324">Obligatoire.</span><span class="sxs-lookup"><span data-stu-id="58737-324">Required.</span></span> <span data-ttu-id="58737-325">Vitesse à laquelle le compteur de performance doit être collecté.</span><span class="sxs-lookup"><span data-stu-id="58737-325">The rate at which the performance counter should be collected.</span></span>|  

## <a name="windowseventlog-element"></a><span data-ttu-id="58737-326">Élément WindowsEventLog</span><span class="sxs-lookup"><span data-stu-id="58737-326">WindowsEventLog Element</span></span>  
 <span data-ttu-id="58737-327">Définit les journaux des événements à surveiller.</span><span class="sxs-lookup"><span data-stu-id="58737-327">Defines the event logs to monitor.</span></span>

 <span data-ttu-id="58737-328">Élément parent : [Élément DiagnosticMonitorConfiguration](#DiagnosticMonitorConfiguration).</span><span class="sxs-lookup"><span data-stu-id="58737-328">Parent Element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).</span></span>

  <span data-ttu-id="58737-329">Attributs :</span><span class="sxs-lookup"><span data-stu-id="58737-329">Attributes:</span></span>

|<span data-ttu-id="58737-330">Attribut</span><span class="sxs-lookup"><span data-stu-id="58737-330">Attribute</span></span>|<span data-ttu-id="58737-331">Type</span><span class="sxs-lookup"><span data-stu-id="58737-331">Type</span></span>|<span data-ttu-id="58737-332">Description</span><span class="sxs-lookup"><span data-stu-id="58737-332">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="58737-333">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="58737-333">**bufferQuotaInMB**</span></span>|<span data-ttu-id="58737-334">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="58737-334">unsignedInt</span></span>|<span data-ttu-id="58737-335">facultatif.</span><span class="sxs-lookup"><span data-stu-id="58737-335">Optional.</span></span> <span data-ttu-id="58737-336">Définit la quantité maximale de stockage du système de fichiers disponible pour les données spécifiées.</span><span class="sxs-lookup"><span data-stu-id="58737-336">Specifies the maximum amount of file system storage that is available for the specified data.</span></span><br /><br /> <span data-ttu-id="58737-337">La valeur par défaut est 0.</span><span class="sxs-lookup"><span data-stu-id="58737-337">The default is 0.</span></span>|  
|<span data-ttu-id="58737-338">**scheduledTransferLogLevelFilter**</span><span class="sxs-lookup"><span data-stu-id="58737-338">**scheduledTransferLogLevelFilter**</span></span>|<span data-ttu-id="58737-339">string</span><span class="sxs-lookup"><span data-stu-id="58737-339">string</span></span>|<span data-ttu-id="58737-340">facultatif.</span><span class="sxs-lookup"><span data-stu-id="58737-340">Optional.</span></span> <span data-ttu-id="58737-341">Définit le niveau de gravité minimal des entrées de journal transférées.</span><span class="sxs-lookup"><span data-stu-id="58737-341">Specifies the minimum severity level for log entries that are transferred.</span></span> <span data-ttu-id="58737-342">La valeur par défaut est **Non défini**.</span><span class="sxs-lookup"><span data-stu-id="58737-342">The default value is **Undefined**.</span></span> <span data-ttu-id="58737-343">Les autres valeurs possibles sont **Détaillé**, **Informations**, **Avertissement**, **Erreur**, et **Critique**.</span><span class="sxs-lookup"><span data-stu-id="58737-343">Other possible values are **Verbose**, **Information**, **Warning**, **Error**, and **Critical**.</span></span>|  
|<span data-ttu-id="58737-344">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="58737-344">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="58737-345">duration</span><span class="sxs-lookup"><span data-stu-id="58737-345">duration</span></span>|<span data-ttu-id="58737-346">facultatif.</span><span class="sxs-lookup"><span data-stu-id="58737-346">Optional.</span></span> <span data-ttu-id="58737-347">Définit l’intervalle entre les transferts planifiés de données, arrondi à la minute la plus proche.</span><span class="sxs-lookup"><span data-stu-id="58737-347">Specifies the interval between scheduled transfers of data, rounded up to the nearest minute.</span></span><br /><br /> <span data-ttu-id="58737-348">La valeur par défaut est PT0S.</span><span class="sxs-lookup"><span data-stu-id="58737-348">The default is PT0S.</span></span>|  

## <a name="datasource-element"></a><span data-ttu-id="58737-349">Élément DataSource</span><span class="sxs-lookup"><span data-stu-id="58737-349">DataSource Element</span></span>  
 <span data-ttu-id="58737-350">Définit les journaux des événements à surveiller.</span><span class="sxs-lookup"><span data-stu-id="58737-350">Defines the event log to monitor.</span></span>

 <span data-ttu-id="58737-351">Élément parent : [élément WindowsEventLog](#windowsEventLog).</span><span class="sxs-lookup"><span data-stu-id="58737-351">Parent Element: [WindowsEventLog Element](#windowsEventLog).</span></span>  

 <span data-ttu-id="58737-352">Attributs :</span><span class="sxs-lookup"><span data-stu-id="58737-352">Attributes:</span></span>

|<span data-ttu-id="58737-353">Attribut</span><span class="sxs-lookup"><span data-stu-id="58737-353">Attribute</span></span>|<span data-ttu-id="58737-354">Type</span><span class="sxs-lookup"><span data-stu-id="58737-354">Type</span></span>|<span data-ttu-id="58737-355">Description</span><span class="sxs-lookup"><span data-stu-id="58737-355">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="58737-356">**name**</span><span class="sxs-lookup"><span data-stu-id="58737-356">**name**</span></span>|<span data-ttu-id="58737-357">string</span><span class="sxs-lookup"><span data-stu-id="58737-357">string</span></span>|<span data-ttu-id="58737-358">Obligatoire.</span><span class="sxs-lookup"><span data-stu-id="58737-358">Required.</span></span> <span data-ttu-id="58737-359">Expression XPath spécifiant le journal à collecter.</span><span class="sxs-lookup"><span data-stu-id="58737-359">An XPath expression specifying the log to collect.</span></span>|  
