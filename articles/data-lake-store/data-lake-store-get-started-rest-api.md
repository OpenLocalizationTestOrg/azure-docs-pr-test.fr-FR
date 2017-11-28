---
title: "Prise en main de Data Lake Store à l’aide de l’API REST | Microsoft Docs"
description: "Utiliser les API REST de WebHDFS pour effectuer des opérations sur Data Lake Store"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 57ac6501-cb71-4f75-82c2-acc07c562889
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/21/2017
ms.author: nitinme
ms.openlocfilehash: dc2c8f58e0a2faf1b00f4903148328a5141a8637
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-data-lake-store-using-rest-apis"></a><span data-ttu-id="184d2-103">Prise en main d’Azure Data Lake Store avec les API REST</span><span class="sxs-lookup"><span data-stu-id="184d2-103">Get started with Azure Data Lake Store using REST APIs</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="184d2-104">Portail</span><span class="sxs-lookup"><span data-stu-id="184d2-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="184d2-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="184d2-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="184d2-106">Kit SDK .NET</span><span class="sxs-lookup"><span data-stu-id="184d2-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="184d2-107">Kit SDK Java</span><span class="sxs-lookup"><span data-stu-id="184d2-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="184d2-108">API REST</span><span class="sxs-lookup"><span data-stu-id="184d2-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="184d2-109">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="184d2-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="184d2-110">Node.JS</span><span class="sxs-lookup"><span data-stu-id="184d2-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="184d2-111">Python</span><span class="sxs-lookup"><span data-stu-id="184d2-111">Python</span></span>](data-lake-store-get-started-python.md)
>
> 

<span data-ttu-id="184d2-112">Dans cet article, vous allez découvrir comment utiliser les API REST de WebHDFS et de Data Lake Store pour gérer les comptes et effectuer certaines opérations de système de fichiers sur Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="184d2-112">In this article, you will learn how to use WebHDFS REST APIs and Data Lake Store REST APIs to perform account management as well as filesystem operations on Azure Data Lake Store.</span></span> <span data-ttu-id="184d2-113">Azure Data Lake Store expose ses propres API REST pour les opérations de gestion des comptes.</span><span class="sxs-lookup"><span data-stu-id="184d2-113">Azure Data Lake Store exposes its own REST APIs for account management operations.</span></span> <span data-ttu-id="184d2-114">Toutefois, comme Data Lake Store est compatible avec HDFS et l’écosystème Hadoop, il prend en charge l’utilisation des API REST de WebHDFS pour les opérations de système de fichiers.</span><span class="sxs-lookup"><span data-stu-id="184d2-114">However, because Data Lake Store is compatible with HDFS and Hadoop ecosystem, it supports using WebHDFS REST APIs for filesystem operations.</span></span>

> [!NOTE]
> <span data-ttu-id="184d2-115">Pour plus d’informations sur la prise en charge des API REST avec Data Lake Store, consultez [Azure Data Lake Store REST API Reference](https://msdn.microsoft.com/library/mt693424.aspx)(Informations de référence sur les API REST d’Azure Data Lake Store).</span><span class="sxs-lookup"><span data-stu-id="184d2-115">For detailed information on the REST API support for Data Lake Store, see [Azure Data Lake Store REST API Reference](https://msdn.microsoft.com/library/mt693424.aspx).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="184d2-116">Composants requis</span><span class="sxs-lookup"><span data-stu-id="184d2-116">Prerequisites</span></span>
* <span data-ttu-id="184d2-117">**Un abonnement Azure**.</span><span class="sxs-lookup"><span data-stu-id="184d2-117">**An Azure subscription**.</span></span> <span data-ttu-id="184d2-118">Consultez la page [Obtention d’un essai gratuit d’Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="184d2-118">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="184d2-119">**Créez une application Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="184d2-119">**Create an Azure Active Directory Application**.</span></span> <span data-ttu-id="184d2-120">Vous utilisez l’application Azure AD pour authentifier l’application Data Lake Store auprès d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="184d2-120">You use the Azure AD application to authenticate the Data Lake Store application with Azure AD.</span></span> <span data-ttu-id="184d2-121">Il existe différentes approches pour l’authentification auprès d’Azure AD : **authentification de l’utilisateur final** ou **authentification de service à service**.</span><span class="sxs-lookup"><span data-stu-id="184d2-121">There are different approaches to authenticate with Azure AD, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="184d2-122">Pour obtenir des instructions et plus d’informations sur l’authentification, consultez [l’authentification de l’utilisateur final](data-lake-store-end-user-authenticate-using-active-directory.md) ou [l’authentification de service à service](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="184d2-122">For instructions and more information on how to authenticate, see [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md) or [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md).</span></span>
* <span data-ttu-id="184d2-123">[cURL](http://curl.haxx.se/).</span><span class="sxs-lookup"><span data-stu-id="184d2-123">[cURL](http://curl.haxx.se/).</span></span> <span data-ttu-id="184d2-124">Cet article utilise cURL pour montrer comment effectuer des appels d’API REST sur un compte Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="184d2-124">This article uses cURL to demonstrate how to make REST API calls against a Data Lake Store account.</span></span>

## <a name="how-do-i-authenticate-using-azure-active-directory"></a><span data-ttu-id="184d2-125">Comment s’authentifier à l’aide d’Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="184d2-125">How do I authenticate using Azure Active Directory?</span></span>
<span data-ttu-id="184d2-126">Vous avez le choix entre deux méthodes pour vous authentifier à l’aide d’Azure Active Directory :</span><span class="sxs-lookup"><span data-stu-id="184d2-126">You can use two approaches to authenticate using Azure Active Directory.</span></span>

### <a name="end-user-authentication-interactive"></a><span data-ttu-id="184d2-127">Authentification de l’utilisateur final (interactive)</span><span class="sxs-lookup"><span data-stu-id="184d2-127">End-user authentication (interactive)</span></span>
<span data-ttu-id="184d2-128">Dans ce scénario, l’application invite l’utilisateur à se connecter. Toutes les opérations sont effectuées dans le contexte de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="184d2-128">In this scenario, the application prompts the user to log in and all the operations are performed in the context of the user.</span></span> <span data-ttu-id="184d2-129">Pour l’authentification interactive, procédez comme suit.</span><span class="sxs-lookup"><span data-stu-id="184d2-129">Perform the following steps for interactive authentication.</span></span>

1. <span data-ttu-id="184d2-130">Dans votre application, redirigez l’utilisateur vers l’URL suivante :</span><span class="sxs-lookup"><span data-stu-id="184d2-130">Through your application, redirect the user to the following URL:</span></span>
   
        https://login.microsoftonline.com/<TENANT-ID>/oauth2/authorize?client_id=<APPLICATION-ID>&response_type=code&redirect_uri=<REDIRECT-URI>
   
   > [!NOTE]
   > <span data-ttu-id="184d2-131">L’URI \<REDIRECT-URI> doit être codée pour être utilisée dans une URL.</span><span class="sxs-lookup"><span data-stu-id="184d2-131">\<REDIRECT-URI> needs to be encoded for use in a URL.</span></span> <span data-ttu-id="184d2-132">Par conséquent, pour https://localhost, utilisez `https%3A%2F%2Flocalhost`)</span><span class="sxs-lookup"><span data-stu-id="184d2-132">So, for https://localhost, use `https%3A%2F%2Flocalhost`)</span></span>
   > 
   > 
   
    <span data-ttu-id="184d2-133">Pour les besoins de ce didacticiel, vous pouvez remplacer les valeurs d’espace réservé de l’URL ci-dessus et la coller dans la barre d’adresse d’un navigateur web.</span><span class="sxs-lookup"><span data-stu-id="184d2-133">For the purpose of this tutorial, you can replace the placeholder values in the URL above and paste it in a web browser's address bar.</span></span> <span data-ttu-id="184d2-134">Vous serez redirigé pour vous authentifier à l’aide de vos informations de connexion Azure.</span><span class="sxs-lookup"><span data-stu-id="184d2-134">You will be redirected to authenticate using your Azure login.</span></span> <span data-ttu-id="184d2-135">Lorsque vous êtes connecté, la réponse s’affiche dans la barre d’adresse du navigateur.</span><span class="sxs-lookup"><span data-stu-id="184d2-135">Once you successfully log in, the response is displayed in the browser's address bar.</span></span> <span data-ttu-id="184d2-136">La réponse présente le format suivant :</span><span class="sxs-lookup"><span data-stu-id="184d2-136">The response will be in the following format:</span></span>
   
        http://localhost/?code=<AUTHORIZATION-CODE>&session_state=<GUID>
2. <span data-ttu-id="184d2-137">Capturez le code d’autorisation de la réponse.</span><span class="sxs-lookup"><span data-stu-id="184d2-137">Capture the authorization code from the response.</span></span> <span data-ttu-id="184d2-138">Pour ce didacticiel, vous pouvez copier le code d’autorisation de la barre d’adresse du navigateur web et le transmettre dans la demande POST au point de terminaison de jeton, comme indiqué ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="184d2-138">For this tutorial, you can copy the authorization code from the address bar of the web browser and pass it in the POST request to the token endpoint, as shown below:</span></span>
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token \
        -F redirect_uri=<REDIRECT-URI> \
        -F grant_type=authorization_code \
        -F resource=https://management.core.windows.net/ \
        -F client_id=<APPLICATION-ID> \
        -F code=<AUTHORIZATION-CODE>
   
   > [!NOTE]
   > <span data-ttu-id="184d2-139">Dans ce cas, il n’est pas nécessaire de coder l’URI \<REDIRECT-URI>.</span><span class="sxs-lookup"><span data-stu-id="184d2-139">In this case, the \<REDIRECT-URI> need not be encoded.</span></span>
   > 
   > 
3. <span data-ttu-id="184d2-140">La réponse est un objet JSON contenant un jeton d’accès (par exemple, `"access_token": "<ACCESS_TOKEN>"`) et un jeton d’actualisation (par exemple, `"refresh_token": "<REFRESH_TOKEN>"`).</span><span class="sxs-lookup"><span data-stu-id="184d2-140">The response is a JSON object that contains an access token (e.g., `"access_token": "<ACCESS_TOKEN>"`) and a refresh token (e.g., `"refresh_token": "<REFRESH_TOKEN>"`).</span></span> <span data-ttu-id="184d2-141">Votre application utilise le jeton d’accès pour accéder à Azure Data Lake Store et le jeton d’actualisation pour obtenir un autre jeton d’accès lorsque l’un d’eux expire.</span><span class="sxs-lookup"><span data-stu-id="184d2-141">Your application uses the access token when accessing Azure Data Lake Store and the refresh token to get another access token when an access token expires.</span></span>
   
        {"token_type":"Bearer","scope":"user_impersonation","expires_in":"3599","expires_on":"1461865782","not_before":    "1461861882","resource":"https://management.core.windows.net/","access_token":"<REDACTED>","refresh_token":"<REDACTED>","id_token":"<REDACTED>"}
4. <span data-ttu-id="184d2-142">Lorsque le jeton d’accès arrive à expiration, vous pouvez demander un nouveau jeton d’accès à l’aide du jeton d’actualisation, comme indiqué ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="184d2-142">When the access token expires, you can request a new access token using the refresh token, as shown below:</span></span>
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
             -F grant_type=refresh_token \
             -F resource=https://management.core.windows.net/ \
             -F client_id=<APPLICATION-ID> \
             -F refresh_token=<REFRESH-TOKEN>

<span data-ttu-id="184d2-143">Pour plus d’informations sur l’authentification utilisateur interactive, consultez [Flux d’octroi d’un code d’autorisation](https://msdn.microsoft.com/library/azure/dn645542.aspx).</span><span class="sxs-lookup"><span data-stu-id="184d2-143">For more information on interactive user authentication, see [Authorization code grant flow](https://msdn.microsoft.com/library/azure/dn645542.aspx).</span></span>

### <a name="service-to-service-authentication-non-interactive"></a><span data-ttu-id="184d2-144">Authentification de service à service (non interactive)</span><span class="sxs-lookup"><span data-stu-id="184d2-144">Service-to-service authentication (non-interactive)</span></span>
<span data-ttu-id="184d2-145">Dans ce scénario, l’application fournit ses propres informations d’identification pour effectuer les opérations.</span><span class="sxs-lookup"><span data-stu-id="184d2-145">In this scenario, the the application provides its own credentials to perform the operations.</span></span> <span data-ttu-id="184d2-146">Avec cette méthode, vous devez émettre une demande POST, comme celle illustrée ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="184d2-146">For this, you must issue a POST request like the one shown below.</span></span> 

    curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
      -F grant_type=client_credentials \
      -F resource=https://management.core.windows.net/ \
      -F client_id=<CLIENT-ID> \
      -F client_secret=<AUTH-KEY>

<span data-ttu-id="184d2-147">La sortie de cette demande inclut un jeton d’autorisation (indiqué par `access-token` dans la sortie ci-dessous) que vous allez ensuite passer avec vos appels d’API REST.</span><span class="sxs-lookup"><span data-stu-id="184d2-147">The output of this request will include an authorization token (denoted by `access-token` in the output below) that you will subsequently pass with your REST API calls.</span></span> <span data-ttu-id="184d2-148">Enregistrez ce jeton d’authentification dans un fichier texte, car vous en aurez besoin plus loin dans cet article.</span><span class="sxs-lookup"><span data-stu-id="184d2-148">Save this authentication token in a text file; you will need this later in this article.</span></span>

    {"token_type":"Bearer","expires_in":"3599","expires_on":"1458245447","not_before":"1458241547","resource":"https://management.core.windows.net/","access_token":"<REDACTED>"}

<span data-ttu-id="184d2-149">Cet article utilise la méthode **non interactive** .</span><span class="sxs-lookup"><span data-stu-id="184d2-149">This article uses the **non-interactive** approach.</span></span> <span data-ttu-id="184d2-150">Pour plus d’informations sur l’authentification non interactive (appels de service à service), consultez [Appels de service à service à l’aide d’informations d’identification](https://msdn.microsoft.com/library/azure/dn645543.aspx).</span><span class="sxs-lookup"><span data-stu-id="184d2-150">For more information on non-interactive (service-to-service calls), see [Service to service calls using credentials](https://msdn.microsoft.com/library/azure/dn645543.aspx).</span></span>

## <a name="create-a-data-lake-store-account"></a><span data-ttu-id="184d2-151">Créer un compte Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="184d2-151">Create a Data Lake Store account</span></span>
<span data-ttu-id="184d2-152">Cette opération est basée sur l’appel d’API REST défini [ici](https://msdn.microsoft.com/library/mt694078.aspx).</span><span class="sxs-lookup"><span data-stu-id="184d2-152">This operation is based on the REST API call defined [here](https://msdn.microsoft.com/library/mt694078.aspx).</span></span>

<span data-ttu-id="184d2-153">Utilisez la commande cURL suivante.</span><span class="sxs-lookup"><span data-stu-id="184d2-153">Use the following cURL command.</span></span> <span data-ttu-id="184d2-154">Remplacez **\<yourstorename>** par le nom de votre Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="184d2-154">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -H "Content-Type: application/json" https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.DataLakeStore/accounts/<yourstorename>?api-version=2015-10-01-preview -d@"C:\temp\input.json"

<span data-ttu-id="184d2-155">Dans la commande ci-dessus, remplacez \<`REDACTED`\> par le jeton d’autorisation que vous avez récupéré précédemment.</span><span class="sxs-lookup"><span data-stu-id="184d2-155">In the above command, replace \<`REDACTED`\> with the authorization token you retrieved earlier.</span></span> <span data-ttu-id="184d2-156">La charge utile de la demande pour cette commande est contenue dans le fichier **input.json** fourni pour le paramètre `-d` ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="184d2-156">The request payload for this command is contained in the **input.json** file that is provided for the `-d` parameter above.</span></span> <span data-ttu-id="184d2-157">Le contenu du fichier input.json ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="184d2-157">The contents of the input.json file resemble the following:</span></span>

    {
    "location": "eastus2",
    "tags": {
        "department": "finance"
        },
    "properties": {}
    }    

## <a name="create-folders-in-a-data-lake-store-account"></a><span data-ttu-id="184d2-158">Créer des dossiers dans un compte Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="184d2-158">Create folders in a Data Lake Store account</span></span>
<span data-ttu-id="184d2-159">Cette opération est basée sur l’appel de l’API REST de WebHDFS défini [ici](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Make_a_Directory).</span><span class="sxs-lookup"><span data-stu-id="184d2-159">This operation is based on the WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Make_a_Directory).</span></span>

<span data-ttu-id="184d2-160">Utilisez la commande cURL suivante.</span><span class="sxs-lookup"><span data-stu-id="184d2-160">Use the following cURL command.</span></span> <span data-ttu-id="184d2-161">Remplacez **\<yourstorename>** par le nom de votre Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="184d2-161">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -d "" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/?op=MKDIRS'

<span data-ttu-id="184d2-162">Dans la commande ci-dessus, remplacez \<`REDACTED`\> par le jeton d’autorisation que vous avez récupéré précédemment.</span><span class="sxs-lookup"><span data-stu-id="184d2-162">In the above command, replace \<`REDACTED`\> with the authorization token you retrieved earlier.</span></span> <span data-ttu-id="184d2-163">Cette commande crée un répertoire appelé **mytempdir** sous le dossier racine de votre compte Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="184d2-163">This command creates a directory called **mytempdir** under the root folder of your Data Lake Store account.</span></span>

<span data-ttu-id="184d2-164">Si l’opération s’est déroulée correctement, vous devez voir une réponse similaire à celle-ci :</span><span class="sxs-lookup"><span data-stu-id="184d2-164">You should see a response like this if the operation completes successfully:</span></span>

    {"boolean":true}

## <a name="list-folders-in-a-data-lake-store-account"></a><span data-ttu-id="184d2-165">Afficher la liste des dossiers dans un compte Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="184d2-165">List folders in a Data Lake Store account</span></span>
<span data-ttu-id="184d2-166">Cette opération est basée sur l’appel de l’API REST de WebHDFS défini [ici](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#List_a_Directory).</span><span class="sxs-lookup"><span data-stu-id="184d2-166">This operation is based on the WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#List_a_Directory).</span></span>

<span data-ttu-id="184d2-167">Utilisez la commande cURL suivante.</span><span class="sxs-lookup"><span data-stu-id="184d2-167">Use the following cURL command.</span></span> <span data-ttu-id="184d2-168">Remplacez **\<yourstorename>** par le nom de votre Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="184d2-168">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/?op=LISTSTATUS'

<span data-ttu-id="184d2-169">Dans la commande ci-dessus, remplacez \<`REDACTED`\> par le jeton d’autorisation que vous avez récupéré précédemment.</span><span class="sxs-lookup"><span data-stu-id="184d2-169">In the above command, replace \<`REDACTED`\> with the authorization token you retrieved earlier.</span></span>

<span data-ttu-id="184d2-170">Si l’opération s’est déroulée correctement, vous devez voir une réponse similaire à celle-ci :</span><span class="sxs-lookup"><span data-stu-id="184d2-170">You should see a response like this if the operation completes successfully:</span></span>

    {
    "FileStatuses": {
        "FileStatus": [{
            "length": 0,
            "pathSuffix": "mytempdir",
            "type": "DIRECTORY",
            "blockSize": 268435456,
            "accessTime": 1458324719512,
            "modificationTime": 1458324719512,
            "replication": 0,
            "permission": "777",
            "owner": "NotSupportYet",
            "group": "NotSupportYet"
        }]
    }
    }

## <a name="upload-data-into-a-data-lake-store-account"></a><span data-ttu-id="184d2-171">Charger des données dans un compte Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="184d2-171">Upload data into a Data Lake Store account</span></span>
<span data-ttu-id="184d2-172">Cette opération est basée sur l’appel de l’API REST de WebHDFS défini [ici](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Create_and_Write_to_a_File).</span><span class="sxs-lookup"><span data-stu-id="184d2-172">This operation is based on the WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Create_and_Write_to_a_File).</span></span>

<span data-ttu-id="184d2-173">Utilisez la commande cURL suivante.</span><span class="sxs-lookup"><span data-stu-id="184d2-173">Use the following cURL command.</span></span> <span data-ttu-id="184d2-174">Remplacez **\<yourstorename>** par le nom de votre Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="184d2-174">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X PUT -L -T 'C:\temp\list.txt' -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/list.txt?op=CREATE'

<span data-ttu-id="184d2-175">Dans la syntaxe ci-dessus, le paramètre **-T** correspond à l’emplacement du fichier que vous chargez.</span><span class="sxs-lookup"><span data-stu-id="184d2-175">In the above syntax **-T** parameter is the location of the file you are uploading.</span></span>

<span data-ttu-id="184d2-176">Le résultat ressemble à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="184d2-176">The output is similar to the following:</span></span>
   
    HTTP/1.1 307 Temporary Redirect
    ...
    Location: https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/list.txt?op=CREATE&write=true
    ...
    Content-Length: 0

    HTTP/1.1 100 Continue

    HTTP/1.1 201 Created
    ...

## <a name="read-data-from-a-data-lake-store-account"></a><span data-ttu-id="184d2-177">Lire les données d’un compte Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="184d2-177">Read data from a Data Lake Store account</span></span>
<span data-ttu-id="184d2-178">Cette opération est basée sur l’appel de l’API REST de WebHDFS défini [ici](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Open_and_Read_a_File).</span><span class="sxs-lookup"><span data-stu-id="184d2-178">This operation is based on the WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Open_and_Read_a_File).</span></span>

<span data-ttu-id="184d2-179">La lecture des données d’un compte Data Lake Store s’effectue en deux étapes.</span><span class="sxs-lookup"><span data-stu-id="184d2-179">Reading data from a Data Lake Store account is a two-step process.</span></span>

* <span data-ttu-id="184d2-180">D’abord, envoyez une demande GET sur le point de terminaison `https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN`.</span><span class="sxs-lookup"><span data-stu-id="184d2-180">You first submit a GET request against the endpoint `https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN`.</span></span> <span data-ttu-id="184d2-181">Cette opération retourne un emplacement où envoyer la demande GET suivante.</span><span class="sxs-lookup"><span data-stu-id="184d2-181">This will return a location to submit the next GET request to.</span></span>
* <span data-ttu-id="184d2-182">Ensuite, envoyez la deuxième demande GET sur le point de terminaison `https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN&read=true`.</span><span class="sxs-lookup"><span data-stu-id="184d2-182">You then submit the GET request against the endpoint `https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN&read=true`.</span></span> <span data-ttu-id="184d2-183">Cette opération affiche le contenu du fichier.</span><span class="sxs-lookup"><span data-stu-id="184d2-183">This will display the contents of the file.</span></span>

<span data-ttu-id="184d2-184">Toutefois, comme les paramètres d’entrée sont les mêmes pour la première et la deuxième étape, vous pouvez utiliser le paramètre `-L` pour envoyer la première demande.</span><span class="sxs-lookup"><span data-stu-id="184d2-184">However, because there is no difference in the input parameters between the first and the second step, you can use the `-L` parameter to submit the first request.</span></span> <span data-ttu-id="184d2-185">`-L` permet essentiellement de combiner les deux demandes en une seule et d’indiquer à cURL de réexécuter la demande sur le nouvel emplacement.</span><span class="sxs-lookup"><span data-stu-id="184d2-185">`-L` option essentially combines two requests into one and will make cURL redo the request on the new location.</span></span> <span data-ttu-id="184d2-186">La sortie finale de tous les appels de la demande s’affiche, comme illustrée ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="184d2-186">Finally, the output from all the request calls is displayed, like shown below.</span></span> <span data-ttu-id="184d2-187">Remplacez **\<yourstorename>** par le nom de votre Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="184d2-187">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -L GET -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN'

<span data-ttu-id="184d2-188">Le résultat doit ressembler à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="184d2-188">You should see an output similar to the following:</span></span>

    HTTP/1.1 307 Temporary Redirect
    ...
    Location: https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/somerandomfile.txt?op=OPEN&read=true
    ...

    HTTP/1.1 200 OK
    ...

    Hello, Data Lake Store user!

## <a name="rename-a-file-in-a-data-lake-store-account"></a><span data-ttu-id="184d2-189">Renommer un fichier dans un compte Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="184d2-189">Rename a file in a Data Lake Store account</span></span>
<span data-ttu-id="184d2-190">Cette opération est basée sur l’appel de l’API REST de WebHDFS défini [ici](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Rename_a_FileDirectory).</span><span class="sxs-lookup"><span data-stu-id="184d2-190">This operation is based on the WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Rename_a_FileDirectory).</span></span>

<span data-ttu-id="184d2-191">Utilisez la commande cURL suivante pour renommer un fichier.</span><span class="sxs-lookup"><span data-stu-id="184d2-191">Use the following cURL command to rename a file.</span></span> <span data-ttu-id="184d2-192">Remplacez **\<yourstorename>** par le nom de votre Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="184d2-192">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -d "" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=RENAME&destination=/mytempdir/myinputfile1.txt'

<span data-ttu-id="184d2-193">Le résultat doit ressembler à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="184d2-193">You should see an output similar to the following:</span></span>

    HTTP/1.1 200 OK
    ...

    {"boolean":true}

## <a name="delete-a-file-from-a-data-lake-store-account"></a><span data-ttu-id="184d2-194">Supprimer un fichier dans un compte Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="184d2-194">Delete a file from a Data Lake Store account</span></span>
<span data-ttu-id="184d2-195">Cette opération est basée sur l’appel de l’API REST de WebHDFS défini [ici](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Delete_a_FileDirectory).</span><span class="sxs-lookup"><span data-stu-id="184d2-195">This operation is based on the WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Delete_a_FileDirectory).</span></span>

<span data-ttu-id="184d2-196">Utilisez la commande cURL suivante pour supprimer un fichier.</span><span class="sxs-lookup"><span data-stu-id="184d2-196">Use the following cURL command to delete a file.</span></span> <span data-ttu-id="184d2-197">Remplacez **\<yourstorename>** par le nom de votre Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="184d2-197">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X DELETE -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile1.txt?op=DELETE'

<span data-ttu-id="184d2-198">Un résultat similaire à ce qui suit s’affiche normalement :</span><span class="sxs-lookup"><span data-stu-id="184d2-198">You should see an output like the following:</span></span>

    HTTP/1.1 200 OK
    ...

    {"boolean":true}

## <a name="delete-a-data-lake-store-account"></a><span data-ttu-id="184d2-199">Supprimer un compte Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="184d2-199">Delete a Data Lake Store account</span></span>
<span data-ttu-id="184d2-200">Cette opération est basée sur l’appel d’API REST défini [ici](https://msdn.microsoft.com/library/mt694075.aspx).</span><span class="sxs-lookup"><span data-stu-id="184d2-200">This operation is based on the REST API call defined [here](https://msdn.microsoft.com/library/mt694075.aspx).</span></span>

<span data-ttu-id="184d2-201">Utilisez la commande cURL suivante pour supprimer un compte Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="184d2-201">Use the following cURL command to delete a Data Lake Store account.</span></span> <span data-ttu-id="184d2-202">Remplacez **\<yourstorename>** par le nom de votre Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="184d2-202">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X DELETE -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.DataLakeStore/accounts/<yourstorename>?api-version=2015-10-01-preview

<span data-ttu-id="184d2-203">Un résultat similaire à ce qui suit s’affiche normalement :</span><span class="sxs-lookup"><span data-stu-id="184d2-203">You should see an output like the following:</span></span>

    HTTP/1.1 200 OK
    ...
    ...

## <a name="see-also"></a><span data-ttu-id="184d2-204">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="184d2-204">See also</span></span>
* [<span data-ttu-id="184d2-205">Ouvrir des applications Big Data open source compatibles avec Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="184d2-205">Open Source Big Data applications compatible with Azure Data Lake Store</span></span>](data-lake-store-compatible-oss-other-applications.md)

