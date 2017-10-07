---
title: "aaaAssess des applications de Service Fabric avec Azure Analytique de journal à l’aide de PowerShell | Documents Microsoft"
description: "Vous pouvez utiliser la solution de Service Fabric hello dans Analytique de journal à l’aide de risque de hello tooassess PowerShell et l’intégrité de vos applications de Service Fabric, micro-services, nœuds de clusters."
services: log-analytics
documentationcenter: 
author: niniikhena
manager: jochan
editor: 
ms.assetid: 2047b3fa-96b1-4230-af5d-a4c331d973ce
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2017
ms.author: nini
ms.openlocfilehash: 3f6d6c0df02d6d453b77e50b75b64bf7eb73bbbf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="assess-azure-service-fabric-applications-and-micro-services-with-powershell"></a><span data-ttu-id="024c4-103">Évaluer les micro-services et applications Azure Service Fabric avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="024c4-103">Assess Azure Service Fabric applications and micro-services with PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="024c4-104">Gestionnaire de ressources</span><span class="sxs-lookup"><span data-stu-id="024c4-104">Resource Manager</span></span>](log-analytics-service-fabric-azure-resource-manager.md)
> * [<span data-ttu-id="024c4-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="024c4-105">PowerShell</span></span>](log-analytics-service-fabric.md)
>
>


![Symbole Service Fabric](./media/log-analytics-service-fabric/service-fabric-assessment-symbol.png)

<span data-ttu-id="024c4-107">Cet article décrit comment toouse hello solution de l’infrastructure de Service dans le journal Analytique toohelp identifier et résoudre les problèmes sur votre cluster Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="024c4-107">This article describes how toouse hello Service Fabric solution in Log Analytics toohelp identify and troubleshoot issues across your Service Fabric cluster.</span></span> <span data-ttu-id="024c4-108">Il vous permet de voir les performances de vos nœuds Service Fabric et l’exécution de vos applications et micro-services.</span><span class="sxs-lookup"><span data-stu-id="024c4-108">It helps you see how your Service Fabric nodes are performing and how your applications and micro-services are running.</span></span>

<span data-ttu-id="024c4-109">Hello solution d’infrastructure de Service utilise des données de Diagnostics Windows Azure à partir de vos machines virtuelles de l’infrastructure Service, collecte des données de vos tables WAD d’Azure.</span><span class="sxs-lookup"><span data-stu-id="024c4-109">hello Service Fabric solution uses Azure Diagnostics data from your Service Fabric VMs, by collecting this data from your Azure WAD tables.</span></span> <span data-ttu-id="024c4-110">Analytique de journal lit ensuite hello suivant des événements de framework Service Fabric :</span><span class="sxs-lookup"><span data-stu-id="024c4-110">Log Analytics then reads hello following Service Fabric framework events:</span></span>

- <span data-ttu-id="024c4-111">**Événements Reliable Service**</span><span class="sxs-lookup"><span data-stu-id="024c4-111">**Reliable Service Events**</span></span>
- <span data-ttu-id="024c4-112">**Événements d’acteurs**</span><span class="sxs-lookup"><span data-stu-id="024c4-112">**Actor Events**</span></span>
- <span data-ttu-id="024c4-113">**Événements opérationnels**</span><span class="sxs-lookup"><span data-stu-id="024c4-113">**Operational Events**</span></span>
- <span data-ttu-id="024c4-114">**Événements ETW personnalisés**</span><span class="sxs-lookup"><span data-stu-id="024c4-114">**Custom ETW events**</span></span>

<span data-ttu-id="024c4-115">tableau de bord Hello Service Fabric solution montre les problèmes importants et les événements pertinents dans votre environnement de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="024c4-115">hello Service Fabric solution dashboard shows you notable issues and relevant events in your Service Fabric environment.</span></span>

## <a name="installing-and-configuring-hello-solution"></a><span data-ttu-id="024c4-116">L’installation et la configuration de solution de hello</span><span class="sxs-lookup"><span data-stu-id="024c4-116">Installing and configuring hello solution</span></span>
<span data-ttu-id="024c4-117">Suivez ces trois étapes tooinstall et configurer une solution de hello :</span><span class="sxs-lookup"><span data-stu-id="024c4-117">Follow these three easy steps tooinstall and configure hello solution:</span></span>

1. <span data-ttu-id="024c4-118">Associer hello abonnement Azure que vous avez utilisé toocreate toutes les ressources de cluster, y compris les comptes de stockage, avec votre espace de travail.</span><span class="sxs-lookup"><span data-stu-id="024c4-118">Associate hello Azure subscription that you used toocreate all cluster resources, including storage accounts, with your workspace.</span></span> <span data-ttu-id="024c4-119">Pour plus d’informations sur la création d’un espace de travail Log Analytics, consultez [Prise en main de Log Analytics](log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="024c4-119">See [Get started with Log Analytics](log-analytics-get-started.md) for information about creating a Log Analytics workspace.</span></span>
2. <span data-ttu-id="024c4-120">Configurer le journal Analytique toocollect et afficher les journaux de l’infrastructure de Service.</span><span class="sxs-lookup"><span data-stu-id="024c4-120">Configure Log Analytics toocollect and view Service Fabric logs.</span></span>
3. <span data-ttu-id="024c4-121">Activer la solution de Service Fabric hello dans votre espace de travail.</span><span class="sxs-lookup"><span data-stu-id="024c4-121">Enable hello Service Fabric solution in your workspace.</span></span>

## <a name="configure-log-analytics-toocollect-and-view-service-fabric-logs"></a><span data-ttu-id="024c4-122">Configurer le journal Analytique toocollect et afficher les journaux de l’infrastructure de Service</span><span class="sxs-lookup"><span data-stu-id="024c4-122">Configure Log Analytics toocollect and view Service Fabric logs</span></span>
<span data-ttu-id="024c4-123">Dans cette section, vous découvrez comment tooconfigure Analytique de journal tooretrieve Service Fabric se connecte.</span><span class="sxs-lookup"><span data-stu-id="024c4-123">In this section, you learn how tooconfigure Log Analytics tooretrieve Service Fabric logs.</span></span> <span data-ttu-id="024c4-124">Hello journaux vous permettent de tooview, analyser et résoudre les problèmes de votre cluster ou les applications hello et les services exécutés dans ce cluster, à l’aide du portail OMS hello.</span><span class="sxs-lookup"><span data-stu-id="024c4-124">hello logs allow you tooview, analyze, and troubleshoot issues in your cluster or in hello applications and services running in that cluster, using hello OMS portal.</span></span>

> [!NOTE]
> <span data-ttu-id="024c4-125">Configurer hello Azure Diagnostics tooupload hello des journaux d’extension pour les tables de stockage.</span><span class="sxs-lookup"><span data-stu-id="024c4-125">Configure hello Azure Diagnostics extension tooupload hello logs for storage tables.</span></span> <span data-ttu-id="024c4-126">les tables Hello doivent correspondre à ce que recherche Analytique de journal.</span><span class="sxs-lookup"><span data-stu-id="024c4-126">hello tables must match what Log Analytics looks for.</span></span> <span data-ttu-id="024c4-127">Pour plus d’informations, consultez [comment toocollect se connecte avec Azure Diagnostics](../service-fabric/service-fabric-diagnostics-how-to-setup-wad.md).</span><span class="sxs-lookup"><span data-stu-id="024c4-127">For more information, see [How toocollect logs with Azure Diagnostics](../service-fabric/service-fabric-diagnostics-how-to-setup-wad.md).</span></span> <span data-ttu-id="024c4-128">exemples de paramètres de configuration Hello dans cet article montrent les noms hello du stockage hello les tables doivent être.</span><span class="sxs-lookup"><span data-stu-id="024c4-128">hello configuration settings examples in this article show you what hello names of hello storage tables should be.</span></span> <span data-ttu-id="024c4-129">Une fois les Diagnostics est configuré sur le cluster de hello et télécharge le compte de stockage de journaux tooa, étape suivante de hello est tooconfigure Analytique de journal toocollect ces journaux.</span><span class="sxs-lookup"><span data-stu-id="024c4-129">Once Diagnostics is set up on hello cluster and is uploading logs tooa storage account, hello next step is tooconfigure Log Analytics toocollect these logs.</span></span>
>
>

<span data-ttu-id="024c4-130">Assurez-vous que vous mettez à jour hello **EtwEventSourceProviderConfiguration** section Bonjour **template.json** tooadd des entrées pour hello EventSources nouveau avant d’appliquer la configuration de hello mettre à jour par des fichiers en cours d’exécution **deploy.ps1**.</span><span class="sxs-lookup"><span data-stu-id="024c4-130">Ensure that you update hello **EtwEventSourceProviderConfiguration** section in hello **template.json** file tooadd entries for hello new EventSources before you apply hello configuration update by running **deploy.ps1**.</span></span> <span data-ttu-id="024c4-131">table de Hello pour le téléchargement est hello même en tant que (ETWEventTable).</span><span class="sxs-lookup"><span data-stu-id="024c4-131">hello table for upload is hello same as (ETWEventTable).</span></span> <span data-ttu-id="024c4-132">Au moment de hello, Analytique de journal peut uniquement lire événements ETW d’application hello *WADETWEventTable* table.</span><span class="sxs-lookup"><span data-stu-id="024c4-132">At hello moment, Log Analytics can only read application ETW events from hello *WADETWEventTable* table.</span></span>

<span data-ttu-id="024c4-133">Hello outils suivants sont utilisé tooperform certaines opérations hello dans cette section :</span><span class="sxs-lookup"><span data-stu-id="024c4-133">hello following tools are used tooperform some of hello operations in this section:</span></span>

* <span data-ttu-id="024c4-134">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="024c4-134">Azure PowerShell</span></span>
* [<span data-ttu-id="024c4-135">Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="024c4-135">Operations Management Suite</span></span>](http://www.microsoft.com/oms)

### <a name="configure-a-log-analytics-workspace-tooshow-hello-cluster-logs"></a><span data-ttu-id="024c4-136">Configurer un tooshow d’espace de travail Analytique de journal hello les journaux du cluster</span><span class="sxs-lookup"><span data-stu-id="024c4-136">Configure a Log Analytics workspace tooshow hello cluster logs</span></span>

<span data-ttu-id="024c4-137">Après avoir créé un espace de travail Analytique de journal, configurer des journaux de toopull d’espace de travail hello à partir des tables de stockage Azure hello.</span><span class="sxs-lookup"><span data-stu-id="024c4-137">After you create a Log Analytics workspace, configure hello workspace toopull logs from hello Azure storage tables.</span></span> <span data-ttu-id="024c4-138">Ensuite, exécutez hello PowerShell script suivant :</span><span class="sxs-lookup"><span data-stu-id="024c4-138">Then, run hello following PowerShell script:</span></span>

```
<#
    This script will configure an Operations Management Suite workspace (previously called an Operational Insights workspace) tooread Diagnostics from an Azure Storage account.
    It will enable all supported data types (currently Service Fabric Events, ETW Events and IIS Logs).
    It supports Resource Manager storage accounts.
    If you have more than one Azure Subscription, you will be prompted for hello subscription tooconfigure.
    If you have more than one Log Analytics workspace you will be prompted for hello workspace tooconfigure.
    It will then look through your Service Fabric clusters, and configure your Log Analytics workspace tooread Diagnostics from storage accounts that are connected toothat cluster and have diagnostics enabled.
#>

try
{
    Get-AzureRMContext
}
catch [System.Management.Automation.PSInvalidOperationException]
{
    Add-AzureRmAccount
}

$validTables = "WADServiceFabric*EventTable", "WADETWEventTable"
function Select-Subscription {
      $subscription = ""
      $allSubscriptions = Get-AzureRmSubscription
      switch ($allSubscriptions.Count) {
             0 {Write-Error "No Operations Management Suite workspaces found"}
             1 {return $allSubscriptions}
        default {
            $uiPrompt = "Enter hello number corresponding toohello Azure subscription you would like toowork with.`n"

            $count = 1
            foreach ($subscription in $allSubscriptions) {
                $uiPrompt += "$count. " + $subscription.Name + " (" + $subscription.Id + ")`n"
                $count++
            }
            $answer = (Read-Host -Prompt $uiPrompt) - 1
            $subscription = $allSubscriptions[$answer]
             Write-Host $subscription.Id
        }  
    }
    return $subscription
}

function Select-Workspace {
    $workspace = ""
    $allWorkspaces = Get-AzureRmOperationalInsightsWorkspace  

    switch ($allWorkspaces.Count) {
        0 {Write-Error "No Operations Management Suite workspaces found. `n"}
        1 {return $allWorkspaces}
        default {
            $uiPrompt = "Enter hello number corresponding toohello workspace you want tooconfigure.`n"
            $count = 1
            foreach ($workspace in $allWorkspaces) {
                $uiPrompt += "$count. " + $workspace.Name + " (" + $workspace.CustomerId + ")`n"
                $count++
            }
            $answer = (Read-Host -Prompt $uiPrompt) - 1
            $workspace = $allWorkspaces[$answer]
             Write-Host $workspace.WorkspaceName
        }  
    }
    return $workspace
}

function Check-ETWProviderLogging {
     param(
     [string]$id,
     [string]$provider,
     [string]$expectedTable,
     [string]$table
    )       
         Write-Debug ("ID: $id Provider: $provider ExpectedTable $expectedTable ActualTable $table")
         if ( ($table -eq $null) -or ($table -eq ""))  
         {
             Write-Warning ("$id No configuration found for $provider. Configure Azure diagnostics toowrite too$expectedTable.")
         }  
         elseif ( $table -ne $expectedTable )
         {
             Write-Warning ("$id $provider events are being written too$table instead of WAD$expectedTable. Events will not be collected by Log Analytics")
         }  
         else
         {
             Write-Verbose "$id $provider events are being written tooWAD$expectedTable (Correct configuration.)"
         }
 }

function Check-ServiceFabricScaleSetDiagnostics {
     param(
          [psobject]$scaleSetDiagnostics
   )
     $storageAccountsFound = @()
     Write-Verbose ("Checking " + $scaleSetDiagnostics)
     $sfReliableActorTable = $null
     $sfReliableServiceTable = $null
     $sfOperationalTable = $null

     Write-Debug $scaleSetDiagnostics
     $serviceFabricProviderList = ""
     $etwManifestProviderList = ""

     if ( $scaleSetDiagnostics.xmlCfg )  
      {
             Write-Debug ("Found XMLcfg")
             $xmlCfg = [System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String($scaleSetDiagnostics.xmlCfg))
             Write-Debug $xmlCfg
             $etwProviders = Select-Xml -Content $xmlCfg -XPath "//EtwProviders"                 
             $serviceFabricProviderList = $etwProviders.Node.EtwEventSourceProviderConfiguration
             $etwManifestProviderList = $etwProviders.Node.EtwManifestProviderConfiguration
      } elseif ($scaleSetDiagnostics.WadCfg )  
     {
         Write-Debug ("Found WADcfg")
         Write-Debug $scaleSetDiagnostics.WadCfg
         $serviceFabricProviderList = $scaleSetDiagnostics.WadCfg.DiagnosticMonitorConfiguration.EtwProviders.EtwEventSourceProviderConfiguration
         $etwManifestProviderList = $scaleSetDiagnostics.WadCfg.DiagnosticMonitorConfiguration.EtwProviders.EtwManifestProviderConfiguration
     } else
     {
         Write-Error "Unable tooparse Azure Diagnostics setting for $id"
             Write-Warning ("$id does not have diagnostics enabled")
     }
     foreach ($provider in $serviceFabricProviderList)  
     {
         Write-Debug ("Event Source Provider: " + $provider.Provider + " Destination: " + $provider.DefaultEvents.eventDestination)
         if ($provider.Provider -eq "Microsoft-ServiceFabric-Actors")
         {
             $sfReliableActorTable = $provider.DefaultEvents.eventDestination  
         } elseif ($provider.Provider -eq "Microsoft-ServiceFabric-Services")  
         {  
             $sfReliableServiceTable = $provider.DefaultEvents.eventDestination  
         } else  
         {
             Check-ETWProviderLogging $id $provider.Provider "ETWEventTable" $provider.DefaultEvents.eventDestination
         }
     }
     foreach ($provider in $etwManifestProviderList)
     {
         Write-Debug ("Manifest Provider: " + $provider.Provider + " Destination: " + $provider.DefaultEvents.eventDestination)
         if ($provider.Provider -eq "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8")
         {
             $sfOperationalTable = $provider.DefaultEvents.eventDestination  
         } else  
         {
             Check-ETWProviderLogging $id $provider.Provider "ETWEventTable" $provider.DefaultEvents.eventDestination
         }
     }

     Check-ETWProviderLogging $id "Microsoft-ServiceFabric-Actors" "ServiceFabricReliableActorEventTable" $sfReliableActorTable
     Check-ETWProviderLogging $id "Microsoft-ServiceFabric-Services" "ServiceFabricReliableServiceEventTable" $sfReliableServiceTable
     Check-ETWProviderLogging $id "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8 (System events)" "ServiceFabricSystemEventTable" $sfOperationalTable

     Write-Verbose ("StorageAccount: " + $scaleSetDiagnostics.StorageAccount)
     $storageAccountsFound += ($scaleSetDiagnostics.StorageAccount)
     return ($storageAccountsFound)
 }

function Select-StorageAccount {
    $allResources = Get-AzureRmResource #pulls in all resources
    $serviceFabricClusters = $allResources.Where({$_.ResourceType -eq "Microsoft.ServiceFabric/clusters"}) #pulls in all service fabric clusters in hello resource
    $storageAccountList = @()
    foreach($cluster in $serviceFabricClusters) {
        Write-Host("Checking cluster: " + $cluster.Name)
         $scaleSet = $allResources.Where({($_.ResourceType -eq "Microsoft.Compute/virtualMachineScaleSets") -and ($_.ResourceGroupName -eq $cluster.ResourceGroupName)})

         foreach($set in $scaleSet) {
             $resource = Get-AzureRmResource -ResourceId $set.ResourceId
             $extensions = $resource.Properties.VirtualMachineProfile.ExtensionProfile.Extensions

             foreach($ext in $extensions) {
                 if ($ext.Properties.Publisher -eq "Microsoft.Azure.Diagnostics" -and $ext.Properties.Type -eq "IaaSDiagnostics") {
                     $storageAccountList += (Check-ServiceFabricScaleSetDiagnostics $ext.Properties.Settings)
                 }
             }
          }

         $storageAccountsToCheck = $allResources.Where({($_.ResourceType -eq "Microsoft.Storage/storageAccounts") -and ($_.ResourceName -in $storageAccountList)})

         if ($storageAccountsToCheck.Count -eq "0") {
                Write-Error "No storage accounts found"
           }
           else {
                    foreach ($storageAccount in $storageAccountsToCheck) {
                        Write-Host("Checking Storage Account: " + $storageAccount.Name)
                        $insightsName = $storageAccount.Name + $workspace.Name
                        $existingConfig = ""
                        try
                            {
                                $existingConfig = Get-AzureRmOperationalInsightsStorageInsight -Workspace $workspace -Name $insightsName -ErrorAction Stop
                            }
                        catch
                            {
                                # HTTP Not Found is returned if hello storage insight doesn't exist
                            }
                        if ($existingConfig) {                         
                                  [array]$Tables = $existingConfig.Tables
                                   foreach($table in $validTables) {
                                         if($Tables -notcontains $table) {
                                               $Tables += $table
                                               $dirty = $true;
                                               Write-Host "Adding Table: $table";
                                         }
                                         else {
                                               Write-Host "$table is already configured.`n";
                                             }
                                      }
                                      # If any of hello tables from hello table list are not already monitored, then we add them
                                   if($dirty -eq $true) {
                                           Set-AzureRmOperationalInsightsStorageInsight -Workspace $workspace -Name $insightsName -Tables $Tables
                                           Write-Host "Updating Storage Insight. `n"
                                    }
                                    else {
                                           Write-Host "Storage Insight already updated."
                                  }
                          }
                     else {
                            $key = (Get-AzureRmStorageAccountKey -ResourceGroupName $storageAccount.ResourceGroupName -Name $storageAccount.Name)[0].Value
                           New-AzureRmOperationalInsightsStorageInsight -Workspace $workspace -Name $insightsName -StorageAccountResourceId $storageAccount.ResourceId -StorageAccountKey $key -Tables $validTables
                            Write-Host "New Azure Storage Insight Configured. `n"
                           }
                    }
             }
      }
      return
     }

$subscription = Select-Subscription
$subscriptionId = $subscription.SubscriptionId
$subscription = Select-AzureRmSubscription -SubscriptionId $subscriptionId
$workspace = Select-Workspace
$storageAccount = Select-StorageAccount
```

<span data-ttu-id="024c4-139">Après que vous avez configuré hello Analytique de journal espace de travail tooread hello Azure à partir de tables dans votre compte de stockage, connectez-vous toohello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="024c4-139">After you've configured hello Log Analytics workspace tooread from hello Azure tables in your storage account, log in toohello Azure portal.</span></span> <span data-ttu-id="024c4-140">Sélectionnez l’espace de travail hello Analytique de journal à partir de **toutes les ressources**.</span><span class="sxs-lookup"><span data-stu-id="024c4-140">Select hello Log Analytics workspace from **All Resources**.</span></span> <span data-ttu-id="024c4-141">nombre de Hello d’espace de travail toohello stockage compte journaux connectés est affiché.</span><span class="sxs-lookup"><span data-stu-id="024c4-141">hello number of storage account logs connected toohello workspace is displayed.</span></span> <span data-ttu-id="024c4-142">Sélectionnez hello **journaux de compte de stockage** vignette.</span><span class="sxs-lookup"><span data-stu-id="024c4-142">Select hello **Storage account logs** tile.</span></span> <span data-ttu-id="024c4-143">Passez en revue la liste hello de tooverify de journaux de compte de stockage que votre compte de stockage est connecté toohello espace de travail correct.</span><span class="sxs-lookup"><span data-stu-id="024c4-143">Review hello list of storage account logs tooverify that your storage account is connected toohello correct workspace.</span></span>

![Journaux de compte de stockage](./media/log-analytics-service-fabric/sf1.png)

## <a name="enable-hello-service-fabric-solution"></a><span data-ttu-id="024c4-145">Activer la solution de Service Fabric hello</span><span class="sxs-lookup"><span data-stu-id="024c4-145">Enable hello Service Fabric solution</span></span>
<span data-ttu-id="024c4-146">Utilisez hello suivant script tooadd hello solution tooyour Analytique de journal espace de travail.</span><span class="sxs-lookup"><span data-stu-id="024c4-146">Use hello following script tooadd hello solution tooyour Log Analytics workspace.</span></span> <span data-ttu-id="024c4-147">Exécuter le script de hello dans PowerShell, à l’aide de hello abonnement Azure qui est associé avec un espace de travail hello Analytique de journal que vous souhaitez des solutions de Service Fabric tooenable hello dans.</span><span class="sxs-lookup"><span data-stu-id="024c4-147">Run hello script in PowerShell, using hello Azure subscription that is associated with hello Log Analytics workspace that you want tooenable hello Service Fabric solution in.</span></span>

```
function Select-Subscription {
      $subscription = ""
      $allSubscriptions = Get-AzureRmSubscription
      switch ($allSubscriptions.Count) {
             0 {Write-Error "No Operations Management Suite workspaces found"}
             1 {return $allSubscriptions}
        default {
            $uiPrompt = "Enter hello number corresponding toohello Azure subscription you would like toowork with.`n"
            $count = 1
            foreach ($subscription in $allSubscriptions) {
                $uiPrompt += "$count. " + $subscription.SubscriptionName + " (" + $subscription.SubscriptionId + ")`n"
                $count++
            }
            $answer = (Read-Host -Prompt $uiPrompt) - 1
            $subscription = $allSubscriptions[$answer]
             Write-Host $subscription.SubscriptionId
        }  
    }
    return $subscription
}

function Select-Workspace {
    $workspace = ""
    $allWorkspaces = Get-AzureRmOperationalInsightsWorkspace  
    switch ($allWorkspaces.Count) {
        0 {Write-Error "No Operations Management Suite workspaces found"}
        1 {return $allWorkspaces}
        default {
            $uiPrompt = "Enter hello number corresponding toohello workspace you want tooconfigure.`n"
            $count = 1
            foreach ($workspace in $allWorkspaces) {
                $uiPrompt += "$count. " + $workspace.Name + " (" + $workspace.CustomerId + ")`n"
                $count++
            }
            $answer = (Read-Host -Prompt $uiPrompt) - 1
            $workspace = $allWorkspaces[$answer]
                           Write-Host $workspace.WorkspaceName
        }  
    }
    return $workspace
}
$subscription = Select-Subscription
$subscriptionId = $subscription.Id
$subscription = Select-AzureRmSubscription -SubscriptionId $subscriptionId
$workspace = Select-Workspace
Set-AzureRmOperationalInsightsIntelligencePack -ResourceGroupName $workspace.ResourceGroupName -WorkspaceName $workspace.Name -IntelligencePackName "ServiceFabric" -Enabled $true
```

<span data-ttu-id="024c4-148">Après avoir activé la solution de hello, vignette de Service Fabric hello est ajouté tooyour Analytique de journal *vue d’ensemble* page.</span><span class="sxs-lookup"><span data-stu-id="024c4-148">After you enable hello solution, hello Service Fabric tile is added tooyour Log Analytics *Overview* page.</span></span> <span data-ttu-id="024c4-149">page de Hello affiche une vue des problèmes importants, tels que les échecs de runAsync et les annulations hello lors des dernières 24 heures.</span><span class="sxs-lookup"><span data-stu-id="024c4-149">hello page shows a view of notable issues such as runAsync failures and cancellations that occurred in hello last 24 hours.</span></span>

![Vignette Service Fabric](./media/log-analytics-service-fabric/sf2.png)

### <a name="view-service-fabric-events"></a><span data-ttu-id="024c4-151">Afficher les événements Service Fabric</span><span class="sxs-lookup"><span data-stu-id="024c4-151">View Service Fabric events</span></span>
<span data-ttu-id="024c4-152">Cliquez sur hello **Service Fabric** vignette tooopen hello Service Fabric tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="024c4-152">Click hello **Service Fabric** tile tooopen hello Service Fabric dashboard.</span></span> <span data-ttu-id="024c4-153">tableau de bord Hello inclut des colonnes de hello dans la table hello qui suit.</span><span class="sxs-lookup"><span data-stu-id="024c4-153">hello dashboard includes hello columns in hello table that follows.</span></span> <span data-ttu-id="024c4-154">Chaque colonne répertorie les événements de 10 supérieure de hello en mettant en correspondance de nombre que les critères de la colonne pour hello spécifié de plage de temps.</span><span class="sxs-lookup"><span data-stu-id="024c4-154">Each column lists hello top 10 events by count matching that column's criteria for hello specified time range.</span></span> <span data-ttu-id="024c4-155">Vous pouvez exécuter une recherche de journal qui fournit l’intégralité de la liste hello en cliquant sur **afficher tous les** à hello droite en bas de chaque colonne, ou en cliquant sur en-tête de colonne hello.</span><span class="sxs-lookup"><span data-stu-id="024c4-155">You can run a log search that provides hello entire list by clicking **See all** at hello right bottom of each column, or by clicking hello column header.</span></span>

| <span data-ttu-id="024c4-156">**Événement Service Fabric**</span><span class="sxs-lookup"><span data-stu-id="024c4-156">**Service Fabric event**</span></span> | <span data-ttu-id="024c4-157">**description**</span><span class="sxs-lookup"><span data-stu-id="024c4-157">**description**</span></span> |
| --- | --- |
| <span data-ttu-id="024c4-158">Problèmes notables</span><span class="sxs-lookup"><span data-stu-id="024c4-158">Notable Issues</span></span> | <span data-ttu-id="024c4-159">Affiche les problèmes tels que RunAsyncFailures RunAsynCancellations et des pannes de nœud.</span><span class="sxs-lookup"><span data-stu-id="024c4-159">Displays issues including RunAsyncFailures, RunAsynCancellations, and Node Downs.</span></span> |
| <span data-ttu-id="024c4-160">Événements opérationnels</span><span class="sxs-lookup"><span data-stu-id="024c4-160">Operational Events</span></span> | <span data-ttu-id="024c4-161">Affiche des événements opérationnels notables, tels que les déploiements et mises à niveau d’application.</span><span class="sxs-lookup"><span data-stu-id="024c4-161">Displays notable operational events including application upgrade and deployments.</span></span> |
| <span data-ttu-id="024c4-162">Événements de service fiable</span><span class="sxs-lookup"><span data-stu-id="024c4-162">Reliable Service Events</span></span> | <span data-ttu-id="024c4-163">Affiche des événements Reliable services notables, comme Runasyncinvocations.</span><span class="sxs-lookup"><span data-stu-id="024c4-163">Displays notable reliable service events including  Runasyncinvocations.</span></span> |
| <span data-ttu-id="024c4-164">Événements des acteurs</span><span class="sxs-lookup"><span data-stu-id="024c4-164">Actor Events</span></span> | <span data-ttu-id="024c4-165">Affiche des événements d’acteurs importants générés par vos micro-services.</span><span class="sxs-lookup"><span data-stu-id="024c4-165">Displays notable actor events generated by your micro-services.</span></span> <span data-ttu-id="024c4-166">Les événements incluent les exceptions levées par une méthode d’acteur, les activations et les désactivations d’acteur, etc.</span><span class="sxs-lookup"><span data-stu-id="024c4-166">Events include exceptions thrown by an actor method, actor activations and deactivations, and so on.</span></span> |
| <span data-ttu-id="024c4-167">Événements d’application</span><span class="sxs-lookup"><span data-stu-id="024c4-167">Application Events</span></span> | <span data-ttu-id="024c4-168">Affiche tous les événements ETW personnalisés générés par vos applications.</span><span class="sxs-lookup"><span data-stu-id="024c4-168">Displays all custom ETW events generated by your applications.</span></span> |

![Tableau de bord Service Fabric](./media/log-analytics-service-fabric/sf3.png)

![Tableau de bord Service Fabric](./media/log-analytics-service-fabric/sf4.png)

<span data-ttu-id="024c4-171">Hello tableau suivant montre les méthodes de collecte de données et d’autres détails sur la façon dont les données sont collectées pour Service Fabric :</span><span class="sxs-lookup"><span data-stu-id="024c4-171">hello following table shows data collection methods and other details about how data is collected for Service Fabric:</span></span>

| <span data-ttu-id="024c4-172">plateforme</span><span class="sxs-lookup"><span data-stu-id="024c4-172">platform</span></span> | <span data-ttu-id="024c4-173">Agent direct</span><span class="sxs-lookup"><span data-stu-id="024c4-173">Direct Agent</span></span> | <span data-ttu-id="024c4-174">Agent Operations Manager</span><span class="sxs-lookup"><span data-stu-id="024c4-174">Operations Manager agent</span></span> | <span data-ttu-id="024c4-175">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="024c4-175">Azure Storage</span></span> | <span data-ttu-id="024c4-176">Operations Manager requis ?</span><span class="sxs-lookup"><span data-stu-id="024c4-176">Operations Manager required?</span></span> | <span data-ttu-id="024c4-177">Données de l’agent Operations Manager envoyées via un groupe d’administration</span><span class="sxs-lookup"><span data-stu-id="024c4-177">Operations Manager agent data sent via management group</span></span> | <span data-ttu-id="024c4-178">fréquence de collecte</span><span class="sxs-lookup"><span data-stu-id="024c4-178">collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="024c4-179">Windows</span><span class="sxs-lookup"><span data-stu-id="024c4-179">Windows</span></span> |  |  | <span data-ttu-id="024c4-180">&#8226;</span><span class="sxs-lookup"><span data-stu-id="024c4-180">&#8226;</span></span> |  |  |<span data-ttu-id="024c4-181">10 minutes</span><span class="sxs-lookup"><span data-stu-id="024c4-181">10 minutes</span></span> |

> [!NOTE]
> <span data-ttu-id="024c4-182">Modifier l’étendue de hello d’événements avec **données en fonction des sept derniers jours** haut hello du tableau de bord hello.</span><span class="sxs-lookup"><span data-stu-id="024c4-182">Change hello scope of events with **Data based on last seven days** at hello top of hello dashboard.</span></span> <span data-ttu-id="024c4-183">Vous pouvez également afficher les événements générés dans hello sept derniers jours, un jour ou six heures.</span><span class="sxs-lookup"><span data-stu-id="024c4-183">You can also show events generated within hello last seven days, one day, or six hours.</span></span> <span data-ttu-id="024c4-184">Vous pouvez également sélectionner **personnalisé** toospecify une plage de dates personnalisée.</span><span class="sxs-lookup"><span data-stu-id="024c4-184">Or, you can select **Custom** toospecify a custom date range.</span></span>
>
>

## <a name="troubleshoot-your-service-fabric-and-log-analytics-configuration"></a><span data-ttu-id="024c4-185">Résoudre les problèmes de configuration de Service Fabric et de Log Analytics</span><span class="sxs-lookup"><span data-stu-id="024c4-185">Troubleshoot your Service Fabric and Log Analytics configuration</span></span>
<span data-ttu-id="024c4-186">Si vous devez tooverify votre configuration Analytique de journal car vous n’êtes tooview ne peut pas les données d’événement dans le journal Analytique, utilisez hello script suivant.</span><span class="sxs-lookup"><span data-stu-id="024c4-186">If you need tooverify your Log Analytics configuration because you are unable tooview event data in Log Analytics, use hello following script.</span></span> <span data-ttu-id="024c4-187">Il exécute hello suivant des actions :</span><span class="sxs-lookup"><span data-stu-id="024c4-187">It performs hello following actions:</span></span>

1. <span data-ttu-id="024c4-188">Lit la configuration de diagnostics de votre Service Fabric</span><span class="sxs-lookup"><span data-stu-id="024c4-188">Reads your Service Fabric diagnostics configuration</span></span>
2. <span data-ttu-id="024c4-189">Vérifie les données écrites dans des tables de hello</span><span class="sxs-lookup"><span data-stu-id="024c4-189">Checks for data written into hello tables</span></span>
3. <span data-ttu-id="024c4-190">Vérifie que le journal Analytique est tooread configuré à partir des tables de hello</span><span class="sxs-lookup"><span data-stu-id="024c4-190">Verifies that Log Analytics is configured tooread from hello tables</span></span>

```
<#
    Verify Service Fabric and Log Analytics configuration
    1. Read Service Fabric diagnostics configuration
    2. Check for data being written into hello tables
    3. Verify Log Analytics is configured tooread from hello tables

    Supported tables:
    WADServiceFabricReliableActorEventTable
    WADServiceFabricReliableServiceEventTable
    WADServiceFabricSystemEventTable
    WADETWEventTable

    Script will write a warning for every misconfiguration detected
    toosee items that are correctly configured set $VerbosePreference="Continue"
#>
Param
(
    [Parameter(Mandatory=$true,
    ValueFromPipeline=$true,
    Position=1)]
    [string]$workspaceName
)

$WADtables = @("WADServiceFabricReliableActorEventTable",
               "WADServiceFabricReliableServiceEventTable",
               "WADServiceFabricSystemEventTable",
               "WADETWEventTable"
               )

<#
    Check if OMS Log Analytics is configured tooindex service fabric events from hello specified table
#>

function Check-OMSLogAnalyticsConfiguration {
    param(
    [psobject]$workspace,
    [psobject]$storageAccount,
    [string]$id
    )

    $existingInsights = Get-AzureRmOperationalInsightsStorageInsight -ResourceGroupName $workspace.ResourceGroupName -WorkspaceName $workspace.Name

    if ($existingInsights)
    {
        $currentStorageAccountInsight = $existingInsights.Where({$_.StorageAccountResourceId -eq $storageAccount.ResourceId})

        if ("WADServiceFabric*EventTable" -in $currentStorageAccountInsight.Tables)
        {
            Write-Verbose ("OMS Log Analytics workspace " + $workspace.Name + " is configured tooindex service fabric actor, service and operational events from " + $storageAccount.Name)
        } else
        {
            Write-Warning ("OMS Log Analytics workspace " + $workspace.Name + " is not configured tooindex service fabric actor, service and operational events from " + $storageAccount.Name)
        }
        if ("WADETWEventTable" -in $currentStorageAccountInsight.Tables)
        {
            Write-Verbose ("OMS Log Analytics workspace " + $workspace.Name + " is configured tooindex service fabric application events from " + $storageAccount.Name)
        } else
        {
            Write-Warning ("OMS Log Analytics workspace " + $workspace.Name + " is not configured tooindex service fabric application events from " + $storageAccount.Name)
        }
    } else
    {
        Write-Warning ("OMS Log Analytics workspace " + $workspace.Name + "is not configured tooread service fabric events from " + $storageAccount.Name)
    }    
}

<#
    Check Azure table storage tooconfirm there is recent data written by Service Fabric
#>

function Check-TablesForData {
    param(
    [psobject]$storageAccount
    )

    $ctx = (Get-AzureRmStorageAccount -ResourceGroupName $storageAccount.ResourceGroupName -Name $storageAccount.ResourceName).Context

    $createdTables = Get-AzureStorageTable -Context $ctx

    $recently = Get-Date -Format s ((Get-Date).AddMinutes(-20).ToUniversalTime())
    $recently = $recently + "Z"

    foreach ($table in $WADtables)
    {
        if ($table -in $createdTables.Name)
        {
            $tbl = Get-AzureStorageTable -Name $table -Context $ctx
            $query = New-Object Microsoft.WindowsAzure.Storage.Table.TableQuery
            $list = New-Object System.Collections.Generic.List[string]
            $list.Add("RowKey")
            $list.Add("ProviderName")
            $list.Add("Timestamp")
            $query.FilterString = "Timestamp gt datetime'$recently'"
            $query.SelectColumns = $list
            $query.TakeCount = 20
            $entities = $tbl.CloudTable.ExecuteQuery($query)
            Write-Debug $entities
            if ($entities.Count -gt 0)
            {
                Write-Verbose ("Data was written too$table in " + $storageAccount.ResourceName + "after $recently")
            } else
            {
                Write-Warning ("No data after $recently is in  $table in " + $storageAccount.ResourceName)
            }
        } else
        {
            Write-Warning ("$table does not exist in storage account " + $storageAccount.ResourceName)
        }
    }
}

<#
    Check if ETW provider is configured toolog events toohello expected table storage
#>
function Check-ETWProviderLogging {
    param(
    [string]$id,
    [string]$provider,
    [string]$expectedTable,
    [string]$table
    )      
        Write-Debug ("ID: $id Provider: $provider ExpectedTable $expectedTable ActualTable $table")
        if ( ($table -eq $null) -or ($table -eq ""))
        {
            Write-Warning ("$id No configuration found for $provider. Configure Azure diagnostics toowrite too$expectedTable.")
        }
        elseif ( $table -ne $expectedTable )
        {
            Write-Warning ("$id $provider events are being written too$table instead of WAD$expectedTable. Events will not be collected by Log Analytics")
        }
        else
        {
            Write-Verbose "$id $provider events are being written tooWAD$expectedTable (Correct configuration.)"
        }
}

<#
    Check Azure Diagnostics Configuration for a Service Fabric cluster
#>
function Check-ServiceFabricScaleSetDiagnostics {
    param(
    [psobject]$scaleSetDiagnostics
    )

    $storageAccountsFound = @()
    Write-Verbose ("Checking " + $scaleSetDiagnostics)
    $sfReliableActorTable = $null
    $sfReliableServiceTable = $null
    $sfOperationalTable = $null
    Write-Debug $scaleSetDiagnostics
    $serviceFabricProviderList = ""
    $etwManifestProviderList = ""

    if ( $scaleSetDiagnostics.xmlCfg )
    {
        Write-Debug ("Found XMLcfg")
        $xmlCfg = [System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String($scaleSetDiagnostics.xmlCfg))
        Write-Debug $xmlCfg
        $etwProviders = Select-Xml -Content $xmlCfg -XPath "//EtwProviders"                
        $serviceFabricProviderList = $etwProviders.Node.EtwEventSourceProviderConfiguration
        $etwManifestProviderList = $etwProviders.Node.EtwManifestProviderConfiguration
    } elseif ($scaleSetDiagnostics.WadCfg )
    {
        Write-Debug ("Found WADcfg")
        Write-Debug $scaleSetDiagnostics.WadCfg
        $serviceFabricProviderList = $scaleSetDiagnostics.WadCfg.DiagnosticMonitorConfiguration.EtwProviders.EtwEventSourceProviderConfiguration
        $etwManifestProviderList = $scaleSetDiagnostics.WadCfg.DiagnosticMonitorConfiguration.EtwProviders.EtwManifestProviderConfiguration
    } else
    {
        Write-Error "Unable tooparse Azure Diagnostics setting for $id"
        Write-Warning ("$id does not have diagnostics enabled")
    }

    foreach ($provider in $serviceFabricProviderList)
    {
        Write-Debug ("Event Source Provider: " + $provider.Provider + " Destination: " + $provider.DefaultEvents.eventDestination)
        if ($provider.Provider -eq "Microsoft-ServiceFabric-Actors")
        {
            $sfReliableActorTable = $provider.DefaultEvents.eventDestination
        } elseif ($provider.Provider -eq "Microsoft-ServiceFabric-Services")
        {
            $sfReliableServiceTable = $provider.DefaultEvents.eventDestination
        } else
        {
            Check-ETWProviderLogging $id $provider.Provider "ETWEventTable" $provider.DefaultEvents.eventDestination
        }
    }
    foreach ($provider in $etwManifestProviderList)
    {
        Write-Debug ("Manifest Provider: " + $provider.Provider + " Destination: " + $provider.DefaultEvents.eventDestination)
        if ($provider.Provider -eq "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8")
        {
            $sfOperationalTable = $provider.DefaultEvents.eventDestination
        } else
        {
            Check-ETWProviderLogging $id $provider.Provider "ETWEventTable" $provider.DefaultEvents.eventDestination
        }
    }

    Check-ETWProviderLogging $id "Microsoft-ServiceFabric-Actors" "ServiceFabricReliableActorEventTable" $sfReliableActorTable
    Check-ETWProviderLogging $id "Microsoft-ServiceFabric-Services" "ServiceFabricReliableServiceEventTable" $sfReliableServiceTable
    Check-ETWProviderLogging $id "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8 (System events)" "ServiceFabricSystemEventTable" $sfOperationalTable

    Write-Verbose ("StorageAccount: " + $scaleSetDiagnostics.StorageAccount)

    $storageAccountsFound += ($scaleSetDiagnostics.StorageAccount)
    return ($storageAccountsFound)
}

# This script uses Get-AzureRmVMDiagnosticsExtension and needs a version where -Name is not a required parameter
Import-Module AzureRM.Compute -MinimumVersion 1.2.2

try
{
    Get-AzureRmContext
}
catch [System.Management.Automation.PSInvalidOperationException]
{
    Login-AzureRmAccount
}

$allResources = Get-AzureRmResource

$OMSworkspace = $allResources.Where({($_.ResourceType -eq "Microsoft.OperationalInsights/workspaces") -and ($_.ResourceName -eq $workspaceName)})

if ($OMSworkspace.Name -ne $workspaceName)
{
    Write-Error ("Unable toofind Log Analytics Workspace " + $workspaceName)
}

$serviceFabricClusters = $allResources.Where({$_.ResourceType -eq "Microsoft.ServiceFabric/clusters"})
$storageAccountList = @()
foreach($cluster in $serviceFabricClusters) {
    Write-Verbose ("Checking cluster: " + $cluster.Name)
    $scaleSet = ($allResources.Where({($_.ResourceType -eq "Microsoft.Compute/virtualMachineScaleSets") -and ($_.ResourceGroupName -eq $cluster.ResourceGroupName)}))

    foreach($set in $scaleSet) {
        $resource = Get-AzureRmResource -ResourceId $set.ResourceId
        $extensions = $resource.Properties.VirtualMachineProfile.ExtensionProfile.Extensions
        foreach($ext in $extensions) {
            if ($ext.Properties.Publisher -eq "Microsoft.Azure.Diagnostics" -and $ext.Properties.Type -eq "IaaSDiagnostics") {
                $storageAccountList += (Check-ServiceFabricScaleSetDiagnostics $ext.Properties.Settings)
            }
        }
    }
}

$storageAccountList = $storageAccountList | Sort-Object | Get-Unique
$storageAccountsToCheck = ($allResources.Where({($_.ResourceType -eq "Microsoft.Storage/storageAccounts") -and ($_.ResourceName -in $storageAccountList)}))

foreach($storageAccount in $storageAccountsToCheck)
{
    Check-TablesForData $storageAccount
    Check-OMSLogAnalyticsConfiguration $OMSworkspace $storageAccount
}
 ```


## <a name="next-steps"></a><span data-ttu-id="024c4-191">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="024c4-191">Next steps</span></span>
* <span data-ttu-id="024c4-192">Utilisez [recherches de journal dans le journal Analytique](log-analytics-log-searches.md) tooview détaillées des données d’événement Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="024c4-192">Use [Log Searches in Log Analytics](log-analytics-log-searches.md) tooview detailed Service Fabric event data.</span></span>
