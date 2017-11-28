---
title: "Gestion d’Azure Data Lake Analytics à l’aide d’Azure PowerShell | Microsoft Docs"
description: "Apprenez à gérer des comptes Data Lake Analytics, des sources de données, des travaux et des éléments de catalogue. "
services: data-lake-analytics
documentationcenter: 
author: matt1883
manager: jhubbard
editor: cgronlun
ms.assetid: ad14d53c-fed4-478d-ab4b-6d2e14ff2097
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/23/2017
ms.author: mahi
ms.openlocfilehash: 862e9551f1e129b7bba06651fbae94e337c92dcb
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="manage-azure-data-lake-analytics-using-azure-powershell"></a><span data-ttu-id="8b842-103">Gestion d'Azure Data Lake Analytics à l'aide d'Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="8b842-103">Manage Azure Data Lake Analytics using Azure PowerShell</span></span>
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

<span data-ttu-id="8b842-104">Apprenez à gérer des comptes Azure Data Lake Analytics, des sources de données, des travaux et des éléments de catalogue à l'aide d'Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8b842-104">Learn how to manage Azure Data Lake Analytics accounts, data sources, jobs, and catalog items using Azure PowerShell.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="8b842-105">Composants requis</span><span class="sxs-lookup"><span data-stu-id="8b842-105">Prerequisites</span></span>

<span data-ttu-id="8b842-106">Pour créer un compte Data Lake Analytics, vous devez connaître les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="8b842-106">When creating a Data Lake Analytics account, you need to know:</span></span>

* <span data-ttu-id="8b842-107">**ID d’abonnement** : ID d’abonnement Azure sous lequel réside votre compte Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="8b842-107">**Subscription ID**: The Azure subscription ID under which your Data Lake Analytics account resides.</span></span>
* <span data-ttu-id="8b842-108">**Groupe de ressources** : nom du groupe de ressources Azure qui contient votre compte Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="8b842-108">**Resource group**: The name of the Azure resource group that contains your Data Lake Analytics account.</span></span>
* <span data-ttu-id="8b842-109">**Nom du compte Data Lake Analytics** : le nom du compte ne doit contenir que des lettres minuscules et des chiffres.</span><span class="sxs-lookup"><span data-stu-id="8b842-109">**Data Lake Analytics account name**: The account name must only contain lowercase letters and numbers.</span></span>
* <span data-ttu-id="8b842-110">**Compte Data Lake Store par défaut** : chaque compte Data Lake Analytics possède un compte Data Lake Store par défaut.</span><span class="sxs-lookup"><span data-stu-id="8b842-110">**Default Data Lake Store account**: Each Data Lake Analytics account has a default Data Lake Store account.</span></span> <span data-ttu-id="8b842-111">Ces comptes doivent résider au même emplacement.</span><span class="sxs-lookup"><span data-stu-id="8b842-111">These accounts must be in the same location.</span></span>
* <span data-ttu-id="8b842-112">**Emplacement** : emplacement de votre compte Data Lake Analytics, comme « États-Unis de l’Est 2 » ou autres emplacements pris en charge.</span><span class="sxs-lookup"><span data-stu-id="8b842-112">**Location**: The location of your Data Lake Analytics account, such as "East US 2" or other supported locations.</span></span> <span data-ttu-id="8b842-113">Les emplacements pris en charge sont indiqués sur notre [page de tarification](https://azure.microsoft.com/pricing/details/data-lake-analytics/).</span><span class="sxs-lookup"><span data-stu-id="8b842-113">Supported locations can be seen on our [pricing page](https://azure.microsoft.com/pricing/details/data-lake-analytics/).</span></span>

<span data-ttu-id="8b842-114">Dans ce didacticiel, les extraits de code PowerShell utilisent ces variables pour stocker ces informations.</span><span class="sxs-lookup"><span data-stu-id="8b842-114">The PowerShell snippets in this tutorial use these variables to store this information</span></span>

```powershell
$subId = "<SubscriptionId>"
$rg = "<ResourceGroupName>"
$adla = "<DataLakeAnalyticsAccountName>"
$adls = "<DataLakeStoreAccountName>"
$location = "<Location>"
```

## <a name="log-in"></a><span data-ttu-id="8b842-115">Se connecter</span><span class="sxs-lookup"><span data-stu-id="8b842-115">Log in</span></span>

<span data-ttu-id="8b842-116">Connectez-vous à l’aide d’un ID d’abonnement.</span><span class="sxs-lookup"><span data-stu-id="8b842-116">Log in using a subscription id.</span></span>

```powershell
Login-AzureRmAccount -SubscriptionId $subId
```

<span data-ttu-id="8b842-117">Connectez-vous à l’aide d’un nom d’abonnement.</span><span class="sxs-lookup"><span data-stu-id="8b842-117">Log in using a subscription name.</span></span>

```
Login-AzureRmAccount -SubscriptionName $subname 
```

<span data-ttu-id="8b842-118">La cmdlet `Login-AzureRmAccount` demande toujours les informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="8b842-118">The `Login-AzureRmAccount` cmdlet  always prompts for credentials.</span></span> <span data-ttu-id="8b842-119">Vous pouvez éviter cela à l’aide des cmdlets suivantes :</span><span class="sxs-lookup"><span data-stu-id="8b842-119">You can avoid being prompted by using the following cmdlets:</span></span>

```powershell
# Save login session information
Save-AzureRmProfile -Path D:\profile.json  

# Load login session information
Select-AzureRmProfile -Path D:\profile.json 
```

## <a name="managing-accounts"></a><span data-ttu-id="8b842-120">Gérer des comptes</span><span class="sxs-lookup"><span data-stu-id="8b842-120">Managing accounts</span></span>

### <a name="create-a-data-lake-analytics-account"></a><span data-ttu-id="8b842-121">Créer un compte Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="8b842-121">Create a Data Lake Analytics account</span></span>

<span data-ttu-id="8b842-122">Si vous ne disposez pas d’un [groupe de ressources](../azure-resource-manager/resource-group-overview.md#resource-groups), créez-en un.</span><span class="sxs-lookup"><span data-stu-id="8b842-122">If you don't already have a [resource group](../azure-resource-manager/resource-group-overview.md#resource-groups) to use, create one.</span></span> 

```powershell
New-AzureRmResourceGroup -Name  $rg -Location $location
```

<span data-ttu-id="8b842-123">Chaque compte Data Lake Analytics nécessite un compte Data Lake Store par défaut pour stocker les journaux.</span><span class="sxs-lookup"><span data-stu-id="8b842-123">Every Data Lake Analytics account requires a default Data Lake Store account that it uses for storing logs.</span></span> <span data-ttu-id="8b842-124">Vous pouvez réutiliser un compte ou en créer un.</span><span class="sxs-lookup"><span data-stu-id="8b842-124">You can reuse an existing account or create an account.</span></span> 

```powershell
New-AdlStore -ResourceGroupName $rg -Name $adls -Location $location
```

<span data-ttu-id="8b842-125">Lorsqu’un groupe de ressources et un compte Data Lake Store sont disponibles, créez un compte Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="8b842-125">Once a Resource Group and Data Lake Store account is available, create a Data Lake Analytics account.</span></span>

```powershell
New-AdlAnalyticsAccount -ResourceGroupName $rg -Name $adla -Location $location -DefaultDataLake $adls
```

### <a name="get-information-about-an-account"></a><span data-ttu-id="8b842-126">Obtenir des informations sur un compte</span><span class="sxs-lookup"><span data-stu-id="8b842-126">Get information about an account</span></span>

<span data-ttu-id="8b842-127">Obtenez les détails relatifs à un compte.</span><span class="sxs-lookup"><span data-stu-id="8b842-127">Get details about an account.</span></span>

```powershell
Get-AdlAnalyticsAccount -Name $adla
```

<span data-ttu-id="8b842-128">Vérifiez l’existence d’un compte Data Lake Analytics spécifique.</span><span class="sxs-lookup"><span data-stu-id="8b842-128">Check the existence of a specific Data Lake Analytics account.</span></span> <span data-ttu-id="8b842-129">La cmdlet retourne `True` ou `False`.</span><span class="sxs-lookup"><span data-stu-id="8b842-129">The cmdlet returns either `True` or `False`.</span></span>

```powershell
Test-AdlAnalyticsAccount -Name $adla
```

<span data-ttu-id="8b842-130">Vérifiez l’existence d’un compte Data Lake Store spécifique.</span><span class="sxs-lookup"><span data-stu-id="8b842-130">Check the existence of a specific Data Lake Store account.</span></span> <span data-ttu-id="8b842-131">La cmdlet retourne `True` ou `False`.</span><span class="sxs-lookup"><span data-stu-id="8b842-131">The cmdlet returns either `True` or `False`.</span></span>

```powershell
Test-AdlStoreAccount -Name $adls
```

### <a name="listing-accounts"></a><span data-ttu-id="8b842-132">Lister les comptes</span><span class="sxs-lookup"><span data-stu-id="8b842-132">Listing accounts</span></span>

<span data-ttu-id="8b842-133">Listez les comptes Data Lake Analytics dans l’abonnement sélectionné.</span><span class="sxs-lookup"><span data-stu-id="8b842-133">List Data Lake Analytics accounts within the current subscription.</span></span>

```powershell
Get-AdlAnalyticsAccount
```

<span data-ttu-id="8b842-134">Listez les comptes Data Lake Analytics dans un groupe de ressources spécifique.</span><span class="sxs-lookup"><span data-stu-id="8b842-134">List Data Lake Analytics accounts within a specific resource group.</span></span>

```powershell
Get-AdlAnalyticsAccount -ResourceGroupName $rg
```

## <a name="managing-firewall-rules"></a><span data-ttu-id="8b842-135">Gérer les règles de pare-feu</span><span class="sxs-lookup"><span data-stu-id="8b842-135">Managing firewall rules</span></span>

<span data-ttu-id="8b842-136">Listez les règles de pare-feu.</span><span class="sxs-lookup"><span data-stu-id="8b842-136">List firewall rules.</span></span>

```powershell
Get-AdlAnalyticsFirewallRule -Account $adla
```

<span data-ttu-id="8b842-137">Ajoutez une règle de pare-feu.</span><span class="sxs-lookup"><span data-stu-id="8b842-137">Add a firewall rule.</span></span>

```powershell
$ruleName = "Allow access from on-prem server"
$startIpAddress = "<start IP address>"
$endIpAddress = "<end IP address>"

Add-AdlAnalyticsFirewallRule -Account $adla -Name $ruleName -StartIpAddress $startIpAddress -EndIpAddress $endIpAddress
```

<span data-ttu-id="8b842-138">Modifiez une règle de pare-feu.</span><span class="sxs-lookup"><span data-stu-id="8b842-138">Change a firewall rule.</span></span>

```powershell
Set-AdlAnalyticsFirewallRule -Account $adla -Name $ruleName -StartIpAddress $startIpAddress -EndIpAddress $endIpAddress
```

<span data-ttu-id="8b842-139">Supprimez une règle de pare-feu.</span><span class="sxs-lookup"><span data-stu-id="8b842-139">Remove a firewall rule.</span></span>

```powershell
Remove-AdlAnalyticsFirewallRule -Account $adla -Name $ruleName
```



<span data-ttu-id="8b842-140">Autorisez des adresses IP Azure.</span><span class="sxs-lookup"><span data-stu-id="8b842-140">Allow Azure IP addresses.</span></span>

```powershell
Set-AdlAnalyticsAccount -Name $adla -AllowAzureIpState Enabled
```

```powershell
Set-AdlAnalyticsAccount -Name $adla -FirewallState Enabled
Set-AdlAnalyticsAccount -Name $adla -FirewallState Disabled
```

## <a name="managing-data-sources"></a><span data-ttu-id="8b842-141">Gérer les sources de données</span><span class="sxs-lookup"><span data-stu-id="8b842-141">Managing data sources</span></span>
<span data-ttu-id="8b842-142">Azure Data Lake Analytics prend actuellement en charge les sources de données suivantes :</span><span class="sxs-lookup"><span data-stu-id="8b842-142">Azure Data Lake Analytics currently supports the following data sources:</span></span>

* [<span data-ttu-id="8b842-143">Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="8b842-143">Azure Data Lake Store</span></span>](../data-lake-store/data-lake-store-overview.md)
* [<span data-ttu-id="8b842-144">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="8b842-144">Azure Storage</span></span>](../storage/common/storage-introduction.md)

<span data-ttu-id="8b842-145">Quand vous créez un compte Analytics, vous devez désigner un compte Data Lake Store comme source de données par défaut.</span><span class="sxs-lookup"><span data-stu-id="8b842-145">When you create an Analytics account, you must designate a Data Lake Store account to be the default data source.</span></span> <span data-ttu-id="8b842-146">Le compte Data Lake Store par défaut est utilisé pour stocker les métadonnées du travail et les journaux d'audit du travail.</span><span class="sxs-lookup"><span data-stu-id="8b842-146">The default Data Lake Store account is used to store job metadata and job audit logs.</span></span> <span data-ttu-id="8b842-147">Après la création d'un compte Data Lake Analytics, vous pouvez ajouter des comptes Data Lake Store et/ou des comptes de stockage supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="8b842-147">After you have created a Data Lake Analytics account, you can add additional Data Lake Store accounts and/or Storage accounts.</span></span> 

### <a name="find-the-default-data-lake-store-account"></a><span data-ttu-id="8b842-148">Rechercher le compte Data Lake Store par défaut</span><span class="sxs-lookup"><span data-stu-id="8b842-148">Find the default Data Lake Store account</span></span>

```powershell
$adla_acct = Get-AdlAnalyticsAccount -Name $adla
$dataLakeStoreName = $adla_acct.DefaultDataLakeAccount
```

<span data-ttu-id="8b842-149">Vous trouverez le compte Data Lake Store par défaut en filtrant la liste des sources de données par le `IsDefault` propriété :</span><span class="sxs-lookup"><span data-stu-id="8b842-149">You can find the default Data Lake Store account by filtering the list of datasources by the `IsDefault` property:</span></span>

```powershell
Get-AdlAnalyticsDataSource -Account $adla  | ? { $_.IsDefault } 
```

### <a name="add-a-data-source"></a><span data-ttu-id="8b842-150">Ajouter une source de données</span><span class="sxs-lookup"><span data-stu-id="8b842-150">Add a data source</span></span>

```powershell

# Add an additional Storage (Blob) account.
$AzureStorageAccountName = "<AzureStorageAccountName>"
$AzureStorageAccountKey = "<AzureStorageAccountKey>"
Add-AdlAnalyticsDataSource -Account $adla -Blob $AzureStorageAccountName -AccessKey $AzureStorageAccountKey

# Add an additional Data Lake Store account.
$AzureDataLakeStoreName = "<AzureDataLakeStoreAccountName"
Add-AdlAnalyticsDataSource -Account $adla -DataLakeStore $AzureDataLakeStoreName 
```

### <a name="list-data-sources"></a><span data-ttu-id="8b842-151">Lister les sources de données</span><span class="sxs-lookup"><span data-stu-id="8b842-151">List data sources</span></span>

```powershell
# List all the data sources
Get-AdlAnalyticsDataSource -Name $adla

# List attached Data Lake Store accounts
Get-AdlAnalyticsDataSource -Name $adla | where -Property Type -EQ "DataLakeStore"

# List attached Storage accounts
Get-AdlAnalyticsDataSource -Name $adla | where -Property Type -EQ "Blob"
```

## <a name="submit-u-sql-jobs"></a><span data-ttu-id="8b842-152">Envoyer des travaux U-SQL</span><span class="sxs-lookup"><span data-stu-id="8b842-152">Submit U-SQL jobs</span></span>

### <a name="submit-a-string-as-a-u-sql-script"></a><span data-ttu-id="8b842-153">Envoyer une chaîne en tant que script U-SQL</span><span class="sxs-lookup"><span data-stu-id="8b842-153">Submit a string as a U-SQL script</span></span>

```powershell
$script = @"
@a  = 
    SELECT * FROM 
        (VALUES
            ("Contoso", 1500.0),
            ("Woodgrove", 2700.0)
        ) AS D( customer, amount );
OUTPUT @a
    TO "/data.csv"
    USING Outputters.Csv();
"@

$scriptpath = "d:\test.usql"
$script | Out-File $scriptpath 

Submit-AdlJob -AccountName $adla -Script $script -Name "Demo"
```


### <a name="submit-a-file-as-a-u-sql-script"></a><span data-ttu-id="8b842-154">Envoyer un fichier en tant que script U-SQL</span><span class="sxs-lookup"><span data-stu-id="8b842-154">Submit a file as a U-SQL script</span></span>

```powershell
$scriptpath = "d:\test.usql"
$script | Out-File $scriptpath 
Submit-AdlJob -AccountName $adla –ScriptPath $scriptpath -Name "Demo"
```

## <a name="list-jobs-in-an-account"></a><span data-ttu-id="8b842-155">Lister des travaux dans un compte</span><span class="sxs-lookup"><span data-stu-id="8b842-155">List jobs in an account</span></span>

### <a name="list-all-the-jobs-in-the-account"></a><span data-ttu-id="8b842-156">Affichez la liste de tous les travaux dans le compte.</span><span class="sxs-lookup"><span data-stu-id="8b842-156">List all the jobs in the account.</span></span> 

<span data-ttu-id="8b842-157">La sortie comprend les travaux en cours et ceux qui ont été terminés récemment.</span><span class="sxs-lookup"><span data-stu-id="8b842-157">The output includes the currently running jobs and those jobs that have recently completed.</span></span>

```powershell
Get-AdlJob -Account $adla
```


### <a name="list-a-specific-number-of-jobs"></a><span data-ttu-id="8b842-158">Lister un nombre spécifique de travaux</span><span class="sxs-lookup"><span data-stu-id="8b842-158">List a specific number of jobs</span></span>

<span data-ttu-id="8b842-159">Par défaut, la liste des travaux est triée en fonction de l’heure d’envoi.</span><span class="sxs-lookup"><span data-stu-id="8b842-159">By default the list of jobs is sorted on submit time.</span></span> <span data-ttu-id="8b842-160">Par conséquent, les travaux envoyés le plus récemment s’affichent en premier.</span><span class="sxs-lookup"><span data-stu-id="8b842-160">So the most recently submitted jobs appear first.</span></span> <span data-ttu-id="8b842-161">Par défaut, le compte ADLA garde en mémoire les travaux pendant 180 jours, mais la cmdlet AdlJob-Ge ne retourne par défaut que les 500 premiers travaux.</span><span class="sxs-lookup"><span data-stu-id="8b842-161">By default, The ADLA account remembers jobs for 180 days, but the Ge-AdlJob  cmdlet by default returns only the first 500.</span></span> <span data-ttu-id="8b842-162">Utilisez le paramètre -Top pour lister un nombre spécifique de travaux.</span><span class="sxs-lookup"><span data-stu-id="8b842-162">Use -Top parameter to list a specific number of jobs.</span></span>

```powershell
$jobs = Get-AdlJob -Account $adla -Top 10
```


### <a name="list-jobs-based-on-the-value-of-job-property"></a><span data-ttu-id="8b842-163">Lister les travaux en fonction de la valeur de la propriété du travail</span><span class="sxs-lookup"><span data-stu-id="8b842-163">List jobs based on the value of job property</span></span>

<span data-ttu-id="8b842-164">Utilisation du `-State` paramètre.</span><span class="sxs-lookup"><span data-stu-id="8b842-164">Using the `-State` parameter.</span></span> <span data-ttu-id="8b842-165">Vous pouvez combiner chacune de ces valeurs :</span><span class="sxs-lookup"><span data-stu-id="8b842-165">You can combine any of these values:</span></span>

* `Accepted`
* `Compiling`
* `Ended`
* `New`
* `Paused`
* `Queued`
* `Running`
* `Scheduling`
* `Start`

```powershell
# List the running jobs
Get-AdlJob -Account $adla -State Running

# List the jobs that have completed
Get-AdlJob -Account $adla -State Ended

# List the jobs that have not started yet
Get-AdlJob -Account $adla -State Accepted,Compiling,New,Paused,Scheduling,Start
```

<span data-ttu-id="8b842-166">Utilisez le `-Result` paramètre pour détecter si les travaux terminés se sont achevés correctement.</span><span class="sxs-lookup"><span data-stu-id="8b842-166">Use the `-Result` parameter to detect whether ended jobs completed successfully.</span></span> <span data-ttu-id="8b842-167">Il possède ces valeurs :</span><span class="sxs-lookup"><span data-stu-id="8b842-167">It has these values:</span></span>

* <span data-ttu-id="8b842-168">Annulé</span><span class="sxs-lookup"><span data-stu-id="8b842-168">Cancelled</span></span>
* <span data-ttu-id="8b842-169">Échec</span><span class="sxs-lookup"><span data-stu-id="8b842-169">Failed</span></span>
* <span data-ttu-id="8b842-170">Aucune</span><span class="sxs-lookup"><span data-stu-id="8b842-170">None</span></span>
* <span data-ttu-id="8b842-171">Réussi</span><span class="sxs-lookup"><span data-stu-id="8b842-171">Succeeded</span></span>

``` powershell
# List Successful jobs.
Get-AdlJob -Account $adla -State Ended -Result Succeeded

# List Failed jobs.
Get-AdlJob -Account $adla -State Ended -Result Failed
```


<span data-ttu-id="8b842-172">Le `-Submitter` paramètre vous permet d’identifier qui a envoyé une tâche.</span><span class="sxs-lookup"><span data-stu-id="8b842-172">The `-Submitter` parameter helps you identify who submitted a job.</span></span>

```powershell
Get-AdlJob -Account $adla -Submitter "joe@contoso.com"
```

<span data-ttu-id="8b842-173">Le paramètre `-SubmittedAfter` est utile lorsque vous filtrez dans un intervalle de temps.</span><span class="sxs-lookup"><span data-stu-id="8b842-173">The `-SubmittedAfter` is useful in filtering to a time range.</span></span>


```powershell
# List  jobs submitted in the last day.
$d = [DateTime]::Now.AddDays(-1)
Get-AdlJob -Account $adla -SubmittedAfter $d

# List  jobs submitted in the last seven day.
$d = [DateTime]::Now.AddDays(-7)
Get-AdlJob -Account $adla -SubmittedAfter $d
```

### <a name="common-scenarios-for-listing-jobs"></a><span data-ttu-id="8b842-174">Scénarios courants pour lister des travaux</span><span class="sxs-lookup"><span data-stu-id="8b842-174">Common scenarios for listing jobs</span></span>


```
# List jobs submitted in the last five days and that successfully completed.
$d = (Get-Date).AddDays(-5)
Get-AdlJob -Account $adla -SubmittedAfter $d -State Ended -Result Succeeded

# List all failed jobs submitted by "joe@contoso.com" within the past seven days.
Get-AdlJob -Account $adla `
    -Submitter "joe@contoso.com" `
    -SubmittedAfter (Get-Date).AddDays(-7) `
    -Result Failed
```

## <a name="filtering-a-list-of-jobs"></a><span data-ttu-id="8b842-175">Filtrer une liste de travaux</span><span class="sxs-lookup"><span data-stu-id="8b842-175">Filtering a list of jobs</span></span>

<span data-ttu-id="8b842-176">Dès que vous disposez d’une liste de travaux dans votre session PowerShell actuelle.</span><span class="sxs-lookup"><span data-stu-id="8b842-176">Once you have a list of jobs in your current PowerShell session.</span></span> <span data-ttu-id="8b842-177">Vous pouvez utiliser les cmdlets PowerShell normales pour filtrer la liste.</span><span class="sxs-lookup"><span data-stu-id="8b842-177">You can use normal PowerShell cmdlets to filter the list.</span></span>

<span data-ttu-id="8b842-178">Filtrer une liste de travaux sur les travaux envoyés au cours des dernières 24 heures</span><span class="sxs-lookup"><span data-stu-id="8b842-178">Filter a list of jobs to the jobs submitted in the last 24 hours</span></span>

```
$upperdate = Get-Date
$lowerdate = $upperdate.AddHours(-24)
$jobs | Where-Object { $_.EndTime -ge $lowerdate }
```

<span data-ttu-id="8b842-179">Filtrer une liste de travaux sur les travaux qui se sont terminés au cours des dernières 24 heures</span><span class="sxs-lookup"><span data-stu-id="8b842-179">Filter a list of jobs to the jobs that ended in the last 24 hours</span></span>

```
$upperdate = Get-Date
$lowerdate = $upperdate.AddHours(-24)
$jobs | Where-Object { $_.SubmitTime -ge $lowerdate }
```

<span data-ttu-id="8b842-180">Filtrer une liste de travaux sur les travaux dont l’exécution a commencé.</span><span class="sxs-lookup"><span data-stu-id="8b842-180">Filter a list of jobs to the jobs that started running.</span></span> <span data-ttu-id="8b842-181">Un travail peut échouer au moment de la compilation et donc ne jamais démarrer.</span><span class="sxs-lookup"><span data-stu-id="8b842-181">A job might fail at compile time - and so it never starts.</span></span> <span data-ttu-id="8b842-182">Examinons les travaux dont l’exécution a démarré et qui ont ensuite échoué.</span><span class="sxs-lookup"><span data-stu-id="8b842-182">Let's look at the failed jobs that actually started running and then failed.</span></span>

```powershell
$jobs | Where-Object { $_.StartTime -ne $null }
```

### <a name="analyzing-a-list-of-jobs"></a><span data-ttu-id="8b842-183">Analyser une liste de travaux</span><span class="sxs-lookup"><span data-stu-id="8b842-183">Analyzing a list of jobs</span></span>

<span data-ttu-id="8b842-184">Utilisez la cmdlet `Group-Object` pour analyser une liste de travaux.</span><span class="sxs-lookup"><span data-stu-id="8b842-184">Use the `Group-Object` cmdlet to analyze a list of jobs.</span></span>

```
# Count the number of jobs by Submitter
$jobs | Group-Object Submitter | Select -Property Count,Name

# Count the number of jobs by Result
$jobs | Group-Object Result | Select -Property Count,Name

# Count the number of jobs by State
$jobs | Group-Object State | Select -Property Count,Name

#  Count the number of jobs by DegreeOfParallelism
$jobs | Group-Object DegreeOfParallelism | Select -Property Count,Name
```
<span data-ttu-id="8b842-185">Lorsque vous effectuez une analyse, il peut être utile d’ajouter des propriétés aux objets Travail pour faciliter le filtrage et le regroupement.</span><span class="sxs-lookup"><span data-stu-id="8b842-185">When performing an analysis, it can be useful to add properties to the Job objects to make filtering and grouping simpler.</span></span> <span data-ttu-id="8b842-186">L’extrait de code suivant montre comment annoter un objet JobInfo avec des propriétés calculées.</span><span class="sxs-lookup"><span data-stu-id="8b842-186">The following  snippet shows how to annotate a JobInfo with calculated properties.</span></span>

```
function annotate_job( $j )
{
    $dic1 = @{
        Label='AUHours';
        Expression={ ($_.DegreeOfParallelism * ($_.EndTime-$_.StartTime).TotalHours)}}
    $dic2 = @{
        Label='DurationSeconds';
        Expression={ ($_.EndTime-$_.StartTime).TotalSeconds}}
    $dic3 = @{
        Label='DidRun';
        Expression={ ($_.StartTime -ne $null)}}

    $j2 = $j | select *, $dic1, $dic2, $dic3
    $j2
}

$jobs = Get-AdlJob -Account $adla -Top 10
$jobs = $jobs | %{ annotate_job( $_ ) }
```

## <a name="get-information-about-pipelines-and-recurrences"></a><span data-ttu-id="8b842-187">Obtenir des informations sur les pipelines et les périodicités</span><span class="sxs-lookup"><span data-stu-id="8b842-187">Get information about pipelines and recurrences</span></span>

<span data-ttu-id="8b842-188">Utilisez l’ `Get-AdlJobPipeline` applet de commande pour afficher les tâches déjà soumises sur les informations de pipeline.</span><span class="sxs-lookup"><span data-stu-id="8b842-188">Use the `Get-AdlJobPipeline` cmdlet to see the pipeline information previously submitted jobs.</span></span>

```powershell
$pipelines = Get-AdlJobPipeline -Account $adla

$pipeline = Get-AdlJobPipeline -Account $adla -PipelineId "<pipeline ID>"
```

<span data-ttu-id="8b842-189">Utilisez l’ `Get-AdlJobRecurrence` applet de commande pour afficher les informations sur la périodicité des tâches déjà soumises.</span><span class="sxs-lookup"><span data-stu-id="8b842-189">Use the `Get-AdlJobRecurrence` cmdlet to see the recurrence information for previously submitted jobs.</span></span>

```powershell
$recurrences = Get-AdlJobRecurrence -Account $adla

$recurrence = Get-AdlJobRecurrence -Account $adla -RecurrenceId "<recurrence ID>"
```

## <a name="get-information-about-a-job"></a><span data-ttu-id="8b842-190">Obtenir des informations sur un travail</span><span class="sxs-lookup"><span data-stu-id="8b842-190">Get information about a job</span></span>

### <a name="get-job-status"></a><span data-ttu-id="8b842-191">Obtenir l’état de la tâche</span><span class="sxs-lookup"><span data-stu-id="8b842-191">Get job status</span></span>

<span data-ttu-id="8b842-192">Affichez l’état d’un travail.</span><span class="sxs-lookup"><span data-stu-id="8b842-192">Get the status of a specific job.</span></span>

```powershell
Get-AdlJob -AccountName $adla -JobId $job.JobId
```

### <a name="examine-the-job-outputs"></a><span data-ttu-id="8b842-193">Analyser les sorties du travail</span><span class="sxs-lookup"><span data-stu-id="8b842-193">Examine the job outputs</span></span>

<span data-ttu-id="8b842-194">Dès qu’un travail est terminé, vérifiez si le fichier de sortie existe en affichant les fichiers dans un dossier.</span><span class="sxs-lookup"><span data-stu-id="8b842-194">After the job has ended, check if the output file exists by listing the files in a folder.</span></span>

```powershell
Get-AdlStoreChildItem -Account $adls -Path "/"
```

## <a name="manage-running-jobs"></a><span data-ttu-id="8b842-195">Gérer les tâches en cours d’exécution</span><span class="sxs-lookup"><span data-stu-id="8b842-195">Manage running jobs</span></span>

### <a name="cancel-a-job"></a><span data-ttu-id="8b842-196">Annulation d’une tâche</span><span class="sxs-lookup"><span data-stu-id="8b842-196">Cancel a job</span></span>

```powershell
Stop-AdlJob -Account $adls -JobID $jobID
```

### <a name="wait-for-a-job-to-finish"></a><span data-ttu-id="8b842-197">Attendre la fin d’une tâche</span><span class="sxs-lookup"><span data-stu-id="8b842-197">Wait for a job to finish</span></span>

<span data-ttu-id="8b842-198">Au lieu de répéter `Get-AdlAnalyticsJob` jusqu’à ce qu’un travail se termine, vous pouvez utiliser la cmdlet `Wait-AdlJob` pour attendre la fin du travail.</span><span class="sxs-lookup"><span data-stu-id="8b842-198">Instead of repeating `Get-AdlAnalyticsJob` until a job finishes, you can use the `Wait-AdlJob` cmdlet to wait for the job to end.</span></span>

```powershell
Wait-AdlJob -Account $adla -JobId $job.JobId
```

## <a name="manage-compute-policies"></a><span data-ttu-id="8b842-199">Gérer les stratégies de calcul</span><span class="sxs-lookup"><span data-stu-id="8b842-199">Manage compute policies</span></span>

### <a name="list-existing-compute-policies"></a><span data-ttu-id="8b842-200">Lister les stratégies de calcul existantes</span><span class="sxs-lookup"><span data-stu-id="8b842-200">List existing compute policies</span></span>

<span data-ttu-id="8b842-201">L’ `Get-AdlAnalyticsComputePolicy` applet de commande récupère des informations sur les stratégies de calcul pour un compte Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="8b842-201">The `Get-AdlAnalyticsComputePolicy` cmdlet retrieves info about compute policies for a Data Lake Analytics account.</span></span>

```powershell
$policies = Get-AdlAnalyticsComputePolicy -Account $adla
```

### <a name="create-a-compute-policy"></a><span data-ttu-id="8b842-202">Créer une stratégie de calcul</span><span class="sxs-lookup"><span data-stu-id="8b842-202">Create a compute policy</span></span>

<span data-ttu-id="8b842-203">L’ `New-AdlAnalyticsComputePolicy` applet de commande crée une nouvelle stratégie de calcul pour un compte Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="8b842-203">The `New-AdlAnalyticsComputePolicy` cmdlet creates a new compute policy for a Data Lake Analytics account.</span></span> <span data-ttu-id="8b842-204">Cet exemple définit les AU maximales disponibles pour l’utilisateur spécifié à 50 et la priorité minimale de la tâche à 250.</span><span class="sxs-lookup"><span data-stu-id="8b842-204">This example sets  the maximum AUs available to the specified user to 50, and the minimum job priority to 250.</span></span>

```powershell
$userObjectId = (Get-AzureRmAdUser -SearchString "garymcdaniel@contoso.com").Id

New-AdlAnalyticsComputePolicy -Account $adla -Name "GaryMcDaniel" -ObjectId $objectId -ObjectType User -MaxDegreeOfParallelismPerJob 50 -MinPriorityPerJob 250
```

## <a name="check-for-the-existence-of-a-file"></a><span data-ttu-id="8b842-205">Vérifiez l’existence d’un fichier.</span><span class="sxs-lookup"><span data-stu-id="8b842-205">Check for the existence of a file.</span></span>

```powershell
Test-AdlStoreItem -Account $adls -Path "/data.csv"
```

## <a name="uploading-and-downloading"></a><span data-ttu-id="8b842-206">Chargement et téléchargement</span><span class="sxs-lookup"><span data-stu-id="8b842-206">Uploading and downloading</span></span>

<span data-ttu-id="8b842-207">Chargez un fichier.</span><span class="sxs-lookup"><span data-stu-id="8b842-207">Upload a file.</span></span>

```powershell
Import-AdlStoreItem -AccountName $adls -Path "c:\data.tsv" -Destination "/data_copy.csv" 
```

<span data-ttu-id="8b842-208">Chargez un dossier entier de manière récursive.</span><span class="sxs-lookup"><span data-stu-id="8b842-208">Upload an entire folder recursively.</span></span>

```powershell
Import-AdlStoreItem -AccountName $adls -Path "c:\myData\" -Destination "/myData/" -Recurse
```

<span data-ttu-id="8b842-209">Téléchargez un fichier.</span><span class="sxs-lookup"><span data-stu-id="8b842-209">Download a file.</span></span>

```powershell
Export-AdlStoreItem -AccountName $adls -Path "/data.csv" -Destination "c:\data.csv"
```

<span data-ttu-id="8b842-210">Téléchargez un dossier entier de manière récursive.</span><span class="sxs-lookup"><span data-stu-id="8b842-210">Download an entire folder recursively.</span></span>

```powershell
Export-AdlStoreItem -AccountName $adls -Path "/" -Destination "c:\myData\" -Recurse
```

> [!NOTE]
> <span data-ttu-id="8b842-211">Si le processus de chargement ou de téléchargement est interrompu, vous pouvez tenter de reprendre le processus en exécutant à nouveau la cmdlet avec l’indicateur ``-Resume``.</span><span class="sxs-lookup"><span data-stu-id="8b842-211">If the upload or download process is interrupted, you can attempt to resume the process by running the cmdlet again with the ``-Resume`` flag.</span></span>

## <a name="manage-catalog-items"></a><span data-ttu-id="8b842-212">Gestion des éléments du catalogue</span><span class="sxs-lookup"><span data-stu-id="8b842-212">Manage catalog items</span></span>

<span data-ttu-id="8b842-213">Le catalogue U-SQL est utilisé pour structurer les données et le code afin que les scripts U-SQL puissent les partager.</span><span class="sxs-lookup"><span data-stu-id="8b842-213">The U-SQL catalog is used to structure data and code so they can be shared by U-SQL scripts.</span></span> <span data-ttu-id="8b842-214">Le catalogue permet les meilleures performances possibles avec les données comprises dans Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="8b842-214">The catalog enables the highest performance possible with data in Azure Data Lake.</span></span> <span data-ttu-id="8b842-215">Pour plus d'informations, consultez [Utilisation du catalogue U-SQL](data-lake-analytics-use-u-sql-catalog.md).</span><span class="sxs-lookup"><span data-stu-id="8b842-215">For more information, see [Use U-SQL catalog](data-lake-analytics-use-u-sql-catalog.md).</span></span>

### <a name="list-items-in-the-u-sql-catalog"></a><span data-ttu-id="8b842-216">Lister les éléments dans le catalogue U-SQL</span><span class="sxs-lookup"><span data-stu-id="8b842-216">List items in the U-SQL catalog</span></span>

```powershell
# List U-SQL databases
Get-AdlCatalogItem -Account $adla -ItemType Database 

# List tables within a database
Get-AdlCatalogItem -Account $adla -ItemType Table -Path "database"

# List tables within a schema.
Get-AdlCatalogItem -Account $adla -ItemType Table -Path "database.schema"
```

<span data-ttu-id="8b842-217">Listez tous les assemblys dans toutes les bases de données d’un compte ADLA.</span><span class="sxs-lookup"><span data-stu-id="8b842-217">List all the assemblies in all the databases in an ADLA Account.</span></span>

```powershell
$dbs = Get-AdlCatalogItem -Account $adla -ItemType Database

foreach ($db in $dbs)
{
    $asms = Get-AdlCatalogItem -Account $adla -ItemType Assembly -Path $db.Name

    foreach ($asm in $asms)
    {
        $asmname = "[" + $db.Name + "].[" + $asm.Name + "]"
        Write-Host $asmname
    }
}
```

### <a name="get-details-about-a-catalog-item"></a><span data-ttu-id="8b842-218">Obtenir des détails sur un élément de catalogue</span><span class="sxs-lookup"><span data-stu-id="8b842-218">Get details about a catalog item</span></span>

```powershell
# Get details of a table
Get-AdlCatalogItem  -Account $adla -ItemType Table -Path "master.dbo.mytable"

# Test existence of a U-SQL database.
Test-AdlCatalogItem  -Account $adla -ItemType Database -Path "master"
```

### <a name="create-credentials-in-a-catalog"></a><span data-ttu-id="8b842-219">Créer des informations d’identification dans un catalogue</span><span class="sxs-lookup"><span data-stu-id="8b842-219">Create credentials in a catalog</span></span>

<span data-ttu-id="8b842-220">Dans une base de données U-SQL, créez un objet informations d’identification pour une base de données hébergée dans Azure.</span><span class="sxs-lookup"><span data-stu-id="8b842-220">Within a U-SQL database, create a credential object for a database hosted in Azure.</span></span> <span data-ttu-id="8b842-221">Actuellement, les informations d’identification U-SQL sont le seul type d’élément de catalogue que vous pouvez créer via PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8b842-221">Currently, U-SQL credentials are the only type of catalog item that you can create through PowerShell.</span></span>

```powershell
$dbName = "master"
$credentialName = "ContosoDbCreds"
$dbUri = "https://contoso.database.windows.net:8080"

New-AdlCatalogCredential -AccountName $adla `
          -DatabaseName $db `
          -CredentialName $credentialName `
          -Credential (Get-Credential) `
          -Uri $dbUri
```

### <a name="get-basic-information-about-an-adla-account"></a><span data-ttu-id="8b842-222">Obtenir des informations de base sur un compte ADLA</span><span class="sxs-lookup"><span data-stu-id="8b842-222">Get basic information about an ADLA account</span></span>

<span data-ttu-id="8b842-223">À l’aide du nom d’un compte, le code suivant recherche des informations de base sur ce compte</span><span class="sxs-lookup"><span data-stu-id="8b842-223">Given an account name, the following code looks up basic information about the account</span></span>

```
$adla_acct = Get-AdlAnalyticsAccount -Name "saveenrdemoadla"
$adla_name = $adla_acct.Name
$adla_subid = $adla_acct.Id.Split("/")[2]
$adla_sub = Get-AzureRmSubscription -SubscriptionId $adla_subid
$adla_subname = $adla_sub.Name
$adla_defadls_datasource = Get-AdlAnalyticsDataSource -Account $adla_name  | ? { $_.IsDefault } 
$adla_defadlsname = $adla_defadls_datasource.Name

Write-Host "ADLA Account Name" $adla_name
Write-Host "Subscription Id" $adla_subid
Write-Host "Subscription Name" $adla_subname
Write-Host "Defautl ADLS Store" $adla_defadlsname
Write-Host 

Write-Host '$subname' " = ""$adla_subname"" "
Write-Host '$subid' " = ""$adla_subid"" "
Write-Host '$adla' " = ""$adla_name"" "
Write-Host '$adls' " = ""$adla_defadlsname"" "
```

## <a name="working-with-azure"></a><span data-ttu-id="8b842-224">Utilisation d’Azure</span><span class="sxs-lookup"><span data-stu-id="8b842-224">Working with Azure</span></span>

### <a name="get-details-of-azurerm-errors"></a><span data-ttu-id="8b842-225">Obtenir des détails sur les erreurs AzureRm</span><span class="sxs-lookup"><span data-stu-id="8b842-225">Get details of AzureRm errors</span></span>

```powershell
Resolve-AzureRmError -Last
```

### <a name="verify-if-you-are-running-as-an-administrator"></a><span data-ttu-id="8b842-226">Vérifier que vous exécutez en tant qu’administrateur</span><span class="sxs-lookup"><span data-stu-id="8b842-226">Verify if you are running as an administrator</span></span>

```powershell
function Test-Administrator  
{  
    $user = [Security.Principal.WindowsIdentity]::GetCurrent();
    $p = New-Object Security.Principal.WindowsPrincipal $user
    $p.IsInRole([Security.Principal.WindowsBuiltinRole]::Administrator)  
}
```

### <a name="find-a-tenantid"></a><span data-ttu-id="8b842-227">Trouver un TenantID</span><span class="sxs-lookup"><span data-stu-id="8b842-227">Find a TenantID</span></span>

<span data-ttu-id="8b842-228">À partir du nom d’un abonnement :</span><span class="sxs-lookup"><span data-stu-id="8b842-228">From a subscription name:</span></span>

```powershell
function Get-TenantIdFromSubcriptionName( [string] $subname )
{
    $sub = (Get-AzureRmSubscription -SubscriptionName $subname)
    $sub.TenantId
}

Get-TenantIdFromSubcriptionName "ADLTrainingMS"
```

<span data-ttu-id="8b842-229">À partir de l’ID d’un abonnement :</span><span class="sxs-lookup"><span data-stu-id="8b842-229">From a subscription id:</span></span>

```powershell
function Get-TenantIdFromSubcriptionId( [string] $subid )
{
    $sub = (Get-AzureRmSubscription -SubscriptionId $subid)
    $sub.TenantId
}

$subid = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
Get-TenantIdFromSubcriptionId $subid
```

<span data-ttu-id="8b842-230">À partir d’une adresse de domaine, comme « contoso.com »</span><span class="sxs-lookup"><span data-stu-id="8b842-230">From a domain address such as "contoso.com"</span></span>


```powershell
function Get-TenantIdFromDomain( $domain )
{
    $url = "https://login.windows.net/" + $domain + "/.well-known/openid-configuration"
    return (Invoke-WebRequest $url|ConvertFrom-Json).token_endpoint.Split('/')[3]
}

$domain = "contoso.com"
Get-TenantIdFromDomain $domain
```

### <a name="list-all-your-subscriptions-and-tenant-ids"></a><span data-ttu-id="8b842-231">Lister tous vos abonnements et leur ID client</span><span class="sxs-lookup"><span data-stu-id="8b842-231">List all your subscriptions and tenant ids</span></span>

```powershell
$subs = Get-AzureRmSubscription
foreach ($sub in $subs)
{
    Write-Host $sub.Name "("  $sub.Id ")"
    Write-Host "`tTenant Id" $sub.TenantId
}
```

## <a name="create-a-data-lake-analytics-account-using-a-template"></a><span data-ttu-id="8b842-232">Créer un compte Data Lake Analytics à l’aide d’un modèle</span><span class="sxs-lookup"><span data-stu-id="8b842-232">Create a Data Lake Analytics account using a template</span></span>

<span data-ttu-id="8b842-233">Vous pouvez également utiliser un modèle de groupe de ressources Azure à l’aide du script PowerShell suivant :</span><span class="sxs-lookup"><span data-stu-id="8b842-233">You can also use an Azure Resource Group template using the following  PowerShell script:</span></span>

```powershell
$subId = "<Your Azure Subscription ID>"

$rg = "<New Azure Resource Group Name>"
$location = "<Location (such as East US 2)>"
$adls = "<New Data Lake Store Account Name>"
$adla = "<New Data Lake Analytics Account Name>"

$deploymentName = "MyDataLakeAnalyticsDeployment"
$armTemplateFile = "<LocalFolderPath>\azuredeploy.json"  # update the JSON template path 

# Log in to Azure
Login-AzureRmAccount -SubscriptionId $subId

# Create the resource group
New-AzureRmResourceGroup -Name $rg -Location $location

# Create the Data Lake Analytics account with the default Data Lake Store account.
$parameters = @{"adlAnalyticsName"=$adla; "adlStoreName"=$adls}
New-AzureRmResourceGroupDeployment -Name $deploymentName -ResourceGroupName $rg -TemplateFile $armTemplateFile -TemplateParameterObject $parameters 
```

<span data-ttu-id="8b842-234">Pour plus d’informations, consultez [Déploiement d’une application avec un modèle Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md) et [Création de modèles Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="8b842-234">For more information, see [Deploy an application with Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md) and [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="8b842-235">**Exemple de modèle**</span><span class="sxs-lookup"><span data-stu-id="8b842-235">**Example template**</span></span>

<span data-ttu-id="8b842-236">Enregistrez le texte suivant en tant que fichier `.json`, puis utilisez le script PowerShell précédent pour utiliser le modèle.</span><span class="sxs-lookup"><span data-stu-id="8b842-236">Save the following text as a `.json` file, and then use the preceding PowerShell script to use the template.</span></span> 

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "adlAnalyticsName": {
      "type": "string",
      "metadata": {
        "description": "The name of the Data Lake Analytics account to create."
      }
    },
    "adlStoreName": {
      "type": "string",
      "metadata": {
        "description": "The name of the Data Lake Store account to create."
      }
    }
  },
  "resources": [
    {
      "name": "[parameters('adlStoreName')]",
      "type": "Microsoft.DataLakeStore/accounts",
      "location": "East US 2",
      "apiVersion": "2015-10-01-preview",
      "dependsOn": [ ],
      "tags": { }
    },
    {
      "name": "[parameters('adlAnalyticsName')]",
      "type": "Microsoft.DataLakeAnalytics/accounts",
      "location": "East US 2",
      "apiVersion": "2015-10-01-preview",
      "dependsOn": [ "[concat('Microsoft.DataLakeStore/accounts/',parameters('adlStoreName'))]" ],
      "tags": { },
      "properties": {
        "defaultDataLakeStoreAccount": "[parameters('adlStoreName')]",
        "dataLakeStoreAccounts": [
          { "name": "[parameters('adlStoreName')]" }
        ]
      }
    }
  ],
  "outputs": {
    "adlAnalyticsAccount": {
      "type": "object",
      "value": "[reference(resourceId('Microsoft.DataLakeAnalytics/accounts',parameters('adlAnalyticsName')))]"
    },
    "adlStoreAccount": {
      "type": "object",
      "value": "[reference(resourceId('Microsoft.DataLakeStore/accounts',parameters('adlStoreName')))]"
    }
  }
}
```

## <a name="next-steps"></a><span data-ttu-id="8b842-237">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8b842-237">Next steps</span></span>
* [<span data-ttu-id="8b842-238">Vue d'ensemble de Microsoft Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="8b842-238">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* <span data-ttu-id="8b842-239">Prise en main de Data Lake Analytics à l’aide du [portail Azure](data-lake-analytics-get-started-portal.md) | [Azure PowerShell](data-lake-analytics-get-started-powershell.md) | [CLI 2.0](data-lake-analytics-get-started-cli2.md)</span><span class="sxs-lookup"><span data-stu-id="8b842-239">Get started with Data Lake Analytics using [Azure portal](data-lake-analytics-get-started-portal.md) | [Azure PowerShell](data-lake-analytics-get-started-powershell.md) | [CLI 2.0](data-lake-analytics-get-started-cli2.md)</span></span>
* <span data-ttu-id="8b842-240">Gérer Azure Data Lake Analytics à l’aide du [portail Azure](data-lake-analytics-manage-use-portal.md) | [Azure PowerShell](data-lake-analytics-manage-use-powershell.md) | [CLI](data-lake-analytics-manage-use-cli.md)</span><span class="sxs-lookup"><span data-stu-id="8b842-240">Manage Azure Data Lake Analytics using [Azure portal](data-lake-analytics-manage-use-portal.md) | [Azure PowerShell](data-lake-analytics-manage-use-powershell.md) | [CLI](data-lake-analytics-manage-use-cli.md)</span></span> 
