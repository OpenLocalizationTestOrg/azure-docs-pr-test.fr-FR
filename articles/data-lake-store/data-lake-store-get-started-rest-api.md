---
title: aaaUse hello API REST tooget main Data Lake Store | Documents Microsoft
description: "Utilisez des opérations de tooperform WebHDFS REST API sur Data Lake Store"
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
ms.openlocfilehash: 62fce8293dfee730a61f2a3d37fc138ce7c3afdf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-rest-apis"></a><span data-ttu-id="7a013-103">Prise en main d’Azure Data Lake Store avec les API REST</span><span class="sxs-lookup"><span data-stu-id="7a013-103">Get started with Azure Data Lake Store using REST APIs</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7a013-104">Portail</span><span class="sxs-lookup"><span data-stu-id="7a013-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="7a013-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7a013-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="7a013-106">Kit SDK .NET</span><span class="sxs-lookup"><span data-stu-id="7a013-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="7a013-107">Kit SDK Java</span><span class="sxs-lookup"><span data-stu-id="7a013-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="7a013-108">API REST</span><span class="sxs-lookup"><span data-stu-id="7a013-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="7a013-109">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="7a013-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="7a013-110">Node.JS</span><span class="sxs-lookup"><span data-stu-id="7a013-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="7a013-111">Python</span><span class="sxs-lookup"><span data-stu-id="7a013-111">Python</span></span>](data-lake-store-get-started-python.md)
>
> 

<span data-ttu-id="7a013-112">Dans cet article, vous allez apprendre comment toouse WebHDFS REST API et API REST de données Lake Store tooperform compte d’administration ainsi que des opérations de système de fichiers sur Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="7a013-112">In this article, you will learn how toouse WebHDFS REST APIs and Data Lake Store REST APIs tooperform account management as well as filesystem operations on Azure Data Lake Store.</span></span> <span data-ttu-id="7a013-113">Azure Data Lake Store expose ses propres API REST pour les opérations de gestion des comptes.</span><span class="sxs-lookup"><span data-stu-id="7a013-113">Azure Data Lake Store exposes its own REST APIs for account management operations.</span></span> <span data-ttu-id="7a013-114">Toutefois, comme Data Lake Store est compatible avec HDFS et l’écosystème Hadoop, il prend en charge l’utilisation des API REST de WebHDFS pour les opérations de système de fichiers.</span><span class="sxs-lookup"><span data-stu-id="7a013-114">However, because Data Lake Store is compatible with HDFS and Hadoop ecosystem, it supports using WebHDFS REST APIs for filesystem operations.</span></span>

> [!NOTE]
> <span data-ttu-id="7a013-115">Pour plus d’informations sur la prise en charge des API REST de hello pour Data Lake Store, consultez [référence d’API REST Azure données Lake Store](https://msdn.microsoft.com/library/mt693424.aspx).</span><span class="sxs-lookup"><span data-stu-id="7a013-115">For detailed information on hello REST API support for Data Lake Store, see [Azure Data Lake Store REST API Reference](https://msdn.microsoft.com/library/mt693424.aspx).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="7a013-116">Composants requis</span><span class="sxs-lookup"><span data-stu-id="7a013-116">Prerequisites</span></span>
* <span data-ttu-id="7a013-117">**Un abonnement Azure**.</span><span class="sxs-lookup"><span data-stu-id="7a013-117">**An Azure subscription**.</span></span> <span data-ttu-id="7a013-118">Consultez la page [Obtention d’un essai gratuit d’Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7a013-118">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="7a013-119">**Créez une application Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7a013-119">**Create an Azure Active Directory Application**.</span></span> <span data-ttu-id="7a013-120">Vous utilisez hello Azure AD tooauthenticate hello Data Lake Store une application avec Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7a013-120">You use hello Azure AD application tooauthenticate hello Data Lake Store application with Azure AD.</span></span> <span data-ttu-id="7a013-121">Il existe tooauthenticate différentes approches avec Azure AD, qui sont **l’authentification de l’utilisateur final** ou **l’authentification de service**.</span><span class="sxs-lookup"><span data-stu-id="7a013-121">There are different approaches tooauthenticate with Azure AD, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="7a013-122">Pour plus d’informations sur la façon d’et tooauthenticate, consultez [l’authentification de l’utilisateur final](data-lake-store-end-user-authenticate-using-active-directory.md) ou [l’authentification de service](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="7a013-122">For instructions and more information on how tooauthenticate, see [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md) or [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md).</span></span>
* <span data-ttu-id="7a013-123">[cURL](http://curl.haxx.se/).</span><span class="sxs-lookup"><span data-stu-id="7a013-123">[cURL](http://curl.haxx.se/).</span></span> <span data-ttu-id="7a013-124">Cet article utilise toodemonstrate cURL comment toomake API REST appelle par rapport à un compte Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="7a013-124">This article uses cURL toodemonstrate how toomake REST API calls against a Data Lake Store account.</span></span>

## <a name="how-do-i-authenticate-using-azure-active-directory"></a><span data-ttu-id="7a013-125">Comment s’authentifier à l’aide d’Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="7a013-125">How do I authenticate using Azure Active Directory?</span></span>
<span data-ttu-id="7a013-126">Vous pouvez utiliser deux approches tooauthenticate à l’aide d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7a013-126">You can use two approaches tooauthenticate using Azure Active Directory.</span></span>

### <a name="end-user-authentication-interactive"></a><span data-ttu-id="7a013-127">Authentification de l’utilisateur final (interactive)</span><span class="sxs-lookup"><span data-stu-id="7a013-127">End-user authentication (interactive)</span></span>
<span data-ttu-id="7a013-128">Dans ce scénario, application hello invite toolog d’utilisateur hello dans et toutes les opérations de hello sont effectuées dans le contexte de hello d’utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="7a013-128">In this scenario, hello application prompts hello user toolog in and all hello operations are performed in hello context of hello user.</span></span> <span data-ttu-id="7a013-129">Effectuer hello comme suit pour l’authentification interactive.</span><span class="sxs-lookup"><span data-stu-id="7a013-129">Perform hello following steps for interactive authentication.</span></span>

1. <span data-ttu-id="7a013-130">Via votre application, la redirection toohello d’utilisateur hello suivant l’URL :</span><span class="sxs-lookup"><span data-stu-id="7a013-130">Through your application, redirect hello user toohello following URL:</span></span>
   
        https://login.microsoftonline.com/<TENANT-ID>/oauth2/authorize?client_id=<APPLICATION-ID>&response_type=code&redirect_uri=<REDIRECT-URI>
   
   > [!NOTE]
   > <span data-ttu-id="7a013-131">\<URI de redirection > doit toobe codé à utiliser dans une URL.</span><span class="sxs-lookup"><span data-stu-id="7a013-131">\<REDIRECT-URI> needs toobe encoded for use in a URL.</span></span> <span data-ttu-id="7a013-132">Par conséquent, pour https://localhost, utilisez `https%3A%2F%2Flocalhost`)</span><span class="sxs-lookup"><span data-stu-id="7a013-132">So, for https://localhost, use `https%3A%2F%2Flocalhost`)</span></span>
   > 
   > 
   
    <span data-ttu-id="7a013-133">Fins hello de ce didacticiel, vous pouvez remplacer les valeurs d’espace réservé hello URL hello ci-dessus et collez-le dans la barre d’adresses d’un navigateur web.</span><span class="sxs-lookup"><span data-stu-id="7a013-133">For hello purpose of this tutorial, you can replace hello placeholder values in hello URL above and paste it in a web browser's address bar.</span></span> <span data-ttu-id="7a013-134">Vous serez redirigé tooauthenticate à l’aide de votre connexion à Azure.</span><span class="sxs-lookup"><span data-stu-id="7a013-134">You will be redirected tooauthenticate using your Azure login.</span></span> <span data-ttu-id="7a013-135">Une fois que vous connecter avec succès, réponse de hello est affichée dans la barre d’adresses du navigateur hello.</span><span class="sxs-lookup"><span data-stu-id="7a013-135">Once you successfully log in, hello response is displayed in hello browser's address bar.</span></span> <span data-ttu-id="7a013-136">réponse de Hello sera Bonjour suivant le format :</span><span class="sxs-lookup"><span data-stu-id="7a013-136">hello response will be in hello following format:</span></span>
   
        http://localhost/?code=<AUTHORIZATION-CODE>&session_state=<GUID>
2. <span data-ttu-id="7a013-137">Capturer le code d’autorisation de hello de réponse de hello.</span><span class="sxs-lookup"><span data-stu-id="7a013-137">Capture hello authorization code from hello response.</span></span> <span data-ttu-id="7a013-138">Pour ce didacticiel, vous pouvez copier le code d’autorisation de hello à partir de la barre d’adresses hello de navigateur hello et passer dans hello POST demande toohello jeton point de terminaison, comme indiqué ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="7a013-138">For this tutorial, you can copy hello authorization code from hello address bar of hello web browser and pass it in hello POST request toohello token endpoint, as shown below:</span></span>
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token \
        -F redirect_uri=<REDIRECT-URI> \
        -F grant_type=authorization_code \
        -F resource=https://management.core.windows.net/ \
        -F client_id=<APPLICATION-ID> \
        -F code=<AUTHORIZATION-CODE>
   
   > [!NOTE]
   > <span data-ttu-id="7a013-139">Dans ce cas, hello \<URI de redirection > ne doivent pas être encodé.</span><span class="sxs-lookup"><span data-stu-id="7a013-139">In this case, hello \<REDIRECT-URI> need not be encoded.</span></span>
   > 
   > 
3. <span data-ttu-id="7a013-140">réponse de Hello est un objet JSON qui contient un jeton d’accès (par exemple, `"access_token": "<ACCESS_TOKEN>"`) et un jeton d’actualisation (par exemple, `"refresh_token": "<REFRESH_TOKEN>"`).</span><span class="sxs-lookup"><span data-stu-id="7a013-140">hello response is a JSON object that contains an access token (e.g., `"access_token": "<ACCESS_TOKEN>"`) and a refresh token (e.g., `"refresh_token": "<REFRESH_TOKEN>"`).</span></span> <span data-ttu-id="7a013-141">Votre application utilise hello jeton d’accès lors de l’accès d’Azure Data Lake Store et tooget de jeton hello actualiser un autre jeton d’accès quand un jeton d’accès expire.</span><span class="sxs-lookup"><span data-stu-id="7a013-141">Your application uses hello access token when accessing Azure Data Lake Store and hello refresh token tooget another access token when an access token expires.</span></span>
   
        {"token_type":"Bearer","scope":"user_impersonation","expires_in":"3599","expires_on":"1461865782","not_before":    "1461861882","resource":"https://management.core.windows.net/","access_token":"<REDACTED>","refresh_token":"<REDACTED>","id_token":"<REDACTED>"}
4. <span data-ttu-id="7a013-142">Expiration du jeton d’accès hello, vous pouvez demander un nouveau jeton d’accès à l’aide du jeton d’actualisation hello, comme indiqué ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="7a013-142">When hello access token expires, you can request a new access token using hello refresh token, as shown below:</span></span>
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
             -F grant_type=refresh_token \
             -F resource=https://management.core.windows.net/ \
             -F client_id=<APPLICATION-ID> \
             -F refresh_token=<REFRESH-TOKEN>

<span data-ttu-id="7a013-143">Pour plus d’informations sur l’authentification utilisateur interactive, consultez [Flux d’octroi d’un code d’autorisation](https://msdn.microsoft.com/library/azure/dn645542.aspx).</span><span class="sxs-lookup"><span data-stu-id="7a013-143">For more information on interactive user authentication, see [Authorization code grant flow](https://msdn.microsoft.com/library/azure/dn645542.aspx).</span></span>

### <a name="service-to-service-authentication-non-interactive"></a><span data-ttu-id="7a013-144">Authentification de service à service (non interactive)</span><span class="sxs-lookup"><span data-stu-id="7a013-144">Service-to-service authentication (non-interactive)</span></span>
<span data-ttu-id="7a013-145">Dans ce scénario, application hello de hello fournit des opérations de hello tooperform ses propres informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="7a013-145">In this scenario, hello hello application provides its own credentials tooperform hello operations.</span></span> <span data-ttu-id="7a013-146">Pour ce faire, vous devez émettre une demande POST, comme illustré ci-dessous hello.</span><span class="sxs-lookup"><span data-stu-id="7a013-146">For this, you must issue a POST request like hello one shown below.</span></span> 

    curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
      -F grant_type=client_credentials \
      -F resource=https://management.core.windows.net/ \
      -F client_id=<CLIENT-ID> \
      -F client_secret=<AUTH-KEY>

<span data-ttu-id="7a013-147">sortie Hello de cette demande inclut un jeton d’autorisation (indiqué par `access-token` dans la sortie de hello ci-dessous) que vous allez transmettre ensuite avec vos appels d’API REST.</span><span class="sxs-lookup"><span data-stu-id="7a013-147">hello output of this request will include an authorization token (denoted by `access-token` in hello output below) that you will subsequently pass with your REST API calls.</span></span> <span data-ttu-id="7a013-148">Enregistrez ce jeton d’authentification dans un fichier texte, car vous en aurez besoin plus loin dans cet article.</span><span class="sxs-lookup"><span data-stu-id="7a013-148">Save this authentication token in a text file; you will need this later in this article.</span></span>

    {"token_type":"Bearer","expires_in":"3599","expires_on":"1458245447","not_before":"1458241547","resource":"https://management.core.windows.net/","access_token":"<REDACTED>"}

<span data-ttu-id="7a013-149">Cet article utilise hello **non interactif** approche.</span><span class="sxs-lookup"><span data-stu-id="7a013-149">This article uses hello **non-interactive** approach.</span></span> <span data-ttu-id="7a013-150">Pour plus d’informations sur la non interactif (appels de service), consultez [tooservice les appels à l’aide des informations d’identification de Service](https://msdn.microsoft.com/library/azure/dn645543.aspx).</span><span class="sxs-lookup"><span data-stu-id="7a013-150">For more information on non-interactive (service-to-service calls), see [Service tooservice calls using credentials](https://msdn.microsoft.com/library/azure/dn645543.aspx).</span></span>

## <a name="create-a-data-lake-store-account"></a><span data-ttu-id="7a013-151">Créer un compte Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="7a013-151">Create a Data Lake Store account</span></span>
<span data-ttu-id="7a013-152">Cette opération est basée sur les appels hello API REST défini [ici](https://msdn.microsoft.com/library/mt694078.aspx).</span><span class="sxs-lookup"><span data-stu-id="7a013-152">This operation is based on hello REST API call defined [here](https://msdn.microsoft.com/library/mt694078.aspx).</span></span>

<span data-ttu-id="7a013-153">Utilisez hello enroulement de la commande suivante.</span><span class="sxs-lookup"><span data-stu-id="7a013-153">Use hello following cURL command.</span></span> <span data-ttu-id="7a013-154">Remplacez **\<yourstorename>** par le nom de votre Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="7a013-154">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -H "Content-Type: application/json" https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.DataLakeStore/accounts/<yourstorename>?api-version=2015-10-01-preview -d@"C:\temp\input.json"

<span data-ttu-id="7a013-155">Bonjour au-dessus de commande, remplacez \< `REDACTED` \> avec le jeton d’autorisation hello extrait précédemment.</span><span class="sxs-lookup"><span data-stu-id="7a013-155">In hello above command, replace \<`REDACTED`\> with hello authorization token you retrieved earlier.</span></span> <span data-ttu-id="7a013-156">charge utile de demande Hello pour cette commande est contenue dans hello **input.json** fichier fourni pour hello `-d` paramètre ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="7a013-156">hello request payload for this command is contained in hello **input.json** file that is provided for hello `-d` parameter above.</span></span> <span data-ttu-id="7a013-157">contenu Hello du fichier de input.json hello ressemblent aux suivantes de hello :</span><span class="sxs-lookup"><span data-stu-id="7a013-157">hello contents of hello input.json file resemble hello following:</span></span>

    {
    "location": "eastus2",
    "tags": {
        "department": "finance"
        },
    "properties": {}
    }    

## <a name="create-folders-in-a-data-lake-store-account"></a><span data-ttu-id="7a013-158">Créer des dossiers dans un compte Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="7a013-158">Create folders in a Data Lake Store account</span></span>
<span data-ttu-id="7a013-159">Cette opération est basée sur appel hello API REST de WebHDFS défini [ici](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Make_a_Directory).</span><span class="sxs-lookup"><span data-stu-id="7a013-159">This operation is based on hello WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Make_a_Directory).</span></span>

<span data-ttu-id="7a013-160">Utilisez hello enroulement de la commande suivante.</span><span class="sxs-lookup"><span data-stu-id="7a013-160">Use hello following cURL command.</span></span> <span data-ttu-id="7a013-161">Remplacez **\<yourstorename>** par le nom de votre Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="7a013-161">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -d "" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/?op=MKDIRS'

<span data-ttu-id="7a013-162">Bonjour au-dessus de commande, remplacez \< `REDACTED` \> avec le jeton d’autorisation hello extrait précédemment.</span><span class="sxs-lookup"><span data-stu-id="7a013-162">In hello above command, replace \<`REDACTED`\> with hello authorization token you retrieved earlier.</span></span> <span data-ttu-id="7a013-163">Cette commande crée un répertoire appelé **mytempdir** sous le dossier racine de hello de votre compte Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="7a013-163">This command creates a directory called **mytempdir** under hello root folder of your Data Lake Store account.</span></span>

<span data-ttu-id="7a013-164">Vous devez voir une réponse similaire à ceci si l’opération de hello terminée :</span><span class="sxs-lookup"><span data-stu-id="7a013-164">You should see a response like this if hello operation completes successfully:</span></span>

    {"boolean":true}

## <a name="list-folders-in-a-data-lake-store-account"></a><span data-ttu-id="7a013-165">Afficher la liste des dossiers dans un compte Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="7a013-165">List folders in a Data Lake Store account</span></span>
<span data-ttu-id="7a013-166">Cette opération est basée sur appel hello API REST de WebHDFS défini [ici](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#List_a_Directory).</span><span class="sxs-lookup"><span data-stu-id="7a013-166">This operation is based on hello WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#List_a_Directory).</span></span>

<span data-ttu-id="7a013-167">Utilisez hello enroulement de la commande suivante.</span><span class="sxs-lookup"><span data-stu-id="7a013-167">Use hello following cURL command.</span></span> <span data-ttu-id="7a013-168">Remplacez **\<yourstorename>** par le nom de votre Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="7a013-168">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/?op=LISTSTATUS'

<span data-ttu-id="7a013-169">Bonjour au-dessus de commande, remplacez \< `REDACTED` \> avec le jeton d’autorisation hello extrait précédemment.</span><span class="sxs-lookup"><span data-stu-id="7a013-169">In hello above command, replace \<`REDACTED`\> with hello authorization token you retrieved earlier.</span></span>

<span data-ttu-id="7a013-170">Vous devez voir une réponse similaire à ceci si l’opération de hello terminée :</span><span class="sxs-lookup"><span data-stu-id="7a013-170">You should see a response like this if hello operation completes successfully:</span></span>

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

## <a name="upload-data-into-a-data-lake-store-account"></a><span data-ttu-id="7a013-171">Charger des données dans un compte Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="7a013-171">Upload data into a Data Lake Store account</span></span>
<span data-ttu-id="7a013-172">Cette opération est basée sur appel hello API REST de WebHDFS défini [ici](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Create_and_Write_to_a_File).</span><span class="sxs-lookup"><span data-stu-id="7a013-172">This operation is based on hello WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Create_and_Write_to_a_File).</span></span>

<span data-ttu-id="7a013-173">Utilisez hello enroulement de la commande suivante.</span><span class="sxs-lookup"><span data-stu-id="7a013-173">Use hello following cURL command.</span></span> <span data-ttu-id="7a013-174">Remplacez **\<yourstorename>** par le nom de votre Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="7a013-174">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X PUT -L -T 'C:\temp\list.txt' -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/list.txt?op=CREATE'

<span data-ttu-id="7a013-175">Bonjour ci-dessus syntaxe **-T** paramètre est l’emplacement hello du fichier hello vous téléchargez.</span><span class="sxs-lookup"><span data-stu-id="7a013-175">In hello above syntax **-T** parameter is hello location of hello file you are uploading.</span></span>

<span data-ttu-id="7a013-176">sortie de Hello est similaire toohello suivantes :</span><span class="sxs-lookup"><span data-stu-id="7a013-176">hello output is similar toohello following:</span></span>
   
    HTTP/1.1 307 Temporary Redirect
    ...
    Location: https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/list.txt?op=CREATE&write=true
    ...
    Content-Length: 0

    HTTP/1.1 100 Continue

    HTTP/1.1 201 Created
    ...

## <a name="read-data-from-a-data-lake-store-account"></a><span data-ttu-id="7a013-177">Lire les données d’un compte Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="7a013-177">Read data from a Data Lake Store account</span></span>
<span data-ttu-id="7a013-178">Cette opération est basée sur appel hello API REST de WebHDFS défini [ici](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Open_and_Read_a_File).</span><span class="sxs-lookup"><span data-stu-id="7a013-178">This operation is based on hello WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Open_and_Read_a_File).</span></span>

<span data-ttu-id="7a013-179">La lecture des données d’un compte Data Lake Store s’effectue en deux étapes.</span><span class="sxs-lookup"><span data-stu-id="7a013-179">Reading data from a Data Lake Store account is a two-step process.</span></span>

* <span data-ttu-id="7a013-180">D’abord vous envoyez une demande GET sur le point de terminaison hello `https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN`.</span><span class="sxs-lookup"><span data-stu-id="7a013-180">You first submit a GET request against hello endpoint `https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN`.</span></span> <span data-ttu-id="7a013-181">Cette méthode retourne une emplacement toosubmit hello suivante demande GET pour.</span><span class="sxs-lookup"><span data-stu-id="7a013-181">This will return a location toosubmit hello next GET request to.</span></span>
* <span data-ttu-id="7a013-182">Vous puis demander hello GET sur le point de terminaison hello `https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN&read=true`.</span><span class="sxs-lookup"><span data-stu-id="7a013-182">You then submit hello GET request against hello endpoint `https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN&read=true`.</span></span> <span data-ttu-id="7a013-183">Cette action affiche le contenu hello du fichier de hello.</span><span class="sxs-lookup"><span data-stu-id="7a013-183">This will display hello contents of hello file.</span></span>

<span data-ttu-id="7a013-184">Toutefois, les, car il n’existe aucune différence hello des paramètres d’entrée entre hello hello et tout d’abord deuxième étape, vous pouvez utiliser les hello `-L` première demande paramètre toosubmit hello.</span><span class="sxs-lookup"><span data-stu-id="7a013-184">However, because there is no difference in hello input parameters between hello first and hello second step, you can use hello `-L` parameter toosubmit hello first request.</span></span> <span data-ttu-id="7a013-185">`-L`option essentiellement combine deux requêtes en une seule et fera cURL demande hello sur le nouvel emplacement de hello de restauration par progression.</span><span class="sxs-lookup"><span data-stu-id="7a013-185">`-L` option essentially combines two requests into one and will make cURL redo hello request on hello new location.</span></span> <span data-ttu-id="7a013-186">Enfin, hello de tous les appels de demande hello est affiché, comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="7a013-186">Finally, hello output from all hello request calls is displayed, like shown below.</span></span> <span data-ttu-id="7a013-187">Remplacez **\<yourstorename>** par le nom de votre Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="7a013-187">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -L GET -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN'

<span data-ttu-id="7a013-188">Vous devez voir s’afficher une sortie similaire toohello :</span><span class="sxs-lookup"><span data-stu-id="7a013-188">You should see an output similar toohello following:</span></span>

    HTTP/1.1 307 Temporary Redirect
    ...
    Location: https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/somerandomfile.txt?op=OPEN&read=true
    ...

    HTTP/1.1 200 OK
    ...

    Hello, Data Lake Store user!

## <a name="rename-a-file-in-a-data-lake-store-account"></a><span data-ttu-id="7a013-189">Renommer un fichier dans un compte Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="7a013-189">Rename a file in a Data Lake Store account</span></span>
<span data-ttu-id="7a013-190">Cette opération est basée sur appel hello API REST de WebHDFS défini [ici](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Rename_a_FileDirectory).</span><span class="sxs-lookup"><span data-stu-id="7a013-190">This operation is based on hello WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Rename_a_FileDirectory).</span></span>

<span data-ttu-id="7a013-191">Suivant de hello utilisez cURL commande toorename un fichier.</span><span class="sxs-lookup"><span data-stu-id="7a013-191">Use hello following cURL command toorename a file.</span></span> <span data-ttu-id="7a013-192">Remplacez **\<yourstorename>** par le nom de votre Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="7a013-192">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -d "" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=RENAME&destination=/mytempdir/myinputfile1.txt'

<span data-ttu-id="7a013-193">Vous devez voir s’afficher une sortie similaire toohello :</span><span class="sxs-lookup"><span data-stu-id="7a013-193">You should see an output similar toohello following:</span></span>

    HTTP/1.1 200 OK
    ...

    {"boolean":true}

## <a name="delete-a-file-from-a-data-lake-store-account"></a><span data-ttu-id="7a013-194">Supprimer un fichier dans un compte Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="7a013-194">Delete a file from a Data Lake Store account</span></span>
<span data-ttu-id="7a013-195">Cette opération est basée sur appel hello API REST de WebHDFS défini [ici](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Delete_a_FileDirectory).</span><span class="sxs-lookup"><span data-stu-id="7a013-195">This operation is based on hello WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Delete_a_FileDirectory).</span></span>

<span data-ttu-id="7a013-196">Suivant de hello utilisez cURL commande toodelete un fichier.</span><span class="sxs-lookup"><span data-stu-id="7a013-196">Use hello following cURL command toodelete a file.</span></span> <span data-ttu-id="7a013-197">Remplacez **\<yourstorename>** par le nom de votre Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="7a013-197">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X DELETE -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile1.txt?op=DELETE'

<span data-ttu-id="7a013-198">Vous devez voir une sortie semblable à hello suivante :</span><span class="sxs-lookup"><span data-stu-id="7a013-198">You should see an output like hello following:</span></span>

    HTTP/1.1 200 OK
    ...

    {"boolean":true}

## <a name="delete-a-data-lake-store-account"></a><span data-ttu-id="7a013-199">Supprimer un compte Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="7a013-199">Delete a Data Lake Store account</span></span>
<span data-ttu-id="7a013-200">Cette opération est basée sur les appels hello API REST défini [ici](https://msdn.microsoft.com/library/mt694075.aspx).</span><span class="sxs-lookup"><span data-stu-id="7a013-200">This operation is based on hello REST API call defined [here](https://msdn.microsoft.com/library/mt694075.aspx).</span></span>

<span data-ttu-id="7a013-201">Suivant de hello utilisez cURL commande toodelete un compte Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="7a013-201">Use hello following cURL command toodelete a Data Lake Store account.</span></span> <span data-ttu-id="7a013-202">Remplacez **\<yourstorename>** par le nom de votre Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="7a013-202">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X DELETE -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.DataLakeStore/accounts/<yourstorename>?api-version=2015-10-01-preview

<span data-ttu-id="7a013-203">Vous devez voir une sortie semblable à hello suivante :</span><span class="sxs-lookup"><span data-stu-id="7a013-203">You should see an output like hello following:</span></span>

    HTTP/1.1 200 OK
    ...
    ...

## <a name="see-also"></a><span data-ttu-id="7a013-204">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="7a013-204">See also</span></span>
* [<span data-ttu-id="7a013-205">Ouvrir des applications Big Data open source compatibles avec Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="7a013-205">Open Source Big Data applications compatible with Azure Data Lake Store</span></span>](data-lake-store-compatible-oss-other-applications.md)

