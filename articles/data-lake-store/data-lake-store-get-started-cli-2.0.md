---
title: "aaaUse 2.0 de ligne de commande Azure interface tooget main d’Azure Data Lake Store | Documents Microsoft"
description: "Utilisez la ligne de commande interplateforme Azure 2.0 toocreate un compte Data Lake Store et effectuer des opérations de base"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 4ffa0f4a-1cca-46ac-803d-1fc8538c685b
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 374dcd6cdbc13ad19f6c65502329986ecae60ef2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-azure-cli-20"></a>Prise en main d’Azure Data Lake Store avec Azure CLI 2.0
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

Découvrez comment toouse Azure CLI 2.0 toocreate stocker un lac de données Azure compte et effectuer des opérations de base telles que la création de dossiers, téléchargent et téléchargement les fichiers de données, supprimez votre compte, un etc.. Pour plus d’informations sur Data Lake Store, consultez [Vue d’ensemble de Data Lake Store](data-lake-store-overview.md).

Bonjour Azure CLI 2.0 est la nouvelle expérience de ligne de commande de Azure pour la gestion des ressources Azure. Elle peut être utilisée sur macOS, Linux et Windows. Pour plus d’informations, voir [Présentation d’Azure CLI 2.0](https://docs.microsoft.com/cli/azure/overview). Vous pouvez également consulter hello [Azure Data Lake Store CLI 2.0 référence](https://docs.microsoft.com/cli/azure/dls) pour une liste complète des commandes et la syntaxe.


## <a name="prerequisites"></a>Composants requis
Avant de commencer cet article, vous devez disposer de hello :

* **Un abonnement Azure**. Consultez la page [Obtention d’un essai gratuit d’Azure](https://azure.microsoft.com/pricing/free-trial/).

* **Azure CLI 2.0** - Voir [Installer Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) pour plus d’instructions.

## <a name="authentication"></a>Authentification

Pour l’authentification auprès de Data Lake Store, cet article utilise une approche plus simple où vous vous connectez en tant qu’utilisateur final. Hello accès niveau tooData Lake Store compte de système de fichiers et est ensuite régie par niveau d’accès hello Hello à l’utilisateur connecté. Toutefois, il existe d’autres approches en tant que bien tooauthenticate avec Data Lake Store, qui sont **l’authentification de l’utilisateur final** ou **l’authentification de service**. Pour plus d’informations sur la façon d’et tooauthenticate, consultez [l’authentification de l’utilisateur final](data-lake-store-end-user-authenticate-using-active-directory.md) ou [l’authentification de service](data-lake-store-authenticate-using-active-directory.md).


## <a name="log-in-tooyour-azure-subscription"></a>Ouvrez une session dans tooyour abonnement Azure

1. Connectez-vous à votre abonnement Azure.

    ```azurecli
    az login
    ```

    Vous obtenez un toouse du code à l’étape suivante de hello. Utiliser un web navigateur tooopen hello page https://aka.ms/devicelogin et entrez tooauthenticate de code hello. Vous êtes invité à toolog à l’aide de vos informations d’identification.

2. Une fois que vous vous connectez, des listes de fenêtres hello tous les hello abonnements Azure qui sont associés à votre compte. Utilisez hello suivant commande toouse un abonnement spécifique.
   
    ```azurecli
    az account set --subscription <subscription id> 
    ```

## <a name="create-an-azure-data-lake-store-account"></a>Créer un compte Azure Data Lake Store

1. Créez un groupe de ressources. Bonjour la commande suivante, fournir des valeurs de paramètre souhaité toouse hello. Si le nom de l’emplacement hello contient des espaces, placez-le entre guillemets. Par exemple, « East US 2 ». 
   
    ```azurecli
    az group create --location "East US 2" --name myresourcegroup
    ```

2. Créer un compte Data Lake Store de hello.
   
    ```azurecli
    az dls account create --account mydatalakestore --resource-group myresourcegroup
    ```

## <a name="create-folders-in-a-data-lake-store-account"></a>Créer des dossiers dans un compte Data Lake Store

Vous pouvez créer des dossiers sous votre toomanage de compte Azure Data Lake Store et stocker des données. Hello utilisation suivant toocreate commande un dossier appelé **MonNouveauDossier** à racine hello hello Data Lake Store.

```azurecli
az dls fs create --account mydatalakestore --path /mynewfolder --folder
```

> [!NOTE]
> Hello `--folder` paramètre permet de s’assurer que les commandes hello crée un dossier. Si ce paramètre n’est pas présent, la commande hello crée un fichier vide appelé MonNouveauDossier à racine hello hello compte Data Lake Store.
> 
>

## <a name="upload-data-tooa-data-lake-store-account"></a>Télécharger le compte de données tooa Data Lake Store

Vous pouvez télécharger des données tooData Lake Store directement dans le dossier de niveau ou tooa de racine hello que vous avez créé dans le compte de hello. Hello d’extraits de code ci-dessous montrent comment tooupload un dossier de toohello de données exemple (**MonNouveauDossier**) vous avez créé dans la section précédente de hello.

Si vous recherchez des tooupload de données d’exemple, vous pouvez obtenir hello **Ambulance données** dossier hello [référentiel Git de LAC de données Azure](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData). Télécharger le fichier de hello et stockez-le dans un répertoire local sur votre ordinateur, telles que C:\sampledata\.

```azurecli
az dls fs upload --account mydatalakestore --source-path "C:\SampleData\AmbulanceData\vehicle1_09142014.csv" --destination-path "/mynewfolder/vehicle1_09142014.csv"
```

> [!NOTE]
> Destination de hello, vous devez spécifier le chemin d’accès complet hello, y compris le nom de fichier hello.
> 
>


## <a name="list-files-in-a-data-lake-store-account"></a>Répertorier les fichiers dans un compte Data Lake Store

Utilisez hello commande toolist hello fichiers dans un compte Data Lake Store suivants.

```azurecli
az dls fs list --account mydatalakestore --path /mynewfolder
```

sortie de Hello de ce doit être similaire toohello suivantes :

    [
        {
            "accessTime": 1491323529542,
            "aclBit": false,
            "blockSize": 268435456,
            "group": "1808bd5f-62af-45f4-89d8-03c5e81bac20",
            "length": 1589881,
            "modificationTime": 1491323531638,
            "msExpirationTime": 0,
            "name": "mynewfolder/vehicle1_09142014.csv",
            "owner": "1808bd5f-62af-45f4-89d8-03c5e81bac20",
            "pathSuffix": "vehicle1_09142014.csv",
            "permission": "770",
            "replication": 1,
            "type": "FILE"
        }
    ]

## <a name="rename-download-and-delete-data-from-a-data-lake-store-account"></a>Renommer, télécharger et supprimer des données de votre compte Data Lake Store 

* **toorename un fichier**, utilisez hello de commande suivante :
  
    ```azurecli
    az dls fs move --account mydatalakestore --source-path /mynewfolder/vehicle1_09142014.csv --destination-path /mynewfolder/vehicle1_09142014_copy.csv
    ```

* **toodownload un fichier**, utilisez hello commande suivante. Assurez-vous que le chemin d’accès de destination hello que vous spécifiez déjà existe.
  
    ```azurecli     
    az dls fs download --account mydatalakestore --source-path /mynewfolder/vehicle1_09142014_copy.csv --destination-path "C:\mysampledata\vehicle1_09142014_copy.csv"
    ```

    > [!NOTE]
    > commande Hello crée le dossier de destination hello s’il n’existe pas.
    > 
    >

* **toodelete un fichier**, utilisez hello de commande suivante :
  
    ```azurecli
    az dls fs delete --account mydatalakestore --path /mynewfolder/vehicle1_09142014_copy.csv
    ```

    Si vous souhaitez que le dossier de hello toodelete **MonNouveauDossier** et hello **vehicle1_09142014_copy.csv** ensemble en une seule commande, utilisez hello--recurse paramètre

    ```azurecli
    az dls fs delete --account mydatalakestore --path /mynewfolder --recurse
    ```

## <a name="work-with-permissions-and-acls-for-a-data-lake-store-account"></a>Fonctionne avec les autorisations et les listes ACL pour un compte Data Lake Store

Dans cette section vous apprenez toomanage ACL et des autorisations à l’aide d’Azure CLI 2.0. Pour obtenir une présentation détaillée sur la façon dont les listes ACL sont implémentées dans Azure Data Lake Store, voir [Contrôle d’accès dans Azure Data Lake Store](data-lake-store-access-control.md).

* **propriétaire de hello tooupdate d’un fichier/dossier**, utilisez hello de commande suivante :

    ```azurecli
    az dls fs access set-owner --account mydatalakestore --path /mynewfolder/vehicle1_09142014.csv --group 80a3ed5f-959e-4696-ba3c-d3c8b2db6766 --owner 6361e05d-c381-4275-a932-5535806bb323
    ```

* **autorisations de hello tooupdate pour un fichier/dossier**, utilisez hello de commande suivante :

    ```azurecli
    az dls fs access set-permission --account mydatalakestore --path /mynewfolder/vehicle1_09142014.csv --permission 777
    ```
    
* **tooget hello ACL pour un chemin d’accès donné**, utilisez hello de commande suivante :

    ```azurecli
    az dls fs access show --account mydatalakestore --path /mynewfolder/vehicle1_09142014.csv
    ```

    sortie de Hello sont similaires toohello suivants :

        {
            "entries": [
            "user::rwx",
            "group::rwx",
            "other::---"
          ],
          "group": "1808bd5f-62af-45f4-89d8-03c5e81bac20",
          "owner": "1808bd5f-62af-45f4-89d8-03c5e81bac20",
          "permission": "770",
          "stickyBit": false
        }

* **tooset une entrée pour une liste ACL**, utilisez hello de commande suivante :

    ```azurecli
    az dls fs access set-entry --account mydatalakestore --path /mynewfolder --acl-spec user:6360e05d-c381-4275-a932-5535806bb323:-w-
    ```

* **tooremove une entrée pour une liste ACL**, utilisez hello de commande suivante :

    ```azurecli
    az dls fs access remove-entry --account mydatalakestore --path /mynewfolder --acl-spec user:6360e05d-c381-4275-a932-5535806bb323
    ```

* **un ensemble d’ACL par défaut de tooremove**, utilisez hello de commande suivante :

    ```azurecli
    az dls fs access remove-all --account mydatalakestore --path /mynewfolder --default-acl
    ```

* **tooremove une ACL par défaut entière**, utilisez hello de commande suivante :

    ```azurecli
    az dls fs access remove-all --account mydatalakestore --path /mynewfolder
    ```
    
## <a name="delete-a-data-lake-store-account"></a>Supprimer un compte Data Lake Store
Utilisez hello suivant commande toodelete un compte Data Lake Store.

```azurecli
az dls account delete --account mydatalakestore
```

Lorsque vous y êtes invité, entrez **Y** compte de hello toodelete.

## <a name="next-steps"></a>Étapes suivantes

* [Référence Azure Data Lake Store CLI 2.0](https://docs.microsoft.com/cli/azure/dls)
* [Sécuriser les données dans Data Lake Store](data-lake-store-secure-data.md)
* [Utiliser Azure Data Lake Analytics avec Data Lake Store](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [Utiliser Azure HDInsight avec Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md)

[azure-command-line-tools]: ../xplat-cli-install.md
