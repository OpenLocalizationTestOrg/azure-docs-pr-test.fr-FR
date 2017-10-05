---
title: "Utilisation d’Azure CLI 2.0 avec le stockage Azure | Microsoft Docs"
description: "Découvrez comment utiliser Azure CLI 2.0 avec le stockage Azure pour créer et gérer des comptes de stockage et utiliser des fichiers et objets blob Azure. Azure CLI 2.0 est un outil multiplateforme écrit en Python."
services: storage
documentationcenter: na
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: article
ms.date: 06/02/2017
ms.author: marsma
ms.openlocfilehash: 6098216f7dd901ea48fb3ab969c7934cc288b247
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="using-the-azure-cli-20-with-azure-storage"></a><span data-ttu-id="82c3b-104">Utilisation d’Azure CLI 2.0 avec le stockage Azure</span><span class="sxs-lookup"><span data-stu-id="82c3b-104">Using the Azure CLI 2.0 with Azure Storage</span></span>

<span data-ttu-id="82c3b-105">L’interface Azure CLI 2.0 multiplateforme et open source offre un ensemble de commandes dédiées à l’utilisation de la plateforme Azure.</span><span class="sxs-lookup"><span data-stu-id="82c3b-105">The open-source, cross-platform Azure CLI 2.0 provides a set of commands for working with the Azure platform.</span></span> <span data-ttu-id="82c3b-106">Elle offre des fonctionnalités similaires à celles du [portail Azure](https://portal.azure.com), notamment l’accès étendu aux données.</span><span class="sxs-lookup"><span data-stu-id="82c3b-106">It provides much of the same functionality found in the [Azure portal](https://portal.azure.com), including rich data access.</span></span>

<span data-ttu-id="82c3b-107">Dans ce guide, nous vous montrons comment utiliser [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) pour effectuer plusieurs tâches à l’aide de ressources dans votre compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="82c3b-107">In this guide, we show you how to use the [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) to perform several tasks working with resources in your Azure Storage account.</span></span> <span data-ttu-id="82c3b-108">Nous vous recommandons de télécharger et d’installer ou de mettre à niveau la CLI 2.0 vers la dernière version avant d’utiliser ce guide.</span><span class="sxs-lookup"><span data-stu-id="82c3b-108">We recommend that you download and install or upgrade to the latest version of the CLI 2.0 before using this guide.</span></span>

<span data-ttu-id="82c3b-109">Les exemples dans le guide partent du principe que vous utilisez le shell Bash sur Ubuntu, mais les autres plateformes devraient fonctionner de manière similaire.</span><span class="sxs-lookup"><span data-stu-id="82c3b-109">The examples in the guide assume the use of the Bash shell on Ubuntu, but other platforms should perform similarly.</span></span> 

[!INCLUDE [storage-cli-versions](../../includes/storage-cli-versions.md)]

## <a name="prerequisites"></a><span data-ttu-id="82c3b-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="82c3b-110">Prerequisites</span></span>
<span data-ttu-id="82c3b-111">Ce guide part du principe que vous comprenez les concepts de base de Microsoft Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="82c3b-111">This guide assumes that you understand the basic concepts of Azure Storage.</span></span> <span data-ttu-id="82c3b-112">Il suppose également que vous êtes en mesure de satisfaire les exigences de création de compte spécifiées ci-dessous pour Azure et le service Stockage.</span><span class="sxs-lookup"><span data-stu-id="82c3b-112">It also assumes that you're able to satisfy the account creation requirements that are specified below for Azure and the Storage service.</span></span>

### <a name="accounts"></a><span data-ttu-id="82c3b-113">Comptes</span><span class="sxs-lookup"><span data-stu-id="82c3b-113">Accounts</span></span>
* <span data-ttu-id="82c3b-114">**Compte Azure** : si vous ne possédez pas encore d’abonnement Azure, [créez un compte Azure gratuit](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="82c3b-114">**Azure account**: If you don't already have an Azure subscription, [create a free Azure account](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="82c3b-115">**Compte de stockage** : voir la section [Créer un compte de stockage](../storage/storage-create-storage-account.md#create-a-storage-account) de l’article [À propos des comptes de stockage Azure](../storage/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="82c3b-115">**Storage account**: See [Create a storage account](../storage/storage-create-storage-account.md#create-a-storage-account) in [About Azure storage accounts](../storage/storage-create-storage-account.md).</span></span>

### <a name="install-the-azure-cli-20"></a><span data-ttu-id="82c3b-116">Installer Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="82c3b-116">Install the Azure CLI 2.0</span></span>

<span data-ttu-id="82c3b-117">Téléchargez et installez Azure CLI 2.0 en suivant les instructions fournies dans la section [Installer Azure CLI 2.0](/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="82c3b-117">Download and install the Azure CLI 2.0 by following the instructions outlined in [Install Azure CLI 2.0](/cli/azure/install-az-cli2).</span></span>

> [!TIP]
> <span data-ttu-id="82c3b-118">Si vous rencontrez un problème avec l’installation, consultez la section [Dépannage de l’installation](/cli/azure/install-az-cli2#installation-troubleshooting) de l’article et le guide [Dépannage de l’installation](https://github.com/Azure/azure-cli/blob/master/doc/install_troubleshooting.md) sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="82c3b-118">If you have trouble with the installation, check out the [Installation Troubleshooting](/cli/azure/install-az-cli2#installation-troubleshooting) section of the article, and the [Install Troubleshooting](https://github.com/Azure/azure-cli/blob/master/doc/install_troubleshooting.md) guide on GitHub.</span></span>
>

## <a name="working-with-the-cli"></a><span data-ttu-id="82c3b-119">Utilisation de la CLI</span><span class="sxs-lookup"><span data-stu-id="82c3b-119">Working with the CLI</span></span>

<span data-ttu-id="82c3b-120">Une fois la CLI installée, vous pouvez utiliser la commande `az` de votre interface de ligne de commande (invite de ligne de commande, Terminal, Bash) afin d’accéder aux commandes de la CLI Azure.</span><span class="sxs-lookup"><span data-stu-id="82c3b-120">Once you've installed the CLI, you can use the `az` command in your command-line interface (Bash, Terminal, Command Prompt) to access the Azure CLI commands.</span></span> <span data-ttu-id="82c3b-121">Tapez la commande `az` pour afficher la liste complète des commandes de base (l’exemple de sortie suivant a été tronqué) :</span><span class="sxs-lookup"><span data-stu-id="82c3b-121">Type the `az` command to see a full list of the base commands (the following example output has been truncated):</span></span>

```
     /\
    /  \    _____   _ _ __ ___
   / /\ \  |_  / | | | \'__/ _ \
  / ____ \  / /| |_| | | |  __/
 /_/    \_\/___|\__,_|_|  \___|


Welcome to the cool new Azure CLI!

Here are the base commands:

    account          : Manage subscriptions.
    acr              : Manage Azure container registries.
    acs              : Manage Azure Container Services.
    ad               : Synchronize on-premises directories and manage Azure Active Directory
                       resources.
    ...
```

<span data-ttu-id="82c3b-122">Dans l’interface de ligne de commande, exécutez la commande `az storage --help` pour répertorier les sous-groupes de la commande `storage`.</span><span class="sxs-lookup"><span data-stu-id="82c3b-122">In your command-line interface, execute the command `az storage --help` to list the `storage` command subgroups.</span></span> <span data-ttu-id="82c3b-123">Les descriptions des sous-groupes fournissent une vue d’ensemble de la fonctionnalité que la CLI Azure fournit pour l’utilisation de vos ressources de stockage.</span><span class="sxs-lookup"><span data-stu-id="82c3b-123">The descriptions of the subgroups provide an overview of the functionality the Azure CLI provides for working with your storage resources.</span></span>

```
Group
    az storage: Durable, highly available, and massively scalable cloud storage.

Subgroups:
    account  : Manage storage accounts.
    blob     : Object storage for unstructured data.
    container: Manage blob storage containers.
    cors     : Manage Storage service Cross-Origin Resource Sharing (CORS).
    directory: Manage file storage directories.
    entity   : Manage table storage entities.
    file     : File shares that use the standard SMB 3.0 protocol.
    logging  : Manage Storage service logging information.
    message  : Manage queue storage messages.
    metrics  : Manage Storage service metrics.
    queue    : Use queues to effectively scale applications according to traffic.
    share    : Manage file shares.
    table    : NoSQL key-value storage using semi-structured datasets.
```

## <a name="connect-the-cli-to-your-azure-subscription"></a><span data-ttu-id="82c3b-124">Connexion de la CLI à votre abonnement Azure</span><span class="sxs-lookup"><span data-stu-id="82c3b-124">Connect the CLI to your Azure subscription</span></span>

<span data-ttu-id="82c3b-125">Pour utiliser les ressources dans votre abonnement Azure, vous devez tout d’abord vous connecter à votre compte Azure avec `az login`.</span><span class="sxs-lookup"><span data-stu-id="82c3b-125">To work with the resources in your Azure subscription, you must first log in to your Azure account with `az login`.</span></span> <span data-ttu-id="82c3b-126">Vous pouvez vous connecter de plusieurs façons :</span><span class="sxs-lookup"><span data-stu-id="82c3b-126">There are several ways you can log in:</span></span>

* <span data-ttu-id="82c3b-127">**Connexion interactive** : `az login`</span><span class="sxs-lookup"><span data-stu-id="82c3b-127">**Interactive login**: `az login`</span></span>
* <span data-ttu-id="82c3b-128">**Connexion avec nom d’utilisateur et mot de passe** : `az login -u johndoe@contoso.com -p VerySecret`</span><span class="sxs-lookup"><span data-stu-id="82c3b-128">**Log in with user name and password**: `az login -u johndoe@contoso.com -p VerySecret`</span></span>
  * <span data-ttu-id="82c3b-129">Ceci ne fonctionne pas avec les comptes Microsoft ou les comptes qui utilisent l’authentification multifacteur.</span><span class="sxs-lookup"><span data-stu-id="82c3b-129">This doesn't work with Microsoft accounts or accounts that use multi-factor authentication.</span></span>
* <span data-ttu-id="82c3b-130">**Connexion avec un principal du service** : `az login --service-principal -u http://azure-cli-2016-08-05-14-31-15 -p VerySecret --tenant contoso.onmicrosoft.com`</span><span class="sxs-lookup"><span data-stu-id="82c3b-130">**Log in with a service principal**: `az login --service-principal -u http://azure-cli-2016-08-05-14-31-15 -p VerySecret --tenant contoso.onmicrosoft.com`</span></span>

## <a name="azure-cli-20-sample-script"></a><span data-ttu-id="82c3b-131">Exemple de script CLI 2.0 Azure</span><span class="sxs-lookup"><span data-stu-id="82c3b-131">Azure CLI 2.0 sample script</span></span>

<span data-ttu-id="82c3b-132">Ensuite, nous allons utiliser un petit script shell qui émet plusieurs commandes CLI 2.0 Azure de base pour interagir avec les ressources de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="82c3b-132">Next, we'll work with a small shell script that issues a few basic Azure CLI 2.0 commands to interact with Azure Storage resources.</span></span> <span data-ttu-id="82c3b-133">Tout d’abord, le script crée un nouveau conteneur dans votre compte de stockage, puis télécharge un fichier existant (comme un objet blob) dans ce conteneur.</span><span class="sxs-lookup"><span data-stu-id="82c3b-133">The script first creates a new container in your storage account, then uploads an existing file (as a blob) to that container.</span></span> <span data-ttu-id="82c3b-134">Ensuite, il répertorie tous les objets blob dans le conteneur et pour terminer, il télécharge le fichier vers une destination sur l’ordinateur local que vous spécifiez.</span><span class="sxs-lookup"><span data-stu-id="82c3b-134">It then lists all blobs in the container, and finally, downloads the file to a destination on your local computer that you specify.</span></span>

```bash
#!/bin/bash
# A simple Azure Storage example script

export AZURE_STORAGE_ACCOUNT=<storage_account_name>
export AZURE_STORAGE_ACCESS_KEY=<storage_account_key>

export container_name=<container_name>
export blob_name=<blob_name>
export file_to_upload=<file_to_upload>
export destination_file=<destination_file>

echo "Creating the container..."
az storage container create --name $container_name

echo "Uploading the file..."
az storage blob upload --container-name $container_name --file $file_to_upload --name $blob_name

echo "Listing the blobs..."
az storage blob list --container-name $container_name --output table

echo "Downloading the file..."
az storage blob download --container-name $container_name --name $blob_name --file $destination_file --output table

echo "Done"
```

<span data-ttu-id="82c3b-135">**Configuration et exécution du script**</span><span class="sxs-lookup"><span data-stu-id="82c3b-135">**Configure and run the script**</span></span>

1. <span data-ttu-id="82c3b-136">Ouvrez votre éditeur de texte préféré, puis copiez et collez le script précédent dans l’éditeur.</span><span class="sxs-lookup"><span data-stu-id="82c3b-136">Open your favorite text editor, then copy and paste the preceding script into the editor.</span></span>

2. <span data-ttu-id="82c3b-137">Ensuite, mettez à jour les variables du script pour refléter vos paramètres de configuration.</span><span class="sxs-lookup"><span data-stu-id="82c3b-137">Next, update the script's variables to reflect your configuration settings.</span></span> <span data-ttu-id="82c3b-138">Remplacez les valeurs suivantes comme indiqué :</span><span class="sxs-lookup"><span data-stu-id="82c3b-138">Replace the following values as specified:</span></span>

   * <span data-ttu-id="82c3b-139">**\<storage_account_name\>** : nom de votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="82c3b-139">**\<storage_account_name\>** The name of your storage account.</span></span>
   * <span data-ttu-id="82c3b-140">**\<storage_account_key\>** : clé d’accès primaire ou secondaire pour votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="82c3b-140">**\<storage_account_key\>** The primary or secondary access key for your storage account.</span></span>
   * <span data-ttu-id="82c3b-141">**\<container_name\>** : nom du nouveau conteneur à créer, par exemple « azure-cli-sample-container ».</span><span class="sxs-lookup"><span data-stu-id="82c3b-141">**\<container_name\>** A name the new container to create, such as "azure-cli-sample-container".</span></span>
   * <span data-ttu-id="82c3b-142">**\<blob_name\>** : nom de l’objet blob de destination dans le conteneur.</span><span class="sxs-lookup"><span data-stu-id="82c3b-142">**\<blob_name\>** A name for the destination blob in the container.</span></span>
   * <span data-ttu-id="82c3b-143">**\<file_to_upload\>** : chemin d’accès au petit fichier sur l’ordinateur local, par exemple « ~/images/HelloWorld.png ».</span><span class="sxs-lookup"><span data-stu-id="82c3b-143">**\<file_to_upload\>** The path to small file on your local computer, such as "~/images/HelloWorld.png".</span></span>
   * <span data-ttu-id="82c3b-144">**\<destination_file\>** : chemin d’accès au fichier de destination, par exemple « ~/downloadedImage.png ».</span><span class="sxs-lookup"><span data-stu-id="82c3b-144">**\<destination_file\>** The destination file path, such as "~/downloadedImage.png".</span></span>

3. <span data-ttu-id="82c3b-145">Une fois que vous avez mis à jour les variables nécessaires, enregistrez le script et quittez l’éditeur.</span><span class="sxs-lookup"><span data-stu-id="82c3b-145">After you've updated the necessary variables, save the script and exit your editor.</span></span> <span data-ttu-id="82c3b-146">Les étapes suivantes supposent que vous avez nommé votre script **my_storage_sample.sh**.</span><span class="sxs-lookup"><span data-stu-id="82c3b-146">The next steps assume you've named your script **my_storage_sample.sh**.</span></span>

4. <span data-ttu-id="82c3b-147">Rendez le script exécutable, si nécessaire : `chmod +x my_storage_sample.sh`</span><span class="sxs-lookup"><span data-stu-id="82c3b-147">Mark the script as executable, if necessary: `chmod +x my_storage_sample.sh`</span></span>

5. <span data-ttu-id="82c3b-148">Exécutez le script.</span><span class="sxs-lookup"><span data-stu-id="82c3b-148">Execute the script.</span></span> <span data-ttu-id="82c3b-149">Par exemple, dans Bash : `./my_storage_sample.sh`</span><span class="sxs-lookup"><span data-stu-id="82c3b-149">For example, in Bash: `./my_storage_sample.sh`</span></span>

<span data-ttu-id="82c3b-150">Vous devriez voir une sortie similaire à ce qui suit et la variable **\<destination_file\>** spécifiée dans le script doit s’afficher sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="82c3b-150">You should see output similar to the following, and the **\<destination_file\>** you specified in the script should appear on your local computer.</span></span>

```
Creating the container...
{
  "created": true
}
Uploading the file...
Percent complete: %100.0
Listing the blobs...
Name       Blob Type      Length  Content Type              Last Modified
---------  -----------  --------  ------------------------  -------------------------
README.md  BlockBlob        6700  application/octet-stream  2017-05-12T20:54:59+00:00
Downloading the file...
Name
---------
README.md
Done
```

> [!TIP]
> <span data-ttu-id="82c3b-151">La sortie précédente est au format **table**.</span><span class="sxs-lookup"><span data-stu-id="82c3b-151">The preceding output is in **table** format.</span></span> <span data-ttu-id="82c3b-152">Vous pouvez spécifier le format de sortie à utiliser en spécifiant l’argument `--output` dans vos commandes CLI ou en le définissant globalement à l’aide de `az configure`.</span><span class="sxs-lookup"><span data-stu-id="82c3b-152">You can specify which output format to use by specifying the `--output` argument in your CLI commands, or set it globally using `az configure`.</span></span>
>

## <a name="manage-storage-accounts"></a><span data-ttu-id="82c3b-153">Gestion des comptes de stockage</span><span class="sxs-lookup"><span data-stu-id="82c3b-153">Manage storage accounts</span></span>

### <a name="create-a-new-storage-account"></a><span data-ttu-id="82c3b-154">Création d’un nouveau compte de stockage</span><span class="sxs-lookup"><span data-stu-id="82c3b-154">Create a new storage account</span></span>
<span data-ttu-id="82c3b-155">Pour utiliser le Stockage Azure, vous avez besoin d’un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="82c3b-155">To use Azure Storage, you need a storage account.</span></span> <span data-ttu-id="82c3b-156">Vous pouvez créer un nouveau compte de stockage Azure après avoir configuré votre ordinateur pour qu’il se [connecte à votre abonnement](#connect-to-your-azure-subscription).</span><span class="sxs-lookup"><span data-stu-id="82c3b-156">You can create a new Azure Storage account after you've configured your computer to [connect to your subscription](#connect-to-your-azure-subscription).</span></span>

```azurecli
az storage account create \
    --location <location> \
    --name <account_name> \
    --resource-group <resource_group> \
    --sku <account_sku>
```

* <span data-ttu-id="82c3b-157">`--location` [Obligatoire] : emplacement.</span><span class="sxs-lookup"><span data-stu-id="82c3b-157">`--location` [Required]: Location.</span></span> <span data-ttu-id="82c3b-158">Par exemple, « États-Unis de l’Ouest ».</span><span class="sxs-lookup"><span data-stu-id="82c3b-158">For example, "West US".</span></span>
* <span data-ttu-id="82c3b-159">`--name` [Obligatoire] : nom du compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="82c3b-159">`--name` [Required]: The storage account name.</span></span> <span data-ttu-id="82c3b-160">Le nom doit comporter entre 3 et 24 caractères, lesquels ne peuvent être que des caractères alphanumériques minuscules.</span><span class="sxs-lookup"><span data-stu-id="82c3b-160">The name must be 3 to 24 characters in length, and use only lowercase alphanumeric characters.</span></span>
* <span data-ttu-id="82c3b-161">`--resource-group` [Obligatoire] : nom du groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="82c3b-161">`--resource-group` [Required]: Name of resource group.</span></span>
* <span data-ttu-id="82c3b-162">`--sku` [Obligatoire] : référence du compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="82c3b-162">`--sku` [Required]: The storage account SKU.</span></span> <span data-ttu-id="82c3b-163">Valeurs autorisées :</span><span class="sxs-lookup"><span data-stu-id="82c3b-163">Allowed values:</span></span>
  * `Premium_LRS`
  * `Standard_GRS`
  * `Standard_LRS`
  * `Standard_RAGRS`
  * `Standard_ZRS`

### <a name="set-default-azure-storage-account-environment-variables"></a><span data-ttu-id="82c3b-164">Définition des variables d’environnement par défaut pour le compte de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="82c3b-164">Set default Azure storage account environment variables</span></span>
<span data-ttu-id="82c3b-165">Vous pouvez disposer de plusieurs comptes de stockage dans votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="82c3b-165">You can have multiple storage accounts in your Azure subscription.</span></span> <span data-ttu-id="82c3b-166">Pour en sélectionner un à utiliser pour toutes les commandes de stockage suivantes, vous pouvez définir ces variables d’environnement :</span><span class="sxs-lookup"><span data-stu-id="82c3b-166">To select one of them to use for all subsequent storage commands, you can set these environment variables:</span></span>

```azurecli
export AZURE_STORAGE_ACCOUNT=<account_name>
export AZURE_STORAGE_ACCESS_KEY=<key>
```

<span data-ttu-id="82c3b-167">Vous pouvez également définir un compte de stockage par défaut via une chaîne de connexion.</span><span class="sxs-lookup"><span data-stu-id="82c3b-167">Another way to set a default storage account is by using a connection string.</span></span> <span data-ttu-id="82c3b-168">Commencez par obtenir la chaîne de connexion à l’aide de la commande `show-connection-string` :</span><span class="sxs-lookup"><span data-stu-id="82c3b-168">First, get the connection string with the `show-connection-string` command:</span></span>

```azurecli
az storage account show-connection-string \
    --name <account_name> \
    --resource-group <resource_group>
```

<span data-ttu-id="82c3b-169">Ensuite, copiez la chaîne de connexion de sortie et définissez la variable d’environnement `AZURE_STORAGE_CONNECTION_STRING` (vous devrez peut-être mettre la chaîne de connexion entre guillemets) :</span><span class="sxs-lookup"><span data-stu-id="82c3b-169">Then copy the output connection string and set the `AZURE_STORAGE_CONNECTION_STRING` environment variable (you might need to enclose the connection string in quotes):</span></span>

```azurecli
export AZURE_STORAGE_CONNECTION_STRING="<connection_string>"
```

> [!NOTE]
> <span data-ttu-id="82c3b-170">Tous les exemples des sections suivantes de cet article supposent que vous avez défini les variables d’environnement `AZURE_STORAGE_ACCOUNT` et `AZURE_STORAGE_ACCESS_KEY`.</span><span class="sxs-lookup"><span data-stu-id="82c3b-170">All examples in the following sections of this article assume that you've set the `AZURE_STORAGE_ACCOUNT` and `AZURE_STORAGE_ACCESS_KEY` environment variables.</span></span>
>

## <a name="create-and-manage-blobs"></a><span data-ttu-id="82c3b-171">Créer et gérer des objets blob</span><span class="sxs-lookup"><span data-stu-id="82c3b-171">Create and manage blobs</span></span>
<span data-ttu-id="82c3b-172">Le stockage d’objets blob Azure est un service permettant de stocker de gros volumes de données non structurées, telles que du texte ou des données binaires, accessibles depuis n’importe où dans le monde via HTTP ou HTTPS.</span><span class="sxs-lookup"><span data-stu-id="82c3b-172">Azure Blob storage is a service for storing large amounts of unstructured data, such as text or binary data, that can be accessed from anywhere in the world via HTTP or HTTPS.</span></span> <span data-ttu-id="82c3b-173">Cette section suppose que vous êtes déjà familiarisé avec les concepts du Stockage Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="82c3b-173">This section assumes that you are already familiar with Azure Blob storage concepts.</span></span> <span data-ttu-id="82c3b-174">Pour obtenir des informations détaillées, consultez [Prise en main du Stockage Blob Azure à l’aide de .NET](storage-dotnet-how-to-use-blobs.md) et [Concepts de service Blob](/rest/api/storageservices/blob-service-concepts).</span><span class="sxs-lookup"><span data-stu-id="82c3b-174">For detailed information, see [Get started with Azure Blob storage using .NET](storage-dotnet-how-to-use-blobs.md) and [Blob Service Concepts](/rest/api/storageservices/blob-service-concepts).</span></span>

### <a name="create-a-container"></a><span data-ttu-id="82c3b-175">Créer un conteneur</span><span class="sxs-lookup"><span data-stu-id="82c3b-175">Create a container</span></span>
<span data-ttu-id="82c3b-176">Chaque objet blob du stockage Azure doit se trouver dans un conteneur.</span><span class="sxs-lookup"><span data-stu-id="82c3b-176">Every blob in Azure storage must be in a container.</span></span> <span data-ttu-id="82c3b-177">Vous pouvez créer un conteneur à l’aide de la commande `az storage container create` :</span><span class="sxs-lookup"><span data-stu-id="82c3b-177">You can create a container by using the `az storage container create` command:</span></span>

```azurecli
az storage container create --name <container_name>
```

<span data-ttu-id="82c3b-178">Vous pouvez définir l’un des trois niveaux d’accès en lecture pour un nouveau conteneur en spécifiant l’argument facultatif `--public-access` :</span><span class="sxs-lookup"><span data-stu-id="82c3b-178">You can set one of three levels of read access for a new container by specifying the optional  `--public-access` argument:</span></span>

* <span data-ttu-id="82c3b-179">`off` (par défaut) : les données du conteneur sont privées et accessibles uniquement par le propriétaire du compte.</span><span class="sxs-lookup"><span data-stu-id="82c3b-179">`off` (default): Container data is private to the account owner.</span></span>
* <span data-ttu-id="82c3b-180">`blob` : accès en lecture public pour les objets blob.</span><span class="sxs-lookup"><span data-stu-id="82c3b-180">`blob`: Public read access for blobs.</span></span>
* <span data-ttu-id="82c3b-181">`container` : accès en lecture et en création de listes public à l’intégralité du conteneur.</span><span class="sxs-lookup"><span data-stu-id="82c3b-181">`container`: Public read and list access to the entire container.</span></span>

<span data-ttu-id="82c3b-182">Pour plus d’informations, consultez la section [Gestion de l’accès en lecture anonyme aux conteneurs et aux objets blob](storage-manage-access-to-resources.md).</span><span class="sxs-lookup"><span data-stu-id="82c3b-182">For more information, see [Manage anonymous read access to containers and blobs](storage-manage-access-to-resources.md).</span></span>

### <a name="upload-a-blob-to-a-container"></a><span data-ttu-id="82c3b-183">Chargement d’un objet blob dans un conteneur</span><span class="sxs-lookup"><span data-stu-id="82c3b-183">Upload a blob to a container</span></span>
<span data-ttu-id="82c3b-184">Le Stockage Blob Azure prend en charge les objets blob de blocs, d’ajout et de page.</span><span class="sxs-lookup"><span data-stu-id="82c3b-184">Azure Blob storage supports block, append, and page blobs.</span></span> <span data-ttu-id="82c3b-185">Chargez des objets blob dans un conteneur à l’aide de la commande `blob upload` :</span><span class="sxs-lookup"><span data-stu-id="82c3b-185">Upload blobs to a container by using the `blob upload` command:</span></span>

```azurecli
az storage blob upload \
    --file <local_file_path> \
    --container-name <container_name> \
    --name <blob_name>
```

 <span data-ttu-id="82c3b-186">Sinon, la commande `blob upload` charge par défaut les fichiers *.vhd dans les objets blob de pages ou de blocs.</span><span class="sxs-lookup"><span data-stu-id="82c3b-186">By default, the `blob upload` command uploads *.vhd files to page blobs, or block blobs otherwise.</span></span> <span data-ttu-id="82c3b-187">Pour spécifier un autre type lorsque vous chargez un objet blob, vous pouvez utiliser l’argument `--type` ; les valeurs autorisée sont `append`, `block` et `page`.</span><span class="sxs-lookup"><span data-stu-id="82c3b-187">To specify another type when you upload a blob, you can use the `--type` argument--allowed values are `append`, `block`, and `page`.</span></span>

 <span data-ttu-id="82c3b-188">Pour plus d’informations sur les différents objets blob, consultez [Présentation des objets blob de blocs, des objets blob d’ajout et des objets blob de pages](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs).</span><span class="sxs-lookup"><span data-stu-id="82c3b-188">For more information on the different blob types, see [Understanding Block Blobs, Append Blobs, and Page Blobs](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs).</span></span>


### <a name="download-a-blob-from-a-container"></a><span data-ttu-id="82c3b-189">Télécharger un objet blob depuis un conteneur</span><span class="sxs-lookup"><span data-stu-id="82c3b-189">Download a blob from a container</span></span>
<span data-ttu-id="82c3b-190">Cet exemple indique comment télécharger un objet blob à partir d’un conteneur :</span><span class="sxs-lookup"><span data-stu-id="82c3b-190">This example demonstrates how to download a blob from a container:</span></span>

```azurecli
az storage blob download \
    --container-name mycontainer \
    --name myblob.png \
    --file ~/mydownloadedblob.png
```

### <a name="list-the-blobs-in-a-container"></a><span data-ttu-id="82c3b-191">Création d'une liste d'objets blob dans un conteneur</span><span class="sxs-lookup"><span data-stu-id="82c3b-191">List the blobs in a container</span></span>

<span data-ttu-id="82c3b-192">Répertoriez les objets blob dans un conteneur à l’aide de la commande [az storage blob list](/cli/azure/storage/blob#list).</span><span class="sxs-lookup"><span data-stu-id="82c3b-192">List the blobs in a container with the [az storage blob list](/cli/azure/storage/blob#list) command.</span></span>

```azurecli
az storage blob list \
    --container-name mycontainer \
    --output table
```

### <a name="copy-blobs"></a><span data-ttu-id="82c3b-193">Copier des objets blob</span><span class="sxs-lookup"><span data-stu-id="82c3b-193">Copy blobs</span></span>
<span data-ttu-id="82c3b-194">Vous pouvez copier des objets blob au sein d’un compte de stockage, ou vers des comptes de stockage et des régions et ce, de façon asynchrone.</span><span class="sxs-lookup"><span data-stu-id="82c3b-194">You can copy blobs within or across storage accounts and regions asynchronously.</span></span>

<span data-ttu-id="82c3b-195">L’exemple suivant indique comment copier des objets blob depuis un compte de stockage et les coller dans un autre.</span><span class="sxs-lookup"><span data-stu-id="82c3b-195">The following example demonstrates how to copy blobs from one storage account to another.</span></span> <span data-ttu-id="82c3b-196">Nous créons d’abord un conteneur dans le compte de stockage source, en spécifiant l’accès en lecture public pour ses objets blob.</span><span class="sxs-lookup"><span data-stu-id="82c3b-196">We first create a container in the source storage account, specifying public read-access for its blobs.</span></span> <span data-ttu-id="82c3b-197">Ensuite, nous chargeons un fichier dans le conteneur. Pour finir, nous copions l’objet blob de ce conteneur vers un conteneur du compte de stockage de destination.</span><span class="sxs-lookup"><span data-stu-id="82c3b-197">Next, we upload a file to the container, and finally, copy the blob from that container into a container in the destination storage account.</span></span>

```azurecli
# Create container in source account
az storage container create \
    --account-name sourceaccountname \
    --account-key sourceaccountkey \
    --name sourcecontainer \
    --public-access blob

# Upload blob to container in source account
az storage blob upload \
    --account-name sourceaccountname \
    --account-key sourceaccountkey \
    --container-name sourcecontainer \
    --file ~/Pictures/sourcefile.png \
    --name sourcefile.png

# Copy blob from source account to destination account (destcontainer must exist)
az storage blob copy start \
    --account-name destaccountname \
    --account-key destaccountkey \
    --destination-blob destfile.png \
    --destination-container destcontainer \
    --source-uri https://sourceaccountname.blob.core.windows.net/sourcecontainer/sourcefile.png
```

<span data-ttu-id="82c3b-198">Dans l’exemple indiqué ci-dessus, le conteneur de destination doit déjà exister dans le compte de stockage de destination pour que l’opération de copie réussisse.</span><span class="sxs-lookup"><span data-stu-id="82c3b-198">In the above example, the destination container must already exist in the destination storage account for the copy operation to succeed.</span></span> <span data-ttu-id="82c3b-199">En outre, l’objet blob source spécifié dans l’argument `--source-uri` doit inclure un jeton de signature d’accès partagé, ou être accessible publiquement, comme dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="82c3b-199">Additionally, the source blob specified in the `--source-uri` argument must either include a shared access signature (SAS) token, or be publicly accessible, as in this example.</span></span>

### <a name="delete-a-blob"></a><span data-ttu-id="82c3b-200">Supprimer un objet blob</span><span class="sxs-lookup"><span data-stu-id="82c3b-200">Delete a blob</span></span>
<span data-ttu-id="82c3b-201">Pour supprimer un objet blob, utilisez la commande `blob delete` :</span><span class="sxs-lookup"><span data-stu-id="82c3b-201">To delete a blob, use the `blob delete` command:</span></span>

```azurecli
az storage blob delete --container-name <container_name> --name <blob_name>
```

## <a name="create-and-manage-file-shares"></a><span data-ttu-id="82c3b-202">Créer et gérer des partages de fichiers</span><span class="sxs-lookup"><span data-stu-id="82c3b-202">Create and manage file shares</span></span>
<span data-ttu-id="82c3b-203">Le Stockage Fichier Azure propose un stockage partagé pour les applications utilisant le protocole SMB.</span><span class="sxs-lookup"><span data-stu-id="82c3b-203">Azure File storage offers shared storage for applications using the Server Message Block (SMB) protocol.</span></span> <span data-ttu-id="82c3b-204">Les services cloud et les machines virtuelles Microsoft Azure, ainsi que les applications locales, peuvent partager des données de fichiers via des partages montés.</span><span class="sxs-lookup"><span data-stu-id="82c3b-204">Microsoft Azure virtual machines and cloud services, as well as on-premises applications, can share file data via mounted shares.</span></span> <span data-ttu-id="82c3b-205">Vous pouvez gérer des partages de fichiers et des données de fichiers via la CLI Azure.</span><span class="sxs-lookup"><span data-stu-id="82c3b-205">You can manage file shares and file data via the Azure CLI.</span></span> <span data-ttu-id="82c3b-206">Pour plus d’informations sur Azure File Storage, consultez [Prise en main du stockage de fichiers Azure sur Windows](storage-dotnet-how-to-use-files.md) ou [Utilisation du stockage de fichiers Azure avec Linux](storage-how-to-use-files-linux.md).</span><span class="sxs-lookup"><span data-stu-id="82c3b-206">For more information on Azure File storage, see [Get started with Azure File storage on Windows](storage-dotnet-how-to-use-files.md) or [How to use Azure File storage with Linux](storage-how-to-use-files-linux.md).</span></span>

### <a name="create-a-file-share"></a><span data-ttu-id="82c3b-207">Créer un partage de fichiers</span><span class="sxs-lookup"><span data-stu-id="82c3b-207">Create a file share</span></span>
<span data-ttu-id="82c3b-208">Un partage de fichiers Azure est un partage de fichiers SMB dans Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="82c3b-208">An Azure File share is an SMB file share in Azure.</span></span> <span data-ttu-id="82c3b-209">Tous les répertoires et fichiers doivent être créés dans un partage de fichiers.</span><span class="sxs-lookup"><span data-stu-id="82c3b-209">All directories and files must be created in a file share.</span></span> <span data-ttu-id="82c3b-210">Un compte peut contenir un nombre illimité de partages, et un partage peut stocker un nombre illimité de fichiers, dans les limites de capacité du compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="82c3b-210">An account can contain an unlimited number of shares, and a share can store an unlimited number of files, up to the capacity limits of the storage account.</span></span> <span data-ttu-id="82c3b-211">L’exemple suivant détaille la création d’un partage de fichiers nommé **MonPartage**.</span><span class="sxs-lookup"><span data-stu-id="82c3b-211">The following example creates a file share named **myshare**.</span></span>

```azurecli
az storage share create --name myshare
```

### <a name="create-a-directory"></a><span data-ttu-id="82c3b-212">Créer un répertoire</span><span class="sxs-lookup"><span data-stu-id="82c3b-212">Create a directory</span></span>
<span data-ttu-id="82c3b-213">Un répertoire fournit une structure hiérarchique dans un partage de fichiers Azure.</span><span class="sxs-lookup"><span data-stu-id="82c3b-213">A directory provides a hierarchical structure in an Azure file share.</span></span> <span data-ttu-id="82c3b-214">L’exemple suivant crée un répertoire nommé **MonRép** dans le partage de fichiers.</span><span class="sxs-lookup"><span data-stu-id="82c3b-214">The following example creates a directory named **myDir** in the file share.</span></span>

```azurecli
az storage directory create --name myDir --share-name myshare
```

<span data-ttu-id="82c3b-215">Un chemin d’accès peut inclure plusieurs niveaux, par exemple **dir1/dir2**.</span><span class="sxs-lookup"><span data-stu-id="82c3b-215">A directory path can include multiple levels, for example **dir1/dir2**.</span></span> <span data-ttu-id="82c3b-216">Toutefois, avant de créer un sous-répertoire, vous devez vous assurer que tous les répertoires parents existent.</span><span class="sxs-lookup"><span data-stu-id="82c3b-216">However, you must ensure that all parent directories exist before creating a subdirectory.</span></span> <span data-ttu-id="82c3b-217">Par exemple, pour le chemin d’accès **dir1/dir2**, vous devez créer le répertoire **dir1**, puis le répertoire **dir2**.</span><span class="sxs-lookup"><span data-stu-id="82c3b-217">For example, for path **dir1/dir2**, you must first create directory **dir1**, then create directory **dir2**.</span></span>

### <a name="upload-a-local-file-to-a-share"></a><span data-ttu-id="82c3b-218">Chargement d’un fichier local vers un partage</span><span class="sxs-lookup"><span data-stu-id="82c3b-218">Upload a local file to a share</span></span>
<span data-ttu-id="82c3b-219">Dans l’exemple suivant, un fichier est chargé à partir de l’emplacement **~/temp/samplefile.txt** vers la racine du partage de fichiers **myshare**.</span><span class="sxs-lookup"><span data-stu-id="82c3b-219">The following example uploads a file from **~/temp/samplefile.txt** to root of the **myshare** file share.</span></span> <span data-ttu-id="82c3b-220">L’argument `--source` spécifie le fichier local existant à charger.</span><span class="sxs-lookup"><span data-stu-id="82c3b-220">The `--source` argument specifies the existing local file to upload.</span></span>

```azurecli
az storage file upload --share-name myshare --source ~/temp/samplefile.txt
```

<span data-ttu-id="82c3b-221">Comme pour la création d’un répertoire, vous pouvez spécifier un chemin d’accès au répertoire dans le partage pour charger le fichier vers un répertoire existant dans le partage :</span><span class="sxs-lookup"><span data-stu-id="82c3b-221">As with directory creation, you can specify a directory path within the share to upload the file to an existing directory within the share:</span></span>

```azurecli
az storage file upload --share-name myshare/myDir --source ~/temp/samplefile.txt
```

<span data-ttu-id="82c3b-222">Dans le partage, un fichier peut présenter une taille maximale de 1 To.</span><span class="sxs-lookup"><span data-stu-id="82c3b-222">A file in the share can be up to 1 TB in size.</span></span>

### <a name="list-the-files-in-a-share"></a><span data-ttu-id="82c3b-223">Liste des fichiers dans un partage</span><span class="sxs-lookup"><span data-stu-id="82c3b-223">List the files in a share</span></span>
<span data-ttu-id="82c3b-224">Vous pouvez répertorier les fichiers et les répertoires dans un partage à l’aide de la commande `az storage file list` :</span><span class="sxs-lookup"><span data-stu-id="82c3b-224">You can list files and directories in a share by using the `az storage file list` command:</span></span>

```azurecli
# List the files in the root of a share
az storage file list --share-name myshare --output table

# List the files in a directory within a share
az storage file list --share-name myshare/myDir --output table

# List the files in a path within a share
az storage file list --share-name myshare --path myDir/mySubDir/MySubDir2 --output table
```

### <a name="copy-files"></a><span data-ttu-id="82c3b-225">Copie des fichiers</span><span class="sxs-lookup"><span data-stu-id="82c3b-225">Copy files</span></span>      
<span data-ttu-id="82c3b-226">Vous pouvez copier un fichier dans un autre, un fichier dans un objet blob ou un objet blob dans un fichier.</span><span class="sxs-lookup"><span data-stu-id="82c3b-226">You can copy a file to another file, a file to a blob, or a blob to a file.</span></span> <span data-ttu-id="82c3b-227">Par exemple, pour copier un fichier vers un répertoire dans un partage différent :</span><span class="sxs-lookup"><span data-stu-id="82c3b-227">For example, to copy a file to a directory in a different share:</span></span>        
        
```azurecli
az storage file copy start \
--source-share share1 --source-path dir1/file.txt \
--destination-share share2 --destination-path dir2/file.txt     
```

## <a name="next-steps"></a><span data-ttu-id="82c3b-228">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="82c3b-228">Next steps</span></span>
<span data-ttu-id="82c3b-229">Voici quelques ressources supplémentaires pour en savoir plus sur l’utilisation d’Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="82c3b-229">Here are some additional resources for learning more about working with the Azure CLI 2.0.</span></span>

* [<span data-ttu-id="82c3b-230">Prise en main d’Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="82c3b-230">Get started with Azure CLI 2.0</span></span>](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)
* [<span data-ttu-id="82c3b-231">Référence des commandes Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="82c3b-231">Azure CLI 2.0 command reference</span></span>](/cli/azure)
* [<span data-ttu-id="82c3b-232">Azure CLI 2.0 sur GitHub</span><span class="sxs-lookup"><span data-stu-id="82c3b-232">Azure CLI 2.0 on GitHub</span></span>](https://github.com/Azure/azure-cli)
