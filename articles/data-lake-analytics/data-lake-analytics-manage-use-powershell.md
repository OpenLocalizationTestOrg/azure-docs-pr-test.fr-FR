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
# <a name="manage-azure-data-lake-analytics-using-azure-powershell"></a>Gestion d'Azure Data Lake Analytics à l'aide d'Azure PowerShell
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

Découvrez comment les comptes d’Analytique de LAC de données Azure toomanage, sources de données, des travaux et des éléments de catalogue à l’aide d’Azure PowerShell. 

## <a name="prerequisites"></a>Composants requis

Lorsque vous créez un compte Analytique lac de données, vous devez tooknow :

* **ID d’abonnement**: hello ID d’abonnement Azure sous lequel réside votre compte Analytique lac de données.
* **Groupe de ressources**: nom hello hello Azure du groupe de ressources qui contient votre compte Analytique lac de données.
* **Nom du compte Analytique lac de données**: hello compte nom doit contenir uniquement des lettres minuscules et chiffres.
* **Compte Data Lake Store par défaut** : chaque compte Data Lake Analytics possède un compte Data Lake Store par défaut. Ces comptes doivent être Bonjour même emplacement.
* **Emplacement**: prise en charge d’emplacement hello de votre compte Analytique lac de données, telles que « Est des États-Unis 2 » ou d’autres emplacements. Les emplacements pris en charge sont indiqués sur notre [page de tarification](https://azure.microsoft.com/pricing/details/data-lake-analytics/).

extraits de code PowerShell Hello dans ce didacticiel utilisent ces toostore variables ces informations

```powershell
$subId = "<SubscriptionId>"
$rg = "<ResourceGroupName>"
$adla = "<DataLakeAnalyticsAccountName>"
$adls = "<DataLakeStoreAccountName>"
$location = "<Location>"
```

## <a name="log-in"></a>Se connecter

Connectez-vous à l’aide d’un ID d’abonnement.

```powershell
Login-AzureRmAccount -SubscriptionId $subId
```

Connectez-vous à l’aide d’un nom d’abonnement.

```
Login-AzureRmAccount -SubscriptionName $subname 
```

Hello `Login-AzureRmAccount` applet de commande toujours vous invite à entrer des informations d’identification. Vous pouvez éviter d’être invité à l’aide de hello suivant d’applets de commande :

```powershell
# Save login session information
Save-AzureRmProfile -Path D:\profile.json  

# Load login session information
Select-AzureRmProfile -Path D:\profile.json 
```

## <a name="managing-accounts"></a>Gérer des comptes

### <a name="create-a-data-lake-analytics-account"></a>Créer un compte Data Lake Analytics

Si vous n’avez pas déjà un [groupe de ressources](../azure-resource-manager/resource-group-overview.md#resource-groups) toouse, créez-en un. 

```powershell
New-AzureRmResourceGroup -Name  $rg -Location $location
```

Chaque compte Data Lake Analytics nécessite un compte Data Lake Store par défaut pour stocker les journaux. Vous pouvez réutiliser un compte ou en créer un. 

```powershell
New-AdlStore -ResourceGroupName $rg -Name $adls -Location $location
```

Lorsqu’un groupe de ressources et un compte Data Lake Store sont disponibles, créez un compte Data Lake Analytics.

```powershell
New-AdlAnalyticsAccount -ResourceGroupName $rg -Name $adla -Location $location -DefaultDataLake $adls
```

### <a name="get-information-about-an-account"></a>Obtenir des informations sur un compte

Obtenez les détails relatifs à un compte.

```powershell
Get-AdlAnalyticsAccount -Name $adla
```

Vérifier l’existence de hello d’un compte Analytique lac de données spécifique. applet de commande Hello retourne `True` ou `False`.

```powershell
Test-AdlAnalyticsAccount -Name $adla
```

Vérifier l’existence de hello d’un compte Data Lake Store spécifique. applet de commande Hello retourne `True` ou `False`.

```powershell
Test-AdlStoreAccount -Name $adls
```

### <a name="listing-accounts"></a>Lister les comptes

Comptes d’Analytique lac de données de liste dans l’abonnement actuel de hello.

```powershell
Get-AdlAnalyticsAccount
```

Listez les comptes Data Lake Analytics dans un groupe de ressources spécifique.

```powershell
Get-AdlAnalyticsAccount -ResourceGroupName $rg
```

## <a name="managing-firewall-rules"></a>Gérer les règles de pare-feu

Listez les règles de pare-feu.

```powershell
Get-AdlAnalyticsFirewallRule -Account $adla
```

Ajoutez une règle de pare-feu.

```powershell
$ruleName = "Allow access from on-prem server"
$startIpAddress = "<start IP address>"
$endIpAddress = "<end IP address>"

Add-AdlAnalyticsFirewallRule -Account $adla -Name $ruleName -StartIpAddress $startIpAddress -EndIpAddress $endIpAddress
```

Modifiez une règle de pare-feu.

```powershell
Set-AdlAnalyticsFirewallRule -Account $adla -Name $ruleName -StartIpAddress $startIpAddress -EndIpAddress $endIpAddress
```

Supprimez une règle de pare-feu.

```powershell
Remove-AdlAnalyticsFirewallRule -Account $adla -Name $ruleName
```



Autorisez des adresses IP Azure.

```powershell
Set-AdlAnalyticsAccount -Name $adla -AllowAzureIpState Enabled
```

```powershell
Set-AdlAnalyticsAccount -Name $adla -FirewallState Enabled
Set-AdlAnalyticsAccount -Name $adla -FirewallState Disabled
```

## <a name="managing-data-sources"></a>Gérer les sources de données
Analytique de LAC de données Azure prend actuellement en charge hello les sources de données suivantes :

* [Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md)
* [Azure Storage](../storage/common/storage-introduction.md)

Lorsque vous créez un compte Analytique, vous devez désigner une source de données de Data Lake Store compte toobe hello par défaut. Hello compte Data Lake Store de valeur par défaut est utilisé toostore métadonnée de la tâche et le travail de journaux d’audit. Après la création d'un compte Data Lake Analytics, vous pouvez ajouter des comptes Data Lake Store et/ou des comptes de stockage supplémentaires. 

### <a name="find-hello-default-data-lake-store-account"></a>Rechercher le compte Data Lake Store de valeur par défaut hello

```powershell
$adla_acct = Get-AdlAnalyticsAccount -Name $adla
$dataLakeStoreName = $adla_acct.DefaultDataLakeAccount
```

Vous trouverez le compte Data Lake Store de valeur par défaut hello en filtrant la liste hello de sources de données par hello `IsDefault` propriété :

```powershell
Get-AdlAnalyticsDataSource -Account $adla  | ? { $_.IsDefault } 
```

### <a name="add-a-data-source"></a>Ajouter une source de données

```powershell

# Add an additional Storage (Blob) account.
$AzureStorageAccountName = "<AzureStorageAccountName>"
$AzureStorageAccountKey = "<AzureStorageAccountKey>"
Add-AdlAnalyticsDataSource -Account $adla -Blob $AzureStorageAccountName -AccessKey $AzureStorageAccountKey

# Add an additional Data Lake Store account.
$AzureDataLakeStoreName = "<AzureDataLakeStoreAccountName"
Add-AdlAnalyticsDataSource -Account $adla -DataLakeStore $AzureDataLakeStoreName 
```

### <a name="list-data-sources"></a>Lister les sources de données

```powershell
# List all hello data sources
Get-AdlAnalyticsDataSource -Name $adla

# List attached Data Lake Store accounts
Get-AdlAnalyticsDataSource -Name $adla | where -Property Type -EQ "DataLakeStore"

# List attached Storage accounts
Get-AdlAnalyticsDataSource -Name $adla | where -Property Type -EQ "Blob"
```

## <a name="submit-u-sql-jobs"></a>Envoyer des travaux U-SQL

### <a name="submit-a-string-as-a-u-sql-script"></a>Envoyer une chaîne en tant que script U-SQL

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


### <a name="submit-a-file-as-a-u-sql-script"></a>Envoyer un fichier en tant que script U-SQL

```powershell
$scriptpath = "d:\test.usql"
$script | Out-File $scriptpath 
Submit-AdlJob -AccountName $adla –ScriptPath $scriptpath -Name "Demo"
```

## <a name="list-jobs-in-an-account"></a>Lister des travaux dans un compte

### <a name="list-all-hello-jobs-in-hello-account"></a>Afficher tous les travaux de hello dans le compte de hello. 

sortie de Hello inclut hello tâches en cours et les travaux qui viennent de se terminer.

```powershell
Get-AdlJob -Account $adla
```


### <a name="list-a-specific-number-of-jobs"></a>Lister un nombre spécifique de travaux

Liste hello des travaux est triée par défaut lors de l’envoi temps. Afin de hello récemment envoyé travaux s’affichent en premier. Par défaut, hello compte ADLA souvient de travaux de 180 jours, mais hello AdlJob-Ge applet de commande par défaut retourne hello uniquement les 500 premiers. Utilisez - toolist de paramètre supérieur un certain nombre de travaux.

```powershell
$jobs = Get-AdlJob -Account $adla -Top 10
```


### <a name="list-jobs-based-on-hello-value-of-job-property"></a>Liste des travaux en fonction de valeur hello de propriété de tâche

À l’aide de hello `-State` paramètre. Vous pouvez combiner chacune de ces valeurs :

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

Hello d’utilisation `-Result` paramètre toodetect si les travaux terminés s’est déroulée correctement. Il possède ces valeurs :

* Annulé
* Échec
* Aucune
* Réussi

``` powershell
# List Successful jobs.
Get-AdlJob -Account $adla -State Ended -Result Succeeded

# List Failed jobs.
Get-AdlJob -Account $adla -State Ended -Result Failed
```


Hello `-Submitter` paramètre vous permet d’identifier qui a soumis une tâche.

```powershell
Get-AdlJob -Account $adla -Submitter "joe@contoso.com"
```

Hello `-SubmittedAfter` est utile pour filtrer la plage de temps tooa.


```powershell
# List  jobs submitted in hello last day.
$d = [DateTime]::Now.AddDays(-1)
Get-AdlJob -Account $adla -SubmittedAfter $d

# List  jobs submitted in hello last seven day.
$d = [DateTime]::Now.AddDays(-7)
Get-AdlJob -Account $adla -SubmittedAfter $d
```

### <a name="common-scenarios-for-listing-jobs"></a>Scénarios courants pour lister des travaux


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

## <a name="filtering-a-list-of-jobs"></a>Filtrer une liste de travaux

Dès que vous disposez d’une liste de travaux dans votre session PowerShell actuelle. Vous pouvez utiliser la liste d’hello toofilter à des applets de commande PowerShell normale.

Filtre une liste des tâches de toohello travaux soumis Bonjour des dernières 24 heures

```
$upperdate = Get-Date
$lowerdate = $upperdate.AddHours(-24)
$jobs | Where-Object { $_.EndTime -ge $lowerdate }
```

Filtrer une liste de tâches toohello tâches Bonjour des dernières 24 heures

```
$upperdate = Get-Date
$lowerdate = $upperdate.AddHours(-24)
$jobs | Where-Object { $_.SubmitTime -ge $lowerdate }
```

Filtrer une liste des tâches de toohello de travaux démarré. Un travail peut échouer au moment de la compilation et donc ne jamais démarrer. Examinons hello échoué des travaux qui en fait démarré en cours d’exécution et a ensuite échoué.

```powershell
$jobs | Where-Object { $_.StartTime -ne $null }
```

### <a name="analyzing-a-list-of-jobs"></a>Analyser une liste de travaux

Hello d’utilisation `Group-Object` applet de commande tooanalyze une liste des tâches.

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
Lorsque vous effectuez une analyse, il peut être utile tooadd propriétés toohello travail objets toomake filtrage et de regroupement le plus simple. Hello suivant extrait de code montre comment tooannotate un JobInfo avec calculées des propriétés.

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

## <a name="get-information-about-pipelines-and-recurrences"></a>Obtenir des informations sur les pipelines et les périodicités

Hello d’utilisation `Get-AdlJobPipeline` applet de commande toosee hello informations les concernant les travaux précédemment soumises.

```powershell
$pipelines = Get-AdlJobPipeline -Account $adla

$pipeline = Get-AdlJobPipeline -Account $adla -PipelineId "<pipeline ID>"
```

Hello d’utilisation `Get-AdlJobRecurrence` informations de périodicité toosee hello applet de commande pour les travaux soumis précédemment.

```powershell
$recurrences = Get-AdlJobRecurrence -Account $adla

$recurrence = Get-AdlJobRecurrence -Account $adla -RecurrenceId "<recurrence ID>"
```

## <a name="get-information-about-a-job"></a>Obtenir des informations sur un travail

### <a name="get-job-status"></a>Obtenir l’état de la tâche

Obtenir l’état de hello d’une tâche donnée.

```powershell
Get-AdlJob -AccountName $adla -JobId $job.JobId
```

### <a name="examine-hello-job-outputs"></a>Examiner les sorties de travail hello

Une fois le travail de hello terminée, vérifiez si le fichier de sortie hello existe en répertoriant les fichiers hello dans un dossier.

```powershell
Get-AdlStoreChildItem -Account $adls -Path "/"
```

## <a name="manage-running-jobs"></a>Gérer les tâches en cours d’exécution

### <a name="cancel-a-job"></a>Annulation d’une tâche

```powershell
Stop-AdlJob -Account $adls -JobID $jobID
```

### <a name="wait-for-a-job-toofinish"></a>Attendre un toofinish de travail

Au lieu de répéter `Get-AdlAnalyticsJob` jusqu'à ce qu’un travail est terminé, vous pouvez utiliser hello `Wait-AdlJob` toowait d’applet de commande pour tooend de travail hello.

```powershell
Wait-AdlJob -Account $adla -JobId $job.JobId
```

## <a name="manage-compute-policies"></a>Gérer les stratégies de calcul

### <a name="list-existing-compute-policies"></a>Lister les stratégies de calcul existantes

Hello `Get-AdlAnalyticsComputePolicy` applet de commande extrait des informations sur les stratégies de calcul pour un compte Analytique lac de données.

```powershell
$policies = Get-AdlAnalyticsComputePolicy -Account $adla
```

### <a name="create-a-compute-policy"></a>Créer une stratégie de calcul

Hello `New-AdlAnalyticsComputePolicy` applet de commande crée une nouvelle stratégie de calcul pour un compte Analytique lac de données. Cet exemple définit hello maximale toohello de AUs disponible spécifié utilisateur too50 et too250 de priorité hello minimal de tâche.

```powershell
$userObjectId = (Get-AzureRmAdUser -SearchString "garymcdaniel@contoso.com").Id

New-AdlAnalyticsComputePolicy -Account $adla -Name "GaryMcDaniel" -ObjectId $objectId -ObjectType User -MaxDegreeOfParallelismPerJob 50 -MinPriorityPerJob 250
```

## <a name="check-for-hello-existence-of-a-file"></a>Vérifier l’existence de hello d’un fichier.

```powershell
Test-AdlStoreItem -Account $adls -Path "/data.csv"
```

## <a name="uploading-and-downloading"></a>Chargement et téléchargement

Chargez un fichier.

```powershell
Import-AdlStoreItem -AccountName $adls -Path "c:\data.tsv" -Destination "/data_copy.csv" 
```

Chargez un dossier entier de manière récursive.

```powershell
Import-AdlStoreItem -AccountName $adls -Path "c:\myData\" -Destination "/myData/" -Recurse
```

Téléchargez un fichier.

```powershell
Export-AdlStoreItem -AccountName $adls -Path "/data.csv" -Destination "c:\data.csv"
```

Téléchargez un dossier entier de manière récursive.

```powershell
Export-AdlStoreItem -AccountName $adls -Path "/" -Destination "c:\myData\" -Recurse
```

> [!NOTE]
> Si hello télécharger ou les processus de téléchargement est interrompu, vous pouvez tenter de processus de hello tooresume par l’applet de commande hello en cours d’exécution avec hello ``-Resume`` indicateur.

## <a name="manage-catalog-items"></a>Gestion des éléments du catalogue

catalogue de Hello U-SQL est utilisé toostructure données et le code afin qu’ils peuvent être partagés par les scripts U-SQL. catalogue de Hello permet hello performances maximales des données dans Azure Data Lake. Pour plus d'informations, consultez [Utilisation du catalogue U-SQL](data-lake-analytics-use-u-sql-catalog.md).

### <a name="list-items-in-hello-u-sql-catalog"></a>Éléments de liste dans le catalogue de hello U-SQL

```powershell
# List U-SQL databases
Get-AdlCatalogItem -Account $adla -ItemType Database 

# List tables within a database
Get-AdlCatalogItem -Account $adla -ItemType Table -Path "database"

# List tables within a schema.
Get-AdlCatalogItem -Account $adla -ItemType Table -Path "database.schema"
```

Liste de tous les assemblys hello dans toutes les bases de données hello dans un compte ADLA.

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

### <a name="get-details-about-a-catalog-item"></a>Obtenir des détails sur un élément de catalogue

```powershell
# Get details of a table
Get-AdlCatalogItem  -Account $adla -ItemType Table -Path "master.dbo.mytable"

# Test existence of a U-SQL database.
Test-AdlCatalogItem  -Account $adla -ItemType Database -Path "master"
```

### <a name="create-credentials-in-a-catalog"></a>Créer des informations d’identification dans un catalogue

Dans une base de données U-SQL, créez un objet informations d’identification pour une base de données hébergée dans Azure. Actuellement, les informations d’identification U-SQL sont hello seul type d’élément de catalogue que vous pouvez créer via PowerShell.

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

### <a name="get-basic-information-about-an-adla-account"></a>Obtenir des informations de base sur un compte ADLA

Étant donné un nom de compte, hello suivant code recherche des informations de base à propos du compte hello

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

## <a name="working-with-azure"></a>Utilisation d’Azure

### <a name="get-details-of-azurerm-errors"></a>Obtenir des détails sur les erreurs AzureRm

```powershell
Resolve-AzureRmError -Last
```

### <a name="verify-if-you-are-running-as-an-administrator"></a>Vérifier que vous exécutez en tant qu’administrateur

```powershell
function Test-Administrator  
{  
    $user = [Security.Principal.WindowsIdentity]::GetCurrent();
    $p = New-Object Security.Principal.WindowsPrincipal $user
    $p.IsInRole([Security.Principal.WindowsBuiltinRole]::Administrator)  
}
```

### <a name="find-a-tenantid"></a>Trouver un TenantID

À partir du nom d’un abonnement :

```powershell
function Get-TenantIdFromSubcriptionName( [string] $subname )
{
    $sub = (Get-AzureRmSubscription -SubscriptionName $subname)
    $sub.TenantId
}

Get-TenantIdFromSubcriptionName "ADLTrainingMS"
```

À partir de l’ID d’un abonnement :

```powershell
function Get-TenantIdFromSubcriptionId( [string] $subid )
{
    $sub = (Get-AzureRmSubscription -SubscriptionId $subid)
    $sub.TenantId
}

$subid = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
Get-TenantIdFromSubcriptionId $subid
```

À partir d’une adresse de domaine, comme « contoso.com »


```powershell
function Get-TenantIdFromDomain( $domain )
{
    $url = "https://login.windows.net/" + $domain + "/.well-known/openid-configuration"
    return (Invoke-WebRequest $url|ConvertFrom-Json).token_endpoint.Split('/')[3]
}

$domain = "contoso.com"
Get-TenantIdFromDomain $domain
```

### <a name="list-all-your-subscriptions-and-tenant-ids"></a>Lister tous vos abonnements et leur ID client

```powershell
$subs = Get-AzureRmSubscription
foreach ($sub in $subs)
{
    Write-Host $sub.Name "("  $sub.Id ")"
    Write-Host "`tTenant Id" $sub.TenantId
}
```

## <a name="create-a-data-lake-analytics-account-using-a-template"></a>Créer un compte Data Lake Analytics à l’aide d’un modèle

Vous pouvez également utiliser un modèle de groupe de ressources Azure à l’aide de hello PowerShell script suivant :

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

Pour plus d’informations, consultez [Déploiement d’une application avec un modèle Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md) et [Création de modèles Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).

**Exemple de modèle**

Enregistrer hello après le texte comme un `.json` de fichier et l’utiliser hello précédant le modèle de PowerShell script toouse hello. 

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

## <a name="next-steps"></a>Étapes suivantes
* [Vue d'ensemble de Microsoft Azure Data Lake Analytics](data-lake-analytics-overview.md)
* Prise en main de Data Lake Analytics à l’aide du [portail Azure](data-lake-analytics-get-started-portal.md) | [Azure PowerShell](data-lake-analytics-get-started-powershell.md) | [CLI 2.0](data-lake-analytics-get-started-cli2.md)
* Gérer Azure Data Lake Analytics à l’aide du [portail Azure](data-lake-analytics-manage-use-portal.md) | [Azure PowerShell](data-lake-analytics-manage-use-powershell.md) | [CLI](data-lake-analytics-manage-use-cli.md) 
