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
# <a name="get-started-with-azure-data-lake-store-using-azure-cli-20"></a><span data-ttu-id="be27f-103">Prise en main d’Azure Data Lake Store avec Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="be27f-103">Get started with Azure Data Lake Store using Azure CLI 2.0</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="be27f-104">Portail</span><span class="sxs-lookup"><span data-stu-id="be27f-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="be27f-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="be27f-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="be27f-106">Kit SDK .NET</span><span class="sxs-lookup"><span data-stu-id="be27f-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="be27f-107">Kit SDK Java</span><span class="sxs-lookup"><span data-stu-id="be27f-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="be27f-108">API REST</span><span class="sxs-lookup"><span data-stu-id="be27f-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="be27f-109">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="be27f-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="be27f-110">Node.JS</span><span class="sxs-lookup"><span data-stu-id="be27f-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="be27f-111">Python</span><span class="sxs-lookup"><span data-stu-id="be27f-111">Python</span></span>](data-lake-store-get-started-python.md)
>
>

<span data-ttu-id="be27f-112">Découvrez comment toouse Azure CLI 2.0 toocreate stocker un lac de données Azure compte et effectuer des opérations de base telles que la création de dossiers, téléchargent et téléchargement les fichiers de données, supprimez votre compte, un etc.. Pour plus d’informations sur Data Lake Store, consultez [Vue d’ensemble de Data Lake Store](data-lake-store-overview.md).</span><span class="sxs-lookup"><span data-stu-id="be27f-112">Learn how toouse Azure CLI 2.0 toocreate an Azure Data Lake Store account and perform basic operations such as create folders, upload and download data files, delete your account, etc. For more information about Data Lake Store, see [Overview of Data Lake Store](data-lake-store-overview.md).</span></span>

<span data-ttu-id="be27f-113">Bonjour Azure CLI 2.0 est la nouvelle expérience de ligne de commande de Azure pour la gestion des ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="be27f-113">hello Azure CLI 2.0 is Azure's new command-line experience for managing Azure resources.</span></span> <span data-ttu-id="be27f-114">Elle peut être utilisée sur macOS, Linux et Windows.</span><span class="sxs-lookup"><span data-stu-id="be27f-114">It can be used on macOS, Linux, and Windows.</span></span> <span data-ttu-id="be27f-115">Pour plus d’informations, voir [Présentation d’Azure CLI 2.0](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="be27f-115">For more information, see [Overview of Azure CLI 2.0](https://docs.microsoft.com/cli/azure/overview).</span></span> <span data-ttu-id="be27f-116">Vous pouvez également consulter hello [Azure Data Lake Store CLI 2.0 référence](https://docs.microsoft.com/cli/azure/dls) pour une liste complète des commandes et la syntaxe.</span><span class="sxs-lookup"><span data-stu-id="be27f-116">You can also look at hello [Azure Data Lake Store CLI 2.0 reference](https://docs.microsoft.com/cli/azure/dls) for a complete list of commands and syntax.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="be27f-117">Composants requis</span><span class="sxs-lookup"><span data-stu-id="be27f-117">Prerequisites</span></span>
<span data-ttu-id="be27f-118">Avant de commencer cet article, vous devez disposer de hello :</span><span class="sxs-lookup"><span data-stu-id="be27f-118">Before you begin this article, you must have hello following:</span></span>

* <span data-ttu-id="be27f-119">**Un abonnement Azure**.</span><span class="sxs-lookup"><span data-stu-id="be27f-119">**An Azure subscription**.</span></span> <span data-ttu-id="be27f-120">Consultez la page [Obtention d’un essai gratuit d’Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="be27f-120">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="be27f-121">**Azure CLI 2.0** - Voir [Installer Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) pour plus d’instructions.</span><span class="sxs-lookup"><span data-stu-id="be27f-121">**Azure CLI 2.0** - See [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) for instructions.</span></span>

## <a name="authentication"></a><span data-ttu-id="be27f-122">Authentification</span><span class="sxs-lookup"><span data-stu-id="be27f-122">Authentication</span></span>

<span data-ttu-id="be27f-123">Pour l’authentification auprès de Data Lake Store, cet article utilise une approche plus simple où vous vous connectez en tant qu’utilisateur final.</span><span class="sxs-lookup"><span data-stu-id="be27f-123">This article uses a simpler authentication approach with Data Lake Store where you log in as an end-user user.</span></span> <span data-ttu-id="be27f-124">Hello accès niveau tooData Lake Store compte de système de fichiers et est ensuite régie par niveau d’accès hello Hello à l’utilisateur connecté.</span><span class="sxs-lookup"><span data-stu-id="be27f-124">hello access level tooData Lake Store account and file system is then governed by hello access level of hello logged in user.</span></span> <span data-ttu-id="be27f-125">Toutefois, il existe d’autres approches en tant que bien tooauthenticate avec Data Lake Store, qui sont **l’authentification de l’utilisateur final** ou **l’authentification de service**.</span><span class="sxs-lookup"><span data-stu-id="be27f-125">However, there are other approaches as well tooauthenticate with Data Lake Store, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="be27f-126">Pour plus d’informations sur la façon d’et tooauthenticate, consultez [l’authentification de l’utilisateur final](data-lake-store-end-user-authenticate-using-active-directory.md) ou [l’authentification de service](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="be27f-126">For instructions and more information on how tooauthenticate, see [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md) or [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md).</span></span>


## <a name="log-in-tooyour-azure-subscription"></a><span data-ttu-id="be27f-127">Ouvrez une session dans tooyour abonnement Azure</span><span class="sxs-lookup"><span data-stu-id="be27f-127">Log in tooyour Azure subscription</span></span>

1. <span data-ttu-id="be27f-128">Connectez-vous à votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="be27f-128">Log into your Azure subscription.</span></span>

    ```azurecli
    az login
    ```

    <span data-ttu-id="be27f-129">Vous obtenez un toouse du code à l’étape suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="be27f-129">You get a code toouse in hello next step.</span></span> <span data-ttu-id="be27f-130">Utiliser un web navigateur tooopen hello page https://aka.ms/devicelogin et entrez tooauthenticate de code hello.</span><span class="sxs-lookup"><span data-stu-id="be27f-130">Use a web browser tooopen hello page https://aka.ms/devicelogin and enter hello code tooauthenticate.</span></span> <span data-ttu-id="be27f-131">Vous êtes invité à toolog à l’aide de vos informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="be27f-131">You are prompted toolog in using your credentials.</span></span>

2. <span data-ttu-id="be27f-132">Une fois que vous vous connectez, des listes de fenêtres hello tous les hello abonnements Azure qui sont associés à votre compte.</span><span class="sxs-lookup"><span data-stu-id="be27f-132">Once you log in, hello window lists all hello Azure subscriptions that are associated with your account.</span></span> <span data-ttu-id="be27f-133">Utilisez hello suivant commande toouse un abonnement spécifique.</span><span class="sxs-lookup"><span data-stu-id="be27f-133">Use hello following command toouse a specific subscription.</span></span>
   
    ```azurecli
    az account set --subscription <subscription id> 
    ```

## <a name="create-an-azure-data-lake-store-account"></a><span data-ttu-id="be27f-134">Créer un compte Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="be27f-134">Create an Azure Data Lake Store account</span></span>

1. <span data-ttu-id="be27f-135">Créez un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="be27f-135">Create a new resource group.</span></span> <span data-ttu-id="be27f-136">Bonjour la commande suivante, fournir des valeurs de paramètre souhaité toouse hello.</span><span class="sxs-lookup"><span data-stu-id="be27f-136">In hello following command, provide hello parameter values you want toouse.</span></span> <span data-ttu-id="be27f-137">Si le nom de l’emplacement hello contient des espaces, placez-le entre guillemets.</span><span class="sxs-lookup"><span data-stu-id="be27f-137">If hello location name contains spaces, put it in quotes.</span></span> <span data-ttu-id="be27f-138">Par exemple, « East US 2 ».</span><span class="sxs-lookup"><span data-stu-id="be27f-138">For example "East US 2".</span></span> 
   
    ```azurecli
    az group create --location "East US 2" --name myresourcegroup
    ```

2. <span data-ttu-id="be27f-139">Créer un compte Data Lake Store de hello.</span><span class="sxs-lookup"><span data-stu-id="be27f-139">Create hello Data Lake Store account.</span></span>
   
    ```azurecli
    az dls account create --account mydatalakestore --resource-group myresourcegroup
    ```

## <a name="create-folders-in-a-data-lake-store-account"></a><span data-ttu-id="be27f-140">Créer des dossiers dans un compte Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="be27f-140">Create folders in a Data Lake Store account</span></span>

<span data-ttu-id="be27f-141">Vous pouvez créer des dossiers sous votre toomanage de compte Azure Data Lake Store et stocker des données.</span><span class="sxs-lookup"><span data-stu-id="be27f-141">You can create folders under your Azure Data Lake Store account toomanage and store data.</span></span> <span data-ttu-id="be27f-142">Hello utilisation suivant toocreate commande un dossier appelé **MonNouveauDossier** à racine hello hello Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="be27f-142">Use hello following command toocreate a folder called **mynewfolder** at hello root of hello Data Lake Store.</span></span>

```azurecli
az dls fs create --account mydatalakestore --path /mynewfolder --folder
```

> [!NOTE]
> <span data-ttu-id="be27f-143">Hello `--folder` paramètre permet de s’assurer que les commandes hello crée un dossier.</span><span class="sxs-lookup"><span data-stu-id="be27f-143">hello `--folder` parameter ensures that hello command creates a folder.</span></span> <span data-ttu-id="be27f-144">Si ce paramètre n’est pas présent, la commande hello crée un fichier vide appelé MonNouveauDossier à racine hello hello compte Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="be27f-144">If this parameter is not present, hello command creates an empty file called mynewfolder at hello root of hello Data Lake Store account.</span></span>
> 
>

## <a name="upload-data-tooa-data-lake-store-account"></a><span data-ttu-id="be27f-145">Télécharger le compte de données tooa Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="be27f-145">Upload data tooa Data Lake Store account</span></span>

<span data-ttu-id="be27f-146">Vous pouvez télécharger des données tooData Lake Store directement dans le dossier de niveau ou tooa de racine hello que vous avez créé dans le compte de hello.</span><span class="sxs-lookup"><span data-stu-id="be27f-146">You can upload data tooData Lake Store directly at hello root level or tooa folder that you created within hello account.</span></span> <span data-ttu-id="be27f-147">Hello d’extraits de code ci-dessous montrent comment tooupload un dossier de toohello de données exemple (**MonNouveauDossier**) vous avez créé dans la section précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="be27f-147">hello snippets below demonstrate how tooupload some sample data toohello folder (**mynewfolder**) you created in hello previous section.</span></span>

<span data-ttu-id="be27f-148">Si vous recherchez des tooupload de données d’exemple, vous pouvez obtenir hello **Ambulance données** dossier hello [référentiel Git de LAC de données Azure](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span><span class="sxs-lookup"><span data-stu-id="be27f-148">If you are looking for some sample data tooupload, you can get hello **Ambulance Data** folder from hello [Azure Data Lake Git Repository](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span></span> <span data-ttu-id="be27f-149">Télécharger le fichier de hello et stockez-le dans un répertoire local sur votre ordinateur, telles que C:\sampledata\.</span><span class="sxs-lookup"><span data-stu-id="be27f-149">Download hello file and store it in a local directory on your computer, such as  C:\sampledata\.</span></span>

```azurecli
az dls fs upload --account mydatalakestore --source-path "C:\SampleData\AmbulanceData\vehicle1_09142014.csv" --destination-path "/mynewfolder/vehicle1_09142014.csv"
```

> [!NOTE]
> <span data-ttu-id="be27f-150">Destination de hello, vous devez spécifier le chemin d’accès complet hello, y compris le nom de fichier hello.</span><span class="sxs-lookup"><span data-stu-id="be27f-150">For hello destination, you must specify hello complete path including hello file name.</span></span>
> 
>


## <a name="list-files-in-a-data-lake-store-account"></a><span data-ttu-id="be27f-151">Répertorier les fichiers dans un compte Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="be27f-151">List files in a Data Lake Store account</span></span>

<span data-ttu-id="be27f-152">Utilisez hello commande toolist hello fichiers dans un compte Data Lake Store suivants.</span><span class="sxs-lookup"><span data-stu-id="be27f-152">Use hello following command toolist hello files in a Data Lake Store account.</span></span>

```azurecli
az dls fs list --account mydatalakestore --path /mynewfolder
```

<span data-ttu-id="be27f-153">sortie de Hello de ce doit être similaire toohello suivantes :</span><span class="sxs-lookup"><span data-stu-id="be27f-153">hello output of this should be similar toohello following:</span></span>

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

## <a name="rename-download-and-delete-data-from-a-data-lake-store-account"></a><span data-ttu-id="be27f-154">Renommer, télécharger et supprimer des données de votre compte Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="be27f-154">Rename, download, and delete data from a Data Lake Store account</span></span> 

* <span data-ttu-id="be27f-155">**toorename un fichier**, utilisez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="be27f-155">**toorename a file**, use hello following command:</span></span>
  
    ```azurecli
    az dls fs move --account mydatalakestore --source-path /mynewfolder/vehicle1_09142014.csv --destination-path /mynewfolder/vehicle1_09142014_copy.csv
    ```

* <span data-ttu-id="be27f-156">**toodownload un fichier**, utilisez hello commande suivante.</span><span class="sxs-lookup"><span data-stu-id="be27f-156">**toodownload a file**, use hello following command.</span></span> <span data-ttu-id="be27f-157">Assurez-vous que le chemin d’accès de destination hello que vous spécifiez déjà existe.</span><span class="sxs-lookup"><span data-stu-id="be27f-157">Make sure hello destination path you specify already exists.</span></span>
  
    ```azurecli     
    az dls fs download --account mydatalakestore --source-path /mynewfolder/vehicle1_09142014_copy.csv --destination-path "C:\mysampledata\vehicle1_09142014_copy.csv"
    ```

    > [!NOTE]
    > <span data-ttu-id="be27f-158">commande Hello crée le dossier de destination hello s’il n’existe pas.</span><span class="sxs-lookup"><span data-stu-id="be27f-158">hello command creates hello destination folder if it does not exist.</span></span>
    > 
    >

* <span data-ttu-id="be27f-159">**toodelete un fichier**, utilisez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="be27f-159">**toodelete a file**, use hello following command:</span></span>
  
    ```azurecli
    az dls fs delete --account mydatalakestore --path /mynewfolder/vehicle1_09142014_copy.csv
    ```

    <span data-ttu-id="be27f-160">Si vous souhaitez que le dossier de hello toodelete **MonNouveauDossier** et hello **vehicle1_09142014_copy.csv** ensemble en une seule commande, utilisez hello--recurse paramètre</span><span class="sxs-lookup"><span data-stu-id="be27f-160">If you want toodelete hello folder **mynewfolder** and hello file **vehicle1_09142014_copy.csv** together in one command, use hello --recurse parameter</span></span>

    ```azurecli
    az dls fs delete --account mydatalakestore --path /mynewfolder --recurse
    ```

## <a name="work-with-permissions-and-acls-for-a-data-lake-store-account"></a><span data-ttu-id="be27f-161">Fonctionne avec les autorisations et les listes ACL pour un compte Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="be27f-161">Work with permissions and ACLs for a Data Lake Store account</span></span>

<span data-ttu-id="be27f-162">Dans cette section vous apprenez toomanage ACL et des autorisations à l’aide d’Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="be27f-162">In this section you learn about how toomanage ACLs and permissions using Azure CLI 2.0.</span></span> <span data-ttu-id="be27f-163">Pour obtenir une présentation détaillée sur la façon dont les listes ACL sont implémentées dans Azure Data Lake Store, voir [Contrôle d’accès dans Azure Data Lake Store](data-lake-store-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="be27f-163">For a detailed discussion on how ACLs are implemented in Azure Data Lake Store, see [Access control in Azure Data Lake Store](data-lake-store-access-control.md).</span></span>

* <span data-ttu-id="be27f-164">**propriétaire de hello tooupdate d’un fichier/dossier**, utilisez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="be27f-164">**tooupdate hello owner of a file/folder**, use hello following command:</span></span>

    ```azurecli
    az dls fs access set-owner --account mydatalakestore --path /mynewfolder/vehicle1_09142014.csv --group 80a3ed5f-959e-4696-ba3c-d3c8b2db6766 --owner 6361e05d-c381-4275-a932-5535806bb323
    ```

* <span data-ttu-id="be27f-165">**autorisations de hello tooupdate pour un fichier/dossier**, utilisez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="be27f-165">**tooupdate hello permissions for a file/folder**, use hello following command:</span></span>

    ```azurecli
    az dls fs access set-permission --account mydatalakestore --path /mynewfolder/vehicle1_09142014.csv --permission 777
    ```
    
* <span data-ttu-id="be27f-166">**tooget hello ACL pour un chemin d’accès donné**, utilisez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="be27f-166">**tooget hello ACLs for a given path**, use hello following command:</span></span>

    ```azurecli
    az dls fs access show --account mydatalakestore --path /mynewfolder/vehicle1_09142014.csv
    ```

    <span data-ttu-id="be27f-167">sortie de Hello sont similaires toohello suivants :</span><span class="sxs-lookup"><span data-stu-id="be27f-167">hello output should be similar toohello following:</span></span>

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

* <span data-ttu-id="be27f-168">**tooset une entrée pour une liste ACL**, utilisez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="be27f-168">**tooset an entry for an ACL**, use hello following command:</span></span>

    ```azurecli
    az dls fs access set-entry --account mydatalakestore --path /mynewfolder --acl-spec user:6360e05d-c381-4275-a932-5535806bb323:-w-
    ```

* <span data-ttu-id="be27f-169">**tooremove une entrée pour une liste ACL**, utilisez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="be27f-169">**tooremove an entry for an ACL**, use hello following command:</span></span>

    ```azurecli
    az dls fs access remove-entry --account mydatalakestore --path /mynewfolder --acl-spec user:6360e05d-c381-4275-a932-5535806bb323
    ```

* <span data-ttu-id="be27f-170">**un ensemble d’ACL par défaut de tooremove**, utilisez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="be27f-170">**tooremove an entire default ACL**, use hello following command:</span></span>

    ```azurecli
    az dls fs access remove-all --account mydatalakestore --path /mynewfolder --default-acl
    ```

* <span data-ttu-id="be27f-171">**tooremove une ACL par défaut entière**, utilisez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="be27f-171">**tooremove an entire non-default ACL**, use hello following command:</span></span>

    ```azurecli
    az dls fs access remove-all --account mydatalakestore --path /mynewfolder
    ```
    
## <a name="delete-a-data-lake-store-account"></a><span data-ttu-id="be27f-172">Supprimer un compte Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="be27f-172">Delete a Data Lake Store account</span></span>
<span data-ttu-id="be27f-173">Utilisez hello suivant commande toodelete un compte Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="be27f-173">Use hello following command toodelete a Data Lake Store account.</span></span>

```azurecli
az dls account delete --account mydatalakestore
```

<span data-ttu-id="be27f-174">Lorsque vous y êtes invité, entrez **Y** compte de hello toodelete.</span><span class="sxs-lookup"><span data-stu-id="be27f-174">When prompted, enter **Y** toodelete hello account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="be27f-175">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="be27f-175">Next steps</span></span>

* [<span data-ttu-id="be27f-176">Référence Azure Data Lake Store CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="be27f-176">Azure Data Lake Store CLI 2.0 reference</span></span>](https://docs.microsoft.com/cli/azure/dls)
* [<span data-ttu-id="be27f-177">Sécuriser les données dans Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="be27f-177">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="be27f-178">Utiliser Azure Data Lake Analytics avec Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="be27f-178">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="be27f-179">Utiliser Azure HDInsight avec Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="be27f-179">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)

[azure-command-line-tools]: ../xplat-cli-install.md
