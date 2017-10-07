---
title: "aaaManage Analytique de LAC de données Azure à l’aide du Kit de développement .NET Azure | Documents Microsoft"
description: "Découvrez comment toomanage Analytique lac de données des travaux de sources de données, les utilisateurs. "
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.assetid: 811d172d-9873-4ce9-a6d5-c1a26b374c79
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/18/2017
ms.author: saveenr
ms.openlocfilehash: 98630ba411823644a8bce1f1b0c1331f689cbb0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-data-lake-analytics-using-azure-net-sdk"></a>Gestion d’Azure Data Lake Analytics à l’aide du SDK Azure .NET
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

Découvrez comment des comptes toomanage Analytique de LAC de données Azure, des sources de données, des utilisateurs et des travaux à l’aide de hello Azure .NET SDK. 

## <a name="prerequisites"></a>Composants requis

* **Visual Studio 2015, Visual Studio 2013 mise à jour 4 ou Visual Studio 2012 avec Visual C++ installé**.
* **Kit SDK Microsoft Azure pour .NET version 2.5 ou ultérieure**.  Installer à l’aide de hello [le programme d’installation de Web platform](http://www.microsoft.com/web/downloads/platform.aspx).
* **Packages NuGet exigés**

### <a name="install-nuget-packages"></a>Installer les packages NuGet

|Package|Version|
|-------|-------|
|[Microsoft.Rest.ClientRuntime.Azure.Authentication](https://www.nuget.org/packages/Microsoft.Rest.ClientRuntime.Azure.Authentication)| 2.3.1|
|[Microsoft.Azure.Management.DataLake.Analytics](https://www.nuget.org/packages/Microsoft.Azure.Management.DataLake.Analytics)|3.0.0|
|[Microsoft.Azure.Management.DataLake.Store](https://www.nuget.org/packages/Microsoft.Azure.Management.DataLake.Store)|2.2.0|
|[Microsoft.Azure.Management.ResourceManager](https://www.nuget.org/packages/Microsoft.Azure.Management.ResourceManager)|1.6.0-preview|
|[Microsoft.Azure.Graph.RBAC](https://www.nuget.org/packages/Microsoft.Azure.Management.ResourceManager)|3.4.0-preview|

Vous pouvez installer ces packages via la ligne de commande hello NuGet avec hello suivant de commandes :

```
Install-Package -Id Microsoft.Rest.ClientRuntime.Azure.Authentication  -Version 2.3.1
Install-Package -Id Microsoft.Azure.Management.DataLake.Analytics  -Version 3.0.0
Install-Package -Id Microsoft.Azure.Management.DataLake.Store  -Version 2.2.0
Install-Package -Id Microsoft.Azure.Management.ResourceManager  -Version 1.6.0-preview
Install-Package -Id Microsoft.Azure.Graph.RBAC -Version 3.4.0-preview
```

## <a name="common-variables"></a>Variables communes

``` csharp
string subid = "<Subscription ID>"; // Subscription ID (a GUID)
string tenantid = "<Tenant ID>"; // AAD tenant ID or domain. For example, "contoso.onmicrosoft.com"
string rg == "<value>"; // Resource  group name
string clientid = "1950a258-227b-4e31-a9cf-717495945fc2"; // Sample client ID (this will work, but you should pick your own)
```

## <a name="authentication"></a>Authentification

Vous avez plusieurs options d’ouverture de session tooAzure Analytique lac de données. Hello extrait de code suivant montre un exemple d’authentification avec l’authentification d’utilisateur interactif avec un menu contextuel.

``` csharp
using System;
using System.IO;
using System.Threading;
using System.Security.Cryptography.X509Certificates;

using Microsoft.Rest;
using Microsoft.Rest.Azure.Authentication;
using Microsoft.Azure.Management.DataLake.Analytics;
using Microsoft.Azure.Management.DataLake.Analytics.Models;
using Microsoft.Azure.Management.DataLake.Store;
using Microsoft.Azure.Management.DataLake.Store.Models;
using Microsoft.IdentityModel.Clients.ActiveDirectory;
using Microsoft.Azure.Graph.RBAC;

public static Program
{
   public static string TENANT = "microsoft.onmicrosoft.com";
   public static string CLIENTID = "1950a258-227b-4e31-a9cf-717495945fc2";
   public static System.Uri ARM_TOKEN_AUDIENCE = new System.Uri( @"https://management.core.windows.net/");
   public static System.Uri ADL_TOKEN_AUDIENCE = new System.Uri( @"https://datalake.azure.net/" );
   public static System.Uri GRAPH_TOKEN_AUDIENCE = new System.Uri( @"https://graph.windows.net/" );

   static void Main(string[] args)
   {
      string MY_DOCUMENTS= System.Environment.GetFolderPath( System.Environment.SpecialFolder.MyDocuments);
      string TOKEN_CACHE_PATH = System.IO.Path.Combine(MY_DOCUMENTS, "my.tokencache");

      var tokenCache = GetTokenCache(TOKEN_CACHE_PATH);
      var armCreds = GetCreds_User_Popup(TENANT, ARM_TOKEN_AUDIENCE, CLIENTID, tokenCache);
      var adlCreds = GetCreds_User_Popup(TENANT, ADL_TOKEN_AUDIENCE, CLIENTID, tokenCache);
      var graphCreds = GetCreds_User_Popup(TENANT, GRAPH_TOKEN_AUDIENCE, CLIENTID, tokenCache);
   }
}
```

Hello de code source pour **GetCreds_User_Popup** et hello code pour les autres options pour l’authentification sont traitées dans [options d’authentification Data Lake Analytique .NET](https://github.com/Azure-Samples/data-lake-analytics-dotnet-auth-options)


## <a name="create-hello-client-management-objects"></a>Créer des objets de la gestion des clients de hello

``` csharp
var resourceManagementClient = new ResourceManagementClient(armCreds) { SubscriptionId = subid };

var adlaAccountClient = new DataLakeAnalyticsAccountManagementClient(armCreds);
adlaAccountClient.SubscriptionId = subid;

var adlsAccountClient = new DataLakeStoreAccountManagementClient(armCreds);
adlsAccountClient.SubscriptionId = subid;

var adlaCatalogClient = new DataLakeAnalyticsCatalogManagementClient(adlCreds);
var adlaJobClient = new DataLakeAnalyticsJobManagementClient(adlCreds);

var adlsFileSystemClient = new DataLakeStoreFileSystemManagementClient(adlCreds);

var  graphClient = new GraphRbacManagementClient(graphCreds);
graphClient.TenantID = domain;

```

## <a name="manage-accounts"></a>Gérer les comptes

### <a name="create-an-azure-resource-group"></a>Créer un groupe de ressources Azure

Si vous n’avez pas déjà créé un, vous devez disposer d’un groupe de ressources Azure de toocreate vos composants Analytique lac de données. Vous avez besoin de vos informations d’identification d’authentification, d’un ID d’abonnement et d’un emplacement. Hello suivant de code montre comment toocreate un groupe de ressources :

``` csharp
var resourceGroup = new ResourceGroup { Location = location };
resourceManagementClient.ResourceGroups.CreateOrUpdate(groupName, rg);
```
Pour plus d’informations, consultez [Groupes de ressources Azure et Data Lake Analytics](#Azure-Resource-Groups-and-Data-Lake-Analytics).

### <a name="create-a-data-lake-store-account"></a>Créer un compte Data Lake Store

Le compte ADLA nécessite un compte ADLS. Si vous n’avez pas encore un toouse, vous pouvez créer une avec hello suivant de code :

``` csharp
var new_adls_params = new DataLakeStoreAccount(location: _location);
adlsAccountClient.Account.Create(rg, adls, new_adls_params);
```

### <a name="create-a-data-lake-analytics-account"></a>Créer un compte Data Lake Analytics

Hello suivante de code crée un compte ADLS

``` csharp
var new_adla_params = new DataLakeAnalyticsAccount()
{
   DefaultDataLakeStoreAccount = adls,
   Location = location
};

adlaClient.Account.Create(rg, adla, new_adla_params);
```

### <a name="list-data-lake-store-accounts"></a>Lister les comptes Data Lake Store

``` csharp
var adlsAccounts = adlsAccountClient.Account.List().ToList();
foreach (var adls in adlsAccounts)
{
   Console.WriteLine($"ADLS: {0}", adls.Name);
}
```

### <a name="list-data-lake-analytics-accounts"></a>Énumérer les comptes Data Lake Analytics

``` csharp
var adlaAccounts = adlaClient.Account.List().ToList();

for (var adla in AdlaAccounts)
{
   Console.WriteLine($"ADLA: {0}, adla.Name");
}
```

### <a name="checking-if-an-account-exists"></a>Vérifier si un compte existe

``` csharp
bool exists = adlaClient.Account.Exists(rg, adla));
```

### <a name="get-information-about-an-account"></a>Obtenir des informations sur un compte

``` csharp
bool exists = adlaClient.Account.Exists(rg, adla));
if (exists)
{
   var adla_accnt = adlaClient.Account.Get(rg, adla);
}
```

### <a name="delete-an-account"></a>Supprimer un compte

``` csharp
if (adlaClient.Account.Exists(rg, adla))
{
   adlaClient.Account.Delete(rg, adla);
}
```

### <a name="get-hello-default-data-lake-store-account"></a>Obtenir le compte de Data Lake Store hello par défaut

Chaque compte Data Lake Analytics nécessite un compte Data Lake Store par défaut. Utilisez ce compte de magasin de code toodetermine hello par défaut pour un compte Analytique.

``` csharp
if (adlaClient.Account.Exists(rg, adla))
{
  var adla_accnt = adlaClient.Account.Get(rg, adla);
  string def_adls_account = adla_accnt.DefaultDataLakeStoreAccount;
}
```

## <a name="manage-data-sources"></a>Gérer les sources de données

Analytique lac de données prend en charge actuellement les hello les sources de données suivantes :

* [Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md)
* [Compte Stockage Azure](../storage/common/storage-introduction.md)

### <a name="link-tooan-azure-storage-account"></a>Lien tooan compte de stockage Azure

Vous pouvez créer des liens tooAzure les comptes de stockage.

``` csharp
string storage_key = "xxxxxxxxxxxxxxxxxxxx";
string storage_account = "mystorageaccount";
var addParams = new AddStorageAccountParameters(storage_key);            
adlaClient.StorageAccounts.Add(rg, adla, storage_account, addParams);
```

### <a name="list-azure-storage-data-sources"></a>Lister les sources de données de stockage Azure

``` csharp
var stg_accounts = adlaAccountClient.StorageAccounts.ListByAccount(rg, adla);

if (stg_accounts != null)
{
  foreach (var stg_account in stg_accounts)
  {
      Console.WriteLine($"Storage account: {0}", stg_account.Name);
  }
}
```

### <a name="list-data-lake-store-data-sources"></a>Afficher la liste des sources de données Data Lake Store

``` csharp
var adls_accounts = adlsClient.Account.List();

if (adls_accounts != null)
{
  foreach (var adls_accnt in adls_accounts)
  {
      Console.WriteLine($"ADLS account: {0}", adls_accnt.Name);
  }
}
```

### <a name="upload-and-download-folders-and-files"></a>Charger et télécharger des dossiers et des fichiers
Vous pouvez utiliser tooupload objet de hello Data Lake Store fichier système client Gestion et télécharger des fichiers individuels ou des dossiers à partir de l’ordinateur local de Azure tooyour, à l’aide des méthodes suivantes de hello :

- UploadFolder
- UploadFile
- DownloadFolder
- DownloadFile

premier paramètre de Hello pour ces méthodes désigne hello hello compte du magasin Data Lake, suivi par des paramètres pour la source hello et chemin d’accès de destination de hello.

Bonjour à l’exemple suivant montre comment toodownload un dossier dans hello Data Lake Store.

``` csharp
adlsFileSystemClient.FileSystem.DownloadFolder(adls, sourcePath, destinationPath);
```

### <a name="create-a-file-in-a-data-lake-store-account"></a>Créer un fichier dans un compte Data Lake Store

``` csharp
using (var memstream = new MemoryStream())
{
   using (var sw = new StreamWriter(memstream, UTF8Encoding.UTF8))
   {
      sw.WriteLine("Hello World");
      sw.Flush();

      adlsFileSystemClient.FileSystem.Create(adls, "/Samples/Output/randombytes.csv", memstream);
   }
}
```

### <a name="verify-azure-storage-account-paths"></a>Vérifier les chemins des comptes de stockage Azure
Hello de code suivant vérifie si un compte de stockage Azure (storageAccntName) existe dans un compte Analytique lac de données (analyticsAccountName), et si un conteneur (containerName) existe dans le compte de stockage Azure hello.

``` csharp
string storage_account = "mystorageaccount";
string storage_container = "mycontainer";
bool accountExists = adlaClient.Account.StorageAccountExists(rg, adla, storage_account));
bool containerExists = adlaClient.Account.StorageContainerExists(rg, adla, storage_account, storage_container));
```

## <a name="manage-catalog-and-jobs"></a>Gérer le catalogue et les travaux
objet de DataLakeAnalyticsCatalogManagementClient Hello fournit des méthodes pour la gestion de base de données SQL hello fourni pour chaque compte Analytique de LAC de données Azure. Hello DataLakeAnalyticsJobManagementClient fournit les méthodes toosubmit et gérer des tâches exécutées sur la base de données de hello avec scripts U-SQL.

### <a name="list-databases-and-schemas"></a>Afficher la liste des bases de données et des schémas
Entre hello plusieurs choses que vous pouvez répertorier, hello plus courantes sont les bases de données et leur schéma. Bonjour de code suivant obtient une collection de bases de données et énumère ensuite le schéma de hello pour chaque base de données.

``` csharp
var databases = adlaCatalogClient.Catalog.ListDatabases(adla);
foreach (var db in databases)
{
  Console.WriteLine($"Database: {db.Name}");
  Console.WriteLine(" - Schemas:");
  var schemas = adlaCatalogClient.Catalog.ListSchemas(adla, db.Name);
  foreach (var schm in schemas)
  {
      Console.WriteLine($"\t{schm.Name}");
  }
}
```

### <a name="list-table-columns"></a>Afficher la liste des colonnes d’une table
Hello de code suivant montre comment tooaccess hello de base de données avec un catalogue de données Lake Analytique gestion client toolist hello des colonnes dans une table spécifiée.

``` csharp
var tbl = adlaCatalogClient.Catalog.GetTable(adla, "master", "dbo", "MyTableName");
IEnumerable<USqlTableColumn> columns = tbl.ColumnList;

foreach (USqlTableColumn utc in columns)
{
  string scriptPath = "/Samples/Scripts/SearchResults_Wikipedia_Script.txt";
  Stream scriptStrm = adlsFileSystemClient.FileSystem.Open(_adlsAccountName, scriptPath);
  string scriptTxt = string.Empty;
  using (StreamReader sr = new StreamReader(scriptStrm))
  {
      scriptTxt = sr.ReadToEnd();
  }

  var jobName = "SR_Wikipedia";
  var jobId = Guid.NewGuid();
  var properties = new USqlJobProperties(scriptTxt);
  var parameters = new JobInformation(jobName, JobType.USql, properties, priority: 1, degreeOfParallelism: 1, jobId: jobId);
  var jobInfo = adlaJobClient.Job.Create(adla, jobId, parameters);
  Console.WriteLine($"Job {jobName} submitted.");

}
```

### <a name="list-failed-jobs"></a>Afficher la liste des travaux ayant échoué
Hello de code suivant affiche des informations sur les tâches qui ont échoué.

``` csharp
var odq = new ODataQuery<JobInformation> { Filter = "result eq 'Failed'" };
var jobs = adlaJobClient.Job.List(adla, odq);
foreach (var j in jobs)
{
   Console.WriteLine($"{j.Name}\t{j.JobId}\t{j.Type}\t{j.StartTime}\t{j.EndTime}");
}
```

### <a name="list-pipelines"></a>Lister les pipelines
Hello de code suivant répertorie des informations sur chaque pipeline de travaux soumis toohello compte.

``` csharp
var pipelines = adlaJobClient.Pipeline.List(adla);
foreach (var p in pipelines)
{
   Console.WriteLine($"Pipeline: {p.Name}\t{p.PipelineId}\t{p.LastSubmitTime}");
}
```

### <a name="list-recurrences"></a>Lister les récurrences
Hello de code suivant répertorie des informations sur chaque occurrence de travaux soumis toohello compte.

``` csharp
var recurrences = adlaJobClient.Recurrence.List(adla);
foreach (var r in recurrences)
{
   Console.WriteLine($"Recurrence: {r.Name}\t{r.RecurrenceId}\t{r.LastSubmitTime}");
}
```

## <a name="common-graph-scenarios"></a>Scénarios courants de graphe

### <a name="look-up-user-in-hello-aad-directory"></a>Rechercher l’utilisateur dans l’annuaire de hello AAD

``` csharp
var userinfo = graphClient.Users.Get( "bill@contoso.com" );
```

### <a name="get-hello-objectid-of-a-user-in-hello-aad-directory"></a>Obtenir hello ObjectId d’un utilisateur dans l’annuaire de hello AAD

``` csharp
var userinfo = graphClient.Users.Get( "bill@contoso.com" );
Console.WriteLine( userinfo.ObjectId )
```

## <a name="manage-compute-policies"></a>Gérer les stratégies de calcul
objet de DataLakeAnalyticsAccountManagementClient Hello fournit des méthodes pour la gestion hello de calcul des stratégies pour un compte Analytique lac de données.

### <a name="list-compute-policies"></a>Lister les stratégies de calcul
Hello suivant code récupère une liste de stratégies de calcul pour un compte Analytique lac de données.

``` csharp
var policies = adlaAccountClient.ComputePolicies.ListByAccount(rg, adla);
foreach (var p in policies)
{
   Console.WriteLine($"Name: {p.Name}\tType: {p.ObjectType}\tMax AUs / job: {p.MaxDegreeOfParallelismPerJob}\tMin priority / job: {p.MinPriorityPerJob}");
}
```

### <a name="create-a-new-compute-policy"></a>Créer une nouvelle stratégie de calcul
Hello suivante de code crée une nouvelle stratégie de calcul pour un compte Analytique lac de données, paramètre hello maximale AUs disponible toohello spécifié utilisateur too50 et too250 de priorité hello minimal de tâche.

``` csharp
var userAadObjectId = "3b097601-4912-4d41-b9d2-78672fc2acde";
var newPolicyParams = new ComputePolicyCreateOrUpdateParameters(userAadObjectId, "User", 50, 250);
adlaAccountClient.ComputePolicies.CreateOrUpdate(rg, adla, "GaryMcDaniel", newPolicyParams);
```

## <a name="next-steps"></a>Étapes suivantes
* [Vue d'ensemble de Microsoft Azure Data Lake Analytics](data-lake-analytics-overview.md)
* [Gestion d’Azure Data Lake Analytics à l’aide du portail Azure](data-lake-analytics-manage-use-portal.md)
* [Surveiller et résoudre les problèmes des tâches Azure Data Lake Analytics à l’aide du portail Azure](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)
