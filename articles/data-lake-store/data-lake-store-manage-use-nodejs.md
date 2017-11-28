---
title: "Prendre en main Azure Data Lake Store à l’aide du Kit de développement Logiciel (SDK) Azure pour Node.js | Microsoft Docs"
description: "Découvrez comment utiliser Node.js pour travailler avec les comptes Data Lake Store et le système de fichiers."
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 2fee173c-69ae-4e1d-8773-48618cda9e16
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/06/2017
ms.author: nitinme
ms.openlocfilehash: 8c7a2e6ca061bbfa077592efb73d592906c3d070
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-data-lake-store-using-azure-sdk-for-nodejs"></a><span data-ttu-id="19e4a-103">Prendre en main Azure Data Lake Store à l’aide du Kit de développement Logiciel (SDK) Azure pour Node.js</span><span class="sxs-lookup"><span data-stu-id="19e4a-103">Get started with Azure Data Lake Store using Azure SDK for Node.js</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="19e4a-104">Portail</span><span class="sxs-lookup"><span data-stu-id="19e4a-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="19e4a-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="19e4a-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="19e4a-106">Kit SDK .NET</span><span class="sxs-lookup"><span data-stu-id="19e4a-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="19e4a-107">Kit SDK Java</span><span class="sxs-lookup"><span data-stu-id="19e4a-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="19e4a-108">API REST</span><span class="sxs-lookup"><span data-stu-id="19e4a-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="19e4a-109">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="19e4a-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="19e4a-110">Node.JS</span><span class="sxs-lookup"><span data-stu-id="19e4a-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="19e4a-111">Python</span><span class="sxs-lookup"><span data-stu-id="19e4a-111">Python</span></span>](data-lake-store-get-started-python.md)
>
> 

> [!NOTE]
> <span data-ttu-id="19e4a-112">Pour charger et télécharger de grandes quantités de données (des fichiers volumineux, un grand nombre de fichiers ou les deux), nous vous recommandons d’utiliser le [SDK Python](data-lake-store-get-started-python.md), le [SDK .NET](data-lake-store-get-started-net-sdk.md), [Azure CLI 2.0](data-lake-store-get-started-cli-2.0.md) ou [Azure PowerShell](data-lake-store-get-started-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="19e4a-112">For uploading and downloading large amount of data (large files, a large number of files, or both), we recommend that you use the [Python SDK](data-lake-store-get-started-python.md), the [.NET SDK](data-lake-store-get-started-net-sdk.md), [Azure CLI 2.0](data-lake-store-get-started-cli-2.0.md), or [Azure PowerShell](data-lake-store-get-started-powershell.md).</span></span> <span data-ttu-id="19e4a-113">Ces options offrent de meilleures performances, car elles utilisent plusieurs threads pour paralléliser le déplacement des données.</span><span class="sxs-lookup"><span data-stu-id="19e4a-113">These options have better performance as they use multiple threads to parallelize the data movement.</span></span>
> 
> 

<span data-ttu-id="19e4a-114">Apprenez à utiliser le Kit de développement logiciel (SDK) Azure pour Node.js pour créer un compte Azure Data Lake Store et effectuer des opérations de base comme créer des dossiers, télécharger des fichiers de données, supprimer votre compte, etc. Pour plus d’informations sur Data Lake Store, consultez [Vue d’ensemble de Data Lake Store](data-lake-store-overview.md).</span><span class="sxs-lookup"><span data-stu-id="19e4a-114">Learn how to use the Azure SDK for Node.js to create an Azure Data Lake Store account and perform basic operations such as create folders, upload and download data files, delete your account, etc. For more information about Data Lake Store, see [Overview of Data Lake Store](data-lake-store-overview.md).</span></span> <span data-ttu-id="19e4a-115">Le Kit de développement logiciel (SDK) prend actuellement en charge</span><span class="sxs-lookup"><span data-stu-id="19e4a-115">Currently, the SDK supports</span></span>

* <span data-ttu-id="19e4a-116">**Node.js version 0.10.0 ou supérieure**</span><span class="sxs-lookup"><span data-stu-id="19e4a-116">**Node.js version: 0.10.0 or higher**</span></span>
* <span data-ttu-id="19e4a-117">**Version de l’API REST pour le compte : 2015-10-01-preview**</span><span class="sxs-lookup"><span data-stu-id="19e4a-117">**REST API version for Account: 2015-10-01-preview**</span></span>
* <span data-ttu-id="19e4a-118">**Version de l’API REST pour FileSystem : 2015-10-01-preview**</span><span class="sxs-lookup"><span data-stu-id="19e4a-118">**REST API version for FileSystem: 2015-10-01-preview**</span></span>

## <a name="prerequisites"></a><span data-ttu-id="19e4a-119">Composants requis</span><span class="sxs-lookup"><span data-stu-id="19e4a-119">Prerequisites</span></span>
<span data-ttu-id="19e4a-120">Avant de commencer cet article, vous devez disposer des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="19e4a-120">Before you begin this article, you must have the following:</span></span>

* <span data-ttu-id="19e4a-121">**Un abonnement Azure**.</span><span class="sxs-lookup"><span data-stu-id="19e4a-121">**An Azure subscription**.</span></span> <span data-ttu-id="19e4a-122">Consultez la page [Obtention d’un essai gratuit d’Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="19e4a-122">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="19e4a-123">**Créez une application Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="19e4a-123">**Create an Azure Active Directory Application**.</span></span> <span data-ttu-id="19e4a-124">Vous utilisez l’application Azure AD pour authentifier l’application Data Lake Store auprès d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="19e4a-124">You use the Azure AD application to authenticate the Data Lake Store application with Azure AD.</span></span> <span data-ttu-id="19e4a-125">Il existe différentes approches pour l’authentification auprès d’Azure AD : **authentification de l’utilisateur final** ou **authentification de service à service**.</span><span class="sxs-lookup"><span data-stu-id="19e4a-125">There are different approaches to authenticate with Azure AD, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="19e4a-126">Pour obtenir des instructions et plus d’informations sur l’authentification, consultez [l’authentification de l’utilisateur final](data-lake-store-end-user-authenticate-using-active-directory.md) ou [l’authentification de service à service](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="19e4a-126">For instructions and more information on how to authenticate, see [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md) or [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md).</span></span>

## <a name="how-to-install"></a><span data-ttu-id="19e4a-127">Procédure d’installation</span><span class="sxs-lookup"><span data-stu-id="19e4a-127">How to Install</span></span>
```bash
npm install azure-arm-datalake-store
```

## <a name="authenticate-using-azure-active-directory"></a><span data-ttu-id="19e4a-128">S’authentifier à l’aide d’Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="19e4a-128">Authenticate using Azure Active Directory</span></span>
<span data-ttu-id="19e4a-129">Les extraits de code ci-dessous montrent deux méthodes distinctes d’authentification sur Data Lake Store à l’aide d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="19e4a-129">The snippets below show two separate ways of authenticating with Data Lake Store using Azure AD.</span></span> <span data-ttu-id="19e4a-130">Pour une présentation détaillée des différentes méthodes d’authentification sur Data Lake Store, voir [S’authentifier sur Data Lake Store à l’aide d’Azure Active Directory](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="19e4a-130">For a detailed discussion on various methods to use for authentication with Data Lake Store, see [Authenticate with Data Lake Store using Azure Active Directory](data-lake-store-authenticate-using-active-directory.md).</span></span>

<span data-ttu-id="19e4a-131">L’extrait de code ci-dessous requiert également des entrées telles qu’un nom de domaine Azure AD, un ID de client pour une application Azure AD, etc. Toutes ces informations peuvent être extraites d’une application Azure AD que vous devez créer, dont les détails sont également inclus dans le lien ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="19e4a-131">The snippet below also requires inputs like Azure AD domain name, client ID for an Azure AD app, etc. All these details can be retrieved from an Azure AD application that you must created, the details of which are also included in link above.</span></span>

 ```javascript
 var msrestAzure = require('ms-rest-azure');
 //user authentication
 var credentials = new msRestAzure.UserTokenCredentials('your-client-id', 'your-domain', 'your-username', 'your-password', 'your-redirect-uri');
 //service principal authentication
 var credentials = new msRestAzure.ApplicationTokenCredentials('your-client-id', 'your-domain', 'your-secret');
 ```

## <a name="create-the-data-lake-store-clients"></a><span data-ttu-id="19e4a-132">Créer les clients Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="19e4a-132">Create the Data Lake Store Clients</span></span>
```javascript
var adlsManagement = require("azure-arm-datalake-store");
var acccountClient = new adlsManagement.DataLakeStoreAccountClient(credentials, "your-subscription-id");
var filesystemClient = new adlsManagement.DataLakeStoreFileSystemClient(credentials);
```

## <a name="create-a-data-lake-store-account"></a><span data-ttu-id="19e4a-133">Créer un compte Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="19e4a-133">Create a Data Lake Store Account</span></span>
```javascript
var util = require('util');
var resourceGroupName = 'testrg';
var accountName = 'testadlsacct';
var location = 'eastus2';

// account object to create
var accountToCreate = {
  tags: {
    testtag1: 'testvalue1',
    testtag2: 'testvalue2'
  },
  name: accountName,
  location: location
};

client.account.create(resourceGroupName, accountName, accountToCreate, function (err, result, request, response) {
  if (err) {
    console.log(err);
    /*err has reference to the actual request and response, so you can see what was sent and received on the wire.
      The structure of err looks like this:
      err: {
        code: 'Error Code',
        message: 'Error Message',
        body: 'The response body if any',
        request: reference to a stripped version of http request
        response: reference to a stripped version of the response
      }
    */
  } else {
    console.log('result is: ' + util.inspect(result, {depth: null}));
  }
});
```

## <a name="create-a-file-with-content"></a><span data-ttu-id="19e4a-134">Créez un fichier avec du contenu</span><span class="sxs-lookup"><span data-stu-id="19e4a-134">Create a file with content</span></span>
```javascript
var util = require('util');
var accountName = 'testadlsacct';
var fileToCreate = '/myfolder/myfile.txt';
var options = {
  streamContents: new Buffer('some string content')
}

filesystemClient.fileSystem.listFileStatus(accountName, fileToCreate, options, function (err, result, request, response) {
  if (err) {
    console.log(err);
  } else {
    // no result is returned, only a 201 response for success.
    console.log('response is: ' + util.inspect(response, {depth: null}));
  }
});
```

## <a name="get-a-list-of-files-and-folders"></a><span data-ttu-id="19e4a-135">Obtenir une liste de fichiers et de dossiers</span><span class="sxs-lookup"><span data-stu-id="19e4a-135">Get a list of files and folders</span></span>
```javascript
var util = require('util');
var accountName = 'testadlsacct';
var pathToEnumerate = '/myfolder';
filesystemClient.fileSystem.listFileStatus(accountName, pathToEnumerate, function (err, result, request, response) {
  if (err) {
    console.log(err);
  } else {
    console.log('result is: ' + util.inspect(result, {depth: null}));
  }
});
```

## <a name="see-also"></a><span data-ttu-id="19e4a-136">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="19e4a-136">See also</span></span>
* [<span data-ttu-id="19e4a-137">Kit de développement logiciel (SDK) Microsoft Azure pour Node.js</span><span class="sxs-lookup"><span data-stu-id="19e4a-137">Microsoft Azure SDK for Node.js</span></span>](https://github.com/azure/azure-sdk-for-node)
* [<span data-ttu-id="19e4a-138">Kit de développement logiciel (SDK) Microsoft Azure pour Node.js - Gestion de Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="19e4a-138">Microsoft Azure SDK for Node.js - Data Lake Analytics Management</span></span>](https://www.npmjs.com/package/azure-arm-datalake-analytics)

