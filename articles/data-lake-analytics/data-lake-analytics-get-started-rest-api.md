---
title: "aaaGet main Analytique lac de données à l’aide des API REST | Documents Microsoft"
description: "Utilisez des opérations de tooperform WebHDFS REST API sur Analytique lac de données"
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
ms.openlocfilehash: a0b13d521821fd2d74716cc52485585feb7c51b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-rest-apis"></a><span data-ttu-id="f161a-103">Prise en main d’Azure Data Lake Analytics à l’aide d’API REST</span><span class="sxs-lookup"><span data-stu-id="f161a-103">Get started with Azure Data Lake Analytics using REST APIs</span></span>
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

<span data-ttu-id="f161a-104">Découvrez comment toouse WebHDFS REST API et données Lake Analytique reste toomanage Analytique lac de données des comptes, des travaux et de catalogue.</span><span class="sxs-lookup"><span data-stu-id="f161a-104">Learn how toouse WebHDFS REST APIs and Data Lake Analytics REST APIs toomanage Data Lake Analytics accounts, jobs, and catalog.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="f161a-105">Composants requis</span><span class="sxs-lookup"><span data-stu-id="f161a-105">Prerequisites</span></span>
* <span data-ttu-id="f161a-106">**Un abonnement Azure**.</span><span class="sxs-lookup"><span data-stu-id="f161a-106">**An Azure subscription**.</span></span> <span data-ttu-id="f161a-107">Consultez la page [Obtention d’un essai gratuit d’Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f161a-107">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="f161a-108">**Créez une application Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f161a-108">**Create an Azure Active Directory Application**.</span></span> <span data-ttu-id="f161a-109">Vous utilisez hello Azure AD tooauthenticate hello Analytique lac de données une application avec Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f161a-109">You use hello Azure AD application tooauthenticate hello Data Lake Analytics application with Azure AD.</span></span> <span data-ttu-id="f161a-110">Il existe tooauthenticate différentes approches avec Azure AD, qui sont **l’authentification de l’utilisateur final** ou **l’authentification de service**.</span><span class="sxs-lookup"><span data-stu-id="f161a-110">There are different approaches tooauthenticate with Azure AD, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="f161a-111">Pour plus d’informations sur la façon d’et tooauthenticate, consultez [authentifier avec Analytique lac de données à l’aide d’Azure Active Directory](../data-lake-store/data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="f161a-111">For instructions and more information on how tooauthenticate, see [Authenticate with Data Lake Analytics using Azure Active Directory](../data-lake-store/data-lake-store-authenticate-using-active-directory.md).</span></span>
* <span data-ttu-id="f161a-112">[cURL](http://curl.haxx.se/).</span><span class="sxs-lookup"><span data-stu-id="f161a-112">[cURL](http://curl.haxx.se/).</span></span> <span data-ttu-id="f161a-113">Cet article utilise toodemonstrate cURL comment toomake API REST appelle par rapport à un compte Analytique lac de données.</span><span class="sxs-lookup"><span data-stu-id="f161a-113">This article uses cURL toodemonstrate how toomake REST API calls against a Data Lake Analytics account.</span></span>

## <a name="authenticate-with-azure-active-directory"></a><span data-ttu-id="f161a-114">S’authentifier à l’aide d’Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f161a-114">Authenticate with Azure Active Directory</span></span>
<span data-ttu-id="f161a-115">Il existe deux méthodes d’authentification avec Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f161a-115">There are two methods for authenticating with Azure Active Directory.</span></span>

### <a name="end-user-authentication-interactive"></a><span data-ttu-id="f161a-116">Authentification de l’utilisateur final (interactive)</span><span class="sxs-lookup"><span data-stu-id="f161a-116">End-user authentication (interactive)</span></span>
<span data-ttu-id="f161a-117">À l’aide de cette méthode, application demande toolog d’utilisateur hello dans et toutes les opérations de hello sont effectuées dans le contexte de hello d’utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="f161a-117">Using this method, application prompts hello user toolog in and all hello operations are performed in hello context of hello user.</span></span> 

<span data-ttu-id="f161a-118">Pour l’authentification interactive, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="f161a-118">Follow these steps for interactive authentication:</span></span>

1. <span data-ttu-id="f161a-119">Via votre application, la redirection toohello d’utilisateur hello suivant l’URL :</span><span class="sxs-lookup"><span data-stu-id="f161a-119">Through your application, redirect hello user toohello following URL:</span></span>
   
        https://login.microsoftonline.com/<TENANT-ID>/oauth2/authorize?client_id=<CLIENT-ID>&response_type=code&redirect_uri=<REDIRECT-URI>
   
   > [!NOTE]
   > <span data-ttu-id="f161a-120">\<URI de redirection > doit toobe codé à utiliser dans une URL.</span><span class="sxs-lookup"><span data-stu-id="f161a-120">\<REDIRECT-URI> needs toobe encoded for use in a URL.</span></span> <span data-ttu-id="f161a-121">Par conséquent, pour https://localhost, utilisez `https%3A%2F%2Flocalhost`)</span><span class="sxs-lookup"><span data-stu-id="f161a-121">So, for https://localhost, use `https%3A%2F%2Flocalhost`)</span></span>
   > 
   > 
   
    <span data-ttu-id="f161a-122">Fins hello de ce didacticiel, vous pouvez remplacer les valeurs d’espace réservé hello URL hello ci-dessus et collez-le dans la barre d’adresses d’un navigateur web.</span><span class="sxs-lookup"><span data-stu-id="f161a-122">For hello purpose of this tutorial, you can replace hello placeholder values in hello URL above and paste it in a web browser's address bar.</span></span> <span data-ttu-id="f161a-123">Vous serez redirigé tooauthenticate à l’aide de votre connexion à Azure.</span><span class="sxs-lookup"><span data-stu-id="f161a-123">You will be redirected tooauthenticate using your Azure login.</span></span> <span data-ttu-id="f161a-124">Une fois correctement vous connecter, réponse de hello est affichée dans la barre d’adresses du navigateur hello.</span><span class="sxs-lookup"><span data-stu-id="f161a-124">Once you succesfully log in, hello response is displayed in hello browser's address bar.</span></span> <span data-ttu-id="f161a-125">réponse de Hello sera Bonjour suivant le format :</span><span class="sxs-lookup"><span data-stu-id="f161a-125">hello response will be in hello following format:</span></span>
   
        http://localhost/?code=<AUTHORIZATION-CODE>&session_state=<GUID>
2. <span data-ttu-id="f161a-126">Capturer le code d’autorisation de hello de réponse de hello.</span><span class="sxs-lookup"><span data-stu-id="f161a-126">Capture hello authorization code from hello response.</span></span> <span data-ttu-id="f161a-127">Pour ce didacticiel, vous pouvez copier le code d’autorisation de hello à partir de la barre d’adresses hello de navigateur hello et passer dans hello POST demande toohello jeton point de terminaison, comme indiqué ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="f161a-127">For this tutorial, you can copy hello authorization code from hello address bar of hello web browser and pass it in hello POST request toohello token endpoint, as shown below:</span></span>
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token \
        -F redirect_uri=<REDIRECT-URI> \
        -F grant_type=authorization_code \
        -F resource=https://management.core.windows.net/ \
        -F client_id=<CLIENT-ID> \
        -F code=<AUTHORIZATION-CODE>
   
   > [!NOTE]
   > <span data-ttu-id="f161a-128">Dans ce cas, hello \<URI de redirection > ne doivent pas être encodé.</span><span class="sxs-lookup"><span data-stu-id="f161a-128">In this case, hello \<REDIRECT-URI> need not be encoded.</span></span>
   > 
   > 
3. <span data-ttu-id="f161a-129">réponse de Hello est un objet JSON qui contient un jeton d’accès (par exemple, `"access_token": "<ACCESS_TOKEN>"`) et un jeton d’actualisation (par exemple, `"refresh_token": "<REFRESH_TOKEN>"`).</span><span class="sxs-lookup"><span data-stu-id="f161a-129">hello response is a JSON object that contains an access token (e.g., `"access_token": "<ACCESS_TOKEN>"`) and a refresh token (e.g., `"refresh_token": "<REFRESH_TOKEN>"`).</span></span> <span data-ttu-id="f161a-130">Votre application utilise hello jeton d’accès lors de l’accès d’Azure Data Lake Store et tooget de jeton hello actualiser un autre jeton d’accès quand un jeton d’accès expire.</span><span class="sxs-lookup"><span data-stu-id="f161a-130">Your application uses hello access token when accessing Azure Data Lake Store and hello refresh token tooget another access token when an access token expires.</span></span>
   
        {"token_type":"Bearer","scope":"user_impersonation","expires_in":"3599","expires_on":"1461865782","not_before":    "1461861882","resource":"https://management.core.windows.net/","access_token":"<REDACTED>","refresh_token":"<REDACTED>","id_token":"<REDACTED>"}
4. <span data-ttu-id="f161a-131">Expiration du jeton d’accès hello, vous pouvez demander un nouveau jeton d’accès à l’aide du jeton d’actualisation hello, comme indiqué ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="f161a-131">When hello access token expires, you can request a new access token using hello refresh token, as shown below:</span></span>
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
             -F grant_type=refresh_token \
             -F resource=https://management.core.windows.net/ \
             -F client_id=<CLIENT-ID> \
             -F refresh_token=<REFRESH-TOKEN>

<span data-ttu-id="f161a-132">Pour plus d’informations sur l’authentification utilisateur interactive, consultez [Flux d’octroi d’un code d’autorisation](https://msdn.microsoft.com/library/azure/dn645542.aspx).</span><span class="sxs-lookup"><span data-stu-id="f161a-132">For more information on interactive user authentication, see [Authorization code grant flow](https://msdn.microsoft.com/library/azure/dn645542.aspx).</span></span>

### <a name="service-to-service-authentication-non-interactive"></a><span data-ttu-id="f161a-133">Authentification de service à service (non interactive)</span><span class="sxs-lookup"><span data-stu-id="f161a-133">Service-to-service authentication (non-interactive)</span></span>
<span data-ttu-id="f161a-134">À l’aide de cette méthode, application fournit ses propres informations d’identification des opérations de hello tooperform.</span><span class="sxs-lookup"><span data-stu-id="f161a-134">Using this method, application provides its own credentials tooperform hello operations.</span></span> <span data-ttu-id="f161a-135">Pour ce faire, vous devez émettre une demande POST comme hello illustré ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="f161a-135">For this, you must issue a POST request like hello one shown below:</span></span> 

    curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
      -F grant_type=client_credentials \
      -F resource=https://management.core.windows.net/ \
      -F client_id=<CLIENT-ID> \
      -F client_secret=<AUTH-KEY>

<span data-ttu-id="f161a-136">sortie Hello de cette demande inclut un jeton d’autorisation (indiqué par `access-token` dans la sortie de hello ci-dessous) que vous allez transmettre ensuite avec vos appels d’API REST.</span><span class="sxs-lookup"><span data-stu-id="f161a-136">hello output of this request will include an authorization token (denoted by `access-token` in hello output below) that you will subsequently pass with your REST API calls.</span></span> <span data-ttu-id="f161a-137">Enregistrez ce jeton d’authentification dans un fichier texte, car vous en aurez besoin plus loin dans cet article.</span><span class="sxs-lookup"><span data-stu-id="f161a-137">Save this authentication token in a text file; you will need this later in this article.</span></span>

    {"token_type":"Bearer","expires_in":"3599","expires_on":"1458245447","not_before":"1458241547","resource":"https://management.core.windows.net/","access_token":"<REDACTED>"}

<span data-ttu-id="f161a-138">Cet article utilise hello **non interactif** approche.</span><span class="sxs-lookup"><span data-stu-id="f161a-138">This article uses hello **non-interactive** approach.</span></span> <span data-ttu-id="f161a-139">Pour plus d’informations sur la non interactif (appels de service), consultez [tooservice les appels à l’aide des informations d’identification de Service](https://msdn.microsoft.com/library/azure/dn645543.aspx).</span><span class="sxs-lookup"><span data-stu-id="f161a-139">For more information on non-interactive (service-to-service calls), see [Service tooservice calls using credentials](https://msdn.microsoft.com/library/azure/dn645543.aspx).</span></span>

## <a name="create-a-data-lake-analytics-account"></a><span data-ttu-id="f161a-140">Créer un compte Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="f161a-140">Create a Data Lake Analytics account</span></span>
<span data-ttu-id="f161a-141">Vous devez créer un groupe de ressources Azure et un compte Data Lake Store avant de pouvoir créer un compte Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="f161a-141">You must create an Azure Resource group, and a Data Lake Store account before you can create a Data Lake Analytics account.</span></span>  <span data-ttu-id="f161a-142">Consultez [Créer un compte Data Lake Store](../data-lake-store/data-lake-store-get-started-rest-api.md#create-a-data-lake-store-account).</span><span class="sxs-lookup"><span data-stu-id="f161a-142">See [Create a Data Lake Store account](../data-lake-store/data-lake-store-get-started-rest-api.md#create-a-data-lake-store-account).</span></span>

<span data-ttu-id="f161a-143">Hello suivant de commande Curl indique comment toocreate un compte :</span><span class="sxs-lookup"><span data-stu-id="f161a-143">hello following Curl command shows how toocreate an account:</span></span>

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -H "Content-Type: application/json" https://management.azure.com/subscriptions/<AzureSubscriptionID>/resourceGroups/<AzureResourceGroupName>/providers/Microsoft.DataLakeAnalytics/accounts/<NewAzureDataLakeAnalyticsAccountName>?api-version=2016-11-01 -d@"C:\tutorials\adla\CreateDataLakeAnalyticsAccountRequest.json"

<span data-ttu-id="f161a-144">Remplacez \< `REDACTED` \> avec un jeton d’autorisation de hello, \< `AzureSubscriptionID` \> avec votre ID d’abonnement \< `AzureResourceGroupName` \> avec une ressource Azure existante Nom du groupe, et \< `NewAzureDataLakeAnalyticsAccountName` \> avec un nouveau nom de compte d’Analytique Data Lake.</span><span class="sxs-lookup"><span data-stu-id="f161a-144">Replace \<`REDACTED`\> with hello authorization token, \<`AzureSubscriptionID`\> with your subscription ID, \<`AzureResourceGroupName`\> with an existing Azure Resource Group name, and \<`NewAzureDataLakeAnalyticsAccountName`\> with a new Data Lake Analytics Account name.</span></span> <span data-ttu-id="f161a-145">charge utile de demande Hello pour cette commande est contenue dans hello **CreateDatalakeAnalyticsAccountRequest.json** fichier fourni pour hello `-d` paramètre ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="f161a-145">hello request payload for this command is contained in hello **CreateDatalakeAnalyticsAccountRequest.json** file that is provided for hello `-d` parameter above.</span></span> <span data-ttu-id="f161a-146">contenu Hello du fichier de input.json hello ressemblent aux suivantes de hello :</span><span class="sxs-lookup"><span data-stu-id="f161a-146">hello contents of hello input.json file resemble hello following:</span></span>

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


## <a name="list-data-lake-analytics-accounts-in-a-subscription"></a><span data-ttu-id="f161a-147">Énumérer les comptes Data Lake Analytics d’un abonnement</span><span class="sxs-lookup"><span data-stu-id="f161a-147">List Data Lake Analytics accounts in a subscription</span></span>
<span data-ttu-id="f161a-148">Hello enroulement de la commande suivante montre comment toolist comptes dans un abonnement :</span><span class="sxs-lookup"><span data-stu-id="f161a-148">hello following Curl command shows how toolist accounts in a subscription:</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/<AzureSubscriptionID>/providers/Microsoft.DataLakeAnalytics/Accounts?api-version=2016-11-01

<span data-ttu-id="f161a-149">Remplacez \< `REDACTED` \> avec un jeton d’autorisation de hello, \< `AzureSubscriptionID` \> avec votre ID d’abonnement.</span><span class="sxs-lookup"><span data-stu-id="f161a-149">Replace \<`REDACTED`\> with hello authorization token, \<`AzureSubscriptionID`\> with your subscription ID.</span></span> <span data-ttu-id="f161a-150">résultat de Hello est similaire à :</span><span class="sxs-lookup"><span data-stu-id="f161a-150">hello output is similar to:</span></span>

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

## <a name="get-information-about-a-data-lake-analytics-account"></a><span data-ttu-id="f161a-151">Obtenir des informations sur un compte Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="f161a-151">Get information about a Data Lake Analytics account</span></span>
<span data-ttu-id="f161a-152">Hello suivant de commande Curl indique comment tooget une information de compte :</span><span class="sxs-lookup"><span data-stu-id="f161a-152">hello following Curl command shows how tooget an account information:</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/<AzureSubscriptionID>/resourceGroups/<AzureResourceGroupName>/providers/Microsoft.DataLakeAnalytics/accounts/<DataLakeAnalyticsAccountName>?api-version=2015-11-01

<span data-ttu-id="f161a-153">Remplacez \< `REDACTED` \> avec un jeton d’autorisation de hello, \< `AzureSubscriptionID` \> avec votre ID d’abonnement \< `AzureResourceGroupName` \> avec une ressource Azure existante Nom du groupe, et \< `DataLakeAnalyticsAccountName` \> avec nom hello d’un compte d’Analytique Data Lake existant.</span><span class="sxs-lookup"><span data-stu-id="f161a-153">Replace \<`REDACTED`\> with hello authorization token, \<`AzureSubscriptionID`\> with your subscription ID, \<`AzureResourceGroupName`\> with an existing Azure Resource Group name, and \<`DataLakeAnalyticsAccountName`\> with hello name of an existing Data Lake Analytics Account.</span></span> <span data-ttu-id="f161a-154">résultat de Hello est similaire à :</span><span class="sxs-lookup"><span data-stu-id="f161a-154">hello output is similar to:</span></span>

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

## <a name="list-data-lake-stores-of-a-data-lake-analytics-account"></a><span data-ttu-id="f161a-155">Répertorier les magasins Data Lake d’un compte Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="f161a-155">List Data Lake Stores of a Data Lake Analytics account</span></span>
<span data-ttu-id="f161a-156">Hello enroulement de la commande suivante montre en quoi les magasins d’un compte toolist Data Lake :</span><span class="sxs-lookup"><span data-stu-id="f161a-156">hello following Curl command shows how toolist Data Lake Stores of an account:</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/<AzureSubscriptionID>/resourceGroups/<AzureResourceGroupName>/providers/Microsoft.DataLakeAnalytics/accounts/<DataLakeAnalyticsAccountName>/DataLakeStoreAccounts/?api-version=2016-11-01

<span data-ttu-id="f161a-157">Remplacez \< `REDACTED` \> avec un jeton d’autorisation de hello, \< `AzureSubscriptionID` \> avec votre ID d’abonnement \< `AzureResourceGroupName` \> avec une ressource Azure existante Nom du groupe, et \< `DataLakeAnalyticsAccountName` \> avec nom hello d’un compte d’Analytique Data Lake existant.</span><span class="sxs-lookup"><span data-stu-id="f161a-157">Replace \<`REDACTED`\> with hello authorization token, \<`AzureSubscriptionID`\> with your subscription ID, \<`AzureResourceGroupName`\> with an existing Azure Resource Group name, and \<`DataLakeAnalyticsAccountName`\> with hello name of an existing Data Lake Analytics Account.</span></span> <span data-ttu-id="f161a-158">résultat de Hello est similaire à :</span><span class="sxs-lookup"><span data-stu-id="f161a-158">hello output is similar to:</span></span>

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

## <a name="submit-u-sql-jobs"></a><span data-ttu-id="f161a-159">Envoyer des travaux U-SQL</span><span class="sxs-lookup"><span data-stu-id="f161a-159">Submit U-SQL jobs</span></span>
<span data-ttu-id="f161a-160">Hello suivant de commande Curl indique comment le travail de toosubmit U-SQL :</span><span class="sxs-lookup"><span data-stu-id="f161a-160">hello following Curl command shows how toosubmit a U-SQL job:</span></span>

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" https://<DataLakeAnalyticsAccountName>.azuredatalakeanalytics.net/Jobs/<NewGUID>?api-version=2016-03-20-preview -d@"C:\tutorials\adla\SubmitADLAJob.json"

<span data-ttu-id="f161a-161">Remplacez \< `REDACTED` \> avec un jeton d’autorisation de hello, \< `DataLakeAnalyticsAccountName` \> avec nom hello d’un compte d’Analytique Data Lake existant.</span><span class="sxs-lookup"><span data-stu-id="f161a-161">Replace \<`REDACTED`\> with hello authorization token, \<`DataLakeAnalyticsAccountName`\> with hello name of an existing Data Lake Analytics Account.</span></span> <span data-ttu-id="f161a-162">charge utile de demande Hello pour cette commande est contenue dans hello **SubmitADLAJob.json** fichier fourni pour hello `-d` paramètre ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="f161a-162">hello request payload for this command is contained in hello **SubmitADLAJob.json** file that is provided for hello `-d` parameter above.</span></span> <span data-ttu-id="f161a-163">contenu Hello du fichier de input.json hello ressemblent aux suivantes de hello :</span><span class="sxs-lookup"><span data-stu-id="f161a-163">hello contents of hello input.json file resemble hello following:</span></span>

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
        ING Extractors.Tsv();\n\nOUTPUT @searchlog   \n    too\"/Output/SearchLog-from-Data-Lake.csv\"\nUSING Outputters.Csv();"
        }
    }

<span data-ttu-id="f161a-164">résultat de Hello est similaire à :</span><span class="sxs-lookup"><span data-stu-id="f161a-164">hello output is similar to:</span></span>

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


## <a name="list-u-sql-jobs"></a><span data-ttu-id="f161a-165">Répertorier des travaux U-SQL</span><span class="sxs-lookup"><span data-stu-id="f161a-165">List U-SQL jobs</span></span>
<span data-ttu-id="f161a-166">Hello suivant de commande Curl indique comment les travaux toolist U-SQL :</span><span class="sxs-lookup"><span data-stu-id="f161a-166">hello following Curl command shows how toolist U-SQL jobs:</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://<DataLakeAnalyticsAccountName>.azuredatalakeanalytics.net/Jobs?api-version=2016-11-01 

<span data-ttu-id="f161a-167">Remplacez \< `REDACTED` \> avec un jeton d’autorisation de hello, et \< `DataLakeAnalyticsAccountName` \> avec nom hello d’un compte d’Analytique Data Lake existant.</span><span class="sxs-lookup"><span data-stu-id="f161a-167">Replace \<`REDACTED`\> with hello authorization token, and \<`DataLakeAnalyticsAccountName`\> with hello name of an existing Data Lake Analytics Account.</span></span> 

<span data-ttu-id="f161a-168">résultat de Hello est similaire à :</span><span class="sxs-lookup"><span data-stu-id="f161a-168">hello output is similar to:</span></span>

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


## <a name="get-catalog-items"></a><span data-ttu-id="f161a-169">Obtenir les éléments du catalogue</span><span class="sxs-lookup"><span data-stu-id="f161a-169">Get catalog items</span></span>
<span data-ttu-id="f161a-170">Hello enroulement de la commande suivante montre comment les bases de données tooget hello de hello catalogue :</span><span class="sxs-lookup"><span data-stu-id="f161a-170">hello following Curl command shows how tooget hello databases from hello catalog:</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://<DataLakeAnalyticsAccountName>.azuredatalakeanalytics.net/catalog/usql/databases?api-version=2016-11-01

<span data-ttu-id="f161a-171">résultat de Hello est similaire à :</span><span class="sxs-lookup"><span data-stu-id="f161a-171">hello output is similar to:</span></span>

    {
    "@odata.context":"https://myadla0831.azuredatalakeanalytics.net/sqlip/$metadata#databases","value":[
        {
        "computeAccountName":"myadla0831","databaseName":"mytest","version":"f6956327-90b8-4648-ad8b-de3ff09274ea"
        },{
        "computeAccountName":"myadla0831","databaseName":"master","version":"e8bca908-cc73-41a3-9564-e9bcfaa21f4e"
        }
    ]
    }

## <a name="see-also"></a><span data-ttu-id="f161a-172">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="f161a-172">See also</span></span>
* <span data-ttu-id="f161a-173">toosee une requête plus complexe, consultez [site Web d’analyse se connecte à l’aide d’Analytique de LAC de données Azure](data-lake-analytics-analyze-weblogs.md).</span><span class="sxs-lookup"><span data-stu-id="f161a-173">toosee a more complex query, see [Analyze Website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
* <span data-ttu-id="f161a-174">tooget en main le développement d’applications SQL-U, consultez [scripts développer U-SQL à l’aide de Data Lake Tools pour Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="f161a-174">tooget started developing U-SQL applications, see [Develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
* <span data-ttu-id="f161a-175">toolearn U-SQL, consultez [prise en main langage lac de données Azure Analytique U-SQL](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="f161a-175">toolearn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>
* <span data-ttu-id="f161a-176">Pour les tâches de gestion, consultez [Gestion d’Azure Data Lake Analytics à l’aide du portail Azure](data-lake-analytics-manage-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="f161a-176">For management tasks, see [Manage Azure Data Lake Analytics using Azure portal](data-lake-analytics-manage-use-portal.md).</span></span>
* <span data-ttu-id="f161a-177">tooget une vue d’ensemble de données de LAC Analytique, consultez [vue d’ensemble Analytique de LAC de données Azure](data-lake-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f161a-177">tooget an overview of Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span></span>
* <span data-ttu-id="f161a-178">toosee hello même didacticiel à l’aide d’autres outils, cliquez sur les sélecteurs d’onglet hello haut hello de page de hello.</span><span class="sxs-lookup"><span data-stu-id="f161a-178">toosee hello same tutorial using other tools, click hello tab selectors on hello top of hello page.</span></span>

