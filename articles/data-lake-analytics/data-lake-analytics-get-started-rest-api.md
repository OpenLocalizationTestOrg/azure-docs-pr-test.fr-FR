---
title: "Prise en main d’Azure Data Lake Analytics à l’aide d’API REST| Microsoft Docs"
description: "Utiliser les API REST de WebHDFS pour effectuer des opérations sur Data Lake Analytics"
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.assetid: 5e133d92-baaa-44c9-890c-ab2d85c91122
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 02/03/2017
ms.author: jgao
ms.openlocfilehash: 332d7af2539eea8890745005104ac5b0921c2b7f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-rest-apis"></a><span data-ttu-id="15589-103">Prise en main d’Azure Data Lake Analytics à l’aide d’API REST</span><span class="sxs-lookup"><span data-stu-id="15589-103">Get started with Azure Data Lake Analytics using REST APIs</span></span>
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

<span data-ttu-id="15589-104">Découvrez comment utiliser les API REST WebHDFS et les API REST Data Lake Analytique pour gérer les comptes, les travaux et le catalogue Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="15589-104">Learn how to use WebHDFS REST APIs and Data Lake Analytics REST APIs to manage Data Lake Analytics accounts, jobs, and catalog.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="15589-105">Composants requis</span><span class="sxs-lookup"><span data-stu-id="15589-105">Prerequisites</span></span>
* <span data-ttu-id="15589-106">**Un abonnement Azure**.</span><span class="sxs-lookup"><span data-stu-id="15589-106">**An Azure subscription**.</span></span> <span data-ttu-id="15589-107">Consultez la page [Obtention d’un essai gratuit d’Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="15589-107">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="15589-108">**Créez une application Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="15589-108">**Create an Azure Active Directory Application**.</span></span> <span data-ttu-id="15589-109">Vous utilisez l’application Azure AD pour authentifier l’application Data Lake Analytics auprès d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="15589-109">You use the Azure AD application to authenticate the Data Lake Analytics application with Azure AD.</span></span> <span data-ttu-id="15589-110">Il existe différentes approches pour l’authentification auprès d’Azure AD : **authentification de l’utilisateur final** ou **authentification de service à service**.</span><span class="sxs-lookup"><span data-stu-id="15589-110">There are different approaches to authenticate with Azure AD, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="15589-111">Pour plus d’informations sur l’authentification et la procédure associée, consultez [Authenticate with Data Lake Store using Azure Active Directory](../data-lake-store/data-lake-store-authenticate-using-active-directory.md)(Authentification auprès de Data Lake Analytics à l’aide d’Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="15589-111">For instructions and more information on how to authenticate, see [Authenticate with Data Lake Analytics using Azure Active Directory](../data-lake-store/data-lake-store-authenticate-using-active-directory.md).</span></span>
* <span data-ttu-id="15589-112">[cURL](http://curl.haxx.se/).</span><span class="sxs-lookup"><span data-stu-id="15589-112">[cURL](http://curl.haxx.se/).</span></span> <span data-ttu-id="15589-113">Cet article utilise cURL pour montrer comment effectuer des appels d’API REST sur un compte Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="15589-113">This article uses cURL to demonstrate how to make REST API calls against a Data Lake Analytics account.</span></span>

## <a name="authenticate-with-azure-active-directory"></a><span data-ttu-id="15589-114">S’authentifier à l’aide d’Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="15589-114">Authenticate with Azure Active Directory</span></span>
<span data-ttu-id="15589-115">Il existe deux méthodes d’authentification avec Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="15589-115">There are two methods for authenticating with Azure Active Directory.</span></span>

### <a name="end-user-authentication-interactive"></a><span data-ttu-id="15589-116">Authentification de l’utilisateur final (interactive)</span><span class="sxs-lookup"><span data-stu-id="15589-116">End-user authentication (interactive)</span></span>
<span data-ttu-id="15589-117">Avec cette méthode, l’application invite l’utilisateur à se connecter. Toutes les opérations sont effectuées dans le contexte de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="15589-117">Using this method, application prompts the user to log in and all the operations are performed in the context of the user.</span></span> 

<span data-ttu-id="15589-118">Pour l’authentification interactive, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="15589-118">Follow these steps for interactive authentication:</span></span>

1. <span data-ttu-id="15589-119">Dans votre application, redirigez l’utilisateur vers l’URL suivante :</span><span class="sxs-lookup"><span data-stu-id="15589-119">Through your application, redirect the user to the following URL:</span></span>
   
        https://login.microsoftonline.com/<TENANT-ID>/oauth2/authorize?client_id=<CLIENT-ID>&response_type=code&redirect_uri=<REDIRECT-URI>
   
   > [!NOTE]
   > <span data-ttu-id="15589-120">L’URI \<REDIRECT-URI> doit être codée pour être utilisée dans une URL.</span><span class="sxs-lookup"><span data-stu-id="15589-120">\<REDIRECT-URI> needs to be encoded for use in a URL.</span></span> <span data-ttu-id="15589-121">Par conséquent, pour https://localhost, utilisez `https%3A%2F%2Flocalhost`)</span><span class="sxs-lookup"><span data-stu-id="15589-121">So, for https://localhost, use `https%3A%2F%2Flocalhost`)</span></span>
   > 
   > 
   
    <span data-ttu-id="15589-122">Pour les besoins de ce didacticiel, vous pouvez remplacer les valeurs d’espace réservé de l’URL ci-dessus et la coller dans la barre d’adresse d’un navigateur web.</span><span class="sxs-lookup"><span data-stu-id="15589-122">For the purpose of this tutorial, you can replace the placeholder values in the URL above and paste it in a web browser's address bar.</span></span> <span data-ttu-id="15589-123">Vous serez redirigé pour vous authentifier à l’aide de vos informations de connexion Azure.</span><span class="sxs-lookup"><span data-stu-id="15589-123">You will be redirected to authenticate using your Azure login.</span></span> <span data-ttu-id="15589-124">Lorsque vous êtes connecté, la réponse s’affiche dans la barre d’adresse du navigateur.</span><span class="sxs-lookup"><span data-stu-id="15589-124">Once you succesfully log in, the response is displayed in the browser's address bar.</span></span> <span data-ttu-id="15589-125">La réponse présente le format suivant :</span><span class="sxs-lookup"><span data-stu-id="15589-125">The response will be in the following format:</span></span>
   
        http://localhost/?code=<AUTHORIZATION-CODE>&session_state=<GUID>
2. <span data-ttu-id="15589-126">Capturez le code d’autorisation de la réponse.</span><span class="sxs-lookup"><span data-stu-id="15589-126">Capture the authorization code from the response.</span></span> <span data-ttu-id="15589-127">Pour ce didacticiel, vous pouvez copier le code d’autorisation de la barre d’adresse du navigateur web et le transmettre dans la demande POST au point de terminaison de jeton, comme indiqué ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="15589-127">For this tutorial, you can copy the authorization code from the address bar of the web browser and pass it in the POST request to the token endpoint, as shown below:</span></span>
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token \
        -F redirect_uri=<REDIRECT-URI> \
        -F grant_type=authorization_code \
        -F resource=https://management.core.windows.net/ \
        -F client_id=<CLIENT-ID> \
        -F code=<AUTHORIZATION-CODE>
   
   > [!NOTE]
   > <span data-ttu-id="15589-128">Dans ce cas, il n’est pas nécessaire de coder l’URI \<REDIRECT-URI>.</span><span class="sxs-lookup"><span data-stu-id="15589-128">In this case, the \<REDIRECT-URI> need not be encoded.</span></span>
   > 
   > 
3. <span data-ttu-id="15589-129">La réponse est un objet JSON contenant un jeton d’accès (par exemple, `"access_token": "<ACCESS_TOKEN>"`) et un jeton d’actualisation (par exemple, `"refresh_token": "<REFRESH_TOKEN>"`).</span><span class="sxs-lookup"><span data-stu-id="15589-129">The response is a JSON object that contains an access token (e.g., `"access_token": "<ACCESS_TOKEN>"`) and a refresh token (e.g., `"refresh_token": "<REFRESH_TOKEN>"`).</span></span> <span data-ttu-id="15589-130">Votre application utilise le jeton d’accès pour accéder à Azure Data Lake Store et le jeton d’actualisation pour obtenir un autre jeton d’accès lorsque l’un d’eux expire.</span><span class="sxs-lookup"><span data-stu-id="15589-130">Your application uses the access token when accessing Azure Data Lake Store and the refresh token to get another access token when an access token expires.</span></span>
   
        {"token_type":"Bearer","scope":"user_impersonation","expires_in":"3599","expires_on":"1461865782","not_before":    "1461861882","resource":"https://management.core.windows.net/","access_token":"<REDACTED>","refresh_token":"<REDACTED>","id_token":"<REDACTED>"}
4. <span data-ttu-id="15589-131">Lorsque le jeton d’accès arrive à expiration, vous pouvez demander un nouveau jeton d’accès à l’aide du jeton d’actualisation, comme indiqué ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="15589-131">When the access token expires, you can request a new access token using the refresh token, as shown below:</span></span>
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
             -F grant_type=refresh_token \
             -F resource=https://management.core.windows.net/ \
             -F client_id=<CLIENT-ID> \
             -F refresh_token=<REFRESH-TOKEN>

<span data-ttu-id="15589-132">Pour plus d’informations sur l’authentification utilisateur interactive, consultez [Flux d’octroi d’un code d’autorisation](https://msdn.microsoft.com/library/azure/dn645542.aspx).</span><span class="sxs-lookup"><span data-stu-id="15589-132">For more information on interactive user authentication, see [Authorization code grant flow](https://msdn.microsoft.com/library/azure/dn645542.aspx).</span></span>

### <a name="service-to-service-authentication-non-interactive"></a><span data-ttu-id="15589-133">Authentification de service à service (non interactive)</span><span class="sxs-lookup"><span data-stu-id="15589-133">Service-to-service authentication (non-interactive)</span></span>
<span data-ttu-id="15589-134">Avec cette méthode, l’application fournit ses propres informations d’identification pour effectuer les opérations.</span><span class="sxs-lookup"><span data-stu-id="15589-134">Using this method, application provides its own credentials to perform the operations.</span></span> <span data-ttu-id="15589-135">Avec cette méthode, vous devez émettre une demande POST, comme celle illustrée ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="15589-135">For this, you must issue a POST request like the one shown below:</span></span> 

    curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
      -F grant_type=client_credentials \
      -F resource=https://management.core.windows.net/ \
      -F client_id=<CLIENT-ID> \
      -F client_secret=<AUTH-KEY>

<span data-ttu-id="15589-136">La sortie de cette demande inclut un jeton d’autorisation (indiqué par `access-token` dans la sortie ci-dessous) que vous allez ensuite passer avec vos appels d’API REST.</span><span class="sxs-lookup"><span data-stu-id="15589-136">The output of this request will include an authorization token (denoted by `access-token` in the output below) that you will subsequently pass with your REST API calls.</span></span> <span data-ttu-id="15589-137">Enregistrez ce jeton d’authentification dans un fichier texte, car vous en aurez besoin plus loin dans cet article.</span><span class="sxs-lookup"><span data-stu-id="15589-137">Save this authentication token in a text file; you will need this later in this article.</span></span>

    {"token_type":"Bearer","expires_in":"3599","expires_on":"1458245447","not_before":"1458241547","resource":"https://management.core.windows.net/","access_token":"<REDACTED>"}

<span data-ttu-id="15589-138">Cet article utilise la méthode **non interactive** .</span><span class="sxs-lookup"><span data-stu-id="15589-138">This article uses the **non-interactive** approach.</span></span> <span data-ttu-id="15589-139">Pour plus d’informations sur l’authentification non interactive (appels de service à service), consultez [Appels de service à service à l’aide d’informations d’identification](https://msdn.microsoft.com/library/azure/dn645543.aspx).</span><span class="sxs-lookup"><span data-stu-id="15589-139">For more information on non-interactive (service-to-service calls), see [Service to service calls using credentials](https://msdn.microsoft.com/library/azure/dn645543.aspx).</span></span>

## <a name="create-a-data-lake-analytics-account"></a><span data-ttu-id="15589-140">Créer un compte Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="15589-140">Create a Data Lake Analytics account</span></span>
<span data-ttu-id="15589-141">Vous devez créer un groupe de ressources Azure et un compte Data Lake Store avant de pouvoir créer un compte Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="15589-141">You must create an Azure Resource group, and a Data Lake Store account before you can create a Data Lake Analytics account.</span></span>  <span data-ttu-id="15589-142">Consultez [Créer un compte Data Lake Store](../data-lake-store/data-lake-store-get-started-rest-api.md#create-a-data-lake-store-account).</span><span class="sxs-lookup"><span data-stu-id="15589-142">See [Create a Data Lake Store account](../data-lake-store/data-lake-store-get-started-rest-api.md#create-a-data-lake-store-account).</span></span>

<span data-ttu-id="15589-143">La commande Curl suivante montre comment créer un compte :</span><span class="sxs-lookup"><span data-stu-id="15589-143">The following Curl command shows how to create an account:</span></span>

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -H "Content-Type: application/json" https://management.azure.com/subscriptions/<AzureSubscriptionID>/resourceGroups/<AzureResourceGroupName>/providers/Microsoft.DataLakeAnalytics/accounts/<NewAzureDataLakeAnalyticsAccountName>?api-version=2016-11-01 -d@"C:\tutorials\adla\CreateDataLakeAnalyticsAccountRequest.json"

<span data-ttu-id="15589-144">Remplacez \<`REDACTED`\> par le jeton d’autorisation, \<`AzureSubscriptionID`\> par votre ID d’abonnement \<`AzureResourceGroupName`\> par un nom de groupe de ressources Azure existant, et \<`NewAzureDataLakeAnalyticsAccountName`\> par le nom d’un nouveau compte Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="15589-144">Replace \<`REDACTED`\> with the authorization token, \<`AzureSubscriptionID`\> with your subscription ID, \<`AzureResourceGroupName`\> with an existing Azure Resource Group name, and \<`NewAzureDataLakeAnalyticsAccountName`\> with a new Data Lake Analytics Account name.</span></span> <span data-ttu-id="15589-145">La charge utile de la demande pour cette commande est contenue dans le fichier **CreateDatalakeAnalyticsAccountRequest.json** fourni pour le paramètre `-d` ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="15589-145">The request payload for this command is contained in the **CreateDatalakeAnalyticsAccountRequest.json** file that is provided for the `-d` parameter above.</span></span> <span data-ttu-id="15589-146">Le contenu du fichier input.json ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="15589-146">The contents of the input.json file resemble the following:</span></span>

    {  
        "location": "East US 2",  
        "name": "myadla1004",  
        "tags": {},  
        "properties": {  
            "defaultDataLakeStoreAccount": "my1004store",  
            "dataLakeStoreAccounts": [  
                {  
                    "name": "my1004store"  
                }     
            ]
        }  
    }  


## <a name="list-data-lake-analytics-accounts-in-a-subscription"></a><span data-ttu-id="15589-147">Énumérer les comptes Data Lake Analytics d’un abonnement</span><span class="sxs-lookup"><span data-stu-id="15589-147">List Data Lake Analytics accounts in a subscription</span></span>
<span data-ttu-id="15589-148">La commande Curl suivante montre comment répertorier les comptes dans un abonnement :</span><span class="sxs-lookup"><span data-stu-id="15589-148">The following Curl command shows how to list accounts in a subscription:</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/<AzureSubscriptionID>/providers/Microsoft.DataLakeAnalytics/Accounts?api-version=2016-11-01

<span data-ttu-id="15589-149">Remplacez \<`REDACTED`\> par le jeton d’autorisation, \<`AzureSubscriptionID`\> par votre ID d’abonnement.</span><span class="sxs-lookup"><span data-stu-id="15589-149">Replace \<`REDACTED`\> with the authorization token, \<`AzureSubscriptionID`\> with your subscription ID.</span></span> <span data-ttu-id="15589-150">Le résultat ressemble à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="15589-150">The output is similar to:</span></span>

    {
        "value": [
            {
            "properties": {
                "provisioningState": "Succeeded",
                "state": "Active",
                "endpoint": "myadla0831.azuredatalakeanalytics.net",
                "accountId": "21e74660-0941-4880-ae72-b143c2615ea9",
                "creationTime": "2016-09-01T12:49:12.7451428Z",
                "lastModifiedTime": "2016-09-01T12:49:12.7451428Z"
            },
            "location": "East US 2",
            "tags": {},
            "id": "/subscriptions/65a1016d-0f67-45d2-b838-b8f373d6d52e/resourceGroups/myadla0831rg/providers/Microsoft.DataLakeAnalytics/accounts/myadla0831",
            "name": "myadla0831",
            "type": "Microsoft.DataLakeAnalytics/accounts"
            },
            {
            "properties": {
                "provisioningState": "Succeeded",
                "state": "Active",
                "endpoint": "myadla1004.azuredatalakeanalytics.net",
                "accountId": "3ff9b93b-11c4-43c6-83cc-276292eeb350",
                "creationTime": "2016-10-04T20:46:42.287147Z",
                "lastModifiedTime": "2016-10-04T20:46:42.287147Z"
            },
            "location": "East US 2",
            "tags": {},
            "id": "/subscriptions/65a1016d-0f67-45d2-b838-b8f373d6d52e/resourceGroups/myadla1004rg/providers/Microsoft.DataLakeAnalytics/accounts/myadla1004",
            "name": "myadla1004",
            "type": "Microsoft.DataLakeAnalytics/accounts"
            }
        ]
    }

## <a name="get-information-about-a-data-lake-analytics-account"></a><span data-ttu-id="15589-151">Obtenir des informations sur un compte Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="15589-151">Get information about a Data Lake Analytics account</span></span>
<span data-ttu-id="15589-152">La commande Curl suivante montre comment obtenir des informations sur un compte :</span><span class="sxs-lookup"><span data-stu-id="15589-152">The following Curl command shows how to get an account information:</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/<AzureSubscriptionID>/resourceGroups/<AzureResourceGroupName>/providers/Microsoft.DataLakeAnalytics/accounts/<DataLakeAnalyticsAccountName>?api-version=2015-11-01

<span data-ttu-id="15589-153">Remplacez \<`REDACTED`\> par le jeton d’autorisation, \<`AzureSubscriptionID`\> par votre ID d’abonnement \<`AzureResourceGroupName`\> par un nom de groupe de ressources Azure existant, et \<`DataLakeAnalyticsAccountName`\> par le nom d’un compte Data Lake Analytics existant.</span><span class="sxs-lookup"><span data-stu-id="15589-153">Replace \<`REDACTED`\> with the authorization token, \<`AzureSubscriptionID`\> with your subscription ID, \<`AzureResourceGroupName`\> with an existing Azure Resource Group name, and \<`DataLakeAnalyticsAccountName`\> with the name of an existing Data Lake Analytics Account.</span></span> <span data-ttu-id="15589-154">Le résultat ressemble à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="15589-154">The output is similar to:</span></span>

    {
        "properties": {
            "defaultDataLakeStoreAccount": "my1004store",
            "dataLakeStoreAccounts": [
            {
                "properties": {
                "suffix": "azuredatalakestore.net"
                },
                "name": "my1004store"
            }
            ],
            "provisioningState": "Creating",
            "state": null,
            "endpoint": null,
            "accountId": "3ff9b93b-11c4-43c6-83cc-276292eeb350",
            "creationTime": null,
            "lastModifiedTime": null
        },
        "location": "East US 2",
        "tags": {},
        "id": "/subscriptions/65a1016d-0f67-45d2-b838-b8f373d6d52e/resourceGroups/myadla1004rg/providers/Microsoft.DataLakeAnalytics/accounts/myadla1004",
        "name": "myadla1004",
        "type": "Microsoft.DataLakeAnalytics/accounts"
    }

## <a name="list-data-lake-stores-of-a-data-lake-analytics-account"></a><span data-ttu-id="15589-155">Répertorier les magasins Data Lake d’un compte Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="15589-155">List Data Lake Stores of a Data Lake Analytics account</span></span>
<span data-ttu-id="15589-156">La commande Curl suivante montre comment répertorier les magasins Data Lake d’un compte :</span><span class="sxs-lookup"><span data-stu-id="15589-156">The following Curl command shows how to list Data Lake Stores of an account:</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/<AzureSubscriptionID>/resourceGroups/<AzureResourceGroupName>/providers/Microsoft.DataLakeAnalytics/accounts/<DataLakeAnalyticsAccountName>/DataLakeStoreAccounts/?api-version=2016-11-01

<span data-ttu-id="15589-157">Remplacez \<`REDACTED`\> par le jeton d’autorisation, \<`AzureSubscriptionID`\> par votre ID d’abonnement \<`AzureResourceGroupName`\> par un nom de groupe de ressources Azure existant, et \<`DataLakeAnalyticsAccountName`\> par le nom d’un compte Data Lake Analytics existant.</span><span class="sxs-lookup"><span data-stu-id="15589-157">Replace \<`REDACTED`\> with the authorization token, \<`AzureSubscriptionID`\> with your subscription ID, \<`AzureResourceGroupName`\> with an existing Azure Resource Group name, and \<`DataLakeAnalyticsAccountName`\> with the name of an existing Data Lake Analytics Account.</span></span> <span data-ttu-id="15589-158">Le résultat ressemble à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="15589-158">The output is similar to:</span></span>

    {
        "value": [
            {
            "properties": {
                "suffix": "azuredatalakestore.net"
            },
            "id": "/subscriptions/65a1016d-0f67-45d2-b838-b8f373d6d52e/resourceGroups/myadla1004rg/providers/Microsoft.DataLakeAnalytics/accounts/myadla1004/dataLakeStoreAccounts/my1004store",
            "name": "my1004store",
            "type": "Microsoft.DataLakeAnalytics/accounts/dataLakeStoreAccounts"
            }
        ]
    }

## <a name="submit-u-sql-jobs"></a><span data-ttu-id="15589-159">Envoyer des travaux U-SQL</span><span class="sxs-lookup"><span data-stu-id="15589-159">Submit U-SQL jobs</span></span>
<span data-ttu-id="15589-160">La commande Curl suivante montre comment envoyer un travail U-SQL :</span><span class="sxs-lookup"><span data-stu-id="15589-160">The following Curl command shows how to submit a U-SQL job:</span></span>

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" https://<DataLakeAnalyticsAccountName>.azuredatalakeanalytics.net/Jobs/<NewGUID>?api-version=2016-03-20-preview -d@"C:\tutorials\adla\SubmitADLAJob.json"

<span data-ttu-id="15589-161">Remplacez \<`REDACTED`\> par le jeton d’autorisation, \<`DataLakeAnalyticsAccountName`\> par le nom d’un compte Data Lake Analytics existant.</span><span class="sxs-lookup"><span data-stu-id="15589-161">Replace \<`REDACTED`\> with the authorization token, \<`DataLakeAnalyticsAccountName`\> with the name of an existing Data Lake Analytics Account.</span></span> <span data-ttu-id="15589-162">La charge utile de la demande pour cette commande est contenue dans le fichier **SubmitADLAJob.json** fourni pour le paramètre `-d` ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="15589-162">The request payload for this command is contained in the **SubmitADLAJob.json** file that is provided for the `-d` parameter above.</span></span> <span data-ttu-id="15589-163">Le contenu du fichier input.json ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="15589-163">The contents of the input.json file resemble the following:</span></span>

    {
        "jobId": "8f8ebf8c-4b63-428a-ab46-a03d2cc5b65a",
        "name": "convertTSVtoCSV",
        "type": "USql",
        "degreeOfParallelism": 1,
        "priority": 1000,
        "properties": {
            "type": "USql",
            "script": "@searchlog =\n    EXTRACT UserId          int,\n            Start           DateTime,\n            Region          string,\n            Query          
        string,\n            Duration        int?,\n            Urls            string,\n            ClickedUrls     string\n    FROM \"/Samples/Data/SearchLog.tsv\"\n    US
        ING Extractors.Tsv();\n\nOUTPUT @searchlog   \n    TO \"/Output/SearchLog-from-Data-Lake.csv\"\nUSING Outputters.Csv();"
        }
    }

<span data-ttu-id="15589-164">Le résultat ressemble à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="15589-164">The output is similar to:</span></span>

    {
        "jobId": "8f8ebf8c-4b63-428a-ab46-a03d2cc5b65a",
        "name": "convertTSVtoCSV",
        "type": "USql",
        "submitter": "myadl@SPI",
        "degreeOfParallelism": 1,
        "priority": 1000,
        "submitTime": "2016-10-05T13:54:59.9871859+00:00",
        "state": "Compiling",
        "result": "Succeeded",
        "stateAuditRecords": [
            {
            "newState": "New",
            "timeStamp": "2016-10-05T13:54:59.9871859+00:00",
            "details": "userName:myadl@SPI;submitMachine:N/A"
            }
        ],
        "properties": {
            "owner": "myadl@SPI",
            "resources": [],
            "runtimeVersion": "default",
            "rootProcessNodeId": "00000000-0000-0000-0000-000000000000",
            "algebraFilePath": "adl://myadls0831.azuredatalakestore.net/system/jobservice/jobs/Usql/2016/10/05/13/54/8f8ebf8c-4b63-428a-ab46-a03d2cc5b65a/algebra.xml",
            "compileMode": "Semantic",
            "errorSource": "Unknown",
            "totalCompilationTime": "PT0S",
            "totalPausedTime": "PT0S",
            "totalQueuedTime": "PT0S",
            "totalRunningTime": "PT0S",
            "type": "USql"
        }
    }


## <a name="list-u-sql-jobs"></a><span data-ttu-id="15589-165">Répertorier des travaux U-SQL</span><span class="sxs-lookup"><span data-stu-id="15589-165">List U-SQL jobs</span></span>
<span data-ttu-id="15589-166">La commande Curl suivante montre comment répertorier des travaux U-SQL :</span><span class="sxs-lookup"><span data-stu-id="15589-166">The following Curl command shows how to list U-SQL jobs:</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://<DataLakeAnalyticsAccountName>.azuredatalakeanalytics.net/Jobs?api-version=2016-11-01 

<span data-ttu-id="15589-167">Remplacez \<`REDACTED`\> par le jeton d’autorisation et \<`DataLakeAnalyticsAccountName`\> par le nom d’un compte Data Lake Analytics existant.</span><span class="sxs-lookup"><span data-stu-id="15589-167">Replace \<`REDACTED`\> with the authorization token, and \<`DataLakeAnalyticsAccountName`\> with the name of an existing Data Lake Analytics Account.</span></span> 

<span data-ttu-id="15589-168">Le résultat ressemble à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="15589-168">The output is similar to:</span></span>

    {
    "value": [
        {
        "jobId": "65cf1691-9dbe-43cd-90ed-1cafbfb406fb",
        "name": "convertTSVtoCSV",
        "type": "USql",
        "submitter": "someone@microsoft.com",
        "account": null,
        "degreeOfParallelism": 1,
        "priority": 1000,
        "submitTime": "Wed, 05 Oct 2016 13:46:53 GMT",
        "startTime": "Wed, 05 Oct 2016 13:47:33 GMT",
        "endTime": "Wed, 05 Oct 2016 13:48:07 GMT",
        "state": "Ended",
        "result": "Succeeded",
        "errorMessage": null,
        "storageAccounts": null,
        "stateAuditRecords": null,
        "logFilePatterns": null,
        "properties": null
        },
        {
        "jobId": "8f8ebf8c-4b63-428a-ab46-a03d2cc5b65a",
        "name": "convertTSVtoCSV",
        "type": "USql",
        "submitter": "someoneadl@SPI",
        "account": null,
        "degreeOfParallelism": 1,
        "priority": 1000,
        "submitTime": "Wed, 05 Oct 2016 13:54:59 GMT",
        "startTime": "Wed, 05 Oct 2016 13:55:43 GMT",
        "endTime": "Wed, 05 Oct 2016 13:56:11 GMT",
        "state": "Ended",
        "result": "Succeeded",
        "errorMessage": null,
        "storageAccounts": null,
        "stateAuditRecords": null,
        "logFilePatterns": null,
        "properties": null
        }
    ],
    "nextLink": null,
    "count": null
    }


## <a name="get-catalog-items"></a><span data-ttu-id="15589-169">Obtenir les éléments du catalogue</span><span class="sxs-lookup"><span data-stu-id="15589-169">Get catalog items</span></span>
<span data-ttu-id="15589-170">La commande Curl suivante montre comment obtenir les bases de données à partir du catalogue :</span><span class="sxs-lookup"><span data-stu-id="15589-170">The following Curl command shows how to get the databases from the catalog:</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://<DataLakeAnalyticsAccountName>.azuredatalakeanalytics.net/catalog/usql/databases?api-version=2016-11-01

<span data-ttu-id="15589-171">Le résultat ressemble à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="15589-171">The output is similar to:</span></span>

    {
    "@odata.context":"https://myadla0831.azuredatalakeanalytics.net/sqlip/$metadata#databases","value":[
        {
        "computeAccountName":"myadla0831","databaseName":"mytest","version":"f6956327-90b8-4648-ad8b-de3ff09274ea"
        },{
        "computeAccountName":"myadla0831","databaseName":"master","version":"e8bca908-cc73-41a3-9564-e9bcfaa21f4e"
        }
    ]
    }

## <a name="see-also"></a><span data-ttu-id="15589-172">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="15589-172">See also</span></span>
* <span data-ttu-id="15589-173">Pour voir une requête plus complexe, consultez [Analyse de journaux des sites web à l'aide d'Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span><span class="sxs-lookup"><span data-stu-id="15589-173">To see a more complex query, see [Analyze Website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
* <span data-ttu-id="15589-174">Pour commencer à développer des applications U-SQL, consultez [Développer des scripts U-SQL avec Data Lake Tools pour Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="15589-174">To get started developing U-SQL applications, see [Develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
* <span data-ttu-id="15589-175">Pour connaître U-SQL, voir [Prise en main du langage U-SQL d’Analytique Data Lake Azure](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="15589-175">To learn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>
* <span data-ttu-id="15589-176">Pour les tâches de gestion, consultez [Gestion d’Azure Data Lake Analytics à l’aide du portail Azure](data-lake-analytics-manage-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="15589-176">For management tasks, see [Manage Azure Data Lake Analytics using Azure portal](data-lake-analytics-manage-use-portal.md).</span></span>
* <span data-ttu-id="15589-177">Pour obtenir une vue d'ensemble de Data Lake Analytics, consultez [Vue d'ensemble de Data Lake Analytics Azure](data-lake-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="15589-177">To get an overview of Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span></span>
* <span data-ttu-id="15589-178">Pour afficher le même didacticiel en utilisant d’autres outils, cliquez sur les sélecteurs d’onglet en haut de la page.</span><span class="sxs-lookup"><span data-stu-id="15589-178">To see the same tutorial using other tools, click the tab selectors on the top of the page.</span></span>

