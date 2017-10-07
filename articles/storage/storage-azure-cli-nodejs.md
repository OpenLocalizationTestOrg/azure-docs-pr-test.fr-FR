---
title: aaaUsing hello Azure CLI 1.0 avec le stockage Azure | Documents Microsoft
description: "Découvrez comment toouse hello Azure Interface de ligne (Azure) 1.0 avec toocreate de stockage Azure et gérer des comptes de stockage et de travail avec les fichiers et les objets BLOB Windows Azure. Hello CLI d’Azure est un outil inter-plateformes"
services: storage
documentationcenter: na
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: b502232a-e8f6-4d6c-befd-3476592e0e35
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/30/2017
ms.author: seguler
ms.openlocfilehash: 786f2be64875f5094f09fd6e4a47532889c3a82f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-cli-10-with-azure-storage"></a><span data-ttu-id="29c8c-104">À l’aide de hello Azure CLI 1.0 avec le stockage Azure</span><span class="sxs-lookup"><span data-stu-id="29c8c-104">Using hello Azure CLI 1.0 with Azure Storage</span></span>

## <a name="overview"></a><span data-ttu-id="29c8c-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="29c8c-105">Overview</span></span>

<span data-ttu-id="29c8c-106">Hello CLI d’Azure fournit un ensemble d’open source d’inter-plateformes commandes sur l’utilisation de hello plateforme Azure.</span><span class="sxs-lookup"><span data-stu-id="29c8c-106">hello Azure CLI provides a set of open source, cross-platform commands for working with hello Azure Platform.</span></span> <span data-ttu-id="29c8c-107">Il fournit la majeure partie de hello même fonctionnalité trouvée dans hello [portail Azure](https://portal.azure.com) données riches ainsi accéder aux fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="29c8c-107">It provides much of hello same functionality found in hello [Azure portal](https://portal.azure.com) as well as rich data access functionality.</span></span>

<span data-ttu-id="29c8c-108">Dans ce guide, nous allons examiner comment toouse [Azure Interface de ligne (Azure)](../cli-install-nodejs.md) tooperform diverses tâches de développement et d’administration avec le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="29c8c-108">In this guide, we'll explore how toouse [Azure Command-Line Interface (Azure CLI)](../cli-install-nodejs.md) tooperform a variety of development and administration tasks with Azure Storage.</span></span> <span data-ttu-id="29c8c-109">Nous vous recommandons de télécharger et installer ou mettre à niveau toohello dernière CLI d’Azure avant d’utiliser ce guide.</span><span class="sxs-lookup"><span data-stu-id="29c8c-109">We recommend that you download and install or upgrade toohello latest Azure CLI before using this guide.</span></span>

<span data-ttu-id="29c8c-110">Ce guide suppose que vous comprenez les concepts de base hello du stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="29c8c-110">This guide assumes that you understand hello basic concepts of Azure Storage.</span></span> <span data-ttu-id="29c8c-111">Hello Guide d’un nombre de scripts d’utilisation de hello toodemonstrate Hello CLI d’Azure avec le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="29c8c-111">hello guide provides a number of scripts toodemonstrate hello usage of hello Azure CLI with Azure Storage.</span></span> <span data-ttu-id="29c8c-112">Être tooupdate que les variables de script hello en fonction de votre configuration avant d’exécuter chaque script.</span><span class="sxs-lookup"><span data-stu-id="29c8c-112">Be sure tooupdate hello script variables based on your configuration before running each script.</span></span>

> [!NOTE]
> <span data-ttu-id="29c8c-113">guide de Hello fournit des exemples de script et commande de CLI d’Azure hello pour les comptes de stockage classiques.</span><span class="sxs-lookup"><span data-stu-id="29c8c-113">hello guide provides hello Azure CLI command and script examples for classic storage accounts.</span></span> <span data-ttu-id="29c8c-114">Consultez [Using hello CLI d’Azure pour Mac, Linux et Windows avec la gestion des ressources Azure](../virtual-machines/azure-cli-arm-commands.md#azure-storage-commands-to-manage-your-storage-objects) pour les commandes CLI d’Azure pour les comptes de stockage de gestionnaire de ressources.</span><span class="sxs-lookup"><span data-stu-id="29c8c-114">See [Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Management](../virtual-machines/azure-cli-arm-commands.md#azure-storage-commands-to-manage-your-storage-objects) for Azure CLI commands for Resource Manager storage accounts.</span></span>
>
>

[!INCLUDE [storage-cli-versions](../../includes/storage-cli-versions.md)]

## <a name="get-started-with-azure-storage-and-hello-azure-cli-in-5-minutes"></a><span data-ttu-id="29c8c-115">Prise en main Azure Storage et hello CLI d’Azure dans 5 minutes</span><span class="sxs-lookup"><span data-stu-id="29c8c-115">Get started with Azure Storage and hello Azure CLI in 5 minutes</span></span>
<span data-ttu-id="29c8c-116">Ce guide inclut des exemples basés sur Ubuntu, mais les résultats devraient être les mêmes sur d’autres plates-formes.</span><span class="sxs-lookup"><span data-stu-id="29c8c-116">This guide uses Ubuntu for examples, but other OS platforms should perform similarly.</span></span>

<span data-ttu-id="29c8c-117">**Nouvelle tooAzure :** obtenir un abonnement Microsoft Azure et un compte Microsoft associé à cet abonnement.</span><span class="sxs-lookup"><span data-stu-id="29c8c-117">**New tooAzure:** Get a Microsoft Azure subscription and a Microsoft account associated with that subscription.</span></span> <span data-ttu-id="29c8c-118">Pour en savoir plus sur les options d’achat de Microsoft Azure, voir [Essai gratuit](https://azure.microsoft.com/pricing/free-trial/), [Options d’achat](https://azure.microsoft.com/pricing/purchase-options/) et [Offres spéciales membres](https://azure.microsoft.com/pricing/member-offers/) (pour les membres de MSDN, Microsoft Partner Network et BizSpark, ainsi que d’autres programmes Microsoft).</span><span class="sxs-lookup"><span data-stu-id="29c8c-118">For information on Azure purchase options, see [Free Trial](https://azure.microsoft.com/pricing/free-trial/), [Purchase Options](https://azure.microsoft.com/pricing/purchase-options/), and [Member Offers](https://azure.microsoft.com/pricing/member-offers/) (for members of MSDN, Microsoft Partner Network, and BizSpark, and other Microsoft programs).</span></span>

<span data-ttu-id="29c8c-119">Pour plus d’informations sur les abonnements Azure, consultez la section [Attribution de rôles d’administrateur dans Azure Active Directory (Azure AD)](https://msdn.microsoft.com/library/azure/hh531793.aspx) .</span><span class="sxs-lookup"><span data-stu-id="29c8c-119">See [Assigning administrator roles in Azure Active Directory (Azure AD)](https://msdn.microsoft.com/library/azure/hh531793.aspx) for more information about Azure subscriptions.</span></span>

<span data-ttu-id="29c8c-120">**Une fois le compte et l’abonnement à Microsoft Azure créés :**</span><span class="sxs-lookup"><span data-stu-id="29c8c-120">**After creating a Microsoft Azure subscription and account:**</span></span>

1. <span data-ttu-id="29c8c-121">Téléchargez et installez hello CLI d’Azure suivant les instructions hello décrites dans [installation Bonjour Azure CLI](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="29c8c-121">Download and install hello Azure CLI following hello instructions outlined in [Install hello Azure CLI](../cli-install-nodejs.md).</span></span>
2. <span data-ttu-id="29c8c-122">Une fois hello CLI d’Azure a été installé, vous serez en mesure de toouse hello de commande azure à partir de vos commandes de l’interface de ligne de commande (interpréteur de commandes, Terminal Server, invite de commandes) tooaccess hello CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="29c8c-122">Once hello Azure CLI has been installed, you will be able toouse hello azure command from your command-line interface (Bash, Terminal, Command prompt) tooaccess hello Azure CLI commands.</span></span> <span data-ttu-id="29c8c-123">Hello de type _azure_ commande et vous devez voir hello suivant de sortie.</span><span class="sxs-lookup"><span data-stu-id="29c8c-123">Type hello _azure_ command and you should see hello following output.</span></span>

    ![Sorte de commande Microsoft Azure][Image1]
3. <span data-ttu-id="29c8c-125">Dans l’interface de ligne de commande hello, tapez `azure storage` toolist toutes hello les commandes de stockage azure et obtenir une première impression de hello de fonctionnalités hello CLI d’Azure fournit.</span><span class="sxs-lookup"><span data-stu-id="29c8c-125">In hello command-line interface, type `azure storage` toolist out all hello azure storage commands and get a first impression of hello functionalities hello Azure CLI provides.</span></span> <span data-ttu-id="29c8c-126">Vous pouvez taper le nom de la commande avec **-h** paramètre (par exemple, `azure storage share create -h`) toosee les détails de la syntaxe de commande.</span><span class="sxs-lookup"><span data-stu-id="29c8c-126">You can type command name with **-h** parameter (for example, `azure storage share create -h`) toosee details of command syntax.</span></span>
4. <span data-ttu-id="29c8c-127">Maintenant, nous donnons un script simple qui montre la base tooaccess de commandes CLI d’Azure stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="29c8c-127">Now, we'll give you a simple script that shows basic Azure CLI commands tooaccess Azure Storage.</span></span> <span data-ttu-id="29c8c-128">script de Hello tout d’abord vous demandera tooset deux variables de votre compte de stockage et la clé.</span><span class="sxs-lookup"><span data-stu-id="29c8c-128">hello script will first ask you tooset two variables for your storage account and key.</span></span> <span data-ttu-id="29c8c-129">Ensuite, hello script créer un conteneur dans ce nouveau compte de stockage et télécharger un conteneur de toothat (blob) de fichier image existant.</span><span class="sxs-lookup"><span data-stu-id="29c8c-129">Then, hello script will create a new container in this new storage account and upload an existing image file (blob) toothat container.</span></span> <span data-ttu-id="29c8c-130">Une fois le script de hello répertorie tous les objets BLOB dans le conteneur, elle télécharge hello toohello destination répertoire des fichiers image qui existe sur l’ordinateur local de hello.</span><span class="sxs-lookup"><span data-stu-id="29c8c-130">After hello script lists all blobs in that container, it will download hello image file toohello destination directory which exists on hello local computer.</span></span>

    ```azurecli
    #!/bin/bash
    # A simple Azure storage example

    export AZURE_STORAGE_ACCOUNT=<storage_account_name>
    export AZURE_STORAGE_ACCESS_KEY=<storage_account_key>

    export container_name=<container_name>
    export blob_name=<blob_name>
    export image_to_upload=<image_to_upload>
    export destination_folder=<destination_folder>

    echo "Creating hello container..."
    azure storage container create $container_name

    echo "Uploading hello image..."
    azure storage blob upload $image_to_upload $container_name $blob_name

    echo "Listing hello blobs..."
    azure storage blob list $container_name

    echo "Downloading hello image..."
    azure storage blob download $container_name $blob_name $destination_folder

    echo "Done"
    ```

5. <span data-ttu-id="29c8c-131">Sur ce dernier, ouvrez l’éditeur de texte de votre choix (vim, par exemple).</span><span class="sxs-lookup"><span data-stu-id="29c8c-131">In your local computer, open your preferred text editor (vim for example).</span></span> <span data-ttu-id="29c8c-132">Tapez hello au-dessus de script dans votre éditeur de texte.</span><span class="sxs-lookup"><span data-stu-id="29c8c-132">Type hello above script into your text editor.</span></span>
6. <span data-ttu-id="29c8c-133">Maintenant, vous devez les variables de script tooupdate hello en fonction de vos paramètres de configuration.</span><span class="sxs-lookup"><span data-stu-id="29c8c-133">Now, you need tooupdate hello script variables based on your configuration settings.</span></span>

   * <span data-ttu-id="29c8c-134">**< Storage_account_name >** utiliser hello attribué dans le script de hello ou entrez un nouveau nom pour votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="29c8c-134">**<storage_account_name>** Use hello given name in hello script or enter a new name for your storage account.</span></span> <span data-ttu-id="29c8c-135">**Important :** nom hello hello du compte de stockage doit être unique dans Azure.</span><span class="sxs-lookup"><span data-stu-id="29c8c-135">**Important:** hello name of hello storage account must be unique in Azure.</span></span> <span data-ttu-id="29c8c-136">Il doit également inclure des minuscules uniquement.</span><span class="sxs-lookup"><span data-stu-id="29c8c-136">It must be lowercase, too!</span></span>
   * <span data-ttu-id="29c8c-137">**< storage_account_key >** clé d’accès hello de votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="29c8c-137">**<storage_account_key>** hello access key of your storage account.</span></span>
   * <span data-ttu-id="29c8c-138">**< Nom_conteneur >** utiliser hello attribué dans le script de hello ou entrez un nouveau nom pour votre conteneur.</span><span class="sxs-lookup"><span data-stu-id="29c8c-138">**<container_name>** Use hello given name in hello script or enter a new name for your container.</span></span>
   * <span data-ttu-id="29c8c-139">**< Image_to_upload >** saisir une image de tooa de chemin d’accès sur votre ordinateur local, tel que : « ~ / images/HelloWorld.png ».</span><span class="sxs-lookup"><span data-stu-id="29c8c-139">**<image_to_upload>** Enter a path tooa picture on your local computer, such as: "~/images/HelloWorld.png".</span></span>
   * <span data-ttu-id="29c8c-140">**< Destination_folder >** Entrez un chemin d’accès tooa répertoire local toostore les fichiers téléchargés depuis le stockage Azure, telles que : « ~/downloadImages ».</span><span class="sxs-lookup"><span data-stu-id="29c8c-140">**<destination_folder>** Enter a path tooa local directory toostore files downloaded from Azure Storage, such as: "~/downloadImages".</span></span>
7. <span data-ttu-id="29c8c-141">Une fois que vous avez mis à jour les variables nécessaires hello vim, appuyez sur les combinaisons de touches `ESC`, `:`, `wq!` script de hello toosave.</span><span class="sxs-lookup"><span data-stu-id="29c8c-141">After you've updated hello necessary variables in vim, press key combinations `ESC`, `:`, `wq!` toosave hello script.</span></span>
8. <span data-ttu-id="29c8c-142">toorun ce script, simplement type hello script nom de fichier dans la console hello bash.</span><span class="sxs-lookup"><span data-stu-id="29c8c-142">toorun this script, simply type hello script file name in hello bash console.</span></span> <span data-ttu-id="29c8c-143">Une fois que ce script s’exécute, vous devez disposer d’un dossier local de destination qui inclut le fichier d’image hello téléchargé.</span><span class="sxs-lookup"><span data-stu-id="29c8c-143">After this script runs, you should have a local destination folder that includes hello downloaded image file.</span></span> <span data-ttu-id="29c8c-144">Hello suivant capture d’écran montre un exemple de sortie :</span><span class="sxs-lookup"><span data-stu-id="29c8c-144">hello following screenshot shows an example output:</span></span>

<span data-ttu-id="29c8c-145">Après l’exécution du script de hello, vous devez disposer d’un dossier local de destination qui inclut le fichier d’image hello téléchargé.</span><span class="sxs-lookup"><span data-stu-id="29c8c-145">After hello script runs, you should have a local destination folder that includes hello downloaded image file.</span></span>

## <a name="manage-storage-accounts-with-hello-azure-cli"></a><span data-ttu-id="29c8c-146">Gérer les comptes de stockage avec hello CLI d’Azure</span><span class="sxs-lookup"><span data-stu-id="29c8c-146">Manage storage accounts with hello Azure CLI</span></span>
### <a name="connect-tooyour-azure-subscription"></a><span data-ttu-id="29c8c-147">Se connecter tooyour abonnement Azure</span><span class="sxs-lookup"><span data-stu-id="29c8c-147">Connect tooyour Azure subscription</span></span>
<span data-ttu-id="29c8c-148">La plupart des commandes de stockage hello fonctionnera sans un abonnement Azure, nous vous recommandons tooconnect tooyour abonnement hello CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="29c8c-148">While most of hello storage commands will work without an Azure subscription, we recommend you tooconnect tooyour subscription from hello Azure CLI.</span></span> <span data-ttu-id="29c8c-149">tooconfigure hello CLI d’Azure toowork avec votre abonnement, suivez les étapes de hello dans [connecter tooan abonnement Azure à partir de hello CLI d’Azure](../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="29c8c-149">tooconfigure hello Azure CLI toowork with your subscription, follow hello steps in [Connect tooan Azure subscription from hello Azure CLI](../xplat-cli-connect.md).</span></span>

### <a name="create-a-new-storage-account"></a><span data-ttu-id="29c8c-150">Création d’un nouveau compte de stockage</span><span class="sxs-lookup"><span data-stu-id="29c8c-150">Create a new storage account</span></span>
<span data-ttu-id="29c8c-151">Vous devrez toouse le stockage Azure, un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="29c8c-151">toouse Azure storage, you will need a storage account.</span></span> <span data-ttu-id="29c8c-152">Vous pouvez créer un nouveau compte de stockage Azure une fois que vous avez configuré votre abonnement de tooyour tooconnect ordinateur.</span><span class="sxs-lookup"><span data-stu-id="29c8c-152">You can create a new Azure storage account after you have configured your computer tooconnect tooyour subscription.</span></span>

```azurecli
azure storage account create <account_name>
```

<span data-ttu-id="29c8c-153">nom de Hello de votre compte de stockage doit être comprise entre 3 et 24 caractères et utiliser des nombres et des lettres minuscules.</span><span class="sxs-lookup"><span data-stu-id="29c8c-153">hello name of your storage account must be between 3 and 24 characters in length and use numbers and lower-case letters only.</span></span>

### <a name="set-a-default-azure-storage-account-in-environment-variables"></a><span data-ttu-id="29c8c-154">Définir un compte Azure Storage par défaut dans les variables d’environnement</span><span class="sxs-lookup"><span data-stu-id="29c8c-154">Set a default Azure storage account in environment variables</span></span>
<span data-ttu-id="29c8c-155">Vous pouvez disposer de plusieurs comptes de stockage dans votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="29c8c-155">You can have multiple storage accounts in your subscription.</span></span> <span data-ttu-id="29c8c-156">Vous pouvez choisir un d’eux et affectez-lui Bonjour variables d’environnement pour tout le stockage hello commandes Bonjour même session.</span><span class="sxs-lookup"><span data-stu-id="29c8c-156">You can choose one of them and set it in hello environment variables for all hello storage commands in hello same session.</span></span> <span data-ttu-id="29c8c-157">Cela vous permet de toorun hello CLI d’Azure stockage commandes sans spécifier le stockage de hello compte explicitement la clé.</span><span class="sxs-lookup"><span data-stu-id="29c8c-157">This enables you toorun hello Azure CLI storage commands without specifying hello storage account and key explicitly.</span></span>

```azurecli
export AZURE_STORAGE_ACCOUNT=<account_name>
export AZURE_STORAGE_ACCESS_KEY=<key>
```

<span data-ttu-id="29c8c-158">Une autre façon tooset un compte de stockage par défaut utilise la chaîne de connexion.</span><span class="sxs-lookup"><span data-stu-id="29c8c-158">Another way tooset a default storage account is using connection string.</span></span> <span data-ttu-id="29c8c-159">Tout d’abord obtenir la chaîne de connexion hello en commande :</span><span class="sxs-lookup"><span data-stu-id="29c8c-159">Firstly get hello connection string by command:</span></span>

```azurecli
azure storage account connectionstring show <account_name>
```

<span data-ttu-id="29c8c-160">Puis copiez la chaîne de connexion de sortie hello et la définir tooenvironment variable :</span><span class="sxs-lookup"><span data-stu-id="29c8c-160">Then copy hello output connection string and set it tooenvironment variable:</span></span>

```azurecli
export AZURE_STORAGE_CONNECTION_STRING=<connection_string>
```

## <a name="create-and-manage-blobs"></a><span data-ttu-id="29c8c-161">Créer et gérer des objets blob</span><span class="sxs-lookup"><span data-stu-id="29c8c-161">Create and manage blobs</span></span>
<span data-ttu-id="29c8c-162">Stockage d’objets Blob Azure est un service pour stocker de grandes quantités de données non structurées, telles que les données texte ou binaire, qui sont accessibles à partir de n’importe où dans le monde hello via HTTP ou HTTPS.</span><span class="sxs-lookup"><span data-stu-id="29c8c-162">Azure Blob storage is a service for storing large amounts of unstructured data, such as text or binary data, that can be accessed from anywhere in hello world via HTTP or HTTPS.</span></span> <span data-ttu-id="29c8c-163">Cette section part du principe que vous êtes déjà familiarisé avec les concepts de stockage d’objets Blob Azure hello.</span><span class="sxs-lookup"><span data-stu-id="29c8c-163">This section assumes that you are already familiar with hello Azure Blob storage concepts.</span></span> <span data-ttu-id="29c8c-164">Pour obtenir des informations détaillées, consultez [Prise en main du Stockage Blob Azure à l’aide de .NET](storage-dotnet-how-to-use-blobs.md) et [Concepts de service Blob](http://msdn.microsoft.com/library/azure/dd179376.aspx).</span><span class="sxs-lookup"><span data-stu-id="29c8c-164">For detailed information, see [Get started with Azure Blob storage using .NET](storage-dotnet-how-to-use-blobs.md) and [Blob Service Concepts](http://msdn.microsoft.com/library/azure/dd179376.aspx).</span></span>

### <a name="create-a-container"></a><span data-ttu-id="29c8c-165">Créer un conteneur</span><span class="sxs-lookup"><span data-stu-id="29c8c-165">Create a container</span></span>
<span data-ttu-id="29c8c-166">Chaque objet blob du stockage Azure doit se trouver dans un conteneur.</span><span class="sxs-lookup"><span data-stu-id="29c8c-166">Every blob in Azure storage must be in a container.</span></span> <span data-ttu-id="29c8c-167">Vous pouvez créer un conteneur privé à l’aide de hello `azure storage container create` commande :</span><span class="sxs-lookup"><span data-stu-id="29c8c-167">You can create a private container using hello `azure storage container create` command:</span></span>

```azurecli
azure storage container create mycontainer
```

> [!NOTE]
> <span data-ttu-id="29c8c-168">Il existe trois niveaux d’accès en lecture anonyme : **Désactivé**, **Blob** et **Conteneur**.</span><span class="sxs-lookup"><span data-stu-id="29c8c-168">There are three levels of anonymous read access: **Off**, **Blob**, and **Container**.</span></span> <span data-ttu-id="29c8c-169">tooprevent anonyme accéder à tooblobs, le paramètre d’autorisation ensemble hello**hors**.</span><span class="sxs-lookup"><span data-stu-id="29c8c-169">tooprevent anonymous access tooblobs, set hello Permission parameter too**Off**.</span></span> <span data-ttu-id="29c8c-170">Par défaut, hello nouveau conteneur est privé et sont accessibles uniquement par le propriétaire du compte hello.</span><span class="sxs-lookup"><span data-stu-id="29c8c-170">By default, hello new container is private and can be accessed only by hello account owner.</span></span> <span data-ttu-id="29c8c-171">public anonyme de tooallow lire tooblob d’accéder aux ressources, mais pas toocontainer métadonnées ou toohello liste d’objets BLOB dans le conteneur de hello, définissez le paramètre d’autorisation hello trop**Blob**.</span><span class="sxs-lookup"><span data-stu-id="29c8c-171">tooallow anonymous public read access tooblob resources, but not toocontainer metadata or toohello list of blobs in hello container, set hello Permission parameter too**Blob**.</span></span> <span data-ttu-id="29c8c-172">public complet de tooallow lire tooblob d’accéder aux ressources, les métadonnées de conteneur et hello liste d’objets BLOB dans le conteneur de hello, définissez le paramètre d’autorisation hello trop**conteneur**.</span><span class="sxs-lookup"><span data-stu-id="29c8c-172">tooallow full public read access tooblob resources, container metadata, and hello list of blobs in hello container, set hello Permission parameter too**Container**.</span></span> <span data-ttu-id="29c8c-173">Pour plus d’informations, consultez [gérer l’accès en lecture anonyme toocontainers et les objets BLOB](storage-manage-access-to-resources.md).</span><span class="sxs-lookup"><span data-stu-id="29c8c-173">For more information, see [Manage anonymous read access toocontainers and blobs](storage-manage-access-to-resources.md).</span></span>
>
>

### <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="29c8c-174">Charger un objet blob dans un conteneur</span><span class="sxs-lookup"><span data-stu-id="29c8c-174">Upload a blob into a container</span></span>
<span data-ttu-id="29c8c-175">Le service de stockage d’objets blob Azure prend en charge les objets blob de blocs et de page.</span><span class="sxs-lookup"><span data-stu-id="29c8c-175">Azure Blob Storage supports block blobs and page blobs.</span></span> <span data-ttu-id="29c8c-176">Pour plus d’informations, consultez [Présentation des objets blob de blocs, des objets blob d’ajout et des objets blob de pages](http://msdn.microsoft.com/library/azure/ee691964.aspx).</span><span class="sxs-lookup"><span data-stu-id="29c8c-176">For more information, see [Understanding Block Blobs, Append Blobs, and Page Blobs](http://msdn.microsoft.com/library/azure/ee691964.aspx).</span></span>

<span data-ttu-id="29c8c-177">tooupload objets BLOB dans tooa conteneur, vous pouvez utiliser hello `azure storage blob upload`.</span><span class="sxs-lookup"><span data-stu-id="29c8c-177">tooupload blobs in tooa container, you can use hello `azure storage blob upload`.</span></span> <span data-ttu-id="29c8c-178">Par défaut, cette commande télécharge le blob de blocs tooa hello fichiers locaux.</span><span class="sxs-lookup"><span data-stu-id="29c8c-178">By default, this command uploads hello local files tooa block blob.</span></span> <span data-ttu-id="29c8c-179">type de hello toospecify pour l’objet blob de hello, vous pouvez utiliser hello `--blobtype` paramètre.</span><span class="sxs-lookup"><span data-stu-id="29c8c-179">toospecify hello type for hello blob, you can use hello `--blobtype` parameter.</span></span>

```azurecli
azure storage blob upload '~/images/HelloWorld.png' mycontainer myBlockBlob
```

### <a name="download-blobs-from-a-container"></a><span data-ttu-id="29c8c-180">Télécharger des objets blob depuis un conteneur</span><span class="sxs-lookup"><span data-stu-id="29c8c-180">Download blobs from a container</span></span>
<span data-ttu-id="29c8c-181">Bonjour à l’exemple suivant montre comment toodownload les objets BLOB à partir d’un conteneur.</span><span class="sxs-lookup"><span data-stu-id="29c8c-181">hello following example demonstrates how toodownload blobs from a container.</span></span>

```azurecli
azure storage blob download mycontainer myBlockBlob '~/downloadImages/downloaded.png'
```

### <a name="copy-blobs"></a><span data-ttu-id="29c8c-182">Copier des objets blob</span><span class="sxs-lookup"><span data-stu-id="29c8c-182">Copy blobs</span></span>
<span data-ttu-id="29c8c-183">Vous pouvez copier des objets blob au sein d’un compte de stockage, ou vers des comptes de stockage et des régions et ce, de façon asynchrone.</span><span class="sxs-lookup"><span data-stu-id="29c8c-183">You can copy blobs within or across storage accounts and regions asynchronously.</span></span>

<span data-ttu-id="29c8c-184">Hello exemple suivant montre comment le BLOB toocopy à partir du stockage d’un compte tooanother.</span><span class="sxs-lookup"><span data-stu-id="29c8c-184">hello following example demonstrates how toocopy blobs from one storage account tooanother.</span></span> <span data-ttu-id="29c8c-185">Dans cet exemple, nous créons un conteneur incluant des objets blob accessibles de manière publique et anonyme.</span><span class="sxs-lookup"><span data-stu-id="29c8c-185">In this sample we create a container where blobs are publicly, anonymously accessible.</span></span>

```azurecli
azure storage container create mycontainer2 -a <accountName2> -k <accountKey2> -p Blob

azure storage blob upload '~/Images/HelloWorld.png' mycontainer2 myBlockBlob2 -a <accountName2> -k <accountKey2>

azure storage blob copy start 'https://<accountname2>.blob.core.windows.net/mycontainer2/myBlockBlob2' mycontainer
```

<span data-ttu-id="29c8c-186">Cet exemple repose sur une copie asynchrone.</span><span class="sxs-lookup"><span data-stu-id="29c8c-186">This sample performs an asynchronous copy.</span></span> <span data-ttu-id="29c8c-187">Vous pouvez surveiller l’état de hello de chaque opération de copie en exécutant hello `azure storage blob copy show` opération.</span><span class="sxs-lookup"><span data-stu-id="29c8c-187">You can monitor hello status of each copy operation by running hello `azure storage blob copy show` operation.</span></span>

<span data-ttu-id="29c8c-188">Notez que l’URL source du hello fourni pour l’opération de copie hello doit être accessible publiquement, ou inclure un jeton SAP (signature d’accès partagé).</span><span class="sxs-lookup"><span data-stu-id="29c8c-188">Note that hello source URL provided for hello copy operation must either be publicly accessible, or include a SAS (shared access signature) token.</span></span>

### <a name="delete-a-blob"></a><span data-ttu-id="29c8c-189">Supprimer un objet blob</span><span class="sxs-lookup"><span data-stu-id="29c8c-189">Delete a blob</span></span>
<span data-ttu-id="29c8c-190">toodelete un objet blob, utilisez hello commande ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="29c8c-190">toodelete a blob, use hello below command:</span></span>

```azurecli
azure storage blob delete mycontainer myBlockBlob2
```

## <a name="create-and-manage-file-shares"></a><span data-ttu-id="29c8c-191">Créer et gérer des partages de fichiers</span><span class="sxs-lookup"><span data-stu-id="29c8c-191">Create and manage file shares</span></span>
<span data-ttu-id="29c8c-192">Stockage de fichiers Azure offre un stockage partagé pour les applications à l’aide du protocole SMB standard de hello.</span><span class="sxs-lookup"><span data-stu-id="29c8c-192">Azure File storage offers shared storage for applications using hello standard SMB protocol.</span></span> <span data-ttu-id="29c8c-193">Les services cloud et les machines virtuelles Microsoft Azure, ainsi que les applications locales, peuvent partager des données de fichiers via des partages montés.</span><span class="sxs-lookup"><span data-stu-id="29c8c-193">Microsoft Azure virtual machines and cloud services, as well as on-premises applications, can share file data via mounted shares.</span></span> <span data-ttu-id="29c8c-194">Vous pouvez gérer les partages de fichiers et les données de fichier via hello CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="29c8c-194">You can manage file shares and file data via hello Azure CLI.</span></span> <span data-ttu-id="29c8c-195">Pour plus d’informations sur le stockage de fichiers Azure, consultez [prise en main avec un stockage de fichier Azure sur Windows](storage-dotnet-how-to-use-files.md) ou [comment toouse stockage Azure files avec Linux](storage-how-to-use-files-linux.md).</span><span class="sxs-lookup"><span data-stu-id="29c8c-195">For more information on Azure File storage, see [Get started with Azure File storage on Windows](storage-dotnet-how-to-use-files.md) or [How toouse Azure File storage with Linux](storage-how-to-use-files-linux.md).</span></span>

### <a name="create-a-file-share"></a><span data-ttu-id="29c8c-196">Créer un partage de fichiers</span><span class="sxs-lookup"><span data-stu-id="29c8c-196">Create a file share</span></span>
<span data-ttu-id="29c8c-197">Un partage de fichiers Azure est un partage de fichiers SMB dans Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="29c8c-197">An Azure File share is an SMB file share in Azure.</span></span> <span data-ttu-id="29c8c-198">Tous les répertoires et fichiers doivent être créés dans un partage de fichiers.</span><span class="sxs-lookup"><span data-stu-id="29c8c-198">All directories and files must be created in a file share.</span></span> <span data-ttu-id="29c8c-199">Un compte peut contenir un nombre illimité de partages, et un partage peut stocker un nombre illimité de fichiers, les limites de capacité toohello hello du compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="29c8c-199">An account can contain an unlimited number of shares, and a share can store an unlimited number of files, up toohello capacity limits of hello storage account.</span></span> <span data-ttu-id="29c8c-200">Hello exemple suivant crée un partage de fichiers nommé **monsiteweb**.</span><span class="sxs-lookup"><span data-stu-id="29c8c-200">hello following example creates a file share named **myshare**.</span></span>

```azurecli
azure storage share create myshare
```

### <a name="create-a-directory"></a><span data-ttu-id="29c8c-201">Créer un répertoire</span><span class="sxs-lookup"><span data-stu-id="29c8c-201">Create a directory</span></span>
<span data-ttu-id="29c8c-202">Un répertoire fournit une structure hiérarchique facultative pour un partage de fichiers Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="29c8c-202">A directory provides an optional hierarchical structure for an Azure file share.</span></span> <span data-ttu-id="29c8c-203">Hello exemple suivant crée un répertoire nommé **myDir** dans le partage de fichiers hello.</span><span class="sxs-lookup"><span data-stu-id="29c8c-203">hello following example creates a directory named **myDir** in hello file share.</span></span>

```azurecli
azure storage directory create myshare myDir
```

<span data-ttu-id="29c8c-204">Remarque : ce chemin d’accès au répertoire peut inclure plusieurs niveaux, *par exemple*: **a/b**.</span><span class="sxs-lookup"><span data-stu-id="29c8c-204">Note that directory path can include multiple levels, *e.g.*, **a/b**.</span></span> <span data-ttu-id="29c8c-205">Cependant, vous devez vous assurer que tous les répertoires parents existent.</span><span class="sxs-lookup"><span data-stu-id="29c8c-205">However, you must ensure that all parent directories exist.</span></span> <span data-ttu-id="29c8c-206">Par exemple, pour le chemin d’accès **a/b**, vous devez créer le répertoire **a**, puis le répertoire **b**.</span><span class="sxs-lookup"><span data-stu-id="29c8c-206">For example, for path **a/b**, you must create directory **a** first, then create directory **b**.</span></span>

### <a name="upload-a-local-file-toodirectory"></a><span data-ttu-id="29c8c-207">Télécharger un fichier local de toodirectory</span><span class="sxs-lookup"><span data-stu-id="29c8c-207">Upload a local file toodirectory</span></span>
<span data-ttu-id="29c8c-208">exemple Hello télécharge un fichier à partir de **~/temp/samplefile.txt** toohello **myDir** active.</span><span class="sxs-lookup"><span data-stu-id="29c8c-208">hello following example uploads a file from **~/temp/samplefile.txt** toohello **myDir** directory.</span></span> <span data-ttu-id="29c8c-209">Modifier le chemin d’accès du fichier hello pour qu’il pointe tooa de fichier valide sur votre ordinateur local :</span><span class="sxs-lookup"><span data-stu-id="29c8c-209">Edit hello file path so that it points tooa valid file on your local machine:</span></span>

```azurecli
azure storage file upload '~/temp/samplefile.txt' myshare myDir
```

<span data-ttu-id="29c8c-210">Notez qu’un fichier dans le partage de hello peut être jusqu'à to too1 taille.</span><span class="sxs-lookup"><span data-stu-id="29c8c-210">Note that a file in hello share can be up too1 TB in size.</span></span>

### <a name="list-hello-files-in-hello-share-root-or-directory"></a><span data-ttu-id="29c8c-211">Liste des fichiers hello dans la racine du partage hello ou un répertoire</span><span class="sxs-lookup"><span data-stu-id="29c8c-211">List hello files in hello share root or directory</span></span>
<span data-ttu-id="29c8c-212">Vous pouvez répertorier les fichiers de hello et sous-répertoires d’une racine de partage ou un répertoire à l’aide de hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="29c8c-212">You can list hello files and subdirectories in a share root or a directory using hello following command:</span></span>

```azurecli
azure storage file list myshare myDir
```

<span data-ttu-id="29c8c-213">Notez que ce nom de répertoire hello est facultatif pour l’opération de liste de hello.</span><span class="sxs-lookup"><span data-stu-id="29c8c-213">Note that hello directory name is optional for hello listing operation.</span></span> <span data-ttu-id="29c8c-214">Si omis, la commande hello répertorie contenu hello du répertoire racine de hello du partage de hello.</span><span class="sxs-lookup"><span data-stu-id="29c8c-214">If omitted, hello command lists hello contents of hello root directory of hello share.</span></span>

### <a name="copy-files"></a><span data-ttu-id="29c8c-215">Copie des fichiers</span><span class="sxs-lookup"><span data-stu-id="29c8c-215">Copy files</span></span>
<span data-ttu-id="29c8c-216">Depuis la version 0.9.8 de CLI d’Azure, vous pouvez copier un fichier de tooanother, un objet blob tooa de fichier ou un objet blob tooa fichier.</span><span class="sxs-lookup"><span data-stu-id="29c8c-216">Beginning with version 0.9.8 of Azure CLI, you can copy a file tooanother file, a file tooa blob, or a blob tooa file.</span></span> <span data-ttu-id="29c8c-217">Ci-dessous, nous allons montrer comment tooperform ces copier opérations à l’aide des commandes CLI.</span><span class="sxs-lookup"><span data-stu-id="29c8c-217">Below we demonstrate how tooperform these copy operations using CLI commands.</span></span> <span data-ttu-id="29c8c-218">toocopy un répertoire toohello fichier :</span><span class="sxs-lookup"><span data-stu-id="29c8c-218">toocopy a file toohello new directory:</span></span>

```azurecli
azure storage file copy start --source-share srcshare --source-path srcdir/hello.txt --dest-share destshare
    --dest-path destdir/hellocopy.txt --connection-string $srcConnectionString --dest-connection-string $destConnectionString
```

<span data-ttu-id="29c8c-219">toocopy un répertoire de fichiers blob tooa :</span><span class="sxs-lookup"><span data-stu-id="29c8c-219">toocopy a blob tooa file directory:</span></span>

```azurecli
azure storage file copy start --source-container srcctn --source-blob hello2.txt --dest-share hello
    --dest-path hellodir/hello2copy.txt --connection-string $srcConnectionString --dest-connection-string $destConnectionString
```

## <a name="next-steps"></a><span data-ttu-id="29c8c-220">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="29c8c-220">Next Steps</span></span>

<span data-ttu-id="29c8c-221">Vous pouvez trouver la référence des commandes de la CLI Azure 1.0 pour travailler avec des ressources de stockage ici :</span><span class="sxs-lookup"><span data-stu-id="29c8c-221">You can find Azure CLI 1.0 command reference for working with Storage resources here:</span></span>

* [<span data-ttu-id="29c8c-222">Commandes de la CLI Azure en mode Resource Manager</span><span class="sxs-lookup"><span data-stu-id="29c8c-222">Azure CLI commands in Resource Manager mode</span></span>](../virtual-machines/azure-cli-arm-commands.md#azure-storage-commands-to-manage-your-storage-objects)
* [<span data-ttu-id="29c8c-223">Commandes de la CLI Azure en mode Azure Service Management (ASM)</span><span class="sxs-lookup"><span data-stu-id="29c8c-223">Azure CLI commands in Azure Service Management mode</span></span>](../cli-install-nodejs.md)

<span data-ttu-id="29c8c-224">Peut également voulue tootry hello [Azure CLI 2.0](storage-azure-cli.md), notre CLI de nouvelle génération écrit dans Python, pour une utilisation avec le modèle de déploiement du Gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="29c8c-224">You may also like tootry hello [Azure CLI 2.0](storage-azure-cli.md), our next-generation CLI written in Python, for use with hello Resource Manager deployment model.</span></span>

[Image1]: ./media/storage-azure-cli/azure_command.png
