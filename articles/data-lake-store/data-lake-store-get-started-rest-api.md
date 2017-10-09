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
# <a name="get-started-with-azure-data-lake-store-using-rest-apis"></a>Prise en main d’Azure Data Lake Store avec les API REST
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

Dans cet article, vous allez apprendre comment toouse WebHDFS REST API et API REST de données Lake Store tooperform compte d’administration ainsi que des opérations de système de fichiers sur Azure Data Lake Store. Azure Data Lake Store expose ses propres API REST pour les opérations de gestion des comptes. Toutefois, comme Data Lake Store est compatible avec HDFS et l’écosystème Hadoop, il prend en charge l’utilisation des API REST de WebHDFS pour les opérations de système de fichiers.

> [!NOTE]
> Pour plus d’informations sur la prise en charge des API REST de hello pour Data Lake Store, consultez [référence d’API REST Azure données Lake Store](https://msdn.microsoft.com/library/mt693424.aspx).
> 
> 

## <a name="prerequisites"></a>Composants requis
* **Un abonnement Azure**. Consultez la page [Obtention d’un essai gratuit d’Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Créez une application Azure Active Directory**. Vous utilisez hello Azure AD tooauthenticate hello Data Lake Store une application avec Azure AD. Il existe tooauthenticate différentes approches avec Azure AD, qui sont **l’authentification de l’utilisateur final** ou **l’authentification de service**. Pour plus d’informations sur la façon d’et tooauthenticate, consultez [l’authentification de l’utilisateur final](data-lake-store-end-user-authenticate-using-active-directory.md) ou [l’authentification de service](data-lake-store-authenticate-using-active-directory.md).
* [cURL](http://curl.haxx.se/). Cet article utilise toodemonstrate cURL comment toomake API REST appelle par rapport à un compte Data Lake Store.

## <a name="how-do-i-authenticate-using-azure-active-directory"></a>Comment s’authentifier à l’aide d’Azure Active Directory ?
Vous pouvez utiliser deux approches tooauthenticate à l’aide d’Azure Active Directory.

### <a name="end-user-authentication-interactive"></a>Authentification de l’utilisateur final (interactive)
Dans ce scénario, application hello invite toolog d’utilisateur hello dans et toutes les opérations de hello sont effectuées dans le contexte de hello d’utilisateur de hello. Effectuer hello comme suit pour l’authentification interactive.

1. Via votre application, la redirection toohello d’utilisateur hello suivant l’URL :
   
        https://login.microsoftonline.com/<TENANT-ID>/oauth2/authorize?client_id=<APPLICATION-ID>&response_type=code&redirect_uri=<REDIRECT-URI>
   
   > [!NOTE]
   > \<URI de redirection > doit toobe codé à utiliser dans une URL. Par conséquent, pour https://localhost, utilisez `https%3A%2F%2Flocalhost`)
   > 
   > 
   
    Fins hello de ce didacticiel, vous pouvez remplacer les valeurs d’espace réservé hello URL hello ci-dessus et collez-le dans la barre d’adresses d’un navigateur web. Vous serez redirigé tooauthenticate à l’aide de votre connexion à Azure. Une fois que vous connecter avec succès, réponse de hello est affichée dans la barre d’adresses du navigateur hello. réponse de Hello sera Bonjour suivant le format :
   
        http://localhost/?code=<AUTHORIZATION-CODE>&session_state=<GUID>
2. Capturer le code d’autorisation de hello de réponse de hello. Pour ce didacticiel, vous pouvez copier le code d’autorisation de hello à partir de la barre d’adresses hello de navigateur hello et passer dans hello POST demande toohello jeton point de terminaison, comme indiqué ci-dessous :
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token \
        -F redirect_uri=<REDIRECT-URI> \
        -F grant_type=authorization_code \
        -F resource=https://management.core.windows.net/ \
        -F client_id=<APPLICATION-ID> \
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
             -F client_id=<APPLICATION-ID> \
             -F refresh_token=<REFRESH-TOKEN>

Pour plus d’informations sur l’authentification utilisateur interactive, consultez [Flux d’octroi d’un code d’autorisation](https://msdn.microsoft.com/library/azure/dn645542.aspx).

### <a name="service-to-service-authentication-non-interactive"></a>Authentification de service à service (non interactive)
Dans ce scénario, application hello de hello fournit des opérations de hello tooperform ses propres informations d’identification. Pour ce faire, vous devez émettre une demande POST, comme illustré ci-dessous hello. 

    curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
      -F grant_type=client_credentials \
      -F resource=https://management.core.windows.net/ \
      -F client_id=<CLIENT-ID> \
      -F client_secret=<AUTH-KEY>

sortie Hello de cette demande inclut un jeton d’autorisation (indiqué par `access-token` dans la sortie de hello ci-dessous) que vous allez transmettre ensuite avec vos appels d’API REST. Enregistrez ce jeton d’authentification dans un fichier texte, car vous en aurez besoin plus loin dans cet article.

    {"token_type":"Bearer","expires_in":"3599","expires_on":"1458245447","not_before":"1458241547","resource":"https://management.core.windows.net/","access_token":"<REDACTED>"}

Cet article utilise hello **non interactif** approche. Pour plus d’informations sur la non interactif (appels de service), consultez [tooservice les appels à l’aide des informations d’identification de Service](https://msdn.microsoft.com/library/azure/dn645543.aspx).

## <a name="create-a-data-lake-store-account"></a>Créer un compte Data Lake Store
Cette opération est basée sur les appels hello API REST défini [ici](https://msdn.microsoft.com/library/mt694078.aspx).

Utilisez hello enroulement de la commande suivante. Remplacez **\<yourstorename>** par le nom de votre Data Lake Store.

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -H "Content-Type: application/json" https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.DataLakeStore/accounts/<yourstorename>?api-version=2015-10-01-preview -d@"C:\temp\input.json"

Bonjour au-dessus de commande, remplacez \< `REDACTED` \> avec le jeton d’autorisation hello extrait précédemment. charge utile de demande Hello pour cette commande est contenue dans hello **input.json** fichier fourni pour hello `-d` paramètre ci-dessus. contenu Hello du fichier de input.json hello ressemblent aux suivantes de hello :

    {
    "location": "eastus2",
    "tags": {
        "department": "finance"
        },
    "properties": {}
    }    

## <a name="create-folders-in-a-data-lake-store-account"></a>Créer des dossiers dans un compte Data Lake Store
Cette opération est basée sur appel hello API REST de WebHDFS défini [ici](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Make_a_Directory).

Utilisez hello enroulement de la commande suivante. Remplacez **\<yourstorename>** par le nom de votre Data Lake Store.

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -d "" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/?op=MKDIRS'

Bonjour au-dessus de commande, remplacez \< `REDACTED` \> avec le jeton d’autorisation hello extrait précédemment. Cette commande crée un répertoire appelé **mytempdir** sous le dossier racine de hello de votre compte Data Lake Store.

Vous devez voir une réponse similaire à ceci si l’opération de hello terminée :

    {"boolean":true}

## <a name="list-folders-in-a-data-lake-store-account"></a>Afficher la liste des dossiers dans un compte Data Lake Store
Cette opération est basée sur appel hello API REST de WebHDFS défini [ici](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#List_a_Directory).

Utilisez hello enroulement de la commande suivante. Remplacez **\<yourstorename>** par le nom de votre Data Lake Store.

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/?op=LISTSTATUS'

Bonjour au-dessus de commande, remplacez \< `REDACTED` \> avec le jeton d’autorisation hello extrait précédemment.

Vous devez voir une réponse similaire à ceci si l’opération de hello terminée :

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

## <a name="upload-data-into-a-data-lake-store-account"></a>Charger des données dans un compte Azure Data Lake Store
Cette opération est basée sur appel hello API REST de WebHDFS défini [ici](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Create_and_Write_to_a_File).

Utilisez hello enroulement de la commande suivante. Remplacez **\<yourstorename>** par le nom de votre Data Lake Store.

    curl -i -X PUT -L -T 'C:\temp\list.txt' -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/list.txt?op=CREATE'

Bonjour ci-dessus syntaxe **-T** paramètre est l’emplacement hello du fichier hello vous téléchargez.

sortie de Hello est similaire toohello suivantes :
   
    HTTP/1.1 307 Temporary Redirect
    ...
    Location: https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/list.txt?op=CREATE&write=true
    ...
    Content-Length: 0

    HTTP/1.1 100 Continue

    HTTP/1.1 201 Created
    ...

## <a name="read-data-from-a-data-lake-store-account"></a>Lire les données d’un compte Azure Data Lake Store
Cette opération est basée sur appel hello API REST de WebHDFS défini [ici](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Open_and_Read_a_File).

La lecture des données d’un compte Data Lake Store s’effectue en deux étapes.

* D’abord vous envoyez une demande GET sur le point de terminaison hello `https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN`. Cette méthode retourne une emplacement toosubmit hello suivante demande GET pour.
* Vous puis demander hello GET sur le point de terminaison hello `https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN&read=true`. Cette action affiche le contenu hello du fichier de hello.

Toutefois, les, car il n’existe aucune différence hello des paramètres d’entrée entre hello hello et tout d’abord deuxième étape, vous pouvez utiliser les hello `-L` première demande paramètre toosubmit hello. `-L`option essentiellement combine deux requêtes en une seule et fera cURL demande hello sur le nouvel emplacement de hello de restauration par progression. Enfin, hello de tous les appels de demande hello est affiché, comme indiqué ci-dessous. Remplacez **\<yourstorename>** par le nom de votre Data Lake Store.

    curl -i -L GET -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN'

Vous devez voir s’afficher une sortie similaire toohello :

    HTTP/1.1 307 Temporary Redirect
    ...
    Location: https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/somerandomfile.txt?op=OPEN&read=true
    ...

    HTTP/1.1 200 OK
    ...

    Hello, Data Lake Store user!

## <a name="rename-a-file-in-a-data-lake-store-account"></a>Renommer un fichier dans un compte Data Lake Store
Cette opération est basée sur appel hello API REST de WebHDFS défini [ici](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Rename_a_FileDirectory).

Suivant de hello utilisez cURL commande toorename un fichier. Remplacez **\<yourstorename>** par le nom de votre Data Lake Store.

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -d "" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=RENAME&destination=/mytempdir/myinputfile1.txt'

Vous devez voir s’afficher une sortie similaire toohello :

    HTTP/1.1 200 OK
    ...

    {"boolean":true}

## <a name="delete-a-file-from-a-data-lake-store-account"></a>Supprimer un fichier dans un compte Data Lake Store
Cette opération est basée sur appel hello API REST de WebHDFS défini [ici](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Delete_a_FileDirectory).

Suivant de hello utilisez cURL commande toodelete un fichier. Remplacez **\<yourstorename>** par le nom de votre Data Lake Store.

    curl -i -X DELETE -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile1.txt?op=DELETE'

Vous devez voir une sortie semblable à hello suivante :

    HTTP/1.1 200 OK
    ...

    {"boolean":true}

## <a name="delete-a-data-lake-store-account"></a>Supprimer un compte Data Lake Store
Cette opération est basée sur les appels hello API REST défini [ici](https://msdn.microsoft.com/library/mt694075.aspx).

Suivant de hello utilisez cURL commande toodelete un compte Data Lake Store. Remplacez **\<yourstorename>** par le nom de votre Data Lake Store.

    curl -i -X DELETE -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.DataLakeStore/accounts/<yourstorename>?api-version=2015-10-01-preview

Vous devez voir une sortie semblable à hello suivante :

    HTTP/1.1 200 OK
    ...
    ...

## <a name="see-also"></a>Voir aussi
* [Ouvrir des applications Big Data open source compatibles avec Azure Data Lake Store](data-lake-store-compatible-oss-other-applications.md)

