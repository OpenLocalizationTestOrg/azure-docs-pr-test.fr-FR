---
title: aaaDiagnostics dans la pile de Azure | Documents Microsoft
description: "Fonctionnement des fichiers de journal de toocollect pour obtenir des diagnostics dans la pile d’Azure"
services: azure-stack
documentationcenter: 
author: adshar
manager: 
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: adshar
ms.openlocfilehash: a4a5ddf29e75df710e9fae366d6ac16e6fb36d8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-stack-diagnostics-tools"></a><span data-ttu-id="1e0c1-103">Outils de diagnostics Azure Stack</span><span class="sxs-lookup"><span data-stu-id="1e0c1-103">Azure Stack diagnostics tools</span></span>
 
<span data-ttu-id="1e0c1-104">Azure Stack est une grande collection de composants qui fonctionnent ensemble et interagissent.</span><span class="sxs-lookup"><span data-stu-id="1e0c1-104">Azure Stack is a large collection of components working together and interacting with each other.</span></span> <span data-ttu-id="1e0c1-105">Tous ces composants génèrent leurs propres journaux uniques, ce qui signifie que diagnostiquer les problèmes peut rapidement devenir une tâche difficile, en particulier pour les erreurs provenant de plusieurs composants Azure Stack qui interagissent.</span><span class="sxs-lookup"><span data-stu-id="1e0c1-105">All these components  generate their own unique logs, which means that diagnosing issues can quickly become a challenging task, especially for errors coming from multiple interacting Azure Stack components.</span></span> 

<span data-ttu-id="1e0c1-106">Nos outils de diagnostic vous assurer mécanisme de collecte de journal hello est facile et efficace.</span><span class="sxs-lookup"><span data-stu-id="1e0c1-106">Our diagnostics tools help make sure hello log collection mechanism is easy and efficient.</span></span> <span data-ttu-id="1e0c1-107">Hello diagramme suivant affiche comment ouvrir une session outils de collecte dans le travail de la pile de Azure :</span><span class="sxs-lookup"><span data-stu-id="1e0c1-107">hello following diagram shows how log collection tools in Azure Stack work:</span></span>

![Outils de collecte de journaux](media/azure-stack-diagnostics/image01.png)
 
 
## <a name="trace-collector"></a><span data-ttu-id="1e0c1-109">Collecteur de traces</span><span class="sxs-lookup"><span data-stu-id="1e0c1-109">Trace Collector</span></span>
 
<span data-ttu-id="1e0c1-110">le collecteur de traces de Hello est activée par défaut.</span><span class="sxs-lookup"><span data-stu-id="1e0c1-110">hello Trace Collector is enabled by default.</span></span> <span data-ttu-id="1e0c1-111">Il continue s’exécute en arrière-plan de hello et collecte tous les journaux de suivi d’événements pour Windows (ETW) à partir des services de composants sur la pile d’Azure et les stocke sur un partage local commun.</span><span class="sxs-lookup"><span data-stu-id="1e0c1-111">It continuously runs in hello background and collects all Event Tracing for Windows (ETW) logs from component services on Azure Stack and stores them on a common local share.</span></span> 

<span data-ttu-id="1e0c1-112">Hello Voici tooknow points importants sur hello le collecteur de traces :</span><span class="sxs-lookup"><span data-stu-id="1e0c1-112">hello following are important things tooknow about hello Trace Collector:</span></span>
 
* <span data-ttu-id="1e0c1-113">le collecteur de traces de Hello s’exécute en permanence avec les limites de taille par défaut.</span><span class="sxs-lookup"><span data-stu-id="1e0c1-113">hello Trace Collector runs continuously with default size limits.</span></span> <span data-ttu-id="1e0c1-114">taille maximale par défaut est autorisée pour chaque fichier (200 Mo) est de Hello **pas** une taille limite.</span><span class="sxs-lookup"><span data-stu-id="1e0c1-114">hello default maximum size allowed for each file (200 MB) is **not** a cutoff size.</span></span> <span data-ttu-id="1e0c1-115">Une vérification de la taille se produit régulièrement (actuellement toutes les 10 minutes) et si le fichier en cours de hello est > = 200 Mo, il est enregistré et un nouveau fichier est généré.</span><span class="sxs-lookup"><span data-stu-id="1e0c1-115">A size check occurs periodically (currently every 10 minutes) and if hello current file is >= 200 MB, it is saved and a new file is generated.</span></span> <span data-ttu-id="1e0c1-116">Il existe également une limite de 8 Go (configurable) sur hello taille totale du fichier généré par la session d’événements.</span><span class="sxs-lookup"><span data-stu-id="1e0c1-116">There is also an 8 GB (configurable) limit on hello total file size generated per event session.</span></span> <span data-ttu-id="1e0c1-117">Une fois cette limite est atteinte, les fichiers les plus anciens hello sont supprimés comme de nouveaux fichiers sont créés.</span><span class="sxs-lookup"><span data-stu-id="1e0c1-117">Once this limit is reached, hello oldest files are deleted as new ones are created.</span></span>
* <span data-ttu-id="1e0c1-118">Il existe une limite d’âge de 5 jours sur les journaux de hello.</span><span class="sxs-lookup"><span data-stu-id="1e0c1-118">There is a 5-day age limit on hello logs.</span></span> <span data-ttu-id="1e0c1-119">Cette limite est également configurable.</span><span class="sxs-lookup"><span data-stu-id="1e0c1-119">This limit is also configurable.</span></span> 
* <span data-ttu-id="1e0c1-120">Chaque composant définit les propriétés de configuration de trace hello via un fichier JSON.</span><span class="sxs-lookup"><span data-stu-id="1e0c1-120">Each component defines hello trace configuration properties through a JSON file.</span></span> <span data-ttu-id="1e0c1-121">Hello JSON fichiers sont stockés dans `C:\TraceCollector\Configuration`.</span><span class="sxs-lookup"><span data-stu-id="1e0c1-121">hello JSON files are stored in `C:\TraceCollector\Configuration`.</span></span> <span data-ttu-id="1e0c1-122">Si nécessaire, ces fichiers peuvent être modifiés toochange hello taille limites d’âge et de hello collecte des journaux.</span><span class="sxs-lookup"><span data-stu-id="1e0c1-122">If necessary, these files can be edited toochange hello age and size limits of hello collected logs.</span></span> <span data-ttu-id="1e0c1-123">Modifications toothese fichiers nécessitent un redémarrage de hello *le collecteur de traces de pile de Microsoft Azure* service pour hello modifie tootake effet.</span><span class="sxs-lookup"><span data-stu-id="1e0c1-123">Changes toothese files require a restart of hello *Microsoft Azure Stack Trace Collector* service for hello changes tootake effect.</span></span>
* <span data-ttu-id="1e0c1-124">Hello exemple suivant est un fichier de JSON de la configuration de trace pour les opérations de FabricRingServices de hello XRP VM :</span><span class="sxs-lookup"><span data-stu-id="1e0c1-124">hello following example is a trace configuration JSON file for FabricRingServices Operations from hello XRP VM:</span></span> 

```
{
    "LogFile": 
    {
        "SessionName": "FabricRingServicesOperationsLogSession",
        "FileName": "\\\\SU1FileServer\\SU1_ManagementLibrary_1\\Diagnostics\\FabricRingServices\\Operations\\AzureStack.Common.Infrastructure.Operations.etl",
        "RollTimeStamp": "00:00:00",
        "MaxDaysOfFiles": "5",
        "MaxSizeInMB": "200",
        "TotalSizeInMB": "5120"
    },
    "EventSources":
    [
        {"Name": "Microsoft-AzureStack-Common-Infrastructure-ResourceManager" },
        {"Name": "Microsoft-OperationManager-EventSource" },
        {"Name": "Microsoft-Operation-EventSource" }
    ]
}
```

* <span data-ttu-id="1e0c1-125">**MaxDaysOfFiles**</span><span class="sxs-lookup"><span data-stu-id="1e0c1-125">**MaxDaysOfFiles**</span></span>

    <span data-ttu-id="1e0c1-126">Ce paramètre contrôle âge hello de tookeep de fichiers.</span><span class="sxs-lookup"><span data-stu-id="1e0c1-126">This parameter controls hello age of files tookeep.</span></span> <span data-ttu-id="1e0c1-127">Les fichiers journaux plus anciens sont supprimés.</span><span class="sxs-lookup"><span data-stu-id="1e0c1-127">Older log files are deleted.</span></span>
* <span data-ttu-id="1e0c1-128">**MaxSizeInMB**</span><span class="sxs-lookup"><span data-stu-id="1e0c1-128">**MaxSizeInMB**</span></span>

    <span data-ttu-id="1e0c1-129">Ce paramètre contrôle le seuil de taille hello pour un seul fichier.</span><span class="sxs-lookup"><span data-stu-id="1e0c1-129">This parameter controls hello size threshold for a single file.</span></span> <span data-ttu-id="1e0c1-130">Si la taille de hello est atteinte, un nouveau fichier .etl est créé.</span><span class="sxs-lookup"><span data-stu-id="1e0c1-130">If hello size is reached, a new .etl file is created.</span></span>
* <span data-ttu-id="1e0c1-131">**TotalSizeInMB**</span><span class="sxs-lookup"><span data-stu-id="1e0c1-131">**TotalSizeInMB**</span></span>

    <span data-ttu-id="1e0c1-132">Ce paramètre contrôle la taille totale de hello des fichiers .etl de hello généré à partir d’une session d’événements.</span><span class="sxs-lookup"><span data-stu-id="1e0c1-132">This parameter controls hello total size of hello .etl files generated from an event session.</span></span> <span data-ttu-id="1e0c1-133">Si la taille totale des fichiers de hello est supérieure à la valeur de ce paramètre, les fichiers plus anciens sont supprimés.</span><span class="sxs-lookup"><span data-stu-id="1e0c1-133">If hello total file size is greater than this parameter value, older files are deleted.</span></span>
  
## <a name="log-collection-tool"></a><span data-ttu-id="1e0c1-134">Outil de collecte de journaux</span><span class="sxs-lookup"><span data-stu-id="1e0c1-134">Log collection tool</span></span>
 
<span data-ttu-id="1e0c1-135">Hello de commande PowerShell `Get-AzureStackLog` peut être journaux toocollect utilisé à partir de tous les composants de hello dans un environnement de la pile de Azure.</span><span class="sxs-lookup"><span data-stu-id="1e0c1-135">hello PowerShell command `Get-AzureStackLog` can be used toocollect logs from all hello components  in an Azure Stack environment.</span></span> <span data-ttu-id="1e0c1-136">Elle les enregistre dans des fichiers zip à un emplacement défini par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="1e0c1-136">It saves them in zip files in a user defined location.</span></span> <span data-ttu-id="1e0c1-137">Si notre technique prennent en charge les besoins de l’équipe votre toohelp journaux résoudre un problème, ils peuvent vous demander toorun cet outil.</span><span class="sxs-lookup"><span data-stu-id="1e0c1-137">If our technical support team needs your logs toohelp troubleshoot an issue, they may ask you toorun this tool.</span></span>

> [!CAUTION]
> <span data-ttu-id="1e0c1-138">Ces fichiers journaux peuvent contenir des informations d’identification personnelle.</span><span class="sxs-lookup"><span data-stu-id="1e0c1-138">These log files may contain personally identifiable information (PII).</span></span> <span data-ttu-id="1e0c1-139">Pensez-y avant de publier des fichiers journaux publiquement.</span><span class="sxs-lookup"><span data-stu-id="1e0c1-139">Take this into account before you publicly post any log files.</span></span>
 
<span data-ttu-id="1e0c1-140">Actuellement, nous collectons hello les types de journaux suivants :</span><span class="sxs-lookup"><span data-stu-id="1e0c1-140">We currently collect hello following log types:</span></span>
*   <span data-ttu-id="1e0c1-141">**Journaux de déploiement Azure Stack**</span><span class="sxs-lookup"><span data-stu-id="1e0c1-141">**Azure Stack deployment logs**</span></span>
*   <span data-ttu-id="1e0c1-142">**Journaux des événements Windows**</span><span class="sxs-lookup"><span data-stu-id="1e0c1-142">**Windows event logs**</span></span>
*   <span data-ttu-id="1e0c1-143">**Journaux Panther**</span><span class="sxs-lookup"><span data-stu-id="1e0c1-143">**Panther logs**</span></span>

     <span data-ttu-id="1e0c1-144">problèmes de création de machine virtuelle tootroubleshoot.</span><span class="sxs-lookup"><span data-stu-id="1e0c1-144">tootroubleshoot VM creation issues.</span></span>
*   <span data-ttu-id="1e0c1-145">**Journaux de cluster**</span><span class="sxs-lookup"><span data-stu-id="1e0c1-145">**Cluster logs**</span></span>
*   <span data-ttu-id="1e0c1-146">**Journaux de diagnostics de stockage**</span><span class="sxs-lookup"><span data-stu-id="1e0c1-146">**Storage diagnostic logs**</span></span>
*   <span data-ttu-id="1e0c1-147">**Journaux ETW**</span><span class="sxs-lookup"><span data-stu-id="1e0c1-147">**ETW logs**</span></span>

    <span data-ttu-id="1e0c1-148">Celles-ci sont collectées par le collecteur de traces de hello et stockés dans un partage à partir de laquelle `Get-AzureStackLog` les récupère.</span><span class="sxs-lookup"><span data-stu-id="1e0c1-148">These are collected by hello Trace Collector and stored in a share from where `Get-AzureStackLog` retrieves them.</span></span>
 
<span data-ttu-id="1e0c1-149">tooidentify tous hello journaux sont collectés à partir de tous les composants de hello, consultez toohello `<Logs>` balises dans un fichier de configuration de client hello situé à `C:\EceStore\<Guid>\<GuidWithMaxFileSize>`.</span><span class="sxs-lookup"><span data-stu-id="1e0c1-149">tooidentify all hello logs that get collected from all hello components, refer toohello `<Logs>` tags in hello customer configuration file located at `C:\EceStore\<Guid>\<GuidWithMaxFileSize>`.</span></span>
 
### <a name="toorun-get-azurestacklog"></a><span data-ttu-id="1e0c1-150">toorun Get-AzureStackLog</span><span class="sxs-lookup"><span data-stu-id="1e0c1-150">toorun Get-AzureStackLog</span></span>
1.  <span data-ttu-id="1e0c1-151">Connectez-vous en tant que AzureStack\AzureStackAdmin sur l’ordinateur hôte de hello.</span><span class="sxs-lookup"><span data-stu-id="1e0c1-151">Log in as AzureStack\AzureStackAdmin on hello host.</span></span>
2.  <span data-ttu-id="1e0c1-152">Ouvrez une fenêtre PowerShell en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="1e0c1-152">Open a PowerShell window as an administrator.</span></span>
3.  <span data-ttu-id="1e0c1-153">Exécutez `Get-AzureStackLog`.</span><span class="sxs-lookup"><span data-stu-id="1e0c1-153">Run `Get-AzureStackLog`.</span></span>  

    <span data-ttu-id="1e0c1-154">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="1e0c1-154">**Examples**</span></span>

    - <span data-ttu-id="1e0c1-155">Collecter tous les journaux pour tous les rôles :</span><span class="sxs-lookup"><span data-stu-id="1e0c1-155">Collect all logs for all roles:</span></span>

        `Get-AzureStackLog -OutputPath C:\AzureStackLogs`

    - <span data-ttu-id="1e0c1-156">Collecter les journaux à partir des rôles VirtualMachines et BareMetal :</span><span class="sxs-lookup"><span data-stu-id="1e0c1-156">Collect logs from VirtualMachines and BareMetal roles:</span></span>

        `Get-AzureStackLog -OutputPath C:\AzureStackLogs -FilterByRole VirtualMachines,BareMetal`

    - <span data-ttu-id="1e0c1-157">Collecter les journaux à partir de rôles de machines virtuelles et BareMetal, avec la date de filtrage pour les fichiers journaux pour hello dernières heures 8 :</span><span class="sxs-lookup"><span data-stu-id="1e0c1-157">Collect logs from VirtualMachines and BareMetal roles, with date filtering for log files for hello past 8 hours:</span></span>

        `Get-AzureStackLog -OutputPath C:\AzureStackLogs -FilterByRole VirtualMachines,BareMetal -FromDate (Get-Date).AddHours(-8) -ToDate (Get-Date)`

<span data-ttu-id="1e0c1-158">Si hello `FromDate` et `ToDate` paramètres ne sont pas spécifiés, les journaux sont collectés pour hello passées de 4 heures par défaut.</span><span class="sxs-lookup"><span data-stu-id="1e0c1-158">If hello `FromDate` and `ToDate` parameters are not specified, logs are collected for hello past 4 hours by default.</span></span>

<span data-ttu-id="1e0c1-159">Actuellement, vous pouvez utiliser hello `FilterByRole` collecte de journaux paramètre toofilter par hello suivant des rôles :</span><span class="sxs-lookup"><span data-stu-id="1e0c1-159">Currently, you can use hello `FilterByRole` parameter toofilter log collection by hello following roles:</span></span>

|   |   |   |
| - | - | - |
| `ACSMigrationService`     | `ACSMonitoringService`   | `ACSSettingsService` |
| `ACS`                     | `ACSFabric`              | `ACSFrontEnd`        |
| `ACSTableMaster`          | `ACSTableServer`         | `ACSWac`             |
| `ADFS`                    | `ASAppGateway`           | `BareMetal`          |
| `BRP`                     | `CA`                     | `CPI`                |
| `CRP`                     | `DeploymentMachine`      | `DHCP`               |
|`Domain`                   | `ECE`                    | `ECESeedRing`        |        
| `FabricRing`              | `FabricRingServices`     | `FRP`                |
|` Gateway`                 | `HealthMonitoring`       | `HRP`                |               
| `IBC`                     | `InfraServiceController` | `KeyVaultAdminResourceProvider`|
| `KeyVaultControlPlane`    | `KeyVaultDataPlane`      | `NC`                 |            
| `NonPrivilegedAppGateway` | `NRP`                    | `SeedRing`           |
| `SeedRingServices`        | `SLB`                    | `SQL`                |     
| `SRP`                     | `Storage`                | `StorageController`  |
| `URP`                     | `UsageBridge`            | `VirtualMachines`    |  
| `WAS`                     | `WASPUBLIC`              | `WDS`                |


<span data-ttu-id="1e0c1-160">Quelques éléments toonote :</span><span class="sxs-lookup"><span data-stu-id="1e0c1-160">A few things toonote:</span></span>

* <span data-ttu-id="1e0c1-161">Cette commande de collecte de journaux prend un certain temps, en fonction des journaux de rôles qui sont recueillis.</span><span class="sxs-lookup"><span data-stu-id="1e0c1-161">This command takes some time for log collection based on which role logs are collected.</span></span> <span data-ttu-id="1e0c1-162">Facteurs incluent hello durée spécifiée pour la collecte de journaux et les nombres hello de nœuds dans un environnement de Azure pile hello.</span><span class="sxs-lookup"><span data-stu-id="1e0c1-162">Contributing factors include hello time duration specified for log collection, and hello numbers of nodes in hello Azure Stack environment.</span></span>
* <span data-ttu-id="1e0c1-163">Une fois la collecte de journaux est terminée, vérifiez hello nouveau dossier créé dans hello `-OutputPath` paramètre spécifié dans la commande hello.</span><span class="sxs-lookup"><span data-stu-id="1e0c1-163">After log collection completes, check hello new folder created in hello `-OutputPath` parameter specified in hello command.</span></span>
* <span data-ttu-id="1e0c1-164">Un fichier appelé `Get-AzureStackLog_Output.log` est créé dans le dossier hello contenant des fichiers zip hello et inclut la sortie de commande hello, qui peut être utilisé pour résoudre les erreurs dans la collection de journaux.</span><span class="sxs-lookup"><span data-stu-id="1e0c1-164">A file called `Get-AzureStackLog_Output.log` is created in hello folder containing hello zip files and includes hello command output, which can be used for troubleshooting any failures in log collection.</span></span>
* <span data-ttu-id="1e0c1-165">Les journaux de chaque rôle se trouvent à l’intérieur d’un fichier zip individuel.</span><span class="sxs-lookup"><span data-stu-id="1e0c1-165">Each role has its logs inside an individual zip file.</span></span> 
* <span data-ttu-id="1e0c1-166">tooinvestigate un échec spécifique, les journaux peuvent être nécessaires à partir de plusieurs composants.</span><span class="sxs-lookup"><span data-stu-id="1e0c1-166">tooinvestigate a specific failure, logs may be needed from more than one component.</span></span>
    -   <span data-ttu-id="1e0c1-167">Système et les journaux des événements pour tous les ordinateurs virtuels d’infrastructure sont collectés dans hello *machines virtuelles* rôle.</span><span class="sxs-lookup"><span data-stu-id="1e0c1-167">System and Event logs for all infrastructure VMs are collected in hello *VirtualMachines* role.</span></span>
    -   <span data-ttu-id="1e0c1-168">Système et les journaux des événements pour tous les hôtes sont collectés dans hello *BareMetal* rôle.</span><span class="sxs-lookup"><span data-stu-id="1e0c1-168">System and Event logs for all hosts are collected in hello *BareMetal* role.</span></span>
    -   <span data-ttu-id="1e0c1-169">Journaux des événements de Cluster de basculement et Hyper-V sont collectés dans hello *stockage* rôle.</span><span class="sxs-lookup"><span data-stu-id="1e0c1-169">Failover Cluster and Hyper-V event logs are collected in hello *Storage* role.</span></span>
    -   <span data-ttu-id="1e0c1-170">Les journaux des services ACS sont collectés dans hello *stockage* et *ACS* rôles.</span><span class="sxs-lookup"><span data-stu-id="1e0c1-170">ACS logs are collected in hello *Storage* and *ACS* roles.</span></span>
* <span data-ttu-id="1e0c1-171">Pour plus d’informations, vous pouvez consulter le fichier de configuration de client toohello.</span><span class="sxs-lookup"><span data-stu-id="1e0c1-171">For more details, you can refer toohello customer configuration file.</span></span> <span data-ttu-id="1e0c1-172">Examiner hello `<Logs>` des balises pour les différents rôles de hello.</span><span class="sxs-lookup"><span data-stu-id="1e0c1-172">Investigate hello `<Logs>` tags for hello different roles.</span></span>

> [!NOTE]
> <span data-ttu-id="1e0c1-173">Nous sommes en appliquant taille et âge limite toohello les journaux collectés comme il est essentiel tooensure une utilisation efficace de vos toomake d’espace de stockage que vous ne trouverez pas saturation des journaux des.</span><span class="sxs-lookup"><span data-stu-id="1e0c1-173">We are enforcing size and age limits toohello logs collected as it is essential tooensure efficient utilization of your storage space toomake sure it doesn't get flooded with logs.</span></span> <span data-ttu-id="1e0c1-174">Ceci dit, lorsque vous diagnostiquez un problème, que vous devez souvent les journaux n’existe peut-être plus en raison des limites de toothese appliquées.</span><span class="sxs-lookup"><span data-stu-id="1e0c1-174">Having said that, when diagnosing a problem you will often need logs that might not exist anymore due toothese limits being enforced.</span></span> <span data-ttu-id="1e0c1-175">Par conséquent, il est **hautement recommandé** que vous décharger de votre espace de stockage externe tooan journaux (un compte de stockage dans Azure publique, un périphérique de stockage local supplémentaires etc.) toutes les 8 heures too12 et les conserver pendant 1 à 3 mois en fonction de vos besoins.</span><span class="sxs-lookup"><span data-stu-id="1e0c1-175">Hence, it is **highly recommended** that you offload your logs tooan external storage space (a storage account in public Azure, an additional on-prem storage device etc.) every 8 too12 hours and keep them there for 1 - 3 months depending on your requirements.</span></span>


## <a name="next-steps"></a><span data-ttu-id="1e0c1-176">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1e0c1-176">Next steps</span></span>
[<span data-ttu-id="1e0c1-177">Dépannage de Microsoft Azure Stack</span><span class="sxs-lookup"><span data-stu-id="1e0c1-177">Microsoft Azure Stack troubleshooting</span></span>](azure-stack-troubleshooting.md)
