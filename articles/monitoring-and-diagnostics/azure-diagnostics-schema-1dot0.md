---
title: "aaaAzure schéma de Configuration de Diagnostics 1.0 | Documents Microsoft"
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
ms.openlocfilehash: bdd2b26217d6ea28f19e651ab429e7e7401ff57b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-diagnostics-10-configuration-schema"></a><span data-ttu-id="cab77-103">Schéma de configuration Azure Diagnostics 1.0</span><span class="sxs-lookup"><span data-stu-id="cab77-103">Azure Diagnostics 1.0 Configuration Schema</span></span>
> [!NOTE]
> <span data-ttu-id="cab77-104">Diagnostics Azure sont des compteurs de performance toocollect hello composant utilisé et d’autres statistiques à partir de Machines virtuelles Azure, machines virtuelles identiques, l’infrastructure de Service et les Services de Cloud.</span><span class="sxs-lookup"><span data-stu-id="cab77-104">Azure Diagnostics is hello component used toocollect performance counters and other statistics from Azure Virtual Machines, Virtual Machine Scale Sets, Service Fabric, and Cloud Services.</span></span>  <span data-ttu-id="cab77-105">Cette page vous concerne uniquement si vous utilisez l’un de ces services.</span><span class="sxs-lookup"><span data-stu-id="cab77-105">This page is only relevant if you are using one of these services.</span></span>
>

<span data-ttu-id="cab77-106">Azure Diagnostics est utilisé avec d’autres produits de diagnostic Microsoft tels que Azure Monitor, Application Insights et Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="cab77-106">Azure Diagnostics is used with other Microsoft diagnostics products like Azure Monitor, Application Insights, and Log Analytics.</span></span>

<span data-ttu-id="cab77-107">fichier de configuration des Diagnostics Windows Azure Hello définit des valeurs qui sont utilisées tooinitialize hello moniteur de diagnostic.</span><span class="sxs-lookup"><span data-stu-id="cab77-107">hello Azure Diagnostics configuration file defines values that are used tooinitialize hello Diagnostics Monitor.</span></span> <span data-ttu-id="cab77-108">Ce fichier est tooinitialize utilisé les paramètres de configuration de diagnostic lorsque hello diagnostics surveiller démarre.</span><span class="sxs-lookup"><span data-stu-id="cab77-108">This file is used tooinitialize diagnostic configuration settings when hello diagnostics monitor starts.</span></span>  

 <span data-ttu-id="cab77-109">Par défaut, le fichier de schéma de configuration de Diagnostics Windows Azure hello est toohello installé `C:\Program Files\Microsoft SDKs\Azure\.NET SDK\<version>\schemas` active.</span><span class="sxs-lookup"><span data-stu-id="cab77-109">By default, hello Azure Diagnostics configuration schema file is installed toohello `C:\Program Files\Microsoft SDKs\Azure\.NET SDK\<version>\schemas` directory.</span></span> <span data-ttu-id="cab77-110">Remplacez `<version>` avec la version installée de hello Hello [Azure SDK](http://www.windowsazure.com/develop/downloads/).</span><span class="sxs-lookup"><span data-stu-id="cab77-110">Replace `<version>` with hello installed version of hello [Azure SDK](http://www.windowsazure.com/develop/downloads/).</span></span>  

> [!NOTE]
>  <span data-ttu-id="cab77-111">fichier de configuration des diagnostics Hello est généralement utilisé avec les tâches de démarrage qui requièrent toobe de données de diagnostic collectée précédemment dans le processus de démarrage hello.</span><span class="sxs-lookup"><span data-stu-id="cab77-111">hello diagnostics configuration file is typically used with startup tasks that require diagnostic data toobe collected earlier in hello startup process.</span></span> <span data-ttu-id="cab77-112">Pour plus d’informations sur l’utilisation d’Azure Diagnostics, consultez [Collect Logging Data by Using Azure Diagnostics](assetId:///83a91c23-5ca2-4fc9-8df3-62036c37a3d7) (Collecte de données de journalisation à l’aide d’Azure Diagnostics).</span><span class="sxs-lookup"><span data-stu-id="cab77-112">For more information about using Azure Diagnostics, see [Collect Logging Data by Using Azure Diagnostics](assetId:///83a91c23-5ca2-4fc9-8df3-62036c37a3d7).</span></span>  

## <a name="example-of-hello-diagnostics-configuration-file"></a><span data-ttu-id="cab77-113">Exemple de fichier de configuration de diagnostics hello</span><span class="sxs-lookup"><span data-stu-id="cab77-113">Example of hello diagnostics configuration file</span></span>  
 <span data-ttu-id="cab77-114">Bonjour à l’exemple suivant montre un fichier de configuration de diagnostics standard :</span><span class="sxs-lookup"><span data-stu-id="cab77-114">hello following example shows a typical diagnostics configuration file:</span></span>  

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

      <!-- These three elements specify hello special directories   
           that are set up for hello log types -->  
      <CrashDumps container="wad-crash-dumps" directoryQuotaInMB="256" />  
      <FailedRequestLogs container="wad-frq" directoryQuotaInMB="256" />  
      <IISLogs container="wad-iis" directoryQuotaInMB="256" />  

      <!-- For regular directories hello DataSources element is used -->  
      <DataSources>  
         <DirectoryConfiguration container="wad-panther" directoryQuotaInMB="128">  
            <!-- Absolute specifies an absolute path with optional environment expansion -->  
            <Absolute expandEnvironment="true" path="%SystemRoot%\system32\sysprep\Panther" />  
         </DirectoryConfiguration>  
         <DirectoryConfiguration container="wad-custom" directoryQuotaInMB="128">  
            <!-- LocalResource specifies a path relative tooa local   
                 resource defined in hello service definition -->  
            <LocalResource name="MyLoggingLocalResource" relativePath="logs" />  
         </DirectoryConfiguration>  
      </DataSources>  
   </Directories>  

   <PerformanceCounters bufferQuotaInMB="512" scheduledTransferPeriod="PT1M">  
      <!-- hello counter specifier is in hello same format as hello imperative   
           diagnostics configuration API -->  
      <PerformanceCounterConfiguration   
         counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT5S" />  
   </PerformanceCounters>  

   <WindowsEventLog bufferQuotaInMB="512"  
      scheduledTransferLogLevelFilter="Verbose"  
      scheduledTransferPeriod="PT1M">  
      <!-- hello event log name is in hello same format as hello imperative   
           diagnostics configuration API -->  
      <DataSource name="System!*" />  
   </WindowsEventLog>  
</DiagnosticMonitorConfiguration>  
```  

## <a name="diagnosticsconfiguration-namespace"></a><span data-ttu-id="cab77-115">Espace de noms DiagnosticsConfiguration</span><span class="sxs-lookup"><span data-stu-id="cab77-115">DiagnosticsConfiguration Namespace</span></span>  
 <span data-ttu-id="cab77-116">espace de noms XML Hello pour le fichier de configuration de diagnostics hello est la suivante :</span><span class="sxs-lookup"><span data-stu-id="cab77-116">hello XML namespace for hello diagnostics configuration file is:</span></span>  

```  
http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration  
```  

## <a name="schema-elements"></a><span data-ttu-id="cab77-117">Éléments du schéma</span><span class="sxs-lookup"><span data-stu-id="cab77-117">Schema Elements</span></span>  
 <span data-ttu-id="cab77-118">fichier de configuration des diagnostics Hello inclut hello suivant d’éléments.</span><span class="sxs-lookup"><span data-stu-id="cab77-118">hello diagnostics configuration file includes hello following elements.</span></span>


## <a name="diagnosticmonitorconfiguration-element"></a><span data-ttu-id="cab77-119">Élément DiagnosticMonitorConfiguration</span><span class="sxs-lookup"><span data-stu-id="cab77-119">DiagnosticMonitorConfiguration Element</span></span>  
<span data-ttu-id="cab77-120">élément de niveau supérieur Hello hello diagnostics du fichier de configuration.</span><span class="sxs-lookup"><span data-stu-id="cab77-120">hello top-level element of hello diagnostics configuration file.</span></span>  

<span data-ttu-id="cab77-121">Attributs :</span><span class="sxs-lookup"><span data-stu-id="cab77-121">Attributes:</span></span>

|<span data-ttu-id="cab77-122">Attribut</span><span class="sxs-lookup"><span data-stu-id="cab77-122">Attribute</span></span>  |<span data-ttu-id="cab77-123">Type</span><span class="sxs-lookup"><span data-stu-id="cab77-123">Type</span></span>   |<span data-ttu-id="cab77-124">Requis</span><span class="sxs-lookup"><span data-stu-id="cab77-124">Required</span></span>| <span data-ttu-id="cab77-125">Default</span><span class="sxs-lookup"><span data-stu-id="cab77-125">Default</span></span> | <span data-ttu-id="cab77-126">Description</span><span class="sxs-lookup"><span data-stu-id="cab77-126">Description</span></span>|  
|-----------|-------|--------|---------|------------|  
|<span data-ttu-id="cab77-127">**configurationChangePollInterval**</span><span class="sxs-lookup"><span data-stu-id="cab77-127">**configurationChangePollInterval**</span></span>|<span data-ttu-id="cab77-128">duration</span><span class="sxs-lookup"><span data-stu-id="cab77-128">duration</span></span>|<span data-ttu-id="cab77-129">Facultatif</span><span class="sxs-lookup"><span data-stu-id="cab77-129">Optional</span></span> | <span data-ttu-id="cab77-130">PT1M</span><span class="sxs-lookup"><span data-stu-id="cab77-130">PT1M</span></span>| <span data-ttu-id="cab77-131">Spécifie l’intervalle de hello selon les interrogations du moniteur de diagnostic hello pour les modifications de configuration de diagnostic.</span><span class="sxs-lookup"><span data-stu-id="cab77-131">Specifies hello interval at which hello diagnostic monitor polls for diagnostic configuration changes.</span></span>|  
|<span data-ttu-id="cab77-132">**overallQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="cab77-132">**overallQuotaInMB**</span></span>|<span data-ttu-id="cab77-133">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="cab77-133">unsignedInt</span></span>|<span data-ttu-id="cab77-134">Facultatif</span><span class="sxs-lookup"><span data-stu-id="cab77-134">Optional</span></span>| <span data-ttu-id="cab77-135">4 000 Mo.</span><span class="sxs-lookup"><span data-stu-id="cab77-135">4000 MB.</span></span> <span data-ttu-id="cab77-136">La valeur indiquée ne doit pas dépasser ce montant</span><span class="sxs-lookup"><span data-stu-id="cab77-136">If you provide a value, it must not exceed this amount</span></span> |<span data-ttu-id="cab77-137">quantité totale de Hello du stockage de système de fichiers allouée pour toutes les mémoires tampons de journalisation.</span><span class="sxs-lookup"><span data-stu-id="cab77-137">hello total amount of file system storage allocated for all logging buffers.</span></span>|  

## <a name="diagnosticinfrastructurelogs-element"></a><span data-ttu-id="cab77-138">Élément DiagnosticInfrastructureLogs</span><span class="sxs-lookup"><span data-stu-id="cab77-138">DiagnosticInfrastructureLogs Element</span></span>  
<span data-ttu-id="cab77-139">Définit la configuration de mémoire tampon hello pour les journaux hello qui sont générés par l’infrastructure de diagnostics sous-jacente hello.</span><span class="sxs-lookup"><span data-stu-id="cab77-139">Defines hello buffer configuration for hello logs that are generated by hello underlying diagnostics infrastructure.</span></span>

<span data-ttu-id="cab77-140">Élément parent : [Élément DiagnosticMonitorConfiguration](#DiagnosticMonitorConfiguration).</span><span class="sxs-lookup"><span data-stu-id="cab77-140">Parent Element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).</span></span>  

<span data-ttu-id="cab77-141">Attributs :</span><span class="sxs-lookup"><span data-stu-id="cab77-141">Attributes:</span></span>

|<span data-ttu-id="cab77-142">Attribut</span><span class="sxs-lookup"><span data-stu-id="cab77-142">Attribute</span></span>|<span data-ttu-id="cab77-143">Type</span><span class="sxs-lookup"><span data-stu-id="cab77-143">Type</span></span>|<span data-ttu-id="cab77-144">Description</span><span class="sxs-lookup"><span data-stu-id="cab77-144">Description</span></span>|  
|---------|----|-----------------|  
|<span data-ttu-id="cab77-145">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="cab77-145">**bufferQuotaInMB**</span></span>|<span data-ttu-id="cab77-146">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="cab77-146">unsignedInt</span></span>|<span data-ttu-id="cab77-147">facultatif.</span><span class="sxs-lookup"><span data-stu-id="cab77-147">Optional.</span></span> <span data-ttu-id="cab77-148">Spécifie la quantité maximale de hello du stockage de système de fichiers est disponible pour hello spécifié données.</span><span class="sxs-lookup"><span data-stu-id="cab77-148">Specifies hello maximum amount of file system storage that is available for hello specified data.</span></span><br /><br /> <span data-ttu-id="cab77-149">valeur par défaut Hello est 0.</span><span class="sxs-lookup"><span data-stu-id="cab77-149">hello default is 0.</span></span>|  
|<span data-ttu-id="cab77-150">**scheduledTransferLogLevelFilter**</span><span class="sxs-lookup"><span data-stu-id="cab77-150">**scheduledTransferLogLevelFilter**</span></span>|<span data-ttu-id="cab77-151">string</span><span class="sxs-lookup"><span data-stu-id="cab77-151">string</span></span>|<span data-ttu-id="cab77-152">facultatif.</span><span class="sxs-lookup"><span data-stu-id="cab77-152">Optional.</span></span> <span data-ttu-id="cab77-153">Spécifie le niveau de gravité minimal hello pour les entrées de journal sont transférées.</span><span class="sxs-lookup"><span data-stu-id="cab77-153">Specifies hello minimum severity level for log entries that are transferred.</span></span> <span data-ttu-id="cab77-154">la valeur par défaut Hello est **Undefined**.</span><span class="sxs-lookup"><span data-stu-id="cab77-154">hello default value is **Undefined**.</span></span> <span data-ttu-id="cab77-155">Les autres valeurs possibles sont **Détaillé**, **Informations**, **Avertissement**, **Erreur**, et **Critique**.</span><span class="sxs-lookup"><span data-stu-id="cab77-155">Other possible values are **Verbose**, **Information**, **Warning**, **Error**, and **Critical**.</span></span>|  
|<span data-ttu-id="cab77-156">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="cab77-156">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="cab77-157">duration</span><span class="sxs-lookup"><span data-stu-id="cab77-157">duration</span></span>|<span data-ttu-id="cab77-158">facultatif.</span><span class="sxs-lookup"><span data-stu-id="cab77-158">Optional.</span></span> <span data-ttu-id="cab77-159">Spécifie l’intervalle de salutation entre les transferts planifiés de données, arrondies à toohello minute la plus proche.</span><span class="sxs-lookup"><span data-stu-id="cab77-159">Specifies hello interval between scheduled transfers of data, rounded up toohello nearest minute.</span></span><br /><br /> <span data-ttu-id="cab77-160">valeur par défaut Hello est PT0S.</span><span class="sxs-lookup"><span data-stu-id="cab77-160">hello default is PT0S.</span></span>|  

## <a name="logs-element"></a><span data-ttu-id="cab77-161">Élément Logs</span><span class="sxs-lookup"><span data-stu-id="cab77-161">Logs Element</span></span>  
 <span data-ttu-id="cab77-162">Définit la configuration du tampon hello pour les journaux Azure de base.</span><span class="sxs-lookup"><span data-stu-id="cab77-162">Defines hello buffer configuration for basic Azure logs.</span></span>

 <span data-ttu-id="cab77-163">Élément parent : [Élément DiagnosticMonitorConfiguration](#DiagnosticMonitorConfiguration).</span><span class="sxs-lookup"><span data-stu-id="cab77-163">Parent element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).</span></span>  

<span data-ttu-id="cab77-164">Attributs :</span><span class="sxs-lookup"><span data-stu-id="cab77-164">Attributes:</span></span>  

|<span data-ttu-id="cab77-165">Attribut</span><span class="sxs-lookup"><span data-stu-id="cab77-165">Attribute</span></span>|<span data-ttu-id="cab77-166">Type</span><span class="sxs-lookup"><span data-stu-id="cab77-166">Type</span></span>|<span data-ttu-id="cab77-167">Description</span><span class="sxs-lookup"><span data-stu-id="cab77-167">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="cab77-168">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="cab77-168">**bufferQuotaInMB**</span></span>|<span data-ttu-id="cab77-169">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="cab77-169">unsignedInt</span></span>|<span data-ttu-id="cab77-170">facultatif.</span><span class="sxs-lookup"><span data-stu-id="cab77-170">Optional.</span></span> <span data-ttu-id="cab77-171">Spécifie la quantité maximale de hello du stockage de système de fichiers est disponible pour hello spécifié données.</span><span class="sxs-lookup"><span data-stu-id="cab77-171">Specifies hello maximum amount of file system storage that is available for hello specified data.</span></span><br /><br /> <span data-ttu-id="cab77-172">valeur par défaut Hello est 0.</span><span class="sxs-lookup"><span data-stu-id="cab77-172">hello default is 0.</span></span>|  
|<span data-ttu-id="cab77-173">**scheduledTransferLogLevelFilter**</span><span class="sxs-lookup"><span data-stu-id="cab77-173">**scheduledTransferLogLevelFilter**</span></span>|<span data-ttu-id="cab77-174">string</span><span class="sxs-lookup"><span data-stu-id="cab77-174">string</span></span>|<span data-ttu-id="cab77-175">facultatif.</span><span class="sxs-lookup"><span data-stu-id="cab77-175">Optional.</span></span> <span data-ttu-id="cab77-176">Spécifie le niveau de gravité minimal hello pour les entrées de journal sont transférées.</span><span class="sxs-lookup"><span data-stu-id="cab77-176">Specifies hello minimum severity level for log entries that are transferred.</span></span> <span data-ttu-id="cab77-177">la valeur par défaut Hello est **Undefined**.</span><span class="sxs-lookup"><span data-stu-id="cab77-177">hello default value is **Undefined**.</span></span> <span data-ttu-id="cab77-178">Les autres valeurs possibles sont **Détaillé**, **Informations**, **Avertissement**, **Erreur**, et **Critique**.</span><span class="sxs-lookup"><span data-stu-id="cab77-178">Other possible values are **Verbose**, **Information**, **Warning**, **Error**, and **Critical**.</span></span>|  
|<span data-ttu-id="cab77-179">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="cab77-179">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="cab77-180">duration</span><span class="sxs-lookup"><span data-stu-id="cab77-180">duration</span></span>|<span data-ttu-id="cab77-181">facultatif.</span><span class="sxs-lookup"><span data-stu-id="cab77-181">Optional.</span></span> <span data-ttu-id="cab77-182">Spécifie l’intervalle de salutation entre les transferts planifiés de données, arrondies à toohello minute la plus proche.</span><span class="sxs-lookup"><span data-stu-id="cab77-182">Specifies hello interval between scheduled transfers of data, rounded up toohello nearest minute.</span></span><br /><br /> <span data-ttu-id="cab77-183">valeur par défaut Hello est PT0S.</span><span class="sxs-lookup"><span data-stu-id="cab77-183">hello default is PT0S.</span></span>|  

## <a name="directories-element"></a><span data-ttu-id="cab77-184">Élément Directories</span><span class="sxs-lookup"><span data-stu-id="cab77-184">Directories Element</span></span>  
<span data-ttu-id="cab77-185">Définit la configuration du tampon hello pour les fichiers journaux que vous pouvez définir.</span><span class="sxs-lookup"><span data-stu-id="cab77-185">Defines hello buffer configuration for file-based logs that you can define.</span></span>

<span data-ttu-id="cab77-186">Élément parent : [Élément DiagnosticMonitorConfiguration](#DiagnosticMonitorConfiguration).</span><span class="sxs-lookup"><span data-stu-id="cab77-186">Parent element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).</span></span>  


<span data-ttu-id="cab77-187">Attributs :</span><span class="sxs-lookup"><span data-stu-id="cab77-187">Attributes:</span></span>  

|<span data-ttu-id="cab77-188">Attribut</span><span class="sxs-lookup"><span data-stu-id="cab77-188">Attribute</span></span>|<span data-ttu-id="cab77-189">Type</span><span class="sxs-lookup"><span data-stu-id="cab77-189">Type</span></span>|<span data-ttu-id="cab77-190">Description</span><span class="sxs-lookup"><span data-stu-id="cab77-190">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="cab77-191">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="cab77-191">**bufferQuotaInMB**</span></span>|<span data-ttu-id="cab77-192">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="cab77-192">unsignedInt</span></span>|<span data-ttu-id="cab77-193">facultatif.</span><span class="sxs-lookup"><span data-stu-id="cab77-193">Optional.</span></span> <span data-ttu-id="cab77-194">Spécifie la quantité maximale de hello du stockage de système de fichiers est disponible pour hello spécifié données.</span><span class="sxs-lookup"><span data-stu-id="cab77-194">Specifies hello maximum amount of file system storage that is available for hello specified data.</span></span><br /><br /> <span data-ttu-id="cab77-195">valeur par défaut Hello est 0.</span><span class="sxs-lookup"><span data-stu-id="cab77-195">hello default is 0.</span></span>|  
|<span data-ttu-id="cab77-196">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="cab77-196">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="cab77-197">duration</span><span class="sxs-lookup"><span data-stu-id="cab77-197">duration</span></span>|<span data-ttu-id="cab77-198">facultatif.</span><span class="sxs-lookup"><span data-stu-id="cab77-198">Optional.</span></span> <span data-ttu-id="cab77-199">Spécifie l’intervalle de salutation entre les transferts planifiés de données, arrondies à toohello minute la plus proche.</span><span class="sxs-lookup"><span data-stu-id="cab77-199">Specifies hello interval between scheduled transfers of data, rounded up toohello nearest minute.</span></span><br /><br /> <span data-ttu-id="cab77-200">valeur par défaut Hello est PT0S.</span><span class="sxs-lookup"><span data-stu-id="cab77-200">hello default is PT0S.</span></span>|  

## <a name="crashdumps-element"></a><span data-ttu-id="cab77-201">Élément CrashDumps</span><span class="sxs-lookup"><span data-stu-id="cab77-201">CrashDumps Element</span></span>  
 <span data-ttu-id="cab77-202">Définit le répertoire de vidages sur incident hello.</span><span class="sxs-lookup"><span data-stu-id="cab77-202">Defines hello crash dumps directory.</span></span>

 <span data-ttu-id="cab77-203">Élément parent : [élément Directories](#Directories).</span><span class="sxs-lookup"><span data-stu-id="cab77-203">Parent Element: [Directories Element](#Directories).</span></span>  

<span data-ttu-id="cab77-204">Attributs :</span><span class="sxs-lookup"><span data-stu-id="cab77-204">Attributes:</span></span>  

|<span data-ttu-id="cab77-205">Attribut</span><span class="sxs-lookup"><span data-stu-id="cab77-205">Attribute</span></span>|<span data-ttu-id="cab77-206">Type</span><span class="sxs-lookup"><span data-stu-id="cab77-206">Type</span></span>|<span data-ttu-id="cab77-207">Description</span><span class="sxs-lookup"><span data-stu-id="cab77-207">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="cab77-208">**container**</span><span class="sxs-lookup"><span data-stu-id="cab77-208">**container**</span></span>|<span data-ttu-id="cab77-209">string</span><span class="sxs-lookup"><span data-stu-id="cab77-209">string</span></span>|<span data-ttu-id="cab77-210">nom Hello du conteneur hello où contenu hello du répertoire de hello est toobe transféré.</span><span class="sxs-lookup"><span data-stu-id="cab77-210">hello name of hello container where hello contents of hello directory is toobe transferred.</span></span>|  
|<span data-ttu-id="cab77-211">**directoryQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="cab77-211">**directoryQuotaInMB**</span></span>|<span data-ttu-id="cab77-212">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="cab77-212">unsignedInt</span></span>|<span data-ttu-id="cab77-213">facultatif.</span><span class="sxs-lookup"><span data-stu-id="cab77-213">Optional.</span></span> <span data-ttu-id="cab77-214">Spécifie la taille maximale de hello du répertoire de hello en mégaoctets.</span><span class="sxs-lookup"><span data-stu-id="cab77-214">Specifies hello maximum size of hello directory in megabytes.</span></span><br /><br /> <span data-ttu-id="cab77-215">valeur par défaut Hello est 0.</span><span class="sxs-lookup"><span data-stu-id="cab77-215">hello default is 0.</span></span>|  

## <a name="failedrequestlogs-element"></a><span data-ttu-id="cab77-216">Élément FailedRequestLogs</span><span class="sxs-lookup"><span data-stu-id="cab77-216">FailedRequestLogs Element</span></span>  
 <span data-ttu-id="cab77-217">Définit le répertoire du journal des demandes ayant échoué hello.</span><span class="sxs-lookup"><span data-stu-id="cab77-217">Defines hello failed request log directory.</span></span>

 <span data-ttu-id="cab77-218">Élément parent : [élément Directories](#Directories).</span><span class="sxs-lookup"><span data-stu-id="cab77-218">Parent Element [Directories Element](#Directories).</span></span>  

<span data-ttu-id="cab77-219">Attributs :</span><span class="sxs-lookup"><span data-stu-id="cab77-219">Attributes:</span></span>  

|<span data-ttu-id="cab77-220">Attribut</span><span class="sxs-lookup"><span data-stu-id="cab77-220">Attribute</span></span>|<span data-ttu-id="cab77-221">Type</span><span class="sxs-lookup"><span data-stu-id="cab77-221">Type</span></span>|<span data-ttu-id="cab77-222">Description</span><span class="sxs-lookup"><span data-stu-id="cab77-222">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="cab77-223">**container**</span><span class="sxs-lookup"><span data-stu-id="cab77-223">**container**</span></span>|<span data-ttu-id="cab77-224">string</span><span class="sxs-lookup"><span data-stu-id="cab77-224">string</span></span>|<span data-ttu-id="cab77-225">nom Hello du conteneur hello où contenu hello du répertoire de hello est toobe transféré.</span><span class="sxs-lookup"><span data-stu-id="cab77-225">hello name of hello container where hello contents of hello directory is toobe transferred.</span></span>|  
|<span data-ttu-id="cab77-226">**directoryQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="cab77-226">**directoryQuotaInMB**</span></span>|<span data-ttu-id="cab77-227">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="cab77-227">unsignedInt</span></span>|<span data-ttu-id="cab77-228">facultatif.</span><span class="sxs-lookup"><span data-stu-id="cab77-228">Optional.</span></span> <span data-ttu-id="cab77-229">Spécifie la taille maximale de hello du répertoire de hello en mégaoctets.</span><span class="sxs-lookup"><span data-stu-id="cab77-229">Specifies hello maximum size of hello directory in megabytes.</span></span><br /><br /> <span data-ttu-id="cab77-230">valeur par défaut Hello est 0.</span><span class="sxs-lookup"><span data-stu-id="cab77-230">hello default is 0.</span></span>|  

##  <a name="iislogs-element"></a><span data-ttu-id="cab77-231">Élément IISLogs</span><span class="sxs-lookup"><span data-stu-id="cab77-231">IISLogs Element</span></span>  
 <span data-ttu-id="cab77-232">Définit le répertoire des journaux IIS hello.</span><span class="sxs-lookup"><span data-stu-id="cab77-232">Defines hello IIS log directory.</span></span>

 <span data-ttu-id="cab77-233">Élément parent : [élément Directories](#Directories).</span><span class="sxs-lookup"><span data-stu-id="cab77-233">Parent Element [Directories Element](#Directories).</span></span>  

<span data-ttu-id="cab77-234">Attributs :</span><span class="sxs-lookup"><span data-stu-id="cab77-234">Attributes:</span></span>  

|<span data-ttu-id="cab77-235">Attribut</span><span class="sxs-lookup"><span data-stu-id="cab77-235">Attribute</span></span>|<span data-ttu-id="cab77-236">Type</span><span class="sxs-lookup"><span data-stu-id="cab77-236">Type</span></span>|<span data-ttu-id="cab77-237">Description</span><span class="sxs-lookup"><span data-stu-id="cab77-237">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="cab77-238">**container**</span><span class="sxs-lookup"><span data-stu-id="cab77-238">**container**</span></span>|<span data-ttu-id="cab77-239">string</span><span class="sxs-lookup"><span data-stu-id="cab77-239">string</span></span>|<span data-ttu-id="cab77-240">nom Hello du conteneur hello où contenu hello du répertoire de hello est toobe transféré.</span><span class="sxs-lookup"><span data-stu-id="cab77-240">hello name of hello container where hello contents of hello directory is toobe transferred.</span></span>|  
|<span data-ttu-id="cab77-241">**directoryQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="cab77-241">**directoryQuotaInMB**</span></span>|<span data-ttu-id="cab77-242">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="cab77-242">unsignedInt</span></span>|<span data-ttu-id="cab77-243">facultatif.</span><span class="sxs-lookup"><span data-stu-id="cab77-243">Optional.</span></span> <span data-ttu-id="cab77-244">Spécifie la taille maximale de hello du répertoire de hello en mégaoctets.</span><span class="sxs-lookup"><span data-stu-id="cab77-244">Specifies hello maximum size of hello directory in megabytes.</span></span><br /><br /> <span data-ttu-id="cab77-245">valeur par défaut Hello est 0.</span><span class="sxs-lookup"><span data-stu-id="cab77-245">hello default is 0.</span></span>|  

## <a name="datasources-element"></a><span data-ttu-id="cab77-246">Élément DataSources</span><span class="sxs-lookup"><span data-stu-id="cab77-246">DataSources Element</span></span>  
 <span data-ttu-id="cab77-247">Définit zéro ou plusieurs répertoires de journaux supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="cab77-247">Defines zero or more additional log directories.</span></span>

 <span data-ttu-id="cab77-248">Élément parent : [élément Directories](#Directories).</span><span class="sxs-lookup"><span data-stu-id="cab77-248">Parent Element: [Directories Element](#Directories).</span></span>

## <a name="directoryconfiguration-element"></a><span data-ttu-id="cab77-249">Élément DirectoryConfiguration</span><span class="sxs-lookup"><span data-stu-id="cab77-249">DirectoryConfiguration Element</span></span>  
 <span data-ttu-id="cab77-250">Définit le répertoire hello de toomonitor des fichiers journaux.</span><span class="sxs-lookup"><span data-stu-id="cab77-250">Defines hello directory of log files toomonitor.</span></span>

 <span data-ttu-id="cab77-251">Élément parent : [élément DataSources](#DataSources).</span><span class="sxs-lookup"><span data-stu-id="cab77-251">Parent Element: [DataSources Element](#DataSources).</span></span>

<span data-ttu-id="cab77-252">Attributs :</span><span class="sxs-lookup"><span data-stu-id="cab77-252">Attributes:</span></span>

|<span data-ttu-id="cab77-253">Attribut</span><span class="sxs-lookup"><span data-stu-id="cab77-253">Attribute</span></span>|<span data-ttu-id="cab77-254">Type</span><span class="sxs-lookup"><span data-stu-id="cab77-254">Type</span></span>|<span data-ttu-id="cab77-255">Description</span><span class="sxs-lookup"><span data-stu-id="cab77-255">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="cab77-256">**container**</span><span class="sxs-lookup"><span data-stu-id="cab77-256">**container**</span></span>|<span data-ttu-id="cab77-257">string</span><span class="sxs-lookup"><span data-stu-id="cab77-257">string</span></span>|<span data-ttu-id="cab77-258">nom Hello du conteneur hello où contenu hello du répertoire de hello est toobe transféré.</span><span class="sxs-lookup"><span data-stu-id="cab77-258">hello name of hello container where hello contents of hello directory is toobe transferred.</span></span>|  
|<span data-ttu-id="cab77-259">**directoryQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="cab77-259">**directoryQuotaInMB**</span></span>|<span data-ttu-id="cab77-260">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="cab77-260">unsignedInt</span></span>|<span data-ttu-id="cab77-261">facultatif.</span><span class="sxs-lookup"><span data-stu-id="cab77-261">Optional.</span></span> <span data-ttu-id="cab77-262">Spécifie la taille maximale de hello du répertoire de hello en mégaoctets.</span><span class="sxs-lookup"><span data-stu-id="cab77-262">Specifies hello maximum size of hello directory in megabytes.</span></span><br /><br /> <span data-ttu-id="cab77-263">valeur par défaut Hello est 0.</span><span class="sxs-lookup"><span data-stu-id="cab77-263">hello default is 0.</span></span>|  

## <a name="absolute-element"></a><span data-ttu-id="cab77-264">Élément Absolute</span><span class="sxs-lookup"><span data-stu-id="cab77-264">Absolute Element</span></span>  
 <span data-ttu-id="cab77-265">Définit le chemin d’accès absolu de toomonitor de répertoire hello avec expansion d’environnement facultative.</span><span class="sxs-lookup"><span data-stu-id="cab77-265">Defines an absolute path of hello directory toomonitor with optional environment expansion.</span></span>

 <span data-ttu-id="cab77-266">Élément parent : [élément DirectoryConfiguration](#DirectoryConfiguration).</span><span class="sxs-lookup"><span data-stu-id="cab77-266">Parent Element: [DirectoryConfiguration Element](#DirectoryConfiguration).</span></span>  

<span data-ttu-id="cab77-267">Attributs :</span><span class="sxs-lookup"><span data-stu-id="cab77-267">Attributes:</span></span>  

|<span data-ttu-id="cab77-268">Attribut</span><span class="sxs-lookup"><span data-stu-id="cab77-268">Attribute</span></span>|<span data-ttu-id="cab77-269">Type</span><span class="sxs-lookup"><span data-stu-id="cab77-269">Type</span></span>|<span data-ttu-id="cab77-270">Description</span><span class="sxs-lookup"><span data-stu-id="cab77-270">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="cab77-271">**path**</span><span class="sxs-lookup"><span data-stu-id="cab77-271">**path**</span></span>|<span data-ttu-id="cab77-272">string</span><span class="sxs-lookup"><span data-stu-id="cab77-272">string</span></span>|<span data-ttu-id="cab77-273">Obligatoire.</span><span class="sxs-lookup"><span data-stu-id="cab77-273">Required.</span></span> <span data-ttu-id="cab77-274">Bonjour toomonitor de répertoire toohello de chemin d’accès absolu.</span><span class="sxs-lookup"><span data-stu-id="cab77-274">hello absolute path toohello directory toomonitor.</span></span>|  
|<span data-ttu-id="cab77-275">**expandEnvironment**</span><span class="sxs-lookup"><span data-stu-id="cab77-275">**expandEnvironment**</span></span>|<span data-ttu-id="cab77-276">booléenne</span><span class="sxs-lookup"><span data-stu-id="cab77-276">boolean</span></span>|<span data-ttu-id="cab77-277">Obligatoire.</span><span class="sxs-lookup"><span data-stu-id="cab77-277">Required.</span></span> <span data-ttu-id="cab77-278">Si défini trop**true**, variables d’environnement dans le chemin d’accès de hello sont développées.</span><span class="sxs-lookup"><span data-stu-id="cab77-278">If set too**true**, environment variables in hello path are expanded.</span></span>|  

## <a name="localresource-element"></a><span data-ttu-id="cab77-279">Élément LocalResource</span><span class="sxs-lookup"><span data-stu-id="cab77-279">LocalResource Element</span></span>  
 <span data-ttu-id="cab77-280">Définit une ressource locale à chemin d’accès relatif tooa définie dans la définition de service hello.</span><span class="sxs-lookup"><span data-stu-id="cab77-280">Defines a path relative tooa local resource defined in hello service definition.</span></span>

 <span data-ttu-id="cab77-281">Élément parent : [élément DirectoryConfiguration](#DirectoryConfiguration).</span><span class="sxs-lookup"><span data-stu-id="cab77-281">Parent Element: [DirectoryConfiguration Element](#DirectoryConfiguration).</span></span>  

<span data-ttu-id="cab77-282">Attributs :</span><span class="sxs-lookup"><span data-stu-id="cab77-282">Attributes:</span></span>  

|<span data-ttu-id="cab77-283">Attribut</span><span class="sxs-lookup"><span data-stu-id="cab77-283">Attribute</span></span>|<span data-ttu-id="cab77-284">Type</span><span class="sxs-lookup"><span data-stu-id="cab77-284">Type</span></span>|<span data-ttu-id="cab77-285">Description</span><span class="sxs-lookup"><span data-stu-id="cab77-285">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="cab77-286">**name**</span><span class="sxs-lookup"><span data-stu-id="cab77-286">**name**</span></span>|<span data-ttu-id="cab77-287">string</span><span class="sxs-lookup"><span data-stu-id="cab77-287">string</span></span>|<span data-ttu-id="cab77-288">Obligatoire.</span><span class="sxs-lookup"><span data-stu-id="cab77-288">Required.</span></span> <span data-ttu-id="cab77-289">nom Hello de ressource locale hello contenant hello Active toomonitor.</span><span class="sxs-lookup"><span data-stu-id="cab77-289">hello name of hello local resource that contains hello directory toomonitor.</span></span>|  
|<span data-ttu-id="cab77-290">**relativePath**</span><span class="sxs-lookup"><span data-stu-id="cab77-290">**relativePath**</span></span>|<span data-ttu-id="cab77-291">string</span><span class="sxs-lookup"><span data-stu-id="cab77-291">string</span></span>|<span data-ttu-id="cab77-292">Obligatoire.</span><span class="sxs-lookup"><span data-stu-id="cab77-292">Required.</span></span> <span data-ttu-id="cab77-293">Bonjour toomonitor de chemin d’accès relatif toohello ressource locale.</span><span class="sxs-lookup"><span data-stu-id="cab77-293">hello path relative toohello local resource toomonitor.</span></span>|  

## <a name="performancecounters-element"></a><span data-ttu-id="cab77-294">Élément PerformanceCounters</span><span class="sxs-lookup"><span data-stu-id="cab77-294">PerformanceCounters Element</span></span>  
 <span data-ttu-id="cab77-295">Définit toocollect de compteur des performances hello chemin d’accès toohello.</span><span class="sxs-lookup"><span data-stu-id="cab77-295">Defines hello path toohello performance counter toocollect.</span></span>

 <span data-ttu-id="cab77-296">Élément parent : [Élément DiagnosticMonitorConfiguration](#DiagnosticMonitorConfiguration).</span><span class="sxs-lookup"><span data-stu-id="cab77-296">Parent Element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).</span></span>


 <span data-ttu-id="cab77-297">Attributs :</span><span class="sxs-lookup"><span data-stu-id="cab77-297">Attributes:</span></span>  

|<span data-ttu-id="cab77-298">Attribut</span><span class="sxs-lookup"><span data-stu-id="cab77-298">Attribute</span></span>|<span data-ttu-id="cab77-299">Type</span><span class="sxs-lookup"><span data-stu-id="cab77-299">Type</span></span>|<span data-ttu-id="cab77-300">Description</span><span class="sxs-lookup"><span data-stu-id="cab77-300">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="cab77-301">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="cab77-301">**bufferQuotaInMB**</span></span>|<span data-ttu-id="cab77-302">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="cab77-302">unsignedInt</span></span>|<span data-ttu-id="cab77-303">facultatif.</span><span class="sxs-lookup"><span data-stu-id="cab77-303">Optional.</span></span> <span data-ttu-id="cab77-304">Spécifie la quantité maximale de hello du stockage de système de fichiers est disponible pour hello spécifié données.</span><span class="sxs-lookup"><span data-stu-id="cab77-304">Specifies hello maximum amount of file system storage that is available for hello specified data.</span></span><br /><br /> <span data-ttu-id="cab77-305">valeur par défaut Hello est 0.</span><span class="sxs-lookup"><span data-stu-id="cab77-305">hello default is 0.</span></span>|  
|<span data-ttu-id="cab77-306">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="cab77-306">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="cab77-307">duration</span><span class="sxs-lookup"><span data-stu-id="cab77-307">duration</span></span>|<span data-ttu-id="cab77-308">facultatif.</span><span class="sxs-lookup"><span data-stu-id="cab77-308">Optional.</span></span> <span data-ttu-id="cab77-309">Spécifie l’intervalle de salutation entre les transferts planifiés de données, arrondies à toohello minute la plus proche.</span><span class="sxs-lookup"><span data-stu-id="cab77-309">Specifies hello interval between scheduled transfers of data, rounded up toohello nearest minute.</span></span><br /><br /> <span data-ttu-id="cab77-310">valeur par défaut Hello est PT0S.</span><span class="sxs-lookup"><span data-stu-id="cab77-310">hello default is PT0S.</span></span>|  

## <a name="performancecounterconfiguration-element"></a><span data-ttu-id="cab77-311">Élément PerformanceCounterConfiguration</span><span class="sxs-lookup"><span data-stu-id="cab77-311">PerformanceCounterConfiguration Element</span></span>  
 <span data-ttu-id="cab77-312">Définit toocollect de compteur de performances hello.</span><span class="sxs-lookup"><span data-stu-id="cab77-312">Defines hello performance counter toocollect.</span></span>

 <span data-ttu-id="cab77-313">Élément parent : [élément PerformanceCounters](#PerformanceCounters).</span><span class="sxs-lookup"><span data-stu-id="cab77-313">Parent Element: [PerformanceCounters Element](#PerformanceCounters).</span></span>  

 <span data-ttu-id="cab77-314">Attributs :</span><span class="sxs-lookup"><span data-stu-id="cab77-314">Attributes:</span></span>  

|<span data-ttu-id="cab77-315">Attribut</span><span class="sxs-lookup"><span data-stu-id="cab77-315">Attribute</span></span>|<span data-ttu-id="cab77-316">Type</span><span class="sxs-lookup"><span data-stu-id="cab77-316">Type</span></span>|<span data-ttu-id="cab77-317">Description</span><span class="sxs-lookup"><span data-stu-id="cab77-317">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="cab77-318">**counterSpecifier**</span><span class="sxs-lookup"><span data-stu-id="cab77-318">**counterSpecifier**</span></span>|<span data-ttu-id="cab77-319">string</span><span class="sxs-lookup"><span data-stu-id="cab77-319">string</span></span>|<span data-ttu-id="cab77-320">Obligatoire.</span><span class="sxs-lookup"><span data-stu-id="cab77-320">Required.</span></span> <span data-ttu-id="cab77-321">toocollect du compteur de performances de toohello Hello chemin d’accès.</span><span class="sxs-lookup"><span data-stu-id="cab77-321">hello path toohello performance counter toocollect.</span></span>|  
|<span data-ttu-id="cab77-322">**sampleRate**</span><span class="sxs-lookup"><span data-stu-id="cab77-322">**sampleRate**</span></span>|<span data-ttu-id="cab77-323">duration</span><span class="sxs-lookup"><span data-stu-id="cab77-323">duration</span></span>|<span data-ttu-id="cab77-324">Obligatoire.</span><span class="sxs-lookup"><span data-stu-id="cab77-324">Required.</span></span> <span data-ttu-id="cab77-325">taux de Hello à quels hello compteur de performances doit être collecté.</span><span class="sxs-lookup"><span data-stu-id="cab77-325">hello rate at which hello performance counter should be collected.</span></span>|  

## <a name="windowseventlog-element"></a><span data-ttu-id="cab77-326">Élément WindowsEventLog</span><span class="sxs-lookup"><span data-stu-id="cab77-326">WindowsEventLog Element</span></span>  
 <span data-ttu-id="cab77-327">Définit toomonitor de journaux des événements hello.</span><span class="sxs-lookup"><span data-stu-id="cab77-327">Defines hello event logs toomonitor.</span></span>

 <span data-ttu-id="cab77-328">Élément parent : [Élément DiagnosticMonitorConfiguration](#DiagnosticMonitorConfiguration).</span><span class="sxs-lookup"><span data-stu-id="cab77-328">Parent Element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).</span></span>

  <span data-ttu-id="cab77-329">Attributs :</span><span class="sxs-lookup"><span data-stu-id="cab77-329">Attributes:</span></span>

|<span data-ttu-id="cab77-330">Attribut</span><span class="sxs-lookup"><span data-stu-id="cab77-330">Attribute</span></span>|<span data-ttu-id="cab77-331">Type</span><span class="sxs-lookup"><span data-stu-id="cab77-331">Type</span></span>|<span data-ttu-id="cab77-332">Description</span><span class="sxs-lookup"><span data-stu-id="cab77-332">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="cab77-333">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="cab77-333">**bufferQuotaInMB**</span></span>|<span data-ttu-id="cab77-334">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="cab77-334">unsignedInt</span></span>|<span data-ttu-id="cab77-335">facultatif.</span><span class="sxs-lookup"><span data-stu-id="cab77-335">Optional.</span></span> <span data-ttu-id="cab77-336">Spécifie la quantité maximale de hello du stockage de système de fichiers est disponible pour hello spécifié données.</span><span class="sxs-lookup"><span data-stu-id="cab77-336">Specifies hello maximum amount of file system storage that is available for hello specified data.</span></span><br /><br /> <span data-ttu-id="cab77-337">valeur par défaut Hello est 0.</span><span class="sxs-lookup"><span data-stu-id="cab77-337">hello default is 0.</span></span>|  
|<span data-ttu-id="cab77-338">**scheduledTransferLogLevelFilter**</span><span class="sxs-lookup"><span data-stu-id="cab77-338">**scheduledTransferLogLevelFilter**</span></span>|<span data-ttu-id="cab77-339">string</span><span class="sxs-lookup"><span data-stu-id="cab77-339">string</span></span>|<span data-ttu-id="cab77-340">facultatif.</span><span class="sxs-lookup"><span data-stu-id="cab77-340">Optional.</span></span> <span data-ttu-id="cab77-341">Spécifie le niveau de gravité minimal hello pour les entrées de journal sont transférées.</span><span class="sxs-lookup"><span data-stu-id="cab77-341">Specifies hello minimum severity level for log entries that are transferred.</span></span> <span data-ttu-id="cab77-342">la valeur par défaut Hello est **Undefined**.</span><span class="sxs-lookup"><span data-stu-id="cab77-342">hello default value is **Undefined**.</span></span> <span data-ttu-id="cab77-343">Les autres valeurs possibles sont **Détaillé**, **Informations**, **Avertissement**, **Erreur**, et **Critique**.</span><span class="sxs-lookup"><span data-stu-id="cab77-343">Other possible values are **Verbose**, **Information**, **Warning**, **Error**, and **Critical**.</span></span>|  
|<span data-ttu-id="cab77-344">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="cab77-344">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="cab77-345">duration</span><span class="sxs-lookup"><span data-stu-id="cab77-345">duration</span></span>|<span data-ttu-id="cab77-346">facultatif.</span><span class="sxs-lookup"><span data-stu-id="cab77-346">Optional.</span></span> <span data-ttu-id="cab77-347">Spécifie l’intervalle de salutation entre les transferts planifiés de données, arrondies à toohello minute la plus proche.</span><span class="sxs-lookup"><span data-stu-id="cab77-347">Specifies hello interval between scheduled transfers of data, rounded up toohello nearest minute.</span></span><br /><br /> <span data-ttu-id="cab77-348">valeur par défaut Hello est PT0S.</span><span class="sxs-lookup"><span data-stu-id="cab77-348">hello default is PT0S.</span></span>|  

## <a name="datasource-element"></a><span data-ttu-id="cab77-349">Élément DataSource</span><span class="sxs-lookup"><span data-stu-id="cab77-349">DataSource Element</span></span>  
 <span data-ttu-id="cab77-350">Définit toomonitor du journal des événements hello.</span><span class="sxs-lookup"><span data-stu-id="cab77-350">Defines hello event log toomonitor.</span></span>

 <span data-ttu-id="cab77-351">Élément parent : [élément WindowsEventLog](#windowsEventLog).</span><span class="sxs-lookup"><span data-stu-id="cab77-351">Parent Element: [WindowsEventLog Element](#windowsEventLog).</span></span>  

 <span data-ttu-id="cab77-352">Attributs :</span><span class="sxs-lookup"><span data-stu-id="cab77-352">Attributes:</span></span>

|<span data-ttu-id="cab77-353">Attribut</span><span class="sxs-lookup"><span data-stu-id="cab77-353">Attribute</span></span>|<span data-ttu-id="cab77-354">Type</span><span class="sxs-lookup"><span data-stu-id="cab77-354">Type</span></span>|<span data-ttu-id="cab77-355">Description</span><span class="sxs-lookup"><span data-stu-id="cab77-355">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="cab77-356">**name**</span><span class="sxs-lookup"><span data-stu-id="cab77-356">**name**</span></span>|<span data-ttu-id="cab77-357">string</span><span class="sxs-lookup"><span data-stu-id="cab77-357">string</span></span>|<span data-ttu-id="cab77-358">Obligatoire.</span><span class="sxs-lookup"><span data-stu-id="cab77-358">Required.</span></span> <span data-ttu-id="cab77-359">Une expression XPath spécifiant hello journal toocollect.</span><span class="sxs-lookup"><span data-stu-id="cab77-359">An XPath expression specifying hello log toocollect.</span></span>|  
