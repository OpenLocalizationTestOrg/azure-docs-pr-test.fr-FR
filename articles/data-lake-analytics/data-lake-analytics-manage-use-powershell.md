---
title: "aaaManage Analytique de LAC de données Azure à l’aide d’Azure PowerShell | Documents Microsoft"
description: "Découvrez comment les comptes toomanage Analytique lac de données, sources de données, des travaux et des éléments de catalogue. "
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
ms.openlocfilehash: 5954f0efb7d5a9778727edfccae83aec046343bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-data-lake-analytics-using-azure-powershell"></a><span data-ttu-id="f2804-103">Gestion d'Azure Data Lake Analytics à l'aide d'Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="f2804-103">Manage Azure Data Lake Analytics using Azure PowerShell</span></span>
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

<span data-ttu-id="f2804-104">Découvrez comment les comptes d’Analytique de LAC de données Azure toomanage, sources de données, des travaux et des éléments de catalogue à l’aide d’Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f2804-104">Learn how toomanage Azure Data Lake Analytics accounts, data sources, jobs, and catalog items using Azure PowerShell.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="f2804-105">Composants requis</span><span class="sxs-lookup"><span data-stu-id="f2804-105">Prerequisites</span></span>

<span data-ttu-id="f2804-106">Lorsque vous créez un compte Analytique lac de données, vous devez tooknow :</span><span class="sxs-lookup"><span data-stu-id="f2804-106">When creating a Data Lake Analytics account, you need tooknow:</span></span>

* <span data-ttu-id="f2804-107">**ID d’abonnement**: hello ID d’abonnement Azure sous lequel réside votre compte Analytique lac de données.</span><span class="sxs-lookup"><span data-stu-id="f2804-107">**Subscription ID**: hello Azure subscription ID under which your Data Lake Analytics account resides.</span></span>
* <span data-ttu-id="f2804-108">**Groupe de ressources**: nom hello hello Azure du groupe de ressources qui contient votre compte Analytique lac de données.</span><span class="sxs-lookup"><span data-stu-id="f2804-108">**Resource group**: hello name of hello Azure resource group that contains your Data Lake Analytics account.</span></span>
* <span data-ttu-id="f2804-109">**Nom du compte Analytique lac de données**: hello compte nom doit contenir uniquement des lettres minuscules et chiffres.</span><span class="sxs-lookup"><span data-stu-id="f2804-109">**Data Lake Analytics account name**: hello account name must only contain lowercase letters and numbers.</span></span>
* <span data-ttu-id="f2804-110">**Compte Data Lake Store par défaut** : chaque compte Data Lake Analytics possède un compte Data Lake Store par défaut.</span><span class="sxs-lookup"><span data-stu-id="f2804-110">**Default Data Lake Store account**: Each Data Lake Analytics account has a default Data Lake Store account.</span></span> <span data-ttu-id="f2804-111">Ces comptes doivent être Bonjour même emplacement.</span><span class="sxs-lookup"><span data-stu-id="f2804-111">These accounts must be in hello same location.</span></span>
* <span data-ttu-id="f2804-112">**Emplacement**: prise en charge d’emplacement hello de votre compte Analytique lac de données, telles que « Est des États-Unis 2 » ou d’autres emplacements.</span><span class="sxs-lookup"><span data-stu-id="f2804-112">**Location**: hello location of your Data Lake Analytics account, such as "East US 2" or other supported locations.</span></span> <span data-ttu-id="f2804-113">Les emplacements pris en charge sont indiqués sur notre [page de tarification](https://azure.microsoft.com/pricing/details/data-lake-analytics/).</span><span class="sxs-lookup"><span data-stu-id="f2804-113">Supported locations can be seen on our [pricing page](https://azure.microsoft.com/pricing/details/data-lake-analytics/).</span></span>

<span data-ttu-id="f2804-114">extraits de code PowerShell Hello dans ce didacticiel utilisent ces toostore variables ces informations</span><span class="sxs-lookup"><span data-stu-id="f2804-114">hello PowerShell snippets in this tutorial use these variables toostore this information</span></span>

```powershell
$subId = "<SubscriptionId>"
$rg = "<ResourceGroupName>"
$adla = "<DataLakeAnalyticsAccountName>"
$adls = "<DataLakeStoreAccountName>"
$location = "<Location>"
```

## <a name="log-in"></a><span data-ttu-id="f2804-115">Se connecter</span><span class="sxs-lookup"><span data-stu-id="f2804-115">Log in</span></span>

<span data-ttu-id="f2804-116">Connectez-vous à l’aide d’un ID d’abonnement.</span><span class="sxs-lookup"><span data-stu-id="f2804-116">Log in using a subscription id.</span></span>

```powershell
Login-AzureRmAccount -SubscriptionId $subId
```

<span data-ttu-id="f2804-117">Connectez-vous à l’aide d’un nom d’abonnement.</span><span class="sxs-lookup"><span data-stu-id="f2804-117">Log in using a subscription name.</span></span>

```
Login-AzureRmAccount -SubscriptionName $subname 
```

<span data-ttu-id="f2804-118">Hello `Login-AzureRmAccount` applet de commande toujours vous invite à entrer des informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="f2804-118">hello `Login-AzureRmAccount` cmdlet  always prompts for credentials.</span></span> <span data-ttu-id="f2804-119">Vous pouvez éviter d’être invité à l’aide de hello suivant d’applets de commande :</span><span class="sxs-lookup"><span data-stu-id="f2804-119">You can avoid being prompted by using hello following cmdlets:</span></span>

```powershell
# Save login session information
Save-AzureRmProfile -Path D:\profile.json  

# Load login session information
Select-AzureRmProfile -Path D:\profile.json 
```

## <a name="managing-accounts"></a><span data-ttu-id="f2804-120">Gérer des comptes</span><span class="sxs-lookup"><span data-stu-id="f2804-120">Managing accounts</span></span>

### <a name="create-a-data-lake-analytics-account"></a><span data-ttu-id="f2804-121">Créer un compte Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="f2804-121">Create a Data Lake Analytics account</span></span>

<span data-ttu-id="f2804-122">Si vous n’avez pas déjà un [groupe de ressources](../azure-resource-manager/resource-group-overview.md#resource-groups) toouse, créez-en un.</span><span class="sxs-lookup"><span data-stu-id="f2804-122">If you don't already have a [resource group](../azure-resource-manager/resource-group-overview.md#resource-groups) toouse, create one.</span></span> 

```powershell
New-AzureRmResourceGroup -Name  $rg -Location $location
```

<span data-ttu-id="f2804-123">Chaque compte Data Lake Analytics nécessite un compte Data Lake Store par défaut pour stocker les journaux.</span><span class="sxs-lookup"><span data-stu-id="f2804-123">Every Data Lake Analytics account requires a default Data Lake Store account that it uses for storing logs.</span></span> <span data-ttu-id="f2804-124">Vous pouvez réutiliser un compte ou en créer un.</span><span class="sxs-lookup"><span data-stu-id="f2804-124">You can reuse an existing account or create an account.</span></span> 

```powershell
New-AdlStore -ResourceGroupName $rg -Name $adls -Location $location
```

<span data-ttu-id="f2804-125">Lorsqu’un groupe de ressources et un compte Data Lake Store sont disponibles, créez un compte Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="f2804-125">Once a Resource Group and Data Lake Store account is available, create a Data Lake Analytics account.</span></span>

```powershell
New-AdlAnalyticsAccount -ResourceGroupName $rg -Name $adla -Location $location -DefaultDataLake $adls
```

### <a name="get-information-about-an-account"></a><span data-ttu-id="f2804-126">Obtenir des informations sur un compte</span><span class="sxs-lookup"><span data-stu-id="f2804-126">Get information about an account</span></span>

<span data-ttu-id="f2804-127">Obtenez les détails relatifs à un compte.</span><span class="sxs-lookup"><span data-stu-id="f2804-127">Get details about an account.</span></span>

```powershell
Get-AdlAnalyticsAccount -Name $adla
```

<span data-ttu-id="f2804-128">Vérifier l’existence de hello d’un compte Analytique lac de données spécifique.</span><span class="sxs-lookup"><span data-stu-id="f2804-128">Check hello existence of a specific Data Lake Analytics account.</span></span> <span data-ttu-id="f2804-129">applet de commande Hello retourne `True` ou `False`.</span><span class="sxs-lookup"><span data-stu-id="f2804-129">hello cmdlet returns either `True` or `False`.</span></span>

```powershell
Test-AdlAnalyticsAccount -Name $adla
```

<span data-ttu-id="f2804-130">Vérifier l’existence de hello d’un compte Data Lake Store spécifique.</span><span class="sxs-lookup"><span data-stu-id="f2804-130">Check hello existence of a specific Data Lake Store account.</span></span> <span data-ttu-id="f2804-131">applet de commande Hello retourne `True` ou `False`.</span><span class="sxs-lookup"><span data-stu-id="f2804-131">hello cmdlet returns either `True` or `False`.</span></span>

```powershell
Test-AdlStoreAccount -Name $adls
```

### <a name="listing-accounts"></a><span data-ttu-id="f2804-132">Lister les comptes</span><span class="sxs-lookup"><span data-stu-id="f2804-132">Listing accounts</span></span>

<span data-ttu-id="f2804-133">Comptes d’Analytique lac de données de liste dans l’abonnement actuel de hello.</span><span class="sxs-lookup"><span data-stu-id="f2804-133">List Data Lake Analytics accounts within hello current subscription.</span></span>

```powershell
Get-AdlAnalyticsAccount
```

<span data-ttu-id="f2804-134">Listez les comptes Data Lake Analytics dans un groupe de ressources spécifique.</span><span class="sxs-lookup"><span data-stu-id="f2804-134">List Data Lake Analytics accounts within a specific resource group.</span></span>

```powershell
Get-AdlAnalyticsAccount -ResourceGroupName $rg
```

## <a name="managing-firewall-rules"></a><span data-ttu-id="f2804-135">Gérer les règles de pare-feu</span><span class="sxs-lookup"><span data-stu-id="f2804-135">Managing firewall rules</span></span>

<span data-ttu-id="f2804-136">Listez les règles de pare-feu.</span><span class="sxs-lookup"><span data-stu-id="f2804-136">List firewall rules.</span></span>

```powershell
Get-AdlAnalyticsFirewallRule -Account $adla
```

<span data-ttu-id="f2804-137">Ajoutez une règle de pare-feu.</span><span class="sxs-lookup"><span data-stu-id="f2804-137">Add a firewall rule.</span></span>

```powershell
$ruleName = "Allow access from on-prem server"
$startIpAddress = "<start IP address>"
$endIpAddress = "<end IP address>"

Add-AdlAnalyticsFirewallRule -Account $adla -Name $ruleName -StartIpAddress $startIpAddress -EndIpAddress $endIpAddress
```

<span data-ttu-id="f2804-138">Modifiez une règle de pare-feu.</span><span class="sxs-lookup"><span data-stu-id="f2804-138">Change a firewall rule.</span></span>

```powershell
Set-AdlAnalyticsFirewallRule -Account $adla -Name $ruleName -StartIpAddress $startIpAddress -EndIpAddress $endIpAddress
```

<span data-ttu-id="f2804-139">Supprimez une règle de pare-feu.</span><span class="sxs-lookup"><span data-stu-id="f2804-139">Remove a firewall rule.</span></span>

```powershell
Remove-AdlAnalyticsFirewallRule -Account $adla -Name $ruleName
```



<span data-ttu-id="f2804-140">Autorisez des adresses IP Azure.</span><span class="sxs-lookup"><span data-stu-id="f2804-140">Allow Azure IP addresses.</span></span>

```powershell
Set-AdlAnalyticsAccount -Name $adla -AllowAzureIpState Enabled
```

```powershell
Set-AdlAnalyticsAccount -Name $adla -FirewallState Enabled
Set-AdlAnalyticsAccount -Name $adla -FirewallState Disabled
```

## <a name="managing-data-sources"></a><span data-ttu-id="f2804-141">Gérer les sources de données</span><span class="sxs-lookup"><span data-stu-id="f2804-141">Managing data sources</span></span>
<span data-ttu-id="f2804-142">Analytique de LAC de données Azure prend actuellement en charge hello les sources de données suivantes :</span><span class="sxs-lookup"><span data-stu-id="f2804-142">Azure Data Lake Analytics currently supports hello following data sources:</span></span>

* [<span data-ttu-id="f2804-143">Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="f2804-143">Azure Data Lake Store</span></span>](../data-lake-store/data-lake-store-overview.md)
* [<span data-ttu-id="f2804-144">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="f2804-144">Azure Storage</span></span>](../storage/common/storage-introduction.md)

<span data-ttu-id="f2804-145">Lorsque vous créez un compte Analytique, vous devez désigner une source de données de Data Lake Store compte toobe hello par défaut.</span><span class="sxs-lookup"><span data-stu-id="f2804-145">When you create an Analytics account, you must designate a Data Lake Store account toobe hello default data source.</span></span> <span data-ttu-id="f2804-146">Hello compte Data Lake Store de valeur par défaut est utilisé toostore métadonnée de la tâche et le travail de journaux d’audit.</span><span class="sxs-lookup"><span data-stu-id="f2804-146">hello default Data Lake Store account is used toostore job metadata and job audit logs.</span></span> <span data-ttu-id="f2804-147">Après la création d'un compte Data Lake Analytics, vous pouvez ajouter des comptes Data Lake Store et/ou des comptes de stockage supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="f2804-147">After you have created a Data Lake Analytics account, you can add additional Data Lake Store accounts and/or Storage accounts.</span></span> 

### <a name="find-hello-default-data-lake-store-account"></a><span data-ttu-id="f2804-148">Rechercher le compte Data Lake Store de valeur par défaut hello</span><span class="sxs-lookup"><span data-stu-id="f2804-148">Find hello default Data Lake Store account</span></span>

```powershell
$adla_acct = Get-AdlAnalyticsAccount -Name $adla
$dataLakeStoreName = $adla_acct.DefaultDataLakeAccount
```

<span data-ttu-id="f2804-149">Vous trouverez le compte Data Lake Store de valeur par défaut hello en filtrant la liste hello de sources de données par hello `IsDefault` propriété :</span><span class="sxs-lookup"><span data-stu-id="f2804-149">You can find hello default Data Lake Store account by filtering hello list of datasources by hello `IsDefault` property:</span></span>

```powershell
Get-AdlAnalyticsDataSource -Account $adla  | ? { $_.IsDefault } 
```

### <a name="add-a-data-source"></a><span data-ttu-id="f2804-150">Ajouter une source de données</span><span class="sxs-lookup"><span data-stu-id="f2804-150">Add a data source</span></span>

```powershell

# Add an additional Storage (Blob) account.
$AzureStorageAccountName = "<AzureStorageAccountName>"
$AzureStorageAccountKey = "<AzureStorageAccountKey>"
Add-AdlAnalyticsDataSource -Account $adla -Blob $AzureStorageAccountName -AccessKey $AzureStorageAccountKey

# Add an additional Data Lake Store account.
$AzureDataLakeStoreName = "<AzureDataLakeStoreAccountName"
Add-AdlAnalyticsDataSource -Account $adla -DataLakeStore $AzureDataLakeStoreName 
```

### <a name="list-data-sources"></a><span data-ttu-id="f2804-151">Lister les sources de données</span><span class="sxs-lookup"><span data-stu-id="f2804-151">List data sources</span></span>

```powershell
# List all hello data sources
Get-AdlAnalyticsDataSource -Name $adla

# List attached Data Lake Store accounts
Get-AdlAnalyticsDataSource -Name $adla | where -Property Type -EQ "DataLakeStore"

# List attached Storage accounts
Get-AdlAnalyticsDataSource -Name $adla | where -Property Type -EQ "Blob"
```

## <a name="submit-u-sql-jobs"></a><span data-ttu-id="f2804-152">Envoyer des travaux U-SQL</span><span class="sxs-lookup"><span data-stu-id="f2804-152">Submit U-SQL jobs</span></span>

### <a name="submit-a-string-as-a-u-sql-script"></a><span data-ttu-id="f2804-153">Envoyer une chaîne en tant que script U-SQL</span><span class="sxs-lookup"><span data-stu-id="f2804-153">Submit a string as a U-SQL script</span></span>

```powershell
$script = @"
@a  = 
    SELECT * FROM 
        (VALUES
            ("Contoso", 1500.0),
            ("Woodgrove", 2700.0)
        ) AS D( customer, amount );
OUTPUT @a
    too"/data.csv"
    USING Outputters.Csv();
"@

$scriptpath = "d:\test.usql"
$script | Out-File $scriptpath 

Submit-AdlJob -AccountName $adla -Script $script -Name "Demo"
```


### <a name="submit-a-file-as-a-u-sql-script"></a><span data-ttu-id="f2804-154">Envoyer un fichier en tant que script U-SQL</span><span class="sxs-lookup"><span data-stu-id="f2804-154">Submit a file as a U-SQL script</span></span>

```powershell
$scriptpath = "d:\test.usql"
$script | Out-File $scriptpath 
Submit-AdlJob -AccountName $adla –ScriptPath $scriptpath -Name "Demo"
```

## <a name="list-jobs-in-an-account"></a><span data-ttu-id="f2804-155">Lister des travaux dans un compte</span><span class="sxs-lookup"><span data-stu-id="f2804-155">List jobs in an account</span></span>

### <a name="list-all-hello-jobs-in-hello-account"></a><span data-ttu-id="f2804-156">Afficher tous les travaux de hello dans le compte de hello.</span><span class="sxs-lookup"><span data-stu-id="f2804-156">List all hello jobs in hello account.</span></span> 

<span data-ttu-id="f2804-157">sortie de Hello inclut hello tâches en cours et les travaux qui viennent de se terminer.</span><span class="sxs-lookup"><span data-stu-id="f2804-157">hello output includes hello currently running jobs and those jobs that have recently completed.</span></span>

```powershell
Get-AdlJob -Account $adla
```


### <a name="list-a-specific-number-of-jobs"></a><span data-ttu-id="f2804-158">Lister un nombre spécifique de travaux</span><span class="sxs-lookup"><span data-stu-id="f2804-158">List a specific number of jobs</span></span>

<span data-ttu-id="f2804-159">Liste hello des travaux est triée par défaut lors de l’envoi temps.</span><span class="sxs-lookup"><span data-stu-id="f2804-159">By default hello list of jobs is sorted on submit time.</span></span> <span data-ttu-id="f2804-160">Afin de hello récemment envoyé travaux s’affichent en premier.</span><span class="sxs-lookup"><span data-stu-id="f2804-160">So hello most recently submitted jobs appear first.</span></span> <span data-ttu-id="f2804-161">Par défaut, hello compte ADLA souvient de travaux de 180 jours, mais hello AdlJob-Ge applet de commande par défaut retourne hello uniquement les 500 premiers.</span><span class="sxs-lookup"><span data-stu-id="f2804-161">By default, hello ADLA account remembers jobs for 180 days, but hello Ge-AdlJob  cmdlet by default returns only hello first 500.</span></span> <span data-ttu-id="f2804-162">Utilisez - toolist de paramètre supérieur un certain nombre de travaux.</span><span class="sxs-lookup"><span data-stu-id="f2804-162">Use -Top parameter toolist a specific number of jobs.</span></span>

```powershell
$jobs = Get-AdlJob -Account $adla -Top 10
```


### <a name="list-jobs-based-on-hello-value-of-job-property"></a><span data-ttu-id="f2804-163">Liste des travaux en fonction de valeur hello de propriété de tâche</span><span class="sxs-lookup"><span data-stu-id="f2804-163">List jobs based on hello value of job property</span></span>

<span data-ttu-id="f2804-164">À l’aide de hello `-State` paramètre.</span><span class="sxs-lookup"><span data-stu-id="f2804-164">Using hello `-State` parameter.</span></span> <span data-ttu-id="f2804-165">Vous pouvez combiner chacune de ces valeurs :</span><span class="sxs-lookup"><span data-stu-id="f2804-165">You can combine any of these values:</span></span>

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
# List hello running jobs
Get-AdlJob -Account $adla -State Running

# List hello jobs that have completed
Get-AdlJob -Account $adla -State Ended

# List hello jobs that have not started yet
Get-AdlJob -Account $adla -State Accepted,Compiling,New,Paused,Scheduling,Start
```

<span data-ttu-id="f2804-166">Hello d’utilisation `-Result` paramètre toodetect si les travaux terminés s’est déroulée correctement.</span><span class="sxs-lookup"><span data-stu-id="f2804-166">Use hello `-Result` parameter toodetect whether ended jobs completed successfully.</span></span> <span data-ttu-id="f2804-167">Il possède ces valeurs :</span><span class="sxs-lookup"><span data-stu-id="f2804-167">It has these values:</span></span>

* <span data-ttu-id="f2804-168">Annulé</span><span class="sxs-lookup"><span data-stu-id="f2804-168">Cancelled</span></span>
* <span data-ttu-id="f2804-169">Échec</span><span class="sxs-lookup"><span data-stu-id="f2804-169">Failed</span></span>
* <span data-ttu-id="f2804-170">Aucune</span><span class="sxs-lookup"><span data-stu-id="f2804-170">None</span></span>
* <span data-ttu-id="f2804-171">Réussi</span><span class="sxs-lookup"><span data-stu-id="f2804-171">Succeeded</span></span>

``` powershell
# List Successful jobs.
Get-AdlJob -Account $adla -State Ended -Result Succeeded

# List Failed jobs.
Get-AdlJob -Account $adla -State Ended -Result Failed
```


<span data-ttu-id="f2804-172">Hello `-Submitter` paramètre vous permet d’identifier qui a soumis une tâche.</span><span class="sxs-lookup"><span data-stu-id="f2804-172">hello `-Submitter` parameter helps you identify who submitted a job.</span></span>

```powershell
Get-AdlJob -Account $adla -Submitter "joe@contoso.com"
```

<span data-ttu-id="f2804-173">Hello `-SubmittedAfter` est utile pour filtrer la plage de temps tooa.</span><span class="sxs-lookup"><span data-stu-id="f2804-173">hello `-SubmittedAfter` is useful in filtering tooa time range.</span></span>


```powershell
# List  jobs submitted in hello last day.
$d = [DateTime]::Now.AddDays(-1)
Get-AdlJob -Account $adla -SubmittedAfter $d

# List  jobs submitted in hello last seven day.
$d = [DateTime]::Now.AddDays(-7)
Get-AdlJob -Account $adla -SubmittedAfter $d
```

### <a name="common-scenarios-for-listing-jobs"></a><span data-ttu-id="f2804-174">Scénarios courants pour lister des travaux</span><span class="sxs-lookup"><span data-stu-id="f2804-174">Common scenarios for listing jobs</span></span>


```
# List jobs submitted in hello last five days and that successfully completed.
$d = (Get-Date).AddDays(-5)
Get-AdlJob -Account $adla -SubmittedAfter $d -State Ended -Result Succeeded

# List all failed jobs submitted by "joe@contoso.com" within hello past seven days.
Get-AdlJob -Account $adla `
    -Submitter "joe@contoso.com" `
    -SubmittedAfter (Get-Date).AddDays(-7) `
    -Result Failed
```

## <a name="filtering-a-list-of-jobs"></a><span data-ttu-id="f2804-175">Filtrer une liste de travaux</span><span class="sxs-lookup"><span data-stu-id="f2804-175">Filtering a list of jobs</span></span>

<span data-ttu-id="f2804-176">Dès que vous disposez d’une liste de travaux dans votre session PowerShell actuelle.</span><span class="sxs-lookup"><span data-stu-id="f2804-176">Once you have a list of jobs in your current PowerShell session.</span></span> <span data-ttu-id="f2804-177">Vous pouvez utiliser la liste d’hello toofilter à des applets de commande PowerShell normale.</span><span class="sxs-lookup"><span data-stu-id="f2804-177">You can use normal PowerShell cmdlets toofilter hello list.</span></span>

<span data-ttu-id="f2804-178">Filtre une liste des tâches de toohello travaux soumis Bonjour des dernières 24 heures</span><span class="sxs-lookup"><span data-stu-id="f2804-178">Filter a list of jobs toohello jobs submitted in hello last 24 hours</span></span>

```
$upperdate = Get-Date
$lowerdate = $upperdate.AddHours(-24)
$jobs | Where-Object { $_.EndTime -ge $lowerdate }
```

<span data-ttu-id="f2804-179">Filtrer une liste de tâches toohello tâches Bonjour des dernières 24 heures</span><span class="sxs-lookup"><span data-stu-id="f2804-179">Filter a list of jobs toohello jobs that ended in hello last 24 hours</span></span>

```
$upperdate = Get-Date
$lowerdate = $upperdate.AddHours(-24)
$jobs | Where-Object { $_.SubmitTime -ge $lowerdate }
```

<span data-ttu-id="f2804-180">Filtrer une liste des tâches de toohello de travaux démarré.</span><span class="sxs-lookup"><span data-stu-id="f2804-180">Filter a list of jobs toohello jobs that started running.</span></span> <span data-ttu-id="f2804-181">Un travail peut échouer au moment de la compilation et donc ne jamais démarrer.</span><span class="sxs-lookup"><span data-stu-id="f2804-181">A job might fail at compile time - and so it never starts.</span></span> <span data-ttu-id="f2804-182">Examinons hello échoué des travaux qui en fait démarré en cours d’exécution et a ensuite échoué.</span><span class="sxs-lookup"><span data-stu-id="f2804-182">Let's look at hello failed jobs that actually started running and then failed.</span></span>

```powershell
$jobs | Where-Object { $_.StartTime -ne $null }
```

### <a name="analyzing-a-list-of-jobs"></a><span data-ttu-id="f2804-183">Analyser une liste de travaux</span><span class="sxs-lookup"><span data-stu-id="f2804-183">Analyzing a list of jobs</span></span>

<span data-ttu-id="f2804-184">Hello d’utilisation `Group-Object` applet de commande tooanalyze une liste des tâches.</span><span class="sxs-lookup"><span data-stu-id="f2804-184">Use hello `Group-Object` cmdlet tooanalyze a list of jobs.</span></span>

```
# Count hello number of jobs by Submitter
$jobs | Group-Object Submitter | Select -Property Count,Name

# Count hello number of jobs by Result
$jobs | Group-Object Result | Select -Property Count,Name

# Count hello number of jobs by State
$jobs | Group-Object State | Select -Property Count,Name

#  Count hello number of jobs by DegreeOfParallelism
$jobs | Group-Object DegreeOfParallelism | Select -Property Count,Name
```
<span data-ttu-id="f2804-185">Lorsque vous effectuez une analyse, il peut être utile tooadd propriétés toohello travail objets toomake filtrage et de regroupement le plus simple.</span><span class="sxs-lookup"><span data-stu-id="f2804-185">When performing an analysis, it can be useful tooadd properties toohello Job objects toomake filtering and grouping simpler.</span></span> <span data-ttu-id="f2804-186">Hello suivant extrait de code montre comment tooannotate un JobInfo avec calculées des propriétés.</span><span class="sxs-lookup"><span data-stu-id="f2804-186">hello following  snippet shows how tooannotate a JobInfo with calculated properties.</span></span>

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

## <a name="get-information-about-pipelines-and-recurrences"></a><span data-ttu-id="f2804-187">Obtenir des informations sur les pipelines et les périodicités</span><span class="sxs-lookup"><span data-stu-id="f2804-187">Get information about pipelines and recurrences</span></span>

<span data-ttu-id="f2804-188">Hello d’utilisation `Get-AdlJobPipeline` applet de commande toosee hello informations les concernant les travaux précédemment soumises.</span><span class="sxs-lookup"><span data-stu-id="f2804-188">Use hello `Get-AdlJobPipeline` cmdlet toosee hello pipeline information previously submitted jobs.</span></span>

```powershell
$pipelines = Get-AdlJobPipeline -Account $adla

$pipeline = Get-AdlJobPipeline -Account $adla -PipelineId "<pipeline ID>"
```

<span data-ttu-id="f2804-189">Hello d’utilisation `Get-AdlJobRecurrence` informations de périodicité toosee hello applet de commande pour les travaux soumis précédemment.</span><span class="sxs-lookup"><span data-stu-id="f2804-189">Use hello `Get-AdlJobRecurrence` cmdlet toosee hello recurrence information for previously submitted jobs.</span></span>

```powershell
$recurrences = Get-AdlJobRecurrence -Account $adla

$recurrence = Get-AdlJobRecurrence -Account $adla -RecurrenceId "<recurrence ID>"
```

## <a name="get-information-about-a-job"></a><span data-ttu-id="f2804-190">Obtenir des informations sur un travail</span><span class="sxs-lookup"><span data-stu-id="f2804-190">Get information about a job</span></span>

### <a name="get-job-status"></a><span data-ttu-id="f2804-191">Obtenir l’état de la tâche</span><span class="sxs-lookup"><span data-stu-id="f2804-191">Get job status</span></span>

<span data-ttu-id="f2804-192">Obtenir l’état de hello d’une tâche donnée.</span><span class="sxs-lookup"><span data-stu-id="f2804-192">Get hello status of a specific job.</span></span>

```powershell
Get-AdlJob -AccountName $adla -JobId $job.JobId
```

### <a name="examine-hello-job-outputs"></a><span data-ttu-id="f2804-193">Examiner les sorties de travail hello</span><span class="sxs-lookup"><span data-stu-id="f2804-193">Examine hello job outputs</span></span>

<span data-ttu-id="f2804-194">Une fois le travail de hello terminée, vérifiez si le fichier de sortie hello existe en répertoriant les fichiers hello dans un dossier.</span><span class="sxs-lookup"><span data-stu-id="f2804-194">After hello job has ended, check if hello output file exists by listing hello files in a folder.</span></span>

```powershell
Get-AdlStoreChildItem -Account $adls -Path "/"
```

## <a name="manage-running-jobs"></a><span data-ttu-id="f2804-195">Gérer les tâches en cours d’exécution</span><span class="sxs-lookup"><span data-stu-id="f2804-195">Manage running jobs</span></span>

### <a name="cancel-a-job"></a><span data-ttu-id="f2804-196">Annulation d’une tâche</span><span class="sxs-lookup"><span data-stu-id="f2804-196">Cancel a job</span></span>

```powershell
Stop-AdlJob -Account $adls -JobID $jobID
```

### <a name="wait-for-a-job-toofinish"></a><span data-ttu-id="f2804-197">Attendre un toofinish de travail</span><span class="sxs-lookup"><span data-stu-id="f2804-197">Wait for a job toofinish</span></span>

<span data-ttu-id="f2804-198">Au lieu de répéter `Get-AdlAnalyticsJob` jusqu'à ce qu’un travail est terminé, vous pouvez utiliser hello `Wait-AdlJob` toowait d’applet de commande pour tooend de travail hello.</span><span class="sxs-lookup"><span data-stu-id="f2804-198">Instead of repeating `Get-AdlAnalyticsJob` until a job finishes, you can use hello `Wait-AdlJob` cmdlet toowait for hello job tooend.</span></span>

```powershell
Wait-AdlJob -Account $adla -JobId $job.JobId
```

## <a name="manage-compute-policies"></a><span data-ttu-id="f2804-199">Gérer les stratégies de calcul</span><span class="sxs-lookup"><span data-stu-id="f2804-199">Manage compute policies</span></span>

### <a name="list-existing-compute-policies"></a><span data-ttu-id="f2804-200">Lister les stratégies de calcul existantes</span><span class="sxs-lookup"><span data-stu-id="f2804-200">List existing compute policies</span></span>

<span data-ttu-id="f2804-201">Hello `Get-AdlAnalyticsComputePolicy` applet de commande extrait des informations sur les stratégies de calcul pour un compte Analytique lac de données.</span><span class="sxs-lookup"><span data-stu-id="f2804-201">hello `Get-AdlAnalyticsComputePolicy` cmdlet retrieves info about compute policies for a Data Lake Analytics account.</span></span>

```powershell
$policies = Get-AdlAnalyticsComputePolicy -Account $adla
```

### <a name="create-a-compute-policy"></a><span data-ttu-id="f2804-202">Créer une stratégie de calcul</span><span class="sxs-lookup"><span data-stu-id="f2804-202">Create a compute policy</span></span>

<span data-ttu-id="f2804-203">Hello `New-AdlAnalyticsComputePolicy` applet de commande crée une nouvelle stratégie de calcul pour un compte Analytique lac de données.</span><span class="sxs-lookup"><span data-stu-id="f2804-203">hello `New-AdlAnalyticsComputePolicy` cmdlet creates a new compute policy for a Data Lake Analytics account.</span></span> <span data-ttu-id="f2804-204">Cet exemple définit hello maximale toohello de AUs disponible spécifié utilisateur too50 et too250 de priorité hello minimal de tâche.</span><span class="sxs-lookup"><span data-stu-id="f2804-204">This example sets  hello maximum AUs available toohello specified user too50, and hello minimum job priority too250.</span></span>

```powershell
$userObjectId = (Get-AzureRmAdUser -SearchString "garymcdaniel@contoso.com").Id

New-AdlAnalyticsComputePolicy -Account $adla -Name "GaryMcDaniel" -ObjectId $objectId -ObjectType User -MaxDegreeOfParallelismPerJob 50 -MinPriorityPerJob 250
```

## <a name="check-for-hello-existence-of-a-file"></a><span data-ttu-id="f2804-205">Vérifier l’existence de hello d’un fichier.</span><span class="sxs-lookup"><span data-stu-id="f2804-205">Check for hello existence of a file.</span></span>

```powershell
Test-AdlStoreItem -Account $adls -Path "/data.csv"
```

## <a name="uploading-and-downloading"></a><span data-ttu-id="f2804-206">Chargement et téléchargement</span><span class="sxs-lookup"><span data-stu-id="f2804-206">Uploading and downloading</span></span>

<span data-ttu-id="f2804-207">Chargez un fichier.</span><span class="sxs-lookup"><span data-stu-id="f2804-207">Upload a file.</span></span>

```powershell
Import-AdlStoreItem -AccountName $adls -Path "c:\data.tsv" -Destination "/data_copy.csv" 
```

<span data-ttu-id="f2804-208">Chargez un dossier entier de manière récursive.</span><span class="sxs-lookup"><span data-stu-id="f2804-208">Upload an entire folder recursively.</span></span>

```powershell
Import-AdlStoreItem -AccountName $adls -Path "c:\myData\" -Destination "/myData/" -Recurse
```

<span data-ttu-id="f2804-209">Téléchargez un fichier.</span><span class="sxs-lookup"><span data-stu-id="f2804-209">Download a file.</span></span>

```powershell
Export-AdlStoreItem -AccountName $adls -Path "/data.csv" -Destination "c:\data.csv"
```

<span data-ttu-id="f2804-210">Téléchargez un dossier entier de manière récursive.</span><span class="sxs-lookup"><span data-stu-id="f2804-210">Download an entire folder recursively.</span></span>

```powershell
Export-AdlStoreItem -AccountName $adls -Path "/" -Destination "c:\myData\" -Recurse
```

> [!NOTE]
> <span data-ttu-id="f2804-211">Si hello télécharger ou les processus de téléchargement est interrompu, vous pouvez tenter de processus de hello tooresume par l’applet de commande hello en cours d’exécution avec hello ``-Resume`` indicateur.</span><span class="sxs-lookup"><span data-stu-id="f2804-211">If hello upload or download process is interrupted, you can attempt tooresume hello process by running hello cmdlet again with hello ``-Resume`` flag.</span></span>

## <a name="manage-catalog-items"></a><span data-ttu-id="f2804-212">Gestion des éléments du catalogue</span><span class="sxs-lookup"><span data-stu-id="f2804-212">Manage catalog items</span></span>

<span data-ttu-id="f2804-213">catalogue de Hello U-SQL est utilisé toostructure données et le code afin qu’ils peuvent être partagés par les scripts U-SQL.</span><span class="sxs-lookup"><span data-stu-id="f2804-213">hello U-SQL catalog is used toostructure data and code so they can be shared by U-SQL scripts.</span></span> <span data-ttu-id="f2804-214">catalogue de Hello permet hello performances maximales des données dans Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="f2804-214">hello catalog enables hello highest performance possible with data in Azure Data Lake.</span></span> <span data-ttu-id="f2804-215">Pour plus d'informations, consultez [Utilisation du catalogue U-SQL](data-lake-analytics-use-u-sql-catalog.md).</span><span class="sxs-lookup"><span data-stu-id="f2804-215">For more information, see [Use U-SQL catalog](data-lake-analytics-use-u-sql-catalog.md).</span></span>

### <a name="list-items-in-hello-u-sql-catalog"></a><span data-ttu-id="f2804-216">Éléments de liste dans le catalogue de hello U-SQL</span><span class="sxs-lookup"><span data-stu-id="f2804-216">List items in hello U-SQL catalog</span></span>

```powershell
# List U-SQL databases
Get-AdlCatalogItem -Account $adla -ItemType Database 

# List tables within a database
Get-AdlCatalogItem -Account $adla -ItemType Table -Path "database"

# List tables within a schema.
Get-AdlCatalogItem -Account $adla -ItemType Table -Path "database.schema"
```

<span data-ttu-id="f2804-217">Liste de tous les assemblys hello dans toutes les bases de données hello dans un compte ADLA.</span><span class="sxs-lookup"><span data-stu-id="f2804-217">List all hello assemblies in all hello databases in an ADLA Account.</span></span>

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

### <a name="get-details-about-a-catalog-item"></a><span data-ttu-id="f2804-218">Obtenir des détails sur un élément de catalogue</span><span class="sxs-lookup"><span data-stu-id="f2804-218">Get details about a catalog item</span></span>

```powershell
# Get details of a table
Get-AdlCatalogItem  -Account $adla -ItemType Table -Path "master.dbo.mytable"

# Test existence of a U-SQL database.
Test-AdlCatalogItem  -Account $adla -ItemType Database -Path "master"
```

### <a name="create-credentials-in-a-catalog"></a><span data-ttu-id="f2804-219">Créer des informations d’identification dans un catalogue</span><span class="sxs-lookup"><span data-stu-id="f2804-219">Create credentials in a catalog</span></span>

<span data-ttu-id="f2804-220">Dans une base de données U-SQL, créez un objet informations d’identification pour une base de données hébergée dans Azure.</span><span class="sxs-lookup"><span data-stu-id="f2804-220">Within a U-SQL database, create a credential object for a database hosted in Azure.</span></span> <span data-ttu-id="f2804-221">Actuellement, les informations d’identification U-SQL sont hello seul type d’élément de catalogue que vous pouvez créer via PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f2804-221">Currently, U-SQL credentials are hello only type of catalog item that you can create through PowerShell.</span></span>

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

### <a name="get-basic-information-about-an-adla-account"></a><span data-ttu-id="f2804-222">Obtenir des informations de base sur un compte ADLA</span><span class="sxs-lookup"><span data-stu-id="f2804-222">Get basic information about an ADLA account</span></span>

<span data-ttu-id="f2804-223">Étant donné un nom de compte, hello suivant code recherche des informations de base à propos du compte hello</span><span class="sxs-lookup"><span data-stu-id="f2804-223">Given an account name, hello following code looks up basic information about hello account</span></span>

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

## <a name="working-with-azure"></a><span data-ttu-id="f2804-224">Utilisation d’Azure</span><span class="sxs-lookup"><span data-stu-id="f2804-224">Working with Azure</span></span>

### <a name="get-details-of-azurerm-errors"></a><span data-ttu-id="f2804-225">Obtenir des détails sur les erreurs AzureRm</span><span class="sxs-lookup"><span data-stu-id="f2804-225">Get details of AzureRm errors</span></span>

```powershell
Resolve-AzureRmError -Last
```

### <a name="verify-if-you-are-running-as-an-administrator"></a><span data-ttu-id="f2804-226">Vérifier que vous exécutez en tant qu’administrateur</span><span class="sxs-lookup"><span data-stu-id="f2804-226">Verify if you are running as an administrator</span></span>

```powershell
function Test-Administrator  
{  
    $user = [Security.Principal.WindowsIdentity]::GetCurrent();
    $p = New-Object Security.Principal.WindowsPrincipal $user
    $p.IsInRole([Security.Principal.WindowsBuiltinRole]::Administrator)  
}
```

### <a name="find-a-tenantid"></a><span data-ttu-id="f2804-227">Trouver un TenantID</span><span class="sxs-lookup"><span data-stu-id="f2804-227">Find a TenantID</span></span>

<span data-ttu-id="f2804-228">À partir du nom d’un abonnement :</span><span class="sxs-lookup"><span data-stu-id="f2804-228">From a subscription name:</span></span>

```powershell
function Get-TenantIdFromSubcriptionName( [string] $subname )
{
    $sub = (Get-AzureRmSubscription -SubscriptionName $subname)
    $sub.TenantId
}

Get-TenantIdFromSubcriptionName "ADLTrainingMS"
```

<span data-ttu-id="f2804-229">À partir de l’ID d’un abonnement :</span><span class="sxs-lookup"><span data-stu-id="f2804-229">From a subscription id:</span></span>

```powershell
function Get-TenantIdFromSubcriptionId( [string] $subid )
{
    $sub = (Get-AzureRmSubscription -SubscriptionId $subid)
    $sub.TenantId
}

$subid = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
Get-TenantIdFromSubcriptionId $subid
```

<span data-ttu-id="f2804-230">À partir d’une adresse de domaine, comme « contoso.com »</span><span class="sxs-lookup"><span data-stu-id="f2804-230">From a domain address such as "contoso.com"</span></span>


```powershell
function Get-TenantIdFromDomain( $domain )
{
    $url = "https://login.windows.net/" + $domain + "/.well-known/openid-configuration"
    return (Invoke-WebRequest $url|ConvertFrom-Json).token_endpoint.Split('/')[3]
}

$domain = "contoso.com"
Get-TenantIdFromDomain $domain
```

### <a name="list-all-your-subscriptions-and-tenant-ids"></a><span data-ttu-id="f2804-231">Lister tous vos abonnements et leur ID client</span><span class="sxs-lookup"><span data-stu-id="f2804-231">List all your subscriptions and tenant ids</span></span>

```powershell
$subs = Get-AzureRmSubscription
foreach ($sub in $subs)
{
    Write-Host $sub.Name "("  $sub.Id ")"
    Write-Host "`tTenant Id" $sub.TenantId
}
```

## <a name="create-a-data-lake-analytics-account-using-a-template"></a><span data-ttu-id="f2804-232">Créer un compte Data Lake Analytics à l’aide d’un modèle</span><span class="sxs-lookup"><span data-stu-id="f2804-232">Create a Data Lake Analytics account using a template</span></span>

<span data-ttu-id="f2804-233">Vous pouvez également utiliser un modèle de groupe de ressources Azure à l’aide de hello PowerShell script suivant :</span><span class="sxs-lookup"><span data-stu-id="f2804-233">You can also use an Azure Resource Group template using hello following  PowerShell script:</span></span>

```powershell
$subId = "<Your Azure Subscription ID>"

$rg = "<New Azure Resource Group Name>"
$location = "<Location (such as East US 2)>"
$adls = "<New Data Lake Store Account Name>"
$adla = "<New Data Lake Analytics Account Name>"

$deploymentName = "MyDataLakeAnalyticsDeployment"
$armTemplateFile = "<LocalFolderPath>\azuredeploy.json"  # update hello JSON template path 

# Log in tooAzure
Login-AzureRmAccount -SubscriptionId $subId

# Create hello resource group
New-AzureRmResourceGroup -Name $rg -Location $location

# Create hello Data Lake Analytics account with hello default Data Lake Store account.
$parameters = @{"adlAnalyticsName"=$adla; "adlStoreName"=$adls}
New-AzureRmResourceGroupDeployment -Name $deploymentName -ResourceGroupName $rg -TemplateFile $armTemplateFile -TemplateParameterObject $parameters 
```

<span data-ttu-id="f2804-234">Pour plus d’informations, consultez [Déploiement d’une application avec un modèle Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md) et [Création de modèles Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="f2804-234">For more information, see [Deploy an application with Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md) and [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="f2804-235">**Exemple de modèle**</span><span class="sxs-lookup"><span data-stu-id="f2804-235">**Example template**</span></span>

<span data-ttu-id="f2804-236">Enregistrer hello après le texte comme un `.json` de fichier et l’utiliser hello précédant le modèle de PowerShell script toouse hello.</span><span class="sxs-lookup"><span data-stu-id="f2804-236">Save hello following text as a `.json` file, and then use hello preceding PowerShell script toouse hello template.</span></span> 

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "adlAnalyticsName": {
      "type": "string",
      "metadata": {
        "description": "hello name of hello Data Lake Analytics account toocreate."
      }
    },
    "adlStoreName": {
      "type": "string",
      "metadata": {
        "description": "hello name of hello Data Lake Store account toocreate."
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

## <a name="next-steps"></a><span data-ttu-id="f2804-237">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f2804-237">Next steps</span></span>
* [<span data-ttu-id="f2804-238">Vue d'ensemble de Microsoft Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="f2804-238">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* <span data-ttu-id="f2804-239">Prise en main de Data Lake Analytics à l’aide du [portail Azure](data-lake-analytics-get-started-portal.md) | [Azure PowerShell](data-lake-analytics-get-started-powershell.md) | [CLI 2.0](data-lake-analytics-get-started-cli2.md)</span><span class="sxs-lookup"><span data-stu-id="f2804-239">Get started with Data Lake Analytics using [Azure portal](data-lake-analytics-get-started-portal.md) | [Azure PowerShell](data-lake-analytics-get-started-powershell.md) | [CLI 2.0](data-lake-analytics-get-started-cli2.md)</span></span>
* <span data-ttu-id="f2804-240">Gérer Azure Data Lake Analytics à l’aide du [portail Azure](data-lake-analytics-manage-use-portal.md) | [Azure PowerShell](data-lake-analytics-manage-use-powershell.md) | [CLI](data-lake-analytics-manage-use-cli.md)</span><span class="sxs-lookup"><span data-stu-id="f2804-240">Manage Azure Data Lake Analytics using [Azure portal](data-lake-analytics-manage-use-portal.md) | [Azure PowerShell](data-lake-analytics-manage-use-powershell.md) | [CLI](data-lake-analytics-manage-use-cli.md)</span></span> 
