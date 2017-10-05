---
title: "Utiliser l’interface de ligne de commande Azure 2.0 pour la prise en main d’Azure Data Lake Store | Microsoft Docs"
description: "Utilisation de l’interface de ligne de commande multi-plateforme Azure 2.0 pour créer un compte Data Lake Store et effectuer des opérations de base"
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
ms.openlocfilehash: ed78d25f2bac0a9996f1796ee503f31a36940977
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-data-lake-store-using-azure-cli-20"></a><span data-ttu-id="aaca7-103">Prise en main d’Azure Data Lake Store avec Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="aaca7-103">Get started with Azure Data Lake Store using Azure CLI 2.0</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="aaca7-104">Portail</span><span class="sxs-lookup"><span data-stu-id="aaca7-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="aaca7-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="aaca7-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="aaca7-106">Kit SDK .NET</span><span class="sxs-lookup"><span data-stu-id="aaca7-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="aaca7-107">Kit SDK Java</span><span class="sxs-lookup"><span data-stu-id="aaca7-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="aaca7-108">API REST</span><span class="sxs-lookup"><span data-stu-id="aaca7-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="aaca7-109">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="aaca7-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="aaca7-110">Node.JS</span><span class="sxs-lookup"><span data-stu-id="aaca7-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="aaca7-111">Python</span><span class="sxs-lookup"><span data-stu-id="aaca7-111">Python</span></span>](data-lake-store-get-started-python.md)
>
>

<span data-ttu-id="aaca7-112">Apprenez à utiliser Azure CLI 2.0 pour créer un compte Azure Data Lake Store et effectuer des opérations de base comme créer des dossiers, télécharger des fichiers de données, supprimer votre compte, etc. Pour plus d’informations sur Data Lake Store, consultez [Vue d’ensemble de Data Lake Store](data-lake-store-overview.md).</span><span class="sxs-lookup"><span data-stu-id="aaca7-112">Learn how to use Azure CLI 2.0 to create an Azure Data Lake Store account and perform basic operations such as create folders, upload and download data files, delete your account, etc. For more information about Data Lake Store, see [Overview of Data Lake Store](data-lake-store-overview.md).</span></span>

<span data-ttu-id="aaca7-113">Azure CLI 2.0 est la nouvelle expérience de ligne de commande Azure pour la gestion des ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="aaca7-113">The Azure CLI 2.0 is Azure's new command-line experience for managing Azure resources.</span></span> <span data-ttu-id="aaca7-114">Elle peut être utilisée sur macOS, Linux et Windows.</span><span class="sxs-lookup"><span data-stu-id="aaca7-114">It can be used on macOS, Linux, and Windows.</span></span> <span data-ttu-id="aaca7-115">Pour plus d’informations, voir [Présentation d’Azure CLI 2.0](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="aaca7-115">For more information, see [Overview of Azure CLI 2.0](https://docs.microsoft.com/cli/azure/overview).</span></span> <span data-ttu-id="aaca7-116">Pour obtenir la liste complète des commandes et de la syntaxe, consultez la [Référence Azure Data Lake Store CLI 2.0](https://docs.microsoft.com/cli/azure/dls).</span><span class="sxs-lookup"><span data-stu-id="aaca7-116">You can also look at the [Azure Data Lake Store CLI 2.0 reference](https://docs.microsoft.com/cli/azure/dls) for a complete list of commands and syntax.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="aaca7-117">Composants requis</span><span class="sxs-lookup"><span data-stu-id="aaca7-117">Prerequisites</span></span>
<span data-ttu-id="aaca7-118">Avant de commencer cet article, vous devez disposer des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="aaca7-118">Before you begin this article, you must have the following:</span></span>

* <span data-ttu-id="aaca7-119">**Un abonnement Azure**.</span><span class="sxs-lookup"><span data-stu-id="aaca7-119">**An Azure subscription**.</span></span> <span data-ttu-id="aaca7-120">Consultez la page [Obtention d’un essai gratuit d’Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="aaca7-120">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="aaca7-121">**Azure CLI 2.0** - Voir [Installer Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) pour plus d’instructions.</span><span class="sxs-lookup"><span data-stu-id="aaca7-121">**Azure CLI 2.0** - See [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) for instructions.</span></span>

## <a name="authentication"></a><span data-ttu-id="aaca7-122">Authentification</span><span class="sxs-lookup"><span data-stu-id="aaca7-122">Authentication</span></span>

<span data-ttu-id="aaca7-123">Pour l’authentification auprès de Data Lake Store, cet article utilise une approche plus simple où vous vous connectez en tant qu’utilisateur final.</span><span class="sxs-lookup"><span data-stu-id="aaca7-123">This article uses a simpler authentication approach with Data Lake Store where you log in as an end-user user.</span></span> <span data-ttu-id="aaca7-124">Le niveau d’accès au compte et au système de fichiers Data Lake Store est alors régi par le niveau d’accès de l’utilisateur connecté.</span><span class="sxs-lookup"><span data-stu-id="aaca7-124">The access level to Data Lake Store account and file system is then governed by the access level of the logged in user.</span></span> <span data-ttu-id="aaca7-125">Cependant, il existe d’autres approches pour l’authentification sur Data Lake Store, à savoir **l’authentification de l’utilisateur final** ou **l’authentification de service à service**.</span><span class="sxs-lookup"><span data-stu-id="aaca7-125">However, there are other approaches as well to authenticate with Data Lake Store, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="aaca7-126">Pour obtenir des instructions et plus d’informations sur l’authentification, consultez [l’authentification de l’utilisateur final](data-lake-store-end-user-authenticate-using-active-directory.md) ou [l’authentification de service à service](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="aaca7-126">For instructions and more information on how to authenticate, see [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md) or [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md).</span></span>


## <a name="log-in-to-your-azure-subscription"></a><span data-ttu-id="aaca7-127">Connexion à votre abonnement Azure</span><span class="sxs-lookup"><span data-stu-id="aaca7-127">Log in to your Azure subscription</span></span>

1. <span data-ttu-id="aaca7-128">Connectez-vous à votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="aaca7-128">Log into your Azure subscription.</span></span>

    ```azurecli
    az login
    ```

    <span data-ttu-id="aaca7-129">Vous obtenez un code que vous utiliserez à l’étape suivante.</span><span class="sxs-lookup"><span data-stu-id="aaca7-129">You get a code to use in the next step.</span></span> <span data-ttu-id="aaca7-130">Ouvrez la page https://aka.ms/devicelogin dans un navigateur web et entrez le code pour vous authentifier.</span><span class="sxs-lookup"><span data-stu-id="aaca7-130">Use a web browser to open the page https://aka.ms/devicelogin and enter the code to authenticate.</span></span> <span data-ttu-id="aaca7-131">Vous êtes invité à vous connecter en utilisant vos informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="aaca7-131">You are prompted to log in using your credentials.</span></span>

2. <span data-ttu-id="aaca7-132">Une fois que vous êtes connecté, la fenêtre répertorie tous les abonnements Azure qui sont associés à votre compte.</span><span class="sxs-lookup"><span data-stu-id="aaca7-132">Once you log in, the window lists all the Azure subscriptions that are associated with your account.</span></span> <span data-ttu-id="aaca7-133">Exécutez la commande suivante pour utiliser un abonnement spécifique.</span><span class="sxs-lookup"><span data-stu-id="aaca7-133">Use the following command to use a specific subscription.</span></span>
   
    ```azurecli
    az account set --subscription <subscription id> 
    ```

## <a name="create-an-azure-data-lake-store-account"></a><span data-ttu-id="aaca7-134">Créer un compte Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="aaca7-134">Create an Azure Data Lake Store account</span></span>

1. <span data-ttu-id="aaca7-135">Créez un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="aaca7-135">Create a new resource group.</span></span> <span data-ttu-id="aaca7-136">Dans la commande suivante, définissez des valeurs de paramètre que vous souhaitez utiliser.</span><span class="sxs-lookup"><span data-stu-id="aaca7-136">In the following command, provide the parameter values you want to use.</span></span> <span data-ttu-id="aaca7-137">Si le nom de l'emplacement contient des espaces, entourez-le de guillemets.</span><span class="sxs-lookup"><span data-stu-id="aaca7-137">If the location name contains spaces, put it in quotes.</span></span> <span data-ttu-id="aaca7-138">Par exemple, « East US 2 ».</span><span class="sxs-lookup"><span data-stu-id="aaca7-138">For example "East US 2".</span></span> 
   
    ```azurecli
    az group create --location "East US 2" --name myresourcegroup
    ```

2. <span data-ttu-id="aaca7-139">Créez le compte Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="aaca7-139">Create the Data Lake Store account.</span></span>
   
    ```azurecli
    az dls account create --account mydatalakestore --resource-group myresourcegroup
    ```

## <a name="create-folders-in-a-data-lake-store-account"></a><span data-ttu-id="aaca7-140">Créer des dossiers dans un compte Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="aaca7-140">Create folders in a Data Lake Store account</span></span>

<span data-ttu-id="aaca7-141">Vous pouvez créer des dossiers dans votre compte Azure Data Lake Store pour gérer et stocker des données.</span><span class="sxs-lookup"><span data-stu-id="aaca7-141">You can create folders under your Azure Data Lake Store account to manage and store data.</span></span> <span data-ttu-id="aaca7-142">Utilisez la commande suivante pour créer un dossier nommé **mynewfolder** à la racine du Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="aaca7-142">Use the following command to create a folder called **mynewfolder** at the root of the Data Lake Store.</span></span>

```azurecli
az dls fs create --account mydatalakestore --path /mynewfolder --folder
```

> [!NOTE]
> <span data-ttu-id="aaca7-143">Le paramètre `--folder` permet de s’assurer que la commande crée un dossier.</span><span class="sxs-lookup"><span data-stu-id="aaca7-143">The `--folder` parameter ensures that the command creates a folder.</span></span> <span data-ttu-id="aaca7-144">Si ce paramètre n’est pas présent, la commande crée un fichier vide appelé mynewfolder à la racine du compte Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="aaca7-144">If this parameter is not present, the command creates an empty file called mynewfolder at the root of the Data Lake Store account.</span></span>
> 
>

## <a name="upload-data-to-a-data-lake-store-account"></a><span data-ttu-id="aaca7-145">Charger des données dans un compte Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="aaca7-145">Upload data to a Data Lake Store account</span></span>

<span data-ttu-id="aaca7-146">Vous pouvez charger des données dans Data Lake Store directement à la racine ou dans un dossier que vous avez créé dans le compte.</span><span class="sxs-lookup"><span data-stu-id="aaca7-146">You can upload data to Data Lake Store directly at the root level or to a folder that you created within the account.</span></span> <span data-ttu-id="aaca7-147">Les extraits de code ci-dessous montrent comment charger des exemples de données dans le dossier (**mynewfolder**) que vous avez créé dans la section précédente.</span><span class="sxs-lookup"><span data-stu-id="aaca7-147">The snippets below demonstrate how to upload some sample data to the folder (**mynewfolder**) you created in the previous section.</span></span>

<span data-ttu-id="aaca7-148">Si vous recherchez des exemples de données à charger, vous pouvez récupérer le dossier **Données Ambulance** dans le [Référentiel Git Azure Data Lake](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span><span class="sxs-lookup"><span data-stu-id="aaca7-148">If you are looking for some sample data to upload, you can get the **Ambulance Data** folder from the [Azure Data Lake Git Repository](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span></span> <span data-ttu-id="aaca7-149">Téléchargez le fichier et stockez-le dans un répertoire local sur votre ordinateur, comme C:\sampledata\.</span><span class="sxs-lookup"><span data-stu-id="aaca7-149">Download the file and store it in a local directory on your computer, such as  C:\sampledata\.</span></span>

```azurecli
az dls fs upload --account mydatalakestore --source-path "C:\SampleData\AmbulanceData\vehicle1_09142014.csv" --destination-path "/mynewfolder/vehicle1_09142014.csv"
```

> [!NOTE]
> <span data-ttu-id="aaca7-150">Pour la destination, vous devez spécifier le chemin d’accès complet, y compris le nom de fichier.</span><span class="sxs-lookup"><span data-stu-id="aaca7-150">For the destination, you must specify the complete path including the file name.</span></span>
> 
>


## <a name="list-files-in-a-data-lake-store-account"></a><span data-ttu-id="aaca7-151">Répertorier les fichiers dans un compte Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="aaca7-151">List files in a Data Lake Store account</span></span>

<span data-ttu-id="aaca7-152">Utilisez la commande suivante pour afficher les fichiers dans un compte Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="aaca7-152">Use the following command to list the files in a Data Lake Store account.</span></span>

```azurecli
az dls fs list --account mydatalakestore --path /mynewfolder
```

<span data-ttu-id="aaca7-153">Le résultat doit ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="aaca7-153">The output of this should be similar to the following:</span></span>

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

## <a name="rename-download-and-delete-data-from-a-data-lake-store-account"></a><span data-ttu-id="aaca7-154">Renommer, télécharger et supprimer des données de votre compte Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="aaca7-154">Rename, download, and delete data from a Data Lake Store account</span></span> 

* <span data-ttu-id="aaca7-155">Utilisez la commande suivante **pour renommer un fichier** :</span><span class="sxs-lookup"><span data-stu-id="aaca7-155">**To rename a file**, use the following command:</span></span>
  
    ```azurecli
    az dls fs move --account mydatalakestore --source-path /mynewfolder/vehicle1_09142014.csv --destination-path /mynewfolder/vehicle1_09142014_copy.csv
    ```

* <span data-ttu-id="aaca7-156">Utilisez la commande suivante **pour télécharger un fichier**.</span><span class="sxs-lookup"><span data-stu-id="aaca7-156">**To download a file**, use the following command.</span></span> <span data-ttu-id="aaca7-157">Assurez-vous que le chemin de destination que vous spécifiez existe.</span><span class="sxs-lookup"><span data-stu-id="aaca7-157">Make sure the destination path you specify already exists.</span></span>
  
    ```azurecli     
    az dls fs download --account mydatalakestore --source-path /mynewfolder/vehicle1_09142014_copy.csv --destination-path "C:\mysampledata\vehicle1_09142014_copy.csv"
    ```

    > [!NOTE]
    > <span data-ttu-id="aaca7-158">La commande crée le dossier de destination, si celui-ci n’existe pas.</span><span class="sxs-lookup"><span data-stu-id="aaca7-158">The command creates the destination folder if it does not exist.</span></span>
    > 
    >

* <span data-ttu-id="aaca7-159">Utilisez la commande suivante **pour supprimer un fichier** :</span><span class="sxs-lookup"><span data-stu-id="aaca7-159">**To delete a file**, use the following command:</span></span>
  
    ```azurecli
    az dls fs delete --account mydatalakestore --path /mynewfolder/vehicle1_09142014_copy.csv
    ```

    <span data-ttu-id="aaca7-160">Si vous souhaitez supprimer simultanément le dossier **mynewfolder** et le fichier **vehicle1_09142014_copy.csv** en une seule commande, utilisez le paramètre --recurse</span><span class="sxs-lookup"><span data-stu-id="aaca7-160">If you want to delete the folder **mynewfolder** and the file **vehicle1_09142014_copy.csv** together in one command, use the --recurse parameter</span></span>

    ```azurecli
    az dls fs delete --account mydatalakestore --path /mynewfolder --recurse
    ```

## <a name="work-with-permissions-and-acls-for-a-data-lake-store-account"></a><span data-ttu-id="aaca7-161">Fonctionne avec les autorisations et les listes ACL pour un compte Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="aaca7-161">Work with permissions and ACLs for a Data Lake Store account</span></span>

<span data-ttu-id="aaca7-162">Dans cette section, vous allez apprendre à gérer les listes ACL et les autorisations à l’aide d’Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="aaca7-162">In this section you learn about how to manage ACLs and permissions using Azure CLI 2.0.</span></span> <span data-ttu-id="aaca7-163">Pour obtenir une présentation détaillée sur la façon dont les listes ACL sont implémentées dans Azure Data Lake Store, voir [Contrôle d’accès dans Azure Data Lake Store](data-lake-store-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="aaca7-163">For a detailed discussion on how ACLs are implemented in Azure Data Lake Store, see [Access control in Azure Data Lake Store](data-lake-store-access-control.md).</span></span>

* <span data-ttu-id="aaca7-164">**Pour mettre à jour le propriétaire d’un fichier/dossier**, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="aaca7-164">**To update the owner of a file/folder**, use the following command:</span></span>

    ```azurecli
    az dls fs access set-owner --account mydatalakestore --path /mynewfolder/vehicle1_09142014.csv --group 80a3ed5f-959e-4696-ba3c-d3c8b2db6766 --owner 6361e05d-c381-4275-a932-5535806bb323
    ```

* <span data-ttu-id="aaca7-165">**Pour mettre à jour les autorisations d’un fichier/dossier**, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="aaca7-165">**To update the permissions for a file/folder**, use the following command:</span></span>

    ```azurecli
    az dls fs access set-permission --account mydatalakestore --path /mynewfolder/vehicle1_09142014.csv --permission 777
    ```
    
* <span data-ttu-id="aaca7-166">**Pour obtenir les listes ACL pour un chemin d’accès donné**, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="aaca7-166">**To get the ACLs for a given path**, use the following command:</span></span>

    ```azurecli
    az dls fs access show --account mydatalakestore --path /mynewfolder/vehicle1_09142014.csv
    ```

    <span data-ttu-id="aaca7-167">Le résultat doit ressembler à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="aaca7-167">The output should be similar to the following:</span></span>

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

* <span data-ttu-id="aaca7-168">**Pour définir une entrée pour une liste ACL**, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="aaca7-168">**To set an entry for an ACL**, use the following command:</span></span>

    ```azurecli
    az dls fs access set-entry --account mydatalakestore --path /mynewfolder --acl-spec user:6360e05d-c381-4275-a932-5535806bb323:-w-
    ```

* <span data-ttu-id="aaca7-169">**Pour supprimer une entrée d’une liste ACL**, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="aaca7-169">**To remove an entry for an ACL**, use the following command:</span></span>

    ```azurecli
    az dls fs access remove-entry --account mydatalakestore --path /mynewfolder --acl-spec user:6360e05d-c381-4275-a932-5535806bb323
    ```

* <span data-ttu-id="aaca7-170">**Pour supprimer dans son intégralité une liste ACL par défaut**, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="aaca7-170">**To remove an entire default ACL**, use the following command:</span></span>

    ```azurecli
    az dls fs access remove-all --account mydatalakestore --path /mynewfolder --default-acl
    ```

* <span data-ttu-id="aaca7-171">**Pour supprimer dans son intégralité une liste ACL autre que la liste ACL par défaut**, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="aaca7-171">**To remove an entire non-default ACL**, use the following command:</span></span>

    ```azurecli
    az dls fs access remove-all --account mydatalakestore --path /mynewfolder
    ```
    
## <a name="delete-a-data-lake-store-account"></a><span data-ttu-id="aaca7-172">Supprimer un compte Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="aaca7-172">Delete a Data Lake Store account</span></span>
<span data-ttu-id="aaca7-173">Utilisez la commande suivante pour supprimer un compte Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="aaca7-173">Use the following command to delete a Data Lake Store account.</span></span>

```azurecli
az dls account delete --account mydatalakestore
```

<span data-ttu-id="aaca7-174">Quand vous y êtes invité, entrez **Y** pour supprimer le compte.</span><span class="sxs-lookup"><span data-stu-id="aaca7-174">When prompted, enter **Y** to delete the account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="aaca7-175">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="aaca7-175">Next steps</span></span>

* [<span data-ttu-id="aaca7-176">Référence Azure Data Lake Store CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="aaca7-176">Azure Data Lake Store CLI 2.0 reference</span></span>](https://docs.microsoft.com/cli/azure/dls)
* [<span data-ttu-id="aaca7-177">Sécuriser les données dans Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="aaca7-177">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="aaca7-178">Utiliser Azure Data Lake Analytics avec Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="aaca7-178">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="aaca7-179">Utiliser Azure HDInsight avec Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="aaca7-179">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)

[azure-command-line-tools]: ../xplat-cli-install.md
