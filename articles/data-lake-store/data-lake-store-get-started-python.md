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
# <a name="get-started-with-azure-data-lake-store-using-python"></a>Prise en main d’Azure Data Lake Store à l’aide de Python

> [!div class="op_single_selector"]
> * [Portail](data-lake-store-get-started-portal.md)
> * [PowerShell](data-lake-store-get-started-powershell.md)
> * [Kit SDK .NET](data-lake-store-get-started-net-sdk.md)
> * [Kit SDK Java](data-lake-store-get-started-java-sdk.md)
> * [API REST](data-lake-store-get-started-rest-api.md)
> * [Azure CLI 2.0](data-lake-store-get-started-cli-2.0.md)
> * [Node.JS](data-lake-store-manage-use-nodejs.md)
> * [Python](data-lake-store-get-started-python.md)
>
>

Découvrez comment toouse hello Python SDK pour les opérations de base tooperform Azure et d’Azure Data Lake Store telles que la création des dossiers, télécharger des fichiers de données, etc.. Pour plus d’informations sur Data Lake, consultez [Azure Data Lake Store](data-lake-store-overview.md).

## <a name="prerequisites"></a>Composants requis

* **Python** Pour télécharger Python, accédez [ici](https://www.python.org/downloads/). Cet article utilise Python version 3.5.2.

* **Un abonnement Azure**. Consultez la page [Obtention d’un essai gratuit d’Azure](https://azure.microsoft.com/pricing/free-trial/).

* **Créez une application Azure Active Directory**. Vous utilisez hello Azure AD tooauthenticate hello Data Lake Store une application avec Azure AD. Il existe tooauthenticate différentes approches avec Azure AD, qui sont **l’authentification de l’utilisateur final** ou **l’authentification de service**. Pour plus d’informations sur la façon d’et tooauthenticate, consultez [l’authentification de l’utilisateur final](data-lake-store-end-user-authenticate-using-active-directory.md) ou [l’authentification de service](data-lake-store-authenticate-using-active-directory.md).

## <a name="install-hello-modules"></a>Installer les modules hello

toowork avec Data Lake Store à l’aide de Python, vous devez tooinstall trois modules.

* Hello `azure-mgmt-resource` module. Cela inclut les modules Azure pour Active Directory, etc.
* Hello `azure-mgmt-datalake-store` module. Cela inclut les opérations de gestion de compte Azure Data Lake Store hello. Pour plus d’informations sur ce module, consultez les [informations de référence sur les modules de gestion Azure Data Lake Store](http://azure-sdk-for-python.readthedocs.io/en/latest/sample_azure-mgmt-datalake-store.html).
* Hello `azure-datalake-store` module. Cela inclut les opérations de système de fichiers de hello Azure Data Lake Store. Pour plus d’informations sur ce module, consultez les [informations de référence sur les modules du système de fichiers Azure Data Lake Store](http://azure-datalake-store.readthedocs.io/en/latest/).

Utilisez hello suivant des modules de commandes tooinstall hello.

```
pip install azure-mgmt-resource
pip install azure-mgmt-datalake-store
pip install azure-datalake-store
```

## <a name="create-a-new-python-application"></a>Créer une application Python

1. Bonjour IDE de votre choix, créez une application Python, par exemple, **mysample.py**.

2. Ajouter hello suivant des modules de lignes tooimport hello requis

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

3. Enregistrer les modifications toomysample.py.

## <a name="authentication"></a>Authentification

Dans cette section, nous parlons de tooauthenticate de différentes façons hello avec Azure AD. options de Hello disponibles sont :

* Authentification de l’utilisateur final
* Authentification de service à service
* Authentification multifacteur

Vous devez utiliser ces options d’authentification pour les modules de gestion des systèmes de fichiers et des comptes.

### <a name="end-user-authentication-for-account-management"></a>Authentification de l’utilisateur final pour la gestion du compte

Utilisez cette tooauthenticate avec Azure AD pour les opérations de gestion de compte (création/suppression compte Data Lake Store, etc..). Vous devez fournir un nom d’utilisateur et un mot de passe d’utilisateur Azure AD. Notez que l’utilisateur hello ne doit pas être configuré pour l’authentification multifacteur.

    user = input('Enter hello user tooauthenticate with that has permission toosubscription: ')
    password = getpass.getpass()

    credentials = UserPassCredentials(user, password)

### <a name="end-user-authentication-for-filesystem-operations"></a>Authentification de l’utilisateur final pour les opérations du système de fichiers

Utilisez cette tooauthenticate avec Azure AD pour les opérations de système de fichiers (créer de dossier, fichier de téléchargement, etc.).. Utilisez-la avec une application **cliente native** Azure AD. utilisateur Hello Azure AD que vous fournissez des informations d’identification ne doit pas être configuré pour l’authentification multifacteur.

    tenant_id = 'FILL-IN-HERE'
    client_id = 'FILL-IN-HERE'
    user = input('Enter hello user tooauthenticate with that has permission toosubscription: ')
    password = getpass.getpass()

    token = lib.auth(tenant_id, user, password, client_id)

### <a name="service-to-service-authentication-with-client-secret-for-account-management"></a>L’authentification de service à service avec clé secrète client pour al gestion de compte

Utilisez cette tooauthenticate avec Azure AD pour les opérations de gestion de compte (création/suppression compte Data Lake Store, etc..). Hello suivant extrait de code peut être utilisé tooauthenticate votre application en mode non interactif, à l’aide de la clé secrète du client hello pour un principal de l’application ou le service. Utilisez-le avec une « application web » Azure AD existante.

    credentials = ServicePrincipalCredentials(client_id = 'FILL-IN-HERE', secret = 'FILL-IN-HERE', tenant = 'FILL-IN-HERE')

### <a name="service-to-service-authentication-with-client-secret-for-filesystem-operations"></a>Authentification de service à service avec clé secrète client pour les opérations du système de fichiers

Utilisez cette tooauthenticate avec Azure AD pour les opérations de système de fichiers (créer de dossier, fichier de téléchargement, etc.).. Hello suivant extrait de code peut être utilisé tooauthenticate votre application en mode non interactif, à l’aide de la clé secrète du client hello pour un principal de l’application ou le service. Utilisez-le avec une « application web » Azure AD existante.

    token = lib.auth(tenant_id = 'FILL-IN-HERE', client_secret = 'FILL-IN-HERE', client_id = 'FILL-IN-HERE')

### <a name="multi-factor-authentication-for-account-management"></a>Authentification multifacteur pour la gestion des comptes

Utilisez cette tooauthenticate avec Azure AD pour les opérations de gestion de compte (création/suppression compte Data Lake Store, etc..). Hello extrait de code suivant peut être utilisé tooauthenticate votre application à l’aide de l’authentification multifacteur. Utilisez-le avec une « application web » Azure AD existante.

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

### <a name="multi-factor-authentication-for-filesystem-management"></a>Authentification multifacteur pour la gestion des systèmes de fichiers

Utilisez cette tooauthenticate avec Azure AD pour les opérations de système de fichiers (créer de dossier, fichier de téléchargement, etc.).. Hello extrait de code suivant peut être utilisé tooauthenticate votre application à l’aide de l’authentification multifacteur. Utilisez-le avec une « application web » Azure AD existante.

    token = lib.auth(tenant_id='FILL-IN-HERE')

## <a name="create-an-azure-resource-group"></a>Créer un groupe de ressources Azure

Utilisez hello suivant extrait de code toocreate un groupe de ressources Azure :

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

## <a name="create-clients-and-data-lake-store-account"></a>Créer des clients et un compte Data Lake Store

Hello suivant extrait tout d’abord crée un client de compte Data Lake Store hello. Il utilise hello client objet toocreate un compte Data Lake Store. Enfin, extrait de code hello crée un objet de client de système de fichiers.

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

## <a name="list-hello-data-lake-store-accounts"></a>Liste des comptes Data Lake Store hello

    ## List hello existing Data Lake Store accounts
    result_list_response = adlsAcctClient.account.list()
    result_list = list(result_list_response)
    for items in result_list:
        print(items)

## <a name="create-a-directory"></a>Créer un répertoire

    ## Create a directory
    adlsFileSystemClient.mkdir('/mysampledirectory')

## <a name="upload-a-file"></a>Charger un fichier


    ## Upload a file
    multithread.ADLUploader(adlsFileSystemClient, lpath='C:\\data\\mysamplefile.txt', rpath='/mysampledirectory/mysamplefile.txt', nthreads=64, overwrite=True, buffersize=4194304, blocksize=4194304)


## <a name="download-a-file"></a>Téléchargement d’un fichier

    ## Download a file
    multithread.ADLDownloader(adlsFileSystemClient, lpath='C:\\data\\mysamplefile.txt.out', rpath='/mysampledirectory/mysamplefile.txt', nthreads=64, overwrite=True, buffersize=4194304, blocksize=4194304)

## <a name="delete-a-directory"></a>Supprimer un répertoire

    ## Delete a directory
    adlsFileSystemClient.rm('/mysampledirectory', recursive=True)

## <a name="see-also"></a>Voir aussi

- [Sécuriser les données dans Data Lake Store](data-lake-store-secure-data.md)
- [Utiliser Azure Data Lake Analytics avec Data Lake Store](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
- [Utiliser Azure HDInsight avec Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md)
- [Data Lake Store .NET SDK Reference (Informations de référence sur le Kit de développement logiciel (SDK) .NET Azure Data Lake Store)](https://msdn.microsoft.com/library/mt581387.aspx)
- [Data Lake Store REST Reference (Informations de référence sur les API REST Data Lake Store)](https://msdn.microsoft.com/library/mt693424.aspx)
