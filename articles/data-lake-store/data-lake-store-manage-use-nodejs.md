---
title: "aaaGet main d’Azure Data Lake Store à l’aide du Kit de développement logiciel Azure pour Node.js | Documents Microsoft"
description: "Découvrez comment toowork de Node.js toouse avec des comptes Data Lake Store et hello système de fichiers."
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
ms.openlocfilehash: ce36a2e0de4e091a4e85ed784a3381415ef6f9e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-azure-sdk-for-nodejs"></a><span data-ttu-id="d9dab-103">Prendre en main Azure Data Lake Store à l’aide du Kit de développement Logiciel (SDK) Azure pour Node.js</span><span class="sxs-lookup"><span data-stu-id="d9dab-103">Get started with Azure Data Lake Store using Azure SDK for Node.js</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d9dab-104">Portail</span><span class="sxs-lookup"><span data-stu-id="d9dab-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="d9dab-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d9dab-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="d9dab-106">Kit SDK .NET</span><span class="sxs-lookup"><span data-stu-id="d9dab-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="d9dab-107">Kit SDK Java</span><span class="sxs-lookup"><span data-stu-id="d9dab-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="d9dab-108">API REST</span><span class="sxs-lookup"><span data-stu-id="d9dab-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="d9dab-109">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="d9dab-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="d9dab-110">Node.JS</span><span class="sxs-lookup"><span data-stu-id="d9dab-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="d9dab-111">Python</span><span class="sxs-lookup"><span data-stu-id="d9dab-111">Python</span></span>](data-lake-store-get-started-python.md)
>
> 

> [!NOTE]
> <span data-ttu-id="d9dab-112">Pour le téléchargement des grande quantité de données (fichiers volumineux, un grand nombre de fichiers ou les deux), nous vous recommandons d’utiliser hello [Python SDK](data-lake-store-get-started-python.md), hello [.NET SDK](data-lake-store-get-started-net-sdk.md), [Azure CLI 2.0](data-lake-store-get-started-cli-2.0.md), ou [Azure PowerShell](data-lake-store-get-started-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="d9dab-112">For uploading and downloading large amount of data (large files, a large number of files, or both), we recommend that you use hello [Python SDK](data-lake-store-get-started-python.md), hello [.NET SDK](data-lake-store-get-started-net-sdk.md), [Azure CLI 2.0](data-lake-store-get-started-cli-2.0.md), or [Azure PowerShell](data-lake-store-get-started-powershell.md).</span></span> <span data-ttu-id="d9dab-113">Ces options offrent de meilleures performances qu’ils utilisent plusieurs threads tooparallelize hello le déplacement des données.</span><span class="sxs-lookup"><span data-stu-id="d9dab-113">These options have better performance as they use multiple threads tooparallelize hello data movement.</span></span>
> 
> 

<span data-ttu-id="d9dab-114">Découvrez comment toouse hello Azure SDK pour Node.js toocreate, un compte Azure Data Lake Store et effectuer des opérations de base telles que la création de dossiers, téléchargent et téléchargement les fichiers de données, supprimez votre compte, un etc.. Pour plus d’informations sur Data Lake Store, consultez [Vue d’ensemble de Data Lake Store](data-lake-store-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d9dab-114">Learn how toouse hello Azure SDK for Node.js toocreate an Azure Data Lake Store account and perform basic operations such as create folders, upload and download data files, delete your account, etc. For more information about Data Lake Store, see [Overview of Data Lake Store](data-lake-store-overview.md).</span></span> <span data-ttu-id="d9dab-115">Actuellement, hello SDK prend en charge</span><span class="sxs-lookup"><span data-stu-id="d9dab-115">Currently, hello SDK supports</span></span>

* <span data-ttu-id="d9dab-116">**Node.js version 0.10.0 ou supérieure**</span><span class="sxs-lookup"><span data-stu-id="d9dab-116">**Node.js version: 0.10.0 or higher**</span></span>
* <span data-ttu-id="d9dab-117">**Version de l’API REST pour le compte : 2015-10-01-preview**</span><span class="sxs-lookup"><span data-stu-id="d9dab-117">**REST API version for Account: 2015-10-01-preview**</span></span>
* <span data-ttu-id="d9dab-118">**Version de l’API REST pour FileSystem : 2015-10-01-preview**</span><span class="sxs-lookup"><span data-stu-id="d9dab-118">**REST API version for FileSystem: 2015-10-01-preview**</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d9dab-119">Composants requis</span><span class="sxs-lookup"><span data-stu-id="d9dab-119">Prerequisites</span></span>
<span data-ttu-id="d9dab-120">Avant de commencer cet article, vous devez disposer de hello :</span><span class="sxs-lookup"><span data-stu-id="d9dab-120">Before you begin this article, you must have hello following:</span></span>

* <span data-ttu-id="d9dab-121">**Un abonnement Azure**.</span><span class="sxs-lookup"><span data-stu-id="d9dab-121">**An Azure subscription**.</span></span> <span data-ttu-id="d9dab-122">Consultez la page [Obtention d’un essai gratuit d’Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d9dab-122">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="d9dab-123">**Créez une application Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d9dab-123">**Create an Azure Active Directory Application**.</span></span> <span data-ttu-id="d9dab-124">Vous utilisez hello Azure AD tooauthenticate hello Data Lake Store une application avec Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d9dab-124">You use hello Azure AD application tooauthenticate hello Data Lake Store application with Azure AD.</span></span> <span data-ttu-id="d9dab-125">Il existe tooauthenticate différentes approches avec Azure AD, qui sont **l’authentification de l’utilisateur final** ou **l’authentification de service**.</span><span class="sxs-lookup"><span data-stu-id="d9dab-125">There are different approaches tooauthenticate with Azure AD, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="d9dab-126">Pour plus d’informations sur la façon d’et tooauthenticate, consultez [l’authentification de l’utilisateur final](data-lake-store-end-user-authenticate-using-active-directory.md) ou [l’authentification de service](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="d9dab-126">For instructions and more information on how tooauthenticate, see [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md) or [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md).</span></span>

## <a name="how-tooinstall"></a><span data-ttu-id="d9dab-127">Comment tooInstall</span><span class="sxs-lookup"><span data-stu-id="d9dab-127">How tooInstall</span></span>
```bash
npm install azure-arm-datalake-store
```

## <a name="authenticate-using-azure-active-directory"></a><span data-ttu-id="d9dab-128">S’authentifier à l’aide d’Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d9dab-128">Authenticate using Azure Active Directory</span></span>
<span data-ttu-id="d9dab-129">extraits de code Hello ci-dessous montrent deux méthodes distinctes d’authentification avec Data Lake Store à l’aide d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d9dab-129">hello snippets below show two separate ways of authenticating with Data Lake Store using Azure AD.</span></span> <span data-ttu-id="d9dab-130">Pour plus d’informations sur les différentes méthodes toouse, pour l’authentification avec Data Lake Store, consultez [authentifier avec Data Lake Store à l’aide d’Azure Active Directory](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="d9dab-130">For a detailed discussion on various methods toouse for authentication with Data Lake Store, see [Authenticate with Data Lake Store using Azure Active Directory](data-lake-store-authenticate-using-active-directory.md).</span></span>

<span data-ttu-id="d9dab-131">extrait de code Hello ci-dessous requiert également des entrées comme nom de domaine Azure AD, ID de client pour une application Azure AD, un etc.. Tous ces détails peuvent être récupérés à partir d’une application Azure AD que vous devez créée, hello dont les coordonnées sont également incluses dans le lien ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="d9dab-131">hello snippet below also requires inputs like Azure AD domain name, client ID for an Azure AD app, etc. All these details can be retrieved from an Azure AD application that you must created, hello details of which are also included in link above.</span></span>

 ```javascript
 var msrestAzure = require('ms-rest-azure');
 //user authentication
 var credentials = new msRestAzure.UserTokenCredentials('your-client-id', 'your-domain', 'your-username', 'your-password', 'your-redirect-uri');
 //service principal authentication
 var credentials = new msRestAzure.ApplicationTokenCredentials('your-client-id', 'your-domain', 'your-secret');
 ```

## <a name="create-hello-data-lake-store-clients"></a><span data-ttu-id="d9dab-132">Créer des Clients de magasin de LAC de données hello</span><span class="sxs-lookup"><span data-stu-id="d9dab-132">Create hello Data Lake Store Clients</span></span>
```javascript
var adlsManagement = require("azure-arm-datalake-store");
var acccountClient = new adlsManagement.DataLakeStoreAccountClient(credentials, "your-subscription-id");
var filesystemClient = new adlsManagement.DataLakeStoreFileSystemClient(credentials);
```

## <a name="create-a-data-lake-store-account"></a><span data-ttu-id="d9dab-133">Créer un compte Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="d9dab-133">Create a Data Lake Store Account</span></span>
```javascript
var util = require('util');
var resourceGroupName = 'testrg';
var accountName = 'testadlsacct';
var location = 'eastus2';

// account object toocreate
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
    /*err has reference toohello actual request and response, so you can see what was sent and received on hello wire.
      hello structure of err looks like this:
      err: {
        code: 'Error Code',
        message: 'Error Message',
        body: 'hello response body if any',
        request: reference tooa stripped version of http request
        response: reference tooa stripped version of hello response
      }
    */
  } else {
    console.log('result is: ' + util.inspect(result, {depth: null}));
  }
});
```

## <a name="create-a-file-with-content"></a><span data-ttu-id="d9dab-134">Créez un fichier avec du contenu</span><span class="sxs-lookup"><span data-stu-id="d9dab-134">Create a file with content</span></span>
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

## <a name="get-a-list-of-files-and-folders"></a><span data-ttu-id="d9dab-135">Obtenir une liste de fichiers et de dossiers</span><span class="sxs-lookup"><span data-stu-id="d9dab-135">Get a list of files and folders</span></span>
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

## <a name="see-also"></a><span data-ttu-id="d9dab-136">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="d9dab-136">See also</span></span>
* [<span data-ttu-id="d9dab-137">Kit de développement logiciel (SDK) Microsoft Azure pour Node.js</span><span class="sxs-lookup"><span data-stu-id="d9dab-137">Microsoft Azure SDK for Node.js</span></span>](https://github.com/azure/azure-sdk-for-node)
* [<span data-ttu-id="d9dab-138">Kit de développement logiciel (SDK) Microsoft Azure pour Node.js - Gestion de Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="d9dab-138">Microsoft Azure SDK for Node.js - Data Lake Analytics Management</span></span>](https://www.npmjs.com/package/azure-arm-datalake-analytics)

