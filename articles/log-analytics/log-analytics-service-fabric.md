---
title: "Évaluer des applications Service Fabric avec Azure Log Analytics à l’aide de PowerShell | Microsoft Docs"
description: "Vous pouvez utiliser la solution Service Fabric dans Log Analytics, à l’aide de PowerShell, pour évaluer les risques et l’intégrité de vos applications, micro-services, nœuds et clusters Service Fabric."
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
ms.openlocfilehash: ca86787e344aa5e9e68934dee6e9e83aeb4cc340
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="assess-azure-service-fabric-applications-and-micro-services-with-powershell"></a><span data-ttu-id="d2999-103">Évaluer les micro-services et applications Azure Service Fabric avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="d2999-103">Assess Azure Service Fabric applications and micro-services with PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d2999-104">Gestionnaire de ressources</span><span class="sxs-lookup"><span data-stu-id="d2999-104">Resource Manager</span></span>](log-analytics-service-fabric-azure-resource-manager.md)
> * [<span data-ttu-id="d2999-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d2999-105">PowerShell</span></span>](log-analytics-service-fabric.md)
>
>


![Symbole Service Fabric](./media/log-analytics-service-fabric/service-fabric-assessment-symbol.png)

<span data-ttu-id="d2999-107">Cet article décrit comment utiliser la solution Service Fabric dans Log Analytics pour identifier et résoudre les problèmes sur l’ensemble de votre cluster Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="d2999-107">This article describes how to use the Service Fabric solution in Log Analytics to help identify and troubleshoot issues across your Service Fabric cluster.</span></span> <span data-ttu-id="d2999-108">Il vous permet de voir les performances de vos nœuds Service Fabric et l’exécution de vos applications et micro-services.</span><span class="sxs-lookup"><span data-stu-id="d2999-108">It helps you see how your Service Fabric nodes are performing and how your applications and micro-services are running.</span></span>

<span data-ttu-id="d2999-109">La solution Service Fabric utilise les données de diagnostic Azure provenant de vos machines virtuelles Fabric Service. Ces données sont collectées à partir de vos tables Azure WAD.</span><span class="sxs-lookup"><span data-stu-id="d2999-109">The Service Fabric solution uses Azure Diagnostics data from your Service Fabric VMs, by collecting this data from your Azure WAD tables.</span></span> <span data-ttu-id="d2999-110">Log Analytics lit ensuite les événements de framework Service Fabric suivants :</span><span class="sxs-lookup"><span data-stu-id="d2999-110">Log Analytics then reads the following Service Fabric framework events:</span></span>

- <span data-ttu-id="d2999-111">**Événements Reliable Service**</span><span class="sxs-lookup"><span data-stu-id="d2999-111">**Reliable Service Events**</span></span>
- <span data-ttu-id="d2999-112">**Événements d’acteurs**</span><span class="sxs-lookup"><span data-stu-id="d2999-112">**Actor Events**</span></span>
- <span data-ttu-id="d2999-113">**Événements opérationnels**</span><span class="sxs-lookup"><span data-stu-id="d2999-113">**Operational Events**</span></span>
- <span data-ttu-id="d2999-114">**Événements ETW personnalisés**</span><span class="sxs-lookup"><span data-stu-id="d2999-114">**Custom ETW events**</span></span>

<span data-ttu-id="d2999-115">Le tableau de bord de la solution de Service Fabric présente les problèmes notables et les événements pertinents qui concernent votre environnement Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="d2999-115">The Service Fabric solution dashboard shows you notable issues and relevant events in your Service Fabric environment.</span></span>

## <a name="installing-and-configuring-the-solution"></a><span data-ttu-id="d2999-116">Installation et configuration de la solution</span><span class="sxs-lookup"><span data-stu-id="d2999-116">Installing and configuring the solution</span></span>
<span data-ttu-id="d2999-117">Pour installer et configurer la solution, effectuez ces trois étapes simples :</span><span class="sxs-lookup"><span data-stu-id="d2999-117">Follow these three easy steps to install and configure the solution:</span></span>

1. <span data-ttu-id="d2999-118">Associez l’abonnement Azure que vous avez utilisé pour créer toutes les ressources du cluster, notamment les comptes de stockage, à votre espace de travail.</span><span class="sxs-lookup"><span data-stu-id="d2999-118">Associate the Azure subscription that you used to create all cluster resources, including storage accounts, with your workspace.</span></span> <span data-ttu-id="d2999-119">Pour plus d’informations sur la création d’un espace de travail Log Analytics, consultez [Prise en main de Log Analytics](log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="d2999-119">See [Get started with Log Analytics](log-analytics-get-started.md) for information about creating a Log Analytics workspace.</span></span>
2. <span data-ttu-id="d2999-120">Configurez Log Analytics pour collecter et afficher les journaux Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="d2999-120">Configure Log Analytics to collect and view Service Fabric logs.</span></span>
3. <span data-ttu-id="d2999-121">Activez la solution Service Fabric dans votre espace de travail.</span><span class="sxs-lookup"><span data-stu-id="d2999-121">Enable the Service Fabric solution in your workspace.</span></span>

## <a name="configure-log-analytics-to-collect-and-view-service-fabric-logs"></a><span data-ttu-id="d2999-122">Configurer Log Analytics pour collecter et afficher les journaux Service Fabric</span><span class="sxs-lookup"><span data-stu-id="d2999-122">Configure Log Analytics to collect and view Service Fabric logs</span></span>
<span data-ttu-id="d2999-123">Dans cette section, vous allez apprendre à configurer Log Analytics pour récupérer les journaux Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="d2999-123">In this section, you learn how to configure Log Analytics to retrieve Service Fabric logs.</span></span> <span data-ttu-id="d2999-124">Les journaux vous permettent d’afficher, d’analyser et de résoudre les problèmes affectant votre cluster, ou les applications et services qui s’exécutent dans ce cluster, à l’aide du portail OMS.</span><span class="sxs-lookup"><span data-stu-id="d2999-124">The logs allow you to view, analyze, and troubleshoot issues in your cluster or in the applications and services running in that cluster, using the OMS portal.</span></span>

> [!NOTE]
> <span data-ttu-id="d2999-125">Configurez l’extension Azure Diagnostics pour charger les journaux pour les tables de stockage.</span><span class="sxs-lookup"><span data-stu-id="d2999-125">Configure the Azure Diagnostics extension to upload the logs for storage tables.</span></span> <span data-ttu-id="d2999-126">Les tables doivent correspondre à ce que recherche Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="d2999-126">The tables must match what Log Analytics looks for.</span></span> <span data-ttu-id="d2999-127">Pour plus d’informations, consultez [Collecte des journaux avec Azure Diagnostics](../service-fabric/service-fabric-diagnostics-how-to-setup-wad.md).</span><span class="sxs-lookup"><span data-stu-id="d2999-127">For more information, see [How to collect logs with Azure Diagnostics](../service-fabric/service-fabric-diagnostics-how-to-setup-wad.md).</span></span> <span data-ttu-id="d2999-128">Les exemples de paramètres de configuration inclus dans cet article indiquent les noms souhaités pour les tables de stockage.</span><span class="sxs-lookup"><span data-stu-id="d2999-128">The configuration settings examples in this article show you what the names of the storage tables should be.</span></span> <span data-ttu-id="d2999-129">Une fois que Diagnostics est configuré sur le cluster et qu’il charge les journaux sur un compte de stockage, l’étape suivante consiste à configurer Log Analytics pour collecter ces journaux.</span><span class="sxs-lookup"><span data-stu-id="d2999-129">Once Diagnostics is set up on the cluster and is uploading logs to a storage account, the next step is to configure Log Analytics to collect these logs.</span></span>
>
>

<span data-ttu-id="d2999-130">Dans la section **EtwEventSourceProviderConfiguration** du fichier **template.json**, veillez à ajouter les entrées des nouveaux EventSources avant d’appliquer la mise à jour de la configuration en exécutant **deploy.ps1**.</span><span class="sxs-lookup"><span data-stu-id="d2999-130">Ensure that you update the **EtwEventSourceProviderConfiguration** section in the **template.json** file to add entries for the new EventSources before you apply the configuration update by running **deploy.ps1**.</span></span> <span data-ttu-id="d2999-131">La table de chargement est identique à (ETWEventTable).</span><span class="sxs-lookup"><span data-stu-id="d2999-131">The table for upload is the same as (ETWEventTable).</span></span> <span data-ttu-id="d2999-132">Pour le moment, Log Analytics peut lire uniquement les événements ETW d’application à partir de la table *WADETWEventTable*.</span><span class="sxs-lookup"><span data-stu-id="d2999-132">At the moment, Log Analytics can only read application ETW events from the *WADETWEventTable* table.</span></span>

<span data-ttu-id="d2999-133">Les outils suivants sont utilisés pour exécuter certaines opérations décrites dans cette section :</span><span class="sxs-lookup"><span data-stu-id="d2999-133">The following tools are used to perform some of the operations in this section:</span></span>

* <span data-ttu-id="d2999-134">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="d2999-134">Azure PowerShell</span></span>
* [<span data-ttu-id="d2999-135">Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="d2999-135">Operations Management Suite</span></span>](http://www.microsoft.com/oms)

### <a name="configure-a-log-analytics-workspace-to-show-the-cluster-logs"></a><span data-ttu-id="d2999-136">Configurer un espace de travail Log Analytics pour afficher les journaux de cluster</span><span class="sxs-lookup"><span data-stu-id="d2999-136">Configure a Log Analytics workspace to show the cluster logs</span></span>

<span data-ttu-id="d2999-137">Après avoir créé un espace de travail Log Analytics, configurez l’espace de travail pour extraire (Pull) les journaux à partir des tables de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="d2999-137">After you create a Log Analytics workspace, configure the workspace to pull logs from the Azure storage tables.</span></span> <span data-ttu-id="d2999-138">Puis, exécutez le script PowerShell suivant :</span><span class="sxs-lookup"><span data-stu-id="d2999-138">Then, run the following PowerShell script:</span></span>

```
<#
    This script will configure an Operations Management Suite workspace (previously called an Operational Insights workspace) to read Diagnostics from an Azure Storage account.
    It will enable all supported data types (currently Service Fabric Events, ETW Events and IIS Logs).
    It supports Resource Manager storage accounts.
    If you have more than one Azure Subscription, you will be prompted for the subscription to configure.
    If you have more than one Log Analytics workspace you will be prompted for the workspace to configure.
    It will then look through your Service Fabric clusters, and configure your Log Analytics workspace to read Diagnostics from storage accounts that are connected to that cluster and have diagnostics enabled.
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
            $uiPrompt = "Enter the number corresponding to the Azure subscription you would like to work with.`n"

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
            $uiPrompt = "Enter the number corresponding to the workspace you want to configure.`n"
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
             Write-Warning ("$id No configuration found for $provider. Configure Azure diagnostics to write to $expectedTable.")
         }  
         elseif ( $table -ne $expectedTable )
         {
             Write-Warning ("$id $provider events are being written to $table instead of WAD$expectedTable. Events will not be collected by Log Analytics")
         }  
         else
         {
             Write-Verbose "$id $provider events are being written to WAD$expectedTable (Correct configuration.)"
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
         Write-Error "Unable to parse Azure Diagnostics setting for $id"
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
    $serviceFabricClusters = $allResources.Where({$_.ResourceType -eq "Microsoft.ServiceFabric/clusters"}) #pulls in all service fabric clusters in the resource
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
                                # HTTP Not Found is returned if the storage insight doesn't exist
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
                                      # If any of the tables from the table list are not already monitored, then we add them
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

<span data-ttu-id="d2999-139">Après avoir configuré l’espace de travail Log Analytics de sorte qu’il lise les tables Azure dans votre compte de stockage, connectez-vous au portail Azure.</span><span class="sxs-lookup"><span data-stu-id="d2999-139">After you've configured the Log Analytics workspace to read from the Azure tables in your storage account, log in to the Azure portal.</span></span> <span data-ttu-id="d2999-140">Sélectionnez l’espace de travail Log Analytics sous **Toutes les ressources**.</span><span class="sxs-lookup"><span data-stu-id="d2999-140">Select the Log Analytics workspace from **All Resources**.</span></span> <span data-ttu-id="d2999-141">Le nombre de journaux de compte de stockage connectés à l’espace de travail s’affiche.</span><span class="sxs-lookup"><span data-stu-id="d2999-141">The number of storage account logs connected to the workspace is displayed.</span></span> <span data-ttu-id="d2999-142">Sélectionnez la vignette **Journaux de compte de stockage**.</span><span class="sxs-lookup"><span data-stu-id="d2999-142">Select the **Storage account logs** tile.</span></span> <span data-ttu-id="d2999-143">Passez en revue la liste des journaux de compte de stockage pour vérifier que votre compte de stockage est connecté à l’espace de travail correct.</span><span class="sxs-lookup"><span data-stu-id="d2999-143">Review the list of storage account logs to verify that your storage account is connected to the correct workspace.</span></span>

![Journaux de compte de stockage](./media/log-analytics-service-fabric/sf1.png)

## <a name="enable-the-service-fabric-solution"></a><span data-ttu-id="d2999-145">Activer la solution Service Fabric</span><span class="sxs-lookup"><span data-stu-id="d2999-145">Enable the Service Fabric solution</span></span>
<span data-ttu-id="d2999-146">Utilisez le script suivant pour ajouter la solution à votre espace de travail Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="d2999-146">Use the following script to add the solution to your Log Analytics workspace.</span></span> <span data-ttu-id="d2999-147">Exécutez le script dans PowerShell à l’aide de l’abonnement Azure associé à l’espace de travail Log Analytics dans lequel vous souhaitez activer la solution Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="d2999-147">Run the script in PowerShell, using the Azure subscription that is associated with the Log Analytics workspace that you want to enable the Service Fabric solution in.</span></span>

```
function Select-Subscription {
      $subscription = ""
      $allSubscriptions = Get-AzureRmSubscription
      switch ($allSubscriptions.Count) {
             0 {Write-Error "No Operations Management Suite workspaces found"}
             1 {return $allSubscriptions}
        default {
            $uiPrompt = "Enter the number corresponding to the Azure subscription you would like to work with.`n"
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
            $uiPrompt = "Enter the number corresponding to the workspace you want to configure.`n"
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

<span data-ttu-id="d2999-148">Après avoir activé la solution, la vignette Service Fabric est ajoutée à la page *Vue d’ensemble* de votre Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="d2999-148">After you enable the solution, the Service Fabric tile is added to your Log Analytics *Overview* page.</span></span> <span data-ttu-id="d2999-149">La page affiche une vue des problèmes importants, comme les échecs et les annulations runAsync, survenus au cours des dernières 24 heures.</span><span class="sxs-lookup"><span data-stu-id="d2999-149">The page shows a view of notable issues such as runAsync failures and cancellations that occurred in the last 24 hours.</span></span>

![Vignette Service Fabric](./media/log-analytics-service-fabric/sf2.png)

### <a name="view-service-fabric-events"></a><span data-ttu-id="d2999-151">Afficher les événements Service Fabric</span><span class="sxs-lookup"><span data-stu-id="d2999-151">View Service Fabric events</span></span>
<span data-ttu-id="d2999-152">Cliquez sur la vignette **Service Fabric** pour ouvrir le tableau de bord Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="d2999-152">Click the **Service Fabric** tile to open the Service Fabric dashboard.</span></span> <span data-ttu-id="d2999-153">Le tableau de bord comprend les colonnes figurant dans le tableau suivant.</span><span class="sxs-lookup"><span data-stu-id="d2999-153">The dashboard includes the columns in the table that follows.</span></span> <span data-ttu-id="d2999-154">Chaque colonne répertorie les 10 premiers événements, classés selon leur nombre, correspondant aux critères de cette colonne pour l’intervalle de temps spécifié.</span><span class="sxs-lookup"><span data-stu-id="d2999-154">Each column lists the top 10 events by count matching that column's criteria for the specified time range.</span></span> <span data-ttu-id="d2999-155">Vous pouvez exécuter une recherche dans les journaux qui fournit la liste complète. Pour cela, cliquez sur **Afficher tout** en bas à droite de chaque colonne ou cliquez sur l’en-tête de colonne.</span><span class="sxs-lookup"><span data-stu-id="d2999-155">You can run a log search that provides the entire list by clicking **See all** at the right bottom of each column, or by clicking the column header.</span></span>

| <span data-ttu-id="d2999-156">**Événement Service Fabric**</span><span class="sxs-lookup"><span data-stu-id="d2999-156">**Service Fabric event**</span></span> | <span data-ttu-id="d2999-157">**description**</span><span class="sxs-lookup"><span data-stu-id="d2999-157">**description**</span></span> |
| --- | --- |
| <span data-ttu-id="d2999-158">Problèmes notables</span><span class="sxs-lookup"><span data-stu-id="d2999-158">Notable Issues</span></span> | <span data-ttu-id="d2999-159">Affiche les problèmes tels que RunAsyncFailures RunAsynCancellations et des pannes de nœud.</span><span class="sxs-lookup"><span data-stu-id="d2999-159">Displays issues including RunAsyncFailures, RunAsynCancellations, and Node Downs.</span></span> |
| <span data-ttu-id="d2999-160">Événements opérationnels</span><span class="sxs-lookup"><span data-stu-id="d2999-160">Operational Events</span></span> | <span data-ttu-id="d2999-161">Affiche des événements opérationnels notables, tels que les déploiements et mises à niveau d’application.</span><span class="sxs-lookup"><span data-stu-id="d2999-161">Displays notable operational events including application upgrade and deployments.</span></span> |
| <span data-ttu-id="d2999-162">Événements de service fiable</span><span class="sxs-lookup"><span data-stu-id="d2999-162">Reliable Service Events</span></span> | <span data-ttu-id="d2999-163">Affiche des événements Reliable services notables, comme Runasyncinvocations.</span><span class="sxs-lookup"><span data-stu-id="d2999-163">Displays notable reliable service events including  Runasyncinvocations.</span></span> |
| <span data-ttu-id="d2999-164">Événements des acteurs</span><span class="sxs-lookup"><span data-stu-id="d2999-164">Actor Events</span></span> | <span data-ttu-id="d2999-165">Affiche des événements d’acteurs importants générés par vos micro-services.</span><span class="sxs-lookup"><span data-stu-id="d2999-165">Displays notable actor events generated by your micro-services.</span></span> <span data-ttu-id="d2999-166">Les événements incluent les exceptions levées par une méthode d’acteur, les activations et les désactivations d’acteur, etc.</span><span class="sxs-lookup"><span data-stu-id="d2999-166">Events include exceptions thrown by an actor method, actor activations and deactivations, and so on.</span></span> |
| <span data-ttu-id="d2999-167">Événements d’application</span><span class="sxs-lookup"><span data-stu-id="d2999-167">Application Events</span></span> | <span data-ttu-id="d2999-168">Affiche tous les événements ETW personnalisés générés par vos applications.</span><span class="sxs-lookup"><span data-stu-id="d2999-168">Displays all custom ETW events generated by your applications.</span></span> |

![Tableau de bord Service Fabric](./media/log-analytics-service-fabric/sf3.png)

![Tableau de bord Service Fabric](./media/log-analytics-service-fabric/sf4.png)

<span data-ttu-id="d2999-171">Le tableau suivant présente les méthodes de collecte des données et d’autres informations sur le mode de collecte de la solution de données pour Service Fabric :</span><span class="sxs-lookup"><span data-stu-id="d2999-171">The following table shows data collection methods and other details about how data is collected for Service Fabric:</span></span>

| <span data-ttu-id="d2999-172">plateforme</span><span class="sxs-lookup"><span data-stu-id="d2999-172">platform</span></span> | <span data-ttu-id="d2999-173">Agent direct</span><span class="sxs-lookup"><span data-stu-id="d2999-173">Direct Agent</span></span> | <span data-ttu-id="d2999-174">Agent Operations Manager</span><span class="sxs-lookup"><span data-stu-id="d2999-174">Operations Manager agent</span></span> | <span data-ttu-id="d2999-175">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="d2999-175">Azure Storage</span></span> | <span data-ttu-id="d2999-176">Operations Manager requis ?</span><span class="sxs-lookup"><span data-stu-id="d2999-176">Operations Manager required?</span></span> | <span data-ttu-id="d2999-177">Données de l’agent Operations Manager envoyées via un groupe d’administration</span><span class="sxs-lookup"><span data-stu-id="d2999-177">Operations Manager agent data sent via management group</span></span> | <span data-ttu-id="d2999-178">fréquence de collecte</span><span class="sxs-lookup"><span data-stu-id="d2999-178">collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="d2999-179">Windows</span><span class="sxs-lookup"><span data-stu-id="d2999-179">Windows</span></span> |  |  | <span data-ttu-id="d2999-180">&#8226;</span><span class="sxs-lookup"><span data-stu-id="d2999-180">&#8226;</span></span> |  |  |<span data-ttu-id="d2999-181">10 minutes</span><span class="sxs-lookup"><span data-stu-id="d2999-181">10 minutes</span></span> |

> [!NOTE]
> <span data-ttu-id="d2999-182">Modifiez l’étendue des événements avec **Données basées sur les sept derniers jours** en haut du tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="d2999-182">Change the scope of events with **Data based on last seven days** at the top of the dashboard.</span></span> <span data-ttu-id="d2999-183">Vous pouvez également afficher les événements générés durant les sept derniers jours, la journée précédente ou les six dernières heures.</span><span class="sxs-lookup"><span data-stu-id="d2999-183">You can also show events generated within the last seven days, one day, or six hours.</span></span> <span data-ttu-id="d2999-184">Vous pouvez aussi sélectionner **Personnalisé** pour spécifier une plage de dates personnalisée.</span><span class="sxs-lookup"><span data-stu-id="d2999-184">Or, you can select **Custom** to specify a custom date range.</span></span>
>
>

## <a name="troubleshoot-your-service-fabric-and-log-analytics-configuration"></a><span data-ttu-id="d2999-185">Résoudre les problèmes de configuration de Service Fabric et de Log Analytics</span><span class="sxs-lookup"><span data-stu-id="d2999-185">Troubleshoot your Service Fabric and Log Analytics configuration</span></span>
<span data-ttu-id="d2999-186">Si vous ne parvenez pas à afficher les données d’événement dans Log Analytics, vous pouvez vérifier votre configuration Log Analytics à l’aide du script ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="d2999-186">If you need to verify your Log Analytics configuration because you are unable to view event data in Log Analytics, use the following script.</span></span> <span data-ttu-id="d2999-187">Il effectue les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="d2999-187">It performs the following actions:</span></span>

1. <span data-ttu-id="d2999-188">Lit la configuration de diagnostics de votre Service Fabric</span><span class="sxs-lookup"><span data-stu-id="d2999-188">Reads your Service Fabric diagnostics configuration</span></span>
2. <span data-ttu-id="d2999-189">Vérifie les données écrites dans les tables</span><span class="sxs-lookup"><span data-stu-id="d2999-189">Checks for data written into the tables</span></span>
3. <span data-ttu-id="d2999-190">Vérifie que Log Analytics est configuré pour lire à partir des tables</span><span class="sxs-lookup"><span data-stu-id="d2999-190">Verifies that Log Analytics is configured to read from the tables</span></span>

```
<#
    Verify Service Fabric and Log Analytics configuration
    1. Read Service Fabric diagnostics configuration
    2. Check for data being written into the tables
    3. Verify Log Analytics is configured to read from the tables

    Supported tables:
    WADServiceFabricReliableActorEventTable
    WADServiceFabricReliableServiceEventTable
    WADServiceFabricSystemEventTable
    WADETWEventTable

    Script will write a warning for every misconfiguration detected
    To see items that are correctly configured set $VerbosePreference="Continue"
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
    Check if OMS Log Analytics is configured to index service fabric events from the specified table
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
            Write-Verbose ("OMS Log Analytics workspace " + $workspace.Name + " is configured to index service fabric actor, service and operational events from " + $storageAccount.Name)
        } else
        {
            Write-Warning ("OMS Log Analytics workspace " + $workspace.Name + " is not configured to index service fabric actor, service and operational events from " + $storageAccount.Name)
        }
        if ("WADETWEventTable" -in $currentStorageAccountInsight.Tables)
        {
            Write-Verbose ("OMS Log Analytics workspace " + $workspace.Name + " is configured to index service fabric application events from " + $storageAccount.Name)
        } else
        {
            Write-Warning ("OMS Log Analytics workspace " + $workspace.Name + " is not configured to index service fabric application events from " + $storageAccount.Name)
        }
    } else
    {
        Write-Warning ("OMS Log Analytics workspace " + $workspace.Name + "is not configured to read service fabric events from " + $storageAccount.Name)
    }    
}

<#
    Check Azure table storage to confirm there is recent data written by Service Fabric
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
                Write-Verbose ("Data was written to $table in " + $storageAccount.ResourceName + "after $recently")
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
    Check if ETW provider is configured to log events to the expected table storage
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
            Write-Warning ("$id No configuration found for $provider. Configure Azure diagnostics to write to $expectedTable.")
        }
        elseif ( $table -ne $expectedTable )
        {
            Write-Warning ("$id $provider events are being written to $table instead of WAD$expectedTable. Events will not be collected by Log Analytics")
        }
        else
        {
            Write-Verbose "$id $provider events are being written to WAD$expectedTable (Correct configuration.)"
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
        Write-Error "Unable to parse Azure Diagnostics setting for $id"
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
    Write-Error ("Unable to find Log Analytics Workspace " + $workspaceName)
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


## <a name="next-steps"></a><span data-ttu-id="d2999-191">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d2999-191">Next steps</span></span>
* <span data-ttu-id="d2999-192">Utilisez [Recherches dans les journaux dans Log Analytics](log-analytics-log-searches.md) pour afficher des données détaillées sur les événements Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="d2999-192">Use [Log Searches in Log Analytics](log-analytics-log-searches.md) to view detailed Service Fabric event data.</span></span>
