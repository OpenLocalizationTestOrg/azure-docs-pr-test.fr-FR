---
title: aaaUsing hello Azure CLI 2.0 avec le stockage Azure | Documents Microsoft
description: "Découvrez comment toouse hello Azure Interface de ligne (Azure) 2.0 avec le stockage Azure toocreate et gérer des comptes de stockage et de travail avec les fichiers et les objets BLOB Windows Azure. Bonjour Azure CLI 2.0 est un outil d’inter-plateformes écrit dans Python."
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
ms.openlocfilehash: 38402373dcd87f1ef05471a02353c77d58f1a9fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-cli-20-with-azure-storage"></a><span data-ttu-id="11a4d-104">À l’aide de hello Azure CLI 2.0 avec le stockage Azure</span><span class="sxs-lookup"><span data-stu-id="11a4d-104">Using hello Azure CLI 2.0 with Azure Storage</span></span>

<span data-ttu-id="11a4d-105">Hello open source, multiplateforme Azure CLI 2.0 fournit un ensemble de commandes pour travailler avec hello plateforme Azure.</span><span class="sxs-lookup"><span data-stu-id="11a4d-105">hello open-source, cross-platform Azure CLI 2.0 provides a set of commands for working with hello Azure platform.</span></span> <span data-ttu-id="11a4d-106">Il fournit la majeure partie de hello même fonctionnalité trouvée dans hello [portail Azure](https://portal.azure.com), y compris l’accès aux données enrichi.</span><span class="sxs-lookup"><span data-stu-id="11a4d-106">It provides much of hello same functionality found in hello [Azure portal](https://portal.azure.com), including rich data access.</span></span>

<span data-ttu-id="11a4d-107">Dans ce guide, nous vous indiquons comment toouse hello [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) tooperform plusieurs tâches, utilisation des ressources dans votre compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="11a4d-107">In this guide, we show you how toouse hello [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) tooperform several tasks working with resources in your Azure Storage account.</span></span> <span data-ttu-id="11a4d-108">Nous vous recommandons de télécharger et installer ou mettre à niveau la version la plus récente toohello Hello CLI 2.0 avant d’utiliser ce guide.</span><span class="sxs-lookup"><span data-stu-id="11a4d-108">We recommend that you download and install or upgrade toohello latest version of hello CLI 2.0 before using this guide.</span></span>

<span data-ttu-id="11a4d-109">exemples de Hello dans le guide de hello partent du principe utiliser hello hello shell Bash sur Ubuntu, mais autres plateformes doivent exécuter la même façon.</span><span class="sxs-lookup"><span data-stu-id="11a4d-109">hello examples in hello guide assume hello use of hello Bash shell on Ubuntu, but other platforms should perform similarly.</span></span> 

[!INCLUDE [storage-cli-versions](../../includes/storage-cli-versions.md)]

## <a name="prerequisites"></a><span data-ttu-id="11a4d-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="11a4d-110">Prerequisites</span></span>
<span data-ttu-id="11a4d-111">Ce guide suppose que vous comprenez les concepts de base hello du stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="11a4d-111">This guide assumes that you understand hello basic concepts of Azure Storage.</span></span> <span data-ttu-id="11a4d-112">Il suppose également que vous êtes en mesure de toosatisfy hello création exigences relatives aux comptes qui sont spécifiées ci-dessous pour Azure et hello service de stockage.</span><span class="sxs-lookup"><span data-stu-id="11a4d-112">It also assumes that you're able toosatisfy hello account creation requirements that are specified below for Azure and hello Storage service.</span></span>

### <a name="accounts"></a><span data-ttu-id="11a4d-113">Comptes</span><span class="sxs-lookup"><span data-stu-id="11a4d-113">Accounts</span></span>
* <span data-ttu-id="11a4d-114">**Compte Azure** : si vous ne possédez pas encore d’abonnement Azure, [créez un compte Azure gratuit](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="11a4d-114">**Azure account**: If you don't already have an Azure subscription, [create a free Azure account](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="11a4d-115">**Compte de stockage** : voir la section [Créer un compte de stockage](../storage/storage-create-storage-account.md#create-a-storage-account) de l’article [À propos des comptes de stockage Azure](../storage/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="11a4d-115">**Storage account**: See [Create a storage account](../storage/storage-create-storage-account.md#create-a-storage-account) in [About Azure storage accounts](../storage/storage-create-storage-account.md).</span></span>

### <a name="install-hello-azure-cli-20"></a><span data-ttu-id="11a4d-116">Installer hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="11a4d-116">Install hello Azure CLI 2.0</span></span>

<span data-ttu-id="11a4d-117">Téléchargez et installez hello Azure CLI 2.0 en suivant les instructions hello décrites dans [installer Azure CLI 2.0](/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="11a4d-117">Download and install hello Azure CLI 2.0 by following hello instructions outlined in [Install Azure CLI 2.0](/cli/azure/install-az-cli2).</span></span>

> [!TIP]
> <span data-ttu-id="11a4d-118">Si vous avez des difficultés avec l’installation de hello, extraire hello [dépannage de l’Installation](/cli/azure/install-az-cli2#installation-troubleshooting) section de l’article de hello et hello [installer dépannage](https://github.com/Azure/azure-cli/blob/master/doc/install_troubleshooting.md) guide sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="11a4d-118">If you have trouble with hello installation, check out hello [Installation Troubleshooting](/cli/azure/install-az-cli2#installation-troubleshooting) section of hello article, and hello [Install Troubleshooting](https://github.com/Azure/azure-cli/blob/master/doc/install_troubleshooting.md) guide on GitHub.</span></span>
>

## <a name="working-with-hello-cli"></a><span data-ttu-id="11a4d-119">Utilisation de hello CLI</span><span class="sxs-lookup"><span data-stu-id="11a4d-119">Working with hello CLI</span></span>

<span data-ttu-id="11a4d-120">Une fois que vous avez installé hello CLI, vous pouvez utiliser hello `az` dans vos commandes de CLI d’Azure de hello tooaccess interface de ligne de commande (interpréteur de commandes, Terminal Server, invite de commandes).</span><span class="sxs-lookup"><span data-stu-id="11a4d-120">Once you've installed hello CLI, you can use hello `az` command in your command-line interface (Bash, Terminal, Command Prompt) tooaccess hello Azure CLI commands.</span></span> <span data-ttu-id="11a4d-121">Hello de type `az` commande toosee une liste complète des commandes de base hello (hello suivant l’exemple de sortie a été tronquée) :</span><span class="sxs-lookup"><span data-stu-id="11a4d-121">Type hello `az` command toosee a full list of hello base commands (hello following example output has been truncated):</span></span>

```
     /\
    /  \    _____   _ _ __ ___
   / /\ \  |_  / | | | \'__/ _ \
  / ____ \  / /| |_| | | |  __/
 /_/    \_\/___|\__,_|_|  \___|


Welcome toohello cool new Azure CLI!

Here are hello base commands:

    account          : Manage subscriptions.
    acr              : Manage Azure container registries.
    acs              : Manage Azure Container Services.
    ad               : Synchronize on-premises directories and manage Azure Active Directory
                       resources.
    ...
```

<span data-ttu-id="11a4d-122">Dans l’interface de ligne de commande, exécutez la commande hello `az storage --help` hello de toolist `storage` commande sous-groupes.</span><span class="sxs-lookup"><span data-stu-id="11a4d-122">In your command-line interface, execute hello command `az storage --help` toolist hello `storage` command subgroups.</span></span> <span data-ttu-id="11a4d-123">descriptions de Hello de sous-groupes de hello fournissent une vue d’ensemble de hello de fonctionnalité hello que CLI d’Azure fournit pour travailler avec vos ressources de stockage.</span><span class="sxs-lookup"><span data-stu-id="11a4d-123">hello descriptions of hello subgroups provide an overview of hello functionality hello Azure CLI provides for working with your storage resources.</span></span>

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
    file     : File shares that use hello standard SMB 3.0 protocol.
    logging  : Manage Storage service logging information.
    message  : Manage queue storage messages.
    metrics  : Manage Storage service metrics.
    queue    : Use queues tooeffectively scale applications according tootraffic.
    share    : Manage file shares.
    table    : NoSQL key-value storage using semi-structured datasets.
```

## <a name="connect-hello-cli-tooyour-azure-subscription"></a><span data-ttu-id="11a4d-124">Se connecter hello CLI tooyour abonnement Azure</span><span class="sxs-lookup"><span data-stu-id="11a4d-124">Connect hello CLI tooyour Azure subscription</span></span>

<span data-ttu-id="11a4d-125">toowork des ressources de hello dans votre abonnement Azure, vous devez tout d’abord vous connecter tooyour compte Azure avec `az login`.</span><span class="sxs-lookup"><span data-stu-id="11a4d-125">toowork with hello resources in your Azure subscription, you must first log in tooyour Azure account with `az login`.</span></span> <span data-ttu-id="11a4d-126">Vous pouvez vous connecter de plusieurs façons :</span><span class="sxs-lookup"><span data-stu-id="11a4d-126">There are several ways you can log in:</span></span>

* <span data-ttu-id="11a4d-127">**Connexion interactive** : `az login`</span><span class="sxs-lookup"><span data-stu-id="11a4d-127">**Interactive login**: `az login`</span></span>
* <span data-ttu-id="11a4d-128">**Connexion avec nom d’utilisateur et mot de passe** : `az login -u johndoe@contoso.com -p VerySecret`</span><span class="sxs-lookup"><span data-stu-id="11a4d-128">**Log in with user name and password**: `az login -u johndoe@contoso.com -p VerySecret`</span></span>
  * <span data-ttu-id="11a4d-129">Ceci ne fonctionne pas avec les comptes Microsoft ou les comptes qui utilisent l’authentification multifacteur.</span><span class="sxs-lookup"><span data-stu-id="11a4d-129">This doesn't work with Microsoft accounts or accounts that use multi-factor authentication.</span></span>
* <span data-ttu-id="11a4d-130">**Connexion avec un principal du service** : `az login --service-principal -u http://azure-cli-2016-08-05-14-31-15 -p VerySecret --tenant contoso.onmicrosoft.com`</span><span class="sxs-lookup"><span data-stu-id="11a4d-130">**Log in with a service principal**: `az login --service-principal -u http://azure-cli-2016-08-05-14-31-15 -p VerySecret --tenant contoso.onmicrosoft.com`</span></span>

## <a name="azure-cli-20-sample-script"></a><span data-ttu-id="11a4d-131">Exemple de script CLI 2.0 Azure</span><span class="sxs-lookup"><span data-stu-id="11a4d-131">Azure CLI 2.0 sample script</span></span>

<span data-ttu-id="11a4d-132">Ensuite, nous allons utiliser un script shell small qui émet quelques base toointeract de commandes Azure CLI 2.0 avec des ressources de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="11a4d-132">Next, we'll work with a small shell script that issues a few basic Azure CLI 2.0 commands toointeract with Azure Storage resources.</span></span> <span data-ttu-id="11a4d-133">tout d’abord les script Hello crée un nouveau conteneur dans votre compte de stockage, puis télécharge un conteneur existant pour toothat fichier (comme un objet blob).</span><span class="sxs-lookup"><span data-stu-id="11a4d-133">hello script first creates a new container in your storage account, then uploads an existing file (as a blob) toothat container.</span></span> <span data-ttu-id="11a4d-134">Il répertorie ensuite tous les objets BLOB dans le conteneur de hello et enfin, télécharge destination de tooa hello fichier sur votre ordinateur local que vous spécifiez.</span><span class="sxs-lookup"><span data-stu-id="11a4d-134">It then lists all blobs in hello container, and finally, downloads hello file tooa destination on your local computer that you specify.</span></span>

```bash
#!/bin/bash
# A simple Azure Storage example script

export AZURE_STORAGE_ACCOUNT=<storage_account_name>
export AZURE_STORAGE_ACCESS_KEY=<storage_account_key>

export container_name=<container_name>
export blob_name=<blob_name>
export file_to_upload=<file_to_upload>
export destination_file=<destination_file>

echo "Creating hello container..."
az storage container create --name $container_name

echo "Uploading hello file..."
az storage blob upload --container-name $container_name --file $file_to_upload --name $blob_name

echo "Listing hello blobs..."
az storage blob list --container-name $container_name --output table

echo "Downloading hello file..."
az storage blob download --container-name $container_name --name $blob_name --file $destination_file --output table

echo "Done"
```

<span data-ttu-id="11a4d-135">**Configurer et exécuter le script de hello**</span><span class="sxs-lookup"><span data-stu-id="11a4d-135">**Configure and run hello script**</span></span>

1. <span data-ttu-id="11a4d-136">Ouvrez l’éditeur de texte, puis copier- coller hello précédant le script dans l’éditeur de hello.</span><span class="sxs-lookup"><span data-stu-id="11a4d-136">Open your favorite text editor, then copy and paste hello preceding script into hello editor.</span></span>

2. <span data-ttu-id="11a4d-137">Ensuite, mettez à jour tooreflect de variables de script hello vos paramètres de configuration.</span><span class="sxs-lookup"><span data-stu-id="11a4d-137">Next, update hello script's variables tooreflect your configuration settings.</span></span> <span data-ttu-id="11a4d-138">Remplacez hello suivant des valeurs comme indiqué :</span><span class="sxs-lookup"><span data-stu-id="11a4d-138">Replace hello following values as specified:</span></span>

   * <span data-ttu-id="11a4d-139">**\<storage_account_name\>**  nom hello de votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="11a4d-139">**\<storage_account_name\>** hello name of your storage account.</span></span>
   * <span data-ttu-id="11a4d-140">**\<storage_account_key\>**  clé d’accès primaire ou secondaire hello pour votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="11a4d-140">**\<storage_account_key\>** hello primary or secondary access key for your storage account.</span></span>
   * <span data-ttu-id="11a4d-141">**\<nom_conteneur\>**  un nom hello nouvelle toocreate de conteneur, tel que « azure-cli-exemple-container ».</span><span class="sxs-lookup"><span data-stu-id="11a4d-141">**\<container_name\>** A name hello new container toocreate, such as "azure-cli-sample-container".</span></span>
   * <span data-ttu-id="11a4d-142">**\<blob_name\>**  un nom pour l’objet blob de destination hello dans le conteneur de hello.</span><span class="sxs-lookup"><span data-stu-id="11a4d-142">**\<blob_name\>** A name for hello destination blob in hello container.</span></span>
   * <span data-ttu-id="11a4d-143">**\<file_to_upload\>**  hello chemin d’accès fichier toosmall sur votre ordinateur local, tel que « ~ / images/HelloWorld.png ».</span><span class="sxs-lookup"><span data-stu-id="11a4d-143">**\<file_to_upload\>** hello path toosmall file on your local computer, such as "~/images/HelloWorld.png".</span></span>
   * <span data-ttu-id="11a4d-144">**\<destination_file\>**  hello chemin d’accès du fichier de destination, tel que « ~ / downloadedImage.png ».</span><span class="sxs-lookup"><span data-stu-id="11a4d-144">**\<destination_file\>** hello destination file path, such as "~/downloadedImage.png".</span></span>

3. <span data-ttu-id="11a4d-145">Une fois que vous avez mis à jour les variables nécessaires hello, enregistrer le script de hello et quittez l’éditeur.</span><span class="sxs-lookup"><span data-stu-id="11a4d-145">After you've updated hello necessary variables, save hello script and exit your editor.</span></span> <span data-ttu-id="11a4d-146">les étapes suivantes Hello supposent que vous avez nommé votre script **my_storage_sample.sh**.</span><span class="sxs-lookup"><span data-stu-id="11a4d-146">hello next steps assume you've named your script **my_storage_sample.sh**.</span></span>

4. <span data-ttu-id="11a4d-147">Marquer le script hello en tant que fichier exécutable, si nécessaire :`chmod +x my_storage_sample.sh`</span><span class="sxs-lookup"><span data-stu-id="11a4d-147">Mark hello script as executable, if necessary: `chmod +x my_storage_sample.sh`</span></span>

5. <span data-ttu-id="11a4d-148">Exécuter le script de hello.</span><span class="sxs-lookup"><span data-stu-id="11a4d-148">Execute hello script.</span></span> <span data-ttu-id="11a4d-149">Par exemple, dans Bash : `./my_storage_sample.sh`</span><span class="sxs-lookup"><span data-stu-id="11a4d-149">For example, in Bash: `./my_storage_sample.sh`</span></span>

<span data-ttu-id="11a4d-150">Vous devez voir sortie similaire toohello et hello  **\<destination_file\>**  vous avez spécifié dans hello script doit s’afficher sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="11a4d-150">You should see output similar toohello following, and hello **\<destination_file\>** you specified in hello script should appear on your local computer.</span></span>

```
Creating hello container...
{
  "created": true
}
Uploading hello file...
Percent complete: %100.0
Listing hello blobs...
Name       Blob Type      Length  Content Type              Last Modified
---------  -----------  --------  ------------------------  -------------------------
README.md  BlockBlob        6700  application/octet-stream  2017-05-12T20:54:59+00:00
Downloading hello file...
Name
---------
README.md
Done
```

> [!TIP]
> <span data-ttu-id="11a4d-151">Hello sortie précédente est en **table** format.</span><span class="sxs-lookup"><span data-stu-id="11a4d-151">hello preceding output is in **table** format.</span></span> <span data-ttu-id="11a4d-152">Vous pouvez spécifier toouse du format de sortie en spécifiant hello `--output` argument dans vos commandes CLI, ou globalement à l’aide de la valeur `az configure`.</span><span class="sxs-lookup"><span data-stu-id="11a4d-152">You can specify which output format toouse by specifying hello `--output` argument in your CLI commands, or set it globally using `az configure`.</span></span>
>

## <a name="manage-storage-accounts"></a><span data-ttu-id="11a4d-153">Gestion des comptes de stockage</span><span class="sxs-lookup"><span data-stu-id="11a4d-153">Manage storage accounts</span></span>

### <a name="create-a-new-storage-account"></a><span data-ttu-id="11a4d-154">Création d’un nouveau compte de stockage</span><span class="sxs-lookup"><span data-stu-id="11a4d-154">Create a new storage account</span></span>
<span data-ttu-id="11a4d-155">toouse stockage Azure, vous devez un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="11a4d-155">toouse Azure Storage, you need a storage account.</span></span> <span data-ttu-id="11a4d-156">Vous pouvez créer un nouveau compte de stockage Azure une fois que vous avez configuré votre ordinateur trop[connecter tooyour abonnement](#connect-to-your-azure-subscription).</span><span class="sxs-lookup"><span data-stu-id="11a4d-156">You can create a new Azure Storage account after you've configured your computer too[connect tooyour subscription](#connect-to-your-azure-subscription).</span></span>

```azurecli
az storage account create \
    --location <location> \
    --name <account_name> \
    --resource-group <resource_group> \
    --sku <account_sku>
```

* <span data-ttu-id="11a4d-157">`--location` [Obligatoire] : emplacement.</span><span class="sxs-lookup"><span data-stu-id="11a4d-157">`--location` [Required]: Location.</span></span> <span data-ttu-id="11a4d-158">Par exemple, « États-Unis de l’Ouest ».</span><span class="sxs-lookup"><span data-stu-id="11a4d-158">For example, "West US".</span></span>
* <span data-ttu-id="11a4d-159">`--name`[Obligatoire] : nom de compte de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="11a4d-159">`--name` [Required]: hello storage account name.</span></span> <span data-ttu-id="11a4d-160">nom de Hello doit comporter 3 caractères too24 et utiliser uniquement des caractères alphanumériques en minuscules.</span><span class="sxs-lookup"><span data-stu-id="11a4d-160">hello name must be 3 too24 characters in length, and use only lowercase alphanumeric characters.</span></span>
* <span data-ttu-id="11a4d-161">`--resource-group` [Obligatoire] : nom du groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="11a4d-161">`--resource-group` [Required]: Name of resource group.</span></span>
* <span data-ttu-id="11a4d-162">`--sku`[Obligatoire] : hello compte de stockage référence (SKU).</span><span class="sxs-lookup"><span data-stu-id="11a4d-162">`--sku` [Required]: hello storage account SKU.</span></span> <span data-ttu-id="11a4d-163">Valeurs autorisées :</span><span class="sxs-lookup"><span data-stu-id="11a4d-163">Allowed values:</span></span>
  * `Premium_LRS`
  * `Standard_GRS`
  * `Standard_LRS`
  * `Standard_RAGRS`
  * `Standard_ZRS`

### <a name="set-default-azure-storage-account-environment-variables"></a><span data-ttu-id="11a4d-164">Définition des variables d’environnement par défaut pour le compte de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="11a4d-164">Set default Azure storage account environment variables</span></span>
<span data-ttu-id="11a4d-165">Vous pouvez disposer de plusieurs comptes de stockage dans votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="11a4d-165">You can have multiple storage accounts in your Azure subscription.</span></span> <span data-ttu-id="11a4d-166">tooselect un d’eux toouse de stockage suivants toutes les commandes, vous pouvez définir ces variables d’environnement :</span><span class="sxs-lookup"><span data-stu-id="11a4d-166">tooselect one of them toouse for all subsequent storage commands, you can set these environment variables:</span></span>

```azurecli
export AZURE_STORAGE_ACCOUNT=<account_name>
export AZURE_STORAGE_ACCESS_KEY=<key>
```

<span data-ttu-id="11a4d-167">Une autre façon tooset un compte de stockage par défaut est à l’aide d’une chaîne de connexion.</span><span class="sxs-lookup"><span data-stu-id="11a4d-167">Another way tooset a default storage account is by using a connection string.</span></span> <span data-ttu-id="11a4d-168">Chaîne de connexion hello hello d’abord, obtenir `show-connection-string` commande :</span><span class="sxs-lookup"><span data-stu-id="11a4d-168">First, get hello connection string with hello `show-connection-string` command:</span></span>

```azurecli
az storage account show-connection-string \
    --name <account_name> \
    --resource-group <resource_group>
```

<span data-ttu-id="11a4d-169">Hello de copie la sortie de chaîne de connexion, puis définir hello `AZURE_STORAGE_CONNECTION_STRING` variable d’environnement (vous devrez peut-être chaîne de connexion tooenclose hello entre guillemets) :</span><span class="sxs-lookup"><span data-stu-id="11a4d-169">Then copy hello output connection string and set hello `AZURE_STORAGE_CONNECTION_STRING` environment variable (you might need tooenclose hello connection string in quotes):</span></span>

```azurecli
export AZURE_STORAGE_CONNECTION_STRING="<connection_string>"
```

> [!NOTE]
> <span data-ttu-id="11a4d-170">Tous les exemples de hello les sections suivantes de cet article supposent que vous avez défini hello `AZURE_STORAGE_ACCOUNT` et `AZURE_STORAGE_ACCESS_KEY` variables d’environnement.</span><span class="sxs-lookup"><span data-stu-id="11a4d-170">All examples in hello following sections of this article assume that you've set hello `AZURE_STORAGE_ACCOUNT` and `AZURE_STORAGE_ACCESS_KEY` environment variables.</span></span>
>

## <a name="create-and-manage-blobs"></a><span data-ttu-id="11a4d-171">Créer et gérer des objets blob</span><span class="sxs-lookup"><span data-stu-id="11a4d-171">Create and manage blobs</span></span>
<span data-ttu-id="11a4d-172">Stockage d’objets Blob Azure est un service pour stocker de grandes quantités de données non structurées, telles que les données texte ou binaire, qui sont accessibles à partir de n’importe où dans le monde hello via HTTP ou HTTPS.</span><span class="sxs-lookup"><span data-stu-id="11a4d-172">Azure Blob storage is a service for storing large amounts of unstructured data, such as text or binary data, that can be accessed from anywhere in hello world via HTTP or HTTPS.</span></span> <span data-ttu-id="11a4d-173">Cette section suppose que vous êtes déjà familiarisé avec les concepts du Stockage Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="11a4d-173">This section assumes that you are already familiar with Azure Blob storage concepts.</span></span> <span data-ttu-id="11a4d-174">Pour obtenir des informations détaillées, consultez [Prise en main du Stockage Blob Azure à l’aide de .NET](storage-dotnet-how-to-use-blobs.md) et [Concepts de service Blob](/rest/api/storageservices/blob-service-concepts).</span><span class="sxs-lookup"><span data-stu-id="11a4d-174">For detailed information, see [Get started with Azure Blob storage using .NET](storage-dotnet-how-to-use-blobs.md) and [Blob Service Concepts](/rest/api/storageservices/blob-service-concepts).</span></span>

### <a name="create-a-container"></a><span data-ttu-id="11a4d-175">Créer un conteneur</span><span class="sxs-lookup"><span data-stu-id="11a4d-175">Create a container</span></span>
<span data-ttu-id="11a4d-176">Chaque objet blob du stockage Azure doit se trouver dans un conteneur.</span><span class="sxs-lookup"><span data-stu-id="11a4d-176">Every blob in Azure storage must be in a container.</span></span> <span data-ttu-id="11a4d-177">Vous pouvez créer un conteneur à l’aide de hello `az storage container create` commande :</span><span class="sxs-lookup"><span data-stu-id="11a4d-177">You can create a container by using hello `az storage container create` command:</span></span>

```azurecli
az storage container create --name <container_name>
```

<span data-ttu-id="11a4d-178">Vous pouvez définir un des trois niveaux d’accès en lecture pour un conteneur en spécifiant hello facultatif `--public-access` argument :</span><span class="sxs-lookup"><span data-stu-id="11a4d-178">You can set one of three levels of read access for a new container by specifying hello optional  `--public-access` argument:</span></span>

* <span data-ttu-id="11a4d-179">`off`(par défaut) : les données de conteneur soient privé toohello propriétaire du compte.</span><span class="sxs-lookup"><span data-stu-id="11a4d-179">`off` (default): Container data is private toohello account owner.</span></span>
* <span data-ttu-id="11a4d-180">`blob` : accès en lecture public pour les objets blob.</span><span class="sxs-lookup"><span data-stu-id="11a4d-180">`blob`: Public read access for blobs.</span></span>
* <span data-ttu-id="11a4d-181">`container`: Lecture et liste accès toohello ensemble conteneur public.</span><span class="sxs-lookup"><span data-stu-id="11a4d-181">`container`: Public read and list access toohello entire container.</span></span>

<span data-ttu-id="11a4d-182">Pour plus d’informations, consultez [gérer l’accès en lecture anonyme toocontainers et les objets BLOB](storage-manage-access-to-resources.md).</span><span class="sxs-lookup"><span data-stu-id="11a4d-182">For more information, see [Manage anonymous read access toocontainers and blobs](storage-manage-access-to-resources.md).</span></span>

### <a name="upload-a-blob-tooa-container"></a><span data-ttu-id="11a4d-183">Télécharger un conteneur d’objets blob tooa</span><span class="sxs-lookup"><span data-stu-id="11a4d-183">Upload a blob tooa container</span></span>
<span data-ttu-id="11a4d-184">Le Stockage Blob Azure prend en charge les objets blob de blocs, d’ajout et de page.</span><span class="sxs-lookup"><span data-stu-id="11a4d-184">Azure Blob storage supports block, append, and page blobs.</span></span> <span data-ttu-id="11a4d-185">Téléchargement d’objets BLOB tooa conteneur à l’aide de hello `blob upload` commande :</span><span class="sxs-lookup"><span data-stu-id="11a4d-185">Upload blobs tooa container by using hello `blob upload` command:</span></span>

```azurecli
az storage blob upload \
    --file <local_file_path> \
    --container-name <container_name> \
    --name <blob_name>
```

 <span data-ttu-id="11a4d-186">Par défaut, hello `blob upload` commande télécharge les objets BLOB de toopage *.vhd fichiers ou des objets BLOB de blocs dans le cas contraire.</span><span class="sxs-lookup"><span data-stu-id="11a4d-186">By default, hello `blob upload` command uploads *.vhd files toopage blobs, or block blobs otherwise.</span></span> <span data-ttu-id="11a4d-187">toospecify un autre type lorsque vous téléchargez un objet blob, vous pouvez utiliser hello `--type` argument--les valeurs autorisée sont `append`, `block`, et `page`.</span><span class="sxs-lookup"><span data-stu-id="11a4d-187">toospecify another type when you upload a blob, you can use hello `--type` argument--allowed values are `append`, `block`, and `page`.</span></span>

 <span data-ttu-id="11a4d-188">Pour plus d’informations sur les types d’objets blob différents hello, consultez [objets BLOB de blocs, ajouter des objets BLOB et objets BLOB de pages](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs).</span><span class="sxs-lookup"><span data-stu-id="11a4d-188">For more information on hello different blob types, see [Understanding Block Blobs, Append Blobs, and Page Blobs](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs).</span></span>


### <a name="download-a-blob-from-a-container"></a><span data-ttu-id="11a4d-189">Télécharger un objet blob depuis un conteneur</span><span class="sxs-lookup"><span data-stu-id="11a4d-189">Download a blob from a container</span></span>
<span data-ttu-id="11a4d-190">Cet exemple montre comment un objet blob à partir d’un conteneur de toodownload :</span><span class="sxs-lookup"><span data-stu-id="11a4d-190">This example demonstrates how toodownload a blob from a container:</span></span>

```azurecli
az storage blob download \
    --container-name mycontainer \
    --name myblob.png \
    --file ~/mydownloadedblob.png
```

### <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="11a4d-191">Répertorier les objets BLOB hello dans un conteneur</span><span class="sxs-lookup"><span data-stu-id="11a4d-191">List hello blobs in a container</span></span>

<span data-ttu-id="11a4d-192">Répertorier les objets BLOB de hello dans un conteneur avec hello [liste objet blob de stockage az](/cli/azure/storage/blob#list) commande.</span><span class="sxs-lookup"><span data-stu-id="11a4d-192">List hello blobs in a container with hello [az storage blob list](/cli/azure/storage/blob#list) command.</span></span>

```azurecli
az storage blob list \
    --container-name mycontainer \
    --output table
```

### <a name="copy-blobs"></a><span data-ttu-id="11a4d-193">Copier des objets blob</span><span class="sxs-lookup"><span data-stu-id="11a4d-193">Copy blobs</span></span>
<span data-ttu-id="11a4d-194">Vous pouvez copier des objets blob au sein d’un compte de stockage, ou vers des comptes de stockage et des régions et ce, de façon asynchrone.</span><span class="sxs-lookup"><span data-stu-id="11a4d-194">You can copy blobs within or across storage accounts and regions asynchronously.</span></span>

<span data-ttu-id="11a4d-195">Hello exemple suivant montre comment le BLOB toocopy à partir du stockage d’un compte tooanother.</span><span class="sxs-lookup"><span data-stu-id="11a4d-195">hello following example demonstrates how toocopy blobs from one storage account tooanother.</span></span> <span data-ttu-id="11a4d-196">Nous créons d’abord un conteneur dans le compte de stockage source hello, spécifiant l’accès en lecture public pour ses objets BLOB.</span><span class="sxs-lookup"><span data-stu-id="11a4d-196">We first create a container in hello source storage account, specifying public read-access for its blobs.</span></span> <span data-ttu-id="11a4d-197">Ensuite, nous télécharger un conteneur de fichier toohello et pour finir, copie d’objets blob hello conteneur dans un conteneur dans le compte de stockage de destination hello.</span><span class="sxs-lookup"><span data-stu-id="11a4d-197">Next, we upload a file toohello container, and finally, copy hello blob from that container into a container in hello destination storage account.</span></span>

```azurecli
# Create container in source account
az storage container create \
    --account-name sourceaccountname \
    --account-key sourceaccountkey \
    --name sourcecontainer \
    --public-access blob

# Upload blob toocontainer in source account
az storage blob upload \
    --account-name sourceaccountname \
    --account-key sourceaccountkey \
    --container-name sourcecontainer \
    --file ~/Pictures/sourcefile.png \
    --name sourcefile.png

# Copy blob from source account toodestination account (destcontainer must exist)
az storage blob copy start \
    --account-name destaccountname \
    --account-key destaccountkey \
    --destination-blob destfile.png \
    --destination-container destcontainer \
    --source-uri https://sourceaccountname.blob.core.windows.net/sourcecontainer/sourcefile.png
```

<span data-ttu-id="11a4d-198">Bonjour exemple ci-dessus, le conteneur de destination hello doit déjà exister dans le compte de stockage de destination hello pour hello copie opération toosucceed.</span><span class="sxs-lookup"><span data-stu-id="11a4d-198">In hello above example, hello destination container must already exist in hello destination storage account for hello copy operation toosucceed.</span></span> <span data-ttu-id="11a4d-199">En outre, hello objet blob source spécifié dans hello `--source-uri` argument doit inclure un jeton de signature (SAP) d’accès partagé, ou être accessible publiquement, comme dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="11a4d-199">Additionally, hello source blob specified in hello `--source-uri` argument must either include a shared access signature (SAS) token, or be publicly accessible, as in this example.</span></span>

### <a name="delete-a-blob"></a><span data-ttu-id="11a4d-200">Supprimer un objet blob</span><span class="sxs-lookup"><span data-stu-id="11a4d-200">Delete a blob</span></span>
<span data-ttu-id="11a4d-201">toodelete un objet blob, utilisez hello `blob delete` commande :</span><span class="sxs-lookup"><span data-stu-id="11a4d-201">toodelete a blob, use hello `blob delete` command:</span></span>

```azurecli
az storage blob delete --container-name <container_name> --name <blob_name>
```

## <a name="create-and-manage-file-shares"></a><span data-ttu-id="11a4d-202">Créer et gérer des partages de fichiers</span><span class="sxs-lookup"><span data-stu-id="11a4d-202">Create and manage file shares</span></span>
<span data-ttu-id="11a4d-203">Stockage de fichiers Azure offre un stockage partagé pour les applications à l’aide du protocole Server Message Block (SMB) de hello.</span><span class="sxs-lookup"><span data-stu-id="11a4d-203">Azure File storage offers shared storage for applications using hello Server Message Block (SMB) protocol.</span></span> <span data-ttu-id="11a4d-204">Les services cloud et les machines virtuelles Microsoft Azure, ainsi que les applications locales, peuvent partager des données de fichiers via des partages montés.</span><span class="sxs-lookup"><span data-stu-id="11a4d-204">Microsoft Azure virtual machines and cloud services, as well as on-premises applications, can share file data via mounted shares.</span></span> <span data-ttu-id="11a4d-205">Vous pouvez gérer les partages de fichiers et les données de fichier via hello CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="11a4d-205">You can manage file shares and file data via hello Azure CLI.</span></span> <span data-ttu-id="11a4d-206">Pour plus d’informations sur le stockage de fichiers Azure, consultez [prise en main avec un stockage de fichier Azure sur Windows](storage-dotnet-how-to-use-files.md) ou [comment toouse stockage Azure files avec Linux](storage-how-to-use-files-linux.md).</span><span class="sxs-lookup"><span data-stu-id="11a4d-206">For more information on Azure File storage, see [Get started with Azure File storage on Windows](storage-dotnet-how-to-use-files.md) or [How toouse Azure File storage with Linux](storage-how-to-use-files-linux.md).</span></span>

### <a name="create-a-file-share"></a><span data-ttu-id="11a4d-207">Créer un partage de fichiers</span><span class="sxs-lookup"><span data-stu-id="11a4d-207">Create a file share</span></span>
<span data-ttu-id="11a4d-208">Un partage de fichiers Azure est un partage de fichiers SMB dans Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="11a4d-208">An Azure File share is an SMB file share in Azure.</span></span> <span data-ttu-id="11a4d-209">Tous les répertoires et fichiers doivent être créés dans un partage de fichiers.</span><span class="sxs-lookup"><span data-stu-id="11a4d-209">All directories and files must be created in a file share.</span></span> <span data-ttu-id="11a4d-210">Un compte peut contenir un nombre illimité de partages, et un partage peut stocker un nombre illimité de fichiers, les limites de capacité toohello hello du compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="11a4d-210">An account can contain an unlimited number of shares, and a share can store an unlimited number of files, up toohello capacity limits of hello storage account.</span></span> <span data-ttu-id="11a4d-211">Hello exemple suivant crée un partage de fichiers nommé **monsiteweb**.</span><span class="sxs-lookup"><span data-stu-id="11a4d-211">hello following example creates a file share named **myshare**.</span></span>

```azurecli
az storage share create --name myshare
```

### <a name="create-a-directory"></a><span data-ttu-id="11a4d-212">Créer un répertoire</span><span class="sxs-lookup"><span data-stu-id="11a4d-212">Create a directory</span></span>
<span data-ttu-id="11a4d-213">Un répertoire fournit une structure hiérarchique dans un partage de fichiers Azure.</span><span class="sxs-lookup"><span data-stu-id="11a4d-213">A directory provides a hierarchical structure in an Azure file share.</span></span> <span data-ttu-id="11a4d-214">Hello exemple suivant crée un répertoire nommé **myDir** dans le partage de fichiers hello.</span><span class="sxs-lookup"><span data-stu-id="11a4d-214">hello following example creates a directory named **myDir** in hello file share.</span></span>

```azurecli
az storage directory create --name myDir --share-name myshare
```

<span data-ttu-id="11a4d-215">Un chemin d’accès peut inclure plusieurs niveaux, par exemple **dir1/dir2**.</span><span class="sxs-lookup"><span data-stu-id="11a4d-215">A directory path can include multiple levels, for example **dir1/dir2**.</span></span> <span data-ttu-id="11a4d-216">Toutefois, avant de créer un sous-répertoire, vous devez vous assurer que tous les répertoires parents existent.</span><span class="sxs-lookup"><span data-stu-id="11a4d-216">However, you must ensure that all parent directories exist before creating a subdirectory.</span></span> <span data-ttu-id="11a4d-217">Par exemple, pour le chemin d’accès **dir1/dir2**, vous devez créer le répertoire **dir1**, puis le répertoire **dir2**.</span><span class="sxs-lookup"><span data-stu-id="11a4d-217">For example, for path **dir1/dir2**, you must first create directory **dir1**, then create directory **dir2**.</span></span>

### <a name="upload-a-local-file-tooa-share"></a><span data-ttu-id="11a4d-218">Télécharger un partage de fichiers local de tooa</span><span class="sxs-lookup"><span data-stu-id="11a4d-218">Upload a local file tooa share</span></span>
<span data-ttu-id="11a4d-219">exemple Hello télécharge un fichier à partir de **~/temp/samplefile.txt** tooroot Hello **monsiteweb** partage de fichiers.</span><span class="sxs-lookup"><span data-stu-id="11a4d-219">hello following example uploads a file from **~/temp/samplefile.txt** tooroot of hello **myshare** file share.</span></span> <span data-ttu-id="11a4d-220">Hello `--source` argument spécifie tooupload de fichier local existant hello.</span><span class="sxs-lookup"><span data-stu-id="11a4d-220">hello `--source` argument specifies hello existing local file tooupload.</span></span>

```azurecli
az storage file upload --share-name myshare --source ~/temp/samplefile.txt
```

<span data-ttu-id="11a4d-221">Comme avec la création du répertoire, vous pouvez spécifier un chemin d’accès de répertoire dans hello partage tooupload hello fichier tooan répertoire existant au sein de la part d’hello :</span><span class="sxs-lookup"><span data-stu-id="11a4d-221">As with directory creation, you can specify a directory path within hello share tooupload hello file tooan existing directory within hello share:</span></span>

```azurecli
az storage file upload --share-name myshare/myDir --source ~/temp/samplefile.txt
```

<span data-ttu-id="11a4d-222">Un fichier dans le partage de hello peut être jusqu'à to too1 taille.</span><span class="sxs-lookup"><span data-stu-id="11a4d-222">A file in hello share can be up too1 TB in size.</span></span>

### <a name="list-hello-files-in-a-share"></a><span data-ttu-id="11a4d-223">Liste des fichiers dans un partage de hello</span><span class="sxs-lookup"><span data-stu-id="11a4d-223">List hello files in a share</span></span>
<span data-ttu-id="11a4d-224">Vous pouvez répertorier des fichiers et des répertoires dans un partage à l’aide de hello `az storage file list` commande :</span><span class="sxs-lookup"><span data-stu-id="11a4d-224">You can list files and directories in a share by using hello `az storage file list` command:</span></span>

```azurecli
# List hello files in hello root of a share
az storage file list --share-name myshare --output table

# List hello files in a directory within a share
az storage file list --share-name myshare/myDir --output table

# List hello files in a path within a share
az storage file list --share-name myshare --path myDir/mySubDir/MySubDir2 --output table
```

### <a name="copy-files"></a><span data-ttu-id="11a4d-225">Copie des fichiers</span><span class="sxs-lookup"><span data-stu-id="11a4d-225">Copy files</span></span>      
<span data-ttu-id="11a4d-226">Vous pouvez copier un fichier de tooanother, un objet blob tooa de fichier ou un objet blob tooa fichier.</span><span class="sxs-lookup"><span data-stu-id="11a4d-226">You can copy a file tooanother file, a file tooa blob, or a blob tooa file.</span></span> <span data-ttu-id="11a4d-227">Par exemple, toocopy un répertoire tooa de fichiers dans un partage différent :</span><span class="sxs-lookup"><span data-stu-id="11a4d-227">For example, toocopy a file tooa directory in a different share:</span></span>        
        
```azurecli
az storage file copy start \
--source-share share1 --source-path dir1/file.txt \
--destination-share share2 --destination-path dir2/file.txt     
```

## <a name="next-steps"></a><span data-ttu-id="11a4d-228">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="11a4d-228">Next steps</span></span>
<span data-ttu-id="11a4d-229">Voici quelques ressources supplémentaires pour en savoir plus sur l’utilisation de hello Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="11a4d-229">Here are some additional resources for learning more about working with hello Azure CLI 2.0.</span></span>

* [<span data-ttu-id="11a4d-230">Prise en main d’Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="11a4d-230">Get started with Azure CLI 2.0</span></span>](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)
* [<span data-ttu-id="11a4d-231">Référence des commandes Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="11a4d-231">Azure CLI 2.0 command reference</span></span>](/cli/azure)
* [<span data-ttu-id="11a4d-232">Azure CLI 2.0 sur GitHub</span><span class="sxs-lookup"><span data-stu-id="11a4d-232">Azure CLI 2.0 on GitHub</span></span>](https://github.com/Azure/azure-cli)
