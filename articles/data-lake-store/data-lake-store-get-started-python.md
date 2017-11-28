---
title: "aaaUse hello Python SDK tooget main d’Azure Data Lake Store | Documents Microsoft"
description: "Découvrez comment toowork du Kit de développement logiciel Python toouse avec des comptes Data Lake Store et hello système de fichiers."
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 75f6de6f-6fd8-48f4-8707-cb27d22d27a6
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 7061fdf25ef607608bab618a20ddd3d6fc7af01d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-python"></a><span data-ttu-id="c28f6-103">Prise en main d’Azure Data Lake Store à l’aide de Python</span><span class="sxs-lookup"><span data-stu-id="c28f6-103">Get started with Azure Data Lake Store using Python</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="c28f6-104">Portail</span><span class="sxs-lookup"><span data-stu-id="c28f6-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="c28f6-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c28f6-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="c28f6-106">Kit SDK .NET</span><span class="sxs-lookup"><span data-stu-id="c28f6-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="c28f6-107">Kit SDK Java</span><span class="sxs-lookup"><span data-stu-id="c28f6-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="c28f6-108">API REST</span><span class="sxs-lookup"><span data-stu-id="c28f6-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="c28f6-109">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="c28f6-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="c28f6-110">Node.JS</span><span class="sxs-lookup"><span data-stu-id="c28f6-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="c28f6-111">Python</span><span class="sxs-lookup"><span data-stu-id="c28f6-111">Python</span></span>](data-lake-store-get-started-python.md)
>
>

<span data-ttu-id="c28f6-112">Découvrez comment toouse hello Python SDK pour les opérations de base tooperform Azure et d’Azure Data Lake Store telles que la création des dossiers, télécharger des fichiers de données, etc.. Pour plus d’informations sur Data Lake, consultez [Azure Data Lake Store](data-lake-store-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c28f6-112">Learn how toouse hello Python SDK for Azure and Azure Data Lake Store tooperform basic operations such as create folders, upload and download data files, etc. For more information about Data Lake, see [Azure Data Lake Store](data-lake-store-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c28f6-113">Composants requis</span><span class="sxs-lookup"><span data-stu-id="c28f6-113">Prerequisites</span></span>

* <span data-ttu-id="c28f6-114">**Python**</span><span class="sxs-lookup"><span data-stu-id="c28f6-114">**Python**.</span></span> <span data-ttu-id="c28f6-115">Pour télécharger Python, accédez [ici](https://www.python.org/downloads/).</span><span class="sxs-lookup"><span data-stu-id="c28f6-115">You can download Python from [here](https://www.python.org/downloads/).</span></span> <span data-ttu-id="c28f6-116">Cet article utilise Python version 3.5.2.</span><span class="sxs-lookup"><span data-stu-id="c28f6-116">This article uses Python 3.5.2.</span></span>

* <span data-ttu-id="c28f6-117">**Un abonnement Azure**.</span><span class="sxs-lookup"><span data-stu-id="c28f6-117">**An Azure subscription**.</span></span> <span data-ttu-id="c28f6-118">Consultez la page [Obtention d’un essai gratuit d’Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c28f6-118">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="c28f6-119">**Créez une application Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c28f6-119">**Create an Azure Active Directory Application**.</span></span> <span data-ttu-id="c28f6-120">Vous utilisez hello Azure AD tooauthenticate hello Data Lake Store une application avec Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c28f6-120">You use hello Azure AD application tooauthenticate hello Data Lake Store application with Azure AD.</span></span> <span data-ttu-id="c28f6-121">Il existe tooauthenticate différentes approches avec Azure AD, qui sont **l’authentification de l’utilisateur final** ou **l’authentification de service**.</span><span class="sxs-lookup"><span data-stu-id="c28f6-121">There are different approaches tooauthenticate with Azure AD, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="c28f6-122">Pour plus d’informations sur la façon d’et tooauthenticate, consultez [l’authentification de l’utilisateur final](data-lake-store-end-user-authenticate-using-active-directory.md) ou [l’authentification de service](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="c28f6-122">For instructions and more information on how tooauthenticate, see [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md) or [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md).</span></span>

## <a name="install-hello-modules"></a><span data-ttu-id="c28f6-123">Installer les modules hello</span><span class="sxs-lookup"><span data-stu-id="c28f6-123">Install hello modules</span></span>

<span data-ttu-id="c28f6-124">toowork avec Data Lake Store à l’aide de Python, vous devez tooinstall trois modules.</span><span class="sxs-lookup"><span data-stu-id="c28f6-124">toowork with Data Lake Store using Python, you need tooinstall three modules.</span></span>

* <span data-ttu-id="c28f6-125">Hello `azure-mgmt-resource` module.</span><span class="sxs-lookup"><span data-stu-id="c28f6-125">hello `azure-mgmt-resource` module.</span></span> <span data-ttu-id="c28f6-126">Cela inclut les modules Azure pour Active Directory, etc.</span><span class="sxs-lookup"><span data-stu-id="c28f6-126">This includes Azure modules for Active Directory, etc..</span></span>
* <span data-ttu-id="c28f6-127">Hello `azure-mgmt-datalake-store` module.</span><span class="sxs-lookup"><span data-stu-id="c28f6-127">hello `azure-mgmt-datalake-store` module.</span></span> <span data-ttu-id="c28f6-128">Cela inclut les opérations de gestion de compte Azure Data Lake Store hello.</span><span class="sxs-lookup"><span data-stu-id="c28f6-128">This includes hello Azure Data Lake Store account management operations.</span></span> <span data-ttu-id="c28f6-129">Pour plus d’informations sur ce module, consultez les [informations de référence sur les modules de gestion Azure Data Lake Store](http://azure-sdk-for-python.readthedocs.io/en/latest/sample_azure-mgmt-datalake-store.html).</span><span class="sxs-lookup"><span data-stu-id="c28f6-129">For more information on this module, see [Azure Data Lake Store Management module reference](http://azure-sdk-for-python.readthedocs.io/en/latest/sample_azure-mgmt-datalake-store.html).</span></span>
* <span data-ttu-id="c28f6-130">Hello `azure-datalake-store` module.</span><span class="sxs-lookup"><span data-stu-id="c28f6-130">hello `azure-datalake-store` module.</span></span> <span data-ttu-id="c28f6-131">Cela inclut les opérations de système de fichiers de hello Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="c28f6-131">This includes hello Azure Data Lake Store filesystem operations.</span></span> <span data-ttu-id="c28f6-132">Pour plus d’informations sur ce module, consultez les [informations de référence sur les modules du système de fichiers Azure Data Lake Store](http://azure-datalake-store.readthedocs.io/en/latest/).</span><span class="sxs-lookup"><span data-stu-id="c28f6-132">For more information on this module, see [Azure Data Lake Store Filesystem module reference](http://azure-datalake-store.readthedocs.io/en/latest/).</span></span>

<span data-ttu-id="c28f6-133">Utilisez hello suivant des modules de commandes tooinstall hello.</span><span class="sxs-lookup"><span data-stu-id="c28f6-133">Use hello following commands tooinstall hello modules.</span></span>

```
pip install azure-mgmt-resource
pip install azure-mgmt-datalake-store
pip install azure-datalake-store
```

## <a name="create-a-new-python-application"></a><span data-ttu-id="c28f6-134">Créer une application Python</span><span class="sxs-lookup"><span data-stu-id="c28f6-134">Create a new Python application</span></span>

1. <span data-ttu-id="c28f6-135">Bonjour IDE de votre choix, créez une application Python, par exemple, **mysample.py**.</span><span class="sxs-lookup"><span data-stu-id="c28f6-135">In hello IDE of your choice create a new Python application, for example, **mysample.py**.</span></span>

2. <span data-ttu-id="c28f6-136">Ajouter hello suivant des modules de lignes tooimport hello requis</span><span class="sxs-lookup"><span data-stu-id="c28f6-136">Add hello following lines tooimport hello required modules</span></span>

    ```
    ## Use this only for Azure AD service-to-service authentication
    from azure.common.credentials import ServicePrincipalCredentials

    ## Use this only for Azure AD end-user authentication
    from azure.common.credentials import UserPassCredentials

    ## Use this only for Azure AD multi-factor authentication
    from msrestazure.azure_active_directory import AADTokenCredentials

    ## Required for Azure Data Lake Store account management
    from azure.mgmt.datalake.store import DataLakeStoreAccountManagementClient
    from azure.mgmt.datalake.store.models import DataLakeStoreAccount

    ## Required for Azure Data Lake Store filesystem management
    from azure.datalake.store import core, lib, multithread

    # Common Azure imports
    from azure.mgmt.resource.resources import ResourceManagementClient
    from azure.mgmt.resource.resources.models import ResourceGroup

    ## Use these as needed for your application
    import logging, getpass, pprint, uuid, time
    ```

3. <span data-ttu-id="c28f6-137">Enregistrer les modifications toomysample.py.</span><span class="sxs-lookup"><span data-stu-id="c28f6-137">Save changes toomysample.py.</span></span>

## <a name="authentication"></a><span data-ttu-id="c28f6-138">Authentification</span><span class="sxs-lookup"><span data-stu-id="c28f6-138">Authentication</span></span>

<span data-ttu-id="c28f6-139">Dans cette section, nous parlons de tooauthenticate de différentes façons hello avec Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c28f6-139">In this section, we talk about hello different ways tooauthenticate with Azure AD.</span></span> <span data-ttu-id="c28f6-140">options de Hello disponibles sont :</span><span class="sxs-lookup"><span data-stu-id="c28f6-140">hello options available are:</span></span>

* <span data-ttu-id="c28f6-141">Authentification de l’utilisateur final</span><span class="sxs-lookup"><span data-stu-id="c28f6-141">End-user authentication</span></span>
* <span data-ttu-id="c28f6-142">Authentification de service à service</span><span class="sxs-lookup"><span data-stu-id="c28f6-142">Service-to-service authentication</span></span>
* <span data-ttu-id="c28f6-143">Authentification multifacteur</span><span class="sxs-lookup"><span data-stu-id="c28f6-143">Multi-factor authentication</span></span>

<span data-ttu-id="c28f6-144">Vous devez utiliser ces options d’authentification pour les modules de gestion des systèmes de fichiers et des comptes.</span><span class="sxs-lookup"><span data-stu-id="c28f6-144">You must use these authentication options for both account management and filesystem management modules.</span></span>

### <a name="end-user-authentication-for-account-management"></a><span data-ttu-id="c28f6-145">Authentification de l’utilisateur final pour la gestion du compte</span><span class="sxs-lookup"><span data-stu-id="c28f6-145">End-user authentication for account management</span></span>

<span data-ttu-id="c28f6-146">Utilisez cette tooauthenticate avec Azure AD pour les opérations de gestion de compte (création/suppression compte Data Lake Store, etc..).</span><span class="sxs-lookup"><span data-stu-id="c28f6-146">Use this tooauthenticate with Azure AD for account management operations (create/delete Data Lake Store account, etc.).</span></span> <span data-ttu-id="c28f6-147">Vous devez fournir un nom d’utilisateur et un mot de passe d’utilisateur Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c28f6-147">You must provide username and password for an Azure AD user.</span></span> <span data-ttu-id="c28f6-148">Notez que l’utilisateur hello ne doit pas être configuré pour l’authentification multifacteur.</span><span class="sxs-lookup"><span data-stu-id="c28f6-148">Note that hello user should not be configured for multi-factor authentication.</span></span>

    user = input('Enter hello user tooauthenticate with that has permission toosubscription: ')
    password = getpass.getpass()

    credentials = UserPassCredentials(user, password)

### <a name="end-user-authentication-for-filesystem-operations"></a><span data-ttu-id="c28f6-149">Authentification de l’utilisateur final pour les opérations du système de fichiers</span><span class="sxs-lookup"><span data-stu-id="c28f6-149">End-user authentication for filesystem operations</span></span>

<span data-ttu-id="c28f6-150">Utilisez cette tooauthenticate avec Azure AD pour les opérations de système de fichiers (créer de dossier, fichier de téléchargement, etc.)..</span><span class="sxs-lookup"><span data-stu-id="c28f6-150">Use this tooauthenticate with Azure AD for filesystem operations (create folder, upload file, etc.).</span></span> <span data-ttu-id="c28f6-151">Utilisez-la avec une application **cliente native** Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c28f6-151">Use this with an existing Azure AD **native client** application.</span></span> <span data-ttu-id="c28f6-152">utilisateur Hello Azure AD que vous fournissez des informations d’identification ne doit pas être configuré pour l’authentification multifacteur.</span><span class="sxs-lookup"><span data-stu-id="c28f6-152">hello Azure AD user you provide credentials for should not be configured for multi-factor authentication.</span></span>

    tenant_id = 'FILL-IN-HERE'
    client_id = 'FILL-IN-HERE'
    user = input('Enter hello user tooauthenticate with that has permission toosubscription: ')
    password = getpass.getpass()

    token = lib.auth(tenant_id, user, password, client_id)

### <a name="service-to-service-authentication-with-client-secret-for-account-management"></a><span data-ttu-id="c28f6-153">L’authentification de service à service avec clé secrète client pour al gestion de compte</span><span class="sxs-lookup"><span data-stu-id="c28f6-153">Service-to-service authentication with client secret for account management</span></span>

<span data-ttu-id="c28f6-154">Utilisez cette tooauthenticate avec Azure AD pour les opérations de gestion de compte (création/suppression compte Data Lake Store, etc..).</span><span class="sxs-lookup"><span data-stu-id="c28f6-154">Use this tooauthenticate with Azure AD for account management operations (create/delete Data Lake Store account, etc.).</span></span> <span data-ttu-id="c28f6-155">Hello suivant extrait de code peut être utilisé tooauthenticate votre application en mode non interactif, à l’aide de la clé secrète du client hello pour un principal de l’application ou le service.</span><span class="sxs-lookup"><span data-stu-id="c28f6-155">hello following snippet can be used tooauthenticate your application non-interactively, using hello client secret for an application / service principal.</span></span> <span data-ttu-id="c28f6-156">Utilisez-le avec une « application web » Azure AD existante.</span><span class="sxs-lookup"><span data-stu-id="c28f6-156">Use this with an existing Azure AD "Web App" application.</span></span>

    credentials = ServicePrincipalCredentials(client_id = 'FILL-IN-HERE', secret = 'FILL-IN-HERE', tenant = 'FILL-IN-HERE')

### <a name="service-to-service-authentication-with-client-secret-for-filesystem-operations"></a><span data-ttu-id="c28f6-157">Authentification de service à service avec clé secrète client pour les opérations du système de fichiers</span><span class="sxs-lookup"><span data-stu-id="c28f6-157">Service-to-service authentication with client secret for filesystem operations</span></span>

<span data-ttu-id="c28f6-158">Utilisez cette tooauthenticate avec Azure AD pour les opérations de système de fichiers (créer de dossier, fichier de téléchargement, etc.)..</span><span class="sxs-lookup"><span data-stu-id="c28f6-158">Use this tooauthenticate with Azure AD for filesystem operations (create folder, upload file, etc.).</span></span> <span data-ttu-id="c28f6-159">Hello suivant extrait de code peut être utilisé tooauthenticate votre application en mode non interactif, à l’aide de la clé secrète du client hello pour un principal de l’application ou le service.</span><span class="sxs-lookup"><span data-stu-id="c28f6-159">hello following snippet can be used tooauthenticate your application non-interactively, using hello client secret for an application / service principal.</span></span> <span data-ttu-id="c28f6-160">Utilisez-le avec une « application web » Azure AD existante.</span><span class="sxs-lookup"><span data-stu-id="c28f6-160">Use this with an existing Azure AD "Web App" application.</span></span>

    token = lib.auth(tenant_id = 'FILL-IN-HERE', client_secret = 'FILL-IN-HERE', client_id = 'FILL-IN-HERE')

### <a name="multi-factor-authentication-for-account-management"></a><span data-ttu-id="c28f6-161">Authentification multifacteur pour la gestion des comptes</span><span class="sxs-lookup"><span data-stu-id="c28f6-161">Multi-factor authentication for account management</span></span>

<span data-ttu-id="c28f6-162">Utilisez cette tooauthenticate avec Azure AD pour les opérations de gestion de compte (création/suppression compte Data Lake Store, etc..).</span><span class="sxs-lookup"><span data-stu-id="c28f6-162">Use this tooauthenticate with Azure AD for account management operations (create/delete Data Lake Store account, etc.).</span></span> <span data-ttu-id="c28f6-163">Hello extrait de code suivant peut être utilisé tooauthenticate votre application à l’aide de l’authentification multifacteur.</span><span class="sxs-lookup"><span data-stu-id="c28f6-163">hello following snippet can be used tooauthenticate your application using multi-factor authentication.</span></span> <span data-ttu-id="c28f6-164">Utilisez-le avec une « application web » Azure AD existante.</span><span class="sxs-lookup"><span data-stu-id="c28f6-164">Use this with an existing Azure AD "Web App" application.</span></span>

    authority_host_url = "https://login.microsoftonline.com"
    tenant = "FILL-IN-HERE"
    authority_url = authority_host_url + '/' + tenant
    client_id = 'FILL-IN-HERE'
    redirect = 'urn:ietf:wg:oauth:2.0:oob'
    RESOURCE = 'https://management.core.windows.net/'
    
    context = adal.AuthenticationContext(authority_url)
    code = context.acquire_user_code(RESOURCE, client_id)
    print(code['message'])
    mgmt_token = context.acquire_token_with_device_code(RESOURCE, code, client_id)
    credentials = AADTokenCredentials(mgmt_token, client_id)

### <a name="multi-factor-authentication-for-filesystem-management"></a><span data-ttu-id="c28f6-165">Authentification multifacteur pour la gestion des systèmes de fichiers</span><span class="sxs-lookup"><span data-stu-id="c28f6-165">Multi-factor authentication for filesystem management</span></span>

<span data-ttu-id="c28f6-166">Utilisez cette tooauthenticate avec Azure AD pour les opérations de système de fichiers (créer de dossier, fichier de téléchargement, etc.)..</span><span class="sxs-lookup"><span data-stu-id="c28f6-166">Use this tooauthenticate with Azure AD for filesystem operations (create folder, upload file, etc.).</span></span> <span data-ttu-id="c28f6-167">Hello extrait de code suivant peut être utilisé tooauthenticate votre application à l’aide de l’authentification multifacteur.</span><span class="sxs-lookup"><span data-stu-id="c28f6-167">hello following snippet can be used tooauthenticate your application using multi-factor authentication.</span></span> <span data-ttu-id="c28f6-168">Utilisez-le avec une « application web » Azure AD existante.</span><span class="sxs-lookup"><span data-stu-id="c28f6-168">Use this with an existing Azure AD "Web App" application.</span></span>

    token = lib.auth(tenant_id='FILL-IN-HERE')

## <a name="create-an-azure-resource-group"></a><span data-ttu-id="c28f6-169">Créer un groupe de ressources Azure</span><span class="sxs-lookup"><span data-stu-id="c28f6-169">Create an Azure Resource Group</span></span>

<span data-ttu-id="c28f6-170">Utilisez hello suivant extrait de code toocreate un groupe de ressources Azure :</span><span class="sxs-lookup"><span data-stu-id="c28f6-170">Use hello following code snippet toocreate an Azure Resource Group:</span></span>

    ## Declare variables
    subscriptionId= 'FILL-IN-HERE'
    resourceGroup = 'FILL-IN-HERE'
    location = 'eastus2'
    
    ## Create management client object
    resourceClient = ResourceManagementClient(
        credentials,
        subscriptionId
    )
    
    ## Create an Azure Resource Group
    resourceClient.resource_groups.create_or_update(
        resourceGroup,
        ResourceGroup(
            location=location
        )
    )

## <a name="create-clients-and-data-lake-store-account"></a><span data-ttu-id="c28f6-171">Créer des clients et un compte Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="c28f6-171">Create clients and Data Lake Store account</span></span>

<span data-ttu-id="c28f6-172">Hello suivant extrait tout d’abord crée un client de compte Data Lake Store hello.</span><span class="sxs-lookup"><span data-stu-id="c28f6-172">hello following snippet first creates hello Data Lake Store account client.</span></span> <span data-ttu-id="c28f6-173">Il utilise hello client objet toocreate un compte Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="c28f6-173">It uses hello client object toocreate a Data Lake Store account.</span></span> <span data-ttu-id="c28f6-174">Enfin, extrait de code hello crée un objet de client de système de fichiers.</span><span class="sxs-lookup"><span data-stu-id="c28f6-174">Finally, hello snippet creates a filesystem client object.</span></span>

    ## Declare variables
    subscriptionId = 'FILL-IN-HERE'
    adlsAccountName = 'FILL-IN-HERE'

    ## Create management client object
    adlsAcctClient = DataLakeStoreAccountManagementClient(credentials, subscriptionId)

    ## Create a Data Lake Store account
    adlsAcctResult = adlsAcctClient.account.create(
        resourceGroup,
        adlsAccountName,
        DataLakeStoreAccount(
            location=location
        )
    ).wait()

    ## Create a filesystem client object
    adlsFileSystemClient = core.AzureDLFileSystem(token, store_name=adlsAccountName)

## <a name="list-hello-data-lake-store-accounts"></a><span data-ttu-id="c28f6-175">Liste des comptes Data Lake Store hello</span><span class="sxs-lookup"><span data-stu-id="c28f6-175">List hello Data Lake Store accounts</span></span>

    ## List hello existing Data Lake Store accounts
    result_list_response = adlsAcctClient.account.list()
    result_list = list(result_list_response)
    for items in result_list:
        print(items)

## <a name="create-a-directory"></a><span data-ttu-id="c28f6-176">Créer un répertoire</span><span class="sxs-lookup"><span data-stu-id="c28f6-176">Create a directory</span></span>

    ## Create a directory
    adlsFileSystemClient.mkdir('/mysampledirectory')

## <a name="upload-a-file"></a><span data-ttu-id="c28f6-177">Charger un fichier</span><span class="sxs-lookup"><span data-stu-id="c28f6-177">Upload a file</span></span>


    ## Upload a file
    multithread.ADLUploader(adlsFileSystemClient, lpath='C:\\data\\mysamplefile.txt', rpath='/mysampledirectory/mysamplefile.txt', nthreads=64, overwrite=True, buffersize=4194304, blocksize=4194304)


## <a name="download-a-file"></a><span data-ttu-id="c28f6-178">Téléchargement d’un fichier</span><span class="sxs-lookup"><span data-stu-id="c28f6-178">Download a file</span></span>

    ## Download a file
    multithread.ADLDownloader(adlsFileSystemClient, lpath='C:\\data\\mysamplefile.txt.out', rpath='/mysampledirectory/mysamplefile.txt', nthreads=64, overwrite=True, buffersize=4194304, blocksize=4194304)

## <a name="delete-a-directory"></a><span data-ttu-id="c28f6-179">Supprimer un répertoire</span><span class="sxs-lookup"><span data-stu-id="c28f6-179">Delete a directory</span></span>

    ## Delete a directory
    adlsFileSystemClient.rm('/mysampledirectory', recursive=True)

## <a name="see-also"></a><span data-ttu-id="c28f6-180">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="c28f6-180">See also</span></span>

- [<span data-ttu-id="c28f6-181">Sécuriser les données dans Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="c28f6-181">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
- [<span data-ttu-id="c28f6-182">Utiliser Azure Data Lake Analytics avec Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="c28f6-182">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
- [<span data-ttu-id="c28f6-183">Utiliser Azure HDInsight avec Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="c28f6-183">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
- [<span data-ttu-id="c28f6-184">Data Lake Store .NET SDK Reference (Informations de référence sur le Kit de développement logiciel (SDK) .NET Azure Data Lake Store)</span><span class="sxs-lookup"><span data-stu-id="c28f6-184">Data Lake Store .NET SDK Reference</span></span>](https://msdn.microsoft.com/library/mt581387.aspx)
- [<span data-ttu-id="c28f6-185">Data Lake Store REST Reference (Informations de référence sur les API REST Data Lake Store)</span><span class="sxs-lookup"><span data-stu-id="c28f6-185">Data Lake Store REST Reference</span></span>](https://msdn.microsoft.com/library/mt693424.aspx)
