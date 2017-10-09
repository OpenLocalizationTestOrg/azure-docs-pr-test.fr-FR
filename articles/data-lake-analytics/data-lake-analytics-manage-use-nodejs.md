---
title: "aaaManage Analytique de LAC de données Azure à l’aide du Kit de développement logiciel Azure pour Node.js | Documents Microsoft"
description: "Découvrez comment les comptes toomanage Analytique lac de données, sources de données, des travaux et des utilisateurs à l’aide du Kit de développement logiciel Azure pour Node.js"
services: data-lake-analytics
documentationcenter: 
author: edmacauley
manager: jhubbard
editor: cgronlun
ms.assetid: 9de1bcf4-b15b-4d0b-9284-8889ecf0c438
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: edmaca
ms.openlocfilehash: 07acd058bf252af2fc98c4cfe87a135e0b79900f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-data-lake-analytics-using-azure-sdk-for-nodejs"></a><span data-ttu-id="2ac21-103">Gestion d’Azure Data Lake Analytics à l’aide du kit de développement logiciel (SDK) Azure pour Node.js</span><span class="sxs-lookup"><span data-stu-id="2ac21-103">Manage Azure Data Lake Analytics using Azure SDK for Node.js</span></span>
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

<span data-ttu-id="2ac21-104">Bonjour Azure SDK pour Node.js utilisable pour la gestion des comptes, les travaux et les catalogues Analytique de LAC de données Azure.</span><span class="sxs-lookup"><span data-stu-id="2ac21-104">hello Azure SDK for Node.js can be used for managing Azure Data Lake Analytics accounts, jobs and catalogs.</span></span> <span data-ttu-id="2ac21-105">rubrique de gestion de toosee à l’aide d’autres outils, cliquez sur l’onglet hello ci-dessus, sélectionnez.</span><span class="sxs-lookup"><span data-stu-id="2ac21-105">toosee management topic using other tools, click hello tab select above.</span></span>

<span data-ttu-id="2ac21-106">Pour le moment, il prend en charge :</span><span class="sxs-lookup"><span data-stu-id="2ac21-106">Right now it supports:</span></span>

* <span data-ttu-id="2ac21-107">**Node.js version 0.10.0 ou supérieure**</span><span class="sxs-lookup"><span data-stu-id="2ac21-107">**Node.js version: 0.10.0 or higher**</span></span>
* <span data-ttu-id="2ac21-108">**Version de l’API REST pour le compte : 2015-10-01-preview**</span><span class="sxs-lookup"><span data-stu-id="2ac21-108">**REST API version for Account: 2015-10-01-preview**</span></span>
* <span data-ttu-id="2ac21-109">**Version de l’API REST pour le catalogue : 2015-10-01-preview**</span><span class="sxs-lookup"><span data-stu-id="2ac21-109">**REST API version for Catalog: 2015-10-01-preview**</span></span>
* <span data-ttu-id="2ac21-110">**Version de l’API REST pour la tâche : 2016-03-20-preview**</span><span class="sxs-lookup"><span data-stu-id="2ac21-110">**REST API version for Job: 2016-03-20-preview**</span></span>

## <a name="features"></a><span data-ttu-id="2ac21-111">Caractéristiques</span><span class="sxs-lookup"><span data-stu-id="2ac21-111">Features</span></span>
* <span data-ttu-id="2ac21-112">Gestion de compte : créer, obtenir, répertorier, mettre à jour et supprimer.</span><span class="sxs-lookup"><span data-stu-id="2ac21-112">Account management: create, get, list, update, and delete.</span></span>
* <span data-ttu-id="2ac21-113">Gestion de travail : envoyer, obtenir, répertorier et annuler.</span><span class="sxs-lookup"><span data-stu-id="2ac21-113">Job management: submit, get, list, and cancel.</span></span>
* <span data-ttu-id="2ac21-114">Gestion de catalogue : obtenir et répertorier.</span><span class="sxs-lookup"><span data-stu-id="2ac21-114">Catalog management: get and list.</span></span>

## <a name="how-tooinstall"></a><span data-ttu-id="2ac21-115">Comment tooInstall</span><span class="sxs-lookup"><span data-stu-id="2ac21-115">How tooInstall</span></span>
```bash
npm install azure-arm-datalake-analytics
```

## <a name="authenticate-using-azure-active-directory"></a><span data-ttu-id="2ac21-116">S’authentifier à l’aide d’Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2ac21-116">Authenticate using Azure Active Directory</span></span>
 ```javascript
 var msrestAzure = require('ms-rest-azure');
 //user authentication
 var credentials = new msRestAzure.UserTokenCredentials('your-client-id', 'your-domain', 'your-username', 'your-password', 'your-redirect-uri');
 //service principal authentication
 var credentials = new msRestAzure.ApplicationTokenCredentials('your-client-id', 'your-domain', 'your-secret');
 ```

## <a name="create-hello-data-lake-analytics-client"></a><span data-ttu-id="2ac21-117">Créer hello Analytique lac de données client</span><span class="sxs-lookup"><span data-stu-id="2ac21-117">Create hello Data Lake Analytics client</span></span>
```javascript
var adlaManagement = require("azure-arm-datalake-analytics");
var acccountClient = new adlaManagement.DataLakeAnalyticsAccountClient(credentials, 'your-subscription-id');
var jobClient = new adlaManagement.DataLakeAnalyticsJobClient(credentials, 'azuredatalakeanalytics.net');
var catalogClient = new adlaManagement.DataLakeAnalyticsCatalogClient(credentials, 'azuredatalakeanalytics.net');
```

## <a name="create-a-data-lake-analytics-account"></a><span data-ttu-id="2ac21-118">Créer un compte Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="2ac21-118">Create a Data Lake Analytics account</span></span>
```javascript
var util = require('util');
var resourceGroupName = 'testrg';
var accountName = 'testadlaacct';
var location = 'eastus2';

// A Data Lake Store account must already have been created toocreate
// a Data Lake Analytics account. See hello Data Lake Store readme for
// information on doing so. For now, we assume one exists already.
var datalakeStoreAccountName = 'existingadlsaccount';

// account object toocreate
var accountToCreate = {
  tags: {
    testtag1: 'testvalue1',
    testtag2: 'testvalue2'
  },
  name: accountName,
  location: location,
  properties: {
    defaultDataLakeStoreAccount: datalakeStoreAccountName,
    dataLakeStoreAccounts: [
      {
        name: datalakeStoreAccountName
      }
    ]
  }
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

## <a name="get-a-list-of-jobs"></a><span data-ttu-id="2ac21-119">Obtenir une liste des tâches</span><span class="sxs-lookup"><span data-stu-id="2ac21-119">Get a list of jobs</span></span>
```javascript
var util = require('util');
var accountName = 'testadlaacct';
jobClient.job.list(accountName, function (err, result, request, response) {
  if (err) {
    console.log(err);
  } else {
    console.log('result is: ' + util.inspect(result, {depth: null}));
  }
});
```

## <a name="get-a-list-of-databases-in-hello-data-lake-analytics-catalog"></a><span data-ttu-id="2ac21-120">Obtenir la liste des bases de données dans hello Data Lake Analytique Catalog</span><span class="sxs-lookup"><span data-stu-id="2ac21-120">Get a list of databases in hello Data Lake Analytics Catalog</span></span>
```javascript
var util = require('util');
var accountName = 'testadlaacct';
catalogClient.catalog.listDatabases(accountName, function (err, result, request, response) {
  if (err) {
    console.log(err);
  } else {
    console.log('result is: ' + util.inspect(result, {depth: null}));
  }
});
```

## <a name="see-also"></a><span data-ttu-id="2ac21-121">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="2ac21-121">See also</span></span>
* [<span data-ttu-id="2ac21-122">Kit de développement logiciel (SDK) Microsoft Azure pour Node.js</span><span class="sxs-lookup"><span data-stu-id="2ac21-122">Microsoft Azure SDK for Node.js</span></span>](https://github.com/azure/azure-sdk-for-node)
* [<span data-ttu-id="2ac21-123">Kit de développement logiciel (SDK) Microsoft Azure pour Node.js - Gestion du Magasin Data Lake</span><span class="sxs-lookup"><span data-stu-id="2ac21-123">Microsoft Azure SDK for Node.js - Data Lake Store Management</span></span>](https://github.com/Azure/azure-sdk-for-node/tree/autorest/lib/services/dataLake.Store)

