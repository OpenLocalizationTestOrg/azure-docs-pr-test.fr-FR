---
title: "Gestion d’Azure Data Lake Analytics à l’aide du SDK Azure .NET | Microsoft Docs"
description: "Apprenez à gérer des travaux Data Lake Analytics, des sources de données, des utilisateurs. "
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
ms.openlocfilehash: 0f8a95f96ce4c816dfb9132923faa9a9bf20c205
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="manage-azure-data-lake-analytics-using-azure-net-sdk"></a><span data-ttu-id="456d0-103">Gestion d’Azure Data Lake Analytics à l’aide du SDK Azure .NET</span><span class="sxs-lookup"><span data-stu-id="456d0-103">Manage Azure Data Lake Analytics using Azure .NET SDK</span></span>
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

<span data-ttu-id="456d0-104">Apprenez à gérer des comptes Azure Data Lake Analytics, des sources de données, des utilisateurs et des travaux à l’aide du kit SDK Azure .NET.</span><span class="sxs-lookup"><span data-stu-id="456d0-104">Learn how to manage Azure Data Lake Analytics accounts, data sources, users, and jobs using the Azure .NET SDK.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="456d0-105">Composants requis</span><span class="sxs-lookup"><span data-stu-id="456d0-105">Prerequisites</span></span>

* <span data-ttu-id="456d0-106">**Visual Studio 2015, Visual Studio 2013 mise à jour 4 ou Visual Studio 2012 avec Visual C++ installé**.</span><span class="sxs-lookup"><span data-stu-id="456d0-106">**Visual Studio 2015, Visual Studio 2013 update 4, or Visual Studio 2012 with Visual C++ Installed**.</span></span>
* <span data-ttu-id="456d0-107">**Kit SDK Microsoft Azure pour .NET version 2.5 ou ultérieure**.</span><span class="sxs-lookup"><span data-stu-id="456d0-107">**Microsoft Azure SDK for .NET version 2.5 or above**.</span></span>  <span data-ttu-id="456d0-108">Installez-le avec [Web Platform Installer](http://www.microsoft.com/web/downloads/platform.aspx).</span><span class="sxs-lookup"><span data-stu-id="456d0-108">Install it using the [Web platform installer](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
* <span data-ttu-id="456d0-109">**Packages NuGet exigés**</span><span class="sxs-lookup"><span data-stu-id="456d0-109">**Required NuGet Packages**</span></span>

### <a name="install-nuget-packages"></a><span data-ttu-id="456d0-110">Installer les packages NuGet</span><span class="sxs-lookup"><span data-stu-id="456d0-110">Install NuGet packages</span></span>

|<span data-ttu-id="456d0-111">Package</span><span class="sxs-lookup"><span data-stu-id="456d0-111">Package</span></span>|<span data-ttu-id="456d0-112">Version</span><span class="sxs-lookup"><span data-stu-id="456d0-112">Version</span></span>|
|-------|-------|
|[<span data-ttu-id="456d0-113">Microsoft.Rest.ClientRuntime.Azure.Authentication</span><span class="sxs-lookup"><span data-stu-id="456d0-113">Microsoft.Rest.ClientRuntime.Azure.Authentication</span></span>](https://www.nuget.org/packages/Microsoft.Rest.ClientRuntime.Azure.Authentication)| <span data-ttu-id="456d0-114">2.3.1</span><span class="sxs-lookup"><span data-stu-id="456d0-114">2.3.1</span></span>|
|[<span data-ttu-id="456d0-115">Microsoft.Azure.Management.DataLake.Analytics</span><span class="sxs-lookup"><span data-stu-id="456d0-115">Microsoft.Azure.Management.DataLake.Analytics</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Management.DataLake.Analytics)|<span data-ttu-id="456d0-116">3.0.0</span><span class="sxs-lookup"><span data-stu-id="456d0-116">3.0.0</span></span>|
|[<span data-ttu-id="456d0-117">Microsoft.Azure.Management.DataLake.Store</span><span class="sxs-lookup"><span data-stu-id="456d0-117">Microsoft.Azure.Management.DataLake.Store</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Management.DataLake.Store)|<span data-ttu-id="456d0-118">2.2.0</span><span class="sxs-lookup"><span data-stu-id="456d0-118">2.2.0</span></span>|
|[<span data-ttu-id="456d0-119">Microsoft.Azure.Management.ResourceManager</span><span class="sxs-lookup"><span data-stu-id="456d0-119">Microsoft.Azure.Management.ResourceManager</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Management.ResourceManager)|<span data-ttu-id="456d0-120">1.6.0-preview</span><span class="sxs-lookup"><span data-stu-id="456d0-120">1.6.0-preview</span></span>|
|[<span data-ttu-id="456d0-121">Microsoft.Azure.Graph.RBAC</span><span class="sxs-lookup"><span data-stu-id="456d0-121">Microsoft.Azure.Graph.RBAC</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Management.ResourceManager)|<span data-ttu-id="456d0-122">3.4.0-preview</span><span class="sxs-lookup"><span data-stu-id="456d0-122">3.4.0-preview</span></span>|

<span data-ttu-id="456d0-123">Vous pouvez installer ces packages via la ligne de commande NuGet avec les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="456d0-123">You can install these packages via the NuGet command line with the following commands:</span></span>

```
Install-Package -Id Microsoft.Rest.ClientRuntime.Azure.Authentication  -Version 2.3.1
Install-Package -Id Microsoft.Azure.Management.DataLake.Analytics  -Version 3.0.0
Install-Package -Id Microsoft.Azure.Management.DataLake.Store  -Version 2.2.0
Install-Package -Id Microsoft.Azure.Management.ResourceManager  -Version 1.6.0-preview
Install-Package -Id Microsoft.Azure.Graph.RBAC -Version 3.4.0-preview
```

## <a name="common-variables"></a><span data-ttu-id="456d0-124">Variables communes</span><span class="sxs-lookup"><span data-stu-id="456d0-124">Common variables</span></span>

``` csharp
string subid = "<Subscription ID>"; // Subscription ID (a GUID)
string tenantid = "<Tenant ID>"; // AAD tenant ID or domain. For example, "contoso.onmicrosoft.com"
string rg == "<value>"; // Resource  group name
string clientid = "1950a258-227b-4e31-a9cf-717495945fc2"; // Sample client ID (this will work, but you should pick your own)
```

## <a name="authentication"></a><span data-ttu-id="456d0-125">Authentification</span><span class="sxs-lookup"><span data-stu-id="456d0-125">Authentication</span></span>

<span data-ttu-id="456d0-126">Pour vous connecter à Azure Data Lake Analytics, plusieurs options s’offrent à vous.</span><span class="sxs-lookup"><span data-stu-id="456d0-126">You have multiple options for logging on to Azure Data Lake Analytics.</span></span> <span data-ttu-id="456d0-127">L’extrait de code suivant montre un exemple d’authentification avec l’authentification utilisateur interactif à l’aide d’un menu contextuel.</span><span class="sxs-lookup"><span data-stu-id="456d0-127">The following snippet shows an example of authentication with interactive user authentication with a pop-up.</span></span>

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

<span data-ttu-id="456d0-128">Le code source pour **GetCreds_User_Popup** et le code pour les autres options d’authentification sont traités dans la rubrique [Options d’authentification Data Lake Analytics .NET](https://github.com/Azure-Samples/data-lake-analytics-dotnet-auth-options)</span><span class="sxs-lookup"><span data-stu-id="456d0-128">The source code for **GetCreds_User_Popup** and the code for other options for authentication are covered in [Data Lake Analytics .NET authentication options](https://github.com/Azure-Samples/data-lake-analytics-dotnet-auth-options)</span></span>


## <a name="create-the-client-management-objects"></a><span data-ttu-id="456d0-129">Créer les objets de gestion de client</span><span class="sxs-lookup"><span data-stu-id="456d0-129">Create the client management objects</span></span>

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

## <a name="manage-accounts"></a><span data-ttu-id="456d0-130">Gérer les comptes</span><span class="sxs-lookup"><span data-stu-id="456d0-130">Manage accounts</span></span>

### <a name="create-an-azure-resource-group"></a><span data-ttu-id="456d0-131">Créer un groupe de ressources Azure</span><span class="sxs-lookup"><span data-stu-id="456d0-131">Create an Azure Resource Group</span></span>

<span data-ttu-id="456d0-132">Si ce n’est déjà fait, vous devez créer un groupe de ressources Azure pour pouvoir créer vos composants Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="456d0-132">If you haven't already created one, you must have an Azure Resource Group to create your Data Lake Analytics components.</span></span> <span data-ttu-id="456d0-133">Vous avez besoin de vos informations d’identification d’authentification, d’un ID d’abonnement et d’un emplacement.</span><span class="sxs-lookup"><span data-stu-id="456d0-133">You  need your authentication credentials, subscription ID, and a location.</span></span> <span data-ttu-id="456d0-134">Le code suivant montre comment créer un groupe de ressources :</span><span class="sxs-lookup"><span data-stu-id="456d0-134">The following code shows how to create a resource group:</span></span>

``` csharp
var resourceGroup = new ResourceGroup { Location = location };
resourceManagementClient.ResourceGroups.CreateOrUpdate(groupName, rg);
```
<span data-ttu-id="456d0-135">Pour plus d’informations, consultez [Groupes de ressources Azure et Data Lake Analytics](#Azure-Resource-Groups-and-Data-Lake-Analytics).</span><span class="sxs-lookup"><span data-stu-id="456d0-135">For more information, see [Azure Resource Groups and Data Lake Analytics](#Azure-Resource-Groups-and-Data-Lake-Analytics).</span></span>

### <a name="create-a-data-lake-store-account"></a><span data-ttu-id="456d0-136">Créer un compte Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="456d0-136">Create a Data Lake Store account</span></span>

<span data-ttu-id="456d0-137">Le compte ADLA nécessite un compte ADLS.</span><span class="sxs-lookup"><span data-stu-id="456d0-137">Ever ADLA account requires an ADLS account.</span></span> <span data-ttu-id="456d0-138">Si vous n’en avez pas, vous pouvez en créer un avec le code suivant :</span><span class="sxs-lookup"><span data-stu-id="456d0-138">If you don't already have one to use, you can create one with the following code:</span></span>

``` csharp
var new_adls_params = new DataLakeStoreAccount(location: _location);
adlsAccountClient.Account.Create(rg, adls, new_adls_params);
```

### <a name="create-a-data-lake-analytics-account"></a><span data-ttu-id="456d0-139">Créer un compte Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="456d0-139">Create a Data Lake Analytics account</span></span>

<span data-ttu-id="456d0-140">Le code suivant crée un compte ADLS</span><span class="sxs-lookup"><span data-stu-id="456d0-140">The following code creates an ADLS account</span></span>

``` csharp
var new_adla_params = new DataLakeAnalyticsAccount()
{
   DefaultDataLakeStoreAccount = adls,
   Location = location
};

adlaClient.Account.Create(rg, adla, new_adla_params);
```

### <a name="list-data-lake-store-accounts"></a><span data-ttu-id="456d0-141">Lister les comptes Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="456d0-141">List Data Lake Store accounts</span></span>

``` csharp
var adlsAccounts = adlsAccountClient.Account.List().ToList();
foreach (var adls in adlsAccounts)
{
   Console.WriteLine($"ADLS: {0}", adls.Name);
}
```

### <a name="list-data-lake-analytics-accounts"></a><span data-ttu-id="456d0-142">Énumérer les comptes Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="456d0-142">List Data Lake Analytics accounts</span></span>

``` csharp
var adlaAccounts = adlaClient.Account.List().ToList();

for (var adla in AdlaAccounts)
{
   Console.WriteLine($"ADLA: {0}, adla.Name");
}
```

### <a name="checking-if-an-account-exists"></a><span data-ttu-id="456d0-143">Vérifier si un compte existe</span><span class="sxs-lookup"><span data-stu-id="456d0-143">Checking if an account exists</span></span>

``` csharp
bool exists = adlaClient.Account.Exists(rg, adla));
```

### <a name="get-information-about-an-account"></a><span data-ttu-id="456d0-144">Obtenir des informations sur un compte</span><span class="sxs-lookup"><span data-stu-id="456d0-144">Get information about an account</span></span>

``` csharp
bool exists = adlaClient.Account.Exists(rg, adla));
if (exists)
{
   var adla_accnt = adlaClient.Account.Get(rg, adla);
}
```

### <a name="delete-an-account"></a><span data-ttu-id="456d0-145">Supprimer un compte</span><span class="sxs-lookup"><span data-stu-id="456d0-145">Delete an account</span></span>

``` csharp
if (adlaClient.Account.Exists(rg, adla))
{
   adlaClient.Account.Delete(rg, adla);
}
```

### <a name="get-the-default-data-lake-store-account"></a><span data-ttu-id="456d0-146">Afficher le compte Data Lake Store par défaut</span><span class="sxs-lookup"><span data-stu-id="456d0-146">Get the default Data Lake Store account</span></span>

<span data-ttu-id="456d0-147">Chaque compte Data Lake Analytics nécessite un compte Data Lake Store par défaut.</span><span class="sxs-lookup"><span data-stu-id="456d0-147">Every Data Lake Analytics account requires a default Data Lake Store account.</span></span> <span data-ttu-id="456d0-148">Utilisez ce code pour identifier le compte par défaut d’un compte Analytics.</span><span class="sxs-lookup"><span data-stu-id="456d0-148">Use this code to determine the default Store account for an Analytics account.</span></span>

``` csharp
if (adlaClient.Account.Exists(rg, adla))
{
  var adla_accnt = adlaClient.Account.Get(rg, adla);
  string def_adls_account = adla_accnt.DefaultDataLakeStoreAccount;
}
```

## <a name="manage-data-sources"></a><span data-ttu-id="456d0-149">Gérer les sources de données</span><span class="sxs-lookup"><span data-stu-id="456d0-149">Manage data sources</span></span>

<span data-ttu-id="456d0-150">Data Lake Analytics prend actuellement en charge les sources de données suivantes :</span><span class="sxs-lookup"><span data-stu-id="456d0-150">Data Lake Analytics currently supports the following data sources:</span></span>

* [<span data-ttu-id="456d0-151">Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="456d0-151">Azure Data Lake Store</span></span>](../data-lake-store/data-lake-store-overview.md)
* [<span data-ttu-id="456d0-152">Compte Stockage Azure</span><span class="sxs-lookup"><span data-stu-id="456d0-152">Azure Storage Account</span></span>](../storage/common/storage-introduction.md)

### <a name="link-to-an-azure-storage-account"></a><span data-ttu-id="456d0-153">Lier à un compte de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="456d0-153">Link to an Azure Storage account</span></span>

<span data-ttu-id="456d0-154">Vous pouvez créer des liens vers des comptes Stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="456d0-154">You can create links to Azure Storage accounts.</span></span>

``` csharp
string storage_key = "xxxxxxxxxxxxxxxxxxxx";
string storage_account = "mystorageaccount";
var addParams = new AddStorageAccountParameters(storage_key);            
adlaClient.StorageAccounts.Add(rg, adla, storage_account, addParams);
```

### <a name="list-azure-storage-data-sources"></a><span data-ttu-id="456d0-155">Lister les sources de données de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="456d0-155">List Azure Storage data sources</span></span>

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

### <a name="list-data-lake-store-data-sources"></a><span data-ttu-id="456d0-156">Afficher la liste des sources de données Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="456d0-156">List Data Lake Store data sources</span></span>

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

### <a name="upload-and-download-folders-and-files"></a><span data-ttu-id="456d0-157">Charger et télécharger des dossiers et des fichiers</span><span class="sxs-lookup"><span data-stu-id="456d0-157">Upload and download folders and files</span></span>
<span data-ttu-id="456d0-158">Vous pouvez utiliser l’objet de gestion de client du système de fichiers Data Lake Store pour charger et télécharger des fichiers ou des dossiers à partir d’Azure sur votre ordinateur local. Pour cela, utilisez les méthodes suivantes :</span><span class="sxs-lookup"><span data-stu-id="456d0-158">You can use the Data Lake Store file system client management object to upload and download individual files or folders from Azure to your local computer, using the following methods:</span></span>

- <span data-ttu-id="456d0-159">UploadFolder</span><span class="sxs-lookup"><span data-stu-id="456d0-159">UploadFolder</span></span>
- <span data-ttu-id="456d0-160">UploadFile</span><span class="sxs-lookup"><span data-stu-id="456d0-160">UploadFile</span></span>
- <span data-ttu-id="456d0-161">DownloadFolder</span><span class="sxs-lookup"><span data-stu-id="456d0-161">DownloadFolder</span></span>
- <span data-ttu-id="456d0-162">DownloadFile</span><span class="sxs-lookup"><span data-stu-id="456d0-162">DownloadFile</span></span>

<span data-ttu-id="456d0-163">Le premier paramètre de ces méthodes est le nom du compte Data Lake Store, suivi des paramètres du chemin source et du chemin de destination.</span><span class="sxs-lookup"><span data-stu-id="456d0-163">The first parameter for these methods is the name of the Data Lake Store Account, followed by parameters for the source path and the destination path.</span></span>

<span data-ttu-id="456d0-164">L’exemple suivant montre comment télécharger un dossier dans le Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="456d0-164">The following example shows how to download a folder in the Data Lake Store.</span></span>

``` csharp
adlsFileSystemClient.FileSystem.DownloadFolder(adls, sourcePath, destinationPath);
```

### <a name="create-a-file-in-a-data-lake-store-account"></a><span data-ttu-id="456d0-165">Créer un fichier dans un compte Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="456d0-165">Create a file in a Data Lake Store account</span></span>

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

### <a name="verify-azure-storage-account-paths"></a><span data-ttu-id="456d0-166">Vérifier les chemins des comptes de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="456d0-166">Verify Azure Storage account paths</span></span>
<span data-ttu-id="456d0-167">Le code suivant vérifie si un compte de stockage Azure (storageAccntName) existe dans un compte Data Lake Analytics (analyticsAccountName) et si un conteneur (containerName) existe dans le compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="456d0-167">The following code checks if an Azure Storage account (storageAccntName) exists in a Data Lake Analytics account (analyticsAccountName), and if a container (containerName) exists in the Azure Storage account.</span></span>

``` csharp
string storage_account = "mystorageaccount";
string storage_container = "mycontainer";
bool accountExists = adlaClient.Account.StorageAccountExists(rg, adla, storage_account));
bool containerExists = adlaClient.Account.StorageContainerExists(rg, adla, storage_account, storage_container));
```

## <a name="manage-catalog-and-jobs"></a><span data-ttu-id="456d0-168">Gérer le catalogue et les travaux</span><span class="sxs-lookup"><span data-stu-id="456d0-168">Manage catalog and jobs</span></span>
<span data-ttu-id="456d0-169">L’objet DataLakeAnalyticsCatalogManagementClient fournit des méthodes pour gérer la base de données SQL fournie pour chaque compte Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="456d0-169">The DataLakeAnalyticsCatalogManagementClient object provides methods for managing the SQL database provided for each Azure Data Lake Analytics account.</span></span> <span data-ttu-id="456d0-170">L’objet DataLakeAnalyticsJobManagementClient fournit des méthodes pour envoyer et gérer les tâches exécutées sur la base de données avec des scripts U-SQL.</span><span class="sxs-lookup"><span data-stu-id="456d0-170">The DataLakeAnalyticsJobManagementClient provides methods to submit and manage jobs run on the database with U-SQL scripts.</span></span>

### <a name="list-databases-and-schemas"></a><span data-ttu-id="456d0-171">Afficher la liste des bases de données et des schémas</span><span class="sxs-lookup"><span data-stu-id="456d0-171">List databases and schemas</span></span>
<span data-ttu-id="456d0-172">Parmi les éléments dont vous pouvez afficher la liste, les plus courants sont les bases de données et leur schéma.</span><span class="sxs-lookup"><span data-stu-id="456d0-172">Among the several things you can list, the most common are databases and their schema.</span></span> <span data-ttu-id="456d0-173">Le code suivant obtient une collection de bases de données, puis indique le schéma pour chaque base de données.</span><span class="sxs-lookup"><span data-stu-id="456d0-173">The following code obtains a collection of databases, and then enumerates the schema for each database.</span></span>

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

### <a name="list-table-columns"></a><span data-ttu-id="456d0-174">Afficher la liste des colonnes d’une table</span><span class="sxs-lookup"><span data-stu-id="456d0-174">List table columns</span></span>
<span data-ttu-id="456d0-175">Le code suivant montre comment accéder à la base de données avec un objet DataLakeAnalyticsCatalogManagementClient pour répertorier les colonnes de la table spécifiée.</span><span class="sxs-lookup"><span data-stu-id="456d0-175">The following code shows how to access the database with a Data Lake Analytics Catalog management client to list the columns in a specified table.</span></span>

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

### <a name="list-failed-jobs"></a><span data-ttu-id="456d0-176">Afficher la liste des travaux ayant échoué</span><span class="sxs-lookup"><span data-stu-id="456d0-176">List failed jobs</span></span>
<span data-ttu-id="456d0-177">Le code suivant répertorie les informations sur les travaux qui ont échoué.</span><span class="sxs-lookup"><span data-stu-id="456d0-177">The following code lists information about jobs that failed.</span></span>

``` csharp
var odq = new ODataQuery<JobInformation> { Filter = "result eq 'Failed'" };
var jobs = adlaJobClient.Job.List(adla, odq);
foreach (var j in jobs)
{
   Console.WriteLine($"{j.Name}\t{j.JobId}\t{j.Type}\t{j.StartTime}\t{j.EndTime}");
}
```

### <a name="list-pipelines"></a><span data-ttu-id="456d0-178">Lister les pipelines</span><span class="sxs-lookup"><span data-stu-id="456d0-178">List pipelines</span></span>
<span data-ttu-id="456d0-179">Le code suivant liste des informations sur chaque pipeline de travaux envoyés au compte.</span><span class="sxs-lookup"><span data-stu-id="456d0-179">The following code lists information about each pipeline of jobs submitted to the account.</span></span>

``` csharp
var pipelines = adlaJobClient.Pipeline.List(adla);
foreach (var p in pipelines)
{
   Console.WriteLine($"Pipeline: {p.Name}\t{p.PipelineId}\t{p.LastSubmitTime}");
}
```

### <a name="list-recurrences"></a><span data-ttu-id="456d0-180">Lister les récurrences</span><span class="sxs-lookup"><span data-stu-id="456d0-180">List recurrences</span></span>
<span data-ttu-id="456d0-181">Le code suivant liste des informations sur chaque récurrence de travaux envoyés au compte.</span><span class="sxs-lookup"><span data-stu-id="456d0-181">The following code lists information about each recurrence of jobs submitted to the account.</span></span>

``` csharp
var recurrences = adlaJobClient.Recurrence.List(adla);
foreach (var r in recurrences)
{
   Console.WriteLine($"Recurrence: {r.Name}\t{r.RecurrenceId}\t{r.LastSubmitTime}");
}
```

## <a name="common-graph-scenarios"></a><span data-ttu-id="456d0-182">Scénarios courants de graphe</span><span class="sxs-lookup"><span data-stu-id="456d0-182">Common graph scenarios</span></span>

### <a name="look-up-user-in-the-aad-directory"></a><span data-ttu-id="456d0-183">Rechercher l’utilisateur dans le répertoire AAD</span><span class="sxs-lookup"><span data-stu-id="456d0-183">Look up user in the AAD directory</span></span>

``` csharp
var userinfo = graphClient.Users.Get( "bill@contoso.com" );
```

### <a name="get-the-objectid-of-a-user-in-the-aad-directory"></a><span data-ttu-id="456d0-184">Obtenir l’ObjectId d’un utilisateur dans le répertoire AAD</span><span class="sxs-lookup"><span data-stu-id="456d0-184">Get the ObjectId of a user in the AAD directory</span></span>

``` csharp
var userinfo = graphClient.Users.Get( "bill@contoso.com" );
Console.WriteLine( userinfo.ObjectId )
```

## <a name="manage-compute-policies"></a><span data-ttu-id="456d0-185">Gérer les stratégies de calcul</span><span class="sxs-lookup"><span data-stu-id="456d0-185">Manage compute policies</span></span>
<span data-ttu-id="456d0-186">L’objet DataLakeAnalyticsAccountManagementClient fournit des méthodes de gestion des stratégies de calcul pour un compte Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="456d0-186">The DataLakeAnalyticsAccountManagementClient object provides methods for managing the compute policies for a Data Lake Analytics account.</span></span>

### <a name="list-compute-policies"></a><span data-ttu-id="456d0-187">Lister les stratégies de calcul</span><span class="sxs-lookup"><span data-stu-id="456d0-187">List compute policies</span></span>
<span data-ttu-id="456d0-188">Le code suivant récupère une liste de stratégies de calcul pour un compte Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="456d0-188">The following code retrieves a list of compute policies for a Data Lake Analytics account.</span></span>

``` csharp
var policies = adlaAccountClient.ComputePolicies.ListByAccount(rg, adla);
foreach (var p in policies)
{
   Console.WriteLine($"Name: {p.Name}\tType: {p.ObjectType}\tMax AUs / job: {p.MaxDegreeOfParallelismPerJob}\tMin priority / job: {p.MinPriorityPerJob}");
}
```

### <a name="create-a-new-compute-policy"></a><span data-ttu-id="456d0-189">Créer une nouvelle stratégie de calcul</span><span class="sxs-lookup"><span data-stu-id="456d0-189">Create a new compute policy</span></span>
<span data-ttu-id="456d0-190">Le code suivant crée une nouvelle stratégie de calcul pour un compte Data Lake Analytics, en définissant les unités Analytics maximales disponibles pour l’utilisateur spécifié sur 50 et la priorité minimale du travail sur 250.</span><span class="sxs-lookup"><span data-stu-id="456d0-190">The following code creates a new compute policy for a Data Lake Analytics account, setting the maximum AUs available to the specified user to 50, and the minimum job priority to 250.</span></span>

``` csharp
var userAadObjectId = "3b097601-4912-4d41-b9d2-78672fc2acde";
var newPolicyParams = new ComputePolicyCreateOrUpdateParameters(userAadObjectId, "User", 50, 250);
adlaAccountClient.ComputePolicies.CreateOrUpdate(rg, adla, "GaryMcDaniel", newPolicyParams);
```

## <a name="next-steps"></a><span data-ttu-id="456d0-191">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="456d0-191">Next steps</span></span>
* [<span data-ttu-id="456d0-192">Vue d'ensemble de Microsoft Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="456d0-192">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="456d0-193">Gestion d’Azure Data Lake Analytics à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="456d0-193">Manage Azure Data Lake Analytics using Azure portal</span></span>](data-lake-analytics-manage-use-portal.md)
* [<span data-ttu-id="456d0-194">Surveiller et résoudre les problèmes des tâches Azure Data Lake Analytics à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="456d0-194">Monitor and troubleshoot Azure Data Lake Analytics jobs using Azure portal</span></span>](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)
