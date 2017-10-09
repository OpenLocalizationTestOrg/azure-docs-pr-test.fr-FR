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
# <a name="get-started-with-azure-data-lake-analytics-using-rest-apis"></a>Prise en main d’Azure Data Lake Analytics à l’aide d’API REST
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

Découvrez comment toouse WebHDFS REST API et données Lake Analytique reste toomanage Analytique lac de données des comptes, des travaux et de catalogue. 

## <a name="prerequisites"></a>Composants requis
* **Un abonnement Azure**. Consultez la page [Obtention d’un essai gratuit d’Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Créez une application Azure Active Directory**. Vous utilisez hello Azure AD tooauthenticate hello Analytique lac de données une application avec Azure AD. Il existe tooauthenticate différentes approches avec Azure AD, qui sont **l’authentification de l’utilisateur final** ou **l’authentification de service**. Pour plus d’informations sur la façon d’et tooauthenticate, consultez [authentifier avec Analytique lac de données à l’aide d’Azure Active Directory](../data-lake-store/data-lake-store-authenticate-using-active-directory.md).
* [cURL](http://curl.haxx.se/). Cet article utilise toodemonstrate cURL comment toomake API REST appelle par rapport à un compte Analytique lac de données.

## <a name="authenticate-with-azure-active-directory"></a>S’authentifier à l’aide d’Azure Active Directory
Il existe deux méthodes d’authentification avec Azure Active Directory.

### <a name="end-user-authentication-interactive"></a>Authentification de l’utilisateur final (interactive)
À l’aide de cette méthode, application demande toolog d’utilisateur hello dans et toutes les opérations de hello sont effectuées dans le contexte de hello d’utilisateur de hello. 

Pour l’authentification interactive, procédez comme suit :

1. Via votre application, la redirection toohello d’utilisateur hello suivant l’URL :
   
        https://login.microsoftonline.com/<TENANT-ID>/oauth2/authorize?client_id=<CLIENT-ID>&response_type=code&redirect_uri=<REDIRECT-URI>
   
   > [!NOTE]
   > \<URI de redirection > doit toobe codé à utiliser dans une URL. Par conséquent, pour https://localhost, utilisez `https%3A%2F%2Flocalhost`)
   > 
   > 
   
    Fins hello de ce didacticiel, vous pouvez remplacer les valeurs d’espace réservé hello URL hello ci-dessus et collez-le dans la barre d’adresses d’un navigateur web. Vous serez redirigé tooauthenticate à l’aide de votre connexion à Azure. Une fois correctement vous connecter, réponse de hello est affichée dans la barre d’adresses du navigateur hello. réponse de Hello sera Bonjour suivant le format :
   
        http://localhost/?code=<AUTHORIZATION-CODE>&session_state=<GUID>
2. Capturer le code d’autorisation de hello de réponse de hello. Pour ce didacticiel, vous pouvez copier le code d’autorisation de hello à partir de la barre d’adresses hello de navigateur hello et passer dans hello POST demande toohello jeton point de terminaison, comme indiqué ci-dessous :
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token \
        -F redirect_uri=<REDIRECT-URI> \
        -F grant_type=authorization_code \
        -F resource=https://management.core.windows.net/ \
        -F client_id=<CLIENT-ID> \
        -F code=<AUTHORIZATION-CODE>
   
   > [!NOTE]
   > Dans ce cas, hello \<URI de redirection > ne doivent pas être encodé.
   > 
   > 
3. réponse de Hello est un objet JSON qui contient un jeton d’accès (par exemple, `"access_token": "<ACCESS_TOKEN>"`) et un jeton d’actualisation (par exemple, `"refresh_token": "<REFRESH_TOKEN>"`). Votre application utilise hello jeton d’accès lors de l’accès d’Azure Data Lake Store et tooget de jeton hello actualiser un autre jeton d’accès quand un jeton d’accès expire.
   
        {"token_type":"Bearer","scope":"user_impersonation","expires_in":"3599","expires_on":"1461865782","not_before":    "1461861882","resource":"https://management.core.windows.net/","access_token":"<REDACTED>","refresh_token":"<REDACTED>","id_token":"<REDACTED>"}
4. Expiration du jeton d’accès hello, vous pouvez demander un nouveau jeton d’accès à l’aide du jeton d’actualisation hello, comme indiqué ci-dessous :
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
             -F grant_type=refresh_token \
             -F resource=https://management.core.windows.net/ \
             -F client_id=<CLIENT-ID> \
             -F refresh_token=<REFRESH-TOKEN>

Pour plus d’informations sur l’authentification utilisateur interactive, consultez [Flux d’octroi d’un code d’autorisation](https://msdn.microsoft.com/library/azure/dn645542.aspx).

### <a name="service-to-service-authentication-non-interactive"></a>Authentification de service à service (non interactive)
À l’aide de cette méthode, application fournit ses propres informations d’identification des opérations de hello tooperform. Pour ce faire, vous devez émettre une demande POST comme hello illustré ci-dessous : 

    curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
      -F grant_type=client_credentials \
      -F resource=https://management.core.windows.net/ \
      -F client_id=<CLIENT-ID> \
      -F client_secret=<AUTH-KEY>

sortie Hello de cette demande inclut un jeton d’autorisation (indiqué par `access-token` dans la sortie de hello ci-dessous) que vous allez transmettre ensuite avec vos appels d’API REST. Enregistrez ce jeton d’authentification dans un fichier texte, car vous en aurez besoin plus loin dans cet article.

    {"token_type":"Bearer","expires_in":"3599","expires_on":"1458245447","not_before":"1458241547","resource":"https://management.core.windows.net/","access_token":"<REDACTED>"}

Cet article utilise hello **non interactif** approche. Pour plus d’informations sur la non interactif (appels de service), consultez [tooservice les appels à l’aide des informations d’identification de Service](https://msdn.microsoft.com/library/azure/dn645543.aspx).

## <a name="create-a-data-lake-analytics-account"></a>Créer un compte Data Lake Analytics
Vous devez créer un groupe de ressources Azure et un compte Data Lake Store avant de pouvoir créer un compte Data Lake Analytics.  Consultez [Créer un compte Data Lake Store](../data-lake-store/data-lake-store-get-started-rest-api.md#create-a-data-lake-store-account).

Hello suivant de commande Curl indique comment toocreate un compte :

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -H "Content-Type: application/json" https://management.azure.com/subscriptions/<AzureSubscriptionID>/resourceGroups/<AzureResourceGroupName>/providers/Microsoft.DataLakeAnalytics/accounts/<NewAzureDataLakeAnalyticsAccountName>?api-version=2016-11-01 -d@"C:\tutorials\adla\CreateDataLakeAnalyticsAccountRequest.json"

Remplacez \< `REDACTED` \> avec un jeton d’autorisation de hello, \< `AzureSubscriptionID` \> avec votre ID d’abonnement \< `AzureResourceGroupName` \> avec une ressource Azure existante Nom du groupe, et \< `NewAzureDataLakeAnalyticsAccountName` \> avec un nouveau nom de compte d’Analytique Data Lake. charge utile de demande Hello pour cette commande est contenue dans hello **CreateDatalakeAnalyticsAccountRequest.json** fichier fourni pour hello `-d` paramètre ci-dessus. contenu Hello du fichier de input.json hello ressemblent aux suivantes de hello :

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


## <a name="list-data-lake-analytics-accounts-in-a-subscription"></a>Énumérer les comptes Data Lake Analytics d’un abonnement
Hello enroulement de la commande suivante montre comment toolist comptes dans un abonnement :

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/<AzureSubscriptionID>/providers/Microsoft.DataLakeAnalytics/Accounts?api-version=2016-11-01

Remplacez \< `REDACTED` \> avec un jeton d’autorisation de hello, \< `AzureSubscriptionID` \> avec votre ID d’abonnement. résultat de Hello est similaire à :

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

## <a name="get-information-about-a-data-lake-analytics-account"></a>Obtenir des informations sur un compte Data Lake Analytics
Hello suivant de commande Curl indique comment tooget une information de compte :

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/<AzureSubscriptionID>/resourceGroups/<AzureResourceGroupName>/providers/Microsoft.DataLakeAnalytics/accounts/<DataLakeAnalyticsAccountName>?api-version=2015-11-01

Remplacez \< `REDACTED` \> avec un jeton d’autorisation de hello, \< `AzureSubscriptionID` \> avec votre ID d’abonnement \< `AzureResourceGroupName` \> avec une ressource Azure existante Nom du groupe, et \< `DataLakeAnalyticsAccountName` \> avec nom hello d’un compte d’Analytique Data Lake existant. résultat de Hello est similaire à :

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

## <a name="list-data-lake-stores-of-a-data-lake-analytics-account"></a>Répertorier les magasins Data Lake d’un compte Data Lake Analytics
Hello enroulement de la commande suivante montre en quoi les magasins d’un compte toolist Data Lake :

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/<AzureSubscriptionID>/resourceGroups/<AzureResourceGroupName>/providers/Microsoft.DataLakeAnalytics/accounts/<DataLakeAnalyticsAccountName>/DataLakeStoreAccounts/?api-version=2016-11-01

Remplacez \< `REDACTED` \> avec un jeton d’autorisation de hello, \< `AzureSubscriptionID` \> avec votre ID d’abonnement \< `AzureResourceGroupName` \> avec une ressource Azure existante Nom du groupe, et \< `DataLakeAnalyticsAccountName` \> avec nom hello d’un compte d’Analytique Data Lake existant. résultat de Hello est similaire à :

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

## <a name="submit-u-sql-jobs"></a>Envoyer des travaux U-SQL
Hello suivant de commande Curl indique comment le travail de toosubmit U-SQL :

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" https://<DataLakeAnalyticsAccountName>.azuredatalakeanalytics.net/Jobs/<NewGUID>?api-version=2016-03-20-preview -d@"C:\tutorials\adla\SubmitADLAJob.json"

Remplacez \< `REDACTED` \> avec un jeton d’autorisation de hello, \< `DataLakeAnalyticsAccountName` \> avec nom hello d’un compte d’Analytique Data Lake existant. charge utile de demande Hello pour cette commande est contenue dans hello **SubmitADLAJob.json** fichier fourni pour hello `-d` paramètre ci-dessus. contenu Hello du fichier de input.json hello ressemblent aux suivantes de hello :

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

résultat de Hello est similaire à :

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


## <a name="list-u-sql-jobs"></a>Répertorier des travaux U-SQL
Hello suivant de commande Curl indique comment les travaux toolist U-SQL :

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://<DataLakeAnalyticsAccountName>.azuredatalakeanalytics.net/Jobs?api-version=2016-11-01 

Remplacez \< `REDACTED` \> avec un jeton d’autorisation de hello, et \< `DataLakeAnalyticsAccountName` \> avec nom hello d’un compte d’Analytique Data Lake existant. 

résultat de Hello est similaire à :

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


## <a name="get-catalog-items"></a>Obtenir les éléments du catalogue
Hello enroulement de la commande suivante montre comment les bases de données tooget hello de hello catalogue :

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://<DataLakeAnalyticsAccountName>.azuredatalakeanalytics.net/catalog/usql/databases?api-version=2016-11-01

résultat de Hello est similaire à :

    {
    "@odata.context":"https://myadla0831.azuredatalakeanalytics.net/sqlip/$metadata#databases","value":[
        {
        "computeAccountName":"myadla0831","databaseName":"mytest","version":"f6956327-90b8-4648-ad8b-de3ff09274ea"
        },{
        "computeAccountName":"myadla0831","databaseName":"master","version":"e8bca908-cc73-41a3-9564-e9bcfaa21f4e"
        }
    ]
    }

## <a name="see-also"></a>Voir aussi
* toosee une requête plus complexe, consultez [site Web d’analyse se connecte à l’aide d’Analytique de LAC de données Azure](data-lake-analytics-analyze-weblogs.md).
* tooget en main le développement d’applications SQL-U, consultez [scripts développer U-SQL à l’aide de Data Lake Tools pour Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).
* toolearn U-SQL, consultez [prise en main langage lac de données Azure Analytique U-SQL](data-lake-analytics-u-sql-get-started.md).
* Pour les tâches de gestion, consultez [Gestion d’Azure Data Lake Analytics à l’aide du portail Azure](data-lake-analytics-manage-use-portal.md).
* tooget une vue d’ensemble de données de LAC Analytique, consultez [vue d’ensemble Analytique de LAC de données Azure](data-lake-analytics-overview.md).
* toosee hello même didacticiel à l’aide d’autres outils, cliquez sur les sélecteurs d’onglet hello haut hello de page de hello.

