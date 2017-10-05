---
title: "Prise en main d’Azure Data Lake Store à l’aide du Kit de développement logiciel (SDK) Python | Microsoft Docs"
description: "Découvrez comment gérer le kit de développement logiciel (SDK) Python avec les comptes Data Lake Store et le système de fichiers."
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
ms.openlocfilehash: 375a603360ac249fc1b08923a94c85652390a3fc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-data-lake-store-using-python"></a><span data-ttu-id="99ca2-103">Prise en main d’Azure Data Lake Store à l’aide de Python</span><span class="sxs-lookup"><span data-stu-id="99ca2-103">Get started with Azure Data Lake Store using Python</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="99ca2-104">Portail</span><span class="sxs-lookup"><span data-stu-id="99ca2-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="99ca2-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="99ca2-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="99ca2-106">Kit SDK .NET</span><span class="sxs-lookup"><span data-stu-id="99ca2-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="99ca2-107">Kit SDK Java</span><span class="sxs-lookup"><span data-stu-id="99ca2-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="99ca2-108">API REST</span><span class="sxs-lookup"><span data-stu-id="99ca2-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="99ca2-109">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="99ca2-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="99ca2-110">Node.JS</span><span class="sxs-lookup"><span data-stu-id="99ca2-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="99ca2-111">Python</span><span class="sxs-lookup"><span data-stu-id="99ca2-111">Python</span></span>](data-lake-store-get-started-python.md)
>
>

<span data-ttu-id="99ca2-112">Découvrez comment utiliser le Kit de développement logiciel (SDK) Python et Azure Data Lake Store pour effectuer des opérations de base comme créer des dossiers ou charger et télécharger des fichiers de données. Pour plus d’informations sur Data Lake, consultez [Azure Data Lake Store](data-lake-store-overview.md).</span><span class="sxs-lookup"><span data-stu-id="99ca2-112">Learn how to use the Python SDK for Azure and Azure Data Lake Store to perform basic operations such as create folders, upload and download data files, etc. For more information about Data Lake, see [Azure Data Lake Store](data-lake-store-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="99ca2-113">Composants requis</span><span class="sxs-lookup"><span data-stu-id="99ca2-113">Prerequisites</span></span>

* <span data-ttu-id="99ca2-114">**Python**</span><span class="sxs-lookup"><span data-stu-id="99ca2-114">**Python**.</span></span> <span data-ttu-id="99ca2-115">Pour télécharger Python, accédez [ici](https://www.python.org/downloads/).</span><span class="sxs-lookup"><span data-stu-id="99ca2-115">You can download Python from [here](https://www.python.org/downloads/).</span></span> <span data-ttu-id="99ca2-116">Cet article utilise Python version 3.5.2.</span><span class="sxs-lookup"><span data-stu-id="99ca2-116">This article uses Python 3.5.2.</span></span>

* <span data-ttu-id="99ca2-117">**Un abonnement Azure**.</span><span class="sxs-lookup"><span data-stu-id="99ca2-117">**An Azure subscription**.</span></span> <span data-ttu-id="99ca2-118">Consultez la page [Obtention d’un essai gratuit d’Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="99ca2-118">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="99ca2-119">**Créez une application Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="99ca2-119">**Create an Azure Active Directory Application**.</span></span> <span data-ttu-id="99ca2-120">Vous utilisez l’application Azure AD pour authentifier l’application Data Lake Store auprès d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="99ca2-120">You use the Azure AD application to authenticate the Data Lake Store application with Azure AD.</span></span> <span data-ttu-id="99ca2-121">Il existe différentes approches pour l’authentification auprès d’Azure AD : **authentification de l’utilisateur final** ou **authentification de service à service**.</span><span class="sxs-lookup"><span data-stu-id="99ca2-121">There are different approaches to authenticate with Azure AD, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="99ca2-122">Pour obtenir des instructions et plus d’informations sur l’authentification, consultez [l’authentification de l’utilisateur final](data-lake-store-end-user-authenticate-using-active-directory.md) ou [l’authentification de service à service](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="99ca2-122">For instructions and more information on how to authenticate, see [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md) or [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md).</span></span>

## <a name="install-the-modules"></a><span data-ttu-id="99ca2-123">Installer les modules</span><span class="sxs-lookup"><span data-stu-id="99ca2-123">Install the modules</span></span>

<span data-ttu-id="99ca2-124">Pour utiliser Data Lake Store avec Python, vous devez installer trois modules.</span><span class="sxs-lookup"><span data-stu-id="99ca2-124">To work with Data Lake Store using Python, you need to install three modules.</span></span>

* <span data-ttu-id="99ca2-125">Le module `azure-mgmt-resource`.</span><span class="sxs-lookup"><span data-stu-id="99ca2-125">The `azure-mgmt-resource` module.</span></span> <span data-ttu-id="99ca2-126">Cela inclut les modules Azure pour Active Directory, etc.</span><span class="sxs-lookup"><span data-stu-id="99ca2-126">This includes Azure modules for Active Directory, etc..</span></span>
* <span data-ttu-id="99ca2-127">Le module `azure-mgmt-datalake-store`.</span><span class="sxs-lookup"><span data-stu-id="99ca2-127">The `azure-mgmt-datalake-store` module.</span></span> <span data-ttu-id="99ca2-128">Cela inclut les opérations de gestion du compte Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="99ca2-128">This includes the Azure Data Lake Store account management operations.</span></span> <span data-ttu-id="99ca2-129">Pour plus d’informations sur ce module, consultez les [informations de référence sur les modules de gestion Azure Data Lake Store](http://azure-sdk-for-python.readthedocs.io/en/latest/sample_azure-mgmt-datalake-store.html).</span><span class="sxs-lookup"><span data-stu-id="99ca2-129">For more information on this module, see [Azure Data Lake Store Management module reference](http://azure-sdk-for-python.readthedocs.io/en/latest/sample_azure-mgmt-datalake-store.html).</span></span>
* <span data-ttu-id="99ca2-130">Le module `azure-datalake-store`.</span><span class="sxs-lookup"><span data-stu-id="99ca2-130">The `azure-datalake-store` module.</span></span> <span data-ttu-id="99ca2-131">Cela inclut les opérations du système de fichiers Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="99ca2-131">This includes the Azure Data Lake Store filesystem operations.</span></span> <span data-ttu-id="99ca2-132">Pour plus d’informations sur ce module, consultez les [informations de référence sur les modules du système de fichiers Azure Data Lake Store](http://azure-datalake-store.readthedocs.io/en/latest/).</span><span class="sxs-lookup"><span data-stu-id="99ca2-132">For more information on this module, see [Azure Data Lake Store Filesystem module reference](http://azure-datalake-store.readthedocs.io/en/latest/).</span></span>

<span data-ttu-id="99ca2-133">Utilisez les commandes suivantes pour installer les modules.</span><span class="sxs-lookup"><span data-stu-id="99ca2-133">Use the following commands to install the modules.</span></span>

```
pip install azure-mgmt-resource
pip install azure-mgmt-datalake-store
pip install azure-datalake-store
```

## <a name="create-a-new-python-application"></a><span data-ttu-id="99ca2-134">Créer une application Python</span><span class="sxs-lookup"><span data-stu-id="99ca2-134">Create a new Python application</span></span>

1. <span data-ttu-id="99ca2-135">Utilisez l’IDE de votre choix pour créer une application Python, par exemple, **mysample.py**.</span><span class="sxs-lookup"><span data-stu-id="99ca2-135">In the IDE of your choice create a new Python application, for example, **mysample.py**.</span></span>

2. <span data-ttu-id="99ca2-136">Ajoutez les lignes suivantes pour importer les modules requis.</span><span class="sxs-lookup"><span data-stu-id="99ca2-136">Add the following lines to import the required modules</span></span>

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

3. <span data-ttu-id="99ca2-137">Enregistrez les modifications apportées à mysample.py.</span><span class="sxs-lookup"><span data-stu-id="99ca2-137">Save changes to mysample.py.</span></span>

## <a name="authentication"></a><span data-ttu-id="99ca2-138">Authentification</span><span class="sxs-lookup"><span data-stu-id="99ca2-138">Authentication</span></span>

<span data-ttu-id="99ca2-139">Dans cette section, nous aborderons les différentes méthodes permettant de s’authentifier auprès d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="99ca2-139">In this section, we talk about the different ways to authenticate with Azure AD.</span></span> <span data-ttu-id="99ca2-140">Voici les options disponibles :</span><span class="sxs-lookup"><span data-stu-id="99ca2-140">The options available are:</span></span>

* <span data-ttu-id="99ca2-141">Authentification de l’utilisateur final</span><span class="sxs-lookup"><span data-stu-id="99ca2-141">End-user authentication</span></span>
* <span data-ttu-id="99ca2-142">Authentification de service à service</span><span class="sxs-lookup"><span data-stu-id="99ca2-142">Service-to-service authentication</span></span>
* <span data-ttu-id="99ca2-143">Authentification multifacteur</span><span class="sxs-lookup"><span data-stu-id="99ca2-143">Multi-factor authentication</span></span>

<span data-ttu-id="99ca2-144">Vous devez utiliser ces options d’authentification pour les modules de gestion des systèmes de fichiers et des comptes.</span><span class="sxs-lookup"><span data-stu-id="99ca2-144">You must use these authentication options for both account management and filesystem management modules.</span></span>

### <a name="end-user-authentication-for-account-management"></a><span data-ttu-id="99ca2-145">Authentification de l’utilisateur final pour la gestion du compte</span><span class="sxs-lookup"><span data-stu-id="99ca2-145">End-user authentication for account management</span></span>

<span data-ttu-id="99ca2-146">Utilisez cette méthode pour l’authentification auprès d’Azure AD pour les opérations de gestion du compte (créer/supprimer un compte Data Lake Store, etc.).</span><span class="sxs-lookup"><span data-stu-id="99ca2-146">Use this to authenticate with Azure AD for account management operations (create/delete Data Lake Store account, etc.).</span></span> <span data-ttu-id="99ca2-147">Vous devez fournir un nom d’utilisateur et un mot de passe d’utilisateur Azure AD.</span><span class="sxs-lookup"><span data-stu-id="99ca2-147">You must provide username and password for an Azure AD user.</span></span> <span data-ttu-id="99ca2-148">Notez que l’utilisateur ne doit pas être configuré pour l’authentification multifacteur.</span><span class="sxs-lookup"><span data-stu-id="99ca2-148">Note that the user should not be configured for multi-factor authentication.</span></span>

    user = input('Enter the user to authenticate with that has permission to subscription: ')
    password = getpass.getpass()

    credentials = UserPassCredentials(user, password)

### <a name="end-user-authentication-for-filesystem-operations"></a><span data-ttu-id="99ca2-149">Authentification de l’utilisateur final pour les opérations du système de fichiers</span><span class="sxs-lookup"><span data-stu-id="99ca2-149">End-user authentication for filesystem operations</span></span>

<span data-ttu-id="99ca2-150">Utilisez cette méthode pour procéder à une authentification auprès d’Azure AD pour les opérations du système de fichiers (créer un dossier, charger un fichier, etc.).</span><span class="sxs-lookup"><span data-stu-id="99ca2-150">Use this to authenticate with Azure AD for filesystem operations (create folder, upload file, etc.).</span></span> <span data-ttu-id="99ca2-151">Utilisez-la avec une application **cliente native** Azure AD.</span><span class="sxs-lookup"><span data-stu-id="99ca2-151">Use this with an existing Azure AD **native client** application.</span></span> <span data-ttu-id="99ca2-152">L’utilisateur Azure AD pour lequel vous fournissez des informations d’identification ne doit pas être configuré pour l’authentification multifacteur.</span><span class="sxs-lookup"><span data-stu-id="99ca2-152">The Azure AD user you provide credentials for should not be configured for multi-factor authentication.</span></span>

    tenant_id = 'FILL-IN-HERE'
    client_id = 'FILL-IN-HERE'
    user = input('Enter the user to authenticate with that has permission to subscription: ')
    password = getpass.getpass()

    token = lib.auth(tenant_id, user, password, client_id)

### <a name="service-to-service-authentication-with-client-secret-for-account-management"></a><span data-ttu-id="99ca2-153">L’authentification de service à service avec clé secrète client pour al gestion de compte</span><span class="sxs-lookup"><span data-stu-id="99ca2-153">Service-to-service authentication with client secret for account management</span></span>

<span data-ttu-id="99ca2-154">Utilisez cette méthode pour l’authentification auprès d’Azure AD pour les opérations de gestion du compte (créer/supprimer un compte Data Lake Store, etc.).</span><span class="sxs-lookup"><span data-stu-id="99ca2-154">Use this to authenticate with Azure AD for account management operations (create/delete Data Lake Store account, etc.).</span></span> <span data-ttu-id="99ca2-155">Vous pouvez faire appel à l’extrait de code suivant pour authentifier votre application en mode non interactif, en utilisant la clé secrète client pour une application/un principal du service.</span><span class="sxs-lookup"><span data-stu-id="99ca2-155">The following snippet can be used to authenticate your application non-interactively, using the client secret for an application / service principal.</span></span> <span data-ttu-id="99ca2-156">Utilisez-le avec une « application web » Azure AD existante.</span><span class="sxs-lookup"><span data-stu-id="99ca2-156">Use this with an existing Azure AD "Web App" application.</span></span>

    credentials = ServicePrincipalCredentials(client_id = 'FILL-IN-HERE', secret = 'FILL-IN-HERE', tenant = 'FILL-IN-HERE')

### <a name="service-to-service-authentication-with-client-secret-for-filesystem-operations"></a><span data-ttu-id="99ca2-157">Authentification de service à service avec clé secrète client pour les opérations du système de fichiers</span><span class="sxs-lookup"><span data-stu-id="99ca2-157">Service-to-service authentication with client secret for filesystem operations</span></span>

<span data-ttu-id="99ca2-158">Utilisez cette méthode pour procéder à une authentification auprès d’Azure AD pour les opérations du système de fichiers (créer un dossier, charger un fichier, etc.).</span><span class="sxs-lookup"><span data-stu-id="99ca2-158">Use this to authenticate with Azure AD for filesystem operations (create folder, upload file, etc.).</span></span> <span data-ttu-id="99ca2-159">Vous pouvez faire appel à l’extrait de code suivant pour authentifier votre application en mode non interactif, en utilisant la clé secrète client pour une application/un principal du service.</span><span class="sxs-lookup"><span data-stu-id="99ca2-159">The following snippet can be used to authenticate your application non-interactively, using the client secret for an application / service principal.</span></span> <span data-ttu-id="99ca2-160">Utilisez-le avec une « application web » Azure AD existante.</span><span class="sxs-lookup"><span data-stu-id="99ca2-160">Use this with an existing Azure AD "Web App" application.</span></span>

    token = lib.auth(tenant_id = 'FILL-IN-HERE', client_secret = 'FILL-IN-HERE', client_id = 'FILL-IN-HERE')

### <a name="multi-factor-authentication-for-account-management"></a><span data-ttu-id="99ca2-161">Authentification multifacteur pour la gestion des comptes</span><span class="sxs-lookup"><span data-stu-id="99ca2-161">Multi-factor authentication for account management</span></span>

<span data-ttu-id="99ca2-162">Utilisez cette méthode pour l’authentification auprès d’Azure AD pour les opérations de gestion du compte (créer/supprimer un compte Data Lake Store, etc.).</span><span class="sxs-lookup"><span data-stu-id="99ca2-162">Use this to authenticate with Azure AD for account management operations (create/delete Data Lake Store account, etc.).</span></span> <span data-ttu-id="99ca2-163">L’extrait de code suivant peut être utilisé pour authentifier votre application à l’aide de l’authentification multifacteur.</span><span class="sxs-lookup"><span data-stu-id="99ca2-163">The following snippet can be used to authenticate your application using multi-factor authentication.</span></span> <span data-ttu-id="99ca2-164">Utilisez-le avec une « application web » Azure AD existante.</span><span class="sxs-lookup"><span data-stu-id="99ca2-164">Use this with an existing Azure AD "Web App" application.</span></span>

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

### <a name="multi-factor-authentication-for-filesystem-management"></a><span data-ttu-id="99ca2-165">Authentification multifacteur pour la gestion des systèmes de fichiers</span><span class="sxs-lookup"><span data-stu-id="99ca2-165">Multi-factor authentication for filesystem management</span></span>

<span data-ttu-id="99ca2-166">Utilisez cette méthode pour procéder à une authentification auprès d’Azure AD pour les opérations du système de fichiers (créer un dossier, charger un fichier, etc.).</span><span class="sxs-lookup"><span data-stu-id="99ca2-166">Use this to authenticate with Azure AD for filesystem operations (create folder, upload file, etc.).</span></span> <span data-ttu-id="99ca2-167">L’extrait de code suivant peut être utilisé pour authentifier votre application à l’aide de l’authentification multifacteur.</span><span class="sxs-lookup"><span data-stu-id="99ca2-167">The following snippet can be used to authenticate your application using multi-factor authentication.</span></span> <span data-ttu-id="99ca2-168">Utilisez-le avec une « application web » Azure AD existante.</span><span class="sxs-lookup"><span data-stu-id="99ca2-168">Use this with an existing Azure AD "Web App" application.</span></span>

    token = lib.auth(tenant_id='FILL-IN-HERE')

## <a name="create-an-azure-resource-group"></a><span data-ttu-id="99ca2-169">Créer un groupe de ressources Azure</span><span class="sxs-lookup"><span data-stu-id="99ca2-169">Create an Azure Resource Group</span></span>

<span data-ttu-id="99ca2-170">L’extrait de code suivant permet de créer un groupe de ressources Azure :</span><span class="sxs-lookup"><span data-stu-id="99ca2-170">Use the following code snippet to create an Azure Resource Group:</span></span>

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

## <a name="create-clients-and-data-lake-store-account"></a><span data-ttu-id="99ca2-171">Créer des clients et un compte Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="99ca2-171">Create clients and Data Lake Store account</span></span>

<span data-ttu-id="99ca2-172">L’extrait de code suivant crée dans un premier temps le client du compte Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="99ca2-172">The following snippet first creates the Data Lake Store account client.</span></span> <span data-ttu-id="99ca2-173">Il utilise l’objet client pour créer le compte Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="99ca2-173">It uses the client object to create a Data Lake Store account.</span></span> <span data-ttu-id="99ca2-174">Enfin, l’extrait de code crée un objet client de système de fichiers.</span><span class="sxs-lookup"><span data-stu-id="99ca2-174">Finally, the snippet creates a filesystem client object.</span></span>

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

## <a name="list-the-data-lake-store-accounts"></a><span data-ttu-id="99ca2-175">Répertorier les comptes Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="99ca2-175">List the Data Lake Store accounts</span></span>

    ## List the existing Data Lake Store accounts
    result_list_response = adlsAcctClient.account.list()
    result_list = list(result_list_response)
    for items in result_list:
        print(items)

## <a name="create-a-directory"></a><span data-ttu-id="99ca2-176">Créer un répertoire</span><span class="sxs-lookup"><span data-stu-id="99ca2-176">Create a directory</span></span>

    ## Create a directory
    adlsFileSystemClient.mkdir('/mysampledirectory')

## <a name="upload-a-file"></a><span data-ttu-id="99ca2-177">Charger un fichier</span><span class="sxs-lookup"><span data-stu-id="99ca2-177">Upload a file</span></span>


    ## Upload a file
    multithread.ADLUploader(adlsFileSystemClient, lpath='C:\\data\\mysamplefile.txt', rpath='/mysampledirectory/mysamplefile.txt', nthreads=64, overwrite=True, buffersize=4194304, blocksize=4194304)


## <a name="download-a-file"></a><span data-ttu-id="99ca2-178">Téléchargement d’un fichier</span><span class="sxs-lookup"><span data-stu-id="99ca2-178">Download a file</span></span>

    ## Download a file
    multithread.ADLDownloader(adlsFileSystemClient, lpath='C:\\data\\mysamplefile.txt.out', rpath='/mysampledirectory/mysamplefile.txt', nthreads=64, overwrite=True, buffersize=4194304, blocksize=4194304)

## <a name="delete-a-directory"></a><span data-ttu-id="99ca2-179">Supprimer un répertoire</span><span class="sxs-lookup"><span data-stu-id="99ca2-179">Delete a directory</span></span>

    ## Delete a directory
    adlsFileSystemClient.rm('/mysampledirectory', recursive=True)

## <a name="see-also"></a><span data-ttu-id="99ca2-180">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="99ca2-180">See also</span></span>

- [<span data-ttu-id="99ca2-181">Sécuriser les données dans Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="99ca2-181">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
- [<span data-ttu-id="99ca2-182">Utiliser Azure Data Lake Analytics avec Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="99ca2-182">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
- [<span data-ttu-id="99ca2-183">Utiliser Azure HDInsight avec Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="99ca2-183">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
- [<span data-ttu-id="99ca2-184">Data Lake Store .NET SDK Reference (Informations de référence sur le Kit de développement logiciel (SDK) .NET Azure Data Lake Store)</span><span class="sxs-lookup"><span data-stu-id="99ca2-184">Data Lake Store .NET SDK Reference</span></span>](https://msdn.microsoft.com/library/mt581387.aspx)
- [<span data-ttu-id="99ca2-185">Data Lake Store REST Reference (Informations de référence sur les API REST Data Lake Store)</span><span class="sxs-lookup"><span data-stu-id="99ca2-185">Data Lake Store REST Reference</span></span>](https://msdn.microsoft.com/library/mt693424.aspx)
