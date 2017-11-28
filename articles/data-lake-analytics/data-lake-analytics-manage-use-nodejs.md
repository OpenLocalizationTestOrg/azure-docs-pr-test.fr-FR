---
title: "Gestion d’Azure Data Lake Analytics à l’aide du kit de développement logiciel (SDK) Azure pour Node.js | Microsoft Docs"
description: "Apprenez à gérer des comptes Data Lake Analytics, des sources de données, des utilisateurs et des tâches à l’aide du kit de développement logiciel Azure pour Node.js"
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
ms.openlocfilehash: 769cf9b09eecd204c8b5b944065dad57a6d73231
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-azure-data-lake-analytics-using-azure-sdk-for-nodejs"></a><span data-ttu-id="9398b-103">Gestion d’Azure Data Lake Analytics à l’aide du kit de développement logiciel (SDK) Azure pour Node.js</span><span class="sxs-lookup"><span data-stu-id="9398b-103">Manage Azure Data Lake Analytics using Azure SDK for Node.js</span></span>
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

<span data-ttu-id="9398b-104">Le kit de développement logiciel (SDK) Azure pour Node.js peut être utilisé pour gérer les comptes Azure Data Lake Analytics, les tâches et les catalogues.</span><span class="sxs-lookup"><span data-stu-id="9398b-104">The Azure SDK for Node.js can be used for managing Azure Data Lake Analytics accounts, jobs and catalogs.</span></span> <span data-ttu-id="9398b-105">Pour afficher la rubrique de gestion à l’aide d’autres outils, cliquez sur l’onglet de sélection ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="9398b-105">To see management topic using other tools, click the tab select above.</span></span>

<span data-ttu-id="9398b-106">Pour le moment, il prend en charge :</span><span class="sxs-lookup"><span data-stu-id="9398b-106">Right now it supports:</span></span>

* <span data-ttu-id="9398b-107">**Node.js version 0.10.0 ou supérieure**</span><span class="sxs-lookup"><span data-stu-id="9398b-107">**Node.js version: 0.10.0 or higher**</span></span>
* <span data-ttu-id="9398b-108">**Version de l’API REST pour le compte : 2015-10-01-preview**</span><span class="sxs-lookup"><span data-stu-id="9398b-108">**REST API version for Account: 2015-10-01-preview**</span></span>
* <span data-ttu-id="9398b-109">**Version de l’API REST pour le catalogue : 2015-10-01-preview**</span><span class="sxs-lookup"><span data-stu-id="9398b-109">**REST API version for Catalog: 2015-10-01-preview**</span></span>
* <span data-ttu-id="9398b-110">**Version de l’API REST pour la tâche : 2016-03-20-preview**</span><span class="sxs-lookup"><span data-stu-id="9398b-110">**REST API version for Job: 2016-03-20-preview**</span></span>

## <a name="features"></a><span data-ttu-id="9398b-111">Caractéristiques</span><span class="sxs-lookup"><span data-stu-id="9398b-111">Features</span></span>
* <span data-ttu-id="9398b-112">Gestion de compte : créer, obtenir, répertorier, mettre à jour et supprimer.</span><span class="sxs-lookup"><span data-stu-id="9398b-112">Account management: create, get, list, update, and delete.</span></span>
* <span data-ttu-id="9398b-113">Gestion de travail : envoyer, obtenir, répertorier et annuler.</span><span class="sxs-lookup"><span data-stu-id="9398b-113">Job management: submit, get, list, and cancel.</span></span>
* <span data-ttu-id="9398b-114">Gestion de catalogue : obtenir et répertorier.</span><span class="sxs-lookup"><span data-stu-id="9398b-114">Catalog management: get and list.</span></span>

## <a name="how-to-install"></a><span data-ttu-id="9398b-115">Procédure d’installation</span><span class="sxs-lookup"><span data-stu-id="9398b-115">How to Install</span></span>
```bash
npm install azure-arm-datalake-analytics
```

## <a name="authenticate-using-azure-active-directory"></a><span data-ttu-id="9398b-116">S’authentifier à l’aide d’Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9398b-116">Authenticate using Azure Active Directory</span></span>
 ```javascript
 var msrestAzure = require('ms-rest-azure');
 //user authentication
 var credentials = new msRestAzure.UserTokenCredentials('your-client-id', 'your-domain', 'your-username', 'your-password', 'your-redirect-uri');
 //service principal authentication
 var credentials = new msRestAzure.ApplicationTokenCredentials('your-client-id', 'your-domain', 'your-secret');
 ```

## <a name="create-the-data-lake-analytics-client"></a><span data-ttu-id="9398b-117">Créer le client Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="9398b-117">Create the Data Lake Analytics client</span></span>
```javascript
var adlaManagement = require("azure-arm-datalake-analytics");
var acccountClient = new adlaManagement.DataLakeAnalyticsAccountClient(credentials, 'your-subscription-id');
var jobClient = new adlaManagement.DataLakeAnalyticsJobClient(credentials, 'azuredatalakeanalytics.net');
var catalogClient = new adlaManagement.DataLakeAnalyticsCatalogClient(credentials, 'azuredatalakeanalytics.net');
```

## <a name="create-a-data-lake-analytics-account"></a><span data-ttu-id="9398b-118">Créer un compte Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="9398b-118">Create a Data Lake Analytics account</span></span>
```javascript
var util = require('util');
var resourceGroupName = 'testrg';
var accountName = 'testadlaacct';
var location = 'eastus2';

// A Data Lake Store account must already have been created to create
// a Data Lake Analytics account. See the Data Lake Store readme for
// information on doing so. For now, we assume one exists already.
var datalakeStoreAccountName = 'existingadlsaccount';

// account object to create
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

## <a name="get-a-list-of-jobs"></a><span data-ttu-id="9398b-119">Obtenir une liste des tâches</span><span class="sxs-lookup"><span data-stu-id="9398b-119">Get a list of jobs</span></span>
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

## <a name="get-a-list-of-databases-in-the-data-lake-analytics-catalog"></a><span data-ttu-id="9398b-120">Obtenir une liste des bases de données dans le catalogue Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="9398b-120">Get a list of databases in the Data Lake Analytics Catalog</span></span>
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

## <a name="see-also"></a><span data-ttu-id="9398b-121">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="9398b-121">See also</span></span>
* [<span data-ttu-id="9398b-122">Kit de développement logiciel (SDK) Microsoft Azure pour Node.js</span><span class="sxs-lookup"><span data-stu-id="9398b-122">Microsoft Azure SDK for Node.js</span></span>](https://github.com/azure/azure-sdk-for-node)
* [<span data-ttu-id="9398b-123">Kit de développement logiciel (SDK) Microsoft Azure pour Node.js - Gestion du Magasin Data Lake</span><span class="sxs-lookup"><span data-stu-id="9398b-123">Microsoft Azure SDK for Node.js - Data Lake Store Management</span></span>](https://github.com/Azure/azure-sdk-for-node/tree/autorest/lib/services/dataLake.Store)

