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
# <a name="manage-azure-data-lake-analytics-using-azure-net-sdk"></a><span data-ttu-id="1fd35-103">Gestion d’Azure Data Lake Analytics à l’aide du SDK Azure .NET</span><span class="sxs-lookup"><span data-stu-id="1fd35-103">Manage Azure Data Lake Analytics using Azure .NET SDK</span></span>
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

<span data-ttu-id="1fd35-104">Découvrez comment des comptes toomanage Analytique de LAC de données Azure, des sources de données, des utilisateurs et des travaux à l’aide de hello Azure .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="1fd35-104">Learn how toomanage Azure Data Lake Analytics accounts, data sources, users, and jobs using hello Azure .NET SDK.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="1fd35-105">Composants requis</span><span class="sxs-lookup"><span data-stu-id="1fd35-105">Prerequisites</span></span>

* <span data-ttu-id="1fd35-106">**Visual Studio 2015, Visual Studio 2013 mise à jour 4 ou Visual Studio 2012 avec Visual C++ installé**.</span><span class="sxs-lookup"><span data-stu-id="1fd35-106">**Visual Studio 2015, Visual Studio 2013 update 4, or Visual Studio 2012 with Visual C++ Installed**.</span></span>
* <span data-ttu-id="1fd35-107">**Kit SDK Microsoft Azure pour .NET version 2.5 ou ultérieure**.</span><span class="sxs-lookup"><span data-stu-id="1fd35-107">**Microsoft Azure SDK for .NET version 2.5 or above**.</span></span>  <span data-ttu-id="1fd35-108">Installer à l’aide de hello [le programme d’installation de Web platform](http://www.microsoft.com/web/downloads/platform.aspx).</span><span class="sxs-lookup"><span data-stu-id="1fd35-108">Install it using hello [Web platform installer](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
* <span data-ttu-id="1fd35-109">**Packages NuGet exigés**</span><span class="sxs-lookup"><span data-stu-id="1fd35-109">**Required NuGet Packages**</span></span>

### <a name="install-nuget-packages"></a><span data-ttu-id="1fd35-110">Installer les packages NuGet</span><span class="sxs-lookup"><span data-stu-id="1fd35-110">Install NuGet packages</span></span>

|<span data-ttu-id="1fd35-111">Package</span><span class="sxs-lookup"><span data-stu-id="1fd35-111">Package</span></span>|<span data-ttu-id="1fd35-112">Version</span><span class="sxs-lookup"><span data-stu-id="1fd35-112">Version</span></span>|
|-------|-------|
|[<span data-ttu-id="1fd35-113">Microsoft.Rest.ClientRuntime.Azure.Authentication</span><span class="sxs-lookup"><span data-stu-id="1fd35-113">Microsoft.Rest.ClientRuntime.Azure.Authentication</span></span>](https://www.nuget.org/packages/Microsoft.Rest.ClientRuntime.Azure.Authentication)| <span data-ttu-id="1fd35-114">2.3.1</span><span class="sxs-lookup"><span data-stu-id="1fd35-114">2.3.1</span></span>|
|[<span data-ttu-id="1fd35-115">Microsoft.Azure.Management.DataLake.Analytics</span><span class="sxs-lookup"><span data-stu-id="1fd35-115">Microsoft.Azure.Management.DataLake.Analytics</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Management.DataLake.Analytics)|<span data-ttu-id="1fd35-116">3.0.0</span><span class="sxs-lookup"><span data-stu-id="1fd35-116">3.0.0</span></span>|
|[<span data-ttu-id="1fd35-117">Microsoft.Azure.Management.DataLake.Store</span><span class="sxs-lookup"><span data-stu-id="1fd35-117">Microsoft.Azure.Management.DataLake.Store</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Management.DataLake.Store)|<span data-ttu-id="1fd35-118">2.2.0</span><span class="sxs-lookup"><span data-stu-id="1fd35-118">2.2.0</span></span>|
|[<span data-ttu-id="1fd35-119">Microsoft.Azure.Management.ResourceManager</span><span class="sxs-lookup"><span data-stu-id="1fd35-119">Microsoft.Azure.Management.ResourceManager</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Management.ResourceManager)|<span data-ttu-id="1fd35-120">1.6.0-preview</span><span class="sxs-lookup"><span data-stu-id="1fd35-120">1.6.0-preview</span></span>|
|[<span data-ttu-id="1fd35-121">Microsoft.Azure.Graph.RBAC</span><span class="sxs-lookup"><span data-stu-id="1fd35-121">Microsoft.Azure.Graph.RBAC</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Management.ResourceManager)|<span data-ttu-id="1fd35-122">3.4.0-preview</span><span class="sxs-lookup"><span data-stu-id="1fd35-122">3.4.0-preview</span></span>|

<span data-ttu-id="1fd35-123">Vous pouvez installer ces packages via la ligne de commande hello NuGet avec hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="1fd35-123">You can install these packages via hello NuGet command line with hello following commands:</span></span>

```
Install-Package -Id Microsoft.Rest.ClientRuntime.Azure.Authentication  -Version 2.3.1
Install-Package -Id Microsoft.Azure.Management.DataLake.Analytics  -Version 3.0.0
Install-Package -Id Microsoft.Azure.Management.DataLake.Store  -Version 2.2.0
Install-Package -Id Microsoft.Azure.Management.ResourceManager  -Version 1.6.0-preview
Install-Package -Id Microsoft.Azure.Graph.RBAC -Version 3.4.0-preview
```

## <a name="common-variables"></a><span data-ttu-id="1fd35-124">Variables communes</span><span class="sxs-lookup"><span data-stu-id="1fd35-124">Common variables</span></span>

``` csharp
string subid = "<Subscription ID>"; // Subscription ID (a GUID)
string tenantid = "<Tenant ID>"; // AAD tenant ID or domain. For example, "contoso.onmicrosoft.com"
string rg == "<value>"; // Resource  group name
string clientid = "1950a258-227b-4e31-a9cf-717495945fc2"; // Sample client ID (this will work, but you should pick your own)
```

## <a name="authentication"></a><span data-ttu-id="1fd35-125">Authentification</span><span class="sxs-lookup"><span data-stu-id="1fd35-125">Authentication</span></span>

<span data-ttu-id="1fd35-126">Vous avez plusieurs options d’ouverture de session tooAzure Analytique lac de données.</span><span class="sxs-lookup"><span data-stu-id="1fd35-126">You have multiple options for logging on tooAzure Data Lake Analytics.</span></span> <span data-ttu-id="1fd35-127">Hello extrait de code suivant montre un exemple d’authentification avec l’authentification d’utilisateur interactif avec un menu contextuel.</span><span class="sxs-lookup"><span data-stu-id="1fd35-127">hello following snippet shows an example of authentication with interactive user authentication with a pop-up.</span></span>

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

<span data-ttu-id="1fd35-128">Hello de code source pour **GetCreds_User_Popup** et hello code pour les autres options pour l’authentification sont traitées dans [options d’authentification Data Lake Analytique .NET](https://github.com/Azure-Samples/data-lake-analytics-dotnet-auth-options)</span><span class="sxs-lookup"><span data-stu-id="1fd35-128">hello source code for **GetCreds_User_Popup** and hello code for other options for authentication are covered in [Data Lake Analytics .NET authentication options](https://github.com/Azure-Samples/data-lake-analytics-dotnet-auth-options)</span></span>


## <a name="create-hello-client-management-objects"></a><span data-ttu-id="1fd35-129">Créer des objets de la gestion des clients de hello</span><span class="sxs-lookup"><span data-stu-id="1fd35-129">Create hello client management objects</span></span>

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

## <a name="manage-accounts"></a><span data-ttu-id="1fd35-130">Gérer les comptes</span><span class="sxs-lookup"><span data-stu-id="1fd35-130">Manage accounts</span></span>

### <a name="create-an-azure-resource-group"></a><span data-ttu-id="1fd35-131">Créer un groupe de ressources Azure</span><span class="sxs-lookup"><span data-stu-id="1fd35-131">Create an Azure Resource Group</span></span>

<span data-ttu-id="1fd35-132">Si vous n’avez pas déjà créé un, vous devez disposer d’un groupe de ressources Azure de toocreate vos composants Analytique lac de données.</span><span class="sxs-lookup"><span data-stu-id="1fd35-132">If you haven't already created one, you must have an Azure Resource Group toocreate your Data Lake Analytics components.</span></span> <span data-ttu-id="1fd35-133">Vous avez besoin de vos informations d’identification d’authentification, d’un ID d’abonnement et d’un emplacement.</span><span class="sxs-lookup"><span data-stu-id="1fd35-133">You  need your authentication credentials, subscription ID, and a location.</span></span> <span data-ttu-id="1fd35-134">Hello suivant de code montre comment toocreate un groupe de ressources :</span><span class="sxs-lookup"><span data-stu-id="1fd35-134">hello following code shows how toocreate a resource group:</span></span>

``` csharp
var resourceGroup = new ResourceGroup { Location = location };
resourceManagementClient.ResourceGroups.CreateOrUpdate(groupName, rg);
```
<span data-ttu-id="1fd35-135">Pour plus d’informations, consultez [Groupes de ressources Azure et Data Lake Analytics](#Azure-Resource-Groups-and-Data-Lake-Analytics).</span><span class="sxs-lookup"><span data-stu-id="1fd35-135">For more information, see [Azure Resource Groups and Data Lake Analytics](#Azure-Resource-Groups-and-Data-Lake-Analytics).</span></span>

### <a name="create-a-data-lake-store-account"></a><span data-ttu-id="1fd35-136">Créer un compte Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="1fd35-136">Create a Data Lake Store account</span></span>

<span data-ttu-id="1fd35-137">Le compte ADLA nécessite un compte ADLS.</span><span class="sxs-lookup"><span data-stu-id="1fd35-137">Ever ADLA account requires an ADLS account.</span></span> <span data-ttu-id="1fd35-138">Si vous n’avez pas encore un toouse, vous pouvez créer une avec hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="1fd35-138">If you don't already have one toouse, you can create one with hello following code:</span></span>

``` csharp
var new_adls_params = new DataLakeStoreAccount(location: _location);
adlsAccountClient.Account.Create(rg, adls, new_adls_params);
```

### <a name="create-a-data-lake-analytics-account"></a><span data-ttu-id="1fd35-139">Créer un compte Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="1fd35-139">Create a Data Lake Analytics account</span></span>

<span data-ttu-id="1fd35-140">Hello suivante de code crée un compte ADLS</span><span class="sxs-lookup"><span data-stu-id="1fd35-140">hello following code creates an ADLS account</span></span>

``` csharp
var new_adla_params = new DataLakeAnalyticsAccount()
{
   DefaultDataLakeStoreAccount = adls,
   Location = location
};

adlaClient.Account.Create(rg, adla, new_adla_params);
```

### <a name="list-data-lake-store-accounts"></a><span data-ttu-id="1fd35-141">Lister les comptes Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="1fd35-141">List Data Lake Store accounts</span></span>

``` csharp
var adlsAccounts = adlsAccountClient.Account.List().ToList();
foreach (var adls in adlsAccounts)
{
   Console.WriteLine($"ADLS: {0}", adls.Name);
}
```

### <a name="list-data-lake-analytics-accounts"></a><span data-ttu-id="1fd35-142">Énumérer les comptes Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="1fd35-142">List Data Lake Analytics accounts</span></span>

``` csharp
var adlaAccounts = adlaClient.Account.List().ToList();

for (var adla in AdlaAccounts)
{
   Console.WriteLine($"ADLA: {0}, adla.Name");
}
```

### <a name="checking-if-an-account-exists"></a><span data-ttu-id="1fd35-143">Vérifier si un compte existe</span><span class="sxs-lookup"><span data-stu-id="1fd35-143">Checking if an account exists</span></span>

``` csharp
bool exists = adlaClient.Account.Exists(rg, adla));
```

### <a name="get-information-about-an-account"></a><span data-ttu-id="1fd35-144">Obtenir des informations sur un compte</span><span class="sxs-lookup"><span data-stu-id="1fd35-144">Get information about an account</span></span>

``` csharp
bool exists = adlaClient.Account.Exists(rg, adla));
if (exists)
{
   var adla_accnt = adlaClient.Account.Get(rg, adla);
}
```

### <a name="delete-an-account"></a><span data-ttu-id="1fd35-145">Supprimer un compte</span><span class="sxs-lookup"><span data-stu-id="1fd35-145">Delete an account</span></span>

``` csharp
if (adlaClient.Account.Exists(rg, adla))
{
   adlaClient.Account.Delete(rg, adla);
}
```

### <a name="get-hello-default-data-lake-store-account"></a><span data-ttu-id="1fd35-146">Obtenir le compte de Data Lake Store hello par défaut</span><span class="sxs-lookup"><span data-stu-id="1fd35-146">Get hello default Data Lake Store account</span></span>

<span data-ttu-id="1fd35-147">Chaque compte Data Lake Analytics nécessite un compte Data Lake Store par défaut.</span><span class="sxs-lookup"><span data-stu-id="1fd35-147">Every Data Lake Analytics account requires a default Data Lake Store account.</span></span> <span data-ttu-id="1fd35-148">Utilisez ce compte de magasin de code toodetermine hello par défaut pour un compte Analytique.</span><span class="sxs-lookup"><span data-stu-id="1fd35-148">Use this code toodetermine hello default Store account for an Analytics account.</span></span>

``` csharp
if (adlaClient.Account.Exists(rg, adla))
{
  var adla_accnt = adlaClient.Account.Get(rg, adla);
  string def_adls_account = adla_accnt.DefaultDataLakeStoreAccount;
}
```

## <a name="manage-data-sources"></a><span data-ttu-id="1fd35-149">Gérer les sources de données</span><span class="sxs-lookup"><span data-stu-id="1fd35-149">Manage data sources</span></span>

<span data-ttu-id="1fd35-150">Analytique lac de données prend en charge actuellement les hello les sources de données suivantes :</span><span class="sxs-lookup"><span data-stu-id="1fd35-150">Data Lake Analytics currently supports hello following data sources:</span></span>

* [<span data-ttu-id="1fd35-151">Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="1fd35-151">Azure Data Lake Store</span></span>](../data-lake-store/data-lake-store-overview.md)
* [<span data-ttu-id="1fd35-152">Compte Stockage Azure</span><span class="sxs-lookup"><span data-stu-id="1fd35-152">Azure Storage Account</span></span>](../storage/common/storage-introduction.md)

### <a name="link-tooan-azure-storage-account"></a><span data-ttu-id="1fd35-153">Lien tooan compte de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="1fd35-153">Link tooan Azure Storage account</span></span>

<span data-ttu-id="1fd35-154">Vous pouvez créer des liens tooAzure les comptes de stockage.</span><span class="sxs-lookup"><span data-stu-id="1fd35-154">You can create links tooAzure Storage accounts.</span></span>

``` csharp
string storage_key = "xxxxxxxxxxxxxxxxxxxx";
string storage_account = "mystorageaccount";
var addParams = new AddStorageAccountParameters(storage_key);            
adlaClient.StorageAccounts.Add(rg, adla, storage_account, addParams);
```

### <a name="list-azure-storage-data-sources"></a><span data-ttu-id="1fd35-155">Lister les sources de données de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="1fd35-155">List Azure Storage data sources</span></span>

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

### <a name="list-data-lake-store-data-sources"></a><span data-ttu-id="1fd35-156">Afficher la liste des sources de données Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="1fd35-156">List Data Lake Store data sources</span></span>

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

### <a name="upload-and-download-folders-and-files"></a><span data-ttu-id="1fd35-157">Charger et télécharger des dossiers et des fichiers</span><span class="sxs-lookup"><span data-stu-id="1fd35-157">Upload and download folders and files</span></span>
<span data-ttu-id="1fd35-158">Vous pouvez utiliser tooupload objet de hello Data Lake Store fichier système client Gestion et télécharger des fichiers individuels ou des dossiers à partir de l’ordinateur local de Azure tooyour, à l’aide des méthodes suivantes de hello :</span><span class="sxs-lookup"><span data-stu-id="1fd35-158">You can use hello Data Lake Store file system client management object tooupload and download individual files or folders from Azure tooyour local computer, using hello following methods:</span></span>

- <span data-ttu-id="1fd35-159">UploadFolder</span><span class="sxs-lookup"><span data-stu-id="1fd35-159">UploadFolder</span></span>
- <span data-ttu-id="1fd35-160">UploadFile</span><span class="sxs-lookup"><span data-stu-id="1fd35-160">UploadFile</span></span>
- <span data-ttu-id="1fd35-161">DownloadFolder</span><span class="sxs-lookup"><span data-stu-id="1fd35-161">DownloadFolder</span></span>
- <span data-ttu-id="1fd35-162">DownloadFile</span><span class="sxs-lookup"><span data-stu-id="1fd35-162">DownloadFile</span></span>

<span data-ttu-id="1fd35-163">premier paramètre de Hello pour ces méthodes désigne hello hello compte du magasin Data Lake, suivi par des paramètres pour la source hello et chemin d’accès de destination de hello.</span><span class="sxs-lookup"><span data-stu-id="1fd35-163">hello first parameter for these methods is hello name of hello Data Lake Store Account, followed by parameters for hello source path and hello destination path.</span></span>

<span data-ttu-id="1fd35-164">Bonjour à l’exemple suivant montre comment toodownload un dossier dans hello Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="1fd35-164">hello following example shows how toodownload a folder in hello Data Lake Store.</span></span>

``` csharp
adlsFileSystemClient.FileSystem.DownloadFolder(adls, sourcePath, destinationPath);
```

### <a name="create-a-file-in-a-data-lake-store-account"></a><span data-ttu-id="1fd35-165">Créer un fichier dans un compte Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="1fd35-165">Create a file in a Data Lake Store account</span></span>

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

### <a name="verify-azure-storage-account-paths"></a><span data-ttu-id="1fd35-166">Vérifier les chemins des comptes de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="1fd35-166">Verify Azure Storage account paths</span></span>
<span data-ttu-id="1fd35-167">Hello de code suivant vérifie si un compte de stockage Azure (storageAccntName) existe dans un compte Analytique lac de données (analyticsAccountName), et si un conteneur (containerName) existe dans le compte de stockage Azure hello.</span><span class="sxs-lookup"><span data-stu-id="1fd35-167">hello following code checks if an Azure Storage account (storageAccntName) exists in a Data Lake Analytics account (analyticsAccountName), and if a container (containerName) exists in hello Azure Storage account.</span></span>

``` csharp
string storage_account = "mystorageaccount";
string storage_container = "mycontainer";
bool accountExists = adlaClient.Account.StorageAccountExists(rg, adla, storage_account));
bool containerExists = adlaClient.Account.StorageContainerExists(rg, adla, storage_account, storage_container));
```

## <a name="manage-catalog-and-jobs"></a><span data-ttu-id="1fd35-168">Gérer le catalogue et les travaux</span><span class="sxs-lookup"><span data-stu-id="1fd35-168">Manage catalog and jobs</span></span>
<span data-ttu-id="1fd35-169">objet de DataLakeAnalyticsCatalogManagementClient Hello fournit des méthodes pour la gestion de base de données SQL hello fourni pour chaque compte Analytique de LAC de données Azure.</span><span class="sxs-lookup"><span data-stu-id="1fd35-169">hello DataLakeAnalyticsCatalogManagementClient object provides methods for managing hello SQL database provided for each Azure Data Lake Analytics account.</span></span> <span data-ttu-id="1fd35-170">Hello DataLakeAnalyticsJobManagementClient fournit les méthodes toosubmit et gérer des tâches exécutées sur la base de données de hello avec scripts U-SQL.</span><span class="sxs-lookup"><span data-stu-id="1fd35-170">hello DataLakeAnalyticsJobManagementClient provides methods toosubmit and manage jobs run on hello database with U-SQL scripts.</span></span>

### <a name="list-databases-and-schemas"></a><span data-ttu-id="1fd35-171">Afficher la liste des bases de données et des schémas</span><span class="sxs-lookup"><span data-stu-id="1fd35-171">List databases and schemas</span></span>
<span data-ttu-id="1fd35-172">Entre hello plusieurs choses que vous pouvez répertorier, hello plus courantes sont les bases de données et leur schéma.</span><span class="sxs-lookup"><span data-stu-id="1fd35-172">Among hello several things you can list, hello most common are databases and their schema.</span></span> <span data-ttu-id="1fd35-173">Bonjour de code suivant obtient une collection de bases de données et énumère ensuite le schéma de hello pour chaque base de données.</span><span class="sxs-lookup"><span data-stu-id="1fd35-173">hello following code obtains a collection of databases, and then enumerates hello schema for each database.</span></span>

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

### <a name="list-table-columns"></a><span data-ttu-id="1fd35-174">Afficher la liste des colonnes d’une table</span><span class="sxs-lookup"><span data-stu-id="1fd35-174">List table columns</span></span>
<span data-ttu-id="1fd35-175">Hello de code suivant montre comment tooaccess hello de base de données avec un catalogue de données Lake Analytique gestion client toolist hello des colonnes dans une table spécifiée.</span><span class="sxs-lookup"><span data-stu-id="1fd35-175">hello following code shows how tooaccess hello database with a Data Lake Analytics Catalog management client toolist hello columns in a specified table.</span></span>

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

### <a name="list-failed-jobs"></a><span data-ttu-id="1fd35-176">Afficher la liste des travaux ayant échoué</span><span class="sxs-lookup"><span data-stu-id="1fd35-176">List failed jobs</span></span>
<span data-ttu-id="1fd35-177">Hello de code suivant affiche des informations sur les tâches qui ont échoué.</span><span class="sxs-lookup"><span data-stu-id="1fd35-177">hello following code lists information about jobs that failed.</span></span>

``` csharp
var odq = new ODataQuery<JobInformation> { Filter = "result eq 'Failed'" };
var jobs = adlaJobClient.Job.List(adla, odq);
foreach (var j in jobs)
{
   Console.WriteLine($"{j.Name}\t{j.JobId}\t{j.Type}\t{j.StartTime}\t{j.EndTime}");
}
```

### <a name="list-pipelines"></a><span data-ttu-id="1fd35-178">Lister les pipelines</span><span class="sxs-lookup"><span data-stu-id="1fd35-178">List pipelines</span></span>
<span data-ttu-id="1fd35-179">Hello de code suivant répertorie des informations sur chaque pipeline de travaux soumis toohello compte.</span><span class="sxs-lookup"><span data-stu-id="1fd35-179">hello following code lists information about each pipeline of jobs submitted toohello account.</span></span>

``` csharp
var pipelines = adlaJobClient.Pipeline.List(adla);
foreach (var p in pipelines)
{
   Console.WriteLine($"Pipeline: {p.Name}\t{p.PipelineId}\t{p.LastSubmitTime}");
}
```

### <a name="list-recurrences"></a><span data-ttu-id="1fd35-180">Lister les récurrences</span><span class="sxs-lookup"><span data-stu-id="1fd35-180">List recurrences</span></span>
<span data-ttu-id="1fd35-181">Hello de code suivant répertorie des informations sur chaque occurrence de travaux soumis toohello compte.</span><span class="sxs-lookup"><span data-stu-id="1fd35-181">hello following code lists information about each recurrence of jobs submitted toohello account.</span></span>

``` csharp
var recurrences = adlaJobClient.Recurrence.List(adla);
foreach (var r in recurrences)
{
   Console.WriteLine($"Recurrence: {r.Name}\t{r.RecurrenceId}\t{r.LastSubmitTime}");
}
```

## <a name="common-graph-scenarios"></a><span data-ttu-id="1fd35-182">Scénarios courants de graphe</span><span class="sxs-lookup"><span data-stu-id="1fd35-182">Common graph scenarios</span></span>

### <a name="look-up-user-in-hello-aad-directory"></a><span data-ttu-id="1fd35-183">Rechercher l’utilisateur dans l’annuaire de hello AAD</span><span class="sxs-lookup"><span data-stu-id="1fd35-183">Look up user in hello AAD directory</span></span>

``` csharp
var userinfo = graphClient.Users.Get( "bill@contoso.com" );
```

### <a name="get-hello-objectid-of-a-user-in-hello-aad-directory"></a><span data-ttu-id="1fd35-184">Obtenir hello ObjectId d’un utilisateur dans l’annuaire de hello AAD</span><span class="sxs-lookup"><span data-stu-id="1fd35-184">Get hello ObjectId of a user in hello AAD directory</span></span>

``` csharp
var userinfo = graphClient.Users.Get( "bill@contoso.com" );
Console.WriteLine( userinfo.ObjectId )
```

## <a name="manage-compute-policies"></a><span data-ttu-id="1fd35-185">Gérer les stratégies de calcul</span><span class="sxs-lookup"><span data-stu-id="1fd35-185">Manage compute policies</span></span>
<span data-ttu-id="1fd35-186">objet de DataLakeAnalyticsAccountManagementClient Hello fournit des méthodes pour la gestion hello de calcul des stratégies pour un compte Analytique lac de données.</span><span class="sxs-lookup"><span data-stu-id="1fd35-186">hello DataLakeAnalyticsAccountManagementClient object provides methods for managing hello compute policies for a Data Lake Analytics account.</span></span>

### <a name="list-compute-policies"></a><span data-ttu-id="1fd35-187">Lister les stratégies de calcul</span><span class="sxs-lookup"><span data-stu-id="1fd35-187">List compute policies</span></span>
<span data-ttu-id="1fd35-188">Hello suivant code récupère une liste de stratégies de calcul pour un compte Analytique lac de données.</span><span class="sxs-lookup"><span data-stu-id="1fd35-188">hello following code retrieves a list of compute policies for a Data Lake Analytics account.</span></span>

``` csharp
var policies = adlaAccountClient.ComputePolicies.ListByAccount(rg, adla);
foreach (var p in policies)
{
   Console.WriteLine($"Name: {p.Name}\tType: {p.ObjectType}\tMax AUs / job: {p.MaxDegreeOfParallelismPerJob}\tMin priority / job: {p.MinPriorityPerJob}");
}
```

### <a name="create-a-new-compute-policy"></a><span data-ttu-id="1fd35-189">Créer une nouvelle stratégie de calcul</span><span class="sxs-lookup"><span data-stu-id="1fd35-189">Create a new compute policy</span></span>
<span data-ttu-id="1fd35-190">Hello suivante de code crée une nouvelle stratégie de calcul pour un compte Analytique lac de données, paramètre hello maximale AUs disponible toohello spécifié utilisateur too50 et too250 de priorité hello minimal de tâche.</span><span class="sxs-lookup"><span data-stu-id="1fd35-190">hello following code creates a new compute policy for a Data Lake Analytics account, setting hello maximum AUs available toohello specified user too50, and hello minimum job priority too250.</span></span>

``` csharp
var userAadObjectId = "3b097601-4912-4d41-b9d2-78672fc2acde";
var newPolicyParams = new ComputePolicyCreateOrUpdateParameters(userAadObjectId, "User", 50, 250);
adlaAccountClient.ComputePolicies.CreateOrUpdate(rg, adla, "GaryMcDaniel", newPolicyParams);
```

## <a name="next-steps"></a><span data-ttu-id="1fd35-191">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1fd35-191">Next steps</span></span>
* [<span data-ttu-id="1fd35-192">Vue d'ensemble de Microsoft Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="1fd35-192">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="1fd35-193">Gestion d’Azure Data Lake Analytics à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="1fd35-193">Manage Azure Data Lake Analytics using Azure portal</span></span>](data-lake-analytics-manage-use-portal.md)
* [<span data-ttu-id="1fd35-194">Surveiller et résoudre les problèmes des tâches Azure Data Lake Analytics à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="1fd35-194">Monitor and troubleshoot Azure Data Lake Analytics jobs using Azure portal</span></span>](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)
